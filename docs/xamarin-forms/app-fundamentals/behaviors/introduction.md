---
title: Einführung in Verhalten
description: Durch Verhalten können Sie Steuerelementen für Benutzeroberflächen Funktionen hinzufügen, ohne Unterklassen erstellen zu müssen. Stattdessen wird die Funktion in einer Verhaltensklasse implementiert und an das Steuerelement angefügt, als wäre sie ein Teil des Steuerelements selbst. In diesem Artikel werden Verhalten grundlegend vorgestellt.
ms.prod: xamarin
ms.assetid: 0DF1EF8C-A212-4142-A3C6-DF760A82A757
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/06/2016
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 37c76a5f325c363a92c2a2c1e597dab28f064cd9
ms.sourcegitcommit: a003b036f6fb83818e2ecc9c72a641e3aeb373bd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88964609"
---
# <a name="introduction-to-behaviors"></a>Einführung in Verhalten

_Durch Verhalten können Sie Steuerelementen für Benutzeroberflächen Funktionen hinzufügen, ohne Unterklassen erstellen zu müssen. Stattdessen wird die Funktion in einer Verhaltensklasse implementiert und an das Steuerelement angefügt, als wäre sie ein Teil des Steuerelements selbst. In diesem Artikel werden Verhalten grundlegend vorgestellt._

Durch Verhalten können Sie Code implementieren, den Sie normalerweise in eine CodeBehind-Datei schreiben würden, da dieser so direkt mit der API des Steuerelements interagiert, dass er präzise an das Steuerelement angefügt werden und zur Wiederverwendung in mehr als eine App gepackt werden kann. Sie können verwendet werden, um vollständige Funktionen der Steuerelemente bereitzustellen, wie:

- Hinzufügen eines Validierungssteuerelement für E-Mails an [`Entry`](xref:Xamarin.Forms.Entry)
- Erstellen eines Bewertungssteuerelements mithilfe einer Gestenerkennung für Tippbewegungen
- Steuern einer Animation
- Hinzufügen eines Effekts zu einem Steuerelement

Verhalten aktivieren auch fortgeschrittenere Szenarios. Bei *Befehlen* sind Verhalten nützlich, um ein Steuerelement mit einem Befehl zu verbinden. Sie können auch zum Zuordnen von Befehlen zu Steuerelementen verwendet werden, die nicht zum Interagieren mit Befehlen konzipiert sind. Beispielsweise können diese als Reaktion auf ein auslösendes Ereignis zum Aufrufen eines Befehls verwendet werden.

Xamarin.Forms unterstützt zwei verschiedene Verhalten:

- **Xamarin.Forms-Verhalten:** Klassen, die von der Klasse [`Behavior`](xref:Xamarin.Forms.Behavior) oder [`Behavior<T>`](xref:Xamarin.Forms.Behavior`1) abgeleitet werden, in der `T` der Steuerelementtyp ist, für das Verhalten gelten soll. Weitere Informationen zu Xamarin.Forms-Verhaltensweisen finden Sie unter [Xamarin.Forms-Verhaltensweisen](~/xamarin-forms/app-fundamentals/behaviors/creating.md).
- **Angefügte Verhalten:** `static`-Klassen mit einer oder mehreren angefügten Eigenschaften. Weitere Informationen zu angefügten Verhalten finden Sie unter [Attached Behaviors (Angefügte Verhalten)](~/xamarin-forms/app-fundamentals/behaviors/attached.md).

In diesem Leitfaden werden vor allem Xamarin.Forms-Verhalten beschrieben, da sie die bevorzugte Herangehensweise für die Verhaltenserstellung darstellen.

## <a name="related-links"></a>Verwandte Links

- [Behavior class (Behavior-Klasse)](xref:Xamarin.Forms.Behavior)
- [Behavior&lt;T&gt; class (Behavior<T>-Klasse)](xref:Xamarin.Forms.Behavior`1)
