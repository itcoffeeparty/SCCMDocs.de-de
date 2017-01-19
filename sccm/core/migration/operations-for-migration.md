---
title: "Migrationsvorgänge | Microsoft-Dokumentation"
description: "Erstellen Sie Aufträge zum Migrieren von Daten und Clients zu System Center Configuration Manager, und führen Sie diese aus."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: 3b5fc05542125454e224df73344cb29cb5f502ef


---
# <a name="operations-for-migrating-to-system-center-configuration-manager"></a>Vorgänge der Migration zu System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei der Migration in System Center Configuration Manager können Sie nach der erfolgreichen Datensammlung von einem Quellstandort in einer unterstützten Quellhierarchie mit dem Migrieren von Daten und Clients beginnen. Verwenden Sie die Informationen in den folgenden Abschnitten zum Erstellen und Ausführen von Migrationsaufträgen, um Daten und Clients zu migrieren und den Migrationsprozess abzuschließen.  

-   [Erstellen und Bearbeiten von Migrationsaufträgen](#Create_Edit_migration_Jobs)  

-   [Ausführen von Migrationsaufträgen](#Run_Migration_Jobs)  

-   [Aktualisieren oder erneutes Zuweisen eines freigegebenen Verteilungspunkts](#BKMK_ProcUpgrdSS)  

-   [Überwachen der Migrationsaktivität im Arbeitsbereich „Migration“](#Monitor_MIgration)  

-   [Migrieren von Clients](#BKMK_MigrateClients)  

-   [Abschließen der Migration](#Complete_Migration)  

##  <a name="a-namecreateeditmigrationjobsa-create-and-edit-migration-jobs"></a><a name="Create_Edit_migration_Jobs"></a> Erstellen und Bearbeiten von Migrationsaufträgen  
 Gehen Sie wie folgt vor, um Datenmigrationsaufträge zu erstellen, die Ausschlussliste für sammlungsbasierte Migrationsaufträge zu bearbeiten, freigegebene Verteilungspunkte zu konfigurieren und Zeitpläne für Migrationsaufträge zu bearbeiten.  

> [!NOTE]  
>  Das folgende Verfahren zum Erstellen eines Migrationsauftrags, bei dem anhand von Sammlungen migriert wird, gilt nur für Quellhierarchien, für die eine unterstützte Version von Configuration Manager 2007 ausgeführt wird. Der sammlungsbasierte Migrationsauftragstyp ist nicht verfügbar, wenn Sie aus einer System Center 2012 Configuration Manager- oder der System Center Configuration Manager-Quellhierarchie migrieren.  

#### <a name="to-create-a-migration-job-to-migrate-by-collections"></a>So erstellen Sie einen Migrationsauftrag zum Migrieren nach Sammlungen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und klicken Sie dann auf **Migrationsaufträge**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Migrationsauftrag erstellen**.  

4.  Konfigurieren Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Migrationsaufträgen die folgenden Optionen, und klicken Sie dann auf **OK**:  

    -   Geben Sie einen Namen für den Migrationsauftrag an.  

    -   Wählen Sie in der Dropdownliste **Auftragstyp** die Option **Sammlungsmigration**aus.  

5.  Konfigurieren Sie auf der Seite **Sammlungen auswählen** die folgenden Optionen, und klicken Sie dann auf **Weiter**:  

    -   Wählen Sie die Sammlungen aus, die Sie migrieren möchten.  

    -   Wenn Sie nur die Sammlungen und nicht zusätzlich die diesen Sammlungen zugewiesenen Objekte migrieren möchten, deaktivieren Sie die Option **Objekte migrieren, die den angegebenen Sammlungen zugewiesen sind** . Wenn Sie diese Option deaktivieren, werden bei diesem Auftrag keine zugewiesenen Objekte migriert, und Sie können die Schritte 6 und 7 überspringen.  

6.  Deaktivieren Sie auf der Seite **Objekte auswählen** alle Objekttypen oder bestimmte verfügbare Objekte, die Sie nicht migrieren möchten. Standardmäßig werden alle zugeordneten Objekttypen und verfügbaren Objekte ausgewählt. Klicken Sie anschließend auf **Weiter**.  

7.  Weisen Sie auf der Seite **Inhaltsbesitz** den Besitz des Inhalts jedes aufgeführten Quellstandorts einem Standort in der Zielhierarchie zu, und klicken Sie dann auf **Weiter**.  

8.  Wählen Sie auf der Seite **Sicherheitsbereich** einen oder mehrere rollenbasierte Verwaltungssicherheitsbereiche aus, die den zu migrierenden Objekten dieses Migrationsauftrags zugewiesen werden sollen, und klicken Sie dann auf **Weiter**.  

9. Konfigurieren Sie auf der Seite **Sammlungsbegrenzung** eine Sammlung der Zielhierarchie zur Begrenzung des Bereichs jeder aufgeführten Sammlung, und klicken Sie dann auf **Weiter**. Wenn keine Sammlungen aufgeführt werden, klicken Sie auf **Weiter**.  

10. Weisen Sie auf der Seite **Ersetzung von Standortcodes** einen Standortcode aus der Zielhierarchie zu, um den Configuration Manager 2007-Standortcode für jede aufgeführte Sammlung zu ersetzen, und klicken Sie anschließend auf **Weiter**. Wenn keine Sammlungen aufgeführt werden, klicken Sie auf **Weiter**.  

11. Klicken Sie auf der Seite **Informationen überprüfen** auf **In Datei speichern** , um die angezeigten Informationen später ggf. erneut anzuzeigen. Klicken Sie zum Fortfahren auf **Weiter**.  

12. Konfigurieren Sie auf der Seite **Einstellungen** den Zeitpunkt der Ausführung des Migrationsauftrags und alle zusätzlichen Einstellungen, die Sie für diesen Migrationsauftrag benötigen, und klicken Sie dann auf **Weiter**.  

13. Bestätigen Sie die Einstellungen, und beenden Sie den Assistenten.  

#### <a name="to-create-a-migration-job-to-migrate-by-objects"></a>So erstellen Sie einen Migrationsauftrag zum Migrieren nach Objekten  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und klicken Sie dann auf **Migrationsaufträge**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Migrationsauftrag erstellen**.  

4.  Konfigurieren Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Migrationsaufträgen die folgenden Optionen, und klicken Sie dann auf **Weiter**:  

    -   Geben Sie einen Namen für den Migrationsauftrag an.  

    -   Wählen Sie in der Dropdownliste **Auftragstyp** die Option **Objektmigration**aus.  

5.  Wählen Sie auf der Seite **Objekte auswählen** die Objekttypen aus, die Sie migrieren möchten. Standardmäßig werden für jeden von Ihnen ausgewählten Objekttyp alle verfügbaren Objekte ausgewählt.  

6.  Weisen Sie auf der Seite **Inhaltsbesitz** den Besitz des Inhalts jedes aufgeführten Quellstandorts einem Standort in der Zielhierarchie zu, und klicken Sie dann auf **Weiter**. Wenn keine Quellstandorte aufgeführt werden, klicken Sie auf **Weiter**.  

7.  Wählen Sie auf der Seite **Sicherheitsbereich** einen oder mehrere rollenbasierte Verwaltungssicherheitsbereiche aus, die den Objekten dieses Migrationsauftrags zugewiesen werden sollen, und klicken Sie dann auf **Weiter**.  

8.  Klicken Sie auf der Seite **Informationen überprüfen** auf **In Datei speichern** , um die angezeigten Informationen später ggf. erneut anzuzeigen. Klicken Sie zum Fortfahren auf **Weiter**.  

9. Konfigurieren Sie auf der Seite **Einstellungen** den Zeitpunkt der Ausführung des Migrationsauftrags und alle zusätzlichen Einstellungen, die Sie für diesen Migrationsauftrag benötigen. Klicken Sie anschließend auf **Weiter**.  

10. Bestätigen Sie die Einstellungen, und beenden Sie den Assistenten.  

#### <a name="to-create-a-migration-job-to-migrate-changed-objects"></a>So erstellen Sie einen Migrationsauftrag zum Migrieren von geänderten Objekten  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und klicken Sie dann auf **Migrationsaufträge**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Migrationsauftrag erstellen**.  

4.  Konfigurieren Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Migrationsaufträgen die folgenden Optionen, und klicken Sie dann auf **Weiter**:  

    -   Geben Sie einen Namen für den Migrationsauftrag an.  

    -   Wählen Sie in der Dropdownliste **Auftragstyp** die Option **Nach der Migration geänderte Objekte**aus.  

5.  Wählen Sie auf der Seite **Objekte auswählen** die Objekttypen aus, die Sie migrieren möchten. Standardmäßig werden für jeden von Ihnen ausgewählten Objekttyp alle verfügbaren Objekte ausgewählt.  

6.  Weisen Sie auf der Seite **Inhaltsbesitz** den Besitz des Inhalts jedes aufgeführten Quellstandorts einem Standort in der Zielhierarchie zu, und klicken Sie dann auf **Weiter**. Wenn keine Quellstandorte aufgeführt werden, klicken Sie auf **Weiter**.  

7.  Wählen Sie auf der Seite **Sicherheitsbereich** einen oder mehrere rollenbasierte Verwaltungssicherheitsbereiche aus, die den Objekten dieses Migrationsauftrags zugewiesen werden sollen, und klicken Sie dann auf **Weiter**.  

8.  Klicken Sie auf der Seite **Informationen überprüfen** auf **In Datei speichern** , um die angezeigten Informationen später ggf. erneut anzuzeigen. Klicken Sie zum Fortfahren auf **Weiter**.  

9. Konfigurieren Sie auf der Seite **Einstellungen** den Zeitpunkt der Ausführung des Migrationsauftrags und alle zusätzlichen Einstellungen, die Sie für diesen Migrationsauftrag benötigen. Im Gegensatz zu anderen Migrationsauftragstypen müssen bei diesem Migrationsauftrag die zuvor migrierten Objekte in der System Center Configuration Manager-Datenbank überschrieben werden. Klicken Sie auf **Weiter**.  

10. Bestätigen Sie die Einstellungen, und beenden Sie dann den Assistenten.  

###  <a name="a-namebkmkmodifyexclusionlista-to-modify-the-exclusion-list-for-migration"></a><a name="BKMK_Modify_Exclusion_List"></a> So ändern Sie die Ausschlussliste für die Migration  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Migration** , um auf die Ausschlussliste zuzugreifen. Sie können auch über den Knoten **Quellhierarchie** oder **Migrationsaufträge** auf die Ausschlussliste zugreifen.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Migration** auf **Ausschlussliste bearbeiten**.  

4.  Wählen Sie im Dialogfeld **Ausschlussliste bearbeiten** das ausgeschlossene Objekt aus, das Sie aus der Ausschlussliste entfernen möchten, und klicken Sie dann auf **Entfernen**.  

5.  Klicken Sie auf **OK** , um die Änderungen zu speichern und die Bearbeitung abzuschließen. Klicken Sie zum Verwerfen der aktuellen Änderungen und zum Wiederherstellen aller entfernten Objekte auf **Abbrechen**und dann auf **Nein**. Dadurch wird das Entfernen der Objekte abgebrochen, und das Dialogfeld **Ausschlussliste bearbeiten** wird geschlossen.  

#### <a name="to-share-distribution-points-from-the-source-hierarchy"></a>So geben Sie Verteilungspunkte aus der Quellhierarchie frei  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, klicken Sie auf **Quellhierarchie**, und wählen Sie dann den Quellstandort aus, den Sie konfigurieren möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Quellstandort** auf **Konfigurieren**.  

4.  Wählen Sie im Dialogfeld **Anmeldeinformationen des Quellstandorts** die Option **Gemeinsame Verwendung des Verteilungspunkts für den Quellstandortserver aktivieren**aus, und klicken Sie dann auf **OK**.  

5.  Wenn die Datensammlung abgeschlossen ist, klicken Sie auf **Schließen**.  

#### <a name="to-change-the-schedule-of-a-migration-job"></a>So ändern Sie den Zeitplan eines Migrationsauftrags  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und klicken Sie dann auf **Migrationsaufträge**.  

3.  Klicken Sie auf den Migrationsauftrag, den Sie ändern möchten. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Wählen Sie in den Eigenschaften des Migrationsauftrags die Registerkarte **Einstellungen** aus, ändern Sie die Laufzeit des Migrationsauftrags, und klicken Sie dann auf **OK**.  

##  <a name="a-namerunmigrationjobsa-run-migration-jobs"></a><a name="Run_Migration_Jobs"></a> Ausführen von Migrationsaufträgen  
 Verwenden Sie das folgende Verfahren, um einen Migrationsauftrag auszuführen, der noch nicht gestartet wurde.  

#### <a name="to-run-migration-jobs"></a>So führen Sie Migrationsaufträge aus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und klicken Sie dann auf **Migrationsaufträge**.  

3.  Klicken Sie auf den Migrationsauftrag, den Sie ausführen möchten. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Migrationsauftrag** auf **Starten**.  

4.  Klicken Sie auf **Ja** , um den Migrationsauftrag jetzt zu starten.  

##  <a name="a-namebkmkprocupgrdssa-upgrade-or-reassign-a-shared-distribution-point"></a><a name="BKMK_ProcUpgrdSS"></a> Aktualisieren oder erneutes Zuweisen eines freigegebenen Verteilungspunkts  
 Sie können einen unterstützten Verteilungspunkt aktualisieren, der von einem Configuration Manager 2007-Quellstandort freigegeben wird. Außerdem können Sie einen von einem System Center Configuration Manager-Quellstandort freigegebenen Verteilungspunkt als Verteilungspunkt in der Zielhierarchie neu zuweisen.  

> [!IMPORTANT]  
>  Bevor Sie ein Upgrade für einen Configuration Manager 2007-Zweigverteilungspunkt ausführen, müssen Sie die Configuration Manager 2007-Clientsoftware auf dem Zweigverteilungspunkt-Computer deinstallieren. Wenn die Configuration Manager 2007-Clientsoftware beim Versuch installiert wird, den Verteilungspunkt zu aktualisieren, tritt ein Fehler auf, und Inhalte, die zuvor auf dem Zweigverteilungspunkt bereitgestellt wurden, werden vom Computer entfernt.  

> [!CAUTION]  
>  Beim Aktualisieren oder erneuten Zuweisen eines freigegebenen Verteilungspunkts werden die Standortsystemrolle Verteilungspunkt und der Standortsystemcomputer am Quellstandort entfernt und dem gewählten Standort in der Zielhierarchie als Verteilungspunkt hinzugefügt.  

#### <a name="to-upgrade-or-reassign-a-shared-distribution-point"></a>So können Sie einen freigegebenen Verteilungspunkt aktualisieren oder neu zuweisen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und klicken Sie dann auf **Quellhierarchie**.  

3.  Wählen Sie den Standort aus, der Besitzer des zu aktualisierenden Verteilungspunkts ist. Klicken Sie auf **Freigegebene Verteilungspunkte** , und wählen Sie den geeigneten Verteilungspunkt aus, den Sie aktualisieren bzw. neu zuweisen möchten.  

4.  Klicken Sie auf der Registerkarte **Verteilungspunkt** in der Gruppe **Verteilungspunkt** auf **Neu zuweisen**.  

5.  Geben Sie im Assistenten zur Neuzuweisung des freigegebenen Verteilungspunkts dieselben Einstellungen wie bei der Installation eines neuen Verteilungspunkts für die Zielhierarchie an, und fügen Sie Folgendes hinzu:  

    -   Prüfen Sie auf der Seite **Inhaltskonvertierung** die Richtlinien zum Speicherplatz, der zum Konvertieren des vorhandenen Inhalts erforderlich ist. Stellen Sie anschließend auf der Seite **Laufwerkseinstellungen** des Assistenten sicher, dass auf dem Laufwerk des ausgewählten Verteilungspunktcomputers die erforderliche Menge an freiem Festplattenspeicher verfügbar ist.  

6.  Bestätigen Sie die Einstellungen, und beenden Sie dann den Assistenten.  

##  <a name="a-namemonitormigrationa-monitor-migration-activity-in-the-migration-workspace"></a><a name="Monitor_MIgration"></a> Überwachen der Migrationsaktivität im Arbeitsbereich „Migration“  
 Gehen Sie wie folgt vor, um die Configuration Manager-Konsole zum Überwachen der Migration zu verwenden.  

#### <a name="to-monitor-migration-activity-in-the-migration-workspace"></a>So überwachen Sie die Migrationsaktivität im Arbeitsbereich "Migration"  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und klicken Sie dann auf **Migrationsaufträge**.  

3.  Klicken Sie auf den Migrationsauftrag, den Sie überwachen möchten.  

4.  Auf den Registerkarten **Zusammenfassung** und **Objekte in Auftrag**können Sie Details und Status von ausgewählten Migrationsaufträgen anzeigen.  

##  <a name="a-namebkmkmigrateclientsa-migrate-clients"></a><a name="BKMK_MigrateClients"></a> Migrieren von Clients  
 Planen Sie die Migration der Clients zur Zielhierarchie, nachdem das Migrieren von Clientdaten zwischen Hierarchien fertig gestellt wurde, die Migration aber noch nicht abgeschlossen ist. Im Rahmen der Clientmigration zwischen Hierarchien muss die Configuration Manager-Clientsoftware von Computern deinstalliert werden, die der Quellhierarchie zugewiesen sind. Anschließend muss die Configuration Manager-Clientsoftware aus der Zielhierarchie installiert werden. Bei der Clientinstallation aus der Zielhierarchie weisen Sie den Client auch einem primären Standort dieser Hierarchie zu. Weitere Informationen zur Clientmigration finden Sie unter [Planen einer Strategie für die Clientmigration in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="a-namecompletemigrationa-complete-migration"></a><a name="Complete_Migration"></a> Abschließen der Migration  
 Gehen Sie wie folgt vor, um die Migration von der Quellhierarchie abzuschließen.  

#### <a name="to-complete-migration"></a>So schließen Sie die Migration ab  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und klicken Sie dann auf **Quellhierarchie**.  

3.  Wählen Sie für eine Configuration Manager 2007-Quellhierarchie einen Quellstandort aus, der sich auf der unteren Ebene der Quellhierarchie befindet. Für eine System Center 2012 Configuration Manager- oder System Center Configuration Manager-Quellhierarchie wählen Sie den verfügbaren Quellstandort.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereinigen** auf **Sammeln von Daten beenden**.  

5.  Klicken Sie zum Bestätigen der Aktion auf **Ja** .  

6.  Bevor Sie für eine Configuration Manager 2007-Quellhierarchie mit dem nächsten Schritt fortfahren, wiederholen Sie die Schritte 3, 4 und 5. Führen Sie diese Schritte für jeden Standort in der Hierarchie von unten nach oben aus. Für eine System Center 2012 Configuration Manager- oder System Center Configuration Manager-Quellhierarchie fahren Sie mit dem nächsten Schritt fort.  

7.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereinigen** auf **Migrationsdaten bereinigen**.  

8.  Wählen Sie im Dialogfeld **Migrationsdaten bereinigen** aus der Dropdownliste **Quellhierarchie** den Standortcode und den Standortserver des Standorts der obersten Ebene der Quellhierarchie aus, und klicken Sie dann auf **OK**.  

9. Klicken Sie auf **Ja** , um den Migrationsprozess für die Quellhierarchie abzuschließen.  



<!--HONumber=Dec16_HO3-->


