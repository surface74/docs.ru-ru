---
title: <serviceCertificate> элемента <clientCredentials>
ms.date: 03/30/2017
ms.assetid: e50c0ac5-f0df-4c90-b54b-fc602c1f84ea
ms.openlocfilehash: a3013d0f7efd3014892cf6400447d708809c5fcd
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69936341"
---
# <a name="servicecertificate-of-clientcredentials-element"></a>\<serviceCertificate > \<>ного элемента ClientCredentials
Задает сертификат для использования при проверке подлинности службы для клиента.  
  
 \<системой. > ServiceModel  
\<> поведения  
\<endpointBehaviors >  
\<> поведения  
\<> clientCredentials  
\<serviceCertificate >  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<serviceCertificate />
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
 Нет.  
  
### <a name="child-elements"></a>Дочерние элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<Дефаултцертификате >](defaultcertificate-element.md)|Задает сертификат X.509 для использования, когда служба или служба маркеров безопасности не предоставляет сертификат посредством протокола согласования.|  
|[\<Скопедцертификатес >](scopedcertificates-element.md)|Представляет коллекцию сертификатов X.509, предоставленную конкретными службами (в области действия) для проверки подлинности. Эта коллекция обычно используется, чтобы задать сертификаты служб для служб маркеров безопасности в федеративной инфраструктуре.|  
|[\<authentication>](authentication-of-servicecertificate-element.md)|Задает поведение проверки подлинности для сертификатов служб, используемых клиентом.|  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<> clientCredentials](clientcredentials.md)|Задает учетные данные, используемые клиентом для подтверждения своей подлинности при подключении к службе.|  
  
## <a name="remarks"></a>Примечания  
 Этот элемент конфигурации содержит параметры, используемые клиентом для проверки сертификата, представленного службой с помощью проверки подлинности SSL. Он также содержит сертификат для службы, который явно задан в клиенте для шифрования сообщений для службы с помощью безопасности сообщений.  
  
 Атрибуты `serviceCertificate` элемента идентичны атрибутам [ \<> clientcertificate](clientcertificate-of-clientcredentials-element.md).  
  
## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.ServiceCertificate%2A>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ClientCredentials.ServiceCertificate%2A>
- <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>
- [Поведения безопасности](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [Защита клиентов](../../../wcf/securing-clients.md)
- [Работа с сертификатами](../../../wcf/feature-details/working-with-certificates.md)
- [Защита служб и клиентов](../../../wcf/feature-details/securing-services-and-clients.md)
