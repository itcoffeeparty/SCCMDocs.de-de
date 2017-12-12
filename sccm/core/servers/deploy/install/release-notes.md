---
title: 'Anmerkungen zu dieser Version '
titleSuffix: Configuration Manager
description: In diesen Anmerkungen finden Sie Informationen zu dringenden Problemen, die im Produkt noch nicht behoben oder bisher in keinem Microsoft Knowledge Base-Artikel beschrieben wurden.
ms.custom: na
ms.date: 11/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: "41"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 8030ce7f98ebb34d9581ad036513b9b1c879c0ad
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/04/2017
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



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Clientbereitstellung und -upgrade  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>Bei der Clientinstallation tritt ein Fehler mit Fehlercode 0x8007064c auf
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*Folgendes gilt für alle aktiven Versionen von Configuration Manager.*   
Wenn Sie den Client auf Windows-Computern bereitstellen, tritt bei der Installation ein Fehler auf. Die Datei „ccmsetup.log“ enthält den Eintrag: „File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation“, gefolgt von „InstallFromManifest failed 0x8007064c“.

**Problemumgehung**: Dieser Fehler wird durch eine zuvor installierte, beschädigte Version von Silverlight verursacht. Versuchen Sie, auf dem betroffenen Computer das folgende Tool auszuführen: [https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## <a name="operating-system-deployment"></a>Betriebssystembereitstellung  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Wartungspläne erstellen standardmäßig eine Vielzahl von doppelten Softwareupdategruppen und -bereitstellungen  
Der Assistent zum Erstellen eines Wartungsplans wird zurzeit standardmäßig nach jedem Synchronisierungsvorgang für Softwareupdates ausgeführt. Bei jeder Ausführung erstellt der Assistent eine neue Softwareupdategruppe und -bereitstellung. Wenn Sie z. B. über einen Synchronisierungszeitplan für Softwareupdates verfügen, der mehrmals täglich ausgeführt wird, erstellt der Assistent zum Erstellen eines Wartungsplans jeden Tag mehrere, wahrscheinlich identische, Softwareupdategruppen und -bereitstellungen.  

**Problemumgehung**:    
Nachdem Sie einen Wartungsplan erstellt haben, öffnen Sie die Eigenschaften des Plans, wechseln Sie zur Registerkarte **Auswertungszeitplan**, wählen Sie **Regel nach Zeitplan ausführen** aus, klicken Sie auf **Anpassen**, und erstellen Sie einen benutzerdefinierten Zeitplan. Sie können den Wartungsplan beispielsweise alle 60 Tage ausführen.  



## <a name="software-updates"></a>Softwareupdates

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>Das Importieren von Office 365-Clienteinstellungen aus einer Konfigurationsdatei schlägt fehl, wenn sie nicht unterstützte Sprachen enthält
<!-- 489258  Fixed in 1706  -->
*Folgendes gilt für Version 1702 und früher.*   
Wenn Sie die Office 365-Clienteinstellungen aus einer vorhandenen XML-Konfigurationsdatei importieren und die Datei Sprachen enthält, die vom Office 365 ProPlus-Client nicht unterstützt werden, tritt ein Fehler auf. Details finden Sie unter [Bereitstellen von Office 365-Apps für Clients aus dem Office 365-Clientverwaltungsdashboard](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Problemumgehung**:    
Verwenden Sie in der XML-Konfigurationsdatei nur [vom Office 365 ProPlus-Client unterstützte Sprachen](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx).  



## <a name="mobile-device-management"></a>Verwaltung mobiler Geräte  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>Ab Version 1710 können Sie Windows Phone 8.1 VPN-Profile nicht mehr unter Windows 10 bereitstellen   <!-- 503274  Should be fixed by 1802, if not sooner -->
In Version 1710 ist es nicht mehr möglich, ein VPN-Profil mit dem Windows Phone 8.1-Workflow zu erstellen, der auch für Windows 10-Geräte gilt. Bei diesen Profilen wird im Erstellungs-Assistenten die Seite „Unterstützte Plattformen“ nicht mehr angezeigt, und Windows Phone 8.1 wird automatisch im Back-End ausgewählt. Auf den Eigenschaftsseiten ist die Seite „Unterstützte Plattformen“ verfügbar, aber die Windows 10-Optionen werden nicht angezeigt.

**Problemumgehung**: Verwenden Sie für Windows 10-Geräte den Workflow für Windows 10-VPN-Profile. Falls dies für Ihre Umgebung nicht möglich ist, wenden Sie sich an den Support. Der Support kann Ihnen bei Bedarf helfen, Unterstützung für Windows 10 hinzuzufügen.


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
<!-- ## Endpoint Protection -->
