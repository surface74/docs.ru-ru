---
title: Аналитическая трассировка WCF
ms.date: 03/30/2017
ms.assetid: 6029c7c7-3515-4d36-9d43-13e8f4971790
ms.openlocfilehash: ba4f1778059f7b960eebd42822048fa031e6961e
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044546"
---
# <a name="wcf-analytic-tracing"></a>Аналитическая трассировка WCF
В этом примере показано, как добавить собственные события трассировки в поток аналитических трассировок, которые Windows Communication Foundation (WCF) записывают в ETW [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]в. Аналитически отслеживаемые события предназначены для упрощения добавления видимости в службы без ущерба для производительности. В этом примере показано, как использовать <xref:System.Diagnostics.Eventing?displayProperty=nameWithType> API для записи событий, которые интегрируются со службами WCF.  
  
 Дополнительные сведения об API см <xref:System.Diagnostics.Eventing?displayProperty=nameWithType> . в разделе <xref:System.Diagnostics.Eventing?displayProperty=nameWithType>.  
  
 Дополнительные сведения о трассировке событий в Windows см. в статье [улучшение отладки и настройка производительности с помощью ETW](https://go.microsoft.com/fwlink/?LinkId=166488).  
  
## <a name="disposing-eventprovider"></a>Удаление EventProvider  
 В этом образце используется класс <xref:System.Diagnostics.Eventing.EventProvider?displayProperty=nameWithType>, который реализует <xref:System.IDisposable?displayProperty=nameWithType>. При реализации трассировки для службы WCF, скорее всего, вы можете использовать ресурсы в <xref:System.Diagnostics.Eventing.EventProvider>течение времени существования службы. По этой причине, а также для удобочитаемости, этот образец никогда не удаляет упакованный <xref:System.Diagnostics.Eventing.EventProvider>. Если по какой-либо причине ваша служба имеет другие требования для трассировки и вы должны удалить этот ресурс, то вы должны изменить этот пример в соответствии с подходящими рекомендациями по удалению неуправляемых ресурсов. Дополнительные сведения об освобождении неуправляемых ресурсов см. в разделе [Реализация метода Dispose](https://go.microsoft.com/fwlink/?LinkId=166436).  
  
## <a name="self-hosting-vs-web-hosting"></a>Резидентное размещение в сравнении с размещением на веб-узле  
 Для служб, размещенных в Интернете, аналитические трассировки WCF предоставляют поле с именем «HostReference», которое используется для указания службы, которая выдает трассировку. В этой модели могут участвовать расширяемые пользовательские трассировки, а в данном образце демонстрируются рекомендации, как это сделать. Формат ссылки на веб-узел, когда в результирующей&#124;строке фактически отображается символ вертикальной черты, может быть одним из следующих:  
  
- Если приложение находится не в корне.  
  
     \<SiteName >\<аппликатионвиртуалпас >&#124;\<сервицевиртуалпас&#124;>\<ServiceName >  
  
- Если приложение находится в корне.  
  
     \<SiteName >&#124;\<сервицевиртуалпас >&#124;\<ServiceName >  
  
 Для служб, размещенных на собственном сервере, аналитические трассировки WCF не заполняют поле "HostReference". В этом образце класс `WCFUserEventProvider` ведет себя согласованно при использовании резидентной службой.  
  
## <a name="custom-event-details"></a>Данные пользовательских событий  
 Манифест поставщика событий ETW WCF определяет три события, предназначенные для порождения авторами служб WCF из кода службы. В следующей таблице приведена разбивка этих трех событий.  
  
|событие|Описание|Идентификатор события|  
|-----------|-----------------|--------------|  
|UserDefinedInformationEventOccurred|Это событие выдается, когда в службе происходит что-то примечательное, что не является проблемой. Например, можно выдать событие после успешного вызова базы данных.|301|  
|UserDefinedWarningOccurred|Это событие выдается, когда возникает проблема, которая в будущем может привести к сбою. Например, можно выдавать событие предупреждения, когда вызов базы данных завершается неудачей, но удалось выполнить восстановление, переключившись на резервное хранилище данных.|302|  
|UserDefinedErrorOccurred|Это событие выдается, когда служба не ведет себя, как положено. Например, можно выдавать событие, если вызов базы данных завершается неудачей и данные не удалось получить из другого источника.|303|  
  
#### <a name="to-use-this-sample"></a>Использование этого образца  
  
1. С помощью Visual Studio 2012 откройте файл решения ВкфаналитиктраЦинжекстенсибилити. sln.  
  
2. Для построения решения нажмите CTRL+SHIFT+B.  
  
3. Чтобы запустить решение, нажмите клавиши CTRL+F5.  
  
     В веб-браузере щелкните **Калькулятор. svc**. В браузере должен появиться URI WSDL-документа для службы. Скопируйте этот URI.  
  
4. Запустите тестовый клиент WCF (клиент WcfTestClient. exe).  
  
     Тестовый клиент WCF (клиент WcfTestClient. exe) находится в `\<Visual Studio 2012 Install Dir>\Common7\IDE\WcfTestClient.exe`папке. Каталог установки Visual Studio 2012 по умолчанию `C:\Program Files\Microsoft Visual Studio 10.0`—.  
  
5. В тестовом клиенте WCF добавьте службу, выбрав **файл**, а затем **Добавить службу**.  
  
     Добавьте адрес конечной точки в поле ввода.  
  
6. Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно.  
  
     Служба ICalculator добавляется в левой области в разделе **Мои проекты служб**.  
  
7. Откройте приложение просмотра событий.  
  
     Перед вызовом службы запустите Просмотр событий и убедитесь, что журнал событий прослушивает события отслеживания, созданные из службы WCF.  
  
8. В меню **Пуск** выберите **Администрирование**, а затем **Просмотр событий**. Включите журналы **аналитики** и **отладки** .  
  
9. В древовидном представлении в Просмотр событий перейдите к **Просмотр событий**, **журналы приложений и служб**, **Microsoft**, **Windows**, а затем **сервер приложений — приложения**. Щелкните правой кнопкой мыши **сервер приложений — приложения**, выберите **вид**, а затем **Показать журналы аналитики и отладки**.  
  
     Убедитесь, что установлен флажок **отображать журналы аналитики и отладки** . Включите **аналитический** журнал.  
  
     В древовидном представлении в Просмотр событий перейдите к **Просмотр событий**, **журналы приложений и служб**, **Microsoft**, **Windows**, **сервер приложений — приложения**, а затем **аналитика**. Щелкните правой кнопкой мыши аналитика и выберите **Включить журнал**.  
  
10. Проверьте службу с помощью тестового клиента WCF.  
  
    1. В тестовом клиенте WCF дважды щелкните **Добавить ()** в узле службы ICalculator.  
  
         Метод **Add ()** отображается в правой области с двумя параметрами.  
  
    2. Введите 2 для первого параметра и 3 для второго.  
  
    3. Нажмите кнопку **вызвать** , чтобы вызвать метод.  
  
11. Перейдите в уже открытое окно **Просмотр событий** . Перейдите в раздел **Просмотр событий**, **журналы приложений и служб**, **Microsoft**, **Windows**, **сервер приложений — приложения**.  
  
12. Щелкните правой кнопкой мыши **аналитический** узел и выберите **Обновить**.  
  
     События появятся в области справа.  
  
13. Найдите событие с идентификатором 303 и щелкните его дважды, чтобы открыть его и ознакомиться с его содержимым.  
  
     Это событие было создано `Add()` методом службы ICalculator и имеет полезные данные, равные "2 + 3 = 5".  
  
#### <a name="to-clean-up-optional"></a>Очистка (необязательно)  
  
1. Откройте **Просмотр событий**.  
  
2. Перейдите к **Просмотр событий**, **журналам приложений и служб**, **Microsoft**, **Windows**, а затем **Application-Servers-Applications**. Щелкните правой кнопкой мыши аналитика и выберите **Отключить журнал**.  
  
3. Перейдите к разделу **Просмотр событий**, **журналы приложений и служб**, **Microsoft**, **Windows**, **Application-Servers-Applications**и затем **аналитика**. Щелкните правой кнопкой мыши аналитика и выберите **Очистить журнал**.  
  
4. Нажмите кнопку **очистить** , чтобы очистить события.  
  
## <a name="known-issue"></a>Известная проблема  
 Существует известная ошибка в **Просмотр событий** , в которой может не расшифровать события трассировки событий Windows. Может появиться сообщение об ошибке с текстом: "Не удается найти описание идентификатора \<события ID > из источника Microsoft-Windows-Application Server-Applications. Возможно, компонент, вызывающий это событие, не установлен на локальном компьютере, либо установка повреждена. Компонент можно установить или восстановить на локальном компьютере ". Если возникла эта ошибка, выберите **Обновить** в меню **действия** . Теперь декодирование события должно выполняться правильно.  
  
> [!IMPORTANT]
> Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> Если этот каталог не существует, перейдите к [примерам Windows Communication Foundation (WCF) и Windows Workflow Foundation (WF) для .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) , чтобы скачать все Windows Communication Foundation (WCF) [!INCLUDE[wf1](../../../../includes/wf1-md.md)] и примеры. Этот образец расположен в следующем каталоге.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ETWTrace`  
  
## <a name="see-also"></a>См. также

- [Примеры мониторинга AppFabric](https://go.microsoft.com/fwlink/?LinkId=193959)
