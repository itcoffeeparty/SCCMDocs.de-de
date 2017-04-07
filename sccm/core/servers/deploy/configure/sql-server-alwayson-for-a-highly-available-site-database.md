---
title: SQL Server Always On | Microsoft-Dokumentation
ms.custom: na
ms.date: 1/4/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: aaaab003ddd22f18160d4be63cfeab3a7e7f6b03
ms.lasthandoff: 03/27/2017


---
# <a name="sql-server-alwayson-for-a-highly-available-site-database-for-system-center-configuration-manager"></a>SQL Server AlwaysOn für eine hoch verfügbare Standortdatenbank für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 Beginnend mit der System Center Configuration Manager-Version 1602 können Sie SQL Server-[Always On-Verfügbarkeitsgruppen](https://msdn.microsoft.com/library/hh510230\(v=sql.120\).aspx) zum Hosten der Standortdatenbank an primären Standorten und am Standort der zentralen Verwaltung als Lösung für hohe Verfügbarkeit und Notfallwiederherstellung nutzen. Die Verfügbarkeitsgruppe kann lokal oder in Microsoft Azure gehostet werden.  

 Wenn Sie Microsoft Azure zum Hosten der Verfügbarkeitsgruppe verwenden, können Sie die Verfügbarkeit Ihrer Standortdatenbank weiter steigern, indem Sie SQL Server AlwaysOn-Verfügbarkeitsgruppen mit Azure-Verfügbarkeitsgruppen einsetzen. Weitere Informationen zu Azure-Verfügbarkeitsgruppen finden Sie unter [Verwalten der Verfügbarkeit von virtuellen Computern](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).  

 Configuration Manager unterstützt das Hosten der Standortdatenbank auf einer SQL-Verfügbarkeitsgruppe, die sich hinter einem internen oder externen Lastenausgleich befindet. Zusätzlich zum Konfigurieren von Firewallausnahmen für jedes Replikat müssen Sie Lastenausgleichsregeln für die folgenden Ports hinzufügen:
  - SQL über TCP: TCP 1433
  - SQL Server Service Broker: TCP 4022
  - Server Message Block (SMB): TCP 445
  - RPC-Endpunktzuordnung: TCP 135


Die folgenden Szenarios werden mit Verfügbarkeitsgruppen unterstützt:  

-   Sie können Ihre Standortdatenbank in die Standardinstanz einer Verfügbarkeitsgruppe verschieben.  

-   Sie können einer Verfügbarkeitsgruppe, die eine Standortdatenbank hostet, Replikationsmitglieder hinzufügen oder diese daraus entfernen.  

-   Sie können Ihre Standortdatenbank aus einer Verfügbarkeitsgruppe in eine Standard- oder benannte Instanz einer eigenständigen SQL Server-Instanz verschieben.  

> [!Important]  
> Wenn Sie Microsoft Intune mit Configuration Manager in einer Hybridkonfiguration verwenden, löst das Verschieben der Standortdatenbank zu oder von einer Verfügbarkeitsgruppe eine erneute Synchronisierung von Daten mit der Cloud aus. Dies kann nicht vermieden werden. 



> [!NOTE]  
>  Die erfolgreiche Konfiguration und Verwendung von Verfügbarkeitsgruppen erfordert, dass Sie mit dem Konfigurieren von SQL Server und SQL Server-Verfügbarkeitsgruppen vertraut sind. Für die Verfahren für System Center Configuration Manager in diesem Thema gibt es in der SQL Server-Dokumentationsbibliothek zusätzliche Dokumentation und Verfahren.  

 **Bekannte Probleme, wenn Sie AlwaysOn-Verfügbarkeitsgruppen mit Configuration Manager verwenden:**  

