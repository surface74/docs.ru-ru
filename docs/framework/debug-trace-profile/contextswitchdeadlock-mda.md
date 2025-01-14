---
title: contextSwitchDeadlock MDA
ms.date: 03/30/2017
helpviewer_keywords:
- deadlocks [.NET Framework]
- pumping messages
- STA message pumping
- single-threaded COM components
- MDAs (managed debugging assistants), context switching deadlocks
- managed debugging assistants (MDAs), context switching deadlocks
- ContextSwitchDeadlock MDA
- message pumping
- context switching deadlocks
ms.assetid: 26dfaa15-9ddb-4b0a-b6da-999bba664fa6
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c1a0e2a6c7851b261baa3e02f6431e7a4ff697e4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64660327"
---
# <a name="contextswitchdeadlock-mda"></a>contextSwitchDeadlock MDA

Помощник отладки управляемого кода `contextSwitchDeadlock` (MDA) активируется при обнаружении взаимоблокировки во время попытки перехода к контексту COM.

## <a name="symptoms"></a>Симптомы

Наиболее распространенный признак заключается в том, что вызов неуправляемого компонента COM из управляемого кода не возвращает данные.  Еще одним признаком является постепенное увеличение объема используемой памяти.

## <a name="cause"></a>Причина

Наиболее вероятная причина заключается в том, что поток однопотокового подразделения (STA) не выдает сообщения. Поток однопотокового подразделения либо ожидает без выдачи сообщений, либо выполняет продолжительные операции и не позволяет очереди сообщений выдавать их.

Постепенное увеличение объема используемой памяти вызвано тем, что поток метода завершения пытается вызвать `Release` для неуправляемого компонента COM, и этот компонент не возвращает данные.  Это не позволяет методу завершения освободить другие объекты.

По умолчанию потоковой моделью для основного потока консольных приложений Visual Basic является однопотоковое подразделение. Помощник отладки управляемого кода активируется, если поток однопотокового подразделения использует взаимодействие с COM напрямую либо косвенно посредством среды CLR или стороннего элемента управления.  Чтобы предотвратить активацию помощника отладки управляемого кода в консольном приложении Visual Basic, примените атрибут <xref:System.MTAThreadAttribute> для основного метода или измените приложение, чтобы оно выдавало сообщения.

Существует возможность ошибочной активации помощника отладки управляемого кода при соблюдении всех следующих условий:

- Приложение создает компоненты COM из потоков однопотокового подразделения напрямую или косвенно с помощью библиотек.

- Приложение было остановлено в отладчике, и пользователь либо продолжил выполнение приложения, либо выполнил его в пошаговом режиме.

- Отладка неуправляемого кода выключена.

Чтобы определить, происходит ли ошибочная активация помощника отладки управляемого кода, отключите все точки останова, перезапустите приложение и позвольте ему выполняться без остановок. Если помощник отладки управляемого кода не активируется, вероятно, первоначальная активация была ошибочной. В этом случае отключите помощник отладки управляемого кода, чтобы не нарушать работу сеанса отладки.

> [!NOTE]
> Данный MDA находится в стандартный набор для Visual Studio. Сведения о том, как отключить MDA, см. в разделе [Диагностика ошибок посредством управляемых помощников по отладке](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md#enable-and-disable-mdas).

## <a name="resolution"></a>Решение

Соблюдайте правила COM в отношении выдачи сообщений однопотокового подразделения.

## <a name="effect-on-the-runtime"></a>Влияние на среду выполнения

Этот помощник отладки управляемого кода не оказывает никакого влияния на среду CLR. Он только выводит данные о контекстах COM.

## <a name="output"></a>Вывод

Сообщение с описанием текущего контекста и целевого контекста.

## <a name="configuration"></a>Параметр Configuration

```xml
<mdaConfig>
  <assistants>
    <contextSwitchDeadlock />
  </assistants>
</mdaConfig>
```

## <a name="see-also"></a>См. также

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Диагностика ошибок посредством помощников по отладке управляемого кода](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
- [Маршалинг взаимодействия](../../../docs/framework/interop/interop-marshaling.md)
