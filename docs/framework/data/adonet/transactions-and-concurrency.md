---
title: Транзакции и параллельность
ms.date: 03/30/2017
ms.assetid: f46570de-9e50-4fe6-8710-a8c31fa8569b
ms.openlocfilehash: c78031150d9b1209372dece49813dfcf0a03b9d5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965216"
---
# <a name="transactions-and-concurrency"></a>Транзакции и параллельность
Транзакция состоит из одной команды или группы команд, которые выполняются как пакет. Транзакции позволяют объединить несколько операций в одну единицу работы. Если в какой-либо точке транзакции возникает ошибка, может быть выполнен откат всех обновлений к их состоянию до начала транзакции.  
  
 Для обеспечения согласованности данных транзакция должна соответствовать свойствам ACID (атомарность, согласованность, изоляция и устойчивость). Большая часть систем реляционных баз данных, таких как Microsoft SQL Server, поддерживает транзакции, предоставляя блокировку, ведение журнала и средства управления транзакцией при выполнении клиентским приложением операций обновления, вставки или удаления.  
  
> [!NOTE]
> Транзакции, которые задействуют множество ресурсов, могут снизить параллелизм, если слишком долго удерживают блокировки. Поэтому транзакции следует делать как можно короче.  
  
 В том случае, если в транзакции участвует несколько таблиц одной базы данных или одного сервера, явные транзакции в хранимых процедурах часто выполняются лучше. Транзакции можно создавать в хранимых процедурах SQL Server с использованием инструкций Transact-SQL `BEGIN TRANSACTION`, `COMMIT TRANSACTION` и `ROLLBACK TRANSACTION`. Дополнительные сведения см. в электронной документации по SQL Server.  
  
 Для транзакций, включающих различные диспетчеры ресурсов, например транзакцию между SQL Server и Oracle, требуется распределенная транзакция.  
  
## <a name="in-this-section"></a>В этом разделе  
 [Локальные транзакции](../../../../docs/framework/data/adonet/local-transactions.md)  
 Демонстрирует выполнение транзакций на базе данных.  
  
 [Распределенные транзакции](../../../../docs/framework/data/adonet/distributed-transactions.md)  
 Описывает выполнение распределенных транзакций в ADO.NET.  
  
 [Интеграция System.Transactions с SQL Server](../../../../docs/framework/data/adonet/system-transactions-integration-with-sql-server.md)  
 Описывает <xref:System.Transactions> интеграцию с SQL Server для работы с распределенными транзакциями.  
  
 [Оптимистическая блокировка](../../../../docs/framework/data/adonet/optimistic-concurrency.md)  
 Описывается оптимистичный и пессимистичный параллелизм и проверка на выявление нарушений параллелизма.  
  
## <a name="see-also"></a>См. также

- [Основные сведения о транзакциях](../../../../docs/framework/data/transactions/transaction-fundamentals.md)
- [Подключение к источнику данных](../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)
- [Команды и параметры](../../../../docs/framework/data/adonet/commands-and-parameters.md)
- [Объекты DataAdapter и DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)
- [DbProviderFactories](../../../../docs/framework/data/adonet/dbproviderfactories.md)
- [Центр разработчиков наборов данных и управляемых поставщиков ADO.NET](https://go.microsoft.com/fwlink/?LinkId=217917)
