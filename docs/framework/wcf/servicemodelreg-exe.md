---
title: Средство регистрации ServiceModel (ServiceModelReg.exe)
ms.date: 03/30/2017
ms.assetid: 396ec5ae-e34f-4c64-a164-fcf50e86b6ac
ms.openlocfilehash: 519f303507ed873266cc05a7556073887b66ba6f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923027"
---
# <a name="servicemodel-registration-tool-servicemodelregexe"></a>Средство регистрации ServiceModel (ServiceModelReg.exe)
Этот инструмент командной строки предоставляет возможность управления регистрацией компонентов WCF и WF на одном компьютере. В обычных условиях использование данного средства не требуется, так как при установке компонентов WCF и WF производится их правильная настройка. Но если вы испытываете проблемы с активацией службы, то можно попробовать зарегистрировать компоненты с помощью этого средства.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
ServiceModelReg.exe[(-ia|-ua|-r)|((-i|-u) -c:<command>)] [-v|-q] [-nologo] [-?]  
```  
  
## <a name="remarks"></a>Примечания  
 Это средство можно найти в следующей папке:  
  
 %SystemRoot%\Microsoft.Net\Framework\v3.0\Windows Communication Foundation\  
  
> [!NOTE]
> [!INCLUDE[wv](../../../includes/wv-md.md)]При запуске средства регистрации ServiceModel в диалоговом окне " **компоненты Windows** " может не отображаться, что параметр **Windows Communication Foundation активации HTTP** в разделе **Microsoft .NET Framework 3,0** включен. Чтобы открыть диалоговое окно **компонентов Windows** , нажмите кнопку **Пуск**, выберите команду **выполнить** и введите **оптионалфеатурес**.  
  
 В следующей таблице представлены параметры, которые могут использоваться с ServiceModelReg.exe.  
  
|Параметр|Описание|  
|------------|-----------------|  
|`-ia`|Устанавливает все компоненты WCF и WF.|  
|`-ua`|Удаляет все компоненты WCF и WF.|  
|`-r`|Ремонтирует все компоненты WCF и WF.|  
|`-i`|Устанавливает компоненты WCF и WF, заданные с помощью ключа «-с».|  
|`-u`|Удаляет компоненты WCF и WF, заданные с помощью ключа «-с».|  
|`-c`|Устанавливает или удаляет компонент.<br /><br /> -хттпнамеспаце — резервирование пространства имен HTTP<br />-ткппортшаринг — служба общего доступа к портам TCP<br />-ткпактиватион — служба активации TCP (не поддерживается в клиентском профиле .NET 4)<br />-намедпипеактиватион — служба активации именованных каналов (не поддерживается в клиентском профиле .NET 4)<br />-Служба msmqactivation — служба активации MSMQ (не поддерживается в клиентском профиле .NET 4)<br />-ETW — манифесты трассировки событий ETW (Windows Vista или более поздней версии)|  
|`-q`|Тихий режим (только для отображения журнала ошибок)|  
|`-v`|Режим подробного вывода.|  
|`-nologo`|Подавляет вывод логотипа и сообщения об авторском праве.|  
|`-?`|Отображает текст справки|  
  
## <a name="fixing-the-fileloadexception-error"></a>Исправление ошибки FileLoadException  
 Если вы установили предыдущие версии WCF на компьютере, при запуске средства ServiceModelReg для `FileLoadFoundException` регистрации новой установки может возникнуть ошибка. Это может произойти, даже если пользователь вручную удалил файлы из каталога установки предыдущей версии, но оставил файл machine.config без изменений.  
  
 Сообщение об ошибке подобно приведенному ниже.  
  
```  
Error: System.IO.FileLoadException: Could not load file or assembly 'System.ServiceModel, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' or one of its dependencies. The located assembly's manifest definition does not match the assembly reference. (Exception from HRESULT: 0x80131040)  
File name: 'System.ServiceModel, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'  
```  
  
 Из этого сообщения об ошибке можно выяснить, что сборка System.ServiceModel версии 2.0.0.0 была установлена более ранней CTP-версией. Текущая версия сборки System.ServiceModel - 3.0.0.0. Таким образом, эта проблема возникает, если необходимо установить официальный выпуск WCF на компьютере, где была установлена ранняя CTP-версия WCF, но не полностью удалена.  
  
 ServiceModelReg.exe не может удалять записи предыдущих версий или регистрировать записи новой версии. Единственным решением является изменение файла machine.config вручную. Этот файл находится в следующем расположении.  
  
```  
%windir%\Microsoft.NET\Framework\v2.0.50727\config\machine.config   
```  
  
 Если WCF выполняется на 64-разрядном компьютере, необходимо также изменить тот же файл в этом расположении.  
  
```  
%windir%\Microsoft.NET\Framework64\v2.0.50727\config\machine.config   
```  
  
 Найдите в этом файле все XML-узлы, которые ссылаются на "System. ServiceModel, версия = 2.0.0.0", удалите их и все дочерние узлы. Сохраните файл и повторно запустите ServiceModelReg.exe. Проблема устранена.  
  
## <a name="examples"></a>Примеры  
 В следующих примерах показано, как использовать наиболее употребимые параметры средства ServiceModelReg.exe.  
  
```  
ServiceModelReg.exe -ia  
  Installs all components  
ServiceModelReg.exe -i -c:httpnamespace -c:etw  
  Installs HTTP namespace reservation and ETW manifests  
ServiceModelReg.exe -u -c:etw  
  Uninstalls ETW manifests  
ServiceModelReg.exe -r  
  Repairs an extended install  
```
