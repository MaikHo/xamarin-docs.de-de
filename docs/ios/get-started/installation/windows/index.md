---
title: Installieren von Xamarin.iOS unter Windows
description: In diesem Dokument wird die Einrichtung eines Windows-Computers, eines Mac-Buildhosts sowie das Koppeln von Windows und Mac für die Xamarin.iOS-Entwicklung beschrieben.
zone_pivot_groups: platform-win
ms.prod: xamarin
ms.assetid: abf85d3e-a365-44a2-b1a4-6c572c7f76dd
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 04/16/2018
ms.openlocfilehash: 12066b25ff3e5f02cf4ad17e7c8cbfdb31395405
ms.sourcegitcommit: c4be32ef914465e808d89767c4d5ee72afe93cc6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/02/2019
ms.locfileid: "58854885"
---
# <a name="installing-xamarinios-on-windows"></a>Installieren von Xamarin.iOS unter Windows

_In diesem Artikel wird beschrieben, wie Sie einen Windows-Computer und einen Mac-Buildhost zur Entwicklung mit Xamarin.iOS einrichten._

::: zone pivot="windows"

## <a name="overview"></a>Übersicht

Zur Erstellung von Xamarin.iOS-Apps mit Visual Studio 2019 unter Windows benötigen Sie Folgendes:

- Einen Windows-Computer, auf dem Visual Studio 2019 installiert ist. Dabei kann es sich um einen physischen oder virtuellen Computer handeln.

  - [Systemanforderungen für Windows](~/cross-platform/get-started/requirements.md#windows-requirements)

- Einen Mac, der über ein Netzwerk zugänglich ist. Für diesen müssen die Apple-Buildtools und Xamarin.iOS eingerichtet sein. Visual Studio 2019 greift über eine Netzwerkverbindung auf diesen Computer zu, um die Apple-Buildtools zu verwenden. Diese werden zum Kompilieren von nativen iOS-Anwendungen benötigt.

  - [Systemanforderungen für Mac](~/cross-platform/get-started/requirements.md#macos-requirements)

## <a name="setup"></a>Setup

Führen Sie zur Einrichtung von Xamarin.iOS in Visual Studio 2019 die folgenden Schritte aus:

1. Einrichten des Windows-Computers (Installieren von Visual Studio 2019)

    Xamarin.iOS kann mit den Editionen Visual Studio 2019 Community, Professional und Enterprise auf einem eigenständigen oder virtuellen Computer verwendet werden.

    - [Visual Studio 2019 installieren](~/get-started/installation/windows.md)

2. Einrichten des Macs (Installieren von Xcode und Visual Studio für Mac)

    Wenn Sie iOS-Anwendungen zur Verteilung erstellen, debuggen und signieren möchten, muss Visual Studio 2017 über eine Netzwerkverbindung auf einen Mac-Buildhost zugreifen können, für den sowohl die Apple-Entwicklertools (Xcode) als auch Xamarin.iOS konfiguriert sind.

    - [Laden Sie Xcode aus dem Mac App Store herunter, und installieren Sie die IDE](https://itunes.apple.com/us/app/xcode/id497799835?mt=12). 
    - [Installieren Sie Visual Studio für Mac](https://docs.microsoft.com/visualstudio/mac/installation), wodurch auch Xamarin.iOS installiert wird.

    > [!NOTE]
    > Wenn Sie Visual Studio für Mac nicht installieren möchten, kann in Visual Studio 2019 [der Mac-Buildhost automatisch mit der Software konfiguriert werden](https://docs.microsoft.com/visualstudio/releasenotes/vs2017-relnotes#automatic-macos-provisioning), die zur Erstellung von Xamarin.iOS-Anwendungen erforderlich ist. Weitere Informationen finden Sie unter [Automatische Bereitstellung eines Macs](~/ios/get-started/installation/windows/connecting-to-mac/index.md#automatic-mac-provisioning).

3. Führen Sie eine Kopplung mit dem Mac durch (Verbinden von Visual Studio 2019 mit dem Mac)

    Damit Visual Studio 2019 auf die iOS-Buildtools auf dem Mac zugreifen kann, müssen beide Computer über ein Netzwerk verbunden sein.

    - Informationen hierzu finden Sie im Leitfaden [Durchführen einer Kopplung mit einem Mac](~/ios/get-started/installation/windows/connecting-to-mac/index.md).

::: zone-end
::: zone pivot="win-vs2017"

## <a name="overview"></a>Übersicht

Zur Erstellung von Xamarin.iOS-Apps mit Visual Studio 2017 unter Windows benötigen Sie Folgendes:

-  Einen Windows-Computer, auf dem Visual Studio 2017 installiert ist. Dabei kann es sich um einen physischen oder virtuellen Computer handeln.
    - [Systemanforderungen für Windows](~/cross-platform/get-started/requirements.md#windows-requirements)
    
-  Einen Mac, der über ein Netzwerk zugänglich ist. Für diesen müssen die Apple-Buildtools und Xamarin.iOS eingerichtet sein. Visual Studio 2017 greift über eine Netzwerkverbindung auf diesen Computer zu, um die Apple-Buildtools zu verwenden. Diese werden zum Kompilieren von nativen iOS-Anwendungen benötigt. 
    - [Systemanforderungen für Mac](~/cross-platform/get-started/requirements.md#macos-requirements)

## <a name="setup"></a>Setup

Führen Sie zur Einrichtung von Xamarin.iOS in Visual Studio 2017 die folgenden Schritte aus:

1. Einrichten des Windows-Computers (Installieren von Visual Studio 2017)

    Xamarin.iOS kann mit den Editionen Visual Studio 2017 Community, Professional und Enterprise auf einem eigenständigen oder virtuellen Computer verwendet werden.
    
    - [Installieren Sie Visual Studio 2017](~/get-started/installation/windows.md).

2. Einrichten des Macs (Installieren von Xcode und Visual Studio für Mac)

    Wenn Sie iOS-Anwendungen zur Verteilung erstellen, debuggen und signieren möchten, muss Visual Studio 2017 über eine Netzwerkverbindung auf einen Mac-Buildhost zugreifen können, für den sowohl die Apple-Entwicklertools (Xcode) als auch Xamarin.iOS konfiguriert sind.

    - [Laden Sie Xcode aus dem Mac App Store herunter, und installieren Sie die IDE](https://itunes.apple.com/us/app/xcode/id497799835?mt=12). 
    - [Installieren Sie Visual Studio für Mac](https://docs.microsoft.com/visualstudio/mac/installation), wodurch auch Xamarin.iOS installiert wird.

    > [!NOTE]
    > Wenn Sie Visual Studio für Mac nicht installieren möchten, kann ab der [Version 15.6 von Visual Studio 2017](https://docs.microsoft.com/visualstudio/releasenotes/vs2017-relnotes#automatic-macos-provisioning) der Mac-Buildhost automatisch mit der Software konfiguriert werden, die zur Erstellung von Xamarin.iOS-Anwendungen erforderlich ist. Weitere Informationen finden Sie unter [Automatische Bereitstellung eines Macs](~/ios/get-started/installation/windows/connecting-to-mac/index.md#automatic-mac-provisioning).

3. Durchführen einer Kopplung mit dem Mac (Verbinden von Visual Studio 2017 mit dem Mac)

    Damit Visual Studio 2017 auf die iOS-Buildtools auf dem Mac zugreifen kann, müssen beide Computer über ein Netzwerk verbunden sein.

    - Informationen hierzu finden Sie im Leitfaden [Durchführen einer Kopplung mit einem Mac](~/ios/get-started/installation/windows/connecting-to-mac/index.md).

::: zone-end

## <a name="summary"></a>Zusammenfassung

In diesem Artikel wurde beschrieben, wie Sie einen Windows-Computer und den zugehörigen Mac-Buildhost zur Entwicklung mit Xamarin.iOS einrichten.

## <a name="next-steps"></a>Nächste Schritte

- [Einführung in Xamarin.iOS für Visual Studio](introduction-to-xamarin-ios-for-visual-studio.md)
- [Konfigurieren von Visual Studio für die iOS-Entwicklung](config-options.md)
- [Bereitstellung von Geräten](~/ios/get-started/installation/device-provisioning/index.md)
