---
title: <clientCredentials>
ms.date: 03/30/2017
ms.assetid: 1e6eef0d-a34e-4d74-b0f7-f65d2181858d
ms.openlocfilehash: c3e756f49b7054d6553eb6c3f1850f0fbce14943
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69926116"
---
# <a name="clientcredentials"></a>\<> clientCredentials
Задает учетные данные, используемые для проверки подлинности клиента при подключении к службе.  
  
 \<системой. > ServiceModel  
\<> поведения  
\<endpointBehaviors >  
\<> поведения  
\<> clientCredentials  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<clientCredentials type="String"
                   supportInteractive="Boolean" >
  <clientCertificate>
  </clientCertificate>
  <digest>
  </digest>
  <isuedToken>
  </isuedToken>
  <peer>
  </peer>
  <serviceCertificate>
  </serviceCertificate>
  <windowsAuthentication>
  </windowsAuthentication>
</clientCredentials>
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|`supportInteractive`|Логическое значение, которое указывает, может ли текущий пользователь принимать участие в выборе учетных данных клиента во время выполнения. Значение по умолчанию — `true`.|  
|`type`|Строка, задающая тип данного элемента конфигурации.|  
  
### <a name="child-elements"></a>Дочерние элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<clientCertificate >](clientcertificate-of-clientcredentials-element.md)|Задает сертификат, используемый для проверки подлинности клиента при подключении к службе. Это элемент типа <xref:System.ServiceModel.Configuration.X509InitiatorCertificateClientElement>.|  
|[\<Хттпдижест >](httpdigest-element.md)|Задает хэш-код, используемый для проверки подлинности клиента при подключении к службе. Это элемент типа <xref:System.ServiceModel.Configuration.HttpDigestClientElement>.|  
|[\<issuedToken >](issuedtoken.md)|Задает тип пользовательского маркера, используемого для проверки подлинности клиента при подключении к службе маркеров безопасности (STS). Это элемент типа <xref:System.ServiceModel.Configuration.IssuedTokenClientElement>.|  
|[\<Одноранговые >](peer-of-clientcredentials-element.md)|Задает учетные данные текущего однорангового узла. Это элемент типа <xref:System.ServiceModel.Configuration.PeerCredentialElement>.|  
|[\<serviceCertificate >](servicecertificate-of-clientcredentials-element.md)|Задает сертификат, используемый при проверки подлинности службы для клиента, и предоставляет структуру для настройки параметров сертификата. Данный сертификат должен быть предоставлен вне диапазона службой клиенту. Это элемент типа <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement>.|  
|[\<> Windows](windows-of-clientcredentials-element.md)|Задает учетные данные Windows. Значением по умолчанию являются учетные данные текущего потока. Это элемент типа <xref:System.ServiceModel.Configuration.WindowsClientElement>.|  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<> поведения](behavior-of-endpointbehaviors.md)|Задает поведение конечной точки.|  
  
## <a name="remarks"></a>Примечания  
 Учетные данные клиента используются для проверки подлинности клиента при подключении к службам в случаях, когда требуется взаимная проверка подлинности. Данный раздел конфигурации также можно использовать для задания сертификатов служб для сценариев, где клиент должен обеспечить защиту сообщений, передаваемых службе, с помощью сертификатов службы.  
  
## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Description.ClientCredentials>
- [Поведения безопасности](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [Защита клиентов](../../../wcf/securing-clients.md)
