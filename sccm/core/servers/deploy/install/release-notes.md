---
title: Anmerkungen zu dieser Version | System Center Configuration Manager
description: In diesen Anmerkungen finden Sie Informationen zu dringenden Problemen, die im Produkt noch nicht behoben oder bisher in keinem Microsoft Knowledge Base-Artikel beschrieben wurden.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 41
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 0b6c49f3c5e817f1dbd40b40c78d89c4a018e0f1


---
# <a name="release-notes-for-system-center-configuration-manager"></a>Anmerkungen zu dieser Version von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei System Center Configuration Manager sind Anmerkungen zur Produktversion auf dringende Probleme beschränkt, die noch nicht im Produkt behoben wurden (in einem konsoleninternen Update verfügbar sind) oder in einem Microsoft Knowledge Base-Artikel beschrieben sind.  

 Informationen zu bekannten Problemen, die wichtige Szenarien betreffen, sind in der Onlineproduktdokumentation in der System Center Configuration Manager-Dokumentationsbibliothek beschrieben.  

> [!TIP]  
>  Dieses Thema enthält Anmerkungen System Center Configuration Manager Current Branch. Wenn Sie eine Technical Preview-Version von System Center Configuration Manager verwenden, finden Sie unter [Technical Preview for System Center Configuration Manager (Technical Preview für System Center Configuration Manager)](../../../../core/get-started/technical-preview.md) weitere Informationen.  

## <a name="setup-and-upgrade"></a>Setup und Upgrade  



### <a name="the-sql-server-backup-model-in-use-by-configuration-manager-can-change-from-full-to-simple"></a>Das von Configuration Manager verwendete SQL Server-Sicherungsmodell kann von „Vollständig“ auf „Einfach“ geändert werden.  
 Beim Upgrade auf System Center Configuration Manager, Version 1511, kann sich das von Configuration Manager verwendete SQL Server-Sicherungsmodell vom vollständigen in das einfache Modell ändern.  

-   Wenn Sie einen benutzerdefinierten SQL Server-Sicherungstask mit dem vollständigen Sicherungsmodell (anstelle des integrierten Sicherungstasks für Configuration Manager) verwenden, kann das Sicherungsmodell durch das Upgrade vom vollständigen in das einfache Modell geändert werden.  

**Problemumgehung**: Überprüfen Sie nach dem Upgrade auf Version 1511 die SQL Server-Konfiguration, und stellen Sie ggf. das vollständige Modell wieder her.  

### <a name="when-you-add-a-service-window-to-a-new-site-server-service-windows-that-were-configured-for-another-site-server-are-deleted"></a>Wenn Sie einem neuen Standortserver ein Dienstfenster hinzufügen, werden die für einen anderen Standortserver konfigurierten Dienstfenster gelöscht.  
 Bei Verwendung von Dienstfenstern mit System Center Configuration Manager, Version 1511, können diese nur für einen einzelnen Standortserver in einer Hierarchie konfiguriert werden. Wenn Sie nach dem Konfigurieren von Dienstfenstern auf einem Server ein Dienstfenster auf einem zweiten Standortserver konfigurieren, werden die Dienstfenster auf dem ersten Standortserver im Hintergrund und ohne Warnung oder Fehler gelöscht.  

