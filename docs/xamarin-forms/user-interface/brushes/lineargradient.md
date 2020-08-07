---
title: 'Xamarin.FormsPinsel: lineare Farbverläufe'
description: Die Xamarin.Forms LinearGradientBrush-Klasse zeichnet einen Bereich mit einem linearen Farbverlauf.
ms.prod: xamarin
ms.assetid: BEA2B3F5-96B0-4E39-88A6-0FAFE95C3DCD
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/28/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: e83e3cc110e2ab5f9bf6a1cda54fbb88e65bee17
ms.sourcegitcommit: 08290d004d1a7e7ac579bf1f96abf8437921dc70
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87919094"
---
# <a name="no-locxamarinforms-brushes-linear-gradients"></a>Xamarin.FormsPinsel: lineare Farbverläufe

![Vorschau-API](~/media/shared/preview.png "Diese API ist derzeit als Vorabversion erhältlich.")

[![Beispiel herunterladen](~/media/shared/download.png) Herunterladen des Beispiels](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)

Die `LinearGradientBrush` -Klasse wird von der `GradientBrush` -Klasse abgeleitet und zeichnet einen Bereich mit einem linearen Farbverlauf, der zwei oder mehr Farben entlang einer Linie kombiniert, die als Farbverlaufs Achse bezeichnet wird. `GradientStop`-Objekte werden verwendet, um die Farben im Farbverlauf und deren Positionen anzugeben. Weitere Informationen zu `GradientStop` Objekten finden Sie unter [ Xamarin.Forms Pinsel: Farbverläufe](gradient.md).

Die `LinearGradientBrush`-Klasse definiert die folgenden Eigenschaften:

- `StartPoint`vom Typ [`Point`](xref:Xamarin.Forms.Point) , der die zweidimensionalen anfangs Koordinaten des linearen Farbverlaufs darstellt. Der Standardwert dieser Eigenschaft ist (0,0).
- `EndPoint`vom Typ [`Point`](xref:Xamarin.Forms.Point) , der die zweidimensionalen Endkoordinaten des linearen Farbverlaufs darstellt. Der Standardwert dieser Eigenschaft ist (1, 1).

Diese Eigenschaften werden von Objekten unterstützt [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) . Dies bedeutet, dass Sie Ziele von Daten Bindungen und formatiert sein können.

Die- `LinearGradientBrush` Klasse ist auch eine- `IsEmpty` Methode, die einen zurückgibt `bool` , der angibt, ob dem Pinsel Objekte zugewiesen wurden `GradientStop` .

> [!NOTE]
> Lineare Farbverläufe können auch mit der CSS-Funktion erstellt werden `linear-gradient()` .

## <a name="create-a-lineargradientbrush"></a>Erstellen eines LinearGradientBrush

Die Verlaufs Stopps eines linearen Farbverlaufs Pinsels werden entlang der Farbverlaufs Achse positioniert. Die Ausrichtung und die Größe der Farbverlaufs Achse können mithilfe der-und-Eigenschaften des Pinsels geändert werden `StartPoint` `EndPoint` . Durch die Bearbeitung dieser Eigenschaften können Sie horizontale, vertikale und diagonale Farbverläufe erstellen, die Richtung des Farbverlaufs umkehren, die Verlaufs Verteilung und vieles mehr umkehren.

Die `StartPoint` -Eigenschaft und die-Eigenschaft `EndPoint` sind relativ zum Bereich, der gezeichnet wird. (0,0) stellt die obere linke Ecke des gezeichneten Bereichs dar, und (1, 1) stellt die untere rechte Ecke des Bereichs dar, der gezeichnet wird. Das folgende Diagramm zeigt die Farbverlaufs Achse für einen diagonalen linearen Farbverlaufs Pinsel:

![Frame mit koordinaler Farbverlaufs Achse](lineargradient-images/gradient-axis.png)

In diesem Diagramm zeigt die gestrichelte Linie die Farbverlaufs Achse, mit der der Interpolations Pfad des Farbverlaufs vom Startpunkt bis zum Endpunkt hervorgehoben wird.

### <a name="create-a-horizontal-linear-gradient"></a>Horizontalen linearen Farbverlauf erstellen

