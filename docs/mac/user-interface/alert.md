---
title: Warnungen in xamarin. Mac
description: In diesem Artikel wird das Arbeiten mit Warnungen in einer xamarin. Mac-Anwendung behandelt. Es beschreibt das Erstellen und Anzeigen von Warnungen aus c#-Code und das reagieren auf Benutzerinteraktionen.
ms.prod: xamarin
ms.assetid: F1DB93A1-7549-4540-AD5E-D7605CCD8435
ms.technology: xamarin-mac
author: davidortinau
ms.author: daortin
ms.date: 03/14/2017
ms.openlocfilehash: 00e5b2a2238763822172a1b7d7a7c3090634ed17
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/22/2020
ms.locfileid: "86938085"
---
# <a name="alerts-in-xamarinmac"></a>Warnungen in xamarin. Mac

_In diesem Artikel wird das Arbeiten mit Warnungen in einer xamarin. Mac-Anwendung behandelt. Es beschreibt das Erstellen und Anzeigen von Warnungen aus c#-Code und das reagieren auf Benutzerinteraktionen._

Wenn Sie mit c# und .net in einer xamarin. Mac-Anwendung arbeiten, haben Sie Zugriff auf dieselben Warnungen, die ein Entwickler in *Ziel-C* und *Xcode* verwendet. 

Eine Warnung ist eine besondere Art von Dialogfeld, das angezeigt wird, wenn ein schwerwiegendes Problem auftritt (z. b. ein Fehler) oder eine Warnung (z. b. das Löschen einer Datei). Da es sich bei einer Warnung um ein Dialogfeld handelt, ist auch eine Benutzer Antwort erforderlich, bevor Sie geschlossen werden kann.

