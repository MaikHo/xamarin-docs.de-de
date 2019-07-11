---
title: Xamarin.Forms-Anwendungsgrundlagen
description: In diesem Artikel werden die Grundlagen der Xamarin.Forms-Anwendungsentwicklung erläutert, einschließlich aller erforderlichen Grundlagen bis hin zu den letzten Details wie die Barrierefreiheit und Lokalisierung.
ms.prod: xamarin
ms.assetid: 7B516BBC-F7E1-4387-9779-7754E2E69723
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 01/08/2018
ms.openlocfilehash: 61d9c5b1c7b81bfc8a20932ce1d188cd0cb0f980
ms.sourcegitcommit: c1d85b2c62ad84c22bdee37874ad30128581bca6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/08/2019
ms.locfileid: "67650430"
---
# <a name="xamarinforms-application-fundamentals"></a>Xamarin.Forms-Anwendungsgrundlagen

## <a name="accessibilityaccessibilityindexmd"></a>[Barrierefreiheit](accessibility/index.md)

Tipps, wie Barrierefreiheitsfunktionen (z.B. Unterstützung von Sprachausgabetools) mit Xamarin.Forms integriert werden.

## <a name="app-classapplication-classmd"></a>[App-Klasse](application-class.md)

Die `Application`-Klasse stellt den Startpunkt für Xamarin.Forms dar – jede App muss eine `App`-Unterklasse implementieren, um die Startseite festzulegen. Sie stellt auch die `Properties`-Sammlung für die Speicherung einfacher Daten bereit. Sie kann entweder in C# oder XAML definiert werden.

## <a name="app-lifecycleapp-lifecyclemd"></a>[App-Lebenszyklus](app-lifecycle.md)

Sie können mit der `Application`-Klasse `OnStart`, `OnSleep` und `OnResume`-Methoden sowie der modalen Navigationsereignisse die Ereignisse des Anwendungslebenszyklus mit benutzerdefiniertem Code behandeln.

## <a name="application-indexing-and-deep-linkingdeep-linkingmd"></a>[Anwendungsindizierung und Deep Linking](deep-linking.md)

Mit der Anwendungsindizierung können Anwendungen, die andernfalls nach einigem Gebrauch vergessen würden, relevant bleiben, indem sie in den Suchergebnissen angezeigt werden. Mit Deep Linking können Anwendungen auf ein Suchergebnis reagieren, das Anwendungsdaten enthält, in der Regel durch Navigation zu einer Seite, auf die über einen Deeplink verwiesen wird.

## <a name="behaviorsbehaviorsindexmd"></a>[Verhalten](behaviors/index.md)

Benutzeroberflächensteuerelemente können ganz einfach erweitert werden, ohne Unterklassen zu erstellen, indem Verhalten zum Hinzufügen von Funktionen verwendet werden.

## <a name="custom-rendererscustom-rendererindexmd"></a>[Benutzerdefinierte Renderer](custom-renderer/index.md)

Mithilfe benutzerdefinierter Renderer können Entwickler das Standardrendering der Xamarin.Forms-Steuerelemente „überschreiben“, um so ihre Darstellung und ihr Verhalten auf jeder Plattform (ggf. mit nativen SDKs) anzupassen.

## <a name="data-bindingdata-bindingindexmd"></a>[Datenbindung](data-binding/index.md)

Durch die Datenbindung werden die Eigenschaften von zwei Objekten verknüpft. Dadurch werden Änderungen an einer Eigenschaft automatisch in der anderen widergespiegelt. Die Datenbindung ist ein integraler Teil der „Model View ViewModel“-Anwendungsarchitektur ([MVVM](~/xamarin-forms/enterprise-application-patterns/mvvm.md)).

## <a name="dependency-servicedependency-serviceindexmd"></a>[Abhängigkeitsdienst](dependency-service/index.md)

Der `DependencyService` stellt einen einfachen Locator bereit, mit dem Sie Code für Schnittstellen in Ihrem freigegebenen Code schreiben und plattformspezifische Implementierungen bereitstellen können, die automatisch aufgelöst werden. Dadurch kann einfach auf die plattformspezifische Funktionalität in Xamarin.Forms verwiesen werden.

## <a name="effectseffectsindexmd"></a>[Effekte](effects/index.md)

Durch Effekte können native Steuerelemente auf jeder Plattform angepasst werden. Sie werden normalerweise für kleine Formatierungsänderungen verwendet.

## <a name="gesturesgesturesindexmd"></a>[Gesten](gestures/index.md)

Die Xamarin.Forms [`GestureRecognizer`](xref:Xamarin.Forms.GestureRecognizer)-Klasse unterstützt Tipp-, Zusammendrück- und Schwenkbewegungen auf Benutzeroberflächensteuerelementen.

## <a name="localizationlocalizationindexmd"></a>[Lokalisierung](localization/index.md)

Das integrierte .NET-Lokalisierungsframework kann zum Erstellen plattformübergreifender mehrsprachiger Anwendungen mit Xamarin.Forms verwendet werden.

## <a name="messaging-centermessaging-centermd"></a>[Messaging Center](messaging-center.md)

Mit Xamarin.Forms `MessagingCenter` können ViewModels und andere Komponenten kommunizieren, ohne etwas über die andere Partei wissen zu müssen, nur mit einem einfachen Nachrichtenvertrag.

## <a name="navigationnavigationindexmd"></a>[Navigation](navigation/index.md)

Xamarin.Forms stellt abhängig von dem verwendeten `Page`-Typ eine Reihe unterschiedlicher Seitennavigationen bereit.

## <a name="shellshellindexmd"></a>[Shell](shell/index.md)

Die Xamarin.Forms-Shell reduziert die Komplexität der Entwicklung mobiler Anwendungen, indem es die grundlegenden Features bereitstellt, die die meisten mobilen Anwendungen benötigen. Dazu gehören eine gemeinsame Navigationsbenutzerumgebung, ein URI-basiertes Navigationsschema und ein integrierter Suchhandler.

## <a name="templatestemplatesindexmd"></a>[Vorlagen](templates/index.md)

Steuerelementvorlagen bieten die Möglichkeit, Anwendungsseiten einfach zur Laufzeit zu entwerfen und zu überarbeiten. Mit Datenvorlagen kann die Darstellung von Daten für unterstützte Steuerelemente definiert werden.

## <a name="triggerstriggersmd"></a>[Trigger](triggers.md)

Steuerelemente können aktualisiert werden, indem auf Eigenschaftenänderungen und Ereignisse in XAML reagiert wird.
