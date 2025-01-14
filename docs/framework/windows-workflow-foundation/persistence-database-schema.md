---
title: Схема базы данных постоянного хранения
ms.date: 03/30/2017
ms.assetid: 34f69f4c-df81-4da7-b281-a525a9397a5c
ms.openlocfilehash: 65d8b2f7a6283d65823e1a186239d398ee4a530a
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038333"
---
# <a name="persistence-database-schema"></a>Схема базы данных постоянного хранения
В этом разделе описаны открытые представления, поддерживаемые хранилищем экземпляров рабочих процессов SQL.  
  
## <a name="instances-view"></a>Представление экземпляров  
 Представление **экземпляры** содержит общие сведения обо всех экземплярах рабочих процессов в базе данных.  
  
|Имя столбца|Тип столбца|Описание|  
|-----------------|-----------------|-----------------|  
|InstanceId|UniqueIdentifier|Идентификатор экземпляра рабочего процесса.|  
|PendingTimer|DateTime|Указывает, что рабочий процесс блокирован действием Delay и будет возобновлен по истечении интервала таймера. Это значение может быть равно null, если рабочий процесс не блокирован, и ожидает срабатывания таймера.|  
|CreationTime|DateTime|Указывает, что был создан рабочий процесс.|  
|LastUpdatedTime|DateTime|Указывает время последнего сохранения рабочего процесса в базе данных.|  
|ServiceDeploymentId|BigInt|Служит внешним ключом в представлении [ServiceDeployments]. Если текущий экземпляр рабочего процесса представляет экземпляр службы, размещенной в Интернете, то этот столбец содержит значение, в противном случае значение будет равно null.|  
|SuspensionExceptionName|Nvarchar(450)|Указывает тип исключения (например, InvalidOperationException), которое вызвало приостановку рабочего процесса.|  
|SuspensionReason|Nvarchar(max)|Указывает причины приостановки выполнения экземпляра рабочего процесса. Если исключение вызвало приостановку рабочего процесса, этот столбец содержит сообщение, связанное с исключением.<br /><br /> Если экземпляр был приостановлен вручную, этот столбец содержит указанную пользователем причину приостановки экземпляра.|  
|ActiveBookmarks|Nvarchar(max)|Если экземпляр рабочего процесса бездействует, это свойство указывает, по каким закладкам блокирован экземпляр. Если экземпляр рабочего процесса не бездействует, значение этого столбца равно null.|  
|CurrentMachine|Nvarchar(128)|Указывает имя компьютера, на котором в данный момент загружен в память экземпляр рабочего процесса.|  
|LastMachine|Nvarchar(450)|Указывает последний компьютер, на котором был загружен в память экземпляр рабочего процесса.|  
|ExecutionStatus|Nvarchar(450)|Указывает текущее состояние выполнения рабочего процесса. Возможные состояния: **исполнение**, **бездействие**, **закрыто**.|  
|IsInitialized|Разряд|Указывает, инициализирован ли экземпляр рабочего процесса. Инициализированный экземпляр рабочего процесса - это экземпляр, который был материализован хотя бы один раз.|  
|IsSuspended|Разряд|Указывает, приостановлен ли экземпляр рабочего процесса.|  
|IsCompleted|Разряд|Указывает, завершено ли выполнение экземпляра рабочего процесса. **Примечание.**  IIf свойство **инстанцекомплетионактион** имеет значение **DeleteAll**, а экземпляры удаляются из представления после завершения.|  
|EncodingOption|TinyInt|Описывает способ кодирования, используемый для сериализации свойств данных.<br /><br /> -0 — без кодирования<br />-1 — GzipStream|  
|ReadWritePrimitiveDataProperties|Varbinary(max)|Содержит сериализованные свойства данных экземпляра, которые будут передаваться обратно в среду выполнения рабочих процессов при загрузке экземпляра.<br /><br /> Каждое свойство-примитив имеет собственный тип CLR, то есть для десериализации задания не требуются специальные сборки.|  
|WriteOnlyPrimitiveDataProperties|Varbinary(max)|Содержит сериализованные свойства данных экземпляра, которые не передаются обратно в среду выполнения рабочих процессов при загрузке экземпляра.<br /><br /> Каждое свойство-примитив имеет собственный тип CLR, то есть для десериализации задания не требуются специальные сборки.|  
|ReadWriteComplexDataProperties|Varbinary(max)|Содержит сериализованные свойства данных экземпляра, которые будут передаваться обратно в среду выполнения рабочих процессов при загрузке экземпляра.<br /><br /> Десериализатору требуется набор знаний для всех типов объектов, хранящихся в этом большом двоичном объекте.|  
|WriteOnlyComplexDataProperties|Varbinary(max)|Содержит сериализованные свойства данных экземпляра, которые не передаются обратно в среду выполнения рабочих процессов при загрузке экземпляра.<br /><br /> Десериализатору требуется набор знаний для всех типов объектов, хранящихся в этом большом двоичном объекте.|  
|IdentityName|Nvarchar(max)|Имя определения рабочего процесса.|  
|IdentityPackage|Nvarchar(max)|Данные о пакете, указанные при создании рабочего процесса (например, имя сборки).|  
|Построить|BigInt|Номер сборки версии рабочего процесса.|  
|Значительно|BigInt|Основной номер версии рабочего процесса.|  
|Дополнительный номер|BigInt|Дополнительный номер версии рабочего процесса.|  
|Номер редакции|BigInt|Номер редакции версии рабочего процесса.|  
  
