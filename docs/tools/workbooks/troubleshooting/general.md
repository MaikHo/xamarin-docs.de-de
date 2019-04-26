---
title: Bekannte Probleme und Problemumgehungen
description: Dieses Dokument beschreibt die bekannten Probleme und problemumgehungen für Xamarin Workbooks. Es wird erläutert, CultureInfo-Probleme, Probleme mit JSON und mehr.
ms.prod: xamarin
ms.assetid: 495958BA-C9C2-4910-9BAD-F48A425208CF
author: lobrien
ms.author: laobri
ms.date: 03/30/2017
ms.openlocfilehash: 221ed97db17da62f513448b6c85d4df205a7cbaf
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61268883"
---
# <a name="known-issues--workarounds"></a>Bekannte Probleme und Problemumgehungen

## <a name="persistence-of-cultureinfo-across-cells"></a>Persistenz der CultureInfo in Zellen

Festlegen von `System.Threading.CurrentThread.CurrentCulture` oder `System.Globalization.CultureInfo.CurrentCulture` behält nicht über die Zellen der Arbeitsmappe für Mono-basierte Arbeitsmappen-Ziele (Mac, iOS und Android) aufgrund einer [Fehler in der Mono- `AppContext.SetSwitch` ] [ appcontext-bug] Implementierung .

### <a name="workarounds"></a>Problemumgehung

* Legen Sie die Domäne-lokalen `DefaultThreadCurrentCulture`:
```csharp
using System.Globalization;
CultureInfo.DefaultThreadCurrentCulture = new CultureInfo("de-DE")
```

* Oder Update Arbeitsmappen 1.2.1 oder höher, werden die Zuweisungen zu schreiben `System.Threading.CurrentThread.CurrentCulture` und `System.Globalization.CultureInfo.CurrentCulture` für das gewünschte Verhalten (umgehen von Mono / Fehler) bereitstellen.

## <a name="unable-to-use-newtonsoftjson"></a>Kann nicht verwendet "newtonsoft.JSON"

### <a name="workaround"></a>Problemumgehung

* Aktualisieren Sie auf Arbeitsmappen 1.2.1, wodurch Newtonsoft.Json 9.0.1 installiert werden.
  Arbeitsmappen 1.3, unterstützt derzeit im Alphakanal, Version 10 und höher.

### <a name="details"></a>Details

"Newtonsoft.JSON" 10 wurde veröffentlicht, die tatsächlich von der Abhängigkeit Microsoft.CSharp, wodurch ein Konflikt mit der Arbeitsmappen der Version ausgeliefert wird, zur Unterstützung `dynamic`. Dies ist in der Vorschauversion von Arbeitsmappen 1.3 behoben, aber vorerst wir haben daran gearbeitet Umgehung dieses Problems von angehefteten "newtonsoft.JSON" speziell für Version 9.0.1.

NuGet-Pakete, die explizit je nach "newtonsoft.JSON" 10 oder höher werden nur Arbeitsmappen 1.3, derzeit im Alphakanal unterstützt.

## <a name="code-tooltips-are-blank"></a>Code-QuickInfos sind leer

Es gibt eine [Fehler in dem Monaco-Editor] [ monaco-bug] in Safari/WebKit, die in der Mac-Workbooks-app verwendet wird, führt, die Code-QuickInfos Rendering ohne Text.

![](general-images/monaco-signature-help-bug.png)

### <a name="workaround"></a>Problemumgehung

* Die QuickInfo auf, wenn es angezeigt wird, wird den Text, der Rendering erzwungen.

* Oder aktualisieren Sie die Arbeitsmappen 1.2.1 oder höher

[appcontext-bug]: https://bugzilla.xamarin.com/show_bug.cgi?id=54448
[monaco-bug]: https://github.com/Microsoft/monaco-editor/issues/408

## <a name="skiasharp-renderers-are-missing-in-workbooks-13"></a>SkiaSharp-Renderer werden in Arbeitsmappen 1.3 fehlt

Arbeitsmappen 1.3 ab, haben wir die SkiaSharp-Renderern, die wir haben in Arbeitsmappen 0.99.0, zugunsten von SkiaSharp die Renderer bereitgestellt, indem enthalten unsere [SDK](~/tools/workbooks/sdk/index.md).

### <a name="workaround"></a>Problemumgehung

* Aktualisieren Sie SkiaSharp, auf die neueste Version in NuGet. Zum Zeitpunkt der Verfassung ist dies 1.57.1.

## <a name="related-links"></a>Verwandte Links

- [Melden von Fehlern](~/tools/workbooks/install.md#reporting-bugs)
