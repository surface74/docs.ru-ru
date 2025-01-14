---
title: EventWaitHandle
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], EventWaitHandle class
- EventWaitHandle class
- event wait handles [.NET Framework]
- threading [.NET Framework], cross-process synchronization
ms.assetid: 11ee0b38-d663-4617-b793-35eb6c64e9fc
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d9c90a3bd272b54d2884d013e62123dd67d836e3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960056"
---
# <a name="eventwaithandle"></a>EventWaitHandle
Класс <xref:System.Threading.EventWaitHandle> позволяет потокам взаимодействовать друг с другом, передавая и ожидая передачи сигналов. Дескрипторы ожидания событий (часто их называют просто "события") — это дескрипторы ожидания, которые можно создавать для освобождения одного или нескольких потоков в состоянии ожидания. Созданное событие (дескриптор ожидания) затем сбрасывается вручную или автоматически. Класс <xref:System.Threading.EventWaitHandle> может представлять любой локальный дескриптор ожидания событий (локальное событие) или именованный системный дескриптор ожидания событий (именованное событие), который доступен для всех процессов.  
  
> [!NOTE]
> Дескрипторы ожидания событий не являются [событиями](../events/index.md) .NET. Для них не существует делегатов или обработчиков. Слово "событие" здесь используется лишь потому, что такие дескрипторы традиционно именовались событиями операционной системы, а при создании дескриптора ожидания и потоков в состоянии ожидания передаются сведения о том, что произошло событие.  
  
 Как локальные, так и именованные дескрипторы ожидания событий используют системные объекты синхронизации, защищенные оболочками <xref:Microsoft.Win32.SafeHandles.SafeWaitHandle> для правильного освобождения ресурсов. Вы можете использовать метод <xref:System.Threading.WaitHandle.Dispose%2A>, чтобы освободить ресурсы, как только закончите работу с объектом.  
  
## <a name="event-wait-handles-that-reset-automatically"></a>Дескрипторы ожидания событий, которые сбрасываются автоматически  
 Чтобы создать событие с автоматическим сбросом, укажите <xref:System.Threading.EventResetMode.AutoReset?displayProperty=nameWithType> при создании объекта <xref:System.Threading.EventWaitHandle>. Как можно понять по имени, это событие синхронизации после создания освобождает один поток в состоянии ожидания и автоматически сбрасывается. Чтобы создать событие, вызовите его метод <xref:System.Threading.EventWaitHandle.Set%2A>.  
  
 События с автоматическим сбросом обычно используются, чтобы поочередно предоставлять монопольный доступ к ресурсу для одного потока из нескольких. В потоке подается запрос на ресурс. Для этого вызывается метод <xref:System.Threading.WaitHandle.WaitOne%2A>. Если в этот момент ни один поток не удерживает дескриптор ожидания, метод возвращает `true` и предоставляет вызывающему потоку управление ресурсом.  
  
> [!IMPORTANT]
> Как и для всех механизмов синхронизации, необходимо гарантировать во всех ветвях кода правильное ожидание дескриптора перед осуществлением доступа к защищенному ресурсу. Синхронизация потоков выполняется совместно.  
  
 Если событие с автоматическим сбросом создается при отсутствии потоков в состоянии ожидания, оно сохраняет свой статус, пока не получит обращение от потока. Тогда событие освобождает поток и немедленно сбрасывается, блокируя следующие потоки.  
  
## <a name="event-wait-handles-that-reset-manually"></a>Дескрипторы ожидания событий, которые сбрасываются вручную  
 Чтобы создать событие со сбросом вручную, укажите <xref:System.Threading.EventResetMode.ManualReset?displayProperty=nameWithType> при создании объекта <xref:System.Threading.EventWaitHandle>. Как можно понять по имени, это событие синхронизации после создания сбрасывается вручную. Пока не будет вызван метод <xref:System.Threading.EventWaitHandle.Reset%2A> для сброса события, все потоки, ожидающие этот дескриптор события, продолжают работу немедленно и без блокировки.  
  
 Событие со сбросом вручную действует как ворота загона. Пока событие не создано, потоки ожидают его, как стадо лошадей в загоне. Сразу после создания события путем вызова метода <xref:System.Threading.EventWaitHandle.Set%2A> все потоки в состоянии ожидания освобождаются и могут продолжать работу. Событие сохраняет статус созданного, пока не будет вызван его метод <xref:System.Threading.EventWaitHandle.Reset%2A>. Благодаря этому свойству событие со сбросом вручную идеально подходит для ситуации, когда нужно удерживать несколько потоков в ожидании завершения конкретной задачи.  
  
 Как и лошадям, выходящим из загона, освобожденным потокам потребуется некоторое время, пока операционная система сможет возобновить их выполнение. Если метод <xref:System.Threading.EventWaitHandle.Reset%2A> будет вызван раньше, чем все эти потоки возобновят выполнение, оставшиеся в ожидании потоки снова будут заблокированы. Какие конкретно потоки начнут работу, а какие снова останутся ожидать, зависит от многих случайных факторов, таких как загрузка системы, количество ожидающих выполнения потоков и т. д. Не возникнет никаких проблем, если поток, в котором создается событие, завершится сразу после его создания. Это самый распространенный вариант использования этого подхода. Если нужно, чтобы создающий событие поток начал выполнение новой задачи только после того, как все потоки в состоянии ожидания возобновят работу, заблокируйте его. Иначе возникнет состояние гонки и поведение кода будет непредсказуемым.  
  
