---
title: Настройка ведения журналов сообщений
ms.date: 03/30/2017
helpviewer_keywords:
- message logging [WCF]
ms.assetid: 0ff4c857-8f09-4b85-9dc0-89084706e4c9
ms.openlocfilehash: f9324370539b41d21365e0bd126c2f632ac67789
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044281"
---
# <a name="configuring-message-logging"></a>Настройка ведения журналов сообщений

В этом разделе описывается, как настроить ведение журнала сообщений для различных сценариев.

## <a name="enabling-message-logging"></a>Включение ведения журнала сообщений

Windows Communication Foundation (WCF) не регистрирует сообщения по умолчанию. Чтобы включить ведение журнала сообщений, необходимо добавить прослушиватель трассировки в источник трассировки `System.ServiceModel.MessageLogging` и задать атрибуты элемента `<messagelogging>` в файле конфигурации.

В следующем примере показано, как включить ведение журнала и указать дополнительные параметры.

```xml
<system.diagnostics>
  <sources>
    <source name="System.ServiceModel.MessageLogging">
      <listeners>
         <add name="messages"
              type="System.Diagnostics.XmlWriterTraceListener"
              initializeData="c:\logs\messages.svclog" />
        </listeners>
    </source>
  </sources>
</system.diagnostics>

<system.serviceModel>
  <diagnostics>
    <messageLogging
         logEntireMessage="true"
         logMalformedMessages="false"
         logMessagesAtServiceLevel="true"
         logMessagesAtTransportLevel="false"
         maxMessagesToLog="3000"
         maxSizeOfMessageToLog="2000"/>
  </diagnostics>
</system.serviceModel>
```

Дополнительные сведения о параметрах ведения журнала сообщений см. в разделе [Рекомендуемые параметры для трассировки и ведения журнала сообщений](../../../../docs/framework/wcf/diagnostics/tracing/recommended-settings-for-tracing-and-message-logging.md).

С помощью элемента `add` можно задать имя и тип прослушивателя, который требуется использовать. В данном примере прослушиватель с именем «messages» добавляет стандартный прослушиватель трассировки .NET Framework (`System.Diagnostics.XmlWriterTraceListener`) в качестве используемого типа. Если используется прослушиватель `System.Diagnostics.XmlWriterTraceListener`, необходимо задать расположение выходного файла и имя файла конфигурации. Для этого нужно присвоить свойству `initializeData` имя файла журнала. В противном случае система создает исключение. Кроме того, можно реализовать пользовательский прослушиватель, который выводит журналы в файл по умолчанию.

> [!NOTE]
> Поскольку для журнала сообщений требуется место на диске, необходимо ограничить число сообщений, записываемых на диск для конкретной службы. Когда достигается максимальное число сообщений, создается трассировка на уровне информации, и все операции по ведению журнала сообщений останавливаются.

Уровень ведения журнала, а также дополнительные параметры, описаны в разделе Уровень и параметры ведения журнала.

Действие атрибута `switchValue` элемента `source` распространяется только на трассировку. Если задать атрибут `switchValue` источника трассировки `System.ServiceModel.MessageLogging`, как показано ниже, это ни к чему не приведет.

```xml
<source name="System.ServiceModel.MessageLogging" switchValue="Verbose">
```

Если требуется отключить источник трассировки, следует использовать атрибуты `logMessagesAtServiceLevel`, `logMalformedMessages` и `logMessagesAtTransportLevel` элемента `messageLogging`. Все эти атрибуты должны иметь значение `false`. Для этого можно воспользоваться файлом конфигурации, приведенным в последнем примере кода, пользовательским интерфейсом редактора конфигурации или инструментарием WMI. Дополнительные сведения о средстве редактора конфигураций см. в разделе [средство редактора конфигурации (SvcConfigEditor. exe)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md). Дополнительные сведения об инструментарии WMI см. [в разделе использование инструментарий управления Windows (WMI) для диагностики](../../../../docs/framework/wcf/diagnostics/wmi/index.md).

## <a name="logging-levels-and-options"></a>Уровни и параметры ведения журнала

Для входящих сообщений регистрация в журнале осуществляется сразу после формирования сообщения, непосредственно перед попаданием сообщения в пользовательский код на уровне службы и при обнаружении неправильно сформированных сообщений.

Для исходящих сообщений регистрация в журнале осуществляется сразу после выхода сообщения из пользовательского кода и непосредственно перед отправкой сообщения по каналам связи.

WCF регистрирует сообщения на двух разных уровнях: служба и транспорт. Также регистрируются неправильно сформированные сообщения. Эти три категории журнала не зависят друг от друга и могут активироваться в конфигурации по отдельности.

Для управления уровнем ведения журнала необходимо задать атрибуты `logMessagesAtServiceLevel`, `logMalformedMessages` и `logMessagesAtTransportLevel` элемента `messageLogging`.

