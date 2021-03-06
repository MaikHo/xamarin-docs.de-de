---
title: Verwenden des natürlicher sprach-Frameworks mit xamarin. IOS
description: In diesem Dokument wird das Framework für natürliche Sprache beschrieben. Das Framework für natürliche Sprache wurde in IOS 12 eingeführt und ist die bevorzugte IOS-API für die Spracherkennung, Teile der sprach Identifikation und benannte Entitäts Erkennung.
ms.prod: xamarin
ms.assetid: 126C8764-F873-4EB9-98A3-D82AB5689111
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 08/20/2018
ms.openlocfilehash: 1598bad7bdbea8334b7fdfa2b950400b698579b0
ms.sourcegitcommit: 2fbe4932a319af4ebc829f65eb1fb1816ba305d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/29/2019
ms.locfileid: "73031992"
---
# <a name="using-the-natural-language-framework-with-xamarinios"></a>Verwenden des natürlicher sprach-Frameworks mit xamarin. IOS

Das Framework für natürliche Sprache wurde in IOS 12 eingeführt und ermöglicht die Verarbeitung natürlicher Sprache in natürlicher Sprache. Es unterstützt die Spracherkennung, Tokenisierung und Tagging. Die Tokenisierung teilt Text in seine Komponenten Wörter,-Sätze oder-Absätze auf. Tagging identifiziert Teile von Sprache, Personen, Orten und Organisationen.

Das Framework für natürliche Sprache kann auch benutzerdefinierte Core ml-Modelle verwenden, um Text in speziellen Kontexten zu klassifizieren und zu markieren.

Die [nslinguistictagger](xref:Foundation.NSLinguisticTagger) -Klasse ist weiterhin verfügbar. Allerdings ist das Framework für natürliche Sprache der bevorzugte Mechanismus für die Verarbeitung natürlicher Sprache.

## <a name="sample-app-xamarinnl"></a>Beispiel-App: xamarinnl

