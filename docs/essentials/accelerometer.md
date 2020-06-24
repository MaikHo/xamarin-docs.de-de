---
title: 'Xamarin.Essentials: Beschleunigungsmesser'
description: Mit der Accelerometer-Klasse in Xamarin.Essentials können Sie den Sensor für die Beschleunigungsmessung des Geräts überwachen, der die Beschleunigung des Geräts im dreidimensionalen Raum angibt.
ms.assetid: 97883573-F0D9-4854-AC7C-A654814401C5
author: jamesmontemagno
ms.author: jamont
ms.date: 04/02/2019
ms.custom: video
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: f3d7b313039e66294a0095fd34a2caa6689cef2e
ms.sourcegitcommit: 32d2476a5f9016baa231b7471c88c1d4ccc08eb8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2020
ms.locfileid: "84802535"
---
# <a name="xamarinessentials-accelerometer"></a>Xamarin.Essentials: Beschleunigungsmesser

Mit der **Accelerometer**-Klasse können Sie den Sensor für die Beschleunigungsmessung des Geräts überwachen, der die Beschleunigung des Geräts im dreidimensionalen Raum angibt.

## <a name="get-started"></a>Erste Schritte

[!include[](~/essentials/includes/get-started.md)]

## <a name="using-accelerometer"></a>Verwenden der Accelerometer-Klasse

Fügen Sie in Ihrer Klasse einen Verweis auf Xamarin.Essentials hinzu:

```csharp
using Xamarin.Essentials;
```

Accelerometer ruft die Methoden `Start` und `Stop` auf, um auf Änderungen der Beschleunigung zu lauschen. Änderungen werden über das `ReadingChanged`-Ereignis zurück gesendet. Sie können sie z.B. wie folgt verwenden:

```csharp

public class AccelerometerTest
{
    // Set speed delay for monitoring changes.
    SensorSpeed speed = SensorSpeed.UI;

    public AccelerometerTest()
    {
        // Register for reading changes, be sure to unsubscribe when finished
        Accelerometer.ReadingChanged += Accelerometer_ReadingChanged;
    }

    void Accelerometer_ReadingChanged(object sender, AccelerometerChangedEventArgs e)
    {
        var data = e.Reading;
        Console.WriteLine($"Reading: X: {data.Acceleration.X}, Y: {data.Acceleration.Y}, Z: {data.Acceleration.Z}");
        // Process Acceleration X, Y, and Z
    }

    public void ToggleAccelerometer()
    {
        try
        {
            if (Accelerometer.IsMonitoring)
              Accelerometer.Stop();
            else
              Accelerometer.Start(speed);
        }
        catch (FeatureNotSupportedException fnsEx)
        {
            // Feature not supported on device
        }
        catch (Exception ex)
        {
            // Other error has occurred.
        }
    }
}
```

Ergebnisse des Beschleunigungsmessers werden in G angegeben. Mit der Einheit G wird eine Gravitationskraft angegeben, die der Kraft des Gravitationsfelds der Erde entspricht (9,81 m/s^2).

Das Koordinatensystem wird relativ zum Bildschirm des Mobilgeräts in seiner Standardausrichtung definiert. Die Achsen bleiben unverändert, wenn sich die Bildschirmausrichtung des Geräts ändert.

Die X-Achse ist horizontal und zeigt nach rechts. Die Y-Achse ist vertikal und zeigt nach oben. Die Z-Achse verläuft abgewandt von der Vorderseite des Bildschirms. In diesem System sind Koordinaten hinter dem Bildschirm negative Z-Werte.

Beispiele:

- Wenn das Gerät flach auf einem Tisch liegt und auf seiner linken Seite nach rechts geschoben wird, ist der X-Beschleunigungswert positiv.

- Wenn das Gerät flach auf einem Tisch liegt, ist der Beschleunigungswert +1,00 G oder (+9,81 m/s^2), was der Beschleunigung des Geräts (0 m/s^2) abzüglich der Gravitationskraft (–9,81 m/s^2) entspricht, was in G normiert wird.

- Wenn das Gerät flach auf einem Tisch liegt und nach oben mit einer Beschleunigung von A m/s^2 bewegt wird, entspricht der Beschleunigungswert A+9,81, was der Beschleunigung des Geräts (+A m/s^2) minus der Gravitationskraft (–9,81 m/s^2) entspricht, was in G normiert wird.

[!include[](~/essentials/includes/sensor-speed.md)]

## <a name="api"></a>API

- [Quellcode für einen Beschleunigungsmesser](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/Accelerometer)
- [Dokumentation für Beschleunigungsmesser-API](xref:Xamarin.Essentials.Accelerometer)

## <a name="related-video"></a>Zugehörige Videos

> [!Video https://channel9.msdn.com/Shows/XamarinShow/Accelerometer-XamarinEssentials-API-of-the-Week/player]

[!include[](~/essentials/includes/xamarin-show-essentials.md)]
