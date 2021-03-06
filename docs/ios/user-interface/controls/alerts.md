---
title: Anzeigen von Warnungen in xamarin. IOS
description: In diesem Dokument wird beschrieben, wie Warnungen in xamarin. IOS mithilfe der in ios 8 eingeführten uialertcontroller-APIs angezeigt werden.
ms.prod: xamarin
ms.assetid: 61C671E9-3757-4052-86E4-28640025A34A
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/21/2017
ms.openlocfilehash: 1264b28b2ee56ec5de610350a199668c67d5c33c
ms.sourcegitcommit: 2fbe4932a319af4ebc829f65eb1fb1816ba305d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/29/2019
ms.locfileid: "73022104"
---
# <a name="displaying-alerts-in-xamarinios"></a>Anzeigen von Warnungen in xamarin. IOS

Ab IOS 8 hat uialertcontroller den ersetzten uiaktionsheet und UIAlertView abgeschlossen, die beide nun als veraltet markiert wurden.

Anders als bei den ersetzten Klassen, bei denen es sich um Unterklassen von UIView handelt, ist uialertcontroller eine Unterklasse von UIViewController.

Verwenden Sie `UIAlertControllerStyle`, um den Typ der Warnung anzugeben, die angezeigt werden soll. Diese Warnungs Typen lauten wie folgt:

- **Uialertcontrollerstylesheet**
  - Pre-IOS 8: Dies wäre ein uiaktionsheet.
- **Uialertcontrollerstylealert**
  - Pre-IOS 8: Dies wäre UIAlertView. 

Beim Erstellen eines Warnungs Controllers sind drei Schritte erforderlich:

- Erstellen und konfigurieren Sie die Warnung mit einem:
  - Titel
  - message
  - preferredstyle

- Optionale Textfeld hinzufügen
- Erforderliche Aktionen hinzufügen
- Zeigen Sie den Ansichts Controller an

Die einfachste Warnung enthält eine einzelne Schaltfläche, wie in diesem Screenshot gezeigt:

 ![Warnung mit einer Schaltfläche](alerts-images/alert1.png)

Der Code zum Anzeigen einer einfachen Warnung lautet wie folgt:

```csharp
okayButton.TouchUpInside += (sender, e) => {

    //Create Alert
    var okAlertController = UIAlertController.Create ("Title", "The message", UIAlertControllerStyle.Alert);

    //Add Action
    okAlertController.AddAction (UIAlertAction.Create ("OK", UIAlertActionStyle.Default, null));

    // Present Alert
    PresentViewController (okAlertController, true, null);
};
```

Die Anzeige einer Warnung mit mehreren Optionen erfolgt auf ähnliche Weise, aber es werden zwei Aktionen hinzugefügt. Der folgende Screenshot zeigt beispielsweise eine Warnung mit zwei Schaltflächen:

 ![Warnung mit zwei Schaltflächen](alerts-images/alert2.png)

```csharp
okayCancelButton.TouchUpInside += ((sender, e) => {

    //Create Alert
    var okCancelAlertController = UIAlertController.Create("Alert Title", "Choose from two buttons", UIAlertControllerStyle.Alert);

    //Add Actions
    okCancelAlertController.AddAction(UIAlertAction.Create("OK", UIAlertActionStyle.Default, alert => Console.WriteLine ("Okay was clicked")));
    okCancelAlertController.AddAction(UIAlertAction.Create("Cancel", UIAlertActionStyle.Cancel, alert => Console.WriteLine ("Cancel was clicked")));

    //Present Alert
    PresentViewController(okCancelAlertController, true, null);
});
```

Warnungen können auch ein Aktions Blatt ähnlich dem folgenden Screenshot anzeigen:

 ![Warnung zu Aktions Blatt](alerts-images/alert3.png)

Der Warnung werden mit der `AddAction`-Methode Schaltflächen hinzugefügt:

```csharp
actionSheetButton.TouchUpInside += ((sender, e) => {

    // Create a new Alert Controller
    UIAlertController actionSheetAlert = UIAlertController.Create("Action Sheet", "Select an item from below", UIAlertControllerStyle.ActionSheet);

    // Add Actions
    actionSheetAlert.AddAction(UIAlertAction.Create("OK",UIAlertActionStyle.Default, (action) => Console.WriteLine ("Item One pressed.")));

    actionSheetAlert.AddAction(UIAlertAction.Create("custom button 1",UIAlertActionStyle.Default, (action) => Console.WriteLine ("Item Two pressed.")));

    actionSheetAlert.AddAction(UIAlertAction.Create("Cancel",UIAlertActionStyle.Cancel, (action) => Console.WriteLine ("Cancel button pressed.")));

    // Required for iPad - You must specify a source for the Action Sheet since it is
    // displayed as a popover
    UIPopoverPresentationController presentationPopover = actionSheetAlert.PopoverPresentationController;
    if (presentationPopover!=null) {
        presentationPopover.SourceView = this.View;
        presentationPopover.PermittedArrowDirections = UIPopoverArrowDirection.Up;
    }

    // Display the alert
    this.PresentViewController(actionSheetAlert,true,null);
});
```

## <a name="related-links"></a>Verwandte Links

- [Steuerelemente (Beispiel)](https://docs.microsoft.com/samples/xamarin/ios-samples/controls)
- [Warnungs Controller](https://github.com/xamarin/recipes/tree/master/Recipes/ios/standard_controls/alertcontroller)
