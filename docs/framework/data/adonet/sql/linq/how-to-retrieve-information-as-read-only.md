---
title: Практическое руководство. Как получать информацию в режиме только для чтения
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fb09e298-0b53-47e5-97fb-ab318bcd4fad
ms.openlocfilehash: b98c5e6ea49695015eb566ca2176b23c5260017a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69928709"
---
# <a name="how-to-retrieve-information-as-read-only"></a>Практическое руководство. Как получать информацию в режиме только для чтения
Если не планируется изменять данные, можно повысить производительность запросов за счет поиска результатов, предназначенных только для чтения.  
  
 Чтобы реализовать обработку запросов только для чтения, установите для свойства <xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A> значение `false`.  
  
> [!NOTE]
> Если для свойства <xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A> установлено значение `false`, то для свойства <xref:System.Data.Linq.DataContext.DeferredLoadingEnabled%2A> неявно устанавливается значение `false`.  
  
## <a name="example"></a>Пример  
 В следующем примере кода извлекается коллекция дат приема на работу сотрудников, предназначенная только для чтения.  
  
 [!code-csharp[DLinqQuerying#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#2)]
 [!code-vb[DLinqQuerying#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#2)]  
  
## <a name="see-also"></a>См. также

- [Основные принципы запросов](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)
- [Запрос к базе данных](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md)
- [Отложенная и немедленная загрузка](../../../../../../docs/framework/data/adonet/sql/linq/deferred-versus-immediate-loading.md)
