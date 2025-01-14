---
title: Вопросы и ответы
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 252ed666-0679-4eea-b71b-2f14117ef443
ms.openlocfilehash: 714ec7bda4f6c79b789d6c3029b68a04cef1342b
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2019
ms.locfileid: "70041231"
---
# <a name="frequently-asked-questions"></a>Вопросы и ответы

В следующих разделах даны ответы на некоторые вопросы, которые могут возникнуть при реализации [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)].

Дополнительные проблемы описаны в [статье Устранение неполадок](../../../../../../docs/framework/data/adonet/sql/linq/troubleshooting.md).

## <a name="cannot-connect"></a>Не удается подключиться

В. Не удается соединиться с базой данных.

A. Убедитесь в правильности строки подключения и в том, что экземпляр SQL Server работает. Обратите внимание, что для [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] требуется включенный протокол именованных каналов. Дополнительные сведения см. [в разделе обучение по](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)пошаговым руководствам.

## <a name="changes-to-database-lost"></a>Потеряны изменения, внесенные в базу данных

В. В базу данных были внесены изменения, однако при повторном запуске приложения их там не оказалось.

A. Проверьте, что для сохранения результатов в базе данных был вызван метод <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.

## <a name="database-connection-open-how-long"></a>Соединение с базой данных: как долго сохранять открытым?

В. Как долго соединение с базой данных будет оставаться открытым?

A. Как правило, подключение остается открытым до тех пор, пока не будут использованы результаты запроса. Если планируется выделить время для обработки и кэширования всех результатов, к запросу следует применить <xref:System.Linq.Enumerable.ToList%2A>. В типичных сценариях, где каждый объект обрабатывается только один раз, потоковая модель является предпочтительной в `DataReader` и [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].

Точные сведения об использовании подключения зависят от следующих моментов.

- Состояние подключения, если <xref:System.Data.Linq.DataContext> создан с помощью объекта подключения.

- Параметры строки подключения (например, включение режима MARS). Дополнительные сведения см. в разделе [Несколько активных результирующих наборов (MARS)](../../../../../../docs/framework/data/adonet/sql/multiple-active-result-sets-mars.md).

## <a name="updating-without-querying"></a>Обновление без выполнения запросов

В. Можно ли обновить данные таблицы, не отправляя запрос в базу данных?

A. Хотя в [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] отсутствуют команды обновления на основе наборов, для обновления без выполнения запроса можно воспользоваться любым из следующих способов.

- Чтобы отправить код SQL, используйте <xref:System.Data.Linq.DataContext.ExecuteCommand%2A>.

- Создайте новый экземпляр объекта и инициализируйте все текущие значения (поля), влияющие на обновление. Затем прикрепите объект к <xref:System.Data.Linq.DataContext> с помощью <xref:System.Data.Linq.Table%601.Attach%2A> и отредактируйте поле, которое нужно изменить.

## <a name="unexpected-query-results"></a>Неожиданные результаты запроса

В. Запрос возвращает непредвиденные результаты. Как узнать, что случилось?

A. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] предусматривает несколько средств для проверки создаваемого кода SQL. Одним из наиболее важных <xref:System.Data.Linq.DataContext.Log%2A>. Дополнительные сведения см. в разделе [Поддержка отладки](../../../../../../docs/framework/data/adonet/sql/linq/debugging-support.md).

## <a name="unexpected-stored-procedure-results"></a>Неожиданные результаты хранимой процедуры

В. Имеется хранимая процедура, возвращаемое значение которой вычислено с помощью функции `MAX()`. При перетаскивании хранимой процедуры в область конструктора O/R возвращаемое значение неверно.

A. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] обеспечивает два способа возврата значений, сформированных в базе данных, с помощью хранимых процедур.

- Путем именования выходного результата.

- Путем явного указания выходного параметра.

Ниже представлен пример неверных выходных данных. Поскольку [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] не может сопоставить результаты, он всегда возвращает 0.

```sql
create procedure proc2

as

begin

select max(i) from t where name like 'hello'

end
```

Ниже представлен пример правильных выходных данных с использованием выходного параметра.

```sql
create procedure proc2

@result int OUTPUT

as

select @result = MAX(i) from t where name like 'hello'

go
```

Ниже представлен пример правильных выходных данных с именованием выходного результата.

```sql
create procedure proc2

as

begin

select nax(i) AS MaxResult from t where name like 'hello'

end
```

