---
title: "Überwachen von Inhalt | System Center Configuration Manager"
description: "Hier finden Sie Informationen zur Überwachung von verteiltem Inhalt mithilfe der Configuration Manager-Konsole."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 402c06ed92bbfe509206d3e7800e41e90c5d3a38

---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>Überwachen von mit System Center Configuration Manager verteilten Inhalten

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit der System Center Configuration Manager-Konsole können Sie folgende verteilten Inhalte überwachen:  

-   Den Status aller Pakettypen im Zusammenhang mit den zugeordneten Verteilungspunkten  

-   Den Inhaltsprüfungsstatus des Paketinhalts  

-   Den Status von Inhalt, der einer bestimmten Verteilungspunktgruppe zugeordnet ist  

-   Den Zustand von Inhalt, der einem Verteilungspunkt zugeordnet ist  

-   Den Status optionaler Funktionen jedes Verteilungspunkts (Inhaltsprüfung, PXE und Multicast)  

> [!NOTE]  
>  Von Configuration Manager wird nur der Inhalt auf einem Verteilungspunkt überwacht, der sich in der Inhaltsbibliothek befindet. Inhalt, der auf dem Verteilungspunkt in Paketfreigaben oder benutzerdefinierten Freigaben gespeichert ist, wird nicht überwacht.  

##  <a name="a-namebkmkcontentstatusa-content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Überwachung des Inhaltsstatus  
 Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Inhaltsstatus** Informationen zu Inhaltspaketen. In der Configuration Manager-Konsole können Sie z.B. folgende Informationen überprüfen:  

-   Den Paketnamen  

-   Typ  

-   An wie viele Verteilungspunkte ein Paket gesendet wurde  

-   Die Kompatibilitätsrate  

-   Wann das Paket erstellt wurde  

-   Paketkennung  

-   Quellversion  

Außerdem finden Sie hier detaillierte Statusinformationen zu allen Paketen sowie den Verteilungsstatus eines Pakets, einschließlich:  

-   Fehleranzahl  

-   Ausstehende Verteilungen  

-   Anzahl der Installationen  

Sie können außerdem Verteilungen an einen Verteilungspunkt verwalten, die noch in Bearbeitung sind bzw. aufgrund von Fehlern nicht erfolgreich ausgeführt werden konnten:  

-   Die zutreffende Option zum Abbrechen oder erneuten Verteilen des Inhalts ist verfügbar, wenn Sie im Fensterbereich **Bestandsdetails** auf einer der Registerkarten **In Bearbeitung** oder **Fehler** des Knotens **Inhaltsstatus** die Statusmeldung zu einem Verteilungsauftrag an einen Verteilungspunkt anzeigen.  

-   Außerdem werden beim Einsehen der Auftragsdetails folgende Informationen angezeigt: auf der Registerkarte **In Bearbeitung** der Prozentsatz, zu dem der Auftrag abgeschlossen ist; auf der Registerkarte **Fehler** die Anzahl der noch ausstehenden Wiederholungen für einen Auftrag sowie das Intervall bis zur nächten Wiederholung.  

Beim Abbrechen einer Bereitstellung, die noch nicht abgeschlossen ist, wird der Verteilungsauftrag zur Übertragung des betreffenden Inhalts beendet:  

-   Der Status der Bereitstellung wird dann aktualisiert, um anzuzeigen, dass die Verteilung fehlgeschlagen ist oder von einem Benutzer abgebrochen wurde.  

-   Dieser neue Status wird auf der Registerkarte **Fehler** angezeigt.  

> [!TIP]  
>  Wenn eine Bereitstellung fast abgeschlossen ist, kann es sein, dass ein Befehl zum Abbruch der Verteilung nicht rechtzeitig vor Ende der Verteilung an den Verteilungspunkt verarbeitet werden kann. In diesem Fall wird der Abbruch der Bereitstellung ignoriert, und der Status der Bereitstellung wird als erfolgreich angezeigt.  

> [!NOTE]  
>  Zwar können Sie die Option zum Abbrechen einer Verteilung an einen Verteilungspunkt auf einem Standortserver auswählen, aber diese Auswahl ist unwirksam. Dies liegt daran, dass der Standortserver und der Verteilungspunkt auf einem Standortserver den gleichen Single Instance Content Store verwenden und es keinen Verteilungsauftrag gibt, der abgebrochen werden könnte.  

Beim erneuten Verteilen von Inhalt an einen Verteilungspunkt, bei dessen Übertragung zuvor ein Fehler auftrat, wird die erneute Bereitstellung des Inhalts an den Verteilungspunkt von Configuration Manager sofort gestartet, und der Status der Bereitstellung wird entsprechend aktualisiert, um den laufenden Stand der betreffenden erneuten Bereitstellung widerzuspiegeln.  

Gehen Sie wie folgt vor, um den Inhaltsstatus anzuzeigen und Verteilungen zu verwalten, die noch in Bearbeitung sind oder aufgrund von Fehlern nicht abgeschlossen werden konnten.  

