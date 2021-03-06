---
title: 画笔概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], about brushes
ms.assetid: ecea1955-420b-45c6-bf43-c1404c072c41
ms.openlocfilehash: 18ca9b79a6ee801638a54fcb227c44e9aea21fd0
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2020
ms.locfileid: "76746204"
---
# <a name="wpf-brushes-overview"></a>WPF 画笔概述
屏幕上可见的所有内容都可见，因为它是由画笔绘制的。 例如，画笔用于描述按钮的背景、文本的前景和形状的填充效果。 本主题介绍与 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 画笔进行绘制的概念，并提供示例。 借助画笔，可以利用任意内容（从简单的纯色到复杂的图案和图像集）绘制 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 对象。  
  
<a name="paintingwithbrush"></a>   
## <a name="painting-with-a-brush"></a>使用画笔进行绘制  
 <xref:System.Windows.Media.Brush> "绘制" 带有其输出的区域。 不同的画笔具有不同类型的输出。 某些画笔使用纯色绘制区域，其他画笔使用渐变、图案、图像或绘图。 下图显示了每种不同 <xref:System.Windows.Media.Brush> 类型的示例。  
  
 ![画笔类型](./media/graphicsmm-brushtypes.jpg "graphicsmm_brushtypes")  
画笔示例  
  
 大多数视觉对象使您能够指定如何绘制它们。 下表列出了一些可以使用 <xref:System.Windows.Media.Brush>的常见对象和属性。  
  
|类|画笔属性|  
|-----------|----------------------|  
|<xref:System.Windows.Controls.Border>|<xref:System.Windows.Controls.Border.BorderBrush%2A>、<xref:System.Windows.Controls.Border.Background%2A>|  
|<xref:System.Windows.Controls.Control>|<xref:System.Windows.Controls.Control.Background%2A>、<xref:System.Windows.Controls.Control.Foreground%2A>|  
|<xref:System.Windows.Controls.Panel>|<xref:System.Windows.Controls.Panel.Background%2A>|  
|<xref:System.Windows.Media.Pen>|<xref:System.Windows.Media.Pen.Brush%2A>|  
|<xref:System.Windows.Shapes.Shape>|<xref:System.Windows.Shapes.Shape.Fill%2A>、<xref:System.Windows.Shapes.Shape.Stroke%2A>|  
|<xref:System.Windows.Controls.TextBlock>|<xref:System.Windows.Controls.TextBlock.Background%2A>|  
  
 以下各节介绍了不同的 <xref:System.Windows.Media.Brush> 类型，并提供了每种类型的示例。  
  
<a name="paintwithsolidcolorbrush"></a>   
## <a name="paint-with-a-solid-color"></a>使用纯色绘制  
 <xref:System.Windows.Media.SolidColorBrush> 使用纯色 <xref:System.Windows.Media.Color>绘制区域。 有多种方法可以指定 <xref:System.Windows.Media.SolidColorBrush>的 <xref:System.Windows.Media.SolidColorBrush.Color%2A>：例如，可以指定其 alpha、红色、蓝色和绿色通道，或使用 <xref:System.Windows.Media.Colors> 类提供的预定义颜色之一。  
  
 下面的示例使用 <xref:System.Windows.Media.SolidColorBrush> 绘制 <xref:System.Windows.Shapes.Rectangle>的 <xref:System.Windows.Shapes.Shape.Fill%2A>。 下图显示了绘制的矩形。  
  
 ![使用 System.windows.media.solidcolorbrush> 绘制的矩形](./media/graphicsmm-brush-ovw-solidcolorbrush.png "graphicsmm_brush_ovw_solidcolorbrush")  
使用 System.windows.media.solidcolorbrush> 绘制的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmsolidcolorbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmsolidcolorbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmsolidcolorbrushexampleinline)]  
  
 有关 <xref:System.Windows.Media.SolidColorBrush> 类的详细信息，请参阅[采用纯色和渐变进行绘制概述](painting-with-solid-colors-and-gradients-overview.md)。  
  
<a name="paintwithlineargradientbrush"></a>   
## <a name="paint-with-a-linear-gradient"></a>使用线性渐变绘制  
 <xref:System.Windows.Media.LinearGradientBrush> 使用线性渐变绘制区域。 线性渐变跨线条（渐变轴）混合两种或多种颜色。 使用 <xref:System.Windows.Media.GradientStop> 对象来指定渐变中的颜色及其位置。  
  
 下面的示例使用 <xref:System.Windows.Media.LinearGradientBrush> 绘制 <xref:System.Windows.Shapes.Rectangle>的 <xref:System.Windows.Shapes.Shape.Fill%2A>。 下图显示了绘制的矩形。  
  
 ![使用 LinearGradientBrush 绘制的矩形](./media/graphicsmm-brush-ovw-lineargradientbrush.jpg "graphicsmm_brush_ovw_lineargradientbrush")  
