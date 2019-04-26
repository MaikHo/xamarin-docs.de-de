---
title: Fehler wegen fehlender Pakete nach dem Aktualisieren von NuGet-Paketen
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: D61CC966-1D4A-49A5-8A6F-41572E28329B
author: asb3993
ms.author: amburns
ms.date: 05/08/2018
ms.openlocfilehash: 7cb802dd60d4e4879a260ff56d4f94ea5acb2965
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61356889"
---
# <a name="missing-packages-error-after-updating-nuget-packages"></a>Fehler wegen fehlender Pakete nach dem Aktualisieren von NuGet-Paketen

Dieses Problem wurde in erster Linie auf Xamarin.Forms-Beispiel-app-Lösungen gemeldet, aber das Potenzial für dieses Problem kann auftreten, in einem Projekt, das NuGet-Pakete verwendet. 

Nach dem Update des Nuget-Pakete in Ihrem Projekt oder Projektmappe, sehen Sie eine Fehlermeldung, die die alte Paket-Versionsnummern, z. B. verweist:

```csharp
Error: This project references NuGet package(s) that are missing on this computer.
Enable NuGet Package Restore to download them.  
For more information, see http://go.microsoft.com/fwlink/?LinkID=322105

The missing file is ../../packages/Xamarin.Forms.1.3.1.6296/build/portable-win+net45+wp80+MonoAndroid10+MonoTouch10+Xamarin.iOS10/Xamarin.Forms.targets. (FormsGallery)
```

In diesem Beispiel *Xamarin.Forms.1.3.1.6296* ist die alte Versionsnummer, die mit dem Update des Nuget-Paket entfernt wurde.

Dies kann auftreten, wenn die XML-Elemente in der CSPROJ-Datei, die Versionsnummer des alten Pakets verweisen manuell hinzugefügt wurden oder bearbeitet, Nuget nicht entfernen oder aktualisieren Sie sie an, wenn sie manuell hinzugefügt/bearbeitet, gewesen wäre, damit das Projekt jetzt Pakete sucht, die wurden gelöscht. 

Um dieses Problem zu beheben, bearbeiten Sie die CSPROJ-Dateien manuell, und löschen Sie alle Elemente, die die alte Versionsnummer verweisen an. 

Beispielelemente zu entfernen (Wenn sie die Versionsnummer des alten Pakets besitzen):

```xml
<Reference Include="Xamarin.Forms.Maps">
    <HintPath>..\..\packages\Xamarin.Forms.Maps.1.3.1.6296\lib\portable-win+net45+wp80+MonoAndroid10+MonoTouch10+Xamarin.iOS10\Xamarin.Forms.Maps.dll</HintPath>
</Reference>

<Import Project="..\..\packages\Xamarin.Forms.1.3.1.6296\build\portable-win+net45+wp80+MonoAndroid10+MonoTouch10+Xamarin.iOS10\Xamarin.Forms.targets" Condition="Exists('..\..\packages\Xamarin.Forms.1.3.1.6296\build\portable-win+net45+wp80+MonoAndroid10+MonoTouch10+Xamarin.iOS10\Xamarin.Forms.targets')" />
<Error Condition="!Exists('..\..\packages\Xamarin.Forms.1.3.1.6296\build\portable-win+net45+wp80+MonoAndroid10+MonoTouch10+Xamarin.iOS10\Xamarin.Forms.targets')" Text="$([System.String]::Format('$(ErrorText)', '..\..\packages\Xamarin.Forms.1.3.1.6296\build\portable-win+net45+wp80+MonoAndroid10+MonoTouch10+Xamarin.iOS10\Xamarin.Forms.targets'))" />
```