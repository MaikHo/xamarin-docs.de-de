---
title: Erste Schritte mit Xamarin.Essentials
description: Xamarin.Essentials stellt eine einzelne plattformübergreifende API bereit, die mit jeder iOS-, Android- und UWP-Anwendung kompatibel ist, auf die über freigegebenen Code zugegriffen werden kann, unabhängig davon, wie die Benutzeroberfläche erstellt wird.
ms.assetid: B2669C48-B659-4854-BD80-FEB0E876F5B9
author: jamesmontemagno
ms.author: jamont
ms.custom: video
ms.date: 07/10/2019
ms.openlocfilehash: c73144f797447832d795c1379f12a52494c1fbca
ms.sourcegitcommit: 1c87135a47780f34102952d4b140850b4f08b075
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/26/2019
ms.locfileid: "74536520"
---
# <a name="get-started-with-xamarinessentials"></a>Erste Schritte mit Xamarin.Essentials

Xamarin.Essentials stellt eine einzelne plattformübergreifende API bereit, die mit jeder iOS-, Android- und UWP-Anwendung kompatibel ist, auf die über freigegebenen Code zugegriffen werden kann, unabhängig davon, wie die Benutzeroberfläche erstellt wird. Weitere Informationen zu unterstützten Betriebssystemen finden Sie im [Leitfaden zur Plattform- und Featureunterstützung](platform-feature-support.md).

## <a name="installation"></a>Installation

Xamarin.Essentials ist als NuGet-Paket verfügbar, das jedem vorhandenen oder neuen Projekt mit Visual Studio hinzugefügt werden kann.

1. Laden Sie [Visual Studio](https://visualstudio.microsoft.com/) mit den [Visual Studio-Tools für Xamarin](~/get-started/installation/index.md) herunter, und installieren Sie die Suite.

2. Öffnen Sie ein vorhandenes Projekt, oder erstellen Sie ein neues Projekt mit der Vorlage „Leere App“ unter **Visual Studio C#** (Android, iPhone & iPad oder plattformübergreifend).

    > [!IMPORTANT]
    > Überprüfen Sie beim Hinzufügen zu einem UWP-Projekt, ob Build 16299 oder höher in den Projekteigenschaften festgelegt ist.

3. Fügen Sie das NuGet-Paket [**Xamarin.Essentials**](https://www.nuget.org/packages/Xamarin.Essentials/) jedem Projekt hinzu:

    <!--markdownlint-disable MD023 -->
    # <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

    Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Namen der Projektmappe, und wählen Sie **NuGet-Pakete** aus. Suchen Sie nach **Xamarin.Essentials**, und installieren Sie das Paket in **ALLEN** Projekten, einschließlich der Android-, iOS-, UWP- und .NET-Standardbibliotheken.

    # <a name="visual-studio-for-mactabmacos"></a>[Visual Studio für Mac](#tab/macos)

    Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Projektnamen, und wählen Sie **Hinzufügen > NuGet-Pakete...** aus. Suchen Sie nach **Xamarin.Essentials**, und installieren Sie das Paket in **ALLEN** Projekten, einschließlich der Android-, iOS- und .NET-Standardbibliotheken.

    -----

4. Fügen Sie in jeder C#-Klasse einen Verweis auf Xamarin.Essentials als Referenz auf die APIs hinzu.

    ```csharp
    using Xamarin.Essentials;
    ```

5. Xamarin.Essentials erfordert ein plattformspezifisches Setup:

    # <a name="androidtabandroid"></a>[Android](#tab/android)

    Xamarin.Essentials unterstützt die Android-Mindestversion 4.4, d.h. API-Ebene 19, doch die Android-Zielversion für die Kompilierung muss 9.0 entsprechen, d.h. API-Ebene 28. In Visual Studio werden diese beiden Versionen auf der Registerkarte „Android-Manifest“ im Dialogfeld „Projekteigenschaften“ für das Android-Projekt festgelegt. In Visual Studio für Mac werden sie auf der Registerkarte „Android-Anwendung“ im Dialogfeld „Projektoptionen“ für das Android-Projekt eingerichtet.

    Xamarin.Essentials installiert die benötigte Version 28.0.0.1 der Xamarin.Android.Support-Bibliotheken. Alle anderen Xamarin.Android.Support-Bibliotheken, die Ihre Anwendung benötigt, sollten ebenfalls mit dem NuGet-Paket-Manager auf Version 28.0.0.1 aktualisiert werden. Alle von Ihrer Anwendung verwendeten Xamarin.Android.Support-Bibliotheken sollten gleich sein und mindestens die Version 28.0.0.1 haben. Wenn Sie Probleme beim Hinzufügen des Xamarin.Essentials-NuGets oder beim Aktualisieren von NuGet-Paketen in Ihrer Projektmappe haben, lesen Sie [Problembehandlung](troubleshooting.md).

    Im `MainLauncher`-Element oder in einem beliebigen `Activity`-Element des Android-Projekts, das gestartet wird, muss Xamarin.Essentials in der `OnCreate`-Methode initialisiert werden:

    ```csharp
    protected override void OnCreate(Bundle savedInstanceState) {
        //...
        base.OnCreate(savedInstanceState);
        Xamarin.Essentials.Platform.Init(this, savedInstanceState); // add this line to your code, it may also be called: bundle
        //...
    ```

    Um Laufzeitberechtigungen auf Android zu verwalten, muss Xamarin.Essentials `OnRequestPermissionsResult` erhalten. Fügen Sie allen `Activity`-Klassen den folgenden Code hinzu:

    ```csharp
    public override void OnRequestPermissionsResult(int requestCode, string[] permissions, Android.Content.PM.Permission[] grantResults)
    {
        Xamarin.Essentials.Platform.OnRequestPermissionsResult(requestCode, permissions, grantResults);

        base.OnRequestPermissionsResult(requestCode, permissions, grantResults);
    }
    ```

    # <a name="iostabios"></a>[iOS](#tab/ios)

    Es ist kein zusätzliches Setup erforderlich.

    # <a name="uwptabuwp"></a>[UWP](#tab/uwp)

    Es ist kein zusätzliches Setup erforderlich.

    -----

6. Befolgen Sie die [Xamarin.Essentials-Anleitungen](index.md), mit denen Sie Codeausschnitte für jedes Feature kopieren und einfügen können.

## <a name="xamarinessentials---cross-platform-apis-for-mobile-apps-video"></a>Xamarin.Essentials – plattformübergreifende APIs für Mobile Apps (Video)

> [!Video https://channel9.msdn.com/Shows/XamarinShow/Snack-Pack-XamarinEssentials-Cross-Platform-APIs-for-Mobile-Apps/player]

## <a name="other-resources"></a>Weitere Ressourcen

Noch nicht mit Xamarin vertrauten Entwicklern wird empfohlen, [Erste Schritte mit der Xamarin-Entwicklung](~/cross-platform/getting-started/index.md) zu besuchen.

Im [Xamarin.Essentials-GitHub-Repository](https://github.com/xamarin/Essentials) finden Sie den aktuellen Quellcode sowie Ankündigungen und erfahren, wie Sie Beispiele ausführen und das Repository klonen. Wir freuen uns über Beiträge aus der Community.

In der [API-Dokumentation](xref:Xamarin.Essentials) finden Sie weitere Informationen zu allen Funktionen von Xamarin.Essentials.
