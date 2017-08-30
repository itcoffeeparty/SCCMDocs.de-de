---
title: "Versionshinweise – Configuration Manager | Microsoft-Dokumentation"
description: In diesen Anmerkungen finden Sie Informationen zu dringenden Problemen, die im Produkt noch nicht behoben oder bisher in keinem Microsoft Knowledge Base-Artikel beschrieben wurden.
ms.custom: na
ms.date: 08/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: "41"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: e54c2cd1c3e83609bff6a8cb64fb3c23b26a4eaa
ms.sourcegitcommit: 974fbc4408028c8be28911e5cd646efcf47c7f15
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Anmerkungen zu dieser Version von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei System Center Configuration Manager sind Anmerkungen zur Produktversion auf dringende Probleme beschränkt, die noch nicht im Produkt behoben wurden (in einem konsoleninternen Update verfügbar sind) oder in einem Microsoft Knowledge Base-Artikel beschrieben sind.  

Informationen zu bekannten Problemen, die wichtige Szenarien betreffen, sind in der Onlineproduktdokumentation in der System Center Configuration Manager-Dokumentationsbibliothek beschrieben.  

> [!TIP]  
>  Dieses Thema enthält Anmerkungen System Center Configuration Manager Current Branch. Wenn Sie eine Technical Preview-Version von System Center Configuration Manager verwenden, finden Sie unter [Technical Preview for System Center Configuration Manager (Technical Preview für System Center Configuration Manager)](../../../../core/get-started/technical-preview.md) weitere Informationen.  

