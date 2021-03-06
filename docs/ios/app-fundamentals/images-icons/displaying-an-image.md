---
title: Anzeigen eines Bilds in xamarin. IOS
description: In diesem Artikel wird beschrieben, wie Sie ein Image-Asset in eine xamarin. IOS-App einschließen und dieses Bild entweder mithilfe von c#-Code oder durch Zuweisen zu einem Steuerelement im IOS-Designer anzeigen.
ms.prod: xamarin
ms.assetid: 60288B12-49E3-4E87-8690-D04A5EC7A664
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 04/24/2018
ms.openlocfilehash: a7bc2b87e267e78d841217b7860e5d54c046b788
ms.sourcegitcommit: d7c09c6cc2f479b8f14910ad2d20ec76800cd9c7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/25/2020
ms.locfileid: "91248138"
---
# <a name="displaying-an-image-in-xamarinios"></a>Anzeigen eines Bilds in xamarin. IOS

_In diesem Artikel wird beschrieben, wie Sie ein Image-Asset in eine xamarin. IOS-App einschließen und dieses Bild entweder mithilfe von c#-Code oder durch Zuweisen zu einem Steuerelement im IOS-Designer anzeigen._

## <a name="adding-and-organizing-images-in-a-xamarinios-app"></a>Hinzufügen und organisieren von Bildern in einer xamarin. IOS-App

Wenn Sie ein Image für die Verwendung in einer xamarin. IOS-app hinzufügen, verwendet der Entwickler einen Ressourcen _Katalog_ , um alle IOS-Geräte und-Lösungen zu unterstützen, die von einer APP benötigt werden.

In ios 7 hinzugefügt wurden, enthalten **Image Sätze für Asset-Kataloge** alle Versionen oder Darstellungen eines Images, die zur Unterstützung verschiedener Geräte und Skalierungsfaktoren für eine APP erforderlich sind. Anstatt sich auf den Image Ressourcen Dateinamen zu verlassen, verwenden **Image-Sets** eine JSON-Datei, um anzugeben, welches Image zu welchem Gerät und/oder zur Auflösung gehört. Dies ist die bevorzugte Methode zum Verwalten und unterstützen von Images in ios (ab IOS 9).

## <a name="adding-images-to-an-asset-catalog-image-set"></a>Hinzufügen von Bildern zu einem Asset Catalog-Image Satz

Wie bereits erwähnt, enthalten die **Image Sätze der Asset-Kataloge** alle Versionen oder Darstellungen eines Bilds, die zur Unterstützung verschiedener Geräte und Skalierungsfaktoren für eine APP erforderlich sind. Anstatt sich auf den Image Ressourcen Dateinamen zu verlassen, verwenden **Image-Sets** eine JSON-Datei, um anzugeben, welches Image zu welchem Gerät und/oder zur Auflösung gehört.

Gehen Sie folgendermaßen vor, um eine neue Abbild Gruppe zu erstellen und Ihr Bilder hinzuzufügen:

# <a name="visual-studio-for-mac"></a>[Visual Studio für Mac](#tab/macos)

1. Doppelklicken Sie im **Projektmappen-Explorer**auf die `Assets.xcassets` Datei, um Sie zur Bearbeitung zu öffnen:

    ![Die Assets. xcassets im Projektmappen-Explorer](displaying-an-image-images/imageset01.png)
2. Klicken Sie mit der rechten Maustaste auf die **Liste Assets** , und wählen Sie **neue Bildmenge**aus:

    ![Hinzufügen eines neuen Image Satzes](displaying-an-image-images/imageset02.png)
3. Wählen Sie den neuen Bildsatz aus, und der Editor wird angezeigt:

    ![Der bildrsatz-Editor](displaying-an-image-images/imageset03.png)
4. Ziehen Sie von hier aus Bilder für jedes der verschiedenen Geräte und Auflösungen, die erforderlich sind.
5. Doppelklicken Sie auf den **Namen** des neuen Image Satzes in der **Liste Assets** , um ihn zu bearbeiten: Bearbeiten ![ des Namens des neuen Image Satzes](displaying-an-image-images/imageset04.png)

Wenn Sie ein **Bild** im IOS-Designer verwenden, wählen Sie einfach den Namen der Gruppe in der Dropdown Liste im Eigenschaften-Editor aus:

![Wählen Sie in der Dropdown Liste den Namen eines Image Satzes aus.](displaying-an-image-images/imageset06.png)

# <a name="visual-studio"></a>[Visual Studio](#tab/windows)