Дополнительные сведения см. в разделе [Настройка операций с помощью хранимых процедур](../../../../../../docs/framework/data/adonet/sql/linq/customizing-operations-by-using-stored-procedures.md).

## <a name="serialization-errors"></a>Ошибки сериализации

В. При попытке сериализации возникает следующая ошибка: «Тип 'System.Data.Linq.ChangeTracker+StandardChangeTracker'... не помечен как сериализуемый».

A. Формирование кода в [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] поддерживает сериализацию <xref:System.Runtime.Serialization.DataContractSerializer>. Оно не поддерживает <xref:System.Xml.Serialization.XmlSerializer> или <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>. Дополнительные сведения см. в разделе [Сериализация](../../../../../../docs/framework/data/adonet/sql/linq/serialization.md).

## <a name="multiple-dbml-files"></a>Несколько DBML-файлов

В. При работе с несколькими DBML-файлами, использующими общие таблицы, возникает ошибка компилятора.

A. Задайте для свойств **пространства имен контекста** и **пространства имен сущности** реляционный конструктор объектов различные значения для каждого DBML-файла. Это способ исключает конфликты имен/пространств имен.

## <a name="avoiding-explicit-setting-of-database-generated-values-on-insert-or-update"></a>Предупреждение явного задания значений, созданных базой данных, в Insert или Update

В. В базе данных имеется таблица со столбцом `DateCreated`, в качестве значения по умолчанию которой указана функция SQL `Getdate()`. При попытке вставить новую запись с помощью [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] возвращается значение `NULL`. Хотя ожидается заданное по умолчанию значение базы данных.

A. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] автоматически обрабатывает данную ситуацию для столбцов identity (автоувеличение), rowguidcol (формируемые базой данных идентификаторы GUID) и timestamp. В других случаях <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> следует задавать Свойстваи= <xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A> <xref:System.Data.Linq.Mapping.AutoSync.Always> вручную./ = `true` <xref:System.Data.Linq.Mapping.AutoSync.OnInsert> / <xref:System.Data.Linq.Mapping.AutoSync.OnUpdate>

## <a name="multiple-dataloadoptions"></a>Несколько параметров DataLoadOptions

В. Можно ли задать дополнительные параметры загрузки, не переопределяя исходные?

A. Да. Исходные параметры не переопределяются, как показано в следующем примере.

```vb
Dim dlo As New DataLoadOptions()
dlo.LoadWith(Of Order)(Function(o As Order) o.Customer)
dlo.LoadWith(Of Order)(Function(o As Order) o.OrderDetails)
```

```csharp
DataLoadOptions dlo = new DataLoadOptions();
dlo.LoadWith<Order>(o => o.Customer);
dlo.LoadWith<Order>(o => o.OrderDetails);
```

## <a name="errors-using-sql-compact-35"></a>Ошибки при использовании SQL Compact 3.5

В. При перетаскивании таблиц из базы данных SQL Server Compact 3,5 возникает ошибка.

A. Реляционный конструктор объектов не поддерживает SQL Server Compact 3,5, хотя [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] среда выполнения выполняет. В этом случае необходимо создать собственные классы сущностей и добавить соответствующие атрибуты.

## <a name="errors-in-inheritance-relationships"></a>Ошибки в связях наследования

В. Я использовал фигуру наследования панели элементов в реляционный конструктор объектов для соединения двух сущностей, но выдает ошибки.

A. Простого создания связи недостаточно. Необходимо предоставить сведения, такие как столбец дискриминатора, значение дискриминатора базового класса и значение дискриминатора производного класса.

## <a name="provider-model"></a>Модель поставщика

В. Доступна ли модель общего поставщика?

A. Такая модель отсутствует. В настоящее время [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] поддерживает только SQL Server и SQL Server Compact 3,5.

## <a name="sql-injection-attacks"></a>Атаки путем внедрения кода SQL

В. Каким образом [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] защищен от атак путем внедрения кода SQL?

A. Внедрение SQL-кода представляло серьезную угрозу для традиционных SQL-запросов, создаваемых путем объединения данных, вводимых пользователем. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] предотвращает подобное внедрение за счет использования в запросах объектов <xref:System.Data.SqlClient.SqlParameter>. Вводимые данные преобразуются в значения параметров. Этот способ исключает использование вредоносных команд из введенных данных.

## <a name="changing-read-only-flag-in-dbml-files"></a>Создание флага "Только чтение" в файлах DBML.

В. Как можно избавиться от некоторых методов задания свойств при создании объектной модели из файла DBM?

A. Выполните следующие действия.

