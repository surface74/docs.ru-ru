---
title: <identity>
ms.date: 03/30/2017
ms.assetid: c1d2ae56-e231-4a07-9c3f-9f13381dc0d8
ms.openlocfilehash: 262ac9be6d5ce6466cf9aff33c0c2791c0e149dd
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988381"
---
# <a name="identity"></a>\<> удостоверений
Элемент identity позволяет разработчику клиента указать во время разработки ожидаемое удостоверение службы. В процессе подтверждения между клиентом и службой инфраструктура Windows Communication Foundation (WCF) обеспечит соответствие идентификатора ожидаемой службы значениям этого элемента и, таким образом, может пройти проверку подлинности. Дополнительные сведения см. в статье [удостоверение службы и проверка](../../../wcf/feature-details/service-identity-and-authentication.md)подлинности.  
  
 \<системой. > ServiceModel  
\<> клиента  
\<> конечной точки  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<identity>
  <certificate encodedValue="String" />
  <certificateReference findValue="String"
                        isChainIncluded="Boolean"
                        storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                        storeLocation="LocalMachine/CurrentUser"
                        X509FindType="Enumeration" />
  <dns value="String" />
  <rsa value="String" />
  <servicePrincipalName value="String" />
  <userPrincipalName value="String" />
</identity>
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
 Нет.  
  
### <a name="child-elements"></a>Дочерние элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|сертификат|Задает параметры сертификата X.509. Это элемент типа <xref:System.ServiceModel.Configuration.CertificateElement>. Он содержит атрибут `encodedValue`, являющийся строкой, указывающей значение, зашифрованное с помощью этого сертификата.|  
|certificateReference|Задает параметры для проверки сертификата X.509. Это элемент типа <xref:System.ServiceModel.Configuration.CertificateReferenceElement>.|  
|dns|Задает службу DNS-сертификата X.509, используемого для проверки подлинности службы. Этот элемент содержит атрибут `value`, являющийся строкой, и содержит фактическое удостоверение.|  
|rsa|Задает значение поля RSA сертификата X.509, используемое для проверки подлинности службы для клиента. Этот элемент содержит атрибут `value`, являющийся строкой, и содержит фактическое удостоверение.|  
|servicePrincipalName|Задает удостоверение имени участника-сервера, являющегося именем участника, используемым клиентом для уникальной идентификации экземпляра службы. Этот элемент содержит атрибут `value`, являющийся строкой, и содержит фактическое имя участника. Это элемент типа <xref:System.ServiceModel.Configuration.ServicePrincipalNameElement>.|  
|userPrincipalName|Задает удостоверение имени участника-пользователя, являющегося именем входа пользователя в сеть. Имя участника-пользователя состоит из имени объекта пользователя, используемого в Active Directory, за которым следует символ (\@) и, как правило, родительский домен системы доменных имен. Например, Джефф в дереве доменов Fabrikam.com может иметь имя [jeff@fabrikam.com](mailto:jeffsmith@fabrikam.com)участника-пользователя.  Этот элемент содержит атрибут `value`, являющийся строкой, и содержит фактическое имя участника. Это элемент типа <xref:System.ServiceModel.Configuration.UserPrincipalNameElement>.|  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<custom>](custom.md)|Задает настраиваемый одноранговый распознаватель для netPeerTcpBinding.|  
|[\<> конечной точки](endpoint-element.md)|Настраивает конечные точки службы.|  
|[\<Конечная точка \<> клиента >](endpoint-of-client.md)|Настраивает конечные точки канала.|  
|[\<issuer>](issuer.md)|Задает службу маркеров безопасности для федеративной службы.|  
|[\<issuerMetadata >](issuermetadata.md)|Задает конечную точку метаданных для службы маркеров безопасности федеративной службы.|  
|[\<issuedTokenParameters>](issuedtokenparameters.md)|Задает параметры для выданного маркера в настраиваемой привязке.|  
|[\<Локалиссуер >](localissuer.md)|Задает локальную службу маркеров безопасности.|  
  
## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.Configuration.IdentityElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.EndpointAddress.Identity%2A>
- [Идентификация и проверка подлинности службы](../../../wcf/feature-details/service-identity-and-authentication.md)
- [Конеч Адреса, привязки и контракты](../../../wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)
