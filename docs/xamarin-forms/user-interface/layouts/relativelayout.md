---
title: Xamarin.Forms RelativeLayout
description: Xamarin.FormsRelativelayout wird in Relation zu den Eigenschaften des Layouts oder gleich geordneten Elements als untergeordnete Elemente der Position und Größe verwendet.
ms.prod: xamarin
ms.assetid: 2530BCB8-01B8-4C4F-BF14-CA53659F1B5A
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/13/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: b23da34239d99faa64578bd30c5a3e969cf4b289
ms.sourcegitcommit: 808ff109928a1eea16e17e23ea81f8c903a239e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/13/2020
ms.locfileid: "88181812"
---
# <a name="no-locxamarinforms-relativelayout"></a>Xamarin.Forms RelativeLayout

[![Beispiel herunterladen](~/media/shared/download.png) Herunterladen des Beispiels](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-relativelayoutdemos)

[![::: NO-LOC (xamarin. Forms)::: relativelayout](relativelayout-images/layouts.png)](relativelayout-images/layouts-large.png#lightbox)

Eine [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) wird verwendet, um untergeordnete Elemente relativ zu den Eigenschaften des Layouts oder der gleich geordneten Elemente zu positionieren und zu verkleinern. Dies ermöglicht das Erstellen von UIs, das proportional über Gerätegrößen skaliert werden kann. Außerdem kann im Gegensatz zu einigen anderen layoutklassen untergeordnete Elemente `RelativeLayout` So positionieren, dass Sie sich überlappen.

Die- [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) Klasse definiert die folgenden Eigenschaften:

- [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty)vom Typ [`Constraint`](xref:Xamarin.Forms.Constraint) , bei dem es sich um eine angefügte Eigenschaft handelt, die die Einschränkung an der X-Position des untergeordneten Elements darstellt.
- [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty)vom Typ [`Constraint`](xref:Xamarin.Forms.Constraint) , bei dem es sich um eine angefügte Eigenschaft handelt, die die Einschränkung an der Y-Position des untergeordneten Elements darstellt.
- [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty)vom Typ [`Constraint`](xref:Xamarin.Forms.Constraint) , bei dem es sich um eine angefügte Eigenschaft handelt, die die Einschränkung für die Breite des untergeordneten Elements darstellt.
- [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty)vom Typ [`Constraint`](xref:Xamarin.Forms.Constraint) , bei dem es sich um eine angefügte Eigenschaft handelt, die die Einschränkung für die Höhe des untergeordneten Elements darstellt.
- [`BoundsConstraint`](xref:Xamarin.Forms.RelativeLayout.BoundsConstraintProperty)vom Typ [`BoundsConstraint`](xref:Xamarin.Forms.BoundsConstraint) , bei dem es sich um eine angefügte Eigenschaft handelt, die die Einschränkung der Position und Größe des untergeordneten Elements darstellt. Diese Eigenschaft kann nicht problemlos von XAML verwendet werden.

Diese Eigenschaften werden von- [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) Objekten unterstützt. Dies bedeutet, dass die Eigenschaften Ziele von Daten Bindungen und formatierten sein können. Weitere Informationen zu angefügten Eigenschaften finden Sie unter [ Xamarin.Forms angefügte Eigenschaften](~/xamarin-forms/xaml/attached-properties.md).

> [!NOTE]
> Die Breite und Höhe eines untergeordneten Elements in einem [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) kann auch über die `WidthRequest` Eigenschaften und anstelle der `HeightRequest` [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty) [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty) angefügten Eigenschaften und angegeben werden.

Die- [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) Klasse wird von der- `Layout<T>` Klasse abgeleitet, die eine `Children` Eigenschaft vom Typ definiert `IList<T>` . Die `Children` -Eigenschaft ist der der `ContentProperty` `Layout<T>` -Klasse und muss daher nicht explizit aus XAML festgelegt werden.

> [!TIP]
> Vermeiden Sie möglichst die Verwendung eines [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout). Dies führt dazu, dass die CPU erheblich mehr Arbeit übernehmen muss.

## <a name="constraints"></a>Einschränkungen

Innerhalb [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) von werden die Position und Größe von untergeordneten Elementen als Einschränkungen mit absoluten Werten oder relativen Werten angegeben. Wenn keine Einschränkungen angegeben werden, wird ein untergeordnetes Element in der oberen linken Ecke des Layouts positioniert.

In der folgenden Tabelle wird gezeigt, wie Einschränkungen in XAML und c# angegeben werden:

|     | XAML | C# |
| --- | ---- | -- |
| **Absolute Werte** | Absolute Einschränkungen werden angegeben, indem die [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) angefügten Eigenschaften auf Werte festgelegt werden `double` . | Absolute Einschränkungen werden durch die- [`Constraint.Constant`](xref:Xamarin.Forms.Constraint.Constant*) Methode oder durch Verwendung der-Überladung angegeben, `Children.Add` die ein- `Func<Rectangle>` Argument erfordert. |
| **Relative Werte** | Relative Einschränkungen werden angegeben, indem die [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) angefügten Eigenschaften auf Objekte festgelegt werden [`Constraint`](xref:Xamarin.Forms.Constraint) , die von der Markup Erweiterung zurückgegeben werden `ConstraintExpression` . | Relative Einschränkungen werden von- [`Constraint`](xref:Xamarin.Forms.Constraint) Objekten angegeben, die von Methoden der-Klasse zurückgegeben werden `Constraint` . |

Weitere Informationen zum Angeben von Einschränkungen mit absoluten Werten finden Sie unter [absolute Positionierung und Größen](#absolute-positioning-and-sizing)Anpassung. Weitere Informationen zum Angeben von Einschränkungen mit relativen Werten finden Sie unter [relative Positionierung und Größen](#relative-positioning-and-sizing)Anpassung.

In c# können untergeordnete Elemente [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) durch drei über Ladungen hinzugefügt werden `Add` . Die erste Überladung erfordert `Expression<Func<Rectangle>>` , dass die Position und Größe eines untergeordneten Elements angibt. Die zweite Überladung erfordert optionale `Expression<Func<double>>` -Objekte für die `x` `y` Argumente,, `width` und `height` . Die dritte Überladung erfordert optionale `Constraint` -Objekte für die `x` `y` Argumente,, `width` und `height` .

Es ist möglich, die Position und Größe eines untergeordneten Elements in einem [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) mit den [`SetXConstraint`](xref:Xamarin.Forms.RelativeLayout.SetXConstraint*) [`SetYConstraint`](xref:Xamarin.Forms.RelativeLayout.SetYConstraint*) Methoden,, [`SetWidthConstraint`](xref:Xamarin.Forms.RelativeLayout.SetWidthConstraint*) und [`SetHeightConstraint`](xref:Xamarin.Forms.RelativeLayout.SetHeightConstraint*) zu ändern. Das erste Argument für jede dieser Methoden ist das untergeordnete Element, und das zweite ist ein- [`Constraint`](xref:Xamarin.Forms.Constraint) Objekt. Außerdem [`SetBoundsConstraint`](xref:Xamarin.Forms.RelativeLayout.SetBoundsConstraint*) kann die-Methode auch verwendet werden, um die Position und Größe eines untergeordneten Elements zu ändern. Das erste Argument für diese Methode ist das untergeordnete Element, und das zweite ist ein- [`BoundsConstraint`](xref:Xamarin.Forms.BoundsConstraint) Objekt.

## <a name="absolute-positioning-and-sizing"></a>Absolute Positionierung und Größenanpassung

Ein [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) kann untergeordnete Elemente mit absoluten Werten positionieren und verkleinern, die in geräteunabhängigen Einheiten angegeben sind, die explizit definieren, wo untergeordnete Elemente im Layout platziert werden sollen. Dies wird erreicht, indem der-Auflistung von ein untergeordnete Elemente hinzugefügt `Children` `RelativeLayout` und die [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty) Eigenschaften,, und für jedes untergeordnete Element [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty) [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty) [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty) auf absolute Position und/oder Größen Werte festgelegt werden.

> [!WARNING]
> Die Verwendung absoluter Werte für die Positionierung und Größenanpassung von untergeordneten Elementen kann problematisch sein, da unterschiedliche Geräte unterschiedliche Bildschirmgrößen und Auflösungen aufweisen. Daher können die Koordinaten für den Mittelpunkt des Bildschirms auf einem Gerät auf anderen Geräten versetzt werden.

Der folgende XAML-Code zeigt ein-Element, [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) dessen untergeordnete Elemente mit absoluten Werten positioniert werden:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="RelativeLayoutDemos.Views.StylishHeaderDemoPage"
             Title="Stylish header demo">
    <RelativeLayout Margin="20">
        <BoxView Color="Silver"
                 RelativeLayout.XConstraint="0"
                 RelativeLayout.YConstraint="10"
                 RelativeLayout.WidthConstraint="200"
                 RelativeLayout.HeightConstraint="5" />
        <BoxView Color="Silver"
                 RelativeLayout.XConstraint="0"
                 RelativeLayout.YConstraint="20"
                 RelativeLayout.WidthConstraint="200"
                 RelativeLayout.HeightConstraint="5" />
        <BoxView Color="Silver"
                 RelativeLayout.XConstraint="10"
                 RelativeLayout.YConstraint="0"
                 RelativeLayout.WidthConstraint="5"
                 RelativeLayout.HeightConstraint="65" />
        <BoxView Color="Silver"
                 RelativeLayout.XConstraint="20"
                 RelativeLayout.YConstraint="0"
                 RelativeLayout.WidthConstraint="5"
                 RelativeLayout.HeightConstraint="65" />
        <Label Text="Stylish header"
               FontSize="24"
               RelativeLayout.XConstraint="30"
               RelativeLayout.YConstraint="25" />
    </RelativeLayout>
</ContentPage>
```

In diesem Beispiel wird die Position der einzelnen [`BoxView`](xref:Xamarin.Forms.BoxView) -Objekte mit den Werten definiert, die in [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty) den [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty) angefügten Eigenschaften und angegeben sind. Die Größe jedes `BoxView` wird mit den Werten definiert, die in den [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty) [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty) angefügten Eigenschaften und angegeben sind. Die Position des [`Label`](xref:Xamarin.Forms.Label) -Objekts wird auch mit den Werten definiert, die in `XConstraint` den `YConstraint` angefügten Eigenschaften und angegeben sind. Größen Werte werden jedoch nicht für die festgelegt `Label` , und daher ist die Größe nicht beschränkt. In allen Fällen stellen die absoluten Werte geräteunabhängige Einheiten dar.

Die folgenden Screenshots zeigen das resultierende Layout:

![Untergeordnete Elemente in einem relativelayout mit absoluten Werten](relativelayout-images/absolute-values.png)

Der entsprechende c#-Code wird unten dargestellt:

```csharp
public class StylishHeaderDemoPageCS : ContentPage
{
    public StylishHeaderDemoPageCS()
    {
        RelativeLayout relativeLayout = new RelativeLayout
        {
            Margin = new Thickness(20)
        };

        relativeLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, () => new Rectangle(0, 10, 200, 5));

        relativeLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, () => new Rectangle(0, 20, 200, 5));

        relativeLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, () => new Rectangle(10, 0, 5, 65));

        relativeLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, () => new Rectangle(20, 0, 5, 65));

        relativeLayout.Children.Add(new Label
        {
            Text = "Stylish Header",
            FontSize = 24
        }, Constraint.Constant(30), Constraint.Constant(25));

        Title = "Stylish header demo";
        Content = relativeLayout;
    }
}
```

In diesem Beispiel [`BoxView`](xref:Xamarin.Forms.BoxView) werden-Objekte mithilfe einer Überladung hinzugefügt, die [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) `Add` einen erfordert, `Expression<Func<Rectangle>>` um die Position und Größe der einzelnen untergeordneten Elemente anzugeben. Die Position von [`Label`](xref:Xamarin.Forms.Label) wird mithilfe einer Überladung definiert `Add` , die optionale-Objekte erfordert [`Constraint`](xref:Xamarin.Forms.Constraint) , in diesem Fall von der- [`Constraint.Constant`](xref:Xamarin.Forms.Constraint.Constant*) Methode erstellt.

> [!NOTE]
> Ein [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) , der absolute Werte verwendet, kann untergeordnete Elemente positionieren und verkleinern, sodass Sie nicht innerhalb der Begrenzungen des Layouts passen.

## <a name="relative-positioning-and-sizing"></a>Relative Positionierung und Größenanpassung

Ein [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) kann untergeordnete Elemente mithilfe von Werten positionieren und verkleinern, die relativ zu den Eigenschaften des Layouts oder gleich geordnete Elemente sind. Dies wird erreicht, indem der-Auflistung untergeordnete Elemente hinzugefügt `Children` `RelativeLayout` werden und die [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty) Eigenschaften,, und für jedes untergeordnete Element [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty) [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty) [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty) auf relative Werte mithilfe [`Constraint`](xref:Xamarin.Forms.Constraint) von-Objekten festgelegt werden.

Einschränkungen können eine Konstante sein, die relativ zu einem übergeordneten Element oder relativ zu einem gleich geordneten Element ist. Der Typ der Einschränkung wird durch die- [`ConstraintType`](xref:Xamarin.Forms.ConstraintType) Enumeration dargestellt, die die folgenden Member definiert:

- `RelativeToParent`, das eine Einschränkung angibt, die relativ zu einem übergeordneten Element ist.
- `RelativeToView`, das eine Einschränkung angibt, die relativ zu einer Ansicht (oder gleich geordnet) ist.
- `Constant`, die eine Konstante Einschränkung angibt.

### <a name="constraint-markup-extension"></a>Einschränkungs Markup Erweiterung

In XAML kann ein- [`Constraint`](xref:Xamarin.Forms.Constraint) Objekt von der [`ConstraintExpression`](xref:Xamarin.Forms.ConstraintExpression) Markup Erweiterung erstellt werden. Diese Markup Erweiterung wird in der Regel verwendet, um die Position und Größe eines untergeordneten Elements innerhalb eines [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) mit dem übergeordneten Element oder einem gleich geordneten Element in Beziehung zu setzen.

Die- [`ConstraintExpression`](xref:Xamarin.Forms.ConstraintExpression) Klasse definiert die folgenden Eigenschaften:

- [`Constant`](xref:Xamarin.Forms.ConstraintExpression.Constant)vom Typ, der den Einschränkungs `double` Konstanten Wert darstellt.
- [`ElementName`](xref:Xamarin.Forms.ConstraintExpression.ElementName)vom Typ `string` , der den Namen eines Quell Elements darstellt, für das die Einschränkung berechnet werden soll.
- [`Factor`](xref:Xamarin.Forms.ConstraintExpression.Factor)vom Typ `double` , der den Faktor darstellt, um den eine eingeschränkte Dimension relativ zum Quell Element skaliert werden soll. Diese Eigenschaft hat den Standardwert 1.
- [`Property`](xref:Xamarin.Forms.ConstraintExpression.Property)vom Typ `string` , der den Namen der Eigenschaft für das Quell Element darstellt, das bei der Einschränkungs Berechnung verwendet werden soll.
- [`Type`](xref:Xamarin.Forms.ConstraintExpression.Type)vom Typ [`ConstraintType`](xref:Xamarin.Forms.ConstraintType) , der den Typ der Einschränkung darstellt.

Weitere Informationen über Xamarin.Forms-Markuperweiterungen finden Sie unter [XAML-Markuperweiterungen](~/xamarin-forms/xaml/markup-extensions/index.md).

Der folgende XAML-Code zeigt ein-Element, dessen untergeordnete Elemente [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) durch die [`ConstraintExpression`](xref:Xamarin.Forms.ConstraintExpression) Markup Erweiterung eingeschränkt werden:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="RelativeLayoutDemos.Views.RelativePositioningAndSizingDemoPage"
             Title="RelativeLayout demo">
    <RelativeLayout>
        <BoxView Color="Red"
                 RelativeLayout.XConstraint="{ConstraintExpression Type=Constant, Constant=0}"
                 RelativeLayout.YConstraint="{ConstraintExpression Type=Constant, Constant=0}" />
        <BoxView Color="Green"
                 RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Constant=-40}"
                 RelativeLayout.YConstraint="{ConstraintExpression Type=Constant, Constant=0}" />
        <BoxView Color="Blue"
                 RelativeLayout.XConstraint="{ConstraintExpression Type=Constant, Constant=0}"
                 RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Constant=-40}" />
        <BoxView Color="Yellow"
                 RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Constant=-40}"
                 RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Constant=-40}" />

        <!-- Centered and 1/3 width and height of parent -->
        <BoxView x:Name="oneThird"
                 Color="Silver"
                 RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=0.33}"
                 RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0.33}"
                 RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=0.33}"
                 RelativeLayout.HeightConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0.33}" />

        <!-- 1/3 width and height of previous -->
        <BoxView Color="Black"
                 RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToView, ElementName=oneThird, Property=X}"
                 RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToView, ElementName=oneThird, Property=Y}"
                 RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToView, ElementName=oneThird, Property=Width, Factor=0.33}"
                 RelativeLayout.HeightConstraint="{ConstraintExpression Type=RelativeToView, ElementName=oneThird, Property=Height, Factor=0.33}" />
    </RelativeLayout>
</ContentPage>
```

