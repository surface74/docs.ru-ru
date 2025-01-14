---
title: Перенос библиотек в .NET Core
description: Узнайте, как перенести проекты библиотеки из .NET Framework в .NET Core.
author: cartermp
ms.date: 12/07/2018
ms.custom: seodec18
ms.openlocfilehash: c7a770ba2da8c245ba9140852fc7c2a33a55f7a2
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/21/2019
ms.locfileid: "69660700"
---
# <a name="port-net-framework-libraries-to-net-core"></a>Перенос библиотек .NET Framework в .NET Core

Узнайте, как перенести код библиотеки .NET Framework в .NET Core, чтобы выполнять его на разных платформах и расширить диапазон использующих его приложений.

## <a name="prerequisites"></a>Предварительные требования

В этой статье предполагается, что вы:

- используете Visual Studio 2017 или более поздней версии, так как
  - .NET Core не поддерживается в более ранних версиях Visual Studio;
- ознакомлены с [рекомендуемым процессом переноса](index.md);
- устранили все проблемы с [зависимостями сторонних разработчиков](third-party-deps.md).

Стоит также ознакомиться со следующими статьями:

[.NET Standard](../../standard/net-standard.md)\
В этой статье рассматривается официальная спецификация API-интерфейсов .NET, которые должны быть доступны во всех реализациях .NET.

[Пакеты, метапакеты и платформы](../packages.md)   
Из этой статьи вы узнаете, как .NET Core определяет и использует пакеты и как пакеты поддерживают выполнение кода во множестве реализаций .NET.

[Разработка библиотек с помощью кроссплатформенных средств](../tutorials/libraries.md)   
В этой статье объясняется создание библиотек для .NET с помощью кроссплатформенных средств интерфейса командной строки.

[Дополнения к формату *CSPROJ* для .NET Core](../tools/csproj.md)   
В этой статье перечислены изменения, внесенные в файлы проекта при перемещении в *CSPROJ* и MSBuild.

[Перенос кода в .NET Core — анализ зависимостей сторонних разработчиков](third-party-deps.md)   
В этом разделе рассматривается переносимость зависимостей сторонних разработчиков и объясняется, что делать, если зависимость пакета NuGet не работает в .NET Core.

## <a name="retargeting-your-net-framework-code-to-net-framework-472"></a>Изменение целевой платформы для кода .NET Framework на .NET Framework 4.7.2

Если ваш код не предназначен для .NET Framework 4.7.2, рекомендуем изменить его целевую платформу на эту версию. Это обеспечит доступность альтернативных API-интерфейсов последних версий в случаях, когда .NET Standard не поддерживает существующие API-интерфейсы.

Для каждого проекта в Visual Studio, который нужно перенести, выполните указанные ниже действия:

1. Щелкните проект правой кнопкой мыши и выберите пункт **Свойства**.
1. В раскрывающемся списке **Требуемая версия .NET Framework** выберите значение **.NET Framework 4.7.2**.
1. Перекомпилируйте проекты.

Так как ваши проекты теперь предназначены для .NET Framework 4.7.2, используйте эту версию .NET Framework в качестве основы для переноса кода.

## <a name="determining-the-portability-of-your-code"></a>Определение переносимости кода

Следующий шаг — запуск анализатора переносимости API (ApiPort) для создания отчета о переносимости и его анализа.

Для работы с .NET Core вам потребуются навыки использования [ApiPort](../../standard/analyzers/portability-analyzer.md) и создания отчетов о переносимости. Процедура зависит от ваших потребностей и личных предпочтений. Ниже описано несколько подходов. Вы можете использовать их в различных сочетаниях в зависимости от структуры кода.

### <a name="dealing-primarily-with-the-compiler"></a>Работа в первую очередь с компилятором

Такой подход может быть оптимальным для небольших проектов или проектов, в которых используется небольшое количество интерфейсов API .NET Framework. Этот подход прост:

1. При необходимости запустите средство ApiPort для проекта. Если вы запустили ApiPort, проверьте, нет ли проблем с отчетом, которые необходимо устранить.
1. Скопируйте весь код в новый проект .NET Core.
1. Обращаясь к отчету о переносимости (если он создан), устраните ошибки компилятора, пока проект не будет полностью компилироваться.

Хотя такой подход является бессистемным, ориентация на код помогает быстро устранить все проблемы и может оказаться оптимальной для небольших проектов или библиотек. Этот подход лучше применять к проектам, содержащим только модели данных.

### <a name="staying-on-the-net-framework-until-portability-issues-are-resolved"></a>Использование .NET Framework вплоть до устранения проблем переносимости

Такой подход может быть оптимальным, если вам нужен код, который компилируется на протяжении всего процесса. Он выглядит следующим образом.

1. Запустите средство ApiPort для проекта.
1. Устраните проблемы, используя другие API-интерфейсы, являющиеся переносимыми.
1. Запомните области, в которых невозможно использовать прямые альтернативы.
1. Повторяйте предыдущие шаги для всех переносимых проектов, пока не удостоверитесь в том, что каждый из них готов к копированию в новый проект .NET Core.
1. Скопируйте код в новый проект .NET Core.
1. Устраните все проблемы, для решения которых нет прямых альтернатив.

Такой тщательный подход более систематизирован, чем простое устранение ошибок компилятора. Но он по-прежнему в некоторой степени ориентирован на код. При этом код является компилируемым на всех этапах. Есть множество способов устранения некоторых проблем, которые не удалось решить, просто использовав другой API-интерфейс. Для некоторых проектов может оказаться необходимым разработать более детальный план. Эта задача рассматривается в следующем подходе.

