---
title: Метод ICLRSyncManager::CreateRWLockOwnerIterator
ms.date: 03/30/2017
api_name:
- ICLRSyncManager.CreateRWLockOwnerIterator
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRSyncManager::CreateRWLockOwnerIterator
helpviewer_keywords:
- ICLRSyncManager::CreateRWLockOwnerIterator method [.NET Framework hosting]
- CreateRWLockOwnerIterator method [.NET Framework hosting]
ms.assetid: b5535b87-9439-424e-b9b3-7d6fafb9819e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 64179e132cfaffbb1fcdc2cd0a47bbcc11be2ff0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69943274"
---
# <a name="iclrsyncmanagercreaterwlockowneriterator-method"></a>Метод ICLRSyncManager::CreateRWLockOwnerIterator
Запрашивает, что среда CLR создает итератор для узла, который будет использоваться для определения набора задач, ожидающих блокировки чтения и записи.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT CreateRWLockOwnerIterator (  
    [in]  SIZE_T    cookie,  
    [out] SIZE_T   *pIterator  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `cookie`  
 окне Файл cookie, связанный с требуемой блокировкой чтения и записи.  
  
 `pIterator`  
 заполняет Указатель на итератор, который может быть передан методам [жетрвлокковнернекст](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-getrwlockownernext-method.md) и [DeleteRWLockOwnerIterator](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-deleterwlockowneriterator-method.md) .  
  
## <a name="return-value"></a>Возвращаемое значение  
  
|HRESULT|Описание|  
|-------------|-----------------|  
|S_OK|`CreateRWLockOwnerIterator`успешно возвращено.|  
|HOST_E_CLRNOTAVAILABLE|Среда CLR не была загружена в процесс, или среда CLR находится в состоянии, в котором она не может выполнить управляемый код или успешно обработать вызов.|  
|HOST_E_TIMEOUT|Время ожидания вызова истекло.|  
|HOST_E_NOT_OWNER|Вызывающий объект не владеет блокировкой.|  
|HOST_E_ABANDONED|Событие было отменено, пока заблокированный поток или волокно ожидают его.|  
|E_FAIL|Произошла неизвестная фатальная ошибка. Когда метод возвращает значение E_FAIL, среда CLR больше не может использоваться в процессе. Последующие вызовы методов размещения возвращают HOST_E_CLRNOTAVAILABLE.|  
|HOST_E_INVALIDOPERATION|`CreateRWLockOwnerIterator`был вызван в потоке, который в настоящий момент выполняет управляемый код.|  
  
## <a name="remarks"></a>Примечания  
 Узлы обычно вызывают `CreateRWLockOwnerIterator`методы, `DeleteRWLockOwnerIterator`и `GetRWLockOwnerNext` во время обнаружения взаимоблокировки. Узел отвечает за обеспечение допустимости блокировки чтения и записи, так как среда CLR не пытается сохранить блокировку чтения-записи в активном состоянии. Для обеспечения допустимости блокировки на узле доступны несколько стратегий.  
  
- Узел может блокировать вызовы освобождения для блокировки чтения-записи (например, [IHostSemaphore:: ReleaseSemaphore](../../../../docs/framework/unmanaged-api/hosting/ihostsemaphore-releasesemaphore-method.md)), гарантируя, что этот блок не вызывает взаимоблокировку.  
  
- Узел может блокировать выход из режима ожидания объекта события, связанного с блокировкой чтения и записи, еще раз гарантируя, что этот блок не вызывает взаимоблокировку.  
  
> [!NOTE]
> `CreateRWLockOwnerIterator`метод должен вызываться только для потоков, выполняющих в данный момент неуправляемый код.  
  
## <a name="requirements"></a>Требования  
 **Платформ** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** MSCorEE. h  
  
 **Библиотечная** Включается в качестве ресурса в библиотеку MSCorEE. dll  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICLRSyncManager](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-interface.md)
- [Интерфейс IHostSyncManager](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-interface.md)
