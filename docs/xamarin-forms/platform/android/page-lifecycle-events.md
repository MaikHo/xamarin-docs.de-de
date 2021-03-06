---
title: Seiten Lebenszyklus-Ereignisse unter Android
description: Platt Form Besonderheiten ermöglichen es Ihnen, Funktionen zu nutzen, die nur auf einer bestimmten Plattform verfügbar sind, ohne dass benutzerdefinierte Renderer oder Effekte implementiert werden. In diesem Artikel wird erläutert, wie Sie die plattformspezifische Android-Anwendung nutzen, die das Verschwinden und die Anzeige von Seiten Ereignissen für die Anwendungs Unterbrechung bzw. Fortsetzung deaktiviert.
ms.prod: xamarin
ms.assetid: F6E3759C-D347-407A-91A2-CF9B3B7D4CBD
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/10/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: fb4d1e28fded70005ef23eb4f7540eccd2fba372
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/22/2020
ms.locfileid: "86939307"
---
# <a name="page-lifecycle-events-on-android"></a>Seiten Lebenszyklus-Ereignisse unter Android

[![Beispiel herunterladen](~/media/shared/download.png) Das Beispiel herunterladen](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

Diese Android-plattformspezifische wird verwendet, um [`Disappearing`](xref:Xamarin.Forms.Page.Appearing) die [`Appearing`](xref:Xamarin.Forms.Page.Appearing) Seiten Ereignisse und für Anwendungen zu deaktivieren, die AppCompat verwenden. Darüber hinaus bietet Sie die Möglichkeit, zu steuern, ob die weiche Tastatur beim fortsetzen angezeigt wird, wenn Sie beim Anhalten angezeigt wurde, vorausgesetzt, dass der Betriebsmodus der Soft Tastatur auf festgelegt ist [`WindowSoftInputModeAdjust.Resize`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.WindowSoftInputModeAdjust.Resize) .

> [!NOTE]
> Beachten Sie, dass diese Ereignisse standardmäßig aktiviert sind, um ein vorhandenes Verhalten für Anwendungen beizubehalten, die auf den Ereignissen basieren. Durch das Deaktivieren dieser Ereignisse wird der AppCompat-Ereignis Kreis mit dem Pre-AppCompat-Ereignis Cycle verglichen.

Diese plattformspezifische kann in XAML verwendet werden, indem die [`Application.SendDisappearingEventOnPause`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat.Application.SendDisappearingEventOnPauseProperty) [`Application.SendAppearingEventOnResume`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat.Application.SendAppearingEventOnResumeProperty) [`Application.ShouldPreserveKeyboardOnResume`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat.Application.ShouldPreserveKeyboardOnResumeProperty) angefügten Eigenschaften, und auf-Werte festgelegt werden `boolean` :

```xaml
<Application ...
             xmlns:android="clr-namespace:Xamarin.Forms.PlatformConfiguration.AndroidSpecific;assembly=Xamarin.Forms.Core"             xmlns:androidAppCompat="clr-namespace:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat;assembly=Xamarin.Forms.Core"
             android:Application.WindowSoftInputModeAdjust="Resize"
             androidAppCompat:Application.SendDisappearingEventOnPause="false"
             androidAppCompat:Application.SendAppearingEventOnResume="false"
             androidAppCompat:Application.ShouldPreserveKeyboardOnResume="true">
  ...
</Application>
```

Alternativ kann Sie mithilfe der flüssigen API von c# genutzt werden:

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.AndroidSpecific;
using Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat;
...

Xamarin.Forms.Application.Current.On<Android>()
     .UseWindowSoftInputModeAdjust(WindowSoftInputModeAdjust.Resize)
     .SendDisappearingEventOnPause(false)
     .SendAppearingEventOnResume(false)
     .ShouldPreserveKeyboardOnResume(true);
```

Die- `Application.Current.On<Android>` Methode gibt an, dass diese plattformspezifische nur unter Android ausgeführt wird. [ `Application.SendDisappearingEventOnPause` ] (Xref: Xamarin.Forms . Platformconfiguration. androidspecific. AppCompat. Application. senddiserscheinung ingeventonpause ( Xamarin.Forms . Iplatformelementconfiguration { Xamarin.Forms . Platformconfiguration. Android, Xamarin.Forms . Application}, System. Boolean))-Methode im- [`Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat) Namespace wird verwendet, um das Auslösen des Seiten Ereignisses zu aktivieren bzw. zu deaktivieren [`Disappearing`](xref:Xamarin.Forms.Page.Appearing) , wenn die Anwendung in den Hintergrund wechselt. [ `Application.SendAppearingEventOnResume` ] (Xref: Xamarin.Forms . Platformconfiguration. androidspecific. AppCompat. Application. sendappearingeventonresume ( Xamarin.Forms . Iplatformelementconfiguration { Xamarin.Forms . Platformconfiguration. Android, Xamarin.Forms . Die Application}, System. Boolean)-Methode wird verwendet, um das Auslösen des Seiten Ereignisses zu aktivieren bzw. zu deaktivieren [`Appearing`](xref:Xamarin.Forms.Page.Appearing) , wenn die Anwendung im Hintergrund fortgesetzt wird. [ `Application.ShouldPreserveKeyboardOnResume` ] (Xref: Xamarin.Forms . Platformconfiguration. androidspecific. AppCompat. Application. schuldpreservekeyboardonresume ( Xamarin.Forms . Iplatformelementconfiguration { Xamarin.Forms . Platformconfiguration. Android, Xamarin.Forms . Application}, System. Boolean))-Methode verwendet, um zu steuern, ob die weiche Tastatur beim fortsetzen angezeigt wird, wenn Sie beim Anhalten angezeigt wurde, vorausgesetzt, dass der Betriebsmodus der Soft Tastatur auf festgelegt ist [`WindowSoftInputModeAdjust.Resize`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.WindowSoftInputModeAdjust.Resize) .

Das Ergebnis ist, dass das [`Disappearing`](xref:Xamarin.Forms.Page.Appearing) -Ereignis und das- [`Appearing`](xref:Xamarin.Forms.Page.Appearing) Seiten Ereignis beim Anhalten und Fortsetzen der Anwendung nicht ausgelöst werden. wenn die weiche Tastatur beim Anhalten der Anwendung angezeigt wird, wird Sie auch angezeigt, wenn die Anwendung fortgesetzt wird:

[![Plattformspezifische Lebenszyklus Ereignisse](page-lifecycle-events-images/keyboard-on-resume.png)](page-lifecycle-events-images/keyboard-on-resume-large.png#lightbox "Plattformspezifische Lebenszyklus Ereignisse")

## <a name="related-links"></a>Verwandte Links

- [Platformbesonderheiten (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [Erstellen von Plattformeigenschaften](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [Androidspecific-API](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific)
- [Androidspecific. AppCompat-API](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat)
