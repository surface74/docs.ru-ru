---
title: Глобализация для WPF
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [WPF], international user interface
- XAML [WPF], globalization
- international user interface [WPF], XAML
- globalization [WPF]
ms.assetid: 4571ccfe-8a60-4f06-9b37-7ac0b1c2d10f
ms.openlocfilehash: 948d147a0990961a8706298f1112f85882e30119
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015619"
---
# <a name="globalization-for-wpf"></a>Глобализация для WPF
В этом разделе рассматриваются проблемы, которые следует учитывать при написании [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] приложений для глобального рынка. Элементы программирования глобализации определяются в [!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)] в `System.Globalization`.

<a name="xaml_globalization"></a>
## <a name="xaml-globalization"></a>Глобализация XAML
 [!INCLUDE[TLA#tla_xaml#initcap](../../../../includes/tlasharptla-xamlsharpinitcap-md.md)]основывается на [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] и использует преимущества поддержки глобализации, определенной [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] в спецификации. В следующих разделах описаны некоторые [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] функции, о которых следует знать.

<a name="char_reference"></a>
### <a name="character-references"></a>Ссылки символов
Ссылка на символ предоставляет единицу кода UTF16 определенного [!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)] символа, который он представляет, в десятичном или шестнадцатеричном формате. В следующем примере показана ссылка на десятичный символ для КОПТСКИЙ ПРОПИСной буквы по или Ϩ:

```
&#1000;
```

В следующем примере показана ссылка на шестнадцатеричный символ. Обратите внимание, что в начале шестнадцатеричного числа имеется **x** .

```
&#x3E8;
```

<a name="encoding"></a>
### <a name="encoding"></a>кодировка
 Кодировка, поддерживаемая [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] , — [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] это ASCII, UTF-16 и UTF-8. Оператор Encoding находится в начале [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] документа. Если атрибут кодировки и порядок байтов отсутствуют, по умолчанию в средстве синтаксического анализа используется кодировка UTF-8. Предпочтительные кодировки: UTF-8 и UTF-16. UTF-7 не поддерживается. В следующем примере показано, как задать кодировку UTF-8 в [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] файле.

```
?xml encoding="UTF-8"?
```

<a name="lang_attrib"></a>
### <a name="language-attribute"></a>Атрибут Language
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]использует [XML: lang](../../xaml-services/xml-lang-handling-in-xaml.md) для представления атрибута language элемента.  Чтобы воспользоваться преимуществами <xref:System.Globalization.CultureInfo> класса, значение атрибута language должно быть одним из имен языка и региональных параметров, <xref:System.Globalization.CultureInfo>предопределенных. [xml:lang](../../xaml-services/xml-lang-handling-in-xaml.md) наследуется в дереве элементов (правилами XML, не обязательно из-за наследования свойства зависимости), и его значение по умолчанию — пустая строка, если оно не назначено явно.

 Атрибут языка полезно использовать для задания диалектов. Например, французский язык имеет разные написание, словарь и произношение во Франции, Квебеке, Бельгии и Швейцарии. Кроме того, на китайском, японском и корейском языках кодовые точки в [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)], но идеографические фигуры различаются и используют совершенно разные шрифты.

 В следующем [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] примере `fr-CA` используется атрибут Language для указания канадского французского языка.

```xml
<TextBlock xml:lang="fr-CA">Découvrir la France</TextBlock>
```

<a name="unicode"></a>
### <a name="unicode"></a>Юникод
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]поддерживает все [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] функции, включая суррогаты. Если кодировка может быть сопоставлена с [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)], она поддерживается. Например, GB18030 представляет определенные символы, которые сопоставляются расширениям A и B и парам суррогатов китайского, японского и корейского. Следовательно, этот набор символов полностью поддерживается. Приложение может использовать <xref:System.Globalization.StringInfo> для работы со строками, не зная, есть ли у них суррогатные пары или самостоятельные символы. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]

