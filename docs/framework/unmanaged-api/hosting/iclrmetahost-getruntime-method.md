---
title: Метод ICLRMetaHost::GetRuntime
ms.date: 03/30/2017
api_name:
- ICLRMetaHost.GetRuntime
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost::GetRuntime
helpviewer_keywords:
- GetRuntime method [.NET Framework hosting]
- ICLRMetaHost::GetRuntime method [.NET Framework hosting]
ms.assetid: a10749f1-ab91-47cf-982f-d8ccd2e81bd2
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f4b796942df153bf2c6ab703d748449331c9a0b1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939850"
---
# <a name="iclrmetahostgetruntime-method"></a>Метод ICLRMetaHost::GetRuntime
Возвращает интерфейс [ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md) , соответствующий определенной версии среды CLR. Этот метод заменяет функцию [CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) , используемую с флагом [STARTUP_LOADER_SAFEMODE](../../../../docs/framework/unmanaged-api/hosting/startup-flags-enumeration.md) .  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT GetRuntime (  
    [in] LPCWSTR pwzVersion,  
    [in] REFIID riid,  
    [out,iid_is(riid), retval] LPVOID *ppRuntime  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `pwzVersion`  
 окне Версия компиляции .NET Framework, хранящаяся в метаданных, в формате "v*A*. *Б* [. *X*] ". *A*, *B*и *X* — это десятичные числа, соответствующие основной версии, дополнительной версии и номеру сборки.  
  
> [!NOTE]
> Этот параметр должен соответствовать имени каталога для .NET Framework версии, так как она отображается в разделе К:\виндовс\микрософт.нет\фрамеворк или C:\Windows\Microsoft.NET\Framework64.  
  
 Примеры значений: "v 1.0.3705", "v 1.1.4322", "v 2.0.50727" и "v 4.0. *X*", где *X* зависит от установленного номера сборки. Требуется префикс "v".  
  
 `riid`  
 окне Идентификатор требуемого интерфейса. Сейчас единственным допустимым значением для этого параметра является IID_ICLRRuntimeInfo.  
  
 `ppRuntime`  
 заполняет Указатель на интерфейс [ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md) , соответствующий запрошенной среде выполнения.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Этот метод возвращает следующие конкретные результаты HRESULT, а также ошибки HRESULT, которые указывают на сбой метода.  
  
|HRESULT|Описание|  
|-------------|-----------------|  
|S_OK|Метод завершился успешно.|  
|E_POINTER|`pwzVersion` или `ppRuntime` равно null.|  
  
## <a name="remarks"></a>Примечания  
 Этот метод взаимодействует согласованно с устаревшими интерфейсами, такими как интерфейс [ICorRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md) , и устаревшими функциями `CorBindTo*` , такими как устаревшие функции (см. статью [устаревшие функции размещения CLR](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md) в размещении .NET Framework 2,0). API). То есть среды выполнения, загруженные с помощью API прежних версий, видимы для нового API, а среды выполнения, которые загружаются с новым API, видимы для API прежних версий.  
  
## <a name="requirements"></a>Требования  
 **Платформ** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** Метахост. h  
  
 **Библиотечная** Включается в качестве ресурса в библиотеку MSCorEE. dll  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICLRMetaHost](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-interface.md)
- [Устаревшие интерфейсы размещения CLR и коклассы](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-interfaces-and-coclasses.md)
- [Интерфейсы размещения CLR](../../../../docs/framework/unmanaged-api/hosting/clr-hosting-interfaces.md)
- [Устаревшие функции размещения CLR](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
- [Размещение](../../../../docs/framework/unmanaged-api/hosting/index.md)
