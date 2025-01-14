---
title: Счетчики производительности WCF
ms.date: 03/30/2017
helpviewer_keywords:
- performance counters [WCF]
ms.assetid: f559b2bd-ed83-4988-97a1-e88f06646609
ms.openlocfilehash: 4368bd57718f52816d4efad39932bcc0959b67a2
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69951305"
---
# <a name="wcf-performance-counters"></a>Счетчики производительности WCF
Windows Communication Foundation (WCF) включает большой набор счетчиков производительности, помогающих оценить производительность приложения.  
  
## <a name="enabling-performance-counters"></a>Включение счетчиков производительности  
 Вы можете включить счетчики производительности для службы WCF с помощью файла конфигурации App. config службы WCF, как показано ниже.  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <diagnostics performanceCounters="All" />  
    </system.serviceModel>  
</configuration>  
```  
  
 Атрибут `performanceCounters` можно настроить так, чтобы включать определенный тип счетчиков производительности. Допустимы следующие значения:  
  
- Каждого Все счетчики категорий (Сервицемоделсервице, Сервицемоделендпоинт и Сервицемоделоператион) включены.  
  
- Сервицеонли: Включены только счетчики категории Сервицемоделсервице. Это значение по умолчанию.  
  
- Автоном Счетчики производительности ServiceModel * отключены.  
  
 Если вы хотите включить счетчики производительности для всех приложений WCF, можно поместить параметры конфигурации в файл Machine. config.  Дополнительные сведения о настройке достаточного объема памяти для счетчиков производительности на компьютере см. в разделе **увеличение объема памяти для счетчиков производительности** .  
  
 При использовании точек расширения WCF, таких как пользовательские вызывающие операции, следует также создавать собственные счетчики производительности. Это связано с тем, что при реализации точки расширения WCF может больше не создавать стандартные данные счетчиков производительности в пути по умолчанию. Если поддержка трассировки вручную путем создания счетчика производительности не реализована, можно не увидеть ожидаемые данные счетчика производительности.  
  
 Также счетчики производительности можно включить в коде следующим образом.  
  
```  
using System.Configuration;  
using System.ServiceModel.Configuration;  
using System.ServiceModel.Diagnostics;  
Configuration config = ConfigurationManager.OpenExeConfiguration(  
    ConfigurationUserLevel.None);  
