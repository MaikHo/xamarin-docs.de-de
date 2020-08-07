---
title: 'Xamarin.FormsPinsel: radiale Farbverläufe'
description: Die Xamarin.Forms Klasse RadialGradientBrush zeichnet einen Bereich mit einem radialen Farbverlauf.
ms.prod: xamarin
ms.assetid: 099BA530-3B38-4005-9B19-A0EB4D4DEEFC
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/28/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: dd915384c630cc08a2bd79a52dd22ccb40835dfa
ms.sourcegitcommit: 08290d004d1a7e7ac579bf1f96abf8437921dc70
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87919095"
---
# <a name="no-locxamarinforms-brushes-radial-gradients"></a>Xamarin.FormsPinsel: radiale Farbverläufe

![Vorschau-API](~/media/shared/preview.png "Diese API ist derzeit als Vorabversion erhältlich.")

[![Beispiel herunterladen](~/media/shared/download.png) Herunterladen des Beispiels](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)

Die `RadialGradientBrush` -Klasse wird von der `GradientBrush` -Klasse abgeleitet und zeichnet einen Bereich mit einem radialen Farbverlauf, der zwei oder mehr Farben in einem Kreis kombiniert. `GradientStop`-Objekte werden verwendet, um die Farben im Farbverlauf und deren Positionen anzugeben. Weitere Informationen zu `GradientStop` Objekten finden Sie unter [ Xamarin.Forms Pinsel: Farbverläufe](gradient.md).

Die `RadialGradientBrush`-Klasse definiert die folgenden Eigenschaften:

- `Center`vom Typ [`Point`](xref:Xamarin.Forms.Point) , der den Mittelpunkt des Kreises für den radialen Farbverlauf darstellt. Der Standardwert dieser Eigenschaft ist (0,5, 0,5).
- `Radius`vom Typ `double` , der den Radius des Kreises für den radialen Farbverlauf darstellt. Der Standardwert dieser Eigenschaft ist 0,5.

Diese Eigenschaften werden von Objekten unterstützt [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) . Dies bedeutet, dass Sie Ziele von Daten Bindungen und formatiert sein können.

Die- `RadialGradientBrush` Klasse verfügt auch über eine- `IsEmpty` Methode, die einen zurückgibt `bool` , der angibt, ob dem Pinsel Objekte zugewiesen wurden `GradientStop` .

> [!NOTE]
> Radiale Farbverläufe können auch mit der `radial-gradient()` CSS-Funktion erstellt werden.

## <a name="create-a-radialgradientbrush"></a>Erstellen eines RadialGradientBrush

Die Farbverlaufs Stopps eines radialen Farbverlaufs werden entlang einer durch einen Kreis definierten Farbverlaufs Achse positioniert. Die Farbverlaufs Achse strahlt von der Mitte des Kreises bis zu ihrem Umfang. Die Position und die Größe des Kreises können mithilfe der-und-Eigenschaften des Pinsels geändert werden `Center` `Radius` . Der Kreis definiert den Endpunkt des Farbverlaufs. Daher definiert ein Farbverlaufs Ende bei 1,0 die Farbe im Kreisumfang. Ein Farbverlaufs Ende bei 0,0 definiert die Farbe in der Mitte des Kreises.

Um einen radialen Farbverlauf zu erstellen, erstellen Sie ein `RadialGradientBrush` -Objekt, und legen Sie dessen `Center` und- `Radius` Eigenschaften Fügen Sie dann zwei oder mehr- `GradientStop` Objekte zur `RadialGradientBrush.GradientStops` -Auflistung hinzu, die die Farben im Farbverlauf und deren Positionen angeben.

Das folgende XAML-Beispiel zeigt eine `RadialGradientBrush` , die als eines festgelegt ist `Background` [`Frame`](xref:Xamarin.Forms.Frame) :

```xaml    
<Frame BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120">
    <Frame.Background>
        <!-- Center defaults to (0.5,0.5)
             Radius defaults to (0.5) -->
        <RadialGradientBrush>
            <GradientStop Color="Red"
                          Offset="0.1" />
            <GradientStop Color="DarkBlue"
                          Offset="1.0" />
        </RadialGradientBrush>
    </Frame.Background>
</Frame>
```

In diesem Beispiel wird der Hintergrund von [`Frame`](xref:Xamarin.Forms.Frame) mit einem gezeichnet, der `RadialGradientBrush` von rot bis dunkelblau interpoliert. Die Mitte des radialen Farbverlaufs befindet sich im Mittelpunkt der `Frame` :

![Frame, gezeichnet mit einem zentrierten RadialGradientBrush](radialgradient-images/center.png)

Im folgenden XAML-Beispiel wird der Mittelpunkt des radialen Farbverlaufs in die linke obere Ecke der verschoben [`Frame`](xref:Xamarin.Forms.Frame) :

```xaml
<!-- Radius defaults to (0.5) -->
<RadialGradientBrush Center="0.0,0.0">
    <GradientStop Color="Red"
                  Offset="0.1" />
    <GradientStop Color="DarkBlue"
                  Offset="1.0" />
</RadialGradientBrush>
```

In diesem Beispiel wird der Hintergrund von [`Frame`](xref:Xamarin.Forms.Frame) mit einem gezeichnet, der `RadialGradientBrush` von rot bis dunkelblau interpoliert. Die Mitte des radialen Farbverlaufs befindet sich in der oberen linken Ecke des `Frame` :

![Frame, gezeichnet mit einem oberen linken RadialGradientBrush](radialgradient-images/top-left.png)

Im folgenden XAML-Beispiel wird die Mitte des radialen Farbverlaufs in die untere rechte Ecke der verschoben [`Frame`](xref:Xamarin.Forms.Frame) :

```xaml
<!-- Radius defaults to (0.5) -->
<RadialGradientBrush Center="1.0,1.0">
    <GradientStop Color="Red"
                  Offset="0.1" />
    <GradientStop Color="DarkBlue"
                  Offset="1.0" />
</RadialGradientBrush>            
```

In diesem Beispiel wird der Hintergrund von [`Frame`](xref:Xamarin.Forms.Frame) mit einem gezeichnet, der `RadialGradientBrush` von rot bis dunkelblau interpoliert. Die Mitte des radialen Farbverlaufs befindet sich unten rechts in der `Frame` :

![Mit einem unteren rechten RadialGradientBrush gezeichnetes Frame](radialgradient-images/bottom-right.png)

## <a name="related-links"></a>Verwandte Links

- [Brushesdemos (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)
- [Xamarin.FormsPinsel: Farbverläufe](gradient.md)
