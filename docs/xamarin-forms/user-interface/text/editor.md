---
title: Xamarin.Forms Editor
description: In diesem Artikel wird erläutert, wie das Xamarin.Forms Editor-Steuerelement verwendet wird, um mehrzeilige Texteingaben in einer Anwendung zu akzeptieren.
ms.prod: xamarin
ms.assetid: 7074DB3A-30D2-4A6B-9A89-B029EEF20B07
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/21/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 3a7dedad6fc33b75a687f94897b64d04a72a0b08
ms.sourcegitcommit: 08290d004d1a7e7ac579bf1f96abf8437921dc70
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87918434"
---
# <a name="no-locxamarinforms-editor"></a>Xamarin.Forms Editor

[![Beispiel herunterladen](~/media/shared/download.png) Herunterladen des Beispiels](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-text)

Das- [`Editor`](xref:Xamarin.Forms.Editor) Steuerelement wird verwendet, um mehrzeilige Eingaben zu akzeptieren.

## <a name="set-and-read-text"></a>Festlegen und Lesen von Text

Die [`Editor`](xref:Xamarin.Forms.Editor) -Eigenschaft wird wie bei anderen Text dargestellten Sichten von verfügbar gemacht `Text` . Diese Eigenschaft kann verwendet werden, um den von dargestellten Text festzulegen und zu lesen `Editor` . Im folgenden Beispiel wird veranschaulicht, wie die- `Text` Eigenschaft in XAML festgelegt wird:

```xaml
<Editor Text="I am an Editor" />
```

In C#:

```csharp
var MyEditor = new Editor { Text = "I am an Editor" };
```

Um Text zu lesen, greifen Sie `Text` in c# auf die-Eigenschaft zu:

```csharp
var text = MyEditor.Text;
```

## <a name="set-placeholder-text"></a>Platzhalter Text festlegen

[`Editor`](xref:Xamarin.Forms.Editor)Kann so festgelegt werden, dass Platzhalter Text angezeigt wird, wenn keine Benutzereingaben gespeichert werden. Dies wird erreicht, indem die [`Placeholder`](xref:Xamarin.Forms.InputView.Placeholder) -Eigenschaft auf festgelegt wird `string` und häufig verwendet wird, um den Typ des Inhalts anzugeben, der für geeignet ist `Editor` . Außerdem kann die Platzhalter Textfarbe gesteuert werden, indem die-Eigenschaft auf festgelegt wird [`PlaceholderColor`](xref:Xamarin.Forms.InputView.PlaceholderColor) [`Color`](xref:Xamarin.Forms.Color) :

```xaml
<Editor Placeholder="Enter text here" PlaceholderColor="Olive" />
```

```csharp
var editor = new Editor { Placeholder = "Enter text here", PlaceholderColor = Color.Olive };
```

## <a name="prevent-text-entry"></a>Text Eintrag verhindern

Benutzer können daran gehindert werden, den Text in einer [`Editor`](xref:Xamarin.Forms.Editor) zu ändern, indem Sie die-Eigenschaft mit dem `IsReadOnly` Standardwert `false` auf festlegen `true` :

```xaml
<Editor Text="This is a read-only Editor"
        IsReadOnly="true" />
```

```csharp
var editor = new Editor { Text = "This is a read-only Editor", IsReadOnly = true });
```

> [!NOTE]
> Die- `IsReadonly` Eigenschaft ändert nicht die visuelle Darstellung eines [`Editor`](xref:Xamarin.Forms.Editor) , anders als die- `IsEnabled` Eigenschaft, die auch die visuelle Darstellung von `Editor` in grau ändert.

## <a name="transform-text"></a>Transformieren von Text

Ein- [`Editor`](xref:Xamarin.Forms.Editor) Objekt kann die Schreibweise seines Texts, der in der-Eigenschaft gespeichert ist, Transformieren `Text` , indem die- `TextTransform` Eigenschaft auf einen Wert der-Enumeration festgelegt wird `TextTransform` . Diese Enumeration hat vier Werte:

