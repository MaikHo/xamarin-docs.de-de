---
title: 'Xamarin.Essentials: Vibration'
description: In diesem Dokument wird die Vibration-Klasse in Xamarin.Essentials beschrieben, mit der Sie die Vibrationsfunktion für eine gewünschte Zeitspanne starten und anhalten können.
ms.assetid: 7E8B24C4-2625-4DAE-A129-383542D34F1E
author: jamesmontemagno
ms.custom: video
ms.author: jamont
ms.date: 11/04/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: e2ed2dfdca6b6811089d4dbb5d6e90e794c79591
ms.sourcegitcommit: 32d2476a5f9016baa231b7471c88c1d4ccc08eb8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2020
ms.locfileid: "84801802"
---
# <a name="xamarinessentials-vibration"></a>Xamarin.Essentials: Vibration

Mit der Klasse **Vibration** können Sie die Vibrationsfunktion für eine gewünschte Zeitspanne starten und anhalten.

## <a name="get-started"></a>Erste Schritte

[!include[](~/essentials/includes/get-started.md)]

Für den Zugriff auf die **Vibrationsfunktion** ist die folgende plattformspezifische Einrichtung erforderlich.

# <a name="android"></a>[Android](#tab/android)

Die Berechtigung „Vibrate“ (Vibrieren) ist obligatorisch und muss im Android-Projekt konfiguriert werden. Das Hinzufügen erfolgt folgendermaßen:

Öffnen Sie die Datei **AssemblyInfo.cs** im Ordner **Eigenschaften** und fügen Sie Folgendes hinzu:

```csharp
[assembly: UsesPermission(Android.Manifest.Permission.Vibrate)]
```

Alternativ können Sie das Android-Manifest aktualisieren:

Öffnen Sie die Datei **AndroidManifest.xml** im Ordner **Eigenschaften**, und fügen Sie Folgendes im Knoten **Manifest** hinzu.

```xml
<uses-permission android:name="android.permission.VIBRATE" />
```

Alternativ können Sie mit der rechten Maustaste auf das Android-Projekt klicken und die Eigenschaften des Projekts öffnen. Suchen Sie unter **Android-Manifest** den Bereich **Erforderliche Berechtigungen:** , und aktivieren Sie die Berechtigung **VIBRATE** (Vibrieren). Dadurch wird die Datei **AndroidManifest.xml** automatisch aktualisiert.

# <a name="ios"></a>[iOS](#tab/ios)

Es ist kein zusätzliches Setup erforderlich.

# <a name="uwp"></a>[UWP](#tab/uwp)

Keine Plattformunterschiede.

-----

## <a name="using-vibration"></a>Verwenden der Vibrationsfunktion

Fügen Sie in Ihrer Klasse einen Verweis auf Xamarin.Essentials hinzu:

```csharp
using Xamarin.Essentials;
```

Die Vibrationsfunktion kann für eine bestimmte Zeitspanne oder den Standardzeitraum von 500 Millisekunden angefordert werden.

```csharp
try
{
    // Use default vibration length
    Vibration.Vibrate();

    // Or use specified time
    var duration = TimeSpan.FromSeconds(1);
    Vibration.Vibrate(duration);
}
catch (FeatureNotSupportedException ex)
{
    // Feature not supported on device
}
catch (Exception ex)
{
    // Other error has occurred.
}
```

Der Abbruch der Gerätevibration kann mit der Methode `Cancel` angefordert werden:

```csharp
try
{
    Vibration.Cancel();
}
catch (FeatureNotSupportedException ex)
{
    // Feature not supported on device
}
catch (Exception ex)
{
    // Other error has occurred.
}
```

## <a name="platform-differences"></a>Plattformunterschiede

# <a name="android"></a>[Android](#tab/android)

Keine Plattformunterschiede.

# <a name="ios"></a>[iOS](#tab/ios)

- Vibriert nur, wenn das Gerät auf „Beim Klingeln vibrieren“ eingestellt ist.
- Vibriert immer für 500 Millisekunden.
- Es ist nicht möglich, die Vibration abzubrechen.

# <a name="uwp"></a>[UWP](#tab/uwp)

Keine Plattformunterschiede.

-----

## <a name="api"></a>API

- [Vibration-Quellcode](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/Vibration)
- [Vibration-API-Dokumentation](xref:Xamarin.Essentials.Vibration)

## <a name="related-video"></a>Zugehörige Videos

> [!Video https://channel9.msdn.com/Shows/XamarinShow/Vibration-XamarinEssentials-API-of-the-Week/player]

[!include[](~/essentials/includes/xamarin-show-essentials.md)]
