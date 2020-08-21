---
title: Verpacken von Wear-apps
description: In diesem Artikel wird beschrieben, wie Sie Android Wear-apps verpacken.
ms.prod: xamarin
ms.assetid: E32DD855-78DD-46F8-B234-4EAC0756BDA2
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 02/02/2018
ms.openlocfilehash: 83c4ba8cbdc360682a4e06a885be15dd20d0f249
ms.sourcegitcommit: f4b26c5b8cc84f79123951e80c15061eb859452d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/21/2020
ms.locfileid: "88720304"
---
# <a name="packaging-wear-apps"></a>Verpacken von Wear-apps

> [!WARNING]
> Die folgenden Dokumente und Beispiel Projekte werden möglicherweise nicht mehr verwaltet.
> Ab [xamarin. Android 11,1][xa-11.1]wird die automatische Paket Erstellung einer Android Wear-Anwendung in einer Android-Anwendung mit einer Android-Anwendung nicht mehr unterstützt. Stattdessen wird empfohlen, Android Wear-Anwendungen als [eigenständige Anwendungen][standalone] zu verteilen.

Android Wear 1,0-apps werden mit einer vollständigen Android-App für die Verteilung auf Google Play verpackt.

Android Wear 2,0-Apps können als [eigenständige Anwendungen][standalone]an Google Play übermittelt werden.

[xa-11.1]: https://docs.microsoft.com/xamarin/android/release-notes/11/11.1
[standalone]: https://developer.android.com/training/wearables/apps/standalone-apps

## <a name="automatic-packaging"></a>Automatisches Verpacken

Ab xamarin Android 5,0 wird Ihre Wear-App automatisch als Ressource in ihrer handgehaltenen App verpackt, wenn Sie einen Projekt Verweis aus dem Hand Held Projekt auf das Wear-Projekt erstellen. Sie können die folgenden Schritte ausführen, um diese Zuordnung zu erstellen: 

# <a name="visual-studio"></a>[Visual Studio](#tab/windows)

1. Wenn Ihre Wear-APP nicht bereits Teil ihrer handgehaltenen Lösung ist, klicken Sie mit der rechten Maustaste auf den Projektmappenknoten, und wählen Sie **Hinzufügen > vorhandenes Projekt hinzufügen**aus.

2. Navigieren Sie zu der **csproj** -Datei Ihrer Wear-APP, wählen Sie Sie aus, und klicken Sie auf **Öffnen**. Das App-Projekt "Wear" sollte nun in Ihrer Hand Held Lösung sichtbar sein.

3. Klicken Sie mit der rechten Maustaste auf den Knoten **Verweise** und wählen Sie **Verweis hinzufügen**

4. Aktivieren Sie im Dialogfeld **Verweis-Manager** das Projekt "Wear" (Klicken Sie, um ein Häkchen hinzuzufügen), und klicken Sie auf **OK**.

5. Ändern Sie den Paketnamen für das Wear-Projekt so, dass er mit dem Paketnamen des Handheld-Projekts übereinstimmt (der Paketname kann unter **Eigenschaften > Android-Manifest**geändert werden).

# <a name="visual-studio-for-mac"></a>[Visual Studio für Mac](#tab/macos)

1. Wenn Ihre Wear-APP nicht bereits Teil ihrer handgehaltenen Lösung ist, klicken Sie mit der rechten Maustaste auf den Projektmappenknoten, und wählen Sie **Hinzufügen > vorhandenes Projekt hinzufügen**aus.

2. Navigieren Sie zu der **csproj** -Datei Ihrer Wear-APP, wählen Sie Sie aus, und klicken Sie auf **Öffnen**. Das App-Projekt "Wear" sollte nun in Ihrer Hand Held Lösung sichtbar sein.

3. Klicken Sie mit der rechten Maustaste auf den Projekt Knoten "Handheld" in der Projekt Mappe, und klicken Sie auf **Verweise bearbeiten.**