1. Öffnen Sie den Ressourcen Katalog über die **Projektmappen-Explorer**, und klicken Sie in der linken oberen Ecke auf die Schaltfläche **plus** :

    ![Klicken Sie auf die Schaltfläche Plus](displaying-an-image-images/asset5.png)

2. Wählen Sie **Bild Satz hinzufügen** aus, und der Bild Satz-Editor wird für die neue Bildmenge angezeigt. Ziehen Sie von hier aus Bilder für jedes der verschiedenen Geräte und Auflösungen, die erforderlich sind.

    ![Der bildrsatz-Editor](displaying-an-image-images/asset7.png)

### <a name="renaming-an-image-set"></a>Umbenennen eines Bild Satzes

Gehen Sie folgendermaßen vor, um einen Bildsatz umzubenennen:

1. Doppelklicken Sie im **Projektmappen-Explorer**auf die **Asset Catalog** -Datei, um Sie zur Bearbeitung zu öffnen:

    ![Der Asset-Katalog im Projektmappen-Explorer](displaying-an-image-images/rename01.png)
2. Wählen Sie das umzubenennende **Bild** aus:

    ![Wählen Sie das umzubenennende Bild aus.](displaying-an-image-images/rename02.png)
3. Scrollen Sie im **Eigenschaften-Explorer**nach unten, und wählen Sie " **Name**" ( **im Abschnitt "** Sonstige") aus:

    ![Wählen Sie im Abschnitt Verschiedenes den Namen aus.](displaying-an-image-images/rename03.png)
4. Geben Sie einen neuen **Namen** für die **Abbild Gruppe** ein, und speichern Sie die Änderungen.

-----

Wenn Sie einen **Bildsatz** im Code verwenden, verweisen Sie ihn anhand des Namens, indem Sie die- `FromBundle` Methode der- `UIImage` Klasse aufrufen. Beispiel:

```csharp
MonkeyImage.Image = UIImage.FromBundle ("PurpleMonkey");
```

> [!IMPORTANT]
> Wenn die einem Bild Satz zugewiesenen Bilder nicht ordnungsgemäß angezeigt werden, stellen Sie sicher, dass der richtige Dateiname mit der-Methode verwendet wird `FromBundle` (die **Bildmenge** und nicht der Name des übergeordneten **Objekt Katalogs** ). Bei PNG-Bildern `.png` kann die Erweiterung weggelassen werden. Bei anderen Bildformaten ist die Erweiterung erforderlich (z. b. `PurpleMonkey.jpg`).

### <a name="using-vector-images-in-asset-catalogs"></a>Verwenden von Vektorbildern in Asset-Katalogen

Ab IOS 8 wurde eine spezielle **Vektor** Klasse zu **Bild Sätzen** hinzugefügt, die es dem Entwickler ermöglichen, ein **PDF-** formatiertes Vektorbild in die Kassette einzubeziehen, anstatt einzelne Bitmapdateien in den verschiedenen Auflösungen einzubeziehen. Stellen Sie mit dieser Methode eine einzelne Vektor Datei für die `@1x` Auflösung (formatiert als Vektor-PDF-Datei) bereit, und die `@2x` -und- `@3x` Versionen der Datei werden zur Kompilierzeit generiert und in das Paket der Anwendung eingeschlossen.

# <a name="visual-studio-for-mac"></a>[Visual Studio für Mac](#tab/macos)

![Vektorbilder im Asset-Katalog-Editor](displaying-an-image-images/imageset05.png)

# <a name="visual-studio"></a>[Visual Studio](#tab/windows)

![Vektorbilder im Asset-Katalog-Editor](displaying-an-image-images/asset8.png)

-----

Wenn der Entwickler z. b. eine `MonkeyIcon.pdf` Datei als Vektor für einen Asset-Katalog mit einer Auflösung von 150px x 150px enthält, sind die folgenden bitmapassets in die abschließende App Bundle eingeschlossen, als Sie kompiliert wurde:

- `MonkeyIcon@1x.png` -150px x 150px Auflösung.
- `MonkeyIcon@2x.png` -300 px x 300 px Auflösung.
- `MonkeyIcon@3x.png` -450 px x 450 px Auflösung.

Bei der Verwendung von PDF-Vektorbildern in Asset-Katalogen sollten folgende Aspekte berücksichtigt werden:

