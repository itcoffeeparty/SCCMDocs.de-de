---
title: 'Anmerkungen zu dieser Version '
titleSuffix: Configuration Manager
description: In diesen Anmerkungen finden Sie Informationen zu dringenden Problemen, die im Produkt noch nicht behoben oder bisher in keinem Microsoft Knowledge Base-Artikel beschrieben wurden.
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53685ef2647cfd87c2fcb603097186360f1c96a5
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2018
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Anmerkungen zu dieser Version von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei Configuration Manager sind die Versionsanmerkungen auf dringende Probleme beschränkt. Diese Probleme sind im Produkt noch nicht behoben oder wurden bisher in keinem Microsoft Knowledge Base-Artikel beschrieben.  

Die Dokumentation zu den einzelnen Features enthält Informationen zu bekannten Problemen, die sich auf wichtige Szenarien auswirken.  

> [!TIP]  
>  Dieses Thema enthält Versionsanmerkungen zum aktuellen Configuration Manager-Branch. Informationen zum Technical Preview-Branch finden Sie unter [Technical Preview für System Center Configuration Manager](../../../../core/get-started/technical-preview.md).  

Informationen zu den neuen, in den verschiedenen Versionen eingeführten Features finden Sie in den folgenden Artikeln:
- [Neues in Version 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [Neues in Version 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [Neuigkeiten in Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)



## <a name="setup-and-upgrade"></a>Setup und Upgrade  


### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Wenn Sie einen Long-Term Servicing Branch-Standort (LTSB) mit Version 1606 installieren, wird ein aktueller Current Branch-Standort installiert
<!-- Consider move to core content  -->
Wenn Sie das Baselinemedium von Version 1606 aus der Version vom Oktober 2016 zum Installieren eines Long-Term Servicing Branch-Standorts (LTSB) verwenden, installiert Setup stattdessen einen Current Branch-Standort. Dieses Verhalten tritt auf, weil die Option zum Installieren eines Dienstverbindungspunkts mit der Installation des Standorts nicht ausgewählt ist.

 - Obwohl ein Dienstverbindungspunkt nicht erforderlich ist, muss er während der Installation eines LTSB-Standorts ebenfalls installiert werden.

Nach Abschluss der Installation können Sie den Dienstverbindungspunkt deinstallieren. Allerdings benötigen Sie einen Dienstverbindungspunkt im Offline- oder Onlinemodus zum Senden von Telemetriedaten und Abrufen von Sicherheitsupdates für die Current Branch- und LTSB-Standorte.

Wenn Ihr Standort als Current Branch-Standort installiert ist und Sie einen LTSB-Standort installieren wollten, können Sie den Standort deinstallieren und anschließend neu installieren. Sie können auch [Microsoft-Hilfe und -Support](http://go.microsoft.com/fwlink/?LinkId=243064) aufrufen, um Unterstützung zu erhalten.  

Damit Sie sehen, welcher Standort installiert ist, wechseln Sie in der Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**, und öffnen Sie die **Hierarchieeinstellungen**. Die Option zum Konvertieren des Standorts zu einem Current Branch-Standort ist nur verfügbar, wenn ein LTSB-Standort installiert ist.  

**Problemumgehung:** Keiner   


### <a name="an-update-persists-in-downloading-state-in-the-updates-and-servicing-node-of-the-console"></a>Ein Update verbleibt im Konsolenknoten „Updates und Wartung“ im Status „Wird heruntergeladen“  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
Während des automatischen Downloads von Updates durch einen Online-Dienstverbindungspunkt kann ein Update im Status „Wird heruntergeladen“ hängen bleiben. In diesem Fall werden in den angegebenen Protokolldateien Einträge ähnlich den folgenden angezeigt:  

DMPdownloader.log:  
`ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"`  

ConfigMgrSetup.log:  
`Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.`  
`Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi`  

**Problemumgehung**: Ändern Sie den folgenden Registrierungsschlüssel auf dem Standortserver so, dass er dem folgenden Wert entspricht:  

-   **Zu bearbeitender Schlüssel:** HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Wert für Status**: Auf **146944** (dezimal) oder **0x00023e00** (hexadezimal) festlegen  

Starten Sie dann entweder den SMS_Executive-Dienst neu, oder warten Sie bis zu 24 Stunden auf den nächsten automatischen Downloadzyklus.

### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>Manifestüberprüfungsfehler beim Setup, wenn verteilbare Dateien aus dem Ordner „CD.Latest“ verwendet werden
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

Wenn Setup über einen für Version 1606 erstellten CD.Latest-Ordner ausgeführt wird und die verteilbaren Dateien aus diesem Ordner verwendet werden, treten beim Setup folgende Fehler auf, die im Configuration Manager-Setupprotokoll aufgeführt werden:

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

**Problemumgehung**: Nutzen Sie eine der folgenden Optionen:
 - Laden Sie beim Setup die neuesten verteilbaren Dateien von Microsoft herunter. Verwenden Sie die neuesten verteilbaren Dateien statt der Dateien, die im CD.Latest-Ordner enthalten sind.
 - Löschen Sie den Ordner *cd.latest\redist\languagepack\zhh*, und führen Sie anschließend Setup erneut aus.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Clientbereitstellung und -upgrade  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>Bei der Clientinstallation tritt ein Fehler mit Fehlercode 0x8007064c auf
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*Folgendes Problem betrifft alle aktiven Versionen von Configuration Manager.*  

Wenn Sie den Client auf Windows-Computern bereitstellen, tritt bei der Installation ein Fehler auf. Die Protokolldatei „ccmsetup.log“ enthält folgende Einträge: 

`File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation`  
`InstallFromManifest failed 0x8007064c`

**Problemumgehung**: Dieser Fehler wird durch eine zuvor installierte, beschädigte Version von Silverlight verursacht. Um dieses Problem zu beheben, führen Sie auf dem betroffenen Computer das Tool aus, das Sie hier finden: [Behebt Probleme, die eine Installation oder Deinstallation von Programmen blockieren](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed).

## <a name="operating-system-deployment"></a>Betriebssystembereitstellung  

### <a name="servicing-plans-create-many-duplicate-software-update-groups-and-deployments-by-default"></a>Wartungspläne erstellen standardmäßig eine Vielzahl von doppelten Softwareupdategruppen und -bereitstellungen  
Der Assistent zum Erstellen eines Wartungsplans wird zurzeit standardmäßig nach jedem Synchronisierungsvorgang für Softwareupdates ausgeführt. Bei jeder Ausführung erstellt der Assistent eine neue Softwareupdategruppe und -bereitstellung. Wenn Sie über einen Synchronisierungszeitplan für Softwareupdates verfügen, der mehrmals täglich ausgeführt wird, erstellt der Assistent zum Erstellen eines Wartungsplans jeden Tag mehrere Softwareupdategruppen und -bereitstellungen.  

**Problemumgehung**: Nachdem Sie einen Wartungsplan erstellt haben, öffnen Sie die Eigenschaften des Plans, wechseln Sie zur Registerkarte **Auswertungszeitplan**, wählen Sie **Regel nach Zeitplan ausführen** aus, klicken Sie auf **Anpassen**, und erstellen Sie einen benutzerdefinierten Zeitplan. Sie können den Wartungsplan beispielsweise alle 60 Tage ausführen.  



## <a name="software-updates"></a>Softwareupdates

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>Das Importieren von Office 365-Clienteinstellungen aus einer Konfigurationsdatei schlägt fehl, wenn sie nicht unterstützte Sprachen enthält
<!-- 489258  Fixed in 1706  -->
*Folgendes Problem betrifft Version 1702 und früher.*   

Wenn Sie die Office 365-Clienteinstellungen aus einer vorhandenen XML-Konfigurationsdatei importieren und die Datei Sprachen enthält, die vom Office 365 ProPlus-Client nicht unterstützt werden, tritt ein Fehler auf. Weitere Informationen finden Sie unter [Bereitstellen von Office 365-Apps für Clients aus dem Office 365-Clientverwaltungsdashboard](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Problemumgehung**: Verwenden Sie in der XML-Konfigurationsdatei nur die [vom Office 365 ProPlus-Client unterstützten](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) Sprachen.  



## <a name="mobile-device-management"></a>Verwaltung mobiler Geräte  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>Ab Version 1710 können Sie Windows Phone 8.1 VPN-Profile nicht mehr unter Windows 10 bereitstellen   <!-- 503274  Should be fixed by 1802, if not sooner -->
In Version 1710 ist es nicht mehr möglich, ein VPN-Profil mit dem Windows Phone 8.1-Workflow zu erstellen, der auch für Windows 10-Geräte gilt. Für diese Profile wird die Seite „Unterstützte Plattformen“ im Assistenten für die Erstellung nicht mehr angezeigt. Windows Phone 8.1 wird im Back-End automatisch ausgewählt. Die Seite „Unterstützte Plattformen“ ist in den Profileigenschaften verfügbar, wird jedoch in den Windows 10-Optionen angezeigt.

**Problemumgehung**: Verwenden Sie für Windows 10-Geräte den Workflow für Windows 10-VPN-Profile. Falls dies für Ihre Umgebung nicht möglich ist, wenden Sie sich an den Support. Der Support kann Ihnen helfen, Unterstützung für Windows 10 hinzuzufügen.


### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-of-memory"></a>Eine vollständige Zurücksetzung deaktiviert Windows 10-Geräte mit weniger als 4 GB Arbeitsspeicher.
Eine vollständige Zurücksetzung von Geräten unter Windows 10 Version 1507 mit weniger als 4 GB RAM kann das Gerät unbrauchbar machen. Nach dem versuchten Zurücksetzen des Geräts startet oder reagiert es nicht mehr.

**Problemumgehung**: Stellen Sie sicher, dass Windows 10-Geräte über mindestens 4 GB Arbeitsspeicher verfügen, bevor Sie eine vollständige Zurücksetzung ausführen. Geben Sie zum Anzeigen der Versionsnummer des Windows-10-Geräts 'winver' an der Befehlszeile ein. Wenn Sie das Gerät bereits zurückgesetzt haben und es nicht mehr reagiert, verwenden Sie ein bootfähiges Windows 10-USB-Laufwerk, um das Gerät wiederherzustellen.


### <a name="when-a-user-belongs-to-two-or-more-user-collections-to-which-you-deploy-a-terms-and-conditions-policy-the-user-sees-multiple-sets-of-the-same-terms"></a>Wenn ein Benutzer zwei oder mehr Benutzersammlungen angehört, für die Sie eine Geschäftsbedingungsrichtlinie bereitgestellt haben, werden dem Benutzer mehrere Kopien derselben Geschäftsbedingungen angezeigt  
<!-- 454394    -->
Wenn Sie eine Reihe von Geschäftsbedingungen für mehrere Benutzersammlungen bereitstellen und ein Benutzer Mitglied von mehreren dieser Sammlungen ist, werden diesem Benutzer in Unternehmensportal mehrere Kopien identischer Geschäftsbedingungen angezeigt. Zum Beispiel:
- Ein Benutzer namens „SampleUser“ ist Mitglied von zwei verschiedenen Benutzersammlungen: „CompanyEmployeesFTE“ und „CompanyEmployeesNA“.
- Sie stellen die Geschäftsbedingungen „CompanyTerms“ sowohl für „CompanyEmployeesFTE“ als auch für „CompanyEmployeesNA“ bereit.
- Für „SampleUser“ werden auf der Seite zum Akzeptieren der Geschäftsbedingungen im Unternehmensportal zwei identische Kopien von „CompanyTerms“ angezeigt. 

Benutzer können nur alle Geschäftsbedingungen akzeptieren oder ablehnen. Daher besteht keine Gefahr eines mehrdeutigen Akzeptanzzustands. (Ein solcher mehrdeutiger Zustand würde bestehen, wenn ein Benutzer die gleichen Geschäftsbedingungen sowohl akzeptiert als auch ablehnt.) Der Akzeptanzbericht für die Geschäftsbedingungen umfasst nur eine Zeile für jeden Satz von Geschäftsbedingungen pro Benutzer, daher weist der Bericht keinen Fehler auf. Der einzige Effekt ist, dass dem Benutzer auf der Seite zur Annahme der Geschäftsbedingungen zwei Kopien der Geschäftsbedingungen angezeigt werden.  

**Problemumgehung**: Stellen Sie sicher, dass jeder Benutzer nur in einer Auflistung enthalten ist, für die die Geschäftsbedingungen bereitgestellt werden.  


<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
