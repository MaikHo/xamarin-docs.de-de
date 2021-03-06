---
title: Xamarin.Essentials Karte
description: Mit der Map-Klasse in Xamarin.Essentials kann eine Anwendung die installierte Kartenanwendung für einen bestimmten Standort oder eine bestimmte Ortsmarkierung öffnen.
ms.assetid: BABF40CC-8BEE-43FD-BE12-6301DF27DD33
author: jamesmontemagno
ms.author: jamont
ms.date: 05/26/2020
ms.custom: video
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: b566b6705d1cd8e229b6a2636fffd2ebc2ed5cde
ms.sourcegitcommit: 32d2476a5f9016baa231b7471c88c1d4ccc08eb8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2020
ms.locfileid: "84802263"
---
# <a name="xamarinessentials-map"></a>Xamarin.Essentials: Karte

Mit der **Map**-Klasse kann eine Anwendung die installierte Kartenanwendung für einen bestimmten Standort oder eine bestimmte Ortsmarkierung öffnen.

## <a name="get-started"></a>Erste Schritte

[!include[](~/essentials/includes/get-started.md)]

## <a name="using-map"></a>Verwenden von Map

Fügen Sie in Ihrer Klasse einen Verweis auf Xamarin.Essentials hinzu:

```csharp
using Xamarin.Essentials;
```

Die Map-Funktionalität ruft die `OpenAsync`-Methode mit `Location` oder `Placemark` zum Öffnen des optionalen `MapLaunchOptions` auf.

```csharp
public class MapTest
{
    public async Task NavigateToBuilding25()
    {
        var location = new Location(47.645160, -122.1306032);
        var options =  new MapLaunchOptions { Name = "Microsoft Building 25" };

        try
        {
            await Map.OpenAsync(location, options);
        }
        catch (Exception ex)
        {
            // No map application available to open
        }
    }
}
```

Beim Öffnen mit einem `Placemark`-Element werden die folgenden Informationen benötigt:

- `CountryName`
- `AdminArea`
- `Thoroughfare`
- `Locality`

```csharp
public class MapTest
{
    public async Task NavigateToBuilding25()
    {
        var placemark = new Placemark
            {
                CountryName = "United States",
                AdminArea = "WA",
                Thoroughfare = "Microsoft Building 25",
                Locality = "Redmond"
            };
        var options =  new MapLaunchOptions { Name = "Microsoft Building 25" };

        try
        {
            await Map.OpenAsync(placemark, options);
        }
        catch (Exception ex)
        {
            // No map application available to open or placemark can not be located
        }
    }
}
```

## <a name="extension-methods"></a>Erweiterungsmethoden

Wenn Sie bereits einen Verweis auf ein `Location`- oder `Placemark`-Element haben, können Sie die integrierte Erweiterungsmethode `OpenMapAsync` mit dem optionalen `MapLaunchOptions`-Element verwenden:

```csharp
public class MapTest
{
    public async Task OpenPlacemarkOnMap(Placemark placemark)
    {
        try
        {
            await placemark.OpenMapAsync();
        }
        catch (Exception ex)
        {
            // No map application available to open
        }
    }
}
```

## <a name="directions-mode"></a>Modus „Wegbeschreibung“

Wenn Sie `OpenMapAsync` ohne `MapLaunchOptions` aufrufen, startet die Karte an der angegebenen Position. Optional können Sie eine Navigationsroute ausgehend von der aktuellen Position des Geräts berechnen lassen. Dafür muss `NavigationMode` für `MapLaunchOptions` festgelegt werden.

```csharp
public class MapTest
{
    public async Task NavigateToBuilding25()
    {
        var location = new Location(47.645160, -122.1306032);
        var options =  new MapLaunchOptions { NavigationMode = NavigationMode.Driving };

        await Map.OpenAsync(location, options);
    }
}
```

## <a name="platform-differences"></a>Plattformunterschiede

# <a name="android"></a>[Android](#tab/android)

- `NavigationMode` unterstützt Radfahren, Fahren und Gehen.

# <a name="ios"></a>[iOS](#tab/ios)

- `NavigationMode` unterstützt Fahren, öffentliche Verkehrsmittel und Gehen.

# <a name="uwp"></a>[UWP](#tab/uwp)

- `NavigationMode` unterstützt Fahren, öffentliche Verkehrsmittel und Gehen.

--------------

## <a name="platform-implementation-specifics"></a>Besonderheiten bei der plattformspezifischen Implementierung

# <a name="android"></a>[Android](#tab/android)

Android verwendet das URI-Schema `geo:`, um die Kartenanwendung auf dem Gerät zu starten. Möglicherweise wird der Benutzer aufgefordert, eine vorhandene App auszuwählen, die dieses URI-Schema unterstützt.  Xamarin.Essentials wurde mit Google Maps getestet, da dieser Dienst das Schema unterstützt.

# <a name="ios"></a>[iOS](#tab/ios)

Keine plattformspezifischen Implementierungsangaben.

# <a name="uwp"></a>[UWP](#tab/uwp)

Keine plattformspezifischen Implementierungsangaben.

--------------

## <a name="api"></a>API

- [Kartenquellcode](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/Map)
- [Karten- API-Dokumentation](xref:Xamarin.Essentials.Map)

## <a name="related-video"></a>Zugehörige Videos

> [!Video https://channel9.msdn.com/Shows/XamarinShow/Maps-XamarinEssentials-API-of-the-Week/player]

[!include[](~/essentials/includes/xamarin-show-essentials.md)]
