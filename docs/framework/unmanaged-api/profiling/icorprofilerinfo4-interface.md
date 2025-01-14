---
title: Интерфейс ICorProfilerInfo4
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4
helpviewer_keywords:
- ICorProfilerInfo4 interface [.NET Framework profiling]
ms.assetid: 80a5308e-c22f-4201-ba89-31cc8562515b
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 34c358a3405262787ed495bf9d8d75462d97a71f
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/30/2019
ms.locfileid: "66380333"
---
# <a name="icorprofilerinfo4-interface"></a>Интерфейс ICorProfilerInfo4
Предоставляет методы, используемые профилировщиками кода для взаимодействия с CLR (CLR) для управления отслеживанием событий и сведения о запросе. . `ICorProfilerInfo4` Интерфейс является расширением другой `ICorProfilerInfo` интерфейсов. Он предоставляет новые методы для поддержки перекомпиляции just-in-time (JIT), добавленные в .NET Framework 4.5.  
  
## <a name="methods"></a>Методы  
  
|Метод|Описание|  
|------------|-----------------|  
|[Метод EnumJITedFunctions2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-enumjitedfunctions2-method.md)|Возвращает перечислитель для всех функций, которые были ранее JIT-компиляции и перекомпиляции JIT.|  
|[Метод EnumThreads](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-enumthreads-method.md)|Возвращает перечислитель, который предоставляет методы для последовательного перебора коллекции все управляемые потоки в процессе профилирования.|  
|[Метод GetCodeInfo3](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getcodeinfo3-method.md)|Получает экстенты машинного кода, связанного с перекомпилированной с помощью JIT-компилятора версией указанной функции.|  
|[Метод GetFunctionFromIP2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getfunctionfromip2-method.md)|Сопоставляет указатель инструкции управляемого кода для перекомпиляции JIT версию указанной функции.|  
|[Метод GetILToNativeMapping2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getiltonativemapping2-method.md)|Получает сопоставление из смещений промежуточного языка MSIL в собственные смещения для кода, содержащегося в перекомпиляции JIT версию указанной функции.|  
|[Метод GetObjectSize2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getobjectsize2-method.md)|Возвращает размер указанного объекта.|  
|[Метод GetReJITIDs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getrejitids-method.md)|Возвращает массив идентификаторов, определяющих все перекомпиляции JIT версии указанной функции, по-прежнему выделяются.|  
|[Метод InitializeCurrentThread](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-initializecurrentthread-method.md)|Инициализирует текущий поток до последующих вызовов API в одном потоке, поэтому можно избежать этой взаимоблокировки профилировщика.|  
|[Метод RequestReJIT](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-requestrejit-method.md)|Запрашивает перекомпиляцию JIT всех экземпляров указанных функций.|  
|[Метод RequestRevert](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-requestrevert-method.md)|Восстанавливает исходные версии всех экземпляров указанных функций.|  
  
## <a name="remarks"></a>Примечания  
 Среда CLR реализует методы интерфейса `ICorProfilerInfo4` с помощью модели свободных потоков. Каждый метод возвращает значение HRESULT, указывающее на успешное выполнение или сбой. Список возможных кодов возврата см. в файле CorError.h.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** CorProf.idl, CorProf.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейсы профилирования](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [Интерфейс ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
