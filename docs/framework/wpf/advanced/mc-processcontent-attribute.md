---
title: Атрибут mc:ProcessContent
ms.date: 03/30/2017
helpviewer_keywords:
- mc:ProcessContent attribute
- XAML [WPF], mc:ProcessContent attribute
ms.assetid: 2689b2c8-b4dc-4b71-b9bd-f95e619122d7
ms.openlocfilehash: bc406659bec3fd8d5da87b597356a3411c7a2605
ms.sourcegitcommit: 29a9b29d8b7d07b9c59d46628da754a8bff57fa4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/17/2019
ms.locfileid: "69567398"
---
# <a name="mcprocesscontent-attribute"></a>Атрибут mc:ProcessContent
Указывает, [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] какие элементы по-прежнему должны обрабатываться соответствующими родительскими элементами, даже если непосредственный родительский элемент может [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] игнорироваться процессором из-за указания [MC: Ignorable атрибута](mc-ignorable-attribute.md). Атрибут поддерживает совместимость разметки как для пользовательского сопоставления пространства имен, [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] так и для управления версиями. `mc:ProcessContent`  
  
## <a name="xaml-attribute-usage"></a>Использование атрибута XAML  
  
```  
<object  
  xmlns:ignorablePrefix="ignorableUri"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix"...  
  mc:ProcessContent="ignorablePrefix:ThisElementCanBeIgnored"  
>  
    <ignorablePrefix:ThisElementCanBeIgnored>  
        [content]  
    </ignorablePrefix:ThisElementCanBeIgnored>  
</object>  
```  
  
## <a name="xaml-values"></a>Значения XAML  
  
|||  
|-|-|  
|*игнораблепрефикс*|Любая допустимая строка префикса, согласно спецификации XML 1,0.|  
|*игнораблеури*|Любой допустимый URI для обозначения пространства имен в соответствии с спецификацией XML 1,0.|  
|*сиселементканбеигноред*|Элемент, который может игнорироваться [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] реализациями процессора, если базовый тип не может быть разрешен.|  
|*содержани*|*Сиселементканбеигноред* помечен как Ignorable. Если процессор не обрабатывает этот элемент, *[content]* обрабатывается *объектом*.|  
  
## <a name="remarks"></a>Примечания  
 По умолчанию [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] процессор будет игнорировать содержимое внутри игнорируемого элемента. Можно указать конкретный элемент с помощью `mc:ProcessContent`, [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] а процессор продолжит обрабатывать содержимое внутри элемента, пропускаемого пропуском. Обычно это используется, если содержимое вложено в несколько тегов, по крайней мере один из которых является игнорируемым и по крайней мере один из которых не может быть проигнорирован.  
  
 В атрибуте можно указать несколько префиксов, используя разделитель пробелов, например: `mc:ProcessContent="ignore:Element1 ignore:Element2"`.  
  
 [!INCLUDE[TLA#tla_mcxmlnsv1](../../../../includes/tlasharptla-mcxmlnsv1-md.md)] Пространство имен определяет другие элементы и атрибуты, не описанные в этой области пакета SDK. Дополнительные сведения см. в разделе [Спецификация совместимости XML-разметки](https://go.microsoft.com/fwlink/?LinkId=73824).  
  
## <a name="see-also"></a>См. также

- [Атрибут mc: Ignorable](mc-ignorable-attribute.md)
- [Общие сведения о языке XAML (WPF)](xaml-overview-wpf.md)
