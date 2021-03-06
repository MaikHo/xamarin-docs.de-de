---
title: Sirikit in xamarin. IOS
description: In diesem Artikel erfahren Sie, wie Sie mithilfe von "Sirikit" in einer xamarin. IOS-App Dienste bereitstellen, auf die der Benutzer mithilfe von Siri auf einem IOS-Gerät zugreifen kann.
ms.prod: xamarin
ms.assetid: 84E5681A-F557-4967-AA99-F831169157AA
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/16/2017
ms.openlocfilehash: 90d3a3b6a1e3a3c20ba8cf2ed1f12f234e3af33b
ms.sourcegitcommit: 2fbe4932a319af4ebc829f65eb1fb1816ba305d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/29/2019
ms.locfileid: "73031485"
---
# <a name="sirikit-in-xamarinios"></a>Sirikit in xamarin. IOS

_In diesem Artikel erfahren Sie, wie Sie mithilfe von "Sirikit" in einer xamarin. IOS-App Dienste bereitstellen, auf die der Benutzer mithilfe von Siri auf einem IOS-Gerät zugreifen kann._

Mit dem neuen IOS 10 ermöglicht das Sirikit einer IOS-APP, Dienste bereitzustellen, auf die der Benutzer mithilfe von Siri und der Maps-APP auf einem IOS-Gerät mithilfe von App-Erweiterungen und den neuen **Intents** und **Intents-Benutzer** Oberflächen-Frameworks zugreifen kann.

Siri arbeitet mit dem Konzept von **Domänen**, Gruppen von bekannten Aktionen für Verwandte Aufgaben. Jede Interaktion, die eine APP mit Siri hat, muss wie folgt in eine der bekannten Dienst Domänen fallen:

- Aufrufen von Audiodaten oder Videos.
- Die Reservierung einer Fahrt.
- Verwalten von-Workouts.
- Übermittlung.
- Fotos werden gesucht.
- Senden oder empfangen von Zahlungen.

Wenn der Benutzer eine Anforderung von Siri an einen der Dienste einer APP-Erweiterung sendet, sendet Sirikit der Erweiterung ein **Intent** -Objekt, das die Anforderung des Benutzers zusammen mit allen unterstützenden Daten beschreibt. Die APP-Erweiterung generiert dann das entsprechende **Antwort** Objekt für die angegebene **Absicht**und erläutert, wie die Erweiterung die Anforderung verarbeiten kann.

## <a name="understanding-sirikit-conceptsiosplatformsirikitunderstanding-sirikitmd"></a>[Grundlegendes zu SiriKit-Konzepten](~/ios/platform/sirikit/understanding-sirikit.md)

In diesem Artikel werden die wichtigsten Konzepte behandelt, die für die Arbeit mit dem Sirikit in einer xamarin. IOS-App erforderlich sind. Dabei werden die neuen Intents und Intents-Benutzeroberflächen-Erweiterungs Punkte behandelt, und es wird erläutert, wie Sie mit App-und Benutzer Vokabulars zum Öffnen einer APP für Siri

## <a name="implementing-sirikitiosplatformsirikitimplementing-sirikitmd"></a>[Implementieren von SiriKit](~/ios/platform/sirikit/implementing-sirikit.md)

In diesem Artikel werden die Schritte beschrieben, die zum Implementieren der Unterstützung von Sirikit in xamarin. IOS-apps erforderlich sind. Der Entwickler sollte vor dem Hinzufügen von Sirikit-Unterstützung zu einer APP das grundlegendes Thema zu den Konzepten von Sirikit lesen, da wichtige Konzepte behandelt werden, die für eine erfolgreiche Implementierung erforderlich sind.

## <a name="related-links"></a>Verwandte Links

- [Elizachat-Beispiel](https://docs.microsoft.com/samples/xamarin/ios-samples/ios10-elizachat)
- [Sirikit-Programmier Handbuch](https://developer.apple.com/library/prerelease/content/documentation/Intents/Conceptual/SiriIntegrationGuide/index.html)
- [Intents Framework-Referenz](https://developer.apple.com/reference/intents)
- [Intents UI-frameworkreferenz](https://developer.apple.com/reference/intentsui)
