---
title: XAML-Kompilierung in Xamarin.Forms
description: In diesem Artikel wird erläutert, wie XAML optional direkt in intermediate Language (IL) mit der Xamarin.Forms-XAML-Compiler (XAMLC) kompiliert werden kann.
ms.prod: xamarin
ms.assetid: 9A2D10A6-5DFC-485F-A75A-2F7B98314025
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/22/2018
ms.openlocfilehash: 9567f3ad8d748a94a03cd1c86254072d4ba3bbdc
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61075119"
---
# <a name="xaml-compilation-in-xamarinforms"></a>XAML-Kompilierung in Xamarin.Forms

_XAML kann optional auch direkt in intermediate Language (IL) mit dem XAML-Compiler (XAMLC) kompiliert werden._

XAML-Kompilierung bietet eine Reihe von Vorteilen:

- Er führt eine XAML-Überprüfung zur Kompilierzeit durch und benachrichtigt den Benutzer über eventuelle Fehler.
- Er entfernt etwas Lade- und Instanziierungszeit für XAML-Elemente.
- Er hilft bei der Verringerung der Dateigröße der finalen Assembly, indem XAML-Dateien nicht mehr eingeschlossen werden.

XAML-Kompilierung ist standardmäßig für die Abwärtskompatibilität sichergestellt deaktiviert. Es kann durch Hinzufügen der Assembly und Klasse-Ebene aktiviert werden die [ `XamlCompilation` ](xref:Xamarin.Forms.Xaml.XamlCompilationAttribute) Attribut.

Im folgenden Codebeispiel wird veranschaulicht, sodass XAML-Kompilierung auf der Assemblyebene:

```csharp
using Xamarin.Forms.Xaml;
...
[assembly: XamlCompilation (XamlCompilationOptions.Compile)]
namespace PhotoApp
{
  ...
}
```

In diesem Beispiel wird mit XAML-Fehlern, die zur Kompilierzeit statt zur Laufzeit gemeldet wird zur Kompilierzeit von allen XAML, die innerhalb der Assembly enthaltenen ausgeführt werden. Aus diesem Grund die `assembly` Präfix für die [ `XamlCompilation` ](xref:Xamarin.Forms.Xaml.XamlCompilationAttribute) Attribut gibt an, dass das Attribut für die gesamte Assembly gilt.

> [!NOTE]
> Die [ `XamlCompilation` ](xref:Xamarin.Forms.Xaml.XamlCompilationAttribute) Attribut und die [ `XamlCompilationOptions` ](xref:Xamarin.Forms.Xaml.XamlCompilationOptions) Enumeration befinden sich in der `Xamarin.Forms.Xaml` -Namespace, der für deren Verwendung importiert werden muss.

Im folgenden Codebeispiel wird veranschaulicht, sodass XAML-Kompilierung auf Klassenebene:

```csharp
using Xamarin.Forms.Xaml;
...
[XamlCompilation (XamlCompilationOptions.Compile)]
public class HomePage : ContentPage
{
  ...
}
```

In diesem Beispiel während der Kompilierung der XAML für die Überprüfung der `HomePage` Klasse erfolgen und Fehler, die als Teil des Kompilierungsprozesses gemeldet.

> [!NOTE]
> Kompilierte Bindungen können aktiviert werden, um die Bindung datenleistung in Xamarin.Forms-Anwendungen zu verbessern. Weitere Informationen finden Sie unter [kompiliert Bindungen](~/xamarin-forms/app-fundamentals/data-binding/compiled-bindings.md).

## <a name="related-links"></a>Verwandte Links

- [`XamlCompilation`](xref:Xamarin.Forms.Xaml.XamlCompilationAttribute)
- [`XamlCompilationOptions`](xref:Xamarin.Forms.Xaml.XamlCompilationOptions)
