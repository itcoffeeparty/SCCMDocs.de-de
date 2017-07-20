---
title: "Konfigurieren von Verfügbarkeitsgruppen | Microsoft-Dokumentation"
description: "Verwenden Sie SCCM zum Einrichten und Verwalten von SQL Server AlwaysOn-Verfügbarkeitsgruppen."
ms.custom: na
ms.date: 5/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dc221ddf547c43ab1f25ff83c3c9bb603297ece6
ms.openlocfilehash: 138834b6cc64332202256961ad1d2f5ab6d176db
ms.contentlocale: de-de
ms.lasthandoff: 06/01/2017


---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Konfigurieren von SQL Server AlwaysOn-Verfügbarkeitsgruppen für Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie die Informationen in diesem Thema zum Konfigurieren und Verwalten der Verfügbarkeitsgruppen, die Sie mit Configuration Manager verwenden.

Vorbereitung:  
-   Machen Sie sich mit den Informationen unter [Vorbereiten der Verwendung von SQL Server AlwaysOn-Verfügbarkeitsgruppen mit Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database) vertraut.
-   Machen Sie sich mit der SQL Server-Dokumentation vertraut, die die Verwendung von Verfügbarkeitsgruppen und damit verbundener Verfahren behandelt, die zum Abschießen der folgenden Szenarien erforderlich sind.

> [!TIP]  
>  Links zu SQL Server in diesem Thema beziehen sich auf Inhalte für SQL Server 2016. Wenn Sie diese Version von SQL Server nicht verwenden, greifen Sie auf die Dokumentation der von Ihnen verwendeten Version zurück.

## <a name="create-and-configure-an-availability-group"></a>Erstellen und Konfigurieren einer Verfügbarkeitsgruppe
Verwenden Sie das folgende Verfahren zum Erstellen einer Verfügbarkeitsgruppe, und verschieben Sie dann eine Kopie der Standortdatenbank in diese Verfügbarkeitsgruppe.

Um dieses Verfahren ausführen zu können, muss für das verwendete Konto Folgendes gelten:
-   Es muss auf jedem Computer, der zur Verfügbarkeitsgruppe gehören soll, ein Mitglied der Gruppe **Lokale Administratoren** sein.
-   Es muss ein **Systemadministrator** für jede SQL Server-Instanz sein, die die Standortdatenbank hostet.

