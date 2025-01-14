---
title: Элемент <legacyImpersonationPolicy>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#legacyImpersonationPolicy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/legacyImpersonationPolicy
helpviewer_keywords:
- <legacyImpersonationPolicy> element
- legacyImpersonationPolicy element
ms.assetid: 6e00af10-42f3-4235-8415-1bb2db78394e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: da01d0dac2e67d6c0131a2b5965472bbd19213fe
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927319"
---
# <a name="legacyimpersonationpolicy-element"></a>\<Элемент > Легациимперсонатионполици
Указывает, что удостоверение Windows не проходит через асинхронные точки, независимо от параметров потока для контекста выполнения в текущем потоке.  
  
 \<configuration>  
\<> среды выполнения  
\<Легациимперсонатионполици >  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<legacyImpersonationPolicy    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|`enabled`|Обязательный атрибут.<br /><br /> Указывает, что <xref:System.Security.Principal.WindowsIdentity> объект не передается по асинхронным точкам, <xref:System.Threading.ExecutionContext> независимо от параметров потока в текущем потоке.|  
  
## <a name="enabled-attribute"></a>Атрибут enabled  
  
|Значение|Описание|  
|-----------|-----------------|  
|`false`|<xref:System.Security.Principal.WindowsIdentity>проходит через асинхронные точки в зависимости от <xref:System.Threading.ExecutionContext> параметров потока для текущего потока. Это значение по умолчанию.|  
|`true`|<xref:System.Security.Principal.WindowsIdentity>не перетекает через асинхронные точки, независимо от <xref:System.Threading.ExecutionContext> параметров потока в текущем потоке.|  
  
### <a name="child-elements"></a>Дочерние элементы  
 Нет.  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|`configuration`|Корневой элемент в любом файле конфигурации, используемом средой CLR и приложениями .NET Framework.|  
|`runtime`|Содержит сведения о привязке сборок и сборке мусора.|  
  
## <a name="remarks"></a>Примечания  
 В .NET Framework версиях 1,0 и 1,1, объект <xref:System.Security.Principal.WindowsIdentity> не проходит через определенные пользователем асинхронные точки. Начиная с версии .NET Framework 2,0, существует <xref:System.Threading.ExecutionContext> объект, который содержит сведения о выполняющемся в данный момент потоке и проходит через асинхронные точки в пределах домена приложения. <xref:System.Security.Principal.WindowsIdentity> Включается в этот контекст выполнения и, следовательно, проходит через асинхронные точки, что означает, что если контекст олицетворения существует, он также будет работать.  
  
 Начиная с .NET Framework 2,0, можно использовать `<legacyImpersonationPolicy>` элемент, чтобы указать, что <xref:System.Security.Principal.WindowsIdentity> не передается через асинхронные точки.  
  
> [!NOTE]
> Общеязыковая среда выполнения (CLR) осведомлена об операциях олицетворения, выполняемых только с помощью управляемого кода, а не олицетворения, выполненных за пределами управляемого кода, например посредством вызова неуправляемого кода платформой или прямых вызовов функций Win32. Только управляемые <xref:System.Security.Principal.WindowsIdentity> объекты могут передаваться по асинхронным точкам, `alwaysFlowImpersonationPolicy` если только элемент не имеет`<alwaysFlowImpersonationPolicy enabled="true"/>`значение true (). Если задать для элемента значение true, удостоверение Windows всегда проходит через асинхронные точки независимо от того, как было выполнено олицетворение. `alwaysFlowImpersonationPolicy` Дополнительные сведения о передаче неуправляемого олицетворения через асинхронные точки см. в разделе [ \<алвайсфловимперсонатионполици > Element](alwaysflowimpersonationpolicy-element.md).  
  
 Это поведение по умолчанию можно изменить двумя способами.  
  
1. В управляемом коде на основе каждого потока.  
  
     Можно <xref:System.Threading.ExecutionContext> подавить поток на основе каждого потока, изменив параметры и <xref:System.Security.SecurityContext> с помощью <xref:System.Threading.ExecutionContext.SuppressFlow%2A?displayProperty=nameWithType>метода, <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity%2A?displayProperty=nameWithType> или <xref:System.Security.SecurityContext.SuppressFlow%2A?displayProperty=nameWithType> .  
  
2. В вызове неуправляемого интерфейса размещения для загрузки среды CLR.  
  
     Если для загрузки среды CLR используется неуправляемый интерфейс размещения (вместо простого управляемого исполняемого файла), можно указать специальный флаг в вызове функции [функции CorBindToRuntimeEx](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md) . Чтобы включить режим совместимости для всего процесса, задайте `flags` для параметра [CorBindToRuntimeEx функции](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md) значение STARTUP_LEGACY_IMPERSONATION.  
  
 Дополнительные сведения см. в [ \<описании элемента алвайсфловимперсонатионполици >](alwaysflowimpersonationpolicy-element.md).  
  
## <a name="configuration-file"></a>Файл конфигурации  
 В приложении .NET Framework этот элемент можно использовать только в файле конфигурации приложения.  
  
 Для приложения ASP.NET поток олицетворения можно настроить в файле aspnet. config, который \<находится в папке Windows > \микрософт.нет\фрамеворк\вкс.КС.кскскскс.  
  
 ASP.NET по умолчанию отключает поток олицетворения в файле aspnet. config, используя следующие параметры конфигурации:  
  
``` xml
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="true"/>  
      <alwaysFlowImpersonationPolicy enabled="false"/>  
   </runtime>  
</configuration>  
```  
  
 В ASP.NET, если требуется разрешить поток олицетворения, необходимо явно использовать следующие параметры конфигурации:  
  
```xml  
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="false"/>  
      <alwaysFlowImpersonationPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="example"></a>Пример  
 В следующем примере показано, как задать устаревшее поведение, которое не пополняет удостоверение Windows в асинхронных точках.  
  
```xml  
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>См. также

- [Схема параметров среды выполнения](index.md)
- [Схема файла конфигурации](../index.md)
- [\<Элемент > Алвайсфловимперсонатионполици](alwaysflowimpersonationpolicy-element.md)
