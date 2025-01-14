---
title: Типизированные наборы данных
ms.date: 03/30/2017
ms.assetid: 033d2548-cf24-4c05-8179-67d8b009c048
ms.openlocfilehash: 92ed3f8fd392238785fd2d205668f14fe477f2b8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61607130"
---
# <a name="typed-datasets"></a>Типизированные наборы данных
Наряду с доступом к значениям с поздним связыванием через слабо типизированные переменные, в объекте <xref:System.Data.DataSet> предоставляется доступ к данным на основе принципа строгой типизации. Таблицы и столбцы, которые являются частью **набора данных** может осуществляться с использованием понятных имен и строго типизированных переменных.  
  
 Типизированный **набора данных** — это класс, производный от **набора данных**. Таким образом, он наследует все методы, события и свойства **набора данных**. Кроме того, типизированный **набора данных** предоставляет строго типизированные методы, события и свойства. Это означает, что к таблицам и столбцам можно обращаться путем указания имен вместо использования методов на основе коллекций. Помимо повышения понятности кода, типизированный **набора данных** позволяет редактор автоматическое завершение строк при вводе кода Visual Studio .NET.  
  
 Кроме того, строго типизированные **набора данных** предоставляет доступ к значениям как правильный тип во время компиляции. С помощью строго типизированного **набора данных**, перехватываются ошибки несоответствия типов, когда код компилируется а не во время выполнения.  
  
## <a name="in-this-section"></a>В этом разделе  
 [Создание объектов DataSet со строгой типизацией](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-strongly-typed-datasets.md)  
 Описывает, как создать и использовать строго типизированный **набора данных**.  
  
 [Добавление заметок к типизированным объектам DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/annotating-typed-datasets.md)  
 Описание добавления заметок к схеме определения языка XSD схемы XML, используемый для создания строго типизированного **набора данных**, что позволяет присваивать **набора данных** понятные имена элементов без изменения базовой схемы.  
  
## <a name="see-also"></a>См. также

- [Наборы данных, таблицы данных и объекты DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)
- [Центр разработчиков наборов данных и управляемых поставщиков ADO.NET](https://go.microsoft.com/fwlink/?LinkId=217917)
