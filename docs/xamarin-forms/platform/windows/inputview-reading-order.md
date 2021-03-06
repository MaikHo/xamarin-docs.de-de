---
title: Inputview-Lesefolge unter Windows
description: Platt Form Besonderheiten ermöglichen es Ihnen, Funktionen zu nutzen, die nur auf einer bestimmten Plattform verfügbar sind, ohne dass benutzerdefinierte Renderer oder Effekte implementiert werden. In diesem Artikel wird erläutert, wie Sie die Windows-plattformspezifische verwenden können, mit der die Lesefolge von bidirektionalem Text dynamisch erkannt werden kann.
ms.prod: xamarin
ms.assetid: E61BAEE0-C8B7-4F33-8DDC-FA1B9CA8E81D
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/24/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: f5f0bcdc2d2c8eb1b51ad8dcd1014c649af80c90
ms.sourcegitcommit: 32d2476a5f9016baa231b7471c88c1d4ccc08eb8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2020
ms.locfileid: "84137760"
---
# <a name="inputview-reading-order-on-windows"></a>Inputview-Lesefolge unter Windows

[![Beispiel herunterladen](~/media/shared/download.png) Das Beispiel herunterladen](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

Diese universelle Windows-Plattform plattformspezifisch ermöglicht das dynamische Erkennen der Lesereihenfolge (von links nach rechts oder von rechts nach links) von bidirektionalem Text in [`Entry`](xref:Xamarin.Forms.Entry) -,- [`Editor`](xref:Xamarin.Forms.Editor) und- [`Label`](xref:Xamarin.Forms.Label) Instanzen. Sie wird in XAML verwendet, indem die [`InputView.DetectReadingOrderFromContent`](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.InputView.DetectReadingOrderFromContentProperty) (für `Entry` -und- `Editor` Instanzen) oder die [`Label.DetectReadingOrderFromContent`](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.Label.DetectReadingOrderFromContentProperty) angefügte-Eigenschaft auf einen `boolean` Wert festgelegt wird:

```xaml
<ContentPage ...
             xmlns:windows="clr-namespace:Xamarin.Forms.PlatformConfiguration.WindowsSpecific;assembly=Xamarin.Forms.Core">
    <StackLayout>
        <Editor ... windows:InputView.DetectReadingOrderFromContent="true" />
        ...
    </StackLayout>
</ContentPage>
```

Alternativ kann Sie mithilfe der flüssigen API von c# genutzt werden:

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.WindowsSpecific;
...

editor.On<Windows>().SetDetectReadingOrderFromContent(true);
```

Die- `Editor.On<Windows>` Methode gibt an, dass diese plattformspezifische nur auf der universelle Windows-Plattform ausgeführt wird. [ `InputView.SetDetectReadingOrderFromContent` ] (Xref: Xamarin.Forms . Platformconfiguration. windowsspecific. inputview. setdetectreadingorderfromcontent ( Xamarin.Forms . Iplatformelementconfiguration { Xamarin.Forms . Platformconfiguration. Windows, Xamarin.Forms . Die inputview}, System. Boolean)-Methode im- [`Xamarin.Forms.PlatformConfiguration.WindowsSpecific`](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific) Namespace wird verwendet, um zu steuern, ob die Lesereihenfolge aus dem Inhalt in der erkannt wird [`InputView`](xref:Xamarin.Forms.InputView) . Außerdem kann die- `InputView.SetDetectReadingOrderFromContent` Methode verwendet werden, um zu wechseln, ob die Lesereihenfolge aus dem Inhalt durch Aufrufen von [ `InputView.GetDetectReadingOrderFromContent` ] (Xref:) erkannt wird Xamarin.Forms . Platformconfiguration. windowsspecific. inputview. getdetectreadingorderfromcontent ( Xamarin.Forms . Iplatformelementconfiguration { Xamarin.Forms . Platformconfiguration. Windows, Xamarin.Forms . Inputview}))-Methode zum Zurückgeben des aktuellen Werts:

```csharp
editor.On<Windows>().SetDetectReadingOrderFromContent(!editor.On<Windows>().GetDetectReadingOrderFromContent());
```

Das Ergebnis ist, [`Entry`](xref:Xamarin.Forms.Entry) dass [`Editor`](xref:Xamarin.Forms.Editor) -,-und- [`Label`](xref:Xamarin.Forms.Label) Instanzen die Lesereihenfolge ihrer Inhalte dynamisch erkennen können:

[![Inputview zum Erkennen der Lesefolge von Inhalts plattformspezifisch](inputview-reading-order-images/editor-readingorder.png "Inputview zum Erkennen der Lesefolge von Inhalts plattformspezifisch")](inputview-reading-order-images/editor-readingorder-large.png#lightbox "Inputview zum Erkennen der Lesefolge von Inhalts plattformspezifisch")

> [!NOTE]
> Im Gegensatz zum Festlegen der- [`FlowDirection`](xref:Xamarin.Forms.VisualElement.FlowDirection) Eigenschaft wirkt sich die Logik für Sichten, die die Lesefolge von Ihrem Text Inhalt erkennen, nicht auf die Ausrichtung des Texts innerhalb der Sicht aus. Stattdessen wird die Reihenfolge angepasst, in der Blöcke von bidirektionalem Text angeordnet werden.

## <a name="related-links"></a>Verwandte Links

- [Platformbesonderheiten (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [Erstellen von Plattformeigenschaften](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [Windowsspecific-API](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific)
