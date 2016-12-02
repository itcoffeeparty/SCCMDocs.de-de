---
title: "Verwaltung der Netzwerkbandbreite für Inhalt | System Center Configuration Manager"
description: "Konfigurieren Sie Zeitplanung, Bandbreiteneinschränkung und vorab bereitgestellten Inhalt für System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 92a08908f284abb02ce8000122b0839c474616d7


---

##  <a name="a-namebkmkplanningforthrottlingascheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a>Zeitplanung und Bandbreiteneinschränkung  
 Um Ihnen die Verwaltung der Netzwerkbandbreite zu erleichtern, die für den Inhaltsverwaltungsvorgang verwendet wird, können Sie die integrierten Configuration Manager-Steuerelemente für Zeitplanung und Einschränkung oder vorab bereitgestellten Inhalt verwenden.  

 Wenn Sie ein Paket erstellen, den Quellpfad für den Inhalt ändern oder Inhalt am Verteilungspunkt aktualisieren, werden die Dateien aus dem Quellpfad auf die Inhaltsbibliothek auf dem Standortserver kopiert. Dann wird der Inhalt aus der Inhaltsbibliothek auf dem Standortserver in die Inhaltsbibliothek an den Verteilungspunkten kopiert. Wenn ein Update bei Inhaltsquelldateien ausgeführt wird und die Quelldateien bereits verteilt wurden, werden von Configuration Manager nur die Dateien abgerufen und an den Verteilungspunkt gesendet, die neu sind oder bei denen das Update ausgeführt wurde. Die Steuerung der Zeitplanung und Einschränkung kann für die Kommunikation zwischen Standorten sowie zwischen Standortserver und Remoteverteilungspunkt konfiguriert werden. Wenn die Netzwerkbandbreite zwischen Standortserver und Remoteverteilungspunkt begrenzt ist, obwohl Sie die Einstellungen für Zeitplanung und Einschränkung konfiguriert haben, können Sie eine Vorabbereitstellung des Inhalts am Verteilungspunkt erwägen.  

 Sie können in Configuration Manager einen Zeitplan konfigurieren und spezifische Einschränkungseinstellungen an Remoteverteilungspunkten festlegen, von denen bestimmt wird, wann und wie die Inhaltsverteilung ausgeführt wird. Es sind für jeden Remoteverteilungspunkt andere Konfigurationen möglich, mithilfe derer Sie mit Netzwerkbandbreiteneinschränkungen zwischen Standortserver und Remoteverteilungspunkt umgehen können. Die Steuerelemente für die Zeitplanung und die Einschränkung am Remoteverteilungspunkt sind mit den Einstellungen für eine Standardabsenderadresse vergleichbar, allerdings werden die Einstellungen in diesem Fall von der neuen Komponente „Paketübertragungs-Manager“ verwendet. Vom Paketübertragungs-Manager wird Inhalt von einem Standortserver als primärem oder sekundärem Standort an einen Verteilungspunkt verteilt, der auf einem Standortsystem installiert ist. Bei einem Verteilungspunkt, der sich nicht auf einem Standortserver befindet, werden die Einschränkungseinstellungen auf der Registerkarte **Begrenzung der Datenübertragungsrate** konfiguriert, und die Zeitplaneinstellungen werden auf der Registerkarte **Zeitplan** konfiguriert. Die Zeiteinstellungen basieren auf der Zeitzone am sendenden Standort, nicht auf der am Verteilungspunkt.  

> [!WARNING]  
>  Die Registerkarten **Begrenzung der Datenübertragungsrate** und **Zeitplan** werden nur in den Eigenschaften von Verteilungspunkten, die nicht auf einem Standortserver installiert sind, angezeigt.  