[![Beispiel für eine Warnung](alert-images/alert06.png)](alert-images/alert06.png#lightbox)

In diesem Artikel werden die Grundlagen der Arbeit mit Warnungen in einer xamarin. Mac-Anwendung behandelt. 

<a name="Introduction_to_Alerts"></a>

## <a name="introduction-to-alerts"></a>Einführung in Warnungen

Eine Warnung ist eine besondere Art von Dialogfeld, das angezeigt wird, wenn ein schwerwiegendes Problem auftritt (z. b. ein Fehler) oder eine Warnung (z. b. das Löschen einer Datei). Da Warnungen den Benutzer stören, da sie verworfen werden müssen, bevor der Benutzer mit der Aufgabe fortfahren kann, sollten Sie eine Warnung nur anzeigen, wenn dies unbedingt erforderlich ist.

Apple empfiehlt die folgenden Richtlinien:

- Verwenden Sie nur eine Warnung, um den Benutzern Informationen zu senden.
- Es wird keine Warnung für allgemeine, nicht doable-Aktionen angezeigt. Auch wenn diese Situation zu Datenverlusten führen kann.
- Wenn eine Situation eine Warnung ist, sollten Sie die Verwendung eines anderen Benutzeroberflächen Elements oder einer anderen Methode zum Anzeigen vermeiden.
- Das Symbol "Vorsicht" sollte sparsam verwendet werden.
- Beschreiben Sie die Warnungs Situation eindeutig und kurz in der Warnmeldung.
- Der Standardname der Schaltfläche sollte der Aktion entsprechen, die Sie in der Warnmeldung beschreiben.

Weitere Informationen finden Sie im Abschnitt " [Warnungen](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/OSXHIGuidelines/WindowAlerts.html#//apple_ref/doc/uid/20000957-CH44-SW1) " in den [Richtlinien für die Benutzeroberfläche von Apple OS X](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/OSXHIGuidelines/) .

<a name="Anatomy_of_an_Alert"></a>

## <a name="anatomy-of-an-alert"></a>Anatomie einer Warnung

Wie bereits erwähnt, sollten dem Benutzer der Anwendung Warnungen angezeigt werden, wenn ein schwerwiegendes Problem auftritt, oder als Warnung für potenziellen Datenverlust (z. b. das Schließen einer nicht gespeicherten Datei). In xamarin. Mac wird eine Warnung in c#-Code erstellt, z. b.:

```csharp
var alert = new NSAlert () {
  AlertStyle = NSAlertStyle.Critical,
  InformativeText = "We need to save the document here...",
  MessageText = "Save Document",
};
alert.RunModal ();
```

Der obige Code zeigt eine Warnung an, bei der das Anwendungssymbol auf dem Warnungs Symbol, einem Titel, einer Warnmeldung und einer einzelnen Schaltfläche " **OK** " überlagert wurde:

[![Eine Warnung mit der Schaltfläche "OK"](alert-images/alert01.png)](alert-images/alert01.png#lightbox)

Apple bietet verschiedene Eigenschaften, die verwendet werden können, um eine Warnung anzupassen:

- **AlertStyle** definiert den Typ einer Warnung als eine der folgenden:
  - **Warnung** : wird verwendet, um den Benutzer zu einem aktuellen oder bevorstehenden Ereignis zu warnen, das nicht kritisch ist. Dies ist das Standardformat.
  - **Information** -wird verwendet, um den Benutzer vor einem aktuellen oder bevorstehenden Ereignis zu warnen. Zurzeit gibt es keinen sichtbaren Unterschied zwischen einer **Warnung** und einem **Informations** -
  - **Kritisch** : wird verwendet, um den Benutzer vor schwerwiegenden Konsequenzen eines bevorstehenden Ereignisses (z. b. Löschen einer Datei) zu warnen. Diese Art von Warnung sollte sparsam verwendet werden.
- **MessageText** : Dies ist die Haupt Nachricht oder der Titel der Warnung und sollte schnell die Situation für den Benutzer definieren.
- **InformativeText** : Hierbei handelt es sich um den Hauptteil der Warnung, bei der Sie die Situation eindeutig definieren und dem Benutzer die Möglichkeit zur Verfügung stellen müssen.
- **Symbol** : Hiermit kann ein benutzerdefiniertes Symbol für den Benutzer angezeigt werden.
- **Helpanchor**  &  **Showshelp** : ermöglicht die Bindung der Warnung an das Anwendungs helpbook und das Anzeigen der Hilfe für die Warnung.
- **Schaltflächen: Standard** mäßig hat eine Warnung nur die Schaltfläche **OK** , aber mit der Auflistung **Buttons** können Sie je nach Bedarf weitere Optionen hinzufügen.
- **Showssuppressionbutton** -if `true` zeigt ein Kontrollkästchen an, mit dem der Benutzer die Warnung für nachfolgende Vorkommen des Ereignisses unterdrücken kann, von dem das Ereignis ausgelöst wurde.
- **Accessoryview** : ermöglicht das Anfügen einer anderen unter Ansicht an die Warnung, um zusätzliche Informationen bereitzustellen, z. b. das Hinzufügen eines **Textfelds** für die Dateneingabe. Wenn Sie eine neue **accessoryview** festlegen oder eine vorhandene ändern, müssen Sie die- `Layout()` Methode zum Anpassen des sichtbaren Layouts der Warnung aufruft.

<a name="Displaying_an_Alert"></a>

## <a name="displaying-an-alert"></a>Anzeigen einer Warnung

Es gibt zwei unterschiedliche Möglichkeiten, wie eine Warnung angezeigt werden kann, eine freie Gleit Komma Zahl oder ein Blatt. Der folgende Code zeigt eine Warnung als frei Gleit Komma Zahl an:

```csharp
var alert = new NSAlert () {
  AlertStyle = NSAlertStyle.Informational,
  InformativeText = "This is the body of the alert where you describe the situation and any actions to correct it.",
  MessageText = "Alert Title",
};
alert.RunModal ();
```

Wenn dieser Code ausgeführt wird, wird Folgendes angezeigt:

[![Eine einfache Warnung](alert-images/alert02.png)](alert-images/alert02.png#lightbox)

Der folgende Code zeigt dieselbe Warnung an wie ein Blatt:

```csharp
var alert = new NSAlert () {
  AlertStyle = NSAlertStyle.Informational,
  InformativeText = "This is the body of the alert where you describe the situation and any actions to correct it.",
  MessageText = "Alert Title",
};
alert.BeginSheet (this);
```

Wenn dieser Code ausgeführt wird, wird Folgendes angezeigt:

[![Eine Warnung, die als Blatt angezeigt wird.](alert-images/alert03.png)](alert-images/alert03.png#lightbox)

<a name="Working_with_Alert_Buttons"></a>

## <a name="working-with-alert-buttons"></a>Arbeiten mit Warn Schaltflächen

Standardmäßig wird in einer Warnung nur die Schaltfläche **OK** angezeigt. Sie sind jedoch nicht darauf beschränkt. Sie können zusätzliche Schaltflächen erstellen, indem Sie Sie an die **Schalt** Flächen Auflistung anhängen. Der folgende Code erstellt eine unverankerte Warnung mit der Schaltfläche **OK**, **Abbrechen** und **vielleicht** :

```csharp
var alert = new NSAlert () {
  AlertStyle = NSAlertStyle.Informational,
  InformativeText = "This is the body of the alert where you describe the situation and any actions to correct it.",
  MessageText = "Alert Title",
};
alert.AddButton ("Ok");
alert.AddButton ("Cancel");
alert.AddButton ("Maybe");
var result = alert.RunModal ();
```

Die erste Schaltfläche, die hinzugefügt wird, ist die _Standard_ Schaltfläche, die aktiviert wird, wenn der Benutzer die EINGABETASTE drückt. Der zurückgegebene Wert ist eine ganze Zahl, die angibt, welche Schaltfläche der Benutzer gedrückt hat. In unserem Fall werden die folgenden Werte zurückgegeben:

- **OK** -1000.
- **Abbrechen** -1001.
- **Vielleicht** -1002.

Wenn Sie den Code ausführen, wird Folgendes angezeigt:

[![Eine Warnung mit drei Schaltflächen Optionen](alert-images/alert04.png)](alert-images/alert04.png#lightbox)

Dies ist der Code für dieselbe Warnung wie ein Blatt:

```csharp
var alert = new NSAlert () {
  AlertStyle = NSAlertStyle.Informational,
  InformativeText = "This is the body of the alert where you describe the situation and any actions to correct it.",
  MessageText = "Alert Title",
};
alert.AddButton ("Ok");
alert.AddButton ("Cancel");
alert.AddButton ("Maybe");
alert.BeginSheetForResponse (this, (result) => {
  Console.WriteLine ("Alert Result: {0}", result);
});
```

Wenn dieser Code ausgeführt wird, wird Folgendes angezeigt:

[![Eine drei Schaltflächen Warnung wird als Blatt angezeigt.](alert-images/alert05.png)](alert-images/alert05.png#lightbox)

> [!IMPORTANT]
> Sie sollten einer Warnung niemals mehr als drei Schaltflächen hinzufügen.

<a name="Showing_the_Suppress_Button"></a>

## <a name="showing-the-suppress-button"></a>Schaltfläche "unterdrücken"

Wenn die-Eigenschaft der Warnung `ShowSuppressButton` ist `true` , wird in der Warnung ein Kontrollkästchen angezeigt, mit dem der Benutzer die Warnung für nachfolgende Vorkommen des Ereignisses unterdrücken kann, von dem das Ereignis ausgelöst wurde. Im folgenden Code wird eine unverankerte Warnung mit der Schaltfläche unterdrücken angezeigt:

```csharp
var alert = new NSAlert () {
  AlertStyle = NSAlertStyle.Informational,
  InformativeText = "This is the body of the alert where you describe the situation and any actions to correct it.",
  MessageText = "Alert Title",
};
alert.AddButton ("Ok");
alert.AddButton ("Cancel");
alert.AddButton ("Maybe");
alert.ShowsSuppressionButton = true;
var result = alert.RunModal ();
Console.WriteLine ("Alert Result: {0}, Suppress: {1}", result, alert.SuppressionButton.State == NSCellStateValue.On);
```

Wenn der Wert von `alert.SuppressionButton.State` ist `NSCellStateValue.On` , hat der Benutzer das Kontrollkästchen unterdrücken aktiviert, andernfalls ist dies nicht der Fall.

Wenn der Code ausgeführt wird, wird Folgendes angezeigt:

[![Eine Warnung mit der Schaltfläche "unterdrücken"](alert-images/alert06.png)](alert-images/alert06.png#lightbox)

Dies ist der Code für dieselbe Warnung wie ein Blatt:

```csharp
var alert = new NSAlert () {
  AlertStyle = NSAlertStyle.Informational,
  InformativeText = "This is the body of the alert where you describe the situation and any actions to correct it.",
  MessageText = "Alert Title",
};
alert.AddButton ("Ok");
alert.AddButton ("Cancel");
alert.AddButton ("Maybe");
alert.ShowsSuppressionButton = true;
alert.BeginSheetForResponse (this, (result) => {
  Console.WriteLine ("Alert Result: {0}, Suppress: {1}", result, alert.SuppressionButton.State == NSCellStateValue.On);
});
```

Wenn dieser Code ausgeführt wird, wird Folgendes angezeigt:

[![Eine Warnung mit der Schaltfläche "unterdrücken" als Blatt](alert-images/alert07.png)](alert-images/alert07.png#lightbox)

<a name="Adding_a_Custom_SubView"></a>

## <a name="adding-a-custom-subview"></a>Hinzufügen einer benutzerdefinierten unter Ansicht

Warnungen verfügen über eine- `AccessoryView` Eigenschaft, die zum weiteren Anpassen der Warnung und zum Hinzufügen von Elementen wie einem **Textfeld** für Benutzereingaben verwendet werden kann. Mit dem folgenden Code wird eine unverankerte Warnung mit einem hinzugefügten Texteingabefeld erstellt:

```csharp
var input = new NSTextField (new CGRect (0, 0, 300, 20));

var alert = new NSAlert () {
AlertStyle = NSAlertStyle.Informational,
InformativeText = "This is the body of the alert where you describe the situation and any actions to correct it.",
  MessageText = "Alert Title",
};
alert.AddButton ("Ok");
alert.AddButton ("Cancel");
alert.AddButton ("Maybe");
alert.ShowsSuppressionButton = true;
alert.AccessoryView = input;
alert.Layout ();
var result = alert.RunModal ();
Console.WriteLine ("Alert Result: {0}, Suppress: {1}", result, alert.SuppressionButton.State == NSCellStateValue.On);
```

In den folgenden Schlüssel Zeilen `var input = new NSTextField (new CGRect (0, 0, 300, 20));` wird ein neues **Textfeld** erstellt, in dem die Warnung hinzugefügt wird. `alert.AccessoryView = input;`Dabei wird das **Textfeld** an die Warnung angefügt und der-Befehl an die- `Layout()` Methode übergeben, die für die Größe der Warnung an die neue unter Ansicht angepasst werden muss.

Wenn Sie den Code ausführen, wird Folgendes angezeigt:

[![Wenn Sie den Code ausführen, wird Folgendes angezeigt:](alert-images/alert08.png)](alert-images/alert08.png#lightbox)

Dies ist dieselbe Warnung wie ein Blatt:

```csharp
var input = new NSTextField (new CGRect (0, 0, 300, 20));

var alert = new NSAlert () {
  AlertStyle = NSAlertStyle.Informational,
  InformativeText = "This is the body of the alert where you describe the situation and any actions to correct it.",
  MessageText = "Alert Title",
};
alert.AddButton ("Ok");
alert.AddButton ("Cancel");
alert.AddButton ("Maybe");
alert.ShowsSuppressionButton = true;
alert.AccessoryView = input;
alert.Layout ();
alert.BeginSheetForResponse (this, (result) => {
  Console.WriteLine ("Alert Result: {0}, Suppress: {1}", result, alert.SuppressionButton.State == NSCellStateValue.On);
});
```

Wenn Sie diesen Code ausführen, wird Folgendes angezeigt:

[![Eine Warnung mit einer benutzerdefinierten Ansicht](alert-images/alert09.png)](alert-images/alert09.png#lightbox)

<a name="Summary"></a>

## <a name="summary"></a>Zusammenfassung

In diesem Artikel wurde die Arbeit mit Warnungen in einer xamarin. Mac-Anwendung ausführlich erläutert. Wir haben die verschiedenen Typen und Verwendungsmöglichkeiten von Warnungen gesehen, das Erstellen und Anpassen von Warnungen und das Arbeiten mit Warnungen in c#-Code.

## <a name="related-links"></a>Ähnliche Themen

- [Macwindows (Beispiel)](https://docs.microsoft.com/samples/xamarin/mac-samples/macwindows)
- [Hello, Mac (Hallo Mac)](~/mac/get-started/hello-mac.md)
- [Arbeiten mit Windows](~/mac/user-interface/window.md)
- [Eingaberichtlinien für OS X](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/OSXHIGuidelines/)
- [Einführung in Windows](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/WinPanel/Introduction.html#//apple_ref/doc/uid/10000031-SW1)
- [Nsalert](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Classes/NSAlert_Class/index.html#//apple_ref/doc/uid/TP40004001)
