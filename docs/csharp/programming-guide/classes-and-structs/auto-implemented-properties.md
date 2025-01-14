---
title: Руководство по программированию на C#. Автоматически реализуемые свойства
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- auto-implemented properties [C#]
- properties [C#], auto-implemented
ms.assetid: aa55fa97-ccec-431f-b5e9-5ac789fd32b7
ms.openlocfilehash: 44f3beb9de8c9d339c42db26bb9c510998abc7d7
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2019
ms.locfileid: "69597134"
---
# <a name="auto-implemented-properties-c-programming-guide"></a>Автоматически реализуемые свойства (Руководство по программированию на C#)
В C# 3.0 и более поздних версиях автоматически реализуемые свойства делают объявление свойств более лаконичным, когда в методах доступа к свойствам не требуется дополнительная логика. Они также позволяют клиентскому коду создавать объекты. При объявлении свойства, как показано в следующем примере, компилятор создает закрытое анонимное резервное поле, которое может быть доступно только через методы доступа `get` и `set` свойства.  
  
## <a name="example"></a>Пример  
 В следующем примере показан простой класс, имеющий несколько автоматически реализуемых свойств.  
  
 [!code-csharp[csProgGuideLINQ#28](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#28)]  
  
 В C# 6 и более поздних версиях можно инициализировать автоматически реализуемые свойства аналогично полям.  
  
```csharp  
public string FirstName { get; set; } = "Jane";  
```  
  
 Класс, который показан в предыдущем примере, является изменяемым. Клиентский код может изменить значения в объектах после их создания. В сложных классах, которые содержат значительные возможности (методы) и данные, часто необходимо иметь открытые свойства. Однако для небольших классов или структур, которые просто инкапсулируют набор значений (данных) и имеют мало функциональных возможностей или совсем их не имеют, вы должны сделать объекты неизменяемыми либо путем объявления метода доступа set как [закрытого](../../language-reference/keywords/private.md) (неизменяемого для потребителей), либо путем объявления только метода доступа get (неизменяемого везде, кроме конструктора).  Дополнительные сведения см. в разделе [Практическое руководство. реализации облегченного класса с автоматически реализуемыми свойствами](./how-to-implement-a-lightweight-class-with-auto-implemented-properties.md).  
  
## <a name="see-also"></a>См. также

- [Свойства](./properties.md)
- [Модификаторы](../../language-reference/keywords/modifiers.md)
