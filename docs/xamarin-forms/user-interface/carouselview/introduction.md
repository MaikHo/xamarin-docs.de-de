---
title: Xamarin.FormsEinführung in carouselview
description: Carouselview ist eine Ansicht für die Darstellung von Daten in einem Bild lauffähigen Layout, in dem Benutzer durch eine Auflistung von Elementen navigieren können.
ms.prod: xamarin
ms.assetid: 2a96e4bd-c29b-4658-bb4c-ab00872b0f8f
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/08/2019
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: a78536463b4966c38025d5c46a33aa07cb81bfdf
ms.sourcegitcommit: 08290d004d1a7e7ac579bf1f96abf8437921dc70
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87918389"
---
# <a name="no-locxamarinforms-carouselview-introduction"></a>Xamarin.FormsEinführung in carouselview

![Vorabrelease der API](~/media/shared/preview.png)

[`CarouselView`](xref:Xamarin.Forms.CarouselView)ist eine Ansicht für die Darstellung von Daten in einem Bild lauffähigen Layout, in dem Benutzer zum Durchlaufen einer Auflistung von Elementen schwenken können. In der Standardeinstellung `CarouselView` werden die Elemente in horizontaler Ausrichtung angezeigt. Auf dem Bildschirm wird ein einzelnes Element angezeigt, das eine Schwenkbewegung und eine rückwärts Navigation durch die Auflistung von Elementen zur Folge hat. Außerdem können Indikatoren angezeigt werden, die die einzelnen Elemente in der darstellen `CarouselView` :

[![Screenshot von "carouselview" und "indikatorview" unter IOS und Android](populate-data-images/indicators.png "Sichorview-Kreise")](populate-data-images/indicators-large.png#lightbox "Sichorview-Kreise")

[`CarouselView`](xref:Xamarin.Forms.CarouselView)ist in Xamarin.Forms 4,3 verfügbar. Es ist jedoch zurzeit experimentell und kann nur verwendet werden, indem die folgende Codezeile zu Ihrer `AppDelegate` Klasse unter IOS oder ihrer Klasse unter Android hinzugefügt wird `MainActivity` , bevor aufgerufen wird `Forms.Init` :

```csharp
Forms.SetFlags("CarouselView_Experimental");
```

> [!IMPORTANT]
> [`CarouselView`](xref:Xamarin.Forms.CarouselView)ist unter IOS und Android verfügbar, einige Funktionen sind jedoch möglicherweise nur teilweise auf dem universelle Windows-Plattform verfügbar.

[`CarouselView`](xref:Xamarin.Forms.CarouselView)teilt einen Großteil seiner Implementierung mit [`CollectionView`](xref:Xamarin.Forms.CollectionView) . Die beiden Steuerelemente haben jedoch unterschiedliche Anwendungsfälle. `CollectionView`wird normalerweise verwendet, um Listen mit Daten beliebiger Länge darzustellen, wohingegen `CarouselView` in der Regel verwendet wird, um Informationen in einer Liste mit begrenzter Länge hervorzuheben.
