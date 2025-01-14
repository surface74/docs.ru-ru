---
title: 'Инициализаторы объектов: Именованные и анонимные типы (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.ObjectInitializer
helpviewer_keywords:
- object initializers [Visual Basic]
- anonymous types [Visual Basic], object initializers
- initializing properties [Visual Basic]
- initializers [Visual Basic]
- named types [Visual Basic]
ms.assetid: e2df3807-a70f-49dd-ac94-f1e07f472b1b
ms.openlocfilehash: e1f461cc98fb104f78a6c83a207cff7f4eda9227
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046453"
---
# <a name="object-initializers-named-and-anonymous-types-visual-basic"></a>Инициализаторы объектов: Именованные и анонимные типы (Visual Basic)
Инициализаторы объектов позволяют задавать свойства для сложного объекта с помощью одного выражения. Они могут использоваться для создания экземпляров именованных типов и анонимных типов.  
  
## <a name="declarations"></a>Объявления  
 Объявления экземпляров именованных и анонимных типов могут выглядеть почти одинаково, но их последствия не совпадают. Каждая категория имеет свои возможности и ограничения. В следующем примере показан удобный способ объявления и инициализации экземпляра именованного класса `Customer`с помощью списка инициализаторов объектов. Обратите внимание, что имя класса указывается после ключевого слова `New`.  
  
 [!code-vb[VbVbalrObjectInit#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#1)]  
  
 Анонимный тип не имеет имени. Поэтому создание экземпляра анонимного типа не может включать имя класса.  
  
 [!code-vb[VbVbalrObjectInit#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#2)]  
  
 Требования и результаты двух объявлений не совпадают. Для `namedCust`класс, имеющий `Name` свойство, должен уже существовать, а объявление создает экземпляр этого класса. `Customer` Для `anonymousCust`компилятор определяет новый класс, который имеет одно свойство, строку с именем `Name`и создает новый экземпляр этого класса.  
  
## <a name="named-types"></a>Именованные типы  
 Инициализаторы объектов предоставляют простой способ вызова конструктора типа, а затем задают значения некоторых или всех свойств в одной инструкции. Компилятор вызывает соответствующий конструктор для инструкции: конструктор без параметров, если аргументы не представлены, или параметризованный конструктор при отправке одного или нескольких аргументов. После этого заданные свойства инициализируются в том порядке, в котором они представлены в списке инициализаторов.  
  
 Каждая инициализация в списке инициализаторов состоит из присваивания начального значения члену класса. Имена и типы данных элементов определяются при определении класса. В следующих примерах `Customer` класс должен существовать и должен иметь члены с именем `Name` и `City` , которые могут принимать строковые значения.  
  
 [!code-vb[VbVbalrObjectInit#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#3)]  
  
 Кроме того, можно получить тот же результат, используя следующий код:  
  
 [!code-vb[VbVbalrObjectInit#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#4)]  
  
 Каждое из `Customer` этих объявлений эквивалентно следующему примеру, который создает объект с помощью конструктора без параметров, а затем задает начальные значения `Name` для свойств и `City` с помощью элемента `With` баланс.  
  
 [!code-vb[VbVbalrObjectInit#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#5)]  
  
 Если класс содержит параметризованный конструктор, который позволяет отправить значение для `Name`, например, можно `Customer` также объявить и инициализировать объект следующими способами. `Customer`  
  
 [!code-vb[VbVbalrObjectInit#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#6)]  
  
 Не нужно инициализировать все свойства, как показано в следующем коде.  
  
 [!code-vb[VbVbalrObjectInit#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#7)]  
  
 Однако список инициализации не может быть пустым. Неинициализированные свойства сохраняют значения по умолчанию.  
  
### <a name="type-inference-with-named-types"></a>Вывод типа с именованными типами  
 Код для объявления `cust1` можно сократить, объединив инициализаторы объектов и вывод локального типа. Это позволяет опустить `As` предложение в объявлении переменной. Тип данных переменной выводится из типа объекта, созданного назначением. В следующем примере типом `cust6` является. `Customer`  
  
 [!code-vb[VbVbalrObjectInit#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#8)]  
  
### <a name="remarks-about-named-types"></a>Примечания об именованных типах  
  
- Член класса не может быть инициализирован более одного раза в списке инициализаторов объектов. Объявление `cust7` вызывает ошибку.  
  
     [!code-vb[VbVbalrObjectInit#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#9)]  
  
- Элемент может использоваться для инициализации самого себя или другого поля. Если доступ к элементу осуществляется до инициализации, как показано в следующем объявлении для `cust8`, будет использоваться значение по умолчанию. Помните, что при обработке объявления, использующего инициализатор объекта, первое, что происходит, это то, что вызывается соответствующий конструктор. После этого инициализируются отдельные поля в списке инициализаторов. В следующих примерах значение по умолчанию для `Name` `cust8`присваивается, а инициализированное значение присваивается в `cust9`.  
  
     [!code-vb[VbVbalrObjectInit#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#10)]  
  
     В следующем примере параметризованный конструктор используется `cust3` из и `cust4` `cust11`для объявления и инициализации `cust10` и.  
  
     [!code-vb[VbVbalrObjectInit#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#11)]  
  
- Инициализаторы объектов могут быть вложенными. В `AddressClass` следующем примере класс имеет два свойства: `City` и `State`, и `Customer` класс имеет `Address` свойство, которое является экземпляром `AddressClass`.  
  
     [!code-vb[VbVbalrObjectInit#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#12)]  
  
- Список инициализации не может быть пустым.  
  
- Инициализируемый экземпляр не может иметь тип Object.  
  
- Инициализируемые члены класса не могут быть общими членами, членами только для чтения, константами или вызовами методов.  
  
- Инициализируемые члены класса не могут индексироваться или уточняться. В следующих примерах вызываются ошибки компилятора:  
  
     `'' Not valid.`  
  
     `' Dim c1 = New Customer With {.OrderNumbers(0) = 148662}`  
  
     `' Dim c2 = New Customer with {.Address.City = "Springfield"}`  
  
## <a name="anonymous-types"></a>Анонимные типы  
 Анонимные типы используют инициализаторы объектов для создания экземпляров новых типов, которые явно не определены и не имеют имени. Вместо этого компилятор создает тип в соответствии со свойствами, которые вы указываете в списке инициализатора объекта. Так как имя типа не указано, оно называется *анонимным типом*. Например, Сравните следующее объявление с предыдущим для `cust6`.  
  
 [!code-vb[VbVbalrObjectInit#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#13)]  
  
 Единственное отличие состоит в том, что после `New` для типа данных не указано имя. Тем не менее, что происходит совершенно иначе. Компилятор определяет новый анонимный тип, который имеет два свойства: `Name` и `City`и создает экземпляр с указанными значениями. Определение типа определяет типы `Name` и `City` в примере как строки.  
  
> [!CAUTION]
> Имя анонимного типа создается компилятором и может отличаться от компиляции к компиляции. Код не должен использовать имя анонимного типа или полагаться на него.  
  
 Поскольку имя типа недоступно, нельзя использовать `As` предложение для объявления. `cust13` Его тип должен быть определен. Без использования позднего связывания это ограничивает использование анонимных типов локальными переменными.  
  
 Анонимные типы обеспечивают важную поддержку [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] запросов. Дополнительные сведения об использовании анонимных типов в запросах см. в разделе [анонимные типы](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md) и [Введение в LINQ в Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md).  
  
### <a name="remarks-about-anonymous-types"></a>Примечания о анонимных типах  
  
- Как правило, все или большинство свойств в объявлении анонимного типа будут ключевыми свойствами, которые указываются путем ввода ключевого `Key` слова перед именем свойства.  
  
     [!code-vb[VbVbalrObjectInit#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#14)]  
  
     Дополнительные сведения о ключевых свойствах см. в разделе [Key](../../../../visual-basic/language-reference/modifiers/key.md).  
  
- Как и именованные типы, списки инициализаторов для определений анонимных типов должны объявлять хотя бы одно свойство.  
  
     [!code-vb[VbVbalrObjectInit#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#2)]  
  
- При объявлении экземпляра анонимного типа компилятор создает соответствующее определение анонимного типа. Имена и типы данных свойств берутся из объявления экземпляра и включаются компилятором в определение. Свойства не именуются и не определяются заранее, так как они бы были для именованного типа. Их типы выводятся. Нельзя указать типы данных свойств с помощью `As` предложения.  
  
- Анонимные типы также могут устанавливать имена и значения их свойств несколькими другими способами. Например, свойство анонимного типа может принимать как имя, так и значение переменной, а также имя и значение свойства другого объекта.  
  
     [!code-vb[VbVbalrObjectInit#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#15)]  
  
     Дополнительные сведения о параметрах определения свойств в анонимных типах см. в [разделе как Выводит имена и типы свойств в объявлениях](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)анонимного типа.  
  
## <a name="see-also"></a>См. также

- [Вывод локального типа](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [Анонимные типы](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md) (Знакомство с LINQ в Visual Basic)
- [Практическое руководство. Выводит имена и типы свойств в объявлениях анонимных типов](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)
- [Key](../../../../visual-basic/language-reference/modifiers/key.md)
- [Практическое руководство. Объявление объекта с помощью инициализатора объекта](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)
