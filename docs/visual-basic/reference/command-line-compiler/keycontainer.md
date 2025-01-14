---
title: -keycontainer
ms.date: 03/10/2018
helpviewer_keywords:
- -keycontainer compiler option [Visual Basic]
- keycontainer compiler option [Visual Basic]
- /keycontainer compiler option [Visual Basic]
ms.assetid: 6a9bc861-1752-4db1-9f64-b5252f0482cc
ms.openlocfilehash: 5892baaa2732d95cfe698147e06b914af968adc5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69929427"
---
# <a name="-keycontainer"></a>-keycontainer
Указывает имя контейнера для пары ключей, чтобы задать для сборки строгое имя.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-keycontainer:container  
```  
  
## <a name="arguments"></a>Аргументы  
  
|Термин|Определение|  
|---|---|  
|`container`|Обязательный. Файл контейнера, содержащий ключ. Заключите имя файла в кавычки (""), если оно содержит пробел.|  
  
## <a name="remarks"></a>Примечания  
 Компилятор создает совместно используемый компонент, вставляя открытый ключ в манифест сборки и подписывая окончательную сборку с закрытым ключом. Чтобы создать файл ключа, в командной строке введите `sn -k file`. `-i` Параметр устанавливает пару ключей в контейнер. Дополнительные сведения см. в разделе [Sn. exe (средство строгих имен)](../../../framework/tools/sn-exe-strong-name-tool.md).  
  
 При компиляции с `-target:module`параметром имя файла ключа сохраняется в модуле и включается в сборку, созданную при компиляции сборки с параметром [-addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md).  
  
 Этот параметр можно также указать в исходном коде любого модуля MSIL в качестве настраиваемого атрибута (<xref:System.Reflection.AssemblyKeyNameAttribute>).  
  
 Также можно передать сведения о шифровании компилятору с помощью параметра [-keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md). Если требуется использовать частично подписанную сборку, применяйте параметр [-delaysign](../../../visual-basic/reference/command-line-compiler/delaysign.md).  
  
 Дополнительные сведения о подписывании сборки см. в разделе [Создание и использование сборок со строгими именами](../../../framework/app-domains/create-and-use-strong-named-assemblies.md) .  
  
> [!NOTE]
> Этот `-keycontainer` параметр недоступен в среде разработки Visual Studio; он доступен только при компиляции из командной строки.  
  
## <a name="example"></a>Пример  
 Следующий код компилирует исходный файл `Input.vb` и задает контейнер ключей.  
  
```  
vbc -keycontainer:key1 input.vb  
```  
  
## <a name="see-also"></a>См. также

- [Сборки в .NET](../../../standard/assembly/index.md)
- [Компилятор Visual Basic с интерфейсом командной строки](../../../visual-basic/reference/command-line-compiler/index.md)
- [-keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)
- [Примеры командных строк компиляции](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
