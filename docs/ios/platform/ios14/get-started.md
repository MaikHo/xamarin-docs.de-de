---
title: Einstieg in ios 14
description: In diesem Dokument wird beschrieben, wie Sie einrichten, um IOS 14-apps mit xamarin zu erstellen. Darin wird erläutert, wie Sie Xcode 12 herunterladen und Visual Studio für Mac aktualisieren.
ms.prod: xamarin
ms.assetid: 0d721b4b-86bd-495a-8c0f-1f2f9fd6855e
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 09/17/2020
ms.openlocfilehash: 1bf77ca71d5fda945c81ac3ac6b338eec0164a76
ms.sourcegitcommit: 0c45e3f810947e3d43223aa01bf3e43a0defca65
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/21/2020
ms.locfileid: "90843610"
---
# <a name="get-started-with-ios-14"></a>Einstieg in ios 14

In diesem Dokument wird beschrieben, wie Sie mit dem Entwickeln von xamarin-apps beginnen, die mit Xcode 12 für IOS 14 veröffentlichte APIs aufzurufen. Für die Verwendung der Vorschau ist macOS Catalina 10.15.4 oder höher erforderlich.

## <a name="download-and-install"></a>Herunterladen und Installieren

1. **Installieren von Xcode 12** – registrierte Apple-Entwickler können die neueste Version von Xcode 12 aus dem Apple- [Entwickler Portal](https://developer.apple.com/download/) oder dem **App Store**herunterladen und installieren.

2. **Führen Sie Xcode 12** – Ausführen von Xcode 12 vor dem Aktualisieren und Ausführen von Visual Studio für Mac oder Visual Studio 2019 aus, da es einige Tools installiert, die xamarin benötigt.

3. **Update Visual Studio für Mac und Visual Studio 2019** – stellen Sie sicher, dass Sie über die neueste stabile Version von xamarin verfügen.

4. Optionale **Installieren von IOS 14 auf Ihren IOS-Geräten** – für Gerätetests von apps, die mit Xcode 12 eingeführte APIs verwenden, können registrierte Apple-Entwickler das Betriebssystem auf Ihren Geräten [herunterladen](https://developer.apple.com/download) und installieren. 

   > [!TIP]
   > Auch wenn Ihre APP keine neuen APIs verwendet, stellen Sie sicher, dass Sie mit den neuesten Xcode 12-sdys erstellt werden, und testen Sie Sie, um sicherzustellen, dass alles wie erwartet funktioniert. Wenn eine APP keine neuen APIs aufruft, können Sie Sie mit diesen neuen sdchen neu kompilieren und auf Geräten testen, für die noch kein Upgrade auf das neue Betriebssystem durchgeführt wurde.
   >
   > Bevor Sie Ihre Geräte auf die neuesten Betriebssystemversionen von Apple aktualisieren, um Ihre xamarin-apps zu testen, stellen Sie Folgendes sicher:
   >
   > - Lesen Sie die Anmerkungen zu dieser [Version](https://developer.apple.com/download/) für die Betriebssystemupdates.

## <a name="related-links"></a>Verwandte Links

- [XCode herunterladen](https://developer.apple.com/download/)
- [Xamarin.iOS release notes (Xamarin.iOS-Versionshinweise)](/xamarin/ios/release-notes/14/14.0)
- [Anmerkungen zu dieser Version von Xcode 12](https://developer.apple.com/documentation/xcode-release-notes/xcode-12-release-notes)
