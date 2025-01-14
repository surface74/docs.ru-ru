---
title: Метод ICLRDataTarget2::AllocVirtual
ms.date: 03/30/2017
api_name:
- ICLRDataTarget2.AllocVirtual
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget2::AllocVirtual
helpviewer_keywords:
- ICLRDataTarget2::AllocVirtual method [.NET Framework debugging]
- AllocVirtual method [.NET Framework debugging]
ms.assetid: e3226230-964b-47fb-9f53-d6fdbeda1e9e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 92eff65078f05557f542c64c1be7d4f6eca43eb5
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67738467"
---
# <a name="iclrdatatarget2allocvirtual-method"></a>Метод ICLRDataTarget2::AllocVirtual
Вызывается службами доступа к данным среды выполнения (CLR) для выделения памяти в адресном пространстве данного целевого процесса.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT AllocVirtual(  
    [in] CLRDATA_ADDRESS addr,  
    [in] ULONG32 size,  
    [in] ULONG32 typeFlags,  
    [in] ULONG32 protectFlags,  
    [out] CLRDATA_ADDRESS* virt  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `addr`  
 [in] Объект `CLRDATA_ADDRESS` значение, указывающее запрошенный начальный адрес в памяти для выделения.  
  
 `size`  
 [in] Размер в байтах, выделение памяти.  
  
 `typeFlags`  
 [in] Флаги, которые управляют распределением памяти. См. в разделе Win32 `VirtualAlloc` функции.  
  
 `protectFlags`  
 [in] Атрибуты защиты выделенную память. См. в разделе Win32 `VirtualAlloc` функции.  
  
 `virt`  
 [out] Указатель на `CLRDATA_ADDRESS` значение, указывающее фактический начальный адрес области памяти.  
  
## <a name="remarks"></a>Примечания  
 `AllocVirtual` Метод служит в качестве логической программой-оболочкой для Win32 `VirtualAlloc` функции.  
  
 Этот метод реализуется модулем записи отладчика.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** ClrData.idl, ClrData.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICLRDataTarget2](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget2-interface.md)
- [Метод FreeVirtual](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget2-freevirtual-method.md)
