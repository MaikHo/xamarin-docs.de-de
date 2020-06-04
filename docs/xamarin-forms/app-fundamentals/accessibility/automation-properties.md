---
title: ''
description: In diesem Artikel wird beschrieben, wie Sie die AutomationProperties-Klasse in einer Xamarin.Forms-Anwendung verwenden, damit eine Sprachausgabe über die Elemente auf der Seite sprechen kann.
ms.prod: ''
ms.assetid: ''
ms.technology: ''
author: ''
ms.author: ''
ms.date: ''
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: ad6d315ccc5be0a7709164d40685c842b61b90b4
ms.sourcegitcommit: 57bc714633364aeb34aba9803e88802bebf321ba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2020
ms.locfileid: "84129960"
---
# <a name="automation-properties-in-xamarinforms"></a>Automatisierungseigenschaften in Xamarin.Forms

[![Beispiel herunterladen](~/media/shared/download.png) Das Beispiel herunterladen](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-accessibility)

_Xamarin.Forms ermöglicht das Festlegen von Barrierefreiheitswerten auf Benutzeroberflächenelemente, indem angefügte Eigenschaften der AutomationProperties-Klasse verwendet werden, die wiederum native Barrierefreiheitswerte festlegen. In diesem Artikel wird erläutert, wie Sie die AutomationProperties-Klasse verwenden, sodass eine Sprachausgabe über die Elemente auf der Seite sprechen kann._

Xamarin.Forms ermöglicht das Festlegen von Automatisierungseigenschaften auf Benutzeroberflächenelemente über die folgenden angefügten Eigenschaften:

