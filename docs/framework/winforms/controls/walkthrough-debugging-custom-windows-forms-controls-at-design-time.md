---
title: Пошаговое руководство. Отладка пользовательских элементов управления Windows Forms во время разработки
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- debugging [Visual Studio], walkthroughs
- custom controls [Windows Forms], walkthroughs
- visual editors
- debugging [Visual Studio], Windows Forms
- custom controls [Windows Forms], debugging
- designers
- controls [Windows Forms], debugging
- walkthroughs [Windows Forms], debugging
- design-time debugging
ms.assetid: 1fd83ccd-3798-42fc-85a3-6cba99467387
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 824d8a7de8e9e37899cb84d6cee9621f84a5bc65
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015701"
---
# <a name="walkthrough-debug-custom-windows-forms-controls-at-design-time"></a>Пошаговое руководство. Отладка пользовательских элементов управления Windows Forms во время разработки

При создании пользовательского элемента управления часто возникает необходимость в отладке его поведения во время разработки. Это особенно справедливо при создании пользовательского конструктора для пользовательского элемента управления. Дополнительные сведения см. [в разделе Пошаговое руководство. Создание элемента управления Windows Forms, который использует преимущества функций](creating-a-wf-control-design-time-features.md)времени разработки Visual Studio.

Вы можете выполнять отладку пользовательских элементов управления с помощью Visual Studio точно так же, как при отладке любых других классов .NET Framework. Разница заключается в том, что будет выполняться отладка отдельного экземпляра Visual Studio, на котором выполняется код пользовательского элемента управления.

## <a name="create-the-project"></a>Создание проекта

Первым шагом является создание проекта приложения. Этот проект будет использоваться для создания приложения, в котором размещается пользовательский элемент управления.

В Visual Studio создайте проект приложения Windows и назовите его **дебуггинжексампле**.

## <a name="create-the-control-library-project"></a>Создание проекта библиотеки элементов управления

1. Добавьте в решение проект **библиотеки элементов управления Windows** .

2. Добавьте новый элемент **UserControl** в проект дебугконтроллибрари. Назовите его **дебугконтрол**.

3. В **Обозреватель решений**удалите элемент управления проекта по умолчанию, удалив файл кода с базовым именем UserControl1.

4. Постройте решение.

## <a name="checkpoint"></a>Контрольная точка

На этом этапе вы сможете увидеть пользовательский элемент управления на **панели элементов**.

Чтобы проверить ход выполнения, найдите новую вкладку с именем **компоненты дебугконтроллибрари** и щелкните, чтобы выбрать ее. При открытии элемент управления отображается в списке как **дебугконтрол** со значком по умолчанию рядом с ним.

## <a name="add-a-property-to-your-custom-control"></a>Добавление свойства в пользовательский элемент управления

Чтобы продемонстрировать, что код пользовательского элемента управления выполняется во время разработки, добавьте свойство и задайте точку останова в коде, который реализует свойство.

1. Откройте **дебугконтрол** в **редакторе кода**. Добавьте следующий код в определение класса:

    ```vb
    Private demoStringValue As String = Nothing
    <BrowsableAttribute(true)>
    Public Property DemoString() As String

        Get
            Return Me.demoStringValue
        End Get

        Set(ByVal value As String)
            Me.demoStringValue = value
        End Set

    End Property
    ```

    ```csharp
    private string demoStringValue = null;
    [Browsable(true)]
    public string DemoString
    {
        get
        {
            return this.demoStringValue;
        }
        set
        {
            demoStringValue = value;
        }
    }
    ```

2. Постройте решение.

## <a name="add-your-custom-control-to-the-host-form"></a>Добавление пользовательского элемента управления в форму размещения

Чтобы отладить поведение пользовательского элемента управления во время разработки, необходимо разместить экземпляр класса пользовательского элемента управления в форме узла.

1. В проекте "Дебуггинжексампле" откройте Form1 в **конструктор Windows Forms**.

2. На **панели элементов**откройте вкладку **компоненты дебугконтроллибрари** и перетащите экземпляр **дебугконтрол** на форму.

3. Найдите пользовательское свойство в окне **Свойства.** `DemoString` Обратите внимание, что его значение можно изменить так же, как любое другое свойство. Также обратите внимание, `DemoString` что при выборе свойства строка описания свойства отображается в нижней части окна **Свойства** .

