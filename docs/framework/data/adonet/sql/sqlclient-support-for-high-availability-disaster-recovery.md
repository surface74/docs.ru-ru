---
title: Поддержка SqlClient для высокого уровня доступности, аварийного восстановления
ms.date: 03/30/2017
ms.assetid: 61e0b396-09d7-4e13-9711-7dcbcbd103a0
ms.openlocfilehash: 104fdd78ce3f4b9c18f09fc41fddebe46815d217
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69938469"
---
# <a name="sqlclient-support-for-high-availability-disaster-recovery"></a>Поддержка SqlClient для высокого уровня доступности, аварийного восстановления
В этом разделе обсуждается поддержка SqlClient (добавлена в .NET Framework 4,5) для обеспечения высокого уровня доступности, аварийного восстановления и группы доступности AlwaysOn.  Компонент группы доступности AlwaysOn был добавлен в SQL Server 2012. Дополнительные сведения о группы доступности AlwaysOn см. в разделе электронная документация на SQL Server.  
  
 Теперь можно указать прослушиватель группы доступности (высокий уровень доступности, аварийное восстановление) или экземпляр отказоустойчивого кластера SQL Server 2012 в свойстве Connection. Если во время переноса базы данных AlwaysOn к ней подключено приложение SqlClient, то изначальное подключение будет разорвано, а приложение должно создать новое подключение для продолжения работы после отработки отказа.  
  
 Если вы не подключаетесь к прослушивателю группы доступности или экземпляру отказоустойчивого кластера SQL Server 2012 и если с именем узла связано несколько IP-адресов, SqlClient перебирает все IP-адреса, связанные с записью DNS. Это может занять продолжительное время в случае, если первый IP-адрес, возвращенный сервером DNS, не привязан ни к одному из адаптеров сетевого интерфейса. При подключении к прослушивателю группы доступности или экземпляру отказоустойчивого кластера SQL Server 2012 SqlClient пытается установить подключения ко всем IP-адресам параллельно, и если попытка подключения завершается удачно, драйвер удалит все незавершенные подключения. ошибок.  
  
> [!NOTE]
> Увеличение максимального времени ожидания соединения и реализация логики повторных попыток соединения повышает вероятность успешного подключения приложения к группе доступности. Кроме того, поскольку существует вероятность разрыва соединения вследствие отработки отказа, рекомендуется реализация логики повторных попыток подключения, при которой будут выполняться повторные попытки подключения до успешного восстановления связи.  
  
 Следующие свойства соединения были добавлены в SqlClient в .NET Framework 4,5:  
  
- `ApplicationIntent`  
  
- `MultiSubnetFailover`  
  
 Можно программно изменять эти ключевые слова строки подключения с помощью следующего:  
  
1. <xref:System.Data.SqlClient.SqlConnectionStringBuilder.ApplicationIntent%2A>  
  
2. <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A>  

> [!NOTE]
> Параметр `MultiSubnetFailover` не `true` является обязательным для .NET Framework 4.6.1 или более поздних версий.
  
## <a name="connecting-with-multisubnetfailover"></a>Соединение с MultiSubnetFailover  
 Всегда указывайте `MultiSubnetFailover=True` при подключении к прослушивателю группы доступности SQL Server 2012 или экземпляру отказоустойчивого кластера SQL Server 2012. `MultiSubnetFailover`обеспечивает более быструю отработку отказа для всех групп доступности и экземпляра отказоустойчивого кластера в SQL Server 2012 и значительно сокращает время отработки отказа для топологий с одной и несколькими подсетями AlwaysOn. Во время отработки отказа в топологии с несколькими подсетями клиент будет пытаться установить соединения параллельно. Во время отработки отказа в топологии с одной подсетью клиент будет агрессивно пытаться восстановить соединение TCP.  
  
 Свойство `MultiSubnetFailover` Connection указывает, что приложение развертывается в группе доступности или экземпляре отказоустойчивого кластера SQL Server 2012, и что SqlClient попытается подключиться к базе данных на основном экземпляре SQL Server, пытаясь Подключитесь ко всем IP-адресам. Если для соединения указано `MultiSubnetFailover=True`, частота повторных попыток клиента восстановить соединение TCP превышает частоту интервалов повторной передачи TCP по умолчанию в операционной системе. Это обеспечивает более скорое восстановление подключения после переноса группы доступности AlwaysOn или экземпляра отказоустойчивого кластера AlwaysOn и применяется как к топологиям с одной подсетью, так и к топологиям с несколькими подсетями.  
  
 Дополнительные сведения о ключевых словах строки подключения SqlClient см. в разделе <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
 Указание `MultiSubnetFailover=True` при подключении к чему-либо, кроме прослушивателя группы доступности или экземпляра отказоустойчивого кластера SQL Server 2012, может отрицательно сказаться на производительности и не поддерживается.  
  
 Используйте следующие рекомендации для подключения к серверу в группе доступности или экземпляра отказоустойчивого кластера SQL Server 2012:  
  
- Использование свойства соединения `MultiSubnetFailover` повысит производительность как в топологии с одной подсетью, так и в топологии с несколькими подсетями.  
  
- Для подключения к группе доступности укажите в строке подключения в качестве сервера прослушиватель группы доступности.  
  