### <a name="to-create-and-configure-an-availability-group-for-configuration-manager"></a>So erstellen und konfigurieren Sie eine Verfügbarkeitsgruppe für Configuration Manager  
1.    Verwenden Sie den folgenden Befehl, um den Configuration Manager-Standort zu beenden: **Preinst.exe /stopsite**. Weitere Informationen zur Verwendung von „Preinst.exe“ finden Sie unter [Hierarchiewartungstool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2.    Ändern Sie das Sicherungsmodell der Standortdatenbank von **EINFACH** in **VOLLSTÄNDIG**.
Siehe [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) in der SQL Server-Dokumentation. (Verfügbarkeitsgruppen unterstützen nur VOLLSTÄNDIG).

3.    Verwenden Sie SQL Server, um eine vollständige Sicherung Ihrer Standortdatenbank zu erstellen, und führen Sie dann eines der folgenden Verfahren aus. Das jeweilige Verfahren ist davon abhängig, ob der Server, der die Standortdatenbank hostet, ein Replikationsmitglied der neuen Verfügbarkeitsgruppe sein soll:
    -   **Soll ein Mitglied der Verfügbarkeitsgruppe sein:**  
        Wenn Sie diesen Server als das anfängliche primäre Replikationsmitglied der Verfügbarkeitsgruppe verwenden, müssen Sie keine Kopie der Standortdatenbank auf diesem oder einem anderen Server in der Gruppe wiederherstellen. Die Datenbank ist bereits auf dem primären Replikat eingerichtet, und SQL Server repliziert in einem späteren Schritt die Datenbank auf die sekundären Replikate.  

      -    **Soll kein Mitglied der Verfügbarkeitsgruppe sein:**   
    Sie müssen eine Kopie der Standortdatenbank auf dem Server wiederherstellen, der das primäre Replikat der Gruppe hosten soll.

    Informationen zum Ausführen dieses Schritts finden Sie unter [Erstellen einer vollständigen Datenbanksicherung](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) und [Wiederherstellen einer Datenbanksicherung mit SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) in der SQL Server-Dokumentation.

4.    Verwenden Sie auf dem Server, auf dem das anfängliche primäre Replikat der Gruppe gehostet wird, den [Assistenten für neue Verfügbarkeitsgruppen](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) zum Erstellen der Verfügbarkeitsgruppe. Gehen Sie im Assistenten so vor:
      -    Wählen Sie auf der Seite **Datenbank auswählen** die Datenbank für Ihren Configuration Manager-Standort aus.  

      -    Konfigurieren Sie auf der Seite **Replikate angeben** Folgendes:
          -    **Replikate**: Geben Sie die Server an, die die sekundären Replikate hosten sollen.

          -    **Listener**: Geben Sie den **DNS-Listenernamen** als vollständigen DNS-Namen wie **&lt;Listenerserver>.fabrikam.com** ein. Dieser Vorgang wird verwendet, wenn Sie Configuration Manager für die Verwendung der Datenbank in der Verfügbarkeitsgruppe konfigurieren.

      -    Wählen Sie auf der Seite **Anfängliche Datensynchronisierung auswählen** die Einstellung **Vollständig**aus. Nachdem der Assistent die Verfügbarkeitsgruppe erstellt hat, sichert er die primäre Datenbank und das Transaktionsprotokoll und stellt dann beides auf allen Servern wieder her, auf denen ein sekundäres Replikat gehostet wird. (Wenn Sie diesen Schritt nicht ausführen, müssen Sie eine Kopie der Standortdatenbank auf allen Servern wiederherstellen, auf denen ein sekundäres Replikat gehostet wird, und die Datenbank manuell mit der Gruppe verknüpfen.)   

5.    Überprüfen Sie die Konfiguration auf jedem Replikat:   
  1.    Stellen Sie sicher, dass das Computerkonto des Standortservers Mitglied der Gruppe **Lokale Administratoren** auf allen Computern ist, die zur Verfügbarkeitsgruppe gehören.  

  2.  Führen Sie die [Überprüfungsskript](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) aus den Voraussetzungen aus, um sicherzustellen, dass die Standortdatenbank auf jedem Replikat ordnungsgemäß konfiguriert ist.

  3.    Wenn auf sekundären Replikaten Konfigurationen festgelegt werden müssen, müssen Sie manuell ein Failover des primären Replikats auf das sekundäre Replikat ausführen, bevor Sie fortfahren. Sie können nämlich nur die Datenbank eines primären Replikats konfigurieren. Weitere Informationen finden Sie unter [Ausführen eines geplanten manuellen Failovers einer Verfügbarkeitsgruppe](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) in der SQL Server-Dokumentation.

6.    Wenn alle Replikate die Anforderungen erfüllen, kann die Verfügbarkeitsgruppe mit Configuration Manager verwendet werden.

## <a name="configure-a-site-to-use-the-database-in-the-availability-group"></a>Konfigurieren eines Standorts, um die Datenbank in der Verfügbarkeitsgruppe zu verwenden
Nachdem Sie [die Verfügbarkeitsgruppe erstellt und konfiguriert haben](#create-and-configure-an-availability-group), verwenden Sie die Configuration Manager-Standortwartung, um den Standort für die Verwendung der Datenbank zu konfigurieren, die von der Verfügbarkeitsgruppe gehostet wird.

Das Installieren eines neuen Standorts mit einer Datenbank in einer Verfügbarkeitsgruppe wird nicht unterstützt. Wenn Sie die Medien der Baseline 1702 verwenden, müssen Sie den Standort mithilfe einer einzelnen Instanz von SQL Server installieren. Nach der Installation des Standorts können Sie die Standortdatenbank in die Verfügbarkeitsgruppe verschieben.

Um dieses Verfahren auszuführen, muss für das Konto, mit dem das Configuration Manager-Setup ausgeführt wird, Folgendes gelten:
-   Es muss auf jedem Computer, der Mitglied der Verfügbarkeitsgruppe ist, ein Mitglied der Gruppe **Lokale Administratoren** sein.
-   Es muss ein **Systemadministrator** für jede SQL Server-Instanz sein, die die Standortdatenbank hostet.

> [!IMPORTANT]
> Wenn Sie Microsoft Intune mit Configuration Manager in einer Hybridkonfiguration verwenden, löst das Verschieben der Standortdatenbank in oder aus einer Verfügbarkeitsgruppe eine erneute Synchronisierung von Daten mit der Cloud aus. Dies kann nicht vermieden werden.

### <a name="to-configure-a-site-to-use-the-availability-group"></a>So konfigurieren Sie einen Standort zur Verwendung der Verfügbarkeitsgruppe
1.    Führen Sie das **Configuration Manager-Setup** unter **&lt;*Installationsordner des Configuration Manager-Standorts*>\BIN\X64\setup.exe** aus.

2.    Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen**aus, und klicken Sie dann auf **Weiter**.

3.    Wählen Sie die Option **SQL Server-Konfiguration ändern** aus, und klicken Sie auf **Weiter**.

4.    Konfigurieren Sie Folgendes für die Standortdatenbank neu:
    -   **SQL Server-Name**: Geben Sie den virtuellen Namen für den **Verfügbarkeitsgruppenlistener** ein, den Sie beim Erstellen der Verfügbarkeitsgruppe konfiguriert haben. Der virtuelle Name sollte ein vollständiger DNS-Name sein, wie z.B. **&lt;*Endpunktserver*>.fabrikam.com**.  

    -   **Instanz**: Dieser Wert muss leer sein, um die Standardinstanz für den *Listener* der Verfügbarkeitsgruppe anzugeben. Wenn die aktuelle Standortdatenbank auf einer benannten Instanz installiert ist, ist die benannte Instanz aufgeführt und muss gelöscht werden.

    -   **Datenbank:** Belassen Sie den angezeigten Namen unverändert. Dies ist der Name der aktuellen Standortdatenbank.

5.    Nachdem Sie die Informationen zum neuen Speicherort der Datenbank bereitgestellt haben, schließen Sie das Setup mit der üblichen Vorgehensweise und den normalen Konfigurationen ab.



## <a name="add-and-remove-replica-members"></a>Hinzufügen und Entfernen von Replikationsmitgliedern  
Wenn die Standortdatenbank in einer Verfügbarkeitsgruppe gehostet wird, verwenden Sie die folgenden Verfahren, um Replikationsmitglieder hinzuzufügen oder zu entfernen. Configuration Manager unterstützt einen einzelnen primären und bis zu zwei sekundäre Knoten.

Um die folgenden Verfahren ausführen zu können, muss für das verwendete Konto Folgendes gelten:
-   Es muss auf jedem Computer, der Mitglied der Verfügbarkeitsgruppe ist, ein Mitglied der Gruppe **Lokale Administratoren** sein.
-   Es muss ein **Systemadministrator** für jede SQL Server-Instanz sein, die die Standortdatenbank hostet.


### <a name="to-add-a-new-replica-member"></a>So fügen Sie ein neue Replikatsmitglied hinzu
1.    Fügen Sie den neuen Server als sekundäres Replikat der Verfügbarkeitsgruppe hinzu. Siehe [Hinzufügen eines sekundären Replikats zu einer Verfügbarkeitsgruppe (SQL Server)](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server) in der SQL Server-Dokumentationsbibliothek.

2.    Beenden Sie durch Ausführen von **Preinst.exe /stopsite** den Configuration Manager-Standort. Siehe [Hierarchiewartungstool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

3.    Verwenden Sie SQL Server, um eine Sicherung der Standortdatenbank aus dem primären Replikat zu erstellen, und stellen Sie dann diese Sicherung auf dem neuen sekundären Replikatserver wieder her. Siehe [Erstellen einer vollständigen Datenbanksicherung](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) und [Wiederherstellen einer Datenbanksicherung mit SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) in der SQL Server-Dokumentation.

4.    Konfigurieren Sie alle sekundären Replikate. Führen Sie die folgenden Schritte für alle sekundären Replikate in der Verfügbarkeitsgruppe aus:

    1.    Stellen Sie sicher, dass das Computerkonto des Standortservers Mitglied der Gruppe **Lokale Administratoren** auf allen Computern ist, die zur Verfügbarkeitsgruppe gehören.

    2.    Führen Sie die [Überprüfungsskript](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) aus den Voraussetzungen aus, um sicherzustellen, dass die Standortdatenbank auf jedem Replikat ordnungsgemäß konfiguriert ist.

    3.    Wenn ein neues Replikat konfiguriert werden muss, führen Sie ein manuelles Failover des primären Replikats auf das neue sekundäre Replikat aus, und legen Sie dann die erforderlichen Einstellungen fest. Siehe [Ausführen eines geplanten manuellen Failovers einer Verfügbarkeitsgruppe](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) in der SQL Server-Dokumentation.

5.    Starten Sie den Standort neu, indem Sie die Dienste Standortkomponenten-Manager (**sitecomp**) und **SMS_Executive** starten.

### <a name="to-remove-a-replica-member"></a>So entfernen Sie ein Replikationsmitglied
Verwenden Sie für dieses Verfahren die Informationen unter [Entfernen eines sekundären Replikats aus einer Verfügbarkeitsgruppe](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server) in der SQL Server-Dokumentation.

## <a name="stop-using-an-availability-group"></a>Beenden der Verwendung einer Verfügbarkeitsgruppe
Führen Sie das folgende Verfahren aus, wenn Sie Ihre Standortdatenbank nicht mehr in einer Verfügbarkeitsgruppe hosten möchten. Dies umfasst, die Standortdatenbank wieder auf eine einzelne Instanz von SQL Server zu verschieben.

Um dieses Verfahren ausführen zu können, muss für das verwendete Konto Folgendes gelten:
-   Es muss auf jedem Computer, der Mitglied der Verfügbarkeitsgruppe ist, ein Mitglied der Gruppe **Lokale Administratoren** sein.
-   Es muss ein **Systemadministrator** für jede SQL Server-Instanz sein, die die Standortdatenbank hostet.

> [!IMPORTANT]  
> Wenn Sie Microsoft Intune mit Configuration Manager in einer Hybridkonfiguration verwenden, löst das Verschieben der Standortdatenbank in oder aus einer Verfügbarkeitsgruppe eine erneute Synchronisierung von Daten mit der Cloud aus. Dies kann nicht vermieden werden.

### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>So verschieben Sie die Standortdatenbank aus einer Verfügbarkeitsgruppe zurück in eine einzelne Instanz von SQL Server
1.    Beenden Sie den Configuration Manager-Standort mit dem folgenden Befehl: **Preinst.exe /stopsite**. Weitere Informationen finden Sie unter [Hierarchiewartungstool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2.    Verwenden Sie SQL Server, um eine vollständige Sicherung Ihrer Standortdatenbank anhand des primären Replikats zu erstellen. Informationen zum Ausführen dieses Schritts finden Sie unter [Erstellen einer vollständigen Datenbanksicherung](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) in der SQL Server-Dokumentation.

3.    Wenn der Server, der das primäre Replikat für die Verfügbarkeitsgruppe ist, die einzelne Instanz der Standortdatenbank hostet, können Sie diesen Schritt überspringen:  

    -   Verwenden Sie SQL Server, um die Sicherung der Standortdatenbank auf dem Server wiederherzustellen, der die Standortdatenbank hostet. Siehe [Wiederherstellen einer Datenbanksicherung mit SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) in der SQL Server-Dokumentation.   <br />  <br />

4.    Ändern Sie auf dem Server, der die Standortdatenbank hosten soll (das primäre Replikat oder der Server, auf dem Sie die Standortdatenbank wiederhergestellt haben), das Sicherungsmodell für die Standortdatenbank von **VOLLSTÄNDIG** in **EINFACH**. Siehe [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) in der SQL Server-Dokumentation.  

5.    Führen Sie das **Configuration Manager-Setup** unter **&lt;*Installationsordner des Configuration Manager-Standorts>*\BIN\X64\setup.exe** aus.

6.    Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen**aus, und klicken Sie dann auf **Weiter**.  

7.    Wählen Sie die Option **SQL Server-Konfiguration ändern** aus, und klicken Sie auf **Weiter**.  

8.    Konfigurieren Sie Folgendes für die Standortdatenbank neu:
    -   **Name des SQL-Servers** : Geben Sie den Namen des Servers ein, auf dem nun die Standortdatenbank gehostet wird.

    -   **Instanz:** Geben Sie die benannte Instanz an, die die Standortdatenbank hostet. Lassen Sie dieses Feld leer, wenn sich die Datenbank in der Standardinstanz befindet.

    -   **Datenbank:** Belassen Sie den angezeigten Namen unverändert. Dies ist der Name der aktuellen Standortdatenbank.    

9.    Nachdem Sie die Informationen zum neuen Speicherort der Datenbank bereitgestellt haben, schließen Sie das Setup mit der üblichen Vorgehensweise und den normalen Konfigurationen ab. Nach Abschluss des Setups wird der Standort neu gestartet und beginnt mit der Nutzung des neuen Speicherorts der Datenbank.    

10.    Zur Bereinigung der Server, die Mitglied der Verfügbarkeitsgruppe waren, befolgen Sie die Anleitung unter [Entfernen einer Verfügbarkeitsgruppe](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server) in der SQL Server-Dokumentation.

