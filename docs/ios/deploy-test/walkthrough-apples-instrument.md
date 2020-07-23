---
title: 'Exemplarische Vorgehensweise: Verwenden des Apple-Tools „Instruments“'
description: In diesem Artikel wird die Verwendung des Apple-Tools Instruments erläutert, um Speicherprobleme in einer iOS-Anwendung zu diagnostizieren, die mit Xamarin erstellt wurde. Es wird gezeigt, wie Instruments gestartet wird, wie Heap-Momentaufnahmen erfasst werden, wie der Anstieg des benötigten Speichers analysiert wird und mehr.
ms.prod: xamarin
ms.assetid: 8f21db1d-7107-4158-8058-d47e417689a0
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/19/2017
ms.openlocfilehash: 6fa1357adc9cf2f545fbcdf3a30fef70280593bb
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/22/2020
ms.locfileid: "86938020"
---
# <a name="walkthrough---using-apples-instruments-tool"></a>Exemplarische Vorgehensweise: Verwenden des Apple-Tools „Instruments“

_Dieser Artikel erläutert die Verwendung des Apple-Tools Instruments, um Speicherprobleme in einer iOS-Anwendung zu diagnostizieren, die mit Xamarin erstellt wurde. Es wird gezeigt, wie Instruments gestartet wird, wie Heap-Momentaufnahmen erfasst werden und wie der Anstieg des benötigten Speichers analysiert wird. Ebenfalls wird beschrieben, wie Instruments dafür verwendet wird, die genauen Codezeilen zu ermitteln und anzuzeigen, die das Speicherproblem verursachen._

