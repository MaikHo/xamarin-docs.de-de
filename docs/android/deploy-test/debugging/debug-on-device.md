---
title: Debugvorgang auf einem Gerät
description: In diesem Artikel wird das Debuggen einer Xamarin.Android-Anwendung auf einem physischen Android-Gerät erläutert.
ms.prod: xamarin
ms.assetid: 153D3746-A27F-198B-48FE-D219C0133A79
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 02/16/2018
ms.openlocfilehash: e697459b20a481b1d2bada69677647ad4fbd3023
ms.sourcegitcommit: 2fbe4932a319af4ebc829f65eb1fb1816ba305d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/29/2019
ms.locfileid: "73021586"
---
# <a name="debug-on-device"></a>Debugvorgang auf einem Gerät

_In diesem Artikel wird das Debuggen einer Xamarin.Android-Anwendung auf einem physischen Android-Gerät erläutert._

## <a name="debug-on-device-overview"></a>Übersicht: Debuggen auf einem Gerät

Es ist möglich, eine Xamarin.Android-Anwendung auf einem Android-Gerät mit Visual Studio für Mac oder Visual Studio zu debuggen. Bevor ein Gerät debuggt werden kann, muss es [für die Entwicklung vorbereitet](~/android/get-started/installation/set-up-device-for-development.md), und mit Ihrem PC oder Mac verbunden werden.

## <a name="debug-application"></a>Debuggen der Anwendung

Nachdem ein Gerät mit dem Computer verbunden ist, erfolgt auf die gleiche Weise wie bei anderen Xamarin-Produkten oder .NET-Anwendungen das Debuggen einer Xamarin.Android-Anwendung. Stellen Sie sicher, dass die **Debug**-Konfiguration und das externe Gerät in der IDE ausgewählt werden. Dadurch wird sichergestellt, dass die erforderlichen Debugsymbole verfügbar sind, und dass die IDE eine Verbindung mit der ausgeführten Anwendung herstellen kann: 

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

![Debugkonfiguration ausgewählt](debug-on-device-images/image1-vs.png)

Als nächstes wird ein Haltepunkt im Code festgelegt:

![Haltepunkt in der Codezeile festgelegt](debug-on-device-images/image2-vs.png)

Nachdem das Gerät ausgewählt wurde, wird Xamarin.Android eine Verbindung mit dem Gerät herstellen, die Anwendung bereitstellen und sie dann ausführen. Wenn der Haltepunkt erreicht wird, hält der Debugger die Anwendung an. Die Anwendung kann ähnlich wie andere C#-Anwendungen debuggt werden: 

![Haltepunkt erreicht](debug-on-device-images/image3-vs.png)

# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio für Mac](#tab/macos)

![Debugkonfiguration ausgewählt](debug-on-device-images/image1-xs.png)

Als nächstes wird ein Haltepunkt im Code festgelegt:

![Haltepunkt in der Codezeile festgelegt](debug-on-device-images/image2-xs.png)

Nachdem das Gerät ausgewählt wurde, wird Xamarin.Android eine Verbindung mit dem Gerät herstellen, die Anwendung bereitstellen und sie dann ausführen. Wenn der Haltepunkt erreicht wird, hält der Debugger die Anwendung an. Die Anwendung kann ähnlich wie andere C#-Anwendungen debuggt werden: 

![Haltepunkt erreicht](debug-on-device-images/image3-xs.png)

-----

## <a name="summary"></a>Zusammenfassung

In diesem Dokument wird erläutert, wie eine Xamarin.Android-Anwendung durch das Festlegen eines Haltepunkts und das Auswählen eines Zielgeräts debuggt wird.

## <a name="related-links"></a>Verwandte Links

- [Set Up Device for Development (Einrichten eines Geräts für die Entwicklung)](~/android/get-started/installation/set-up-device-for-development.md)
- [Festlegen des Debuggable-Attributs](~/android/deploy-test/debuggable-attribute.md)