- `AutomationProperties.IsInAccessibleTree` gibt an, ob das Element für eine barrierefreie Anwendung verfügbar ist. Weitere Informationen finden Sie unter [AutomationProperties.IsInAccessibleTree](#isinaccessibletree).
- `AutomationProperties.Name` ist eine kurze Beschreibung des Elements, das als aussprechbarer Bezeichner für das Element dient. Weitere Informationen finden Sie unter [AutomationProperties.Name](#name).
- `AutomationProperties.HelpText` ist eine längere Beschreibung des Elements, das als dem Element zugeordneter QuickInfo-Text verstanden werden kann. Weitere Informationen finden Sie unter [AutomationProperties.HelpText](#helptext).
- `AutomationProperties.LabeledBy` ermöglicht es einem anderen Element, Informationen zur Barrierefreiheit für das aktuelle Element zu definieren. Weitere Informationen finden Sie unter [AutomationProperties.LabeledBy](#labeledby).

Diese angefügten Eigenschaften legen native Barrierefreiheitswerte so fest, dass eine Sprachausgabe über das Element sprechen kann. Weitere Informationen zu angefügten Eigenschaften finden Sie unter [Angefügte Eigenschaften](~/xamarin-forms/xaml/attached-properties.md).

> [!IMPORTANT]
> Die Verwendung der angefügten `AutomationProperties`-Eigenschaften kann die Ausführung des UI-Tests unter Android beeinträchtigen. Die Eigenschaften [`AutomationId`](xref:Xamarin.Forms.Element.AutomationId), `AutomationProperties.Name` und `AutomationProperties.HelpText` legen die native `ContentDescription`-Eigenschaft fest, wobei die Eigenschaftswerte `AutomationProperties.Name` und `AutomationProperties.HelpText` Vorrang vor dem `AutomationId`-Wert haben (wenn `AutomationProperties.Name` und `AutomationProperties.HelpText` festgelegt wurden, werden die Werte verkettet). Dies bedeutet, dass alle Tests, die nach `AutomationId` suchen, fehlschlagen, wenn `AutomationProperties.Name` oder `AutomationProperties.HelpText` auch auf das Element festgelegt werden. In diesem Szenario sollten UI-Tests so geändert werden, dass sie nach dem Wert von `AutomationProperties.Name` oder `AutomationProperties.HelpText` oder einer Verkettung der beiden suchen.

Jede Plattform verfügt über eine andere Sprachausgabe, die die Barrierefreiheitswerte versprachlicht:

- iOS verfügt über VoiceOver. Weitere Informationen finden Sie unter [Test Accessibility on Your Device with VoiceOver (Testen der Barrierefreiheit auf Ihrem Gerät mit VoiceOver)](https://developer.apple.com/library/content/technotes/TestingAccessibilityOfiOSApps/TestAccessibilityonYourDevicewithVoiceOver/TestAccessibilityonYourDevicewithVoiceOver.html) auf developer.apple.com.
- Android verfügt über TalkBack. Weitere Informationen finden Sie unter [Testing Your App's Accessibility (Testen der Barrierefreiheit Ihrer App)](https://developer.android.com/training/accessibility/testing.html#talkback) auf developer.android.com.
- Windows verfügt über Narrator. Weitere Informationen finden Sie unter [Verify main app scenarios by using Narrator (Überprüfen der wichtigsten App-Szenarios mit Narrator)](/windows/uwp/accessibility/accessibility-testing#verify-main-app-scenarios-by-using-narrator).

Das genaue Verhalten einer Sprachausgabe hängt jedoch von der Software und deren Konfiguration durch den Benutzer ab. Die meisten Sprachausgaben lesen zum Beispiel den einem Steuerelement zugeordneten Text, wenn dieses fokussiert wird. So können sich Benutzer orientieren, wenn sie zwischen den Steuerelementen auf der Seite wechseln. Einige Sprachausgaben lesen auch die komplette Benutzeroberfläche der Anwendung, wenn eine Seite angezeigt wird. Dadurch kann der Benutzer alle auf der Seite verfügbaren Informationsinhalte erhalten, bevor er darin navigiert.

Sprachausgaben lesen auch unterschiedliche Barrierefreiheitswerte vor. In der Beispielanwendung:

- VoiceOver liest den `Placeholder`-Wert von `Entry` und dann die Anweisungen für die Verwendung des Steuerelements.
- TalkBack liest den `Placeholder`-Wert von `Entry`, dann den `AutomationProperties.HelpText`-Wert und dann die Anweisungen für die Verwendung des Steuerelements.
- Narrator liest den `AutomationProperties.LabeledBy`-Wert von `Entry` und dann die Anweisungen für die Verwendung des Steuerelements.

Darüber hinaus priorisiert Narrator `AutomationProperties.Name`, `AutomationProperties.LabeledBy` und dann `AutomationProperties.HelpText`. Unter Android kombiniert TalkBack möglicherweise die Werte `AutomationProperties.Name` und `AutomationProperties.HelpText`. Deshalb empfiehlt es sich, die Barrierefreiheit auf jeder Plattform umfassend zu testen, um eine optimale Funktionsweise sicherzustellen.

<a name="isinaccessibletree" />

## <a name="automationpropertiesisinaccessibletree"></a>AutomationProperties.IsInAccessibleTree

Die angefügte Eigenschaft `AutomationProperties.IsInAccessibleTree` ist ein `boolean`-Wert, der festlegt, ob das Element barrierefrei und somit für Sprachausgaben sichtbar ist. Der Wert muss auf `true` festgelegt werden, damit die anderen angefügten Eigenschaften der Barrierefreiheit verwendet werden. Dies kann in XAML folgendermaßen erfüllt werden:

```xaml
<Entry AutomationProperties.IsInAccessibleTree="true" />
```

Alternativ kann es in C# folgendermaßen festgelegt werden:

```csharp
var entry = new Entry();
AutomationProperties.SetIsInAccessibleTree(entry, true);
```

> [!NOTE]
> Beachten Sie, dass die [`SetValue`](xref:Xamarin.Forms.BindableObject.SetValue(Xamarin.Forms.BindableProperty,System.Object))-Methode auch zum Festlegen der angefügten Eigenschaft `AutomationProperties.IsInAccessibleTree` verwendet werden kann: `entry.SetValue(AutomationProperties.IsInAccessibleTreeProperty, true);`.

<a name="name" />

## <a name="automationpropertiesname"></a>AutomationProperties.Name

Der Wert der angefügten Eigenschaft `AutomationProperties.Name` sollte eine kurze beschreibende Textzeichenfolge sein, mit der eine Sprachausgabe ein Element ankündigen kann. Diese Eigenschaft sollte für Elemente festgelegt werden, deren Bedeutung wichtig für das Verstehen des Inhalts oder die Interaktion mit der Benutzeroberfläche ist. Dies kann in XAML folgendermaßen erfüllt werden:

```xaml
<ActivityIndicator AutomationProperties.IsInAccessibleTree="true"
                   AutomationProperties.Name="Progress indicator" />
```

Alternativ kann es in C# folgendermaßen festgelegt werden:

```csharp
var activityIndicator = new ActivityIndicator();
AutomationProperties.SetIsInAccessibleTree(activityIndicator, true);
AutomationProperties.SetName(activityIndicator, "Progress indicator");
```

> [!NOTE]
> Beachten Sie, dass die [`SetValue`](xref:Xamarin.Forms.BindableObject.SetValue(Xamarin.Forms.BindableProperty,System.Object))-Methode auch zum Festlegen der angefügten Eigenschaft `AutomationProperties.Name` verwendet werden kann: `activityIndicator.SetValue(AutomationProperties.NameProperty, "Progress indicator");`.

<a name="helptext" />

## <a name="automationpropertieshelptext"></a>AutomationProperties.HelpText

Die angefügte Eigenschaft `AutomationProperties.HelpText` sollte auf Text festgelegt werden, der das Benutzeroberflächenelement beschreibt, und kann als QuickInfo-Text verstanden werden, der dem Element zugeordnet ist. Dies kann in XAML folgendermaßen erfüllt werden:

```xaml
<Button Text="Toggle ActivityIndicator"
        AutomationProperties.IsInAccessibleTree="true"
        AutomationProperties.HelpText="Tap to toggle the activity indicator" />
```

Alternativ kann es in C# folgendermaßen festgelegt werden:

```csharp
var button = new Button { Text = "Toggle ActivityIndicator" };
AutomationProperties.SetIsInAccessibleTree(button, true);
AutomationProperties.SetHelpText(button, "Tap to toggle the activity indicator");
```

> [!NOTE]
> Beachten Sie, dass die [`SetValue`](xref:Xamarin.Forms.BindableObject.SetValue(Xamarin.Forms.BindableProperty,System.Object))-Methode auch zum Festlegen der angefügten Eigenschaft `AutomationProperties.HelpText` verwendet werden kann: `button.SetValue(AutomationProperties.HelpTextProperty, "Tap to toggle the activity indicator");`.

Auf manchen Plattformen kann für Bearbeitungssteuerelemente wie [`Entry`](xref:Xamarin.Forms.Entry) die `HelpText`-Eigenschaft in einigen Fällen weggelassen und durch Platzhaltertext ersetzt werden. Zum Beispiel ist „Geben Sie hier Ihren Namen ein“ eine gute Variante für die [`Entry.Placeholder`](xref:Xamarin.Forms.InputView.Placeholder)-Eigenschaft, die vor der tatsächlichen Eingabe durch den Benutzer den Text in das Steuerelement platziert.

<a name="labeledby" />

## <a name="automationpropertieslabeledby"></a>AutomationProperties.LabeledBy

Die angefügte Eigenschaft `AutomationProperties.LabeledBy` ermöglicht es einem anderen Element, Informationen zur Barrierefreiheit für das aktuelle Element zu definieren. Zum Beispiel kann eine [`Label`](xref:Xamarin.Forms.Label)-Klasse neben einer [`Entry`](xref:Xamarin.Forms.Entry)-Klasse verwendet werden, um zu beschreiben, wofür die `Entry`-Klasse steht. Dies kann in XAML folgendermaßen erfüllt werden:

```xaml
<Label x:Name="label" Text="Enter your name: " />
<Entry AutomationProperties.IsInAccessibleTree="true"
       AutomationProperties.LabeledBy="{x:Reference label}" />
```

Alternativ kann es in C# folgendermaßen festgelegt werden:

```csharp
var nameLabel = new Label { Text = "Enter your name: " };
var entry = new Entry();
AutomationProperties.SetIsInAccessibleTree(entry, true);
AutomationProperties.SetLabeledBy(entry, nameLabel);
```

> [!NOTE]
> Beachten Sie, dass die [`SetValue`](xref:Xamarin.Forms.BindableObject.SetValue(Xamarin.Forms.BindableProperty,System.Object))-Methode auch zum Festlegen der angefügten Eigenschaft `AutomationProperties.IsInAccessibleTree` verwendet werden kann: `entry.SetValue(AutomationProperties.LabeledByProperty, nameLabel);`.

## <a name="accessibility-intricacies"></a>Schwierigkeiten beim Zugriff

In den folgenden Abschnitten werden die Schwierigkeiten beim Festlegen von Zugriffswerten auf bestimmten Steuerelementen beschrieben.

### <a name="navigationpage"></a>NavigationPage

Legen Sie unter Android die Eigenschaften `AutomationProperties.Name` und `AutomationProperties.HelpText` auf eine [`Page`](xref:Xamarin.Forms.Page)-Klasse fest, um den Text festzulegen, der von Sprachausgaben für den „Zurück“-Pfeil in der Aktionsleiste in einer [`NavigationPage`](xref:Xamarin.Forms.NavigationPage)-Klasse gelesen werden kann. Beachten Sie jedoch, dass dies keine Auswirkungen auf die „Zurück“-Pfeile im Betriebssystem hat.

### <a name="masterdetailpage"></a>MasterDetailPage

Legen Sie unter iOS und auf der Universellen Windows-Plattform (UWP) entweder die Eigenschaften `AutomationProperties.Name` und `AutomationProperties.HelpText` auf die `MasterDetailPage`-Klasse oder auf die Eigenschaft `IconImageSource` der `Master`-Seite fest, um den Text festzulegen, der von Sprachausgaben für die Umschaltfläche auf einer [`MasterDetailPage`](xref:Xamarin.Forms.MasterDetailPage)-Klasse gelesen werden kann.

Fügen Sie unter Android dem Android-Projekt Zeichenfolgenressourcen hinzu, um den Text festzulegen, der von Sprachausgaben für die Umschaltfläche auf einer [`MasterDetailPage`](xref:Xamarin.Forms.MasterDetailPage) gelesen werden kann:

```xml
<resources>
    <string name="app_name">Xamarin Forms Control Gallery</string>
    <string name="btnMDPAutomationID_open">Open Side Menu message</string>
    <string name="btnMDPAutomationID_close">Close Side Menu message</string>
</resources>
```

Legen Sie anschließend die Eigenschaft `AutomationId` auf die Eigenschaft `IconImageSource` der `Master`-Seite für die entsprechende Zeichenfolge fest:

```csharp
var master = new ContentPage { ... };
master.IconImageSource.AutomationId = "btnMDPAutomationID";
```

### <a name="toolbaritem"></a>ToolbarItem

Unter iOS, Android und UWP lesen Sprachausgaben den `Text`-Eigenschaftswert von [`ToolbarItem`](xref:Xamarin.Forms.ToolbarItem)-Instanzen, sofern die Werte `AutomationProperties.Name` und `AutomationProperties.HelpText` nicht definiert sind.

Unter iOS und UWP ersetzt der Eigenschaftswert `AutomationProperties.Name` den Eigenschaftswert `Text`, der von der Sprachausgabe gelesen wird.

Unter Android ersetzt der Eigenschaftswert `AutomationProperties.Name` und/oder `AutomationProperties.HelpText` den Eigenschaftswert `Text` vollständig. Dieser ist sichtbar und kann von der Sprachausgabe gelesen werden. Beachten Sie, dass es eine Einschränkung auf weniger als 26 APIs gibt.

## <a name="related-links"></a>Verwandte Links

- [Angefügte Eigenschaften](~/xamarin-forms/xaml/attached-properties.md)
- [Accessibility (Barrierefreiheit (Beispiel))](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-accessibility)
