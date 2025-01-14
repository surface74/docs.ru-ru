---
title: Практическое руководство. Проверка совпадения двух объектов же (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], reference
- Is operator [Visual Basic], comparing objects
- reference variables [Visual Basic]
- variables [Visual Basic], referring to same object
- objects [Visual Basic], variables referring to same
- Visual Basic code, operators
ms.assetid: f760e828-8704-4256-bc2d-c22a4c93b524
ms.openlocfilehash: 6301228d786fe55e8851b6207dd84819671656f4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64649682"
---
# <a name="how-to-test-whether-two-objects-are-the-same-visual-basic"></a>Практическое руководство. Проверка совпадения двух объектов же (Visual Basic)
Если у вас есть две переменные, которые ссылаются на объекты, можно использовать либо `Is` или `IsNot` оператора, или оба, чтобы определить, ссылаются ли они на один экземпляр.  
  
### <a name="to-test-whether-two-objects-are-the-same"></a>Для проверки совпадения двух объектов  
  
- Используйте [оператор Is](../../../../visual-basic/language-reference/operators/is-operator.md) или [оператор IsNot](../../../../visual-basic/language-reference/operators/isnot-operator.md) с двумя переменными в качестве операндов.  
  
     [!code-vb[VbVbalrOperators#69](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#69)]  
  
 Может потребоваться выполнить определенные действия в зависимости от того, ссылаются ли два объекта на тот же экземпляр. В предыдущем примере сравнивается управления `c` с активным элементом управления в форме `f`. Если отсутствует активный элемент управления отсутствует, или нет, но он является не тем же экземпляром `c`, а затем `If` инструкция завершается ошибкой и процедура возвращает без дальнейшей обработки.  
  
 Использование `Is` или `IsNot` в зависимости от предпочтений пользователя. Одной может быть более удобным для чтения, чем-то в заданном выражении.  
  
## <a name="see-also"></a>См. также

- [Операторы сравнения в Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)
