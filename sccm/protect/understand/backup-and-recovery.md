---
title: Sicherung und Wiederherstellung | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Standorte bei Ausfall oder Datenverlust in System Center Configuration Manager sichern und wiederherstellen.
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: ea6668ee7ee6b209b659426a0dc2c0be605ceaf1
ms.lasthandoff: 03/27/2017

---

# <a name="backup-and-recovery"></a>Sicherung und Wiederherstellung

*Gilt für: System Center Configuration Manager (Current Branch)*

Bereiten Sie Sicherungs- und Wiederherstellungs-Ansätze vor, um Datenverluste zu vermeiden. Für Configuration Manager-Standorte kann ein Ansatz für die Sicherung und Wiederherstellung dazu beitragen, Standorte und Hierarchien schneller und mit geringstem Datenverlust wiederherzustellen. In den folgenden Abschnitten wird erläutert, wie Sie Standorte sichern und bei einem Ausfall oder Datenverlust wiederherstellen.  



- [Sichern eines Configuration Manager-Standorts](#BKMK_SiteBackup)   

  - [Sicherungswartungstask](#BKMK_BackupMaintenanceTask)   

  - [Verwenden von Data Protection Manager zur Sicherung der Standortdatenbank](#BKMK_DPMBackup)   

  -  [Archivieren der Sicherungsmomentaufnahme](#BKMK_ArchivingBackupSnapshot)   

  -  [Verwenden der Datei „AfterBackup.bat“](#BKMK_UsingAfterBackup)   

  -  [Zusätzliche Sicherungstasks](#BKMK_SupplementalBackup)   

-  [Wiederherstellen eines Configuration Manager-Standorts](#BKMK_RecoverSite)   

  -   [Bestimmen der Wiederherstellungsoptionen](#BKMK_DetermineRecoveryOptions)   

         -   [Wiederherstellungsoptionen für den Standortserver](#BKMK_SiteServerRecoveryOptions)   

         -   [Wiederherstellungsoptionen für die Standortdatenbank](#BKMK_SiteDatabaseRecoveryOption)   

         -   [Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server](#bkmk_SQLretention)   

         -   [Prozess zum erneuten Initialisieren der Standortdaten oder der globalen Daten](#bkmk_reinit)   

         -   [Wiederherstellungsszenarien für die Standortdatenbank](#BKMK_SiteDBRecoveryScenarios)  

  -   [Skriptdateischlüssel für unbeaufsichtigte Standortwiederherstellung](#BKMK_UnattendedSiteRecoveryKeys)  

  -   [Aufgaben nach der Wiederherstellung](#BKMK_PostRecovery)  

  -   [Wiederherstellen eines sekundären Standorts](#BKMK_RecoverSecondarySite)  

-   [SMS-Writer-Dienst](#BKMK_SMSWriterService)  

> [!NOTE]  
>  Wenn Sie eine SQL Server Always On-Verfügbarkeitsgruppe zum Hosten der Standortdatenbank verwenden, ändern Sie Ihre Sicherungs- und Wiederherstellungspläne wie im Abschnitt [Änderungen bei Sicherung und Wiederherstellung bei Verwendung einer SQL Server Always On-Verfügbarkeitsgruppe](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#bkmk_BnR) des Themas [SQL Server Always On für eine hoch verfügbare Standortdatenbank für System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) beschrieben.  

##  <a name="BKMK_SiteBackup"></a> Sichern eines Configuration Manager-Standorts  
 Configuration Manager hat einen Sicherungswartungstask:  

-   Wird nach einem Zeitplan ausgeführt  

-   Sichert die Standortdatenbank  

-   Sichert bestimmte Registrierungsschlüssel  

-   Sichert bestimmte Ordner und Dateien  

-   Sichert den Ordner **CD.Latest** (Siehe [Der Ordner „CD.Latest“ für System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md))  

 Planen Sie die Ausführung des Standardtasks für die Standortsicherung mindestens alle 5 Tage. Der Grund dafür ist, dass Configuration Manager einen Zeitraum für die [Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server](#bkmk_SQLretention) von fünf Tagen verwendet.  

 Zur Vereinfachung des Sicherungsprozesses können Sie eine Datei **AfterBackup.bat** erstellen, um nach der erfolgreichen Ausführung des Sicherungswartungstasks weitere Aktionen automatisch auszuführen. Die Datei „AfterBackup.bat“ wird normalerweise zur Archivierung der Sicherungsmomentaufnahme an einem sicheren Speicherort verwendet. Sie können mit der Datei „AfterBackup.bat“ auch Dateien in den Sicherungsordner kopieren und andere zusätzliche Sicherungstasks starten.

In den folgenden Abschnitten erfahren Sie, wie Sie eine Configuration Manager-Sicherungsstrategie erstellen.  

> [!NOTE]  
>  Configuration Manager kann die Standortdatenbank aus dem Configuration Manager-Sicherungswartungstask oder aus der Standortdatenbanksicherung wiederherstellen, die Sie mit einem anderen Prozess erstellt haben. Beispielsweise können Sie die Standortdatenbank anhand einer Sicherung wiederherstellen, die im Rahmen des Microsoft SQL Server-Wartungsplans erstellt wurde. Sie können die Standortdatenbank anhand einer Sicherung wiederherstellen, die mithilfe von System Center 2012 Data Protection Manager (DPM) erstellt wurde. Weitere Informationen finden Sie unter [Verwenden von Data Protection Manager zur Sicherung der Standortdatenbank](#BKMK_DPMBackup).  

###  <a name="BKMK_BackupMaintenanceTask"></a> Sicherungswartungstask  
 Durch Planen des vordefinierten Wartungstasks „Standortserver sichern“ können Sie die Sicherung von Configuration Manager-Standorten automatisieren. Sie können einen Standort der zentralen Verwaltung und einen primären Standort sichern. Bei sekundären Standorten oder Standortsystemservern hingegen wird eine Sicherung nicht unterstützt. Wenn der Configuration Manager-Sicherungsdienst ausgeführt wird, läuft dieser Vorgang den in der Sicherungssteuerungsdatei (**&lt;Configuration Manager-Installationsordner\>\Inboxes\Smsbkup.box\Smsbkup.ctl**) definierten Anweisungen entsprechend ab. Sie können die Sicherungssteuerungsdatei ändern, um das Verhalten des Sicherungsdienstes zu ändern. Informationen zum Status der Standortsicherung werden in die Datei **Smsbkup.log** geschrieben. Diese Datei wird in dem Zielordner erstellt, den Sie in den Eigenschaften des Wartungstasks „Standortserver sichern“ angeben.  


##### <a name="to-enable-the-site-backup-maintenance-task"></a>So aktivieren Sie den Wartungstask zur Standortsicherung  

1.  Öffnen Sie in der Configuration Manager-Konsole **Verwaltung** > **Standortkonfiguration**.  

     \> **Standorte**.  

2.  Wählen Sie den Standort aus, an dem Sie den Wartungstask zur Standortsicherung aktivieren möchten.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** die **Standortwartungstasks**.  

4.  Wählen Sie **Standortserver sichern**  >  **Bearbeiten** aus.  

5.  Wählen Sie **Diese Aufgabe aktivieren** > **Pfade festlegen** aus, um das Sicherungsziel anzugeben. Hierzu stehen Ihnen folgende Optionen zur Verfügung:  

    > [!IMPORTANT]  
    >  Speichern Sie die Dateien an einem sicheren Ort, um einer Manipulation der Sicherungsdateien vorzubeugen. Der sicherste Pfad für eine Sicherung verweist auf ein lokales Laufwerk, sodass Sie NTFS-Dateisystemberechtigungen für den Ordner einrichten können. Configuration Manager verschlüsselt nicht die Sicherungsdaten, die im den Sicherungspfad gespeichert sind.  

    -   **Lokales Laufwerk auf Standortserver für Standortdaten und -datenbank**: Bei Auswahl dieser Option werden die Sicherungsdateien für den Standort und die Standortdatenbank im angegebenen Pfad auf dem lokalen Laufwerk des Standortservers gespeichert. Sie müssen den lokalen Ordner erstellen, bevor der Sicherungstask ausgeführt wird. Das lokale Systemkonto auf dem Standortserver muss über die NTFS-Dateisystemberechtigung **Schreiben** für den lokalen Ordner verfügen, der für die Sicherung des Standorts vorgesehen ist. Das lokale Systemkonto auf dem Computer, auf dem SQL Server ausgeführt wird, muss über die NTFS-Berechtigung **Schreiben** für den Ordner verfügen, der für die Sicherung der Standortdatenbank vorgesehen ist.  

    -   **Netzwerkpfad (UNC-Name) für Standortdaten und -datenbank**: Bei Auswahl dieser Option werden die Sicherungsdateien für den Standort und die Standortdatenbank im angegebenen UNC-Pfad gespeichert. Sie müssen die Freigabe erstellen, bevor der Sicherungstask ausgeführt wird. Das Computerkonto des Standortservers sowie das Computerkonto von SQL Server, so SQL Server auf einem anderen Computer installiert ist, müssen die NTFS-Berechtigung **Schreiben** sowie Freigabeberechtigungen für den freigegebenen Netzwerkordner aufweisen.  

    -   **Lokale Laufwerke auf dem Standortserver und SQL Server**: Bei Auswahl dieser Option werden die Sicherungsdateien für den Standort im angegebenen Pfad auf dem lokalen Laufwerk des Standortservers gespeichert, und die Sicherungsdateien für die Standortdatenbank werden im angegebenen Pfad auf dem lokalen Laufwerk des Standortdatenbankservers gespeichert. Sie müssen die lokalen Ordner erstellen, bevor der Sicherungstask ausgeführt wird. Für das Computerkonto des Standortservers müssen die NTFS-Berechtigungen **Schreiben** für den Ordner vorliegen, den Sie auf dem Standortserver erstellen. Für das Computerkonto des SQL Servers müssen die NTFS-Berechtigungen **Schreiben** für den Ordner vorliegen, den Sie auf dem Standortdatenbankserver erstellen. Diese Option ist nur verfügbar, wenn die Standortdatenbank nicht auf dem Standortserver installiert ist.  

    > [!NOTE]  
    >    - Die Option zum Durchsuchen des Sicherungsziels ist nur verfügbar, wenn Sie den UNC-Pfad des Sicherungsziels angeben.

    > - Der Ordner- oder Freigabename, der für das Sicherungsziel verwendet wird, darf keine Unicode-Zeichen enthalten.  


6.  Konfigurieren Sie einen Zeitplan für den Standortsicherungstask. Empfehlenswert ist ein Sicherungszeitplan, der außerhalb der Arbeitszeit liegt. Falls Sie über eine Hierarchie verfügen, empfiehlt sich ein Zeitplan, der mindestens zweimal pro Woche ausgeführt wird. Auf diese Weise bleibt bei einem Standortausfall ein Maximum an Daten erhalten.  

    Wenn Sie die Configuration Manager-Konsole auf dem gleichen Standortserver ausführen, den Sie für die Sicherung konfigurieren, wird vom Wartungstask „Standortserver sichern“ die lokale Zeit für den Zeitplan verwendet. Wenn Sie die Configuration Manager-Konsole auf einem Computer außerhalb des Standorts ausführen, den Sie für die Sicherung konfigurieren, wird vom Wartungstask „Standortserver sichern“ UTC (Coordinated Universal Time, koordinierte Weltzeit) für den Zeitplan verwendet.  

7.  Geben Sie an, ob eine Warnung generiert werden soll, wenn beim Standortsicherungstask ein Fehler auftritt, und klicken Sie auf **OK**. Klicken Sie anschließend auf **OK**. Wenn diese Option ausgewählt ist, wird von Configuration Manager bei einem Sicherungsfehler eine kritische Warnung generiert. Details zu dieser Warnung können Sie im Arbeitsbereich **Überwachung** im Knoten **Warnungen** einsehen.  

 Überprüfen Sie als nächstes, ob der Wartungstask „Standortserver sichern“ ausgeführt wird, um sicherzustellen, dass die Sicherungen erstellt werden.  

##### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>So überprüfen Sie, ob der Wartungstask „Standortserver sichern“ ausgeführt wird  

-   Überprüfen Sie wie folgt, ob der Wartungstask zur Standortsicherung ausgeführt wird:  

    -   Überprüfen Sie den Zeitstempel auf den Dateien im Sicherungszielordner, die vom Task erstellt wurden. Überprüfen Sie, ob der Zeitstempel aktualisiert wurde und die Zeitangabe mit der Zeit übereinstimmt, zu der die Ausführung des Tasks laut Zeitplan zuletzt vorgesehen war.  

    -   Prüfen Sie im Arbeitsbereich **Überwachung** im Knoten **Komponentenstatus** die Statusmeldungen für SMS_SITE_BACKUP. Wenn die Standortsicherung erfolgreich abgeschlossen ist, wird die Meldungs-ID 5035 angezeigt. Dies bedeutet, dass die Standortsicherung ohne Fehler abgeschlossen wurde.  

    -   Wenn vom Wartungstask „Standortserver sichern“ bei einem Sicherungsfehler konfigurationsgemäß eine Warnung generiert wird, können Sie die Systemfehler im Arbeitsbereich **Überwachung** im Knoten **Warnungen** überprüfen.  

    -   Prüfen Sie die Datei „Smsbkup.log“ unter „&lt;*Configuration Manager-Installationsordner*>\Logs“ auf Warnungen und Fehler. Wenn die Standortsicherung erfolgreich abgeschlossen ist, wird `Backup completed` zusammen mit einem Zeitstempel und der Meldungs-ID `STATMSG: ID=5035`angezeigt.  

    > [!TIP]  
    >  Wenn beim Sicherungswartungstask ein Fehler auftritt, können Sie den Task durch Anhalten und Neustarten des Dienstes SMS_SITE_BACKUP neu starten.  

###  <a name="BKMK_DPMBackup"></a> Verwenden von Data Protection Manager zur Sicherung der Standortdatenbank  
 Sie können die Standortdatenbank mit System Center 2012 Data Protection Manager (DPM) sichern. Sie müssen in DPM eine neue Schutzgruppe für den Standortdatenbankcomputer erstellen. Auf der Seite **Gruppenmitglieder auswählen** des Assistenten zum Erstellen einer neuen Schutzgruppe wählen Sie den SMS-Writer-Dienst aus der Datenquellenliste und anschließend die Standortdatenbank als geeignetes Mitglied aus. Weitere Informationen zur Verwendung DPM zur Sicherung Ihrer Standortdatenbank finden Sie in der [Data Protection Manager-Dokumentationsbibliothek](http://go.microsoft.com/fwlink/?LinkId=272772) auf der TechNet-Webseite.  

> [!IMPORTANT]  
>  Configuration Manager unterstützt nicht die DPM-Sicherung für ein SQL Server-Cluster, das eine benannte Instanz verwendet, wohl aber eine DPM-Sicherung auf einem SQL Server-Cluster, das die Standardinstanz von SQL Server verwendet.  

 Nachdem Sie die Standortdatenbank wiederhergestellt haben, befolgen Sie die Schritte im Setup, um den Standort wiederherzustellen. Wählen Sie die Wiederherstellungsoption **Manuell wiederhergestellte Standortdatenbank verwenden** aus, um die Standortdatenbank zu verwenden, die Sie mithilfe von Data Protection Manager wiederhergestellt haben.  

###  <a name="BKMK_ArchivingBackupSnapshot"></a> Archivieren der Sicherungsmomentaufnahme  
 Bei der ersten Ausführung des Wartungstasks „Standortserver sichern“ wird eine Sicherungsmomentaufnahme erstellt, mit der Sie Ihren Standortserver nach einem Fehler wiederherstellen können. Wenn der Sicherungstask im Verlauf späterer Zyklen erneut ausgeführt wird, erstellt er jeweils einen neuen Sicherungssnapshot, mit dem der vorherige Snapshot überschrieben wird. Für einen Standort gibt es daher immer nur eine Sicherungsmomentaufnahme, und es ist nicht möglich, eine frühere Sicherungsmomentaufnahme abzurufen.  

 Aus den folgenden Gründen wird empfohlen, mehrere Archive der Sicherungsmomentaufnahme aufzubewahren:  

-   Es kommt häufig vor, dass Sicherungsmedien ausfallen, verlegt werden oder nur eine unvollständige Sicherung enthalten. Das Wiederherstellen eines ausgefallenen eigenständigen primären Standorts anhand einer älteren Sicherung ist besser als das Wiederherstellen ohne Sicherung. Bei einem Standortserver in einer Hierarchie muss die Sicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server liegen. Andernfalls ist die Sicherung nicht erforderlich.  

-   Eine Beschädigung im Standort kann über mehrere Sicherungszyklen hinweg unentdeckt bleiben. Sie müssen möglicherweise eine Sicherungsmomentaufnahme verwenden, die vor der Beschädigung des Standorts erstellt wurde. Dies gilt für einen eigenständigen primären Standort und Standorte in einer Hierarchie, bei denen die Sicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server liegt.  

-   Für den Standort gibt es möglicherweise keine Sicherungsmomentaufnahme, beispielsweise weil beim Wartungstask „Standortserver sichern“ ein Fehler aufgetreten ist. Da der Sicherungstask den vorherigen Sicherungssnapshot entfernt, bevor er mit dem Sichern der aktuellen Daten beginnt, gibt es zeitweise keinen gültigen Sicherungssnapshot.  

###  <a name="BKMK_UsingAfterBackup"></a> Verwenden der Datei „AfterBackup.bat“  
 Nach der erfolgreichen Sicherung des Standorts wird vom Task „Standortserver sichern“ automatisch versucht, eine Datei namens AfterBackup.bat auszuführen. Sie müssen die Datei „AfterBackup.bat“ manuell in „&lt;*Configuration Manager-Installationsordner*>\Inboxes\Smsbkup“ erstellen. Wenn eine Datei „AfterBackup.bat“ vorhanden ist und sich im richtigen Ordner befindet, wird sie nach Abschluss des Sicherungstasks automatisch ausgeführt. Mit der Datei AfterBackup.bat können Sie die Sicherungsmomentaufnahme am Ende jedes Sicherungsvorgangs archivieren und automatisch andere nach der Sicherung erforderliche Tasks ausführen, die nicht zum Wartungstask „Standortserver sichern“ gehören. Mit der Datei AfterBackup.bat werden die Archivierungs- und Sicherungsvorgänge integriert. Dadurch wird sichergestellt, dass jede neue Sicherungsmomentaufnahme archiviert wird. Wenn die Datei AfterBackup.bat nicht vorhanden ist, wird sie vom Sicherungstask übersprungen. Dies hat keine Auswirkungen auf den Sicherungsvorgang. Prüfen Sie im Arbeitsbereich **Überwachung** im Knoten **Komponentenstatus** die Statusmeldungen für SMS_SITE_BACKUP. Daran erkennen Sie, ob die Datei "AfterBackup.bat" vom Standortsicherungstask erfolgreich ausgeführt wurde. Wenn die Befehlsdatei „AfterBackup.bat“ erfolgreich gestartet wurde, wird die Meldungs-ID 5040 angezeigt.  

> [!TIP]  
>  Sie müssen ein Kopierbefehlstool wie Robocopy in der Batchdatei verwenden, um die Datei „AfterBackup.bat“ zum Archivieren der Sicherungsdateien für den Standortserver zu erstellen. Beispielsweise können Sie die Datei "AfterBackup.bat" erstellen und der ersten Zeile Folgendes hinzufügen: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`. Weitere Informationen zu Robocopy finden Sie in der Befehlszeilenreferenz unter [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408) .  

 Die Datei AfterBackup.bat ist zwar zum Archivieren von Sicherungsmomentaufnahmen vorgesehen, Sie aber können auch eine Datei AfterBackup.bat erstellen, um am Ende jedes Sicherungsvorgangs zusätzliche Tasks auszuführen.  

###  <a name="BKMK_SupplementalBackup"></a> Zusätzliche Sicherungstasks  
 Mit dem Wartungstask „Standortserver sichern“ wird eine Sicherungsmomentaufnahme für die Standortserverdateien und die Standortdatenbank erstellt. Beim Erstellen einer Sicherungsstrategie müssen Sie aber noch andere Elemente berücksichtigen, die nicht gesichert werden. In den folgenden Abschnitten erfahren Sie, wie Sie eine Configuration Manager-Sicherungsstrategie vervollständigen.  

#### <a name="back-up-custom-reporting-services-reports"></a>Sichern benutzerdefinierter Reporting Services-Berichte  
 Wenn Sie vordefinierte Reporting Services-Berichte geändert oder benutzerdefinierte Reporting Services-Berichte erstellt haben, stellt die Sicherung der Berichtsserver-Datenbankdateien eine wichtige Komponente Ihrer Sicherungsstrategie dar. Die Berichtsserver-Sicherung muss eine Sicherung der Quelldateien für Berichte und Modelle, Verschlüsselungsschlüssel, benutzerdefinierte Assemblys oder Erweiterungen, Konfigurationsdateien, in benutzerdefinierten Berichten verwendete benutzerdefinierte SQL Server-Ansichten, benutzerdefinierte gespeicherte Prozeduren usw. umfassen.  

> [!IMPORTANT]  
>  Wenn Configuration Manager auf eine neuere Version aktualisiert wird, werden die vordefinierten Berichte möglicherweise von neuen Berichten überschrieben. Wenn Sie einen vordefinierten Bericht ändern, sichern Sie ihn, und stellen Sie den Bericht dann in Reporting Services wieder her.  

 Weitere Informationen zum Sichern benutzerdefinierter Berichte in Reporting Services finden Sie unter [Sicherungs- und Wiederherstellungsvorgänge für eine Reporting Services-Installation](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) in der Onlinedokumentation zu SQL Server 2014.  

#### <a name="backup-content-files"></a>Sichern von Inhaltsdateien  
 Die Inhaltsbibliothek in Configuration Manager ist der Ort, an dem alle Inhaltsdateien für Softwareupdates, Anwendungen, Betriebssystembereitstellungen usw. gespeichert werden. Sie befindet sich auf dem Standortserver und an jedem Verteilungspunkt. Vom Wartungstask „Standortserver sichern“ wird keine Sicherung der Inhaltsbibliothek oder der Paketquelldateien ausgeführt. Beim Ausfall eines Standortservers werden die Informationen zu den Dateien der Inhaltsbibliothek in der Standortdatenbank wiederhergestellt. Sie müssen jedoch die Inhaltsbibliothek sowie die Paketquelldateien auf dem Standortserver wiederherstellen.  

-   **Inhaltsbibliothek**: Die Inhaltsbibliothek muss wiederhergestellt werden, damit Sie Inhalt erneut an Verteilungspunkte verteilen können. Wenn Sie die Neuverteilung des Inhalts starten, werden die Dateien von Configuration Manager aus der Inhaltsbibliothek auf dem Standortserver auf die Verteilungspunkte kopiert. Die Inhaltsbibliothek für den Standortserver befindet sich im Ordner „SCCMContentLib“. Dieser Ordner wiederum befindet sich in der Regel auf dem Laufwerk, auf dem zum Zeitpunkt der Standortinstallation am meisten freier Speicher verfügbar war.  

-   **Paketquelldateien**: Die Paketquelldateien müssen wiederhergestellt werden, damit Sie ein Update des Inhalts an Verteilungspunkten ausführen können. Wenn Sie ein Inhaltsupdate starten, werden neue oder geänderte Dateien von Configuration Manager aus der Paketquelle in die Inhaltsbibliothek kopiert. Von dort werden die Dateien auf die zugeordneten Verteilungspunkte kopiert. Sie können die folgende Abfrage in SQL Server ausführen, um den Quellspeicherort für alle Pakete und Anwendungen zu ermitteln: `SELECT * FROM v_Package`. Sie können den Paketquellstandort anhand der ersten drei Zeichen der Paket-ID identifizieren. Wenn beispielsweise die Paket-ID „CEN00001“ lautet, ist „CEN“ der Standortcode für den Quellstandort. Paketquelldateien müssen an den gleichen Speicherort wiederhergestellt werden wie vor dem Fehler.  

 Achten Sie darauf, bei der Dateisystemsicherung für den Standortserver sowohl die Inhaltsbibliothek als auch die Paketquellspeicherorte einzuschließen.  

#### <a name="back-up-custom-software-updates"></a>Sichern benutzerdefinierter Softwareupdates  
 System Center Updates Publisher 2011 ist ein eigenständiges Tool, mit dem Sie benutzerdefinierte Softwareupdates in Windows Server Update Services (WSUS) veröffentlichen, die Softwareupdates mit Configuration Manager synchronisieren, die Konformität der Softwareupdates bewerten sowie die benutzerdefinierten Softwareupdates für Clients bereitstellen können. Updates Publisher verwendet eine lokale Datenbank für das Softwareupdaterepository. Wenn Sie den Updates Publisher zur Verwaltung benutzerdefinierter Softwareupdates verwenden, legen Sie fest, ob die Updates Publisher-Datenbank in Ihrem Sicherungsplan beinhaltet sein muss. Weitere Informationen zu Updates Publisher finden Sie unter [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) in der System Center TechNet-Bibliothek.  

 Gehen Sie wie folgt vor, um die Updates Publisher-Datenbank zu sichern.  

###### <a name="to-back-up-the-updates-publisher-2011-database"></a>So sichern Sie die Updates Publisher 2011-Datenbank  

1.  Suchen Sie auf dem Computer, auf dem Updates Publisher ausgeführt wird, die Updates Publisher-Datenbankdatei („Scupdb.sdf“) in „%*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\“. Für jeden Benutzer, der Updates Publisher ausführt, gibt es eine eigene Datenbankdatei.  

2.  Kopieren Sie die Datenbankdatei in das Sicherungsziel. Wenn das Sicherungsziel beispielsweise „E:\ConfigMgr_Backup“ lautet, können Sie die Updates Publisher-Datenbankdatei nach „E:\ConfigMgr_Backup\SCUP2011“ kopieren.  

    > [!TIP]  
    >  Wenn es auf einem Computer mehrere Datenbankdateien gibt, empfiehlt es sich, die Datei in einem Unterordner zu speichern, der den Namen des mit der Datenbankdatei verbundenen Benutzerprofils trägt. Beispielsweise kann sich eine Datenbankdatei in E:\ConfigMgr_Backup\SCUP2011\User1 befinden und eine andere Datenbankdatei in E:\ConfigMgr_Backup\SCUP2011\User2.  

### <a name="user-state-migration-data"></a>Daten zur Benutzerzustandsmigration  
 Mit Configuration Manager-Tasksequenzen können Sie bei der Betriebssystembereitstellung die Benutzerstatusdaten erfassen und wiederherstellen, wenn Sie den Benutzerstatus des aktuellen Betriebssystems beibehalten möchten. Die Ordner, in denen die Benutzerzustandsdaten gespeichert werden, werden in den Eigenschaften des Zustandsmigrationspunkts aufgeführt. Diese Daten zur Benutzerzustandsmigration werden vom Wartungstask „Standortserver sichern“ nicht gesichert. Im Rahmen Ihres Sicherungsplans müssen Sie die Ordner, in denen die Daten zur Benutzerzustandsmigration gespeichert werden, manuell sichern.   

#### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>So bestimmen Sie die Ordner, in denen die Daten zur Benutzerzustandsmigration gespeichert werden  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Knoten **Standortkonfiguration**, und wählen Sie anschließend **Server und Standortsystemrollen**.  

3.  Wählen Sie das Standortsystem aus, auf dem die Rolle „Zustandsmigration“ gehostet wird. Wählen Sie anschließend in **Standortsystemrollen** die Option **Zustandsmigrationspunkt**aus.  


4.  Klicken Sie auf der Registerkarte **Standortrolle** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  
5.  Die Ordner, in denen die Daten zur Benutzerzustandsmigration gespeichert werden, werden auf der Registerkarte **Allgemein** im Abschnitt **Ordnerdetails** aufgeführt.  

## <a name="recover-a-configuration-manager-site"></a>Wiederherstellen eines Configuration Manager-Standorts
 Eine Configuration Manager-Standortwiederherstellung ist bei einem Configuration Manager-Standortausfall oder bei einem Datenverlust in der Standortdatenbank erforderlich. Bei der Standortwiederherstellung geht es primär darum, Daten zu reparieren und erneut zu synchronisieren, um eine Unterbrechung von Vorgängen zu vermeiden.  

> [!IMPORTANT]  
>  Wenn Sie die Datenbank für einen Standort wiederherstellen, gilt Folgendes:  

>  -   Sie müssen die gleiche Version und Edition von SQL Server verwenden. Eine Datenbank, die unter SQL Server 2012 ausgeführt wurde, kann z.B. nicht unter SQL Server 2014 wiederhergestellt werden. Gleichermaßen kann eine Standortdatenbank, die unter einer Standard Edition von SQL Server 2014 ausgeführt wurde, nicht unter einer Enterprise Edition von SQL Server 2014 wiederhergestellt werden.  
> -   SQL Server darf nicht auf den **Einzelbenutzermodus**festgelegt werden.  
> -   Stellen Sie sicher, dass die MDF- und. LDF-Dateien gültig sind. Wenn Sie einen Standort wiederherstellen, wird der Status der Dateien, die Sie wiederherstellen möchten, nicht überprüft.  


 Die Standortwiederherstellung wird durch Ausführen des Configuration Manager-Setup-Assistenten aus dem Ordner „CD.Latest“ gestartet.  Sie können auch das Skript für die unbeaufsichtigte Installation konfigurieren und dann die Setup-Befehlsoption **/script** zum Ausführen des Setup aus diesem Ordner „CD.Latest“ verwenden. Welche Wiederherstellungsoptionen zur Auswahl stehen, hängt davon ab, ob Ihnen eine Sicherung der Configuration Manager-Standortdatenbank vorliegt. Weitere Informationen finden Sie unter [Der Ordner „CD.Latest“ für System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md).  

> [!IMPORTANT]  
>  Wenn Sie das Configuration Manager-Setup auf dem Standortserver über das Menü **Start** ausführen, ist die Option **Standort wiederherstellen** nicht verfügbar.  

>  Wenn Sie vor der Sicherung Updates von der Configuration Manager-Konsole aus installiert haben, können Sie den Standort nicht erfolgreich neu installieren, indem Sie das Setup vom Installationsmedium oder aus dem Installationspfad für Configuration Manager verwenden.  

> [!NOTE]  
>  Nachdem Sie eine Standortdatenbank wiederhergestellt haben, die für Datenbankreplikate konfiguriert war, müssen Sie vor der Verwendung der Datenbankreplikate jedes Replikat neu konfigurieren, indem Sie die Veröffentlichungen und die Abonnements neu erstellen.  

###  <a name="BKMK_DetermineRecoveryOptions"></a> Bestimmen der Wiederherstellungsoptionen  
 Bei der Wiederherstellung des primären Standortservers und des Standorts der zentralen Verwaltung von Configuration Manager müssen Sie zwei Hauptbereiche berücksichtigen: den Standortserver und die Standortdatenbank. In den folgenden Abschnitten wird erläutert, wie Sie die Optionen bestimmen, die Sie für Ihr Wiederherstellungsszenario auswählen müssen.  

> [!NOTE]  

####  <a name="BKMK_SiteServerRecoveryOptions"></a> Wiederherstellungsoptionen für den Standortserver  
 Sie müssen das Setup aus einer Kopie des Ordners „CD.Latest“ starten, die Sie außerhalb des Configuration Manager-Installationsordners erstellen. Dann wählen Sie die Option **Standort wiederherstellen** aus. Beim Ausführen von Setup stehen für den ausgefallenen Standortserver die folgenden Wiederherstellungsoptionen zur Verfügung:  

-   **Den Standortserver mit einem vorhandenen Sicherungssatz wiederherstellen**: Verwenden Sie diese Option, wenn Sie über eine Sicherung des Configuration Manager-Standortservers verfügen, die vor dem Standortausfall im Rahmen des Wartungstasks **Standortserver sichern** auf dem Standortserver erstellt wurde. Der Standort wird erneut installiert, und die Standardeinstellungen werden anhand des gesicherten Standorts konfiguriert.  

-   **Diesen Standortserver erneut installieren**: Verwenden Sie diese Option, wenn Sie über keine Sicherung des Standortservers verfügen. Der Standortserver wird erneut installiert, und Sie müssen die Standorteinstellungen genau wie bei einer Erstinstallation angeben. Sie müssen den gleichen Standortcode und Datenbanknamen verwenden, die Sie bei der Erstinstallation des ausgefallenen Standorts angegeben hatten, damit der Standort erfolgreich wiederhergestellt werden kann.  

> [!NOTE]  
>  Wenn beim Setup ein vorhandener Configuration Manager-Standort auf dem Server erkannt wird, können Sie eine Standortwiederherstellung starten. Allerdings sind die Wiederherstellungsoptionen für den Standortserver beschränkt. Wenn Sie Setup beispielsweise auf einem vorhandenen Standortserver ausführen und die Wiederherstellung auswählen, können Sie zwar den Standortdatenbankserver wiederherstellen, aber die Option zum Wiederherstellen des Standortservers ist deaktiviert.  

####  <a name="BKMK_SiteDatabaseRecoveryOption"></a> Wiederherstellungsoptionen für die Standortdatenbank  
 Beim Ausführen von Setup stehen für die Standortdatenbank die folgenden Wiederherstellungsoptionen zur Verfügung:  

-   **Die Standortdatenbank mit dem Sicherungssatz wiederherstellen**: Verwenden Sie diese Option, wenn Sie über eine Sicherung der Configuration Manager-Standortdatenbank verfügen, die vor dem Standortdatenbankfehler bei der Ausführung des Wartungstasks **Standortserver sichern** auf dem Standort erstellt wurde. Wenn Sie über eine Hierarchie verfügen, werden die Änderungen, die Sie seit der letzten Sicherung der Standortdatenbank an der Standortdatenbank vorgenommen haben, für einen primären Standort vom Standort der zentralen Verwaltung abgerufen bzw. für einen Standort der zentralen Verwaltung von einem primären Referenzstandort. Wenn Sie die Standortdatenbank für einen eigenständigen primären Standort wiederherstellen, gehen die Standortänderungen seit der letzten Sicherung verloren.  

     Wenn Sie die Standortdatenbank für einen Standort in einer Hierarchie wiederherstellen, hängt das Wiederherstellungsverhalten vom Standorttyp (Standort der zentralen Verwaltung oder primärer Standort) sowie davon ob, ob die letzte Sicherung innerhalb oder außerhalb der Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server liegt. Weitere Informationen finden Sie im Abschnitt [Wiederherstellungsszenarien für die Standortdatenbank](#BKMK_SiteDBRecoveryScenarios) in diesem Thema.  

    > [!NOTE]  
    >  Die Wiederherstellung ist nicht möglich, wenn Sie angeben, dass die Standortdatenbank anhand eines Sicherungssatzes wiederhergestellt werden soll, die Standortdatenbank aber bereits vorhanden ist.  

-   **Eine neue Datenbank für diesen Standort erstellen**: Verwenden Sie diese Option, wenn Sie über keine Sicherung der Configuration Manager-Standortdatenbank verfügen. Wenn Sie über eine Hierarchie verfügen, wird eine neue Standortdatenbank erstellt. Die Daten werden anhand replizierter Daten wiederhergestellt, die bei einem primären Standort vom Standort der zentralen Verwaltung stammen bzw. bei einem Standort der zentralen Verwaltung von einem primären Referenzstandort. Diese Option ist beim Wiederherstellen eines eigenständigen primären Standorts oder eines Standorts der zentralen Verwaltung, der keine primären Standorte hat, nicht verfügbar.  

-   **Manuell wiederhergestellte Standortdatenbank verwenden**: Verwenden Sie diese Option, wenn Sie die Configuration Manager-Standortdatenbank bereits wiederhergestellt haben, aber den Wiederherstellungsprozess noch abschließen müssen. Configuration Manager kann die Standortdatenbank aus dem Configuration Manager-Sicherungswartungstask oder aus der Standortdatenbanksicherung wiederherstellen, die Sie mit DPM oder einem anderen Prozess ausgeführt haben. Nachdem Sie die Standortdatenbank mithilfe einer Methode außerhalb von Configuration Manager wiederhergestellt haben, müssen Sie das Setup ausführen und diese Option auswählen, um die Wiederherstellung der Standortdatenbank abzuschließen. Wenn Sie über eine Hierarchie verfügen, werden die Änderungen, die Sie seit der letzten Sicherung der Standortdatenbank an der Standortdatenbank vorgenommen haben, für einen primären Standort vom Standort der zentralen Verwaltung abgerufen bzw. für einen Standort der zentralen Verwaltung von einem primären Referenzstandort. Wenn Sie die Standortdatenbank für einen eigenständigen primären Standort wiederherstellen, gehen die Standortänderungen seit der letzten Sicherung verloren.  

    > [!NOTE]  
    >  Wenn Sie DPM verwenden, um die Standortdatenbank zu sichern, dann verwenden Sie DPM-Prozeduren, um die Standortdatenbank an einem angegebenen Ort wiederherzustellen, bevor Sie den Wiederherstellungsprozess in Configuration Manager fortsetzen. Weitere Informationen zu DPM finden Sie in der [Data Protection Manager-Dokumentationsbibliothek](http://go.microsoft.com/fwlink/?LinkId=272772) auf der TechNet-Webseite.  

-   **Datenbankwiederherstellung überspringen**: Verwenden Sie diese Option, wenn es auf dem Configuration Manager-Standortdatenbankserver keine Datenverluste gab. Diese Option gilt nur, wenn die Standortdatenbank sich auf einem anderen Computer als der Standortserver, den Sie wiederherstellen, befindet.  

####  <a name="bkmk_SQLretention"></a> Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server  
 Die Änderungsnachverfolgung ist für die Standortdatenbank in SQL Server aktiviert. Bei der Änderungsnachverfolgung können von Configuration Manager Informationen über die Änderungen abgefragt werden, die seit einem früheren Zeitpunkt an den Datenbanktabellen vorgenommen wurden. Mit der Beibehaltungsdauer wird angegeben, wie lange Informationen zur Änderungsnachverfolgung beibehalten werden. Für die Standortdatenbank ist standardmäßig eine Beibehaltungsdauer von 5 Tagen konfiguriert. Beim Wiederherstellen einer Standortdatenbank richtet sich der Wiederherstellungsprozess danach, ob die Sicherung innerhalb oder außerhalb der Beibehaltungsdauer liegt. Wenn beispielsweise ein Standortdatenbankserver ausfällt und die letzte Sicherung vor 7 Tagen erstellt wurde, liegt die Sicherung außerhalb der Beibehaltungsdauer.

 Weitere Informationen zur SQL Server-Änderungsnachverfolgung finden Sie in den folgenden Blogs des SQL Server-Teams: [Change Tracking Cleanup - part 1 (Cleanup für die Änderungsnachverfolgung - Teil 1)](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1) und [Change Tracking Cleanup - part 2 (Cleanup für die Änderungsnachverfolgung - Teil 2)](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).



####  <a name="bkmk_reinit"></a> Prozess zum erneuten Initialisieren der Standortdaten oder der globalen Daten  
 Beim erneuten Initialisieren der Standortdaten oder der globalen Daten werden in der Standortdatenbank vorhandene Daten durch Daten aus einer anderen Standortdatenbank ersetzt. Wenn beispielsweise an Standort ABC Daten von Standort XYZ erneut initialisiert werden, werden die folgenden Schritte ausgeführt:  

-   Die Daten werden von Standort XYZ zu Standort ABC kopiert.  

-   Die für Standort XYZ vorhandenen Daten werden aus der Standortdatenbank an Standort ABC entfernt.  

-   Die von Standort XYZ kopierten Daten werden in die Standortdatenbank an Standort ABC eingefügt.  

##### <a name="example-scenario-1"></a>Beispielszenario 1  
 **Die globalen Daten vom Standort der zentralen Verwaltung werden am primären Standort erneut initialisiert**: Bei der Wiederherstellung werden die vorhandenen globalen Daten für den primären Standort aus der Datenbank des primären Standorts entfernt und durch die am Standort der zentralen Verwaltung kopierten globalen Daten ersetzt.  

##### <a name="example-scenario-2"></a>Beispielszenario 2  
 **Die Standortdaten von einem primären Standort werden am Standort der zentralen Verwaltung erneut initialisiert**: Bei der Wiederherstellung werden die vorhandenen Standortdaten für diesen primären Standort aus der Datenbank des Standorts der zentralen Verwaltung entfernt und durch die am primären Standort kopierten Standortdaten ersetzt. Die Standortdaten für andere primäre Standorte bleiben unverändert.  

####  <a name="BKMK_SiteDBRecoveryScenarios"></a> Wiederherstellungsszenarien für die Standortdatenbank  
 Nach der Wiederherstellung einer Standortdatenbank anhand einer Sicherung wird von Configuration Manager versucht, die seit der letzten Datenbanksicherung an den Standortdaten und globalen Daten vorgenommenen Änderungen wiederherzustellen. Im Folgenden sind die Aktionen aufgeführt, die nach der Wiederherstellung einer Standortdatenbank anhand einer Sicherung von Configuration Manager gestartet werden.  

 **Der wiederhergestellte Standort ist ein Standort der zentralen Verwaltung:**  

-   **Datenbanksicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung**  

    -   **Globale Daten:** Die Änderungen in globalen Daten nach der Sicherung werden von allen primären Standorten repliziert.  

    -   **Standortdaten:** Die Änderungen in Standortdaten nach der Sicherung werden von allen primären Standorten repliziert.  

-   **Datenbanksicherung, die älter ist als die Beibehaltungsdauer der Änderungsnachverfolgung**  

    -   **Globale Daten:** Am Standort der zentralen Verwaltung werden die globalen Daten vom primären Referenzstandort, sofern angegeben, neu initialisiert. Anschließend werden die globalen Daten vom Standort der zentralen Verwaltung auf allen anderen primären Standorten neu initialisiert. Wenn kein Referenzstandort angegeben wurde, werden die globalen Daten vom Standort der zentralen Verwaltung (die aus der Sicherung wiederhergestellten Daten) auf allen primären Standorten neu initialisiert.  

    -   **Standortdaten:** Am Standort der zentralen Verwaltung werden die Standortdaten von jedem primären Standort neu initialisiert.  

 **Der wiederhergestellte Standort ist ein primärer Standort:**  

-   **Datenbanksicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung**  

    -   **Globale Daten:** Die nach der Sicherung an globalen Daten vorgenommenen Änderungen werden vom Standort der zentralen Verwaltung repliziert.  

    -   **Standortdaten:** Am Standort der zentralen Verwaltung werden die Standortdaten vom primären Standort erneut initialisiert. Die nach der Sicherung ausgeführten Änderungen gehen verloren. Die meisten Daten werden jedoch von Clients erneut generiert, von denen Informationen an den primären Standort gesendet werden.  

-   **Datenbanksicherung, die älter ist als die Beibehaltungsdauer der Änderungsnachverfolgung**  

    -   **Globale Daten:** Am primären Standort werden die globalen Daten vom Standort der zentralen Verwaltung erneut initialisiert.  

    -   **Standortdaten:** Am Standort der zentralen Verwaltung werden die Standortdaten vom primären Standort erneut initialisiert. Die nach der Sicherung ausgeführten Änderungen gehen verloren. Die meisten Daten werden jedoch von Clients erneut generiert, von denen Informationen an den primären Standort gesendet werden.  

### <a name="site-recovery-procedures"></a>Verfahren zur Standortwiederherstellung  
 Wenden Sie eines der folgenden Verfahren an, um Standortserver und Standortdatenbank wiederherzustellen.  

##### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>So starten Sie eine Standortwiederherstellung im Setup-Assistenten  

1.  Kopieren Sie den Ordner „CD.Latest“ an einen Speicherort außerhalb des Configuration Manager-Installationsordners. (Siehe [Der Ordner „CD.Latest“ für System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md))  

     Führen Sie von der Kopie des Ordners „CD.Latest“ aus den Configuration Manager-Setup-Assistenten aus.  

2.  Wählen Sie auf der Seite **Erste Schritte** die Option **Standort wiederherstellen**aus, und klicken Sie dann auf **Weiter**.  

3.  Wählen Sie die Optionen aus, die für die Standortwiederherstellung geeignet sind, und schließen Sie den Assistenten ab.  

    > [!IMPORTANT]  
    >  Während der Wiederherstellung wird der Port des SQL Server-Service Brokers (SSB), der von SQL Server verwendet wird, von Setup identifiziert. Ändern Sie die Einstellung für diesen Port während der Wiederherstellung nicht, da andernfalls die Datenreplikation nach Abschluss der Wiederherstellung nicht ordnungsgemäß ausgeführt werden kann.  

    > [!NOTE]  
    >  Sie können den ursprünglichen oder einen neuen Pfad für die Configuration Manager-Installation im Setup-Assistenten angeben.  

##### <a name="to-start-an-unattended-site-recovery"></a>So starten Sie eine unbeaufsichtigte Standortwiederherstellung  

1.  Bereiten Sie das Skript für eine unbeaufsichtigte Installation mit den für die Standortwiederherstellung erforderlichen Optionen vor.  

2.  Führen Sie das Configuration Manager-Setup mit der Befehlszeilenoption **/script** aus. Wenn der Name der Setupinitialisierungsdatei zum Beispiel „ConfigMgrUnattend.ini“ lautet und die Datei im Verzeichnis „C:\Temp“ des Computers gespeichert ist, auf dem Sie das Setup ausführen, lautet der Befehl wie folgt: **Setup /script C:\temp\ConfigMgrUnattend.ini**  

> [!NOTE]  
>  Nach dem Wiederherstellen eines zentralen Verwaltungsstandorts kann es bei der Replikation bestimmter Standortdaten von untergeordneten Standorten zu Fehlern kommen. Dies kann Hardwareinventur, Softwareinventur und Statusmeldungen umfassen.  
>   
>  In diesem Fall müssen Sie **ConfigMgrDRSSiteQueue** für die Datenbankreplikation erneut initialisieren.  Verwenden Sie hierzu **SQL Server Manager** zum Ausführen der folgenden Abfrage über die Configuration Manager-Standortdatenbank am Standort der zentralen Verwaltung:  
>   
>  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**  
>   
>  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**  

###  <a name="BKMK_UnattendedSiteRecoveryKeys"></a> Skriptdateischlüssel für unbeaufsichtigte Standortwiederherstellung  
 Wenn Sie eine unbeaufsichtigte Wiederherstellung eines Standorts der zentralen Verwaltung oder eines primären Standorts für Configuration Manager ausführen möchten, können Sie ein Skript für eine unbeaufsichtigte Installation erstellen und das Setup mit der Befehlsoption „/script“ ausführen. Mit dem Skript werden die gleichen Informationen bereitgestellt, die andernfalls über den Setup-Assistenten eingegeben werden müssten. Das Skript enthält jedoch keine Standardeinstellungen. Alle Werte müssen für die Setup-Schlüssel angegeben werden, die für den jeweils verwendeten Wiederherstellungstyp gelten.  

 Sie können das Configuration Manager-Setup unbeaufsichtigt ausführen, indem Sie eine Initialisierungsdatei mit der Setup-Befehlszeilenoption „/script“ verwenden. Die unbeaufsichtigte Installation wird bei der Wiederherstellung eines Standorts der zentralen Verwaltung und eines primären Standorts für Configuration Manager unterstützt. Damit Sie die Setup-Befehlszeilenoption /script verwenden können, müssen Sie eine Initialisierungsdatei erstellen und den Namen der Initialisierungsdatei nach der Setup-Befehlszeilenoption /script angeben. Der Name der Datei ist unerheblich. Wichtig ist, dass er die Dateinamenerweiterung „.ini“ aufweist. Wenn Sie in der Befehlszeile auf die Setup-Initialisierungsdatei verweisen, müssen Sie den vollständigen Dateipfad angeben. Wenn sich beispielsweise die Initialisierungsdatei mit dem Namen setup.ini im Ordner C:\setup befindet, muss die Befehlszeile wie folgt lauten:  

 **setup /script c:\setup\setup.ini**.  

> [!IMPORTANT]  
>  Zum Ausführen von Setup benötigen Sie Administratorrechte. Wenn Sie Setup mit dem unbeaufsichtigten Skript ausführen, starten Sie die Eingabeaufforderung im Kontext eines Administrators mit **Als Administrator ausführen**.  

 Das Skript enthält Abschnittsnamen, Schlüsselnamen und Werte. Welche Abschnitts- und Schlüsselnamen erforderlich sind, hängt vom Wiederherstellungstyp ab, für den Sie das Skript erstellen. Die Reihenfolge der Schlüssel in den Abschnitten und die Reihenfolge der Abschnitte in der Datei spielen keine Rolle. Bei Schlüsseln wird die Groß-/Kleinschreibung nicht beachtet. Wenn Sie Werte für Schlüssel angeben, müssen dem Namen des Schlüssels ein Gleichheitszeichen (=) und der Wert für den Schlüssel folgen.  

 In den folgenden Abschnitten erfahren Sie, wie Sie ein Skript für die unbeaufsichtigte Standortwiederherstellung erstellen. In den Tabellen werden die verfügbaren Setupskriptschlüssel und die entsprechenden Werte aufgeführt. Außerdem wird angegeben, ob die Schlüssel erforderlich sind und für welchen Installationstyp sie verwendet werden. In der letzten Spalte finden Sie zudem eine kurze Beschreibung der einzelnen Schlüssel.  

#### <a name="recover-a-central-administration-site-unattended"></a>Unbeaufsichtigtes Wiederherstellen eines Standorts der zentralen Verwaltung  
 Konfigurieren Sie mit den folgenden Informationen eine Setup-Skriptdatei zur unbeaufsichtigten Wiederherstellung eines Standorts der zentralen Verwaltung.  

 **Identification**  

-   **Schlüsselname:** Action  

    -   **Erforderlich:** Ja  

    -   **Werte:** RecoverCCAR  

    -   **Details:** Mit diesem Schlüssel wird ein Standort der zentralen Verwaltung wiederhergestellt.  

-   **Schlüsselname:** CDLatest  

    -   **Erforderlich:** Ja; nur wenn Sie Medien aus dem Ordner „CD.Latest“ verwenden    

    -   **Werte:** 1; bei jedem Wert außer 1 wird davon ausgegangen, dass er nicht „CD.Latest“ verwendet

    -   **Details:** Ihr Skript muss diesen Schlüssel und diesen Wert enthalten, wenn Sie das Setup von einem Medium in dem Ordner „CD.Latest“ ausführen, um einen Standort der primären oder zentralen Verwaltung zu installieren oder diesen wiederherstellen möchten. Dieser Wert informiert das Setup darüber, das Medien aus „CD.Latest“ verwendet werden.  

**RecoveryOptions**  

-   **Schlüsselname:** ServerRecoveryOptions  

    -   **Erforderlich:** Ja  

    -   **Werte:** 1, 2 oder 4  

         1 = Wiederherstellung von Standortserver und SQL Server  

         2 = nur Wiederherstellung von Standortserver  

         4 = nur Wiederherstellung von SQL Server  

    -   **Details:** Hiermit wird angegeben, ob von Setup der Standortserver, SQL Server oder beides wiederhergestellt wird. Die zugeordneten Schlüssel sind erforderlich, wenn Sie den folgenden Wert für die Einstellung ServerRecoveryOptions festlegen:  

        -   **Wert = 1:** Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

             Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.  

        -   **Wert = 2:** Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

        -   **Wert = 4** Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **10** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.  

-   **Schlüsselname:** DatabaseRecoveryOptions  

    -   **Erforderlich:** Vielleicht  

    -   **Werte:** 10, 20, 40, 80  

         10 = Wiederherstellen der Standortdatenbank aus einer Sicherung  

         20 = Verwenden einer Standortdatenbank, die mithilfe einer anderen Methode manuell wiederhergestellt wurde  

         40 = Erstellen einer neuen Datenbank für den Standort. Verwenden Sie diese Option, wenn keine Standortdatenbank verfügbar ist. Globale Daten und Standortdaten werden durch die Replikation von anderen Standorten wiederhergestellt.  

         80 = Datenbankwiederherstellung überspringen  

    -   **Details:** Über diesen Schlüssel wird angegeben, wie Setup die Standortdatenbank in SQL Server wiederherstellen soll. Dieser Schlüssel ist erforderlich, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **4**konfiguriert wurde.  

-   **Schlüsselname:** ReferenceSite  

    -   **Erforderlich:** Vielleicht  

    -   **Werte:** &lt;ReferenceSiteFQDN\>  

    -   **Details:** Hiermit wird der primäre Referenzstandort angegeben, der vom Standort der zentralen Verwaltung verwendet wird, um globale Daten wiederherzustellen, wenn die Datenbanksicherung älter ist als die Beibehaltungsdauer der Änderungsnachverfolgung, oder wenn Sie den Standort ohne Sicherung wiederherstellen.  

         Wenn Sie keinen Referenzstandort angeben und die Sicherung älter als die Beibehaltungsdauer der Änderungsnachverfolgung ist, dann werden alle primären Standorte mit den wiederhergestellten Daten vom Standort der zentralen Verwaltung neu initialisiert.  

         Wenn Sie keinen Referenzstandort angeben und die Sicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung liegt, dann werden nur Änderungen, die seit der Sicherung vorgenommen wurden, von den primären Standorten repliziert. Wenn Änderungen von verschiedenen primären Standorten vorliegen, die miteinander in Konflikt stehen, dann wird vom Standort der zentralen Verwaltung die zuerst empfangene verwendet.  

         Dieser Schlüssel ist erforderlich, wenn für die Einstellung **DatabaseRecoveryOptions** der Wert **40**vorliegt.  

-   **Schlüsselname:** SiteServerBackupLocation  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;PathToSiteServerBackupSet\>  

    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz des Standortservers angegeben. Dieser Schlüssel ist optional, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **2**konfiguriert wurde. Geben Sie einen Wert für den Schlüssel **SiteServerBackupLocation** an, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

-   **Schlüsselname:** BackupLocation  

    -   **Erforderlich:** Vielleicht  

    -   **Werte:** &lt;PathToSiteDatabaseBackupSet\>  

    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz der Standortdatenbank angegeben. Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **ServerRecoveryOptions** den Wert **1** oder **4** konfigurieren und für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** .  

**Optionen**  

-   **Schlüsselname:** ProductID  

    -   **Erforderlich:** Ja  

    -   **Werte:**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         – Evaluierungsversion  

    -   **Details:** Gibt den Product Key für die Configuration Manager-Installation einschließlich der Gedankenstriche an. Geben Sie **Eval** ein, um die Evaluierungsversion von Configuration Manager zu installieren.  

-   **Schlüsselname:** SiteCode  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;Standortcode\>  

    -   **Details:** Drei alphanumerische Zeichen, die den Standort in der Hierarchie eindeutig angeben. Sie müssen den Standortcode angeben, der vor dem Auftreten des Fehlers vom Standort verwendet wurde.  

-   **Schlüsselname:** SiteName  

    -   **Erforderlich:** Ja  

    -   **Werte:** Standortname  

    -   **Details:** Beschreibung für diesen Standort.  

-   **Schlüsselname:** SMSInstallDir  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;*ConfigMgrInstallationPath*>  

    -   **Details:** Hiermit wird der Installationsordner für die Configuration Manager-Programmdateien angegeben.  

        > [!NOTE]  
        >  Sie können den ursprünglichen oder einen neuen Pfad für die Configuration Manager-Installation angeben.  

-   **Schlüsselname:** SDKServer  

    -   **Erforderlich:** Ja  

    -   **Werte:**&lt;*FQDN des SMS-Anbieters*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird. Sie müssen den Server angeben, von dem der SMS-Anbieter vor Auftreten des Fehlers gehostet wurde.  

         Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren.  

-   **Schlüsselname:** PrerequisiteComp  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = herunterladen  

         1 = bereits heruntergeladen  

    -   **Details:** Hiermit wird angegeben, ob die für Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert 0 angeben, werden die Dateien von Setup heruntergeladen.  

-   **Schlüsselname:** PrerequisitePath  

    -   **Erforderlich:** Ja  

    -   **Werte:**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für Setup erforderlichen Dateien angegeben. Je nach dem Wert unter **PrerequisiteComp** wird dieser Pfad von Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

-   **Schlüsselname:** AdminConsole  

    -   **Erforderlich:** Vielleicht  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll. Dieser Schlüssel ist erforderlich, außer wenn für die Einstellung **ServerRecoveryOptions** der Wert **4**vorliegt.  

-   **Schlüsselname:** JoinCEIP  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht teilnehmen  

         1 = teilnehmen  

    -   **Details:** Gibt an, ob am Programm zur Verbesserung der Benutzerfreundlichkeit teilgenommen wird.  

**SQLConfigOptions**  

-   **Schlüsselname:** SQLServerName  

    -   **Erforderlich:** Ja  

    -   **Werte:** *&lt;SQLServerName\>*  

    -   **Details:** Der Name des Servers oder der gruppierten Instanz mit SQL Server, auf dem bzw. der die Standortdatenbank gehostet werden soll. Sie müssen den Server angeben, von dem die Standortdatenbank vor dem Auftreten des Fehlers gehostet wurde.  

-   **Schlüsselname:** DatabaseName  

    -   **Erforderlich:** Ja  

    -   **Werte:**  

         *&lt;Name_der_Standortdatenbank\>*  

         auf der Registerkarte  

         *&lt;Instanzname\>*\\*&lt;Name_der_Standortdatenbank\>*  

    -   **Details:** Gibt den Namen der SQL Server-Datenbank an, die bei der Installation der Datenbank für den Standort der zentralen Verwaltung erstellt oder verwendet werden soll. Sie müssen den gleichen Datenbanknamen angeben, der vor Auftreten des Fehlers verwendet wurde.  

        > [!IMPORTANT]  
        >  Sie müssen den Instanznamen und den Namen der Standortdatenbank angeben, falls Sie die Standardinstanz nicht verwenden.  

-   **Schlüsselname:** SQLSSBPort  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*SSBPortNumber*>  

    -   **Details:** Gibt den Port des SQL Server-Service Brokers (SSB) an, der von SQL Server verwendet wird. Von SSB wird zwar in der Regel TCP-Port 4022 verwendet, aber es werden auch andere Ports unterstützt. Sie müssen den gleichen SSB-Port angeben, der vor Auftreten des Fehlers verwendet wurde.  

#### <a name="recover-a-primary-site-unattended"></a>Unbeaufsichtigtes Wiederherstellen eines primären Standorts  
 Konfigurieren Sie mit den folgenden Informationen eine Setup-Skriptdatei zur unbeaufsichtigten Wiederherstellung eines Standorts der zentralen Verwaltung.  

 **Identification**  

-   **Schlüsselname:** Action  

    -   **Erforderlich:** Ja  

    -   **Werte:** RecoverPrimarySite  

    -   **Details:** Mit diesem Schlüssel wird ein primärer Standort wiederhergestellt.  

-   **Schlüsselname:** CDLatest  

    -   **Erforderlich:** Ja; nur wenn Sie Medien aus dem Ordner „CD.Latest“ verwenden    

    -   **Werte:** 1; bei jedem Wert außer 1 wird davon ausgegangen, dass er nicht „CD.Latest“ verwendet

    -   **Details:** Ihr Skript muss diesen Schlüssel und diesen Wert enthalten, wenn Sie das Setup von einem Medium in dem Ordner „CD.Latest“ ausführen, um einen Standort der primären oder zentralen Verwaltung zu installieren oder diesen wiederherstellen möchten. Dieser Wert informiert das Setup darüber, das Medien aus „CD.Latest“ verwendet werden.

**RecoveryOptions**  

-   **Schlüsselname:** ServerRecoveryOptions  

    -   **Erforderlich:** Ja  

    -   **Werte:** 1, 2 oder 4  

         1 = Wiederherstellung von Standortserver und SQL Server  

         2 = nur Wiederherstellung von Standortserver  

         4 = nur Wiederherstellung von SQL Server  

    -   **Details:** Hiermit wird angegeben, ob von Setup der Standortserver, SQL Server oder beides wiederhergestellt wird. Die zugeordneten Schlüssel sind erforderlich, wenn Sie den folgenden Wert für die Einstellung ServerRecoveryOptions festlegen:  

        -   **Wert = 1:** Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

             Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.  

        -   **Wert = 2:** Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

        -   **Wert = 4** Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **10** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.  

-   **Schlüsselname:** DatabaseRecoveryOptions  

    -   **Erforderlich:** Vielleicht  

    -   **Werte:** 10, 20, 40, 80  

         10 = Wiederherstellen der Standortdatenbank aus einer Sicherung  

         20 = Verwenden einer Standortdatenbank, die mithilfe einer anderen Methode manuell wiederhergestellt wurde  

         40 = Erstellen einer neuen Datenbank für den Standort. Verwenden Sie diese Option, wenn keine Standortdatenbank verfügbar ist. Globale Daten und Standortdaten werden durch die Replikation von anderen Standorten wiederhergestellt.  

         80 = Datenbankwiederherstellung überspringen  

    -   **Details:** Über diesen Schlüssel wird angegeben, wie Setup die Standortdatenbank in SQL Server wiederherstellen soll. Dieser Schlüssel ist erforderlich, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **4**konfiguriert wurde.  

-   **Schlüsselname:** SiteServerBackupLocation  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;PathToSiteServerBackupSet\>  

    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz des Standortservers angegeben. Dieser Schlüssel ist optional, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **2**konfiguriert wurde. Geben Sie einen Wert für den Schlüssel **SiteServerBackupLocation** an, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

-   **Schlüsselname:** BackupLocation  

    -   **Erforderlich:** Vielleicht  

    -   **Werte:** &lt;PathToSiteDatabaseBackupSet\>  

    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz der Standortdatenbank angegeben. Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **ServerRecoveryOptions** den Wert **1** oder **4** konfigurieren und für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** .  

**Optionen**  

-   **Schlüsselname:** ProductID  

    -   **Erforderlich:** Ja  

    -   **Werte:**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         – Evaluierungsversion  

    -   **Details:** Gibt den Product Key für die Configuration Manager-Installation einschließlich der Gedankenstriche an. Geben Sie **Eval** ein, um die Evaluierungsversion von Configuration Manager zu installieren.  

-   **Schlüsselname:** SiteCode  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;Standortcode\>  

    -   **Details:** Drei alphanumerische Zeichen, die den Standort in der Hierarchie eindeutig angeben. Sie müssen den Standortcode angeben, der vor dem Auftreten des Fehlers vom Standort verwendet wurde.  

-   **Schlüsselname:** SiteName  

    -   **Erforderlich:** Ja  

    -   **Werte:** Standortname  

    -   **Details:** Beschreibung für diesen Standort.  

-   **Schlüsselname:** SMSInstallDir  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;*ConfigMgrInstallationPath*>  

    -   **Details:** Hiermit wird der Installationsordner für die Configuration Manager-Programmdateien angegeben.  

        > [!NOTE]  
        >  Sie können den ursprünglichen oder einen neuen Pfad für die Configuration Manager-Installation angeben.  

-   **Schlüsselname:** SDKServer  

    -   **Erforderlich:** Ja  

    -   **Werte:**&lt;*FQDN des SMS-Anbieters*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird. Sie müssen den Server angeben, von dem der SMS-Anbieter vor Auftreten des Fehlers gehostet wurde.  

         Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren.  

-   **Schlüsselname:** PrerequisiteComp  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = herunterladen  

         1 = bereits heruntergeladen  

    -   **Details:** Hiermit wird angegeben, ob die für Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert 0 angeben, werden die Dateien von Setup heruntergeladen.  

-   **Schlüsselname:** PrerequisitePath  

    -   **Erforderlich:** Ja  

    -   **Werte:**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für Setup erforderlichen Dateien angegeben. Je nach dem Wert unter **PrerequisiteComp** wird dieser Pfad von Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

-   **Schlüsselname:** AdminConsole  

    -   **Erforderlich:** Vielleicht  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll. Dieser Schlüssel ist erforderlich, außer wenn für die Einstellung **ServerRecoveryOptions** der Wert **4**vorliegt.  

-   **Schlüsselname:** JoinCEIP  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht teilnehmen  

         1 = teilnehmen  

    -   **Details:** Gibt an, ob am Programm zur Verbesserung der Benutzerfreundlichkeit teilgenommen wird.  

**SQLConfigOptions**  

-   **Schlüsselname:** SQLServerName  

    -   **Erforderlich:** Ja  

    -   **Werte:** *&lt;SQLServerName\>*  

    -   **Details:** Der Name des Servers oder der gruppierten Instanz mit SQL Server, auf dem bzw. der die Standortdatenbank gehostet werden soll. Sie müssen den Server angeben, von dem die Standortdatenbank vor dem Auftreten des Fehlers gehostet wurde.  

-   **Schlüsselname:** DatabaseName  

    -   **Erforderlich:** Ja  

    -   **Werte:**  

         *&lt;Name_der_Standortdatenbank\>*  

         auf der Registerkarte  

         *&lt;Instanzname\>*\\*&lt;Name_der_Standortdatenbank\>*  

    -   **Details:** Gibt den Namen der SQL Server-Datenbank an, die bei der Installation der Datenbank für den Standort der zentralen Verwaltung erstellt oder verwendet werden soll. Sie müssen den gleichen Datenbanknamen angeben, der vor Auftreten des Fehlers verwendet wurde.  

        > [!IMPORTANT]  
        >  Sie müssen den Instanznamen und den Namen der Standortdatenbank angeben, falls Sie die Standardinstanz nicht verwenden.  

-   **Schlüsselname:** SQLSSBPort  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*SSBPortNumber*>  

    -   **Details:** Gibt den Port des SQL Server-Service Brokers (SSB) an, der von SQL Server verwendet wird. Von SSB wird zwar in der Regel TCP-Port 4022 verwendet, aber es werden auch andere Ports unterstützt. Sie müssen den gleichen SSB-Port angeben, der vor Auftreten des Fehlers verwendet wurde.  

**Hierarchie-ExpansionOption**  

-   **Schlüsselname:** CCARSiteServer  

    -   **Erforderlich:** Vielleicht  

    -   **Werte:** &lt;*SiteCodeForCentralAdministrationSite*>  

    -   **Details:** Über diesen Schlüssel wird der Standort der zentralen Verwaltung angegeben, dem ein primärer Standort beim Hinzufügen zur Configuration Manager-Hierarchie zugeordnet wird. Diese Einstellung ist erforderlich, wenn der primäre Standort vor dem Fehler mit einem zentralen Verwaltungsstandort verbunden war. Sie müssen den Standortcode angeben, der vor dem Auftreten des Fehlers vom zentralen Verwaltungsstandort verwendet wurde.  

-   **Schlüsselname:** CASRetryInterval  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*Intervall*>  

    -   **Details:** Über diesen Schlüssel wird das Wiederholungsintervall angegeben (in Minuten), wenn beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler aufgetreten ist. Wenn beispielsweise beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler auftritt, wird der Verbindungsversuch auf dem primären Standort nach der für CASRetryInterval angegebenen Anzahl von Minuten wiederholt.  

-   **Schlüsselname:** WaitForCASTimeout  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*Timeout*>  

    -   **Details:** Über diesen Schlüssel wird der maximale Timeoutwert (in Minuten) für die Verbindung eines primären Standorts mit dem Standort der zentralen Verwaltung angegeben. Wenn beispielsweise beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler auftritt, wird der Verbindungsversuch auf dem primären Standort basierend auf dem Wert für CASRetryInterval solange wiederholt, bis der für WaitForCASTimeout angegebene Zeitraum abgelaufen ist. Sie können einen Wert von 0 bis 100 angeben.  

###  <a name="BKMK_PostRecovery"></a> Aufgaben nach der Wiederherstellung  
 Nach der Wiederherstellung Ihres Standorts müssen Sie ggf. einige zusätzliche Tasks ausführen, bevor die Standortwiederherstellung abgeschlossen ist. In den folgenden Abschnitten erfahren Sie, wie Sie Ihre Standortwiederherstellung abschließen.  

#### <a name="re-enter-user-account-passwords"></a>Erneutes Eingeben der Kennwörter von Benutzerkonten  
 Nach der Wiederherstellung eines Standortservers müssen die Kennwörter der für den Standort angegebenen Benutzerkonten erneut eingegeben werden, da sie im Rahmen der Standortwiederherstellung zurückgesetzt werden. Die Konten werden nach Abschluss der Standortwiederherstellung im Setup-Assistenten auf der Seite **Fertig gestellt** aufgelistet und auf dem wiederhergestellten Standortserver unter "C:\ConfigMgrPostRecoveryActions.html" gespeichert.  

###### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>So geben Sie Kennwörter für Benutzerkonten nach der Standortwiederherstellung erneut ein  

1.  Öffnen Sie die Configuration Manager-Konsole, und stellen Sie eine Verbindung mit dem wiederhergestellten Standort her.  

2.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

3.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Eintrag **Sicherheit**, und klicken Sie dann auf **Konten**.  

4.  Gehen Sie für jedes Konto, für das Sie das Kennwort erneut eingeben müssen, wie folgt vor:  

    1.  Wählen Sie das Konto aus der nach der Standortwiederherstellung angezeigten Liste von Konten aus. Sie finden diese Liste auf dem wiederhergestellten Standortserver unter C:\ConfigMgrPostRecoveryActions.html.  

    2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften** , um die Kontoeigenschaften zu öffnen.  

    3.  Klicken Sie auf der Registerkarte **Allgemein** auf **Festlegen**, und geben Sie dann die Kennwörter für das Konto erneut ein.  

    4.  Klicken Sie auf **Überprüfen**, wählen Sie die entsprechende Datenquelle für das ausgewählte Benutzerkonto aus, und klicken Sie dann auf **Testverbindung** , um zu überprüfen, ob eine Verbindung des Benutzerkontos mit der Datenquelle möglich ist.  

    5.  Klicken Sie auf **OK** , um die Kennwortänderungen zu speichern, und klicken Sie dann auf **OK**.  

#### <a name="re-enter-sideloading-keys"></a>Sideload-Schlüssel neu eingeben  
 Nach der Wiederherstellung eines Standortservers müssen Sie die Windows-Sideload-Schlüssel für den Standort erneut eingeben, weil diese im Rahmen der Standortwiederherstellung zurückgesetzt werden. Nach dem erneuten Eingeben der Sideload-Schlüssel wird der Zähler in der Spalte **Verwendete Aktivierungen** für Windows-Sideload-Schlüssel in der Configuration Manager-Konsole zurückgesetzt. Angenommen, vor dem Standortausfall hätte der Zähler **Aktivierungen insgesamt** den Wert **100** und **Verwendete Aktivierungen** den Wert **90** für die Anzahl der von Geräten verwendeten Schlüssel gehabt. Nach der Standortwiederherstellung zeigt die Spalte **Aktivierungen insgesamt** weiterhin **100**an, der Wert in **Verwendete Aktivierungen** wurde jedoch fälschlich auf **0**zurückgesetzt. Wenn nun jedoch Sideload-Schlüssel von zehn weiteren Geräten verwendet werden, sind nachfolgend keine Sideload-Schlüssel mehr übrig, und für das nächste Gerät wird kein Sideload-Schlüssel mehr zur Anwendung verfügbar sein.  

#### <a name="recreate-the-microsoft-intune-subscription"></a>Neuerstellen des Microsoft Intune-Abonnements  
 Wenn Sie einen Configuration Manager-Standortserver wiederherstellen, nachdem ein neues Image auf den Standortservercomputer aufgespielt wurde, wird das Microsoft Intune-Abonnement nicht wiederhergestellt. Sie müssen Ihr Abonnement nach dem Wiederherstellen des Standorts erneut verbinden.  Erstellen Sie keine neue APN-Anforderung, sondern laden Sie stattdessen die aktuell gültige PEM-Datei hoch, die bei der letzten Konfiguration oder Erneuerung der iOS-Verwaltung hochgeladen wurde. Weitere Informationen finden Sie unter [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).  

#### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Konfigurieren von SSL für Standortsystemrollen, die IIS verwenden  
 Wenn Sie Standortserver wiederherstellen, auf denen IIS ausgeführt wird und die vor dem Auftreten des Fehlers für HTTPS konfiguriert wurden, müssen Sie IIS für die Verwendung des Webserverzertifikats umkonfigurieren.  

#### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>Erneutes Installieren von Hotfixes auf dem wiederhergestellten Standortserver  
 Nach der Wiederherstellung eines Standorts müssen Sie alle Hotfixes neu installieren, die auf den Standortserver angewendet worden waren. Die zuvor installierten Hotfixes werden nach Abschluss der Standortwiederherstellung im Setup-Assistenten auf der Seite **Fertig gestellt** aufgelistet und auf dem wiederhergestellten Standortserver unter **C:\ConfigMgrPostRecoveryActions.html** gespeichert.  

#### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>Wiederherstellen von benutzerdefinierten Berichten auf dem Computer, auf dem Reporting Services ausgeführt wird  
 Wenn Sie benutzerdefinierte Reporting Services-Berichte erstellt haben und ein Fehler in Reporting Services auftritt, können Sie die Berichte wiederherstellen, sofern der Berichtsserver gesichert wurde. Weitere Informationen zum Wiederherstellen benutzerdefinierter Berichte in Reporting Services finden Sie unter [Sicherungs- und Wiederherstellungsvorgänge für eine Reporting Services-Installation](http://go.microsoft.com/fwlink/p/?LinkId=228724) in der Onlinedokumentation zu SQL Server 2008.  

#### <a name="recover-content-files"></a>Wiederherstellen von Inhaltsdateien  
 Die Standortdatenbank enthält Informationen zum Speicherort der Inhaltsdateien auf dem Standortserver, jedoch werden die Inhaltsdateien beim normalen Sicherungs- und Wiederherstellungsverfahren nicht berücksichtigt. Zum vollständigen Wiederherstellen von Inhaltsdateien müssen Sie die Inhaltsbibliothek und die Paketquelldateien am Originalspeicherort wiederherstellen. Es gibt verschiedene Methoden zum Wiederherstellen von Inhaltsdateien. Am einfachsten ist die Wiederherstellung der Dateien aus einer Sicherung des Dateisystems des Standortservers.  

 Wenn eine Sicherung des Dateisystems für die Paketquelldateien nicht verfügbar ist, müssen Sie diese Dateien wie beim ursprünglichen Erstellen des Pakets manuell kopieren bzw. herunterladen. Sie können die folgende Abfrage in SQL Server ausführen, um den Quellspeicherort für alle Pakete und Anwendungen zu ermitteln: `SELECT * FROM v_Package`. Sie können den Paketquellstandort anhand der ersten drei Zeichen der Paket-ID identifizieren. Wenn beispielsweise die Paket-ID „CEN00001“ lautet, ist „CEN“ der Standortcode für den Quellstandort. Paketquelldateien müssen an den gleichen Speicherort wiederhergestellt werden wie vor dem Fehler.  

 Wenn eine Sicherung des Dateisystems mit der Inhaltsbibliothek nicht verfügbar ist, gibt es folgende Möglichkeiten zur Wiederherstellung:  

-   **Importieren einer vorab bereitgestellten Inhaltsdatei**: Wenn Sie über eine Configuration Manager-Hierarchie verfügen, können Sie eine vorab bereitgestellte Inhaltsdatei mit allen Paketen und Anwendungen von einem anderen Speicherort erstellen und anschließend die vorab bereitgestellte Inhaltsdatei importieren, um die Inhaltsbibliothek auf dem Standortserver wiederherzustellen.  

-   **Aktualisieren des Inhalts**: Wenn Sie die Aktion zum Aktualisieren des Inhalts für den Bereitstellungstyp eines Pakets oder einer Anwendung starten, wird der Inhalt aus der Paketquelle in die Inhaltsbibliothek kopiert. Die Paketquelldateien müssen im ursprünglichen Speicherort verfügbar sein, damit diese Aktion erfolgreich ausgeführt werden kann. Sie müssen diese Aktion für jedes Paket und jede Anwendung ausführen.  

#### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>Wiederherstellen von benutzerdefinierten Softwareupdates auf dem Computer, auf dem Updates Publisher ausgeführt wird  
 Wenn Sie Updates Publisher-Datenbankdateien in Ihren Sicherungsplan einbezogen haben, können Sie die Datenbanken wiederherstellen, falls auf dem Computer, auf dem Updates Publisher ausgeführt wird, ein Fehler auftritt. Weitere Informationen zu Updates Publisher finden Sie unter [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) in der System Center TechNet-Bibliothek.  

 Gehen Sie wie folgt vor, um die Updates Publisher-Datenbank wiederherzustellen.  

###### <a name="to-restore-the-updates-publisher-2011-database"></a>So stellen Sie die Updates Publisher 2011-Datenbank wieder her  

1.  Installieren Sie Updates Publisher auf dem wiederhergestellten Computer neu.  

2.  Kopieren Sie die Datenbankdatei (Scupdb.sdf) von Ihrem Sicherungsziel nach „%*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\“ auf dem Computer, auf dem Updates Publisher ausgeführt wird.  

3.  Wenn Updates Publisher auf dem Computer von mehreren Benutzern ausgeführt wird, müssen Sie jede Datenbankdatei in den Speicherort für das entsprechende Benutzerprofil kopieren.  

#### <a name="user-state-migration-data"></a>Daten zur Benutzerzustandsmigration  
 In den Standortsystemeigenschaften für den Zustandsmigrationspunkt geben Sie die Ordner an, in denen die Daten zur Benutzerzustandsmigration gespeichert werden. Nach der Wiederherstellung eines Servers mit einem Ordner, in dem Daten zur Benutzerzustandsmigration gespeichert sind, müssen Sie die Daten zur Benutzerzustandsmigration auf dem Server manuell in den gleichen Ordner wiederherstellen, in dem sie vor dem Auftreten des Fehlers gespeichert waren.  

#### <a name="regenerate-the-certificates-for-distribution-points"></a>Generieren der Zertifikate für Verteilungspunkte  
 Nach der Wiederherstellung eines Standorts kann die Datei „distmgr.log“ den folgenden Eintrag für einen oder mehrere Verteilungspunkte enthalten: **Fehler beim Entschlüsseln der Zertifikat-PFX-Daten**. Dieser Eintrag gibt an, dass die Verteilungspunktzertifikat-Daten nicht vom Standort entschlüsselt werden können. Zum Beheben dieses Problems müssen Sie das Zertifikat für die betroffenen Verteilungspunkte erneut generieren oder erneut importieren. Dies kann mithilfe des PowerShell-Cmdlets [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) erfolgen.  

#### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Aktualisieren von Zertifikaten für cloudbasierte Verteilungspunkte  
 Für Configuration Manager ist ein Verwaltungszertifikat erforderlich, das für die Kommunikation zwischen Standortserver und cloudbasiertem Verteilungspunkt verwendet wird. Nach einer Standortwiederherstellung müssen Sie die Zertifikate für cloudbasierte Verteilungspunkte aktualisieren.  

####  <a name="BKMK_RecoverSecondarySite"></a> Wiederherstellen eines sekundären Standorts  
 Die Sicherung der Datenbank an einem sekundären Standort wird von Configuration Manager nicht unterstützt, während die Wiederherstellung durch Neuinstallation des sekundären Standorts unterstützt wird. Bei einem Fehler auf einem sekundären Standort von Configuration Manager ist eine Wiederherstellung des sekundären Standorts erforderlich. Sie können einen sekundären Standort wiederherstellen, indem Sie in der Configuration Manager-Konsole unter dem Knoten **Standorte** die Aktion **Sekundären Standort wiederherstellen** verwenden. Im Gegensatz zur Wiederherstellung für einen Standort der zentralen Verwaltung oder einen primären Standort verwendet die Wiederherstellung für einen sekundären Standort keine Sicherungsdatei und installiert stattdessen die sekundären Standortdateien auf dem fehlerhaften Computer des sekundären Standorts neu. Anschließend werden die Daten des sekundären Standorts mit Daten vom übergeordneten primären Standort neu initialisiert. Während des Wiederherstellungsprozesses wird von Configuration Manager überprüft, ob die Inhaltsbibliothek auf dem Computer des sekundären Standorts vorhanden und der entsprechende Inhalt verfügbar ist. Der sekundäre Standort verwendet die vorhandene Inhaltsbibliothek, wenn sie den entsprechenden Inhalt enthält. Andernfalls muss zum Wiederherstellen der Inhaltsbibliothek eines wiederhergestellten sekundären Standorts der Inhalt für diesen wiederhergestellten Standort verteilt oder vorab bereitgestellt werden. Bei einem Verteilungspunkt, der sich nicht am sekundären Standort befindet, müssen Sie während der Wiederherstellung des sekundären Standorts den Verteilungspunkt nicht neu installieren. Nach der Wiederherstellung des sekundären Standorts wird der Standort automatisch mit dem Verteilungspunkt synchronisiert.  

 Sie können den Status der Wiederherstellung des sekundären Standorts überprüfen, indem Sie in der Configuration Manager-Konsole unter dem Knoten **Standorte** die Aktion **Installationsstatus anzeigen** verwenden.  

> [!IMPORTANT]  
>  Sie müssen einen Computer mit derselben Konfiguration wie der des fehlerhaften Computers verwenden, wie etwa dessen FQDN, um den sekundären Standort erfolgreich wiederherzustellen. Der Computer muss außerdem alle Voraussetzungen für einen sekundären Standort erfüllen, und es müssen die entsprechenden Sicherheitsrechte konfiguriert sein. Außerdem verwenden Sie den gleichen Installationspfad, der für den fehlerhaften Standort verwendet wurde.  

> [!IMPORTANT]  
>  Während der Wiederherstellung eines sekundären Standorts wird SQL Server Express nicht von Configuration Manager installiert, wenn dies nicht auf dem Computer installiert ist. Daher müssen Sie vor der Wiederherstellung des sekundären Standorts SQL Server Express oder SQL Server manuell installieren. Sie müssen dieselbe Version und Instanz von SQL Server verwenden, die Sie vor Auftreten des Fehlers für die sekundäre Standortdatenbank verwendet haben.  

##  <a name="BKMK_SMSWriterService"></a> SMS-Writer-Dienst  
 Während des Sicherungsprozesses findet zwischen dem SMS-Writer-Dienst und dem Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) eine Interaktion statt. Der SMS-Writer-Dienst muss ausgeführt werden, damit die Configuration Manager-Standortsicherung erfolgreich abgeschlossen werden kann.  

### <a name="purpose"></a>Zweck  
 SMS-Writer wird beim VSS registriert und an dessen Schnittstellen und Ereignissse gebunden. Wenn vom VSS Ereignisse übertragen oder bestimmte Benachrichtigungen an SMS-Writer gesendet werden, wird von SMS-Writer daraufhin eine entsprechende Aktion ausgeführt. Zunächst wird die Sicherungssteuerungsdatei „smsbkup.ctl“, die sich unter „&lt;*Configuration Manager-Installationspfad*>\inboxes\smsbkup.box“ befindet, von SMS-Writer gelesen, und dann werden die zu sichernden Dateien und Daten ermittelt. Anschließend werden von SMS-Writer Metadaten erstellt, die sich aus verschiedenen Komponenten zusammensetzen. Dabei dienen die ermittelten Informationen sowie bestimmte Daten aus den SMS-Registrierungsschlüsseln und Unterschlüsseln als Grundlage. Die Metadaten werden an den VSS gesendet, wenn sie angefordert werden. Vom VSS werden die Metadaten wiederum an die anfordernde Anwendung gesendet (Configuration Manager-Sicherungs-Manager). Vom Sicherungs-Manager werden die zu sichernden Daten ausgewählt und über den VSS an SMS-Writer gesendet. Von SMS-Writer werden geeignete Maßnahmen zur Vorbereitung der Sicherung ergriffen. Vom VSS wird ein Ereignis gesendet, wenn er für die Momentaufnahme bereit ist. Daraufhin werden von SMS-Write sämtliche Configuration Manager-Dienste angehalten, und es wird sichergestellt, dass die Configuration Manager-Aktivitäten während der Erstellung der Momentaufnahme gesperrt sind. Nachdem die Momentaufnahme erstellt wurde, werden die Dienste und Aktivitäten von SMS-Writer neu gestartet.  

 Der SMS-Writer-Dienst wird automatisch installiert. Dieser Dienst muss ausgeführt werden, wenn eine Sicherungs- oder Wiederherstellungsanforderung von der VSS-Anwendung eingeht.  

### <a name="writer-id"></a>Writer-ID  
 Die Writer-ID für SMS-Writer lautet: 03ba67dd-dc6d-4729-a038-251f7018463b.  

### <a name="permissions"></a>Berechtigungen  
 Der SMS-Writer-Dienst muss unter dem lokalen Systemkonto ausgeführt werden.  

### <a name="volume-shadow-copy-service"></a>Volumeschattenkopie-Dienst  
 Der Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) ist ein Satz COM APIs, mit denen ein Framework implementiert wird. Dank dieses Frameworks können Volumesicherungen ausgeführt werden, während von Anwendungen auf einem System weiterhin auf die Volumes geschrieben wird. Mit dem VSS wird eine konsistente Schnittstelle bereitgestellt, mit der Benutzeranwendungen, die zum Ausführen eines Updates für Daten auf einem Datenträger dienen (SMS-Writer-Dienst), und Benutzeranwendungen, die zur Anwendungssicherung verwendet werden (Sicherungs-Manager-Dienst), koordiniert werden können. Weitere Informationen zum VSS finden Sie im Thema [Volume Shadow Copy Service (Volumeschattenkopie-Dienst)](http://go.microsoft.com/fwlink/p/?LinkId=241968) im Windows Server TechCenter.  

