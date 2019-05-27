---
title: Systemanforderungen
description: In diesem Artikel werden die Systemanforderungen zum Erstellen von Apps mit Xamarin auf Mac- und Windows-Computern aufgeführt. Außerdem sind Links zu Installationsanweisungen enthalten.
ms.prod: xamarin
ms.assetid: dd344d57-18e2-42a5-8c15-3f5be4123c72
author: conceptdev
ms.author: crdun
ms.date: 04/26/2018
ms.openlocfilehash: 3f51b61cd7dcc3c7b17881b3576aa2c22a45e470
ms.sourcegitcommit: be9658de032f3893741261f16162a664952ce178
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2019
ms.locfileid: "64987056"
---
# <a name="system-requirements"></a>Systemanforderungen

Xamarin-Produkte sind abhängig von den Plattform SDKs von Apple und Google, um iOS oder Android als Ziel verwenden zu können, sodass unsere Systemanforderungen ihren entsprechen. Auf dieser Seite werden die Systemkompatibilität für die Xamarin-Plattform und für die empfohlene Entwicklungsumgebung sowie die SDK-Versionen erläutert.

Weitere Informationen zum Abrufen der Software und der erforderlichen SDKs finden Sie unter [installation instructions (Installationsanweisungen)](#installation-instructions).

## <a name="development-environments"></a>Entwicklungsumgebungen

Diese Tabelle zeigt, welche Plattformen mit verschiedenen Entwicklungstool- und Betriebssystemkombinationen erstellt werden können:

[!include[](~/cross-platform/includes/development-environment.md)]

> [!NOTE]
> Zur Entwicklung von iOS auf Windows-Computern muss für die Remotekompilierung und das Debuggen [ein Mac-Computer im Netzwerk verfügbar sein](~/ios/get-started/installation/windows/connecting-to-mac/index.md). Sie können Visual Studio auch innerhalb einer Windows-VM auf einem Mac-Computer ausführen.

## <a name="macos-requirements"></a>macOS-Anforderungen

Die Verwendung eines Mac-Computers für die Xamarin-Entwicklung erfordert folgende Software-/SDK-Versionen. Überprüfen Sie Ihre Betriebssystemversion, und folgen Sie den Anweisungen für den [Xamarin-Installer](#installation-instructions).

[!include[](~/cross-platform/includes/macos-requirements.md)]

> [!NOTE]
> Xcode kann auf [developer.apple.com](https://developer.apple.com/xcode/download/) oder über den Mac App Store installiert (und aktualisiert) werden.

### <a name="testing--debugging-on-macos"></a>Testen und Debuggen unter macOS

- Mobile Xamarin-Anwendungen können über USB für Tests und das Debuggen auf physischen Geräten bereitgestellt werden (Apple Watch-Apps werden zunächst auf dem gekoppelten iPhone bereitgestellt).
- Xamarin.Mac-Apps können direkt auf dem Entwicklungscomputer getestet werden.

[!include[](~/cross-platform/includes/macos-testing.md)]

> [!WARNING]
> Xamarin.Mac 4.8 unterstützt nur macOS 10.9 (Mavericks) oder höher.
> Ältere Versionen von Xamarin.Mac unterstützen macOS 10.7 oder höher, aber diese älteren Versionen von MacOS verfügen nicht über ausreichende TLS-Infrastruktur zur Unterstützung von TLS 1.2. Für macOS 10.7 oder macOS 10.8 sollten Sie Xamarin.Mac 4.6 oder niedriger verwenden.

## <a name="windows-requirements"></a>Windows-Anforderungen

Die Verwendung eines Windows-Computers für die Xamarin-Entwicklung erfordert folgende Software-/SDK-Versionen.
Überprüfen Sie Ihre Betriebssystemversion und bestätigen Sie, dass Sie keine *Express*-Version von Visual Studio haben. Falls doch, sollten Sie darüber nachdenken, auf die *Community*-Edition zu aktualisieren.
Der Visual Studio 2019-Installer bzw. der Visual Studio 2017-Installer umfasst eine Option zum automatischen Installieren von Xamarin (die Workload **Mobile Entwicklung mit .NET**).

[!include[](~/cross-platform/includes/windows-requirements.md)]

> [!NOTE]
> - Xamarin für Visual Studio unterstützt jede Version von Visual Studio 2019 oder von Visual Studio 2017 (Community, Professional und Enterprise).
> - Die Entwicklung von Xamarin.Forms-Apps für die universelle Windows-Plattform (UWP) erfordert Windows 10 mit Visual Studio 2017. Visual Studio 2019 wird empfohlen.

### <a name="testing--debugging-on-windows"></a>Testen und Debuggen unter Windows

Mobile Xamarin-Anwendungen können über USB oder drahtlos für Tests und das Debuggen auf physischen Geräten bereitgestellt werden (iOS-Geräte müssen mit dem Mac-Computer verbunden sein, nicht mit dem Computer, auf dem Visual Studio ausgeführt wird).

[!include[](~/cross-platform/includes/windows-testing.md)]

## <a name="installation-instructions"></a>Installationsanweisungen

Das neueste Xamarin-Release für macOS kann mit [Visual Studio für Mac](https://docs.microsoft.com/visualstudio/mac/installation) heruntergeladen werden. Folgen Sie für Windows den [Installationsanweisungen für Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).

Eine vollständige Liste unserer aktuellen Produktversionen ist auf der [Seite für die aktuellen Releases](https://developer.xamarin.com/releases/current/) verfügbar. Dort sind auch die einzelnen Produktversionen (und Links zu den Anmerkungen zur Version) für unsere Beta- und Alphakanäle erklärt.

Spezifische Anleitungen für die [Installation](~/get-started/installation/index.md) auf den einzelnen Plattformen finden Sie hier:

- [Xamarin.iOS](~/ios/get-started/installation/index.md)
- [Xamarin.Android](~/android/get-started/installation/index.md)
- [Xamarin.Mac](~/mac/get-started/installation.md)

Dort finden Sie auch zusätzliche Informationen über [Xamarin.Forms-Anforderungen und unterstützte Plattformen](~/get-started/requirements.md).

## <a name="related-links"></a>Verwandte Links

- [Xamarin herunterladen](https://visualstudio.microsoft.com/xamarin/)
- [Xamarin.Forms-Versionshinweise](/xamarin/xamarin-forms/release-notes/)
- [Xamarin.Android-Versionshinweise](/xamarin/android/release-notes/)
- [Xamarin.iOS-Versionshinweise](/xamarin/ios/release-notes/)
