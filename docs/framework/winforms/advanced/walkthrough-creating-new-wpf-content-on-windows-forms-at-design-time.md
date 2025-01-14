---
title: Пошаговое руководство. Создание содержимого WPF для формы Windows Forms во время разработки
ms.date: 08/18/2018
helpviewer_keywords:
- interoperability [Windows Forms], WPF and Windows Forms
- WPF content [Windows Forms], hosting in Windows Forms
- hosting WPF content in Windows Forms
- ElementHost control
- WPF user control [Windows Forms], hosting in Windows Forms
ms.assetid: 2e92d8e8-f0e4-4df7-9f07-2acf35cd798c
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 5e5112aa0b025648ce68a93f0f3da026ec99fe89
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987137"
---
# <a name="walkthrough-create-new-wpf-content-on-windows-forms-at-design-time"></a>Пошаговое руководство. Создание нового содержимого WPF на Windows Forms во время разработки

В этой статье показано, как создать элемент управления Windows Presentation Foundation (WPF) для использования в приложениях на основе Windows Forms.

## <a name="prerequisites"></a>Предварительные требования

Для выполнения шагов, описанных в этом руководстве, вам понадобится Visual Studio.

## <a name="create-the-project"></a>Создание проекта

Откройте Visual Studio и создайте новый проект **Windows Forms приложения (.NET Framework)** в Visual Basic или Visual C# с именем `HostingWpf`.

> [!NOTE]
> При размещении содержимого WPF поддерживаются только проекты C# и Visual Basic.

## <a name="create-a-new-wpf-control"></a>Создание нового элемента управления WPF

Создать элемент управления WPF и добавить его в проект можно так же легко, как добавить в проект любой другой элемент. Конструктор Windows Forms работает с определенным видом элемента управления с именем *составного элемента*управления или *пользовательским элементом управления*. Подробнее о пользовательских элементах управления WPF см. в разделе <xref:System.Windows.Controls.UserControl>.

> [!NOTE]
> Тип <xref:System.Windows.Controls.UserControl?displayProperty=nameWithType> для элементов управления WPF отличается от типа пользовательских элементов управления, предоставляемого Windows Forms, который также называется <xref:System.Windows.Forms.UserControl?displayProperty=nameWithType>.

Чтобы создать новый элемент управления WPF, сделайте следующее:

1. В **Обозреватель решений**добавьте в решение новый проект **библиотеки пользовательских элементов управления WPF (.NET Framework)** . Используйте имя по умолчанию для библиотеки элементов управления (`WpfControlLibrary1`). Имя элемента управления по умолчанию — `UserControl1.xaml`.

   Добавление нового элемента управления имеет следующие последствия.

   - Добавляется файл UserControl1.xaml.

   - Добавлен файл UserControl1.xaml.cs (или UserControl1. XAML. vb). Этот файл содержит код программной части для обработчиков событий и иных реализованных компонентов.

   - Добавляются ссылки на сборки WPF.

   - Файл UserControl1. XAML откроется в конструкторе WPF для Visual Studio.

2. Убедитесь в том, что элемент `UserControl1` выбран в представлении конструирования.

3. В окне **Свойства** задайте для свойств <xref:System.Windows.FrameworkElement.Width%2A> и <xref:System.Windows.FrameworkElement.Height%2A> значение **200**.

4. Перетащите<xref:System.Windows.Controls.TextBox?displayProperty=nameWithType> элемент управления из области **элементов**в область конструктора.

5. В окне **Свойства** присвойте <xref:System.Windows.Controls.TextBox.Text%2A> свойству значение **размещенное содержимое**.

   > [!NOTE]
   > Обычно размещается более сложное содержимое WPF. Элемент управления <xref:System.Windows.Controls.TextBox?displayProperty=nameWithType> используется здесь в целях наглядности.

6. Выполните построение проекта.

## <a name="add-a-wpf-control-to-a-windows-form"></a>Добавление элемента управления WPF в форму Windows Forms

Новый элемент управления WPF готов к использованию в форме. Windows Forms использует <xref:System.Windows.Forms.Integration.ElementHost> элемент управления для размещения содержимого WPF.

Чтобы добавить элемент управления WPF в форму Windows Forms, выполните следующие действия.

1. Откройте `Form1` в конструкторе Windows Forms.

2. На **панели элементов**найдите вкладку с надписью **впфусерконтроллибрари User Controls (пользовательские элементы управления WPF**).

3. Перетащите экземпляр `UserControl1` в форму.

    - Для размещения элемента управления WPF на форме будет автоматически создан элемент управления <xref:System.Windows.Forms.Integration.ElementHost>.

    - <xref:System.Windows.Forms.Integration.ElementHost.Child%2A> Элемент управления называется, и в окне Свойства можно увидеть, что его свойство имеет значение UserControl1. `elementHost1` <xref:System.Windows.Forms.Integration.ElementHost>

    - В проект добавляются ссылки на сборки WPF.

    - Элемент управления `elementHost1` имеет панель смарт-тегов, на которой приводятся имеющиеся параметры размещения.

4. На панели смарт-тегов **Задачи ElementHost** выберите закрепить **в родительском контейнере**.

5. Нажмите клавишу **F5**, чтобы выполнить сборку приложения и запустить его.

## <a name="next-steps"></a>Следующие шаги

Windows Forms и WPF — это разные технологии, но они предназначены для тесного взаимодействия. Чтобы обеспечить расширенный внешний вид и поведение приложений, попробуйте выполнить следующие действия.

- Размещение элемента управления Windows Forms на странице WPF. Дополнительные сведения см. в разделе [Пошаговое руководство: Размещение элемента управления Windows Forms в WPF](../../wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md).

- Применение стилей оформления Windows Forms к содержимому WPF. Дополнительные сведения см. в разделе [Практическое руководство. Включение визуальных стилей в гибридном](../../wpf/advanced/how-to-enable-visual-styles-in-a-hybrid-application.md)приложении.

- Изменение стиля оформления содержимого WPF. Дополнительные сведения см. в разделе [Пошаговое руководство: Стилизация содержимого](walkthrough-styling-wpf-content.md)WPF.

## <a name="see-also"></a>См. также

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Миграция и взаимодействие систем](../../wpf/advanced/migration-and-interoperability.md)
- [Использование элементов управления WPF](using-wpf-controls.md)
- [Проектирование XAML в Visual Studio](/visualstudio/designers/designing-xaml-in-visual-studio)