## <a name="set-up-the-project-for-design-time-debugging"></a>Настройка проекта для отладки во время разработки

Для отладки поведения пользовательского элемента управления во время разработки будет выполняться отладка отдельного экземпляра Visual Studio, на котором выполняется код пользовательского элемента управления.

1. Щелкните правой кнопкой мыши проект **дебугконтроллибрари** в **Обозреватель решений** и выберите пункт **Свойства**.

2. На странице свойств **дебугконтроллибрари** выберите вкладку Отладка .

     В разделе **действие при запуске** выберите **Запуск внешней программы**. Вы будете выполнять отладку отдельного экземпляра Visual Studio, поэтому нажмите кнопку с многоточием![(...) в окно свойств в Visual Studio](./media/visual-studio-ellipsis-button.png)), чтобы найти интегрированную среду разработки Visual Studio. Имя исполняемого файла — **devenv. exe**, и если вы установили в расположение по умолчанию, его путь: *% ProgramFiles (x86)% \ Microsoft Visual Studio\2019\\\<Edition > \Common7\IDE*.

3. Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно.

4. Щелкните правой кнопкой мыши проект **дебугконтроллибрари** и выберите **Назначить запускаемым проектом** , чтобы включить эту конфигурацию отладки.

## <a name="debug-your-custom-control-at-design-time"></a>Отладка пользовательского элемента управления во время разработки

Теперь вы готовы к отладке пользовательского элемента управления, как он выполняется в режиме конструктора. При запуске сеанса отладки будет создан новый экземпляр Visual Studio, который будет использоваться для загрузки решения "Дебуггинжексампле". При открытии формы Form1 в **конструкторе форм**будет создан экземпляр пользовательского элемента управления и начнется его выполнение.

1. Откройте исходный файл **дебугконтрол** в **редакторе кода** и поместите `Set` точку останова в метод доступа `DemoString` свойства.

2. Нажмите клавишу **F5** , чтобы запустить сеанс отладки. Создается новый экземпляр Visual Studio. Можно различать экземпляры двумя способами:

    - Экземпляр отладки содержит слово, которое **выполняется** в заголовке окна

    - В экземпляре отладки на панели инструментов **отладки** отключена кнопка " **Пуск** "

   Точка останова задается в экземпляре отладки.

3. В новом экземпляре Visual Studio откройте решение "Дебуггинжексампле". Решение можно легко найти, выбрав **последние проекты** в меню **файл** . Файл решения "Дебуггинжексампле. sln" будет указан как самый последний использовавшийся файл.

4. Откройте форму Form1 в **конструкторе форм** и выберите элемент управления **дебугконтрол** .

5. Измените значение свойства `DemoString` . При фиксации изменения экземпляр отладки Visual Studio получает фокус и выполнение останавливается в точке останова. Метод доступа к свойству можно выполнить одним шагом, как и любой другой код.

6. Чтобы прекратить отладку, выйдите из размещенного экземпляра Visual Studio или нажмите кнопку " **прекратить отладку** " в экземпляре отладки.

## <a name="next-steps"></a>Следующие шаги

Теперь, когда вы можете выполнять отладку пользовательских элементов управления во время разработки, существует множество возможностей расширения взаимодействия элемента управления с интегрированной средой разработки Visual Studio.

- <xref:System.ComponentModel.Component.DesignMode%2A> Свойство<xref:System.ComponentModel.Component> класса можно использовать для написания кода, который будет выполняться только во время разработки. Дополнительные сведения см. в разделе <xref:System.ComponentModel.Component.DesignMode%2A>.

- Существует несколько атрибутов, которые можно применить к свойствам элемента управления, чтобы управлять взаимодействием пользовательского элемента управления с конструктором. Эти атрибуты можно найти в <xref:System.ComponentModel?displayProperty=nameWithType> пространстве имен.

- Можно написать пользовательский конструктор для пользовательского элемента управления. Это дает полный контроль над процессом разработки с помощью расширяемой инфраструктуры конструктора, предоставляемой Visual Studio. Дополнительные сведения см. [в разделе Пошаговое руководство. Создание элемента управления Windows Forms, который использует преимущества функций](creating-a-wf-control-design-time-features.md)времени разработки Visual Studio.

## <a name="see-also"></a>См. также

- [Пошаговое руководство: Создание элемента управления Windows Forms, который использует преимущества функций времени разработки Visual Studio](creating-a-wf-control-design-time-features.md)