**Problemumgehung**: Installieren Sie den Hotfix aus dem [Microsoft Knowledge Base-Artikel 3142341](http://support.microsoft.com/kb/3142341). Dieses Problem wird auch durch Installation von Update 1602 für System Center Configuration Manager behoben.  

### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Ein Update bleibt im Knoten „Updates und Wartung“ der Configuration Manager-Konsole im Status „Wird heruntergeladen“ hängen  
Während des automatischen Downloads von Updates durch einen Online-Dienstverbindungspunkt kann ein Update im Status „Wird heruntergeladen“ hängen bleiben. In diesem Fall werden in den angegebenen Protokolldateien Einträge ähnlich den folgenden angezeigt:  

DMPdownloader.log:  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log:  

-   Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Problemumgehung:** Ändern Sie auf dem Standortserver den folgenden Registrierungsschlüssel auf den unten angegebenen, und starten Sie anschließend den SMS_Executive-Dienst neu, oder warten Sie bis zu 24 Stunden auf den nächsten automatischen Downloadzyklus.  

-   **Zu bearbeitender Schlüssel:** HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Wert für Status:** Auf **146944** (dezimal) oder **0x00023e00** (hexadezimal) festlegen  

### <a name="pre-release-features-introduced-in-system-center-configuration-manager-1602"></a>Vorab veröffentlichte Features in System Center Configuration Manager 1602  

Vorab veröffentlichte Features werden in das Produkt aufgenommen, um sie in einem frühen Stadium in einer Produktionsumgebung zu testen. Sie sollten nicht als für den Produktivbetrieb geeignet betrachtet werden.  

Ab Update 1606 müssen Sie vor der Nutzung von Vorabfeatures Ihr Einverständnis erklären. Weitere Informationen finden Sie unter [Use pre-release features from updates](../../../../core/servers/manage/install-in-console-updates.md) (Verwenden von Vorabfeatures aus Updates).

Mit der System Center Configuration Manager Version 1602 werden zwei neue vorab veröffentlichte Features eingeführt:  

-   Bedingter Zugriff für PCs, die von System Center Configuration Manager verwaltet werden. Weitere Informationen finden Sie unter [Manage access to O365 services for PCs managed by System Center Configuration Manager (Verwalten des Zugriffs auf Office 365-Dienste für PCs, die von System Center Configuration Manager verwaltet werden)](../../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).
    - Nach der Installation von Update 1602 wird der Featuretyp als endgültige Version angezeigt, obwohl es sich um eine Vorabversion handelt.
    - Wenn Sie anschließend von 1602 auf 1606 aktualisieren, wird der Featuretyp als endgültige Version angezeigt, obwohl es sich weiterhin um eine Vorabversion handelt.
    - Wenn Sie von Version 1511 direkt auf 1606 aktualisieren, wird der Featuretyp als Vorabversion angezeigt.


-   Warten einer clusterfähigen Sammlung. Weitere Informationen finden Sie unter [Service a server group](../../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups) (Warten einer Servergruppe) in [Capabilities in Technical Preview 1605 for System Center Configuration Manager](../../../../core/get-started/capabilities-in-technical-preview-1605.md) (Funktionen in Technical Preview 1605 für System Center Configuration Manager).  




### <a name="recovery-options-for-a-secondary-site-are-not-available-in-the-console"></a>Wiederherstellungsoptionen für einen sekundären Standort sind in der Konsole nicht verfügbar  
Wenn bei der Wiederherstellung eines sekundären Standorts ein Fehler auftritt, ist die Option **Sekundären Standort wiederherstellen** möglicherweise nicht mehr in der Configuration Manager-Konsole verfügbar.  

Dieses Problem betrifft System Center Configuration Manager Version 1511 und 1602 und soll in einem zukünftigen Update behoben werden.  

**Problemumgehung**: Verwenden Sie eine der folgenden Methoden, um den sekundären Standort wiederherzustellen (neu zu installieren):  

-   Verwenden Sie die Befehle **Preinst.exe** und **/delsite**, um den sekundären Standort zu entfernen, und installieren Sie den sekundären Standort erneut. Weitere Informationen finden Sie unter [Hierarchiewartungstool (Preinst.exe) für System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

-   Führen Sie das folgende Skript aus, um die Wiederherstellung des sekundären Standorts zu starten. Dieses Skript wird in der Datenbank auf dem primären übergeordneten Standort des sekundären Standorts ausgeführt, den Sie wiederherstellen möchten:  

    ```  
    declare @SiteCode NVARCHAR(3)=N'<replace with secondary site code>'   

    UPDATE Sites SET Status = 9  
                    , DetailedStatus = 3  
    FROM Sites WHERE SiteCode = @SiteCode  

    UPDATE SCP SET SCP.Value1 = 9  
                    , SCP.Value2 = N'3'  
    FROM SC_SiteDefinition_Property SCP INNER JOIN SC_SiteDefinition SC ON SC.SiteNumber = SCP.SiteNumber  
    WHERE SC.SiteCode = @SiteCode AND SCP.[Name] = N'Requested Status'  
  ```  

###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>Manifestüberprüfungsfehler beim Setup, wenn verteilbare Dateien aus dem Ordner „CD.latest“ verwendet werden.
Fehler beim Ausführen von Setup mit den folgenden Fehlermeldungen im Setup-Protokoll für Configuration Manager, wenn Setup über einen für Version 1606 erstellten „CD.latest“-Ordner ausgeführt wird und die verteilbaren Dateien in diesem „CD.latest“-Ordner verwendet werden:

  - FEHLER: File hash check failed for defaultcategories.dll (Fehler bei Dateihashüberprüfung für „defaultcategories.dll“).
  - FEHLER: Manifest verification failed (Fehler bei Manifestüberprüfung). Falsche Version des Manifests?

**Problemumgehung:** Folgende Problemumgehungen sind möglich:
 - Laden Sie beim Ausführen des Setups die aktuellen verteilbaren Dateien von Microsoft herunter, um diese anstelle der im Ordner „CD.latest“ enthaltenden Dateien zu verwenden.
 - Löschen Sie den Ordner *cd.latest\redist\languagepack\zhh*, und führen Sie anschließend Setup erneut aus.

## <a name="backup-and-recovery"></a>Sicherung und Wiederherstellung
### <a name="pre-production-client-is-not-available-after-a-site-restore"></a>Der Präproduktionsclient ist nach einer Standortwiederherstellung nicht verfügbar
Wenn Sie in Version 1602 Präproduktionsclients verwenden und den Standort der obersten Ebene in Ihrer Hierarchie aus einer Sicherung wiederherstellen, ist die Version des Präproduktionsclients nach der Wiederherstellung des Standorts nicht verfügbar.  

**Problemumgehung:** Nach dem Wiederherstellen des Standorts der obersten Ebene in Ihrer Hierarchie müssen Sie die Dateien des Präproduktionsclients manuell kopieren, damit Configuration Manager sie für die Verwendung verarbeiten und wiederherstellen kann:
1. Kopieren Sie auf dem Standortservercomputer der obersten Ebene den Inhalt des Ordners *&lt;CM_Install_Location\>\\Client* in den Ordner *&lt;CM_Install_Location\>\\StagingClient*.

2. Erstellen Sie eine leere Datei namens **client.acu**, und kopieren Sie diese Datei in den Ordner *&lt;CM_Install_Location\>\\Inboxes\\hman.box* auf dem Standortserver. (Diese Datei kann eine umbenannte Textdatei sein, solange diese nicht mehr die Erweiterung TXT aufweist). Nachdem Sie diese Datei im Ordner „hman.box“ platziert wurde, startet der Hierarchie\-Manager auf dem Standortserver, verarbeitet die Clientdateien und stellt die zu verwendenden Dateien des Präproduktionsclients wieder her.

Dieses Problem wurde in Version 1606 behoben.


## <a name="client-deployment-and-upgrade"></a>Clientbereitstellung und -upgrade  

### <a name="expansion-to-central-administration-site-stops-automatic-client-upgrades"></a>Durch Erweiterung auf einen Standort der zentralen Verwaltung werden automatische Clientupgrades beendet  
Gilt nur für Version 1511: Sie können keine automatischen Clientupgrades für einen Standort durchführen, der von einem primären Standort auf einen Standort der zentralen Verwaltung erweitert wurde. Wenn der Standort erweitert wird, wird der autorisierende Standort im Clientupgradepaket nicht ordnungsgemäß auf den neuen Standort der zentralen Verwaltung festgelegt, sodass automatische Clientupgrades nicht erfolgreich ausgeführt werden können. Dieses Problem besteht nur in Version 1511. In Version 1602 und höhere wurde das Problem behoben.  

**Problemumgehung**: Führen Sie das folgende SQL-Skript in der Datenbank am Standort der zentralen Verwaltung aus. Nach Ausführung des Skripts sollten automatische Clientupgrades normal ausgeführt werden.  

  ```  
  DECLARE @RootSite AS NVARCHAR(3)  
  DECLARE @SourceServer AS NVARCHAR(255)  
  DECLARE @FullClientPkgSource AS NVARCHAR(255)  
  DECLARE @UpgradePkgSource AS NVARCHAR(255)  

  SELECT @RootSite = SiteCode, @SourceServer = SiteServer  
  FROM sites  
  WHERE ISNULL(ReportToSite, N'') = N''  

  SELECT @FullClientPkgSource = N'\\' + @SourceServer + N'\SMS_' + @RootSite + N'\Client'  
  SELECT @UpgradePkgSource = N'\\' + @SourceServer + N'\SMS_' + @RootSite + N'\ClientUpgrade'  

  UPDATE SMSPackages_G  
  SET Source = @FullClientPkgSource, SourceSite = @RootSite  
  WHERE PkgID IN  
      (SELECT FullPackageID FROM ClientDeploymentSettings)  

  UPDATE SMSPackages_G  
  SET Source = @UpgradePkgSource, SourceSite = @RootSite  
  WHERE PkgID IN  
      (SELECT UpgradePackageID FROM ClientDeploymentSettings)  

  UPDATE ProgramOffers_G  
  SET SourceSite = @RootSite  
  WHERE OfferID IN  
      (SELECT UpgradeAdvertisementID FROM ClientDeploymentSettings)  
  ```  

## <a name="operating-system-deployment"></a>Betriebssystembereitstellung  

### <a name="issue-with-the-windows-adk-for-windows-10-version-1511"></a>Probleme mit dem Windows ADK für Windows 10, Version 1511  
Wenn Sie über das Softwarecenter eine Tasksequenz ausführen, die ein Windows PE v.10.0.10586-Startimage der Version 1511 von Windows ADK 10 verwendet, tritt beim Neustarten des Computers mit Windows PE während der Initialisierung von Hardwaregeräten folgender Fehler auf: **Fehler bei der Windows PE-Initialisierung; Fehlercode 0x80220014**.  

**Problemumgehung**: Verwenden Sie das ursprüngliche Windows 10 ADK. Weitere Informationen finden Sie im folgenden System Center Configuration Manager-Teamblog: [Problem mit dem Windows ADK für Windows 10](http://blogs.technet.com/b/configmgrteam/archive/2015/11/20/issue-with-the-windows-adk-for-windows-10-version-1511.aspx).  

### <a name="dynamic-application-installation-fails-during-task-sequence-which-successfully-completes"></a>Bei der dynamischen Anwendungsinstallation tritt während der Tasksequenz, die erfolgreich abgeschlossen wurde, ein Fehler auf  
Wenn Sie eine Tasksequenz bereitstellen, die die Option **Anwendungen entsprechend der dynamischen Variablenliste installieren**verwendet, und eine Anwendung aus irgendeinem Grund nicht installiert werden kann, wird von der Tasksequenz gemeldet, dass der Vorgang erfolgreich gewesen sei. Dieses Verhalten tritt unabhängig von der Konfiguration der folgenden Optionen auf:  

-   **Bei Fehler fortsetzen** (auf der Registerkarte „Optionen“ des Schritts „Anwendung installieren“)  

-   **Bei Installationsfehler einer Anwendung die Installation der anderen Anwendungen auf der Liste fortsetzen** (auf der Registerkarte „Eigenschaften“ des Schritts „Anwendung installieren“)  

Sie können „smsts.log“ anzeigen, um zu bestimmen, ob bei der Installation einer Anwendung ein Fehler aufgetreten ist.  

**Problemumgehung**: Verwenden Sie die **_TSAppInstallStatus** -Variable in einem nachfolgenden Schritt in einer Tasksequenz als eine Bedingung, wodurch die Tasksequenz fehlschlägt, wenn bei einer der dynamischen Anwendungen ein Fehler auftritt.  

### <a name="smb-might-not-work-properly-after-you-use-a-task-sequence-to-install-windows-10"></a>SMB funktioniert nach Verwendung einer Tasksequenz zur Installation von Windows 10 möglicherweise nicht ordnungsgemäß  
Wenn Sie zum Installieren von Windows 10 eine Tasksequenz verwenden, funktioniert SMB möglicherweise nicht ordnungsgemäß, nachdem der Configuration Manager-Client installiert wurde. Bei folgenden Tasksequenzschritten tritt möglicherweise ein Fehler auf:  

-   Benutzerzustand wiederherstellen – bei Verwendung mit einem Zustandsmigrationspunkt  

-   Verbindung mit Netzwerkordner herstellen  

Sie können den Computer von einer Administratoreingabeaufforderung (F8) weiterhin pingen, bei jeglichem SMB-Netzwerkdatenverkehr (beispielsweise NET USE von einer Eingabeaufforderung) tritt jedoch der Fehler 1231 auf – die Netzwerkadresse ist nicht erreichbar.  

**Problemumgehung**:  
Fügen Sie nach dem Tasksequenzschritt „Windows und ConfigMgr einrichten“ einen Tasksequenzschritt „Befehlszeile ausführen“ ein, um die Tasksequenz anzuhalten, und starten Sie anschließend den Arbeitsstationsdienst wie folgt:    
**net stop workstation /y & net start workstation**  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Wartungspläne erstellen standardmäßig eine Vielzahl von doppelten Softwareupdategruppen und -bereitstellungen  
Der Assistent zum Erstellen eines Wartungsplans wird zurzeit standardmäßig nach jedem Synchronisierungsvorgang für Softwareupdates ausgeführt. Bei jeder Ausführung erstellt der Assistent eine neue Softwareupdategruppe und -bereitstellung. Wenn Sie z. B. über einen Synchronisierungszeitplan für Softwareupdates verfügen, der mehrmals täglich ausgeführt wird, erstellt der Assistent zum Erstellen eines Wartungsplans jeden Tag mehrere, wahrscheinlich identische, Softwareupdategruppen und -bereitstellungen.  

**Problemumgehung**:    
Nachdem Sie einen Wartungsplan erstellt haben, öffnen Sie die Eigenschaften des Plans, wechseln Sie zur Registerkarte **Auswertungszeitplan**, wählen Sie **Regel nach Zeitplan ausführen** aus, klicken Sie auf **Anpassen**, und erstellen Sie einen benutzerdefinierten Zeitplan. Sie können den Wartungsplan beispielsweise alle 60 Tage ausführen.  

## <a name="mobile-device-management"></a>Verwaltung mobiler Geräte  

### <a name="cannot-create-an-enrollment-profile-on-a-primary-site"></a>An einem primären Standort konnte kein Anmeldungsprofil erstellt werden  
Ein Administrator kann in der System Center Configuration Manager-Verwaltungskonsole, die eine Verbindung mit einem primären Standort herstellt, kein Anmeldungsprofil erstellen. Beim Registrieren wird dem Administrator im Assistent zum Erstellen von Registrierungsprofilen folgender Fehler angezeigt: „Das DEP-Token wurde nicht hochgeladen. Laden Sie ein DEP-Token hoch.“ Dieser Fehler tritt auf, obwohl ein gültiges DEP-Token an den Standort der zentralen Verwaltung hochgeladen wurde.  

**Problemumgehung**: Erstellen Sie ein Anmeldungsprofil in der System Center Configuration Manager-Konsole, die eine Verbindung mit dem Standort der zentralen Verwaltung herstellt.  

### <a name="dep-cannot-use-non-alpha-numeric-characters-in-enrollment-profiles"></a>DEP kann in nur alphanumerische Zeichen Anmeldungsprofilen verwenden.  
In Anmeldungsprofilen, die mit dem Geräteanmeldungsprofil von Apple (Device Enrollment Profile, DEP) verknüpft sind, dürfen die Felder **Name**, **Beschreibung**, **Abteilung** und **Telefonnummer** des Anmeldungsprofils bei aktiviertem DEP nur alphanumerische Zeichen enthalten. Werden in diesen Feldern nicht alphanumerische Zeichen verwendet, wird das Anmeldungsprofil zwar erstellt, kann aber nicht zu Apple hochgeladen werden. Vom Apple-Server wird keine Fehlermeldung oder Warnung gesendet, und die Profile werden für DEP verwaltete Geräte nicht bereitgestellt.  

**Problemumgehung:** Keine

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>Das vollständige Zurücksetzen deaktiviert Windows 10-Geräte mit weniger als 4 GB RAM.

Eine vollständige Zurücksetzung von Windows 10 RTM-Geräten (frühere Versionen als Version 1511) mit weniger als 4 GB RAM machen das Gerät unbrauchbar. Nach dem versuchten Zurücksetzen des Geräts startet oder reagiert es nicht mehr.

**Problemumgehung**: Stellen Sie sicher, dass Ihre Windows 10 RTM -PCs über mindestens 4 GB RAM verfügen, bevor Sie eine vollständige Zurücksetzung auf dem Gerät ausführen. Geben Sie zum Anzeigen der Versionsnummer des Windows-10-Geräts 'winver' an der Befehlszeile ein. Wenn das Gerät bereits zurückgesetzt wurde und nicht mehr reagiert, verwenden Sie ein bootfähiges Windows 10-USB-Laufwerk, um den Zugriff auf das Gerät zu starten und wiederherzustellen.

### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Wenn ein Benutzer zwei oder mehr Benutzersammlungen angehört, für die eine Geschäftsbedingungsrichtlinie bereitgestellt wurde, werden dem Benutzer mehrere Kopien derselben Geschäftsbedingungen angezeigt  

Wenn ein Administrator mehreren Benutzersammlungen eine Reihe von Geschäftsbedingungen bereitstellt, und ein Benutzer Mitglied von mehreren dieser Sammlungen ist, werden diesem Benutzer beim Öffnen des Unternehmensportals mehrere Kopien identischer Geschäftsbedingungen angezeigt.  Beispiel: Wenn ein Benutzer mit dem Namen „SampleUser“ Mitglied von zwei verschiedenen Benutzersammlungen mit den Namen „CompanyEmployeesFTE“ und „CompanyEmployeesNA“ ist, und die Geschäftsbedingungen namens „CompanyTerms“ sowohl der Sammlung „CompanyEmployeesFTE“ als auch der Sammlung „CompanyEmployeesNA“ bereitgestellt wurde, werden dem Benutzer „SampleUser“ auf der Seite für die Annahme der Geschäftsbedingungen zwei identische Kopien von „CompanyTerms“ angezeigt. Da die Benutzer jeweils nur alle Geschäftsbedingungen annehmen oder ablehnen können, besteht keine Gefahr, dass sich ein mehrdeutiger Zustand ergibt, in dem der Benutzer Geschäftsbedingungen sowohl angenommen als auch abgelehnt hat. Der Akzeptanzbericht für die Geschäftsbedingungen umfasst nur eine Zeile für jeden Satz von Geschäftsbedingungen für den jeweiligen Benutzer, damit in dem Bericht kein Fehler auftritt. Der einzige Effekt ist, dass dem Benutzer auf der Seite zur Annahme der Geschäftsbedingungen zwei Kopien der Geschäftsbedingungen angezeigt werden.  

**Problemumgehung**: Stellen Sie sicher, dass jeder Benutzer nur in einer Auflistung enthalten ist, für die die Geschäftsbedingungen bereitgestellt werden.  

## <a name="reports-and-monitoring"></a>Berichte und Überwachung  

### <a name="the-health-attestation-report-is-empty-even-though-health-attestation-data-was-previously-collected"></a>Der Health Attestation-Bericht ist leer, obwohl Integritätsnachweisdaten gesammelt wurden  
Wenn ein Administrator mit einer Sicherheitsrolle, die die Berechtigung **Lesen** für die Berechtigungsgruppe **Health Attestation** umfasst, den Health Attestation-Bericht anzeigt, ist der Bericht leer und zeigt keine Daten an. Dies liegt daran, dass die Berechtigungen zum Anzeigen von Daten im Health Attestation-Bericht mit der Berechtigungsgruppe **Benutzer-/Geräteaffinitäten** verknüpft ist, nicht mit der Berechtigungsgruppe „Health Attestation“.  

Dieses Problem betrifft System Center Configuration Manager mit Update 1602 und soll in einem zukünftigen Update behoben werden.  

**Problemumgehung:** Weisen Sie dem Administrator eine Sicherheitsgruppe zu, die die Berechtigung **Lesen** für die Berechtigungsgruppe **Benutzer-/Geräteaffinitäten** umfasst.  

### <a name="conditional-access"></a>Bedingter Zugriff  

#### <a name="the-same-user-collection-is-not-blocked-from-being-added-to-both-exempted-and-targeted-collections"></a>Das Hinzufügen einer Benutzersammlung sowohl zu einer ausgeschlossenen Sammlung als auch zu einer Zielsammlung wird nicht blockiert  
Dies geschieht nur, wenn Sie dieselbe **Benutzersammlung** zur Seite **Ausnahmensammlung** hinzufügen, **bevor** Sie sie zur Seite **Zielsammlungen** hinzufügen.  Wenn Sie eine **Benutzersammlung** erst zur Seite **Zielsammlungen** hinzufügen und anschließend versuchen, die gleiche **Benutzersammlung** zur Seite **Ausnahmensammlungen** hinzuzufügen, sollte die normale Blockierungsmeldung angezeigt werden.  

Dieses Problem betrifft den bedingten Zugriff von System Center Configuration Manager auf **Exchange lokal** mit Update 1602 und soll in einem zukünftigen Update behoben werden.  

**Problemumgehung:** Fügen Sie die **Benutzersammlung** zur Seite **Zielsammlungen** hinzu, bevor Sie die **Benutzersammlung** auf der Seite **Ausnahmensammlungen** auswählen, oder stellen Sie sicher, dass Sie die gleiche **Benutzersammlung** nicht sowohl einer Zielsammlung als auch einer Ausnahmensammlung hinzufügen.



<!--HONumber=Nov16_HO1-->


