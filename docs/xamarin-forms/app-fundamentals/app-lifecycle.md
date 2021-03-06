---
title: Lebenszyklus der Xamarin.Forms-App
description: In diesem Artikel wird erläutert, wie Sie auf den Lebenszyklus der App reagieren, einschließlich Lebenszyklusmethoden, Seitenbenachrichtigungsereignisse und modaler Navigationsereignisse.
ms.prod: xamarin
ms.assetid: 69B416CF-B243-4790-AB29-F030B32465BE
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 05/31/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 2a67d0c3adb54332bf30879a5b6f1d086581f0ec
ms.sourcegitcommit: 32d2476a5f9016baa231b7471c88c1d4ccc08eb8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2020
ms.locfileid: "84573338"
---
# <a name="xamarinforms-app-lifecycle"></a>Lebenszyklus der Xamarin.Forms-App

Die [`Application`](xref:Xamarin.Forms.Application)-Basisklasse bietet folgende Features:

- [Lebenszyklusmethoden:](#lifecycle-methods) `OnStart`, `OnSleep` und `OnResume`
- [Seitennavigationsereignisse:](#page-navigation-events) [`PageAppearing`](xref:Xamarin.Forms.Application.PageAppearing), [`PageDisappearing`](xref:Xamarin.Forms.Application.PageDisappearing)
- [Modale Navigationsereignisse:](#modal-navigation-events) `ModalPushing`, `ModalPushed`, `ModalPopping` und `ModalPopped`

## <a name="lifecycle-methods"></a>Lebenszyklusmethoden

Die [`Application`](xref:Xamarin.Forms.Application)-Klasse enthält drei virtuelle Methoden, die überarbeitet werden können, um auf Lebenszyklusänderungen zu reagieren:

- `OnStart`: Wird aufgerufen, wenn die App startet.
- `OnSleep`: Wird jedes Mal aufgerufen, wenn die Ausführung der App im Hintergrund fortgesetzt wird.
- `OnResume`: Wird aufgerufen, wenn die App aus dem Hintergrund aufgerufen und fortgesetzt wird.

> [!NOTE]
> Es gibt *keine* Methode zum Beenden der App. Unter normalen Umständen (d.h. kein Absturz) wird die App im Status *OnSleep* beendet, ohne dass Ihr Code darüber benachrichtigt wird.

Implementieren Sie wie nachfolgend veranschaulicht einen `WriteLine`-Aufruf in jeder Methode, und testen Sie diesen auf jeder Plattform. So können Sie beobachten, wann die Methoden aufgerufen werden.

```csharp
protected override void OnStart()
{
    Debug.WriteLine ("OnStart");
}
protected override void OnSleep()
{
    Debug.WriteLine ("OnSleep");
}
protected override void OnResume()
{
    Debug.WriteLine ("OnResume");
}
```

> [!IMPORTANT]
> Unter Android wird die `OnStart`-Methode rotierend und beim ersten Ausführen der App aufgerufen, wenn `ConfigurationChanges = ConfigChanges.ScreenSize | ConfigChanges.Orientation` im `[Activity()]`-Attribut in der Hauptaktivität nicht vorhanden ist.

## <a name="page-navigation-events"></a>Seitennavigationsereignisse

Die [`Application`](xref:Xamarin.Forms.Application)-Klasse verfügt über zwei Ereignisse, die Benachrichtigungen zu angezeigten und ausgeblendeten Seiten bereitstellt:

- [`PageAppearing`](xref:Xamarin.Forms.Application.PageAppearing): Wird ausgelöst, wenn eine Seite auf dem Bildschirm angezeigt wird.
- [`PageDisappearing`](xref:Xamarin.Forms.Application.PageDisappearing): Wird ausgelöst, wenn eine Seite auf dem Bildschirm ausgeblendet wird.

Diese Ereignisse können in Szenarios verwendet werden, bei denen Sie Seiten beim Anzeigen auf dem Bildschirm nachverfolgen möchten.

> [!NOTE]
> Die Ereignisse [`PageAppearing`](xref:Xamarin.Forms.Application.PageAppearing) und [`PageDisappearing`](xref:Xamarin.Forms.Application.PageDisappearing) werden unmittelbar nach den Ereignissen [`Page.Appearing`](xref:Xamarin.Forms.Page.Appearing) und [`Page.Disappearing`](xref:Xamarin.Forms.Page.Disappearing) in der [`Page`](xref:Xamarin.Forms.Page)-Basisklasse ausgelöst.

## <a name="modal-navigation-events"></a>Modale Navigationsereignisse

Es gibt vier Ereignisse in der [`Application`](xref:Xamarin.Forms.Application)-Klasse (jedes enthält eigen Ereignisargumente), mit deren Hilfe Sie auf modale Seiten reagieren können, die angezeigt und geschlossen werden:

- `ModalPushing`: Wird ausgelöst, wenn eine Seite modal mithilfe von Push übertragen wird.
- `ModalPushed`: Wird ausgelöst, nachdem eine Seite modal mithilfe von Push übertragen wurde.
- `ModalPopping`: Wird ausgelöst, wenn eine Seite modal angehalten wird.
- `ModalPopped`: Wird ausgelöst, nachdem eine Seite modal angehalten wurde.

> [!NOTE]
> Die `ModalPopping`-Ereignisargumente vom Typ `ModalPoppingEventArgs` enthalten eine `Cancel`-Eigenschaft. Wenn `Cancel` auf `true` festgelegt ist, wird der modale Pop geschlossen.
