---
title: Globale Stile inXamarin.Forms
description: Stile können global verfügbar gemacht werden, indem Sie dem Ressourcen Wörterbuch der Anwendung hinzugefügt werden. Dadurch wird das Duplizieren von Stilen über mehrere Seiten oder Steuerelemente hinweg vermieden.
ms.prod: xamarin
ms.assetid: BDC65F82-65E0-4C8E-BB91-8E340EB2D15A
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 02/17/2016
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: ae3759c1e111906b82596af80d4bdcffd5d23305
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/22/2020
ms.locfileid: "86938527"
---
# <a name="global-styles-in-xamarinforms"></a>Globale Stile inXamarin.Forms

[![Beispiel herunterladen](~/media/shared/download.png) Das Beispiel herunterladen](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-styles-basicstyles)

_Stile können global verfügbar gemacht werden, indem Sie dem Ressourcen Wörterbuch der Anwendung hinzugefügt werden. Dadurch wird das Duplizieren von Stilen über mehrere Seiten oder Steuerelemente hinweg vermieden._

## <a name="create-a-global-style-in-xaml"></a>Erstellen eines globalen Stils in XAML

Standardmäßig verwenden alle Xamarin.Forms Anwendungen, die aus einer Vorlage erstellt werden, die **App** -Klasse, um die [`Application`](xref:Xamarin.Forms.Application) Unterklasse zu implementieren. Um ein [`Style`](xref:Xamarin.Forms.Style) auf Anwendungsebene zu deklarieren, muss in der Anwendung, die [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary) XAML verwendet, die Standard- **App** -Klasse durch eine XAML- **App** -Klasse und zugehörige Code Behind ersetzt werden. Weitere Informationen finden Sie unter [Arbeiten mit der App-Klasse](~/xamarin-forms/app-fundamentals/application-class.md).

Das folgende Codebeispiel zeigt einen, [`Style`](xref:Xamarin.Forms.Style) der auf Anwendungsebene deklariert ist:

```xaml
<Application xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="Styles.App">
    <Application.Resources>
        <ResourceDictionary>
            <Style x:Key="buttonStyle" TargetType="Button">
                <Setter Property="HorizontalOptions" Value="Center" />
                <Setter Property="VerticalOptions" Value="CenterAndExpand" />
                <Setter Property="BorderColor" Value="Lime" />
                <Setter Property="BorderRadius" Value="5" />
                <Setter Property="BorderWidth" Value="5" />
                <Setter Property="WidthRequest" Value="200" />
                <Setter Property="TextColor" Value="Teal" />
            </Style>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

[`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary)Definiert einen einzelnen *expliziten* Stil, `buttonStyle` , der verwendet wird, um die Darstellung von- [`Button`](xref:Xamarin.Forms.Button) Instanzen festzulegen. Globale Stile können jedoch *explizit* oder *implizit*sein.

Das folgende Codebeispiel zeigt eine XAML `buttonStyle` -Seite, die auf die Instanzen der Seite anwendet [`Button`](xref:Xamarin.Forms.Button) :

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="Styles.ApplicationStylesPage" Title="Application" IconImageSource="xaml.png">
    <ContentPage.Content>
        <StackLayout Padding="0,20,0,0">
            <Button Text="These buttons" Style="{StaticResource buttonStyle}" />
            <Button Text="are demonstrating" Style="{StaticResource buttonStyle}" />
            <Button Text="application style overrides" Style="{StaticResource buttonStyle}" />
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```

Dies ergibt die in den folgenden Screenshots gezeigte Darstellung:

[![Beispiel für globale Stile](application-images/application-styles-1.png)](application-images/application-styles-1-large.png#lightbox "Beispiel für globale Stile")

Weitere Informationen zum Erstellen von Stilen in einer Seite [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary) finden Sie unter [explizite Stile](~/xamarin-forms/user-interface/styles/explicit.md) und [implizite Stile](~/xamarin-forms/user-interface/styles/implicit.md).

### <a name="override-styles"></a>Überschreibungs Stile

Stile niedriger in der Ansichts Hierarchie haben Vorrang vor der höheren Definition. Beispielsweise wird festgelegt, dass ein auf [`Style`](xref:Xamarin.Forms.Style) [`Button.TextColor`](xref:Xamarin.Forms.Button.TextColor) `Red` der Anwendungsebene auf festgelegt wird, indem auf Seitenebene auf festgelegt wird `Button.TextColor` `Green` . Ebenso wird ein Stil auf Seitenebene durch einen Stil auf Steuerelement Ebene überschrieben. Wenn außerdem `Button.TextColor` direkt für eine Steuerelement Eigenschaft festgelegt wird, hat dies Vorrang vor beliebigen Stilen. Diese Rangfolge wird im folgenden Codebeispiel veranschaulicht:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="Styles.ApplicationStylesPage" Title="Application" IconImageSource="xaml.png">
    <ContentPage.Resources>
        <ResourceDictionary>
            <Style x:Key="buttonStyle" TargetType="Button">
                ...
                <Setter Property="TextColor" Value="Red" />
            </Style>
        </ResourceDictionary>
    </ContentPage.Resources>
    <ContentPage.Content>
        <StackLayout Padding="0,20,0,0">
            <StackLayout.Resources>
                <ResourceDictionary>
                    <Style x:Key="buttonStyle" TargetType="Button">
                        ...
                        <Setter Property="TextColor" Value="Blue" />
                    </Style>
                </ResourceDictionary>
            </StackLayout.Resources>
            <Button Text="These buttons" Style="{StaticResource buttonStyle}" />
            <Button Text="are demonstrating" Style="{StaticResource buttonStyle}" />
            <Button Text="application style overrides" Style="{StaticResource buttonStyle}" />
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```

