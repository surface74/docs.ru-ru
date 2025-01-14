---
title: Абстрактные классы
description: Сведения о F# абстрактных классах, которые оставляют некоторые или все члены нереализованными и представляют общие функциональные возможности различных наборов типов объектов.
ms.date: 05/16/2016
ms.openlocfilehash: a6bbfc23b858d5f3833f3f52b6dca46753080f03
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/30/2019
ms.locfileid: "68629678"
---
# <a name="abstract-classes"></a>Абстрактные классы

*Абстрактные классы* — это классы, которые оставляют некоторые или все элементы нереализованными, чтобы реализации могли предоставляться производными классами.

## <a name="syntax"></a>Синтаксис

```fsharp
// Abstract class syntax.
[<AbstractClass>]
type [ accessibility-modifier ] abstract-class-name =
[ inherit base-class-or-interface-name ]
[ abstract-member-declarations-and-member-definitions ]

// Abstract member syntax.
abstract member member-name : type-signature
```

## <a name="remarks"></a>Примечания

В объектно-ориентированном программировании абстрактный класс используется в качестве базового класса иерархии и представляет общие функциональные возможности различных наборов типов объектов. Как предполагает имя "abstract", абстрактные классы часто не соответствуют конкретным сущностям в области, в которой возникла проблема. Однако они показывают, сколько различных конкретных сущностей встречается чаще всего.

Абстрактные классы должны иметь `AbstractClass` атрибут. Они могут иметь реализованные и нереализованные члены. Использование термина *abstract* при применении к классу аналогично условию в других языках .NET; Однако использование термина *abstract* при применении к методам (и свойствам) немного отличается F# от его использования в других языках .NET. В F#при условии, что метод помечен с `abstract` помощью ключевого слова, это означает, что элемент имеет запись, называемую *виртуальным слотом диспетчеризации*, во внутренней таблице виртуальных функций для этого типа. Иными словами, метод является виртуальным, хотя `virtual` ключевое слово не используется в F# языке. Ключевое `abstract` слово используется в виртуальных методах независимо от того, реализован ли метод. Объявление виртуального слота диспетчеризации отделено от определения метода для этого слота диспетчеризации. Таким образом, F# эквивалент объявления виртуального метода и определения в другом языке .NET является сочетанием объявления абстрактного метода и отдельного определения с `default` ключевым словом или `override` ключевым словом. Дополнительные сведения и примеры см. в разделе [методы](./members/methods.md).

Класс считается абстрактным, только если существуют абстрактные методы, которые объявлены, но не определены. Поэтому классы, имеющие абстрактные методы, не обязательно являются абстрактными классами. Если класс не имеет неопределенных абстрактных методов, не используйте атрибут **абстракткласс** .

В предыдущем синтаксисе *Модификатор Accessibility* может иметь `public` `private` значение или `internal`. Дополнительные сведения см. в статье [Управление доступом](access-control.md).

Как и в случае с другими типами, абстрактные классы могут иметь базовый класс и один или несколько базовых интерфейсов. Каждый базовый класс или интерфейс отображается в отдельной строке вместе с `inherit` ключевым словом.

Определение типа абстрактного класса может содержать полностью определенные члены, но оно также может содержать абстрактные члены. Синтаксис абстрактных элементов показан отдельно в предыдущем синтаксисе. В этом синтаксисе *сигнатура типа* элемента является списком, который содержит типы параметров в порядке и возвращаемые типы, разделенные токенами и `->` (или `*` ) маркерами в соответствии с переданным и кортежными параметрами. Синтаксис сигнатур типов абстрактных элементов такой же, как и в файлах сигнатур, которые отображаются в IntelliSense в редакторе Visual Studio Code.

В следующем коде показана абстрактная фигура класса, которая имеет два неабстрактных производных класса: квадратные и круговые. В примере показано, как использовать абстрактные классы, методы и свойства. В примере фигура абстрактного класса представляет общие элементы конкретных сущностей Circle и Square. Общие функции всех фигур (в двухмерной системе координат) являются абстрактными в классе Shape: положение в сетке, угол поворота, а также свойства области и периметра. Они могут быть переопределены, за исключением расположения, поведения отдельных фигур, которые не могут изменяться.

Метод вращения можно переопределить, как в классе Circle, который является неизменяемым в связи с его симметрией. Поэтому в классе Circle метод вращения заменяется методом, который ничего не делает.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2901.fs)]

**Выходные данные:**

```
Perimeter of square with side length 10.000000 is 40.000000
Circumference of circle with radius 5.000000 is 31.415927
Area of Square: 100.000000
Area of Circle: 78.539816
```

## <a name="see-also"></a>См. также

- [Классы](classes.md)
- [Члены](./members/index.md)
- [Методы](./members/methods.md)
- [Свойства](./members/Properties.md)