Um zu erfahren, wie Sie das Framework für natürliche Sprache mit xamarin. IOS verwenden, sehen Sie sich die [xamarinnl-Beispiel-App](https://docs.microsoft.com/samples/xamarin/ios-samples/ios12-xamarinnl)an.
Diese Beispiel-App veranschaulicht, wie das Framework für natürliche Sprache für Folgendes verwendet wird:

- [Erkennen von Sprachen](#recognizing-languages).
- Setzen Sie [Text in Wörter und Sätze](#tokenizing-text-into-words-sentences-and-paragraphs)um.
- [Markieren Sie benannte Entitäten und Teile der Sprache](#tagging-named-entities-and-parts-of-speech).

## <a name="recognizing-languages"></a>Erkennen von Sprachen

Die Registerkarte **Erkennung** der Beispiel-App veranschaulicht die Verwendung einer [`NLLanguageRecognizer`](xref:NaturalLanguage.NLLanguageRecognizer)
, um die Sprache für einen TextBlock zu bestimmen.

> [!NOTE]
> Die Spracherkennung ist eine bestimmte Art von Text Klassifizierung. Das Framework für natürliche Sprache unterstützt auch die benutzerdefinierte Text Klassifizierung über vom Entwickler bereitgestellte Core ml-Modelle. Weitere Informationen finden Sie in der [Einführung der Natural Language Framework](https://developer.apple.com/videos/play/wwdc2018/713/) -Sitzung von WWDC 2018.

### <a name="dominant-language"></a>Dominierende Sprache

Tippen Sie auf die Schaltfläche **Sprache** , um die dominierende Sprache in der Benutzereingabe zu identifizieren.

Die `HandleDetermineLanguageButtonTap`-Methode der `LanguageRecognizerViewController` verwendet die [`GetDominantLanguage`](xref:NaturalLanguage.NLLanguageRecognizer.GetDominantLanguage*)
Methode einer `NLLanguageRecognizer` zum Abrufen des [`NLLanguage`](xref:NaturalLanguage.NLLanguage)
für die primäre Sprache im Text:

```csharp
partial void HandleDetermineLanguageButtonTap(UIButton sender)
{
    UserInput.ResignFirstResponder();
    if (!String.IsNullOrWhiteSpace(UserInput.Text))
    {
        NLLanguage lang = NLLanguageRecognizer.GetDominantLanguage(UserInput.Text);
        DominantLanguageLabel.Text = lang.ToString();
    }
}
```

### <a name="language-probabilities"></a>Sprach Wahrscheinlichkeiten

Tippen Sie auf die Schaltfläche **sprach Wahrscheinlichkeiten** , um eine Liste der sprach Hypothese für die Benutzereingabe abzurufen.

Die `HandleLanguageProbabilitiesButtonTap`-Methode der `LanguageRecognizerViewController`-Klasse instanziiert eine `NLLanguageRecognizer` und fordert Sie zur [`Process`](xref:NaturalLanguage.NLLanguageRecognizer.Process*)
der Text des Benutzers. Anschließend ruft er die [`GetNativeLanguageHypotheses`](xref:NaturalLanguage.NLLanguageRecognizer.GetNativeLanguageHypotheses*) der Spracherkennung auf.
-Methode, die ein Wörterbuch mit Sprachen und zugeordneten Wahrscheinlichkeiten abruft. Die `LanguageRecognizerTableViewController`-Klasse rendert dann diese Sprachen und Wahrscheinlichkeiten.

```csharp
partial void HandleLanguageProbabilitiesButtonTap(UIButton sender)
{
    UserInput.ResignFirstResponder();
    if (!String.IsNullOrWhiteSpace(UserInput.Text))
    {
        var recognizer = new NLLanguageRecognizer();
        recognizer.Process(UserInput.Text);
        NSDictionary<NSString, NSNumber> probabilities = recognizer.GetNativeLanguageHypotheses(10);
        PerformSegue(ShowLanguageProbabilitiesSegue, this);
    }
}
```

Mögliche `NLLanguage` Werte sind:

- `Amharic`
- `Arabic`
- `Armenian`
- `Bengali`
- `Bulgarian`
- `Burmese`
- `Catalan`
- `Cherokee`
- `Croatian`
- `Czech`
- `Danish`
- `Dutch`
- `English`
- `Finnish`
- `French`
- `Georgian`
- `German`
- `Greek`
- `Gujarati`
- `Hebrew`
- `Hindi`
- `Hungarian`
- `Icelandic`
- `Indonesian`
- `Italian`
- `Japanese`
- `Kannada`
- `Khmer`
- `Korean`
- `Lao`
- `Malay`
- `Malayalam`
- `Marathi`
- `Mongolian`
- `Norwegian`
- `Oriya`
- `Persian`
- `Polish`
- `Portuguese`
- `Punjabi`
- `Romanian`
- `Russian`
- `SimplifiedChinese`
- `Sinhalese`
- `Slovak`
- `Spanish`
- `Swedish`
- `Tamil`
- `Telugu`
- `Thai`
- `Tibetan`
- `TraditionalChinese`
- `Turkish`
- `Ukrainian`
- `Undetermined`
- `Urdu`
- `Vietnamese`

Eine vollständige Liste der unterstützten Sprachen steht als Teil der [`NLLanguage`](xref:NaturalLanguage.NLLanguage)
API-API-Dokumentation.

## <a name="tokenizing-text-into-words-sentences-and-paragraphs"></a>Umschalten von Text in Wörter, Sätzen und Absätzen

Die Registerkarte **Tokenizer** der Beispiel-App veranschaulicht, wie ein TextBlock in seine Komponenten Wörter oder-Sätze mit einem- [`NLTokenizer`](xref:NaturalLanguage.NLTokenizer)getrennt werden kann.

Tippen Sie auf die Schaltfläche **Wörter** oder **Sätze** , um eine Liste der Token abzurufen. Jedes Token ist einem Wort oder Satz im ursprünglichen Text zugeordnet.

`ShowTokens` teilt die Eingabe des Benutzers durch Aufrufen der [`GetTokens`](xref:NaturalLanguage.NLTokenizer.GetTokens*)
Methode einer `NLTokenizer`. Diese Methode gibt ein Array von [`NSValue`](xref:Foundation.NSValue)
-Objekte, von denen jede einen `NSRange` Wert umwickelt, der einem Token im ursprünglichen Text entspricht.

```csharp
void ShowTokens(NLTokenUnit unit)
{
    if (!String.IsNullOrWhiteSpace(UserInput.Text))
    {
        var tokenizer = new NLTokenizer(unit);
        tokenizer.String = UserInput.Text;
        var range = new NSRange(0, UserInput.Text.Length);
        NSValue[] tokens = tokenizer.GetTokens(range);
        PerformSegue(ShowTokensSegue, this);
    }
}
```

`LanguageTokenizerTableViewController` rendert ein einzelnes Token in jeder Tabellenzelle. Es extrahiert eine `NSRange` aus einem Token `NSValue`, sucht die entsprechende Zeichenfolge im ursprünglichen Text und legt eine Bezeichnung für die Tabellen Ansichts Zelle fest:

```csharp
public override UITableViewCell GetCell(UITableView tableView, NSIndexPath indexPath)
{
    var cell = TableView.DequeueReusableCell(TokenCell);
    NSRange range = Tokens[indexPath.Row].RangeValue;
    cell.TextLabel.Text = Text.Substring((int)range.Location, (int)range.Length);
    return cell;
}
```

## <a name="tagging-named-entities-and-parts-of-speech"></a>Tagging benannte Entitäten und Teile der Sprache

Die Registerkarte **Tagger** der xamarinnl-Beispiel-App veranschaulicht die Verwendung des [`NLTagger`](xref:NaturalLanguage.NLTagger)
Klasse zum Zuordnen von Kategorien zu Token einer Eingabe Zeichenfolge.
Das Framework für natürliche Sprache umfasst integrierte Unterstützung für die Erkennung von Personen, Orten, Organisationen und Teilen der Sprache.

> [!NOTE]
> Das Framework für natürliche Sprache unterstützt auch benutzerdefinierte Tagging-Schemas über vom Entwickler bereitgestellte Core ml-Modelle. Weitere Informationen finden Sie in der [Einführung der Natural Language Framework](https://developer.apple.com/videos/play/wwdc2018/713/) -Sitzung von WWDC 2018.

Tippen Sie auf die Schaltfläche **benannte Entitäten** oder **Teile der Sprache** zum Abrufen:

- Ein Array von `NSValue`-Objekten, von denen jedes eine `NSRange` für ein Token im ursprünglichen Text umwickelt.
- Ein Array von [`NLTag`](xref:NaturalLanguage.NLTag) Werten – Kategorien für die `NSValue`-Token am gleichen Array Index.

`HandlePartsOfSpeechButtonTap` und `HandleNamedEntitiesButtonTap` in `LanguageTaggerViewController`jeden Aufruf`ShowTags`, wobei eine [`NLTagScheme`](xref:NaturalLanguage.NLTagScheme) – entweder `NLTagScheme.LexicalClass` (für Teile der Sprache) oder `NLTagScheme.NameType` (für benannte Entitäten) übergeben wird.

`ShowTags` erstellt einen `NLTagger`und instanziiert ihn mit einem Array von `NLTagScheme` Typen, für die er abgefragt wird (in diesem Fall nur der übergebenen `NLTagScheme` Wert). Anschließend wird der [`GetTags`](xref:NaturalLanguage.NLTagger.GetTags*)
-Methode für den `NLTagger`, um die für den Text in der Benutzereingabe relevanten Tags zu bestimmen.

```csharp
void ShowTags(NLTagScheme tagScheme)
{
    if (!String.IsNullOrWhiteSpace(UserInput.Text))
    {
        var tagger = new NLTagger(new NLTagScheme[] { tagScheme });
        var range = new NSRange(0, UserInput.Text.Length);
        tagger.String = UserInput.Text;

        NLTag[] tags = tagger.GetTags(range, NLTokenUnit.Word, tagScheme, NLTaggerOptions.OmitWhitespace, out NSValue[] ranges);
        NSValue[] tokenRanges = ranges;
        detailViewTitle = tagScheme == NLTagScheme.NameType ? "Named Entities" : "Parts of Speech";

        PerformSegue(ShowEntitiesSegue, this);
    }
}
```

Die Tags werden dann vom `LanguageTaggerTableViewController`in einer Tabelle angezeigt.

Mögliche `NLTag` Werte sind:

- `Adjective`
- `Adverb`
- `Classifier`
- `CloseParenthesis`
- `CloseQuote`
- `Conjunction`
- `Dash`
- `Determiner`
- `Idiom`
- `Interjection`
- `Noun`
- `Number`
- `OpenParenthesis`
- `OpenQuote`
- `OrganizationName`
- `Other`
- `OtherPunctuation`
- `OtherWhitespace`
- `OtherWord`
- `ParagraphBreak`
- `Particle`
- `PersonalName`
- `PlaceName`
- `Preposition`
- `Pronoun`
- `Punctuation`
- `SentenceTerminator`
- `Verb`
- `Whitespace`
- `Word`
- `WordJoiner`

Eine vollständige Liste der unterstützten Tags steht als Teil der [`NLTag`](xref:NaturalLanguage.NLTag)
API-API-Dokumentation.

## <a name="related-links"></a>Verwandte Links

- [Beispiel-App – xamarinnl](https://docs.microsoft.com/samples/xamarin/ios-samples/ios12-xamarinnl)
- [Einführung in das Framework für natürliche Sprache](https://developer.apple.com/videos/play/wwdc2018/713/)
- [Natürliche Sprache (Apple)](https://developer.apple.com/documentation/naturallanguage?language=objc)
