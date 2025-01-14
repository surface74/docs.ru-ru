---
title: Настройка разрешений с олицетворением в SQL Server
ms.date: 03/30/2017
ms.assetid: dc733d09-1d6d-4af0-9c4b-8d24504860f1
ms.openlocfilehash: 52e11bd983a8c9155d90659834df03dea6449a8e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69961115"
---
# <a name="customizing-permissions-with-impersonation-in-sql-server"></a>Настройка разрешений с олицетворением в SQL Server
Во многих приложениях используются хранимые процедуры для получения доступа к данным, что позволяет ограничивать доступ к базовым таблицам на основе формирования цепочки владения. При этом можно предоставлять разрешения EXECUTE для хранимых процедур, отзывая или отменяя разрешения по отношению к базовым таблицам. В СУБД SQL Server если хранимая процедура и таблицы имеют одного владельца, то разрешения вызывающего объекта не проверяются. Но формирование цепочки владения перестает действовать, если объекты имеют разных владельцев, а также в случае применения динамического кода SQL.  
  
 Начиная с версии SQL Server 2005, появилась возможность использовать предложение EXECUTE AS в хранимой процедуре, если вызывающий объект не имеет разрешений на указанные в ссылках объекты базы данных. Результат действия предложения EXECUTE AS состоит в том, что контекст выполнения переключается на пользователя-посредника. Весь код, а также все вызовы вложенных хранимых процедур или триггеров выполняются в контексте безопасности пользователя-посредника. Контекст выполнения переходит к вызывающему объекту только после выполнения процедуры или при выполнении инструкции REVERT.  
  
## <a name="context-switching-with-the-execute-as-statement"></a>Переключение контекста с помощью инструкции EXECUTE AS  
 Инструкция EXECUTE AS языка Transact-SQL позволяет переключать контекст выполнения инструкции путем олицетворения другого имени входа или пользователя базы данных. Это удобный метод проверки запросов и процедур от имени другого пользователя.  
  
```  
EXECUTE AS LOGIN = 'loginName';  
EXECUTE AS USER = 'userName';  
```  
  
 В данном случае необходимо иметь разрешения IMPERSONATE по отношению к олицетворяемому имени входа или пользователю. Это разрешение подразумевается для `sysadmin` во всех базах данных, а также для членов роли `db_owner` в базах данных, которыми они владеют.  
  
## <a name="granting-permissions-with-the-execute-as-clause"></a>Предоставление разрешений с помощью предложения EXECUTE AS  
 Предложение EXECUTE AS можно использовать в заголовке определения хранимой процедуры, триггера или определяемой пользователем функции (за исключением встроенных функций с табличным значением). Применение этого предложения приводит к выполнению процедуры в контексте пользователя с указанным именем или ключевого слова, заданного в предложении EXECUTE AS. В базе данных можно создать пользователя-посредника, не сопоставленного с каким-либо именем входа, и предоставить ему только самые необходимые разрешения на объекты, доступ к которым осуществляется в процедуре. Только пользователь-посредник, указанный в предложении EXECUTE AS, должен иметь разрешения на все объекты, к которым осуществляется доступ в модуле.  
  
> [!NOTE]
> Некоторые действия, такие как TRUNCATE TABLE, не имеют предоставляемых разрешений. Включение инструкции в процедуру и определение пользователя-посредника, имеющего разрешения ALTER TABLE, позволяет распространить разрешения на усечение таблицы на те вызывающие объекты, которые имеют только разрешения EXECUTE на процедуру.  
  
 Контекст, заданный в предложении EXECUTE AS, действует только на время выполнения процедуры, включая вложенные процедуры и триггеры. Контекст снова становится контекстом вызывающего объекта после завершения выполнения или после выдачи инструкции REVERT.  
  
 Чтобы использовать предложение EXECUTE AS в процедуре, необходимо выполнить следующие три действия.  
  
1. Создать в базе данных пользователя-посредника, который не сопоставляется с именем входа. Этот шаг не является обязательным, но позволяет упростить управление разрешениями.  
  
```  
CREATE USER proxyUser WITHOUT LOGIN  
```  
  
1. Предоставить пользователю-посреднику необходимые разрешения.  
  
2. Добавить предложение EXECUTE AS в хранимую процедуру или определяемую пользователем функцию.  
  
```  
CREATE PROCEDURE [procName] WITH EXECUTE AS 'proxyUser' AS ...  
```  
  
> [!NOTE]
> Работа приложений, требующих аудита, может быть нарушена, поскольку первоначальный контекст безопасности вызывающего объекта не сохраняется. Встроенные функции, которые возвращают идентификатор текущего пользователя, такие как SESSION_USER, USER или USER_NAME, возвращают данные о пользователе, связанном с предложением EXECUTE AS, а не данные первоначального вызывающего объекта.  
  
### <a name="using-execute-as-with-revert"></a>Использование предложения EXECUTE AS с инструкцией REVERT  
 Инструкцию REVERT языка Transact-SQL можно использовать для возврата к первоначальному контексту выполнения.  
  
 Необязательное предложение с параметром NO REVERT cookie = @variableNameпозволяет переключить контекст выполнения обратно вызывающему объекту, @variableName если переменная содержит правильное значение. Это позволяет переключать контекст выполнения обратно к контексту вызывающего объекта в тех средах, где используются пулы соединений. Поскольку значение @variableName известно только вызывающему объекту инструкции EXECUTE AS, вызывающий объект может гарантировать, что контекст выполнения не может быть изменен конечным пользователем, который вызывает приложение. Соединение после закрытия возвращается в пул. Дополнительные сведения о пуле подключений в ADO.NET см. в разделе [SQL Server подключение пулов (ADO.NET)](../../../../../docs/framework/data/adonet/sql-server-connection-pooling.md).  
  
### <a name="specifying-the-execution-context"></a>Определение контекста выполнения  
 Предложение EXECUTE AS можно не только использовать для указания пользователя, но и указывать в нем любое из следующих ключевых слов.  
  
- CALLER. По умолчанию происходит выполнение с ключевым словом CALLER. Если не указан другой параметр, то процедура выполняется в контексте безопасности вызывающего объекта.  
  
- OWNER. Выполнение с ключевым словом OWNER приводит к выполнению процедуры в контексте владельца процедуры. Если процедура создана в схеме, принадлежащей `dbo` или владельцу базы данных, то процедура выполняется с неограниченными разрешениями.  
  
- SELF. Выполнение с ключевым словом SELF приводит к выполнению в контексте безопасности создателя хранимой процедуры. Это эквивалентно вызову на выполнение от имени указанного пользователя, где указанным пользователем является лицо, создавшее или изменившее процедуру.  
  
## <a name="see-also"></a>См. также

- [Защита приложений ADO.NET](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)
- [Общие сведения о безопасности SQL Server](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)
- [Сценарии безопасности приложений в SQL Server](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)
- [Управление разрешениями с использованием хранимых процедур в SQL Server](../../../../../docs/framework/data/adonet/sql/managing-permissions-with-stored-procedures-in-sql-server.md)
- [Написание безопасного динамического кода SQL в SQL Server](../../../../../docs/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server.md)
- [Подписывание хранимых процедур в SQL Server](../../../../../docs/framework/data/adonet/sql/signing-stored-procedures-in-sql-server.md)
- [Изменение данных с помощью хранимых процедур](../../../../../docs/framework/data/adonet/modifying-data-with-stored-procedures.md)
- [Центр разработчиков наборов данных и управляемых поставщиков ADO.NET](https://go.microsoft.com/fwlink/?LinkId=217917)