In diesem Beispiel wird die Position der einzelnen [`BoxView`](xref:Xamarin.Forms.BoxView) -Objekte durch Festlegen der [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty) [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty) angefügten Eigenschaften und definiert. In der ersten `BoxView` ist die `XConstraint` angefügte-Eigenschaft und die-Eigenschaft `YConstraint` auf Konstanten festgelegt, die absolute Werte sind. Für die restlichen `BoxView` Objekte wird Ihre Position festgelegt, indem mindestens ein relativer Wert verwendet wird. Beispielsweise legt das gelbe `BoxView` Objekt die `XConstraint` angefügte-Eigenschaft auf die Breite seines übergeordneten Elements (das [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) ) minus 40 fest. Auf ähnliche Weise wird `BoxView` die `YConstraint` angefügte-Eigenschaft auf die Höhe der übergeordneten minus 40 festgelegt. Dadurch wird sichergestellt, dass der gelbe `BoxView` in der unteren rechten Ecke des Bildschirms angezeigt wird.

> [!NOTE]
> [`BoxView`](xref:Xamarin.Forms.BoxView) für Objekte, die keine Größe angeben, wird die Größe automatisch um 40 x 40 x vergrößert Xamarin.Forms .

Das Silber [`BoxView`](xref:Xamarin.Forms.BoxView) benannte `oneThird` ist zentral positioniert, relativ zum übergeordneten Element. Die Größe ist auch relativ zum übergeordneten Element, das ein Drittel seiner Breite und Höhe ist. Dies wird erreicht, indem die [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty) [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty) angefügten Eigenschaften und auf die Breite des übergeordneten Elements (der [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) ), multipliziert mit 0,33, festgelegt werden. Entsprechend werden die [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty) [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty) angefügten Eigenschaften und auf die Höhe des übergeordneten Elements, multipliziert mit 0,33, festgelegt.

