---
title: Gleichzeitige Erkennung von Schwenken in ios
description: Platt Form Besonderheiten ermöglichen es Ihnen, Funktionen zu nutzen, die nur auf einer bestimmten Plattform verfügbar sind, ohne dass benutzerdefinierte Renderer oder Effekte implementiert werden. In diesem Artikel wird erläutert, wie die plattformspezifische IOS-Anwendung verwendet wird, die die gleichzeitige Erkennung von Schwenken in einer Anwendung ermöglicht.
ms.prod: xamarin
ms.assetid: 883D89DA-F8FF-4B97-9C3F-2DD05C96A495
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/24/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 125685150243ba8e8099cbfbdfec90e5a0b4d6b7
ms.sourcegitcommit: 32d2476a5f9016baa231b7471c88c1d4ccc08eb8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2020
ms.locfileid: "84138579"
---
# <a name="simultaneous-pan-gesture-recognition-on-ios"></a>Gleichzeitige Erkennung von Schwenken in ios

[![Beispiel herunterladen](~/media/shared/download.png) Das Beispiel herunterladen](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

Wenn eine [`PanGestureRecognizer`](xref:Xamarin.Forms.PanGestureRecognizer) in einer Bild Lauf Ansicht an eine Ansicht angefügt wird, werden alle Schwenk Gesten vom aufgezeichnet `PanGestureRecognizer` und nicht an die scrollansicht übergeben. Die scrollansicht führt daher keinen Bildlauf mehr durch.

Mit diesem IOS-plattformspezifischen kann ein `PanGestureRecognizer` in einer scrollansicht in der scrollansicht aufzeichnen und die Schwenkbewegung freigeben. Sie wird in XAML verwendet, indem die [`Application.PanGestureRecognizerShouldRecognizeSimultaneously`](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific.Application.PanGestureRecognizerShouldRecognizeSimultaneouslyProperty) angefügte-Eigenschaft auf festgelegt wird `true` :

```xaml
<Application ...
             xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core"
             ios:Application.PanGestureRecognizerShouldRecognizeSimultaneously="true">
    ...
</Application>
```

Alternativ kann Sie mithilfe der flüssigen API von c# genutzt werden:

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;
...

Xamarin.Forms.Application.Current.On<iOS>().SetPanGestureRecognizerShouldRecognizeSimultaneously(true);
```

Die- `Application.On<iOS>` Methode gibt an, dass diese plattformspezifische nur unter IOS ausgeführt wird. [ `Application.SetPanGestureRecognizerShouldRecognizeSimultaneously` ] (Xref: Xamarin.Forms . Platformconfiguration. iosspecific. Application. setpangesturerecognizerschuldrecognizegleich ( Xamarin.Forms . Iplatformelementconfiguration { Xamarin.Forms . Platformconfiguration. IOS, Xamarin.Forms . Application}, System. Boolean)) im- [`Xamarin.Forms.PlatformConfiguration.iOSSpecific`](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific) Namespace wird verwendet, um zu steuern, ob eine aufzeichnungsinitierkennung in einer scrollansicht die Schwenkbewegung erfasst, oder die schwenken-Geste mit der scrollansicht zu erfassen und freizugeben. Außerdem ist [ `Application.GetPanGestureRecognizerShouldRecognizeSimultaneously` ] (Xref: Xamarin.Forms . Platformconfiguration. iosspecific. Application. getpangesturerecognizerschuldrecognizegleich ( Xamarin.Forms . Iplatformelementconfiguration { Xamarin.Forms . Platformconfiguration. IOS, Xamarin.Forms . Application}))-Methode kann verwendet werden, um zurückzugeben, ob die Schwenkbewegung für die scrollansicht freigegeben ist, die enthält [`PanGestureRecognizer`](xref:Xamarin.Forms.PanGestureRecognizer) .

Wenn diese plattformspezifisch aktiviert ist und ein [`ListView`](xref:Xamarin.Forms.ListView) enthält [`PanGestureRecognizer`](xref:Xamarin.Forms.PanGestureRecognizer) , empfangen sowohl der als auch das die Schwenk `ListView` `PanGestureRecognizer` Bewegung und verarbeiten es. Wenn allerdings eine plattformspezifische deaktivierte ist und ein `ListView` -Wert enthält `PanGestureRecognizer` , erfasst der die Schwenk `PanGestureRecognizer` Bewegung und verarbeitet Sie, und der `ListView` empfängt die Schwenkbewegung nicht.

## <a name="related-links"></a>Verwandte Links

- [Platformbesonderheiten (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [Erstellen von Plattformeigenschaften](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [iosspecific-API](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)
