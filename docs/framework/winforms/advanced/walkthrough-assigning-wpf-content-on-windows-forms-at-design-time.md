---
title: Пошаговое руководство. Назначение содержимого WPF для формы Windows Forms во время разработки
ms.date: 03/30/2017
helpviewer_keywords:
- WPF content [Windows Forms], assigning at design time
- ElementHost control [Windows Forms], assigning WPF content at design time
- interoperability [WPF]
- Windows Forms, content assignments
- WPF user control [Windows Forms], hosting in Windows Forms
ms.assetid: b3e9ef93-7e0f-4a2f-8f1e-3437609a1eb7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bc5f5e2d8808c0a60df721bf2c0ed76b45ef49a0
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666259"
---
# <a name="walkthrough-assign-wpf-content-on-windows-forms-at-design-time"></a>Пошаговое руководство. Назначение содержимого WPF на Windows Forms во время разработки

В этой статье показано, как выбрать типы элементов управления Windows Presentation Foundation (WPF), которые должны отображаться в форме. Можно выбрать любые типы элементов управления WPF, включенные в проект.

## <a name="prerequisites"></a>Предварительные требования

Для выполнения шагов, описанных в этом руководстве, вам понадобится Visual Studio.

## <a name="create-the-project"></a>Создание проекта

Откройте Visual Studio и создайте новый проект Windows Forms приложения в Visual Basic или Visual C# с именем `SelectingWpfContent`.

> [!NOTE]
> При размещении содержимого WPF поддерживаются только проекты C# и Visual Basic.

## <a name="create-the-wpf-control-types"></a>Создание типов элементов управления WPF

После добавления типов элементов управления WPF в проект их можно разместить в разных элементах управления <xref:System.Windows.Forms.Integration.ElementHost>.

1. Добавьте в решение новый проект WPF <xref:System.Windows.Controls.UserControl>. Используйте имя по умолчанию для этого типа элемента управления (`UserControl1.xaml`). Дополнительные сведения см. в разделе [Пошаговое руководство: Создание нового содержимого WPF на Windows Forms во время](walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)разработки.

2. Убедитесь в том, что элемент `UserControl1` выбран в представлении конструирования.

3. В окне **Свойства** задайте для свойств <xref:System.Windows.FrameworkElement.Width%2A> и <xref:System.Windows.FrameworkElement.Height%2A> значение **200**.

4. Добавьте элемент управления <xref:System.Windows.Controls.UserControl> в и <xref:System.Windows.Controls.TextBox.Text%2A> задайте в качестве значения свойства **размещенное содержимое**. <xref:System.Windows.Controls.TextBox?displayProperty=nameWithType>

5. Добавьте в проект второй элемент управления WPF <xref:System.Windows.Controls.UserControl>. Используйте имя по умолчанию для этого типа элемента управления (`UserControl2.xaml`).

6. В окне **Свойства** задайте для свойств <xref:System.Windows.FrameworkElement.Width%2A> и <xref:System.Windows.FrameworkElement.Height%2A> значение **200**.

7. Добавьте элемент управления <xref:System.Windows.Controls.UserControl> в и <xref:System.Windows.Controls.TextBox.Text%2A> задайте для свойства значение **размещенное содержимое 2**. <xref:System.Windows.Controls.TextBox?displayProperty=nameWithType>

   > [!NOTE]
   > Обычно размещается более сложное содержимое WPF. Элемент управления <xref:System.Windows.Controls.TextBox?displayProperty=nameWithType> используется здесь в целях наглядности.

8. Выполните построение проекта.

## <a name="select-wpf-controls"></a>Выбор элементов управления WPF

Для элемента управления <xref:System.Windows.Forms.Integration.ElementHost>, в котором уже размещено содержимое, можно назначить различное содержимое WPF.

1. Откройте `Form1` в конструкторе Windows Forms.

2. На **панели элементов**дважды щелкните `UserControl1` , чтобы `UserControl1` создать экземпляр в форме.

   Экземпляр `UserControl1` размещается в новом элементе управления <xref:System.Windows.Forms.Integration.ElementHost> с именем `elementHost1`.

3. На панели смарт-тегов для `elementHost1`откройте раскрывающийся список **выберите размещенное содержимое** .

4. В раскрывающемся списке выберите **UserControl2** .

   В элементе управления `elementHost1` теперь будет размещен экземпляр типа `UserControl2`.

5. В окне **Свойства** убедитесь, что <xref:System.Windows.Forms.Integration.ElementHost.Child%2A> для свойства задано значение **UserControl2**.

6. Из **панели элементов**в группе **взаимодействие WPF** перетащите <xref:System.Windows.Forms.Integration.ElementHost> элемент управления на форму.

   Имя по умолчанию для нового элемента управления — `elementHost2`.

7. На панели смарт-тегов для `elementHost2`откройте раскрывающийся список **выберите размещенное содержимое** .

8. Выберите элемент **UserControl1** из раскрывающегося списка.

9. В элементе управления `elementHost2` теперь будет размещен экземпляр типа `UserControl1`.

## <a name="see-also"></a>См. также

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Миграция и взаимодействие систем](../../wpf/advanced/migration-and-interoperability.md)
- [Использование элементов управления WPF](using-wpf-controls.md)
- [Проектирование XAML в Visual Studio](/visualstudio/designers/designing-xaml-in-visual-studio)