<a name="design_intl_ui_with_xaml"></a>
## <a name="designing-an-international-user-interface-with-xaml"></a>Проектирование международного интерфейса пользователя с XAML
 В этом разделе [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] описываются функции, которые следует учитывать при написании приложения.

<a name="intl_text"></a>
### <a name="international-text"></a>Международный текст
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]включает встроенную обработку для всех платформ Microsoft .NET, поддерживаемых системой записи.

 В настоящее время поддерживаются следующие скрипты.

- Арабский

- бенгальский

- деванагари

- кириллица

- Греческий

- Гуджарати

- гурмухи

- Иврит

- Идеографические скрипты

- Каннада

- Лаосский

- Латиница

- Малаялам

- Монгольский

- Ория

- Сирийский

- Тамильский

- Телугу

- мальдивский

- Тайский *

- Тибетский

 \* В этом выпуске отображение и изменение текста на тайском языке поддерживается; а разбиение по словам — нет.

 В настоящее время не поддерживаются следующие скрипты.

- Кхмерский

- Старый хангыль (корейский)

- бирманский

- Сингальский

 Все обработчики системы записи поддерживают шрифты OpenType. Шрифты OpenType могут включать Макетные таблицы OpenType, позволяющие авторам шрифтов разрабатывать более удобные и типографские шрифты. Таблицы макетов шрифтов OpenType содержат сведения о подстановке глифов, позиционировании глифов, обоснованиях и расположении базовых показателей, что позволяет приложениям обработки текста улучшить макет текста.

 Шрифты OpenType позволяют обрабатывать крупные наборы глифов с помощью [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] кодирования. Такая кодировка обеспечивает широкую международную поддержку и возможность использования типографских вариантов глифов.

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]отрисовка текста реализована в виде вспомогательной точки Microsoft ClearType, которая поддерживает независимость от разрешения. Это значительно улучшает читаемость и предоставляет возможность поддержки качественных документов журнального стиля для всех скриптов.

<a name="intl_layout"></a>
### <a name="international-layout"></a>Международный макет
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] предоставляет очень удобный способ поддержки горизонтальных, двунаправленных и вертикальных макетов. В среде Presentation Framework <xref:System.Windows.FrameworkElement.FlowDirection%2A> свойство можно использовать для определения макета. Ниже перечислены шаблоны направления текста:

- *LeftToRight* — горизонтальная разметка для латиницы, восточноазиатских языков и т. д.

- *RightToLeft* — двунаправленная разметка для арабского, иврита и т. д.

<a name="developing_localizable_apps"></a>
## <a name="developing-localizable-applications"></a>Разработка локализуемых приложений
 При написании приложений для мирового рынка следует помнить, что приложения должны быть локализуемыми. В следующих разделах указано, на что обратить внимание.