### <a name="service-level"></a>Уровень службы

Сообщения, регистрируемые на этом уровне, готовы к входу (при получении) в пользовательский код или выходу (при отправке) из него. Если определены фильтры, в журнал записываются только сообщения, соответствующие этим фильтрам. В противном случае в журнал записываются все сообщения на уровне службы. На этом уровне также регистрируются сообщения инфраструктуры (транзакции, сообщения одноранговых каналов и безопасности), кроме сообщений системы надежного обмена сообщениями. Для потоковых сообщений в журнал заносятся только заголовки. Защищенные сообщения регистрируются на этом уровне в расшифрованном виде.

### <a name="transport-level"></a>Уровень транспорта

Сообщения, записываемые в журнал на этом уровне, готовы к кодированию или раскодированию для передачи по каналам связи или после нее. Если определены фильтры, в журнал записываются только сообщения, соответствующие этим фильтрам. В противном случае в журнал записываются все сообщения на уровне транспорта. На этом уровне регистрируются все сообщения инфраструктуры, включая сообщения системы надежного обмена сообщениями. Для потоковых сообщений в журнал заносятся только заголовки. Защищенные сообщения регистрируются на этом уровне в зашифрованном виде, если не используется защищенный транспорт, например протокол HTTPS.

### <a name="malformed-level"></a>Уровень неправильно составленных сообщений

Неправильно сформированные сообщения — это сообщения, которые отклоняются стеком WCF на любом этапе обработки. Сообщения неправильного формата записываются в журнал в исходном виде, зашифровываются с неправильным XML и т. д. Свойство `maxSizeOfMessageToLog` определяет размер сообщения, записываемого в журнал в виде CDATA. По умолчанию свойство `maxSizeOfMessageToLog` имеет значение 256 КБ. Дополнительные сведения об этом атрибуте см. в разделе другие параметры.

### <a name="other-options"></a>Другие параметры

Помимо уровня ведения журнала можно задать следующие параметры.

- Заносить в журнал`logEntireMessage` сообщение целиком (атрибут): Это значение указывает, записывается ли в журнал все сообщение (заголовок и текст сообщения). Значением по умолчанию является `false`, означающее, что в журнал записывается только заголовок сообщения. Действие этого параметра распространяется на уровни ведения журнала службы и транспорта.

- Максимальное число сообщений в журнале`maxMessagesToLog` (атрибут): Это значение указывает максимальное количество сообщений для записи в журнал. Это значение относится ко всем сообщениям (службы, транспорта и неправильно сформированным сообщениям). После достижения этого значения создается трассировка и новые сообщения в журнал не заносятся. Значение по умолчанию — 10000.

- Максимальный размер сообщения для журнала (`maxSizeOfMessageToLog` атрибут): Это значение указывает максимальный размер сообщений для журнала в байтах. Сообщения, превышающие этот размер, в журнал не заносятся, и никакие другие действия с этими сообщениями не выполняются. Действие этого параметра распространяется на все уровни трассировки. Если включена трассировка ServiceModel, в первой точке записи в журнал (ServiceModelSend* или TransportReceive) создается трассировка порога предупреждений для уведомления пользователя. Значение по умолчанию для сообщений уровня службы и транспорта составляет 256 КБ, а для сформированных сообщений неправильного формата - 4 КБ.

  > [!CAUTION]
  > Размер сообщения, вычисляемый для сравнения со значением `maxSizeOfMessageToLog`, является размером сообщения в памяти до сериализации. Этот размер может отличаться от фактической длины строки сообщения, записываемой в журнал, и часто превышает фактический размер сообщения. Поэтому сообщение может быть не записано в журнал. Можно учесть этот факт, установив для атрибута `maxSizeOfMessageToLog` значение, на 10% превышающее ожидаемый размер сообщения. Кроме того, при внесении в журнал неправильно сформированного сообщения фактическое место на диске, занимаемое журналом сообщений, может до 5 раз превышать размер, задаваемый значением `maxSizeOfMessageToLog`.

Если в файле конфигурации не задан прослушиватель трассировки, в журнал ничего не записывается независимо от установленного уровня ведения журнала.

Параметры ведения журнала, например описанные в этом разделе атрибуты, можно изменить во время выполнения с помощью инструментария управления Windows (WMI). Это можно сделать, обратившись к экземпляру [аппдомаининфо](../../../../docs/framework/wcf/diagnostics/wmi/appdomaininfo.md) , который предоставляет эти логические свойства: `LogMessagesAtServiceLevel`, `LogMessagesAtTransportLevel`и `LogMalformedMessages`. Поэтому, если в файле конфигурации прослушиватель трассировки настроен на ведение журнала, но эти параметры имеют значение `false`, можно впоследствии изменить их значения на `true`, когда приложение будет выполняться. В результате ведение журнала будет включено во время выполнения. Аналогично, если ведение журнала было включено в файле конфигурации, его можно отключить во время выполнения с помощью инструментария WMI. Дополнительные сведения см. [в разделе использование инструментарий управления Windows (WMI) для диагностики](../../../../docs/framework/wcf/diagnostics/wmi/index.md).

