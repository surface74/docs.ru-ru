---
title: Общие сведения о потоках сообщений
ms.date: 03/30/2017
ms.assetid: fb0899e1-84cc-4d90-b45b-dc5a50063943
ms.openlocfilehash: cee579f272700ca37228bacecdf387d03637610a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963056"
---
# <a name="message-flow-overview"></a>Общие сведения о потоках сообщений
В распределенной системе со связанными между собой службами необходимо определять причинные взаимоотношения между службами. Понимать, какие из различных компонентов входили в путь потока запроса, необходимо для решения таких важнейших задач, как наблюдения за работоспособностью, устранение неполадок и анализ первопричин. Для поддержки трассировки в различных службах в .NET Framework 4 была добавлена поддержка следующих функций.

- Аналитическая трассировка: Высокая производительность и Детальная трассировка с низким уровнем детализации с помощью трассировки событий Windows (ETW).

- Модель сквозных действий для служб WCF/WF: Эта функция поддерживает корреляцию трассировок, созданных <xref:System.ServiceModel> пространствами имен и. <xref:System.Workflow.ComponentModel>

- Отслеживание ETW для WF: Эта функция использует записи отслеживания, созданные службами WF, чтобы обеспечить видимость текущего состояния и хода выполнения рабочего процесса.

 Ошибки, зарегистрированные в сеансе отслеживания или трассировки, позволяют находить дефекты кода или неверно сформированные сообщения. Свойство ActivityId узла Correlation в заголовке сообщения события может использоваться для нахождения сбойного действия. Сведения о включении трассировки потока сообщений по ИДЕНТИФИКАТОРу действия см. в разделе [Настройка трассировки потока сообщений](../../../../docs/framework/wcf/diagnostics/etw/configuring-message-flow-tracing.md). В этом разделе описывается включение трассировки потока сообщений в проекте, который был создан в учебнике «Приступая к работе».

### <a name="to-enable-message-flow-tracing-in-the-getting-started-tutorial"></a>Включение трассировки потока сообщений в проекте, который был создан в учебнике «Приступая к работе»

1. Откройте Просмотр событий, нажав кнопку **Пуск**, **выполните**и введите `eventvwr.exe`.

2. Если вы не включили аналитическую трассировку, разверните узел **журналы приложений и служб**, **Microsoft**, **Windows**, **сервер приложений — приложения**. Выберите **вид**, **Показать журналы аналитики и отладки**. Щелкните правой кнопкой мыши аналитика и выберите **Включить журнал**. Оставьте средство просмотра событий открытым, чтобы можно было просматривать трассировки.

3. Откройте пример, созданный в [руководстве по начало работы](../../../../docs/framework/wcf/getting-started-tutorial.md) в Visual Studio 2012. Обратите внимание, что для создания службы необходимо запустить Visual Studio 2012 от имени администратора. Если установлены образцы WCF, можно открыть [Начало работы](../../../../docs/framework/wcf/samples/getting-started-sample.md), содержащий завершенный проект, созданный в этом руководстве.

4. Щелкните правой кнопкой мыши проект **службы** и выберите **Добавить**, **новый элемент**. Выберите **файл конфигурации приложения** и нажмите кнопку **ОК**.

5. Добавьте следующий код в файл App.Config, созданный в предыдущем шаге.

    ```xml
    <system.serviceModel>
      <diagnostics>
        <endToEndTracing propagateActivity="true" messageFlowTracing="true"/>
      </diagnostics>
    </system.serviceModel>
    ```

6. Выполните серверное приложение без отладки, нажав CTRL+F5. Выполните клиентский проект, щелкнув правой кнопкой мыши **клиентский** проект ивыбрав Отладка, **запустить новый экземпляр**.

7. Для трассировки событий от клиента на сервер добавьте в файл конфигурации приложения в проекте Client следующее.

    ```xml
    <diagnostics>
      <endToEndTracing propagateActivity="true" messageFlowTracing="true"/>
    </diagnostics>
    ```

8. В файле Program.cs в клиенте добавьте следующий оператор Using.

    ```csharp
    using System.Diagnostics;
    ```

9. В методе Main файла program.cs клиентского проекта задайте распространение идентификатора GUID трассировки в журнале событий.

    ```csharp
    Guid guid = Guid.NewGuid();
    Trace.CorrelationManager.ActivityId = guid;
    ```

10. Обновите и изучите **аналитический** журнал.  Найдите событие с идентификатором 220.  Выберите событие и перейдите на вкладку **сведения** в области просмотра. Это событие будет содержать идентификатор корреляции для вызывающего действия.

    ```xml
    <Correlation ActivityID="{A066CCF1-8AB3-459B-B62F-F79F957A5036}" />
    ```

    > [!NOTE]
    > Все события с одним и тем же идентификатором GUID в поле ActivityID (идентификатора действия) относятся к одному запросу. Это позволяет сопоставлять сообщения от конкретного клиента определенной службе. Если один клиент вызывает другую службу, то этого клиента можно определить по ActivityID.

11. В некоторых случаях ActivityID может изменяться с исходного идентификатора GUID на новый ActivityID. В этом случае возникает событие передачи. У этого события будет идентификатор 499, а в заголовке события будут содержаться следующие данные.

    ```xml
    <Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
        <System>
            <Provider Name="Microsoft-Windows-Application Server-Applications" Guid="{c651f5f6-1c0d-492e-8ae1-b4efd7c9d503}" />
            <EventID>499</EventID>
            ...
            <Correlation ActivityID="{A066CCF1-8AB3-459B-B62F-F79F957A5036}" RelatedActivityID="{85FC0930-9C49-42DA-804B-A7368104BD1B}" />
            ...
       </System>
    </Event>
    ```

    > [!NOTE]
    > Событие передачи фиксирует изменение активного ActivityID с GUID, указанного в качестве ActivityID, на GUID, указанный в качестве RelatedActivityID. После выдачи события передачи все последующие события будут содержать новый GUID в качестве ActivityID.
