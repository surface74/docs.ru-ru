---
title: Несколько конечных точек по одному ListenUri
ms.date: 03/30/2017
ms.assetid: 911ffad4-4d47-4430-b7c2-79192ce6bcbd
ms.openlocfilehash: 8e514b28d9b3719a52d420551c607c49c70738e1
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044851"
---
# <a name="multiple-endpoints-at-a-single-listenuri"></a>Несколько конечных точек по одному ListenUri
В этом образце показана служба, в которой размещается несколько конечных точек по одному адресу `ListenUri`. Этот образец основан на [Начало работы](../../../../docs/framework/wcf/samples/getting-started-sample.md) , который реализует службу калькулятора.  
  
> [!NOTE]
> Процедура настройки и инструкции по построению для данного образца приведены в конце этого раздела.  
  
 Как показано в примере с [несколькими конечными точками](../../../../docs/framework/wcf/samples/multiple-endpoints.md) , служба может размещать несколько конечных точек, каждый из которых имеет разные адреса и, возможно, также различные привязки. В этом образце показано, что можно разместить несколько конечных точек по одному адресу. Кроме того, в этом образце демонстрируются различия между двумя видами адресов конечной точки службы: `EndpointAddress` и `ListenUri`.  
  
 `EndpointAddress` является логическим адресом службы. Это адрес, по которому отправляются сообщения SOAP. `ListenUri` является физическим адресом службы. В нем содержится информация о порте и адресе, где конечная точка службы фактически прослушивает сообщения на текущем компьютере. В большинстве случаев эти адреса не должны отличаться; если `ListenUri` не указан явно, по умолчанию используется URI из адреса `EndpointAddress` конечной точки. В некоторых случаях, например при настройке маршрутизатора, который может принимать сообщения, адресованные нескольким различным службам, эти адреса полезно различать.  
  
## <a name="service"></a>Служба  
 Служба в образце имеет два контракта: `ICalculator` и `IEcho`. Кроме обычной конечной точки `IMetadataExchange` существуют три конечные точки приложения, как показано в следующем коде.  
  
```xml  
<endpoint address="urn:Stuff"  
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.ICalculator"   
        listenUri="http://localhost/servicemodelsamples/service.svc" />  
<endpoint address="urn:Stuff"  
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.IEcho"   
        listenUri="http://localhost/servicemodelsamples/service.svc" />  
<endpoint address="urn:OtherEcho"  
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.IEcho"   
        listenUri="http://localhost/servicemodelsamples/service.svc" />  
```  
  
 Все три конечные точки размещаются по одному адресу `ListenUri` и используют одну привязку (`binding`) - конечные точки, расположенные по одному адресу `ListenUri`, должны иметь одну и ту же привязку, поскольку они совместно используют один стек каналов, который прослушивает сообщения в расположении, определенном данным физическим адресом на компьютере. Адрес (`address`) каждой конечной точки является универсальным именем ресурса (URN); несмотря на то что обычно адреса представляют физические расположения, фактически, адресом может быть URI любого вида, поскольку адрес используется для сопоставления и фильтрации, как показано в данном образце.  
  
 Так как все три конечные точки `ListenUri`имеют одинаковое значение, при поступлении сообщения Windows Communication Foundation (WCF) должен выбрать конечную точку, для которой предназначено сообщение. Каждая конечная точка имеет фильтр сообщений, состоящий из двух частей: фильтр адресов и фильтр контрактов. Фильтр адресов сопоставляет значение поля `To` сообщения SOAP с адресом конечной точки службы. Например, только сообщения с адресацией `To "Urn:OtherEcho"` являются кандидатами для третьей конечной точки данной службы. Фильтр контрактов соответствует действиям, связанным с операциями конкретного контракта. Например, сообщения с действием `IEcho`. `Echo` сопоставляется с фильтрами контрактов второй и третьей конечной точки данной службы, поскольку обе эти конечные точки размещают контракт `IEcho`.  
  
 Таким образом, комбинация фильтра адресов и фильтра контрактов позволяет направлять каждое сообщение, поступающее по адресу `ListenUri` данной службы, в правильную конечную точку. Третья конечная точка отличается от других двух, поскольку она принимает сообщения, отправляемые по другому адресу из других конечных точек. Первая и вторая конечные точки отличаются друг от друга своими контрактами (действием исходящего сообщения).  
  
## <a name="client"></a>Клиент  
 Как и в случае конечных точек сервера у конечных точек клиента имеется два адреса. Логический адрес на сервере и на клиенте называется `EndpointAddress`. Однако на сервере физический адрес называется `ListenUri`, в то время как на клиенте он называется `Via`.  
  
 Аналогично серверу по умолчанию эти два адреса одинаковы. Для задания на клиенте адреса `Via`, отличающегося от адреса конечной точки, используется `ClientViaBehavior`:  
  
```csharp  
Uri via = new Uri("http://localhost/ServiceModelSamples/service.svc");  
CalculatorClient calcClient = new CalculatorClient();  
calcClient.ChannelFactory.Endpoint.Behaviors.Add(  
        new ClientViaBehavior(via));  
```  
  
 Как обычно, адрес поступает из файла конфигурации клиента, созданного с помощью средства Svcutil.exe. Адрес `Via` (который соответствует `ListenUri` службы) не отображается в метаданных службы, таким образом, эту информацию необходимо передать клиенту вне диапазона (аналогично адресу метаданных службы).  
  
 В этом образце клиент отправляет сообщения каждой из трех конечных точек приложения, чтобы показать, что он может взаимодействовать со всеми тремя конечными точками (и различать их), даже если они имеют один и тот же адрес `Via`.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Настройка, сборка и выполнение образца  
  
1. Убедитесь, что вы выполнили [однократную процедуру настройки для Windows Communication Foundation примеров](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Чтобы создать выпуск решения на языке C# или Visual Basic .NET, следуйте инструкциям в разделе [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3. Чтобы запустить пример в конфигурации с одним или несколькими компьютерами, следуйте инструкциям в разделе [выполнение примеров Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
    > [!NOTE]
    > В случае нескольких компьютеров в файле Client.cs необходимо заменить localhost именем компьютера службы.  
  
> [!IMPORTANT]
> Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> Если этот каталог не существует, перейдите к [примерам Windows Communication Foundation (WCF) и Windows Workflow Foundation (WF) для .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) , чтобы скачать все Windows Communication Foundation (WCF) [!INCLUDE[wf1](../../../../includes/wf1-md.md)] и примеры. Этот образец расположен в следующем каталоге.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\MultipleEndpointsSingleUri`  
