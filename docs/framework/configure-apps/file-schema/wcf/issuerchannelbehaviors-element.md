---
title: Элемент <issuerChannelBehaviors>
ms.date: 03/30/2017
ms.assetid: f7378673-8e9b-45b2-98d1-cf5dccdd8c40
ms.openlocfilehash: e0e41b4f6d66cd4455c43dda7c77798553f2b58f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69929929"
---
# <a name="issuerchannelbehaviors-element"></a>\<Элемент > issuerChannelBehaviors

Содержит коллекцию поведений конечной точки клиента Windows Communication Foundation (WCF) (определенную в конфигурации) для использования при взаимодействии с указанными службами маркеров службы. Определенные поведения не могут включать в себя [ \<> элементы ClientCredentials](clientcredentials.md) .

```xml
<system.ServiceModel>
  <behaviors>
    <endpointBehaviors>
      <behavior>
        <clientCredentials>
          <issuedToken>
            <issuerChannelBehaviors>
```

## <a name="syntax"></a>Синтаксис

```xml
<issuerChannelBehaviors>
  <add behaviorConfiguration="string"
       issuerAddress="string" />
</issuerChannelBehaviors>
```

## <a name="attributes-and-elements"></a>Атрибуты и элементы

В следующих разделах описаны атрибуты, дочерние и родительские элементы.

### <a name="attributes"></a>Атрибуты

Нет.

### <a name="child-elements"></a>Дочерние элементы

|Элемент|Описание|
|-------------|-----------------|
|[\<add>](add-of-issuerchannelbehaviors.md)|Добавляет поведение в коллекцию.|

### <a name="parent-elements"></a>Родительские элементы

|Элемент|Описание|
|-------------|-----------------|
|[\<issuedToken >](issuedtoken.md)|Задает пользовательский маркер, используемый для проверки подлинности клиента при подключении к службе.|

## <a name="remarks"></a>Примечания

Этот элемент используется, когда для связи со службой необходимо любое поведение (кроме поведений, в которые включаются элементы `<clientCredentials>`). Например, если [ \<](datacontractserializer-element.md) необходимо добавить элемент поведения dataContractSerializer >.

## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.Configuration.IssuedTokenClientElement.IssuerChannelBehaviors%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenClientBehaviorsElement>
- <xref:System.ServiceModel.Configuration.IssuedTokenClientBehaviorsElementCollection>
- <xref:System.ServiceModel.Security.IssuedTokenClientCredential.IssuerChannelBehaviors%2A>
- [Идентификация и проверка подлинности службы](../../../wcf/feature-details/service-identity-and-authentication.md)
- [Поведения безопасности](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [Федерация и выданные маркеры](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [Защита служб и клиентов](../../../wcf/feature-details/securing-services-and-clients.md)
- [Защита клиентов](../../../wcf/securing-clients.md)
- [Практическое руководство. Создание федеративного клиента](../../../wcf/feature-details/how-to-create-a-federated-client.md)
- [Практическое руководство. Настройка локального издателя](../../../wcf/feature-details/how-to-configure-a-local-issuer.md)
- [Федерация и выданные маркеры](../../../wcf/feature-details/federation-and-issued-tokens.md)
