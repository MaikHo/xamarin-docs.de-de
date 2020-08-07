---
title: 'Xamarin.FormsPinsel: voll Tonfarben'
description: Die Xamarin.Forms SolidColorBrush-Klasse zeichnet einen Bereich mit einer voll Tonfarbe.
ms.prod: xamarin
ms.assetid: 4225D40A-16C1-40E1-ACBE-23E321E7FDE4
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/27/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 04e882f9b64d0e1f56e1170d353af4e13b079933
ms.sourcegitcommit: 08290d004d1a7e7ac579bf1f96abf8437921dc70
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87919090"
---
# <a name="no-locxamarinforms-brushes-solid-colors"></a>Xamarin.FormsPinsel: voll Tonfarben

![Vorschau-API](~/media/shared/preview.png "Diese API ist derzeit als Vorabversion erhältlich.")

[![Beispiel herunterladen](~/media/shared/download.png) Herunterladen des Beispiels](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)

Die `SolidColorBrush` -Klasse wird von der `Brush` -Klasse abgeleitet und zum Zeichnen eines Bereichs mit einer voll Tonfarbe verwendet. Es gibt eine Vielzahl von Ansätzen zum Angeben der Farbe einer `SolidColorBrush` . Beispielsweise können Sie die Farbe mit einem [`Color`](xref:Xamarin.Forms.Color) Wert oder mit einem der vordefinierten Objekte angeben, `SolidColorBrush` die von der-Klasse bereitgestellt werden `Brush` .

Die- `SolidColorBrush` Klasse definiert die- `Color` Eigenschaft vom Typ [`Color`](xref:Xamarin.Forms.Color) , die die Farbe des Pinsels darstellt. Diese Eigenschaft wird von einem [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) -Objekt unterstützt. Dies bedeutet, dass es sich um das Ziel der Daten Bindungen handeln und formatiert werden kann.

Die- `SolidColorBrush` Klasse verfügt auch über eine- `IsEmpty` Methode, die einen zurückgibt `bool` , der angibt, ob dem Pinsel eine Farbe zugewiesen wurde.

## <a name="create-a-solidcolorbrush"></a>Erstellen eines SolidColorBrush

Es gibt drei Haupttechniken zum Erstellen einer `SolidColorBrush` . Sie können einen `SolidColorBrush` aus einem erstellen [`Color`](xref:Xamarin.Forms.Color) , einen vordefinierten Pinsel verwenden oder mithilfe der hexadezimal Schreibweise ein erstellen `SolidColorBrush` .

### <a name="use-a-predefined-color"></a>Vordefinierte Farbe verwenden

Xamarin.Formsenthält einen Typkonverter, der einen `SolidColorBrush` aus einem- [`Color`](xref:Xamarin.Forms.Color) Wert erstellt. In XAML ermöglicht dies das `SolidColorBrush` Erstellen eines aus einem vordefinierten `Color` Wert:

```xaml
<Frame Background="DarkBlue"
       BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120" />
```

In diesem Beispiel wird der Hintergrund von [`Frame`](xref:Xamarin.Forms.Frame) mit einem dunkelblauen gezeichnet `SolidColorBrush` :

![Frame mit einer vordefinierten Farbe gezeichnet](solidcolor-images/predefined-color.png)

Alternativ kann der [`Color`](xref:Xamarin.Forms.Color) Wert mit der Eigenschaft Tagsyntax angegeben werden:

```xaml
<Frame BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120">
       <Frame.Background>
           <SolidColorBrush Color="DarkBlue" />
       </Frame.Background>
</Frame>
```

In diesem Beispiel wird der Hintergrund von [`Frame`](xref:Xamarin.Forms.Frame) mit einem gezeichnet, `SolidColorBrush` dessen Farbe durch Festlegen der-Eigenschaft angegeben wird `SolidColorBrush.Color` .

### <a name="use-a-predefined-brush"></a>Verwenden eines vordefinierten Pinsels

Die- `Brush` Klasse definiert eine Reihe von häufig verwendeten- `SolidColorBrush` Objekten. Im folgenden Beispiel wird eines der folgenden vordefinierten `SolidColorBrush` Objekte verwendet:

```xaml
<Frame Background="{x:Static Brush.Indigo}"
       BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120" />       
```

Der entsprechende C#-Code lautet:

```csharp
Frame frame = new Frame
{
    Background = Brush.Indigo,
    BorderColor = Color.LightGray,
    // ...
};
```

In diesem Beispiel wird der Hintergrund der [`Frame`](xref:Xamarin.Forms.Frame) mit einem Indigo gezeichnet `SolidColorBrush` :

![Mit einem vordefinierten SolidColorBrush gezeichnetes Frame](solidcolor-images/predefined-brush.png)

Eine Liste der von `SolidColorBrush` der-Klasse bereitgestellten vordefinierten Objekte finden Sie unter Pinsel mit voll `Brush` [Tonfarbe](#solid-color-brushes).

### <a name="use-hexadecimal-notation"></a>Hexadezimale Notation verwenden

`SolidColorBrush`Objekte können auch mit hexadezimal Notation erstellt werden. Bei diesem Ansatz wird eine Farbe in Bezug auf die Menge von rot, grün und blau angegeben, um eine Farbe zu kombinieren. Das Haupt Format zum Angeben einer Farbe mit hexadezimal Notation ist `#rrggbb` , wobei Folgendes gilt:

- `rr`eine zweistellige hexadezimal Zahl, die die relative Menge von rot angibt.
- `gg`eine zweistellige hexadezimal Zahl, die die relative Menge von grün angibt.
- `bb`eine zweistellige hexadezimal Zahl, die die relative Menge an blau angibt.

Außerdem kann eine Farbe angegeben werden, `#aarrggbb` wobei `aa` den Alpha Wert oder Transparenz der Farbe angibt. Dieser Ansatz ermöglicht Ihnen die Erstellung von Farben, die teilweise transparent sind.

Im folgenden Beispiel wird der Farbwert eines `SolidColorBrush` mithilfe von hexadezimal Notation festgelegt:

```xaml
<Frame Background="#FF9988"
       BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120" />
```

In diesem Beispiel wird der Hintergrund der [`Frame`](xref:Xamarin.Forms.Frame) mit einem Lachs gefärbt gezeichnet `SolidColorBrush` :

![Frame, gezeichnet mit einem mit hexadezimalen Notation erstellten SolidColorBrush](solidcolor-images/hex.png)

Weitere Methoden zum Beschreiben von Farben finden Sie unter [Farben Xamarin.Forms in ](~/xamarin-forms/user-interface/colors.md).

## <a name="solid-color-brushes"></a>Einfarbige Pinsel

Aus Gründen der praktische `Brush` bereitstellt die-Klasse eine Reihe von häufig verwendeten `SolidColorBrush` Objekten bereit, wie z `AliceBlue` . b `YellowGreen` . und. Die folgende Abbildung zeigt die Farbe jedes vordefinierten Pinsels, seinen Namen und seinen hexadezimalen Wert:

[![Farbtabelle einschließlich eines Farb Musters, eines Farbnamens und eines hexadezimal Werts](solidcolor-images/solidcolorbrushes.png)](solidcolor-images/solidcolorbrushes-large.png#lightbox)

## <a name="related-links"></a>Verwandte Links

- [Brushesdemos (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)
- [Farben inXamarin.Forms](~/xamarin-forms/user-interface/colors.md)