-   **Alle Replikatserver erfordern einen identischen Dateipfad zum Zeitpunkt, an dem Sie Configuration Manager für die Verwendung einer Verfügbarkeitsgruppe einrichten:**  

    -   Zum Zeitpunkt, an dem Sie das Setup von Configuration Manager so ausführen, dass der Standort für die Verwendung der Datenbank in einer Verfügbarkeitsgruppe umgeleitet wird, muss jeder sekundäre Replikatserver in der Gruppe einen Dateipfad aufweisen, der identisch mit dem Dateipfad ist, der zum Hosten der Standortdatenbank-Dateien für das aktuelle primäre Replikat verwendet wird. Wenn für sekundäre Replikate kein identischer Pfad vorhanden ist, kann das Setup nicht die Verfügbarkeitsgruppeninstanz als neuen Speicherort der Standortdatenbank hinzufügen.  

         Darüber hinaus muss das lokale SQL Server-Dienstkonto für jeden sekundären Replikatserver über die Berechtigung **Vollzugriff** für diesen Ordner verfügen.  

         Die sekundären Replikatserver benötigen diesen Dateipfad nur, während Sie Setup verwenden, um die Datenbankinstanz der Verfügbarkeitsgruppe anzugeben.  Nachdem vom Setup die Änderung zum Verwenden der Standortdatenbank in der Verfügbarkeitsgruppe durchgeführt wurde, können Sie den nicht verwendeten Pfad von sekundären Replikatservern löschen.  

         Betrachten Sie beispielsweise das folgende Szenario:  

        -   Sie erstellen eine Verfügbarkeitsgruppe, die drei SQL Server-Instanzen verwendet.  

        -   Ihr primärer Replikatserver ist eine Neuinstallation von SQL Server 2014.  Standardmäßig werden die Datenbankdateien der Typen MDF und LDF in „C:\Programme\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA“ gespeichert.  

        -   Ihre beiden sekundären Replikatserver wurden von früheren Versionen auf SQL Server 2014 aktualisiert, und Sie behalten den ursprünglichen Dateipfad zum Speichern von Datenbankdateien bei, nämlich: C:\Programme\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA  

        -   Bevor Sie versuchen, die Standortdatenbank in diese Verfügbarkeitsgruppe zu verschieben, müssen Sie auf allen sekundären Replikatservern den folgenden Dateipfad anlegen, auch wenn die sekundären Replikate diesen Dateispeicherort nicht nutzen: C:\Programme\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA (ein Duplikat des Pfads, der für das primäre Replikat verwendet wird)  

        -   Anschließend gewähren Sie dem SQL Server-Dienstkonto für jedes sekundäre Replikat Vollzugriff auf den neu erstellten Speicherort auf dem Server.  

        -   Sie können nun das Setup von Configuration Manager erfolgreich so ausführen, dass die Standortdatenbank in der Verfügbarkeitsgruppe verwendet wird.  

-   **Wenn das Setup so ausgeführt wird, dass die Standortdatenbank für die Verwendung der Verfügbarkeitsgruppe konfiguriert wird, kann in der Datei „ConfigMgrSetup.log“ Folgendes protokolliert werden:**  

    -   Fehler: SQL Server-Fehler: [25000] [3906] [Microsoft] [SQL Server Native Client 11.0] [SQL Server]-Fehler beim Aktualisieren der Datenbank „CM_AAA“, weil die Datenbank schreibgeschützt ist.   Configuration Manager-Setup 1/21/2016 4:54:59 PM  7344 (0x1CB0)  

     Diese Fehler werden protokolliert, wenn Setup versucht, Datenbankrollen für sekundäre Replikate der Verfügbarkeitsgruppe zu verarbeiten. Diese Fehler können problemlos ignoriert werden.
- **SQL-Server, die zusätzliche Verfügbarkeitsgruppen hosten:**

  Wenn Sie eine Verfügbarkeitsgruppe verwenden und dann das Configuration Manager-Setup ausführen oder ein Update für Configuration Manager installieren, muss jedes Replikat in jeder zusätzlichen Verfügbarkeitsgruppe auf dem SQL-Server, der die Configuration Manager-Verfügbarkeitsgruppe hostet, vor der Installation von Version 1610 die folgenden Konfigurationen aufweisen:
    - **Manuelles Failover**
    - **Alle schreibgeschützten Verbindungen zulassen**


