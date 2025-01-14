---
title: -win32resource
ms.date: 03/13/2018
f1_keywords:
- -win32resource
- win32resource
helpviewer_keywords:
- /win32resource compiler option [Visual Basic]
- -win32resource compiler option [Visual Basic]
- win32resource compiler option [Visual Basic]
ms.assetid: e226946d-19ce-4cc9-91f5-aed24f77aa2b
ms.openlocfilehash: 382dcc6571aa06ecdfc32bf43080c4b7a36eb1f0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69961305"
---
# <a name="-win32resource"></a>-win32resource
Вставляет файл ресурсов Win32 в выходной файл.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-win32resource:filename  
```  
  
## <a name="arguments"></a>Аргументы  
 `filename`  
 Имя файла ресурсов, добавляемого в выходной файл. Заключите имя файла в кавычки (""), если оно содержит пробел.  
  
## <a name="remarks"></a>Примечания  
 Вы можете создать файл ресурсов Win32 с помощью компилятора ресурсов Microsoft Windows (RC).  
  
 Ресурс Win32 может содержать сведения о версии или битовой карте (значок), которые помогают в определении приложения в **проводнике**. Если не указать `-win32resource`, компилятор создает сведения о версии на основе версии сборки. Параметры `-win32resource` и`-win32icon` являются взаимоисключающими.  
  
 Чтобы присоединить файл ресурсов .NET Framework, см. раздел [-linkresource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/linkresource.md) для ссылки на файл ресурсов .NET Framework или [-Resource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/resource.md) .  
  
> [!NOTE]
> Этот `-win32resource` параметр недоступен в среде разработки Visual Studio; он доступен только при компиляции из командной строки.  
  
## <a name="example"></a>Пример  
 Следующий код компилирует `In.vb` и присоединяет `Rf.res`файл ресурсов Win32:  
  
```console  
vbc -win32resource:rf.res in.vb  
```  
  
## <a name="see-also"></a>См. также

- [Компилятор Visual Basic с интерфейсом командной строки](../../../visual-basic/reference/command-line-compiler/index.md)
- [Примеры командных строк компиляции](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
