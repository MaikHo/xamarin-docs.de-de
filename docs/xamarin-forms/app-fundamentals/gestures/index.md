---
title: Xamarin.Forms-Gesten
description: In diesem Leitfaden wird beschrieben, wie Gestenerkennungsfunktionen von Xamarin.Forms verwendet werden können, um Benutzerinteraktionen mit Ansichten in einer Xamarin.Forms-Anwendung zu erkennen.
ms.prod: xamarin
ms.assetid: 0E197A51-2304-4C09-A710-C7FF24A89F15
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/04/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 7528afd0971cf06eb69df4ed7c08c3fd6dcc9e22
ms.sourcegitcommit: 08290d004d1a7e7ac579bf1f96abf8437921dc70
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87917825"
---
# <a name="no-locxamarinforms-gestures"></a>Xamarin.Forms-Gesten

_Gestenerkennungsfunktionen können verwendet werden, um Benutzerinteraktionen mit Ansichten in einer Xamarin.Forms-Anwendung zu erkennen._

Die Xamarin.Forms [`GestureRecognizer`](xref:Xamarin.Forms.GestureRecognizer)-Klasse unterstützt Tipp-, Zusammendrück-, Schwenk-, Wisch- und Drag & Drop-Gesten auf [`View`](xref:Xamarin.Forms.View)-Instanzen.

## <a name="add-a-tap-gesture-recognizer"></a>[Hinzufügen einer Tippgestenerkennung](tap.md)

Eine Tippbewegung wird für die Tipperkennung verwendet und mit der [`TapGestureRecognizer`](xref:Xamarin.Forms.TapGestureRecognizer)-Klasse erkannt.

## <a name="add-a-pinch-gesture-recognizer"></a>[Hinzufügen einer Zusammendrückgestenerkennung](pinch.md)

Eine Zusammendrückbewegung wird zum Ausführen des interaktiven Zooms verwendet und mit der Klasse [`PinchGestureRecognizer`](xref:Xamarin.Forms.PinchGestureRecognizer) erkannt.

## <a name="add-a-pan-gesture-recognizer"></a>[Hinzufügen einer Schwenkgestenerkennung](pan.md)

Eine Schwenkbewegung wird verwendet, um die Bewegung von Fingern um den Bildschirm zu erkennen und um diese Bewegung auf den Inhalt zu übertragen. Diese wird mit der [`PanGestureRecognizer`](xref:Xamarin.Forms.PanGestureRecognizer)-Klasse erkannt.

## <a name="add-a-swipe-gesture-recognizer"></a>[Hinzufügen einer Wischgestenerkennung](swipe.md)

Eine Wischbewegung tritt auf, wenn ein Finger in horizontaler oder vertikaler Richtung über den Bildschirm bewegt wird. Diese Bewegung wird oft genutzt, um durch Inhalte zu navigieren. Wischgesten werden mit der [`SwipeGestureRecognizer`](xref:Xamarin.Forms.SwipeGestureRecognizer)-Klasse erkannt.

## <a name="add-a-drag-and-drop-gesture-recognizer"></a>[Hinzufügen einer Drag & Drop-Gestenerkennung](drag-and-drop.md)

Mithilfe einer Drag & Drop-Geste können Elemente und die zugehörigen Datenpakete mit einer kontinuierlichen Geste von einer Bildschirmposition an eine andere gezogen werden. Ziehgesten werden mit der `DragGestureRecognizer`-Klasse und Ablegegesten mit der `DropGestureRecognizer`-Klasse erkannt.