使用 LinearGradientBrush 绘制的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmlineargradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmlineargradientbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmlineargradientbrushexampleinline)]  
  
 有关 <xref:System.Windows.Media.LinearGradientBrush> 类的详细信息，请参阅[采用纯色和渐变进行绘制概述](painting-with-solid-colors-and-gradients-overview.md)。  
  
<a name="paintwithradialgradientbrush"></a>   
## <a name="paint-with-a-radial-gradient"></a>使用径向渐变绘制  
 使用径向渐变绘制区域 <xref:System.Windows.Media.RadialGradientBrush>。 径向渐变跨一个圆混合两种或多种颜色。 与 <xref:System.Windows.Media.LinearGradientBrush> 类一样，您可以使用 <xref:System.Windows.Media.GradientStop> 对象来指定渐变中的颜色及其位置。  
  
 下面的示例使用 <xref:System.Windows.Media.RadialGradientBrush> 绘制 <xref:System.Windows.Shapes.Rectangle>的 <xref:System.Windows.Shapes.Shape.Fill%2A>。 下图显示了绘制的矩形。  
  
 ![使用 RadialGradientBrush 绘制的矩形](./media/graphicsmm-brush-ovw-radialgradientbrush.jpg "graphicsmm_brush_ovw_radialgradientbrush")  
使用 RadialGradientBrush 绘制的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmradialgradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmradialgradientbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmradialgradientbrushexampleinline)]  
  
 有关 <xref:System.Windows.Media.RadialGradientBrush> 类的详细信息，请参阅[采用纯色和渐变进行绘制概述](painting-with-solid-colors-and-gradients-overview.md)。  
  
<a name="paintwithimage"></a>   
## <a name="paint-with-an-image"></a>使用图像进行绘制  
 <xref:System.Windows.Media.ImageBrush> 使用 <xref:System.Windows.Media.ImageSource>绘制区域。  
  
 下面的示例使用 <xref:System.Windows.Media.ImageBrush> 绘制 <xref:System.Windows.Shapes.Rectangle>的 <xref:System.Windows.Shapes.Shape.Fill%2A>。 下图显示了绘制的矩形。  
  
 ![System.windows.media.imagebrush> 绘制的矩形](./media/graphicsmm-brush-ovw-imagebrush.jpg "graphicsmm_brush_ovw_imagebrush")  
使用图像绘制的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmimagebrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmimagebrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmimagebrushexampleinline)]  
  
 有关 <xref:System.Windows.Media.ImageBrush> 类的详细信息，请参阅[利用图像、绘图和视觉对象进行绘制](painting-with-images-drawings-and-visuals.md)。  
  
<a name="paintwithdrawing"></a>   
## <a name="paint-with-a-drawing"></a>使用绘图绘制  
 <xref:System.Windows.Media.DrawingBrush> 使用 <xref:System.Windows.Media.Drawing>绘制区域。 <xref:System.Windows.Media.Drawing> 可以包含形状、图像、文本和媒体。  
  
 下面的示例使用 <xref:System.Windows.Media.DrawingBrush> 绘制 <xref:System.Windows.Shapes.Rectangle>的 <xref:System.Windows.Shapes.Shape.Fill%2A>。 下图显示了绘制的矩形。  
  
 ![使用 System.windows.media.drawingbrush> 绘制的矩形](./media/graphicsmm-brush-ovw-drawingbrush.jpg "graphicsmm_brush_ovw_drawingbrush")  
使用 System.windows.media.drawingbrush> 绘制的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmdrawingbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmdrawingbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmdrawingbrushexampleinline)]  
  
 有关 <xref:System.Windows.Media.DrawingBrush> 类的详细信息，请参阅[利用图像、绘图和视觉对象进行绘制](painting-with-images-drawings-and-visuals.md)。  
  
<a name="paintwithvisual"></a>   
## <a name="paint-with-a-visual"></a>使用视觉对象进行绘制  
 <xref:System.Windows.Media.VisualBrush> 使用 <xref:System.Windows.Media.Visual> 对象绘制区域。 视觉对象的示例包括 <xref:System.Windows.Controls.Button>、<xref:System.Windows.Controls.Page>和 <xref:System.Windows.Controls.MediaElement>。 使用 <xref:System.Windows.Media.VisualBrush> 还可以将应用程序的一个部分的内容投影到另一个区域;这对于创建反射效果和屏幕的放大部分非常有用。  
  
 下面的示例使用 <xref:System.Windows.Media.VisualBrush> 绘制 <xref:System.Windows.Shapes.Rectangle>的 <xref:System.Windows.Shapes.Shape.Fill%2A>。 下图显示了绘制的矩形。  
  
 ![使用 System.windows.media.visualbrush> 绘制的矩形](./media/graphicsmm-brush-ovw-visualbrush.jpg "graphicsmm_brush_ovw_visualbrush")  
