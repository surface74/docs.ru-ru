---
title: Пример автономного веб-канала диагностики
ms.date: 03/30/2017
ms.assetid: d31c6c1f-292c-4d95-8e23-ed8565970ea5
ms.openlocfilehash: 6b83bda154a76fe10487da00359e0ceace8ce8cb
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044682"
---
# <a name="stand-alone-diagnostics-feed-sample"></a>Пример автономного веб-канала диагностики
В этом примере показано, как создать канал RSS/Atom для синдикации с помощью Windows Communication Foundation (WCF). Это базовая программа "Hello World", которая показывает основы объектной модели и способ ее настройки в службе Windows Communication Foundation (WCF).  
  
 WCF моделирует веб-каналы синдикации как операции службы, возвращающие Специальный тип <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter>данных. Экземпляры <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> могут сериализовать веб-канал в форматы RSS 2.0 и Atom 1.0. В следующем примере кода показан использованный контракт.  
  
```  
[ServiceContract(Namespace = "")]  
    interface IDiagnosticsService  
    {  
        [OperationContract]  
        //The [WebGet] attribute controls how WCF dispatches  
        //HTTP requests to service operations based on a URI suffix  
        //(the part of the request URI after the endpoint address)  
        //using the HTTP GET method. The UriTemplate specifies a relative  
        //path of 'feed', and specifies that the format is  
        //supplied using a query string.   
        [WebGet(UriTemplate="feed?format={format}")]  
        [ServiceKnownType(typeof(Atom10FeedFormatter))]  
        [ServiceKnownType(typeof(Rss20FeedFormatter))]  
        SyndicationFeedFormatter GetProcesses(string format);  
    }  
```  
  
 Операция помечена <xref:System.ServiceModel.Web.WebGetAttribute> атрибутом, который позволяет управлять тем, как WCF отправляет HTTP-запросы GET к операциям службы и задает формат отправленных сообщений. `GetProcesses`  
  
 Как и любая служба WCF, веб-каналы синдикации могут размещаться в любом управляемом приложении. Для правильной работы служб синдикации требуются особая привязка (<xref:System.ServiceModel.WebHttpBinding>) и специальное поведение конечной точки (<xref:System.ServiceModel.Description.WebHttpBehavior>). Новый класс <xref:System.ServiceModel.Web.WebServiceHost> обеспечивает удобный программный интерфейс для создания таких конечных точек без особой конфигурации.  
  
```  
WebServiceHost host = new WebServiceHost(typeof(ProcessService), new Uri("http://localhost:8000/diagnostics"));  
  
            //The WebServiceHost will automatically provide a default endpoint at the base address  
            //using the proper binding (the WebHttpBinding) and endpoint behavior (the WebHttpBehavior)  
```  
  
 В качестве альтернативного варианта можно использовать <xref:System.ServiceModel.Activation.WebServiceHostFactory> из размещенного в службах IIS файла SVC, чтобы обеспечить аналогичную функциональность (этот метод не показан в примере коде).  
  
```  
<%@ ServiceHost Language="C#|VB" Debug="true" Service="ProcessService" %>  
```  
  
 Поскольку эта служба получает запросы с использованием стандартного метода HTTP GET, для доступа к службе можно использовать любой клиент, поддерживающий RSS или ATOM. Например, можно просмотреть выходные данные этой службы, перейдя по `http://localhost:8000/diagnostics/feed/?format=atom` адресу или `http://localhost:8000/diagnostics/feed/?format=rss` в браузере, поддерживающем RSS.
  
 Вы также можете использовать [объектную модель синдикации WCF для сопоставления с Atom и RSS](../../../../docs/framework/wcf/feature-details/how-the-wcf-syndication-object-model-maps-to-atom-and-rss.md) , чтобы считывать данные из синдикации и обрабатывать их с помощью императивного кода.  
  
```  
XmlReader reader = XmlReader.Create( "http://localhost:8000/diagnostics/feed/?format=rss",  
new XmlReaderSettings()  
{  
//MaxCharactersInDocument can be used to control the maximum amount of data   
//read from the reader and helps prevent OutOfMemoryException  
MaxCharactersInDocument = 1024 * 64  
} );  
  
SyndicationFeed feed = SyndicationFeed.Load( reader );  
  
foreach (SyndicationItem i in feed.Items)  
{  
        XmlSyndicationContent content = i.Content as XmlSyndicationContent;  
        ProcessData pd = content.ReadContent<ProcessData>();  
  
        Console.WriteLine(i.Title.Text);  
        Console.WriteLine(pd.ToString());  
}  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Настройка, сборка и выполнение образца  
  
1. Убедитесь, что у вас есть право на регистрацию адресов HTTP и HTTPS на компьютере, как описано в разделе Настройка инструкций в ходе [одноразовой настройки для Windows Communication Foundation примеров](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Постройте решение.  
  
3. Запустите консольное приложение.  
  
4. Во время работы консольного приложения перейдите к `http://localhost:8000/diagnostics/feed/?format=atom` браузеру, поддерживающему RSS, или `http://localhost:8000/diagnostics/feed/?format=rss` используйте его.  
  
> [!IMPORTANT]
> Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> Если этот каталог не существует, перейдите к [примерам Windows Communication Foundation (WCF) и Windows Workflow Foundation (WF) для .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) , чтобы скачать все Windows Communication Foundation (WCF) [!INCLUDE[wf1](../../../../includes/wf1-md.md)] и примеры. Этот образец расположен в следующем каталоге.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Syndication\DiagnosticsFeed`  
  
## <a name="see-also"></a>См. также

- [Модель веб-программирования HTTP WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
- [Синдикация WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)