- `None`Gibt an, dass der Text nicht transformiert wird.
- `Default`Gibt an, dass das Standardverhalten für die Plattform verwendet wird. Dies ist der Standardwert der `TextTransform`-Eigenschaft.
- `Lowercase`Gibt an, dass der Text in Kleinbuchstaben umgewandelt wird.
- `Uppercase`Gibt an, dass der Text in Großbuchstaben umgewandelt wird.

Im folgenden Beispiel wird gezeigt, wie Text in Großbuchstaben umgewandelt wird:

```xaml
<Editor Text="This text will be displayed in uppercase."
        TextTransform="Uppercase" />
```

Der entsprechende C#-Code lautet:

```csharp
Editor editor = new Editor
{
    Text = "This text will be displayed in uppercase.",
    TextTransform = TextTransform.Uppercase
};
```

## <a name="limit-input-length"></a>Eingabe Länge begrenzen

Die [`MaxLength`](xref:Xamarin.Forms.InputView.MaxLength) -Eigenschaft kann verwendet werden, um die für zulässige Eingabe Länge einzuschränken [`Editor`](xref:Xamarin.Forms.Editor) . Diese Eigenschaft sollte auf eine positive ganze Zahl festgelegt werden:

```xaml
<Editor ... MaxLength="10" />
```

```csharp
var editor = new Editor { ... MaxLength = 10 };
```

Ein [`MaxLength`](xref:Xamarin.Forms.InputView.MaxLength) -Eigenschafts Wert von 0 gibt an, dass keine Eingabe zulässig ist, und der Wert `int.MaxValue` , der der Standardwert für ein ist [`Editor`](xref:Xamarin.Forms.Editor) , gibt an, dass die Anzahl der Zeichen, die eingegeben werden können, nicht wirksam ist.

## <a name="character-spacing"></a>Zeichenabstand

Der Zeichenabstand kann auf ein angewendet werden, [`Editor`](xref:Xamarin.Forms.Editor) indem die- `Editor.CharacterSpacing` Eigenschaft auf einen Wert festgelegt wird `double` :

```xaml
<Editor ...
        CharacterSpacing="10" />
```

Der entsprechende C#-Code lautet:

```csharp
Editor editor = new editor { CharacterSpacing = 10 };
```

Das Ergebnis ist, dass Zeichen im Text, die von angezeigt [`Editor`](xref:Xamarin.Forms.Editor) werden, `CharacterSpacing` geräteunabhängige Einheiten voneinander getrennt sind.

> [!NOTE]
> Der `CharacterSpacing` -Eigenschafts Wert wird auf den Text angewendet, der von den `Text` Eigenschaften und angezeigt wird `Placeholder` .

## <a name="auto-size-an-editor"></a>Automatische Größe eines Editors

Eine [`Editor`](xref:Xamarin.Forms.Editor) kann so festgelegt werden, dass die Größe des Inhalts automatisch geändert wird, indem die-Eigenschaft auf festgelegt wird [`Editor.AutoSize`](xref:Xamarin.Forms.Editor.AutoSize) [`TextChanges`](xref:Xamarin.Forms.EditorAutoSizeOption.TextChanges) . Dies ist ein Wert der- [`EditoAutoSizeOption`](xref:Xamarin.Forms.EditorAutoSizeOption) Enumeration. Diese Enumeration verfügt über zwei Werte:

- [`Disabled`](xref:Xamarin.Forms.EditorAutoSizeOption.Disabled)Gibt an, dass die automatische Größe der Größe deaktiviert ist und der Standardwert ist.
- [`TextChanges`](xref:Xamarin.Forms.EditorAutoSizeOption.TextChanges)Gibt an, dass die automatische Größe der Größe aktiviert ist.

Dies kann im Code wie folgt erreicht werden:

