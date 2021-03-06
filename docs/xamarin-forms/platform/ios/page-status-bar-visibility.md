---
title: Sichtbarkeit von Seiten Status Leiste unter IOS
description: Platt Form Besonderheiten ermöglichen es Ihnen, Funktionen zu nutzen, die nur auf einer bestimmten Plattform verfügbar sind, ohne dass benutzerdefinierte Renderer oder Effekte implementiert werden. In diesem Artikel wird erläutert, wie die plattformspezifische IOS-Anwendung verwendet wird, die die Sichtbarkeit der Statusleiste auf einer Seite festlegt.
ms.prod: xamarin
ms.assetid: D8BB7C24-A27F-4758-8557-6A81F909ABD9
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/24/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 22d54b1726858b1f46cf312f4962091374385704
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/22/2020
ms.locfileid: "86936824"
---
# <a name="page-status-bar-visibility-on-ios"></a>Sichtbarkeit von Seiten Status Leiste unter IOS

[![Beispiel herunterladen](~/media/shared/download.png) Das Beispiel herunterladen](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

Diese plattformspezifische IOS-Datei wird verwendet, um die Sichtbarkeit der Statusleiste eines festzulegen [`Page`](xref:Xamarin.Forms.Page) , und bietet die Möglichkeit, zu steuern, wie die Statusleiste in das-Element gelangt oder Sie verlässt `Page` . Sie wird in XAML verwendet, indem die `Page.PrefersStatusBarHidden` angefügte-Eigenschaft auf einen Wert der `StatusBarHiddenMode` -Enumeration festgelegt wird, und optional die `Page.PreferredStatusBarUpdateAnimation` angefügte-Eigenschaft auf einen Wert der- `UIStatusBarAnimation` Enumeration:

```xaml
<ContentPage ...
             xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core"
             ios:Page.PrefersStatusBarHidden="True"
             ios:Page.PreferredStatusBarUpdateAnimation="Fade">
  ...
</ContentPage>
```

Alternativ kann Sie mithilfe der flüssigen API von c# genutzt werden:

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;
...

On<iOS>().SetPrefersStatusBarHidden(StatusBarHiddenMode.True)
         .SetPreferredStatusBarUpdateAnimation(UIStatusBarAnimation.Fade);
```

Die- `Page.On<iOS>` Methode gibt an, dass diese plattformspezifische nur unter IOS ausgeführt wird. Die- `Page.SetPrefersStatusBarHidden` Methode im- `Xamarin.Forms.PlatformConfiguration.iOSSpecific` Namespace wird verwendet, um die Sichtbarkeit der Statusleiste eines festzulegen, [`Page`](xref:Xamarin.Forms.Page) indem Sie einen der- `StatusBarHiddenMode` Enumerationswerte angeben: `Default` , `True` oder `False` . Der `StatusBarHiddenMode.True` -Wert und der- `StatusBarHiddenMode.False` Wert legen die Status leisten Sichtbarkeit unabhängig von der Geräte Ausrichtung fest, und der Wert blendet `StatusBarHiddenMode.Default` die Statusleiste in einer vertikal kompakten Umgebung aus.

Das Ergebnis ist, dass die Sichtbarkeit der Statusleiste eines [`Page`](xref:Xamarin.Forms.Page) festgelegt werden kann:

![Sichtbarkeit der Status Leiste für plattformspezifisch](page-status-bar-visibility-images/hide-status-bar.png)

> [!NOTE]
> Bei einem [`TabbedPage`](xref:Xamarin.Forms.TabbedPage) aktualisiert der angegebene `StatusBarHiddenMode` Enumerationswert auch die Statusleiste auf allen untergeordneten Seiten. Bei allen anderen von [`Page`](xref:Xamarin.Forms.Page) abgeleiteten Typen aktualisiert der angegebene `StatusBarHiddenMode` Enumerationswert nur die Statusleiste auf der aktuellen Seite.

Die- `Page.SetPreferredStatusBarUpdateAnimation` Methode wird verwendet, um festzulegen, wie die Statusleiste [`Page`](xref:Xamarin.Forms.Page) durch Angeben eines der-Enumerationswerte in die Statusleiste wechselt oder Sie verlässt `UIStatusBarAnimation` : `None` , `Fade` oder `Slide` . Wenn der `Fade` - `Slide` Enumerationswert oder der-Enumerationswert angegeben wird, wird eine 0,25 Sekunden-Animation ausgeführt, wenn die Statusleiste in den Eintritt `Page`

## <a name="related-links"></a>Verwandte Links

- [Platformbesonderheiten (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [Erstellen von Plattformeigenschaften](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [iosspecific-API](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)
