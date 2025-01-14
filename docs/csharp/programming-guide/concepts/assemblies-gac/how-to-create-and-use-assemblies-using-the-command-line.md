---
title: Практическое руководство. Создание и использование сборок с помощью командной строки (C#)
ms.date: 07/20/2015
ms.assetid: 408ddce3-89e3-4e12-8353-34a49beeb72b
ms.openlocfilehash: 0a8db22a05d834d15f6e6b7f049f59f86bc1fe1d
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2019
ms.locfileid: "69595964"
---
# <a name="how-to-create-and-use-assemblies-using-the-command-line-c"></a>Практическое руководство. Создание и использование сборок с помощью командной строки (C#)
Сборка (или библиотека динамической компоновки (DLL)) связывается с программой во время выполнения. Сборка и использование библиотеки DLL рассматривается в следующем сценарии:  
  
- `MathLibrary.DLL`: Файл библиотеки с методами, вызываемыми во время выполнения. В этом примере библиотека DLL содержит два метода: `Add` и `Multiply`.  
  
- `Add`: Исходный файл с методом `Add`. Он возвращает сумму своих параметров. Класс `AddClass` с методом `Add` является членом пространства имен `UtilityMethods`.  
  
- `Mult`: Исходный код, содержащий метод `Multiply`. Он возвращает результат своих параметров. Класс `MultiplyClass` с методом `Multiply` также является членом пространства имен `UtilityMethods`.  
  
- `TestCode`: Файл с методом `Main`. Он использует методы в DLL-файле для вычисления суммы и результата аргументов времени выполнения.  
  
## <a name="example"></a>Пример  
  
```csharp  
// File: Add.cs   
namespace UtilityMethods  
{  
    public class AddClass   
    {  
        public static long Add(long i, long j)   
        {   
            return (i + j);  
        }  
    }  
}  
```  
  
```csharp  
// File: Mult.cs  
namespace UtilityMethods   
{  
    public class MultiplyClass  
    {  
        public static long Multiply(long x, long y)   
        {  
            return (x * y);   
        }  
    }  
}  
```  
  
```csharp  
// File: TestCode.cs  
  
using UtilityMethods;  
  
class TestCode  
{  
    static void Main(string[] args)   
    {  
        System.Console.WriteLine("Calling methods from MathLibrary.DLL:");  
  
        if (args.Length != 2)  
        {  
            System.Console.WriteLine("Usage: TestCode <num1> <num2>");  
            return;  
        }  
  
        long num1 = long.Parse(args[0]);  
        long num2 = long.Parse(args[1]);  
  
        long sum = AddClass.Add(num1, num2);  
        long product = MultiplyClass.Multiply(num1, num2);  
  
        System.Console.WriteLine("{0} + {1} = {2}", num1, num2, sum);  
        System.Console.WriteLine("{0} * {1} = {2}", num1, num2, product);  
    }  
}  
/* Output (assuming 1234 and 5678 are entered as command-line arguments):  
    Calling methods from MathLibrary.DLL:  
    1234 + 5678 = 6912  
    1234 * 5678 = 7006652          
*/  
```  
  
 Этот файл содержит алгоритм, использующий методы DLL `Add` и `Multiply`. Алгоритм начинается с разбора аргументов, введенных в командной строке: `num1` и `num2`. Затем он вычисляет сумму с помощью метода `Add` в классе `AddClass` и результат с помощью метода `Multiply` в классе `MultiplyClass`.  
  
 Следует отметить, что директива `using` в начале файла позволяет использовать неполные имена классов для ссылки на методы DLL во время компиляции, как показано ниже.  
  
```csharp  
MultiplyClass.Multiply(num1, num2);  
```  
  
 В противном случае потребуется использовать полные имена, как показано ниже.  
  
```csharp  
UtilityMethods.MultiplyClass.Multiply(num1, num2);  
```  
  
## <a name="execution"></a>Выполнение  
 Для запуска программы введите имя EXE-файла и два числа, как показано далее.  
  
 `TestCode 1234 5678`  
  
## <a name="see-also"></a>См. также

- [Руководство по программированию на C#](../../index.md)
- [Сборки в .NET](../../../../standard/assembly/index.md)
- [Создание класса, содержащего функции DLL](../../../../framework/interop/creating-a-class-to-hold-dll-functions.md)