Informationen zu den neuen, in den verschiedenen Versionen eingeführten Features finden Sie hier:
- [Neues in Version 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [Neuigkeiten in Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)
- [Neuigkeiten in Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)
   


## <a name="setup-and-upgrade"></a>Setup und Upgrade  

### <a name="after-you-update-a-configuration-manager-console-using-consolesetupexe-from-the-site-server-folder-recent-language-pack-changes-are-not-available"></a>Nachdem Sie eine Configuration Manager-Konsole mithilfe von „ConsoleSetup.exe“ aus dem Ordner des Standortservers aktualisiert haben, sind neuere Änderungen des Sprachpakets nicht verfügbar
<!--  SMS 486420  Applicability should be 1610 and 1702.  -->
*Folgendes gilt für die Versionen 1610 und 1702.*   
Nachdem Sie ein direktes Update einer Konsole mithilfe von „ConsoleSetup.exe“ aus dem Installationsordner eines Standortservers durchgeführt haben, sind kürzlich installierte Sprachpakete möglicherweise nicht verfügbar. Dies hat folgende Gründe:
- An Ihrem Standort wird Version 1610 oder 1702 ausgeführt.
- Die Konsole wurde direkt mithilfe von „ConsoleSetup.exe“ aus dem Installationsordner des Standortservers aktualisiert.

Wenn dieses Problem auftritt, verwendet die neu installierte Konsole nicht die aktuellsten Sprachpakete, die konfiguriert wurden. Es werden keine Fehler zurückgegeben, aber die für die Konsole verfügbaren Sprachpakete haben sich nicht geändert.  

**Problembehebung:** Deinstallieren Sie die aktuelle Konsole, und installieren Sie anschließend die Konsole erneut als neue Installation. Sie können „ConsoleSetup.exe“ aus dem Installationsordner des Standortservers verwenden. Stellen Sie sicher, dass Sie während der Installation die Sprachpaketdateien auswählen, die Sie verwenden möchten.


### <a name="with-version-1702-the-default-site-boundary-group-is-configured-for-use-for-site-assignment"></a>Ab Version 1702 ist die Standardbegrenzungsgruppe für die Standortzuweisung konfiguriert
<!--  SMS 486380   Applicability should only be to 1702. -->
*Folgendes gilt für Version 1702.*  
Die Option **Diese Begrenzungsgruppe für die Standortzuweisung verwenden** ist auf der Registerkarte „Referenz“ der Begrenzungsgruppe aktiviert; außerdem ist dort der Standort als **Zugewiesener Standort** aufgelistet. Die Option ist ausgeblendet, damit die Konfiguration nicht bearbeitet oder entfernt werden kann.

**Problemumgehung:** Keiner Sie können diese Einstellung ignorieren. Die Standard-Standortbegrenzungsgruppe wird nicht für die Standortzuweisung verwendet, obwohl die Standortzuweisung für diese aktiviert ist. Ab Version 1702 stellt diese Konfiguration sicher, dass die Standard-Standortbegrenzungsgruppe dem richtigen Standort zugeordnet ist.



### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Wenn Sie einen Long-Term Servicing Branch-Standort (LTSB) mit Version 1606 installieren, wird ein aktueller Current Branch-Standort installiert
<!-- Consider move to core content  -->
Wenn Sie das Baselinemedium von Version 1606 aus der Version vom Oktober 2016 zum Installieren eines Long-Term Servicing Branch-Standorts (LTSB) verwenden, installiert Setup stattdessen einen Current Branch-Standort. Dies geschieht, weil die Option zum Installieren eines Dienstverbindungspunkts mit der Installation des Standorts nicht ausgewählt ist.

 - Obwohl ein Dienstverbindungspunkt nicht erforderlich ist, muss er während des Setups beim Installieren eines LTSB-Standorts zum Installieren ausgewählt werden.

Nach Abschluss der Installation können Sie den Dienstverbindungspunkt deinstallieren.  Allerdings benötigen Sie einen Dienstverbindungspunkt im Offline- oder Onlinemodus zum Senden von Telemetriedaten und Abrufen von Sicherheitsupdates für die Current Branch- und LTSB-Standorte.

Wenn Ihr Standort als Current Branch-Standort installiert ist und Sie einen LTSB-Standort installieren wollten, können Sie den Standort deinstallieren und anschließend neu installieren. Sie können auch [Microsoft-Hilfe und -Support](http://go.microsoft.com/fwlink/?LinkId=243064) aufrufen, um Unterstützung zu erhalten.  

Damit Sie sehen, welcher Standort installiert ist, wechseln Sie in der Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**, und öffnen Sie die **Hierarchieeinstellungen**. Die Option zum Konvertieren des Standorts zu einem Current Branch-Standort ist nur verfügbar, wenn ein LTSB-Standort installiert ist.  

**Problemumgehung:**  Keine.   


### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Ein Update bleibt im Knoten „Updates und Wartung“ der Configuration Manager-Konsole im Status „Wird heruntergeladen“ hängen  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
Während des automatischen Downloads von Updates durch einen Online-Dienstverbindungspunkt kann ein Update im Status „Wird heruntergeladen“ hängen bleiben. In diesem Fall werden in den angegebenen Protokolldateien Einträge ähnlich den folgenden angezeigt:  

DMPdownloader.log:  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log:  

-   Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Problemumgehung:** Ändern Sie auf dem Standortserver den folgenden Registrierungsschlüssel auf den unten angegebenen, und starten Sie anschließend den SMS_Executive-Dienst neu, oder warten Sie bis zu 24 Stunden auf den nächsten automatischen Downloadzyklus.  

-   **Zu bearbeitender Schlüssel:** HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Wert für Status:** Auf **146944** (dezimal) oder **0x00023e00** (hexadezimal) festlegen  


###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>Manifestüberprüfungsfehler beim Setup, wenn verteilbare Dateien aus dem Ordner „CD.latest“ verwendet werden.
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

Fehler beim Ausführen von Setup mit den folgenden Fehlermeldungen im Setup-Protokoll für Configuration Manager, wenn Setup über einen für Version 1606 erstellten „CD.latest“-Ordner ausgeführt wird und die verteilbaren Dateien in diesem „CD.latest“-Ordner verwendet werden:

  - FEHLER: File hash check failed for defaultcategories.dll (Fehler bei Dateihashüberprüfung für „defaultcategories.dll“).
  - FEHLER: Manifest verification failed (Fehler bei Manifestüberprüfung). Falsche Version des Manifests?

**Problemumgehung:** Folgende Problemumgehungen sind möglich:
 - Laden Sie beim Ausführen des Setups die aktuellen verteilbaren Dateien von Microsoft herunter, um diese anstelle der im Ordner „CD.latest“ enthaltenden Dateien zu verwenden.
 - Löschen Sie den Ordner *cd.latest\redist\languagepack\zhh*, und führen Sie anschließend Setup erneut aus.


### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>Das Dienstverbindungstool löst eine Ausnahme aus, wenn SQL Server remote verfügbar ist oder Shared Memory deaktiviert ist
<!-- 479223   Fixed in 1702 and later   -->
*Folgendes gilt für Version 1610 und früher.*  
Das Dienstverbindungstool generiert eine Ausnahme, wenn eine der folgenden Bedingungen zutrifft:  
 -  Die Standortdatenbank befindet sich nicht auf dem Computer, der den Dienstverbindungspunkt hostet, und verwendet einen nicht standardmäßigen Port (nicht Port 1433)
 -  Die Standortdatenbank ist auf demselben Server wie der Dienstverbindungspunkt, aber das SQL-Protokoll **Shared Memory** ist deaktiviert

Die Ausnahme ist ähnlich der folgenden:
 - *Nicht behandelte Ausnahme: System.Data.SqlClient.SqlException: Netzwerkbezogener oder instanzspezifischer Fehler beim Herstellen einer Verbindung mit SQL Server. Der Server wurde nicht gefunden oder war nicht zugänglich. Stellen Sie sicher, dass der Instanzname richtig ist und dass SQL Server für das Zulassen von Remoteverbindungen konfiguriert ist. (Anbieter: Named Pipes-Provider, Fehler: 40 – Verbindung mit SQL Server konnte nicht geöffnet werden) --*

**Problemumgehung**: Bei Verwendung des Tools müssen Sie die Registrierung des Servers, der den Dienstverbindungspunkt hostet, mit Informationen zum SQL Server-Port ändern:

   1.   Bearbeiten Sie vor der Verwendung des Tools den folgenden Registrierungsschlüssel, und fügen Sie die Nummer des verwendeten Ports dem Namen des SQL Servers hinzu:
    - Schlüssel: HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - Wert: &lt;SQL Server-Name>
    - Hinzufügen: **,&lt;PORT>**

    Z.B. bei Hinzufügen des Ports *15001* zu einem Server namens *testserver.test.net* wäre der resultierende Schlüssel: ***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001***

   2.   Nachdem Sie den Port in der Registrierung hinzufügen, sollte das Tool normal funktionieren.  

   3.   Nachdem Sie das Tool verwendet haben, ändern Sie für die Schritte **Verbindung** und **Import** den Registrierungsschlüssel auf den ursprünglichen Wert zurück.  


<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Clientbereitstellung und -upgrade  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>Bei der Clientinstallation tritt ein Fehler mit Fehlercode 0x8007064c auf
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*Folgendes gilt für alle aktiven Versionen von Configuration Manager.*   
Wenn Sie den Client auf Windows-Computern bereitstellen, tritt bei der Installation ein Fehler auf. Die Datei „ccmsetup.log“ enthält den Eintrag: „File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation“, gefolgt von „InstallFromManifest failed 0x8007064c“.

**Problemumgehung**: Dieser Fehler wird durch eine zuvor installierte, beschädigte Version von Silverlight verursacht. Versuchen Sie, auf dem betroffenen Computer das folgende Tool auszuführen: [https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## <a name="operating-system-deployment"></a>Betriebssystembereitstellung  

### <a name="if-the-boot-image-contains-drivers-the-image-fails-to-reload-the-current-windows-pe-version-from-the-windows-assessment-and-deployment-kit-adk"></a>Wenn das Startimage Treiber enthält, kann das Image die aktuelle Windows PE-Version nicht erneut aus dem Windows Assessment and Deployment Kit (ADK) laden.
<!-- 495087 -->
Mit dem Updateverteilungspunkt-Assistenten können Sie Updateverteilungspunkte mit einem Startimage, das in der neuesten Version von Windows PE gespeichert ist, aus dem Installationsverzeichnis des Windows Assessment and Deployment Kit (ADK) aktualisieren. Öffnen Sie zum Aktualisieren den Updateverteilungspunkt-Assistenten, und wählen Sie **Neuladen dieses Startimages mit der aktuellen PE-Version von Windows ADK**.

Wenn allerdings Ihr Startimage Treiber enthält, tritt beim Update ein Fehler auf. Stattdessen lädt der Assistent das Image neu aus dem ADK, zeigt ein Ausnahmedialogfeld an, das der Benutzer schließen kann, und dann einen Erfolgsbildschirm. Allerdings werden die aktuellen Configuration Manager-Clientkomponenten dem Startimage nicht hinzugefügt. Das Startimage wird auf dem Verteilungspunkt nicht aktualisiert.

**Problemumgehung**: Führen Sie den Updateverteilungspunkt-Assistenten zweimal aus.

1. Führen Sie den Assistenten mit Auswahl von **Dieses Startimage mit der aktuellen Windows PE-Version aus dem Windows ADK neu laden** aus. Dadurch wird die neueste Version von Windows PE abgerufen.
2. Führen Sie den Assistenten erneut ohne Auswahl von **Dieses Startimage mit der aktuellen Windows PE-Version aus dem Windows ADK neu laden** aus. Hiermit werden die aktuellen Clientbinärdateien abgerufen und das Startimage auf dem Verteilungspunkt aktualisiert.

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Wartungspläne erstellen standardmäßig eine Vielzahl von doppelten Softwareupdategruppen und -bereitstellungen  
Der Assistent zum Erstellen eines Wartungsplans wird zurzeit standardmäßig nach jedem Synchronisierungsvorgang für Softwareupdates ausgeführt. Bei jeder Ausführung erstellt der Assistent eine neue Softwareupdategruppe und -bereitstellung. Wenn Sie z. B. über einen Synchronisierungszeitplan für Softwareupdates verfügen, der mehrmals täglich ausgeführt wird, erstellt der Assistent zum Erstellen eines Wartungsplans jeden Tag mehrere, wahrscheinlich identische, Softwareupdategruppen und -bereitstellungen.  

**Problemumgehung**:    
Nachdem Sie einen Wartungsplan erstellt haben, öffnen Sie die Eigenschaften des Plans, wechseln Sie zur Registerkarte **Auswertungszeitplan**, wählen Sie **Regel nach Zeitplan ausführen** aus, klicken Sie auf **Anpassen**, und erstellen Sie einen benutzerdefinierten Zeitplan. Sie können den Wartungsplan beispielsweise alle 60 Tage ausführen.  


### <a name="when-a-high-risk-deployment-dialog-is-visible-to-a-user-subsequent-high-risk-dialogs-with-a-sooner-deadline-are-not-displayed"></a>Wenn einem Benutzer ein Dialogfeld über eine risikoreiche Bereitstellung angezeigt wird, werden keine nachfolgenden Dialogfelder über risikoreiche Bereitstellungen mit einem früheren Stichtag angezeigt.
<!-- Fixed in 1702 and later -->
*Folgendes gilt für Version 1610 und früher.*   
Nachdem Sie eine risikoreiche Taskbereitstellung für Benutzer erstellt und bereitgestellt haben, wird dem Benutzer ein Dialogfeld über eine risikoreiche Bereitstellung angezeigt. Wenn der Benutzer das Dialogfeld nicht schließt und Sie eine weitere risikoreiche Bereitstellung mit einem früheren Stichtag erstellen, wird dem Benutzer das aktualisierte Dialogfeld nicht angezeigt, weil er das erste Dialogfeld nicht geschlossen hat. Die Bereitstellungen werden dennoch am konfigurierten Stichtag ausgeführt.

**Problemumgehung**:  
Der Benutzer muss das Dialogfeld für die erste risikoreiche Bereitstellung schließen, damit das Dialogfeld für die nächste risikoreiche Bereitstellung angezeigt wird.



## <a name="software-updates"></a>Softwareupdates

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>Das Importieren von Office 365-Clienteinstellungen aus einer Konfigurationsdatei schlägt fehl, wenn sie nicht unterstützte Sprachen enthält
<!-- 489258  Fixed in 1706  -->
*Folgendes gilt für Version 1702 und früher.*   
Wenn Sie die Office 365-Clienteinstellungen aus einer vorhandenen XML-Konfigurationsdatei importieren und die Datei Sprachen enthält, die vom Office 365 ProPlus-Client nicht unterstützt werden, tritt ein Fehler auf. Details finden Sie unter [Bereitstellen von Office 365-Apps für Clients aus dem Office 365-Clientverwaltungsdashboard](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Problemumgehung**:    
Verwenden Sie in der XML-Konfigurationsdatei nur [vom Office 365 ProPlus-Client unterstützte Sprachen](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx).  



## <a name="mobile-device-management"></a>Verwaltung mobiler Geräte  

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>Das vollständige Zurücksetzen deaktiviert Windows 10-Geräte mit weniger als 4 GB RAM.
Eine vollständige Zurücksetzung von Windows 10 RTM-Geräten (frühere Versionen als Version 1511) mit weniger als 4 GB RAM machen das Gerät unbrauchbar. Nach dem versuchten Zurücksetzen des Geräts startet oder reagiert es nicht mehr.

**Problemumgehung**: Stellen Sie sicher, dass Ihre Windows 10 RTM -PCs über mindestens 4 GB RAM verfügen, bevor Sie eine vollständige Zurücksetzung auf dem Gerät ausführen. Geben Sie zum Anzeigen der Versionsnummer des Windows-10-Geräts 'winver' an der Befehlszeile ein. Wenn das Gerät bereits zurückgesetzt wurde und nicht mehr reagiert, verwenden Sie ein bootfähiges Windows 10-USB-Laufwerk, um den Zugriff auf das Gerät zu starten und wiederherzustellen.


### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Wenn ein Benutzer zwei oder mehr Benutzersammlungen angehört, für die eine Geschäftsbedingungsrichtlinie bereitgestellt wurde, werden dem Benutzer mehrere Kopien derselben Geschäftsbedingungen angezeigt  
<!-- 454394    -->
Wenn ein Administrator mehreren Benutzersammlungen eine Reihe von Geschäftsbedingungen bereitstellt, und ein Benutzer Mitglied von mehreren dieser Sammlungen ist, werden diesem Benutzer beim Öffnen des Unternehmensportals mehrere Kopien identischer Geschäftsbedingungen angezeigt.  Beispiel: Wenn ein Benutzer mit dem Namen „SampleUser“ Mitglied von zwei verschiedenen Benutzersammlungen mit den Namen „CompanyEmployeesFTE“ und „CompanyEmployeesNA“ ist, und die Geschäftsbedingungen namens „CompanyTerms“ sowohl der Sammlung „CompanyEmployeesFTE“ als auch der Sammlung „CompanyEmployeesNA“ bereitgestellt wurde, werden dem Benutzer „SampleUser“ auf der Seite für die Annahme der Geschäftsbedingungen zwei identische Kopien von „CompanyTerms“ angezeigt. Da die Benutzer jeweils nur alle Geschäftsbedingungen annehmen oder ablehnen können, besteht keine Gefahr, dass sich ein mehrdeutiger Zustand ergibt, in dem der Benutzer Geschäftsbedingungen sowohl angenommen als auch abgelehnt hat. Der Akzeptanzbericht für die Geschäftsbedingungen umfasst nur eine Zeile für jeden Satz von Geschäftsbedingungen für den jeweiligen Benutzer, damit in dem Bericht kein Fehler auftritt. Der einzige Effekt ist, dass dem Benutzer auf der Seite zur Annahme der Geschäftsbedingungen zwei Kopien der Geschäftsbedingungen angezeigt werden.  

**Problemumgehung**: Stellen Sie sicher, dass jeder Benutzer nur in einer Auflistung enthalten ist, für die die Geschäftsbedingungen bereitgestellt werden.  


### <a name="android-for-work-email-profiles-that-use-certificate-authentication-are-not-applied-to-devices"></a>Android for Work-E-Mail-Profile mit Zertifikatauthentifizierung werden nicht auf Geräte angewendet.
<!--  487657      -->
Bei der Erstellung eines Android for Work-E-Mail-Profils stehen zwei Authentifizierungsoptionen zur Verfügung: Einerseits mittels Benutzername und Kennwort und andererseits mittels Zertifikaten. Zu diesem Zeitpunkt funktioniert die Zertifikatoption nicht. Wenn das Profil mit der Authentifizierungsmethode **Zertifikate** erstellt wird, wird das Profil nicht auf das Gerät angewendet, und der Benutzer wird aufgefordert, Details zum E-Mail-Konto manuell einzugeben.

**PROBLEMUMGEHUNG**: Keine. Administratoren müssen entweder die Option **Benutzername und Kennwort** verwenden, oder warten, bis dieses Problem behoben wurde.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->


## <a name="endpoint-protection"></a>Endpoint Protection

### <a name="antimalware-policy-fails-to-apply-on-windows-server-2016-core"></a>Richtlinie für Antischadsoftware kann unter Windows Server 2016 Core nicht angewendet werden
<!--  Product Studio bug 485370 added 04 19 2017   Fixed in 1702 -->
*Folgendes gilt für Version 1610 und früher.*  
Die Richtlinie für Antischadsoftware kann unter Windows Server 2016 Core nicht angewendet werden.  Der Fehlercode lautet 0x80070002.  Fehlende Abhängigkeit für ConfigSecurityPolicy.exe.

**Problemumgehung**: Dieses Problem wird mit dem Update im [Knowledge Base-Artikel 4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) behoben, der am 9. Mai 2017 veröffentlicht wurde.


### <a name="windows-defender-advanced-threat-protection-policies-fail-on-older-client-agents"></a>Windows Defender Advanced Threat Protection-Richtlinien schlagen auf älteren Client-Agents fehl
<!-- Product Studio bug 462286 added  05 25 2017 and valid until July 2017 GA release      Fixed in 1610 -->
Windows Defender Advanced Threat Protection-Richtlinien, die über einen Standortserver mit Configuration Manager, Version 1610 oder höher, erstellt wurden, können auf Clients mit Configuration Manager, Version 1606 und früher, nicht angewendet werden.  Die Clients wurden nicht integriert, und bei der Richtlinienauswertung wird ein Fehler gemeldet. Der **Bereitstellungszustand** in der Windows Defender Advanced Threat Protection-Konfiguration zeigt **Fehler** an.

**PROBLEMUMGEHUNG**: Aktualisieren Sie den Configuration Manager-Client auf Version 1610 oder höher.