- Dabei handelt es sich nicht um vollständige Vektor Unterstützung, da die PDF-Datei zur Kompilierzeit in eine Bitmap gerengt wird und die in der abschließenden Anwendung enthaltenen Bitmaps.
- Die Größe des Abbilds kann nicht angepasst werden, sobald es im Asset-Katalog festgelegt wurde. Wenn der Entwickler versucht, die Größe des Bilds zu ändern (entweder im Code oder mithilfe der Klassen für automatisches Layout und Größe), wird das Bild wie jede andere Bitmap verzerrt.
- Assetkataloge sind nur mit IOS 7 und höher kompatibel. Wenn eine APP IOS 6 oder niedriger unterstützen muss, können Ressourcen Kataloge nicht verwendet werden.

## <a name="working-with-template-images"></a>Arbeiten mit Vorlagen Images

Basierend auf dem Entwurf einer IOS-App kann es vorkommen, dass der Entwickler ein Symbol oder Bild innerhalb der Benutzeroberfläche anpassen muss, damit er einer Änderung des Farbschemas entspricht (z. b. basierend auf den Benutzereinstellungen).

Um diesen Effekt zu erzielen, ändern Sie den _Rendermodus_ des Image Assets in das **Vorlagen Image**:

# <a name="visual-studio-for-mac"></a>[Visual Studio für Mac](#tab/macos)