4. Aktivieren Sie im Dialogfeld **Verweise bearbeiten** das Projekt "Wear" (zum Hinzufügen eines Häkchens), und klicken Sie dann auf **OK**.

5. Ändern Sie den Paketnamen für das Wear-Projekt so, dass er mit dem Paketnamen des Handheld-Projekts übereinstimmt (der Paketname kann unter **Projektoptionen > Android-Anwendung**geändert werden).

-----

Beachten Sie, dass ein **XA5211** -Fehler ausgegeben wird, wenn der Paketname der Wear-APP nicht mit dem Paketnamen der Handschrift-App identisch ist. Beispiel:

```shell
Error XA5211: Embedded wear app package name differs from handheld 
app package name (com.companyname.mywearapp != com.companyname.myapp). (XA5211)
```

Um diesen Fehler zu beheben, ändern Sie den Paketnamen der Wear-APP so, dass er mit dem Paketnamen der handgehaltenen App übereinstimmt.

Wenn Sie auf **erstellen > Build all**(erstellen) klicken, löst diese Zuordnung die automatische Paket Erstellung des Wear-Projekts in das Haupt-Handheld-Projekt (Phone) aus. Die Wear-APP wird automatisch erstellt und als Ressource in die Handheld-App eingeschlossen.

Die Assembly, die das Projekt der Wear-App generiert, wird nicht als Assemblyverweis im Handheld-Projekt (Phone) verwendet. Stattdessen führt der Buildprozess Folgendes aus:

- Überprüft, ob die Paketnamen Stimmen. 

- Generiert XML und fügt es dem Handheld-Projekt hinzu, um es der Wear-App zuzuordnen. Beispiel: 

    ```xml
    <!-- Handheld (Phone) Project.csproj -->
    <ProjectReference Include="..\MyWearApp\MyWearApp.csproj">
        <Project>{D80E1FEF-653B-448C-B2AA-609C74E88340}</Project>
        <Name>MyWearApp</Name>
        <IsAppExtension>True</IsAppExtension>
    </ProjectReference>
    ```

- Fügt dem Handheld-Projekt die Wear-App als **rohressource** hinzu. 

## <a name="manual-packaging"></a>Manuelle Paket Erstellung

Sie können Android Wear-apps in xamarin. Android vor Version 5,0 schreiben, aber Sie müssen diese Anweisungen zur manuellen Paket Erstellung befolgen, um die APP zu verteilen: 

1. Stellen Sie sicher, dass das Projekt und die handgehaltenen Projekte (Telefon Projekte) dieselbe Versionsnummer und denselben Paketnamen aufweisen.

2. Erstellen Sie das Projekt "Wearable" manuell als **Releasebuild** .

3. Fügen Sie das Release manuell hinzu **. APK** von Schritt (2) in das Verzeichnis **Resources/RAW** des handes (Phone)-Projekts.

4. Manuelles Hinzufügen eines neuen XML **-Ressourcen Ressourcen/XML/wearable_app_desc.xml** im Handheld-Projekt, das auf ein Wearable **APK** aus Schritt (3) verweist:

    ```xml
    <wearableApp package="wearable.app.package.name">
        <versionCode>1</versionCode>
        <versionName>1.0</versionName>
        <rawPathResId>NAME_OF_APK_FROM_STEP_3</rawPathResId>
    </wearableApp>
    ```

5. Fügen Sie `<meta-data />` dem **AndroidManifest.xml** -Element des Handlers, `<application>` das auf die neue XML-Ressource verweist, manuell ein-Element hinzu:

    ```xml
    <meta-data android:name="com.google.android.wearable.beta.app"
        android:resource="@xml/wearable_app_desc"/>
    ```

Weitere Informationen finden Sie auch in den [manuellen packging-Anweisungen](https://developer.android.com/training/wearables/apps/packaging.html#PackageManually)der Android Developer-Website.
