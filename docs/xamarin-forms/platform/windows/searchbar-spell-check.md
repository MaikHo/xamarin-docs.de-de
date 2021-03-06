---
title: " Searchbar-Rechtschreibprüfung unter Windows"
description: Platt Form Besonderheiten ermöglichen es Ihnen, Funktionen zu nutzen, die nur auf einer bestimmten Plattform verfügbar sind, ohne dass benutzerdefinierte Renderer oder Effekte implementiert werden. In diesem Artikel wird erläutert, wie Sie das Windows-plattformspezifische verwenden können, das es einer Suchleiste ermöglicht, mit dem Rechtschreib Prüfungs Modul zu interagieren.
ms.prod: xamarin
ms.assetid: 7974C91F-7502-4DB3-B0E9-C45E943DDA26
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/24/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: f6c8810ea37c767ef67c7f53d312b63a9de09f26
ms.sourcegitcommit: 32d2476a5f9016baa231b7471c88c1d4ccc08eb8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2020
ms.locfileid: "84136564"
---
# <a name="searchbar-spell-check-on-windows"></a>Searchbar-Rechtschreibprüfung unter Windows

[![Beispiel herunterladen](~/media/shared/download.png) Das Beispiel herunterladen](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

Diese universelle Windows-Plattform plattformspezifisch ermöglicht einem [`SearchBar`](xref:Xamarin.Forms.SearchBar) die Interaktion mit der Rechtschreibprüfung. Sie wird in XAML verwendet, indem die [`SearchBar.IsSpellCheckEnabled`](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.SearchBar.IsSpellCheckEnabledProperty) angefügte-Eigenschaft auf einen Wert festgelegt wird `boolean` :

```xaml
<ContentPage ...
             xmlns:windows="clr-namespace:Xamarin.Forms.PlatformConfiguration.WindowsSpecific;assembly=Xamarin.Forms.Core">
    <StackLayout>
        <SearchBar ... windows:SearchBar.IsSpellCheckEnabled="true" />
        ...
    </StackLayout>
</ContentPage>
```

Alternativ kann Sie mithilfe der flüssigen API von c# genutzt werden:

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.WindowsSpecific;
...

searchBar.On<Windows>().SetIsSpellCheckEnabled(true);
```

Die- `SearchBar.On<Windows>` Methode gibt an, dass diese plattformspezifische nur auf der universelle Windows-Plattform ausgeführt wird. [ `SearchBar.SetIsSpellCheckEnabled` ] (Xref: Xamarin.Forms . Platformconfiguration. windowsspecific. Searchbar. *-Rechtschreib Check aktiviert ( Xamarin.Forms . Iplatformelementconfiguration { Xamarin.Forms . Platformconfiguration. Windows, Xamarin.Forms . Searchbar}, System. Boolean))-Methode im- [`Xamarin.Forms.PlatformConfiguration.WindowsSpecific`](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific) Namespace schaltet die Rechtschreibprüfung ein und aus. Außerdem kann die- `SearchBar.SetIsSpellCheckEnabled` Methode verwendet werden, um die Rechtschreibprüfung durch Aufrufen von [ `SearchBar.GetIsSpellCheckEnabled` ] (Xref:) zu wechseln Xamarin.Forms . Platformconfiguration. windowsspecific. Searchbar. getisrechtschreib checkaktivierte ( Xamarin.Forms . Iplatformelementconfiguration { Xamarin.Forms . Platformconfiguration. Windows, Xamarin.Forms . Searchbar})) Methode, die zurückgibt, ob die Rechtschreibprüfung aktiviert ist:

```csharp
searchBar.On<Windows>().SetIsSpellCheckEnabled(!searchBar.On<Windows>().GetIsSpellCheckEnabled());
```

Das Ergebnis ist, dass der in das eingegebene Text [`SearchBar`](xref:Xamarin.Forms.SearchBar) Rechtschreibprüfung ausführen kann, wobei dem Benutzer falsche Rechtschreib Werte angezeigt werden:

![Plattformspezifische Überprüfung der Suchleiste](searchbar-spell-check-images/searchbar-spellcheck.png "Plattformspezifische Überprüfung der Suchleiste")

> [!NOTE]
> Die `SearchBar` -Klasse im [`Xamarin.Forms.PlatformConfiguration.WindowsSpecific`](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific) -Namespace verfügt auch über die [`EnableSpellCheck`](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.SearchBar.EnableSpellCheck*) -Methode und die- [`DisableSpellCheck`](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.SearchBar.DisableSpellCheck*) Methode, die verwendet werden können, um die Rechtschreibprüfung für die zu aktivieren und zu deaktivieren `SearchBar` .

## <a name="related-links"></a>Verwandte Links

- [Platformbesonderheiten (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [Erstellen von Plattformeigenschaften](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [Windowsspecific-API](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific)
