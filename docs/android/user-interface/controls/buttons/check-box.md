---
title: CheckBox
ms.prod: xamarin
ms.assetid: A884AF10-D5EA-72CA-2301-B80CEC7FFBE7
ms.technology: xamarin-android
author: conceptdev
ms.author: crdun
ms.date: 02/06/2018
ms.openlocfilehash: 9f2fd10e5cfe28206d323b2769517c2584919232
ms.sourcegitcommit: 654df48758cea602946644d2175fbdfba59a64f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2019
ms.locfileid: "67829723"
---
# <a name="checkbox"></a>CheckBox

In diesem Abschnitt erstellen Sie ein Kontrollkästchen zur Auswahl von Elementen mithilfe der [`CheckBox`](https://developer.xamarin.com/api/type/Android.Widget.CheckBox)
widget. Wenn das Kontrollkästchen geklickt wird, wird eine eingeblendeten Nachricht den aktuellen Status des Kontrollkästchens angeben.

Öffnen der **Resources/layout/Main.axml** -Datei und fügen die [ `CheckBox` ](https://developer.xamarin.com/api/type/Android.Widget.CheckBox/) Element (innerhalb der [ `LinearLayout` ](https://developer.xamarin.com/api/type/Android.Widget.LinearLayout)):

```xml
<CheckBox android:id="@+id/checkbox"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="check it out" />
```

Etwas erfolgt, wenn der Status geändert wird, fügen Sie den folgenden Code am Ende der [`OnCreate()`](https://developer.xamarin.com/api/member/Android.App.Activity.OnCreate/p/Android.OS.Bundle/Android.OS.PersistableBundle)
Methode:

```csharp
CheckBox checkbox = FindViewById<CheckBox>(Resource.Id.checkbox);

checkbox.Click += (o, e) => {
    if (checkbox.Checked)
        Toast.MakeText (this, "Selected", ToastLength.Short).Show ();
    else
        Toast.MakeText (this, "Not selected", ToastLength.Short).Show ();
};
```

Hierbei werden zusammengefasst, die [`CheckBox`](https://developer.xamarin.com/api/type/Android.Widget.CheckBox/)
Element aus dem Layout, klicken Sie dann behandelt das Click-Ereignis, das definiert die Aktion, die vorgenommen werden, wenn das Kontrollkästchen geklickt wird. Beim Klicken auf die [`Checked`](https://developer.xamarin.com/api/property/Android.Widget.CompoundButton.Checked/)
-Eigenschaft wird aufgerufen, um den neuen Zustand des Kontrollkästchens zu überprüfen. Wenn sie überprüft wurde, wird eine [`Toast`](https://developer.xamarin.com/api/type/Android.Widget.Toast/)
Zeigt die Meldung "Selected", andernfalls wird "Nicht ausgewählt" angezeigt. Die [`CheckBox`](https://developer.xamarin.com/api/type/Android.Widget.CheckBox/)
verarbeitet die eigenen Zustandsänderungen, daher Sie nur den aktuellen Status Abfragen müssen.

Führen sie aus.

> [!TIP]
> Wenn Sie den Status selbst ändern möchten (z. B. beim Laden eine gespeicherte [ `CheckBoxPreference` ](https://developer.xamarin.com/api/type/Android.Preferences.CheckBoxPreference), verwenden Sie die [`Checked`](https://developer.xamarin.com/api/property/Android.Widget.CompoundButton.Checked)
> Eigenschaften-Setter oder [`Toggle()`](https://developer.xamarin.com/api/member/Android.Widget.CompoundButton.Toggle)
> -Methode.

*Teile dieser Seite werden Änderungen, die basierend auf der Arbeit erstellt und freigegeben werden, indem Sie das Android Open Source-Projekt, und gemäß den Bedingungen, die in beschriebenen verwendet die*
[*Creative Commons 2.5 Attribution-Lizenz* ](http://creativecommons.org/licenses/by/2.5/).
