---
title: Hinzufügen von Drag & Drop-Gestenerkennung
description: In diesem Artikel wird erläutert, wie Drag & Drop-Gesten mit Xamarin.Forms erkannt werden.
ms.prod: xamarin
ms.assetid: 4CB2F270-908A-4A89-B852-70BC04066E8C
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/04/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 2d929043a6b4cd5dd8b06318df0d7a347708fe6c
ms.sourcegitcommit: c3329ab25d377907d8804cdd5e26dc84a274f39c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88130915"
---
# <a name="add-drag-and-drop-gesture-recognizers"></a>Hinzufügen von Drag & Drop-Gestenerkennung

![Vorabrelease der API](~/media/shared/preview.png)

[![Beispiel herunterladen](~/media/shared/download.png) Herunterladen des Beispiels](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/workingwithgestures-draganddropgesture/)

Mithilfe einer Drag & Drop-Geste können Elemente und die zugehörigen Datenpakete mit einer kontinuierlichen Geste von einer Bildschirmposition an eine andere gezogen werden. Drag & Drop kann in einer einzelnen Anwendung stattfinden, oder in einer Anwendung beginnen und in einer anderen Anwendung enden.

> [!IMPORTANT]
> Die Drag & Drop-Gestenerkennung von Xamarin.Forms ist zurzeit experimentell und kann nur verwendet werden, wenn das `DragAndDrop_Experimental`-Flag festgelegt wird. Weitere Informationen finden Sie unter [Experimentelle Flags](~/xamarin-forms/internals/experimental-flags.md).
>
> Das Erkennen von Drag & Drop-Gesten wird unter iOS, Android und der universellen Windows-Plattform (UWP) unterstützt. Unter iOS ist jedoch mindestens iOS 11 erforderlich.

Die *Ziehquelle*, das Element, auf dem die Ziehgeste initiiert wird, kann Daten bereitstellen, die durch Auffüllen eines Datenpaketobjekts übertragen werden. Wenn die Ziehquelle losgelassen wird, findet das Ablegen statt. Das *Ablageziel*, das Element unter der Ziehquelle, verarbeitet dann das Datenpaket.

Der Vorgang zum Aktivieren von Drag & Drop in einer Anwendung läuft wie folgt ab:

