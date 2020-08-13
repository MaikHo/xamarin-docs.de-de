---
title: Xamarin.Forms AbsoluteLayout
description: Das Xamarin.Forms AbsoluteLayout wird zum Positionieren und Anpassen von Elementen mithilfe von expliziten Werten oder Werten verwendet, die proportional zur Größe des Layouts sind.
ms.prod: xamarin
ms.assetid: 01A5CCE0-AD45-4806-84FD-72C007005B38
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/07/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: a6efa4615f0061c83243f2d00d2d141a51607301
ms.sourcegitcommit: 808ff109928a1eea16e17e23ea81f8c903a239e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/13/2020
ms.locfileid: "88181497"
---
# <a name="no-locxamarinforms-absolutelayout"></a>Xamarin.Forms AbsoluteLayout

[![Beispiel herunterladen](~/media/shared/download.png) Herunterladen des Beispiels](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-absolutelayoutdemos)

[![::: NO-LOC (xamarin. Forms)::: AbsoluteLayout](absolutelayout-images/layouts.png)](absolutelayout-images/layouts-large.png#lightbox)

Eine [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) wird verwendet, um untergeordnete Elemente mit expliziten Werten zu positionieren und zu verkleinern. Die Position wird von der linken oberen Ecke des untergeordneten Elements relativ zur linken oberen Ecke des `AbsoluteLayout` in geräteunabhängigen Einheiten angegeben. `AbsoluteLayout` implementiert außerdem eine Funktion für proportionale Positionierung und Größenanpassung. Außerdem kann im Gegensatz zu einigen anderen layoutklassen untergeordnete Elemente `AbsoluteLayout` So positionieren, dass Sie sich überlappen.

Ein [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) sollte als ein spezielles Layout angesehen werden, das nur verwendet werden kann, wenn Sie eine Größe für untergeordnete Elemente festlegen können, oder wenn die Größe des Elements die Positionierung anderer untergeordneter Elemente nicht beeinträchtigt.

Die- [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) Klasse definiert die folgenden Eigenschaften:

- [`LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty)vom Typ [`Rectangle`](xref:Xamarin.Forms.Rectangle) , bei dem es sich um eine angefügte Eigenschaft handelt, die die Position und Größe eines untergeordneten Elements darstellt. Der Standardwert dieser Eigenschaft ist (0, 0, AutoSize, AutoSize).
- [`LayoutFlags`](xref:Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty)vom Typ [`AbsoluteLayoutFlags`](xref:Xamarin.Forms.AbsoluteLayoutFlags) . dabei handelt es sich um eine angefügte Eigenschaft, die angibt, ob Eigenschaften der layoutgrenzen, die für die Position und Größe der untergeordneten Elemente verwendet werden, proportional interpretiert werden Der Standardwert dieser Eigenschaft ist `AbsoluteLayoutFlags.None`.

Diese Eigenschaften werden von- [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) Objekten unterstützt. Dies bedeutet, dass die Eigenschaften Ziele von Daten Bindungen und formatierten sein können. Weitere Informationen zu angefügten Eigenschaften finden Sie unter [ Xamarin.Forms angefügte Eigenschaften](~/xamarin-forms/xaml/attached-properties.md).

Die- [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) Klasse wird von der- `Layout<T>` Klasse abgeleitet, die eine `Children` Eigenschaft vom Typ definiert `IList<T>` . Die `Children` -Eigenschaft ist der der `ContentProperty` `Layout<T>` -Klasse und muss daher nicht explizit aus XAML festgelegt werden.

> [!TIP]
> Um die bestmögliche layoutleistung zu erzielen, befolgen Sie die Richtlinien unter [Optimieren der layoutleistung](~/xamarin-forms/deploy-test/performance.md#optimize-layout-performance).

## <a name="position-and-size-children"></a>Untergeordnete Positions-und Größen Elemente

Die Position und Größe von untergeordneten Elementen in einer [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) wird durch Festlegen der [`AbsoluteLayout.LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty) angefügten-Eigenschaft der einzelnen untergeordneten Elemente definiert, wobei absolute Werte oder proportionale Werte verwendet werden. Absolute und proportionale Werte können für untergeordnete Elemente gemischt werden, wenn die Position skaliert werden soll, die Größe aber korrigiert bleiben muss oder umgekehrt. Informationen zu absoluten Werten finden Sie unter [absolute Positionierung und Größen](#absolute-positioning-and-sizing)Anpassung. Weitere Informationen überproportionale Werte finden Sie unter [proportionale Positionierung und Größen](#proportional-positioning-and-sizing)Anpassung.

Die [`AbsoluteLayout.LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty) angefügte-Eigenschaft kann mit zwei Formaten festgelegt werden, unabhängig davon, ob absolute oder proportionale Werte verwendet werden:

- `x, y`. Bei diesem Format geben die `x` `y` Werte und die Position der linken oberen Ecke des untergeordneten Elements relativ zum übergeordneten Element an. Das untergeordnete Element ist nicht eingeschränkt, und die Größe selbst ist.
- `x, y, width, height`. Bei diesem Format geben die `x` `y` Werte und die Position der linken oberen Ecke des untergeordneten Elements relativ zum übergeordneten Element an, während die `width` Werte und die `height` Größe des untergeordneten Elements angeben.

Legen Sie die- `width` und/oder- `height` Werte auf die-Eigenschaft fest, um anzugeben, dass eine untergeordnete Größe horizontal oder vertikal ist [`AbsoluteLayout.AutoSize`](xref:Xamarin.Forms.AbsoluteLayout.AutoSize) . Allerdings kann die übermäßige Verwendung dieser Eigenschaft die Anwendungsleistung beeinträchtigen, da dies bewirkt, dass die Layout-Engine weitere Layoutberechnungen durchführt.

> [!IMPORTANT]
> Die [`HorizontalOptions`](xref:Xamarin.Forms.View.HorizontalOptions) -Eigenschaft und die-Eigenschaft [`VerticalOptions`](xref:Xamarin.Forms.View.VerticalOptions) haben keine Auswirkung auf untergeordnete Elemente eines [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) .

## <a name="absolute-positioning-and-sizing"></a>Absolute Positionierung und Größenanpassung

Standardmäßig werden untergeordnete [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) Positionen und Größen untergeordnete Elemente mit absoluten Werten in geräteunabhängigen Einheiten angegeben, die explizit definieren, wo untergeordnete Elemente im Layout platziert werden sollen. Dies wird erreicht, indem der-Auflistung eines untergeordnete Elemente hinzugefügt `Children` `AbsoluteLayout` und die [`AbsoluteLayout.LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty) angefügte-Eigenschaft für jedes untergeordnete Element auf absolute Position und/oder Größen Werte festgelegt wird.

> [!WARNING]
> Die Verwendung absoluter Werte für die Positionierung und Größenanpassung von untergeordneten Elementen kann problematisch sein, da unterschiedliche Geräte unterschiedliche Bildschirmgrößen und Auflösungen aufweisen. Daher können die Koordinaten für den Mittelpunkt des Bildschirms auf einem Gerät auf anderen Geräten versetzt werden.

Der folgende XAML-Code zeigt ein-Element, [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) dessen untergeordnete Elemente mit absoluten Werten positioniert werden:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="AbsoluteLayoutDemos.Views.StylishHeaderDemoPage"
             Title="Stylish header demo">
    <AbsoluteLayout Margin="20">
        <BoxView Color="Silver"
                 AbsoluteLayout.LayoutBounds="0, 10, 200, 5" />
        <BoxView Color="Silver"
                 AbsoluteLayout.LayoutBounds="0, 20, 200, 5" />
        <BoxView Color="Silver"
                 AbsoluteLayout.LayoutBounds="10, 0, 5, 65" />
        <BoxView Color="Silver"
                 AbsoluteLayout.LayoutBounds="20, 0, 5, 65" />
        <Label Text="Stylish Header"
               FontSize="24"
               AbsoluteLayout.LayoutBounds="30, 25" />
    </AbsoluteLayout>
</ContentPage>
```

In diesem Beispiel wird die Position der einzelnen- [`BoxView`](xref:Xamarin.Forms.BoxView) Objekte mit den ersten beiden absoluten Werten definiert, die in der [`AbsoluteLayout.LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty) angefügten-Eigenschaft angegeben sind. Die Größe der einzelnen `BoxView` Werte wird mithilfe der dritten und der vierten Werte definiert. Die Position des- [`Label`](xref:Xamarin.Forms.Label) Objekts wird mit den beiden absoluten Werten definiert, die in der `AbsoluteLayout.LayoutBounds` angefügten-Eigenschaft angegeben sind. Größen Werte werden nicht für das angegeben `Label` , daher ist die Größe nicht eingeschränkt und die Größe selbst. In allen Fällen stellen die absoluten Werte geräteunabhängige Einheiten dar.

Der folgende Screenshot zeigt das Layout, das sich ergibt:

![Untergeordnete Elemente in einem AbsoluteLayout mit absoluten Werten](absolutelayout-images/absolute-values.png)

Der entsprechende c#-Code wird unten dargestellt:

```csharp
public class StylishHeaderDemoPageCS : ContentPage
{
    public StylishHeaderDemoPageCS()
    {
        AbsoluteLayout absoluteLayout = new AbsoluteLayout
        {
            Margin = new Thickness(20)
        };

        absoluteLayout.Children.Add(new BoxView
        {
            Color = Color.Silver,
        }, new Rectangle(0, 10, 200, 5));
        absoluteLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, new Rectangle(0, 20, 200, 5));
        absoluteLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, new Rectangle(10, 0, 5, 65));
        absoluteLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, new Rectangle(20, 0, 5, 65));

        absoluteLayout.Children.Add(new Label
        {
            Text = "Stylish Header",
            FontSize = 24
        }, new Point(30,25));                    

        Title = "Stylish header demo";
        Content = absoluteLayout;
    }
}
```

In diesem Beispiel werden die Position und die Größe der einzelnen [`BoxView`](xref:Xamarin.Forms.BoxView) mithilfe eines- [`Rectangle`](xref:Xamarin.Forms.Rectangle) Objekts definiert. Die Position von [`Label`](xref:Xamarin.Forms.Label) wird mithilfe eines- [`Point`](xref:Xamarin.Forms.Point) Objekts definiert.

In c# ist es auch möglich, die Position und Größe eines untergeordneten Elements von festzulegen [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) , nachdem es der-Auflistung mithilfe der-Methode hinzugefügt wurde `Children` [`AbsoluteLayout.SetLayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.SetLayoutBounds*) . Das erste Argument für diese Methode ist das untergeordnete Element, und das zweite ist ein- [`Rectangle`](xref:Xamarin.Forms.Rectangle) Objekt.

> [!NOTE]
> Ein [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) , das absolute Werte verwendet, kann untergeordnete Elemente positionieren und verkleinern, sodass Sie nicht in die Grenzen des Layouts passen.

## <a name="proportional-positioning-and-sizing"></a>Proportionale Positionierung und Größenanpassung

Ein kann untergeordnete Elemente [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) mithilfe von proportionalen Werten positionieren und verkleinern. Dies wird erreicht, indem der-Auflistung von untergeordnete Elemente hinzugefügt `Children` `AbsoluteLayout` werden, und indem die angefügte-Eigenschaft für jedes untergeordnete Element [`AbsoluteLayout.LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty) auf proportionale Positions-und/oder Größen Werte im Bereich 0-1 festgelegt wird. Positions-und Größen Werte werden proportional durch Festlegen der [`AbsoluteLayout.LayoutFlags`](xref:Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty) angefügten-Eigenschaft für jedes untergeordnete Element gemacht.

Mit der [`AbsoluteLayout.LayoutFlags`](xref:Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty) angefügten-Eigenschaft des Typs [`AbsoluteLayoutFlags`](xref:Xamarin.Forms.AbsoluteLayoutFlags) können Sie ein Flag festlegen, das angibt, dass die Positions-und Größen Werte der layoutwerte für ein untergeordnetes Element proportional zur Größe von sind `AbsoluteLayout` . Wenn Sie ein untergeordnetes Element anordnen, werden `AbsoluteLayout` die Positions-und Größen Werte entsprechend auf eine beliebige Gerätegröße skaliert.

Die- [`AbsoluteLayoutFlags`](xref:Xamarin.Forms.AbsoluteLayoutFlags) Enumeration definiert die folgenden Member:

- `None`Gibt an, dass die Werte als absolut interpretiert werden. Dies ist der Standardwert der [`AbsoluteLayout.LayoutFlags`](xref:Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty) angefügten-Eigenschaft.
- `XProportional`Gibt an, dass der `x` Wert als proportional interpretiert wird, während alle anderen Werte als absolut behandelt werden.
- `YProportional`Gibt an, dass der `y` Wert als proportional interpretiert wird, während alle anderen Werte als absolut behandelt werden.
- `WidthProportional`Gibt an, dass der `width` Wert als proportional interpretiert wird, während alle anderen Werte als absolut behandelt werden.
- `HeightProportional`Gibt an, dass der `height` Wert als proportional interpretiert wird, während alle anderen Werte als absolut behandelt werden.
- `PositionProportional`Gibt an, dass der `x` -Wert und der- `y` Wert als proportional interpretiert werden, während die Größen Werte als absolut interpretiert werden.
- `SizeProportional`Gibt an, dass der `width` -Wert und der- `height` Wert als proportional interpretiert werden, während die Positionswerte als absolut interpretiert werden.
- `All`Gibt an, dass alle Werte als proportional interpretiert werden.

> [!TIP]
> Die- [`AbsoluteLayoutFlags`](xref:Xamarin.Forms.AbsoluteLayoutFlags) Enumeration ist eine- `Flags` Enumeration, was bedeutet, dass Enumerationsmember kombiniert werden können. Dies wird in XAML mit einer durch Trennzeichen getrennten Liste und in c# mit dem bitweisen OR-Operator erreicht.

Wenn Sie z. b. das `SizeProportional` -Flag verwenden und die Breite eines untergeordneten Elements auf 0,25 und die Höhe auf 0,1 festlegen, ist das untergeordnete Element ein Viertel der Breite des [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) und ein Zehntel der Höhe. Das- `PositionProportional` Flag ist ähnlich. Eine Position von (0,0) legt das untergeordnete Element in der oberen linken Ecke ab, während eine Position von (1,1) das untergeordnete Element in der unteren rechten Ecke einfügt und eine Position von (0,5, 0,5) das untergeordnete Element in der zentriert `AbsoluteLayout` .

Der folgende XAML-Code zeigt einen, [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) dessen untergeordnete Elemente mithilfe von proportionalen Werten positioniert werden:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="AbsoluteLayoutDemos.Views.ProportionalDemoPage"
             Title="Proportional demo">
    <AbsoluteLayout>
        <BoxView Color="Blue"
                 AbsoluteLayout.LayoutBounds="0.5,0,100,25"
                 AbsoluteLayout.LayoutFlags="PositionProportional" />
        <BoxView Color="Green"
                 AbsoluteLayout.LayoutBounds="0,0.5,25,100"
                 AbsoluteLayout.LayoutFlags="PositionProportional" />
        <BoxView Color="Red"
                 AbsoluteLayout.LayoutBounds="1,0.5,25,100"
                 AbsoluteLayout.LayoutFlags="PositionProportional" />
        <BoxView Color="Black"
                 AbsoluteLayout.LayoutBounds="0.5,1,100,25"
                 AbsoluteLayout.LayoutFlags="PositionProportional" />
        <Label Text="Centered text"
               AbsoluteLayout.LayoutBounds="0.5,0.5,110,25"
               AbsoluteLayout.LayoutFlags="PositionProportional" />
    </AbsoluteLayout>
</ContentPage>
```

In diesem Beispiel wird jedes untergeordnete Element mithilfe von proportionalen Werten positioniert, aber mit absoluten Werten. Dies wird erreicht, indem die [`AbsoluteLayout.LayoutFlags`](xref:Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty) angefügte-Eigenschaft jedes untergeordneten Elements auf festgelegt wird `PositionProportional` . Die ersten beiden Werte, die in der [`AbsoluteLayout.LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty) angefügten-Eigenschaft angegeben sind, definieren für jedes untergeordnete Element die Position mithilfe von proportionalen Werten. Die Größe jedes untergeordneten Elements wird mit geräteunabhängigen Einheiten mit den dritten und den absoluten Werten definiert.

Der folgende Screenshot zeigt das Layout, das sich ergibt:

![Untergeordnete Elemente in einem AbsoluteLayout mithilfe von proportionalen Positions Werten](absolutelayout-images/proportional-position.png)

Der entsprechende c#-Code wird unten dargestellt:

```csharp
public class ProportionalDemoPageCS : ContentPage
{
    public ProportionalDemoPageCS()
    {
        BoxView blue = new BoxView { Color = Color.Blue };
        AbsoluteLayout.SetLayoutBounds(blue, new Rectangle(0.5, 0, 100, 25));
        AbsoluteLayout.SetLayoutFlags(blue, AbsoluteLayoutFlags.PositionProportional);

        BoxView green = new BoxView { Color = Color.Green };
        AbsoluteLayout.SetLayoutBounds(green, new Rectangle(0, 0.5, 25, 100));
        AbsoluteLayout.SetLayoutFlags(green, AbsoluteLayoutFlags.PositionProportional);

        BoxView red = new BoxView { Color = Color.Red };
        AbsoluteLayout.SetLayoutBounds(red, new Rectangle(1, 0.5, 25, 100));
        AbsoluteLayout.SetLayoutFlags(red, AbsoluteLayoutFlags.PositionProportional);

        BoxView black = new BoxView { Color = Color.Black };
        AbsoluteLayout.SetLayoutBounds(black, new Rectangle(0.5, 1, 100, 25));
        AbsoluteLayout.SetLayoutFlags(black, AbsoluteLayoutFlags.PositionProportional);

        Label label = new Label { Text = "Centered text" };
        AbsoluteLayout.SetLayoutBounds(label, new Rectangle(0.5, 0.5, 110, 25));
        AbsoluteLayout.SetLayoutFlags(label, AbsoluteLayoutFlags.PositionProportional);

        Title = "Proportional demo";
        Content = new AbsoluteLayout
        {
            Children = { blue, green, red, black, label }
        };
    }
}
```

In diesem Beispiel werden die Position und die Größe der einzelnen untergeordneten Elemente mit der-Methode festgelegt [`AbsoluteLayout.SetLayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.SetLayoutBounds*) . Das erste Argument für die-Methode ist das untergeordnete Element, und das zweite ist ein- [`Rectangle`](xref:Xamarin.Forms.Rectangle) Objekt. Die Position jedes untergeordneten Elements wird mit proportionalen Werten festgelegt, während die Größe jedes untergeordneten Elements mithilfe von geräteunabhängigen Einheiten mit absoluten Werten festgelegt wird.

> [!NOTE]
> Ein [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) , das proportionale Werte verwendet, kann untergeordnete Elemente positionieren und verkleinern, sodass Sie nicht innerhalb der Begrenzungen des Layouts passen, indem Sie Werte außerhalb des 0-1-Bereichs verwenden.

## <a name="related-links"></a>Verwandte Links

- [AbsoluteLayout-Demos (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-absolutelayoutdemos)
- [Xamarin.Forms Angefügte Eigenschaften](~/xamarin-forms/xaml/attached-properties.md)
- [Layout auswählen Xamarin.Forms](choose-layout.md)
- [Optimieren der Xamarin.Forms App-Leistung](~/xamarin-forms/deploy-test/performance.md)
