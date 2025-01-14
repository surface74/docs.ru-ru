---
title: -platform (Visual Basic)
ms.date: 03/13/2018
helpviewer_keywords:
- platform compiler option [Visual Basic]
- /platform compiler option [Visual Basic]
- -platform compiler option [Visual Basic]
ms.assetid: f9bc61e6-e854-4ae1-87b9-d6244de23fd1
ms.openlocfilehash: eb5513c6d8e4085e1b3f69de1d36a007fa27271e
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/30/2019
ms.locfileid: "66380303"
---
# <a name="-platform-visual-basic"></a>-platform (Visual Basic)
Указывает, на какой версии платформы среды CLR может запускаться выходной файл.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-platform:{ x86 | x64 | Itanium | arm | anycpu | anycpu32bitpreferred }  
```  
  
## <a name="arguments"></a>Аргументы  
  
|Термин|Определение|  
|---|---|  
|`x86`|Компилирует сбору для запуска в 32-разрядной среде CLR с архитектурой x86.|  
|`x64`|Компилирует сбору для запуска в 64-разрядной среде CLR на компьютере, поддерживающем набор инструкций AMD64 или EM64T.|  
|`Itanium`|Компилирует сбору для запуска в 64-разрядной среде CLR на компьютере с процессором Itanium.|  
|`arm`|Компилирует сбору для запуска на компьютере с процессором ARM.|  
|`anycpu`|Компилирует сбору для запуска на любой платформе. Приложение будет выполняться как 32-разрядное приложение в 32-разрядных версиях Windows и как 64-разрядное приложение в 64-разрядных версиях Windows. Этот флаг — значение по умолчанию.|  
|`anycpu32bitpreferred`|Компилирует сбору для запуска на любой платформе. Приложение будет выполняться как 32-разрядное приложение в 32-разрядных и 64-разрядных версиях Windows. Этот флаг допустим только для исполняемых файлов (. (EXE) и требует наличия .NET Framework 4.5.|  
  
## <a name="remarks"></a>Примечания  
 Используйте параметр `-platform`, чтобы указать процессор назначения для выходного файла.  
  
 В целом, сборки .NET Framework, написанные на Visual Basic, будут работать одинаково вне зависимости от платформы. Тем не менее, в некоторых случаях поведение программ на разных платформах может различаться. Вот эти случаи:  
  
- Структуры, содержащие члены, размер которых изменяется в зависимости от платформы, например, любые типы указателей.  
  
- Арифметика указателя, содержащая постоянные размеры.  
  
- Неверный вызов платформ или объявления СОМ, использующие дескрипторы `Integer` вместо <xref:System.IntPtr>.  
  
- Приведение <xref:System.IntPtr> к `Integer`.  
  
- Использование вызов платформ или взаимодействия СОМ с компонентами, существующими не на всех платформах.  
  
 **-Платформа** параметр позволит устранить некоторые проблемы, если вы знаете, что внесенные предположения об архитектуре, код будет работать на. В частности:  
  
- Если целевой является 64-разрядная платформа, а приложение запущено на 32-разрядном компьютере, сообщение об ошибке появится гораздо раньше и будет более точным, чем сообщение об ошибке, которое появится без этого параметра.  
  
- Если задать флаг `x86` для параметра, а потом запустить приложение на 64-разрядном компьютере, приложение будет запущено в подсистеме WOW, а не непосредственно.  
  
 В 64-разрядной ОС Windows:  
  
- Сборки, скомпилированные с параметром `-platform:x86`, будут выполняться в 32-разрядной среде CLR с WOW64.  
  
- Исполняемые файлы, скомпилированные с параметром `-platform:anycpu`, будут выполняться в 64-разрядной среде CLR.  
  
- Библиотеки DLL, скомпилированные с параметром `-platform:anycpu`, будут выполняться в тоже де среде CLR, что и процесс, загрузивший эти библиотеки.  
  
- Исполняемые файлы, скомпилированные с параметром `-platform:anycpu32bitpreferred`, будут выполняться в 32-разрядной среде CLR.  
  
 Дополнительные сведения о разработке приложений для запуска на 64-разрядной версии Windows, см. в разделе [64-разрядных приложений](../../../framework/64-bit-apps.md).  
  
### <a name="to-set--platform-in-the-visual-studio-ide"></a>Для установки - платформы в Интегрированной среде разработки Visual Studio  
  
1. В **обозревателе решений**, выберите проект, откройте **проекта** меню, а затем щелкните **свойства**.  
  
2. На **компиляции** установите или снимите **предпочтительно 32-разрядных** "флажок", либо в **целевой ЦП** выберите значение.  
  
     Дополнительные сведения см. в разделе [компиляция, конструктор проектов (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic).  
  
## <a name="example"></a>Пример  
 В следующем примере показано использование параметра компилятора `-platform`.  
  
```console
vbc -platform:x86 myFile.vb  
```  
  
## <a name="see-also"></a>См. также

- [/ Target (Visual Basic)](target.md)
- [Компилятор Visual Basic с интерфейсом командной строки](index.md)
- [Примеры командных строк компиляции](sample-compilation-command-lines.md)