1. Aktivieren Sie Ziehen für ein Element, indem Sie dessen `GestureRecognizers`-Sammlung ein `DragGestureRecognizer`-Objekt hinzufügen und die Eigenschaft `DragGestureRecognizer.CanDrag` auf `true` festlegen. Weitere Informationen finden Sie unter [Aktivieren des Ziehens](#enable-drag).
1. [optional] Erstellen Sie ein Datenpaket. Xamarin.Forms füllt das Datenpaket für Bild- und Textsteuerelemente automatisch auf, aber für andere Inhalte müssen Sie ein eigenes Datenpaket erstellen. Weitere Informationen finden Sie unter [Erstellen eines Datenpakets](#build-a-data-package).
1. Aktivieren Sie Ablegen für ein Element, indem Sie dessen `GestureRecognizers`-Sammlung ein `DropGestureRecognizer`-Objekt hinzufügen und die Eigenschaft `DropGestureRecognizer.AllowDrop` auf `true` festlegen. Weitere Informationen finden Sie unter [Aktivieren des Ablegens](#enable-drop).
1. [optional] Verarbeiten Sie das `DropGestureRecognizer.DragOver`-Ereignis, um den Vorgangstyp anzugeben, den das Ablageziel zulässt. Weitere Informationen finden Sie unter [Verarbeiten des DragOver-Ereignisses](#handle-the-dragover-event).
1. [optional] Verarbeiten Sie das Datenpaket, um den gelöschten Inhalt zu empfangen. Xamarin.Forms ruft automatisch Bild- und Textdaten aus dem Datenpaket ab, aber für andere Inhalte müssen Sie das Datenpaket verarbeiten. Weitere Informationen finden Sie unter [Verarbeiten des Datenpakets](#process-the-data-package).

> [!NOTE]
> Das Ziehen von Elementen in eine und aus einer [`CollectionView`](xref:Xamarin.Forms.CollectionView) wird derzeit nicht unterstützt.

## <a name="enable-drag"></a>Aktivieren des Ziehens

In Xamarin.Forms sorgt die `DragGestureRecognizer`-Klasse für die Erkennung der Ziehgeste. Diese Klasse definiert die folgenden Eigenschaften:

- `CanDrag` vom Typ `bool` gibt an, ob das Element, dem die Gestenerkennung angefügt ist, eine Ziehquelle sein kann. Der Standardwert dieser Eigenschaft ist `false`.
- `DragStartingCommand` vom Typ `ICommand`, der ausgeführt wird, sobald eine Ziehgeste erkannt wird.
- `DragStartingCommandParameter` vom Typ `object`: der Parameter, der an `DragStartingCommand` übergeben wird.
- `DropCompletedCommmand` vom Typ `ICommand`, der ausgeführt wird, sobald die Ziehquelle abgelegt wird.
- `DropCompletedCommandParameter` vom Typ `object`: der Parameter, der an `DropCompletedCommand` übergeben wird.

Diese Eigenschaften werden durch [`BindableProperty`](xref:Xamarin.Forms.BindableProperty)-Objekte gestützt, was bedeutet, dass sie Ziele von Datenbindungen sein können, und geformt.

Die `DragGestureRecognizer`-Klasse definiert auch `DragStarting`- und `DropCompleted`-Ereignisse. Wenn ein `DragGestureRecognizer`-Objekt eine Ziehgeste erkennt, führt es den `DragStartingCommand` aus und ruft das `DragStarting`-Ereignis auf. Wenn dann das `DragGestureRecognizer`-Objekt die Ausführung einer Ablegegeste erkennt, führt es den `DropCompletedCommand` aus und ruft das `DropCompleted`-Ereignis auf.

Das `DragStartingEventArgs`-Objekt, das das `DragStarting`-Ereignis begleitet, definiert folgende Eigenschaften:

- `Handled` vom Typ `bool` gibt an, ob der Ereignishandler das Ereignis verarbeitet hat oder ob Xamarin.Forms seine eigene Verarbeitung fortsetzen sollte.
- `Cancel` vom Typ `bool` gibt an, ob das Ereignis abgebrochen werden sollte.
- `Data` vom Typ `DataPackage` gibt das Datenpaket an, das die Ziehquelle begleitet. Dies ist eine schreibgeschützte Eigenschaft.

Das `DropCompletedEventArgs`-Objekt, das das `DropCompleted`-Ereignis begleitet, verfügt über eine schreibgeschützte `DropResult`-Eigenschaft vom Typ `DataPackageOperation`. Weitere Informationen zur `DataPackageOperation`-Enumeration finden Sie unter [Verarbeiten des DragOver-Ereignisses](#handle-the-dragover-event).

Das folgende XAML-Beispiel zeigt einen `DragGestureRecognizer`, der einem [`Image`](xref:Xamarin.Forms.Image) angefügt ist:

```xaml
<Image Source="monkeyface.png">
    <Image.GestureRecognizers>
        <DragGestureRecognizer CanDrag="True" />
    </Image.GestureRecognizers>
</Image>
```

In diesem Beispiel kann eine Ziehgeste auf dem [`Image`](xref:Xamarin.Forms.Image) initiiert werden.

> [!TIP]
> Unter iOS, Android und UWP wird eine Ziehgeste mit einem langen Drücken gefolgt von einem Ziehen initiiert.

## <a name="build-a-data-package"></a>Erstellen eines Datenpakets

Xamarin.Forms erstellt beim Initiieren eines Ziehvorgang für die folgenden Steuerelemente automatisch ein Datenpaket für Sie:

- Textsteuerelemente. Textwerte können aus [`CheckBox`](xref:Xamarin.Forms.CheckBox)-, [`DatePicker`](xref:Xamarin.Forms.DatePicker)-, [`Editor`](xref:Xamarin.Forms.Editor)-, [`Entry`](xref:Xamarin.Forms.Entry)-, [`Label`](xref:Xamarin.Forms.Label)-, [`RadioButton`](xref:Xamarin.Forms.RadioButton)-, [`Switch`](xref:Xamarin.Forms.Switch)- und [`TimePicker`](xref:Xamarin.Forms.TimePicker)-Objekten gezogen werden.
- Bildsteuerelemente. Bilder können aus [`Button`](xref:Xamarin.Forms.Button)-, [`Image`](xref:Xamarin.Forms.Image)- und [`ImageButton`](xref:Xamarin.Forms.ImageButton)-Steuerelementen gezogen werden.

In der folgenden Tabelle sind die Eigenschaften aufgeführt, die beim Initiieren eines Ziehens für ein Textsteuerelement gelesen, und alle Konvertierungen, die versucht werden:

| Control | Eigenschaft | Konvertierung |
| --- | --- | --- |
| `CheckBox` | `IsChecked` | `bool`, konvertiert in einen `string`. |
| `DatePicker` | `Date` | `DateTime`, konvertiert in einen `string`. |
| `Editor` | `Text` ||
| `Entry` | `Text` ||
| `Label` | `Text` ||
| `RadioButton` | `IsChecked` | `bool`, konvertiert in einen `string`. |
| `Switch` | `IsToggled` | `bool`, konvertiert in einen `string`. |
| `TimePicker` | `Time` | `TimeSpan`, konvertiert in einen `string`. |

Für andere Inhalte als Text und Bilder müssen Sie selbst ein Datenpaket erstellen.

Datenpakete werden von der `DataPackage`-Klasse dargestellt, die die folgenden Eigenschaften definiert:

- `Properties` vom Typ `DataPackagePropertySet`, eine Sammlung von Eigenschaften, die die im `DataPackage` enthaltenen Daten umfassen. Diese Eigenschaft ist schreibgeschützt.
- `Image` vom Typ [`ImageSource`](xref:Xamarin.Forms.ImageSource), das im `DataPackage` enthaltene Bild.
- `Text` vom Typ `string`, der im `DataPackage` enthaltene Text.
- `View` vom Typ `DataPackageView`, eine schreibgeschützte Version des `DataPackage`.

Die `DataPackagePropertySet`-Klasse stellt eine als `Dictionary<string,object>` gespeicherte Eigenschaftensammlung dar. Weitere Informationen zur `DataPackageView`-Klasse finden Sie unter [Verarbeiten des Datenpakets](#process-the-data-package).

### <a name="store-image-or-text-data"></a>Speichern von Bild- oder Textdaten

Bild- oder Textdaten können mit einer Ziehquelle verknüpft werden, indem die Daten in der `DataPackage.Image`- oder `DataPackage.Text`-Eigenschaft gespeichert werden. Dies kann im Handler für das `DragStarting`-Ereignis durchgeführt werden.

Das folgende XAML-Beispiel zeigt einen `DragGestureRecognizer`, der einen Handler für das `DragStarting`-Ereignis registriert:

```xaml
<Path Stroke="Black"
      StrokeThickness="4">
    <Path.GestureRecognizers>
        <DragGestureRecognizer CanDrag="True"
                               DragStarting="OnDragStarting" />
    </Path.GestureRecognizers>
    <Path.Data>
        <!-- PathGeometry goes here -->
    </Path.Data>
</Path>
```

In diesem Beispiel wird der `DragGestureRecognizer` einem `Path`-Objekt angefügt. Das `DragStarting`-Ereignis wird ausgelöst, wenn eine Ziehgeste im `Path` erkannt wird, wodurch der `OnDragStarting`-Ereignishandler ausgeführt wird:

```csharp
void OnDragStarting(object sender, DragStartingEventArgs e)
{
    e.Data.Text = "My text data goes here";
}
```

Das `DragStartingEventArgs`-Objekt, das das `DragStarting`-Ereignis begleitet, hat eine `Data`-Eigenschaft vom Typ `DataPackage`. In diesem Beispiel wird die `Text`-Eigenschaft des `DataPackage`-Objekts auf einen `string` festgelegt. Auf das `DataPackage` kann dann beim Ablegen zugegriffen werden, um den `string` abzurufen.

### <a name="store-data-in-the-property-bag"></a>Speichern von Daten in der Eigenschaftensammlung

Alle Daten einschließlich Bilder und Text können mit einer Ziehquelle verknüpft werden, indem die Daten in der `DataPackage.Properties`-Sammlung gespeichert werden. Dies kann im Handler für das `DragStarting`-Ereignis durchgeführt werden.

Das folgende XAML-Beispiel zeigt einen `DragGestureRecognizer`, der einen Handler für das `DragStarting`-Ereignis registriert:

```xaml
<Rectangle Stroke="Red"
           Fill="DarkBlue"
           StrokeThickness="4"
           HeightRequest="200"
           WidthRequest="200">
    <Rectangle.GestureRecognizers>
        <DragGestureRecognizer CanDrag="True"
                               DragStarting="OnDragStarting" />
    </Rectangle.GestureRecognizers>
</Rectangle>
```

In diesem Beispiel wird der `DragGestureRecognizer` einem `Rectangle`-Objekt angefügt. Das `DragStarting`-Ereignis wird ausgelöst, wenn eine Ziehgeste im `Rectangle` erkannt wird, wodurch der `OnDragStarting`-Ereignishandler ausgeführt wird:

```csharp
void OnDragStarting(object sender, DragStartingEventArgs e)
{
    Shape shape = (sender as Element).Parent as Shape;
    e.Data.Properties.Add("Square", new Square(shape.Width, shape.Height));
}
```

Das `DragStartingEventArgs`-Objekt, das das `DragStarting`-Ereignis begleitet, hat eine `Data`-Eigenschaft vom Typ `DataPackage`. Die `Properties`-Sammlung des `DataPackage`-Objekts, eine `Dictionary<string, object>`-Sammlung, kann so geändert werden, dass alle erforderlichen Daten gespeichert werden. In diesem Beispiel wird das `Properties`-Wörterbuch so geändert, dass ein `Square`-Objekt, das die Größe des `Rectangle` darstellt, mit einem „Square“-Schlüssel gespeichert wird.

## <a name="enable-drop"></a>Aktivieren des Ablegens

In Xamarin.Forms sorgt die `DropGestureRecognizer`-Klasse für die Erkennung der Ablegegeste. Diese Klasse definiert die folgenden Eigenschaften:

- `AllowDrop` vom Typ `bool` gibt an, ob das Element, dem die Gestenerkennung angefügt ist, ein Ablageziel sein kann. Der Standardwert dieser Eigenschaft ist `false`.
- `DragOverCommand` vom Typ `ICommand`, der ausgeführt wird, sobald die Ziehquelle über das Ablageziel gezogen wird.
- `DragOverCommandParameter` vom Typ `object`: der Parameter, der an `DragOverCommand` übergeben wird.
- `DropCommand` vom Typ `ICommand`, der ausgeführt wird, sobald die Ziehquelle über dem Ablageziel abgelegt wird.
- `DropCommandParameter` vom Typ `object`: der Parameter, der an `DropCommand` übergeben wird.

Diese Eigenschaften werden durch [`BindableProperty`](xref:Xamarin.Forms.BindableProperty)-Objekte gestützt, was bedeutet, dass sie Ziele von Datenbindungen sein können, und geformt.

Die `DropGestureRecognizer`-Klasse definiert auch `DragOver`- und `Drop`-Ereignisse. Wenn ein `DropGestureRecognizer` eine Ziehquelle über dem Ablageziel erkennt, führt er den `DragOverCommand` aus und ruft das `DragOver`-Ereignis auf. Wenn dann ein `DropGestureRecognizer` eine Ziehquelle über dem Ablageziel erkennt, führt er den `DropCommand` aus und ruft das `Drop`-Ereignis auf.

Die `DragEventArgs`-Klasse, die das `DragOver`-Ereignis begleitet, definiert folgende Eigenschaften:

- `Data` vom Typ `DataPackage`, wo die mit der Ziehquelle verknüpften Daten enthalten sind. Diese Eigenschaft ist schreibgeschützt.
- `AcceptedOperation` vom Typ `DataPackageOperation`, womit angegeben wird, welche Vorgänge das Ablageziel zulässt.

Informationen zur `DataPackageOperation`-Enumeration finden Sie unter [Verarbeiten des DragOver-Ereignisses](#handle-the-dragover-event).

Die `DropEventArgs`-Klasse, die das `Drop`-Ereignis begleitet, definiert folgende Eigenschaften:

- `Data` vom Typ `DataPackageView`, eine schreibgeschützte Version des Datenpakets.
- `Handled` vom Typ `bool` gibt an, ob der Ereignishandler das Ereignis verarbeitet hat oder ob Xamarin.Forms seine eigene Verarbeitung fortsetzen sollte.

Das folgende XAML-Beispiel zeigt einen `DropGestureRecognizer`, der einem [`Image`](xref:Xamarin.Forms.Image) angefügt ist:

```xaml
<Image BackgroundColor="Silver"
       HeightRequest="300"
       WidthRequest="250">
    <Image.GestureRecognizers>
        <DropGestureRecognizer AllowDrop="True" />
    </Image.GestureRecognizers>
</Image>
```

Wenn in diesem Beispiel eine Ziehquelle auf dem [`Image`](xref:Xamarin.Forms.Image)-Ablageziel abgelegt wird, wird die Ziehquelle in das Ablageziel kopiert, sofern die Ziehquelle eine [`ImageSource`](xref:Xamarin.Forms.ImageSource) ist. Dies geschieht, weil Xamarin.Forms gezogene Bilder und Texte automatisch in kompatible Ablageziele kopiert.

## <a name="handle-the-dragover-event"></a>Verarbeiten des DragOver-Ereignisses

Das `DropGestureRecognizer.DragOver`-Ereignis kann optional verarbeitet werden, um anzugeben, welche Typen von Vorgängen das Ablageziel zulässt. Zu diesem Zweck kann die `AcceptedOperation`-Eigenschaft des Typs `DataPackageOperation` des `DragEventArgs`-Objekts festgelegt werden, das das `DragOver`-Ereignis begleitet.

Die `DataPackageOperation`-Enumeration definiert die folgenden Member:

- `None` gibt an, dass keine Aktion ausgeführt wird.
- `Copy` gibt an, dass der Inhalt der Ziehquelle in das Ablageziel kopiert wird.

> [!IMPORTANT]
> Wenn ein `DragEventArgs`-Objekt erstellt wird, wird die Eigenschaft `AcceptedOperation` standardmäßig auf `DataPackageOperation.Copy` gesetzt.

Das folgende XAML-Beispiel zeigt einen `DropGestureRecognizer`, der einen Handler für das `DragOver`-Ereignis registriert:

```xaml
<Image BackgroundColor="Silver"
       HeightRequest="300"
       WidthRequest="250">
    <Image.GestureRecognizers>
        <DropGestureRecognizer AllowDrop="True"
                               DragOver="OnDragOver" />
    </Image.GestureRecognizers>
</Image>
```

In diesem Beispiel wird der `DropGestureRecognizer` einem [`Image`](xref:Xamarin.Forms.Image)-Objekt angefügt. Das `DragOver`-Ereignis wird ausgelöst, wenn eine Ziehquelle über das Ablageziel gezogen wird, aber noch nicht gelöscht wurde, wodurch der `OnDragOver`-Ereignishandler ausgeführt wird:

```csharp
void OnDragOver(object sender, DragEventArgs e)
{
    e.AcceptedOperation = DataPackageOperation.None;
}
```

In diesem Beispiel wird die `AcceptedOperation`-Eigenschaft des `DragEventArgs`-Objekts auf `DataPackageOperation.None` festgelegt. Dadurch wird sichergestellt, dass keine Aktion ausgeführt wird, wenn eine Ziehquelle über dem Ablageziel abgelegt wird.

## <a name="process-the-data-package"></a>Verarbeiten des Datenpakets

Das `Drop`-Ereignis wird ausgelöst, wenn eine Ziehquelle über einem Ablageziel freigegeben wird. In diesem Fall wird Xamarin.Forms automatisch versuchen, Daten aus dem Datenpaket abzurufen, wenn eine Ziehquelle auf den folgenden Steuerelementen abgelegt wird:

- Textsteuerelemente. Textwerte können auf [`CheckBox`](xref:Xamarin.Forms.CheckBox)-, [`DatePicker`](xref:Xamarin.Forms.DatePicker)-, [`Editor`](xref:Xamarin.Forms.Editor)-, [`Entry`](xref:Xamarin.Forms.Entry)-, [`Label`](xref:Xamarin.Forms.Label)-, [`RadioButton`](xref:Xamarin.Forms.RadioButton)-, [`Switch`](xref:Xamarin.Forms.Switch)- und [`TimePicker`](xref:Xamarin.Forms.TimePicker)-Objekten abgelegt werden.
- Bildsteuerelemente. Bilder können auf [`Button`](xref:Xamarin.Forms.Button)-, [`Image`](xref:Xamarin.Forms.Image)- und [`ImageButton`](xref:Xamarin.Forms.ImageButton)-Steuerelementen abgelegt werden.

In der folgenden Tabelle sind die Eigenschaften aufgeführt, die beim Ablegen einer textbasierten Ziehquelle auf einem Textsteuerelement festgelegt, und alle Konvertierungen, die versucht werden:

| Control | Eigenschaft | Konvertierung |
| --- | --- | --- |
| `CheckBox` | `IsChecked` | `string` wird in `bool` konvertiert. |
| `DatePicker` | `Date` | `string` wird in `DateTime` konvertiert. |
| `Editor` | `Text` ||
| `Entry` | `Text` ||
| `Label` | `Text` ||
| `RadioButton` | `IsChecked` | `string` wird in `bool` konvertiert. |
| `Switch` | `IsToggled` | `string` wird in `bool` konvertiert. |
| `TimePicker` | `Time` | `string` wird in eine `TimeSpan` konvertiert. |

Für andere Inhalte als Text und Bilder müssen Sie das Datenpaket selbst verarbeiten.

Die `DropEventArgs`-Klasse, die das `Drop`-Ereignis begleitet, definiert eine `Data`-Eigenschaft vom Typ `DataPackageView`. Diese Eigenschaft stellt eine schreibgeschützte Version des Datenpakets dar.

### <a name="retrieve-image-or-text-data"></a>Abrufen von Bild- oder Textdaten

Bild- oder Textdaten können mithilfe von Methoden, die in der `DataPackageView`-Klasse definiert sind, aus einem Datenpaket im Handler für das `Drop`-Ereignis abgerufen werden.

Die `DataPackageView`-Klasse beinhaltet die `GetImageAsync`- und die `GetTextAsync`-Methode. Die `GetImageAsync`-Methode ruft ein Bild aus dem Datenpaket ab, das in der `DataPackage.Image`-Eigenschaft gespeichert wurde, und gibt `Task<ImageSource>` zurück. Ebenso ruft die `GetTextAsync`-Methode einen Text aus dem Datenpaket ab, der in der `DataPackage.Text`-Eigenschaft gespeichert wurde, und gibt `Task<string>` zurück.

Das folgende Beispiel zeigt einen `Drop`-Ereignishandler, der aus dem Datenpaket Text für einen `Path` abruft:

```csharp
async void OnDrop(object sender, DropEventArgs e)
{
    string text = await e.Data.GetTextAsync();

    // Perform logic to take action based on the text value.
}
```

In diesem Beispiel werden Textdaten mithilfe der `GetTextAsync`-Methode aus dem Datenpaket abgerufen. Dann kann eine Aktion durchgeführt werden, die auf dem Textwert basiert.

### <a name="retrieve-data-from-the-property-bag"></a>Abrufen von Daten aus der Eigenschaftensammlung

Alle Daten können für das `Drop`-Ereignis aus einem Datenpaket im Handler abgerufen werden, indem auf die `Properties`-Sammlung des Datenpakets zugegriffen wird.

Die `DataPackageView`-Klasse definiert eine `Properties`-Eigenschaft vom Typ `DataPackagePropertySetView`. Die `DataPackagePropertySetView`-Klasse stellt eine als `Dictionary<string, object>` gespeicherte schreibgeschützte Eigenschaftensammlung dar.

Das folgende Beispiel zeigt einen `Drop`-Ereignishandler, der aus der Eigenschaftensammlung eines Datenpakets Daten für ein `Rectangle` abruft:

```csharp
void OnDrop(object sender, DropEventArgs e)
{
    Square square = (Square)e.Data.Properties["Square"];

    // Perform logic to take action based on retrieved value.
}
```

In diesem Beispiel wird durch Angabe des Wörterbuchschlüssels „Square“ das `Square`-Objekt aus der Eigenschaftensammlung des Datenpakets abgerufen. Dann kann eine Aktion durchgeführt werden, die auf dem abgerufenen Wert basiert.

## <a name="related-links"></a>Verwandte Links

- [Xamarin.Forms – Drag & Drop-Gestenerkennung](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/workingwithgestures-draganddropgesture/)