Der schwarze [`BoxView`](xref:Xamarin.Forms.BoxView) ist positioniert und ist relativ zum `oneThird` `BoxView` . Dies wird erreicht, indem die [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty) [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty) angefügten Eigenschaften und auf `X` die `Y` Werte und des neben geordneten Elements festgelegt werden. Entsprechend wird die Größe auf ein Drittel der Breite und Höhe des neben geordneten Elements festgelegt. Dies wird erreicht, indem [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty) [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty) die angefügten Eigenschaften und auf die Werte und des neben geordneten Elements festgelegt werden `Width` `Height` , die dann mit 0,33 multipliziert werden.

Der folgende Screenshot zeigt das Layout, das sich ergibt:

![Untergeordnete Elemente in einem relativelayout mithilfe relativer Werte](relativelayout-images/relative-values.png)

### <a name="constraint-objects"></a>Einschränkungs Objekte

Die- [`Constraint`](xref:Xamarin.Forms.Constraint) Klasse definiert die folgenden öffentlichen statischen Methoden, die-Objekte zurückgeben `Constraint` :

- [`Constant`](xref:Xamarin.Forms.Constraint.Constant*), wodurch ein untergeordnetes Element auf eine mit einem angegebene Größe beschränkt wird `double` .
- [`FromExpression`](xref:Xamarin.Forms.Constraint.FromExpression*), die ein untergeordnetes Element mithilfe eines Lambda-Ausdrucks einschränkt.
- [`RelativeToParent`](xref:Xamarin.Forms.Constraint.RelativeToParent*), die ein untergeordnetes Element in Relation zur Größe des übergeordneten Elements einschränkt.
- [`RelativeToView`](xref:Xamarin.Forms.Constraint.RelativeToView*), die ein untergeordnetes Element in Relation zur Größe einer Ansicht einschränkt.

