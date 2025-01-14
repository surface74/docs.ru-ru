---
title: Задание и обработка сбоев в контрактах и службах
ms.date: 03/30/2017
helpviewer_keywords:
- handling faults [WCF]
ms.assetid: a9696563-d404-4905-942d-1e0834c26dea
ms.openlocfilehash: de12097f018e17b11a2beac663e0b0c51c7a2a17
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038391"
---
# <a name="specifying-and-handling-faults-in-contracts-and-services"></a>Задание и обработка сбоев в контрактах и службах

Приложения Windows Communication Foundation (WCF) обрабатывают ошибки, выполнив сопоставление объектов управляемого исключения с объектами сбоя SOAP и объектами ошибок SOAP для управляемых объектов исключений. В подразделах этого раздела описывается, как разрабатывать контракты, чтобы представлять ошибки в виде пользовательских ошибок SOAP, как возвращать эти ошибки в реализации службы, и как клиенты могут перехватывать такие ошибки.

## <a name="error-handling-overview"></a>Общие сведения об обработке ошибок

Во всех управляемых приложениях обработка ошибок представлена объектами <xref:System.Exception>. В приложениях на основе SOAP, таких как приложения WCF, методы служб обмениваются сведениями об ошибках обработки с помощью сообщений о сбоях SOAP. Сообщения об ошибках SOAP являются типами сообщения, которые включаются в метаданные, связанные с работой службы, и таким образом создают контракт ошибок, который клиенты могут использовать для повышения надежности и интерактивности своей работы. Кроме того, поскольку ошибки SOAP выражаются для клиентов в XML-форме, это система типов с высокой степенью доступности, которую клиенты могут использовать на любой платформе SOAP, увеличивая уровень доступа к приложению WCF.

Поскольку приложения WCF выполняются в обоих типах систем ошибок, все управляемые сведения об исключениях, отправляемые клиенту, должны быть преобразованы из исключений в ошибки SOAP в службе, отправлены и преобразованы из ошибок SOAP в исключения ошибок в клиентах WCF. В случае дуплексных клиентов клиентские контракты могут отправлять ошибки SOAP обратно в службу. В обоих случаях можно использовать поведения исключений для службы по умолчанию или можно явно управлять тем, будут ли исключения сопоставляться с сообщениями об ошибке и как будет выполняться это сопоставление.

Можно отправлять два типа ошибок SOAP: объявленные и необъявленные. Объявленные ошибки SOAP представляют ошибки, в которых в операции имеется атрибут <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType>, указывающий пользовательский тип ошибки SOAP. Не объявлено Ошибки SOAP не указаны в контракте для операции.

Настоятельно рекомендуется, чтобы операции службы объявляли свои ошибки с помощью атрибута <xref:System.ServiceModel.FaultContractAttribute>. Это позволит формально указать все ошибки SOAP, которые клиент может получить во время обычной операции. Кроме того, чтобы свести к минимум раскрытие информации, рекомендуется возвращать в ошибке SOAP только те сведения, которые необходимо знать клиенту.

Обычно службы (и дуплексные клиенты) выполняют следующие шаги, чтобы интегрировать обработку в свои приложения.

- Сопоставление исключений и пользовательскими ошибками SOAP.

- Клиенты и службы отправляют и получают ошибки SOAP в виде исключений.

Кроме того, клиенты и службы WCF могут использовать необъявленные ошибки SOAP для отладки и могут расширять поведение при ошибке по умолчанию. В следующих разделах рассматриваются эти задачи и принципы.

## <a name="map-exceptions-to-soap-faults"></a>Сопоставление исключений с ошибками SOAP

Первым шагом в создании операции, обрабатывающей ошибки, является определение условий, при которых клиентское приложение должно быть проинформировано об ошибках. Для некоторых операций имеются ошибки, относящиеся к их функциональности. Например, операция `PurchaseOrder` может возвратить конкретную информацию клиенту, которому больше не разрешено размещать заказ на покупку. В других случаях, например в службе `Calculator`, более общая ошибка SOAP `MathFault` может описать все условия ошибки во всей службе. После определения ошибок клиентов может быть создана пользовательская ошибка SOAP. Кроме того, можно отметить, что операция возвращает данную эту ошибку при возникновении соответствующей ошибки.

Дополнительные сведения об этом этапе разработки службы или клиента см. в разделе [Определение и указание ошибок](../../../docs/framework/wcf/defining-and-specifying-faults.md).

## <a name="clients-and-services-handle-soap-faults-as-exceptions"></a>Клиенты и службы обрабатывают ошибки SOAP в виде исключений