Um einen horizontalen linearen Farbverlauf zu erstellen, erstellen Sie ein `LinearGradientBrush` -Objekt, und legen `StartPoint` Sie dessen auf (0, 0) und den Wert `EndPoint` auf (1, 0) fest. Fügen Sie dann zwei oder mehr- `GradientStop` Objekte zur `LinearGradientBrush.GradientStops` -Auflistung hinzu, die die Farben im Farbverlauf und deren Positionen angeben.

Das folgende XAML-Beispiel zeigt ein horizontales `LinearGradientBrush` , das als eines festgelegt ist `Background` [`Frame`](xref:Xamarin.Forms.Frame) :

```xaml
<Frame BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120">
    <Frame.Background>
        <!-- StartPoint defaults to (0,0) -->
        <LinearGradientBrush EndPoint="1,0">
            <GradientStop Color="Yellow"
                          Offset="0.1" />
            <GradientStop Color="Green"
                          Offset="1.0" />
        </LinearGradientBrush>
    </Frame.Background>
</Frame>  
```

In diesem Beispiel wird der Hintergrund von [`Frame`](xref:Xamarin.Forms.Frame) mit einem gezeichnet, `LinearGradientBrush` das horizontal zwischen gelb und grün interpoliert:

![Mit horizontaler LinearGradientBrush gezeichnetes Frame](lineargradient-images/horizontal.png)

### <a name="create-a-vertical-linear-gradient"></a>Einen vertikalen linearen Farbverlauf erstellen

Um einen vertikalen linearen Farbverlauf zu erstellen, erstellen Sie ein `LinearGradientBrush` -Objekt, und legen `StartPoint` Sie dessen auf (0, 0) und den Wert `EndPoint` auf (0,0) fest. Fügen Sie dann zwei oder mehr- `GradientStop` Objekte zur `LinearGradientBrush.GradientStops` -Auflistung hinzu, die die Farben im Farbverlauf und deren Positionen angeben.

Das folgende XAML-Beispiel zeigt eine vertikale `LinearGradientBrush` , die als eines festgelegt ist `Background` [`Frame`](xref:Xamarin.Forms.Frame) :

```xaml
<Frame BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120">
    <Frame.Background>
        <!-- StartPoint defaults to (0,0) -->    
        <LinearGradientBrush EndPoint="0,1">
            <GradientStop Color="Yellow"
                          Offset="0.1" />
            <GradientStop Color="Green"
                          Offset="1.0" />
        </LinearGradientBrush>
    </Frame.Background>
</Frame>
```

In diesem Beispiel wird der Hintergrund von [`Frame`](xref:Xamarin.Forms.Frame) mit einem gezeichnet, `LinearGradientBrush` das vertikal von gelb zu grün interpoliert:

![Mit einem vertikalen LinearGradientBrush gezeichnetes Frame](lineargradient-images/vertical.png)

### <a name="create-a-diagonal-linear-gradient"></a>Einen diagonalen linearen Farbverlauf erstellen

Um einen diagonalen linearen Farbverlauf zu erstellen, erstellen Sie ein `LinearGradientBrush` -Objekt, und legen `StartPoint` Sie dessen auf (0, 0) und den Wert `EndPoint` auf (1, 1) fest. Fügen Sie dann zwei oder mehr- `GradientStop` Objekte zur `LinearGradientBrush.GradientStops` -Auflistung hinzu, die die Farben im Farbverlauf und deren Positionen angeben.

Das folgende XAML-Beispiel zeigt eine Diagonale `LinearGradientBrush` , die als eines festgelegt ist `Background` [`Frame`](xref:Xamarin.Forms.Frame) :

```xaml
<Frame BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120">
    <Frame.Background>
        <!-- StartPoint defaults to (0,0)      
             Endpoint defaults to (1,1) -->
        <LinearGradientBrush>
            <GradientStop Color="Yellow"
                          Offset="0.1" />
            <GradientStop Color="Green"
                          Offset="1.0" />
        </LinearGradientBrush>
    </Frame.Background>
</Frame>
```

In diesem Beispiel wird der Hintergrund von [`Frame`](xref:Xamarin.Forms.Frame) mit einem gezeichnet, der `LinearGradientBrush` von gelb zu grün diagonal interpoliert wird:

![Mit einem diagonalen LinearGradientBrush gezeichnetes Frame](lineargradient-images/diagonal.png)

## <a name="related-links"></a>Verwandte Links

- [Brushesdemos (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)
- [Xamarin.FormsPinsel: Farbverläufe](gradient.md)