Поле `source` в журнале сообщений определяет контекст, в котором регистрируется сообщение: отправка или получение сообщения с запросом, запрос-ответ или односторонний запрос, модель службы или транспортный уровень, либо сформированное сообщение неправильного формата.

Для неверно сформированных сообщений `source` значение `Malformed`равно. В противном случае поле source будет иметь следующие значения в зависимости от контекста.

Запросы и ответы

||Отправка запроса|Получение запроса|Отправка ответа|Получение ответа|
|-|------------------|---------------------|----------------|-------------------|
|Уровень модели службы|Служба<br /><br /> Уровень<br /><br /> Отправить<br /><br /> Запрос|Служба<br /><br /> Уровень<br /><br /> Получить<br /><br /> Запрос|Служба<br /><br /> Уровень<br /><br /> Отправить<br /><br /> Reply|Служба<br /><br /> Уровень<br /><br /> Получить<br /><br /> Reply|
|Уровень транспорта|Transport<br /><br /> Отправить|Transport<br /><br /> Получить|Transport<br /><br /> Отправить|Transport<br /><br /> Получить|

Односторонний запрос

||Отправка запроса|Получение запроса|
|-|------------------|---------------------|
|Уровень модели службы|Служба<br /><br /> Уровень<br /><br /> Отправить<br /><br /> Datagram|Служба<br /><br /> Уровень<br /><br /> Получить<br /><br /> Datagram|
|Уровень транспорта|Transport<br /><br /> Отправить|Transport<br /><br /> Получить|

## <a name="message-filters"></a>Фильтры сообщений

Фильтры сообщений определяются в элементе конфигурации `messageLogging` в разделе `diagnostics`. Они применяются на уровне службы и транспорта. Если в файле конфигурации определены один или несколько фильтров, в журнал записываются только сообщения, соответствующие хотя бы одному из фильтров. Если фильтры не заданы, в журнал записываются все сообщения.

Фильтры поддерживают полный синтаксис XPath и применяются в порядке, в котором они указаны в файле конфигурации. Синтаксически неверные фильтры вызывают исключения конфигурации.

Кроме того, атрибут `nodeQuota` обеспечивает механизм защиты фильтров. Он ограничивает максимальное число узлов объектной модели XPath, которые можно проверить на соответствие фильтру.

В следующем примере показано, как настроить фильтр для записи только сообщений с разделом заголовка SOAP.

```xml
<messageLogging logEntireMessage="true"
    logMalformedMessages="true"
    logMessagesAtServiceLevel="true"
    logMessagesAtTransportLevel="true"
    maxMessagesToLog="420">
    <filters>
        <add nodeQuota="10" xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
                 /soap:Envelope/soap:Header
        </add>
     </filters>
</messageLogging>
```

Фильтры невозможно применить к тексту сообщения. Фильтры, которые пытаются изменять текст сообщения, удаляются из списка фильтров. Кроме того, создается событие, указывающее на это. Например, из таблицы фильтров будет удален следующий фильтр.

```xml
<add xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">/s:Envelope/s:Body[contains(text(), "Hello")]</add>
```

## <a name="configuring-a-custom-listener"></a>Настройка пользовательского прослушивателя

Имеется возможность настроить пользовательский прослушиватель с дополнительными параметрами. Пользовательский прослушиватель может оказаться полезным для удаления из сообщений элементов с личной информацией, относящихся к конкретным приложениям, перед внесением в журнал этих сообщений. Ниже показан пример конфигурации пользовательского прослушивателя.

```xml
<system.diagnostics>
   <sources>
     <source name="System.ServiceModel.MessageLogging">
           <listeners>
             <add name="MyListener"
                    type="YourCustomListener"
                    initializeData="c:\logs\messages.svclog"
                    maxDiskSpace="1000"/>
           </listeners>
     </source>
   </sources>
</system.diagnostics>
```

Следует иметь в виду, что для атрибута `type` следует задавать определенное имя сборки данного типа.

## <a name="see-also"></a>См. также

- [\<Мессажелоггинг >](../../../../docs/framework/configure-apps/file-schema/wcf/messagelogging.md)
- [Ведение журналов сообщений](../../../../docs/framework/wcf/diagnostics/message-logging.md)
- [Рекомендуемые параметры для трассировки и ведения журналов сообщений](../../../../docs/framework/wcf/diagnostics/tracing/recommended-settings-for-tracing-and-message-logging.md)
