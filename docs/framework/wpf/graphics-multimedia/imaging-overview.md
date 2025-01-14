---
title: Общие сведения об обработке изображений
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- metadata [WPF], images
- displaying images [WPF]
- Imaging API [WPF]
- image metadata [WPF]
- converting images [WPF]
- encoding image formats [WPF]
- format decoding for images [WPF]
- painting with images [WPF]
- stretching images [WPF]
- images [WPF], about imaging
- format encoding for images [WPF]
- cropping images [WPF]
- decoding image formats [WPF]
- rotating images [WPF]
ms.assetid: 72aad87a-e6f3-4937-94cd-a18b7766e990
ms.openlocfilehash: 13d5ea2735a799332edd8e552198de0f2b970dad
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69914104"
---
# <a name="imaging-overview"></a>Общие сведения об обработке изображений
В этом разделе содержатся общие сведения о платформе [!INCLUDE[TLA#tla_wic](../../../../includes/tlasharptla-wic-md.md)]. Платформа [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] позволяет разработчикам выполнять отображение, преобразование и форматирование изображений.  

## <a name="wpf-imaging-component"></a>Компонент обработки изображений WPF  
 Платформа [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] предоставляет значительные расширения возможностей в обработке изображений в [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)]. Возможности работы с образами, такие как отображение точечного рисунка или использование изображения в стандартном элементе управления, ранее были связаны с библиотеками Microsoft Windows интерфейс графических устройств (GDI) или Microsoft Windows GDI+. Эти API предоставляют базовые функции создания образов, но не имеют таких функций, как поддержка расширения кодека и поддержка изображений высокого качества. [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]предназначен для преодоления недостатков GDI и GDI+ и предоставления нового набора API для вывода и использования изображений в приложениях.  
  
 Существует два способа доступа [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] к API — управляемому компоненту и неуправляемому компоненту. Неуправляемый компонент предоставляет следующие возможности.  
  
- Модель расширяемости для новых или собственных форматов изображений.  
  
- Улучшенная производительность и безопасность в собственных форматах образов, включая точечные рисунки (BMP), группу экспертов по образам (JPEG), PNG [!INCLUDE[TLA#tla_tiff](../../../../includes/tlasharptla-tiff-md.md)] [!INCLUDE[TLA#tla_wdp](../../../../includes/tlasharptla-wdp-md.md)],,, формат GIF и значок (ICO).  
  
- Сохранение изображений с большой глубиной цвета — до 8 бит на канал (32 бита на пиксель).  
  
- Неразрушающее масштабирование, обрезка и повороты.  
  
- Упрощенное управление цветом.  
  
- Поддержка собственных метаданных в файле.  
  
- Управляемый компонент использует неуправляемую инфраструктуру для обеспечения плавной интеграции изображений с другими функциями [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], такими как [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)], анимация и графика. Управляемый компонент также имеет преимущества от модели расширения кодека Windows Presentation Foundation (WPF) для создания образов, которая обеспечивает автоматическое распознавание новых [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] форматов изображений в приложениях.  
  
 Большая часть [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] управляемого API находится <xref:System.Windows.Media.Imaging?displayProperty=nameWithType> в пространстве имен, хотя несколько <xref:System.Windows.Media.ImageBrush> важных типов, например и <xref:System.Windows.Media.ImageDrawing> , находятся в <xref:System.Windows.Media?displayProperty=nameWithType> пространстве имен и <xref:System.Windows.Controls.Image> <xref:System.Windows.Controls?displayProperty=nameWithType> находятся в имен.  
  
 В этом разделе содержатся дополнительные сведения об управляемом компоненте. Дополнительные сведения о неуправляемом API см. в документации по неуправляемым компонентам работы с образами [WPF](/windows/desktop/wic/-wic-lh) .  
  
<a name="_imageformats"></a>   
## <a name="wpf-image-formats"></a>Форматы изображений в WPF  
 Для кодирования и декодирования конкретного формата мультимедиа используются кодеки. [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]включает кодек для форматов изображений BMP, JPEG, PNG [!INCLUDE[TLA2#tla_tiff](../../../../includes/tla2sharptla-tiff-md.md)], [!INCLUDE[TLA2#tla_wdp](../../../../includes/tla2sharptla-wdp-md.md)], GIF и Icon. Каждый из этих кодеков позволяет приложениям декодировать и, за исключением формата ICON, кодировать изображения соответствующих форматов.  
  
 <xref:System.Windows.Media.Imaging.BitmapSource>является важным классом, используемым при декодировании и кодировании образов. Это основной строительный блок конвейера [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]. Он представляет отдельный постоянный набор точек определенного размера и разрешения. Может быть отдельным кадром изображения в нескольких кадрах или результатом преобразования, выполненного <xref:System.Windows.Media.Imaging.BitmapSource>в. <xref:System.Windows.Media.Imaging.BitmapSource> Он является родительским для многих основных классов, используемых в [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] создании образов, таких как. <xref:System.Windows.Media.Imaging.BitmapFrame>  
  
 <xref:System.Windows.Media.Imaging.BitmapFrame> Используется для хранения данных о фактическом растровом изображении формата изображения. Многие форматы изображений поддерживают только один <xref:System.Windows.Media.Imaging.BitmapFrame>формат, хотя такие форматы, как GIF, и [!INCLUDE[TLA2#tla_tiff](../../../../includes/tla2sharptla-tiff-md.md)] поддерживают несколько кадров на изображение. Кадры используются декодерами в качестве входных данных и передаются кодировщикам для создания файлов изображений.  
  
 В следующем примере показано, как <xref:System.Windows.Media.Imaging.BitmapFrame> создается объект <xref:System.Windows.Media.Imaging.BitmapSource> из, [!INCLUDE[TLA2#tla_tiff](../../../../includes/tla2sharptla-tiff-md.md)] а затем добавляется в изображение.  
  
 [!code-csharp[BitmapFrameExample#10](~/samples/snippets/csharp/VS_Snippets_Wpf/BitmapFrameExample/CSharp/BitmapFrame.cs#10)]
 [!code-vb[BitmapFrameExample#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitmapFrameExample/VB/BitmapFrame.vb#10)]  
  
### <a name="image-format-decoding"></a>Декодирование изображений разных форматов  
 Декодирование изображения — это преобразование изображения в некотором формате в данные изображения, которые могут быть использованы системой. Данные изображения затем могут использоваться для отображения, обработки или кодирования в другой формат. Выбор декодера зависит от формата изображения. Выбор кодека производится автоматически, если не указан определенный декодер. Примеры в разделе [Отображение изображений в WPF](#_displayingimages) демонстрируют автоматическое декодирование. Декодеры пользовательских форматов, разработанные с помощью неуправляемых интерфейсов [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] и зарегистрированные в системе, автоматически участвуют в выборе декодера. Благодаря этому пользовательские форматы могут автоматически отображаться в приложениях [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
 В следующем примере демонстрируется использование декодера точечных рисунков для декодирования изображения формата BMP.  
  
 [!code-cpp[BmpBitmapDecoderEncoder#5](~/samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#5)]
 [!code-csharp[BmpBitmapDecoderEncoder#5](~/samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#5)]
 [!code-vb[BmpBitmapDecoderEncoder#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#5)]  
  
### <a name="image-format-encoding"></a>Кодирование изображений разных форматов  
 Кодирование изображения — это преобразование данных изображения в определенный формат. Кодированные данные изображения могут затем быть использованы для создания новых файлов изображений. Платформа [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] предоставляет кодировщики для всех описанных выше форматов изображения.  
  
 В следующем примере показано использование кодировщика для сохранения вновь созданного точечного рисунка.  
  
 [!code-cpp[BmpBitmapDecoderEncoder#3](~/samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#3)]
 [!code-csharp[BmpBitmapDecoderEncoder#3](~/samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#3)]
 [!code-vb[BmpBitmapDecoderEncoder#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#3)]  
  
<a name="_displayingimages"></a>   
## <a name="displaying-images-in-wpf"></a>Отображение изображений в WPF  
 Существует несколько способов отобразить изображение в приложении Windows Presentation Foundation (WPF). Изображения могут отображаться с помощью <xref:System.Windows.Controls.Image> элемента управления, закрашены на визуальном элементе <xref:System.Windows.Media.ImageBrush>с помощью или нарисованы с помощью <xref:System.Windows.Media.ImageDrawing>.  
  
### <a name="using-the-image-control"></a>Использование элемента управления Image  
 <xref:System.Windows.Controls.Image>— Это элемент Framework и основной способ просмотра изображений в приложениях. В [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]можноиспользоватьдвумя способами:синтаксисатрибутаилисинтаксиссвойства.<xref:System.Windows.Controls.Image> В следующем примере показано, как можно отобразить изображение размером 200 пикселей в ширину, используя синтаксис атрибута и синтаксис тега свойства. Дополнительные сведения о синтаксисе атрибутов и синтаксисе свойств см. в разделе [Общие сведения о свойствах зависимостей](../advanced/dependency-properties-overview.md).  
  
 [!code-xaml[ImageElementExample_snip#ImageSimpleExampleInlineMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml#imagesimpleexampleinlinemarkup)]  
  
 Во многих примерах для ссылки <xref:System.Windows.Media.Imaging.BitmapImage> на файл изображения используется объект. <xref:System.Windows.Media.Imaging.BitmapImage>является специализированным <xref:System.Windows.Media.Imaging.BitmapSource> , оптимизированным для [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] загрузки, и является простым способом для вывода <xref:System.Windows.Controls.Image> изображений в <xref:System.Windows.Controls.Image.Source%2A> виде элемента управления.  
  
 В следующем примере показано, как построить изображение шириной 200 пикселей с использованием кода.  
  
> [!NOTE]
> <xref:System.Windows.Media.Imaging.BitmapImage><xref:System.ComponentModel.ISupportInitialize> реализует интерфейс для оптимизации инициализации нескольких свойств. Изменения свойств происходят только во время инициализации объекта. Вызовите метод <xref:System.Windows.Media.Imaging.BitmapImage.BeginInit%2A> , чтобы сообщить, что <xref:System.Windows.Media.Imaging.BitmapImage.EndInit%2A> инициализация началась, и сообщить о завершении инициализации. После инициализации изменения свойств игнорируются.  
  
 [!code-csharp[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml.cs#imagesimpleexampleinlinecode1)]
 [!code-vb[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/ImageSimpleExample.xaml.vb#imagesimpleexampleinlinecode1)]  
  
#### <a name="rotating-converting-and-cropping-images"></a>Вращение, преобразование и обрезка изображений  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]позволяет пользователям преобразовывать изображения с помощью <xref:System.Windows.Media.Imaging.BitmapImage> свойств или с помощью дополнительных <xref:System.Windows.Media.Imaging.BitmapSource> объектов, таких как <xref:System.Windows.Media.Imaging.CroppedBitmap> или <xref:System.Windows.Media.Imaging.FormatConvertedBitmap>. С помощью этих преобразований можно масштабировать или поворачивать изображения, изменять формат пикселей изображения и обрезать изображения.  
  
 Поворот изображения выполняется с помощью <xref:System.Windows.Media.Imaging.BitmapImage.Rotation%2A> <xref:System.Windows.Media.Imaging.BitmapImage>свойства. Вращение возможно только с шагом 90 градусов. В следующем примере изображение поворачивается на 90 градусов.  
  
 [!code-xaml[ImageElementExample#TransformedXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml#transformedxaml2)]  
  
 [!code-csharp[ImageElementExample#TransformedCSharp1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml.cs#transformedcsharp1)]
 [!code-vb[ImageElementExample#TransformedCSharp1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/TransformedImageExample.xaml.vb#transformedcsharp1)]  
  
 Преобразование изображения в другой формат пикселей, например в градации серого, <xref:System.Windows.Media.Imaging.FormatConvertedBitmap>выполняется с помощью. В следующих примерах изображение преобразуется в <xref:System.Windows.Media.PixelFormats.Gray4%2A>.  
  
 [!code-xaml[ImageElementExample_snip#ConvertedXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml#convertedxaml2)]  
  
 [!code-csharp[ImageElementExample_snip#ConvertedCSharp1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml.cs#convertedcsharp1)]
 [!code-vb[ImageElementExample_snip#ConvertedCSharp1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/FormatConvertedExample.xaml.vb#convertedcsharp1)]  
  
 Чтобы обрезать изображение, <xref:System.Windows.UIElement.Clip%2A> можно использовать <xref:System.Windows.Controls.Image> свойство или <xref:System.Windows.Media.Imaging.CroppedBitmap> . Как правило, если нужно просто отобразить часть изображения, <xref:System.Windows.UIElement.Clip%2A> следует использовать. Если необходимо закодировать и сохранить обрезанное изображение, <xref:System.Windows.Media.Imaging.CroppedBitmap> следует использовать. В следующем примере изображение обрезается с помощью свойства Clip с помощью <xref:System.Windows.Media.EllipseGeometry>.  
  
 [!code-xaml[ImageElementExample_snip#CroppedXAMLUsingClip1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml#croppedxamlusingclip1)]  
  
 [!code-csharp[ImageElementExample_snip#CroppedCSharpUsingClip1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml.cs#croppedcsharpusingclip1)]
 [!code-vb[ImageElementExample_snip#CroppedCSharpUsingClip1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/CroppedImageExample.xaml.vb#croppedcsharpusingclip1)]  
  
#### <a name="stretching-images"></a>Растягивание изображений  
 <xref:System.Windows.Controls.Image.Stretch%2A> Свойство определяет способ растяжения изображения для заполнения его контейнера. Свойство принимает следующие значения, определяемые <xref:System.Windows.Media.Stretch> перечислением: <xref:System.Windows.Controls.Image.Stretch%2A>  
  
- <xref:System.Windows.Media.Stretch.None>: Изображение не растягивается для заполнения области вывода. Если изображение больше, чем область вывода, изображение заполняет область вывода с обрезкой тех частей, которые не входят.  
  
- <xref:System.Windows.Media.Stretch.Fill>: Изображение масштабируется в соответствии с областью вывода. Так как высота и ширина изображения масштабируются независимо друг от друга, исходные пропорции изображения могут не сохраниться. То есть изображение может быть деформировано для полного заполнения контейнера вывода.  
  
- <xref:System.Windows.Media.Stretch.Uniform>: Изображение масштабируется таким образом, чтобы оно полностью поместилось в область вывода. Пропорции изображения сохраняются.  
  
- <xref:System.Windows.Media.Stretch.UniformToFill>: Изображение масштабируется таким образом, чтобы полностью заполнить область вывода с сохранением исходного пропорций изображения.  
  
 В следующем примере каждое из доступных <xref:System.Windows.Media.Stretch> перечислений применяется <xref:System.Windows.Controls.Image>к.  
  
 На следующем рисунке показаны выходные данные из примера и демонстрируется влияние различных <xref:System.Windows.Controls.Image.Stretch%2A> параметров на применение к изображению.  
  
 ![Различные параметры растяжения TileBrush](./media/img-mmgraphics-stretchenum.jpg "img_mmgraphics_stretchenum")  
Различные параметры растяжения  
  
 [!code-xaml[ImageElementExample_snip#ImageStretchExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageStretchExample.xaml#imagestretchexamplewholepage)]  
  
### <a name="painting-with-images"></a>Закрашивание с помощью изображений  
 Изображения также могут отображаться в приложении путем рисования с <xref:System.Windows.Media.Brush>помощью. Кисти позволяют заполнять объекты [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] различными изображениями, начиная с просто сплошного цвета и заканчивая сложными наборами шаблонов и изображений. Для рисования с помощью изображений используйте <xref:System.Windows.Media.ImageBrush>. <xref:System.Windows.Media.ImageBrush> — Это<xref:System.Windows.Media.TileBrush> тип, который определяет его содержимое в виде растрового изображения. Отображает одно изображение, которое задается его <xref:System.Windows.Media.ImageBrush.ImageSource%2A> свойством. <xref:System.Windows.Media.ImageBrush> Способом растяжения изображения, выравнивания и заполнения мозаикой можно управлять, что позволяет избегать искажений, создавать шаблоны и применять другие эффекты. На следующем рисунке показаны некоторые эффекты, которые можно достичь с помощью <xref:System.Windows.Media.ImageBrush>.  
  
 ![Примеры выходных данных ImageBrush](./media/wcpsdk-mmgraphics-imagebrushexamples.gif "wcpsdk_mmgraphics_imagebrushexamples")  
Используя кисти изображения, можно заполнять фигуры, элементы управления, текст и многое другое  
  
 В следующем примере показано, как закрасить фон кнопки с изображением с помощью <xref:System.Windows.Media.ImageBrush>.  
  
 [!code-xaml[UsingImageBrush#4](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush/CS/PaintingWithImages.xaml#4)]  
  
 Дополнительные сведения о <xref:System.Windows.Media.ImageBrush> и рисовании изображений см. [в статье Рисование с помощью изображений, рисунков и визуальных элементов](painting-with-images-drawings-and-visuals.md).  
  
<a name="_metadata"></a>   
## <a name="image-metadata"></a>Метаданные изображений  
 Некоторые файлы изображений содержат метаданные, описывающие содержимое или характеристики файла. Например, большинство цифровых фотоаппаратов создают изображения, содержащие метаданные об изготовителе и модели фотоаппарата, использованного для создания изображения. В разных форматах изображения метаданные обрабатываются по-разному. Платформа [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] предоставляет универсальный способ хранения и извлечения метаданных для всех поддерживаемых форматов изображения.  
  
 Доступ к метаданным предоставляется через <xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A> свойство <xref:System.Windows.Media.Imaging.BitmapSource> объекта. <xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A><xref:System.Windows.Media.Imaging.BitmapMetadata> возвращает объект, содержащий все метаданные, содержащиеся в изображении. Эти данные могут представлять собой одну схему метаданных или комбинацию различных схем. [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]поддерживает следующие схемы метаданных изображения: Файл обмена изображениями (EXIF), текст (текстовые данные PNG), каталог файлов изображений (IFD), Международный совет по Прессским коммуникациям (IPTC [!INCLUDE[TLA#tla_xmp](../../../../includes/tlasharptla-xmp-md.md)]) и.  
  
 Чтобы упростить процесс чтения метаданных <xref:System.Windows.Media.Imaging.BitmapMetadata> , предоставляет несколько именованных свойств, которые можно легко получить, <xref:System.Windows.Media.Imaging.BitmapMetadata.Author%2A>например, <xref:System.Windows.Media.Imaging.BitmapMetadata.Title%2A>, и <xref:System.Windows.Media.Imaging.BitmapMetadata.CameraModel%2A>. Многие из этих именованных свойств могут также использоваться для записи метаданных. Дополнительная поддержка чтения метаданных обеспечивается благодаря использованию считывателя запросов метаданных. Метод используется для получения считывателя запросов метаданных путем предоставления строкового запроса, например *"/APP1/EXIF/".* <xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A> В следующем примере <xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A> используется для получения текста, хранящегося в расположении *"/Text/Description"* .  
  
 [!code-cpp[BitmapMetadata#GetQuery](~/samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#getquery)]
 [!code-csharp[BitmapMetadata#GetQuery](~/samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#getquery)]
 [!code-vb[BitmapMetadata#GetQuery](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#getquery)]  
  
 Для написания метаданных используется мастер написания запросов метаданных. <xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A>Получает модуль записи запросов и задает нужное значение. В следующем примере <xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A> используется для записи текста, хранящегося в расположении *"/Text/Description"* .  
  
 [!code-cpp[BitmapMetadata#SetQuery](~/samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#setquery)]
 [!code-csharp[BitmapMetadata#SetQuery](~/samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#setquery)]
 [!code-vb[BitmapMetadata#SetQuery](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#setquery)]  
  
<a name="_extensibility"></a>   
## <a name="codec-extensibility"></a>Расширяемость кодеков  
 Основной особенностью [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] является модель расширяемости для новых кодеков изображений. Эти неуправляемые интерфейсы позволяют разработчикам кодеков интегрировать кодеки в [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]. Благодаря этому новые форматы изображений могут автоматически использоваться приложениями [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
 Пример API расширяемости см. в [примере кодека Win32](https://go.microsoft.com/fwlink/?LinkID=160052). В этом примере показано создание декодера и кодировщика для пользовательского формата изображения.  
  
> [!NOTE]
> Чтобы система могла распознать кодек, он должен иметь цифровую подпись.  
  
## <a name="see-also"></a>См. также

- <xref:System.Windows.Media.Imaging.BitmapSource>
- <xref:System.Windows.Media.Imaging.BitmapImage>
- <xref:System.Windows.Controls.Image>
- <xref:System.Windows.Media.Imaging.BitmapMetadata>
- [Двумерная графика и изображения](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [Пример кодека Win32](https://go.microsoft.com/fwlink/?LinkID=160052)
