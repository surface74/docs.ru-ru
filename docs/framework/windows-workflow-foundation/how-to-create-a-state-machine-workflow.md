---
title: Практическое руководство. Создание рабочего процесса конечного автомата
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3ec60e8f-fad4-493e-a426-e7962d7aee8c
ms.openlocfilehash: 451f9581ae997ad86fee968fa978713db2049455
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044389"
---
# <a name="how-to-create-a-state-machine-workflow"></a>Практическое руководство. Создание рабочего процесса конечного автомата
Рабочие процессы могут создаваться как из встроенных, так и из пользовательских действий. В этом разделе описывается создание рабочего процесса, который использует как встроенные действия, такие как <xref:System.Activities.Statements.StateMachine> действие, так и пользовательские действия из предыдущего [руководства. Создание раздела действия](how-to-create-an-activity.md) . Рабочий процесс моделирует игру по угадыванию числа.  
  
> [!NOTE]
> Каждый раздел в учебнике «Приступая к работе» построен на основе предыдущих разделов. Для выполнения этой статьи сначала необходимо выполнить [следующие действия: Создайте действие](how-to-create-an-activity.md).  
  
> [!NOTE]
> Чтобы скачать завершенную версию учебника, см. раздел [Windows Workflow Foundation (WF45), учебник "Приступая к работе"](https://go.microsoft.com/fwlink/?LinkID=248976).  
  
### <a name="to-create-the-workflow"></a>Создание рабочего процесса  
  
1. Щелкните правой кнопкой мыши **NumberGuessWorkflowActivities** в **Обозреватель решений** и выберите **добавить**, **новый элемент**.  
  
2. В узле **установленные** **Общие элементы** выберите **Рабочий процесс**. Выберите **действие** из списка **Рабочий процесс** .  
  
3. Введите `StateMachineNumberGuessWorkflow` в поле **имя** и нажмите кнопку **Добавить**.  
  
4. Перетащите действие **StateMachine** из раздела **конечный автомат** на **панели элементов** и поместите его в метку **Перетащите сюда действие** в рабочей области конструктора рабочих процессов.  
  
### <a name="to-create-the-workflow-variables-and-arguments"></a>Создание переменных и аргументов рабочего процесса  
  
1. Дважды щелкните **StateMachineNumberGuessWorkflow. XAML** в **Обозреватель решений** , чтобы отобразить рабочий процесс в конструкторе, если он еще не отображается.  
  
2. Щелкните **аргументы** в левой нижней части конструктора рабочих процессов, чтобы отобразить панель **аргументы** .  
  
3. Нажмите кнопку **Создать аргумент**.  
  
4. Введите `MaxNumber` в поле **имя** , выберите **в** раскрывающемся списке **направление** значение **Int32** , а затем нажмите клавишу ВВОД , чтобы сохранить аргумент.  
  
5. Нажмите кнопку **Создать аргумент**.  
  
6. Введите `Turns` в поле **имя** , которое находится ниже вновь добавленного `MaxNumber` аргумента, выберите из раскрывающегося списка **направление** , выберите **Int32** из раскрывающегося списка **тип аргумента** и нажмите клавишу ВВОД.  
  
7. Щелкните **аргументы** в нижней левой части конструктора операций, чтобы закрыть панель **аргументы** .  
  
8. Щелкните **переменные** в левой нижней части конструктора рабочих процессов, чтобы отобразить панель **переменные** .  
  
9. Нажмите кнопку **создать переменную**.  
  
    > [!TIP]
    > Если поле **создать переменную** не отображается, щелкните <xref:System.Activities.Statements.StateMachine> действие в области конструктора рабочих процессов, чтобы выбрать его.  
  
10. Введите `Guess` в поле **имя** , выберите **Int32** в раскрывающемся списке **тип переменной** и нажмите клавишу ВВОД, чтобы сохранить переменную.  
  
11. Нажмите кнопку **создать переменную**.  
  
12. Введите `Target` в поле **имя** , выберите **Int32** в раскрывающемся списке **тип переменной** и нажмите клавишу ВВОД, чтобы сохранить переменную.  
  
13. Щелкните **переменные** в левой нижней части конструктора действий, чтобы закрыть панель **переменные** .  
  
### <a name="to-add-the-workflow-activities"></a>Добавление действий рабочего процесса  
  
1. Щелкните **State1** , чтобы выбрать его. В **окне Свойства**измените **DisplayName** на `Initialize Target`.  
  
    > [!TIP]
    > Если **окно Свойства** не отображается, в меню **вид** выберите пункт **окно свойств** .  
  
2. Дважды щелкните только что переименованное целевое состояние **инициализации** в конструкторе рабочих процессов, чтобы развернуть его.  
  
3. Перетащите действие **Assign (назначение** ) из раздела примитивы на **панели элементов** и поместите его в раздел **Entry (запись** ) состояния. Введите `Target` в поле **to** и следующее выражение в поле **введите C# выражение** или **введите выражение VB** .  
  
    ```vb  
    New System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    ```csharp  
    new System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    > [!TIP]
    > Если окно **панель элементов** не отображается, в меню **вид** выберите пункт **область элементов** .  
  
4. Вернитесь к общему представлению конечного автомата в конструкторе рабочих процессов, щелкнув **StateMachine** в окне Навигатор в верхней части конструктора рабочих процессов.  
  
5. Перетащите действие **State** из раздела **конечный автомат** на **панели элементов** в конструктор рабочих процессов и наведите его на состояние **Инициализация целевого объекта** . Обратите внимание, что рядом с целевым состоянием **инициализации** будут отображаться четыре треугольника, когда новое состояние находится над ним. Удалите новое состояние на треугольнике, расположенном непосредственно под целевым состоянием **инициализации** . Это помещает новое состояние в рабочий процесс и создает переход от целевого состояния **инициализации** к новому состоянию.  
  
6. Щелкните **State1** , чтобы выбрать его, измените **DisplayName** на `Enter Guess`, а затем дважды щелкните состояние в конструкторе рабочих процессов, чтобы развернуть его.  
  
7. Перетащите действие **WriteLine** из раздела **примитивы** **области элементов** и поместите его в раздел **запись** состояния.  
  
8. Введите следующее выражение в поле свойства **текст** для **WriteLine**.  
  
    ```vb  
    "Please enter a number between 1 and " & MaxNumber  
    ```  
  
    ```csharp  
    "Please enter a number between 1 and " + MaxNumber  
    ```  
  
9. Перетащите действие **Assign (назначение** ) из раздела примитивы на **панели элементов** и поместите в раздел **Exit** состояния.  
  
10. Введите `Turns` в поле **Кому** и `Turns + 1` в поле **введите C# выражение** или **введите выражение VB** .  
  
11. Вернитесь к общему представлению конечного автомата в конструкторе рабочих процессов, щелкнув **StateMachine** в окне Навигатор в верхней части конструктора рабочих процессов.  
  
12. Перетащите действие **FinalState** из раздела **конечный автомат** на **панели элементов**, наведите его на пункт **Перейти** в состояние подбора и поместите его на треугольник, расположенный справа от состояния « **Ввод предположения** », чтобы переход был создается между **вводом предположения** и **FinalState**.  
  
13. По умолчанию используется имя перехода **T2**. Щелкните переход в конструкторе рабочих процессов, чтобы выбрать его, и задайте для свойства **DisplayName** значение **верное**. Затем щелкните и выберите **FinalState**и перетащите его вправо, чтобы место для полного перехода отображалось без переименования одного из двух состояний. Это позволит упростить выполнение оставшихся действий в учебнике.  
  
14. Дважды щелкните вновь переименованный **правильный** переход в конструкторе рабочих процессов, чтобы развернуть его.  
  
15. Перетащите действие **ReadInt** из раздела **NumberGuessWorkflowActivities** на **панели элементов** и поместите его в раздел **Trigger** перехода.  
  
16. В **окне Свойства** для действия **ReadInt** введите `"EnterGuess"` , включая кавычки, в поле значение свойства **BookmarkName** и введите `Guess` в поле значение свойства **результата** .  
  
17. Введите следующее выражение в поле значение свойства **условия** **правильного** перехода.  
  
    ```vb  
    Guess = Target  
    ```  
  
    ```csharp  
    Guess == Target  
    ```  
  
18. Вернитесь к общему представлению конечного автомата в конструкторе рабочих процессов, щелкнув **StateMachine** в окне Навигатор в верхней части конструктора рабочих процессов.  
  
    > [!NOTE]
    > Переход происходит при получении события триггера и оценке <xref:System.Activities.Statements.Transition.Condition%2A> значением `True` (если оно присутствует). Для этого перехода, если пользователь `Guess` соответствует созданному `Target`случайным образом, управление передается в **FinalState** и завершает рабочий процесс.  
  
19. В зависимости от того, верно ли предположение, Рабочий процесс должен перейти в **FinalState** или вернуться в состояние **подбора** для другой попытки. Оба перехода используют один и тот же триггер ожидания получения предположения пользователя через действие **ReadInt** . Это называется общим переходом. Чтобы создать общий переход, щелкните окружность, указывающий начало правильного перехода с **предположения** , и перетащите его в нужное состояние. В этом случае переход является самопереходом, поэтому перетащите начальную точку **правильного** перехода и поместите его обратно в нижнюю часть состояния « **Ввод предположения** ». После создания перехода выберите его в конструкторе рабочих процессов и присвойте его свойству **DisplayName** неверное значение **угадать**.  
  
    > [!NOTE]
    > Общие переходы также можно создать в конструкторе переходов, щелкнув **Добавить общий переход триггера** в нижней части конструктора переходов, а затем выбрав нужное целевое состояние из **доступных состояний для подключения** . раскрывающийся список.  
  
    > [!NOTE]
    > Обратите внимание, что если состояние <xref:System.Activities.Statements.Transition.Condition%2A> перехода оценивается как `false` (или все условия общего перехода триггера оцениваются как `false`), переход не выполняется, а все триггеры для всех переходов из состояния будут запланированы заново. В этом учебнике такая ситуация невозможна из-за способа настройки условий (имеются определенные действия для случая, если догадка верна или неверна).  
  
20. Дважды щелкните некорректный переход в конструкторе рабочих процессов, чтобы развернуть его. Обратите внимание , что для триггера уже задано то же действие **ReadInt** , которое было использовано в правильном переходе с **предположения** .  
  
21. Введите следующее выражение в поле значение свойства **Condition** .  
  
    ```vb  
    Guess <> Target  
    ```  
  
    ```csharp  
    Guess != Target  
    ```  
  
22. Перетащите действие **If** из раздела **поток управления** на **панели элементов** и поместите его в раздел Action ( **действие** ) перехода.  
  
23. Введите следующее выражение в поле значение свойства **Condition** действия **If** .  
  
    ```
    Guess < Target  
    ```  
  
24. Перетащите два действия **WriteLine** из раздела **примитивы** на **панели элементов** и поместите их так, чтобы один из них находящегося в разделе **then** действия **If** , а другой — в разделе **else** .  
  
25. Щелкните действие **WriteLine** в разделе **then (затем** ), чтобы выбрать его, и введите следующее выражение в поле значение свойства **текста** .  
  
    ```
    "Your guess is too low."  
    ```  
  
26. Щелкните действие **WriteLine** в разделе **else** , чтобы выбрать его, и введите следующее выражение в поле значение свойства **текста** .  
  
    ```
    "Your guess is too high."  
    ```  
  
27. Вернитесь к общему представлению конечного автомата в конструкторе рабочих процессов, щелкнув **StateMachine** в окне Навигатор в верхней части конструктора рабочих процессов.  
  
     В следующем примере показан завершенный рабочий процесс.  
  
     ![Иллюстрация, показывающая Завершенный рабочий процесс конечного автомата.](./media/how-to-create-a-state-machine-workflow/complete-state-machine-workflow.jpg)  
  
### <a name="to-build-the-workflow"></a>Построение рабочего процесса  
  
1. Чтобы построить решение, нажмите CTRL+SHIFT+B.  
  
     Инструкции по запуску рабочего процесса см. в следующем разделе [: Запустите рабочий процесс](how-to-run-a-workflow.md). Если вы уже выполнили [действия в следующих случаях: Запустите этап рабочего](how-to-run-a-workflow.md) процесса с другим стилем рабочего процесса и захотите запустить его с помощью рабочего процесса конечного автомата из этого шага, перейдите к разделу [ [Создание и запуск приложения](how-to-run-a-workflow.md#BKMK_ToRunTheApplication) , посвященного следующим инструкциям. Запустите рабочий процесс](how-to-run-a-workflow.md).  
  
## <a name="see-also"></a>См. также

- <xref:System.Activities.Statements.Flowchart>
- <xref:System.Activities.Statements.FlowDecision>
- [Программирование в Windows Workflow Foundation](programming.md)
- [Разработка рабочих процессов](designing-workflows.md)
- [Руководство по началу работы](getting-started-tutorial.md)
- [Практическое руководство. Создание действия](how-to-create-an-activity.md)
- [Практическое руководство. Запуск рабочего процесса](how-to-run-a-workflow.md)