使用 System.windows.media.visualbrush> 绘制的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmvisualbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmvisualbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmvisualbrushexampleinline)]  
  
 有关 <xref:System.Windows.Media.VisualBrush> 类的详细信息，请参阅[利用图像、绘图和视觉对象进行绘制](painting-with-images-drawings-and-visuals.md)。  
  
<a name="paintwithpredefinedbrushesandsystemcolors"></a>   
## <a name="paint-using-predefined-and-system-brushes"></a>使用预定义画笔和系统画笔进行绘制  
 为方便起见，Windows Presentation Foundation （WPF）提供了一组预定义的和系统画笔，可用于绘制对象。  
  
- 有关可用预定义画笔的列表，请参阅 <xref:System.Windows.Media.Brushes> 类。 有关演示如何使用预定义画笔的示例，请参阅[使用纯色绘制区域](how-to-paint-an-area-with-a-solid-color.md)。  
  
- 有关可用系统画笔的列表，请参阅 <xref:System.Windows.SystemColors> 类。 有关示例，请参阅[使用系统画笔绘制区域](how-to-paint-an-area-with-a-system-brush.md)。  
  
<a name="commonbrushfeatures"></a>   
## <a name="common-brush-features"></a>常用画笔功能  
 <xref:System.Windows.Media.Brush> 对象提供了一个 <xref:System.Windows.Media.Brush.Opacity%2A> 属性，该属性可用于使画笔透明或部分透明。 <xref:System.Windows.Media.Brush.Opacity%2A> 值0会使画笔完全透明，而 <xref:System.Windows.Media.Brush.Opacity%2A> 值1会使画笔完全不透明。 下面的示例使用 <xref:System.Windows.Media.Brush.Opacity%2A> 属性，使 <xref:System.Windows.Media.SolidColorBrush> 25% 不透明。  
  
 [!code-xaml[BrushOverviewExamples_snip#OpacityExample1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/OpacityExample.xaml#opacityexample1xaml)]  
  
 [!code-csharp[BrushOverviewExamples_snip#OpacityExample1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/OpacityExample.cs#opacityexample1csharp)]  
  
 如果画笔包含部分透明的颜色，则使用画笔的不透明度值组合颜色的不透明度值。 例如，如果画笔的不透明度值为0.5，并且画笔中使用的颜色的不透明度值为0.5，则输出颜色的不透明度值为0.25。  
  
> [!NOTE]
> 更改画笔的不透明度值比使用其 <xref:System.Windows.UIElement.Opacity%2A?displayProperty=nameWithType> 属性更改整个元素的不透明度更为有效。  
  
 您可以使用画笔的 <xref:System.Windows.Media.Brush.Transform%2A> 或 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 属性来旋转、缩放、倾斜和平移画笔的内容。 有关详细信息，请参阅[刷子转换概述](brush-transformation-overview.md)。  
  
 因为它们是 <xref:System.Windows.Media.Animation.Animatable> 对象，所以可以对 <xref:System.Windows.Media.Brush> 对象进行动画处理。 有关详细信息，请参阅 [动画概述](animation-overview.md)。  
  
<a name="freezable_features"></a>   
### <a name="freezable-features"></a>Freezable 功能  
 因为它继承自 <xref:System.Windows.Freezable> 类，所以 <xref:System.Windows.Media.Brush> 类提供若干特殊功能： <xref:System.Windows.Media.Brush> 对象可以声明为[资源](../../../desktop-wpf/fundamentals/xaml-resources-define.md)、在多个对象之间共享以及进行克隆。 此外，除 <xref:System.Windows.Media.VisualBrush> 之外的所有 <xref:System.Windows.Media.Brush> 类型都可以变为只读，以提高性能并使其成为线程安全的。  
  
 有关 <xref:System.Windows.Freezable> 对象提供的不同功能的详细信息，请参阅可[冻结对象概述](../advanced/freezable-objects-overview.md)。  
  
 有关无法冻结 <xref:System.Windows.Media.VisualBrush> 对象的原因的详细信息，请参阅 <xref:System.Windows.Media.VisualBrush> 类型 "页。  
  
## <a name="see-also"></a>另请参阅

- <xref:System.Windows.Media.Brush>
- <xref:System.Windows.Media.Brushes>
- [使用纯色和渐变进行绘制概述](painting-with-solid-colors-and-gradients-overview.md)
- [使用图像、绘图和视觉对象进行绘制](painting-with-images-drawings-and-visuals.md)
- [Freezable 对象概述](../advanced/freezable-objects-overview.md)
- [画笔示例](https://go.microsoft.com/fwlink/?LinkID=159973)
- [System.windows.media.imagebrush> 示例](https://go.microsoft.com/fwlink/?LinkID=160005)
- [VisualBrush 示例](https://go.microsoft.com/fwlink/?LinkID=160049)
- [帮助主题](brushes-how-to-topics.md)
- [其他性能建议](../advanced/optimizing-performance-other-recommendations.md)
