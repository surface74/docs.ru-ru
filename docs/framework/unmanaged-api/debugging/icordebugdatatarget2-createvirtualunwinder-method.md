---
title: Метод ICorDebugDataTarget2::CreateVirtualUnwinder
ms.date: 03/30/2017
ms.assetid: 354c8b4c-7d23-45c6-a7d7-3be4c2a5b772
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a983561f34bee96f5de1e05d608bff930c7ec8c0
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67750243"
---
# <a name="icordebugdatatarget2createvirtualunwinder-method"></a>Метод ICorDebugDataTarget2::CreateVirtualUnwinder
Создает новый элемент очистки стека, запускающий операцию очистки, начиная с исходного контекста (который не обязательно является концом потока).  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT CreateVirtualUnwinder(  
    [in] DWORD nativeThreadID,  
    [in] ULONG32 contextFlags,  
    [in] ULONG32 cbContext,  
    [in, size_is(cbContext)] BYTE initialContext[],  
    [out] ICorDebugVirtualUnwinder ** ppUnwinder);  
};  
```  
  
## <a name="parameters"></a>Параметры  
 nativeThreadID  
 [входной] Идентификатор собственного потока, стек которого должен быть очищен.  
  
 contextFlags  
 [входной] Флаги, указывающие, какие части контекста определены в `initialContext`.  
  
 cbContext  
 [входной] Размер `initialContext`.  
  
 initialContext  
 [входной] Данные в контексте.  
  
 ppUnwinder  
 [выходной] Указатель на адрес объекта интерфейса ICorDebugVirtualUnwinder.  
  
## <a name="return-value"></a>Возвращаемое значение  
 `S_OK` в случае успешного выполнения. Любое другое значение `HRESULT` указывает на ошибку. Любое ошибочное `HRESULT` , полученное процессом mscordbi считается неустранимым и приводит к [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) методам возвращать `CORDBG_E_DATA_TARGET_ERROR`.  
  
## <a name="remarks"></a>Примечания  
  
> [!NOTE]
>  Этот метод доступен только в машинном коде .NET.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICorDebugDataTarget2](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget2-interface.md)
- [Интерфейсы отладки](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
