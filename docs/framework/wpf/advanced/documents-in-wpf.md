---
title: Документы в WPF
ms.date: 03/30/2017
helpviewer_keywords:
- documents [WPF], packaging
- documents [WPF], text layout
- documents [WPF], XPS
- 'XPS documents [WPF], , '
- documents [WPF], controls
- documents [WPF], types of
- documents [WPF], browser-viewable
ms.assetid: 6e8db7bc-050a-4070-aa72-bb8c46e87ff8
ms.openlocfilehash: 9fac4e1a98f67c6d5d946ade1b7f2115ce0d5f8e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964880"
---
# <a name="documents-in-wpf"></a>Документы в WPF
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]предлагает широкий спектр возможностей документов, позволяющих создавать высокоточные материалы, которые упрощают доступ и чтение, чем в предыдущих поколениях Windows. В дополнение к расширенным возможностям и повышенному качеству [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] предоставляет интегрированные службы для отображения, упаковки и обеспечения безопасности документов. В этом разделе содержатся вводные сведения о типах и упаковке документов [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  

<a name="types_of_documents"></a>   
## <a name="types-of-documents"></a>Типы документов  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] разделяет документы на две основные категории на основе их предполагаемого использования; эти категории документов называются "документы фиксированного формата" и "документы нефиксированного формата".  
  
 Документы фиксированного формата предназначены для сфер применения, требующих точного представления [!INCLUDE[TLA#tla_wys](../../../../includes/tlasharptla-wys-md.md)] независимо от используемого дисплея или принтера. Документы фиксированного формата используются в компьютерной верстке, текстовой обработке и макетах форм, где строгое соответствие дизайну исходной страницы имеет критическое значение. При использовании такого макета документ фиксированного формата сохраняет точное расположение элементов содержимого независимо от используемого устройства изображения или печати. Так, страница документа фиксированного формата, отображаемая на дисплее 96 точек на дюйм, будет совершенно одинаково отображаться на лазерном принтере 600 точек на дюйм и фотонаборной машине 4800 точек на дюйм. Макет страницы остается неизменным во всех случаях, хотя качество документа повышается с учетом возможностей устройства.  
  
 Для сравнения: документы нефиксированного формата предназначены для повышения удобства просмотра и чтения; их лучше всего использовать, когда в работе с документом важнее всего удобство чтения. Вместо того чтобы использовать какой-либо определенный макет, документы нефиксированного формата динамически корректируют и перемещают содержимое с учетом переменных времени выполнения, таких как размер окна, разрешение устройства и дополнительные пользовательские настройки. Веб-страница — это простой пример документа нефиксированного формата, содержимое на которой динамически форматируется, чтобы уместиться в окне. Документы нефиксированного формата оптимизируют просмотр и чтение для пользователя в зависимости от среды выполнения. Например, один и тот же документ нефиксированного формата будет динамически переформатирован, чтобы обеспечить оптимальную читаемость на дисплее высокого разрешения 19 дюймов или небольшом экране PDA размером 2 x 3 дюйма. Кроме того, документы нефиксированного формата имеют несколько встроенных возможностей, включая поиск, режимы просмотра, оптимизирующие читаемость, и возможность менять размер и внешний вид шрифта.  См. иллюстрации, примеры и подробное описание документов нефиксированного формата в разделе [Общие сведения о документах нефиксированного формата](flow-document-overview.md).  
  
<a name="document_viewer"></a>   
## <a name="document-controls-and-text-layout"></a>Элементы управления документами и макеты текста  
 .NET Framework предоставляет набор предварительно созданных элементов управления, упрощающих использование фиксированных документов, документов нефиксированного формата и общего текста в приложении.  Отображение фиксированного содержимого документа поддерживается с помощью <xref:System.Windows.Controls.DocumentViewer> элемента управления.  Отображение содержимого документа нефиксированного формата поддерживается тремя различными элементами управления <xref:System.Windows.Controls.FlowDocumentReader>: <xref:System.Windows.Controls.FlowDocumentPageViewer>, и <xref:System.Windows.Controls.FlowDocumentScrollViewer> , которые сопоставляются с различными пользовательскими сценариями (см. разделы ниже).  Другие элементы управления [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] предоставляют упрощенную разметку для стандартных способов использования текста (см. раздел [Текст в пользовательском интерфейсе](#text_in_the_user_interface) ниже).  
  
### <a name="fixed-document-control---documentviewer"></a>Элемент управления документом фиксированного формата DocumentViewer  
 Элемент управления предназначен для вывода <xref:System.Windows.Documents.FixedDocument> содержимого. <xref:System.Windows.Controls.DocumentViewer> <xref:System.Windows.Controls.DocumentViewer> Элемент управления предоставляет интуитивно понятный пользовательский интерфейс, обеспечивающий встроенную поддержку общих операций, в том числе вывод вывода на печать, копирование в буфер обмена, масштаб и текстовый поиск. Элемент управления предоставляет доступ к страницам содержимого через знакомый механизм прокрутки. Как и [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] все элементы <xref:System.Windows.Controls.DocumentViewer> управления, поддерживает полную или частичную переопределение стиля, что позволяет визуально интегрировать элемент управления в практически любое приложение или среду.  
  
 <xref:System.Windows.Controls.DocumentViewer>предназначен для вывода содержимого в режиме только для чтения; изменение или изменение содержимого недоступно и не поддерживается.  
  
<a name="flow_document"></a>   
### <a name="flow-document-controls"></a>Элементы управления документа нефиксированного формата  

> [!NOTE]
> Более подробные сведения о возможностях документов нефиксированного формата и способах их создания см. в разделе [Общие сведения о потоковых документах](flow-document-overview.md).  
  
 Отображение содержимого документа нефиксированного формата поддерживается тремя элементами управления <xref:System.Windows.Controls.FlowDocumentReader>: <xref:System.Windows.Controls.FlowDocumentPageViewer>, и <xref:System.Windows.Controls.FlowDocumentScrollViewer>.  
  
#### <a name="flowdocumentreader"></a>FlowDocumentReader  
 <xref:System.Windows.Controls.FlowDocumentReader>включает функции, позволяющие пользователю динамически выбирать между различными режимами просмотра, включая одностраничный (страничный) режим просмотра, два страничных режима (формат чтения книги) и непрерывный режим просмотра (без нижнего прокрутки).  Дополнительные сведения об этих режимах просмотра см. <xref:System.Windows.Controls.FlowDocumentReaderViewingMode>в разделе.  Если не требуется возможность динамически переключаться между разными режимами <xref:System.Windows.Controls.FlowDocumentPageViewer> просмотра и <xref:System.Windows.Controls.FlowDocumentScrollViewer> предоставить облегченные средства просмотра содержимого нефиксированного формата, исправленные в определенном режиме просмотра.  
  
#### <a name="flowdocumentpageviewer-and-flowdocumentscrollviewer"></a>FlowDocumentPageViewer и FlowDocumentScrollViewer  
 <xref:System.Windows.Controls.FlowDocumentPageViewer>показывает содержимое в режиме просмотра на странице, в то время как <xref:System.Windows.Controls.FlowDocumentScrollViewer> отображает содержимое в режиме непрерывной прокрутки.  И, <xref:System.Windows.Controls.FlowDocumentScrollViewer> и исправляются в определенный режим просмотра. <xref:System.Windows.Controls.FlowDocumentPageViewer> Сравните с <xref:System.Windows.Controls.FlowDocumentReader>, который включает функции, позволяющие пользователю динамически выбирать между различными режимами просмотра (в соответствии <xref:System.Windows.Controls.FlowDocumentReaderViewingMode> с перечислением), за счет более ресурсоемких ресурсов, чем <xref:System.Windows.Controls.FlowDocumentPageViewer> или <xref:System.Windows.Controls.FlowDocumentScrollViewer>.  
  
 По умолчанию вертикальная полоса прокрутки отображается всегда, а горизонтальная полоса прокрутки становится видимой при необходимости. Значение по [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] умолчанию для <xref:System.Windows.Controls.FlowDocumentScrollViewer> не включает <xref:System.Windows.Controls.FlowDocumentScrollViewer.IsToolBarVisible%2A> панель инструментов, однако свойство можно использовать для включения встроенной панели инструментов.  
  
<a name="text_in_the_user_interface"></a>   
### <a name="text-in-the-user-interface"></a>Текст в пользовательском интерфейсе  
 Текст можно добавлять не только в документы, но и использовать в интерфейсе приложений, например в формах. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] предоставляет множество элементов управления для отображения текста на экране. Каждый элемент управления предназначен для своего сценария и имеет собственный список функций и ограничений. Как правило <xref:System.Windows.Controls.TextBlock> , элемент следует использовать, если требуется ограниченная поддержка текста, например краткое предложение [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]в. <xref:System.Windows.Controls.Label>может использоваться, если требуется минимальная поддержка текста. Дополнительные сведения см. в разделе [Общие сведения о классе TextBlock](../controls/textblock-overview.md).  
  
<a name="packaging"></a>   
## <a name="document-packaging"></a>Упаковка документов  
 <xref:System.IO.Packaging> Интерфейсы API предоставляют эффективные средства для организации данных приложений, содержимого документов и связанных ресурсов в одном контейнере, который прост в доступе, переносимости и простоте распространения. ZIP-файл — это пример типа, <xref:System.IO.Packaging.Package> способного удерживать несколько объектов как единое целое. API упаковки предоставляют реализацию по умолчанию <xref:System.IO.Packaging.ZipPackage> , разработанную с использованием стандарта Open Packaging Conventions с архитектурой XML и ZIP-файла. Интерфейсы [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] API упаковки упрощают создание пакетов, а также хранение и доступ к объектам в них. Объект, хранящийся в <xref:System.IO.Packaging.Package> , называется <xref:System.IO.Packaging.PackagePart> ("часть"). Пакеты также могут включать подписанные цифровые сертификаты, с помощью которых можно идентифицировать создателя части и убедиться, что содержимое пакета не было изменено.  Пакеты также включают в <xref:System.IO.Packaging.PackageRelationship> себя функцию, которая позволяет добавлять дополнительные сведения в пакет или связывать их с конкретными частями без фактического изменения содержимого существующих частей.  Службы пакета также поддерживают [!INCLUDE[TLA#tla_rm](../../../../includes/tlasharptla-rm-md.md)].  
  
 Архитектура пакета [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] лежит в основе ряда ключевых технологий:  
  
- Документы [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)], соответствующие стандарту [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)].  
  
- Документы открытого XML-формата Microsoft Office "12" (.docx).  
  
- Пользовательские форматы хранения для собственного приложения.  
  
 Основываясь на интерфейсах API упаковки <xref:System.Windows.Xps.Packaging.XpsDocument> , специально разработан для хранения [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] документов с фиксированным содержимым. — Это автономный документ, который может быть открыт в средстве просмотра, отображен <xref:System.Windows.Controls.DocumentViewer> в элементе управления, направляется в очередь печати [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)]или выводится непосредственно на совместимый принтер. <xref:System.Windows.Xps.Packaging.XpsDocument>  
  
 В следующих разделах приводятся дополнительные сведения <xref:System.IO.Packaging.Package> о <xref:System.Windows.Xps.Packaging.XpsDocument> API-интерфейсах и, предоставляемых [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]в.  
  
<a name="packages"></a>   
### <a name="package-components"></a>Компоненты пакета  
 Интерфейсы API упаковки [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] позволяют упорядочить данные и документы приложения в единый портативный блок. ZIP-файл является одним из наиболее распространенных типов пакетов и типом пакета по умолчанию, предоставляемым [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  <xref:System.IO.Packaging.Package>сам по себе является абстрактным классом, который <xref:System.IO.Packaging.ZipPackage> реализуется с помощью стандартной архитектуры XML и ZIP-файла.  <xref:System.IO.Packaging.Package.Open%2A> Метод использует<xref:System.IO.Packaging.ZipPackage> для создания и использования ZIP-файлов по умолчанию. Пакет может содержать три основных типа элементов:  
  
|||  
|-|-|  
|<xref:System.IO.Packaging.PackagePart>|Содержимое приложения, данные, документы и файлы ресурсов.|  
|<xref:System.IO.Packaging.PackageDigitalSignature>|[Сертификат X.509] для идентификации, аутентификации и проверки.|  
|<xref:System.IO.Packaging.PackageRelationship>|Добавленные сведения о пакете или определенной части.|  
  
<a name="PackageParts"></a>   
#### <a name="packageparts"></a>PackageParts  
 ("Часть") — это абстрактный класс, который ссылается на объект, хранящийся <xref:System.IO.Packaging.Package>в. <xref:System.IO.Packaging.PackagePart> В ZIP-файле части пакета соответствуют отдельным файлам, хранящимся в ZIP-файле.  <xref:System.IO.Packaging.ZipPackagePart>предоставляет реализацию по умолчанию для сериализуемых объектов, <xref:System.IO.Packaging.ZipPackage>хранящихся в.  Как и в файловой системе, части, которые содержатся в пакете, хранятся в иерархическом каталоге или организованы по папкам.  С помощью API <xref:System.IO.Packaging.PackagePart> упаковкиприложениямогутзаписывать,хранитьисчитыватьнесколькообъектовспомощьюодногоконтейнера[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ZIP-файлов.  
  
<a name="PackageDigitalSignatures"></a>   
#### <a name="packagedigitalsignatures"></a>PackageDigitalSignatures  
 В <xref:System.IO.Packaging.PackageDigitalSignature> целях безопасности ("цифровую подпись") можно связать с частями внутри пакета. <xref:System.IO.Packaging.PackageDigitalSignature> Включает [509], который предоставляет две функции:  
  
1. Идентификация и проверка подлинности создателя части.  
  
2. Проверка, не была ли часть изменена.  
  
 Цифровая подпись не защищает часть от изменения, но проверка цифровой подписи завершится ошибкой, если часть изменяется каким-либо образом. В таком случае приложение может предпринять соответствующие действия, например не допустить открытия части или уведомить пользователя об изменении (и, следовательно, ненадежности) части.  
  
<a name="PackageRelationships"></a>   
#### <a name="packagerelationships"></a>PackageRelationships  
 A <xref:System.IO.Packaging.PackageRelationship> ("связь") предоставляет механизм для связывания дополнительных сведений с пакетом или частью внутри пакета. Отношение — это возможность на уровне пакета, позволяющая связывать дополнительную информацию с частью, не меняя фактического содержимого части. Вставлять новые данные непосредственно в содержимое части, как правило, нецелесообразно:  
  
- Фактический тип части и схема содержимого неизвестны.  
  
- Даже если эти параметры известны, схема содержимого может не обеспечивать средства для добавления новых данных.  
  
- Часть может быть защищена от изменений цифровой подписью или шифрованием.  
  
 Отношения пакета предоставляют видимые средства добавления дополнительной информации в отдельные части или весь пакет и создания соответствующих связей между этой информацией и объектами. Отношения пакетов используются для решения двух основных задач:  
  
1. Определение отношений зависимости между частями.  
  
2. Определение информационных отношений, добавляющих примечания или другие данные, связанные с частью.  
  
 <xref:System.IO.Packaging.PackageRelationship> Предоставляет быстрые, обнаруживаемые средства для определения зависимостей и добавления других сведений, связанных с частью пакета или пакета в целом.  
  
<a name="Dependency_Relationships"></a>   
##### <a name="dependency-relationships"></a>Отношения зависимости  
 Отношения зависимости используются для описания зависимостей между частями. Например, пакет может содержать HTML-часть, которая включает один или несколько тегов изображений \<img>. Теги изображений относятся к изображениям, которые хранятся как части внутри пакета или вне его (например, части, доступные через Интернет). <xref:System.IO.Packaging.PackageRelationship> Создание связанного с файлом HTML файла позволяет быстро и легко обнаружить зависимые ресурсы и получить к ним доступ. Браузер или приложение средства просмотра может осуществлять прямой доступ к отношениям частей и сразу приступать к сборке зависимых ресурсов, даже не зная схемы и не выполняя синтаксического анализа документа.  
  
<a name="Information_Relationships"></a>   
##### <a name="information-relationships"></a>Информационные отношения  
 Аналогично примечанию или заметке <xref:System.IO.Packaging.PackageRelationship> , можно также использовать для хранения других типов данных, которые должны быть связаны с частью, без фактического изменения содержимого части.  
  
<a name="XPS_Documents"></a>   
## <a name="xps-documents"></a>XPS-документы  
 Документ [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] — это пакет, который содержит один или несколько фиксированных документов и все ресурсы и сведения, необходимые для отображения.  [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] также является собственным форматом файлов в очереди на печать [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)].  Объект <xref:System.Windows.Xps.Packaging.XpsDocument> хранится в стандартном наборе данных ZIP и может включать в себя сочетание XML-и двоичных компонентов, таких как файлы изображений и шрифтов. [PackageRelationships](#PackageRelationships) используются для определения зависимостей между содержимым и ресурсами, необходимыми для полного отображения документа.  <xref:System.Windows.Xps.Packaging.XpsDocument> Проект предоставляет единое высококачественное решение для документов, которое поддерживает несколько целей:  
  
- Чтение, запись и хранение содержимого и ресурсов документов фиксированного формата в одном портативном документе с возможностью удобного распространения.  
  
- Отображение документов в приложении средства просмотра [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)].  
  
- Вывод документов в собственном формате вывода в очередь на печать [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)].  
  
- Перенаправление документов непосредственно на совместимый с [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] принтер.  
  
## <a name="see-also"></a>См. также

- <xref:System.Windows.Documents.FixedDocument>
- <xref:System.Windows.Documents.FlowDocument>
- <xref:System.Windows.Xps.Packaging.XpsDocument>
- <xref:System.IO.Packaging.ZipPackage>
- <xref:System.IO.Packaging.ZipPackagePart>
- <xref:System.IO.Packaging.PackageRelationship>
- <xref:System.Windows.Controls.DocumentViewer>
- [Text](optimizing-performance-text.md)
- [Общие сведения о документах нефиксированного формата](flow-document-overview.md)
- [Общие сведения о печати](printing-overview.md)
- [Сериализация и хранение документов](document-serialization-and-storage.md)