Der `buttonStyle` auf Anwendungsebene definierte ursprüngliche wird von der `buttonStyle` auf der Seitenebene definierten Instanz überschrieben. Außerdem wird der Stil auf Seitenebene von der Steuerelement Ebene überschrieben `buttonStyle` . Aus diesem Grund [`Button`](xref:Xamarin.Forms.Button) werden die Instanzen mit blauem Text angezeigt, wie in den folgenden Screenshots gezeigt:

[![Überschreiben von Stilen](application-images/application-styles-2.png)](application-images/application-styles-2-large.png#lightbox "Überschreiben von Stilen")

## <a name="create-a-global-style-in-c35"></a>Erstellen Sie einen globalen Stil in C-&#35;

[`Style`](xref:Xamarin.Forms.Style)der Auflistung der Anwendung in c# können-Instanzen hinzugefügt werden [`Resources`](xref:Xamarin.Forms.VisualElement.Resources) , indem ein neuer erstellt [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary) und dann der-Instanz hinzugefügt wird `Style` `ResourceDictionary` , wie im folgenden Codebeispiel gezeigt:

```csharp
public class App : Application
{
    public App ()
    {
        var buttonStyle = new Style (typeof(Button)) {
            Setters = {
                ...
                new Setter { Property = Button.TextColorProperty,    Value = Color.Teal }
            }
        };

        Resources = new ResourceDictionary ();
        Resources.Add ("buttonStyle", buttonStyle);
        ...
    }
    ...
}
```

Der-Konstruktor definiert einen einzelnen *expliziten* Stil für [`Button`](xref:Xamarin.Forms.Button) die Anwendung auf Instanzen in der gesamten Anwendung. *Explizit* [`Style`](xref:Xamarin.Forms.Style) -Instanzen werden [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary) mithilfe der-Methode hinzugefügt [`Add`](xref:Xamarin.Forms.ResourceDictionary.Add(System.String,System.Object)) , wobei eine Zeichenfolge angegeben wird, `key` die auf die `Style` Instanz verweist. Die `Style` Instanz kann dann auf alle Steuerelemente des richtigen Typs in der Anwendung angewendet werden. Globale Stile können jedoch *explizit* oder *implizit*sein.

Das folgende Codebeispiel zeigt eine c# `buttonStyle` -Seite, die auf die Instanzen der Seite anwendet [`Button`](xref:Xamarin.Forms.Button) :

```csharp
public class ApplicationStylesPageCS : ContentPage
{
    public ApplicationStylesPageCS ()
    {
        ...
        Content = new StackLayout {
            Children = {
                new Button { Text = "These buttons", Style = (Style)Application.Current.Resources ["buttonStyle"] },
                new Button { Text = "are demonstrating", Style = (Style)Application.Current.Resources ["buttonStyle"] },
                new Button { Text = "application styles", Style = (Style)Application.Current.Resources ["buttonStyle"]
                }
            }
        };
    }
}
```

`buttonStyle`Wird [`Button`](xref:Xamarin.Forms.Button) durch Festlegen der Eigenschaften auf die-Instanzen angewendet [`Style`](xref:Xamarin.Forms.NavigableElement.Style) und steuert die Darstellung der- `Button` Instanzen.

## <a name="related-links"></a>Verwandte Links

- [XAML-Markuperweiterungen](~/xamarin-forms/xaml/xaml-basics/xaml-markup-extensions.md)
- [Grundlegende Stile (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-styles-basicstyles)
- [Arbeiten mit Stilen (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/workingwithstyles)
- [ResourceDictionary](xref:Xamarin.Forms.ResourceDictionary)
- [style](xref:Xamarin.Forms.Style)
- [Trend](xref:Xamarin.Forms.Setter)
