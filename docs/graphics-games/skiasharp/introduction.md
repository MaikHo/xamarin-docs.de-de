---
title: SkiaSharp-plattformunabhängige-Beispiele
description: Dieses Dokument enthält eine kurze Einführung in SkiaSharp Kernkonzepte. Insbesondere erläutert er abrufen, und klicken Sie auf eine SKCanvas zeichnen.
ms.prod: xamarin
ms.techonology: xamarin-skiasharp
ms.assetid: 19506F08-2603-465E-A806-6BD01638DE90
author: davidbritch
ms.author: dabritch
ms.date: 10/03/2018
ms.openlocfilehash: 4d0e57b98a479112b9fdf4f9c503418f3966cc73
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61158888"
---
# <a name="skiasharp-platform-independent-examples"></a>SkiaSharp-plattformunabhängige-Beispiele

_Dies bietet eine kurze plattformunabhängige Einführung in die Konzepte hinter der SkiaSharp_

SkiaSharp bietet eine umfassende und leistungsfähige 2D-Grafik-API, die zum Rendern in das 2D Puffer verwendet werden kann.  Sie können diese verwenden, implementieren Sie benutzerdefinierte Elemente der Benutzeroberfläche und Direct2D-Grafiken, die in Ihrer Anwendung integriert werden können. SkiaSharp ist eine .NET an der [Skia](https://skia.org) Bibliothek und erbt die Funktionen und die Leistungsfähigkeit dieser Bibliothek.

Die Bibliothek ist derzeit als eine plattformübergreifende verfügbar [NuGet-Paket](https://www.nuget.org/packages/SkiaSharp), Sie können sie zu Ihrem Projekt hinzufügen, indem Sie den NuGet-Verweis hinzugefügt haben.

Um zu zeichnen, Ihren Code erstellt ein `SkCanvas` beschreibt die Oberfläche, in denen die Zeichenoperationen werden durchgeführt.

## <a name="obtaining-an-skcanvas"></a>Abrufen einer SKCanvas

```csharp
using (var surface = SKSurface.Create (width: 640, height: 480, SKImageInfo.PlatformColorType, SKAlphaType.Premul)) {
    SKCanvas myCanvas = surface.Canvas;

    // Your drawing code goes here.
}
```

## <a name="drawing-on-skcanvas"></a>Die Zeichnung SKCanvas

Die `SKCanvas` verwendet ein zeichnen Modell ähnlich wie ein im Geiste anderer Modelle, dass Sie möglicherweise kennen, Farben mit einer optionalen transparenzkanal verwendet und können Zeichnen von Linien, Bögen, Text und Bildern.

Im folgenden sind nur einige der viele verschiedene Dinge, die mit SkiaSharp ausgeführt werden können.  In den Beispielen unten die Variable `canvas` ist vom Typ SKCanvas.

### <a name="drawing-xamagon"></a>Zeichnen Xamagon

In diesem Beispiel zeichnet die Xamarin Logo der Xamagon:

```csharp
// clear the canvas / fill with white
canvas.Clear (SKColors.White);

// set up drawing tools
using (var paint = new SKPaint ()) {
  paint.IsAntialias = true;
  paint.Color = new SKColor (0x2c, 0x3e, 0x50);
  paint.StrokeCap = SKStrokeCap.Round;

  // create the Xamagon path
  using (var path = new SKPath ()) {
    path.MoveTo (71.4311121f, 56f);
    path.CubicTo (68.6763107f, 56.0058575f, 65.9796704f, 57.5737917f, 64.5928855f, 59.965729f);
    path.LineTo (43.0238921f, 97.5342563f);
    path.CubicTo (41.6587026f, 99.9325978f, 41.6587026f, 103.067402f, 43.0238921f, 105.465744f);
    path.LineTo (64.5928855f, 143.034271f);
    path.CubicTo (65.9798162f, 145.426228f, 68.6763107f, 146.994582f, 71.4311121f, 147f);
    path.LineTo (114.568946f, 147f);
    path.CubicTo (117.323748f, 146.994143f, 120.020241f, 145.426228f, 121.407172f, 143.034271f);
    path.LineTo (142.976161f, 105.465744f);
    path.CubicTo (144.34135f, 103.067402f, 144.341209f, 99.9325978f, 142.976161f, 97.5342563f);
    path.LineTo (121.407172f, 59.965729f);
    path.CubicTo (120.020241f, 57.5737917f, 117.323748f, 56.0054182f, 114.568946f, 56f);
    path.LineTo (71.4311121f, 56f);
    path.Close ();

    // draw the Xamagon path
    canvas.DrawPath (path, paint);
  }
}
```

### <a name="drawing-text"></a>Zeichnen von Text

```csharp
// clear the canvas / fill with white
canvas.DrawColor (SKColors.White);

// set up drawing tools
using (var paint = new SKPaint ()) {
  paint.TextSize = 64.0f;
  paint.IsAntialias = true;
  paint.Color = new SKColor (0x42, 0x81, 0xA4);
  paint.IsStroke = false;

  // draw the text
  canvas.DrawText ("Skia", 0.0f, 64.0f, paint);
}
```

### <a name="drawing-bitmaps"></a>Zeichnen von bitmaps

```csharp
Stream fileStream = File.OpenRead ("MyImage.png");

// clear the canvas / fill with white
canvas.DrawColor (SKColors.White);

// decode the bitmap from the stream
using (var stream = new SKManagedStream(fileStream))
using (var bitmap = SKBitmap.Decode(stream))
using (var paint = new SKPaint()) {
  canvas.DrawBitmap(bitmap, SKRect.Create(Width, Height), paint);
}
```

### <a name="drawing-with-image-filters"></a>Zeichnen mit Bildfilter

```csharp
Stream fileStream = File.OpenRead ("MyImage.png"); // open a stream to an image file

// clear the canvas / fill with white
canvas.DrawColor (SKColors.White);

// decode the bitmap from the stream
using (var stream = new SKManagedStream(fileStream))
using (var bitmap = SKBitmap.Decode(stream))
using (var paint = new SKPaint()) {
  // create the image filter
  using (var filter = SKImageFilter.CreateBlur(5, 5)) {
    paint.ImageFilter = filter;

    // draw the bitmap through the filter
    canvas.DrawBitmap(bitmap, SKRect.Create(width, height), paint);
  }
}
```

## <a name="more-information"></a>Weitere Informationen

Weitere Informationen zum Verwenden von SkiaSharp befinden sich die [-API-Dokumentation](https://docs.microsoft.com/dotnet/api/skiasharp)
