---
title: Функция CorBindToRuntimeHost
ms.date: 03/30/2017
api_name:
- CorBindToRuntimeHost
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- CorBindToRuntimeHost
helpviewer_keywords:
- CorBindToRuntimeHost function [.NET Framework hosting]
ms.assetid: 5c826ba3-8258-49bc-a417-78807915fcaf
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7e1965917e8a1c5ae07cf119df3664b969a979be
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969253"
---
# <a name="corbindtoruntimehost-function"></a>Функция CorBindToRuntimeHost
Позволяет узлам загружать в процесс указанную версию среды CLR.  
  
 Эта функция является устаревшей в .NET Framework 4.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT CorBindToRuntimeHost (  
    [in] LPCWSTR       pwszVersion,   
    [in] LPCWSTR       pwszBuildFlavor,   
    [in] LPCWSTR       pwszHostConfigFile,   
    [in] VOID*         pReserved,   
    [in] DWORD         startupFlags,   
    [in] REFCLSID      rclsid,   
    [in] REFIID        riid,   
    [out] LPVOID FAR  *ppv  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `pwszVersion`  
 окне Строка, описывающая версию среды CLR, которую требуется загрузить.  
  
 Номер версии в .NET Framework состоит из четырех частей, разделенных точками: *основной. дополнительный. сборка. Редакция*. Строка, передаваемая `pwszVersion` как, должна начинаться с символа "v", за которым следуют первые три части номера версии (например, "v 1.0.1529").  
  
 Некоторые версии среды CLR устанавливаются с инструкцией политики, которая определяет совместимость с предыдущими версиями среды CLR. По умолчанию оболочка `pwszVersion` запуска выполняет проверку на соответствие инструкциям политики и загружает последнюю версию среды выполнения, совместимую с запрашиваемой версией. Узел может заставить оболочку пропускать вычисление политики и загружать точную версию, указанную `pwszVersion` в, передав значение STARTUP_LOADER_SAFEMODE `startupFlags` для параметра.  
  
 Если `pwszVersion` —`null,` метод не загружает ни одной версии среды CLR. Вместо этого он возвращает CLR_E_SHIM_RUNTIMELOAD, который указывает, что ему не удалось загрузить среду выполнения.  
  
 `pwszBuildFlavor`  
 окне Строка, указывающая, загружать ли сервер или рабочую станцию сборку среды CLR. Допустимые значения: `svr` и `wks`. Сборка сервера оптимизирована для использования нескольких процессоров для сборок мусора, а сборка рабочей станции оптимизирована для клиентских приложений, работающих на однопроцессорном компьютере.  
  
 Если `pwszBuildFlavor` параметр имеет значение null, загружается сборка рабочей станции. При запуске на однопроцессорном компьютере сборка рабочей станции всегда загружается, даже если `pwszBuildFlavor` параметр имеет `svr`значение. Однако если `pwszBuildFlavor` задано `svr` значение и задана параллельная сборка мусора ( `startupFlags` см. Описание параметра), то загружается серверная сборка.  
  
> [!NOTE]
> Параллельная сборка мусора не поддерживается в приложениях, использующих Эмулятор WOW64 x86 в 64-разрядных системах, которые реализуют архитектуру Intel Itanium (прежнее название — IA-64). Дополнительные сведения об использовании WOW64 в 64-разрядных системах Windows см. в разделе [выполнение 32-разрядных приложений](/windows/desktop/WinProg64/running-32-bit-applications).  
  
 `pwszHostConfigFile`  
 окне Имя файла конфигурации узла, указывающего версию среды CLR для загрузки. Если имя файла не содержит полного пути, предполагается, что файл находится в том же каталоге, что и исполняемый файл, выполняющий вызов.  
  
 `pReserved`  
 окне Зарезервировано для будущего расширения.  
  
 `startupFlags`  
 окне Набор флагов, управляющих параллельной сборкой мусора, нейтральным к домену кодом и поведением `pwszVersion` параметра. Значение по умолчанию — один домен, если флаг не установлен. Список поддерживаемых значений см. в разделе Перечисление [STARTUP_FLAGS](../../../../docs/framework/unmanaged-api/hosting/startup-flags-enumeration.md).  
  
 `rclsid`  
 окне Объект `CLSID` coclass, реализующий интерфейс [ICorRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md) или [ICLRRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/iclrruntimehost-interface.md) . Поддерживаемые значения: CLSID_CorRuntimeHost или CLSID_CLRRuntimeHost.  
  
 `riid`  
 окне `IID` Запрашиваемый интерфейс. Поддерживаемые значения: IID_ICorRuntimeHost или IID_ICLRRuntimeHost.  
  
 `ppv`  
 заполняет Указатель интерфейса на версию загруженной среды выполнения.  
  
## <a name="requirements"></a>Требования  
 **Платформ** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** MSCorEE. idl  
  
 **Библиотечная** MSCorEE. dll  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Функция CorBindToCurrentRuntime](../../../../docs/framework/unmanaged-api/hosting/corbindtocurrentruntime-function.md)
- [Функция CorBindToRuntime](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntime-function.md)
- [Функция CorBindToRuntimeByCfg](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md)
- [Функция CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)
- [Интерфейс ICorRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md)
- [Устаревшие функции размещения CLR](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