> [!CAUTION]
> Представление **экземпляров** также содержит триггер DELETE. Пользователи с соответствующими разрешениями могут выполнять в этом представлении инструкции удаления, которые принудительно удаляют экземпляры рабочего процесса из базы данных. Рекомендуем выполнять удаление непосредственно из представления только в крайнем случае, так как удаление экземпляра не из среды выполнения рабочего процесса может привести к непредвиденным последствиям. Вместо этого используйте конечную точку управления экземпляром рабочего процесса, чтобы среда выполнения рабочего процесса завершила экземпляр. Если нужно удалить большое количество экземпляров из представления, убедитесь, что отсутствуют активные среды выполнения, которые могут работать с данными экземплярами.  
  
## <a name="servicedeployments-view"></a>Представление ServiceDeployments  
 Представление **сервицедеплойментс** содержит сведения о развертывании для всех служб рабочих процессов, размещенных в Интернете (IIS/WAS). Каждый экземпляр рабочего процесса, размещенный в Интернете, будет содержать **сервицедеплойментид** , ссылающийся на строку в этом представлении.  
  
|Имя столбца|Тип столбца|Описание|  
|-----------------|-----------------|-----------------|  
|ServiceDeploymentId|BigInt|Первичный ключ для этого представления.|  
|SiteName|Nvarchar(max)|Представляет имя сайта, содержащего службу рабочего процесса (например, **веб-сайт по умолчанию**).|  
|RelativeServicePath|Nvarchar(max)|Представляет виртуальный путь относительно узла, указывающего на службу рабочего процесса. Например.  **/APP1/PurchaseOrderService.svc**).|  
|RelativeApplicationPath|Nvarchar(max)|Представляет виртуальный путь относительно узла, который указывает на приложение, содержащее службу рабочего процесса. (например, **/APP1**).|  
|ServiceName|Nvarchar(max)|Представляет имя службы рабочего процесса. (например, **пурчасеордерсервице**).|  
|ServiceNamespace|Nvarchar(max)|Представляет пространство имен службы рабочего процесса. (например, **MyCompany**).|  
  
 Представление ServiceDeployments также содержит триггер Delete. Пользователи с соответствующими разрешениями могут выполнять инструкции удаления в этом представлении, чтобы удалить элементы ServiceDeployment из базы данных. Обратите внимание на следующее.  
  
1. удаление элементов из этого представления может быть дорогостоящей операцией, так как перед ее выполнением должна быть заблокирована вся база данных. Это необходимо, чтобы избежать ситуации, когда экземпляр рабочего процесса может ссылаться на несуществующий элемент ServiceDeployment. Выполняйте удаление из этого представления только во время простоев и в периоды технического обслуживания.  
  
2. Любая попытка удалить строку Сервицедеплоймент, на которую ссылается запись в представлении **экземпляров** , приведет к отсутствию Op. Можно удалять только строки ServiceDeployment, на которые отсутствуют ссылки.  
  
## <a name="instancepromotedproperties-view"></a>Представление InstancePromotedProperties  
 Представление **инстанцепромотедпропертиес** содержит сведения обо всех повышенных свойствах, указанных пользователем. Свойство повышенного уровня функционирует как свойство первого класса, которое пользователь может использовать в запросах для извлечения экземпляров.  Например, пользователь может добавить предложение PurchaseOrder, которое всегда хранит стоимость заказа в столбце **value1** . Это даст пользователю возможность выполнять запрос для всех заказов на покупку, стоимость которых превышает определенное значение.  
  
|Тип столбца|Тип столбца|Описание|  
|-|-|-|  
|InstanceId|UniqueIdentifier|Идентификатор экземпляра рабочего процесса|  
|EncodingOption|TinyInt|Описывает кодировку, используемую для сериализации повышенных свойств данных двоичного типа.<br /><br /> -0 — без кодирования<br />-1 — GZipStream|  
|PromotionName|Nvarchar(400)|Имя повышения, связанного с данным экземпляром. Имя PromotionName необходимо, чтобы добавить контекст к универсальным столбцам в этой строке.<br /><br /> Например, PromotionName для PurchaseOrder может указывать, что Value1 содержит стоимость заказа, Value2 содержит имя клиента, разместившего заказ, Value3 содержит адрес клиента и т. д.|  
|Value[1-32]|SqlVariant|Value[1-32] содержит значения, которые можно сохранить в столбце SqlVariant. Одно повышение не может содержать более 32 значений SqlVariant.|  
|Value[33-64]|Varbinary(max)|Value[33-64] содержит сериализованные значения. Например, Value33 может содержать изображение покупаемого товара в формате JPEG. Одно повышение не может содержать более 32 свойств двоичного типа.|  
  
 Представление InstancePromotedProperties привязано к схеме, то есть пользователи могут добавлять индексы по одному или нескольким столбцам, чтобы оптимизировать запросы к представлению.  
  
> [!NOTE]
> Для индексированного представления требуется больше памяти и увеличиваются затраты на обработку. Дополнительные сведения см. в статье [повышение производительности с помощью индексированных представлений SQL Server 2008](https://go.microsoft.com/fwlink/?LinkId=179529) .
