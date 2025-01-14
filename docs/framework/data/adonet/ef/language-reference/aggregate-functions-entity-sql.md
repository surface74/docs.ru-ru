---
title: Агрегатные функции (Entity SQL)
ms.date: 03/30/2017
ms.assetid: acfd3149-f519-4c6e-8fe1-b21d243a0e58
ms.openlocfilehash: b01c7dca675e79c61b87bcc1fb30455286db3118
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2019
ms.locfileid: "66489962"
---
# <a name="aggregate-functions-entity-sql"></a>Агрегатные функции (Entity SQL)
Статистическое выражение представляет собой языковую конструкцию, которая сжимает коллекцию в скаляр в составе операции группировки. В языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)] статистические выражения встречаются в двух формах.  
  
- [!INCLUDE[esql](../../../../../../includes/esql-md.md)] функции коллекций, которые могут использоваться в любом месте в выражении. Сюда относится использование агрегатных функций в проекциях и предикатах, применяемых к коллекциям. Функции коллекций — это предпочтительный способ задания статистических функций в [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
- Групповые статистические выражения в выражениях запроса с предложением GROUP BY. Как и в Transact-SQL групповые статистические выражения принимают DISTINCT и ALL в качестве модификаторов входа статистической функции.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] Сначала предпринимается попытка интерпретировать выражение как функцию коллекции и является ли выражение в контексте выражения SELECT он интерпретирует его как групповое статистическое выражение.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] Определяет специальный статистический оператор [GROUPPARTITION](../../../../../../docs/framework/data/adonet/ef/language-reference/grouppartition-entity-sql.md). Этот оператор позволяет получить ссылку на сгруппированный входной набор. Это позволяет выполнять расширенные запросы группирования, в которых результаты предложения GROUP BY могут использоваться в местах, отличных от функций коллекции или группового статистического выражения.  
  
## <a name="collection-functions"></a>Функции коллекции  
 Функции коллекции работают с коллекциями и возвращают скалярное значение. Например, если `orders` - это коллекция всех объектов `orders`, то можно рассчитать самую раннюю дату отгрузки с помощью следующего выражения:  
  
 `min(select value o.ShipDate from LOB.Orders as o)`  
  
## <a name="group-aggregates"></a>Групповые статистические выражения  
 Групповые статистические выражения вычисляются по результату группирования, определенного предложением GROUP BY. Предложение GROUP BY разделяет данные на группы. К каждой группе в результате применяется агрегатная функция, и вычисляется отдельное статистическое выражение с использованием элементов каждой группы в качестве входных значений. Если в выражении SELECT используется предложение GROUP BY, то в проекции, а также предложении HAVING или ORDER BY, могут присутствовать только имена выражений группирования, статистические функции или константные выражения.  
  
 В следующем примере вычисляется средняя величина заказа для каждого продукта.  
  
 `select p, avg(ol.Quantity) from LOB.OrderLines as ol`  
  
 `group by ol.Product as p`  
  
 В выражении SELECT может присутствовать групповое статистическое выражение без явно заданного предложения GROUP BY. Все элементы при этом рассматриваются как одна группа, что эквивалентно определению группирования на основе константы.  
  
 `select avg(ol.Quantity) from LOB.OrderLines as ol`  
  
 `select avg(ol.Quantity) from LOB.OrderLines as ol group by 1`  
  
 Выражения, используемые в предложении GROUP BY, вычисляются в той же области разрешения имен, которая является видимой для выражения предложения WHERE.  
  
## <a name="see-also"></a>См. также

- [Функции](../../../../../../docs/framework/data/adonet/ef/language-reference/functions-entity-sql.md)
