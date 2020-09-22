---
title: Einführung in ios 14
description: Dieses Dokument enthält eine allgemeine Beschreibung einiger IOS 14-APIs, für die xamarin c#-Bindungen bereitstellt.
ms.prod: xamarin
ms.assetid: 4953216e-472b-4484-9c1e-7263ac537f21
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 09/17/2020
ms.openlocfilehash: e9793617c76813fb68a57213edd8b48529f19ac7
ms.sourcegitcommit: 0c45e3f810947e3d43223aa01bf3e43a0defca65
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/21/2020
ms.locfileid: "90843606"
---
# <a name="introduction-to-ios-14"></a>Einführung in ios 14

Befolgen Sie diese [Anweisungen](~/ios/platform/ios14/get-started.md) , um zu beginnen.

## <a name="new-control-uicolorwell"></a>Neues Steuerelement: uicolorwell

[`UIColorWell`](https://developer.apple.com/documentation/uikit/uicolorwell) ist ein neues UIKit-Steuerelement zum Auswählen von Farben aus einer Auswahl von swatches, mithilfe eines Droppers oder durch manuelles Eingeben von Werten. Das-Steuerelement zeigt eine zirkuläre Farb Schaltfläche an, die beim Tippen eine modale Form

![Uicolorwell](ios14-images/colorwell.png)

```xaml
<ios:UIColorWell
    SelectedColor="{x:Static ios:UIColor.Red}"
    ValueChanged="OnColorChanged" />
```

```csharp
private void OnColorChanged(object sender, EventArgs e)
{
    var colorWell = (UIColorWell)sender; 
    Debug.WriteLine(colorWell.SelectedColor);
}
```

## <a name="modified-controls"></a>Geänderte Steuerelemente

Mehrere Steuerelemente haben Updates erhalten, insbesondere:

- [Uibarbuttonitem](https://developer.apple.com/documentation/uikit/uibarbuttonitem) kann nun eine uimdeu hinzufügen, die als Popup angezeigt wird.
- [UIDatePicker](https://developer.apple.com/documentation/uikit/uidatepicker) unterstützt jetzt mehrere Stile: automatisch (Standard), kompakt, Inline und Rad.
- [Uisplitviewcontroller](https://developer.apple.com/documentation/uikit/uisplitviewcontroller) unterstützt nun drei Spalten: primär, Sekundär und ergänzender.
 
![Vorabrelease der API](~/media/shared/preview.png)

## <a name="embedded-widgetkit-support"></a>Eingebettete widgetkit-Unterstützung

Diese Version des SDK bietet Unterstützung für das Einbetten von widgetkit-Erweiterungen, die in SWIFT geschrieben sind, in die xamarin. IOS-Hauptanwendung. Dies ermöglicht Ihnen das Erstellen von apps mit widgeunterstützung heute.

Mit dieser Methode erstellen Sie eine "Hybrid"-Anwendung, die eine widgeenweiterung mit swiartui erstellt und in eine xamarin. IOS-Anwendung einbettet.

Die Nutzung der widgetkit-Unterstützung erfordert einige manuelle Änderungen an der Projektdatei.

Fügen Sie dem Projekt einen Abschnitt wie den folgenden hinzu:

```xml
<AdditionalAppExtensions Include="$(MSBuildProjectDirectory)/../../native">
     <Name>NativeTodayExtension</Name>
     <BuildOutput Condition="'$(Platform)' == 'iPhone'">build/Debug-iphoneos</BuildOutput>
     <BuildOutput Condition="'$(Platform)' == 'iPhoneSimulator'">build/Debug-iphonesimulator</BuildOutput>
</AdditionalAppExtensions>
```

Ändern Sie den im ersten Link enthaltenen Pfad so, dass er auf das Buildverzeichnis der SWIFT-Benutzeroberflächen Erweiterung verweist.

Es ist möglicherweise hilfreich, einen Projekt relativen Ausgabe Speicherort in Ihrem Xcode-Projekt (Datei → Projekteinstellungen) zu aktivieren, um einen einfacheren Pfad zu finden:

![Xcode-Einstellungen](ios14-images/xcode-settings.png)

Diese [Beispielanwendung](https://github.com/chamons/xamarin-ios-swift-extension/blob/master/App/TestApplication/TestApplication.csproj#L143) verwendet die JSON-Serialisierung zum Übertragen von Daten aus einer xamarin. IOS-app in ein beispielwidget für die Anzeige.

Die Benutzer, die an widgetkit interessiert sind, werden eingeladen, Ihr [Feedback hier](https://github.com/xamarin/xamarin-macios/issues/8933)bereitzustellen.

## <a name="related-links"></a>Verwandte Links

- [Anmerkungen zu dieser Version von xamarin. IOS 14](/xamarin/ios/release-notes/14/14.0)
- [Uicolorwell-Dokumentation](https://developer.apple.com/documentation/uikit/uicolorwell)
