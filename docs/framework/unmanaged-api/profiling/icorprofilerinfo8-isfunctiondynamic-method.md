---
title: 'ICorProfilerInfo8:: Исфунктиондинамик'
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo8.IsFunctionDynamic
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: 046db493db77572904a8454a5b002dcae15b9e1d
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/21/2019
ms.locfileid: "69661157"
---
# <a name="icorprofilerinfo8isfunctiondynamic-method"></a>Метод ICorProfilerInfo8:: Исфунктиондинамик

Определяет, имеет ли функция связанные метаданные.

## <a name="syntax"></a>Синтаксис

```cpp
HRESULT IsFunctionDynamic( [in]  FunctionID  functionId,
                           [out] BOOL        *isDynamic);
```

#### <a name="parameters"></a>Параметры

`functionId` \
окне  Объект `FunctionID` , определяющий рассматриваемую функцию.

`isDynamic` \
заполняет Указатель на объект `BOOL` , который будет содержать значение, указывающее, имеет ли функция метаданные.

## <a name="remarks"></a>Примечания

Функция считается динамической, если она не имеет метаданных. Некоторые методы, такие как заглушки IL или методы LCG, не имеют связанных метаданных, которые можно получить с помощью API-интерфейсов интерфейса IMetaDataImport. Эти методы могут быть обнаружены профилировщиками с помощью указателей инструкций или путем прослушивания в [ICorProfilerCallback::D инамикмесоджиткомпилатионстартед](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md).

## <a name="requirements"></a>Требования

**Платформ** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).

**Заголовок.** CorProf. idl, CorProf. h

**Библиотечная** Коргуидс. lib

**.NET Framework версии:** [! ВКЛЮЧИТЬ[net_current_v472plus](../../../../includes/net-current-v472plus.md)

## <a name="see-also"></a>См. также

- [Интерфейс ICorProfilerInfo8](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo8-interface.md)