[![Der Rendermodus ist auf das Vorlagen Image festgelegt.](displaying-an-image-images/templateimage01.png)](displaying-an-image-images/templateimage01.png#lightbox)

# <a name="visual-studio"></a>[Visual Studio](#tab/windows)

[![Rendermodus auf Vorlage festgelegt](displaying-an-image-images/templateimage01vs.png)](displaying-an-image-images/templateimage01vs.png#lightbox)

-----

Weisen Sie im IOS-Designer das Image-Asset einem UI-Steuerelement zu, und legen Sie dann das **tint** fest, um das Bild zu färben:

# <a name="visual-studio-for-mac"></a>[Visual Studio für Mac](#tab/macos)

[![Legen Sie das tint fest, um das Bild farbig zu färben.](displaying-an-image-images/templateimage03.png)](displaying-an-image-images/templateimage03.png#lightbox)

# <a name="visual-studio"></a>[Visual Studio](#tab/windows)

[![Legen Sie das tint fest, um das Bild farbig zu färben.](displaying-an-image-images/templateimage03vs.png)](displaying-an-image-images/templateimage03vs.png#lightbox)

-----

Optional können Image Asset und tint direkt im Code festgelegt werden:

```csharp
MyIcon.Image = UIImage.FromBundle ("MessageIcon");
MyIcon.TintColor = UIColor.Red;
```

Gehen Sie folgendermaßen vor, um ein Vorlagen Image vollständig aus dem Code zu verwenden:

```csharp
if (MyIcon.Image != null) {
    var mutableImage = MyIcon.Image.ImageWithRenderingMode (UIImageRenderingMode.AlwaysTemplate);
    MyIcon.Image = mutableImage;
    MyIcon.TintColor = UIColor.Red;
}
```

Da die- `RenderMode` Eigenschaft eines schreibgeschützt `UIImage` ist, verwenden Sie die- `ImageWithRenderingMode` Methode, um eine neue Instanz des Bilds mit der gewünschten rendermoduseinstellung zu erstellen.

Es gibt drei mögliche Einstellungen für `UIImage.RenderMode` über die-Aufzählung `UIImageRenderingMode` :

- `AlwaysOriginal` : Erzwingt, dass das Bild ohne Änderungen als ursprüngliche Quell Bilddatei gerendert wird.
- `AlwaysTemplate` -Erzwingt, dass das Bild als Vorlagen Bild gerendert wird, indem die Pixel mit der angegebenen Farbe eingefärbt werden `Tint` .
- `Automatic` : Rendert das Bild entweder als Vorlage oder als ursprüngliches, das auf der Umgebung basiert, in der es verwendet wird. Wenn das Bild beispielsweise in einem `UIToolBar` , oder verwendet wird `UINavigationBar` , `UITabBar` `UISegmentControl` wird es als Vorlage behandelt.

## <a name="adding-new-assets-collections"></a>Neue Ressourcen Sammlungen werden hinzugefügt

Beim Arbeiten mit Bildern in Ressourcen Katalogen kann es vorkommen, dass eine neue Sammlung erforderlich ist, anstatt alle Images der APP der Auflistung hinzuzufügen `Assets.xcassets` . Beispielsweise beim Entwerfen von bedarfsgesteuerten Ressourcen.

So fügen Sie dem Projekt einen neuen Ressourcen Katalog hinzu:

# <a name="visual-studio-for-mac"></a>[Visual Studio für Mac](#tab/macos)

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den **Projektnamen** , und wählen Sie neue Datei **Hinzufügen**  >  **... aus.**
2. Wählen Sie **IOS**  >  **Asset Catalog**aus, geben Sie einen **Namen** für die Sammlung ein, und klicken Sie auf die Schaltfläche **neu**

    ![Erstellen eines neuen Ressourcen Katalogs](displaying-an-image-images/asset01.png)

# <a name="visual-studio"></a>[Visual Studio](#tab/windows)

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner **Asset** Katalogs, und wählen Sie **> neuen Ressourcen Katalog hinzufügen**aus.
2. Geben Sie einen Namen, und klicken Sie auf **Hinzufügen**:

    ![Erstellen eines neuen Ressourcen Katalogs](displaying-an-image-images/asset1.png)

-----

Von hier aus kann die Auflistung genauso wie die standardmäßige Sammlung, die `Assets.xcassets` automatisch im Projekt enthalten ist, bearbeitet werden.

## <a name="using-images-with-controls"></a>Verwenden von Bildern mit Steuerelementen

Zusätzlich zur Verwendung von Images zur Unterstützung einer App verwendet IOS auch Bilder mit App-Steuerelement Typen wie z. b. Registerkarten, Symbolleisten, Navigationsleisten, Tabellen und Schaltflächen. Eine einfache Möglichkeit, ein Bild auf einem-Steuerelement anzuzeigen, besteht darin, `UIImage` der-Eigenschaft des-Steuer Elements eine-Instanz zuzuweisen `Image` .

### <a name="frombundle"></a>Frombundle

Der `FromBundle` Methodenaufrufe ist ein synchroner (blockierender) Befehl, der über eine integrierte Anzahl von Abbild Lade-und-Verwaltungsfunktionen verfügt, wie z. b. Caching-Unterstützung und automatische Behandlung von Bilddateien für verschiedene Auflösungen.

Im folgenden Beispiel wird gezeigt, wie das Image eines auf einem festgelegt wird `UITabBarItem` `UITabBar` :

```csharp
TabBarItem.Image = UIImage.FromBundle ("MyImage");
```

Angenommen, `MyImage` Es handelt sich um den Namen eines imageassets, das einem oben genannten Ressourcen Katalog hinzugefügt wird. Geben Sie beim Arbeiten mit dem Asset-Katalog Abbild einfach den Namen des Bilds an, das in der- `FromBundle` Methode für **PNG** -formatierte Images

```csharp
TabBarItem.Image = UIImage.FromBundle ("MyImage");
```

Fügen Sie die Erweiterung für ein beliebiges anderes Bildformat in den Namen ein. Beispiel:

```csharp
TabBarItem.Image = UIImage.FromBundle ("MyImage.jpg");
```

Weitere Informationen zu Symbolen und Bildern finden Sie in der Apple-Dokumentation zu [Richtlinien für benutzerdefiniertes Symbol und Bild Erstellung](https://developer.apple.com/library/ios/#documentation/UserExperience/Conceptual/MobileHIG/IconsImages/IconsImages.html).

## <a name="displaying-an-image-in-a-storyboard"></a>Anzeigen eines Bilds in einem Storyboard

Nachdem ein Image einem xamarin. IOS-Projekt mit einem Asset-Katalog hinzugefügt wurde, kann es problemlos in einem Storyboard mithilfe von `UIImageView` im IOS-Designer angezeigt werden. Wenn z. b. das folgende bildasset hinzugefügt wurde:

# <a name="visual-studio-for-mac"></a>[Visual Studio für Mac](#tab/macos)

![Ein beispielbildintasset wurde hinzugefügt.](displaying-an-image-images/display01.png)

Gehen Sie folgendermaßen vor, um die Datei auf einem Storyboard anzuzeigen:

1. Doppelklicken Sie auf die `Main.storyboard` Datei im **Projektmappen-Explorer** , um Sie im IOS-Designer zur Bearbeitung zu öffnen.
2. Wählen Sie eine **Bildansicht** aus der **Toolbox**aus:

     ![Wählen Sie eine Bildansicht aus der Toolbox aus.](displaying-an-image-images/display02.png)
3. Ziehen Sie die Bildansicht auf die Entwurfs Oberfläche, und positionieren Sie Sie nach Bedarf:

    ![Eine neue Bildansicht auf der Designoberfläche](displaying-an-image-images/display03.png)
4. Wählen Sie im Abschnitt **Widget** des **Eigenschaften-Explorers** das gewünschte **Bild** Medienobjekt aus, das angezeigt werden soll:

    ![Wählen Sie das gewünschte Bildmedien Objekt für die Anzeige aus.](displaying-an-image-images/display04.png)
5. Verwenden Sie im Abschnitt **Ansicht** den- **Modus** , um zu steuern, wie die Größe des Bilds geändert wird, wenn die Größe der **Bildansicht** geändert wird.
6. Wenn die **Bildansicht** ausgewählt ist, klicken Sie erneut, um **Einschränkungen**hinzuzufügen:

    ![Hinzufügen von Einschränkungen](displaying-an-image-images/display05.png)
7. Ziehen Sie den "T"-förmigen Zieh Punkt an jedem Rand der **Bildansicht** an die entsprechende Seite des Bildschirms, um das Bild an die Seiten anzuheften. Auf diese Weise wird die **Bildansicht** verkleinert und vergrößert, wenn die Größe des Bildschirms geändert wird.
8. Speichern Sie die Änderungen am Storyboard.

# <a name="visual-studio"></a>[Visual Studio](#tab/windows)

![Ein beispielbildintasset wurde hinzugefügt.](displaying-an-image-images/display01vs.png)

Gehen Sie folgendermaßen vor, um die Datei auf einem Storyboard anzuzeigen:

1. Doppelklicken Sie auf die `Main.storyboard` Datei im **Projektmappen-Explorer** , um Sie im IOS-Designer zur Bearbeitung zu öffnen.
2. Wählen Sie eine **Bildansicht** aus der **Toolbox**aus:

     ![Wählen Sie eine Bildansicht aus der Toolbox aus.](displaying-an-image-images/display02vs.png)
3. Ziehen Sie die Bildansicht auf die Entwurfs Oberfläche, und positionieren Sie Sie nach Bedarf:

    ![Eine neue Bildansicht auf der Designoberfläche](displaying-an-image-images/display03vs.png)
4. Wählen Sie im Abschnitt **Widget** des **Eigenschaften-Explorers** das gewünschte **Bild** Medienobjekt aus, das angezeigt werden soll:

    ![Wählen Sie das gewünschte Bildmedien Objekt für die Anzeige aus.](displaying-an-image-images/display04vs.png)
5. Verwenden Sie im Abschnitt **Ansicht** den- **Modus** , um zu steuern, wie die Größe des Bilds geändert wird, wenn die Größe der **Bildansicht** geändert wird.
6. Wenn die **Bildansicht** ausgewählt ist, klicken Sie erneut, um **Einschränkungen**hinzuzufügen:

    ![Hinzufügen von Einschränkungen](displaying-an-image-images/display05vs.png)
7. Ziehen Sie den "T"-förmigen Zieh Punkt an jedem Rand der **Bildansicht** an die entsprechende Seite des Bildschirms, um das Bild an die Seiten anzuheften. Auf diese Weise wird die **Bildansicht** verkleinert und vergrößert, wenn die Größe des Bildschirms geändert wird.
8. Speichern Sie die Änderungen am Storyboard.

-----

## <a name="displaying-an-image-in-code"></a>Anzeigen eines Bilds im Code

Wenn ein Bild einem xamarin. IOS-Projekt mit einem Asset-Katalog hinzugefügt wurde, kann es wie bei der Anzeige eines Bilds in einem Storyboard problemlos mit c#-Code angezeigt werden.

Sehen Sie sich das folgende Beispiel an.

```csharp
// Create an image view that will fill the
// parent image view and set the image from
// an Image Asset

var imageView = new UIImageView (View.Frame);
imageView.Image = UIImage.FromBundle ("Kemah");

// Add the Image View to the parent view
View.AddSubview (imageView);
```

Dieser Code erstellt einen neuen `UIImageView` und gibt ihm eine anfängliche Größe und Position. Anschließend wird das Bild aus einem Image-Asset geladen, das dem Projekt hinzugefügt wurde, und dem übergeordneten Element hinzugefügt `UIImageView` `UIView` , um es anzuzeigen.

## <a name="related-links"></a>Verwandte Links

- [Arbeiten mit Bildern (Beispiel)](https://docs.microsoft.com/samples/xamarin/ios-samples/workingwithimages)
- [Hallo iPhone](~/ios/get-started/hello-ios/index.md)
- [Bildgröße und-Auflösung (Apple)](https://developer.apple.com/design/human-interface-guidelines/ios/icons-and-images/image-size-and-resolution/)
