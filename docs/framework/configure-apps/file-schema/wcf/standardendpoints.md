---
title: <standardEndpoints>
ms.date: 03/30/2017
ms.assetid: d62153d7-a6e6-462a-a784-cca61e9c2ba1
ms.openlocfilehash: f40353d36464c2e759bf2058b244cb854b19806c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69930791"
---
# <a name="standardendpoints"></a>\<Стандардендпоинтс >
Этот раздел конфигурации позволяет задать коллекцию стандартных конечных точек (многократно используемых, заранее настроенных конечных точек). Значение одного или нескольких атрибутов стандартной конечной точки, обозначающих адрес, привязку или контракт, является фиксированным. Например, в конечной точке обнаружения фиксированным является контракт. По аналогии с определением пользовательских привязок можно также использовать стандартные конечные точки для расширения конечной точки службы за счет новых свойств.  
  
 \<системой. > ServiceModel  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<system.serviceModel>
  <standardEndpoints>
  </standardEndpoints>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
 Нет.  
  
### <a name="child-elements"></a>Дочерние элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<Аннаунцементендпоинт >](announcementendpoint.md)|Определяет стандартную конечную точку с фиксированным контрактом объявления. Служба может также объявлять свою доступность путем отправки сообщения в режимах «в сети» и «не в сети» соответственно при открытии и закрытии службы. Служба Windows Communication Foundation (WCF) указывает конечные точки объявления в [ \<элементе > сервицедисковери](servicediscovery.md) и использует аннаунцементклиент для выполнения объявлений. Клиент, желающий прослушивать объявление от другой службы, фактически выступает в роли службы WCF. Поэтому необходимо настроить конечные точки объявления для этого клиента в разделе " [ \<службы >](services.md) ".|  
|[\<Дисковерендпоинт >](discoveryendpoint.md)|Определяет стандартную конечную точку с фиксированным контрактом обнаружения. При добавлении в конфигурацию службы указывает, где необходимо следить за появлением сообщений обнаружения. При добавлении в клиентскую конфигурацию указывает, куда необходимо отправлять запросы обнаружения.|  
|[\<Динамицендпоинт >](dynamicendpoint.md)|Этот элемент конфигурации определяет стандартную конечную точку, содержащую сведения, позволяющие приложению работать в качестве клиентской программы, которая может найти адрес конечной точки динамически во время выполнения.|  
|[\<Мексендпоинт >](mexendpoint.md)|Определяет стандартную конечную точку с фиксированным контрактом IMetadataExchange. Поскольку все конечные точки обмена метаданными указывают IMetadataExchange в качестве своего контракта, можно использовать эту стандартную точку вместо определения собственной точки.|  
|[\<udpAnnouncementEndpoint >](udpannouncementendpoint.md)|Определяет стандартную конечную точку, используемую службами для отправки сообщений с объявлениями по привязке UDP. Имеет фиксированный контракт и поддерживает две версии обнаружения. Кроме того, она имеет фиксированную привязку UDP и значение адреса по умолчанию, как определено в спецификациях WS-Discovery (WS-Discovery от апреля 2005 или WS-Discovery версии 1.1). Можно задать многопоточный адрес, который будет использовать для отправки и получения сообщений объявлений.|  
|[\<Удпдисковерендпоинт >](udpdiscoveryendpoint.md)|Определяет стандартную конечную точку, заранее настроенную для операций обнаружения по привязке многоадресной рассылки UDP. Эта конечная точка имеет фиксированный контракт и поддерживает две версии протокола WS-Discovery. Кроме того, она имеет фиксированную привязку UDP и значение адреса по умолчанию, как определено в спецификациях WS-Discovery (WS-Discovery от апреля 2005 или WS-Discovery версии 1.1).|  
|[\<Вебхттпендпоинт >](webhttpendpoint.md)|Определяет стандартную конечную точку с [ \<](webhttpbinding.md) фиксированной привязкой > WebHttpBinding [ \<](webhttp.md) , которая автоматически добавляет поведение > HTTP. Используйте эту конечную точку при написании службы REST.|  
|[\<Вебскриптендпоинт >](webscriptendpoint.md)|Определяет стандартную конечную точку с [ \<](webhttpbinding.md) фиксированной привязкой > WebHttpBinding [ \<](enablewebscript.md) , которая автоматически добавляет > поведение енаблевебскрипт. Используйте эту конечную точку при написании службы, вызываемой из приложения ASP.NET AJAX.|  
|[\<Воркфловконтролендпоинт >](workflowcontrolendpoint.md)|Определяет стандартную конечную точку для управления выполнением экземпляров рабочего процесса (создание, выполнение, приостановка, завершение и т. д.).|  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|\<системой. > ServiceModel|Корневой элемент всех элементов конфигурации WCF.|  
  
## <a name="see-also"></a>См. также

- [Стандартные конечные точки](../../../wcf/feature-details/standard-endpoints.md)
