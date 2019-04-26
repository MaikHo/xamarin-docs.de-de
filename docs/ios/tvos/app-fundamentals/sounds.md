---
title: Wiedergabe von Sound im TvOS mit AVAudioPlayer in Xamarin
description: In diesem Artikel zeigt, wie eine Hilfsklasse zum Steuern der Wiedergabe von sound mithilfe einer AVAudioPlayer in einer Xamarin.iOS-Anwendung verwendet wird.
ms.prod: xamarin
ms.assetid: E0305572-DC64-48BB-BD97-0A5096E6CA04
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 03/16/2017
ms.openlocfilehash: bc1e9febea9529c3fadbacd689404562952276fe
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61414099"
---
# <a name="playing-sound-in-tvos-with-avaudioplayer-in-xamarin"></a>Wiedergabe von Sound im TvOS mit AVAudioPlayer in Xamarin

## <a name="about-the-avaudioplayer"></a>Informationen zu den AVAudioPlayer

Die `AVAudioPlayer` dient zum Wiedergeben von Audiodaten aus Speicher oder eine Datei. Apple empfiehlt die Verwendung dieser Klasse, die audio in Ihrer app wiedergeben, es sei denn, Sie machen die streaming-Netzwerk oder mit geringer Latenz audio-e/a erfordern.

Sie können die `AVAudioPlayer` die folgenden Schritte ausführen:

- Wiedergeben von Sound beliebiger Dauer mit optionalen Schleifen.
- Mehrere Sound zur gleichen Zeit mit optionalen Synchronisierung.
- Steuern Sie Volumes, Playback-Geschwindigkeit und Stereo-Positionierung für jede Sounds wiedergeben.
- Unterstützung von Funktionen wie ein Zeitsprung oder Rewind.
- Wiedergabe-Ebene, die Verwendungsdaten zu erhalten.

`AVAudioPlayer` unterstützt von Sounds in einem beliebigen audio Format, das von iOS, TvOS und OS X angegeben sind, z. B. `.aif`, `.wav` oder `.mp3`.

## <a name="playing-sounds-in-tvos"></a>Wiedergabe von Sound in tvOS

Da TvOS dieselben Audio Toolbox Klassen als iOS unterstützt, finden Sie unserem iOS [spielen Sound mit AVAudioPlayer](https://github.com/xamarin/recipes/tree/master/Recipes/ios/media/sound/avaudioplayer) Dokumentation für die vollständigen Details der Audiowiedergabe in einer Xamarin.tvOS-app.



## <a name="related-links"></a>Verwandte Links

- [AVAudioPlayer-Referenz](https://developer.apple.com/library/ios/documentation/AVFoundation/Reference/AVAudioPlayerClassReference/)