Außerdem definiert die- [`BoundsConstraint`](xref:Xamarin.Forms.BoundsConstraint) Klasse eine einzelne Methode, [`FromExpression`](xref:Xamarin.Forms.BoundsConstraint.FromExpression*) , die einen zurückgibt, der `BoundsConstraint` die Position und Größe eines untergeordneten Elements mit einem einschränkt `Expression<Func<Rectangle>>` . Diese Methode kann verwendet werden, um die [`BoundsConstraint`](xref:Xamarin.Forms.RelativeLayout.BoundsConstraintProperty) angefügte-Eigenschaft festzulegen.

Der folgende c#-Code zeigt einen, [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) dessen untergeordnete Elemente von-Objekten eingeschränkt werden [`Constraint`](xref:Xamarin.Forms.Constraint) :

```csharp
public class RelativePositioningAndSizingDemoPageCS : ContentPage
{
    public RelativePositioningAndSizingDemoPageCS()
    {
        RelativeLayout relativeLayout = new RelativeLayout();

        // Four BoxView's
        relativeLayout.Children.Add(
            new BoxView { Color = Color.Red },
            Constraint.Constant(0),
            Constraint.Constant(0));

        relativeLayout.Children.Add(
            new BoxView { Color = Color.Green },
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Width - 40;
            }), Constraint.Constant(0));

        relativeLayout.Children.Add(
            new BoxView { Color = Color.Blue },
            Constraint.Constant(0),
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Height - 40;
            }));

        relativeLayout.Children.Add(
            new BoxView { Color = Color.Yellow },
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Width - 40;
            }),
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Height - 40;
            }));

        // Centered and 1/3 width and height of parent
        BoxView silverBoxView = new BoxView { Color = Color.Silver };
        relativeLayout.Children.Add(
            silverBoxView,
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Width * 0.33;
            }),
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Height * 0.33;
            }),
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Width * 0.33;
            }),
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Height * 0.33;
            }));

        // 1/3 width and height of previous
        relativeLayout.Children.Add(
            new BoxView { Color = Color.Black },
            Constraint.RelativeToView(silverBoxView, (parent, sibling) =>
            {
                return sibling.X;
            }),
            Constraint.RelativeToView(silverBoxView, (parent, sibling) =>
            {
                return sibling.Y;
            }),
            Constraint.RelativeToView(silverBoxView, (parent, sibling) =>
            {
                return sibling.Width * 0.33;
            }),
            Constraint.RelativeToView(silverBoxView, (parent, sibling) =>
            {
                return sibling.Height * 0.33;
            }));

        Title = "RelativeLayout demo";
        Content = relativeLayout;
    }
}
```

In diesem Beispiel werden dem untergeordnete Elemente mithilfe der-Überladung hinzugefügt, die [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) `Add` ein optionales `Constraint` -Objekt für die `x` `y` Argumente,, `width` und erfordert `height` .

> [!NOTE]
> Eine [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) , die relative Werte verwendet, kann untergeordnete Elemente positionieren und verkleinern, sodass Sie nicht innerhalb der Begrenzungen des Layouts passen.

## <a name="related-links"></a>Verwandte Links

- [Relativelayout-Demos (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-relativelayoutdemos)
- [Xamarin.Forms Angefügte Eigenschaften](~/xamarin-forms/xaml/attached-properties.md)
- [XAML-Markuperweiterungen](~/xamarin-forms/xaml/markup-extensions/index.md)
- [Layout auswählen Xamarin.Forms](choose-layout.md)
- [Optimieren der Xamarin.Forms App-Leistung](~/xamarin-forms/deploy-test/performance.md)