- Подключение к SQL Serverному экземпляру, для которого настроено более 64 IP-адресов, приведет к сбою подключения.  
  
- Поведение приложения, использующего `MultiSubnetFailover` свойство Connection, не зависит от типа проверки подлинности: Проверка подлинности SQL Server, проверка подлинности Kerberos или проверка подлинности Windows.  
  
- Для согласования времени отработки отказа и уменьшения количества попыток восстановления подключения со стороны приложения следует увеличить значение `Connect Timeout`.  
  
- Распределенные транзакции не поддерживаются.  
  
 Если не применяется маршрутизация только для чтения, подключение к адресу вторичной реплики вернет ошибку в следующих ситуациях.  
  
1. Если адрес вторичной реплики не принимает входящие соединения.  
  
2. Если приложение использует `ApplicationIntent=ReadWrite` (описано ниже) и адрес вторичной реплики настроен только для чтения.  
  
 <xref:System.Data.SqlClient.SqlDependency> не поддерживается на вторичных репликах только для чтения.  
  
 Попытка подключения вернет ошибку, если первичная реплика настроена для отклонения рабочих нагрузок и предназначена только для чтения, а строка подключения содержит `ApplicationIntent=ReadOnly`.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Переход от зеркального отображения базы данных к использованию кластеров с множеством подсетей  
 Если в строке подключения присутствуют ключевые слова <xref:System.ArgumentException> и `MultiSubnetFailover` или если используется `Failover Partner` с любым другим протоколом, кроме TCP, то попытка подключения вернет ошибку (`MultiSubnetFailover=True`). Ошибка (<xref:System.Data.SqlClient.SqlException>) также возникает, если `MultiSubnetFailover` используется, а SQL Server возвращает ответ партнера по обеспечению отработки отказа, указывающий, что он является частью пары зеркального отображения базы данных.  
  
 При обновлении приложения SqlClient, использующего зеркальное отображение базы данных, до сценария с множеством подсетей необходимо удалить свойство подключения `Failover Partner`, заменив его на `MultiSubnetFailover` со значением `True`, а в строке подключения заменить имя сервера на прослушиватель группы доступности. Если в строке подключения указано `Failover Partner` и `MultiSubnetFailover=True`, то драйвер вернет ошибку. Но если в строке подключения указано `Failover Partner` и `MultiSubnetFailover=False` (или `ApplicationIntent=ReadWrite`), то приложение будет использовать зеркальное отображение базы данных.  
  
 Драйвер вернет ошибку, если на базе данных-источнике в группе доступности используется зеркальное отображение базы данных и если указано `MultiSubnetFailover=True` в строке подключения, которая подключается к базе данных-источнику вместо прослушивателя группы доступности.  
  
## <a name="specifying-application-intent"></a>Указание цели приложения  
 Если задано `ApplicationIntent=ReadOnly`, то клиент запрашивает рабочую нагрузку на чтение при попытке соединения с базой данных в режиме AlwaysOn. Сервер принудительно включает цель в момент соединения и в момент выполнения инструкции базы данных USE, но только для баз данных в режиме AlwaysOn.  
  
 Ключевое слово `ApplicationIntent` не работает с базами данных прежних версий, доступными только для чтения.  
  
 База данных может разрешить или запретить рабочие нагрузки для чтения на целевой базе данных в режиме AlwaysOn. (Это делается с помощью `ALLOW_CONNECTIONS` предложения `PRIMARY_ROLE` инструкций Transact-SQL `SECONDARY_ROLE`и.)  
  
 Ключевое слово `ApplicationIntent` служит для включения маршрутизации только для чтения.  
  
## <a name="read-only-routing"></a>Маршрутизация только для чтения  
 Маршрутизация только для чтения способна обеспечить доступность нередактируемой реплики базы данных. Для включения маршрутизации только для чтения:  
  
1. Необходимо подключиться к прослушивателю группы доступности в режиме AlwaysOn.  
  
2. Необходимо присвоить значение `ApplicationIntent` ключевому слову `ReadOnly` строки подключения.  
  
3. Администратор базы данных должен настроить включение маршрутизации только для чтения в группе доступности.  
  
 Возможно, что не все соединения, использующие маршрутизацию только для чтения, смогут подключиться к одной и той же реплике, доступной только для чтения. Изменения в синхронизации базы данных или изменения в настройках маршрутизации на сервере могут привести к соединению клиентов с разными репликами, доступными только для чтения. Чтобы убедиться, что все запросы, доступные только для чтения, подключаются к одной и той же нередактируемой реплике, не указывайте прослушиватель группы доступности в ключевом слове `Data Source` строки подключения. Вместо этого укажите имя экземпляра, доступного только для чтения.  
  
 Подключение в сценарии с маршрутизацией только для чтения может занять больше времени, чем подключение к первичной реплике, так как в сценарии с маршрутизацией только для чтения в первую очередь осуществляется подключение к первичной реплике, затем выполняется поиск наиболее подходящей и доступной вторичной реплики. В связи с этим следует увеличить максимальное время ожидания входа в систему.  
  
## <a name="see-also"></a>См. также

- [Возможности SQL Server и ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-features-and-adonet.md)
- [Центр разработчиков наборов данных и управляемых поставщиков ADO.NET](https://go.microsoft.com/fwlink/?LinkId=217917)
