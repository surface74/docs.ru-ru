---
title: <channelSettings>
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 94a4457f-f43f-458d-a47e-2d11103ee75e
ms.openlocfilehash: 9caf87bdf2029d273a9d6d7ac90b83ba72bafc7a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69945841"
---
# <a name="channelsettings"></a>\<Чаннелсеттингс >
Указывает параметры кэша канала.  
  
\<системой. > ServiceModel  
\<> поведения  
\<serviceBehaviors >  
\<> поведения  
\<sendMessageChannelCache>  
\<Чаннелсеттингс >  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="String">
      <sendMessageChannelCache allowUnsafeCaching="Boolean">
        <channelSettings idleTimeout="TimeSpan" 
                         leaseTimeout="TimeSpan" 
                         maxItemsInCache="Integer" />
      </sendMessageChannelCache>
    </behavior>
  </serviceBehaviors>
</behaviors>  
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|idleTimeout|Значение TimeSpan, указывающее максимальный интервал времени, в течение которого объект может оставаться неактивным в кэше, прежде чем будет удален.|  
|leaseTimeout|Значение TimeSpan, указывающее интервал времени, по истечении которого объект удаляется из кэша.|  
|maxItemsInCache|Целое число, указывающее максимальное количество объектов, которые могут находиться в кэше.|  
  
### <a name="child-elements"></a>Дочерние элементы  
 Нет.  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<sendMessageChannelCache >](sendmessagechannelcache.md)|Поведение службы, которое позволяет настраивать уровни совместного использования кэша, параметры кэша фабрики каналов и параметры кэша канала для рабочих процессов, которые отправляют сообщения в конечные точки службы с помощью операций отправки сообщений.|  
  
## <a name="remarks"></a>Примечания  
 Это поведение службы предназначено для рабочих процессов, отправляющих сообщения в конечные точки служб. Эти рабочие процессы обычно являются клиентскими, но также могут быть службами рабочих процессов, размещенными в <xref:System.ServiceModel.WorkflowServiceHost>.  
  
 По умолчанию в рабочем процессе, размещенном в <xref:System.ServiceModel.WorkflowServiceHost>, кэш, используемый действиями обмена сообщениями <xref:System.ServiceModel.Activities.Send>, совместно используется всеми экземплярами рабочих процессов в <xref:System.ServiceModel.WorkflowServiceHost> (кэширование уровня узла). Для клиентского рабочего процесса, не размещенного в <xref:System.ServiceModel.WorkflowServiceHost>, кэш доступен только для экземпляра рабочего процесса (кэширование уровня экземпляра). По умолчанию кэширование отключено для всех действий отправки в рабочем процессе, в конфигурации которого определены конечные точки.  
  
 Дополнительные сведения о том, как изменить уровни общего доступа к кэшу по умолчанию и параметры кэша для фабрики каналов и кэша каналов, см. [в разделе изменение уровней общего доступа к кэшу для действий отправки](../../../wcf/feature-details/changing-the-cache-sharing-levels-for-send-activities.md).  
  
## <a name="example"></a>Пример  
 В размещенной службе рабочего процесса в файле конфигурации приложения можно указать параметры кэша фабрики и канала. Для этого необходимо создать поведение службы, содержащее параметры для кэша фабрики и канала, и добавить это поведение в службу. В следующем примере показано содержимое файла конфигурации, содержащего `MyChannelCacheBehavior` поведение службы с настройками кэша настраиваемой фабрики и канала. Это поведение службы добавляется в службу с помощью `behaviorConfiguration` атрибута.  
  
```xml  
<configuration>    
  <system.serviceModel>  
    <!-- List of other config sections here -->   
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="MyChannelCacheBehavior">  
          <sendMessageChannelCache allowUnsafeCaching ="false" >  
            <!-- Control only the host level settings -->   
            <factorySettings maxItemsInCache = "8" idleTimeout = "00:05:00" leaseTimeout="10:00:00" />  
            <channelSettings maxItemsInCache = "32" idleTimeout = "00:05:00" leaseTimeout="00:06:00" />  
          </sendMessageChannelCache>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service name="MyService" behaviorConfiguration="MyChannelCacheBehavior" />  
    </services>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.Activities.SendMessageChannelCache>
- <xref:System.ServiceModel.Activities.Configuration.SendMessageChannelCacheElement>
- <xref:System.ServiceModel.Activities.Send>
- <xref:System.ServiceModel.Activities.ChannelCacheSettings>
- [Изменение уровней совместного использования кэша для действий "Send"](../../../wcf/feature-details/changing-the-cache-sharing-levels-for-send-activities.md)
