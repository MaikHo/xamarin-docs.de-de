---
title: Ein grundlegendes recyclerview-Beispiel
description: Eine Beispiel-APP, die die Verwendung von recyclerview veranschaulicht.
ms.prod: xamarin
ms.assetid: A50520D2-1214-40E1-9B27-B0891FE11584
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 07/30/2018
ms.openlocfilehash: 6093c983a80c53b4900bb26c3a7020724a59c06d
ms.sourcegitcommit: 93e6358aac2ade44e8b800f066405b8bc8df2510
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/09/2020
ms.locfileid: "84571295"
---
# <a name="a-basic-recyclerview-example"></a>Ein grundlegendes recyclerview-Beispiel

Um zu verstehen `RecyclerView` , wie in einer typischen Anwendung funktioniert, wird in diesem Thema die Beispiel-app " [recyclerviewer](https://docs.microsoft.com/samples/xamarin/monodroid-samples/android50-recyclerviewer) " erläutert, ein einfaches Codebeispiel, `RecyclerView` mit dem eine große Auflistung von Fotos angezeigt wird: 

[![Zwei Screenshots einer recyclerview-APP, die Kartenansichten zum Anzeigen von Fotos verwendet](recyclerview-example-images/01-recyclerviewer-sml.png)](recyclerview-example-images/01-recyclerviewer.png#lightbox)

" **Recyclerviewer** " verwendet [CardView](~/android/user-interface/controls/card-view.md) , um jedes Foto Element im Layout zu implementieren `RecyclerView` . Aufgrund der `RecyclerView` Leistungsvorteile kann diese Beispiel-app schnell und ohne merkliche Verzögerungen durch eine große Sammlung von Fotos scrollen.

### <a name="an-example-data-source"></a>Ein Beispiel für eine Datenquelle

In dieser Beispiel-App liefert die Datenquelle "Photo Album" (dargestellt durch die- `PhotoAlbum` Klasse) `RecyclerView` Element Inhalt.
`PhotoAlbum`ist eine Sammlung von Fotos mit Untertiteln. Wenn Sie diese instanziieren, erhalten Sie eine vorgefertigte Sammlung von 32 Fotos:

```csharp
PhotoAlbum mPhotoAlbum = new PhotoAlbum ();
```

Jede Foto Instanz in macht Eigenschaften verfügbar, `PhotoAlbum` die es Ihnen ermöglichen, die Image-Ressourcen-ID, `PhotoID` und die Beschriftungs Zeichenfolge zu lesen `Caption` . Die Sammlung von Fotos ist so organisiert, dass auf jedes Foto von einem Indexer zugegriffen werden kann. Die folgenden Codezeilen greifen beispielsweise auf die Image-Ressourcen-ID und die Beschriftung des zehnten Fotos in der-Auflistung zu:

```csharp
int imageId = mPhotoAlbum[9].ImageId;
string caption = mPhotoAlbum[9].Caption;
```

`PhotoAlbum`bietet auch eine `RandomSwap` Methode, die aufgerufen werden kann, um das erste Foto in der Auflistung an einer anderen Stelle in der Sammlung mit einem zufällig ausgewählten Foto auszutauschen:

```csharp
mPhotoAlbum.RandomSwap ();
```

Da die Implementierungsdetails von `PhotoAlbum` nicht für das Verständnis relevant sind `RecyclerView` , `PhotoAlbum` wird der Quellcode hier nicht angezeigt. Der Quellcode für `PhotoAlbum` ist unter [Photoalbum.cs](https://github.com/xamarin/monodroid-samples/blob/master/android5.0/RecyclerViewer/RecyclerViewer/PhotoAlbum.cs) in der Beispiel-app " [recyclerviewer](https://docs.microsoft.com/samples/xamarin/monodroid-samples/android50-recyclerviewer) " verfügbar.

### <a name="layout-and-initialization"></a>Layout und Initialisierung

Die Layoutdatei " **Main. axml**" besteht aus einem einzelnen `RecyclerView` innerhalb einer `LinearLayout` :

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent">
    <android.support.v7.widget.RecyclerView
        android:id="@+id/recyclerView"
        android:scrollbars="vertical"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent" />
</LinearLayout>
```

Beachten Sie, dass Sie den voll qualifizierten Namen **Android. Support. V7. Widget. recyclerview** verwenden müssen, da `RecyclerView` in einer Unterstützungs Bibliothek verpackt ist. Die- `OnCreate` Methode von `MainActivity` initialisiert dieses Layout, instanziiert den Adapter und bereitet die zugrunde liegende Datenquelle vor:

```csharp
public class MainActivity : Activity
{
    RecyclerView mRecyclerView;
    RecyclerView.LayoutManager mLayoutManager;
    PhotoAlbumAdapter mAdapter;
    PhotoAlbum mPhotoAlbum;

    protected override void OnCreate (Bundle bundle)
    {
        base.OnCreate (bundle);

        // Prepare the data source:
        mPhotoAlbum = new PhotoAlbum ();

        // Instantiate the adapter and pass in its data source:
        mAdapter = new PhotoAlbumAdapter (mPhotoAlbum);

        // Set our view from the "main" layout resource:
        SetContentView (Resource.Layout.Main);

        // Get our RecyclerView layout:
        mRecyclerView = FindViewById<RecyclerView> (Resource.Id.recyclerView);

        // Plug the adapter into the RecyclerView:
        mRecyclerView.SetAdapter (mAdapter);
```

Im Code werden folgende Schritte ausgeführt:

1. Instanziiert die `PhotoAlbum` Datenquelle.

2. Übergibt die Photo Album-Datenquelle an den Konstruktor des Adapters `PhotoAlbumAdapter` (der später in diesem Handbuch definiert wird). 
   Beachten Sie, dass es sich als bewährte Vorgehensweise bewährt hat, die Datenquelle als Parameter an den Konstruktor des Adapters zu übergeben. 

3. Ruft den `RecyclerView` aus dem Layout ab.

4. Schließt den Adapter in die-Instanz ein, `RecyclerView` indem die-Methode aufgerufen wird, `RecyclerView` `SetAdapter` wie oben gezeigt.

### <a name="layout-manager"></a>Layout-Manager

Jedes Element in `RecyclerView` besteht aus einer `CardView` , die ein Foto Bild und eine Foto Beschriftung enthält (Details werden im Abschnitt " [Ansichts Halter](#view-holder) " unten beschrieben). Der vordefinierte `LinearLayoutManager` wird verwendet, um die einzelnen `CardView` in einer vertikalen scrollanordnung zu gestalten:

```csharp
mLayoutManager = new LinearLayoutManager (this);
mRecyclerView.SetLayoutManager (mLayoutManager);
```

Dieser Code befindet sich in der-Methode der Hauptaktivität `OnCreate` . Der Konstruktor für den Layout-Manager erfordert einen *Kontext*, sodass der `MainActivity` mithilfe von übergeben wird, `this` wie oben gezeigt.

Anstatt den vordefinierten zu verwenden `LinearLayoutManager` , können Sie einen benutzerdefinierten LayoutManager einbinden, der zwei `CardView` Elemente nebeneinander anzeigt. dabei wird ein Seiten umturn-Animationseffekt implementiert, der die Auflistung der Fotos durchläuft. Später in diesem Handbuch sehen Sie ein Beispiel, wie das Layout durch austauschen in einem anderen LayoutManager geändert werden kann.

<a name="view-holder"></a>

### <a name="view-holder"></a>Anzeige Inhaber

Die Ansichts Inhaber Klasse wird aufgerufen `PhotoViewHolder` . Jede `PhotoViewHolder` Instanz enthält Verweise auf `ImageView` und `TextView` eines zugeordneten Zeilen Elements, das in einem-Objekt `CardView` als Diagramm angeordnet ist:

[![Diagramm von CardView mit ImageView und TextView](recyclerview-example-images/02-cardview-layout-sml.png)](recyclerview-example-images/02-cardview-layout.png#lightbox)

`PhotoViewHolder`wird von abgeleitet `RecyclerView.ViewHolder` und enthält Eigenschaften, mit denen Verweise auf das gespeichert `ImageView` und `TextView` im obigen Layout angezeigt werden.
`PhotoViewHolder`besteht aus zwei Eigenschaften und einem Konstruktor:

```csharp
public class PhotoViewHolder : RecyclerView.ViewHolder
{
    public ImageView Image { get; private set; }
    public TextView Caption { get; private set; }

    public PhotoViewHolder (View itemView) : base (itemView)
    {
        // Locate and cache view references:
        Image = itemView.FindViewById<ImageView> (Resource.Id.imageView);
        Caption = itemView.FindViewById<TextView> (Resource.Id.textView);
    }
}
```

In diesem Codebeispiel wird dem `PhotoViewHolder` Konstruktor ein Verweis auf die übergeordnete Element Ansicht () übergeben, die umschließt `CardView` `PhotoViewHolder` . Beachten Sie, dass Sie die übergeordnete Element Ansicht immer an den Basiskonstruktor weiterleiten. Der `PhotoViewHolder` Konstruktor ruft `FindViewById` für die übergeordnete Element Ansicht auf, um alle untergeordneten Ansichts Verweise zu finden, `ImageView` und `TextView` , und speichert die Ergebnisse in den `Image` -und- `Caption` Eigenschaften bzw. Der Adapter ruft später Ansichts Verweise aus diesen Eigenschaften ab, wenn er `CardView` die untergeordneten Sichten dieses Elements mit neuen Daten aktualisiert.

Weitere Informationen zu finden Sie in `RecyclerView.ViewHolder` der [Klasse "recyclerview. viewholder](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.ViewHolder.html)".

### <a name="adapter"></a>Adapter

Der Adapter lädt jede `RecyclerView` Zeile mit Daten für ein bestimmtes Foto. Für ein bestimmtes Foto an Zeilen Position *p*sucht der Adapter z. b. die zugeordneten Daten an Position *p* innerhalb der Datenquelle und kopiert diese Daten in das Zeilen Element an Position *p* in der Auflistung `RecyclerView` . Der Adapter verwendet den Ansichts Halter, um die Verweise für `ImageView` und `TextView` an dieser Position zu suchen, sodass er für diese Sichten nicht wiederholt aufgerufen werden muss, `FindViewById` Wenn der Benutzer einen Bildlauf durch die Auflistung von Fotos durchführt und Ansichten wieder verwendet.

In **recyclerviewer**wird eine Adapter Klasse von abgeleitet, `RecyclerView.Adapter` um Folgendes zu erstellen `PhotoAlbumAdapter` :

```csharp
public class PhotoAlbumAdapter : RecyclerView.Adapter
{
    public PhotoAlbum mPhotoAlbum;

    public PhotoAlbumAdapter (PhotoAlbum photoAlbum)
    {
        mPhotoAlbum = photoAlbum;
    }
    ...
}
```

Das-Element `mPhotoAlbum` enthält die Datenquelle (das Photo-Album), die an den-Konstruktor übergeben wird. der Konstruktor kopiert das Fotoalbum in diese Element Variable. Die folgenden erforderlichen `RecyclerView.Adapter` Methoden werden implementiert:

- **`OnCreateViewHolder`**&ndash;Instanziiert die elementlayoutdatei und den Ansichts Halter.

- **`OnBindViewHolder`**&ndash;Lädt die Daten an der angegebenen Position in die Sichten, deren Verweise im angegebenen Ansichts Halter gespeichert werden.

- **`ItemCount`**&ndash;Gibt die Anzahl der Elemente in der Datenquelle zurück.

Der Layout-Manager ruft diese Methoden auf, während Elemente innerhalb von positioniert werden `RecyclerView` . Die Implementierung dieser Methoden wird in den folgenden Abschnitten erläutert.

#### <a name="oncreateviewholder"></a>Onkreateviewhälter

Der LayoutManager ruft `OnCreateViewHolder` `RecyclerView` auf, wenn der einen neuen Ansichts Halter zum Darstellen eines Elements benötigt. `OnCreateViewHolder`vergrößert die Element Ansicht aus der Layoutdatei der Ansicht und umschließt die Ansicht in einer neuen- `PhotoViewHolder` Instanz. Der `PhotoViewHolder` -Konstruktor speichert und speichert Verweise auf untergeordnete Sichten im Layout, wie zuvor unter [Ansichts Halter](#view-holder)beschrieben.

Jedes Zeilen Element wird durch ein-Objekt dargestellt `CardView` , das ein `ImageView` -Objekt (für das Foto) und ein-Element `TextView` (für die Beschriftung) enthält. Dieses Layout befindet sich in der Datei " **photocardview. axml**":

```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:card_view="http://schemas.android.com/apk/res-auto"
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content">
    <android.support.v7.widget.CardView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        card_view:cardElevation="4dp"
        card_view:cardUseCompatPadding="true"
        card_view:cardCornerRadius="5dp">
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical"
            android:padding="8dp">
            <ImageView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:id="@+id/imageView"
                android:scaleType="centerCrop" />
            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textAppearance="?android:attr/textAppearanceMedium"
                android:textColor="#333333"
                android:text="Caption"
                android:id="@+id/textView"
                android:layout_gravity="center_horizontal"
                android:layout_marginLeft="4dp" />
        </LinearLayout>
    </android.support.v7.widget.CardView>
</FrameLayout>
```

Dieses Layout stellt ein einzelnes Zeilen Element in der dar `RecyclerView` . Die `OnBindViewHolder` -Methode (unten beschrieben) kopiert Daten aus der Datenquelle in die `ImageView` und `TextView` dieses Layouts.
`OnCreateViewHolder`vergrößert dieses Layout für eine angegebene Foto Position in der `RecyclerView` und instanziiert eine neue- `PhotoViewHolder` Instanz (die Verweise auf die untergeordneten `ImageView` `TextView` Sichten und im zugeordneten Layout sucht und zwischenspeichert `CardView` ):

```csharp
public override RecyclerView.ViewHolder
    OnCreateViewHolder (ViewGroup parent, int viewType)
{
    // Inflate the CardView for the photo:
    View itemView = LayoutInflater.From (parent.Context).
                Inflate (Resource.Layout.PhotoCardView, parent, false);

    // Create a ViewHolder to hold view references inside the CardView:
    PhotoViewHolder vh = new PhotoViewHolder (itemView);
    return vh;
}

```

Die resultierende Sicht Halter Instanz `vh` wird an den Aufrufer zurückgegeben (der LayoutManager).

#### <a name="onbindviewholder"></a>Onbindviewhälter

Wenn der LayoutManager bereit ist, eine bestimmte Ansicht im `RecyclerView` sichtbaren Bildschirmbereich anzuzeigen, wird die-Methode des Adapters aufgerufen, `OnBindViewHolder` um das Element an der angegebenen Zeilen Position mit Inhalt aus der Datenquelle auszufüllen. `OnBindViewHolder`Ruft die Foto Informationen für die angegebene Zeilen Position (die Bildressource des Fotos und die Zeichenfolge für die Beschriftung des Fotos) ab und kopiert diese Daten in die zugeordneten Sichten. Sichten befinden sich über Verweise, die im Ansichts Inhaber Objekt gespeichert sind (das durch den-Parameter übergeben wird `holder` ):

```csharp
public override void
    OnBindViewHolder (RecyclerView.ViewHolder holder, int position)
{
    PhotoViewHolder vh = holder as PhotoViewHolder;

    // Load the photo image resource from the photo album:
    vh.Image.SetImageResource (mPhotoAlbum[position].PhotoID);

    // Load the photo caption from the photo album:
    vh.Caption.Text = mPhotoAlbum[position].Caption;
}
```

Das eingewandelte Ansichts Halter Objekt muss zuerst in den Inhaber-Typ der abgeleiteten Ansicht umgewandelt werden (in diesem Fall `PhotoViewHolder` ), bevor es verwendet wird.
Der Adapter lädt die Bildressource in die Sicht, auf die die-Eigenschaft des Ansichts Besitzers verweist `Image` , und kopiert den Beschriftungs Text in die Sicht, auf die von der-Eigenschaft des Ansichts Besitzers verwiesen wird `Caption` . Dadurch wird die zugeordnete Ansicht an die zugehörigen Daten *gebunden* .

Beachten Sie, dass `OnBindViewHolder` der Code ist, der direkt mit der Struktur der Daten umgeht. In diesem Fall `OnBindViewHolder` versteht, wie die `RecyclerView` Element Position dem zugeordneten Datenelement in der Datenquelle zugeordnet wird. Die Zuordnung ist in diesem Fall unkompliziert, da die Position als Array Index in das Foto Album verwendet werden kann. komplexere Datenquellen erfordern jedoch möglicherweise zusätzlichen Code, um eine solche Zuordnung herzustellen.

#### <a name="itemcount"></a>ItemCount

Die- `ItemCount` Methode gibt die Anzahl der Elemente in der Datensammlung zurück. In der Beispiel-Foto-Viewer-APP ist die Anzahl der Fotos im Photo-Album die Anzahl der Fotos:

```csharp
public override int ItemCount
{
    get { return mPhotoAlbum.NumPhotos; }
}
```

Weitere Informationen zu finden Sie in `RecyclerView.Adapter` der [Klasse "recyclerview. Adapter](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html)".

### <a name="putting-it-all-together"></a>Alles vereint

Die resultierende `RecyclerView` Implementierung für die Beispiel-Foto-APP besteht aus `MainActivity` Code, der die Datenquelle, den Layout-Manager und den Adapter erstellt. `MainActivity`die `mRecyclerView` -Instanz wird erstellt, die Datenquelle und der Adapter werden instanziiert, und der Layout-Manager und der Adapter werden eingebunden:

```csharp
public class MainActivity : Activity
{
    RecyclerView mRecyclerView;
    RecyclerView.LayoutManager mLayoutManager;
    PhotoAlbumAdapter mAdapter;
    PhotoAlbum mPhotoAlbum;

    protected override void OnCreate (Bundle bundle)
    {
        base.OnCreate (bundle);
        mPhotoAlbum = new PhotoAlbum();
        SetContentView (Resource.Layout.Main);
        mRecyclerView = FindViewById<RecyclerView> (Resource.Id.recyclerView);

        // Plug in the linear layout manager:
        mLayoutManager = new LinearLayoutManager (this);
        mRecyclerView.SetLayoutManager (mLayoutManager);

        // Plug in my adapter:
        mAdapter = new PhotoAlbumAdapter (mPhotoAlbum);
        mRecyclerView.SetAdapter (mAdapter);
    }
}

```

`PhotoViewHolder`die Ansichts Verweise werden lokalisiert und zwischengespeichert:

```csharp
public class PhotoViewHolder : RecyclerView.ViewHolder
{
    public ImageView Image { get; private set; }
    public TextView Caption { get; private set; }

    public PhotoViewHolder (View itemView) : base (itemView)
    {
        // Locate and cache view references:
        Image = itemView.FindViewById<ImageView> (Resource.Id.imageView);
        Caption = itemView.FindViewById<TextView> (Resource.Id.textView);
    }
}
```

`PhotoAlbumAdapter`implementiert die drei erforderlichen über schreibungen der-Methode:

```csharp
public class PhotoAlbumAdapter : RecyclerView.Adapter
{
    public PhotoAlbum mPhotoAlbum;
    public PhotoAlbumAdapter (PhotoAlbum photoAlbum)
    {
        mPhotoAlbum = photoAlbum;
    }

    public override RecyclerView.ViewHolder
        OnCreateViewHolder (ViewGroup parent, int viewType)
    {
        View itemView = LayoutInflater.From (parent.Context).
                    Inflate (Resource.Layout.PhotoCardView, parent, false);
        PhotoViewHolder vh = new PhotoViewHolder (itemView);
        return vh;
    }

    public override void
        OnBindViewHolder (RecyclerView.ViewHolder holder, int position)
    {
        PhotoViewHolder vh = holder as PhotoViewHolder;
        vh.Image.SetImageResource (mPhotoAlbum[position].PhotoID);
        vh.Caption.Text = mPhotoAlbum[position].Caption;
    }

    public override int ItemCount
    {
        get { return mPhotoAlbum.NumPhotos; }
    }
}
```

Wenn dieser Code kompiliert und ausgeführt wird, erstellt er die grundlegende Foto Anzeige-APP, wie in den folgenden Screenshots gezeigt:

[![Zwei Screenshots der Foto Anzeige-App mit vertikalen Bildlauf-Fotokarten](recyclerview-example-images/03-recyclerviewer-basic-sml.png)](recyclerview-example-images/03-recyclerviewer-basic.png#lightbox)

Wenn keine Schatten gezeichnet werden (wie im obigen Screenshot dargestellt), bearbeiten Sie **Properties/androidmanifest. XML** , und fügen Sie dem-Element die folgende Attribut Einstellung hinzu `<application>` :

```xml
android:hardwareAccelerated="true"
```

Diese grundlegende App unterstützt nur das Durchsuchen des Foto-Albums. Es antwortet nicht auf Element Berührungs Ereignisse und verarbeitet auch keine Änderungen an den zugrunde liegenden Daten. Diese Funktion wird unter [Erweitern des recyclerview-Beispiels](~/android/user-interface/layouts/recycler-view/extending-the-example.md)hinzugefügt.

### <a name="changing-the-layoutmanager"></a>Ändern von layoutmanager

Aufgrund der `RecyclerView` Flexibilität können Sie die APP leicht ändern, um einen anderen LayoutManager zu verwenden. Im folgenden Beispiel wird Sie so geändert, dass das Foto Album mit einem Raster Layout angezeigt wird, das horizontal und nicht mit einem vertikalen linearen Layout rollt. Zu diesem Zweck wird die Instanziierung des Layout-Managers so geändert, dass die-Instanz `GridLayoutManager` wie folgt verwendet wird:

```csharp
mLayoutManager = new GridLayoutManager(this, 2, GridLayoutManager.Horizontal, false);
```

Diese Codeänderung ersetzt die vertikale `LinearLayoutManager` durch einen `GridLayoutManager` , der ein Raster darstellt, das aus zwei Zeilen besteht, die in horizontaler Richtung scrollen. Wenn Sie die APP erneut kompilieren und ausführen, sehen Sie, dass die Fotos in einem Raster angezeigt werden und dass der Bildlauf horizontal und nicht vertikal verläuft:

[![Screenshot der APP mit horizontal Bildlauf-Fotos in einem Raster](recyclerview-example-images/04-gridlayoutmanager-sml.png)](recyclerview-example-images/04-gridlayoutmanager.png#lightbox)

Wenn Sie nur eine Codezeile ändern, ist es möglich, die Foto-Anzeige-APP so zu ändern, dass Sie ein anderes Layout mit unterschiedlichem Verhalten verwendet.
Beachten Sie, dass weder der Adapter Code noch das LayoutXml geändert werden musste, um den Layoutstil zu ändern. 

Im nächsten Thema, [Erweitern des recyclerview-Beispiels](~/android/user-interface/layouts/recycler-view/extending-the-example.md), wird diese einfache Beispiel-App erweitert, um Ereignisse mit Element Klick zu behandeln und zu aktualisieren, `RecyclerView` Wenn sich die zugrunde liegende Datenquelle ändert.

## <a name="related-links"></a>Verwandte Links

- [Recyclerviewer (Beispiel)](https://docs.microsoft.com/samples/xamarin/monodroid-samples/android50-recyclerviewer)
- [RecyclerView](~/android/user-interface/layouts/recycler-view/index.md)
- [Recyclerview-Teile und-Funktionalität](~/android/user-interface/layouts/recycler-view/parts-and-functionality.md)
- [Erweitern des recyclerview-Beispiels](~/android/user-interface/layouts/recycler-view/extending-the-example.md)
- [RecyclerView](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.html)
