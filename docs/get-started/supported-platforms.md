---
title: Von Xamarin.Forms unterstützte Plattformen
description: Plattform- und Entwicklungssystemanforderungen für Xamarin.Forms.
ms.prod: xamarin
ms.assetid: eecaf6a5-567c-49b2-ac83-2a195596c5bf
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 01/22/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: f93af19587cf962ac0c852599157261a087dadbc
ms.sourcegitcommit: 32d2476a5f9016baa231b7471c88c1d4ccc08eb8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2020
ms.locfileid: "84197543"
---
# <a name="xamarinforms-supported-platforms"></a>Von Xamarin.Forms unterstützte Plattformen

Xamarin.Forms-Anwendungen können für die folgenden Betriebssysteme geschrieben werden:

- iOS 9 oder höher
- Android 4.4 (API 19) oder höher ([weitere Informationen](#android-platform-support)). Als mindestens erforderliche API wird jedoch Android 5.0 (API 21) empfohlen. Damit ist die vollständige Kompatibilität mit allen Android-Unterstützungsbibliotheken gewährleistet, wobei die meisten Android-Geräte weiterhin unterstützt werden.
- Universelle Windows-Plattform (UWP) für Windows 10

In Visual Studio können Xamarin.Forms-Apps für iOS, Android und die Universelle Windows-Plattform (UWP) entwickelt werden. Allerdings wird ein netzwerkfähiger Mac für die iOS-Entwicklung mit der neuesten Version von Xcode und der von Apple angegebenen mindestens erforderlichen Version von macOS benötigt. Weitere Informationen finden Sie unter [Windows-Anforderungen](~/cross-platform/get-started/requirements.md#windows-requirements).

In Visual Studio für Mac können Xamarin.Forms-Apps für iOS und Android entwickelt werden. Weitere Informationen finden Sie unter [macOS-Anforderungen](~/cross-platform/get-started/requirements.md#macos-requirements).

> [!NOTE]
> Für die Entwicklung von Apps mit Xamarin.Forms sollten Sie mit [.NET Standard](~/cross-platform/app-fundamentals/net-standard.md) vertraut sein.

## <a name="additional-platform-support"></a>Unterstützung für zusätzliche Plattformen

Xamarin.Forms unterstützt neben iOS, Android und Windows auch noch weitere Plattformen:

- Samsung Tizen
- macOS 10.13 und höher
- GTK#
- WPF

Der Status dieser Plattformen ist auf dem [GitHub-Wiki zur Plattformunterstützung für Xamarin.Forms](https://github.com/xamarin/Xamarin.Forms/wiki/Platform-Support)abrufbar.

## <a name="android-platform-support"></a>Android-Plattformunterstützung

Auf Ihren Geräten sollten die neuesten Android SDK Tools und die entsprechende Android-API-Plattform installiert sein. Sie können mithilfe des [Android SDK-Managers](~/android/get-started/installation/android-sdk.md) ein Update auf die neuesten Versionen ausführen.

Außerdem **muss** die Ziel-/Kompilierversion für Android-Projekte auf *Zuletzt installierte Plattform verwenden* festgelegt werden. Die Mindestversion kann jedoch auf API 19 festgelegt werden, damit die Unterstützung von Geräten mit Android 4.4 und höher weiterhin möglich ist. Diese Werte werden in den **Projektoptionen** festgelegt:

# <a name="visual-studio"></a>[Visual Studio](#tab/windows)

**Projektoptionen > Anwendung > Anwendungseigenschaften**

![Buildoptionen für Android in Visual Studio](requirements-images/options-android-vs-sml.png)

# <a name="visual-studio-for-mac"></a>[Visual Studio für Mac](#tab/macos)

**Erstellen > Allgemein**

![Auswählen des neuesten Zielframeworks](requirements-images/options-general-sml.png)

**Erstellen > Android-Anwendung**

![Auswählen der mindestens erforderlichen Versionen und Android-Zielversionen für Ihre App](requirements-images/options-android-sml.png)

-----

## <a name="deprecated-platforms"></a>Veraltete Plattformen

Folgende Plattformversionen werden nicht unterstützt, wenn Sie Xamarin.Forms 3.0 oder höher verwenden:

- *Windows 8.1 / Windows Phone 8.1 WinRT*
- *Windows Phone 8 Silverlight*
