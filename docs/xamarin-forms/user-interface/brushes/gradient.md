---
title: 'Xamarin.FormsPinsel: Farbverläufe'
description: Die Xamarin.Forms GradientBrush-Klasse ist eine abstrakte Klasse, die einen Farbverlauf beschreibt, der aus Farbverlaufs Stopps besteht.
ms.prod: xamarin
ms.assetid: 24763E56-74EC-4082-897B-E4EAACCADFEE
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/27/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 6b6fe37fda3fd54b4df5cb6f5dacce0d910ecb3f
ms.sourcegitcommit: 08290d004d1a7e7ac579bf1f96abf8437921dc70
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87919134"
---
# <a name="no-locxamarinforms-brushes-gradients"></a>Xamarin.FormsPinsel: Farbverläufe

![Vorschau-API](~/media/shared/preview.png "Diese API ist derzeit als Vorabversion erhältlich.")

[![Beispiel herunterladen](~/media/shared/download.png) Herunterladen des Beispiels](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)

Die `GradientBrush` -Klasse wird von der `Brush` -Klasse abgeleitet, und ist eine abstrakte Klasse, die einen Farbverlauf beschreibt, der aus Farbverlaufs Stopps besteht. Ein Farbverlaufspinsel zeichnet einen Bereich mit mehreren Farben, die sich auf einer Achse miteinander vermischen. Klassen, die von abgeleitet `GradientBrush` werden, beschreiben verschiedene Möglichkeiten zum Interpretieren von Farbverlaufs Stopps und stellen Xamarin.Forms die folgenden Farbverlaufs Pinsel bereit:

- `LinearGradientBrush`, der einen Bereich mit einem linearen Farbverlauf zeichnet. Weitere Informationen finden Sie unter [ Xamarin.Forms Pinsel: lineare Farbverläufe](lineargradient.md).
- `RadialGradientBrush`, der einen Bereich mit einem radialen Farbverlauf zeichnet. Weitere Informationen finden Sie unter [ Xamarin.Forms Pinsel: radiale Farbverläufe](radialgradient.md).

Die `GradientBrush` -Klasse definiert die `GradientStops` -Eigenschaft vom Typ `GradientStopsCollection` , die die Farbverlaufs Stopps des Pinsels darstellt, von denen jede eine Farbe und einen Offset entlang der Farbverlaufs Achse des Pinsels angibt. Ein- `GradientStopsCollection` Objekt ist ein `ObservableCollection` von- `GradientStop` Objekten. Die `GradientStops` -Eigenschaft wird von einem [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) -Objekt unterstützt. Dies bedeutet, dass es sich um das Ziel der Daten Bindungen und die Formatierung handeln kann.

> [!NOTE]
> Die `GradientStops` -Eigenschaft ist der der `ContentProperty` `GradientBrush` -Klasse und muss daher nicht explizit aus XAML festgelegt werden.

## <a name="gradient-stops"></a>Farbverlaufsstopps

Farbverlaufs Stopps sind die Bausteine eines Farbverlaufs Pinsels und geben die Farben im Farbverlauf und deren Position entlang der Farbverlaufs Achse an. Farbverlaufs Stopps werden mithilfe von- `GradientStop` Objekten angegeben.

Die `GradientStop`-Klasse definiert die folgenden Eigenschaften:

- `Color`vom Typ [`Color`](xref:Xamarin.Forms.Color) , der die Farbe des Farbverlaufs Stopps darstellt. Der Standardwert dieser Eigenschaft ist `Color.Default`.
- `Offset`vom Typ `float` , der den Speicherort des Farbverlaufs Stopps innerhalb des Farbverlaufs Vektors darstellt. Der Standardwert dieser Eigenschaft ist 0. gültige Werte liegen im Bereich 0,0-1.0. Je näher der Wert an 0 liegt, desto näher ist die Farbe am Anfang des Farbverlaufs. Je näher der Wert an 1 liegt, desto näher ist die Farbe am Ende des Farbverlaufs.

Diese Eigenschaften werden von Objekten unterstützt [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) . Dies bedeutet, dass Sie Ziele von Daten Bindungen und formatiert sein können.

> [!IMPORTANT]
> Das von Farbverläufen verwendete Koordinatensystem ist relativ zu einem umgebenden Feld für den Ausgabebereich. 0 gibt 0 Prozent, und 1 gibt 100 Prozent des umgebenden Feldes an. Daher beschreibt (0,5, 0,5) einen Punkt in der Mitte des umgebenden Felds, und (1, 1) beschreibt einen Punkt in der unteren rechten Ecke des umgebenden Felds.

Das folgende XAML-Beispiel erstellt eine Diagonale `LinearGradientBrush` mit vier Farben:

```xaml
<LinearGradientBrush StartPoint="0,0"
                     EndPoint="1,1">
    <GradientStop Color="Yellow"
                  Offset="0.0" />
    <GradientStop Color="Red"
                  Offset="0.25" />
    <GradientStop Color="Blue"
                  Offset="0.75" />             
    <GradientStop Color="LimeGreen"
                  Offset="1.0" />
</LinearGradientBrush>                                                       
```

Die Farbe jedes Punkts zwischen den Farbverlaufs Stopps wird als eine Kombination der Farbe interpoliert, die durch die zwei Begrenzungs Farbverlaufs Stopps angegeben wird. Das folgende Diagramm zeigt die Farbverlaufs Stopps aus dem vorherigen Beispiel:

![Mit einem diagonalen LinearGradientBrush gezeichnetes Frame](gradient-images/gradient-stops.png)

In diesem Diagramm markieren die Kreise die Position von Farbverlaufs Stopps, und die gestrichelte Linie zeigt die Farbverlaufs Achse an. Der erste Farbverlaufs Ende gibt die Farbe Gelb an einem Offset von 0,0 an. Der zweite Farbverlaufs Ende gibt die Farbe rot bei einem Offset von 0,25 an. Die Punkte zwischen diesen beiden Farbverlaufs Stopps werden allmählich von Gelb in rot geändert, wenn Sie von links nach rechts entlang der Farbverlaufs Achse wechseln. Der dritte Farbverlaufs Ende gibt die Farbe blau bei einem Offset von 0,75 an. Die Farbe der Punkte zwischen dem zweiten und dritten Farbverlaufsstopp ändert sich allmählich von Rot zu Blau. Der vierte Farbverlaufs-halte Wert gibt die Farbe für den kalkgrünen Wert am Offset von 1,0 an. Die Farbe der Punkte zwischen dem dritten und vierten Farbverlaufsstopp ändert sich allmählich von Blau zu Gelbgrün.

## <a name="related-links"></a>Verwandte Links

- [Brushesdemos (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)
- [Xamarin.FormsPinsel: lineare Farbverläufe](lineargradient.md)
- [Xamarin.FormsPinsel: radiale Farbverläufe](radialgradient.md)
