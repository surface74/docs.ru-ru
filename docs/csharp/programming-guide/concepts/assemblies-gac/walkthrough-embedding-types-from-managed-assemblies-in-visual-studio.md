---
title: Пошаговое руководство. Внедрение типов из управляемых сборок в Visual Studio в C#
ms.date: 07/20/2015
ms.assetid: 55ed13c9-c5bb-4bc2-bcd8-0587eb568864
ms.openlocfilehash: 5e6494f133128e3982aa07323d2c65b9fa5de47b
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2019
ms.locfileid: "69595803"
---
# <a name="walkthrough-embedding-types-from-managed-assemblies-in-visual-studio-c"></a>Пошаговое руководство. Внедрение типов из управляемых сборок в Visual Studio в C#

Внедряя сведения о типе из управляемой сборки со строгим именем, можно свободно объединять типы в приложении, делая версию независимой. Это означает, что в программе можно использовать типы из нескольких версий управляемой библиотеки, т. е. необходимость компилировать каждую версию отдельно отпадает.

Внедрение типов часто используется с COM-взаимодействием, например в приложениях, использующих объекты автоматизации из Microsoft Office. Сведения о типе внедрения позволяют одной и той же сборке программы работать с различными версиями Microsoft Office на разных компьютерах. Тем не менее внедрение типа можно также использовать с полностью управляемым решением.

Сведения о типе можно внедрить из сборки, имеющей следующие характеристики:

- Сборка предоставляет по крайней мере один открытый интерфейс.

- Внедренные интерфейсы снабжаются аннотацией с указанием атрибута `ComImport` и атрибута `Guid` (уникальный GUID).