## <a name="features-common-to-automatic-and-manual-events"></a>Общие свойства событий с автоматическим сбросом и сбросом вручную  
 Как правило, <xref:System.Threading.EventWaitHandle> блокирует один или несколько потоков, пока незаблокированный поток не вызовет метод <xref:System.Threading.EventWaitHandle.Set%2A>, который освобождает один из потоков в состоянии ожидания (если это событие с автоматическим сбросом) или все потоки сразу (если это событие со сбросом вручную). Поток может создать событие <xref:System.Threading.EventWaitHandle> и заблокироваться в ожидании этого же события в рамках одной атомарной операции, вызвав статический метод <xref:System.Threading.WaitHandle.SignalAndWait%2A?displayProperty=nameWithType>.  
  
 В статических методах <xref:System.Threading.WaitHandle.WaitAll%2A?displayProperty=nameWithType> и <xref:System.Threading.WaitHandle.WaitAny%2A?displayProperty=nameWithType> можно использовать объекты <xref:System.Threading.EventWaitHandle>. Так как классы <xref:System.Threading.EventWaitHandle> и <xref:System.Threading.Mutex> являются производными от <xref:System.Threading.WaitHandle>, вы можете использовать оба этих класса с этими методами.  
  
### <a name="named-events"></a>Именованные события  
 Операционная система Windows позволяет присваивать имена дескрипторам ожидания. Именованное событие применяется во всей системе. Это означает, что после создания именованное событие будет видимым для всех потоков во всех процессах. Таким образом, именованное событие можно использовать для синхронизации действий в разных процессах и потоках.  
  
 Вы можете создать объект <xref:System.Threading.EventWaitHandle>, который представляет именованное системное событие, с помощью любого из конструкторов, использующих имя события.  
  
> [!NOTE]
> Так как именованные события доступны во всей системе, может существовать несколько объектов <xref:System.Threading.EventWaitHandle>, представляющих одно и то же именованное событие. При каждом вызове конструктора или метода <xref:System.Threading.EventWaitHandle.OpenExisting%2A> создается новый объект <xref:System.Threading.EventWaitHandle>. Если указать одно и то же имя несколько раз, создается несколько объектов, представляющих одно и то же именованное событие.  
  
 При использовании именованных событий следует соблюдать осторожность. Поскольку они доступны во всей системе, другой процесс может использовать это же имя события и случайно заблокировать все ваши потоки. Вредоносный код, выполняемый на одном компьютере может использовать это как основу для атак типа "отказ в обслуживании".  
  
 Чтобы защитить объект <xref:System.Threading.EventWaitHandle>, представляющий именованное событие, примените механизм безопасности управления доступом. Лучше всего использовать конструктор, который определяет объект <xref:System.Security.AccessControl.EventWaitHandleSecurity>. Метод <xref:System.Threading.EventWaitHandle.SetAccessControl%2A> тоже обеспечит безопасность управления доступом, но такой подход оставит систему уязвимой в период между созданием и защитой дескриптора ожидания. Защита событий с помощью безопасности управления доступом предотвращает атаки злоумышленников, но не решает проблемы непреднамеренного конфликта имен.  
  
> [!NOTE]
> В отличие от класса <xref:System.Threading.EventWaitHandle>, производные классы <xref:System.Threading.AutoResetEvent> и <xref:System.Threading.ManualResetEvent> могут представлять только локальные дескрипторы ожидания. Они не могут представлять именованные системные события.  
  
## <a name="see-also"></a>См. также

- <xref:System.Threading.EventWaitHandle>
- <xref:System.Threading.WaitHandle>
- <xref:System.Threading.AutoResetEvent>
- <xref:System.Threading.ManualResetEvent>
