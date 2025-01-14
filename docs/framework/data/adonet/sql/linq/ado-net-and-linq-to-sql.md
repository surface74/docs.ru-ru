---
title: ADO.NET и LINQ to SQL
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 49ac6da0-f2e1-46fa-963e-1b6dcb63fef7
ms.openlocfilehash: b47a46f9fd9ef3ef1935fa7a88c2e60fe80db09d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964128"
---
# <a name="adonet-and-linq-to-sql"></a>ADO.NET и LINQ to SQL
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]является частью семейства технологий ADO.NET. Он основан на службах, предоставляемых моделью поставщика ADO.NET. Таким образом, можно [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] смешивать код с существующими ADO.NET приложениями и переносить текущие [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]решения ADO.NET в. На следующем рисунке показано общее представление связи.  
  
 ![LINQ to SQL и ADO.NET](../../../../../../docs/framework/data/adonet/sql/linq/media/dlinq-3.png "DLinq_3")  
  
## <a name="connections"></a>Подключения  
 При создании [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.DataContext>можно указать существующее подключение ADO.NET. Все операции с <xref:System.Data.Linq.DataContext> (включая запросы) используют это предоставленное соединение. Если подключение уже открыто, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] оставляет его как есть после завершения работы с ним.  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#4)]
 [!code-vb[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#4)]  
  
 Для постоянного доступа к подключению и его закрытия можно использовать свойство <xref:System.Data.Linq.DataContext.Connection%2A>, как показано в следующем коде.  
  
 [!code-csharp[DLinqAdoNet#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#1)]
 [!code-vb[DLinqAdoNet#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#1)]  
  
## <a name="transactions"></a>Транзакции  
 Когда приложение уже инициировало транзакцию и в нее требуется включить <xref:System.Data.Linq.DataContext>, его можно добавить в собственную транзакцию базы данных<xref:System.Data.Linq.DataContext>.  
  
 Предпочтительным методом выполнения транзакций с .NET Framework является использование <xref:System.Transactions.TransactionScope> объекта. Благодаря этому способу можно выполнить распределенные транзакции, работающие в базах данных и других находящихся в памяти диспетчерах ресурсов. Для запуска транзакций требуется незначительное количество ресурсов. Они преобразуются в распределенные транзакции только при наличии в области действия транзакции нескольких подключений.  
  
 [!code-csharp[DLinqAdoNet#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#2)]
 [!code-vb[DLinqAdoNet#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#2)]  
  
 Этот способ не подходит для всех баз данных. Например, соединение SqlClient не может повысить системные транзакции, если оно работает с сервером SQL Server 2000. Наоборот, оно автоматически включается в полную, распределенную транзакцию при каждом обнаружении используемой области действия транзакции.  
  
## <a name="direct-sql-commands"></a>Прямые команды SQL  
 Иногда могут возникать ситуации, когда возможность <xref:System.Data.Linq.DataContext> осуществлять запросы или отправлять изменения будет недостаточной для выполнения специализированной задачи. В подобных случаях, чтобы запустить команды SQL в базе данных и преобразовать результаты запроса в объекты, можно использовать метод <xref:System.Data.Linq.DataContext.ExecuteQuery%2A>.  
  
 Например, предположим, что данные для класса `Customer` распределены по двум таблицам (customer1 и customer2). Следующий запрос возвращает последовательность двух объектов `Customer`.  
  
 [!code-csharp[DLinqAdoNet#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#3)]
 [!code-vb[DLinqAdoNet#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#3)]  
  
 При условии, что имена столбцов в табличных результатах соответствуют свойствам столбца класса сущностей [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] , создает объекты из любого SQL запроса.  
  
### <a name="parameters"></a>Параметры  
 Метод <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> допускает использование параметров. В следующем коде выполняется параметризованный запрос.  
  
 [!code-csharp[DlinqAdoNet#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#4)]
 [!code-vb[DlinqAdoNet#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#4)]  
  
> [!NOTE]
> Параметры записываются в тексте запроса с использованием той же нотации с фигурными скобками, что и в методах `Console.WriteLine()` и `String.Format()`. Метод `String.Format()` принимает указанную строку запроса и заменяет параметры в фигурных скобках на автоматически созданные имена, такие как `@p0`, `@p1`…, `@p(n)`.  
  
## <a name="see-also"></a>См. также

- [Основные сведения](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)
- [Практическое руководство. Повторное использование соединения между командой ADO.NET и DataContext](../../../../../../docs/framework/data/adonet/sql/linq/how-to-reuse-a-connection-between-an-ado-net-command-and-a-datacontext.md)