1. В файле DBML измените свойство, присвоив флагу <xref:System.Data.Linq.ITable.IsReadOnly%2A> значение `True`.

2. Добавьте разделяемый класс. Создайте конструктор с параметрами для членов, доступных только для чтения.

3. Проверьте значение по умолчанию <xref:System.Data.Linq.Mapping.UpdateCheck> (<xref:System.Data.Linq.Mapping.UpdateCheck.Never>), чтобы определить, является ли оно правильным для приложения.

    > [!CAUTION]
    > Если вы используете реляционный конструктор объектов в Visual Studio, изменения могут быть перезаписаны.

## <a name="aptca"></a>APTCA

В. Помечена ли сборка System.Data.Linq для использования кодом с частичным доверием?

A. Да, сборка System. Data. LINQ. dll состоит из .NET Framework сборок, <xref:System.Security.AllowPartiallyTrustedCallersAttribute> помеченных атрибутом. Без этой маркировки сборки в .NET Framework предназначены для использования только полностью доверенным кодом.

Основной сценарий в [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] для разрешения частично доверенных вызывающих объектов заключается в том [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] , чтобы обеспечить доступ к сборке из веб-приложений, где конфигурация *доверия* является средней.

## <a name="mapping-data-from-multiple-tables"></a>Сопоставление данных из нескольких таблиц

В. Данные в сущность поступают из нескольких таблиц. Как их сопоставить?

A. В базе данных можно создать представление и сопоставить с ним сущность. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] создает одинаковый SQL-код для представлений и таблиц.

> [!NOTE]
> В данном сценарии использование представлений имеет ограничения. Способ работает с максимальной безопасностью, если операции, выполняемые в <xref:System.Data.Linq.Table%601>, поддерживаются базовым представлением. Операции, которые предполагается использовать, известны только вам. Например, большинство приложений доступны только для чтения, а другой немалым `Create` номер выполняет / `Update` / `Delete` операции только с помощью хранимых процедур в представлениях.

## <a name="connection-pooling"></a>Объединение подключений в пул

В. Существует ли конструкция, которая поможет в организации пула объектов <xref:System.Data.Linq.DataContext>?

A. Не пытайтесь повторно использовать экземпляры <xref:System.Data.Linq.DataContext>. Каждый <xref:System.Data.Linq.DataContext> сохраняет состояние (включая кэш идентификации) для одного определенного сеанса редактирования/запроса. Для получения новых экземпляров на основе текущего состояния базы данных используйте новый <xref:System.Data.Linq.DataContext>.

Вы по-прежнему можете использовать базовые пулы соединений ADO.NET. Дополнительные сведения см. в разделе [Пулы подключений SQL Server (ADO.NET)](../../../../../../docs/framework/data/adonet/sql-server-connection-pooling.md).

## <a name="second-datacontext-is-not-updated"></a>Не выполняется обновление второго DataContext

В. Для хранения значения в базе данных использовался один экземпляр <xref:System.Data.Linq.DataContext>. Однако второй <xref:System.Data.Linq.DataContext> в той же базе данных не отражает обновленные значения. Второй экземпляр <xref:System.Data.Linq.DataContext>, вероятно, возвращает кэшированные значения.

A. Это сделано намеренно. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] по-прежнему возвращает те же экземпляры и значения, которые отображались в первом экземпляре. При выполнении обновлений используется оптимистическая блокировка. Для проверки текущего состояния базы данных используются исходные данные, которые подтверждают неизменность ее состояния. Если состояние изменилось, возникает конфликт, который должен быть устранен приложением. Одним вариантом является сброс исходного состояния до текущего состояния базы данных и повторная попытка обновления. Дополнительные сведения см. в разделе [Практическое руководство. Управление конфликтами](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)изменений.

Кроме того, <xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A> можно задать значение «false», которое отключает кэширование и отслеживание изменений. После этого самые последние значения можно будет извлекать при каждом запросе.

## <a name="cannot-call-submitchanges-in-read-only-mode"></a>Не удается вызвать метод SubmitChanges в режиме "только чтение"

В. При попытке вызова метода <xref:System.Data.Linq.DataContext.SubmitChanges%2A> в режиме только для чтения возникает ошибка.

A. Режим только для чтения отключает для контекста возможность отслеживания изменений.

## <a name="see-also"></a>См. также

- [Ссылки](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)
- [Устранение неполадок](../../../../../../docs/framework/data/adonet/sql/linq/troubleshooting.md)
- [Безопасность в LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/security-in-linq-to-sql.md)
