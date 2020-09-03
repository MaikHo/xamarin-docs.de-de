---
title: Xamarin.Forms-Verhalten
description: Durch Verhalten können Sie Benutzeroberflächen-Steuerelementen Funktionen hinzufügen, ohne diese unterordnen zu müssen. Verhalten werden im Code geschrieben und Steuerelementen mit XAML oder Code hinzugefügt.
ms.prod: xamarin
ms.assetid: 42E32AD7-8E3B-48B3-B402-E75B758DA913
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/06/2016
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: d917d7d6421cfae7fc877c81023a835573fa99b1
ms.sourcegitcommit: a003b036f6fb83818e2ecc9c72a641e3aeb373bd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88964622"
---
# <a name="no-locxamarinforms-behaviors"></a>Xamarin.Forms-Verhalten

_Durch Verhalten können Sie Benutzeroberflächen-Steuerelementen Funktionen hinzufügen, ohne diese unterordnen zu müssen. Verhalten werden im Code geschrieben und Steuerelementen mit XAML oder Code hinzugefügt._

## <a name="introduction-to-behaviors"></a>[Einführung in Verhalten](introduction.md)

Durch Verhalten können Sie Code implementieren, den Sie normalerweise in eine CodeBehind-Datei schreiben würden, da dieser so direkt mit der API des Steuerelements interagiert, dass er präzise an das Steuerelement angefügt werden kann. In diesem Artikel werden Verhalten grundlegend vorgestellt.

## <a name="attached-behaviors"></a>[Angefügte Verhaltensweisen](attached.md)

Angefügte Verhaltensweisen sind `static`-Klassen mit mindestens einer angefügten Eigenschaft. In diesem Artikel wird veranschaulicht, wie Sie angefügte Verhaltensweisen erstellen und verwenden können.

## <a name="no-locxamarinforms-behaviors"></a>[Xamarin.Forms-Verhalten](creating.md)

Xamarin.Forms-Verhalten werden von der Klasse [`Behavior`](xref:Xamarin.Forms.Behavior) oder [`Behavior<T>`](xref:Xamarin.Forms.Behavior`1) abgeleitet. In diesem Artikel wird veranschaulicht, wie Xamarin.Forms-Verhalten erstellt und genutzt werden.

## <a name="reusable-effectbehavior"></a>[Wiederverwendbare EffectBehavior-Klasse](effect-behavior.md)

Verhalten sind ein nützlicher Ansatz, um Effekte zu einem Steuerelement hinzuzufügen. Dadurch wird standardmäßig genutzter Effektbehandlungscode von Codebehind-Dateien verwendet. In diesem Artikel wird das Erstellen und Nutzen eines Xamarin.Forms-Verhaltens veranschaulicht, um einem Steuerelement einen Effekt hinzuzufügen.