```xaml
<Editor Text="Enter text here" AutoSize="TextChanges" />
```

```csharp
var editor = new Editor { Text = "Enter text here", AutoSize = EditorAutoSizeOption.TextChanges };
```

Wenn die automatische Größenänderung aktiviert ist, erhöht sich die Höhe des, [`Editor`](xref:Xamarin.Forms.Editor) Wenn der Benutzer ihn mit Text füllt, und die Höhe wird verringert, wenn der Benutzer Text löscht.

> [!NOTE]
> [`Editor`](xref:Xamarin.Forms.Editor)Wenn die Eigenschaft festgelegt wurde, wird keine automatische Größe angezeigt [`HeightRequest`](xref:Xamarin.Forms.VisualElement.HeightRequest) .

## <a name="customize-the-keyboard"></a>Anpassen der Tastatur

Die Tastatur, die angezeigt wird, wenn Benutzer mit einer interagieren [`Editor`](xref:Xamarin.Forms.Editor) , kann Programm gesteuert über die- [`Keyboard`](xref:Xamarin.Forms.InputView.Keyboard) Eigenschaft auf eine der folgenden Eigenschaften der-Klasse festgelegt werden [`Keyboard`](xref:Xamarin.Forms.Keyboard) :

- [`Chat`](xref:Xamarin.Forms.Keyboard.Chat): Wird zum Schreiben von Texten verwendet und in Situationen, in denen Emojis nützlich sind.
- [`Default`](xref:Xamarin.Forms.Keyboard.Default): die Standardtastatur.
- [`Email`](xref:Xamarin.Forms.Keyboard.Email): Wird beim Eingeben von E-Mail-Adressen verwendet.
- [`Numeric`](xref:Xamarin.Forms.Keyboard.Numeric): Wird beim Eingeben von Zahlen verwendet.
- [`Plain`](xref:Xamarin.Forms.Keyboard.Plain): Wird beim Eingeben von Text verwendet, ohne Angabe von [`KeyboardFlags`](xref:Xamarin.Forms.KeyboardFlags).
- [`Telephone`](xref:Xamarin.Forms.Keyboard.Telephone): Wird beim Eingeben von Telefonnummern verwendet.
- [`Text`](xref:Xamarin.Forms.Keyboard.Text): Wird beim Eingeben von Text verwendet.
- [`Url`](xref:Xamarin.Forms.Keyboard.Url): Wird beim Eingeben von Dateipfaden und Webadressen verwendet.

Dies kann in XAML folgendermaßen erfüllt werden:

```xaml
<Editor Keyboard="Chat" />
```

Der entsprechende C#-Code lautet:

```csharp
var editor = new Editor { Keyboard = Keyboard.Chat };
```

