---
title: Процедура Main в Visual Basic
ms.date: 07/20/2015
f1_keywords:
- vb.Main
helpviewer_keywords:
- Main procedure
- Main method [Visual Basic]
- main function
ms.assetid: f0db283e-f283-4464-b521-b90858cc1b44
ms.openlocfilehash: 19c6fcb04a373d782db3deafc732f69bf20e7f0e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962762"
---
# <a name="main-procedure-in-visual-basic"></a>Процедура Main в Visual Basic
Каждое приложение Visual Basic должно содержать процедуру с именем `Main`. Эта процедура выступает в качестве начальной точки и общего управления для приложения. .NET Framework вызывает `Main` процедуру, когда она загрузила приложение и готова передать ему управление. Если вы не создаете Windows Forms приложение, необходимо написать `Main` процедуру для приложений, выполняемых самостоятельно.

 `Main`содержит код, который выполняется в первую очередь. В `Main`можно определить, какая форма должна загружаться первым при запуске программы, определить, выполняется ли в системе копия приложения, установить набор переменных для приложения или открыть базу данных, требуемую для приложения.

## <a name="requirements-for-the-main-procedure"></a>Требования для основной процедуры
 Файл, который выполняется самостоятельно (обычно с расширением exe), должен содержать `Main` процедуру. Библиотека (например, с расширением DLL) не запускается самостоятельно и не требует `Main` процедуры. Ниже приведены требования к различным типам проектов, которые можно создать.

- Консольные приложения выполняются самостоятельно, и необходимо указать хотя бы одну `Main` процедуру.

- Windows Forms приложения выполняются самостоятельно. Однако компилятор Visual Basic автоматически создает `Main` процедуру в таком приложении, и вам не нужно писать его.

- Библиотеки классов не нуждаются в `Main` процедуре. К ним относятся библиотеки элементов управления Windows и библиотеки веб-элементов управления. Веб-приложения развертываются в виде библиотек классов.

## <a name="declaring-the-main-procedure"></a>Объявление основной процедуры
 Существует четыре способа объявления `Main` процедуры. Он может принимать аргументы, а также не может возвращать значение.

> [!NOTE]
> При объявлении `Main` в классе необходимо `Shared` использовать ключевое слово. В модуле `Main` не обязательно должен быть `Shared`.

- Самый простой способ — объявить `Sub` процедуру, которая не принимает аргументы или не возвращает значение.

    ```vb
    Module mainModule
        Sub Main()
            MsgBox("The Main procedure is starting the application.")
            ' Insert call to appropriate starting place in your code.
            MsgBox("The application is terminating.")
        End Sub
    End Module
    ```

- `Main`также может возвращать `Integer` значение, которое операционная система использует в качестве кода выхода для программы. Другие программы могут протестировать этот код, изучая значение ERRORLEVEL Windows. Чтобы вернуть код выхода, вместо `Main` `Sub` процедуры необходимо объявить `Function` процедуру.

    ```vb
    Module mainModule
        Function Main() As Integer
            MsgBox("The Main procedure is starting the application.")
            Dim returnValue As Integer = 0
            ' Insert call to appropriate starting place in your code.
            ' On return, assign appropriate value to returnValue.
            ' 0 usually means successful completion.
            MsgBox("The application is terminating with error level " &
                 CStr(returnValue) & ".")
            Return returnValue
        End Function
    End Module
    ```

- `Main`также может принимать `String` массив в качестве аргумента. Каждая строка в массиве содержит один из аргументов командной строки, используемых для вызова программы. В зависимости от их значений можно выполнять различные действия.

    ```vb
    Module mainModule
        Function Main(ByVal cmdArgs() As String) As Integer
            MsgBox("The Main procedure is starting the application.")
            Dim returnValue As Integer = 0
            ' See if there are any arguments.
            If cmdArgs.Length > 0 Then
                For argNum As Integer = 0 To UBound(cmdArgs, 1)
                    ' Insert code to examine cmdArgs(argNum) and take
                    ' appropriate action based on its value.
                Next
            End If
            ' Insert call to appropriate starting place in your code.
            ' On return, assign appropriate value to returnValue.
            ' 0 usually means successful completion.
            MsgBox("The application is terminating with error level " &
                 CStr(returnValue) & ".")
            Return returnValue
        End Function
    End Module
    ```

- Можно объявить `Main` , чтобы проверить аргументы командной строки, но не вернуть код выхода, как показано ниже.

    ```vb
    Module mainModule
        Sub Main(ByVal cmdArgs() As String)
            MsgBox("The Main procedure is starting the application.")
            Dim returnValue As Integer = 0
            ' See if there are any arguments.
            If cmdArgs.Length > 0 Then
                For argNum As Integer = 0 To UBound(cmdArgs, 1)
                    ' Insert code to examine cmdArgs(argNum) and take
                    ' appropriate action based on its value.
                Next
            End If
            ' Insert call to appropriate starting place in your code.
            MsgBox("The application is terminating.")
        End Sub
    End Module
    ```
  
## <a name="see-also"></a>См. также

- <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>
- <xref:System.Array.Length%2A>
- <xref:Microsoft.VisualBasic.Information.UBound%2A>
- [Структура программы Visual Basic](../../../visual-basic/programming-guide/program-structure/structure-of-a-visual-basic-program.md)
- [/main](../../../visual-basic/reference/command-line-compiler/main.md)
- [Общие](../../../visual-basic/language-reference/modifiers/shared.md)
- [Оператор Sub](../../../visual-basic/language-reference/statements/sub-statement.md)
- [Оператор Function](../../../visual-basic/language-reference/statements/function-statement.md)
- [Тип данных Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md)
- [Тип данных String](../../../visual-basic/language-reference/data-types/string-data-type.md)