#### <a name="to-monitor-content-status"></a>So überwachen Sie den Inhaltsstatus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Inhaltsstatus**. Die Pakete werden angezeigt.  

3.  Wählen Sie das Paket aus, für das Sie detaillierte Statusinformationen anzeigen möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** auf **Status anzeigen**. Detaillierte Statusinformationen zum Paket werden angezeigt.  

#### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>So brechen Sie eine Verteilung ab, die noch in Bearbeitung ist  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Inhaltsstatus**. Die Pakete werden angezeigt.  

3.  Wählen Sie das Paket aus, das Sie verwalten wollen, und klicken Sie im Detailbereich auf **Status anzeigen**.  

4.  Klicken Sie im Fensterbereich **Bestandsdetails** auf der Registerkarte **In Bearbeitung** mit der rechten Maustaste auf den Eintrag der Verteilung, die Sie abbrechen möchten, und wählen Sie **Abbrechen**aus.  

5.  Klicken Sie auf **Ja** , um den Vorgang zu bestätigen und den Verteilungsauftrag an den betreffenden Verteilungspunkt abzubrechen.  

#### <a name="to-redistribute-content-that-failed-to-distribute"></a>So verteilen Sie Inhalt erneut, dessen Verteilung aufgrund von Fehlern nicht abgeschlossen werden konnte  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Inhaltsstatus**. Die Pakete werden angezeigt.  

3.  Wählen Sie das Paket aus, das Sie verwalten wollen, und klicken Sie im Detailbereich auf **Status anzeigen**.  

4.  Klicken Sie im Fensterbereich **Bestandsdetails** auf der Registerkarte **Fehler** mit der rechten Maustaste auf den Eintrag der Verteilung, die Sie erneut verteilen möchten, und wählen Sie **Neu verteilen**aus.  

5.  Klicken Sie auf **Ja** , um den Vorgang zu bestätigen und den neuen Verteilungsvorgang an den betreffenden Verteilungspunkt zu starten.  

## <a name="distribution-point-group-status"></a>Status von Verteilungspunktgruppen  
Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Status der Verteilungspunktgruppe** Informationen zu Verteilungspunktgruppen. Sie können z. B. folgende Informationen überprüfen:  

-   Namen von Verteilungspunktgruppen  

-   Beschreibung  

-   Wie viele Verteilungspunkte zur Verteilungspunktgruppe gehören  

-   Wie viele Pakete der Gruppe zugewiesen wurden  

-   Status der Verteilungspunktgruppe  

-   Kompatibilitätsrate  

Außerdem werden folgende detaillierte Statusinformationen angezeigt:  

-   Fehler für die Verteilungspunktgruppe  

-   Wie viele Verteilungen aktuell in Bearbeitung sind  

-   Wie viele erfolgreich verteilt wurde  

#### <a name="to-monitor-distribution-point-group-status"></a>So überwachen Sie den Status einer Verteilungspunktgruppe  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Status der Verteilungspunktgruppe**. Die Verteilungspunktgruppen werden angezeigt.  

3.  Wählen Sie die Verteilungspunktgruppe aus, für die detaillierte Statusinformationen angezeigt werden sollen.  

4.  Klicken Sie auf der Registerkarte **Startseite** auf **Status anzeigen**. Detaillierte Statusinformationen zur Verteilungspunktgruppe werden angezeigt.  

## <a name="distribution-point-configuration-status"></a>Status der Verteilungspunktkonfiguration  
 Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Status der Verteilungspunktkonfiguration** Informationen zum Verteilungspunkt. Sie können überprüfen, welche Attribute für den Verteilungspunkt aktiviert sind, wie z. B. PXE, Multicast und Inhaltsprüfung, und den Verteilungsstatus des Verteilungspunkts anzeigen. Außerdem können Sie detaillierte Statusinformationen zum Verteilungspunkt anzeigen.  

> [!WARNING]  
>  Der Status der Verteilungspunktkonfiguration bezieht sich auf die letzten 24 Stunden. Wenn der Verteilungspunkt nach einem Fehler wiederhergestellt wird, wird der Fehlerstatus möglicherweise bis zu 24 Stunden nach der Wiederherstellung des Verteilungspunkts angezeigt.  

Gehen Sie wie folgt vor, um den Status einer Verteilungspunktkonfiguration anzuzeigen.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>So überwachen Sie den Status einer Verteilungspunktkonfiguration  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Status der Verteilungspunktkonfiguration**. Die Verteilungspunkte werden angezeigt.  

3.  Wählen Sie den Verteilungspunkt aus, für den Statusinformationen angezeigt werden sollen.  

4.  Klicken Sie im Ergebnisbereich auf die Registerkarte **Details** . Statusinformationen zum Verteilungspunkt werden angezeigt.  



<!--HONumber=Nov16_HO1-->


