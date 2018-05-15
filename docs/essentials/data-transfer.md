---
title: Xamarin.Essentials-Datenübertragung
description: Die Klasse DataTransfer ermöglicht einer Anwendung zur Freigabe von Daten, z. B. Links "Text" und "Web" für andere Anwendungen auf dem Gerät.
ms.assetid: B7B01D55-0129-4C87-B515-89F8F4E94665
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: baec3bdd89cb98d7595a524b6b9c4263ca18aa41
ms.sourcegitcommit: 0a72c7dea020b965378b6314f558bf5360dbd066
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/10/2018
---
# <a name="xamarinessentials-data-transfer"></a>Xamarin.Essentials-Datenübertragung

![Vorabversion NuGet](~/media/shared/pre-release.png)

Die **DataTransfer** Klasse ermöglicht einer Anwendung, z. B. Text und Web Verknüpfungen für andere Anwendungen auf dem Gerät Daten gemeinsam nutzen.

## <a name="using-data-transfer"></a>Verwenden die Datenübertragung

Fügen Sie einen Verweis auf Xamarin.Essentials in Ihrer Klasse hinzu:

```csharp
using Xamarin.Essentials;
```

Die Funktionalität zum Übertragen von Daten durch den Aufruf funktioniert die `RequestAsync` Methode mit einem Anforderung-Nutzlast, die Informationen zur Freigabe für andere Anwendungen umfasst. Text- und Uri können gemischt werden, und jede Plattform Filterung anhand des Inhalts behandelt.

```csharp

public class DataTransferTest
{
    public async Task ShareText(string text)
    {
        await DataTransfer.RequestAsync(new ShareTextRequest
            {
                Text = text,
                Title = "Share Text"
            });
    }

    public async Task ShareUri(string uri)
    {
        await DataTransfer.RequestAsync(new ShareTextRequest
            {
                Uri = uri,
                Title = "Share Web Link"
            });
    }
}
```

Benutzeroberfläche für die externe Anwendung freigeben, die angezeigt wird, wenn die Anforderung erfolgt:

![Datenübertragung](data-transfer-images/data-transfer.png)

## <a name="platform-differences"></a>Platform-Unterschiede

| Plattform | Unterschied |
| --- | --- |
| Android | Eigenschaft "Subject" wird für die gewünschte Betreff einer Nachricht verwendet. |
| iOS | Betreff, die nicht verwendet werden. |
| iOS | Der Titel nicht verwendet. |
| UWP | Titel wird standardmäßig auf den Anwendungsnamen, sofern nichts anderes festgelegt. |
| UWP | Betreff, die nicht verwendet werden. |

## <a name="api"></a>API

- [Data Transfer-Quellcode](https://github.com/xamarin/Essentials/tree/master/Essentials/DataTransfer)
- [Data Transfer API-Dokumentation](xref:Xamarin.Essentials.DataTransfer)