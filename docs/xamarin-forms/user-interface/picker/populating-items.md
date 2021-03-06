---
title: Hinzufügen von Daten zur Elementsammlung einer Auswahl
description: Die Auswahl Ansicht ist ein Steuerelement zum Auswählen eines Text Elements aus einer Datenliste. In diesem Artikel wird erläutert, wie eine Auswahl mit Daten aufgefüllt wird, indem Sie der Items-Sammlung hinzugefügt wird und wie auf die Elementauswahl durch den Benutzer reagiert wird.
ms.prod: xamarin
ms.assetid: 3C840F64-A430-457D-A4B2-3D7AF46F9DBE
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 02/26/2019
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 8872c6748ba778a2622d82803d580c781bd282cd
ms.sourcegitcommit: 32d2476a5f9016baa231b7471c88c1d4ccc08eb8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2020
ms.locfileid: "84139632"
---
# <a name="adding-data-to-a-pickers-items-collection"></a>Hinzufügen von Daten zur Elementsammlung einer Auswahl

[![Beispiel herunterladen](~/media/shared/download.png) Das Beispiel herunterladen](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-pickerdemo)

_Die Auswahl Ansicht ist ein Steuerelement zum Auswählen eines Text Elements aus einer Datenliste. In diesem Artikel wird erläutert, wie eine Auswahl mit Daten aufgefüllt wird, indem Sie der Items-Sammlung hinzugefügt wird und wie auf die Elementauswahl durch den Benutzer reagiert wird._

## <a name="populating-a-picker-with-data"></a>Auffüllen einer Auswahl mit Daten

Vor Xamarin.Forms 2.3.4 bestand der Vorgang zum Auffüllen eines [`Picker`](xref:Xamarin.Forms.Picker) mit Daten darin, die anzuzeigenden Daten der schreibgeschützten Auflistung hinzuzufügen [`Items`](xref:Xamarin.Forms.Picker.Items) , die vom Typ ist `IList<string>` . Jedes Element in der Auflistung muss den Typ aufweisen `string` . Elemente können in XAML hinzugefügt werden, indem die- `Items` Eigenschaft mit einer Liste von Elementen initialisiert wird `x:String` :

```xaml
<Picker Title="Select a monkey"
        TitleColor="Red">
  <Picker.Items>
    <x:String>Baboon</x:String>
    <x:String>Capuchin Monkey</x:String>
    <x:String>Blue Monkey</x:String>
    <x:String>Squirrel Monkey</x:String>
    <x:String>Golden Lion Tamarin</x:String>
    <x:String>Howler Monkey</x:String>
    <x:String>Japanese Macaque</x:String>
  </Picker.Items>
</Picker>
```

Der entsprechende c#-Code wird unten dargestellt:

```csharp
var picker = new Picker { Title = "Select a monkey", TitleColor = Color.Red };
picker.Items.Add("Baboon");
picker.Items.Add("Capuchin Monkey");
picker.Items.Add("Blue Monkey");
picker.Items.Add("Squirrel Monkey");
picker.Items.Add("Golden Lion Tamarin");
picker.Items.Add("Howler Monkey");
picker.Items.Add("Japanese Macaque");
```

Zusätzlich zum Hinzufügen von Daten mithilfe der- `Items.Add` Methode können Daten auch mithilfe der-Methode in die-Auflistung eingefügt werden `Items.Insert` .

## <a name="responding-to-item-selection"></a>Antworten auf die Elementauswahl

Ein [`Picker`](xref:Xamarin.Forms.Picker) unterstützt jeweils nur ein Element. Wenn ein Benutzer ein Element auswählt, [`SelectedIndexChanged`](xref:Xamarin.Forms.Picker.SelectedIndexChanged) wird das-Ereignis ausgelöst, und die- [`SelectedIndex`](xref:Xamarin.Forms.Picker.SelectedIndex) Eigenschaft wird auf eine ganze Zahl aktualisiert, die den Index des ausgewählten Elements in der Liste darstellt. Die `SelectedIndex` -Eigenschaft ist eine Null basierte Zahl, die das Element angibt, das der Benutzer ausgewählt hat. Wenn kein Element ausgewählt ist (Dies ist der Fall, wenn das `Picker` erstmalig erstellt und initialisiert wird), hat den Wert `SelectedIndex` -1.

> [!NOTE]
> Das Elementauswahl Verhalten in einem [`Picker`](xref:Xamarin.Forms.Picker) kann unter IOS mit einem plattformspezifischen angepasst werden. Weitere Informationen finden Sie unter [Steuern der Auswahl des Auswahl Elements](~/xamarin-forms/platform/ios/picker-selection.md).

Das folgende Codebeispiel zeigt die `OnPickerSelectedIndexChanged` Ereignishandlermethode, die ausgeführt wird, wenn das Ereignis ausgelöst wird [`SelectedIndexChanged`](xref:Xamarin.Forms.Picker.SelectedIndexChanged) :

```csharp
void OnPickerSelectedIndexChanged(object sender, EventArgs e)
{
  var picker = (Picker)sender;
  int selectedIndex = picker.SelectedIndex;

  if (selectedIndex != -1)
  {
    monkeyNameLabel.Text = picker.Items[selectedIndex];
  }
}
```

Diese Methode ruft den [`SelectedIndex`](xref:Xamarin.Forms.Picker.SelectedIndex) -Eigenschafts Wert ab und verwendet den-Wert, um das ausgewählte Element aus der Auflistung abzurufen [`Items`](xref:Xamarin.Forms.Picker.Items) . Da jedes Element in der Auflistung `Items` eine ist `string` , kann es von einem angezeigt werden, [`Label`](xref:Xamarin.Forms.Label) ohne dass eine Umwandlung erforderlich ist.

> [!NOTE]
> Ein [`Picker`](xref:Xamarin.Forms.Picker) kann initialisiert werden, um ein bestimmtes Element anzuzeigen, indem die-Eigenschaft festgelegt wird [`SelectedIndex`](xref:Xamarin.Forms.Picker.SelectedIndex) . Die- `SelectedIndex` Eigenschaft muss jedoch nach dem Initialisieren der-Auflistung festgelegt werden [`Items`](xref:Xamarin.Forms.Picker.Items) .

## <a name="related-links"></a>Verwandte Links

- [Auswahl Demo (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-pickerdemo)
- [Auswahl](xref:Xamarin.Forms.Picker)
