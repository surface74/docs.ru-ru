---
title: Практическое руководство. Как сопоставлять связи баз данных
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 538def39-8399-46fb-b02d-60ede4e050af
ms.openlocfilehash: 42e7a715c8137574bff617715c1f174314080131
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69943610"
---
# <a name="how-to-map-database-relationships"></a>Практическое руководство. Как сопоставлять связи баз данных
Отношения данных, которые всегда останутся неизменными, можно закодировать в виде ссылок в классе сущностей. В учебной базе данных Northwind, всегда существует связь между заказчиками и их заказами, т.к. обычно заказчики размещают заказы.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]<xref:System.Data.Linq.Mapping.AssociationAttribute> определяет атрибут, помогающий представлять подобные связи. Этот атрибут используется совместно с типами <xref:System.Data.Linq.EntitySet%601> и <xref:System.Data.Linq.EntityRef%601> для представления в базе данных связи по внешнему ключу. Дополнительные сведения см. в разделе Атрибут Association в сопоставлении [на основе атрибутов](../../../../../../docs/framework/data/adonet/sql/linq/attribute-based-mapping.md).  
  
> [!NOTE]
> В значениях свойства Storage для атрибутов AssociationAttribute и ColumnAttribute учитывается регистр. Например, следует убедиться в том, что регистр символов в значении, использованном в атрибуте свойства AssociationAttribute.Storage, соответствует регистру символов в соответствующих именах свойств в остальном коде. Это относится ко всем языкам программирования .NET, даже тем, которые обычно не чувствительны к регистру, включая Visual Basic. Дополнительные сведения о свойстве Storage см. в разделе <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A?displayProperty=nameWithType>.  
  
 Большинство связей имеют тип «один ко многим», как и в примере, представленном далее в этом разделе. Отношения "один-к-одному" и "один-ко-многим" можно представить следующим образом.  
  
- Один к одному. Этот тип связей представляется включением элементов <xref:System.Data.Linq.EntitySet%601> с обеих сторон.  
  
     Например `Customer` , рассмотрим - `Customer` связь, созданную таким образом, чтобы код безопасности клиента не найдется в таблице и к нему мог получить доступ только авторизованные лица. `SecurityCode`  
  
- Многие ко многим. В связях «многие ко многим» первичный ключ таблицы компоновки (также называемой связующей таблицей) часто формируется с помощью составных внешних ключей из двух других таблиц.  
  
     Например `Employee` , рассмотрим - `EmployeeProject`связь «многие ко многим», сформированную с помощью Link Table. `Project` [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] требует, чтобы такая связь моделировалась по трем классам: `Employee`, `Project` и `EmployeeProject`. В этом случае изменение отношения между `Employee` и `Project` может потребовать обновления первичного ключа `EmployeeProject`. Однако данная ситуация наилучшим образом моделируется для удаления существующего `EmployeeProject` и создания нового `EmployeeProject`.  
  
    > [!NOTE]
    > Отношения в реляционных базах данных обычно моделируются в виде значений внешнего ключа, ссылающихся на первичные ключи в других таблицах. Для перехода между ними необходимо явно связать две таблицы с помощью операции реляционного *объединения* .  
    >   
    >  Объекты в [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], с другой стороны, ссылаются друг на друга с помощью ссылок на свойства или коллекции ссылок, которые можно перемещать с помощью *точечной* нотации.  
  
## <a name="example"></a>Пример  
 В следующем примере отношения "один-ко-многим" класс `Customer` имеет свойство, объявляющее отношение между клиентами и их заказами.  Свойство `Orders` имеет тип <xref:System.Data.Linq.EntitySet%601>. Этот тип указывает, что данное отношение относится к виду "один-ко-многим" (один клиент - много заказов). Свойство <xref:System.Data.Linq.Mapping.AssociationAttribute.OtherKey%2A> используется для описания установки данной связи, а именно: путем указания в связанном классе имени свойства, которое будет сравниваться с существующим. В этом примере `CustomerID` свойство сравнивается, точно так же, как *соединение* базы данных будет сравнивать это значение столбца.  
  
> [!NOTE]
> При использовании Visual Studio можно использовать реляционный конструктор объектов, чтобы создать ассоциацию между классами.  
  
 [!code-csharp[DlinqCustomize#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCustomize/cs/Program.cs#3)]
 [!code-vb[DlinqCustomize#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCustomize/vb/Module1.vb#3)]  
  
## <a name="example"></a>Пример  
 Возможна и обратная ситуация. Для описания ассоциации между клиентами и заказами вместо класса `Customer` можно использовать класс `Order`. Чтобы описать обратную связь с клиентом, класс `Order` использует тип <xref:System.Data.Linq.EntityRef%601>, как показано в следующем примере кода.  
  
> [!NOTE]
> Класс поддерживает *отложенную загрузку.* <xref:System.Data.Linq.EntityRef%601> Дополнительные сведения см. в *разделе* [Отложенная и немедленная загрузка](../../../../../../docs/framework/data/adonet/sql/linq/deferred-versus-immediate-loading.md).  
  
 [!code-csharp[DLinqCustomize#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCustomize/cs/Program.cs#5)]
 [!code-vb[DLinqCustomize#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCustomize/vb/Module1.vb#5)]  
  
## <a name="see-also"></a>См. также

- [Практическое руководство. Настройка классов сущностей с помощью редактора кода](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)
- [Модель объектов LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)
