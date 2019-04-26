---
title: "Android.Support.v7.AppCompat: Keine Ressource gefunden, die mit dem angegebenen Namen übereinstimmt: attr 'android:actionModeShareDrawable'"
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 5814069C-FC43-41DE-B5A5-024D05E59929
ms.technology: xamarin-android
author: conceptdev
ms.author: crdun
ms.date: 03/09/2018
ms.openlocfilehash: ff2a586773e33a1f4cf78657c3c69c22e79ed047
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61153372"
---
# <a name="androidsupportv7appcompat---no-resource-found-that-matches-the-given-name-attr-androidactionmodesharedrawable"></a>Android.Support.v7.AppCompat: Keine Ressource gefunden, die mit dem angegebenen Namen übereinstimmt: attr 'android:actionModeShareDrawable'

1. Stellen Sie sicher, dass Sie die neuesten Extras als auch für die Android 5.0 (API 21) über den Android SDK-Manager-SDK herunterladen.

2. Stellen Sie sicher, dass Sie die Anwendung mit CompileSdkVersion auf 21 festgelegt kompilieren. Sie können optional die TargetSdkVersion auf 21 ebenfalls festlegen.

3. Wenn Sie eine frühere Version, z. B. API-19 benötigen, laden Sie die entsprechende Version finden Sie auf der Seite "Nuget":

[https://www.nuget.org/packages/Xamarin.Android.Support.v7.AppCompat/](https://www.nuget.org/packages/Xamarin.Android.Support.v7.AppCompat/)

*Hinweis:* Wenn Sie manuell dies über die Paket-Manager-Konsole installieren, stellen Sie sicher, dass Sie auch die gleiche Version von Xamarin.Android.Support.v4 installieren.

[https://www.nuget.org/packages/Xamarin.Android.Support.v4/](https://www.nuget.org/packages/Xamarin.Android.Support.v4/)

Stack Overflow-Referenz: [https://stackoverflow.com/questions/26431676/appcompat-v721-0-0-no-resource-found-that-matches-the-given-name-attr-andro](https://stackoverflow.com/questions/26431676/appcompat-v721-0-0-no-resource-found-that-matches-the-given-name-attr-andro)

## <a name="see-also"></a>Siehe auch

- [Welche Android SDK-Pakete sollte ich installieren?](~/android/troubleshooting/questions/install-android-sdk-packages.md)

