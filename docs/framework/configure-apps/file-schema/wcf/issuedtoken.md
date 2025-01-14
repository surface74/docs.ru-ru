---
title: <issuedToken>
ms.date: 03/30/2017
ms.assetid: b6eae4b7-a6cd-4e1a-b0f6-f407022550b0
ms.openlocfilehash: 68e3a0802a10b14148188a81ee24ed901caa147f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69925385"
---
# <a name="issuedtoken"></a>\<issuedToken >
Задает пользовательский маркер, используемый для проверки подлинности клиента при подключении к службе.  
  
 \<системой. > ServiceModel  
\<> поведения  
раздел endpointBehaviors  
\<> поведения  
\<> clientCredentials  
\<issuedToken >  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<issuedToken cacheIssuedTokens="Boolean"
             defaultKeyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy"
             issuedTokenRenewalThresholdPercentage = "0 to 100"
             issuerChannelBehaviors="String"
             localIssuerChannelBehaviors="String"
             maxIssuedTokenCachingTime="TimeSpan">
</issuedToken>
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|`cacheIssuedTokens`|Дополнительный логический атрибут, указывающий, выполняется ли кэширование маркеров. Значение по умолчанию — `true`.|  
|`defaultKeyEntropyMode`|Дополнительный строковый атрибут, указывающий, какие случайные значения (показатели энтропии) используются для операций «рукопожатия». Допустимы следующие значения: `ClientEntropy`, `ServerEntropy` и `CombinedEntropy`. Значение по умолчанию - `CombinedEntropy`. Это атрибут типа <xref:System.ServiceModel.Security.SecurityKeyEntropyMode>.|  
|`issuedTokenRenewalThresholdPercentage`|Дополнительный целочисленный атрибут, задающий время в процентах от срока действия (предоставляемого издателем маркера), которое может пройти до обновления маркера. Диапазон значений: 0–100. Значение по умолчанию, равное 60, указывает, что попытка возобновления предпринимается по истечении 60% времени.|  
|`issuerChannelBehaviors`|Дополнительный атрибут, определяющий поведения канала во время связи с издателем.|  
|`localIssuerChannelBehaviors`|Дополнительный атрибут, определяющий поведения канала во время связи с локальным издателем.|  
|`maxIssuedTokenCachingTime`|Дополнительный атрибут Timespan, задающий промежуток времени, в течение которого выданные маркеры сохраняются в кэше, если время не указывается издателем маркера (службой маркеров безопасности). Значение по умолчанию — "10675199.02:48:05.4775807".|  
  
### <a name="child-elements"></a>Дочерние элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<Локалиссуер >](localissuer.md)|Определяет адрес локального издателя маркера и привязку, используемую для взаимодействия с конечной точкой.|  
|[\<issuerChannelBehaviors >](issuerchannelbehaviors-element.md)|Задает поведения конечной точки, используемое при связи с локальным издателем.|  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<> clientCredentials](clientcredentials.md)|Задает учетные данные, используемые для проверки подлинности клиента при подключении к службе.|  
  
## <a name="remarks"></a>Примечания  
 Выданный маркер представляет собой пользовательские учетные данные, используемые, например, при проверке подлинности с помощью службы маркеров безопасности при федеративном доступе. По умолчанию используется маркер SAML. Дополнительные сведения см. в разделе [Федерация и выданные токены](../../../wcf/feature-details/federation-and-issued-tokens.md). и [Федерации и выданных токенов](../../../wcf/feature-details/federation-and-issued-tokens.md).  
  
 Этот раздел содержит элементы, используемые для настройки локального издателя маркеров, или поведения, используемые при работе со службой маркеров безопасности. Инструкции по настройке клиента для использования локального издателя см. в разделе [как Настройка локального издателя](../../../wcf/feature-details/how-to-configure-a-local-issuer.md).  
  
## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.Configuration.IssuedTokenClientElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.IssuedToken%2A>
- <xref:System.ServiceModel.Description.ClientCredentials.IssuedToken%2A>
- <xref:System.ServiceModel.Security.IssuedTokenClientCredential>
- [Поведения безопасности](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [Защита служб и клиентов](../../../wcf/feature-details/securing-services-and-clients.md)
- [Федерация и выданные маркеры](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [Защита клиентов](../../../wcf/securing-clients.md)
- [Практическое руководство. Создание федеративного клиента](../../../wcf/feature-details/how-to-create-a-federated-client.md)
- [Практическое руководство. Настройка локального издателя](../../../wcf/feature-details/how-to-configure-a-local-issuer.md)
- [Федерация и выданные маркеры](../../../wcf/feature-details/federation-and-issued-tokens.md)
