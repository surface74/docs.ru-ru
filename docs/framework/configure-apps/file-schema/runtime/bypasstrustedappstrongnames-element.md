---
title: Элемент <bypassTrustedAppStrongNames>
ms.date: 03/30/2017
helpviewer_keywords:
- strong-name bypass feature
- bypassTrustedAppStrongNames element
- strong-named assemblies, loading into trusted application domains
- <bypassTrustedAppStrongNames> element
ms.assetid: 71b2ebf6-3843-41e2-ad52-ffa5cd083a40
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 92873277b4b25e4c1c5981628187078ac7cb5704
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69920885"
---
# <a name="bypasstrustedappstrongnames-element"></a>Элемент \<bypassTrustedAppStrongNames>
Указывает, следует ли обходить проверку строгих имен в сборках с полным доверием, загружаемых в полное <xref:System.AppDomain>доверие.  
  
 \<configuration>  
\<> среды выполнения  
\<bypassTrustedAppStrongNames>  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<bypassTrustedAppStrongNames    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|`enabled`|Обязательный атрибут.<br /><br /> Указывает, включена ли функция обхода, которая не позволяет проверять строгие имена для сборок с полным доверием. Если эта функция включена, строгие имена не проверяются на правильность при загрузке сборки. Значение по умолчанию — `true`.|  
  
## <a name="enabled-attribute"></a>Атрибут enabled  
  
|Значение|Описание|  
|-----------|-----------------|  
|`true`|Подписи строгого имени в сборках с полным доверием не проверяются при загрузке сборок в режиме полного доверия <xref:System.AppDomain>. Это значение по умолчанию.|  
|`false`|Подписи строгого имени в сборках с полным доверием проверяются при загрузке сборок в режиме полного доверия <xref:System.AppDomain>. Подпись строгого имени проверяется только на правильность сигнатуры; оно не сравнивается с другим строгим именем для соответствия.|  
  
### <a name="child-elements"></a>Дочерние элементы  
 Нет.  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|`configuration`|Корневой элемент в любом файле конфигурации, используемом средой CLR и приложениями .NET Framework.|  
|`runtime`|Содержит сведения о привязке сборок и сборке мусора.|  
  
## <a name="remarks"></a>Примечания  
 Функция пропуска строгих имен позволяет избежать дополнительных затрат на проверку подписи строгого имени сборок с полным доверием.  
  
 Функция обхода применима к любой сборке, подписанной со строгим именем и имеющей следующие характеристики.  
  
- Полное доверие без <xref:System.Security.Policy.StrongName> свидетельства (например, наличие `MyComputer` свидетельства зоны).  
  
- Загрузка в домен <xref:System.AppDomain> с полным доверием.  
  
- Загрузка из расположения со свойством <xref:System.AppDomainSetup.ApplicationBase%2A> домена <xref:System.AppDomain>.  
  
- Подпись осуществлена без задержки.  
  
> [!NOTE]
> Если функция обхода отключена для всех приложений на компьютере с помощью раздела реестра, этот параметр файла конфигурации не действует. Дополнительные сведения см. в разделе [Практическое руководство. Отключение функции пропуска строгих имен](../../../app-domains/how-to-disable-the-strong-name-bypass-feature.md)  
  
## <a name="example"></a>Пример  
 В следующем примере показано, как задать поведение, которое проверяет подпись строгого имени в сборках с полным доверием.  
  
```xml  
<configuration>  
   <runtime>  
      <bypassTrustedAppStrongNames enabled="false"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>См. также

- [Схема параметров среды выполнения](index.md)
- [Схема файла конфигурации](../index.md)
- [Практическое руководство. Отключение функции пропуска строгих имен](../../../app-domains/how-to-disable-the-strong-name-bypass-feature.md)