Weitere Informationen zum Konfigurieren von Zeitplanungs- und Einschränkungseinstellungen für einen Remoteverteilungspunkt finden Sie unter [Install and configure distribution points for System Center Configuration Manager (Installieren und Konfigurieren von Verteilungspunkten in System Center Configuration Manager)](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

##  <a name="a-namebkmkprestagingcontentaprestaged-content"></a><a name="BKMK_PrestagingContent"></a>Vorab bereitgestellter Inhalt  
 Sie können Inhalt vorab bereitstellen, um der Inhaltsbibliothek auf einem Standortserver oder Verteilungspunkt vor der Verteilung des Inhalts Inhaltsdateien hinzuzufügen.  

-   Da die Inhaltsdateien sich bereits in der Inhaltsbibliothek befinden, werden sie bei der Verteilung des Inhalts nicht über das Netzwerk übertragen.  

-   Sie können Inhaltsdateien für Anwendungen und Pakete vorab bereitstellen.  

Wählen Sie in der Configuration Manager-Konsole den Inhalt aus, den Sie vorab bereitstellen möchten, und erstellen Sie anschließend mit dem **Assistenten zum Erstellen von vorab bereitgestellten Inhaltsdateien** eine komprimierte, vorab bereitgestellte Inhaltsdatei, die die Dateien und die zugeordneten Metadaten für den Inhalt enthält. Anschließend können Sie den Inhalt zur Bereitstellung auf einem Standortserver oder Verteilungspunkt manuell importieren.  

-   Wenn Sie die vorab bereitgestellte Inhaltsdatei in einen Standortserver importieren, wird sie der Inhaltsbibliothek auf dem Standortserver hinzugefügt und dann in der Datenbank des Standortservers registriert.  

-   Wenn Sie die vorab bereitgestellte Inhaltsdatei in einen Verteilungspunkt importieren, wird sie der Inhaltsbibliothek des Verteilungspunkts hinzugefügt, und an den Standortserver wird eine Statusmeldung über die Verfügbarkeit des Inhalts am Verteilungspunkt gesendet.  

Optional können Sie den Verteilungspunkt als **vorab bereitgestellt** konfigurieren, um die Inhaltsverteilung einfacher verwalten zu können. Anschließend können Sie beim Verteilen von Inhalt zwischen folgenden Möglichkeiten auswählen:  

-   Inhalt wird vorab am Verteilungspunkt bereitgestellt  

-   Der Anfangsinhalt des Pakets wird vorab bereitgestellt, Inhaltsaktualisierungen erfolgen mithilfe des regulären Inhaltsverteilungsvorgangs  

-   Für Inhalt des Pakets wird stets der reguläre Inhaltsverteilungsvorgang verwendet  

###  <a name="a-namebkmkdeterminetoprestagecontentadetermine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>Bestimmen, ob Inhalt vorab bereitgestellt werden soll  
 Erwägen Sie, in den folgenden Szenarien Inhalte für Anwendungen und Pakete vorab bereitzustellen:  

-   **Begrenzte Netzwerkbandbreite zwischen Standortserver und Verteilungspunkt**: Wenn Sie Probleme beim Verteilen von Inhalt über das Netzwerk an einen Remoteverteilungspunkt auch mit Zeitplanung und Einschränkung nicht lösen können, erwägen Sie eine Vorabbereitstellung des Inhalts am Verteilungspunkt. Bei jedem Verteilungspunkt können Sie in den Verteilungspunkteigenschaften die Einstellung **Diesen Verteilungspunkt für vorab bereitgestellten Inhalt aktivieren** konfigurieren. Wenn Sie diese Option aktivieren, wird der Verteilungspunkt als vorab bereitgestellter Verteilungspunkt identifiziert, und Sie können auswählen, wie der Inhalt pro Paket verwaltet werden soll.  

     Die folgenden Einstellungen sind in den Eigenschaften von Anwendungen, Paketen, Treiberpaketen, Startabbildern, Installationsprogrammen für Betriebssysteme sowie Abbildern von Betriebssystemen verfügbar. Mithilfe dieser Einstellungen können Sie konfigurieren, wie die Inhaltsverteilung auf Remoteverteilungspunkten, die als vorab bereitgestellt identifiziert werden, verwaltet werden soll:  

    -   **Inhalt automatisch herunterladen, wenn Pakete Verteilungspunkten zugeordnet sind**: Verwenden Sie diese Option, wenn Sie kleinere Pakete haben, bei denen durch die Zeitplanungs- und Einschränkungseinstellungen eine ausreichende Kontrolle der Inhaltsverteilung gegeben ist.  

    -   **Nur Inhaltsänderungen auf den Verteilungspunkt herunterladen**: Verwenden Sie diese Option, wenn Sie ein erstes Paket haben, das möglicherweise groß ist, jedoch mit zukünftigen Updates für den Paketinhalt rechnen, die allgemein kleiner sind. Beispielsweise könnten Sie eine Anwendung wie Microsoft Office vorab bereitstellen, da die Größe des ersten Pakets mehr als 700 MB beträgt, sodass das Paket nicht über das Netzwerk gesendet werden kann. Die Inhaltsupdates bei diesem Paket könnten jedoch kleiner als 10 MB und damit über das Netzwerk verteilbar sein. Ein weiteres Beispiel wären Treiberpakete, bei denen das erste Paket groß ist, inkrementelle Treiberergänzungen zum Paket jedoch klein sind.  

    -   **Den Inhalt dieses Pakets manuell an den Verteilungspunkt kopieren**: Verwenden Sie diese Option, wenn Sie große Pakete mit Inhalt wie einem Betriebssystem haben, die sie niemals über das Netzwerk an den Verteilungspunkt verteilen möchten. Wenn Sie diese Option auswählen, müssen Sie den Inhalt am Verteilungspunkt vorab bereitstellen.  

    > [!WARNING]  
    >  Die genannten Optionen sind pro Paket gültig und können nur dann verwendet werden, wenn ein Verteilungspunkt als vorab bereitgestellt identifiziert wurde. Von Verteilungspunkten, die nicht als vorab bereitgestellt identifiziert wurden, werden diese Einstellungen ignoriert. In diesem Fall wird Inhalt vom Standortserver stets über das Netzwerk an diese Verteilungspunkte verteilt.  

-   **Wiederherstellen der Inhaltsbibliothek auf einem Standortserver**: Beim Ausfall eines Standortservers werden Informationen zu Paketen und Anwendungen, die in der Inhaltsbibliothek enthalten sind, im Rahmen des Wiederherstellungsvorgangs auf der Standortdatenbank wiederhergestellt. Die Dateien der Inhaltsbibliothek werden bei diesem Vorgang jedoch nicht wiederhergestellt. Wenn Sie nicht über eine Sicherung des Dateisystems verfügen, um die Inhaltsbibliothek wiederherzustellen, können Sie eine vorab bereitgestellte Inhaltsdatei mit den erforderlichen Paketen und Anwendungen von einem anderen Standort erstellen und diese vorab bereitgestellte Inhaltsdatei auf dem wiederhergestellten Standortserver extrahieren. Weitere Informationen zur Standortserversicherung und -wiederherstellung finden Sie unter [Backup and recovery for System Center Configuration Manager (Sicherung und Wiederherstellung für System Center Configuration Manager)](/sccm/protect/understand/backup-and-recovery).  



<!--HONumber=Nov16_HO1-->


