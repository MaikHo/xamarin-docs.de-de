---
title: 'Xamarin.Essentials: Einheitenkonverter'
description: Die Klasse „UnitConverters“ in Xamarin.Essentials stellt mehrere Einheitenkonverter bereit, die Entwickler mit Xamarin.Essentials nutzen können.
ms.assetid: 35DE2704-E730-4337-9476-66CD53376943
author: jamesmontemagno
ms.author: jamont
ms.date: 03/13/2019
ms.openlocfilehash: be560a156647274932265597ae5b83f22255d061
ms.sourcegitcommit: 1dd7d09b60fcb1bf15ba54831ed3dd46aa5240cb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2019
ms.locfileid: "70120134"
---
# <a name="xamarinessentials-unit-converters"></a>Xamarin.Essentials: Einheitenkonverter

Die Klasse **UnitConverters** in Xamarin.Essentials stellt mehrere Einheitenkonverter bereit, die Entwickler mit Xamarin.Essentials nutzen können.

## <a name="get-started"></a>Erste Schritte

[!include[](~/essentials/includes/get-started.md)]

## <a name="using-unit-converters"></a>Verwenden von Einheitenkonvertern

Fügen Sie Ihrer Klasse einen Verweis auf Xamarin.Essentials hinzu:

```csharp
using Xamarin.Essentials;
```

Alle Einheitenkonverter stehen über die statische Klasse `UnitConverters` in Xamarin.Essentials zur Verfügung. Beispielsweise können Sie mühelos Fahrenheit in Celsius konvertieren.

```csharp
var celcius = UnitConverters.FahrenheitToCelsius(32.0);
```

Es folgt eine Liste der verfügbaren Konvertierungen:

- FahrenheitToCelsius
- CelsiusToFahrenheit
- CelsiusToKelvin
- KelvinToCelsius
- MilesToMeters
- MilesToKilometers
- KilometersToMiles
- DegreesToRadians
- RadiansToDegrees
- DegreesPerSecondToRadiansPerSecond
- RadiansPerSecondToDegreesPerSecond
- DegreesPerSecondToHertz
- RadiansPerSecondToHertz
- HertzToDegreesPerSecond
- HertzToRadiansPerSecond
- KilopascalsToHectopascals
- HectopascalsToKilopascals
- KilopascalsToPascals
- HectopascalsToPascals
- AtmospheresToPascals
- PascalsToAtmospheres
- CoordinatesToMiles
- CoordinatesToKilometers

## <a name="api"></a>API

- [Unit Converters source code (Quellcode für den Einheitenkonverter)](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Types/UnitConverters.shared.cs)
- [Unit Converters API documentation (Dokumentation der Einheitenkonverter-API)](xref:Xamarin.Essentials.UnitConverters)