Diese Seite erläutert, wie das **Xcode-Tool Instruments** dafür verwendet wird, Arbeitsspeicherprobleme in einer iOS-Anwendung zu diagnostizieren.
Laden Sie zunächst das [MemoryDemo-Beispiel](https://docs.microsoft.com/samples/xamarin/ios-samples/profiling-memorydemo) herunter und öffnen Sie die Projektmappe **before** in Visual Studio für Mac.

## <a name="diagnosing-the-memory-issues"></a>Diagnostizieren von Arbeitsspeicherproblemen

1. Starten Sie in Visual Studio für Mac die **Instrumente** über das Menüelement **Tools > Instrumente starten**.
2. Laden Sie die Anwendung auf das Gerät hoch, indem Sie das Menüelement **Ausführen > Auf Gerät hochladen** verwenden.
3. Wählen Sie die Vorlage **Zuordnungen** (orangefarbenes Symbol mit weißem Feld) aus.

    ![Auswählen der Vorlage „Zuordnungen“](walkthrough-apples-instrument-images/00-allocations-tempate.png)

4. Wählen Sie die Anwendung **Memory Demo** aus der Liste **Choose a profiling template for:** (Profilerstellungsvorlage auswählen für:) im oberen Bereich des Fensters aus. Klicken Sie zunächst auf das iOS-Gerät, um das Menü zu erweitern, das die installierten Anwendungen anzeigt.

    ![Auswählen der „Memory Demo“-Anwendung](walkthrough-apples-instrument-images/01-mem-demo.png)

5. Drücken Sie auf die Schaltfläche **Auswählen** (unten rechts im Fenster), um **Instrumente** zu starten. Durch die Auswahl dieser Vorlage werden zwei Elemente im oberen Bereich angezeigt: „Allocations“ (Speicherbelegung) und „VM Tracker“ (VM-Tracker).

6. Klicken Sie auf in Instruments auf die Schaltfläche **Aufnehmen** (roter Kreis oben links), um die Anwendung zu starten.

7. Wählen Sie im oberen Bereich die Zeile **VM-Tracker** aus. Da die App nun ausgeführt wird, enthält diese zwei Abschnitte: Dirty Size und Resident Size. Wählen Sie im Bereich **Inspektor** die Option **Show Display Settings** (Anzeigeeinstellungen anzeigen) (das Zahnradsymbol) aus, und aktivieren Sie dann das Kontrollkästchen **Automatic Snapshotting** (Automatische Momentaufnahme), das unten rechts auf diesem Screenshot angezeigt wird:

    ![Auswählen der Option „Show Display Settings“ (Anzeigeeinstellungen anzeigen) (Zahnradsymbol) und anschließendes Aktivieren des Kontrollkästchens „Automatic Snapshotting“ (Automatische Momentaufnahme)](walkthrough-apples-instrument-images/02-auto-snapshot.png)

8. Wählen Sie im oberen Bereich die Zeile **Zuordnungen** aus. Da die App nun ausgeführt wird, zeigt diese *All Heap and Anonymous VM* (Alle Heaps und anonymen VMs) an.
9. Wählen Sie im Bereich **Inspektor** die Option **Anzeigeeinstellungen anzeigen** (das Zahnradsymbol) aus, und klicken Sie dann auf die Schaltfläche **Mark Generation** (Markierungsgenerierung), um eine Baseline zu erstellen. Eine kleine rote Flagge wird im oberen Bereich des Fensters auf der Zeitachse angezeigt.
10. Scrollen Sie durch die Anwendung, und klicken Sie dann erneut auf **Markierungsgenerierung** (mehrmals wiederholen).
11. Klicken Sie auf die Schaltfläche **Beenden**.
12. Erweitern Sie den Knoten **Generierung**, der das größte **Wachstum** aufweist, und sortieren Sie nach **Wachstum** (absteigend).
13. Ändern Sie den Bereich **Inspektor** in **Show Extended Detail** (Erweiterte Details anzeigen) (das „E“), wodurch die **Stapelüberwachung** angezeigt wird.

14. Beachten Sie, dass der Knoten **&lt;non-object>** einen übermäßigen Arbeitsspeicherzuwachs anzeigt. Klicken Sie auf den Pfeil neben diesem Knoten, um weitere Details anzuzeigen. Klicken Sie mit der rechten Maustaste auf die Stapelüberwachung, um einen **Quellort** zum Bereich hinzuzufügen:

    ![Hinzufügen des Quellspeicherorts zum Bereich](walkthrough-apples-instrument-images/03-mem-growth.png)

15. Sortieren Sie nach **Größe**, und zeigen Sie die Ansicht **Extended Detail** (Erweiterte Details) an:

    ![Sortieren nach Größe und Anzeigen der Ansicht „Extended Detail“ (Erweiterte Details)](walkthrough-apples-instrument-images/04-extended-detail.png)

16. Klicken Sie auf den gewünschten Eintrag in der Aufrufliste, um den zugehörigen Code anzeigen zu lassen:

    ![Anzeigen von zugehörigem Code](walkthrough-apples-instrument-images/05-related-code.png)

In diesem Fall wird ein neues Bild erstellt und für jede Zelle in einer Auflistung gespeichert. Die bestehenden Zellen der Auflistungsansicht werden nicht wiederverwendet.

## <a name="resolving-the-memory-issues"></a>Lösen von Arbeitsspeicherproblemen

Es ist möglich, diese Probleme zu beheben und die Anwendung erneut mithilfe von Instruments auszuführen.

Indem Sie eine einzelne Instanz auf Klassenebene deklarieren, können das Bild und das Zellenobjekt wie im Folgenden dargestellt aus einem vorhandenen Pool wiederverwendet werden, statt jedes Mal erneut erstellt werden zu müssen:

```csharp
public override UICollectionViewCell GetCell (UICollectionView collectionView, NSIndexPath indexPath)
{
    // Dequeue a cell from the reuse pool
    var imageCell = (ImageCell)collectionView.DequeueReusableCell (cellId, indexPath);

    // Reuse the image declared at the class level
    imageCell.ImageView.Image = image;

    return imageCell;
}
```

Nun, da die Anwendung ausgeführt wird, ist die Arbeitsspeicherauslastung erheblich reduziert. Das **Wachstum** der Generierungen wird nun in KiB (Kilobyte) statt wie vor dem Korrigieren des Codes in MiB (Megabyte) gemessen:

![Anzeigen der Anwendungsspeichernutzung](walkthrough-apples-instrument-images/06-reduced-memory.png)

Der verbesserte Code ist in Visual Studio für Mac in der Projektmappe **after** im [MemoryDemo-Beispiel](https://docs.microsoft.com/samples/xamarin/ios-samples/profiling-memorydemo) verfügbar.

Dieser Communityblog über [Xamarin.iOS-Garbage Collection](https://c-sharx.net/2015-04-27-xamarin-ios-the-garbage-collector-and-me/) ist hilfreich für den Umgang mit Arbeitsspeicherproblemen mit Xamarin.iOS.

## <a name="summary"></a>Zusammenfassung

In diesem Artikel wurde die Verwendung von Instruments zum Diagnostizieren von Arbeitsspeicherproblemen erläutert.
Es wurde beschrieben, wie Instrumente von Visual Studio für Mac aus gestartet werden, wie die Vorlage für die Arbeitsspeicherzuordnung geladen wird und wie Momentaufnahmen verwendet werden, um Arbeitsspeicherprobleme zu ermitteln.
Schließlich wurde die Anwendung erneut überprüft, um sicherzustellen, dass das Problem behoben wurde.

## <a name="related-links"></a>Verwandte Links

- [MemoryDemo-Beispiel](https://docs.microsoft.com/samples/xamarin/ios-samples/profiling-memorydemo)
- [Xamarin.iOS-Garbage Collection (Blogbeitrag)](https://c-sharx.net/2015-04-27-xamarin-ios-the-garbage-collector-and-me/)
