---
title: Практическое руководство. Асинхронный вызов операций с использованием фабрики каналов
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: cc17dd47-b9ad-451c-a362-e36e0aac7ba0
ms.openlocfilehash: 3080514d06119a2f1b621cff16056ac7577c30b3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966805"
---
# <a name="how-to-call-operations-asynchronously-using-a-channel-factory"></a>Практическое руководство. Асинхронный вызов операций с использованием фабрики каналов
В этой теме описывается, каким образом клиент может асинхронно обратиться к операции службы при использовании клиентского приложения, основанного на <xref:System.ServiceModel.ChannelFactory%601>. (При вызове службы с помощью объекта <xref:System.ServiceModel.ClientBase%601?displayProperty=nameWithType> можно использовать управляемую событиями модель асинхронных вызовов. Дополнительные сведения см. в разделе [Практическое руководство. Асинхронный вызов операций службы](../../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md). Дополнительные сведения о модели асинхронного вызова на основе событий см. в разделе асинхронная модель [на основе событий (EAP)](../../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md).  
  
 Служба в этом разделе реализует интерфейс `ICalculator`. Клиент может асинхронно вызвать операции для этого интерфейса, это означает, что операции типа `Add` разделяются на два метода, `BeginAdd` и `EndAdd`, первый из них инициирует вызов, а второй извлекает результат после завершения операции. Пример, демонстрирующий асинхронную реализацию операции в службе, см. в разделе [как Реализуйте асинхронную операцию](../../../../docs/framework/wcf/how-to-implement-an-asynchronous-service-operation.md)службы. Дополнительные сведения о синхронных и асинхронных операциях см. в разделе [синхронные и асинхронные операции](../../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md).  
  
## <a name="procedure"></a>Процедура  
  
#### <a name="to-call-wcf-service-operations-asynchronously"></a>Асинхронный вызов операций службы WCF  
  
1. Запустите средство [служебной программы метаданных ServiceModel (Svcutil. exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) с `/async` параметром, как показано в следующей команде.  
  
    ```  
    svcutil /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples http://localhost:8000/servicemodelsamples/service/mex /a  
    ```  
  
     Результатом станет создание асинхронной версии клиента контракта службы для операции.  
  
2. Создайте функцию обратного вызова, вызываемую после завершения асинхронной операции, как показано в следующем примере кода.  
  
     [!code-csharp[C_How_To_CF_Async#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/client.cs#2)]
     [!code-vb[C_How_To_CF_Async#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/client.vb#2)]  
  
3. Чтобы асинхронно обратиться к операции службы, создайте клиент и вызовите `Begin[Operation]` (например `BeginAdd`) и задайте функцию обратного вызова, как показано в следующем примере кода.  
  
     [!code-csharp[C_How_To_CF_Async#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/client.cs#3)]
     [!code-vb[C_How_To_CF_Async#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/client.vb#3)]  
  
     При выполнении функции обратного вызова клиент вызывает `End<operation>` (например `EndAdd`), чтобы извлечь результат.  
  
## <a name="example"></a>Пример  
 Служба, используемая с клиентским кодом, который применяется в предыдущей процедуре, реализует интерфейс `ICalculator`, как показано в следующем коде. На стороне `Add` службы операции и `Subtract` в контракте вызываются синхронно с помощью Windows Communication Foundation (WCF) времени выполнения, хотя предыдущие этапы клиента вызываются на клиенте асинхронно. Операции `Multiply` и `Divide` используются для асинхронного вызова службы на стороне службы, даже если клиент вызывает их синхронно. В этом примере свойству <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> присваивается значение `true`. Этот параметр свойства в сочетании с реализацией асинхронного шаблона .NET Framework сообщает времени выполнения о необходимости асинхронного вызова операции.  
  
 [!code-csharp[C_How_To_CF_Async#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/service.cs#4)]
 [!code-vb[C_How_To_CF_Async#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/service.vb#4)]  
