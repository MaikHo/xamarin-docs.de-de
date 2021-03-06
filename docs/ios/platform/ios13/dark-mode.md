---
title: Dunkler Modus in xamarin. IOS
description: Der dunkle Modus ist eine neue systemweite Option für helles und dunkles Design. IOS-Benutzer können jetzt ein Design auswählen oder es IOS gestatten, die Darstellung dynamisch zu ändern.
ms.prod: xamarin
ms.assetid: 4F44446E-36B6-4743-9B4D-32278D1D3D66
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 08/28/2019
ms.openlocfilehash: be487ab839e2fb4d21b85719a56dc34303317a5f
ms.sourcegitcommit: 09bc69d7119a04684c9e804c5cb113b8b1bb7dfc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71206386"
---
# <a name="dark-mode-in-xamarinios"></a>Dunkler Modus in xamarin. IOS

Der dunkle Modus ist eine systemweite Option für helle und dunkle Designs. IOS-Benutzer können jetzt das Design auswählen oder es IOS gestatten, die Darstellung basierend auf der Umgebung und der Tageszeit dynamisch zu ändern.

In diesem Dokument wird der dunkle Modus eingeführt und der dunkle Modus in ios 13-Anwendungen unterstützt.

## <a name="requirements"></a>Anforderungen

Der dunkle Modus erfordert IOS 13 und Xcode 11, xamarin. IOS 12,99 und Visual Studio 2019 oder Visual Studio 2019 für Mac mit Xcode 11-Unterstützung.

## <a name="turning-on-dark-mode"></a>Aktivieren des dunklen Modus

Apple stellt ein Entwicklermenü in iOS 13 bereit, um zwischen dunklen und hellen Modi zu wechseln. Öffnen Sie im iOS 13-Simulator die **Einstellungen** , und wählen Sie den Abschnitt **Entwickler** aus, und scrollen Sie zum Schalter **dunkle** Darstellung. Die Änderung wird in der gesamten Simulatorumgebung reflektiert:

![Aktivieren des dunklen Modus](dark-mode-images/LightAndDark_DeveloperSetting.png)

## <a name="assets-for-light-and-dark-modes"></a>Assets für helle und dunkle Modi

Der Asset-Katalog in Visual Studio unterstützt jetzt optionale Bilder und Farben für jeden Darstellungs Modus: Universell, dunkel und hell. Wenn Sie Ihre Bilder und Farben auf diese Weise definieren, wählt IOS automatisch das passende Bild und die gewünschte Farbe aus.

Öffnen Sie die Datei **Assets.xcassets** in Ihrem iOS-Projekt, und fügen Sie einen neuen Bildsatz hinzu. Beachten Sie, dass Sie universelle, dunkle und helle Bilder in jeder der Zielauflösungen angeben können. Im folgenden Screenshot wird ein Bild für dunkel und hell mit dem Namen "MicrosoftLogo" angezeigt:

![Assets für helle und dunkle Modi](dark-mode-images/LightAndDark_AssetCatalog2.png)

Die Datei **Assets.xcassets** enthält auch Einträge für **BackgroundColor** und **Titlecolor**, bei denen es sich um Farbdefinitionen handelt. Diese Farben sind jetzt nach Namen verfügbar, die in der gesamten Anwendung verwendet werden. **BackgroundColor** wurde dem Hintergrund der Ansicht und **Titlecolor** der Bezeichnung zugewiesen, wie in diesem Screenshot gezeigt:

![Assets für helle und dunkle Modi](dark-mode-images/LightAndDark_01.png)

## <a name="dynamic-system-colors"></a>Dynamische Systemfarben

Apple hat neue Semantik Farben eingeführt, die ihre Darstellung dynamisch basierend auf der neuen Einstellung für den dunklen Modus anpassen.

## <a name="summary"></a>Zusammenfassung

In diesem Artikel wurde der dunkle Modus für IOS und die Angabe von Bildern und Farben für die einzelnen Modi mithilfe des Ressourcen Katalogs eingeführt.

## <a name="related-links"></a>Verwandte Links

- [Entwurfs Richtlinien für den dunklen Modus](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/dark-mode/)
- [Semantik Farben](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/color/#dynamic-system-colors)