### <a name="developing-a-comprehensive-plan-of-attack"></a>Разработка детального плана

Это, возможно, наилучший подход для более крупных и сложных проектов, при реализации которых для поддержки .NET Core может потребоваться реструктурировать код или полностью переписать некоторые его части. Он выглядит следующим образом.

1. Запустите средство ApiPort для проекта.
1. Определите, в каких случаях используется каждый непереносимый тип и как он влияет на переносимость в целом.
   - Изучите особенности этих типов. Их немного, но они часто используются? Или их много, но используются они нечасто? Ограничена ли область их использования или они распределены по всему коду?
   - Можно ли легко изолировать непереносимый код для более эффективной работы с ним?
   - Требуется ли рефакторинг кода?
   - Есть ли для непереносимых типов альтернативные интерфейсы API, выполняющие те же задачи? Например, если используется класс <xref:System.Net.WebClient>, вместо него можно использовать класс <xref:System.Net.Http.HttpClient>.
   - Есть ли другие переносимые API-интерфейсы, которые можно использовать для выполнения задачи, даже если это не совсем равноценная замена? Например, если вы используете класс <xref:System.Xml.Schema.XmlSchema> для анализа XML, но обнаружение схемы XML вам не требуется, вы можете использовать API-интерфейсы<xref:System.Xml.Linq> и выполнять анализ самостоятельно без API.
1. Если у вас есть сборки, которые трудно перенести, возможно, пока стоит оставить их в .NET Framework? Следует учесть ряд факторов:
   - В библиотеке могут быть функции, которые несовместимы с .NET Core, так как они слишком тесно связаны с возможностями .NET Framework или Windows. Возможно, стоит на время отказаться от этих функций и выпустить временную версию библиотеки для .NET Core с ограниченной функциональностью, пока не будет ресурсов для переноса этих функций?
   - Поможет ли рефакторинг?
1. Целесообразно ли написание собственной реализации недоступного интерфейса API .NET Framework?
   Вы можете рассмотреть возможность копирования, изменения и использования кода из [библиотеки эталонного исходного кода .NET Framework](https://github.com/Microsoft/referencesource). Эталонный исходный код распространяется по [лицензии MIT](https://github.com/Microsoft/referencesource/blob/master/LICENSE.txt), поэтому вы можете достаточно свободно использовать его в качестве источника при создании собственного кода. Только не забывайте соответствующим образом упоминать корпорацию Майкрософт в своем коде.
1. При необходимости повторите этот процесс для различных проектов.
 
Этап анализа может занять некоторое время в зависимости от размера базы кода. Потратив некоторое время на этот этап, чтобы тщательно проанализировать требуемый объем изменений и разработать план, вы сможете сэкономить время в долгосрочной перспективе, особенно если у вас сложная база кода.

В плане можно предусмотреть внесение существенных изменений в базу кода с сохранением ориентации на .NET Framework 4.7.2, что делает этот подход более структурированным по сравнению с предыдущим. Способ реализации плана зависит от базы кода.

### <a name="mixing-approaches"></a>Сочетание подходов

В каждом конкретном случае, скорее всего, потребуется использовать описанные выше подходы в разных сочетаниях. Выбирайте наиболее подходящие варианты для себя и вашей базы коды.

## <a name="porting-your-tests"></a>Перенос тестов

Чтобы гарантировать правильную работу кода после его переноса в .NET Core, лучше всего тестировать его в процессе переноса. Для этого потребуется использовать платформу тестирования, которая выполняет сборку и запуск тестов для .NET Core. В настоящее время имеются три варианта:

- [xUnit](https://xunit.github.io/)
  * [Начало работы](https://xunit.github.io/docs/getting-started-dotnet-core.html)
  * [Средство для преобразования проекта MSTest в xUnit](https://github.com/dotnet/codeformatter/tree/master/src/XUnitConverter)
- [NUnit](https://nunit.org/)
  * [Начало работы](https://github.com/nunit/docs/wiki/Installation)
  * [Запись блога о миграции из MSTest в NUnit](https://www.florian-rappl.de/News/Page/275/convert-mstest-to-nunit)
- [MSTest](https://docs.microsoft.com/visualstudio/test/unit-test-basics)

## <a name="recommended-approach-to-porting"></a>Рекомендуемый подход к переносу

Процедура переноса во многом зависит от того, как структурирован ваш код .NET Framework. Перенос кода лучше всего начинать с *основных* объектов библиотеки, которые являются базовыми компонентами кода. Это могут быть модели данных или какие-либо иные базовые классы и методы, используемые всеми остальными компонентами прямо или косвенно.

1. Перенесите тестовый проект для тестирования того уровня библиотеки, который вы переносите на данном этапе.
1. Скопируйте основные объекты библиотеки в новый проект .NET Core и выберите версию .NET Standard, которая должна поддерживаться.
1. Внесите изменения, необходимые для компиляции кода. Как правило, для этого требуется добавить зависимости пакетов NuGet в файл *CSPROJ*.
1. Проведите тесты и внесите необходимые исправления.
1. Выберите следующий уровень кода для переноса и повторите предыдущие шаги.

Двигаясь от базовых объектов библиотеки к более высоким уровням и тестируя каждый из них требуемым образом, вы обеспечиваете систематичность переноса и изоляцию проблем, относящихся к отдельным уровням кода.

>[!div class="step-by-step"]
>[Вперед](project-structure.md)
