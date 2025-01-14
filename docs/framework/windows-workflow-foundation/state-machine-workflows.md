---
title: Рабочие процессы конечного автомата
ms.date: 03/30/2017
ms.assetid: 344caacd-bf3b-4716-bd5a-eca74fc5a61d
ms.openlocfilehash: 7b655208f4cc8274cdc5a8dad68ff1fa9eaad5ef
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69948986"
---
# <a name="state-machine-workflows"></a>Рабочие процессы конечного автомата
Конечный автомат - широко известный принцип разработки программ. Действие <xref:System.Activities.Statements.StateMachine>, а также <xref:System.Activities.Statements.State>, <xref:System.Activities.Statements.Transition> и другие действия могут использоваться для сборки программ рабочего процесса конечных автоматов. В этом разделе представлены общие сведения о создании рабочих процессов конечного автомата.  
  
## <a name="state-machine-workflow-overview"></a>Общие сведения о рабочем процессе конечного автомата  
 Рабочие процессы конечного автомата обеспечивают стиль моделирования, с помощью которого можно моделировать рабочий процесс в режиме, управляемом событиями. Действие <xref:System.Activities.Statements.StateMachine> содержит состояния и переходы, которые образуют логику конечного автомата и могут использоваться везде, где может использоваться действие. В среде выполнения конечного автомата существуют следующие классы.  
  
- <xref:System.Activities.Statements.StateMachine>  
  
- <xref:System.Activities.Statements.State>  
  
- <xref:System.Activities.Statements.Transition>  
  
 В ходе создания рабочего процесса конечного автомата состояния добавляются к действию <xref:System.Activities.Statements.StateMachine>, а переходы используются для управления переключением между состояниями. На следующем снимке экрана [Начало работы](getting-started-tutorial.md) пошаговое [руководство. Создание рабочего процесса](how-to-create-a-state-machine-workflow.md)конечного автомата. показывает рабочий процесс конечного автомата с тремя состояниями и тремя переходами. **Целевой объект инициализации** является начальным состоянием и представляет первое состояние в рабочем процессе. Это означает строка, которая начинается с **начального** узла. Конечное состояние в рабочем процессе называется **FinalState**и представляет точку, в которой завершается рабочий процесс.  
  
 ![Иллюстрация, показывающая Завершенный рабочий процесс конечного автомата.](./media/state-machine-workflows/complete-state-machine-workflow.jpg)  
  
 Рабочий процесс конечного автомата должен содержать только одно начальное состояние и хотя бы одно конечное состояние. Каждое состояние, отличное от конечного, должно иметь по крайней мере один переход. В следующих разделах описывается создание и настройка состояний и переходов.  
  
## <a name="creating-and-configuring-states"></a>Создание и настройка состояний  
 <xref:System.Activities.Statements.State> представляет состояние, в котором может находиться конечный автомат. Чтобы <xref:System.Activities.Statements.State> добавить к рабочему процессу, перетащите конструктор активности **состояний** из раздела **конечный автомат** **области элементов** <xref:System.Activities.Statements.StateMachine> [!INCLUDE[wfd1](../../../includes/wfd1-md.md)] и поместите его на действие на поверхности.  
  
 ![Снимок экрана: раздел "конечный автомат" области элементов.](./media/state-machine-workflows/state-machine-section-toolbox.jpg)  
  
 Чтобы настроить состояние в качестве **начального состояния**, щелкните правой кнопкой мыши состояние и выберите **задать в качестве начального состояния**. Кроме того, если текущее начальное состояние отсутствует, исходное состояние можно назначить, перетащив строку с **начального** узла в начало рабочего процесса в нужное состояние. При перетаскивании действия в конструктор рабочих процессов он предварительно настраивается с начальным состоянием с именем **State1.** <xref:System.Activities.Statements.StateMachine> Рабочий процесс конечного автомата должен содержать только одно начальное состояние.  
  
 Состояние, которое представляет завершающее состояние в конечном автомате, называется конечным состоянием. Конечное состояние - это состояние, для свойства <xref:System.Activities.Statements.State.IsFinal%2A> которого задано значение `true`, которое не имеет действия <xref:System.Activities.Statements.State.Exit%2A>, а также не имеет переходов, исходящих из него. Чтобы добавить конечное состояние в рабочий процесс, перетащите конструктор действий **FinalState** из раздела **конечный автомат** на **панели элементов** <xref:System.Activities.Statements.StateMachine> и поместите его [!INCLUDE[wfd1](../../../includes/wfd1-md.md)] на действие на поверхности. Рабочий процесс конечного автомата должен иметь как минимум одно конечное состояние.  
  
