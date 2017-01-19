---
title: "Checkliste für 1606 | Microsoft-Dokumentation"
description: "Erhalten Sie mehr über Aktionen, die Sie durchführen müssen, bevor Sie eine Aktualisierung von System Center Configuration Manager Version 1511 oder 1602 auf Version 1606 ausführen."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: ba087244ad52087f32acbe413b1e56c7478e4db6

---
# <a name="checklist-for-installing-update-1606-for-system-center-configuration-manager"></a>Checkliste für die Installation von Update 1606 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Version 1606 für System Center Configuration Manager (Current Branch) ist ein Update, das Sie für das Aktualisieren von Version 1511 oder 1602 verwenden können.

Lesen Sie vor der Installation von Version 1606 als Update die folgenden Informationen und die Checkliste mit Aktionen, die vor Beginn des Updates durchgeführt werden müssen.

Informationen zu Basisversionen finden Sie im Abschnitt [Baseline and update versions](../../../core/servers/manage/updates.md#bkmk_Baselines) (Basis- und Updateversionen) unter [Updates for System Center Configuration Manager (Updates für System Center Configuration Manager)](../../../core/servers/manage/updates.md).

 ## <a name="about-installing-update-1606"></a>Informationen zur Installation des Updates 1606

Als *Update* kann 1606 nur am Standort der obersten Ebene Ihrer Hierarchie installiert werden. Das bedeutet, dass Sie die Installation vom Standort der zentralen Verwaltung (falls vorhanden) oder vom eigenständigen primären Standort aus starten.  

-   An untergeordneten primären Standorten wird das Update automatisch installiert, sobald die Installation des Updates am Standort der zentralen Verwaltung abgeschlossen ist. Mithilfe von Dienstfenstern können Sie steuern, wann Updates an einem Standort installiert werden. Vor Version 1606 wurden Dienstfenster als Wartungsfenster bezeichnet. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](../../../core/servers/manage/install-in-console-updates.md#bkmk_ServiceWindow).  

-   Sie müssen sekundäre Standorte von der Configuration Manager-Konsole aus manuell aktualisieren, nachdem die Updateinstallation am primären übergeordneten Standort abgeschlossen wurde. Die automatische Aktualisierung sekundärer Standortserver wird nicht unterstützt.  

Bei der Installation des Updates auf dem Standortserver werden Standortsystemrollen, die auf dem Standortserver und auf Remotecomputern installiert sind, automatisch aktualisiert. Stellen Sie daher vor der Installation des Updates sicher, dass jeder Standortsystemserver die neuen Voraussetzungen für den Betrieb mit der neuen Updateversion erfüllt.  

 Bei der ersten Verwendung einer Configuration Manager-Konsole nach Abschluss des Updates werden Sie aufgefordert, die Konsole zu aktualisieren.  Dazu müssen Sie das Configuration Manager-Setup auf dem Computer ausführen, der die Konsole hostet, und die Option zum Aktualisieren der Konsole auswählen. Es wird empfohlen, die Installation des Updates auf der Konsole unverzüglich durchzuführen.

 **Bekannte Probleme dieses Updates**   
  Die folgenden Probleme betreffen Sie, wenn Sie den Installationsstatus des Updatepakets anzeigen:
  - Beim Aktualisieren von Version 1602 auf 1606 zeigt der Schritt **Updatepaket-Nutzlast extrahieren** den Status **Nicht gestartet** an, auch wenn der Download abgeschlossen ist.
  - Beim Aktualisieren von Version 1511 auf 1606 zeigen einige Schritte den Status **Abgeschlossen**, jedoch keinen Wert für **Zeitpunkt der letzten Aktualisierung** an.


## <a name="checklist"></a>Prüfliste  

 **Stellen Sie sicher, dass an allen Standorten eine unterstützte Version von System Center Configuration Manager ausgeführt wird:** Auf jedem Standortserver in der Hierarchie muss die gleiche Version von Configuration Manager ausgeführt werden (entweder 1511 oder 1602), bevor Sie die Installation des Updates 1606 starten.

 **Überprüfen Sie die installierten .NET-Versionen auf den Standortsystemservern:** Bei der Installation von Update 1606 an einem Standort installiert Configuration Manager automatisch .NET Framework 4.5.2 auf jedem Computer, auf dem eine der folgenden Standortsystemrollen gehostet wird, sofern .NET Framework 4.5 oder höher nicht bereits installiert ist:  

-   Anmeldungsproxypunkt  

-   Anmeldungspunkt  

-   Verwaltungspunkt  

-   Dienstverbindungspunkt  

Diese Installation kann den Standortsystemserver in den Zustand „Ausstehender Neustart“ versetzen und Fehler an die Configuration Manager-Komponentenstatusanzeige melden. Darüber hinaus treten bei .NET-Anwendungen auf dem Server gelegentlich Fehler auf, bis der Server neu gestartet wird.  

 Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Standort- und Standortsystemanforderungen an System Center Configuration Manager).  

 **Prüfen Sie den Standort- und Hierarchiestatus, und stellen Sie sicher, dass keine ungelösten Probleme vorliegen:** Bevor Sie das Update für einen Standort durchführen, sollten Sie alle Betriebsprobleme beheben, die den Standortserver, den Standortdatenbankserver und die auf Remotecomputern installierten Standortsystemrollen betreffen. Betriebsprobleme können die Ursache für Fehler beim Update von Standorten sein.  
 Weitere Informationen finden Sie unter [Verwenden von Benachrichtigungen und des Statussystems für System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Überprüfen Sie die Datei- und Datenreplikation zwischen Standorten:**  Stellen Sie sicher, dass die Datei- und Datenreplikation zwischen Standorten betriebsbereit und aktuell ist. Verzögerungen oder Rückstände können ein reibungsloses und erfolgreiches Update verhindern.    
Für die Datenbankreplikation können Sie die Replikationslinkanalyse verwenden, um Probleme vor Beginn des Updates zu lösen.    
 Weitere Informationen finden Sie unter   
[Informationen zur Replikationslinkanalyse](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) in dem Thema [Überwachen der Hierarchie- und Replikationsinfrastruktur in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

 **Installieren Sie alle anwendbaren wichtigen Updates für Betriebssysteme auf Computern, auf denen der Standort gehostet wird, auf dem Standortdatenbankserver und auf Remote-Standortsystemrollen:** Installieren Sie vor der Installation eines Updates für Configuration Manager alle wichtigen Updates für jedes relevante Standortsystem. Wenn für ein von Ihnen installiertes Update ein Neustart erforderlich ist, starten Sie die jeweiligen Computer neu, bevor Sie mit dem Upgrade beginnen.  

 **Deaktivieren Sie Datenbankreplikate für Verwaltungspunkte an primären Standorten:** Configuration Manager kann einen primären Standort, an dem ein Datenbankreplikat für Verwaltungspunkte aktiviert ist, nicht erfolgreich aktualisieren. Deaktivieren Sie die Datenbankreplikation, bevor Sie folgende Schritte ausführen:  

-   Erstellen einer Sicherung der Standortdatenbank zum Testen des Datenbankupgrades  

-   Installieren Sie ein Update für Configuration Manager  

Weitere Informationen finden Sie unter   
[Datenbankreplikate für Verwaltungspunkte für System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)  

 **Legen Sie SQL Server Always On-Verfügbarkeitsgruppen auf manuelles Failover fest:**  
 Vor der Installation von Updates, z.B. Version 1606, stellen Sie sicher, dass die Verfügbarkeitsgruppe auf manuelles Failover festgelegt ist. Nachdem der Standort aktualisiert wurde, können Sie wieder auf automatisches Failover umstellen. Weitere Informationen finden Sie unter [SQL Server Always On for a highly available site database for System Center Configuration Manager (SQL Server Always On für eine hoch verfügbare Standortdatenbank für System Center Configuration Manager)](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

 **Konfigurieren Sie Softwareupdatepunkte mit NLBs neu:** Configuration Manager kann kein Update für Standorte durchführen, an denen Softwareupdatepunkte mithilfe eines Netzwerklastenausgleich-Clusters (Network Load Balancing, NLB) gehostet werden.  
Wenn Sie für Softwareupdatepunkte NLB-Cluster verwenden, entfernen Sie den NLB-Cluster mithilfe von PowerShell.    

 Weitere Informationen finden Sie unter [Planen von Softwareupdates in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

 **Deaktivieren Sie alle Standortwartungstasks an jedem Standort für die Dauer der Updateinstallation am jeweiligen Standort:** Deaktivieren Sie vor der Updateinstallation alle Standortwartungstasks, die möglicherweise während des Zeitraums ausgeführt werden, für den der Updatevorgang aktiv ist. Zu diesen Tasks gehören u. a. folgende:  

-   Standortserver sichern  

-   Veraltete Clientvorgänge löschen  

-   Veraltete Ermittlungsdaten löschen  

Wenn ein Standortdatenbank-Wartungstask während der Updateinstallation ausgeführt wird, kann bei der Updateinstallation ein Fehler auftreten. Bevor Sie einen Task deaktivieren, zeichnen Sie den Zeitplan des Tasks auf, sodass Sie die Konfiguration nach Abschluss des Updates wiederherstellen können.  
 Weitere Informationen finden Sie unter [Wartungstasks für System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) und [Referenz für Wartungstasks für System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 **Erstellen Sie eine Sicherung der Standortdatenbank am Standort der zentralen Verwaltung und an den primären Standorten:** Sichern Sie vor dem Update eines Standorts die Standortdatenbank, um sicherzustellen, dass Sie eine erfolgreiche Sicherung für die Notfallwiederherstellung besitzen.   
Weitere Informationen finden Sie unter [Backup and recovery for System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md)  


 **Testen Sie das Datenbankupgrade mit einer Kopie der letzten Sicherung der Standortdatenbank:** Bevor Sie ein Update für einen Standort der zentralen Verwaltung oder einen primären Standort von System Center Configuration Manager durchführen, sollten Sie den Datenbankupgradeprozess mit einer Kopie der letzten Sicherung der Standortdatenbank testen.  

-   Sie sollten den Standortdatenbank-Upgradeprozess testen, da die Standortdatenbank während der Aktualisierung eines Standorts geändert werden kann.  

-   Ein Testdatenbankupgrade ist zwar nicht erforderlich, doch können dadurch Probleme beim Upgrade ermittelt werden, bevor die Produktionsdatenbank betroffen ist.  

-   Wenn beim Upgrade einer Standortdatenbank Fehler auftreten, ist die Datenbank möglicherweise nicht mehr betriebsfähig, und es müsste eine Standortwiederherstellung erfolgen.  

-   Obwohl die Standortdatenbank von allen Standorten in einer Hierarchie gemeinsam genutzt wird, sollten Sie die Datenbank an jedem relevanten Standort testen, bevor Sie das Upgrade für diesen Standort durchführen.  

-   Wenn Sie an einem primären Standort Datenbankreplikate für Verwaltungspunkte verwenden, deaktivieren Sie die Replikation, bevor Sie die Sicherung der Standortdatenbank erstellen.  

Configuration Manager unterstützt weder die Sicherung sekundärer Standorte noch das Testupgrade einer sekundären Standortdatenbank.   
Das Testen des Datenbankupgrades für die Datenbank des Produktionsstandorts wird nicht unterstützt. Dadurch würde ein Update der Standortdatenbank durchgeführt, und Ihr Standort wäre möglicherweise nicht mehr betriebsfähig. Weitere Informationen finden Sie im Abschnitt [Test the site database upgrade](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_test) (Testen des Standortdatenbankupgrades) des Themas [Upgrade to System Center Configuration Manager](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) (Upgrade auf System Center Configuration Manager).  

 **Planen Sie Pilottests für Clients:** Bei der Installation eines Updates, das den Client aktualisiert, können Sie das neue Clientupdate in der Präproduktionsphase testen, bevor es bereitgestellt wird und Ihren gesamten aktiven Client upgradet.   
 Um diese Option vor der Installation des Updates zu nutzen, müssen Sie Ihren Standort für die Unterstützung automatischer Updates für die Präproduktionsphase konfigurieren. Weitere Informationen finden Sie unter [Aktualisieren von Clients in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) und   
[How to test client upgrades in a preproduction collection in System Center Configuration Manager (So testen Sie Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager)](../../../core/clients/manage/upgrade/test-client-upgrades.md)  

 **Planen Sie die Verwendung von Dienstfenstern**  
 **, um den Zeitpunkt der Updateinstallation auf den Standortservern zu steuern:** Mithilfe der Dienstfenster können Sie für einen primären Standortserver einen Zeitraum definieren, in dem Updates an diesem Standort installiert werden können.   
Damit können Sie steuern, wann das Update an Standorten in Ihrer Hierarchie installiert werden kann.
Vor Version 1606 wurden Dienstfenster als Wartungsfenster bezeichnet. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](../../../core/servers/manage/install-in-console-updates.md#bkmk_ServiceWindow).  

 **Führen Sie die Setup-Voraussetzungsprüfung aus:** Vor der Installation des Updates 1606 können Sie die Voraussetzungsprüfung unabhängig von der Updateinstallation ausführen. Beim Installieren des Updates am Standort wird die Voraussetzungsprüfung erneut ausgeführt.  
Weitere Informationen finden Sie unter **Schritt 3: Ausführen der Voraussetzungsprüfung vor der Installation eines Updates** im Thema [Updates für System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md).  

> [!IMPORTANT]  
>  Wenn die Voraussetzungsprüfung im Rahmen einer Updateinstallation oder unabhängig davon ausgeführt wird, werden vom Prozess einige Produktquelldateien aktualisiert, die für Standortwartungstasks verwendet werden. Wenn Sie daher nach Durchführung der Voraussetzungsprüfung, aber vor Installation des Updates 1606 einen Standortwartungstask durchführen müssen, führen Sie **Setupwfe.exe** (Configuration Manager-Setup) im Ordner „CD.Latest“ auf dem Standortserver aus.  

 **Aktualisieren Sie Standorte:** Sie können nun die Updateinstallation für Ihre Hierarchie starten.  
  Es wird empfohlen, die Installation des Updates für jeden Standort außerhalb der normalen Geschäftszeiten zu planen, wenn die Installation des Updates und die zugehörigen Aktionen zum Neuinstallieren von Standortkomponenten und Standortsystemrollen die geringsten Auswirkungen auf die Geschäftsvorgänge haben. Weitere Informationen finden Sie unter [Updates für System Center Configuration Manager](../../../core/servers/manage/updates.md).  



<!--HONumber=Dec16_HO3-->