ServiceModelSectionGroup sg = ServiceModelSectionGroup.GetSectionGroup(config);  
sg.Diagnostic.PerformanceCounters = PerformanceCounterScope.All;  
config.Save();  
```  
  
## <a name="viewing-performance-data"></a>Просмотр данных производительности  
 Чтобы просмотреть данные, полученные от счетчиков производительности, можно использовать системный монитор (Perfmon.exe), поставляемый вместе с Windows. Чтобы запустить это средство, нажмите кнопку **Пуск**и выберите пункт **выполнить** и введите `perfmon.exe` в диалоговом окне.  
  
> [!NOTE]
> Экземпляры счетчиков производительности могут быть выпущены до того, как диспетчер конечной точки обработает последние сообщения. Это может привести к тому, что данные производительности для некоторых сообщений не будут получены.  
  
## <a name="increasing-memory-size-for-performance-counters"></a>Увеличение объема памяти для счетчиков производительности  
 WCF использует отдельную общую память для категорий счетчиков производительности.  
  
 По умолчанию объем отдельной общей памяти составляет четвертую часть от объема глобальной памяти счетчиков производительности. По умолчанию объем глобальной памяти счетчиков производительности составляет 524 288 байт. Таким образом, три категории счетчиков производительности WCF по умолчанию имеют размер около 128 КБ. В зависимости от характеристик среды выполнения приложений WCF на компьютере память счетчика производительности может быть исчерпана. В этом случае WCF записывает ошибку в журнал событий приложений. В содержимом ошибки говорится, что счетчик производительности не был загружен, а запись содержит исключение «System. InvalidOperationException: Нехваткой памяти в представлении файла пользовательских счетчиков ". Если включена трассировка на уровне ошибок, этот сбой также трассируется. Если память счетчика производительности исчерпана, продолжение выполнения приложений WCF с включенными счетчиками производительности может привести к снижению производительности. Если вы обладаете правами администратора данного компьютера, настройте его так, чтобы выделить достаточно памяти для поддержки максимального количества счетчиков производительности, которые могут существовать в любое время.  
  
 В реестре можно изменить объем памяти счетчика производительности для категорий WCF. Для этого необходимо добавить новое значение DWORD с именем `FileMappingSize` в три следующих расположения и задать для него требуемое значение в байтах. Перезагрузите компьютер, чтобы эти изменения вступили в силу.  
  
- HKLM\System\CurrentControlSet\Services\ServiceModelEndpoint 4.0.0.0\Performance  
  
- HKLM\System\CurrentControlSet\Services\ServiceModelOperation 4.0.0.0\Performance  
  
- HKLM\System\CurrentControlSet\Services\ServiceModelService 4.0.0.0\Performance  
  
 Если множество объектов (например, ServiceHost) удаляется, но ожидает сборки мусора, счетчик производительности `PrivateBytes` регистрирует необычно большое количество объектов. Чтобы устранить эту проблему, можно либо добавить собственные счетчики, относящиеся к приложению, либо использовать атрибут `performanceCounters`, чтобы включить только счетчики уровня службы.  
  
## <a name="types-of-performance-counters"></a>Типы счетчиков производительности  
 Для счетчиков производительности применяются три разных уровня: Служба, конечная точка и операция.  
  
 Можно использовать инструментарий WMI, чтобы получить имя экземпляра счетчика производительности. Например, примененная к объекту директива  
  
- Имя экземпляра счетчика службы можно получить с помощью свойства "Каунтеринстанценаме" экземпляра [службы](../../../../../docs/framework/wcf/diagnostics/wmi/service.md) WMI.  
  
- Имя экземпляра счетчика конечной точки можно получить с помощью свойства "Каунтеринстанценаме" экземпляра [конечной точки](../../../../../docs/framework/wcf/diagnostics/wmi/endpoint.md) WMI.  
  
- Имя экземпляра счетчика операции можно получить с помощью метода "Жетоператионкаунтеринстанценаме" экземпляра [конечной точки](../../../../../docs/framework/wcf/diagnostics/wmi/endpoint.md) WMI.  
  
 Дополнительные сведения об инструментарии WMI см. в разделе [использование инструментарий управления Windows (WMI) для диагностики](../../../../../docs/framework/wcf/diagnostics/wmi/index.md).  
  
### <a name="service-performance-counters"></a>Счетчики производительности службы  
 Счетчики производительности службы измеряют поведение службы в целом, их можно использовать для диагностики производительности всей службы. Их можно просмотреть с помощью системного монитора, выбрав объект производительности `ServiceModelService 4.0.0.0`. Экземпляры именуются по следующей схеме:  
  
```  
ServiceName@ServiceBaseAddress  
```  
  
 Счетчик в области действия службы агрегируется из счетчика в коллекции конечных точек.  
  
 Значение счетчиков производительности для создания экземпляра службы увеличивается при создании нового InstanceContext. Обратите внимание, что новый InstanceContext создается даже при получении неактивирующего сообщения (с существующей службой) или при подключении к экземпляру из одного сеанса, завершении сеанса и последующем повторном подключении из другого сеанса.  
  
### <a name="endpoint-performance-counters"></a>Счетчики производительности конечных точек  
 Счетчики производительности конечных точек позволяют просматривать данные о том, как именно конечная точка принимает сообщения. Их можно просмотреть с помощью системного монитора, выбрав объект производительности `ServiceModelEndpoint 4.0.0.0`. Экземпляры именуются по следующей схеме:  
  
```  
(ServiceName).(ContractName)@(endpoint listener address)  
```  
  
 Данные аналогичны данным, собираемым для отдельных операций, но агрегируются только на конечной точке.  
  
 Счетчик в области действия конечной точки агрегируется из счетчиков в коллекции операций.  
  
> [!NOTE]
> Если две конечные точки имеют идентичные имена контрактов и адреса, они сопоставляются с одним и тем же экземпляром счетчика.  
  
### <a name="operation-performance-counters"></a>Счетчики производительности операций  
 Счетчики производительности операций можно просмотреть с помощью системного монитора, выбрав объект производительности `ServiceModelOperation 4.0.0.0`. Каждая операция содержит отдельный экземпляр. Следовательно, если указанный контракт имеет 10 операций, 10 экземпляров счетчика операций связаны с этим контрактом. Экземпляры объекта именуются по следующей схеме:  
  
```  
(ServiceName).(ContractName).(OperationName)@(first endpoint listener address)  
```  
  
 Этот счетчик позволяет измерить, как используется вызов и насколько успешно выполняется операция.  
  
 Если счетчики видимы в нескольких областях, данные, полученные из более высокой области, агрегируются с данными, полученными из более низких областей. Например, `Calls` в конечной точке представляет сумму всех вызовов операций в конечной точке. `Calls` в службе представляет сумму все вызовов всех конечных точек в службе.  
  
> [!NOTE]
> При наличии одинаковых имен операций в контракте можно получить только экземпляры одного счетчика для обоих операций.  
  
## <a name="programming-the-wcf-performance-counters"></a>Программирование счетчиков производительности WCF  
 Несколько файлов устанавливаются в папку установки пакета SDK, что позволяет программно получить доступ к счетчикам производительности WCF. Ниже приводится список этих файлов.  
  
- _ServiceModelEndpointPerfCounters.vrg  
  
- _ServiceModelOperationPerfCounters.vrg  
  
- _ServiceModelServicePerfCounters.vrg  
  
- _SMSvcHostPerfCounters.vrg  
  
- _TransactionBridgePerfCounters.vrg  
  
 Дополнительные сведения о программном доступе к счетчикам см. в разделе [Архитектура программирования счетчика производительности](https://go.microsoft.com/fwlink/?LinkId=95179).  
  
## <a name="see-also"></a>См. также

- [Администрирование и диагностика](../../../../../docs/framework/wcf/diagnostics/index.md)
