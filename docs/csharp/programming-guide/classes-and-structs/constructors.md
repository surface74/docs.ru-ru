---
title: Руководство по программированию на C#. Конструкторы
ms.custom: seodec18
ms.date: 05/05/2017
helpviewer_keywords:
- constructors [C#]
- classes [C#], constructors
- C# language, constructors
ms.assetid: df2e2e9d-7998-418b-8e7d-890c17ff6c95
ms.openlocfilehash: ea780fc983ed46c8a5ccb54ab618d1a0a2a928d1
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2019
ms.locfileid: "69597099"
---
# <a name="constructors-c-programming-guide"></a>Конструкторы (Руководство по программированию на C#)

Каждый раз, когда создается [класс](../../language-reference/keywords/class.md) или [структура](../../language-reference/keywords/struct.md), вызывается конструктор. Класс или структура может иметь несколько конструкторов, принимающих различные аргументы. Конструкторы позволяют программисту задавать значения по умолчанию, ограничивать число установок и писать код, который является гибким и удобным для чтения. Дополнительные сведения и примеры см. в разделах [Использование конструкторов](./using-constructors.md) и [Конструкторы экземпляров](./instance-constructors.md).  

## <a name="parameterless-constructors"></a>Конструкторы без параметров
  
Если не предоставить конструктор для класса, C# создаст конструктор по умолчанию, который создает экземпляр объекта и задаст переменным-членам значения по умолчанию, как показано в разделе [Таблица значений по умолчанию](../../language-reference/keywords/default-values-table.md). Если не предоставить конструктор для структуры, C# будет использовать *неявный конструктор без параметров*, чтобы автоматически инициализировать каждое поле значением по умолчанию для данного типа согласно разделу [Таблица значений по умолчанию](../../language-reference/keywords/default-values-table.md). Дополнительные сведения и примеры см. в разделе [Конструкторы экземпляров](./instance-constructors.md).  

## <a name="constructor-syntax"></a>Синтаксис конструктора

Конструктор — это метод, имя которого совпадает с именем его типа. Его сигнатура метода содержит только имя метода и список параметров. Она не содержит возвращаемый тип. В приведенном ниже примере демонстрируется конструктор для класса с именем `Person`.

[!code-csharp[constructors](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/constructors1.cs#1)]  

Если конструктор поддерживает реализацию в виде оператора, можно использовать [определение тела выражения](../statements-expressions-operators/expression-bodied-members.md). В следующем примере определяется класс `Location`, конструктор которого имеет один строковый параметр *name*. Определение тела выражения присваивает аргумент полю `locationName`.

[!code-csharp[expression-bodied-constructor](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/expr-bodied-ctor.cs#1)]  

## <a name="static-constructors"></a>Статические конструкторы

В приведенных выше примерах показаны конструкторы экземпляров, которые создают новый объект. В классе или структуре также может быть статический конструктор, который инициализирует статические члены типа.  Статические конструкторы не имеют параметров. Если вы не предоставили статический конструктор для инициализации статических полей, компилятор C# инициализирует статические поля значениями по умолчанию, которые указаны в [таблице значений по умолчанию](../../language-reference/keywords/default-values-table.md).

В следующем примере статический конструктор используется для инициализации статического поля.

[!code-csharp[constructors](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/constructors1.cs#2)]  

Можно также определить статический конструктор с помощью определения тела выражения, как показано в следующем примере. 

[!code-csharp[constructors](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/constructors1.cs#3)]  

Дополнительные сведения и примеры см. в разделе [Статические конструкторы](./static-constructors.md).  
  
## <a name="in-this-section"></a>В этом разделе  
 [Использование конструкторов](./using-constructors.md)  
  
 [Конструкторы экземпляров](./instance-constructors.md)  
  
 [Закрытые конструкторы](./private-constructors.md)  
  
 [Статические конструкторы](./static-constructors.md)  
  
 [Практическое руководство. Создание конструктора копий](./how-to-write-a-copy-constructor.md)  
  
## <a name="see-also"></a>См. также

- [Руководство по программированию на C#](../index.md)
- [Классы и структуры](./index.md)
- [Методы завершения](./destructors.md)
- [static](../../language-reference/keywords/static.md)
- [Why Do Initializers Run In The Opposite Order As Constructors? Part One](https://blogs.msdn.microsoft.com/ericlippert/2008/02/15/why-do-initializers-run-in-the-opposite-order-as-constructors-part-one) (Почему инициализаторы выполняются в порядке, обратном действию конструкторов? Часть 1)
