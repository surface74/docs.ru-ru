---
title: Создание клиента REST с использованием .NET Core
description: Это руководство раскроет для вас некоторые возможности .NET Core и языка C#.
ms.date: 03/06/2017
ms.assetid: 51033ce2-7a53-4cdd-966d-9da15c8204d2
ms.openlocfilehash: f6e3371a72810b30f804169be4025360aa10c477
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65063881"
---
# <a name="rest-client"></a>Клиент REST

## <a name="introduction"></a>Вступление

Это руководство раскроет для вас некоторые возможности .NET Core и языка C#. Вы узнаете:

* работа с интерфейсом командной строки (CLI) в .NET Core;
* обзор возможностей языка C#;
* управление зависимостями с помощью NuGet;
* взаимодействие по протоколу HTTP;
* обработка информации в формате JSON;
* управление конфигурацией с помощью атрибутов.

Вам предстоит создать приложение, которое отправляет запросы HTTP к службе REST на GitHub. Вы будете считывать данные в формате JSON и преобразовывать полученный пакет JSON в объекты C#. И наконец, вы увидите примеры работы с объектами C#.

В этом руководстве описано множество функций. Давайте начнем поочередно разбирать их.

Если вы хотите поработать с [примером окончательного кода](https://github.com/dotnet/samples/tree/master/csharp/getting-started/console-webapiclient) в этом разделе, вы можете его загрузить. Инструкции по загрузке см. в разделе [Просмотр и скачивание примеров](../../samples-and-tutorials/index.md#viewing-and-downloading-samples).

## <a name="prerequisites"></a>Предварительные требования

Компьютер должен быть настроен для выполнения .NET Core. Инструкции по установке см. на странице [.NET Core](https://www.microsoft.com/net/core). Это приложение можно запустить в ОС Windows, Linux, macOS или в контейнере Docker.
Вам потребуется редактор кода, но вы можете выбрать любой привычный для вас. В примерах ниже используется кроссплатформенный редактор [Visual Studio Code](https://code.visualstudio.com/) с открытым исходным кодом. Вы можете заменить его на любое другое средство, с которым вам удобно работать.

## <a name="create-the-application"></a>Создание приложения

Первым шагом является создание нового приложения. Откройте командную строку и создайте новый каталог для приложения. Перейдите в этот каталог. В командной строке введите команду `dotnet new console`. Эта команда создает начальный набор файлов для базового приложения Hello World. Так как это новый проект, зависимостей нет на месте, поэтому при первом запуске будет скачана платформа .NET Core, установлен сертификат разработки и запущен диспетчер пакетов NuGet для восстановления отсутствующих зависимостей.

Прежде чем вносить изменения, введите `dotnet run` ([см. примечание](#dotnet-restore-note)) в командной строке, чтобы запустить приложение. `dotnet run` автоматически выполняет `dotnet restore` при отсутствии зависимостей в вашей среде. Он также выполнит `dotnet build`, если приложение необходимо пересобрать.
После первоначальной настройки будет достаточно запуска `dotnet restore` или `dotnet build`, когда это имеет смысл для вашего проекта.

## <a name="adding-new-dependencies"></a>Добавление новых зависимостей

Одна из важнейших миссий .NET Core — снизить размер установки .NET. Если для каких-то задач приложению нужны дополнительные библиотеки, добавляйте их в качестве зависимостей в файл проекта C# (\*.csproj). В нашем примере нужно добавить пакет `System.Runtime.Serialization.Json`, чтобы приложение могло обрабатывать ответы JSON.

Откройте файл проекта `csproj`. Первая строка файла должна выглядеть так:

```xml
<Project Sdk="Microsoft.NET.Sdk">
```

Сразу после этой строки добавьте следующий код:

```xml
   <ItemGroup>
      <PackageReference Include="System.Runtime.Serialization.Json" Version="4.3.0" />
   </ItemGroup>
```

Большинство редакторов кода предлагает автозавершение для различных версий этих библиотек. Обычно разработчики предпочитают использовать последнюю версию каждого добавляемого пакета. Но при этом важно убедиться в том, что версии всех пакетов соответствуют друг другу и версии платформы приложений .NET Core.

После внесения этих изменений снова запустите команду `dotnet restore` ([см. примечание](#dotnet-restore-note)), которая установит на компьютер нужный пакет.

## <a name="making-web-requests"></a>Выполнение веб-запросов

Теперь вы готовы получать данные из Интернета. В этом приложении вы будете считывать информацию из [API GitHub](https://developer.github.com/v3/). Давайте, например, получим информацию о проектах под зонтичным брендом [.NET Foundation](https://www.dotnetfoundation.org/). Для начала вам нужно составить запрос к API GitHub для получения информации о проектах. Используемая конечная точка: <https://api.github.com/orgs/dotnet/repos>. Вы будете получать все данные об этих проектах, поэтому используйте запрос HTTP GET.
Браузер также использует запросы HTTP GET, поэтому вы можете указать этот URL-адрес в адресной строке браузера и увидеть, какие сведения вы будете получать и обрабатывать.

Для выполнения веб-запросов используется класс <xref:System.Net.Http.HttpClient>. Как и все современные API-интерфейсы .NET, <xref:System.Net.Http.HttpClient> поддерживает для API-интерфейсов длительного выполнения только асинхронные методы.
Поэтому вам нужно создать асинхронный метод. Реализацию вы будете добавлять постепенно, по мере создания функций приложения. Сначала откройте файл `program.cs`, расположенный в каталоге проекта, и добавьте в класс `Program` следующий метод:

```csharp
private static async Task ProcessRepositories()
{
}
```

В верхней части метода `Main` нужно разместить инструкцию `using`, чтобы компилятор C# распознал тип <xref:System.Threading.Tasks.Task>:

```csharp
using System.Threading.Tasks;
```

Если сейчас вы выполните сборку проекта, то получите предупреждение для этого метода, поскольку он не содержит ни одного оператора `await`, и поэтому будет выполняться синхронно. Пока это предупреждение можно игнорировать. Операторы `await` здесь появятся по мере заполнения метода.

А пока переименуйте пространство имен, определенное в инструкции `namespace`, указав имя `WebAPIClient` вместо имени по умолчанию `ConsoleApp`. Позднее в этом пространстве имен мы определим класс `repo`.

Теперь измените метод `Main`, добавив вызов этого метода. Метод `ProcessRepositories` возвращает задачу, до завершения которой выполнение программы не должно прекращаться. Чтобы обеспечить это, используйте метод `Wait`, который блокирует программу и ожидает завершения задачи:

```csharp
static void Main(string[] args)
{
    ProcessRepositories().Wait();
}
```

Теперь у вас есть программа, которая работает в асинхронном режиме, но не выполняет никаких действий. Давайте улучшим ее.

Для начала нужен объект, который может извлечь данные из Интернета. Для этого подойдет <xref:System.Net.Http.HttpClient>. Он будет обрабатывать запрос и ответы на него. Создайте один экземпляр этого типа в классе `Program` из файла Program.cs.

```csharp
namespace WebAPIClient
{
    class Program
    {
        private static readonly HttpClient client = new HttpClient();

        static void Main(string[] args)
        {
            //...
        }
    }
}
```

Давайте вернемся к методу `ProcessRepositories` и создадим его первую версию.

```csharp
private static async Task ProcessRepositories()
{
    client.DefaultRequestHeaders.Accept.Clear();
    client.DefaultRequestHeaders.Accept.Add(
        new MediaTypeWithQualityHeaderValue("application/vnd.github.v3+json"));
    client.DefaultRequestHeaders.Add("User-Agent", ".NET Foundation Repository Reporter");

    var stringTask = client.GetStringAsync("https://api.github.com/orgs/dotnet/repos");

    var msg = await stringTask;
    Console.Write(msg);
}
```

Чтобы эта версия успешно компилировалась, необходимо добавить две новые инструкции using в верхней части файла:

```csharp
using System.Net.Http;
using System.Net.Http.Headers;
```

Эта первая версия метода выполняет веб-запрос для чтения списка всех репозиториев в организации dotnet foundation. (На сайте gitHub организация .NET Foundation имеет идентификатор dotnet.) Первые несколько строк настраивают <xref:System.Net.Http.HttpClient> для этого запроса. Сначала мы указываем, что он будет принимать ответы GitHub JSON.
Они возвращаются в простом формате JSON. Следующая строка добавляет заголовок User Agent ко всем запросам от этого объекта. Кодом сервера GitHub проверяет эти два заголовка, и их наличие необходимо для извлечения сведений из GitHub.

Когда вы настроите объект <xref:System.Net.Http.HttpClient>, можно выполнить веб-запрос и получить ответ. В первой версии используйте удобный метод <xref:System.Net.Http.HttpClient.GetStringAsync(System.String)?displayProperty=nameWithType>. Этот метод запускает задачу для выполнения веб-запроса, а при получении результатов запроса он считывает поток ответа и извлекает из него содержимое. Текст ответа возвращается в формате <xref:System.String>. Эта строка становится доступна после завершения задачи.

Последние две строки этого метода ожидают выполнения созданной задачи, а затем выводят ответ в консоль.
Выполните сборку приложения и запустите его. Предупреждение при сборке теперь не отображается, поскольку в методе `ProcessRepositories` есть оператор `await`. В ответ вы получите длинный текст в формате JSON.

## <a name="processing-the-json-result"></a>Обработка результатов JSON

Сейчас у вас уже есть код, который получает от веб-сервера ответ и отображает текст из этого ответа. Теперь давайте преобразуем этот ответ JSON в объекты C#.

Сериализатор JSON преобразует данные в формате JSON в объекты C#. Первым делом следует определить тип класса C# для хранения информации, которую вы извлечете из ответа. Мы будем создавать код постепенно, и начнем с простого типа C#, который содержит имя репозитория:

```csharp
using System;

namespace WebAPIClient
{
    public class repo
    {
        public string name;
    }
}
```

Поместите приведенный выше код в новый файл с именем repo.cs. Эта версия класса реализует простейший способ обработки данных JSON. Имя класса и имя элемента совпадают с именами, используемыми в пакете JSON, и не соответствуют соглашениям C# об именовании. Чтобы исправить это, мы позже добавим некоторые атрибуты конфигурации. Этот класс демонстрирует еще одну важную возможность сериализации и десериализации JSON — не все поля в пакете JSON входят в этот класс.
Сериализатор JSON просто игнорирует информацию, которая не входит в используемый тип класса.
Такое поведение позволяет легко создавать типы, работающие с любым подмножеством полей из пакета JSON.

Теперь давайте выполним десериализацию созданного типа. Вам потребуется создать объект <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>. Этот объект должен знать тип среды CLR, которая ожидается для полученного пакета JSON. Пакет, получаемый от GitHub, содержит последовательность репозиториев, и правильным типом в этом случае будет `List<repo>`. Добавьте следующую строку в метод `ProcessRepositories`:

```csharp
var serializer = new DataContractJsonSerializer(typeof(List<repo>));
```

Вы создали два новых пространства имен, и их тоже нужно добавить сюда:

```csharp
using System.Collections.Generic;
using System.Runtime.Serialization.Json;
```

Теперь вызовите сериализатор для преобразования пакета JSON в объекты C#. В методе `ProcessRepositories` замените вызов <xref:System.Net.Http.HttpClient.GetStringAsync(System.String)> следующими двумя строками.

```csharp
var streamTask = client.GetStreamAsync("https://api.github.com/orgs/dotnet/repos");
var repositories = serializer.ReadObject(await streamTask) as List<repo>;
```

Обратите внимание, что теперь вы используете <xref:System.Net.Http.HttpClient.GetStreamAsync(System.String)> вместо <xref:System.Net.Http.HttpClient.GetStringAsync(System.String)>. Сериализатор использует в качестве источника поток, а не строку. Мы хотим объяснить вам функции языка C#, которые используются во второй строке представленного выше фрагмента кода. Аргумент <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject(System.IO.Stream)> является выражением `await`. Выражения await могут использоваться почти в любом месте кода, хотя пока мы их применяли только в операторе присваивания.

Во-вторых, оператор `as` преобразует тип `object`, используемый во время компиляции, в `List<repo>`.
Объявление оператора <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject(System.IO.Stream)> указывает, что он возвращает объект типа <xref:System.Object?displayProperty=nameWithType>. <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject(System.IO.Stream)> возвращает тип, который вы указали при конструировании (в нашем примере это тип `List<repo>`). Если преобразование завершается неудачно, оператор `as` возвращает `null`, но не создает исключение.

В этом разделе все почти готово. Вы уже преобразовали JSON в объекты C#, и теперь можете отобразить имена всех репозиториев. Удалите вот эти строки кода:

```csharp
var msg = await stringTask;   //**Deleted this
Console.Write(msg);
```

и замените их следующим фрагментом:

```csharp
foreach (var repo in repositories)
    Console.WriteLine(repo.name);
```

Скомпилируйте и запустите приложение. Вы получите имена всех репозиториев, которые являются частью .NET Foundation.

## <a name="controlling-serialization"></a>Управление сериализацией

Прежде чем добавлять новые возможности, давайте разберемся с типом `repo`, чтобы он соответствовал стандартным соглашениям C#. Для этого добавьте к объявлению типа `repo` *атрибуты*, которые управляют работой сериализатора JSON. В вашем примере эти атрибуты будут определять сопоставление между именами ключей в пакете JSON и именами классов и членов C#. Вам понадобятся два атрибута: <xref:System.Runtime.Serialization.DataContractAttribute> и <xref:System.Runtime.Serialization.DataMemberAttribute>. По соглашению, все классы атрибутов завершаются суффиксом `Attribute`. Но этот суффикс не обязательно указывать, когда вы применяете атрибуты.

Атрибуты <xref:System.Runtime.Serialization.DataContractAttribute> и <xref:System.Runtime.Serialization.DataMemberAttribute> атрибуты находятся в другой библиотеке, и эту библиотеку необходимо добавить в файл проекта C# в качестве зависимости. Добавьте следующую строку в раздел `<ItemGroup>` файла проекта:

```xml
<PackageReference Include="System.Runtime.Serialization.Primitives" Version="4.3.0" />
```

Сохраните файл и выполните команду `dotnet restore` ([см. примечание](#dotnet-restore-note)), чтобы получить этот пакет.

Теперь откройте файл `repo.cs`. Здесь мы хотим изменить имя, чтобы слово `Repository` было представлено в нем целиком и с капитализацией в стиле Pascal. Но при этом узлы repo из JSON должны по-прежнему сопоставляться с этим типом, так что вам нужно добавить атрибут <xref:System.Runtime.Serialization.DataContractAttribute> к объявлению класса. Для этого атрибута должно быть задано свойство `Name` с именем узлов JSON, которые будут сопоставлены с этим типом:

```csharp
[DataContract(Name="repo")]
public class Repository
```

Атрибут <xref:System.Runtime.Serialization.DataContractAttribute> входит в пространство имен <xref:System.Runtime.Serialization>, поэтому вам потребуется соответствующая инструкция `using` в верхней части файла:

```csharp
using System.Runtime.Serialization;
```

Имя класса изменилось с `repo` на `Repository`, а значит аналогичные изменения нужно внести в файл Program.cs (некоторые редакторы поддерживают рефакторинг путем переименования, при котором все нужные изменения будут применены автоматически).

```csharp
var serializer = new DataContractJsonSerializer(typeof(List<Repository>));

// ...

var repositories = serializer.ReadObject(await streamTask) as List<Repository>;
```

Теперь выполните такие же преобразования для поля `name` в классе <xref:System.Runtime.Serialization.DataMemberAttribute>. В файле repo.cs внесите следующие изменения в объявление `name`:

```csharp
[DataMember(Name="name")]
public string Name;
```

Это изменение требует также изменить код в файле program.cs, который записывает имя каждого хранилища:

```csharp
Console.WriteLine(repo.Name);
```

Выполните `dotnet build`, а затем `dotnet run`, чтобы проверить правильность сопоставления. Результат выполнения должен быть такой же, как прежде. Прежде чем перейти к обработке дополнительных свойств, полученных от веб-сервера, давайте внесем еще одно изменение в класс `Repository`. Член `Name` является общедоступным полем. Это плохо соотносится с рекомендациями по объектно-ориентированному программированию, поэтому вместо него мы будем использовать свойство. В нашем примере пока не требуется выполнять специальный код при получении или задании свойства, но благодаря такому изменению нам позднее будет проще добавить такой код, не переделывая вызовы класса `Repository`.

Удалите определение поля и замените его [автоматически реализуемым свойством](../programming-guide/classes-and-structs/auto-implemented-properties.md):

```csharp
public string Name { get; set; }
```

Компилятор создает текст акцессоров `get` и `set`, а также закрытое поле для хранения имени. Этот код будет выглядеть примерно так, как показано ниже. Вы также можете ввести такой код вручную:

```csharp
public string Name
{
    get { return this._name; }
    set { this._name = value; }
}
private string _name;
```

И еще одно изменение, прежде чем мы начнем добавлять новые функции. Метод `ProcessRepositories` может выполнять работу в асинхронном режиме и возвращает коллекцию репозиториев. Давайте сделаем так, чтобы этот метод возвращал `List<Repository>`, а сегмент кода, который записывает информацию, переместим в метод `Main`.

Измените сигнатуру `ProcessRepositories`, чтобы этот метод возвращал задачу, результатом которой является список объектов `Repository`:

```csharp
private static async Task<List<Repository>> ProcessRepositories()
```

Теперь мы можем просто возвращать репозитории после обработки ответа JSON:

```csharp
var repositories = serializer.ReadObject(await streamTask) as List<Repository>;
return repositories;
```

Компилятор создает в качестве выходных данных объект `Task<T>`, поскольку этот метод обозначен ключевым словом `async`.
Теперь мы изменим метод `Main` так, чтобы он записывает эти результаты и выводил в консоль имя каждого репозитория. Метод `Main` теперь выглядит следующим образом:

```csharp
public static void Main(string[] args)
{
    var repositories = ProcessRepositories().Result;

    foreach (var repo in repositories)
        Console.WriteLine(repo.Name);
}
```

Доступ к свойству `Result` блокируется, пока не завершится созданная задача. Было бы лучше использовать `await`, чтобы подождать завершения задачи, как мы сделали это в методе `ProcessRepositories`, но это не допускается для метода `Main`.

## <a name="reading-more-information"></a>Получение дополнительных сведений

И в завершении нашего руководства мы обработаем еще несколько свойств, содержащихся в пакете JSON, который отправляется из API GitHub. Нет смысла обрабатывать всю информацию, но добавление нескольких свойств поможет продемонстрировать еще несколько возможностей языка C#.

Сначала добавьте еще несколько простых типов в определение класса `Repository`. Добавьте в этот класс следующие свойства:

```csharp
[DataMember(Name="description")]
public string Description { get; set; }

[DataMember(Name="html_url")]
public Uri GitHubHomeUrl { get; set; }

[DataMember(Name="homepage")]
public Uri Homepage { get; set; }

[DataMember(Name="watchers")]
public int Watchers { get; set; }
```

Для этих свойств применяются встроенные преобразования из строкового типа (который используется в пакетах JSON) в целевой тип. Возможно, с типом <xref:System.Uri> вы пока не знакомы. Он представляет универсальный код ресурса, например URL-адрес, как в нашем примере. Если вы используете типы `Uri` и `int`, а пакет JSON содержит данные, для которых невозможно выполнить преобразование в целевой тип, действие сериализации создает исключение.

Добавив новые типы, включите их в метод `Main`:

```csharp
foreach (var repo in repositories)
{
    Console.WriteLine(repo.Name);
    Console.WriteLine(repo.Description);
    Console.WriteLine(repo.GitHubHomeUrl);
    Console.WriteLine(repo.Homepage);
    Console.WriteLine(repo.Watchers);
    Console.WriteLine();
}
```

На последнем этапе мы добавим сведения о последней операции принудительной отправки. Эта информация представлена в ответе JSON в следующем формате:

```json
2016-02-08T21:27:00Z
```

Он не соответствует ни одному из стандартных форматов .NET для типа <xref:System.DateTime>. Поэтому нам нужен специализированный метод для преобразования. Кроме того, нежелательно предоставлять пользователям класса `Repository` доступ к необработанным строковым данным. И здесь нам снова помогут атрибуты. Во-первых, определите свойство `private`, которое будет содержать строковое представление даты и времени в классе `Repository`:

```csharp
[DataMember(Name="pushed_at")]
private string JsonDate { get; set; }
```

Атрибут <xref:System.Runtime.Serialization.DataMemberAttribute> сообщает сериализатору, что эти данные нужно обрабатывать, поскольку по умолчанию обрабатываются только открытые члены. Во-вторых, создайте открытое свойство только для чтения, которое преобразует строку в допустимый объект <xref:System.DateTime> и возвращает этот объект <xref:System.DateTime>.

```csharp
[IgnoreDataMember]
public DateTime LastPush
{
    get
    {
        return DateTime.ParseExact(JsonDate, "yyyy-MM-ddTHH:mm:ssZ", CultureInfo.InvariantCulture);
    }
}
```

Давайте подробнее рассмотрим представленные выше новые конструкции. Атрибут `IgnoreDataMember` сообщает сериализатору, что этот тип не должен использоваться для чтения или записи в любых объектах JSON. Это свойство содержит только акцессор `get`. Метод доступа `set` не существует. Именно так в C# определяются свойства *только для чтения*. (Да, вы можете создать в C# даже свойства *только для записи*, но для них трудно найти применение.) Метод <xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)> анализирует строку и создает объект <xref:System.DateTime>, используя указанный формат даты, а затем включает в `DateTime` дополнительные метаданные, используя объект `CultureInfo`. Если операция анализа завершается неудачей, акцессор этого свойства создает исключение.

Чтобы использовать <xref:System.Globalization.CultureInfo.InvariantCulture>, необходимо добавить пространство имен <xref:System.Globalization> в набор инструкций `using` в файле `repo.cs`:

```csharp
using System.Globalization;
```

Вам осталось только добавить одну инструкцию вывода данных в консоль, и можно будет заново собрать и запустить приложение:

```csharp
Console.WriteLine(repo.LastPush);
```

Теперь версия вашего приложения должна совпадать с [полной версией примера](https://github.com/dotnet/samples/tree/master/csharp/getting-started/console-webapiclient).

## <a name="conclusion"></a>Заключение

В этом руководстве вы увидели, как правильно выполнять веб-запросы, анализировать результаты и отображать полученные в них свойства. Вы также добавили в свой проект несколько новых пакетов в качестве зависимостей. Еще вы увидели примеры некоторых функций языка C#, которые поддерживают объектно-ориентированный подход.

<a name="dotnet-restore-note"></a>

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]