##  <a name="bkmk_BnR"></a> Änderungen bei Sicherung und Wiederherstellung bei Verwendung einer SQL Server AlwaysOn-Verfügbarkeitsgruppe  
 **Sicherung:**  

 Wenn eine Datenbank in einer Verfügbarkeitsgruppe ausgeführt wird, muss der integrierte Serverwartungstask **Standort sichern** weiter ausgeführt werden, um allgemeine Configuration Manager-Einstellungen und -Dateien zu sichern. Planen Sie jedoch nicht das Verwenden der von dieser Sicherung erstellten MDF- und LDF-Dateien. Planen Sie stattdessen das direkte Erstellen von Sicherungskopien der Standortdatenbank mithilfe von SQL Server.  

 Da darüber hinaus das Wiederherstellungsmodell der Datenbank auf „Vollständig“ festgelegt ist, müssen Sie die Überwachung und Verwaltung der Größe des Transaktionsprotokolls der Standortdatenbank planen.  Beim Wiederherstellungsmodell „Vollständig“ werden Transaktionen erst festgeschrieben, nachdem eine vollständige Sicherung der Datenbank oder des Transaktionsprotokolls erfolgt ist. Das Wiederherstellungsmodell „Vollständig“ ist eine Voraussetzung für das Verwenden der Standortdatenbank in einer Verfügbarkeitsgruppe und wird festgelegt, wenn Sie die Gruppe für die Verwendung mit Configuration Manager konfigurieren. Weitere Informationen zur SQL Server-Sicherung und -Wiederherstellung finden Sie unter [Sichern und Wiederherstellen von SQL Server-Datenbanken](https://msdn.microsoft.com/library/ms187048\(v=sql.120\).aspx) in der SQL Server-Dokumentation.  

 **Wiederherstellung:**  

 Wenn während der Wiederherstellung eines Standorts ein Knoten der Verfügbarkeitsgruppe funktionsfähig ist, können Sie die Wiederherstellungsoption **Datenbankwiederherstellung überspringen (diese Option verwenden, wenn die Standortdatenbank nicht betroffen war)**wählen.  

 Wenn jedoch alle Knoten einer Verfügbarkeitsgruppe verloren gegangen sind, bevor Sie den Standort wiederherstellen können, müssen Sie die Verfügbarkeitsgruppe neu erstellen (System Center Configuration Manager kann den Verfügbarkeitsknoten nicht erneut erstellen oder wiederherstellen).  Nachdem die Gruppe mithilfe einer Sicherung wiederhergestellt und neu konfiguriert wurde, können Sie die Wiederherstellungsoption für den Standort **Datenbankwiederherstellung überspringen (diese Option verwenden, wenn die Standortdatenbank nicht betroffen war)** wählen.  

 Weitere Informationen zur Standortserversicherung und -wiederherstellung finden Sie unter [Sicherung und Wiederherstellung für System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

##  <a name="bkmk_create"></a> Konfigurieren einer Verfügbarkeitsgruppe für die Verwendung mit Configuration Manager  
 Bevor Sie das folgende Verfahren starten, sollten Sie mit den SQL Server-Prozeduren, die für diese Konfiguration erforderlich sind, und mit den folgenden Details vertraut sein, die für Verfügbarkeitsgruppen gelten, die Sie für die Verwendung mit Configuration Manager konfigurieren.  

 **Anforderungen an die AlwaysOn-Verfügbarkeitsgruppen, die Sie mit System Center Configuration Manager verwenden:**  

-  *Version*: Jeder Knoten (oder jedes Replikat) in der Verfügbarkeitsgruppe muss eine Version von SQL Server ausführen, die von System Center Configuration Manager unterstützt wird. Wenn von SQL Server unterstützt, können die verschiedenen Knoten der Verfügbarkeitsgruppe unterschiedliche Versionen von SQL Server ausführen.   

- *Edition*: Sie müssen eine Enterprise Edition von SQL Server verwenden.  SQL Server 2016 Standard Edition bietet Basis-Verfügbarkeitsgruppen, die nicht von Configuration Manager unterstützt werden.


-   Die Verfügbarkeitsgruppe muss über ein primäres Replikat verfügen und kann bis zu zwei synchrone sekundäre Replikate enthalten.  

-  Nach dem Hinzufügen einer Datenbank zu einer Verfügbarkeitsgruppe müssen Sie ein Failover für das primäre Replikat in ein sekundäres Replikat ausführen (wodurch dies das neue primäre Replikat wird) und anschließend die Datenbank mit Folgendem konfigurieren:
    - Aktivieren von „Vertrauenswürdig“: auf TRUE setzen
    - Aktivieren von Service Broker: auf TRUE setzen
    - Festlegen des Besitzers: SA eingeben

    Sie können das folgende Skript ausführen, um diese Einstellungen zu konfigurieren, wobei „cm_ABC“ der Name der Standortdatenbank ist:  

    >     USE master  
    >     ALTER DATABASE cm_ABC SET NEW_BROKER   
    >     ALTER DATABASE cm_ABC SET ENABLE_BROKER  
    >     ALTER DATABASE cm_ABC SET TRUSTWORTHY ON;  
    >     USE cm_ABC  
    >     EXEC sp_changedbowner 'sa'  
    >     Exec sp_configure 'max text repl size (B)', 2147483647 reconfigure



-   Die Verfügbarkeitsgruppe muss mindestens einen **Verfügbarkeitsgruppenlistener**besitzen.  Der virtuelle Name dieses Listeners wird verwendet, wenn Sie Configuration Manager für die Verwendung der Standortdatenbank in der Verfügbarkeitsgruppe konfigurieren. Eine Verfügbarkeitsgruppe kann zwar mehrere Listener enthalten, Configuration Manager kann aber nur einen Endpunkt nutzen.  

-   Jedes primäre und sekundäre Replikat muss:  
    - auf **Alle schreibgeschützten Verbindungen zulassen**festgelegt sein.
    - die **Standardinstanz**verwenden.
    - auf **Manuelles Failover**festgelegt sein.  

        > [!TIP]  
        >  System Center Configuration Manager unterstützt bei Festlegung auf „Automatisches Failover“ die Verwendung der Verfügbarkeitsgruppenreplikate. „Manuelles Failover“ muss allerdings festgelegt werden, wenn Sie das Setup ausführen, um die Verwendung der Standortdatenbank in der Verfügbarkeitsgruppe anzugeben, und wenn Sie Updates für Configuration Manager installieren (nicht nur Updates, die Sie auf die Standortdatenbank anwenden).  

  **Einschränkungen für Verfügbarkeitsgruppen**
   - Basis-Verfügbarkeitsgruppen (mit SQL Server 2016 Standard Edition eingeführt) werden nicht unterstützt. Dies ist darauf zurückzuführen, dass Basis-Verfügbarkeitsgruppen den Lesezugriff auf sekundäre Replikate – und somit eine Voraussetzung für die Verwendung mit Configuration Manager – nicht unterstützen. Weitere Informationen finden Sie unter [Basis-Verfügbarkeitsgruppen (Always On-Verfügbarkeitsgruppen)](https://msdn.microsoft.com/en-us/library/mt614935.aspx).

   - Verfügbarkeitsgruppen werden nur für die Standortdatenbank, aber nicht für die Softwareupdatedatenbank oder Berichtsdatenbank unterstützt.   
   - Wenn Sie eine verfügbarkeitsgruppe verwenden, müssen Sie Ihren Berichterstattungspunkt manuell so konfigurieren, damit dieser das aktuelle primäre Replikat und nicht den Verfügbarkeitsgruppenlistener verwendet. Wenn ein Failover des primären Replikats auf ein anderes Replikat durchgeführt wird, müssen Sie den Berichterstattungspunkt für das neue primäre Replikat umkonfigurieren.  
   - Vor der Installation von Updates, z.B. Version 1606, stellen Sie sicher, dass die Verfügbarkeitsgruppe auf manuelles Failover festgelegt ist. Nachdem der Standort aktualisiert wurde, können Sie wieder auf automatisches Failover umstellen.



 **Erforderliche Berechtigungen zum Konfigurieren und Verwenden von Verfügbarkeitsgruppen:**  

-   Das Computerkonto des Standortservers muss Mitglied der Gruppe **Lokale Administratoren** auf allen Computern sein, die zur Verfügbarkeitsgruppe gehören.  

#### <a name="to-configure-an-availability-group-to-host-a-site-database"></a>So konfigurieren Sie eine Verfügbarkeitsgruppe zum Hosten einer Standortdatenbank  

1.  Verwenden Sie den folgenden Befehl, um den Configuration Manager-Standort zu beenden:  
     **Preinst.exe /stopsite**  

     Weitere Informationen zur Verwendung von Preinst.exe finden Sie unter [Hierarchiewartungstool (Preinst.exe) für System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Ändern Sie das Sicherungsmodell der Standortdatenbank von **EINFACH** in **VOLLSTÄNDIG**.  

     Siehe [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) in der SQL Server-Dokumentation. (Verfügbarkeitsgruppen unterstützen nur VOLLSTÄNDIG).  

3.  Verwenden Sie auf dem Server, auf dem das primäre Replikat der Gruppe gehostet wird, den **Assistenten für neue Verfügbarkeitsgruppen** zum Erstellen der Verfügbarkeitsgruppe. Gehen Sie im Assistenten so vor:  

    -   Wählen Sie auf der Seite **Datenbank auswählen** die Datenbank für Ihren Configuration Manager-Standort aus.  

    -   Konfigurieren Sie auf der Seite **Replikate angeben** Folgendes:  

        -   **Replikate**: Geben Sie die Server an, die die sekundären Replikate hosten sollen.  

        -   **Listener**: Geben Sie den **DNS-Listenernamen** als vollständigen DNS-Namen wie **&lt;Listener_Server>.fabrikam.com** ein. Dieser Vorgang wird verwendet, wenn Sie Configuration Manager für die Verwendung der Datenbank in der Verfügbarkeitsgruppe konfigurieren.

    -   Wählen Sie auf der Seite **Anfängliche Datensynchronisierung auswählen** die Einstellung **Vollständig**aus. Nachdem der Assistent die Verfügbarkeitsgruppe erstellt hat, sichert er die primäre Datenbank und das Transaktionsprotokoll und stellt beide auf jedem Server wieder her, auf denen ein sekundäres Replikat gehostet wird. Wenn Sie diesen Schritt nicht verwenden, müssen Sie eine Kopie der Standortdatenbank auf allen Servern wiederherstellen, auf denen ein sekundäres Replikat gehostet wird, und die Datenbank manuell mit der Gruppe verknüpfen.  

    Weitere Informationen finden Sie unter [Verwenden des Assistenten für Verfügbarkeitsgruppen](https://msdn.microsoft.com/library/hh403415\(v=sql.120\).aspx) in der SQL Server-Dokumentation.  

4.  Nach der Konfiguration der Verfügbarkeitsgruppe konfigurieren Sie die Standortdatenbank für das primäre Replikat mit der **TRUSTWORTHY** -Eigenschaft, und **aktivieren Sie dann die CLR-Integration**. Informationen zur entsprechenden Konfiguration finden Sie unter [TRUSTWORTHY-Datenbankeigenschaft](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) und  [Aktivieren der CLR-Integration](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx) in der SQL Server-Dokumentation.  

5.  Führen Sie die folgenden Schritte aus, um alle sekundären Replikate in der Verfügbarkeitsgruppe zu konfigurieren:  

    1.  Führen Sie für das aktuelle primäre Replikat ein manuelles Failover in ein sekundäres Replikat aus. Siehe [Ausführen eines geplanten manuellen Failovers einer Verfügbarkeitsgruppe](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) in der SQL Server-Dokumentation.  

    2.  Konfigurieren Sie die Datenbank für das neue primäre Replikat mit der **TRUSTWORTHY** -Eigenschaft, und **aktivieren Sie dann die CLR-Integration**.  

6.  Nachdem alle Replikate zu primären Replikaten höher gestuft und die Datenbanken konfiguriert wurden, ist die Verfügbarkeitsgruppe für die Verwendung mit Configuration Manager bereit.  





##  <a name="bkmk_direct"></a> Verschieben einer Standortdatenbank zu einer Verfügbarkeitsgruppe  
 Sie können eine Standortdatenbank für einen zuvor installierten Standort in eine Verfügbarkeitsgruppe verschieben. Sie müssen zuerst die Verfügbarkeitsgruppe erstellen und anschließend die Datenbank für den Vorgang in der Verfügbarkeitsgruppe konfigurieren.  

 Zum Ausführen dieses Verfahrens muss das Computerkonto für die Ausführung des Setups von Configuration Manager Mitglied der Gruppe **Lokale Administratoren** auf allen Computern sein, die zur Verfügbarkeitsgruppe gehören.  

#### <a name="to-move-a-site-database-to-an-availability-group"></a>So verschieben Sie eine Standortdatenbank zu einer Verfügbarkeitsgruppe  

1.  Führen Sie das **Configuration Manager-Setup** unter **&lt;Installationsordner des Configuration Manager-Standorts\>\BIN\X64\setup.exe** aus.  

2.  Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen**aus, und klicken Sie dann auf **Weiter**.  

3.  Wählen Sie die Option **SQL Server-Konfiguration ändern** aus, und klicken Sie auf **Weiter**.  

4.  Konfigurieren Sie Folgendes für die Standortdatenbank neu:  

    -   **SQL Server-Name** : Geben Sie den virtuellen Namen für den Verfügbarkeitsgruppenlistener ein, den Sie beim Erstellen der Verfügbarkeitsgruppe konfiguriert haben. Der virtuelle Name sollte ein vollständiger DNS-Name sein, wie z.B. **&lt;Endpunktserver\>.fabrikam.com**.  

    -   **Instanz:** Dieser Wert muss leer sein, um die Standardinstanz für den verfügbaren Verfügbarkeitsgruppenlistener der Verfügbarkeitsgruppe anzugeben.  Wenn die aktuellen Datenbank auf einer benannten Instanz installiert ist, ist die benannte Instanz aufgeführt und muss gelöscht werden.  

    -   **Datenbank:** Belassen Sie den angezeigten Namen unverändert. Dies ist der Name der aktuellen Standortdatenbank.  

5.  Nachdem Sie die Informationen zum neuen Speicherort der Datenbank bereitgestellt haben, schließen Sie das Setup mit der üblichen Vorgehensweise und den normalen Konfigurationen ab.  

##  <a name="bkmk_change"></a> Hinzufügen oder Entfernen von Mitgliedern einer aktiven Verfügbarkeitsgruppe  
 Sobald Configuration Manager eine in einer Verfügbarkeitsgruppe gehostete Standortdatenbank verwendet, können Sie ein Replikatsmitglied entfernen oder ein weiteres hinzufügen (ohne dabei einen primären und zwei sekundäre Knoten zu überschreiten).  

#### <a name="to-add-a-new-replica-member"></a>So fügen Sie ein neue Replikatsmitglied hinzu  

1.  Fügen Sie den neuen Server als sekundäres Replikat der Verfügbarkeitsgruppe hinzu. Siehe  [Hinzufügen eines sekundären Replikats zu einer Verfügbarkeitsgruppe (SQL Server)](https://msdn.microsoft.com/library/hh213247\(v=sql.120\).aspx)in der SQL Server-Dokumentationsbibliothek.  

2.  Beenden Sie den Configuration Manager-Standort, indem Sie **Preinst.exe /stopsite** ausführen. Informationen hierfür finden Sie unter [Hierarchiewartungstool (Preinst.exe) für System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

3.  Konfigurieren Sie alle sekundären Replikate. Führen Sie die folgenden Schritte für alle sekundären Replikate in der Verfügbarkeitsgruppe aus:  

    1.  Führen Sie für das primäre Replikat ein manuelles Failover in ein neues sekundäres Replikat aus. Siehe [Ausführen eines geplanten manuellen Failovers einer Verfügbarkeitsgruppe](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) in der SQL Server-Dokumentation.  

    2.  Konfigurieren Sie die Datenbank auf dem neuen Server mit der „Trustworthy“-Eigenschaft, und aktivieren Sie die CLR-Integration. Siehe [TRUSTWORTHY-Datenbankeigenschaft](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) und  [Aktivieren der CLR-Integration](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx)in der SQL Server-Dokumentation.  

4.  Starten Sie den Standort neu, indem Sie die Dienste Standortkomponenten-Manager (**sitecomp**) und **SMS_Executive** starten.  

#### <a name="to-remove-a-replica-member-from-the-availability-group"></a>So entfernen ein Replikatsmitglied aus der Verfügbarkeitsgruppe  

-   Befolgen Sie die Anweisungen unter [Entfernen eines sekundären Replikats aus einer Verfügbarkeitsgruppe](https://msdn.microsoft.com/library/hh213149\(v=sql.120\).aspx) in der SQL Server-Dokumentation.  

##  <a name="bkmk_remove"></a> Verschieben der Standortdatenbank aus einer Verfügbarkeitsgruppe zurück in eine einzelne Instanz von SQL Server  
 Führen Sie das folgende Verfahren aus, wenn Sie Ihre Standortdatenbank nicht mehr in einer Verfügbarkeitsgruppe hosten möchten.  

#### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>So verschieben Sie die Standortdatenbank aus einer Verfügbarkeitsgruppe zurück in eine einzelne Instanz von SQL Server  

1.  Beenden Sie den Configuration Manager-Standort mithilfe des folgenden Befehls:  
     **Preinst.exe /stopsite**.  Weitere Informationen finden Sie unter [Hierarchiewartungstool (Preinst.exe) für System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Verwenden Sie SQL Server, um eine vollständige Sicherung Ihrer Standortdatenbank anhand des primären Replikats zu erstellen. Informationen zum Ausführen dieses Schritts finden Sie unter [Erstellen einer vollständigen Datenbanksicherung](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) in der SQL Server-Dokumentation.  

3.  Wenn der Server, der das primäre Replikat für die Verfügbarkeitsgruppe hostet, jetzt die einzelne Instanz der Standortdatenbank hostet, können Sie diesen Schritt überspringen:  

    -   Verwenden Sie SQL Server, um die Sicherung der Standortdatenbank auf dem Server wiederherzustellen, der die Standortdatenbank hostet.  Siehe [Wiederherstellen einer Datenbanksicherung (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx) in der SQL Server-Dokumentation.  

4.  Ändern Sie für die wiederhergestellte Datenbank das Sicherungsmodell für die Standortdatenbank von **VOLLSTÄNDIG** in **EINFACH**.  Siehe [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) in der SQL Server-Dokumentation.  

5.  Führen Sie das **Configuration Manager-Setup** unter **&lt;Installationsordner des Configuration Manager-Standorts\>\BIN\X64\setup.exe** aus.  

6.  Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen**aus, und klicken Sie dann auf **Weiter**.  

7.  Wählen Sie die Option **SQL Server-Konfiguration ändern** aus, und klicken Sie auf **Weiter**.  

8.  Konfigurieren Sie Folgendes für die Standortdatenbank neu:  

    -   **Name des SQL-Servers** : Geben Sie den Namen des Servers ein, auf dem nun die Standortdatenbank gehostet wird.  

    -   **Instanz:** Geben Sie die benannte Instanz an, die die Standortdatenbank hostet. Lassen Sie dieses Feld leer, wenn sich die Datenbank in der Standardinstanz befindet.  

    -   **Datenbank:** Belassen Sie den angezeigten Namen unverändert. Dies ist der Name der aktuellen Standortdatenbank.  

9. Nachdem Sie die Informationen zum neuen Speicherort der Datenbank bereitgestellt haben, schließen Sie das Setup mit der üblichen Vorgehensweise und den normalen Konfigurationen ab. Nach Abschluss des Setups wird der Standort neu gestartet und beginnt mit der Nutzung des neuen Speicherorts der Datenbank.  

10. Zur Bereinigung der Server, die Mitglied der Verfügbarkeitsgruppe waren, befolgen Sie die Anleitung unter [Entfernen einer Verfügbarkeitsgruppe](https://msdn.microsoft.com/library/ff878113\(v=sql.120\).aspx) in der SQL Server-Dokumentation.