Определение условий ошибок операций, определение пользовательских ошибок SOAP и пометка этих операций как возвращающие эти ошибки являются первыми этапами успешной обработки ошибок в приложениях WCF. Следующий шаг заключается в надлежащей реализации отправки и получения этих ошибок. Обычно службы отправляют сообщения об ошибках, чтобы информировать клиентские приложения, но дуплексные клиенты также могут отправлять службам сообщения об ошибках протокола SOAP.

Дополнительные сведения см. в разделе [Отправка и получение ошибок](../../../docs/framework/wcf/sending-and-receiving-faults.md).

## <a name="undeclared-soap-faults-and-debugging"></a>Необъявленные ошибки протокола SOAP и отладка

Объявленные ошибки протокола SOAP очень полезны для построения надежных распределенных приложений с возможностью взаимодействия. Однако в некоторых случаях для службы (или дуплексного клиента) полезно отправлять необъявленную ошибку SOAP, которая не упоминается для данной операции в языке WSDL. Например, при разработке службы могут произойти непредвиденные ситуации, в которых для отладки понадобится отправить информацию обратно клиенту. Кроме того, можно задать <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> свойство <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> или свойство `true` , чтобы позволить клиентам WCF получать сведения о внутренних исключениях операций службы. Как отправка отдельных ошибок, так и Настройка свойств поведения отладки описаны в статье [Отправка и получение ошибок](../../../docs/framework/wcf/sending-and-receiving-faults.md).

> [!IMPORTANT]
> Так как управляемые исключения могут предоставлять внутренние сведения о приложении <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> , <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> устанавливать `true` или разрешать клиентам WCF получать сведения о внутренних исключениях операций службы, включая личные идентифицируемые или другие конфиденциальные сведения.
>
> Присваивать свойству <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> или <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> значение `true` рекомендуется только в качестве временного способа отладки приложения службы. Кроме того, WSDL для метода, который возвращает такие необработанные управляемые исключения, не содержит контракт для исключения <xref:System.ServiceModel.FaultException%601> типа <xref:System.ServiceModel.ExceptionDetail>. Клиенты должны рассчитывать на возможность неизвестной ошибки SOAP (возвращается клиентам WCF как <xref:System.ServiceModel.FaultException?displayProperty=nameWithType> объекты) для правильного получения отладочной информации.

## <a name="customizing-error-handling-with-ierrorhandler"></a>Настройка обработки ошибок с помощью интерфейса IErrorHandler

Если имеются особые требования для настройки ответного сообщения клиента при возникновении исключения на уровне приложения или выполнения специальной обработки после возвращения ответного сообщения, реализуйте интерфейс <xref:System.ServiceModel.Dispatcher.IErrorHandler?displayProperty=nameWithType>.

## <a name="fault-serialization-issues"></a>Проблемы сериализации сбоя

При десериализации контракта сбоя службы WCF прежде всего пытаются сопоставить имя контракта сбоя в сообщении протокола SOAP с типом контракта сбоя. Если точное соответствие не обнаружено, просматривается список доступных контрактов сбоя в алфавитном порядке для нахождения совместимого типа. Если совместимые типы имеют два контракта сбоя (например, один является подклассом другого), при десериализации сбоя может быть использован неправильный тип. Это происходит только в случае, если в контракте сбоя не указано имя, пространство имен и действие. Во избежание данной проблемы всегда полностью определяйте контракты сбоя, указывая атрибуты имени, пространства имен и действия. Кроме того, если определено несколько родственных контрактов сбоя, производных от общего базового класса, обязательно помечайте все новые элементы атрибутом `[DataMember(IsRequired=true)]`. Дополнительные сведения об использовании атрибута `IsRequired` см. в разделе <xref:System.Runtime.Serialization.DataMemberAttribute>. В этом случае базовый класс не будет считаться совместимым типом, а сбой будет десериализован в правильный производный тип.

## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.FaultException>
- <xref:System.ServiceModel.FaultContractAttribute>
- <xref:System.ServiceModel.FaultException>
- <xref:System.Xml.Serialization.XmlSerializer>
- <xref:System.ServiceModel.XmlSerializerFormatAttribute>
- <xref:System.ServiceModel.FaultContractAttribute>
- <xref:System.ServiceModel.CommunicationException>
- <xref:System.ServiceModel.FaultContractAttribute.Action%2A>
- <xref:System.ServiceModel.FaultException.Code%2A>
- <xref:System.ServiceModel.FaultException.Reason%2A>
- <xref:System.ServiceModel.FaultCode.SubCode%2A>
- <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A>
- [Определение и указание сбоев](../../../docs/framework/wcf/defining-and-specifying-faults.md)
