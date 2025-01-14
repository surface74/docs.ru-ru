---
title: Очереди в WCF
ms.date: 03/30/2017
ms.assetid: e98d76ba-1acf-42cd-b137-0f8214661112
ms.openlocfilehash: 27c92b0f728b909de16a059485a38ff7fb0fb765
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69913393"
---
# <a name="queuing-in-wcf"></a>Очереди в WCF
В этом разделе описывается использование обмена данными в очереди в Windows Communication Foundation (WCF).  
  
## <a name="queues-as-a-wcf-transport-binding"></a>Очереди в качестве привязки транспорта WCF  
 В WCF контракты указывают, что происходит при обмене. Контракты представляют собой обмен сообщениями, связанными с бизнес-требованиями или конкретными приложениями. Механизм, с помощью которого осуществляется обмен сообщениями, задается в привязках. Привязки в WCF инкапсулируют сведения об обмене сообщениями. Они предоставляют доступ к элементам конфигурации, с помощью которых пользователи могут управлять различными аспектами транспорта или протокола, которые представляются привязками. Очередь в WCF рассматривается как любая другая привязка транспорта, что является существенным преимуществом для многих приложений очереди. В наше время многие приложения с использованием очередей разрабатываются не так, как другие распределенные приложения на базе удаленного вызова процедур, что затрудняет их понимание и обслуживание. При использовании WCF стиль написания распределенного приложения во многом одинаков, что упрощает отслеживание и обслуживание. Более того, отделение механизма обмена данными от бизнес-логики упрощает настройку транспорта или внесение изменений в него, не затрагивая код, относящийся к предметной области. На следующем рисунке показана структура службы и клиента WCF, которые используют MSMQ в качестве транспорта.  
  
 ![Диаграмма приложений в очереди](../../../../docs/framework/wcf/feature-details/media/distributed-queue-figure.jpg "Схема распределенной очереди")  
  
 Как видно из этого рисунка, клиент и служба должны определять только семантику приложения, т. е. контракт и реализацию. Служба настраивает поддерживающую очереди привязку с использованием нужных параметров. Клиент использует [средство служебной программы метаданных ServiceModel (Svcutil. exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) для создания клиента WCF для службы и создания файла конфигурации, описывающего привязки, которые следует использовать для отправки сообщений в службу. Таким же, чтобы отправить сообщение в очереди, клиент создает экземпляр клиента WCF и вызывает для него операцию. В результате сообщение отправляется в очередь передачи, а затем передается в целевую очередь. Все сложные механизмы взаимодействия с использованием очередей оказываются скрытыми от приложения, которое отправляет и получает сообщения.  
  
 Предупреждения о привязке в очереди в WCF включают:  
  
- Все операции службы должны быть односторонними, так как привязка, поставленная в очередь по умолчанию в WCF, не поддерживает дуплексную связь с помощью очередей. Образец двусторонней связи (двустороннее[взаимодействие](../../../../docs/framework/wcf/samples/two-way-communication.md)) иллюстрирует использование 2 1-Way контрактов для реализации дуплексной связи с помощью очередей.  
  
- Для создания клиента WCF с помощью обмена метаданными требуется дополнительная конечная точка HTTP в службе, чтобы ее можно было запрашивать непосредственно для создания клиента WCF и получения сведений о привязке для соответствующей настройки связи в очереди.  
  
- На основе привязки, поставленной в очередь, требуется дополнительные настройки за пределами WCF. Например, <xref:System.ServiceModel.NetMsmqBinding> класс, поставляемый с WCF, требует настройки привязок, а также минимальной настройки очереди сообщений (MSMQ).  
  
 В следующих разделах описываются конкретные привязки в очереди, поставляемые с WCF, которые основаны на MSMQ.  
  
### <a name="msmq"></a>MSMQ  
 Транспорт в очереди в WCF использует MSMQ для связи с очередями.  
  
 MSMQ поставляется как дополнительный компонент Windows и выполняется как служба NT. MSMQ помещает передаваемые сообщения в очередь передачи и доставляет их в целевую очередь. Диспетчеры очередей MSMQ реализуют надежный протокол передачи сообщений, благодаря которому сообщения не могут быть потеряны при передаче. Этот протокол может быть собственным или основанным на SOAP, например как протокол SRMP.  
  
 В MSMQ, очереди могут быть транзакционными и нетранзакционными. Транзакционная очередь позволяет перехватывать и доставлять сообщение в транзакции, а затем продолжительное время хранить его в очереди. Сообщения, отправляемые в транзакционную очередь, передаются только один раз в заданном порядке. С помощью нетранзакционных очередей можно передавать, как неустойчивые, так и устойчивые сообщения. Сообщение, переданное в нетранзакционную очередь, не содержит каких-либо механизмов подтверждения надежной передачи, поэтому такое сообщение может быть потеряно.  
  
 Кроме того, очереди MSMQ можно защищать с помощью удостоверений Windows, зарегистрированных в службе каталогов Active Directory. При установке MSMQ можно установить интеграцию с Active Directory, для чего компьютер должен входить в домен Windows.  
  
 Дополнительные сведения об MSMQ см. в разделе [Установка очереди сообщений (MSMQ)](../../../../docs/framework/wcf/samples/installing-message-queuing-msmq.md).  
  
### <a name="netmsmqbinding"></a>NetMsmqBinding  
 NetMsmqBinding > — это привязка, поставленная в очередь. WCF предоставляет две конечные точки WCF для взаимодействия с помощью MSMQ. [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md) Поэтому привязка предоставляет свойства, имеющие отношение к MSMQ. Тем не менее в `NetMsmqBinding` доступны не все функции и свойства MSMQ. Компактная привязка `NetMsmqBinding` содержит оптимальный набор возможностей, которого должно быть достаточно для большинства пользователей.  
  
 В `NetMsmqBinding` в виде свойств привязок объявлены базовые принципы работы с очередями, рассмотренные выше. Эти свойства, в свою очередь, определяют, каким образом сообщения должны передаваться и отправляться с использованием MSMQ. Описание категорий свойств содержится в приведенных ниже разделах. Дополнительные сведения см. в разделе Основные разделы, в которых описаны конкретные свойства более полностью.  
  
#### <a name="exactlyonce-and-durable-properties"></a>Свойства ExactlyOnce и Durable  
 От значений свойств `ExactlyOnce` и `Durable` зависит то, каким образом сообщения передаются между очередями.  
  
- `ExactlyOnce`: Если задано `true` значение (по умолчанию), канал в очереди гарантирует, что сообщение, если оно доставлено, не повторяется. Кроме того, он контролирует, чтобы сообщение не было потеряно. Если доставить сообщение не удается или срок жизни сообщения истекает до его доставки, это сообщение, а также причина сбоя при его доставке записываются в очередь недоставленных сообщений. Если свойство имеет значение `false`, канал очереди пытается передать сообщение. В этом случае можно (необязательно) выбрать очередь недоставленных сообщений.  
  
- `Durable:` если имеет значение `true` (по умолчанию), канал очереди проверяет, что MSMQ сохраняет сообщение на диск на продолжительное время. Таким образом, если службу MSMQ необходимо остановить и перезапустить, сообщения на диске передаются в целевую очередь или в службу. Если свойство имеет значение `false`, сообщения сохраняются во временном хранилище и теряются в случае остановки и перезапуска службы MSMQ.  
  
 Для реализации надежной передачи в режиме `ExactlyOnce` служба MSMQ требует, чтобы очередь была транзакционной. Кроме того, служба MSMQ требует чтения транзакции из транзакционной очереди. Поэтому при использовании привязки `NetMsmqBinding` следует помнить, что для отправки и получения сообщения требуется транзакция, если свойство `ExactlyOnce` имеет значение `true`. Аналогично служба MSMQ требует, чтобы очередь была нетранзакционной с гарантией наилучшего из возможного, как например в случаях, когда свойство `ExactlyOnce` равняется `false` или при обмене временными сообщениями. Таким образом, если свойство `ExactlyOnce` имеет значение `false` или свойство Durable имеет значение `false`, невозможно осуществлять отправку или получение с использованием транзакций.  
  
> [!NOTE]
> Следите за тем, чтобы создавалась правильная очередь (транзакционная или нетранзакционная) в зависимости от параметров привязок. Если свойство `ExactlyOnce` имеет значение `true`, используется транзакционную очередь; в противном случае используется нетранзакционная очередь.  
  
#### <a name="dead-letter-queue-properties"></a>Свойства очереди недоставленных сообщений  
 Очередь недоставленных сообщений служит для хранения сообщений, которые не удалось доставить. Пользователь может написать дополнительные операции по чтению сообщений из очереди недоставленных сообщений.  
  
 Многие системы организации очереди реализуют общесистемную очередь недоставленных сообщений. Служба MSMQ имеет две общесистемные очереди недоставленных сообщений: общесистемную очередь недоставленных нетранзакционных сообщений, которые не удалось доставить в нетранзакционные очереди, и общесистемную очередь недоставленных транзакционных сообщений, которые не удалось доставить в транзакционные очереди.  
  
 Если несколько клиентов отправляют сообщения в различные целевые очереди с использованием одной службы MSMQ, все отправляемые клиентами сообщения попадают в одну и ту же очередь недоставленных сообщений. Это не всегда желательно. Для лучшей изоляции WCF и MSMQ в [!INCLUDE[wv](../../../../includes/wv-md.md)] предоставляют настраиваемую очередь недоставленных сообщений (или очередь недоставленных сообщений конкретного приложения), которую пользователь может указать для хранения сообщений, которые не удается доставить. В результате различные клиенты не будут использовать одну и ту же очередь недоставленных сообщений.  
  
 У привязок имеются следующие важные свойства.  
  
- `DeadLetterQueue`: Это свойство является перечислением, указывающим, запрошена ли очередь недоставленных сообщений. Кроме того, в перечислении содержится тип очереди недоставленных сообщений, если она запрошена. Значениями являются `None`, `System` и `Custom`. Дополнительные сведения о интерпретации этих свойств см. в разделе [Использование очередей недоставленных сообщений для обработки сбоев](../../../../docs/framework/wcf/feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md) при обмене сообщениями.  
  
- `CustomDeadLetterQueue`: Это свойство представляет собой адрес универсального кода ресурса (URI) очереди недоставленных сообщений, относящейся к конкретному приложению. Это необходимо, если `DeadLetterQueue`.`Custom` выбран.  
  
#### <a name="poison-message-handling-properties"></a>Свойства обработки подозрительных сообщений  
 Когда служба получает сообщение из целевой очереди в рамках транзакции, служба может по какой-либо причине не обработать это сообщение. В этом случае сообщение возвращается в очередь, чтобы быть считанными снова. Для обработки сообщений, которые часто вызывают сбои, в привязке можно настроить набор свойств обработки подозрительных сообщений. Есть четыре свойства: `ReceiveRetryCount`, `MaxRetryCycles`, `RetryCycleDelay` и `ReceiveErrorHandling`. Дополнительные сведения об этих свойствах см. в разделе [Обработка подозрительных сообщений](../../../../docs/framework/wcf/feature-details/poison-message-handling.md).  
  
#### <a name="security-properties"></a>Свойства безопасности  
 Служба MSMQ реализует собственную модель безопасности, например списки управления доступом в очереди или отправку прошедших проверку подлинности сообщений. В привязке `NetMsmqBinding` эти свойства безопасности реализованы как часть параметров безопасности транспорта. В привязке имеется два свойства для обеспечения безопасности транспорта: `MsmqAuthenticationMode` и `MsmqProtectionLevel`. Значения этих свойств зависят от настройки MSMQ. Дополнительные сведения см. в разделе [Защита сообщений с помощью безопасности транспорта](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md).  
  
 Помимо безопасности транспорта само сообщение SOAP можно также защитить с помощью механизмов защиты сообщений. Дополнительные сведения см. в разделе [Защита сообщений с помощью безопасности сообщений](../../../../docs/framework/wcf/feature-details/securing-messages-using-message-security.md).  
  
 `MsmqTransportSecurity` также реализует два свойства: `MsmqEncryptionAlgorithm` и `MsmqHashAlgorithm`. Это перечисления различных алгоритмов, позволяющее задать шифрование при передаче сообщений между очередями и хэширование сигнатур.  
  
#### <a name="other-properties"></a>Другие свойства  
 Помимо описанных выше свойства предоставляемые привязкой свойства MSMQ включают:  
  
- `UseSourceJournal`: Свойство, указывающее, что включено ведение журнала источников. Ведение журнала является возможностью MSMQ, отслеживающей сообщения, которые были успешно переданы из очереди передачи;  
  
- `UseMsmqTracing`: Свойство, указывающее, включена трассировка MSMQ. Функция трассировки MSMQ отправляет сообщение с отчетом в очередь отчетов всякий раз, когда сообщение покидает компьютер с диспетчером очереди MSMQ или приходит на него;  
  
- `QueueTransferProtocol`: Перечисление протокола, используемого для передачи сообщений из очереди в очередь. Служба MSMQ реализует собственный протокол передачи сообщений между очередями, а также протокол на базе SOAP (SRMP). Протокол SRMP используется при передаче сообщений между очередями с помощью протокола HTTP. Если сообщения между очередями передаются с помощью протокола HTTPS, используется протокол SRMP;  
  
- `UseActiveDirectory`: Логическое значение, указывающее, следует ли использовать Active Directory для разрешения адреса очереди. По умолчанию этот режим отключен. Дополнительные сведения см. в статье [конечные точки службы и адресация очередей](../../../../docs/framework/wcf/feature-details/service-endpoints-and-queue-addressing.md).  
  
### <a name="msmqintegrationbinding"></a>MsmqIntegrationBinding  
 Используется `MsmqIntegrationBinding` , если требуется, чтобы конечная точка WCF взаимодействовала с существующим приложением MSMQ, написанным C++на языках C,, com или System. Messaging API.  
  
 Привязка имеет те же свойства, что и `NetMsmqBinding`. Однако имеются следующие различия:  
  
- контракт операции `MsmqIntegrationBinding` может принимать только один параметр типа <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>, где параметр типа является типом тела;  
  
- большинство свойств собственных сообщений MSMQ доступно в <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>;  
  
- для сериализации и десериализации тела сообщения предоставляются сериализаторы, например XML и ActiveX.  
  
### <a name="sample-code"></a>Пример кода  
 Пошаговые инструкции по созданию служб WCF, использующих MSMQ, см. в следующих разделах.  
  
- [Практическое руководство. Обмен сообщениями с конечными точками WCF и приложениями очереди сообщений](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)  
  
- [Практическое руководство. Обмен сообщениями в очереди с конечными точками WCF](../../../../docs/framework/wcf/feature-details/how-to-exchange-queued-messages-with-wcf-endpoints.md)  
  
 Полный образец кода, демонстрирующий использование MSMQ в WCF, см. в следующих разделах.  
  
- [Привязка MSMQ с поддержкой транзакций](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md)  
  
- [Неустойчивое взаимодействие с использованием очереди](../../../../docs/framework/wcf/samples/volatile-queued-communication.md)  
  
- [Очереди недоставленных сообщений](../../../../docs/framework/wcf/samples/dead-letter-queues.md)  
  
- [Сеансы и очереди](../../../../docs/framework/wcf/samples/sessions-and-queues.md)  
  
- [Двусторонний обмен данными](../../../../docs/framework/wcf/samples/two-way-communication.md) 
  
- [SRMP](../../../../docs/framework/wcf/samples/srmp.md)  
  
- [Безопасность сообщений при использовании очереди сообщений](../../../../docs/framework/wcf/samples/message-security-over-message-queuing.md)  
  
## <a name="see-also"></a>См. также

- [Конечные точки служб и адресация очереди](../../../../docs/framework/wcf/feature-details/service-endpoints-and-queue-addressing.md)
- [Размещение веб-узлов в приложении, использующем очереди](../../../../docs/framework/wcf/feature-details/web-hosting-a-queued-application.md)