### <a name="configuring-entry-and-exit-actions"></a>Настройка действия входа и выхода  
 Состояние может иметь действия <xref:System.Activities.Statements.State.Entry%2A> и <xref:System.Activities.Statements.State.Exit%2A>. Состояние, настроенное как конечное состояние, может содержать только действия входа. Когда экземпляр рабочего процесса входит в состояние, выполняются все действия, находящиеся в действии входа. После завершения действия входа планируются триггеры для переходов состояния. При подтверждении перехода к другому состоянию выполняются действия в действии выхода, даже если осуществляется переход в то же самое состояние. После завершения действия выхода выполняются действия, находящиеся в действии перехода, а затем выполняется переход в новое состояние, и потом производится планирование его действий входа.  
  
> [!NOTE]
> При отладке рабочего процесса конечного автомата точки останова можно поместить в корневое действие конечного автомата и в действия в рабочем процессе конечного автомата. Точки останова нельзя размещать непосредственно на переходах, однако их можно размещать на любых действиях, которые содержатся в состояниях и переходах.  
  
## <a name="creating-and-configuring-transitions"></a>Создание и настройка переходов  
 Все состояния, кроме конечного, должны иметь по крайней мере один переход. Конечное состояние не должно иметь переходов. Переходы можно добавлять после добавления состояния в рабочий процесс конечного автомата, а также при сбросе состояния в область конструктора.  
  
 <xref:System.Activities.Statements.State> Чтобы добавить и создать переход за один шаг, перетащите действие **State** из раздела **конечный автомат** **области элементов** и наведите его на другое состояние в конструкторе рабочих процессов. При наведении <xref:System.Activities.Statements.State> на другое <xref:System.Activities.Statements.State> вокруг другого <xref:System.Activities.Statements.State> будут отображены четыре треугольника. Если объект <xref:System.Activities.Statements.State> бросить в один из четырех треугольников, он будет добавлен к конечному автомату, а также будет добавлен переход состояния из исходного <xref:System.Activities.Statements.State> в сброшенное целевое <xref:System.Activities.Statements.State>. Дополнительные сведения см. в разделе [конструктор действий перехода](/visualstudio/workflow-designer/transition-activity-designer).  
  
 После создания состояния существует два способа создания переходов. Первый способ - можно перетащить состояние из рабочей области конструктора рабочих процессов, навести его на существующее состояние и поместить на одну из точек перетаскивания. Это очень похоже на метод, описанный в предыдущем разделе. Можно также навести мышь на выбранное состояние источника и перетащить линию до нужного целевого состояния.  
  
