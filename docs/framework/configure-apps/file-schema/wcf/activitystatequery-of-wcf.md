---
title: <activityStateQuery>WCF
ms.date: 03/30/2017
ms.assetid: d6cdc04b-6f3a-4097-a623-ee4a1be3b5c4
ms.openlocfilehash: ce7505896b9c5bb605bb0f67d735cb324f4fd493
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69926902"
---
# <a name="activitystatequery-of-wcf"></a>\<Активитистатекуери > WCF

Представляет запрос, используемый для трассировки изменений жизненного цикла действий, составляющих экземпляр рабочего процесса. Например, вы можете захотеть отследить каждый раз, когда действие "отправить электронное письмо" завершается в рамках экземпляра рабочего процесса. Этот запрос необходим, чтобы участник отслеживания мог подписываться на объекты записей состояния действия. Состояния, доступные для подписки, указаны в ActivtyStates.  
  
Дополнительные сведения о запросах профиля отслеживания см. в разделе [Профили отслеживания](../../../windows-workflow-foundation/tracking-profiles.md).

\<> отслеживания > \<System. ServiceModel  
\<Профили > \<trackingProfile >  
\<> рабочего процесса  
\<Активитистатекуериес >  
\<Активитистатекуери >  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<tracking>
  <profiles>
    <trackingProfile name="Name">
      <workflow>
        <activityStateQueries>
          <activityStateQuery activityName="String">
            <arguments>
              <argument name="String" />
            </arguments>
            <states>
              <state name="String" />
            </states>
            <variables>
              <variable name="String" />
            </variables>
          </activityStateQuery>
        </activityStateQueries>
      </workflow>
    </trackingProfile>
  </profiles>
</tracking>
```  
  
## <a name="attributes-and-elements"></a>Элементы и атрибуты  

В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|activityName|Строка, указывающая имя действия, по которому будут фильтроваться экземпляры <xref:System.Activities.Tracking.ActivityStateRecord>.|  
  
### <a name="child-elements"></a>Дочерние элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<аргументы >](../windows-workflow-foundation/arguments.md)|Коллекция аргументов, связанных с этим запросом действия.|  
|[\<состояния >](../windows-workflow-foundation/states.md)|Коллекция элементов конфигурации, содержащих состояния действия, на которое установлена подписка и для которого необходимо создать запись отслеживания.|  
|[\<состояния >](../windows-workflow-foundation/states.md)|Коллекция переменных, связанных с этим запросом действия.|  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<Фаултпропагатионкуери >](../windows-workflow-foundation/faultpropagationquery.md)|Представляет список элементов конфигурации, которые используются для отслеживания запросов на отмену дочернего действия родительским действием. Этот запрос необходим, чтобы участник отслеживания подписался на объекты записей запросов на отмену.|  
  
## <a name="remarks"></a>Примечания

Уникальной возможностью ActivityStateQuery является возможность извлекать данные во время отслеживания выполнения рабочего процесса. Это обеспечивает дополнительный контекст при доступе к записям отслеживания после выполнения. Можно использовать [ \<аргументы >](../windows-workflow-foundation/arguments.md), [ \<состояния >](../windows-workflow-foundation/states.md) и [ \<состояния >](../windows-workflow-foundation/states.md) элементы, чтобы извлечь любую переменную или аргумент из любого действия в рабочем процессе. В следующем примере показан запрос состояния действия, который извлекает переменные и аргументы при выдаче записи `Closed` отслеживания действия. Переменные и аргументы могут извлекаться только с помощью активитистатерекорд, поэтому они подписываются в профиль отслеживания с помощью [ \<активитистатекуери >](../windows-workflow-foundation/activitystatequery.md).  
  
```xml  
<activityStateQuery activityName="SendEmailActivity">
  <states>
    <state name="Closed" />
  </states>
  <variables>
    <variable name="FromAddress" />
  </variables>
  <arguments>
    <argument name="Result" />
  </arguments>
</activityStateQuery>
```  
  
## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.Activities.Tracking.Configuration.ActivityStateQueryElement>
- <xref:System.Activities.Tracking.ActivityStateQuery>
- [Отслеживание и трассировка рабочих процессов](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [Профили отслеживания](../../../windows-workflow-foundation/tracking-profiles.md)
