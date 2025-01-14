---
title: Руководство по программированию на C#. Модификаторы доступа
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# Language, access modifiers
- access modifiers [C#], about
ms.assetid: 6e81ee82-224f-4a12-9baf-a0dca2656c5b
ms.openlocfilehash: 266ece1e63bf6d32bf59406dbc72a9e6bd92eb45
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924543"
---
# <a name="access-modifiers-c-programming-guide"></a>Модификаторы доступа (Руководство по программированию в C#)
Все типы и члены имеют уровень доступности, определяющий возможность их использования из другого кода в вашей или в других сборках. Следующие модификаторы доступа позволяют указать доступность типа или члена при объявлении:  
  
 [public](../../language-reference/keywords/public.md)  
 Доступ к типу или члену возможен из любого другого кода в той же сборке или другой сборке, ссылающейся на него. 
  
 [private](../../language-reference/keywords/private.md)  
 Доступ к типу или члену возможен только из кода в том же классе или структуре.  
  
 [protected](../../language-reference/keywords/protected.md)  
 Доступ к типу или члену возможен только из кода в том же классе либо в классе, производном от этого класса.  
 [internal](../../language-reference/keywords/internal.md)  
 Доступ к типу или члену возможен из любого кода в той же сборке, но не из другой сборки.  
  
 [protected internal](../../language-reference/keywords/protected-internal.md) Доступ к типу или члену возможен из любого кода в той сборке, где он был объявлен, или из производного класса в другой сборке. 

 [private protected](../../language-reference/keywords/private-protected.md) Доступ к типу или члену возможен только из его объявляющей сборки из кода в том же классе либо в типе, производном от этого класса.
  
 В следующих примерах показано, как изменить модификаторы доступа для типа или члена типа:  
  
 [!code-csharp[csProgGuideObjects#72](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#72)]  
  
 Не все модификаторы доступа могут использоваться всеми типами или членами типов во всех контекстах, а в некоторых случаях доступность члена типа ограничивается доступностью типа, в котором он содержится. Следующие подразделы содержат дополнительные сведения о доступности.  
  
## <a name="class-and-struct-accessibility"></a>Доступность классов и структур  
 Классы и структуры, объявленные непосредственно в пространстве имен (другими словами, не вложенные в другие классы или структуры), могут быть открытыми или внутренними. Если модификатор доступа не указан, по умолчанию используется внутренний тип.  
  
 Члены структуры, включая вложенные классы и структуры, могут объявляться как открытые, внутренние или закрытые. Члены класса, включая вложенные классы и структуры, могут объявляться как открытые, защищенные внутренние, защищенные, внутренние, защищенные закрытые или закрытые. По умолчанию уровень доступа к членам класса и членам структуры, включая вложенные классы и структуры, является закрытым. Закрытые вложенные типы недоступны за пределами типа, в котором содержатся.  
  
 Производные классы не могут быть более доступны, чем соответствующие базовые типы. Другими словами, нельзя иметь открытый класс `B`, производный от внутреннего класса `A`. Если бы это было возможно, класс `A` стал бы открытым, поскольку все защищенные или внутренние члены класса `A` были бы доступны из производного класса.  
  
 Доступ к внутренним типам можно предоставить некоторым другим сборкам с помощью класса InternalsVisibleToAttribute. Дополнительные сведения см. в разделе [Дружественные сборки](../../../standard/assembly/friend-assemblies.md).  
  
## <a name="class-and-struct-member-accessibility"></a>Доступность членов классов и структур  
 Члены класса (включая вложенные классы и структуры) можно объявлять с любым из шести типов доступа. Члены структуры нельзя объявлять как защищенные, поскольку структуры не поддерживают наследование.  
  
 Как правило, уровень доступности члена не может быть выше уровня доступности типа, в который он входит. При этом открытый член внутреннего класса может быть доступен за пределами сборки, если он реализует методы интерфейса или переопределяет виртуальные методы, определенные в открытом базовом классе.  
  
 Тип любого члена, который является полем, свойством или событием, должен иметь, как минимум, такой же уровень доступности, как у самого члена. Точно так же тип возвращаемого значения и типы параметров любого члена, который является методом, индексатором или делегатом, должен иметь, как минимум, такой же уровень доступности, как у самого члена. Например, нельзя иметь открытый метод `M`, возвращающий класс `C`, если `C` не является также открытым. Аналогичным образом нельзя иметь защищенное свойство типа `A`, если `A` объявлен как закрытый.  
  
 Пользовательские операторы всегда должны объявляться как открытые и статические. Для получения дополнительной информации см. раздел [Перегрузка операторов](../../language-reference/operators/operator-overloading.md).  
  
 Методы завершения не могут иметь модификаторы доступа.  
  
 Чтобы настроить уровень доступа для члена класса или структуры, добавьте в объявление этого члена соответствующее ключевое слово, как показано в следующем примере.  
  
 [!code-csharp[csProgGuideObjects#73](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#73)]  
  
> [!NOTE]
> Защищенный внутренний уровень доступности означает защищенный ИЛИ внутренний доступ, а не защищенный И внутренний. Другими словами, защищенный внутренний член доступен из любого класса в той же сборке, включая производные классы. Чтобы сделать его доступным только для производных классов в той же сборке, объявите сам класс как внутренний, а его члены как защищенные. Кроме того, начиная с C# 7.2, можно использовать защищенные закрытые модификаторы доступа для достижения такого же результата без необходимости преобразования содержащего класса во внутренний.  
  
## <a name="other-types"></a>Другие типы  
 Интерфейсы, объявляемые непосредственно в пространстве имен, могут быть объявлены как открытые или внутренние. Равно как и в случае с классами и структурами, для интерфейсов по умолчанию задается внутренний доступ. Члены интерфейса всегда открыты, поскольку интерфейс как раз и создан для того, чтобы обеспечить доступ к классу или структуре для других типов. Модификаторы доступа к членам интерфейса не применяются.  
  
 Члены перечисления всегда открыты, и модификаторы доступа к ним не применяются.  
  
 Делегаты ведут себя как классы и структуры. По умолчанию они имеют внутренний доступ, если объявляются непосредственно в пространстве имен, и закрытый доступ, если являются вложенными.  
  
## <a name="c-language-specification"></a>Спецификация языка C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>См. также

- [Руководство по программированию на C#](../index.md)
- [Классы и структуры](./index.md)
- [Интерфейсы](../interfaces/index.md)
- [private](../../language-reference/keywords/private.md)
- [public](../../language-reference/keywords/public.md)
- [internal](../../language-reference/keywords/internal.md)
- [protected](../../language-reference/keywords/protected.md)
- [protected internal](../../language-reference/keywords/protected-internal.md)
- [private protected](../../language-reference/keywords/private-protected.md)
- [class](../../language-reference/keywords/class.md)
- [struct](../../language-reference/keywords/struct.md)
- [interface](../../language-reference/keywords/interface.md)
