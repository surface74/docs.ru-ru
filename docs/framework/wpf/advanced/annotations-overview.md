---
title: Общие сведения о заметках
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- highlights [WPF]
- documents [WPF], annotations
- sticky notes [WPF]
ms.assetid: 716bf474-29bd-4c74-84a4-8e0744bdad62
ms.openlocfilehash: 861a757effee8d68d1e41682dd91ffadba20c536
ms.sourcegitcommit: 30a83efb57c468da74e9e218de26cf88d3254597
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/20/2019
ms.locfileid: "68364372"
---
# <a name="annotations-overview"></a>Общие сведения о заметках
Добавление заметок или примечаний на печатные документы — это настолько обыденное действие, что мы воспринимаем его как должное. Такие примечания или комментарии являются "заметками", которые мы добавляем в документ для пометки информации или выделения интересующих элементов, к которым будем обращаться в дальнейшем. Хотя написание заметок на печатных документах является простым и обыденным, возможность добавлять личные примечания в электронные документы, как правило, очень ограниченна, если вообще доступна.  
  
 В этом разделе рассматриваются некоторые распространенные типы заметок, специально записки и особенности, а также показано, как платформа Microsoft Annotations упрощает эти типы заметок в приложениях с помощью Windows Presentation Foundation (WPF ) элементы управления для просмотра документов.  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]элементы управления для просмотра документов, поддерживающие <xref:System.Windows.Controls.FlowDocumentScrollViewer>заметки, включают <xref:System.Windows.Controls.FlowDocumentReader> и, а также <xref:System.Windows.Controls.Primitives.DocumentViewerBase> элементы управления, <xref:System.Windows.Controls.FlowDocumentPageViewer>производные от таких, как <xref:System.Windows.Controls.DocumentViewer> и.  

<a name="caf1_type_stickynotes"></a>   
## <a name="sticky-notes"></a>Записки  
 Обычная записка содержит информацию, написанную на маленьком листке цветной бумаги, который затем "приклеивается" к документу. Цифровые записки предоставляют аналогичные функциональные возможности для электронных документов, однако обеспечивают дополнительную гибкость благодаря включению многих других типов содержимого, например печатного текста, рукописных заметок (например, рукописного ввода [!INCLUDE[TLA#tla_tpc](../../../../includes/tlasharptla-tpc-md.md)]) или веб-ссылок.  
  
 Ниже показаны некоторые примеры заметок: выделение, текстовая записка и рукописная записка.  
  
 ![Выделение, текстовая и рукописная записка](./media/caf-stickynote.jpg "CAF_StickyNote")  
  
 В следующем примере показан метод, который можно использовать для включения поддержки заметок в приложении.  
  
 [!code-csharp[DocViewerAnnotationsXml#DocViewXmlStartAnnotations](~/samples/snippets/csharp/VS_Snippets_Wpf/DocViewerAnnotationsXml/CSharp/Window1.xaml.cs#docviewxmlstartannotations)]
 [!code-vb[DocViewerAnnotationsXml#DocViewXmlStartAnnotations](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DocViewerAnnotationsXml/visualbasic/window1.xaml.vb#docviewxmlstartannotations)]  
  
<a name="caf1_type_callouts"></a>   
## <a name="highlights"></a>Выделение  
 Люди используют различные способы для привлечения внимания к интересующим элементам в бумажном документе, такие как подчеркивание, выделение, заключение слов в предложении в кружок или рисование пометок и примечаний на полях.  Выделение заметок в Microsoft Annotations Framework предоставляет аналогичную функцию для пометки информации [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] , отображаемой в элементах управления просмотром документов.  
  
 На следующем рисунке показан пример заметки-выделения.  
  
 ![Заметка-выделение](./media/caf-callouts.png "CAF_Callouts")  
  
 Пользователи обычно создают аннотации, сначала выбирая какой- <xref:System.Windows.Controls.ContextMenu> либо текст или интересующий элемент, а затем щелкая правой кнопкой мыши для вывода параметров аннотации.  В следующем примере показано [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] , как <xref:System.Windows.Controls.ContextMenu> объявить с помощью перенаправленных команд, к которым пользователи могут получать доступ для создания заметок и управления ими.  
  
 [!code-xaml[DocViewerAnnotationsXps#CreateDeleteAnnotations](~/samples/snippets/csharp/VS_Snippets_Wpf/DocViewerAnnotationsXps/CSharp/Window1.xaml#createdeleteannotations)]  
  
<a name="caf1_framework_data_anchoring"></a>   
## <a name="data-anchoring"></a>Привязка данных  
 Платформа примечаний привязывает заметки к данным, выбираемым пользователем, а не только к положению в представлении отображения. Таким образом, при изменении представления документа, например когда пользователь прокручивает его или изменяет размер окна отображения, заметка остается привязанной к выбранным данным. Например, на следующем графике показана заметка, которую пользователь задал для выделенного текста. При изменении представления документа (прокрутка, изменение размера, масштаба и т. д.) заметка-выделение перемещается вместе с исходным фрагментом данных.  
  
 ![Привязка данных заметки](./media/caf-dataanchoring.png "CAF_DataAnchoring")  
  
<a name="matching_annotations_with_annotated_objects"></a>   
## <a name="matching-annotations-with-annotated-objects"></a>Сопоставление заметок с объектами заметок  
 Можно сопоставить заметки с соответствующими объектами заметок. Например, рассмотрим простое приложение для чтения документа, имеющее панель комментариев. Панель комментариев может быть полем со списком, в котором отображается текст из списка заметок, привязанных к документу. Когда пользователь выбирает элемент в списке, приложение загружает в представление абзац в документе, к которому привязан соответствующий объект заметки.  
  
 Ниже приведен пример, демонстрирующий реализацию обработчика событий такого списка, который служит в качестве панели комментариев.  
  
 [!code-csharp[FlowDocumentAnnotatedViewer#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentAnnotatedViewer/CSharp/Window1.xaml.cs#handler)]
 [!code-vb[FlowDocumentAnnotatedViewer#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentAnnotatedViewer/visualbasic/window1.xaml.vb#handler)]  
  
 Другой пример сценария включает в себя приложения, обеспечивающие обмен заметками и записками между читателями документов по электронной почте. Эта функция позволяет таким приложениям направлять пользователя на страницу, содержащую заметку для обмена.  
  
## <a name="see-also"></a>См. также

- <xref:System.Windows.Controls.Primitives.DocumentViewerBase>
- <xref:System.Windows.Controls.DocumentViewer>
- <xref:System.Windows.Controls.FlowDocumentPageViewer>
- <xref:System.Windows.Controls.FlowDocumentScrollViewer>
- <xref:System.Windows.Controls.FlowDocumentReader>
- <xref:System.Windows.Annotations.IAnchorInfo>
- [Схема примечаний](annotations-schema.md)
- [Общие сведения об элементе ContextMenu](../controls/contextmenu-overview.md)
- [Общие сведения о системе команд](commanding-overview.md)
- [Общие сведения о документах нефиксированного формата](flow-document-overview.md)
- [Практическое руководство. Добавление команды в MenuItem](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms741839(v=vs.90))
