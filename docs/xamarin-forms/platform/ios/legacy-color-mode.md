---
title: Visualelement-Legacy Farben Modus unter IOS
description: Platt Form Besonderheiten ermöglichen es Ihnen, Funktionen zu nutzen, die nur auf einer bestimmten Plattform verfügbar sind, ohne dass benutzerdefinierte Renderer oder Effekte implementiert werden. In diesem Artikel wird erläutert, wie Sie die plattformspezifische IOS-Version verwenden, die den Xamarin.Forms Legacy Farb Modus deaktiviert.
ms.prod: xamarin
ms.assetid: 60FFBA67-6E06-439B-A5EB-8C808285E2CD
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/24/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 401de4883c91c682d4734dd036ea87b6dc694edb
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/22/2020
ms.locfileid: "86939047"
---
# <a name="visualelement-legacy-color-mode-on-ios"></a>Visualelement-Legacy Farben Modus unter IOS

[![Beispiel herunterladen](~/media/shared/download.png) Das Beispiel herunterladen](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

Einige der Xamarin.Forms Ansichten verfügen über einen Legacy Farb Modus. In diesem Modus, wenn die- [`IsEnabled`](xref:Xamarin.Forms.VisualElement.IsEnabled) Eigenschaft der-Sicht auf festgelegt ist, überschreibt `false` die Ansicht die vom Benutzer festgelegten Farben mit den standardmäßigen systemeigenen Farben für den deaktivierten Zustand. Aus Gründen der Abwärtskompatibilität bleibt dieser Legacy Farb Modus das Standardverhalten für unterstützte Ansichten.

Mit diesem IOS-plattformspezifischen wird dieser ältere Farb Modus auf einem deaktiviert [`VisualElement`](xref:Xamarin.Forms.VisualElement) , sodass die für eine Ansicht des Benutzers festgelegten Farben auch dann beibehalten werden, wenn die Ansicht deaktiviert ist. Sie wird in XAML verwendet, indem die [`VisualElement.IsLegacyColorModeEnabled`](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific.VisualElement.IsLegacyColorModeEnabledProperty) angefügte-Eigenschaft auf festgelegt wird `false` :

```xaml
<ContentPage ...
             xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core">
    <StackLayout>
        ...
        <Button Text="Button"
                TextColor="Blue"
                BackgroundColor="Bisque"
                ios:VisualElement.IsLegacyColorModeEnabled="False" />
        ...
    </StackLayout>
</ContentPage>
```

Alternativ kann Sie mithilfe der flüssigen API von c# genutzt werden:

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;
...

_legacyColorModeDisabledButton.On<iOS>().SetIsLegacyColorModeEnabled(false);
```

Die- `VisualElement.On<iOS>` Methode gibt an, dass diese plattformspezifische nur unter IOS ausgeführt wird. [ `VisualElement.SetIsLegacyColorModeEnabled` ] (Xref: Xamarin.Forms . Platformconfiguration. iosspecific. visualelement. * tislegacycolormodeaktivierte ( Xamarin.Forms . Iplatformelementconfiguration { Xamarin.Forms . Platformconfiguration. IOS, Xamarin.Forms . Visualelement}, System. Boolean))-Methode im- [`Xamarin.Forms.PlatformConfiguration.iOSSpecific`](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific) Namespace wird verwendet, um zu steuern, ob der Legacy Farb Modus deaktiviert ist. Außerdem ist [ `VisualElement.GetIsLegacyColorModeEnabled` ] (Xref: Xamarin.Forms . Platformconfiguration. iosspecific. visualelement. getislegacycolormodeaktivierte ( Xamarin.Forms . Iplatformelementconfiguration { Xamarin.Forms . Platformconfiguration. IOS, Xamarin.Forms . Visualelement}))-Methode kann verwendet werden, um zurückzugeben, ob der Legacy Farb Modus deaktiviert ist.

Das Ergebnis ist, dass der Legacy Farb Modus deaktiviert werden kann, sodass die Farben, die für eine Ansicht durch den Benutzer festgelegt sind, auch dann beibehalten werden, wenn die Ansicht deaktiviert ist:

![Legacy Farb Modus deaktiviert](legacy-color-mode-images/legacy-color-mode-disabled.png)

> [!NOTE]
> Wenn Sie [`VisualStateGroup`](xref:Xamarin.Forms.VisualStateGroup) für eine Ansicht festlegen, wird der Legacy Farb Modus vollständig ignoriert. Weitere Informationen zu visuellen Zuständen finden Sie [unter Xamarin.Forms Visual State Manager](~/xamarin-forms/user-interface/visual-state-manager.md).

## <a name="related-links"></a>Verwandte Links

- [Platformbesonderheiten (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [Erstellen von Plattformeigenschaften](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [iosspecific-API](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)
