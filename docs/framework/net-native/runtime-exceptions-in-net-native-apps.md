---
title: Исключения среды выполнения в собственных приложениях .NET
ms.date: 03/30/2017
ms.assetid: 5f050181-8fdd-4a4e-9d16-f84c22a88a97
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6472f02cf2633d936252bfd2a8daa3ff711a4db8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69967879"
---
# <a name="runtime-exceptions-in-net-native-apps"></a>Исключения среды выполнения в собственных приложениях .NET
Очень важно выполнять тестирование сборок выпуска приложения универсальной платформы Windows на их целевых платформах, поскольку конфигурации отладки и выпуска совершенно различны. По умолчанию конфигурация отладки использует для компиляции приложения среду выполнения .NET Core, но конфигурация выпуска использует для компиляции приложения в машинный код среду выполнения .NET Native.  
  
> [!IMPORTANT]
> Сведения о работе с исключениями [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md), [MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md)и [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) , которые могут возникнуть при тестировании версий выпуска приложения, см. в разделе Шаг 4. Вручную разрешить отсутствующие метаданные: в [Начало работы](../../../docs/framework/net-native/getting-started-with-net-native.md) разделе, а также в ссылке на файл конфигурации [отражения и .NET Native](../../../docs/framework/net-native/reflection-and-net-native.md) и [директив среды выполнения (RD. XML)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md).  
  
## <a name="debug-and-release-builds"></a>Отладочные и выпускные сборки  
 Когда отладочная сборка выполняется в среде выполнения .NET Core, она не компилируется в машинный код. Это делает все службы, обычно предоставляемые средой выполнения, доступными вашему приложению.  
  
 С другой стороны, выпускная сборка компилируется в машинный код для целевых платформ, при этом удаляется большинство зависимостей от внешних сред выполнения и библиотек и выполняется серьезная оптимизация кода для достижения максимальной производительности.  
  
 При отладке выпускных сборок, которые компилируются с помощью .NET Native, происходит следующее.  
  
- Вы используете модуль отладки .NET Native, который отличается от обычных средств отладки .NET.  
  
- Размер исполняемого файла максимально уменьшается. Один из способов, которым .NET Native уменьшает размер исполняемого файла, состоит в значительном сокращении сообщений об исключениях времени выполнения. Это более подробно рассматривается в разделе [Runtime exception messages](#Messages) .  
  
- Код сильно оптимизируется. Это означает, что везде, где это возможно, используется встраивание. (Встраивание перемещает код из внешних подпрограмм в вызывающую программу.)   То, что .NET Native предоставляет специализированную среду выполнения и реализует агрессивное встраивание, влияет на стек вызовов, который отображается при отладке.  Дополнительные сведения см. в разделе [Runtime call stack](#CallStack) .  
  
> [!NOTE]
> Вы можете управлять тем, будут ли отладочные и выпускные сборки компилироваться с помощью цепочки инструментов .NET Native, устанавливая или снимая флажок **Компилировать с использованием цепочки инструментов машинного кода .NET** .   Однако обратите внимание, что Магазин Windows всегда будет компилировать рабочую версию вашего приложения с помощью цепочки инструментов .NET Native.  
  
<a name="Messages"></a>   
## <a name="runtime-exception-messages"></a>Runtime exception messages  
 Чтобы свести к минимуму размер исполняемого файла приложения, .NET Native не включает полный текст сообщений об исключениях. В результате исключения среды выполнения, возникающие в выпускной сборке, могут не отображать полный текст сообщений об исключениях. Вместо этого текст может содержать подстроку со ссылкой на дополнительные сведения. Например, сведения об исключении могут выглядеть следующим образом:  
  
```  
Exception thrown: '$16_System.AggregateException' in Unknown Module.  
  
Additional information: AggregateException_ctor_DefaultMessage  
  
If there is a handler for this exception, the program may be safely continued.  
```  
  
 Если вам требуется полное сообщение об исключении, запустите отладочную сборку. Например, предыдущие сведения об исключении из выпускной сборки могут выглядеть в отладочной сборке следующим образом:  
  
```  
Exception thrown: 'System.AggregateException' in NativeApp.exe.  
  
Additional information: Value does not fall within the expected range.  
```  
  
<a name="CallStack"></a>   
## <a name="runtime-call-stack"></a>Runtime call stack  
 Из-за встраивания и других видов оптимизации стек вызовов, отображаемый приложением, которое скомпилировано цепочкой инструментов .NET Native, может не позволить вам четко определить путь к исключению среды выполнения.  
  
 Чтобы получить полный стек, запустите отладочную сборку.  
  
## <a name="see-also"></a>См. также

- [Отладка .NET Native универсальных приложениях Windows](https://devblogs.microsoft.com/devops/debugging-net-native-windows-universal-apps/)
- [Начало работы](../../../docs/framework/net-native/getting-started-with-net-native.md)
