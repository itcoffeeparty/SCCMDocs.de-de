---
title: Anmerkungen zu dieser Version
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zu dringenden Problemen, die im Produkt noch nicht behoben oder bisher in keinem Microsoft Knowledge Base-Artikel beschrieben wurden.
ms.custom: na
ms.date: 04/18/2018
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
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2eabcba6e56bd2a0a9977ab31610a9d747ab6207
ms.sourcegitcommit: e23350fe65ff99228274e465b24b5e163769f38f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/20/2018
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Anmerkungen zu dieser Version von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei Configuration Manager sind die Versionsanmerkungen auf dringende Probleme beschränkt. Diese Probleme sind im Produkt noch nicht behoben oder wurden bisher in keinem Microsoft Knowledge Base-Artikel beschrieben.  

Die Dokumentation zu den einzelnen Features enthält Informationen zu bekannten Problemen, die sich auf wichtige Szenarien auswirken.  

> [!TIP]  
>  Dieses Thema enthält Versionsanmerkungen zum aktuellen Configuration Manager-Branch. Informationen zum Technical Preview-Branch finden Sie unter [Technical Preview für System Center Configuration Manager](../../../../core/get-started/technical-preview.md).  

Informationen zu den neuen, in den verschiedenen Versionen eingeführten Features finden Sie in den folgenden Artikeln:
- [Neues in Version 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)
- [Neues in Version 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [Neues in Version 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  



## <a name="setup-and-upgrade"></a>Setup und Upgrade  


### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>Manifestüberprüfungsfehler beim Setup, wenn verteilbare Dateien aus dem Ordner „CD.Latest“ verwendet werden
<!-- 510080, 490569  -->

Wenn das Setup über einen für Version 1606 erstellten CD.Latest-Ordner ausgeführt wird und die verteilbaren Dateien aus diesem Ordner verwendet werden, treten beim Setup folgende Fehler auf, die im Configuration Manager-Setupprotokoll aufgeführt werden:

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

#### <a name="workaround"></a>Problemumgehung
Verwenden Sie eine der folgenden Optionen:
 - Laden Sie beim Setup die neuesten verteilbaren Dateien von Microsoft herunter. Verwenden Sie die neuesten verteilbaren Dateien statt der Dateien, die im CD.Latest-Ordner enthalten sind.
 - Löschen Sie den Ordner *cd.latest\redist\languagepack\zhh*, und führen Sie anschließend Setup erneut aus.


### <a name="setup-command-line-option-joinceip-must-be-specified"></a>Die Setup-Befehlszeilenoption „JoinCEIP“ muss angegeben werden
<!--510806-->
*Gilt für: Configuration Manager, Version 1802*

Ab Configuration Manager Version 1802 ist das CEIP-Feature (Customer Experience Improvement Program, Programm zur Verbesserung der Benutzerfreundlichkeit) nicht mehr im Produkt enthalten. Wenn über eine Befehlszeile oder ein unbeaufsichtigtes Skript die [Installation eines neuen Standorts automatisiert wird](/sccm/core/servers/deploy/install/command-line-options-for-setup), zeigt das Setup als Fehlermeldung an, dass ein erforderlicher Parameter fehlt. 

#### <a name="workaround"></a>Problemumgehung
Geben Sie über die Befehlszeile für das Setup den Parameter **JoinCEIP** an. Der Abschluss des Setupvorgangs wird hiervon nicht beeinflusst.

 > [!Note]  
 > Der Parameter „EnableSQM“ für das [Konsolensetup](/sccm/core/servers/deploy/install/install-consoles) ist nicht erforderlich.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Clientbereitstellung und -upgrade

### <a name="azure-ad-enabled-clients-cant-communicate-with-management-point"></a>Azure AD-fähige Clients können nicht mit dem Verwaltungspunkt kommunizieren
<!--501089-->
*Gilt für: Configuration Manager, Version 1706*
<!--also fixed in 1710 HFRU-->
Im Szenario zum [Installieren und Zuweisen von Windows 10-Clients für Configuration Manager mithilfe von Azure AD für die Authentifizierung](/sccm/core/clients/deploy/deploy-clients-cmg-azure) schlägt die Clientkommunikation fehl, wenn die HTTPS-fähigen Verwaltungspunkte alternative Datenbank-Anmeldeinformationen verwenden. 

#### <a name="workaround"></a>Problemumgehung
Umgehen Sie dieses Problem durch folgende Schritte:
- Aktualisieren Sie den Standort auf die neueste Version, und installieren Sie den neuesten Hotfix.
- Ändern Sie die Anmeldeinformationen für den Verwaltungspunkt.


<!-- ## Operating system deployment  -->



## <a name="software-updates"></a>Softwareupdates

### <a name="servicing-plans-create-many-duplicate-software-update-groups-and-deployments-by-default"></a>Wartungspläne erstellen standardmäßig eine Vielzahl von doppelten Softwareupdategruppen und -bereitstellungen  
<!-- 474326 -->
Der Assistent zum Erstellen eines Wartungsplans wird zurzeit standardmäßig nach jedem Synchronisierungsvorgang für Softwareupdates ausgeführt. Bei jeder Ausführung erstellt der Assistent eine neue Softwareupdategruppe und -bereitstellung. Wenn Sie über einen Synchronisierungszeitplan für Softwareupdates verfügen, der mehrmals täglich ausgeführt wird, erstellt der Assistent zum Erstellen eines Wartungsplans mehrere Softwareupdategruppen und Bereitstellungen pro Tag.  

#### <a name="workaround"></a>Problemumgehung
 Nachdem Sie einen Wartungsplan erstellt haben, öffnen Sie die Eigenschaften des Plans, wechseln Sie zur Registerkarte **Auswertungszeitplan**, wählen Sie **Regel nach Zeitplan ausführen** aus, klicken Sie auf **Anpassen**, und erstellen Sie einen benutzerdefinierten Zeitplan. Sie können den Wartungsplan beispielsweise alle 60 Tage ausführen.  


### <a name="changing-office-365-client-setting-doesnt-apply"></a>Das Ändern einer Office 365-Clienteinstellung wird nicht übernommen 
<!--511551-->
*Gilt für: Configuration Manager, Version 1802*  

Stellen Sie eine [Clienteinstellung](/sccm/core/clients/deploy/about-client-settings#enable-management-of-the-office-365-client-agent) mit **Verwaltung des Office 365-Client-Agents aktivieren** als `Yes` bereit. Ändern Sie diese Einstellung in `No` oder `Not Configured`. Nach dem Aktualisieren der Richtlinie auf Zielclients werden Office 365-Updates weiterhin von Configuration Manager verwaltet. 

#### <a name="workaround"></a>Problemumgehung
Ändern Sie den folgenden Registrierungswert in `0`, und starten Sie den **Microsoft Office-Klick-und-Los-Dienst** (ClickToRunSvc) neu:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```



## <a name="mobile-device-management"></a>Verwaltung mobiler Geräte  

### <a name="you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10"></a>Sie können Windows Phone 8.1-VPN-Profile nicht mehr für Windows 10 bereitstellen
<!-- 503274  -->
*Gilt für: Configuration Manager, Version 1710*

Sie können über den Workflow für Windows Phone 8.1 kein VPN-Profil erstellen, das auch für Windows 10-Geräte gültig ist. Der Erstellungsassistent zeigt für diese Profile nicht mehr die Seite „Unterstützte Plattformen“ an. Windows Phone 8.1 wird im Back-End automatisch ausgewählt. Die Seite „Unterstützte Plattformen“ ist in den Profileigenschaften verfügbar. Auf ihr werden allerdings die Windows 10-Optionen nicht angezeigt.

#### <a name="workaround"></a>Problemumgehung
 Verwenden Sie für Windows 10-Geräte den Workflow für Windows 10-VPN-Profile. Falls dies für Ihre Umgebung nicht möglich ist, wenden Sie sich an den Support. Der Support kann Ihnen helfen, Unterstützung für Windows 10 hinzuzufügen.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