<a name="mui"></a>
### <a name="multilingual-user-interface"></a>Многоязыковой интерфейс пользователя
 Многоязыковой интерфейс пользователя (MUI) — это поддержка Майкрософт [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] для переключения с одного языка на другой. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] Приложение использует модель сборки для поддержки многоязыкового интерфейса пользователя. Одно приложение содержит независимые от языка сборки, а также зависимые от языка сборки вспомогательных ресурсов. Точкой входа является управляемый EXE-файл в основной сборке.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]загрузчик ресурсов использует преимущества [!INCLUDE[TLA2#tla_netframewk](../../../../includes/tla2sharptla-netframewk-md.md)]диспетчера ресурсов для поддержки поиска и отката ресурсов. Многоязыковые вспомогательные сборки работают с одной и той же основной сборкой. Загружаемая сборка ресурса зависит от <xref:System.Globalization.CultureInfo.CurrentUICulture%2A> текущего потока.

<a name="localizable_ui"></a>
### <a name="localizable-user-interface"></a>Локализуемый пользовательский интерфейс
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]приложения используют [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] для определения их [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] позволяет разработчикам задавать иерархию объектов с набором свойств и определенной логикой. Основное использование [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] — разработка [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] приложений, но его можно использовать для указания иерархии любых объектов среды CLR. Большинство разработчиков используют [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] для указания своего [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] приложения и используют язык программирования, например, C# для реагирования на взаимодействие с пользователем.

 С точки зрения ресурсов, [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] файл, предназначенный для описания зависимого от [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] языка элемента, является элементом ресурса, поэтому его окончательный формат распространения должен быть локализован для поддержки международных языков. Поскольку [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] не может управлять событиями, многие [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] приложения содержат блоки кода для выполнения этой задачи. Дополнительные сведения см. в разделе [Общие сведения о XAML (WPF)](xaml-overview-wpf.md). Код вырезается и компилируется в разные двоичные файлы [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] , когда файл разбивается на форму BAML XAML. Форма BAML файлов XAML, изображения и другие типы управляемых объектов ресурсов внедряются во вспомогательную сборку ресурсов, которая может быть локализована на другие языки, или в основную сборку, если локализация не требуется.

> [!NOTE]
> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]приложения поддерживают все [!INCLUDE[TLA2#tla_netframewk](../../../../includes/tla2sharptla-netframewk-md.md)]ресурсы CLR, включая таблицы строк, изображения и т. д.

<a name="building_localizable_apps"></a>
### <a name="building-localizable-applications"></a>Разработка локализуемых приложений
 Локализация означает адаптации [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] к различным культурам. Чтобы сделать [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] приложение локализуемых, разработчики должны собрать все локализуемые ресурсы в сборку ресурсов. Сборка ресурсов локализуется на разные языки, и для загрузки кода программной части используется API управления ресурсами. Одним из файлов, необходимых для [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] приложения, является файл проекта (proj). Все ресурсы, используемые в приложении, необходимо включить в файл проекта. В следующем примере из CSPROJ-файла показано, как это сделать.

```xml
<Resource Include="data\picture1.jpg"/>
<EmbeddedResource Include="data\stringtable.en-US.restext"/>
```

 Чтобы использовать ресурс в приложении, <xref:System.Resources.ResourceManager> создайте экземпляр и загрузите ресурс, который вы хотите использовать. В следующем примере показано, как это сделать.

 [!code-csharp[LocalizationResources#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationResources/CSharp/page1.xaml.cs#2)]

<a name="using_clickonce"></a>
## <a name="using-clickonce-with-localized-applications"></a>Использование ClickOnce с локализованными приложениями
 ClickOnce — это новая технология развертывания Windows Forms, которая будет поставляться в Visual Studio 2005. Она позволяет устанавливать и обновлять веб-приложения. При локализации приложения, которое было развернуто с помощью ClickOnce, просмотреть его можно только на локализованном языке и с соответствующими региональными параметрами. Например, если развернутое приложение локализовано на японский язык, его можно просмотреть только на [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] японском языке, а не на английском Windows. Это представляет проблему, поскольку это распространенный сценарий для японского пользователя запускать английскую версию Windows.

 Чтобы решить эту проблему, можно задать резервный атрибут нейтрального языка. Разработчик приложения может при необходимости удалить ресурсы из основной сборки и указать, что ресурсы можно найти во вспомогательной сборке, соответствующей определенной культуре. Для управления этим процессом используйте <xref:System.Resources.NeutralResourcesLanguageAttribute>. Конструктор <xref:System.Resources.NeutralResourcesLanguageAttribute> класса имеет две сигнатуры, один из которых <xref:System.Resources.UltimateResourceFallbackLocation> принимает параметр, чтобы <xref:System.Resources.ResourceManager> указать расположение, куда должны извлекаться резервные ресурсы: основная или вспомогательная сборка. В следующем примере показано использование атрибута. Для окончательного резервного расположения код вызывает <xref:System.Resources.ResourceManager> Поиск ресурсов в подкаталоге "de" каталога выполняемой в данный момент сборки.

```
[assembly: NeutralResourcesLanguageAttribute(
    "de" , UltimateResourceFallbackLocation.Satellite)]
```

## <a name="see-also"></a>См. также

- [Общие сведения о глобализации и локализации WPF](wpf-globalization-and-localization-overview.md)
