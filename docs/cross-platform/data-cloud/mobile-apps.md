---
title: Microsoft Azure Mobile Apps
description: Dieses Dokument enthält Links zu Leitfäden, die beschreiben, wie Sie eine Xamarin-app zu erstellen, die mit Azure verbunden ist. Er erläutert das Arbeiten mit der Azure-Xamarin-Komponente, Benutzer und Push-Benachrichtigungen.
ms.prod: xamarin
ms.assetid: 7B9AA8D9-C181-4C33-8AB0-2F56E4DBFC03
author: conceptdev
ms.author: crdun
ms.date: 04/02/2017
ms.openlocfilehash: a1a0b078659441f0f45af66728a5f37d578d6274
ms.sourcegitcommit: 58d8bbc19ead3eb535fb8248710d93ba0892e05d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2019
ms.locfileid: "67675090"
---
# <a name="microsoft-azure-mobile-apps"></a>Microsoft Azure Mobile Apps

_Beispiele und Code-downloads für die Azure-Portal-Dokumentation._

<!--
NOTE TO AUTHORS: this page is referenced from
https://azure.microsoft.com/develop/mobile/xamarin/
as https://developer.xamarin.com/guides/cross-platform/data-cloud/mobile-services/
A redirect has been put in place to /mobile-apps/ HOWEVER the /Resources/ .ZIP files are still located in /mobile-services/ so that the following permalinks don't break

The ZIPs in /Resources/ are also referenced by inbound links
Getting Started  http://go.microsoft.com/fwlink/p/?LinkId=331359
Get started with data   http://go.microsoft.com/fwlink/p/?LinkId=331302
Get started with push   http://go.microsoft.com/fwlink/p/?LinkId=331303
Get started with authentication http://go.microsoft.com/fwlink/p/?LinkId=331328
Get started with Notification Hubs  http://go.microsoft.com/fwlink/p/?LinkId=331329
Validate and modify data    http://go.microsoft.com/fwlink/p/?LinkId=331330
-->


Diese Links sind für die Xamarin-Dokumentation, die auf die [Azure Mobile Apps](https://docs.microsoft.com/azure/app-service-mobile/) Website.
Hinzufügen von Azure-Funktionen zu einer Xamarin-app durch Herunterladen der [Azure Mobile Client](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/).

## <a name="working-with-the-xamarin-azure-component"></a>Arbeiten mit der Xamarin-Azure-Komponente

Allgemeine Dokumentation [arbeiten mit der Xamarin-Clientbibliothek (Komponente)](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library) Ausführen verschiedener Aufgaben mit Azure Mobile Apps. Diese Seite enthält viele Beispielcodeausschnitten, ohne die ausführliche Beschreibungen und Beispiele, die in jedem der unten aufgeführten Artikeln für die exemplarische Vorgehensweise zur Verfügung.

## <a name="getting-started"></a>Erste Schritte

Dieser Artikel enthält schrittweise Anweisungen zum Einrichten und Ausführen Ihrer ersten Xamarin-Azure-app zu erhalten.
Erstellen eine neue Azure Mobile App im Portal, und klicken Sie dann herunterladen und Ausführen der app vorkonfiguriert, dass hierin.

-  [iOS](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-xamarin-ios-get-started/)
-  [Android](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-xamarin-android-get-started/)
-  [Xamarin.Forms](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-xamarin-forms-get-started)

<!--
## Validate, Modify and Augment Data in Scripts

Demonstrates how to add server-side scripts to Azure Mobile Services data tables to implement server-side validation and other functionality.

-  [iOS](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-how-to-use-client-library/#errors)
-  [Android](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-how-to-use-client-library/#errors)
-->

<!--
## Add Paging to Data

A quick example of paging large sets of data using Skip() and Take().

-  [iOS](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-how-to-use-client-library/#paging)
-  [Android](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-how-to-use-client-library/#paging)
-->

## <a name="get-started-with-users"></a>Erste Schritte mit Benutzern

Stellt ausführliche Anweisungen zum Konfigurieren und codieren einen Anmeldebildschirm mit Azure Mobile Services bereit. Anbieter werden unterstützt: Microsoft, Google, Facebook und Twitter.

-  [iOS](https://azure.microsoft.com/documentation/articles/app-service-mobile-xamarin-ios-get-started-users/)
-  [Android](https://azure.microsoft.com/documentation/articles/app-service-mobile-xamarin-android-get-started-users/)


## <a name="authorize-users-in-scripts"></a>Autorisieren von Benutzern in Skripts

Beispielcode für die Javascript-Back-Ends

-  [Todo.js](https://github.com/Azure/azure-mobile-apps-node/blob/master/samples/personal-table/tables/TodoItem.js#L38)


## <a name="get-started-with-push"></a>Erste Schritte mit Pushbenachrichtigungen

Führen Sie die Anweisungen zum Konfigurieren von Pushbenachrichtigungen auf den Apple und Google-Websites, und klicken Sie dann senden eine Pushbenachrichtigung an ein Gerät von Azure Mobile Services.

-  [iOS](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-xamarin-ios-get-started-push)
-  [Android](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-xamarin-android-get-started-push)


## <a name="get-started-with-notification-hubs"></a>Erste Schritte mit Notification Hubs

Führen Sie die Anweisungen zum Konfigurieren von Pushbenachrichtigungen auf den Apple und Google-Websites, Konfigurieren des Azure Notification Hubs und klicken Sie dann Pushbenachrichtigungen an Geräte zu generieren.

-  [iOS](https://docs.microsoft.com/azure/notification-hubs/xamarin-notification-hubs-ios-push-notification-apns-get-started)
-  [Android](https://docs.microsoft.com/azure/notification-hubs/xamarin-notification-hubs-push-notifications-android-gcm)



## <a name="related-links"></a>Verwandte Links

- [Erste Schritte (Beispiel)](https://github.com/xamarin/mobile-samples/tree/master/Azure/GettingStarted)
- [GetStartedWithData-(Beispiel)](https://github.com/xamarin/mobile-samples/tree/master/Azure/GetStartedWithData)
- [GetStartedWithUsers (Beispiel)](https://github.com/xamarin/mobile-samples/tree/master/Azure/GetStartedWithUsers)
- [GetStartedWithPush (Beispiel)](https://github.com/xamarin/mobile-samples/tree/master/Azure/GetStartedWithPush)
- [NotificationHubs (Beispiel)](https://github.com/xamarin/mobile-samples/tree/master/Azure/NotificationHubs)
- [Azure Mobile Client](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
- [Lernpfad für Azure Mobile Apps](https://azure.microsoft.com/documentation/learning-paths/appservice-mobileapps/)

<!--
- [ValidateModifyData (sample)](https://github.com/xamarin/mobile-samples/tree/master/Azure/ValidateModifyData)
-->
