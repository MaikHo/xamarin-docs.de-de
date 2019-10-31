---
title: Attribut „Debuggable“
ms.prod: xamarin
ms.assetid: 1ABF90F1-6A70-45AE-9271-D90DC42807D0
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 02/05/2018
ms.openlocfilehash: 55de652363cb761e730d2d92f66a14a941899ca2
ms.sourcegitcommit: 2fbe4932a319af4ebc829f65eb1fb1816ba305d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/29/2019
ms.locfileid: "73028115"
---
# <a name="debuggable-attribute"></a>Attribut „Debuggable“

Um das Debuggen zu ermöglichen, unterstützt Android das Java Debug Wire Protocol (JDWP). Dies ist eine Technologie, die es Tools wie adb ermöglicht, mit einer JVM zu kommunizieren. Während JDQP während der Entwicklung wichtig ist, sollte es vor der Veröffentlichung der Anwendung deaktiviert werden.

JDWP kann dem Wert des `android:debuggable`-Attributs in einer Android-Anwendung entsprechen. Xamarin.Android bietet die folgenden Möglichkeiten, dieses Attribut festzulegen:

1. Erstellen einer`AndroidManifext.xml`-Datei und Festlegen des `android:debuggable`-Attributs
2. Einschließen des `ApplicationAttribute` in einer `.CS`-Datei, wie hier dargestellt: `[assembly: Application(Debuggable=false)]`.

Wenn jeweils `AndroidManifest.xml` und `ApplicationAttribute` vorhanden sind, hat der Inhalt von `AndroidManifest.xml` Priorität vor dem, was durch `ApplicationAttribute` angegeben wird.

Wenn weder `AndroidManifest.xml` noch `ApplicationAttribute` vorhanden sind, hängt der Standardwert des `android:debuggable`-Attributs davon ab, ob Debugsymbole generiert werden oder nicht. Wenn Debugsymbole vorhanden sind, legt Xamarin.Android das `android:debuggable`-Attribut auf `true` fest.

Beachten Sie, dass der Wert des `android:debuggable`-Attributs NICHT zwingend von der Buildkonfiguration abhängt. Es ist möglich, für Releasebuilds das `android:debuggable`-Attribut auf TRUE festzulegen.

## <a name="related-links"></a>Verwandte Links

- [Debuggable apps in the Android market (Debugfähige Apps im Android Market)](https://labs.f-secure.com/archive/debuggable-apps-in-android-market/)
