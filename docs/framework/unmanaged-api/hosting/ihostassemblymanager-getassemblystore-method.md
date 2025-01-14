---
title: Метод IHostAssemblyManager::GetAssemblyStore
ms.date: 03/30/2017
api_name:
- IHostAssemblyManager.GetAssemblyStore
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostAssemblyManager::GetAssemblyStore
helpviewer_keywords:
- IHostAssemblyManager::GetAssemblyStore method [.NET Framework hosting]
- GetAssemblyStore method [.NET Framework hosting]
ms.assetid: d0f74593-9bb1-4a11-8096-e29734b20698
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 62965fa928522052b6885769e02c0211ca8d3fe0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69937935"
---
# <a name="ihostassemblymanagergetassemblystore-method"></a>Метод IHostAssemblyManager::GetAssemblyStore
Возвращает указатель интерфейса на объект [IHostAssemblyStore](../../../../docs/framework/unmanaged-api/hosting/ihostassemblystore-interface.md) , представляющий список сборок, загруженных узлом.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT GetAssemblyStore (  
    [out] IHostAssemblyStore **ppAssemblyStore  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `ppAssemblyStore`  
 заполняет Указатель функции на `IHostAssemblyStore` экземпляр или значение null, если узел не реализует `IHostAssemblyStore`.  
  
## <a name="return-value"></a>Возвращаемое значение  
  
|HRESULT|Описание|  
|-------------|-----------------|  
|S_OK|`GetAssemblyStore`успешно возвращено.|  
|HOST_E_CLRNOTAVAILABLE|Среда CLR не была загружена в процесс, или среда CLR находится в состоянии, в котором она не может выполнить управляемый код или успешно обработать вызов.|  
|HOST_E_TIMEOUT|Время ожидания вызова истекло.|  
|HOST_E_NOT_OWNER|Вызывающий объект не владеет блокировкой.|  
|HOST_E_ABANDONED|Событие было отменено, пока заблокированный поток или волокно ожидают его.|  
|E_FAIL|Произошла неизвестная фатальная ошибка. Когда метод возвращает значение E_FAIL, среда CLR больше не может использоваться в процессе. Последующие вызовы методов размещения возвращают HOST_E_CLRNOTAVAILABLE.|  
|E_NOINTERFACE|Узел не предоставляет реализацию `IHostAssemblyStore`.|  
  
## <a name="remarks"></a>Примечания  
 `IHostAssemblyStore`предоставляет методы, позволяющие узлу выполнять привязку к сборкам и модулям независимо от среды CLR. Узлы обычно предоставляют хранилища сборок, позволяющие загружать сборки из форматов, отличных от файловой системы.  
  
> [!NOTE]
> Если узел не реализует `IHostAssemblyStore`, `GetAssemblyStore` должен возвращать значение HRESULT E_NOINTERFACE и устанавливать `ppAssemblyStore` его в NULL.  
  
## <a name="requirements"></a>Требования  
 **Платформ** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** MSCorEE. h  
  
 **Библиотечная** Включается в качестве ресурса в библиотеку MSCorEE. dll  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс IHostAssemblyManager](../../../../docs/framework/unmanaged-api/hosting/ihostassemblymanager-interface.md)
- [Интерфейс IHostAssemblyStore](../../../../docs/framework/unmanaged-api/hosting/ihostassemblystore-interface.md)