> [!NOTE]
> Для одного состояния в конечном автомате может быть создано до 76 переходов в конструкторе рабочих процессов. Количество переходов состояний для рабочих процессов, созданных за пределами конструктора, ограничивается только системными ресурсами.  
  
 Переход может содержать объекты <xref:System.Activities.Statements.Transition.Trigger%2A>, <xref:System.Activities.Statements.Transition.Condition%2A> и <xref:System.Activities.Statements.Transition.Action%2A>. <xref:System.Activities.Statements.Transition.Trigger%2A> перехода планируется после завершения действия <xref:System.Activities.Statements.State.Entry%2A> исходного состояния перехода. Обычно <xref:System.Activities.Statements.Transition.Trigger%2A> представляет собой действие, ожидающее появления определенного типа события, но он может быть любым действием или даже не иметь действия. После завершения действия <xref:System.Activities.Statements.Transition.Trigger%2A> вычисляется значение <xref:System.Activities.Statements.Transition.Condition%2A> (если существует). Если действие <xref:System.Activities.Statements.Transition.Trigger%2A> отсутствует, выполняется немедленное вычисление условия <xref:System.Activities.Statements.Transition.Condition%2A>. Если условие оказывается равным `false`, то переход отменяется, а действие <xref:System.Activities.Statements.Transition.Trigger%2A> для всех переходов из состояния планируется заново. Если существуют другие переходы, которые совместно используют одно и то же исходное состояние, что и текущий переход, эти действия <xref:System.Activities.Statements.Transition.Trigger%2A> также отменяются и планируются повторно. Если <xref:System.Activities.Statements.Transition.Condition%2A> имеет значение `true` или условие отсутствует, выполняется действие <xref:System.Activities.Statements.State.Exit%2A> исходного состояния, а затем выполняется <xref:System.Activities.Statements.Transition.Action%2A> перехода. По завершении управление передается в целевое состояние <xref:System.Activities.Statements.Transition.Action%2A>  
  
 Переходы, имеющие общий триггер, называются переходами с общим триггером. Каждый переход в группе переходов с общим триггером имеет один и тот же триггер, но уникальные условие <xref:System.Activities.Statements.Transition.Condition%2A> и действие. Чтобы добавить дополнительные действия в переход и создать общий переход, щелкните круг, указывающий начало нужного перехода, и перетащите его в нужное состояние. Новый переход будет совместно использовать тот же триггер, что и исходный переход, но будет иметь уникальное условие и действие. Общие переходы также можно создать в конструкторе переходов, щелкнув **Добавить общий переход триггера** в нижней части конструктора переходов, а затем выбрав нужное целевое состояние из **доступных состояний для подключения** . раскрывающийся список.  
  
> [!NOTE]
> Обратите внимание, что если состояние <xref:System.Activities.Statements.Transition.Condition%2A> перехода оценивается как `False` (или все условия общего перехода триггера оцениваются как `False`), переход не выполняется, а все триггеры для всех переходов из состояния будут запланированы заново.  
  
 Дополнительные сведения о создании рабочих процессов конечного автомата см [. в разделе как Создайте](how-to-create-a-state-machine-workflow.md)рабочий процесс конечного автомата, [конструктор действий StateMachine](/visualstudio/workflow-designer/statemachine-activity-designer), [конструктор действий состояния](/visualstudio/workflow-designer/state-activity-designer), конструктор [действий FinalState](/visualstudio/workflow-designer/finalstate-activity-designer)и [конструктор действий перехода](/visualstudio/workflow-designer/transition-activity-designer).  
  
## <a name="state-machine-terminology"></a>Терминология конечного автомата  
 В этом разделе описывается словарь конечного автомата, используемый на протяжении данного раздела.  
  
 Область  
 Блок, который составляет основу конечного автомата. Конечный автомат может находиться в одном определенном состоянии в любой момент времени.  
  
 Действие входа  
 Действие, выполняемое при входе в состояние  
  
 Действие выхода  
 Действие, выполняемое при выходе из состояния  
  
 Переход  
 Прямая связь между двумя состояниями, которые представляют полную реакцию конечного автомата на возникновение события определенного типа.  
  
 Общий переход  
 Переход, который имеет общее исходное состояние и триггер с одним или несколькими переходами, но уникальное условие и действие.  
  
 Триггер  
 Запускающее действие, которое вызывает переход.  
  
 Условие  
 Ограничение, которое вычисляется в `true` после выполнения триггера, чтобы допустить завершение перехода.  
  
 Действие перехода  
 Действие, которое выполняется при выполнении определенного перехода.  
  
 Переход по условию  
 Переход с явным условием.  
  
 Переход на себя  
 Переход от состояния к тому же состоянию.  
  
 Начальное состояние  
 Состояние, которое представляет начальную точку конечного автомата.  
  
 Конечное состояние  
 Состояние, представляющее завершение конечного автомата.  
  
## <a name="see-also"></a>См. также

- [Практическое руководство. Создание рабочего процесса конечного автомата](how-to-create-a-state-machine-workflow.md)
- [Конструктор действия StateMachine](/visualstudio/workflow-designer/statemachine-activity-designer)
- [Конструктор действия State](/visualstudio/workflow-designer/state-activity-designer)
- [Конструктор действия FinalState](/visualstudio/workflow-designer/finalstate-activity-designer)
- [Конструктор действий переходов](/visualstudio/workflow-designer/transition-activity-designer)
