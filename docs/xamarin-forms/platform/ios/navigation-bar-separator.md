---
title: Trennzeichen für Navigations Seitenleiste unter IOS
description: Platt Form Besonderheiten ermöglichen es Ihnen, Funktionen zu nutzen, die nur auf einer bestimmten Plattform verfügbar sind, ohne dass benutzerdefinierte Renderer oder Effekte implementiert werden. In diesem Artikel wird erläutert, wie Sie die plattformspezifische IOS-Datei nutzen, die die Trennlinie und den Schatten im unteren Bereich der Navigationsleiste auf einer navigationpage verbirgt.
ms.prod: xamarin
ms.assetid: 5A45748A-6779-4441-82F2-415BD68473B9
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/24/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: c74f9bd17f8da5cd41a55f8b35a66e21df81a8d2
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/22/2020
ms.locfileid: "86931182"
---
# <a name="navigationpage-bar-separator-on-ios"></a>Trennzeichen für Navigations Seitenleiste unter IOS

[![Beispiel herunterladen](~/media/shared/download.png) Herunterladen des Beispiels](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

Diese IOS-plattformspezifische verbirgt die Trennlinie und den Schatten, der sich am unteren Rand der Navigationsleiste eines befindet [`NavigationPage`](xref:Xamarin.Forms.NavigationPage) . Sie wird in XAML verwendet, indem die [`NavigationPage.HideNavigationBarSeparator`](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific.NavigationPage.HideNavigationBarSeparatorProperty) bindbare Eigenschaft auf festgelegt wird `false` :

```xaml
<NavigationPage ...
                xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core"
                ios:NavigationPage.HideNavigationBarSeparator="true">

</NavigationPage>
```

Alternativ kann Sie mithilfe der flüssigen API von c# genutzt werden:

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;

public class iOSTitleViewNavigationPageCS : Xamarin.Forms.NavigationPage
{
    public iOSTitleViewNavigationPageCS()
    {
        On<iOS>().SetHideNavigationBarSeparator(true);
    }
}
```

Die- `NavigationPage.On<iOS>` Methode gibt an, dass diese plattformspezifische nur unter IOS ausgeführt wird. [ `NavigationPage.SetHideNavigationBarSeparator` ] (Xref: Xamarin.Forms . Platformconfiguration. iosspecific. navigationpage. * thidenavigationbarseparator ( Xamarin.Forms . Iplatformelementconfiguration { Xamarin.Forms . Platformconfiguration. IOS, Xamarin.Forms . Navigationpage}, System. Boolean))-Methode im- [`Xamarin.Forms.PlatformConfiguration.iOSSpecific`](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific) Namespace wird verwendet, um zu steuern, ob das Navigationsleisten Trennzeichen ausgeblendet ist. Außerdem ist [ `NavigationPage.HideNavigationBarSeparator` ] (Xref: Xamarin.Forms . Platformconfiguration. iosspecific. navigationpage. hidenavigationbarseparator ( Xamarin.Forms . Iplatformelementconfiguration { Xamarin.Forms . Platformconfiguration. IOS, Xamarin.Forms . Navigationpage}))-Methode kann verwendet werden, um zurückzugeben, ob das Navigationsleisten Trennzeichen ausgeblendet ist.

Das Ergebnis ist, dass das Navigationsleisten Trennzeichen auf einem [`NavigationPage`](xref:Xamarin.Forms.NavigationPage) ausgeblendet werden kann:

![Navigationsleiste "navigationpage" ausgeblendet](navigation-bar-separator-images/navigationpage-hideseparatorbar.png)

## <a name="related-links"></a>Verwandte Links

- [Platformbesonderheiten (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [Erstellen von Plattformeigenschaften](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [iosspecific-API](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)
