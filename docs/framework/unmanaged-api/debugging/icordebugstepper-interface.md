---
title: Интерфейс ICorDebugStepper
ms.date: 03/30/2017
api_name:
- ICorDebugStepper
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper
helpviewer_keywords:
- ICorDebugStepper interface [.NET Framework debugging]
ms.assetid: ed8364eb-f01b-46f6-b5e3-5dda9cae2dfe
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c57b13b05522614ff066b93cb9f6a437cb340576
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962685"
---
# <a name="icordebugstepper-interface"></a>Интерфейс ICorDebugStepper
Представляет предпринимаемый отладчиком шаг при выполнении кода, служащий идентификатором на промежутке между подачей команды и ее завершением, а также предоставляет возможность отмены шага.  
  
## <a name="methods"></a>Методы  
  
|Метод|Описание|  
|------------|-----------------|  
|[Метод Deactivate](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-deactivate-method.md)|`ICorDebugStepper` Приводит к отмене полученной команды последнего шага.|  
|[Метод IsActive](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-isactive-method.md)|Возвращает значение, указывающее, выполняется ли `ICorDebugStepper` в данный момент шаг.|  
|[Метод SetInterceptMask](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setinterceptmask-method.md)|Задает значение CorDebugIntercept, указывающее типы кода, в который выполняется пошаговое выполнение.|  
|[Метод SetRangeIL](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setrangeil-method.md)|Задает значение, указывающее, должны ли вызовы метода [ICorDebugStepper:: степранже](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-steprange-method.md) передавать значения аргументов, относящихся к машинному коду или коду кода на языке MSIL, который проходит через шаг.|  
|[Метод SetUnmappedStopMask](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setunmappedstopmask-method.md)|Задает значение Кордебугунмаппедстоп, указывающее тип несопоставленного кода, в котором выполнение будет остановлено.|  
|[Метод Step](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-step-method.md)|`ICorDebugStepper` Приводит к пошаговому вызову содержащего его потока и, при необходимости, для продолжения единого пошагового выполнения функций, которые вызываются в потоке.|  
|[Метод StepOut](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-stepout-method.md)|`ICorDebugStepper` Приводит к пошаговому вызову содержащего его потока и выполнению, когда текущий кадр возвращает управление вызывающему кадру.|  
|[Метод StepRange](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-steprange-method.md)|`ICorDebugStepper` Приводит к пошаговому вызову содержащего его потока и возврату при достижении кода, находящегося за последним из указанных диапазонов.|  
  
## <a name="remarks"></a>Примечания  
 `ICorDebugStepper` Интерфейс выполняет следующие задачи:  
  
- Он выступает в качестве идентификатора между выдаваемыми командой Step и завершением этой команды.  
  
- Он предоставляет центральный интерфейс для инкапсуляции всех шагов, которые можно выполнить.  
  
- Он позволяет преждевременно отменить операцию пошагового выполнения.  
  
 Для каждого потока может существовать несколько шагов. Например, при пошаговом выполнении функции может быть достигнута точка останова, и пользователю может потребоваться начать новую операцию пошагового выполнения внутри этой функции. Для определения способа решения этой проблемы отладчику необходимо присвоить значение. Отладчик может захотеть отменить исходную операцию пошагового выполнения или вложить две операции. `ICorDebugStepper` Интерфейс поддерживает оба варианта.  
  
 Средство организации пошагового выполнения может переноситься между потоками, если среда CLR выполняет перекрестный потоковый вызов.  
  
> [!NOTE]
> Этот интерфейс не поддерживает удаленные вызовы между компьютерами или между процессами.  
  
## <a name="requirements"></a>Требования  
 **Платформ** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** CorDebug. idl, CorDebug. h  
  
 **Библиотечная** Коргуидс. lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейсы отладки](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
