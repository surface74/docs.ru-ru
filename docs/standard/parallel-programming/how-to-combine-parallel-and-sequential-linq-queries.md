---
title: Практическое руководство. Объединение параллельных и последовательных запросов LINQ
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel queries, combine parallel and sequential
ms.assetid: 1167cfe6-c8aa-4096-94ba-c66c3a4edf4c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 026c7d2be678c4b6aeed4e2e6f9eb43283cd04c1
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988458"
---
# <a name="how-to-combine-parallel-and-sequential-linq-queries"></a>Практическое руководство. Объединение параллельных и последовательных запросов LINQ
Этот пример демонстрирует применение метода <xref:System.Linq.ParallelEnumerable.AsSequential%2A>, который запрашивает последовательную обработку в PLINQ всех последующих операторов текущего запроса. Обычно последовательная обработка выполняется медленнее, чем параллельная, но иногда она необходима, чтобы гарантировать правильные результаты.  
  
> [!WARNING]
> Этот пример предназначен для демонстрации использования и может выполняться не быстрее аналогичного последовательного запроса LINQ to Objects. См. дополнительные сведения об [ускорении выполнения в PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md).  
  
## <a name="example"></a>Пример  
 Следующий пример демонстрирует одну из ситуаций, для которой необходимо <xref:System.Linq.ParallelEnumerable.AsSequential%2A>, поскольку здесь важно сохранить порядок, установленный предыдущим предложением запроса.  
  
 [!code-csharp[PLINQ#24](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#24)]
 [!code-vb[PLINQ#24](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#24)]  
  
## <a name="compiling-the-code"></a>Компиляция кода  
 Чтобы скомпилировать и запустить этот код, вставьте его в проект [Пример данных PLINQ](../../../docs/standard/parallel-programming/plinq-data-sample.md), добавьте строку с вызовом этого метода из `Main` и нажмите клавишу F5.  
  
## <a name="see-also"></a>См. также

- [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
