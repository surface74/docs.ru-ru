---
title: MULTISET (Entity SQL)
ms.date: 03/30/2017
ms.assetid: eb90a377-e47a-43a5-b308-e993b6d611e6
ms.openlocfilehash: eb676feeb168e1fb184f3869a18e138bff34211b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69929345"
---
# <a name="multiset-entity-sql"></a>MULTISET (Entity SQL)
Создает экземпляр мультинабора из списка значений. Все значения конструктора MULTISET должны принадлежать совместимому типу `T`. Применение пустых конструкторов мультинаборов не допускается.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
MULTISET ( expression [{, expression }] )  
or  
{ expression [{, expression }] }  
```  
  
## <a name="arguments"></a>Аргументы  
 `expression`  
 Любой допустимый список значений.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Коллекция мультинаборов\<типов T >.  
  
## <a name="remarks"></a>Примечания  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] предоставляет три типа конструкторов: конструкторы строк, конструкторы объектов и конструкторы мультинаборов (или коллекций). Дополнительные сведения см. в разделе [Создание типов](../../../../../../docs/framework/data/adonet/ef/language-reference/constructing-types-entity-sql.md).  
  
 Конструктор мультинаборов создает экземпляр мультинабора из списка значений. Все значения конструктора MULTISET должны принадлежать совместимому типу.  
  
 Например, следующее выражение создает мультинабор целых чисел.  
  
 `MULTISET(1, 2, 3)`  
  
 `{1, 2, 3}`  
  
> [!NOTE]
> Вложенные литералы мультинабора поддерживаются только в том случае, если в Мультинаборе с несколькими элементами есть один элемент мультинабора; Например, `{{1, 2, 3}}`. Когда же мультинабор-упаковщик имеет несколько элементов мультинабора (например, `{{1, 2}, {3, 4}}`), вложенные литералы мультинаборов не поддерживаются.  
  
## <a name="example"></a>Пример  
 В следующем запросе Entity SQL оператор MULTISET используется для создания экземпляра мультинабора из списка значений. Запрос основан на модели AdventureWorks Sales. Для компиляции и запуска этого запроса выполните следующие шаги.  
  
1. Выполните процедуру, описанную в [разделе инструкции. Выполнение запроса, возвращающего Структуралтипе](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)результаты.  
  
2. Передайте следующий запрос в качестве аргумента методу `ExecuteStructuralTypeQuery` :  
  
 [!code-csharp[DP EntityServices Concepts 2#MULTISET](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#multiset)]  
  
## <a name="see-also"></a>См. также

- [Сборка типов](../../../../../../docs/framework/data/adonet/ef/language-reference/constructing-types-entity-sql.md)
- [Справочник по Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
