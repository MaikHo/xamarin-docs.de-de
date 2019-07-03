---
title: Leistung von Xamarin.Forms
description: Es gibt viele Techniken zum Verbessern der Leistung von Xamarin.Forms-Anwendungen. Wenn Sie diese Kniffe kombinieren, können Sie die CPU-Auslastung und die Speichermenge, die von einer Anwendung verwendet wird, erheblich reduzieren. In diesem Artikel wird Folgendes erläutert.
ms.prod: xamarin
ms.assetid: 0be84c56-6698-448d-be5a-b4205f1caa9f
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 11/29/2017
ms.openlocfilehash: b445c1f8d3d440ecf609d5f3c1b7cc7147343fe0
ms.sourcegitcommit: a153623a69b5cb125f672df8007838afa32e9edf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67268605"
---
# <a name="xamarinforms-performance"></a>Leistung von Xamarin.Forms

_Es gibt viele Methoden zum Verbessern der Leistung von Xamarin.Forms-Anwendungen. Wenn Sie diese Kniffe kombinieren, können Sie die CPU-Auslastung und die Speichermenge, die von einer Anwendung verwendet wird, erheblich reduzieren. In diesem Artikel werden die Methoden beschrieben und erläutert._

> [!VIDEO https://youtube.com/embed/RZvdql3Ev0E]

**Weiterentwicklung 2016: Optimieren der App-Leistung mit Xamarin.Forms**

## <a name="overview"></a>Übersicht

Eine schlechte Anwendungsleistung kann sich auf unterschiedliche Weise bemerkbar machen. Die Anwendung reagiert scheinbar nicht mehr, der Bildlauf ist möglicherweise verlangsamt, und auch die Akkulaufzeit kann abnehmen. Leistungsoptimierung umfasst jedoch mehr als das bloße Implementieren eines effizienten Codes. Es muss ebenfalls berücksichtigt werden, wie der Benutzer die Leistung der Anwendung wahrnimmt. Wenn beispielsweise Vorgänge ausgeführt werden können, ohne dass der Benutzer daran gehindert wird, andere Aktivitäten auszuführen, kann dies zu einer Verbesserung der Benutzerfreundlichkeit beitragen.

Es gibt viele Techniken zum Verbessern der Leistung und der wahrnehmbaren Leistung einer Xamarin.Forms-Anwendung. Dazu zählen:

- [Aktivieren des XAML-Compilers](#xamlc)
- [Auswählen des richtigen Layouts](#correctlayout)
- [Aktivieren der Layoutkomprimierung](#layoutcompression)
- [Verwenden von schnellen Renderern](#fastrenderers)
- [Reduzieren unnötiger Bindungen](#databinding)
- [Optimieren der Layoutleistung](#optimizelayout)
- [Optimieren der ListView-Leistung](#optimizelistview)
- [Optimieren von Bildressourcen](#optimizeimages)
- [Reduzieren der Größe der visuellen Struktur](#visualtree)
- [Reduzieren der Größe des Ressourcenverzeichnisses der Anwendung](#resourcedictionary)
- [Verwenden des benutzerdefinierten Renderer-Musters](#rendererpattern)

> [!NOTE]
>  Bevor Sie diesen Artikel lesen, sollten Sie zuerst den Artikel [Cross-Platform Performance (Plattformübergreifende Leistung)](~/cross-platform/deploy-test/memory-perf-best-practices.md) lesen, der nicht-plattformspezifische Methoden zur Verbesserung der Arbeitsspeicherauslastung und Leistung von Anwendungen beschreibt, die mit der Xamarin-Plattform erstellt wurden.

<a name="xamlc" />

## <a name="enable-the-xaml-compiler"></a>Aktivieren des XAML-Compilers

XAML kann optional auch direkt mit dem XAML-Compiler (XAMLC) in der Zwischensprache (Intermediate Language, IL) kompiliert werden. XAMLC bietet eine Reihe von Vorteilen:

- Er führt eine XAML-Überprüfung zur Kompilierzeit durch und benachrichtigt den Benutzer über eventuelle Fehler.
- Er entfernt etwas Lade- und Instanziierungszeit für XAML-Elemente.
- Er hilft bei der Verringerung der Dateigröße der finalen Assembly, indem XAML-Dateien nicht mehr eingeschlossen werden.

XAMLC ist standardmäßig deaktiviert, damit die Abwärtskompatibilität sichergestellt ist. Er kann jedoch sowohl auf der Assemblyebene als auch auf der Klassenebene aktiviert werden. Weitere Informationen finden Sie unter [Compiling XAML](~/xamarin-forms/xaml/xamlc.md) (Kompilieren von XAML).

<a name="correctlayout" />

## <a name="choose-the-correct-layout"></a>Auswählen des richtigen Layouts

Ein Layout, in dem mehrere untergeordnete Elemente angezeigt werden können, das jedoch nur über ein untergeordnetes Element verfügt, ist Vergeudung. Im folgenden Codebeispiel wird ein [`StackLayout`](xref:Xamarin.Forms.StackLayout) mit einem untergeordneten Element dargestellt:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="DisplayImage.HomePage">
    <ContentPage.Content>
        <StackLayout>
            <Image Source="waterfront.jpg" />
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```

Dies ist Vergeudung, und das [`StackLayout`](xref:Xamarin.Forms.StackLayout)-Element sollte wie im folgenden Codebeispiel gezeigt entfernt werden:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="DisplayImage.HomePage">
    <ContentPage.Content>
        <Image Source="waterfront.jpg" />
    </ContentPage.Content>
</ContentPage>
```

Darüber hinaus sollten Sie nicht versuchen, die Darstellung eines bestimmten Layouts durch Kombinieren anderer Layouts zu reproduzieren. Dies führt dazu, dass unnötige Layoutberechnungen durchgeführt werden. Versuchen Sie beispielsweise nicht, ein [`Grid`](xref:Xamarin.Forms.Grid)-Layout durch eine Kombination aus [`StackLayout`](xref:Xamarin.Forms.StackLayout)-Instanzen zu reproduzieren. Das folgende Codebeispiel veranschaulicht dieses Fehlverhalten beispielhaft:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Details.HomePage"
             Padding="0,20,0,0">
    <ContentPage.Content>
        <StackLayout>
            <StackLayout Orientation="Horizontal">
                <Label Text="Name:" />
                <Entry Placeholder="Enter your name" />
            </StackLayout>
            <StackLayout Orientation="Horizontal">
                <Label Text="Age:" />
                <Entry Placeholder="Enter your age" />
            </StackLayout>
            <StackLayout Orientation="Horizontal">
                <Label Text="Occupation:" />
                <Entry Placeholder="Enter your occupation" />
            </StackLayout>
            <StackLayout Orientation="Horizontal">
                <Label Text="Address:" />
                <Entry Placeholder="Enter your address" />
            </StackLayout>
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```

Dies ist Vergeudung, da unnötige Layoutberechnungen durchgeführt werden. Stattdessen kann das gewünschte Layout besser wie im folgenden Codebeispiel gezeigt über ein [`Grid`](xref:Xamarin.Forms.Grid) erreicht werden:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Details.HomePage"
             Padding="0,20,0,0">
    <ContentPage.Content>
        <Grid>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="100" />
                <ColumnDefinition Width="*" />
            </Grid.ColumnDefinitions>
            <Grid.RowDefinitions>
                <RowDefinition Height="30" />
                <RowDefinition Height="30" />
                <RowDefinition Height="30" />
                <RowDefinition Height="30" />
            </Grid.RowDefinitions>
            <Label Text="Name:" />
            <Entry Grid.Column="1" Placeholder="Enter your name" />
            <Label Grid.Row="1" Text="Age:" />
            <Entry Grid.Row="1" Grid.Column="1" Placeholder="Enter your age" />
            <Label Grid.Row="2" Text="Occupation:" />
            <Entry Grid.Row="2" Grid.Column="1" Placeholder="Enter your occupation" />
            <Label Grid.Row="3" Text="Address:" />
            <Entry Grid.Row="3" Grid.Column="1" Placeholder="Enter your address" />
        </Grid>
    </ContentPage.Content>
</ContentPage>
```

<a name="layoutcompression" />

## <a name="enable-layout-compression"></a>Aktivieren der Layoutkomprimierung

Durch die Layoutkomprimierung werden bestimmte Layouts aus der visuellen Struktur entfernt, um die Leistung des Seitenrenderings zu verbessern. Der daraus resultierende Leistungsvorteil variiert je nach Komplexität einer Seite, der Version des verwendeten Betriebssystems und des Geräts, auf dem die Anwendung ausgeführt wird. Die größten Leistungssteigerungen werden jedoch bei älteren Geräten zu verzeichnen sein. Weitere Informationen finden Sie unter [Layoutkomprimierung](~/xamarin-forms/user-interface/layouts/layout-compression.md).

<a name="fastrenderers" />

## <a name="use-fast-renderers"></a>Verwenden von schnellen Renderern

Schnelle Renderer reduzieren die Inflations- und Renderingkosten von Xamarin.Forms-Steuerelementen in Android, indem sie die resultierende native Steuerelementhierarchie vereinfachen. Durch die Senkung der Anzahl der erstellten Objekte wird die Leistung weiter verbessert, was wiederum die Komplexität der visuellen Struktur und die Speicherbelegung verringert. Weitere Informationen finden Sie unter [Schnelle Renderer](~/xamarin-forms/internals/fast-renderers.md).

<a name="databinding" />

## <a name="reduce-unnecessary-bindings"></a>Reduzieren unnötiger Bindungen

Verwenden Sie keine Bindungen für Inhalte, die problemlos statisch festgelegt werden können. Das Binden von Daten, die nicht gebunden werden müssen, bringt keine Vorteile mit sich, da Bindungen nicht kostengünstig sind. Das Festlegen von `Button.Text = "Accept"` ist beispielsweise mit weniger Aufwand verbunden als das Binden von [`Button.Text`](xref:Xamarin.Forms.Button.Text) an die Eigenschaft `string` mit dem Wert „Akzeptieren“.

<a name="optimizelayout" />

## <a name="optimize-layout-performance"></a>Optimieren der Layoutleistung

Xamarin.Forms 2 hat eine optimierte Layout-Engine eingeführt, die sich auf Layoutupdates auswirkt. Befolgen Sie die nachstehenden Richtlinien, um die bestmögliche Layoutleistung zu erreichen:

- Verringern Sie die Tiefe der Layouthierarchien durch die Angabe von [`Margin`](xref:Xamarin.Forms.View.Margin)-Eigenschaftswerten. Diese ermöglichen die Erstellung von Layouts mit weniger Umbrüchen in Ansichten. Weitere Informationen finden Sie unter [Seitenränder und Textabstand](~/xamarin-forms/user-interface/layouts/margin-and-padding.md).
- Versuchen Sie bei der Verwendung eines [`Grid`](xref:Xamarin.Forms.Grid), sicherzustellen, dass so wenige Zeilen und Spalten wie möglich auf die Größe [`Auto`](xref:Xamarin.Forms.GridLength.Auto) festgelegt werden. Durch jede Zeile oder Spalte, deren Größe automatisch angepasst wird, wird verursacht, dass die Layout-Engine zusätzliche Layoutberechnungen durchführt. Verwenden Sie stattdessen wenn möglich Zeilen und Spalten mit festen Größen. Alternativ können Sie mit dem [`GridUnitType.Star`](xref:Xamarin.Forms.GridUnitType.Star)-Enumerationswert Zeilen und Spalten festlegen, die einen proportionalen Speicherplatz belegen sollen. Voraussetzung hierfür ist, dass die übergeordnete Struktur diese Layoutrichtlinien einhält.
- Legen Sie die Eigenschaften [`VerticalOptions`](xref:Xamarin.Forms.View.VerticalOptions) und [`HorizontalOptions`](xref:Xamarin.Forms.View.VerticalOptions) eines Layouts nur dann fest, wenn dies erforderlich ist. Die Standardwerte von [`LayoutOptions.Fill`](xref:Xamarin.Forms.LayoutOptions.Fill) und [`LayoutOptions.FillAndExpand`](xref:Xamarin.Forms.LayoutOptions.FillAndExpand) ermöglichen die beste Layoutoptimierung. Das Ändern dieser Eigenschaften ist mit Kosten und Speicherplatzbelegung verbunden, selbst dann, wenn sie auf die Standardwerte festgelegt werden.
- Vermeiden Sie möglichst die Verwendung eines [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout). Dies führt dazu, dass die CPU erheblich mehr Arbeit übernehmen muss.
- Vermeiden Sie bei Verwendung eines [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) möglichst die Verwendung der Eigenschaft [`AbsoluteLayout.AutoSize`](xref:Xamarin.Forms.AbsoluteLayout.AutoSize).
- Stellen Sie bei Verwendung eines [`StackLayout`](xref:Xamarin.Forms.StackLayout) sicher, dass für [`LayoutOptions.Expands`](xref:Xamarin.Forms.LayoutOptions.Expands) nur ein untergeordnetes Element festgelegt ist. Mit dieser Eigenschaft wird sichergestellt, dass das angegebene untergeordnete Element den größten Bereich belegt, der im `StackLayout` verfügbar ist. Zudem ist es Vergeudung, diese Berechnungen mehrmals durchzuführen.
- Rufen Sie keine Methode der [`Layout`](xref:Xamarin.Forms.Layout)-Klasse auf, da dies zur Durchführung teurer Layoutberechnungen führt. Die Wahrscheinlichkeit ist groß, dass das gewünschte Layoutverhalten stattdessen durch Festlegen der Eigenschaften [`TranslationX`](xref:Xamarin.Forms.VisualElement.TranslationX) und [`TranslationY`](xref:Xamarin.Forms.VisualElement.TranslationY) abgerufen werden kann. Alternativ können Sie Unterklassen für die [`Layout<View>`](xref:Xamarin.Forms.Layout`1)-Klasse erstellen, um das gewünschte Layoutverhalten zu erzielen.
- Aktualisieren Sie [`Label`](xref:Xamarin.Forms.Label)-Instanzen nicht häufiger als erforderlich. Die Änderung der Bezeichnungsgröße kann dazu führen, dass das gesamte Bildschirmlayout neu berechnet wird.
- Legen Sie die Eigenschaft [`Label.VerticalTextAlignment`](xref:Xamarin.Forms.Label.VerticalTextAlignment) nur dann fest, wenn dies erforderlich ist.
- Legen Sie den [`LineBreakMode`](xref:Xamarin.Forms.Label.LineBreakMode) aller [`Label`](xref:Xamarin.Forms.Label)-Instanzen möglichst auf [`NoWrap`](xref:Xamarin.Forms.LineBreakMode.NoWrap) fest.

<a name="optimizelistview" />

## <a name="optimize-listview-performance"></a>Optimieren der ListView-Leistung

Bei Verwendung eines [`ListView`](xref:Xamarin.Forms.ListView)-Steuerelements müssen einige Benutzeroberflächen optimiert werden:

- **Initialisierung**: Das Zeitintervall beginnt mit der Erstellung des Steuerelements und endet, wenn die Elemente auf dem Bildschirm angezeigt werden.
- **Bildlauf**: Die Möglichkeit, einen Bildlauf durch die Liste durchzuführen, und die Sicherstellung, dass die Benutzeroberfläche nicht hinter Fingerbewegungen zurückbleibt.
- **Interaktion** für das Hinzufügen, Löschen und Auswählen von Elementen.

Für das [`ListView`](xref:Xamarin.Forms.ListView)-Steuerelement ist eine Anwendung erforderlich, mit der Daten- und Zellenvorlagen bereitgestellt werden können. Wie dies erreicht wird, hat großen Einfluss auf die Leistung des Steuerelements. Weitere Informationen finden Sie unter [ListView Performance](~/xamarin-forms/user-interface/listview/performance.md) (ListView-Leistung).

<a name="optimizeimages" />

## <a name="optimize-image-resources"></a>Optimieren von Bildressourcen

Das Anzeigen von Bildressourcen kann den Speicherbedarf der App erheblich erhöhen. Sie sollten daher nur erstellt werden, wenn dies erforderlich ist. Und sie sollten freigegeben werden, sobald die Anwendung sie nicht mehr benötigt. Wenn beispielsweise eine Anwendung ein Bild anzeigt, indem sie die zugehörigen Daten aus einem Datenstrom liest, müssen Sie sicherstellen, dass dieser Datenstrom nur erstellt wird, wenn dies erforderlich ist, und dass er freigegeben wird, sobald er nicht mehr benötigt wird. Dies kann erreicht werden, indem der Datenstrom bei Erstellung der Seite erstellt wird, oder bei Auslösung des [`Page.Appearing`](xref:Xamarin.Forms.Page.Appearing)-Ereignisses, und der Datenstrom anschließend bei Auslösung des [`Page.Disappearing`](xref:Xamarin.Forms.Page.Disappearing)-Ereignisses verworfen wird.

Wenn Sie ein Bild für die Anzeige mit der [`ImageSource.FromUri`](xref:Xamarin.Forms.ImageSource.FromUri(System.Uri))-Methode herunterladen, müssen Sie das heruntergeladene Bild zwischenspeichern, indem Sie sicherstellen, dass die Eigenschaft [`UriImageSource.CachingEnabled`](xref:Xamarin.Forms.UriImageSource.CachingEnabled) auf `true` festgelegt ist. Weitere Informationen finden Sie unter [Arbeiten mit Bildern](~/xamarin-forms/user-interface/images.md).

Weitere Informationen finden Sie unter [Optimieren von Bildressourcen](~/cross-platform/deploy-test/memory-perf-best-practices.md#optimizeimages).

<a name="visualtree" />

## <a name="reduce-the-visual-tree-size"></a>Reduzieren der Größe der visuellen Struktur

Durch eine Reduzierung der Anzahl von Elementen auf einer Seite wird der Seitenrenderer schneller. Es gibt zwei Haupttechniken, um dies zu erreichen. Bei der ersten Technik werden Elemente ausgeblendet, die nicht sichtbar sind. Die Eigenschaft [`IsVisible`](xref:Xamarin.Forms.VisualElement.IsVisible) der einzelnen Elemente bestimmt, ob die Elemente Teil der visuellen Struktur sein sollten. Daher sollten Sie das Element entfernen oder die zugehörige Eigenschaft `IsVisible` auf `false` festlegen, wenn ein Element nicht sichtbar ist, da es ausgeblendet wird.

Bei der zweiten Technik werden unnötige Elemente entfernt. Im folgenden Codebeispiel wird ein Seitenlayout dargestellt, in dem eine Reihe von [`Label`](xref:Xamarin.Forms.Label)-Elementen angezeigt wird:

```xaml
<ContentPage.Content>
    <StackLayout>
        <StackLayout Padding="20,20,0,0">
            <Label Text="Hello" />
        </StackLayout>
        <StackLayout Padding="20,20,0,0">
            <Label Text="Welcome to the App!" />
        </StackLayout>
        <StackLayout Padding="20,20,0,0">
            <Label Text="Downloading Data..." />
        </StackLayout>
    </StackLayout>
</ContentPage.Content>
```

Dasselbe Seitenlayout kann wie im folgenden Codebeispiel gezeigt mit einer reduzierten Elementanzahl verwaltet werden:

```xaml
<ContentPage.Content>
  <StackLayout Padding="20,20,0,0" Spacing="25">
    <Label Text="Hello" />
    <Label Text="Welcome to the App!" />
    <Label Text="Downloading Data..." />
  </StackLayout>
</ContentPage.Content>
```

<a name="resourcedictionary" />

## <a name="reduce-the-application-resource-dictionary-size"></a>Reduzieren der Größe des Ressourcenverzeichnisses der Anwendung

Alle Ressourcen, die in der gesamten Anwendung verwendet werden, sollten im Ressourcenverzeichnis der Anwendung gespeichert werden, damit eine Duplizierung verhindert wird. Dadurch kann der Umfang des XAML-Codes reduziert werden, der in der gesamten Anwendung analysiert werden muss. Das folgende Codebeispiel zeigt die `HeadingLabelStyle`-Ressource, die in der gesamten Anwendung verwendet wird und daher im Ressourcenverzeichnis der Anwendung definiert ist:

```xaml
<Application xmlns="http://xamarin.com/schemas/2014/forms"
                xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Resources.App">
     <Application.Resources>
         <ResourceDictionary>
            <Style x:Key="HeadingLabelStyle" TargetType="Label">
                <Setter Property="HorizontalOptions" Value="Center" />
                <Setter Property="FontSize" Value="Large" />
                <Setter Property="TextColor" Value="Red" />
            </Style>
         </ResourceDictionary>
     </Application.Resources>
</Application>
```

XAML-Code, der für eine Seite spezifisch ist, sollte jedoch nicht im Ressourcenverzeichnis der App enthalten sein, da die Ressourcen dann beim Starten der Anwendung analysiert werden und nicht, wenn dies auf einer Seite erforderlich ist. Wenn eine Ressource von einer anderen Seite als der Startseite verwendet wird, sollte sie in das Ressourcenverzeichnis dieser Seite aufgenommen werden und folglich dabei helfen, den XAML-Code zu reduzieren, der beim Starten der Anwendung analysiert wird. Das folgende Codebeispiel zeigt die `HeadingLabelStyle`-Ressource, die sich nur auf einer einzelnen Seite befindet und daher im Ressourcenverzeichnis der Seite definiert ist:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Test.HomePage"
             Padding="0,20,0,0">
     <ContentPage.Resources>
          <ResourceDictionary>
            <Style x:Key="HeadingLabelStyle" TargetType="Label">
                <Setter Property="HorizontalOptions" Value="Center" />
                <Setter Property="FontSize" Value="Large" />
                <Setter Property="TextColor" Value="Red" />
            </Style>
        </ResourceDictionary>
     </ContentPage.Resources>
    <ContentPage.Content>
      ...
    </ContentPage.Content>
</ContentPage>

```

Weitere Informationen zu Anwendungsressourcen finden Sie unter [`Working with Styles`](~/xamarin-forms/user-interface/styles/index.md).

<a name="rendererpattern" />

## <a name="use-the-custom-renderer-pattern"></a>Verwenden des benutzerdefinierten Renderer-Musters

Die meisten Rendererklassen machen die `OnElementChanged`-Methode verfügbar, die bei der Erstellung eines benutzerdefinierten Xamarin.Forms-Steuerelements aufgerufen wird, um das entsprechende native Steuerelement zu rendern. Passen Sie Rendererklassen in den einzelnen plattformspezifischen Rendererklassen an, und setzen Sie diese Methode anschließend außer Kraft, um das native Steuerelement zu instanziieren und anzupassen. Mit der `SetNativeControl`-Methode wird das native Steuerelement instanziiert und die Steuerelementreferenz der Eigenschaft `Control` zugewiesen.

In einigen Fällen kann die `OnElementChanged`-Methode mehrmals aufgerufen werden. Daher müssen Sie bei der Instanziierung eines nativen Steuerelements sorgfältig vorgehen, um Arbeitsspeicherverluste zu vermeiden, die Auswirkungen auf die Leistung haben können. Im folgenden Codebeispiel ist der Ansatz zu sehen, der beim Instanziieren eines neuen nativen Steuerelements in einem benutzerdefinierten Renderer verwendet werden soll:

```csharp
protected override void OnElementChanged (ElementChangedEventArgs<NativeListView> e)
{
  base.OnElementChanged (e);

  if (e.OldElement != null) {
    // Unsubscribe from event handlers and cleanup any resources
  }

  if (e.NewElement != null) {
    if (Control == null) {
      // Instantiate the native control
    }
    // Configure the control and subscribe to event handlers
  }
}
```

Ein neues natives Steuerelement sollte nur einmal instanziiert werden, wenn der Wert der Eigenschaft `Control` `null` lautet. Ein Steuerelement sollte außerdem nur dann erstellt, konfiguriert und vom Ereignishandler abonniert werden, wenn der benutzerdefinierte Renderer an ein neues Xamarin.Forms-Element angefügt wird. Gleichermaßen sollte das Abonnement für Ereignishandler nur dann gekündigt werden, wenn sich das Element ändert, an das der Renderer angefügt wurde. Mit diesem Ansatz kann ein gut funktionierender benutzerdefinierter Renderer erstellt werden, der nicht durch Speicherverluste beeinträchtigt wird.

> [!IMPORTANT]
> Die `SetNativeControl`-Methode sollte nur aufgerufen werden, wenn `e.NewElement` nicht `null` ist.

Weitere Informationen zu benutzerdefinierten Renderern finden Sie unter [Customizing Controls on Each Platform (Anpassen von Steuerelementen auf den einzelnen Plattformen)](~/xamarin-forms/app-fundamentals/custom-renderer/index.md).

## <a name="summary"></a>Zusammenfassung

In diesem Artikel wurden Techniken zum Verbessern der Leistung von Xamarin.Forms-Anwendungen beschrieben und erläutert. Wenn Sie diese Kniffe kombinieren, können Sie die CPU-Auslastung und die Speichermenge, die von einer Anwendung verwendet wird, erheblich reduzieren.


## <a name="related-links"></a>Verwandte Links

- [Plattformübergreifende Leistung](~/cross-platform/deploy-test/memory-perf-best-practices.md)
- [ListView-Leistung](~/xamarin-forms/user-interface/listview/performance.md)
- [Schnelle Renderer](~/xamarin-forms/internals/fast-renderers.md)
- [Layoutkomprimierung](~/xamarin-forms/user-interface/layouts/layout-compression.md)
- [XamlCompilation](xref:Xamarin.Forms.Xaml.XamlCompilationAttribute)
- [XamlCompilationOptions](xref:Xamarin.Forms.Xaml.XamlCompilationOptions)
