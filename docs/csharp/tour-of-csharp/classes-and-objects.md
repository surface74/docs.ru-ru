---
title: Классы и объекты в C#. Краткий обзор языка C#
description: Вы еще не знакомы с C#? Этот обзор познакомит вас с понятиями классов, объектов и наследования
ms.date: 08/10/2016
ms.assetid: 63a89bde-0f05-4bc4-b0cd-4f693854f0cd
ms.openlocfilehash: ff83a3198c6c9fb4c4a438d2486614a211c913ec
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/13/2019
ms.locfileid: "68971461"
---
# <a name="classes-and-objects"></a>Классы и объекты

*Классы* являются основным типом в языке C#. Класс представляет собой структуру данных, которая объединяет в себе значения (поля) и действия (методы и другие функции-члены). Класс предоставляет определение для динамически создаваемых *экземпляров* класса, которые также именуются *объектами*. Классы поддерживают механизмы *наследования* и *полиморфизма*, которые позволяют создавать *производные классы*, расширяющие и уточняющие определения *базовых классов*.

Новые классы создаются с помощью объявлений классов. Объявление класса начинается с заголовка, в котором указаны атрибуты и модификаторы класса, имя класса, базовый класс (если есть) и интерфейсы, реализуемые этим классом. За заголовком между разделителями `{` и `}` следует тело класса, в котором последовательно объявляются все члены класса.

Вот простой пример объявления класса с именем `Point`:

[!code-csharp[PointClass](~/samples/snippets/csharp/tour/classes-and-objects/Point.cs#L3-L11)]

Экземпляры классов создаются с помощью оператора `new`, который выделяет память для нового экземпляра, вызывает конструктор для инициализации этого экземпляра и возвращает ссылку на экземпляр. Следующие инструкции создают два объекта Point и сохраняют ссылки на них в две переменные:

[!code-csharp[PointExample](~/samples/snippets/csharp/tour/classes-and-objects/Program.cs#L9-L10)]

Занимаемая объектом память автоматически освобождается, когда объект становится недоступен. В C# нет ни необходимости, ни возможности освобождать память объектов явным образом.

## <a name="members"></a>Участники

Члены класса могут быть статическими членами или членами экземпляра. Статические члены принадлежат классу в целом, а члены экземпляра принадлежат конкретным объектам (экземплярам классов).

Ниже перечислены виды членов, которые могут содержаться в классе.

* Константы
  - Константные значения, связанные с классом.
* Поля
  - Переменные класса.
* Методы
  - Вычисления и действия, которые может выполнять класс.
* Свойства
  - Действия, связанные с чтением и записью именованных свойств класса.
* Индексаторы
  - Действия, реализующие индексирование экземпляров класса, чтобы обращаться к ним как к массиву.
* События
  - Уведомления, которые могут быть созданы этим классом.
* Операторы
  - Поддерживаемые классом операторы преобразования и выражения.
* Конструкторы
  - Действия, необходимые для инициализации экземпляров класса или класса в целом.
* Методы завершения
  - Действия, выполняемые перед окончательным удалением экземпляров класса.
* Типы
  - Вложенные типы, объявленные в классе.

## <a name="accessibility"></a>Специальные возможности

Каждый член класса имеет определенный уровень доступности. Он определяет, из какой области программы можно обращаться к этому члену. Существует шесть уровней доступности. Они кратко описаны ниже.

* `public`
  - Доступ не ограничен.
* `protected`
  - Доступ возможен из этого класса и из классов, унаследованных от него.
* `internal`
  - Доступ ограничен только текущей сборкой (.exe, .dll и т. д.).
* `protected internal`
  - Доступ ограничен содержащим классом, классами, которые являются производными от содержащего класса, либо классами в той же сборке
* `private`
  - Доступ возможен только из этого класса.
* `private protected`
  - Доступ ограничен содержащим классом или классами, которые являются производными от содержащего типа в той же сборке

## <a name="type-parameters"></a>Параметры типа

Определение класса может задать набор параметров типа. Список имен параметров типа указывается в угловых скобках после имени класса. Параметры типа можно использовать в теле класса в определениях, описывающих члены класса. В следующем примере для класса `Pair` заданы параметры типа `TFirst` и `TSecond`:

[!code-csharp[Pair](~/samples/snippets/csharp/tour/classes-and-objects/Pair.cs#L3-L7)]

Тип класса, для которого объявлены параметры типа, называется *универсальным типом класса*. Типы структуры, интерфейса и делегата также могут быть универсальными.
Если вы используете универсальный класс, необходимо указать аргумент типа для каждого параметра типа, вот так:

[!code-csharp[PairExample](~/samples/snippets/csharp/tour/classes-and-objects/Program.cs#L15-L17)]

Универсальный тип, для которого указаны аргументы типа, как `Pair<int,string>` в примере выше, называется *сконструированным типом*.

## <a name="base-classes"></a>базовых классов;

В объявлении класса можно указать базовый класс, включив имя базового класса после имени класса и параметров типа, и отделив его двоеточием. Если спецификация базового класса не указана, класс наследуется от типа `object`. В следующем примере `Point3D` имеет базовый класс `Point`, а `Point` — базовый класс `object`:

[!code-csharp[Point3DClass](~/samples/snippets/csharp/tour/classes-and-objects/Point.cs#L3-L20)]

Класс наследует члены базового класса. Наследование означает, что класс неявно содержит все члены своего базового класса, за исключением конструкторов экземпляра, статических конструкторов и методов завершения базового класса. Производный класс может дополнить наследуемые элементы новыми элементами, но он не может удалить определение для наследуемого члена. В предыдущем примере `Point3D` наследует поля `x` и `y` из `Point`, и каждый экземпляр `Point3D` содержит три поля: `x`, `y` и `z`.

Используется неявное преобразование из типа класса к любому из типов соответствующего базового класса. Это означает, что переменная типа класса может ссылаться как на экземпляр этого класса, так и на экземпляры любого производного класса. Например, если мы используем описанные выше объявления классов, то переменная типа `Point` может ссылаться на `Point` или `Point3D`:

[!code-csharp[Point3DExample](~/samples/snippets/csharp/tour/classes-and-objects/Program.cs#L22-L23)]

## <a name="fields"></a>Поля

*Поле* является переменной, связанной с определенным классом или экземпляром класса.

Поле, объявленное с модификатором static, является статическим. Статическое поле определяет строго одно место хранения. Независимо от того, сколько будет создано экземпляров этого класса, существует только одна копия статического поля.

Поле, объявленное без модификатора static, является полем экземпляра. Каждый экземпляр класса содержит отдельные копии всех полей экземпляра, определенных для этого класса.

В следующем примере каждый экземпляр класса `Color` содержит отдельную копию полей экземпляра `r`, `g` и `b`, но для каждого из статических полей `Black`, `White`, `Red`, `Green` и `Blue` существует только одна копия:

[!code-csharp[ColorClass](~/samples/snippets/csharp/tour/classes-and-objects/Color.cs#L3-L17)]

Как показано в предыдущем примере, можно объявить *поля только для чтения*, используя модификатор `readonly`. Присвоение значения полю `readonly` может происходить только при объявлении этого поля или в конструкторе этого класса.

## <a name="methods"></a>Методы

*Метод* — это член, реализующий вычисление или действие, которое может выполнять объект или класс. Доступ к *статическим методам* осуществляется через класс. Доступ к *методам экземпляра* осуществляется через экземпляр класса.

Для метода можно определить список *параметров*, которые представляют переданные методу значения или ссылки на переменные, а также *возвращаемый тип*, который задает тип значения, вычисляемого и возвращаемого методом. Если метод не возвращает значений, для него устанавливается возвращаемый тип `void`.

Как и типы, методы могут иметь набор параметров типа, для которых при вызове метода необходимо указывать аргументы типа. В отличие от типов, аргументы типа зачастую могут выводиться из аргументов вызова метода, и тогда их не обязательно задавать явным образом.

*Сигнатура* метода должна быть уникальной в пределах класса, в котором объявлен этот метод. Сигнатура метода включает имя метода, количество параметров типа, а также количество, модификаторы и типы параметров метода. Сигнатура метода не включает возвращаемый тип.

### <a name="parameters"></a>Параметры

Параметры позволяют передать в метод значения или ссылки на переменные. Фактические значения параметрам метода присваиваются на основе *аргументов*, заданных при вызове метода. Существует четыре типа параметров: параметры значения, ссылочные параметры, параметры вывода и массивы параметров.

*Параметр значения* используется для передачи входных аргументов. Параметр значения сопоставляется с локальной переменной, которая получит начальное значение из значения аргумента, переданного в этом параметре. Изменения параметра значения не влияют на аргумент, переданный для этого параметра.

Параметры значения можно сделать необязательными, указав для них значения по умолчанию. Тогда соответствующие аргументы можно не указывать.

*Ссылочный параметр* используется для передачи аргументов по ссылке. Аргумент, передаваемый в качестве ссылочного параметра, должен представлять собой переменную с определенным значением. При выполнении метода ссылочный параметр указывает на то же место хранения, в котором размещена переменная аргумента. Чтобы объявить ссылочный параметр, используйте модификатор `ref`. Следующий пример кода демонстрирует использование параметров `ref`.

[!code-csharp[swapExample](~/samples/snippets/csharp/tour/classes-and-objects/RefExample.cs#L3-L18)]

*Параметр вывода* используется для передачи аргументов по ссылке. Он похож на ссылочный параметр, однако не требует явно присваивать значение аргумента, предоставляемого вызывающим объектом. Чтобы объявить параметр вывода, используйте модификатор `out`. В следующем примере показано использование параметров `out` с помощью синтаксиса, появившегося в C# 7.

[!code-csharp[OutExample](~/samples/snippets/csharp/tour/classes-and-objects/OutExample.cs#L3-L17)]

*Массив параметров* позволяет передавать в метод переменное число аргументов. Чтобы объявить массив параметров, используйте модификатор `params`. Массив параметров может быть только последним параметром в методе. Для него можно использовать только тип одномерного массива. В качестве примера правильного использования массива параметров можно назвать методы Write и WriteLine, реализованные в классе <xref:System.Console?displayProperty=nameWithType>. Ниже представлены объявления этих методов.

[!code-csharp[ConsoleExample](~/samples/snippets/csharp/tour/classes-and-objects/Program.cs#L78-L83)]

Внутри метода массив параметров полностью идентичен обычному параметру типа массив. Но зато при вызове метода, использующего массив параметров, ему можно передать либо один аргумент типа массив, либо любое количество аргументов типа элемент для массива параметров. В последнем случае экземпляр массива автоматически создается и инициализируется с заданными аргументами. Код из этого примера...

[!code-csharp[StringFormat](~/samples/snippets/csharp/tour/classes-and-objects/Program.cs#L55-L55)]

...эквивалентен следующей конструкции:

[!code-csharp[StringFormat2](~/samples/snippets/csharp/tour/classes-and-objects/Program.cs#L30-L35)]

### <a name="method-body-and-local-variables"></a>Тело метода и локальные переменные

Тело метода содержит инструкции, которые будут выполнены при вызове метода.

В теле метода можно объявлять переменные, относящиеся к выполнению этого метода. Такие переменные называются *локальными переменными*. В объявлении локальной переменной нужно указать имя типа и имя переменной. Также можно задать ее начальное значение. Следующий пример кода объявляет локальную переменную `i` с нулевым начальным значением, и еще одну локальную переменную `j` без начального значения.

[!code-csharp[Squares](~/samples/snippets/csharp/tour/classes-and-objects/Squares.cs#L3-L17)]

C# требует, чтобы локальной переменной было *явно присвоено значение*, прежде чем можно будет получить это значение. Например, если в предложенное выше объявление `i` не включить начальное значение, компилятор сообщит об ошибке при последующем использовании `i`, поскольку для `i` нет явно присвоенного значения.

Метод может использовать инструкцию `return`, чтобы вернуть управление вызывающему объекту. Если метод возвращает `void`, в нем нельзя использовать инструкцию `return` с выражением. В методе, выходное значение которого имеет любой другой тип, инструкции `return` должны содержать выражение, которое вычисляет возвращаемое значение.

### <a name="static-and-instance-methods"></a>Статические методы и методы экземпляра

Метод, объявленный с модификатором static, является *статическим методом*. Статический метод не работает с конкретным экземпляром и может напрямую обращаться только к статическим членам.

Метод, объявленный без модификатора static, является *методом экземпляра*. Метод экземпляра работает в определенном экземпляре и может обращаться как к статическим методам, так и к методам этого экземпляра. В методе можно напрямую обратиться к экземпляру, для которого этот метод был вызван, используя дескриптор `this`. Использование `this` в статическом методе приводит к ошибке.

Следующий класс `Entity` содержит статические члены и члены экземпляра.

[!code-csharp[Entity](~/samples/snippets/csharp/tour/classes-and-objects/Entity.cs#L16-L36)]

Каждый экземпляр `Entity` содержит серийный номер (и может содержать другие данные, которые здесь не показаны). Конструктор объекта `Entity` (который рассматривается как метод экземпляра) задает для нового экземпляра следующий доступный серийный номер. Поскольку конструктор является членом экземпляра, он может обращаться как к полю экземпляра `serialNo`, так и к статическому полю `nextSerialNo`.

Статические методы `GetNextSerialNo` и `SetNextSerialNo` могут обращаться к статическому полю `nextSerialNo`, но прямое обращение из них к полю экземпляра `serialNo` приводит к ошибке.

В следующем примере показано использование класса Entity.

[!code-csharp[EntityExample](~/samples/snippets/csharp/tour/classes-and-objects/Entity.cs#L3-L15)]

Обратите внимание, что статические методы `SetNextSerialNo` и `GetNextSerialNo` вызываются для класса, а метод экземпляра `GetSerialNo` вызывается для экземпляров класса.

### <a name="virtual-override-and-abstract-methods"></a>Виртуальные, переопределяющие и абстрактные методы

Если объявление метода экземпляра включает модификатор `virtual`, такой метод называется *виртуальным методом*. Если модификатор virtual отсутствует, метод считается *невиртуальным*.

При вызове виртуального метода могут быть вызваны разные его реализации в зависимости от того, какой *тип среды выполнения* имеет экземпляр, для которого вызван этот метод. При вызове невиртуального метода решающим фактором является *тип во время компиляции* для этого экземпляра.

Виртуальный метод можно *переопределить* в производном классе. Если объявление метода экземпляра содержит модификатор override, этот метод переопределяет унаследованный виртуальный метод с такой же сигнатурой. Изначальное объявление виртуального метода создает новый метод, а переопределение этого метода создает специализированный виртуальный метод с новой реализацией взамен унаследованного виртуального метода.

*Абстрактным методом* называется виртуальный метод без реализации. Абстрактный метод объявляется с модификатором abstract. Его можно объявить только в классе, который также объявлен абстрактным. Абстрактный метод должен обязательно переопределяться в каждом производном классе, не являющемся абстрактным.

Следующий пример кода объявляет абстрактный класс `Expression`, который представляет узел дерева выражений, а также три производных класса: `Constant`, `VariableReference` и `Operation`, которые реализуют узлы дерева выражений для констант, ссылок на переменные и арифметических операций. (Они похожи на типы дерева выражений, но их нельзя путать.)

[!code-csharp[ExpressionClass](~/samples/snippets/csharp/tour/classes-and-objects/Expressions.cs#L3-L61)]

Четыре приведенных выше класса можно использовать для моделирования арифметических выражений. Например, с помощью экземпляров этих классов выражение `x + 3` можно представить следующим образом.

[!code-csharp[ExpressionExample](~/samples/snippets/csharp/tour/classes-and-objects/Program.cs#L40-L43)]

Метод `Evaluate` экземпляра `Expression` вызывается для вычисления данного выражения и создает значение `double`. Этот метод принимает аргумент `Dictionary`, который содержит имена переменных (в качестве ключей записей) и значения переменных (в качестве значений записей). Так как `Evaluate` — абстрактный метод, то в неабстрактных классах, производных от `Expression`, необходимо переопределить `Evaluate`.

В `Constant` реализация метода `Evaluate` просто возвращает хранимую константу. В `VariableReference` реализация этого метода выполняет поиск имени переменной в словаре и возвращает полученное значение. В `Operation` реализация этого метода сначала вычисляет левый и правый операнды (рекурсивно вызывая их методы `Evaluate`), а затем выполняет предоставленную арифметическую операцию.

В следующей программе классы `Expression` используются для вычисления выражения `x * (y + 2)` с различными значениями `x` и `y`.

[!code-csharp[ExpressionUsage](~/samples/snippets/csharp/tour/classes-and-objects/Expressions.cs#L66-L89)]

### <a name="method-overloading"></a>Перегрузка методов

*Перегрузка* метода позволяет использовать в одном классе несколько методов с одинаковыми именами, если они имеют уникальные сигнатуры. Когда при компиляции встречается вызов перегруженного метода, компилятор использует принцип *разрешения перегрузки*, чтобы определить, какой из методов следует вызвать. Разрешение перегрузки выбирает из методов тот, который лучше всего соответствует предоставленным аргументам, или возвращает ошибку, если не удается выбрать конкретный подходящий метод. В следующем примере показано, как работает разрешение перегрузки. Комментарий к каждому вызову метода `UsageExample` подсказывает, какой из методов будет вызван для этой строки.

[!code-csharp[OverloadUsage](~/samples/snippets/csharp/tour/classes-and-objects/Overloading.cs#L3-L41)]

Как видно из этого примера, вы всегда можете выбрать конкретный метод, явным образом приведя типы аргументов к соответствующим типам параметров, и (или) явно предоставив аргументы нужного типа.

## <a name="other-function-members"></a>Другие функции-члены

Все члены класса, содержащие исполняемый код, совокупно называются *функции-члены*. В предыдущем разделе мы рассмотрели основные варианты методов, используемых как функции-члены. В этом разделе описываются другие типы функций-членов, поддерживаемые в языке C#: конструкторы, свойства, индексаторы, события, операторы и методы завершения.

Ниже приведен универсальный класс с именем `MyList<T>`, который реализует расширяемый список объектов. Этот класс содержит несколько наиболее распространенных типов функций-членов.

> [!NOTE]
> В этом примере создается класс `MyList`, который отличается от стандартного <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> в .NET. Здесь показаны основные понятия, необходимые для этого руководства, но они не заменят собой этот класс.

[!code-csharp[ListClass](~/samples/snippets/csharp/tour/classes-and-objects/ListBasedExamples.cs#L4-L89)]

### <a name="constructors"></a>Конструкторы

C# поддерживает конструкторы экземпляров и статические конструкторы. *Конструктор экземпляра* является членом, который реализует действия для инициализации нового экземпляра класса. *Статический конструктор* является членом, который реализует действия для инициализации самого класса при первоначальной его загрузке.

Конструктор объявляется в виде метода без возвращаемого типа, имя которого совпадает с именем класса, в котором он определен. Если объявление конструктора содержит модификатор static, создается статический конструктор. В противном случае это объявление считается конструктором экземпляра.

Конструкторы экземпляров можно перегружать, и для них можно указать необязательные параметры. Например, класс `MyList<T>` объявляет один конструктор экземпляра с одним необязательным параметром `int`. Конструкторы экземпляров вызываются с помощью оператора `new`. Следующий пример кода выделяет два экземпляра `MyList<string>` с помощью конструкторов класса `MyList`: один с необязательным аргументом, а второй — без.

[!code-csharp[ListExample1](~/samples/snippets/csharp/tour/classes-and-objects/ListBasedExamples.cs#L95-L96)]

В отличие от других членов конструкторы экземпляров не наследуются, и класс не имеет конструкторов экземпляров, кроме объявленных в самом этом классе. Если в классе не объявлен конструктор экземпляра, для него автоматически создается пустой конструктор без параметров.

### <a name="properties"></a>Свойства

*Свойства* естественным образом дополняют поля. И те, и другие являются именованными членами со связанными типами, и для доступа к ним используется одинаковый синтаксис. Однако свойства, в отличие от полей, не указывают места хранения. Вместо этого свойства содержат *методы доступа*, в которых описаны инструкции для выполнения при чтении или записи значений.

Свойство объявляется так же, как поле, за исключением того, что объявление заканчивается не точкой с запятой, а парой разделителей `{` и `}`, между которыми указаны акцессоры get для чтения и (или) set для записи. Свойство, для которого определены акцессоры get и set, является свойством *для чтения и записи*. Если в свойстве есть только акцессор get, оно является *свойством только для чтения*, и если только акцессор set — *свойством только для записи*.

Акцессор get оформляется как метод без параметров, у которого тип возвращаемого значения совпадает с типом, установленным для этого свойства. Во всех ситуациях, кроме использования в качестве назначения в операторе присваивания, для вычисления значения свойства вызывается акцессор get.

Акцессор get имеет вид метода с одним именованным параметром и без возвращаемого типа. Если же свойство используется в качестве назначения в операторе присваивания или в качестве операнда для операции ++ или --, вызывается акцессор set с аргументом, содержащим новое значение.

Класс `MyList<T>` объявляет два свойства: `Count` (только для чтения) и `Capacity` (только для записи). Пример использования этих свойств приведен ниже.

[!code-csharp[ListExample2](~/samples/snippets/csharp/tour/classes-and-objects/ListBasedExamples.cs#L101-L104)]

Как и в отношении полей и методов, C# поддерживает свойства экземпляра и статические свойства. Статические свойства объявляются с модификатором static, а свойства экземпляра — без него.

Акцессоры свойства могут быть виртуальными. Если объявление свойства содержит модификатор `virtual`, `abstract` или `override`, этот модификатор применяется к акцессорам свойства.

### <a name="indexers"></a>Индексаторы

*Индексатор* является членом, позволяющим индексировать объекты так, как будто они включены в массив. Индексатор объявляется так же, как свойство, за исключением того, что именем элемента является `this`, а за этим именем следует список параметров, находящийся между разделителями `[` и `]`. Эти параметры доступны в акцессорах индексатора. Как и свойства, можно объявить индексаторы для чтения и записи, только для чтения или только для записи. Кроме того, поддерживаются виртуальные акцессоры индексатора.

Класс `MyList<T>` объявляет один индексатор для чтения и записи, который принимает параметр `int`. Индексатор позволяет индексировать экземпляры `MyList<T>` значениями с типом `int`. Например:

[!code-csharp[ListExample3](~/samples/snippets/csharp/tour/classes-and-objects/ListBasedExamples.cs#L109-L117)]

Индексаторы можно перегружать, то есть в одном классе можно объявить несколько индексаторов, если у них различаются количество или типы параметров.

### <a name="events"></a>События

*Событие* — это член, с помощью которого класс или объект предоставляют уведомления. Объявление события выглядит так же, как объявление поля, но содержит ключевое слово event и обязано иметь тип делегата.

В классе, который объявляет член события, это событие действует, как обычное поле с типом делегата (если это событие не является абстрактным и не объявляет акцессоры). Это поле хранит ссылку на делегат, который представляет добавленные к событию обработчики событий. Если обработчики событий отсутствуют, это поле имеет значение `null`.

Класс `MyList<T>` объявляет один член события с именем `Changed`, который обрабатывает добавление нового элемента. Событие Changed вызывается виртуальным методом `OnChanged`, который сначала проверяет, не имеет ли это событие значение `null` (это означает, что обработчики отсутствуют). Концепция создания события в точности соответствует вызову делегата, представленного этим событием. Это позволяет обойтись без особой языковой конструкции для создания событий.

Клиенты реагируют на события посредством *обработчиков событий*. Обработчики событий можно подключать с помощью оператора `+=` и удалять с помощью оператора `-=`. Следующий пример кода подключает обработчик события `Changed` к событию `MyList<string>`.

[!code-csharp[EventExample](~/samples/snippets/csharp/tour/classes-and-objects/ListBasedExamples.cs#L132-L148)]

Для более сложных сценариев, требующих контроля над базовым хранилищем события, в объявлении события можно явным образом предоставить акцессоры `add` и `remove`. Они будут действовать примерно так же, как акцессор `set` для свойства.

### <a name="operators"></a>Операторы

*Оператор* является членом, который определяет правила применения определенного выражения к экземплярам класса. Вы можете определить операторы трех типов: унарные операторы, двоичные операторы и операторы преобразования. Все операторы объявляются с модификаторами `public` и `static`.

Класс `MyList<T>` объявляет два оператора: `operator ==` и `operator !=`. Это позволяет определить новое значение для выражений, которые применяют эти операторы к экземплярам `MyList`. В частности, эти операторы определяют, что равенство двух экземпляров `MyList<T>` проверяется путем сравнения всех содержащихся в них объектов с помощью определенных для них методов Equals. Следующий пример кода использует оператор `==` для сравнения двух экземпляров `MyList<int>`.

[!code-csharp[OperatorExample](~/samples/snippets/csharp/tour/classes-and-objects/ListBasedExamples.cs#L121-L129)]

Первый `Console.WriteLine` выводит `True`, поскольку два списка содержат одинаковое число объектов с одинаковыми значениями в том же порядке. Если бы в `MyList<T>` не было определения `operator ==`, первый `Console.WriteLine` возвращал бы `False`, поскольку `a` и `b` указывают на различные экземпляры `MyList<int>`.

### <a name="finalizers"></a>Методы завершения

*Метод завершения* является членом, который реализует действия для завершения существования экземпляра класса. Методы завершения не могут иметь параметры, не могут содержать модификаторы доступа и их нельзя вызвать явным образом. Метод завершения для экземпляра вызывается автоматически в процессе сборки мусора.

Сборщик мусора имеет широкую степень свободы в выборе времени уничтожения объектов и вызова методов завершения. В частности, время вызова методов завершения не является детерминированным, и эти методы могут выполняться в любом потоке. По этим и некоторым другим причинам методы завершения следует использовать в классах только в крайнем случае, когда невозможны другие решения.

Уничтожение объектов лучше контролировать с помощью инструкции `using`.

> [!div class="step-by-step"]
> [Назад](statements.md)
> [Вперед](structs.md)