Beispiele für jede Tastatur finden Sie in unserem [Rezepte](https://github.com/xamarin/recipes/tree/master/Recipes/xamarin-forms/Controls/choose-keyboard-for-entry) -Repository.

Die [`Keyboard`](xref:Xamarin.Forms.Keyboard)-Klasse verfügt auch über eine [`Create`](xref:Xamarin.Forms.Keyboard.Create*)-Factorymethode, die zum Anpassen einer Tastatur durch Festlegen des Verhaltens für Groß-/Kleinschreibung, Rechtschreibprüfung und Vorschläge verwendet werden kann. [`KeyboardFlags`](xref:Xamarin.Forms.KeyboardFlags)-Enumerationswerte werden als Argumente der Methode festgelegt, wobei das benutzerdefinierte `Keyboard` zurückgegeben wird. Die `KeyboardFlags`-Enumeration verfügt über folgende Werte:

- [`None`](xref:Xamarin.Forms.KeyboardFlags.None): Der Tastatur werden keine Features hinzugefügt.
- [`CapitalizeSentence`](xref:Xamarin.Forms.KeyboardFlags.CapitalizeSentence): Gibt an, dass der erste Buchstabe des ersten Worts jedes Satzes automatisch groß geschrieben wird.
- [`Spellcheck`](xref:Xamarin.Forms.KeyboardFlags.Spellcheck): Gibt an, dass die Rechtschreibprüfung für den eingegebenen Text durchgeführt wird.
- [`Suggestions`](xref:Xamarin.Forms.KeyboardFlags.Suggestions): Gibt an, dass Wortvervollständigungen für den eingegebenen Text angeboten werden.
- [`CapitalizeWord`](xref:Xamarin.Forms.KeyboardFlags.CapitalizeWord): Gibt an, dass der erste Buchstabe von jedem Wort automatisch groß geschrieben wird.
- [`CapitalizeCharacter`](xref:Xamarin.Forms.KeyboardFlags.CapitalizeCharacter): Gibt an, dass jedes Zeichen automatisch groß geschrieben wird.
- [`CapitalizeNone`](xref:Xamarin.Forms.KeyboardFlags.CapitalizeNone): Gibt an, dass keine automatische Großschreibung erfolgt.
- [`All`](xref:Xamarin.Forms.KeyboardFlags.All): Gibt an, dass für den eingegebenen Text die Rechtschreibprüfung, die Vervollständigung von Wörtern und die Großschreibung am Satzanfang erfolgen.

Das folgende XAML-Codebeispiel zeigt, wie Sie den Standardwert für [`Keyboard`](xref:Xamarin.Forms.Keyboard) anpassen können, um Wortvervollständigungen anzubieten und jedes eingegebene Zeichen groß zu schreiben:

```xaml
<Editor>
    <Editor.Keyboard>
        <Keyboard x:FactoryMethod="Create">
            <x:Arguments>
                <KeyboardFlags>Suggestions,CapitalizeCharacter</KeyboardFlags>
            </x:Arguments>
        </Keyboard>
    </Editor.Keyboard>
</Editor>
```

Der entsprechende C#-Code lautet:

```csharp
var editor = new Editor();
editor.Keyboard = Keyboard.Create(KeyboardFlags.Suggestions | KeyboardFlags.CapitalizeCharacter);
```

## <a name="enable-and-disable-spell-checking"></a>Aktivieren und Deaktivieren der Rechtschreibprüfung

Die- [`IsSpellCheckEnabled`](xref:Xamarin.Forms.InputView.IsSpellCheckEnabled) Eigenschaft steuert, ob die Rechtschreibprüfung aktiviert ist. Standardmäßig ist die-Eigenschaft auf festgelegt `true` . Wenn der Benutzer Text eingibt, werden falsche Schreibweisen angegeben.

Für einige Texteingabe Szenarios, z. b. die Eingabe eines Benutzernamens, bietet die Rechtschreibprüfung jedoch eine negative Darstellung und sollte daher durch Festlegen der- [`IsSpellCheckEnabled`](xref:Xamarin.Forms.InputView.IsSpellCheckEnabled) Eigenschaft auf deaktiviert werden `false` :

```xaml
<Editor ... IsSpellCheckEnabled="false" />
```

```csharp
var editor = new Editor { ... IsSpellCheckEnabled = false };
```

> [!NOTE]
> Wenn die [`IsSpellCheckEnabled`](xref:Xamarin.Forms.InputView.IsSpellCheckEnabled) -Eigenschaft auf festgelegt ist `false` und eine benutzerdefinierte Tastatur nicht verwendet wird, wird die native Rechtschreibprüfung deaktiviert. Wenn jedoch ein [`Keyboard`](xref:Xamarin.Forms.Keyboard) festgelegt wurde, der die Rechtschreibprüfung deaktiviert (z. b.), [`Keyboard.Chat`](xref:Xamarin.Forms.Keyboard.Chat) wird die- `IsSpellCheckEnabled` Eigenschaft ignoriert. Daher kann die-Eigenschaft nicht verwendet werden, um die Rechtschreibprüfung für einen zu aktivieren `Keyboard` , der diese explizit deaktiviert.

## <a name="enable-and-disable-text-prediction"></a>Aktivieren und Deaktivieren der Text Vorhersage

Die `IsTextPredictionEnabled` -Eigenschaft steuert, ob die Text Vorhersage und die automatische Textkorrektur aktiviert ist. Standardmäßig ist die-Eigenschaft auf festgelegt `true` . Wenn der Benutzer Text eingibt, werden Word-Vorhersagen angezeigt.

Für einige Texteingabe Szenarios, wie z. b. die Eingabe eines Benutzernamens, bietet die Text Vorhersage und die automatische Textkorrektur jedoch eine negative Benutzerumgebung und sollte durch Festlegen der- `IsTextPredictionEnabled` Eigenschaft auf deaktiviert werden `false` :

```xaml
<Editor ... IsTextPredictionEnabled="false" />
```

```csharp
var editor = new Editor { ... IsTextPredictionEnabled = false };
```

> [!NOTE]
> Wenn die `IsTextPredictionEnabled` -Eigenschaft auf festgelegt ist `false` und keine benutzerdefinierte Tastatur verwendet wird, werden die Text Vorhersage und die automatische Textkorrektur deaktiviert. Wenn jedoch ein [`Keyboard`](xref:Xamarin.Forms.Keyboard) festgelegt wurde, der die Text Vorhersage deaktiviert, wird die- `IsTextPredictionEnabled` Eigenschaft ignoriert. Daher kann die-Eigenschaft nicht zum Aktivieren der Text Vorhersage für einen verwendet werden, der diese `Keyboard` explizit deaktiviert.

## <a name="colors"></a>Farben

`Editor`kann festgelegt werden, um eine benutzerdefinierte Hintergrundfarbe über die-Eigenschaft zu verwenden `BackgroundColor` . Eine besondere Sorgfalt ist erforderlich, um sicherzustellen, dass Farben auf jeder Plattform verwendet werden können. Da jede Plattform über andere Standardwerte für die Textfarbe verfügt, müssen Sie möglicherweise für jede Plattform eine benutzerdefinierte Hintergrundfarbe festlegen. Weitere Informationen zur Optimierung der Benutzeroberfläche für die einzelnen Plattformen finden Sie unter [Arbeiten mit Platt Form Anpassungen](~/xamarin-forms/platform/device.md) .

In C#:

```csharp
public partial class EditorPage : ContentPage
{
    public EditorPage ()
    {
        InitializeComponent ();
        var layout = new StackLayout { Padding = new Thickness(5,10) };
        this.Content = layout;
        //dark blue on UWP & Android, light blue on iOS
        var editor = new Editor { BackgroundColor = Device.RuntimePlatform == Device.iOS ? Color.FromHex("#A4EAFF") : Color.FromHex("#2c3e50") };
        layout.Children.Add(editor);
    }
}
```

In XAML:

```xaml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="TextSample.EditorPage"
    Title="Editor Demo">
    <ContentPage.Content>
        <StackLayout Padding="5,10">
            <Editor>
                <Editor.BackgroundColor>
                    <OnPlatform x:TypeArguments="x:Color">
                        <On Platform="iOS" Value="#a4eaff" />
                        <On Platform="Android, UWP" Value="#2c3e50" />
                    </OnPlatform>
                </Editor.BackgroundColor>
            </Editor>
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```

![Editor mit BackgroundColor-Beispiel](editor-images/textbackgroundcolor.png)

Stellen Sie sicher, dass die von Ihnen ausgewählten Hintergrund-und Textfarben auf jeder Plattform verwendbar sind und keinen Platzhalter Text verbergen.

## <a name="events-and-interactivity"></a>Ereignisse und Interaktivität

`Editor`macht zwei Ereignisse verfügbar:

- [TextChanged](xref:Xamarin.Forms.InputView.TextChanged) &ndash; wird ausgelöst, wenn der Text im Editor geändert wird. Stellt den Text vor und nach der Änderung bereit.
- [Abgeschlossen](xref:Xamarin.Forms.Editor.Completed) &ndash; wird ausgelöst, wenn der Benutzer die Eingabe durch Drücken der Rückgabetaste auf der Tastatur beendet hat.

> [!NOTE]
> Die [`VisualElement`](xref:Xamarin.Forms.VisualElement) -Klasse, von der [`Entry`](xref:Xamarin.Forms.Entry) erbt, verfügt auch über die [`Focused`](xref:Xamarin.Forms.VisualElement.Focused) -und- [`Unfocused`](xref:Xamarin.Forms.VisualElement.Unfocused) Ereignisse.

### <a name="completed"></a>Abgeschlossen

Das- `Completed` Ereignis wird verwendet, um auf den Abschluss einer Interaktion mit einer zu reagieren `Editor` . `Completed`wird ausgelöst, wenn der Benutzer die Eingabe mit einem Feld beendet, indem die Rückgabetaste auf der Tastatur eingegeben wird (oder durch Drücken der Tab-Taste auf der UWP). Der Handler für das-Ereignis ist ein generischer Ereignishandler, der den Absender und Folgendes annimmt `EventArgs` :

```csharp
void EditorCompleted (object sender, EventArgs e)
{
    var text = ((Editor)sender).Text; // sender is cast to an Editor to enable reading the `Text` property of the view.
}
```

Das abgeschlossene Ereignis kann im Code und in XAML abonniert werden:

In C#:

```csharp
public partial class EditorPage : ContentPage
{
    public EditorPage ()
    {
        InitializeComponent ();
        var layout = new StackLayout { Padding = new Thickness(5,10) };
        this.Content = layout;
        var editor = new Editor ();
        editor.Completed += EditorCompleted;
        layout.Children.Add(editor);
    }
}
```

In XAML:

```xaml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
x:Class="TextSample.EditorPage"
Title="Editor Demo">
    <ContentPage.Content>
        <StackLayout Padding="5,10">
            <Editor Completed="EditorCompleted" />
        </StackLayout>
    </ContentPage.Content>
</Contentpage>
```

### <a name="textchanged"></a>TextChanged

Das- `TextChanged` Ereignis wird verwendet, um auf eine Änderung im Inhalt eines Felds zu reagieren.

`TextChanged`wird immer dann ausgelöst, wenn der der `Text` `Editor` geändert wird. Der Handler für das-Ereignis nimmt eine Instanz von an `TextChangedEventArgs` . `TextChangedEventArgs`ermöglicht den Zugriff auf die alten und neuen Werte der `Editor` `Text` über die `OldTextValue` -Eigenschaft und die-Eigenschaft `NewTextValue` :

```csharp
void EditorTextChanged (object sender, TextChangedEventArgs e)
{
    var oldText = e.OldTextValue;
    var newText = e.NewTextValue;
}
```

Das abgeschlossene Ereignis kann im Code und in XAML abonniert werden:

In Code:

```csharp
public partial class EditorPage : ContentPage
{
    public EditorPage ()
    {
        InitializeComponent ();
        var layout = new StackLayout { Padding = new Thickness(5,10) };
        this.Content = layout;
        var editor = new Editor ();
        editor.TextChanged += EditorTextChanged;
        layout.Children.Add(editor);
    }
}
```

In XAML:

```xaml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
x:Class="TextSample.EditorPage"
Title="Editor Demo">
    <ContentPage.Content>
        <StackLayout Padding="5,10">
            <Editor TextChanged="EditorTextChanged" />
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```

## <a name="related-links"></a>Verwandte Links

- [Text (Beispiel)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-text)
- [Editor-API](xref:Xamarin.Forms.Editor)
