---
title: Маршалинг с помощью COM- взаимодействия
ms.date: 09/07/2017
helpviewer_keywords:
- COM interop, data marshaling
- marshaling data, COM interop
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 279310fe7aa17a73d129edf98f3477a00fd50767
ms.sourcegitcommit: 29a9b29d8b7d07b9c59d46628da754a8bff57fa4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/17/2019
ms.locfileid: "69567241"
---
# <a name="marshaling-data-with-com-interop"></a>Маршалинг с помощью COM- взаимодействия
COM-взаимодействие обеспечивает поддержку как для использования COM-объектов из управляемого кода, так и для предоставления доступа к управляемым объектам для COM. Поддержка маршалинга данных в COM и обратно достаточно полная и почти всегда обеспечивает правильное поведение маршалинга.  
  
 Пакет Windows SDK содержит следующие средства COM-взаимодействия:  
  
- [Средство импорта библиотек типов (Tlbimp.exe)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md), которое преобразует библиотеку типов COM в сборку взаимодействия. Эта сборка используется службой маршалинга взаимодействия для создания оболочек, маршалирующих данные между управляемой и неуправляемой памятью.  
  
- [Средство экспорта библиотек типов (Tlbexp.exe)](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md), которое создает библиотеку типов COM из сборки и формирует оболочку, которая выполняет маршалинг при вызовах методов.  
  
 Следующие разделы посвящены процессам настройки оболочек взаимодействий для случаев, когда можно (или необходимо) предоставить упаковщику дополнительную информацию о типах.  
  
## <a name="in-this-section"></a>В этом разделе  
[Практическое руководство. Создание оболочек вручную](how-to-create-wrappers-manually.md)   
Сведения о том, как вручную создать программу-оболочку COM в управляемом исходном коде. 
 
 [Практическое руководство. Миграция DCOM с управляемым кодом в WCF](../../../docs/framework/interop/how-to-migrate-managed-code-dcom-to-wcf.md)  
 Сведения о переносе управляемого кода DCOM в WCF для получения наиболее безопасного решения.  
  
## <a name="related-sections"></a>Связанные разделы  
 [Типы данных COM](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/sak564ww(v=vs.100))  
 Содержит описание соответствующих управляемых и неуправляемых типов данных.  
  
 [Настройка вызываемых оболочек COM](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3bwc828w(v=vs.100))  
 В этой статье описан способ явного маршалинга типов данных с использованием атрибута <xref:System.Runtime.InteropServices.MarshalAsAttribute> во время разработки.  
  
 [Настройка вызываемых оболочек времени выполнения](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/e753eftz(v=vs.100))  
 Описаны способы настройки связанного с маршалингом поведения типов в сборке взаимодействия и определения типов COM вручную.  
  
 [Расширенное COM-взаимодействие](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bd9cdfyx(v=vs.100))  
 Приводятся ссылки на дополнительные сведения о включении COM-компонентов в разрабатываемое приложение .NET Framework.  
  
 [Общие сведения о преобразовании сборки в библиотеку типов](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/xk1120c3(v=vs.100))  
 Описывается процесс преобразования при экспорте сборки в библиотеку типов.  
  
 [Общие сведения о преобразовании библиотеки типов в сборку](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100))  
 Описывается процесс преобразования при экспорте библиотеки типов в сборку.  
  
 [Взаимодействие с помощью универсальных типов](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms229590(v=vs.100))  
 Описываются действия, поддерживаемые при использовании универсальных типов для взаимодействия COM.
