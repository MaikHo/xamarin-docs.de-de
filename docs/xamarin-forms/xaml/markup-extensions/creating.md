---
title: Erstellen von XAML-Markuperweiterungen
description: In diesem Artikel wird erläutert, wie Sie Ihre eigenen benutzerdefinierten Xamarin.Forms-XAML-Markuperweiterungen definieren. Eine XAML-Markup Erweiterung ist eine Klasse, die die Schnittstelle "imarkupextension<T> " oder "imarkupextension" implementiert.
ms.prod: xamarin
ms.assetid: 797C1EF9-1C8E-4208-8610-9B79CCF17D46
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 01/05/2018
ms.openlocfilehash: 4d26713f258a8c97abd4b4e9970ebdd4d490f485
ms.sourcegitcommit: 3ea9ee034af9790d2b0dc0893435e997bd06e587
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2019
ms.locfileid: "68655860"
---
# <a name="creating-xaml-markup-extensions"></a>Erstellen von XAML-Markuperweiterungen

[![Beispiel herunterladen](~/media/shared/download.png) Herunterladen des Beispiels](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/xaml-markupextensions)

Auf der Ebene des programmgesteuerten eine XAML-Markuperweiterung ist eine Klasse, die implementiert die [ `IMarkupExtension` ](xref:Xamarin.Forms.Xaml.IMarkupExtension) oder [ `IMarkupExtension<T>` ](xref:Xamarin.Forms.Xaml.IMarkupExtension`1) Schnittstelle. Sie können den Quellcode der standardmäßigen Markuperweiterungen im unten beschriebenen Untersuchen der [ **MarkupExtensions** Directory](https://github.com/xamarin/Xamarin.Forms/tree/master/Xamarin.Forms.Xaml/MarkupExtensions) des Xamarin.Forms-GitHub-Repositorys.

Es ist auch möglich, Ihre eigenen benutzerdefinierten XAML-Markuperweiterungen definieren, durch Ableiten von `IMarkupExtension` oder `IMarkupExtension<T>`. Verwenden Sie das generische Formular aus, wenn die Markuperweiterung einen Wert eines bestimmten Typs erhält. Dies ist der Fall mit einigen der Xamarin.Forms-Markuperweiterungen:

- `TypeExtension` leitet sich von `IMarkupExtension<Type>`
- `ArrayExtension` leitet sich von `IMarkupExtension<Array>`
- `DynamicResourceExtension` leitet sich von `IMarkupExtension<DynamicResource>`
- `BindingExtension` leitet sich von `IMarkupExtension<BindingBase>`
- `ConstraintExpression` leitet sich von `IMarkupExtension<Constraint>`

Die beiden `IMarkupExtension` Schnittstellen definieren, nur eine Methode mit dem Namen `ProvideValue`:

```csharp
public interface IMarkupExtension
{
    object ProvideValue(IServiceProvider serviceProvider);
}

public interface IMarkupExtension<out T> : IMarkupExtension
{
    new T ProvideValue(IServiceProvider serviceProvider);
}
```

Da `IMarkupExtension<T>` leitet sich von `IMarkupExtension` sowie die `new` -Schlüsselwort in `ProvideValue`, er enthält sowohl `ProvideValue` Methoden.

XAML-Markuperweiterungen definieren sehr oft Eigenschaften, die beitragen auf den Rückgabewert an. (Das gilt offensichtlich ist `NullExtension`, in dem `ProvideValue` gibt einfach auftragsantwortnachrichten zurück `null`.) Die `ProvideValue` Methode hat ein einzelnes Argument vom Typ `IServiceProvider` , wird später in diesem Artikel diskutiert werden.

## <a name="a-markup-extension-for-specifying-color"></a>Eine Markuperweiterung für Farbe angeben

Die folgende XAML-Markuperweiterung können Sie zum Erstellen einer `Color` -Wert mit den Farbton, Sättigung und Helligkeit-Komponenten. Er definiert vier Eigenschaften für die vier Komponenten der Farbe, einschließlich einer alpha-Komponente, die auf 1 initialisiert wird. Die Klasse leitet sich von `IMarkupExtension<Color>` an eine `Color` Wert zurückgeben:

```csharp
public class HslColorExtension : IMarkupExtension<Color>
{
    public double H { set; get; }

    public double S { set; get; }

    public double L { set; get; }

    public double A { set; get; } = 1.0;

    public Color ProvideValue(IServiceProvider serviceProvider)
    {
        return Color.FromHsla(H, S, L, A);
    }

    object IMarkupExtension.ProvideValue(IServiceProvider serviceProvider)
    {
        return (this as IMarkupExtension<Color>).ProvideValue(serviceProvider);
    }
}
```

Da `IMarkupExtension<T>` leitet sich von `IMarkupExtension`, muss die Klasse enthalten zwei `ProvideValue` Methoden: eine, die zurückgibt `Color` und eine andere, die zurückgibt `object`, aber die zweite Methode kann einfach die erste Methode aufrufen.

Die **HSL-Farbe Demo** Seite zeigt eine Vielzahl von Möglichkeiten, die `HslColorExtension` darf in einer XAML-Datei an die Farbe für eine `BoxView`:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:MarkupExtensions"
             x:Class="MarkupExtensions.HslColorDemoPage"
             Title="HSL Color Demo">

    <ContentPage.Resources>
        <ResourceDictionary>
            <Style TargetType="BoxView">
                <Setter Property="WidthRequest" Value="80" />
                <Setter Property="HeightRequest" Value="80" />
                <Setter Property="HorizontalOptions" Value="Center" />
                <Setter Property="VerticalOptions" Value="CenterAndExpand" />
            </Style>
        </ResourceDictionary>
    </ContentPage.Resources>

    <StackLayout>
        <BoxView>
            <BoxView.Color>
                <local:HslColorExtension H="0" S="1" L="0.5" A="1" />
            </BoxView.Color>
        </BoxView>

        <BoxView>
            <BoxView.Color>
                <local:HslColor H="0.33" S="1" L="0.5" />
            </BoxView.Color>
        </BoxView>

        <BoxView Color="{local:HslColorExtension H=0.67, S=1, L=0.5}" />

        <BoxView Color="{local:HslColor H=0, S=0, L=0.5}" />

        <BoxView Color="{local:HslColor A=0.5}" />
    </StackLayout>
</ContentPage>
```

Beachten Sie, dass bei `HslColorExtension` ist ein XML-Tag, die vier Eigenschaften werden als Attribute festgelegt, aber wenn es zwischen geschweiften Klammern angezeigt wird, werden die vier Eigenschaften durch Kommas ohne Anführungszeichen getrennt. Die Standardwerte für `H`, `S`, und `L` sind 0 und der Standardwert von `A` 1 ist, sodass diese Eigenschaften ausgelassen werden, können Wenn Sie auf Standardwerte festgelegt werden sollen. Im letzte Beispiel zeigt ein Beispiel, in denen die Helligkeit 0 (null) und führt normalerweise in Schwarz, aber der alpha-Kanal ist 0,5 und halb transparent angezeigt wird, anhand der Seite der weiße Hintergrund grauen:

[![Demo der HSL-Farbe](creating-images/hslcolordemo-small.png "HSL-Farbe Demo")](creating-images/hslcolordemo-large.png#lightbox "HSL-Farbe-Demo")

## <a name="a-markup-extension-for-accessing-bitmaps"></a>Eine Markuperweiterung für den Zugriff auf Bitmaps

Das Argument für `ProvideValue` ist ein Objekt, das implementiert die [ `IServiceProvider` ](xref:System.IServiceProvider) -Schnittstelle, die in .NET definiert ist `System` Namespace. Diese Schnittstelle verfügt über einen Member, eine Methode namens `GetService` mit einem `Type` Argument.

Die `ImageResourceExtension` Klasse, die unten zeigt eine mögliche Verwendung der `IServiceProvider` und `GetService` zum Abrufen einer `IXmlLineInfoProvider` -Objekt, das Angaben kann Zeile und das Zeichen, der angibt, auf denen ein bestimmter Fehler erkannt wurde. In diesem Fall wird eine Ausnahme ausgelöst bei der `Source` Eigenschaft nicht festgelegt wurde:

```csharp
[ContentProperty("Source")]
class ImageResourceExtension : IMarkupExtension<ImageSource>
{
    public string Source { set; get; }

    public ImageSource ProvideValue(IServiceProvider serviceProvider)
    {
        if (String.IsNullOrEmpty(Source))
        {
            IXmlLineInfoProvider lineInfoProvider = serviceProvider.GetService(typeof(IXmlLineInfoProvider)) as IXmlLineInfoProvider;
            IXmlLineInfo lineInfo = (lineInfoProvider != null) ? lineInfoProvider.XmlLineInfo : new XmlLineInfo();
            throw new XamlParseException("ImageResourceExtension requires Source property to be set", lineInfo);
        }

        string assemblyName = GetType().GetTypeInfo().Assembly.GetName().Name;
        return ImageSource.FromResource(assemblyName + "." + Source, typeof(ImageResourceExtension).GetTypeInfo().Assembly);
    }

    object IMarkupExtension.ProvideValue(IServiceProvider serviceProvider)
    {
        return (this as IMarkupExtension<ImageSource>).ProvideValue(serviceProvider);
    }
}
```

`ImageResourceExtension` ist hilfreich, wenn eine XAML-Datei auf eine Bilddatei, die als eingebettete Ressource in der .NET Standard-Bibliotheksprojekts gespeichert muss. Er verwendet den `Source` Eigenschaft zum Aufrufen der statischen `ImageSource.FromResource` Methode. Diese Methode erfordert einen vollqualifizierten Ressourcennamen, besteht der Name der Assembly, den Namen des Ordners und der Dateiname, die durch Punkte getrennt sind. Das zweite Argument für die `ImageSource.FromResource` Methode stellt der Name der Assembly und ist nur erforderlich für Releasebuilds in UWP. Unabhängig davon, `ImageSource.FromResource` muss die Assembly mit der Bitmap, was bedeutet, dass diese Erweiterung der XAML-Ressource Teil einer externen Bibliothek werden kann, es sei denn, die Images auch in dieser Bibliothek aufgerufen werden. (Finden Sie unter den [ **eingebettete Bilder** ](~/xamarin-forms/user-interface/images.md#embedded-images) Weitere Informationen zum Zugreifen auf die Bitmaps, die als eingebettete Ressourcen gespeichert.)

Obwohl `ImageResourceExtension` erfordert die `Source` festzulegende Eigenschaft, die `Source` Eigenschaft wird in einem Attribut angegeben, wie die Content-Eigenschaft der Klasse. Dies bedeutet, dass die `Source=` kann Teil des Ausdrucks in geschweiften Klammern weggelassen werden. In der **Image-Resource-Demo** Seite die `Image` Elemente abgerufen werden zwei Abbilder, die mit den Namen des Ordners und der Dateiname, die durch Punkte getrennt sind:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:MarkupExtensions"
             x:Class="MarkupExtensions.ImageResourceDemoPage"
             Title="Image Resource Demo">
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="*" />
            <RowDefinition Height="*" />
        </Grid.RowDefinitions>

        <Image Source="{local:ImageResource Images.SeatedMonkey.jpg}"
               Grid.Row="0" />

        <Image Source="{local:ImageResource Images.FacePalm.jpg}"
               Grid.Row="1" />

    </Grid>
</ContentPage>
```

Hier wird das Programm ausgeführt wird:

[![Image-Resource-Demo](creating-images/imageresourcedemo-small.png "Image-Resource-Demo")](creating-images/imageresourcedemo-large.png#lightbox "Image-Resource-Demo")

## <a name="service-providers"></a>Dienstanbieter

Mithilfe der `IServiceProvider` Argument `ProvideValue`, XAML-Markuperweiterungen können erhalten Sie Zugriff auf nützliche Informationen über die XAML-Datei, in dem sie verwendet werden können. Sondern die `IServiceProvider` Argument erfolgreich ist, müssen Sie wissen, welche Art von Diensten in bestimmten Kontexten verfügbar sind. Die beste Möglichkeit, Sie erhalten einen Überblick über diese Funktion wird durch den Quellcode von vorhandenen XAML-Markuperweiterungen in der [ **MarkupExtensions** Ordner](https://github.com/xamarin/Xamarin.Forms/tree/master/Xamarin.Forms.Xaml/MarkupExtensions) im Xamarin.Forms-Repository auf GitHub. Denken Sie daran, dass einige Arten von Diensten für Xamarin.Forms intern sind.

In einigen XAML-Markuperweiterungen kann dieser Dienst nützlich sein:

```csharp
 IProvideValueTarget provideValueTarget = serviceProvider.GetService(typeof(IProvideValueTarget)) as IProvideValueTarget;
```

Die `IProvideValueTarget` Schnittstelle definiert zwei Eigenschaften: `TargetObject` und `TargetProperty`. Diese Informationen werden beim abgerufen, der `ImageResourceExtension` -Klasse, `TargetObject` ist die `Image` und `TargetProperty` ist eine `BindableProperty` -Objekt für die `Source` Eigenschaft `Image`. Dies ist die Eigenschaft, die auf der die XAML-Markuperweiterung festgelegt wurde.

Die `GetService` Aufruf mit dem Argument `typeof(IProvideValueTarget)` tatsächlich gibt ein Objekt vom Typ `SimpleValueTargetProvider`, definiert in der `Xamarin.Forms.Xaml.Internals` Namespace. Wenn Sie die Umwandlung des Rückgabewerts von `GetService` in diesen Typ können Sie auch zugreifen eine `ParentObjects` -Eigenschaft, die ein Array ist, enthält der `Image` Element der `Grid` übergeordnetes Element und die `ImageResourceDemoPage` übergeordnet der `Grid`.

## <a name="conclusion"></a>Schlussbemerkung

XAML-Markuperweiterungen spielen eine wichtige Rolle in XAML, durch die Erweiterung der Möglichkeit, Attribute aus einer Vielzahl von Quellen festzulegen. Darüber hinaus, wenn die vorhandenen XAML-Markuperweiterungen nicht angeben, was genau Sie benötigen, können Sie auch eigene schreiben.

## <a name="related-links"></a>Verwandte Links

- [Markuperweiterungen (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/xaml-markupextensions)
- [XAML-Markup Extensions Kapitel von Xamarin.Forms-Buch](~/xamarin-forms/creating-mobile-apps-xamarin-forms/summaries/chapter10.md)
