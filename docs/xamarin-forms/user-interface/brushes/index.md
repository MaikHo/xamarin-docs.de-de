---
title: Xamarin.FormsLlt
description: Die Xamarin.Forms Pinsel Klasse ist eine abstrakte Klasse, die einen Bereich mit ihrer Ausgabe zeichnet.
ms.prod: xamarin
ms.assetid: 44420FC2-304C-4175-8654-76769F79A813
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/28/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 4f1f56103b20eac84ce6106c0955acebf974cfe3
ms.sourcegitcommit: 08290d004d1a7e7ac579bf1f96abf8437921dc70
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87919092"
---
# <a name="no-locxamarinforms-brushes"></a>Xamarin.FormsLlt

![Vorschau-API](~/media/shared/preview.png "Diese API ist derzeit als Vorabversion erhältlich.")

Mit einem Pinsel können Sie einen Bereich, z. b. den Hintergrund eines Steuer Elements, mit unterschiedlichen Ansätzen zeichnen. Die Pinsel Unterstützung in Xamarin.Forms ist im `Xamarin.Forms` -Namespace unter IOS, Android, macOS, der universelle Windows-Plattform (UWP) und Windows Presentation Foundation (WPF) verfügbar.

> [!IMPORTANT]
> Die Pinsel Unterstützung in Xamarin.Forms ist zurzeit experimentell und kann nur verwendet werden, indem das-Flag festgelegt wird `Brush_Experimental` . Weitere Informationen finden Sie unter [experimentelle Flags](~/xamarin-forms/internals/experimental-flags.md).

Die- `Brush` Klasse ist eine abstrakte Klasse, die einen Bereich mit ihrer Ausgabe zeichnet. Klassen, die von abgeleitet werden, `Brush` beschreiben verschiedene Methoden zum Zeichnen eines Bereichs. In der folgenden Liste werden die verschiedenen Pinseltypen beschrieben, die in verfügbar sind Xamarin.Forms :

- `SolidColorBrush`, der einen Bereich mit einer voll Tonfarbe zeichnet. Weitere Informationen finden Sie unter [ Xamarin.Forms Pinsel: voll Tonfarben](solidcolor.md).
- `LinearGradientBrush`, der einen Bereich mit einem linearen Farbverlauf zeichnet. Weitere Informationen finden Sie unter [ Xamarin.Forms Pinsel: lineare Farbverläufe](lineargradient.md).
- `RadialGradientBrush`, der einen Bereich mit einem radialen Farbverlauf zeichnet. Weitere Informationen finden Sie unter [ Xamarin.Forms Pinsel: radiale Farbverläufe](radialgradient.md).

Instanzen dieser Pinseltypen können den `Stroke` -und- `Fill` Eigenschaften von `Shape` und der- `Background` Eigenschaft eines zugewiesen werden [`VisualElement`](xref:Xamarin.Forms.VisualElement) .

> [!NOTE]
> Die- `VisualElement.Background` Eigenschaft ermöglicht die Verwendung von Pinseln als Hintergrund in beliebigen Steuerelementen.

Die- `Brush` Klasse verfügt auch über eine- `IsNullOrEmpty` Methode, die einen zurückgibt `bool` , der angibt, ob der Pinsel definiert ist.
