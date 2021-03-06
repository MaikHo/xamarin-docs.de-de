---
title: Schriftarten inXamarin.Forms
description: In diesem Artikel wird erläutert, wie Sie Schriftart Informationen für Steuerelemente angeben, die Text in Xamarin.Forms Anwendungen anzeigen.
ms.prod: xamarin
ms.assetid: 49DD2249-C575-41AE-AE06-08F890FD6031
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/01/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: a657915edb41573f9637128b4c88233d58a5909a
ms.sourcegitcommit: 32d2476a5f9016baa231b7471c88c1d4ccc08eb8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2020
ms.locfileid: "84572207"
---
# <a name="fonts-in-xamarinforms"></a>Schriftarten inXamarin.Forms

[![Beispiel herunterladen](~/media/shared/download.png) Das Beispiel herunterladen](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/workingwithfonts)

In diesem Artikel wird beschrieben Xamarin.Forms , wie Sie für Steuerelemente, die Text anzeigen, Schriftart Attribute (einschließlich Gewichtung und Größe) angeben können. Schriftart Informationen können [im Code](#set-the-font-in-code) oder [in XAML](#set-the-font-in-xaml)angegeben werden. Es ist auch möglich, eine [benutzerdefinierte Schriftart](#use-a-custom-font)zu verwenden und [Schriftart Symbole anzuzeigen](#display-font-icons).

## <a name="set-the-font-in-code"></a>Festlegen der Schriftart im Code

Verwenden Sie die drei Schriftart bezogenen Eigenschaften von Steuerelementen, die Text anzeigen:

- **FontFamily** &ndash; der `string` Schriftart Name.
- **FontSize** &ndash; die Schriftgröße als `double` .
- **Fontattributes** &ndash; eine Zeichenfolge, die Stil Informationen wie *kursiv* und **Fett** angibt (mithilfe der- `FontAttributes` Enumeration in c#).

Dieser Code zeigt, wie Sie eine Bezeichnung erstellen und den Schrift Grad und die Größe angeben, die angezeigt werden sollen:

```csharp
var about = new Label
{
    FontSize = Device.GetNamedSize (NamedSize.Medium, typeof(Label)),
    FontAttributes = FontAttributes.Bold,
    Text = "Medium Bold Font"
};
```

### <a name="font-size"></a>Schriftgrad

Die- `FontSize` Eigenschaft kann auf einen doppelten Wert festgelegt werden, z. a.:

```csharp
label.FontSize = 24;
```

Der Größen Wert wird in geräteunabhängigen Einheiten gemessen. Weitere Informationen finden Sie unter [Maßeinheiten](~/xamarin-forms/user-interface/controls/common-properties.md#units-of-measurement).

Xamarin.Formsdefiniert auch Felder in der- [`NamedSize`](xref:Xamarin.Forms.NamedSize) Enumeration, die bestimmte Schriftgrößen darstellen. Weitere Informationen zu benannten Schriftgrößen finden Sie unter [benannte Schriftgrößen](#named-font-sizes).

### <a name="font-attributes"></a>Schriftart Attribute

Schriftarten wie **Fett** und *kursiv* können für die-Eigenschaft festgelegt werden `FontAttributes` . Die folgenden Werte werden derzeit unterstützt:

- **None**
- **Fett**
- **Kursiv**

Die- `FontAttribute` Enumeration kann wie folgt verwendet werden (Sie können jeweils ein einzelnes Attribut oder eine beliebige Angabe angeben `OR` ):

```csharp
label.FontAttributes = FontAttributes.Bold | FontAttributes.Italic;
```

### <a name="set-font-info-per-platform"></a>Schriftart Informationen pro Plattform festlegen

Alternativ kann die- `Device.RuntimePlatform` Eigenschaft verwendet werden, um unterschiedliche Schriftart Namen auf jeder Plattform festzulegen, wie in diesem Code veranschaulicht:

```csharp
label.FontFamily = Device.RuntimePlatform == Device.iOS ? "MarkerFelt-Thin" :
   Device.RuntimePlatform == Device.Android ? "Lobster-Regular.ttf#Lobster-Regular" : "Assets/Fonts/ArimaMadurai-Black.ttf#Arima Madurai",
label.FontSize = Device.RuntimePlatform == Device.iOS ? 24 :
   Device.RuntimePlatform == Device.Android ? Device.GetNamedSize(NamedSize.Medium, label) : Device.GetNamedSize(NamedSize.Large, label);
```

Eine gute Quelle für Schriftart Informationen für IOS ist [iosfonts.com](http://iosfonts.com).

## <a name="set-the-font-in-xaml"></a>Festlegen der Schriftart in XAML

Xamarin.FormsSteuerelemente, die Text anzeigen, verfügen über eine `FontSize` Eigenschaft, die in XAML festgelegt werden kann. Die einfachste Möglichkeit zum Festlegen der Schriftart in XAML besteht darin, die benannten Größen Enumerationswerte zu verwenden, wie im folgenden Beispiel gezeigt:

```xaml
<Label Text="Login" FontSize="Large"/>
<Label Text="Instructions" FontSize="Small"/>
```

Es gibt einen integrierten Konverter für die- `FontSize` Eigenschaft, mit der alle Schriftart Einstellungen als Zeichen folgen Wert in XAML ausgedrückt werden können. Außerdem kann die- `FontAttributes` Eigenschaft zum Angeben von Schriftart Attributen verwendet werden:

```xaml
<Label Text="Italics are supported" FontAttributes="Italic" />
<Label Text="Biggest NamedSize" FontSize="Large" />
<Label Text="Use size 72" FontSize="72" />
```

Die- [`Device.RuntimePlatform`](~/xamarin-forms/platform/device.md#provide-platform-specific-values) Eigenschaft kann auch in XAML verwendet werden, um eine andere Schriftart auf jeder Plattform zu erzeugen. Im folgenden Beispiel werden auf jeder Plattform verschiedene Schriftarten verwendet:

```xaml
<Label Text="Hello Forms with XAML">
    <Label.FontFamily>
        <OnPlatform x:TypeArguments="x:String">
                <On Platform="iOS" Value="MarkerFelt-Thin" />
                <On Platform="Android" Value="Lobster-Regular.ttf#Lobster-Regular" />
                <On Platform="UWP" Value="Assets/Fonts/ArimaMadurai-Black.ttf#Arima Madurai" />
        </OnPlatform>
    </Label.FontFamily>
</Label>
```

## <a name="named-font-sizes"></a>Benannte Schriftgrade

Xamarin.Formsdefiniert Felder in der- [`NamedSize`](xref:Xamarin.Forms.NamedSize) Enumeration, die bestimmte Schriftgrößen darstellen. In der folgenden Tabelle werden die Elemente `NamedSize` und ihre Standardgrößen für IOS, Android und die universelle Windows-Plattform (UWP) angezeigt:

| Member | iOS | Android | UWP |
| --- | --- | --- | --- |
| `Default` | 16 | 14 | 14 |
| `Micro` | 11 | 10 | 15,667 |
| `Small` | 13 | 14 | 18,667 |
| `Medium` | 16 | 17 | 22,667 |
| `Large` | 20 | 22 | 32 |
| `Body` | 17 | 16 | 14 |
| `Header` | 17 | 96 | 46 |
| `Title` | 28 | 24 | 24 |
| `Subtitle` | 22 | 16 | 20 |
| `Caption` | 12 | 12 | 12 |

Die Größen Werte werden in geräteunabhängigen Einheiten gemessen. Weitere Informationen finden Sie unter [Maßeinheiten](~/xamarin-forms/user-interface/controls/common-properties.md#units-of-measurement).

Benannte Schriftgrößen können sowohl über XAML als auch über Code festgelegt werden. Außerdem kann die- `Device.GetNamedSize` Methode aufgerufen werden, um einen zurückzugeben `double` , der den benannten Schrift Grad darstellt:

```csharp
label.FontSize = Device.GetNamedSize(NamedSize.Small, typeof(Label));
```

> [!NOTE]
> Unter IOS und Android werden benannte Schriftgrößen basierend auf den Barrierefreiheits Optionen des Betriebssystems automatisch skaliert. Dieses Verhalten kann unter IOS mit einem plattformspezifischen deaktiviert werden. Weitere Informationen finden Sie unter [Barrierefreiheits Skalierung für benannte Schriftgrößen unter IOS](~/xamarin-forms/platform/ios/named-font-size-scaling.md).

## <a name="use-a-custom-font"></a>Benutzerdefinierte Schriftart verwenden

Benutzerdefinierte Schriftarten können dem Xamarin.Forms freigegebenen Projekt hinzugefügt und von Platt Form Projekten verwendet werden, ohne dass zusätzliche Aufgaben ausgeführt werden müssen. Die Vorgehensweise hierfür ist wie folgt:

1. Fügen Sie dem frei Xamarin.Forms gegebenen Projekt die Schriftart als eingebettete Ressource (Buildaktion **: EmbeddedResource**) hinzu.
1. Registrieren Sie die Schriftart Datei mit dem-Attribut in einer Datei, z. b. **AssemblyInfo.cs**, bei der Assembly `ExportFont` . Es kann auch ein optionaler Alias angegeben werden.

> [!IMPORTANT]
> Für eingebettete Schriftarten ist die Verwendung von Xamarin.Forms 4.5.0.530 oder höher erforderlich.

Im folgenden Beispiel wird die in der Assembly für die Assembly registrierte reguläre Schriftart zusammen mit einem Alias veranschaulicht:

```csharp
using Xamarin.Forms;

[assembly: ExportFont("Lobster-Regular.ttf", Alias = "Lobster")]
```

> [!NOTE]
> Die Schriftart kann sich in einem beliebigen Ordner im freigegebenen Projekt befinden, ohne den Ordnernamen beim Registrieren der Schriftart bei der Assembly angeben zu müssen.

Die Schriftart kann dann auf jeder Plattform verwendet werden, indem auf Ihren Namen ohne die Dateierweiterung verwiesen wird:

```xaml
<!-- Use font name -->
<Label Text="Hello Xamarin.Forms"
       FontFamily="Lobster-Regular" />
```

Alternativ kann Sie auf jeder Plattform genutzt werden, indem auf Ihren Alias verwiesen wird:

```xaml
<!-- Use font alias -->
<Label Text="Hello Xamarin.Forms"
       FontFamily="Lobster" />
```

Der entsprechende C#-Code lautet:

```csharp
// Use font name
Label label1 = new Label
{
    Text = "Hello Xamarin.Forms!",
    FontFamily = "Lobster-Regular"
};

// Use font alias
Label label2 = new Label
{
    Text = "Hello Xamarin.Forms!",
    FontFamily = "Lobster"
};
```

Die folgenden Screenshots zeigen die benutzerdefinierte Schriftart:

[![Benutzerdefinierte Schriftart unter IOS und Android](fonts-images/custom-sml.png "Beispiel für benutzerdefinierte Schriftart")](fonts-images/custom.png#lightbox "Beispiel für benutzerdefinierte Schriftart")

> [!IMPORTANT]
> Unter Windows können sich der Schriftart Dateiname und der Schriftart Name unterscheiden. Um den Schriftart Namen unter Windows zu ermitteln, klicken Sie mit der rechten Maustaste auf die Datei. ttf, und wählen Sie **Vorschau**aus. Der Schriftart Name kann dann im Vorschaufenster bestimmt werden.

## <a name="display-font-icons"></a>Anzeigen von Schriftartsymbolen

Schriftart Symbole können von Anwendungen angezeigt werden, Xamarin.Forms indem die Schriftart Symbol Daten in einem-Objekt angegeben werden `FontImageSource` . Diese Klasse, die von der- [`ImageSource`](xref:Xamarin.Forms.ImageSource) Klasse abgeleitet wird, verfügt über die folgenden Eigenschaften:

- `Glyph`– der Unicode-Zeichen Wert des Schriftart Symbols, das als angegeben wird `string` .
- `Size`– ein `double` Wert, der die Größe des gerenderten Schriftart Symbols in geräteunabhängigen Einheiten angibt. Der Standardwert ist 30. Außerdem kann diese Eigenschaft auf eine benannte Schriftgröße festgelegt werden.
- `FontFamily`– eine `string` , die die Schriftfamilie darstellt, zu der das Schriftart Symbol gehört.
- `Color`– ein optionaler [`Color`](xref:Xamarin.Forms.Color) Wert, der beim Anzeigen des Schriftart Symbols verwendet werden soll.

Diese Daten werden verwendet, um eine PNG-Datei zu erstellen, die von jeder Ansicht angezeigt werden kann, in der ein angezeigt werden kann `ImageSource` . Bei diesem Ansatz können Schriftart Symbole, wie z. b. Emojis, von mehreren Ansichten angezeigt werden, anstatt die Anzeige der Schriftart Symbole auf eine Ansicht zu beschränken, wie z [`Label`](xref:Xamarin.Forms.Label) . b. ein.

> [!IMPORTANT]
> Schriftart Symbole können derzeit nur durch ihre Unicode-Zeichen Darstellung angegeben werden.

Das folgende XAML-Beispiel zeigt ein einzelnes Schriftart Symbol, das von einer Ansicht angezeigt wird [`Image`](xref:Xamarin.Forms.Image) :

```xaml
<Image BackgroundColor="#D1D1D1">
    <Image.Source>
        <FontImageSource Glyph="&#xf30c;"
                         FontFamily="{OnPlatform iOS=Ionicons, Android=ionicons.ttf#}"
                         Size="44" />
    </Image.Source>
</Image>
```

Dieser Code zeigt ein Xbox-Symbol von der ionicons-Schriftfamilie in einer [`Image`](xref:Xamarin.Forms.Image) Ansicht an. Beachten Sie, dass das Unicode-Zeichen für dieses Symbol in XAML mit Escapezeichen versehen `\uf30c` werden muss und daher zu wird `&#xf30c;` . Der entsprechende C#-Code lautet:

```csharp
Image image = new Image { BackgroundColor = Color.FromHex("#D1D1D1") };
image.Source = new FontImageSource
{
    Glyph = "\uf30c",
    FontFamily = Device.RuntimePlatform == Device.iOS ? "Ionicons" : "ionicons.ttf#",
    Size = 44
};
```

Die folgenden Screenshots aus dem Beispiel für [bindbare Layouts](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-bindablelayouts) zeigen, dass mehrere Schriftart Symbole von einem bindbaren Layout angezeigt werden:

![Screenshot der angezeigten Schriftart Symbole unter IOS und Android](fonts-images/font-image-source.png "In einer Bildansicht angezeigte Schriftart Symbole")

## <a name="related-links"></a>Verwandte Links

- [Fontssample](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/workingwithfonts)
- [Text (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-text)
- [Bindbare Layouts (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-bindablelayouts)
- [Bindbare Layouts](~/xamarin-forms/user-interface/layouts/bindable-layouts.md)
