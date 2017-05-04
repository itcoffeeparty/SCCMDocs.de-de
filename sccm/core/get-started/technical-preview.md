---
title: "Technical Preview für System Center Configuration Manager | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über das Technical Preview-Release, mit der Sie neue Funktionen und Fähigkeiten in System Center Configuration Manager testen können."
ms.custom: na
ms.date: 4/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: ae008c91a7387ba76f2bfac13f8feb489a0cc558
ms.openlocfilehash: 8ffaee12bd826e2f19653b215ee19423ea672433
ms.lasthandoff: 04/21/2017


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*

**Willkommen bei System Center Configuration Manager Technical Preview**. Dieses Thema stellt Details zur Preview-Version bereit, die konstant weiterentwickelt wird und mit der neue Funktionalität und Funktionen eingeführt werden, an denen wir arbeiten. Mit jeder Version der Technical Preview werden neue Funktionen eingeführt, die zum Zeitpunkt der Veröffentlichung der Technical Preview nicht in Current Branch von System Center Configuration Manager enthalten sind. Diese Funktionen werden dem Current Branch möglicherweise zu einem späteren Zeitpunkt über ein Update hinzugefügt. Bevor wir diese Funktionen jedoch fertigstellen und sie hinzufügen, möchten wir Ihnen die Gelegenheit geben, sie auszuprobieren und uns Feedback zukommen zu lassen.  

 Da es sich hierbei um eine Technical Preview handelt, können Details und Funktionen noch Änderungen unterliegen.  

 Dieses Thema bietet Informationen, die für alle Versionen der Technical Preview gelten, und zählt außerdem jede neue Funktionalität (oder Funktion) zusammen mit der Technical Preview-Version auf, in der die Funktion zum ersten Mal verfügbar war, z.B. Version 1701 für Januar 2017. Die Details dieser Funktionen werden in separaten Themen zu jeder Preview-Version beschrieben.  

 Informationen zu den Neuigkeiten in Current Branch von Configuration Manager finden Sie unter [What's new in System Center Configuration Manager (Neues in System Center Configuration Manager)](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Anforderungen und Einschränkungen für die Technical Preview-Version.  

> [!IMPORTANT]     
>  Die Technical Preview-Version ist ausschließlich für die Verwendung in einer Lab-Umgebung lizenziert.  Microsoft bietet möglicherweise keinen Support, und bestimmte Funktionen sind in der Preview-Software möglicherweise nicht verfügbar. Darüber hinaus gelten bei der Preview-Software im Vergleich zu handelsüblicher Software möglicherweise eingeschränkte oder veränderte Standards bei der Sicherheit, dem Datenschutz, der Barrierefreiheit, der Verfügbarkeit und der Zuverlässigkeit.  

 Informationen zu den meisten Produktvoraussetzungen finden Sie unter [Supported configurations for System Center Configuration Manager (Unterstützte Konfigurationen für System Center Configuration Manager)](../../core/plan-design/configs/supported-configurations.md). Für die Technical Preview-Versionen gelten folgenden Ausnahmen:  

-   Jede Installation wird nach 90 Tagen deaktiviert.  

-   Englisch ist die einzige unterstützte Sprache.  

-   Es wird nur ein eigenständiger primärer Standort unterstützt. In zentraler Verwaltungsstandort, mehrere primäre Standorte oder sekundäre Standorte werden nicht unterstützt.  

-   Es werden nur die folgenden Versionen von SQL Server unterstützt:  

    -   SQL Server 2016 (ohne Service Pack, und höher)
    -   SQL Server 2014 (ohne Service Pack, und höher)
    -   SQL Server 2012 (mit Service Pack 2, und höher)


-   Der Standort unterstützt bis zu 10 Clients mit einem der folgenden Betriebssysteme:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  


-   Nur die folgenden Installationsflags (Switches) werden unterstützt:  

    -   **/silent**  
    -   **/testdbupgrade**    


-   Wenn Sie die Technical Preview verwenden, wird der Dienstverbindungspunkt standardmäßig bei der Installation auf den Onlinemodus festgelegt und kann nicht in den Offlinemodus gewechselt werden.

-   Gegebenenfalls werden zusätzliche Einschränkungen und Anforderungen mit den Details für die einzelnen spezifischen Versionen der technischen Vorschau einbezogen.  

-   Es gibt keine Unterstützung für die Migration zu oder von dieser Vorabversion.  

-   Es gibt keine Unterstützung für ein Upgrade auf diese Vorabversion.  

-   Es gibt keine Unterstützung für ein Upgrade auf einen Erstellungs-Build (Current Branch) dieser Vorabversion. Wenn Updates für eine Vorschauversion verfügbar sind, finden Sie diese im Knoten **Updates und Wartung** der Configuration Manager-Konsole, von wo aus Sie sie installieren können. Ein Video zum Upgradeprozess über die Konsole finden Sie unter [Installieren von ConfigMgr-Updatepaketen](https://www.youtube.com/embed/KBd_EGFbUT8) auf „youtube.com“.  

##  <a name="bkmk_install"></a> Installieren und Aktualisieren der Technical Preview-Version  
 System Center Configuration Manager Technical Preview unterscheidet sich von dem aktuellen Release von System Center Configuration Manager.  

 Sie müssen zum Verwenden der Technical Preview zunächst eine **Basisversion** des Technical Preview-Builds installieren. Nach der Installation einer Basisversion können Sie Ihre Installation mithilfe **konsoleninterner Updates** auf den neuesten Stand der aktuellen Preview-Version bringen.     In der Regel werden neue Technical Preview-Versionen jeden Monat zur Verfügung gestellt.

Jede Preview-Version wird unterstützt bis drei nachfolgende Versionen verfügbar sind. Dies bedeutet, wenn die Version 1702 freigegeben wird, wird die Version 1610 nicht länger unterstützt, aber die Versionen 1611, 1612 und 1701 werden weiterhin unterstützt. Wenn die letzte Baseline nicht mehr unterstützt wird (z.B. Version 1610), wird sie jedoch weiterhin für die Installation eines neuen Technical Preview-Standorts unterstützt (bis eine neue Baselineversion verfügbar ist), solange Sie diese Installation auf eine unterstützte Version aktualisieren. Wenn die aktuelle Version bei der Installierung in Ihrer Konsole verfügbar ist, führen Sie ein Update auf die neueste angebotene Version durch, und wiederholen Sie anschließend den Prozess, bis Sie die aktuellste Version von Technical Preview installieren können.

> [!TIP]  
>  Bei der Installation eines Updates für die Technical Preview-Version wird Ihre Installation auf die jeweils neueste Technical Preview-Version aktualisiert.    Eine Technical Preview-Installation bietet nie die Möglichkeit eines Upgrades auf eine aktuelle Branch-Installation und erhält keine Updates von der aktuellen Branch-Version.  

**Aktive Basisversionen der Technical Preview:**  
Sie können eine Basisversion für bis zu 1 Jahr nach der Veröffentlichung installieren. Wenn Sie einen neuen Technical Preview-Standort erstellen, empfiehlt es sich, die neueste verfügbare Baselineversion zu verwenden.
-  **Technical Preview 1703**: Technical Preview 1703 steht sowohl als konsoleninternes Update für Configuration Manager Technical Preview als auch als neue Basisversion auf der TechNet Evaluation Center-Website zur Verfügung.

-  **Technical Preview 1610**: Technical Preview 1610 steht sowohl als konsoleninternes Update für Configuration Manager Technical Preview als auch als Basisversion auf der TechNet Evaluation Center-Website zur Verfügung. Wenn Sie Medien für die Installation von 1610 haben, empfehlen wir, die Version 1703 herunterladen und stattdessen diese Version zu installieren.




##  <a name="BKMK_TPFeedback"></a> Übermitteln von Feedback  
 Wir würden uns über Ihr Feedback zu unseren technische Vorschauen freuen. Wenn Sie Feedback zu den Funktionen in einer Vorabversion senden möchten, folgen Sie dem Link zu unserem Feedbackformular auf der Seite des [Configuration Manager-Feedbackprogramms](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) auf der Microsoft Connect-Website.  

 Außerdem interessieren uns Ihre Ideen zu neuen Funktionen, die Sie in Zukunft gerne nutzen möchten. Wenn Sie neue Ideen einreichen und über die von anderen Benutzern übermittelten Ideen abstimmen möchten, [besuchen Sie unsere User Voice-Seite](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Funktionen der technischen Vorschauversionen  
 Nachstehend sind die Funktionen der einzelnen Configuration Manager Technical Preview-Releases dargestellt.  Funktionen, die ab einer Version der Technical Preview verfügbar sind, bleiben dies auch in späteren Versionen. Ebenso bleiben Funktionen, die zu diesem System Center Configuration Manager-Release (Current Branch) hinzugefügt wurden, in den nachfolgenden Technical Previews verfügbar.  Klicken Sie sich durch den Inhalt der einzelnen Preview-Version, um mehr über eine bestimmte Funktion zu erfahren.  

 |Funktion |Technical Preview-Version |Current Branch-Version|  
|----------------|---------------------|--------------------|
 |Konfigurieren von Android-Apps mit Konfigurationsrichtlinien für Apps  |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#configure-android-apps-with-app-configuration-policies)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Die Hardwareinventur sammelt Sicherer Start-Informationen |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#hardware-inventory-collects-secure-boot-information)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Hinzufügen von untergeordneten Tasksequenzen zu einer Tasksequenz|[Tech Preview 1704](capabilities-in-technical-preview-1704.md#add-child-task-sequences-to-a-task-sequence)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Neuladen von Startimages mit der aktuellen Version von Windows PE |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#reload-boot-images-with-current-windows-pe-version)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Verbesserungen bei der Betriebssystembereitstellung|[Tech Preview 1704](capabilities-in-technical-preview-1704.md#improvements-to-operating-system-deployment)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Bereitstellen per Volumenlizenz erworbener iOS-Apps in Gerätesammlungen|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#deploy-volume-purchased-ios-apps-to-device-collections)|[Version 1702](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)|
 |Direkte Links zu Anwendungen im Softwarecenter|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#direct-links-to-applications-in-software-center)|![Nicht hinzugefügt](media/Red_X.gif)
 |PFX-Zertifikate für Configuration Manager-Windows-Clientcomputer|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#pfx-certificates-for-configuration-manager-windows-client-computers)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Konfigurieren des Azure Dienste-Assistenten|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#configure-azure-services-wizard)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Konvertieren von BIOS in UEFI in einer Betriebssystem-Upgradetasksequenz| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#convert-from-bios-to-uefi-during-an-in-place-upgrade) |[Version 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)|
 |Reduzierbare Tasksequenzgruppen| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#collapsible-task-sequence-groups) |![Nicht hinzugefügt](media/Red_X.gif)|
 |Clienteinstellungen zum Konfigurieren von Windows Analytics für Upgrade Readiness | [Tech Preview 1703](capabilities-in-technical-preview-1703.md#client-settings-to-configure-windows-analytics-for-upgrade-readiness) |![Nicht hinzugefügt](media/Red_X.gif)|
 |Neue Kompatibilitätseinstellungen für iOS-Geräte|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|[Version 1702](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)|
 |Erstellen von PFX-Zertifikaten mit S/MIME-Unterstützung|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|[Version 1702](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Prüfen Sie auf ausgeführte ausführbare Dateien, bevor Sie eine Anwendung installieren|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|[Version 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Feedback über die Configuration Manager-Konsole geben | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#send-feedback-from-the-configuration-managercconsole)  |
 |Änderungen an Updates und Wartung  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#changes-for-updates-and-servicing) |
 |Verbesserungen des Peercaches  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |[Version 1702](/sccm/core/plan-design/hierarchy/client-peer-cache)|
 |Verwenden von Azure Active Directory  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![Nicht hinzugefügt](media/Red_X.gif)|
 |Verbesserungen bei Gerätekompatibilitätsrichtlinien für bedingten Zugriff | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |[Version 1702](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Warnungen für Clientversionen der Antischadsoftware | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |[Version 1702](/sccm/protect/deploy-use/endpoint-configure-alerts?branch=live#alert-for-outdated-malware-client)|
 |Bewertung der Kompatibilität für Updates von Windows Update for Business | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![Nicht hinzugefügt](media/Red_X.gif)|
 |Verbesserungen bei den Einstellungen und Benachrichtigungen für Tasksequenzen mit schwerwiegenden Auswirkungen in Software Center|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert)|[Version 1702](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)|
 |Unterstützung für Android for Work| [Tech Preview 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |[Version 1702](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment)|
 |Verbesserungen bei Begrenzungsgruppen für Softwareupdatepunkte | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |[Version 1702](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)  |
 |Die Hardwareinventur sammelt UEFI-Informationen | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|[Version 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#hardware-inventory-collects-uefi-information) |
 |Verbesserungen bei der Betriebssystembereitstellung| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment) |
 |Hosten von Softwareupdates auf cloudbasierten Verteilungspunkten| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|![Nicht hinzugefügt](media/Red_X.gif) |
 |Daten zum Nachweis der Geräteintegrität über Verwaltungspunkte überprüfen| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)| [Version 1702](/sccm/core/servers/manage/health-attestation) |
 |OMS-Connector für die Microsoft Azure Government-Cloud |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |[Version 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig) |
 |Android- und iOS-Versionen werden nicht mehr über den Erstellungsassistenten erreicht. |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |![Nicht hinzugefügt](media/Red_X.gif) |
 |Datenzugriff für OData-Endpunkt |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Data Warehouse-Dienstpunkt |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|[Version 1702](/sccm/core/servers/manage/data-warehouse)|
 |Inhaltsbibliothek-Bereinigungstool |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|[Version 1702](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) |
 |Verbesserungen für die Suche in der Konsole |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-for-in-console-search)|
 |Verhindern der Anwendungsinstallation, wenn ein bestimmtes Programm läuft|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|[Version 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Die neue Windows Hello for Business-Benachrichtigung für Endbenutzer|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Support des Windows Store für Unternehmen in Configuration Manager|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Rückkehr zur vorherigen Seite, wenn eine Tasksequenz fehlschlägt|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment)|
 |Unterstützung von Express-Installationsdateien für Windows 10-Updates|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|[Version 1702](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)|
 |Azure Active Directory-Onboarding|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Ändern der Konfigurierung der Multi-Factor Authentication für die Geräteregistrierung|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Zwischenspeichern von Inhalt für Bereitstellungen und Tasksequenzen |[Tech Preview 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|[Version 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
 |Windows Defender-Konfigurationseinstellungen|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[Version 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Anfordern der Richtliniensynchronisierung von der Administratorkonsole|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[Version 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |Unterstützung zusätzlicher Sicherheitsrollen für Knoten „Alle firmeneigenen Geräte“|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[Version 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Bedingter Zugriff für Windows 10-VPN-Profile|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[Version 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |Filtern Sie nach Größe des Inhalts in Regeln zur automatischen Bereitstellung|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |Verbesserte Funktionalität für erforderliche Software-Dialoge|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Zuvor genehmigte Anwendungsanforderungen verweigern|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Clients von einem automatischen Upgrade ausschließen|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[Version 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Verbesserungen bei Endpoint Protection|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|[Version 1610](/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service)|
 |Erhöhte Anzahl registrierter Geräte|[Tech Preview 1609](/sccm/mdm/deploy-use/enable-platform-enrollment)|[Version 1610](/sccm/mdm/deploy-use/enable-platform-enrollment)|
 |Zusätzliche Apple-DEP-Einstellungen|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[Version 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |Verbesserungen der Integration von Windows Store für Unternehmen in Configuration Manager|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[Version 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Neue Kompatibilitätseinstellungen für Konfigurationselemente|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[Version 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Integration mit Upgrade Analytics|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[Version 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Native Verbindungstypen für hybride Windows 10-VPN-Profile|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Verbesserungen für Begrenzungsgruppen|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[Version 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Office 365-Clientverwaltungsdashboard|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[Version 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |Bereitstellen von Office 365-Apps für Clients|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|[Version 1702](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)|
 |Verbesserungen für die Konvertierung von BIOS zu UEFI|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[Version 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Intune-Kompatibilitätsdiagramme|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[Version 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |Verbesserungen am Tasksequenzschritt „ConfigMgr-Client für Erfassung vorbereiten“|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Verbesserungen für Software Center|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |Verbesserungen bei Asset Intelligence|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Tastaturübersetzung bei Remotesteuerung|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Verbesserungen an der Richtlinie für Windows 10-Editionsupgrades|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Version 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Anpassbares Branding für Software Center-Dialogfelder|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|![Nicht hinzugefügt](media/Red_X.gif)|  
 |Verschiedene Geräteverwaltungspunkte für die lokale Verwaltung mobiler Geräte|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Automatisches Kategorisieren von Geräten in Sammlungen|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Version 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Erzwingung der Karenzzeit für erforderliche Anwendungen und Bereitstellungen von Softwareupdates|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Verwendung von Configuration Manager als verwalteter Installer mit Device Guard|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![Nicht hinzugefügt](media/Red_X.gif)|
 |Cloudverwaltungsgateway (ehemals Cloudproxydienst)|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |Verwaltung des Office 365-Client-Agents in Configuration Manager|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |Die Tasksequenzvariable „OSDPreserveDriveLetter“ wurde als veraltet markiert.|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Version 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Änderungen am Knoten „Updates und Wartung“|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |VPN pro App für Windows 10-Geräte|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Version 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Verbesserungen an der Tasksequenz „Softwareupdates installieren“|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Verbesserungen am Tasksequenzschritt „ConfigMgr-Client für Erfassung vorbereiten“ |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |Karenzzeit für die erforderlichen Anwendungsbereitstellungen |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|![Nicht hinzugefügt](media/Red_X.gif)|  
 |Benutzerfreundlichere Remotegeräteaktionen |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Windows Store für Business-Apps |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Allgemeine Verbesserungen für per Volumenlizenz erworbene Apps|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Unternehmensdatenschutz (Enterprise Data Protection; EDP)|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Endbenutzer können Apps über das Unternehmensportal installieren. |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|![Nicht hinzugefügt](media/Red_X.gif)|  
 |Neue Registerkarten für Updates und Betriebssysteme im Software Center|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Version 1606 ](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Bereitstellung einer Servergruppe |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Version 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Unterstützung für Windows Defender Advanced Threat Protection |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Version 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |Neue Neustartoptionen für Windows 10-Clients nach der Installation von Softwareupdates|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |Integritätsnachweis für lokale Geräte |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |Vorabdeklarieren von firmeneigenen Geräten mit IMEI- oder iOS-Seriennummer|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Version 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |Verwalten von per Volumenlizenz aus dem Windows Store für Unternehmen erworbenen Apps| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Verbesserungen an der Microsoft Passport for Work-Verwaltung|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Option für Clients zum Wechsel zu einem neuen Softwareupdatepunkt|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Clienteinstellungen zum Verwalten von Clientcacheeinstellungen und Clientpeercache |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|Clienteinstellungen: [Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>Peercache: [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |Unterstützung für Passport for Work als KSP |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Version 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |Integritätsnachweis für lokale Geräte|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |SmartLock-Einstellung für Android-Geräte|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Version 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 <!--  TP 1603 Aged out of support and all features in Current Branch Builds:
 |Improvements to Software Center|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Improvements to remote control|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
-->
 Wenn alle Features einer Technical Preview-Version in der unterstützten Mindestversion von Current Branch verfügbar sind, werden die Details für die Preview-Version aus dieser Tabelle entfernt.


## <a name="see-also"></a>Siehe auch  
[Neuerungen in System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Einführung in System Center Configuration Manager](../../core/understand/introduction.md)

