---
title: <issuedTokenParameters>
ms.date: 03/30/2017
ms.assetid: 120b3f37-7331-4816-b712-d6aab39655a4
ms.openlocfilehash: 07fc2c4c52c29de1cfc9f498a6dc6b6da887b502
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69925346"
---
# <a name="issuedtokenparameters"></a>\<issuedTokenParameters >
Задает параметры маркера безопасности, выданного в федеративном сценарии безопасности.  
  
 \<> System. serviceModel  
\<привязки >  
\<customBinding >  
\<Привязка >  
\<> безопасности  
\<issuedTokenParameters >  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<issuedTokenParameters defaultMessageSecurityVersion="System.ServiceModel.MessageSecurityVersion"
                       inclusionMode="AlwaysToInitiator/AlwaysToRecipient/Never/Once"
                       keySize="Integer"
                       keyType="AsymmetricKey/BearerKey/SymmetricKey"
                       tokenType="String">
  <additionalRequestParameters />
  <claimTypeRequirements>
    <add claimType="URI"
         isOptional="Boolean" />
  </claimTypeRequirements>
  <issuer address="String"
          binding="" />
  <issuerMetadata address="String" />
</issuedTokenParameters>
```  
  
## <a name="type"></a>Тип  
 `Type`  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|defaultMessageSecurityVersion|Задает версии спецификаций безопасности (WS-Security, WS-Trust, WS-Secure Conversation и WS-Security Policy), которые должны поддерживаться привязкой. Это значение имеет тип <xref:System.ServiceModel.MessageSecurityVersion>.|  
|inclusionMode|Задает требования включения маркера. Это атрибут типа <xref:System.ServiceModel.Security.Tokens.SecurityTokenInclusionMode>.|  
|keySize|Целое число, которое задает размер ключа маркера. Значение по умолчанию — 256.|  
|keyType|Допустимое значение <xref:System.IdentityModel.Tokens.SecurityKeyType>, которое задает тип ключа. Значение по умолчанию — `SymmetricKey`.|  
|tokenType|Строка, задающая тип маркера. Значение по умолчанию - "http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAML".|  
  
### <a name="child-elements"></a>Дочерние элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<Аддитионалрекуестпараметерс >](additionalrequestparameters-element.md)|Коллекция элементов конфигурации, задающих дополнительные параметры запросов.|  
|[\<claimTypeRequirements >](claimtyperequirements-element.md)|Задает коллекцию обязательных типов утверждений.<br /><br /> В федеративном сценарии службы предъявляют требования к входящим учетным данным. Например, входящие учетные данные должны обладать определенным набором типов утверждений. Каждый элемент в этой коллекции задает типы обязательных и необязательных утверждений, которые могут появляться в федеративных учетных данных.|  
|[\<issuer>](issuer-of-issuedtokenparameters.md)|Элемент конфигурации, задающий конечную точку, выдавшую текущий маркер.|  
|[\<issuerMetadata >](issuermetadata-of-issuedtokenparameters.md)|Элемент конфигурации, задающий адрес конечной точки метаданных поставщика маркера.|  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<Секуреконверсатионбутстрап >](secureconversationbootstrap.md)|Задает значения по умолчанию, используемые для инициализации службы безопасного обмена данными.|  
|[\<> безопасности](security-of-custombinding.md)|Задает параметры безопасности для пользовательской привязки.|  
  
## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters>
- <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement>
- <xref:System.ServiceModel.Configuration.SecurityElementBase.IssuedTokenParameters%2A>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [Привязки](../../../wcf/bindings.md)
- [Расширение привязок](../../../wcf/extending/extending-bindings.md)
- [Пользовательские привязки](../../../wcf/extending/custom-bindings.md)
- [\<customBinding >](custombinding.md)
- [Практическое руководство. Создание пользовательской привязки с помощью SecurityBindingElement](../../../wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [Безопасность пользовательской привязки](../../../wcf/samples/custom-binding-security.md)
- [Идентификация и проверка подлинности службы](../../../wcf/feature-details/service-identity-and-authentication.md)
- [Федерация и выданные маркеры](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [Возможности безопасности при использовании пользовательских привязок](../../../wcf/feature-details/security-capabilities-with-custom-bindings.md)
- [Федерация и выданные маркеры](../../../wcf/feature-details/federation-and-issued-tokens.md)