- Сборка снабжается аннотацией с указанием атрибута `ImportedFromTypeLib` или атрибута `PrimaryInteropAssembly`, а также атрибута сборки `Guid`. (По умолчанию шаблоны проектов Visual C# включают атрибут сборки `Guid`.)

После того как открытые интерфейсы, доступные для внедрения, будут указаны, можно создать реализующие их классы среды выполнения. Во время разработки клиентская программа встраивает сведения о типе для этих интерфейсов, ссылаясь на сборку, содержащую открытые интерфейсы и присваивая свойству `Embed Interop Types` ссылки значение `True`. Это эквивалентно использованию компилятора командной строки и ссылки на сборку с помощью параметра компилятора `/link`. После этого клиентская программа может загружать экземпляры объектов среды выполнения, типизированные как указанные интерфейсы. При создании новой версии сборки среды выполнения со строгим именем повторная компиляция клиентской программы с обновленной сборкой среды выполнения не требуется. Клиентская программа продолжает работать с той версией сборки среды выполнения, которая ей доступна, используя сведения о внедренном типе для открытых интерфейсов.

Поскольку основной функцией внедрения типа является поддержка внедрения сведений о типе из сборок COM-взаимодействия, при внедрении сведений о типе в полностью управляемое решение применяются следующие ограничения:

- Внедряются только атрибуты, характерные для COM-взаимодействия; другие атрибуты игнорируются.

- Если тип включает универсальные параметры внедренного типа, использовать этот тип как границу сборки нельзя. Граница сборки пересекается, например, при вызове метода из другой сборки или выведении типа из типа, определенного в другой сборке.

- Константы не внедряются.

- Класс <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType> не поддерживает использование внедренного типа в качестве ключа. Для поддержки внедренного типа в качестве ключа можно реализовать свой собственный тип словаря.

В этом пошаговом руководстве выполняются следующие задачи:

- Создайте сборку со строгим именем и открытым интерфейсом, содержащим сведения о типе, который может быть внедрен.

- Создайте сборку среды выполнения со строгим именем, реализующую открытый интерфейс.

- Создайте клиентскую программу, внедряющую сведения о типе из открытого интерфейса и создающую экземпляр класса из сборки среды выполнения.

- Внесите изменения и создайте сборку среды выполнения заново.

- Запустите клиентскую программу, чтобы увидеть, что новая версия сборки среды выполнения позволяет обойтись без повторной компиляции клиентской программы.

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="creating-an-interface"></a>Создание интерфейса

#### <a name="to-create-the-type-equivalence-interface-project"></a>Создание проекта интерфейса для эквивалентности типа

1. В Visual Studio откройте меню **Файл**, выберите команду **Создать** и щелкните **Проект**.

2. Убедитесь, что в диалоговом окне **Создание проекта** в области **Типы проектов** выбран пункт **Windows**. Выберите **Библиотеки классов** в области **Шаблоны**. В поле **Имя** введите `TypeEquivalenceInterface` и нажмите кнопку **ОК**. Проект создан.

3. В **обозревателе решений** щелкните правой кнопкой мыши файл Class1.cs и нажмите кнопку **Переименовать**. Измените имя файла на `ISampleInterface.cs` и нажмите клавишу ВВОД. При переименовании файла класс также будет переименован в `ISampleInterface`. Этот класс будет представлять открытый интерфейс для класса.

4. Щелкните проект TypeEquivalenceInterface правой кнопкой мыши и выберите **Свойства**. Перейдите на вкладку **Сборка**. Укажите выходной путь к местоположению, существующему на компьютере разработчика, например `C:\TypeEquivalenceSample`. Это расположение также пригодится при последующей работе с данным пошаговым руководством.

5. Не закрывая окно редактирования свойств проекта, откройте вкладку **Подписывание**. Выберите параметр **Подписать сборку**. В списке **Выберите файл ключа строгого имени** выберите **\<Создать...>** . В поле **Имя файла ключа** введите `key.snk`. Снимите флажок **Защитить файл ключа паролем**. Нажмите кнопку **ОК**.

6. Откройте файл ISampleInterface.cs. Добавьте следующий код в файл класса ISampleInterface, чтобы создать интерфейс ISampleInterface.

    ```csharp
    using System;
    using System.Runtime.InteropServices;

    namespace TypeEquivalenceInterface
    {
        [ComImport]
        [Guid("8DA56996-A151-4136-B474-32784559F6DF")]
        public interface ISampleInterface
        {
            void GetUserInput();
            string UserInput { get; }
        }
    }
    ```

7. В меню **Сервис** выберите пункт **Создать GUID**. В диалоговом окне **Создание GUID** нажмите кнопку **Формат реестра**, а затем **Копировать**. Нажмите кнопку **Выход**.

8. В атрибуте `Guid` удалите пример GUID и вставьте GUID, скопированный из диалогового окна **Создание GUID**. Удалите фигурные скобки ({}) из скопированного GUID.

9. В **обозревателе решений** разверните папку **Свойства**. Дважды щелкните файл AssemblyInfo.cs. Добавьте в файл следующий атрибут.

    ```csharp
    [assembly: ImportedFromTypeLib("")]
    ```

     Сохраните файл.

10. Сохраните проект.

11. Щелкните проект TypeEquivalenceInterface правой кнопкой мыши и выберите пункт **Сборка**. DLL-файл библиотеки классов компилируется и сохраняется по указанному выходному пути для сборки (например, C:\TypeEquivalenceSample).

## <a name="creating-a-runtime-class"></a>Создание класса среды выполнения

#### <a name="to-create-the-type-equivalence-runtime-project"></a>Создание проекта среды выполнения для эквивалентности типа

1. В меню **Файл** окна Visual Studio наведите указатель мыши на пункт **Создать** и щелкните **Проект**.

2. Убедитесь, что в диалоговом окне **Создание проекта** в области **Типы проектов** выбран пункт **Windows**. Выберите **Библиотеки классов** в области **Шаблоны**. В поле **Имя** введите `TypeEquivalenceRuntime` и нажмите кнопку **ОК**. Проект создан.

3. В **обозревателе решений** щелкните правой кнопкой мыши файл Class1.cs и нажмите кнопку **Переименовать**. Измените имя файла на `SampleClass.cs` и нажмите клавишу ВВОД. При переименовании файла класс также будет переименован в `SampleClass`. Этот класс реализует интерфейс `ISampleInterface`.

4. Щелкните проект TypeEquivalenceRuntime правой кнопкой мыши и выберите **Свойства**. Перейдите на вкладку **Сборка**. Укажите выходной путь, ведущий в то же расположение, которое вы использовали в проекте TypeEquivalenceInterface, например `C:\TypeEquivalenceSample`.

5. Не закрывая окно редактирования свойств проекта, откройте вкладку **Подписывание**. Выберите параметр **Подписать сборку**. В списке **Выберите файл ключа строгого имени** выберите **\<Создать...>** . В поле **Имя файла ключа** введите `key.snk`. Снимите флажок **Защитить файл ключа паролем**. Нажмите кнопку **ОК**.

6. Щелкните проект TypeEquivalenceRuntime правой кнопкой мыши и выберите пункт **Добавить ссылку**. Откройте вкладку **Обзор** и перейдите в папку выходного пути. Выберите файл TypeEquivalenceInterface.dll и нажмите кнопку **ОК**.

7. В **обозревателе решений** разверните папку **Ссылки**. Выберите ссылку TypeEquivalenceInterface. В окне свойств для ссылки TypeEquivalenceInterface присвойте свойству **Указанная версия** значение **False**.

8. Добавьте следующий код в файл класса SampleClass, чтобы создать класс SampleClass.

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using TypeEquivalenceInterface;

    namespace TypeEquivalenceRuntime
    {
        public class SampleClass : ISampleInterface
        {
            private string p_UserInput;
            public string UserInput { get { return p_UserInput; } }

            public void GetUserInput()
            {
                Console.WriteLine("Please enter a value:");
                p_UserInput = Console.ReadLine();
            }
        }
    }
    ```

9. Сохраните проект.

10. Щелкните проект TypeEquivalenceRuntime правой кнопкой мыши и выберите пункт **Сборка**. DLL-файл библиотеки классов компилируется и сохраняется по указанному выходному пути для сборки (например, C:\TypeEquivalenceSample).

## <a name="creating-a-client-project"></a>Создание проекта клиента

#### <a name="to-create-the-type-equivalence-client-project"></a>Создание проекта клиента для эквивалентности типа

1. В меню **Файл** окна Visual Studio наведите указатель мыши на пункт **Создать** и щелкните **Проект**.

2. Убедитесь, что в диалоговом окне **Создание проекта** в области **Типы проектов** выбран пункт **Windows**. В области **Шаблоны** выберите пункт **Консольное приложение**. В поле **Имя** введите `TypeEquivalenceClient` и нажмите кнопку **ОК**. Проект создан.

3. Щелкните проект TypeEquivalenceClient правой кнопкой мыши и выберите пункт **Свойства**. Перейдите на вкладку **Сборка**. Укажите выходной путь, ведущий в то же расположение, которое вы использовали в проекте TypeEquivalenceInterface, например `C:\TypeEquivalenceSample`.

4. Щелкните проект TypeEquivalenceClient правой кнопкой мыши и выберите пункт **Добавить ссылку**. Откройте вкладку **Обзор** и перейдите в папку выходного пути. Выберите файл TypeEquivalenceInterface.dll (не TypeEquivalenceRuntime.dll) и нажмите кнопку **ОК**.

5. В **обозревателе решений** разверните папку **Ссылки**. Выберите ссылку TypeEquivalenceInterface. В окне свойств для ссылки TypeEquivalenceInterface присвойте свойству **Внедрить типы взаимодействия** значение **True**.

6. Добавьте в файл Program.cs следующий код, чтобы создать клиентскую программу.

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using TypeEquivalenceInterface;
    using System.Reflection;

    namespace TypeEquivalenceClient
    {
        class Program
        {
            static void Main(string[] args)
            {
                Assembly sampleAssembly = Assembly.Load("TypeEquivalenceRuntime");
                ISampleInterface sampleClass =
                    (ISampleInterface)sampleAssembly.CreateInstance("TypeEquivalenceRuntime.SampleClass");
                sampleClass.GetUserInput();
                Console.WriteLine(sampleClass.UserInput);
                Console.WriteLine(sampleAssembly.GetName().Version.ToString());
                Console.ReadLine();
            }
        }
    }
    ```

7. Нажмите сочетание клавиш CTRL+F5, чтобы собрать и запустить программу.

## <a name="modifying-the-interface"></a>Изменение интерфейса

#### <a name="to-modify-the-interface"></a>Изменение интерфейса

1. В Visual Studio откройте меню **Файл**, наведите указатель мыши на пункт **Создать** и щелкните **Проект/решение**.

2. В диалоговом окне **Открыть проект** щелкните проект TypeEquivalenceInterface правой кнопкой мыши и выберите пункт **Свойства**. Перейдите на вкладку **Приложение** . Нажмите кнопку **Сведения о сборке**. Измените значения параметров **Версия сборки** и **Версия файла** на `2.0.0.0`.

3. Откройте файл SampleInterface.cs. Добавьте в интерфейс ISampleInterface следующую строку кода.

    ```csharp
    DateTime GetDate();
    ```

    Сохраните файл.

4. Сохраните проект.

5. Щелкните проект TypeEquivalenceInterface правой кнопкой мыши и выберите пункт **Сборка**. Новая версия DLL-файла библиотеки классов компилируется и сохраняется по указанному выходному пути (например, C:\TypeEquivalenceSample).

## <a name="modifying-the-runtime-class"></a>Изменение класса среды выполнения

#### <a name="to-modify-the-runtime-class"></a>Изменение класса среды выполнения

1. В Visual Studio откройте меню **Файл**, наведите указатель мыши на пункт **Создать** и щелкните **Проект/решение**.

2. В диалоговом окне **Открыть проект** щелкните проект TypeEquivalenceRuntime правой кнопкой мыши и выберите **Свойства**. Перейдите на вкладку **Приложение** . Нажмите кнопку **Сведения о сборке**. Измените значения параметров **Версия сборки** и **Версия файла** на `2.0.0.0`.

3. Откройте файл SampleClass.cs. Добавьте в класс SampleClass следующие строки кода.

    ```csharp
    public DateTime GetDate()
    {
        return DateTime.Now;
    }
    ```

    Сохраните файл.

4. Сохраните проект.

5. Щелкните проект TypeEquivalenceRuntime правой кнопкой мыши и выберите пункт **Сборка**. Обновленная версия DLL-файла библиотеки классов компилируется и сохраняется по указанному ранее выходному пути для сборки (например, C:\TypeEquivalenceSample).

6. В проводнике откройте папку выходного пути (например, C:\TypeEquivalenceSample). Дважды щелкните файл TypeEquivalenceClient.exe, чтобы выполнить программу. Новая версия сборки TypeEquivalenceRuntime отображается в программе без повторной компиляции.

## <a name="see-also"></a>См. также

- [/link (параметры компилятора C#)](../../../language-reference/compiler-options/link-compiler-option.md)
- [Руководство по программированию на C#](../../index.md)
- [Программирование с использованием сборок](../../../../framework/app-domains/programming-with-assemblies.md)
- [Сборки в .NET](../../../../standard/assembly/index.md)
