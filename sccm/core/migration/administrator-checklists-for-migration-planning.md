---
title: "Prüflisten für die Migration | System Center Configuration Manager"
description: "Verwenden Sie Administratorprüflisten zum Planen einer Strategie zur Migration zu System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f3912de04aa3e6196137a7034753013c35180d64


---
# <a name="administrator-checklists-for-migration-planning-in-system-center-configuration-manager"></a>Administratorchecklisten zur Migrationsplanung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie die folgenden Administratorprüflisten zum Planen einer Strategie zur Migration zu System Center Configuration Manager:  

-   [Administratorprüfliste zum Planen der Migration](#Checklist_Migraiton_Planning)  

-   [Administratorprüfliste für die Hierarchiemigration](#Checklist_Hierarchy_for_migration)  

-   [Administratorprüfliste für die Migration](#Checklisit_Migration)  

##  <a name="a-namechecklistmigraitonplanninga-administrator-checklist-for-migration-planning"></a><a name="Checklist_Migraiton_Planning"></a> Administratorprüfliste zum Planen der Migration  
 Verwenden Sie die folgende Checkliste für die Planungsschritte vor der Migration.  

-   **Bewerten Sie die aktuelle Umgebung:**  

     Identifizieren Sie bestehende Geschäftsanforderungen, die von der Quellhierarchie erfüllt werden, und entwickeln Sie Pläne, wie diese Anforderungen auch in der Zielhierarchie erfüllt werden können.  

-   **Sehen Sie sich die Funktionalität und Änderungen an, die in Ihrer aktuell verwendeten Configuration Manager-Version möglich sind, und nutzen Sie diese Informationen beim Entwerfen der Zielhierarchie:**  

    Weitere Informationen finden Sie unter [Fundamentals of System Center Configuration Manager](../../core/understand/fundamentals.md) und [What's new in System Center Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).  


-   **Bestimmen Sie das Modell der administrativen Sicherheit, das für die rollenbasierte Verwaltung verwendet werden soll.**  

    Weitere Informationen finden Sie unter [Grundlagen der rollenbasierten Verwaltung für System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   **Bewerten Sie Ihre Netzwerk- und Active Directory-Topologie:**  

    Überprüfen Sie Ihre bestehende Domänenstruktur und Netzwerktopologie. Beachten Sie, inwiefern Ihr Hierarchieentwurf dadurch beeinflusst wird.  

-   **Stellen Sie den Entwurf Ihrer Zielhierarchie fertig:**  

    Entscheiden Sie die Platzierung von zentralem Verwaltungsstandort, primären Standorten und sekundären Standorten sowie die Inhaltsverteilungsoptionen.  

-   **Ordnen Sie die Hierarchie den Computern zu, die für die Standorte und Standortserver in der Zielhierarchie verwendet werden sollen:**  

    Identifizieren Sie die Computer, die von Standorten und Standortsystemservern in der Zielhierarchie verwendet werden sollen, und vergewissern Sie sich, dass diese über entsprechende Kapazitäten für aktuelle und zukünftige Betriebsanforderungen verfügen.  

-   **Planen Sie Ihre Objektmigrationsstrategie:**  

    Planen Sie den Einsatz der verfügbaren Migrationsaufträge zum Migrieren unterschiedlicher Objekte, z. B. Standortgrenzen, Sammlungen, Ankündigungen und Bereitstellungen. Weitere Informationen finden Sie unter [Types of Migration Jobs](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration) in [Planning a migration job strategy in System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md).  

    Von Configuration Manager werden nur Objekte migriert, die Sie ausgewählt haben. Alle Objekte, die nicht migriert werden und in der Zielhierarchie erforderlich sind, müssen in der Zielhierarchie neu erstellt werden.  

    Objekte, die migriert werden können, werden beim Konfigurieren von Migrationsaufträgen angezeigt.  

-   **Planen Sie Ihre Clientmigrationsstrategie:**  

    Planen Sie die Migration von Clients anhand eines kontrollierten Ansatzes, mit dem beim Migrieren von Clients zur Zielhierarchie die Netzwerkbandbreite und Serververarbeitung begrenzt wird. Weitere Informationen zum Planen einer Strategie für die Clientmigration finden Sie unter [Planning a client migration strategy in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Planen Sie Inventur- und Kompatibilitätsdaten:**  

    Von Configuration Manager wird keine Migration von Hardwareinventurdaten, Softwareinventurdaten oder Kompatibilitätsdaten zur Verwaltung gewünschter Konfigurationen für Softwareupdates oder Clients unterstützt.  

    Stattdessen übermittelt der Client diese Informationen an seinen zugewiesenen Standort, nachdem er zu seinem neuen Standort in der Zielhierarchie migriert wurde und Richtlinien für diese Konfigurationen erhalten hat. Bei dieser Aktion wird die Datenbank des Zielstandorts mit aktuellen Inventur- und Kompatibilitätsdaten gefüllt.  

-   **Planen Sie den Abschluss der Migration von der Quellhierarchie:**  

    Entscheiden Sie, wann Objekte und Clients migriert werden. Nach Abschluss der Migration können Sie die Außerbetriebnahme der Standortserver in der Quellhierarchie planen.  

##  <a name="a-namechecklisthierarchyformigrationa-administrator-checklist-for-hierarchy-migration"></a><a name="Checklist_Hierarchy_for_migration"></a> Administratorprüfliste für die Hierarchiemigration  
Verwenden Sie die folgende Checkliste, um eine Zielhierarchie zu planen, bevor Sie mit der Migration beginnen.  

-   **Identifizieren Sie die Computer, die in der Zielhierarchie verwendet werden sollen:**  

    Configuration Manager unterstützt kein direktes Upgrade der Configuration Manager 2007-Infrastruktur. Stattdessen verwenden Sie die Migration zum Verschieben von Daten von Configuration Manager 2007 zu System Center Configuration Manager. Dies erfordert, dass Sie eine parallele Bereitstellung verwenden und System Center Configuration Manager auf neuen Computern installieren.  

    Außerdem müssen Sie beim Migrieren aus einer anderen System Center Configuration Manager-Hierarchie eine neue Zielhierarchie installieren, bei der es sich um eine parallele Bereitstellung zur Quellhierarchie handelt.  

-   **Erstellen Sie die Zielhierarchie:**  

    Installieren und konfigurieren Sie zur Vorbereitung der Migration eine System Center Configuration Manager-Zielhierarchie mit einem primären Standort. Beispiel:  

    -   Installieren eines Standorts der zentralen Verwaltung und mindestens eines untergeordneten primären Standorts  

    -   Installieren Sie einen eigenständigen primären Standort, wenn Sie keinen Standort der zentralen Verwaltung verwenden möchten.  

-   **Konfigurieren Sie einen Softwareupdatepunkt in der Zielhierarchie, und synchronisieren Sie Softwareupdates, wenn Sie auf Softwareupdates bezogene Informationen migrieren möchten:**  

    Sie müssen Softwareupdates in der Zielhierarchie konfigurieren und synchronisieren, bevor Sie Softwareupdateinformationen aus der Quellhierarchie migrieren können.  


-   **Installieren und konfigurieren Sie zusätzliche Standortsystemrollen in der Zielhierarchie:**  

    Konfigurieren Sie zusätzliche Standortsystemrollen und Standortsysteme, die Sie benötigen werden.  

-   **Überprüfen Sie den ordnungsgemäßen Betrieb der Zielhierarchie:**  

    Überprüfen Sie Folgendes:  

    -   Vergewissern Sie sich, dass die Datenbankreplikation zwischen Standorten funktioniert, wenn die Zielhierarchie mehrere Standorte enthält. Die Datenbankreplikation ist nicht auf eigenständige primäre Standorte anwendbar.  

    -   Stellen Sie sicher, dass alle installierten Standortsystemrollen funktionsfähig sind.  

    -   Stellen Sie sicher, dass Configuration Manager-Clients, die Sie unter der Zielhierarchie installieren, mit dem jeweils zugewiesenen Standort kommunizieren können.  


##  <a name="a-namechecklisitmigrationa-administrator-checklist-for-migration"></a><a name="Checklisit_Migration"></a> Administratorprüfliste für die Migration  
Verwenden Sie die folgende Checkliste für die Datenmigration von der Quellhierarchie zur Zielhierarchie.  

-   **Aktivieren Sie die Migration in der Zielhierarchie:**  

    Konfigurieren Sie eine Quellhierarchie, indem Sie den Standort der obersten Ebene der Quellhierarchie angeben. Weitere Informationen zum Angeben des Quellstandorts finden Sie unter [Planning a source hierarchy strategy in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).  

-   **Wählen Sie weitere Standorte in der Quellhierarchie aus, und konfigurieren Sie diese, wenn in der Quellhierarchie Configuration Manager 2007 SP2 ausgeführt wird:**  

    Für jeden zusätzlichen Standort in der Configuration Manager 2007 SP2-Quellhierarchie, von dem Sie Daten sammeln möchten, müssen Sie Anmeldeinformationen für die Datensammlung konfigurieren. Wenn Sie die einzelnen Quellstandorte konfigurieren, beginnt der Datensammlungsvorgang sofort und wird während der gesamten Migrationsphase fortgesetzt, bis Sie das Sammeln von Daten für den jeweiligen Standort beenden. Die Datensammlung ermöglicht das Migrieren von Objekten aus der Quellhierarchie, die seit der letzten Datensammlung neu dazugekommen sind oder aktualisiert wurden.  

    > [!NOTE]  
    >  Wenn von der Quellhierarchie System Center 2012 Configuration Manager oder höher ausgeführt wird, müssen Sie keine zusätzlichen Quellstandorte konfigurieren.  

-   **Konfigurieren Sie die Verteilungspunktfreigabe:**  

    Sie können Verteilungspunkte zwischen den beiden Hierarchien freigeben, damit Clients in der Zielhierarchie auf Inhalte migrierter Objekte zugreifen können. So bleiben dieselben Inhalte für Clients in beiden Hierarchien verfügbar und können beibehalten werden, bis die Datensammlung beendet und die Migration abgeschlossen ist.  

    Informationen zu freigegebenen Verteilungspunkten finden Sie im Abschnitt *Share Distribution Points Between Source and Destination Hierarchies* des Themas [Planning a content deployment migration strategy in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md) .  

-   **Erstellen und führen Sie Migrationsaufträge aus, um die Objekte zu migrieren, die den Clients in der Quellhierarchie zugeordnet sind:**  

    Erstellen Sie Migrationsaufträge zum Migrieren von Objekten zwischen Hierarchien. Die erforderlichen Konfigurationen für die einzelnen Migrationsaufträge können in Abhängigkeit davon variieren, welche Daten im Rahmen des Auftrags migriert werden.  

    Wenn Sie beispielsweise Inhalte migrieren, müssen Sie unabhängig vom verwendeten Migrationsauftrag einen Standort in der Zielhierarchie für die Verwaltung dieser Inhalte zuweisen. Der zugewiesene Standort greift auf den ursprünglichen Quelldateispeicherort für den Inhalt zu und ist für das Verteilen des Inhalts auf die Verteilungspunkte in der Zielhierarchie verantwortlich.  

    Weitere Informationen finden Sie im Abschnitt [Create and Edit Migration Jobs for System Center Configuration Manager](../../core/migration/operations-for-migration.md#create_edit_migration_jobs) des Themas [Operations for migrating to System Center Configuration Manager](../../core/migration/operations-for-migration.md) .  

-   **Migrieren Sie Clients in die Zielhierarchie:**  

    Der Prozess für die Migration von Clients richtet sich nach Ihrem Migrationsszenario:  

    -   Beim Migrieren von Clients, deren Clientversion nicht der Version der Zielhierarchie entspricht, muss für die Clientsoftware ein Upgrade ausgeführt werden. Das Upgrade erfordert die Entfernung des aktuellen Configuration Manager-Clients und die anschließende Installation der neuen Clientversion, die der Version des Zielstandorts entspricht.  

    -   Beim Migrieren von Clients, deren Clientversion der Version der Zielhierarchie entspricht, wird für den Client kein Upgrade und keine Neuinstallation ausgeführt. Stattdessen wird der Client einem primären Standort in der Zielhierarchie neu zugewiesen.  

    Wenn Sie einen Client zur Zielhierarchie migrieren, wird der Client seinen Daten zugeordnet, die Sie bereits vorher zur Zielhierarchie migriert haben.  

    Weitere Informationen finden Sie unter [Planning a client migration strategy in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Führen Sie eine Aktualisierung oder Neuzuweisung freigegebener Verteilungspunkte durch:**  

    Wenn Sie in Ihrer Quellhierarchie keine Clients mehr unterstützen müssen, können Sie freigegebene Verteilungspunkte von einem Configuration Manager 2007-Quellstandort aktualisieren oder solche von einem System Center 2012 Configuration Manager- oder System Center Configuration Manager-Quellstandort neu zuweisen. Beim Aktualisieren oder erneuten Zuweisen eines Verteilungspunkts wird die Standortsystemrolle an einen primären Standort in der Zielhierarchie übertragen, und der Verteilungspunkt wird vom Quellstandort in der Quellhierarchie entfernt. Wenn Sie einen freigegebenen Verteilungspunkt aktualisieren oder neu zuweisen, verbleiben die Inhalte auf dem Verteilungspunktcomputer, sodass Sie sie nicht an neuen Verteilungspunkten der Zielhierarchie erneut bereitstellen müssen.  

    Sie können auch ein Upgrade von einem Configuration Manager 2007-Verteilungspunkt durchführen, der sich auf einem sekundären Standortserver befindet. Hierbei wird der sekundäre Standort entfernt, sodass sich in der Zielhierarchie nur ein Verteilungspunkt ergibt.  

    Informationen zu freigegebenen Verteilungspunkten finden Sie im Abschnitt [Share Distribution Points Between Source and Destination Hierarchies](../../core/migration/planning-a-content-deployment-migration-strategy.md#about_shared_dps_in_migrations) des Themas [Planning a content deployment migration strategy in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md) .  

-   **Abschließen der Migration:**  

    Nachdem Sie die Daten und Clients aller Standorte der Quellhierarchie migriert und ein Upgrade der relevanten Verteilungspunkte durchgeführt haben, können Sie die Migration abschließen. Zum Abschließen der Migration beenden Sie das Sammeln von Daten für jeden Quellstandort in der Quellhierarchie. Dann können nicht benötigte Migrationsinformationen entfernt werden, und die Infrastruktur der Quellhierarchie kann außer Betrieb genommen werden. Weitere Informationen finden Sie unter [Planning to complete migration in System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md).  



<!--HONumber=Nov16_HO1-->


