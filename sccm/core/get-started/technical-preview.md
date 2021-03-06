---
title: Technical Preview-Releases
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über das Technical Preview-Release, mit dem Sie neue Funktionen und Fähigkeiten in Configuration Manager testen können.
ms.date: 04/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6b39f5eec4209e176374dcbdffc11183625c4967
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*

**Willkommen bei System Center Configuration Manager Technical Preview**. In diesem Artikel werden Details zur Preview-Version bereitgestellt, die konstant weiterentwickelt wird und mit der neue Funktionen eingeführt werden, an denen gearbeitet wird. Mir jeder Version der Technical Preview werden neue Funktionen eingeführt, die zum Zeitpunkt der Veröffentlichung der Technical Preview nicht in Current Branch von Configuration Manager enthalten sind. Diese Funktionen werden dem Current Branch möglicherweise zu einem späteren Zeitpunkt über ein Update hinzugefügt. Bevor wir diese Funktionen jedoch fertigstellen und sie hinzufügen, möchten wir Ihnen die Gelegenheit geben, sie auszuprobieren und uns Feedback zukommen zu lassen.  

 Da es sich bei diesem Release um eine Technical Preview handelt, können Details und Funktionen noch Änderungen unterliegen.  

 Dieser Artikel enthält Informationen, die für sämtliche Versionen der Technical Preview gelten. Außerdem wird jede neue Funktion bzw. jedes neue Feature zusammen mit der Technical Preview-Version aufgeführt, in der sie zum ersten Mal verfügbar war, z.B. Version 1804 für April 2018. Diese Funktionen werden in separaten Abschnitten zu jeder Preview-Version detailliert beschrieben.  

 Informationen zu den Neuigkeiten in Current Branch von Configuration Manager finden Sie unter [What's new in System Center Configuration Manager (Neues in System Center Configuration Manager)](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Anforderungen und Einschränkungen für die Technical Preview-Version.  

> [!IMPORTANT]     
>  Die Technical Preview-Version ist ausschließlich für die Verwendung in einer Lab-Umgebung lizenziert.  Microsoft bietet möglicherweise keinen Support, und bestimmte Funktionen sind in der Preview-Software möglicherweise nicht verfügbar. Darüber hinaus gelten bei der Preview-Software im Vergleich zu handelsüblicher Software möglicherweise eingeschränkte oder veränderte Standards bei der Sicherheit, dem Datenschutz, der Barrierefreiheit, der Verfügbarkeit und der Zuverlässigkeit.  

 Informationen zu den meisten Produktvoraussetzungen finden Sie unter [Supported configurations for System Center Configuration Manager (Unterstützte Konfigurationen für System Center Configuration Manager)](../../core/plan-design/configs/supported-configurations.md). Für die Technical Preview-Versionen gelten folgenden Ausnahmen:  

-   Jede Installation wird nach 90 Tagen deaktiviert.  

-   Englisch ist die einzige unterstützte Sprache.


-   Nur die folgenden Installationsflags (Switches) werden unterstützt:  

    -   **/silent**  
    -   **/testdbupgrade**    


-   Bei der Verwendung der Technical Preview wird der Dienstverbindungspunkt standardmäßig im Onlinemodus installiert. Sie können nicht in den Offlinemodus wechseln.

-   Die zusätzlichen Artikel zu den einzelnen Versionen der Technical Preview umfassen ggf. zusätzliche Einschränkungen und Anforderungen.

-   Es gibt keine Unterstützung für die Migration zu oder von dieser Vorabversion.  

-   Es gibt keine Unterstützung für ein Upgrade auf diese Vorabversion. 

-   Es gibt keine Unterstützung für die Standortwiederherstellung aus dem Ordner „CD.Latest“.  <!--507106-->

-   Es gibt keine Unterstützung für ein Upgrade auf einen Erstellungs-Build (Current Branch) dieser Vorabversion. Wenn Updates für eine Vorschauversion verfügbar sind, finden Sie diese im Knoten **Updates und Wartung** der Configuration Manager-Konsole, von wo aus Sie sie installieren können. Ein Video zum Upgradeprozess über die Konsole finden Sie unter [Installieren von ConfigMgr-Updatepaketen](https://www.youtube.com/embed/KBd_EGFbUT8) auf „youtube.com“.  
-   Es wird nur ein eigenständiger primärer Standort unterstützt. In zentraler Verwaltungsstandort, mehrere primäre Standorte oder sekundäre Standorte werden nicht unterstützt.  

Die folgenden Produkte und Technologien werden von diesem Branch von Configuration Manager unterstützt. Die Tatsache, dass diese Produkte und Technologien hier beschrieben werden, bedeutet jedoch nicht, dass damit der Support über den Support Lifecycle der jeweiligen Produkte oder Versionen hinaus erweitert wurde. Produkte, deren Support Lifecycle überschritten ist, werden nicht für die Verwendung mit Configuration Manager unterstützt. Weitere Informationen zum Microsoft Support Lifecycle finden Sie auf der Website [Microsoft Support Lifecycle](http://go.microsoft.com/fwlink/p/?LinkId=208270).  

-   Es werden nur die folgenden Versionen von SQL Server unterstützt:  

    -   SQL Server 2017 (mit kumulativem Update 2 und höher) ab Version 1710 von Configuration Manager
    -   SQL Server 2016 (ohne Service Pack, und höher)
    -   SQL Server 2014 (mit Service Pack 1, und höher)
    -   SQL Server 2012 (mit Service Pack 3, oder höher)


-   Der Standort unterstützt bis zu 10 Clients mit einer der folgenden Windows-Version:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

##  <a name="bkmk_install"></a> Installieren und Aktualisieren der Technical Preview-Version  
 System Center Configuration Manager Technical Preview unterscheidet sich von dem aktuellen Release von System Center Configuration Manager.  

 Sie müssen zum Verwenden der Technical Preview zunächst eine **Baselineversion** des Technical Preview-Builds installieren. Nach der Installation einer Basisversion können Sie Ihre Installation mithilfe **konsoleninterner Updates** auf den neuesten Stand der aktuellen Preview-Version bringen. In der Regel werden neue Technical Preview-Versionen jeden Monat zur Verfügung gestellt.

Jede Preview-Version wird unterstützt bis drei nachfolgende Versionen verfügbar sind. Das bedeutet, bei Freigabe von Version 1708 wird die Version 1704 nicht mehr unterstützt, die Unterstützung für die Versionen 1705, 1706 und 1707 bleibt aber bestehen. Wenn die Unterstützung für eine Baseline endet, wird die Baseline jedoch weiterhin für die Installation eines neuen Technical Preview-Standorts unterstützt, bis eine neue Baselineversion verfügbar ist, solange Sie diese Installation auf eine unterstützte Version aktualisieren. Führen Sie ein Update auf die neuste verfügbare Version aus, und wiederholen Sie diesen Vorgang dann solange, bis Sie die neuste Version der Technical Preview installieren können.

> [!TIP]  
>  Bei der Installation eines Updates für die Technical Preview-Version wird Ihre Installation auf die jeweils neueste Technical Preview-Version aktualisiert. Eine Technical Preview-Installation bietet nie die Möglichkeit eines Upgrades auf eine aktuelle Branch-Installation und erhält keine Updates des aktuellen Branch-Releases.  

**Aktive Basisversionen der Technical Preview:**
   
Sie können Baselineversionen bis zu ein Jahr nach der Veröffentlichung installieren. Wenn Sie einen neuen Technical Preview-Standort erstellen, empfiehlt es sich, die neueste verfügbare Baselineversion zu verwenden.
-  **Technical Preview 1804:** Die Technical Preview 1804 für Configuration Manager steht sowohl als konsoleninternes Update als auch als neue Baselineversion zur Verfügung. Laden Sie die Baselineversionen über das [TechNet-Evaluierungscenter](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) herunter.


##  <a name="BKMK_TPFeedback"></a> Übermitteln von Feedback  
 Wir würden uns über Ihr Feedback zu den Funktionen der Technical Preview freuen. Weitere Informationen finden Sie unter [Produktfeedback](../understand/find-help.md#product-feedback).

Außerdem interessieren uns Ihre Ideen zu neuen Funktionen, die Sie in Zukunft gerne nutzen möchten. Wenn Sie neue Ideen einreichen und über die von anderen Benutzern übermittelten Ideen abstimmen möchten, [besuchen Sie unsere User Voice-Seite](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Von der neuesten Technical Preview-Version gebotene Funktionen  
Nachfolgend sind die Funktionen der neusten Releases der Technical Preview für Configuration Manager dargestellt.  Funktionen, die in einer Vorgängerversion der Technical Preview verfügbar waren, bleiben auch in späteren Versionen enthalten. Ebenso bleiben Funktionen, die dem Current Branch von Configuration Manager hinzugefügt wurden, in weiteren Releases der Technical Preview enthalten.  Klicken Sie sich durch den Inhalt der einzelnen Preview-Version, um mehr über eine bestimmte Funktion zu erfahren.  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1804"></a>Technical Preview-Version 1804
- [Konfigurieren einer remoten Inhaltsbibliothek für den Standortserver](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)<!--1357525--> 
- [Übermitteln von Feedback über die Configuration Manager-Konsole](capabilities-in-technical-preview-1804.md#bkmk_feedback)<!--1357542--> 
- [Supportcenter](capabilities-in-technical-preview-1804.md#support-center)<!--1357489--> 
- [Configuration Manager-Toolkit](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit) <!--1357145--> 
- [Deinstallieren von Anwendungen bei Widerruf von Genehmigungen](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation) <!--1357891--> 
- [Ausschließen von Active Directory-Containern von der Ermittlung](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery) <!--1358143--> 
- [Angeben der Sichtbarkeit des Links zur Anwendungskatalog-Website im Softwarecenter](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center) <!--1358214--> 
- [Filtern der automatischen Bereitstellungsregeln durch Softwareupdates für Architektur](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture) <!--1322266--> 
- [Verbesserungen bei der Bereitstellung von Betriebssystemen](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) <!--1358330,1358493--> 
- [Verbesserungen der Configuration Manager-Konsole](capabilities-in-technical-preview-1804.md#improvements-to-the-configuration-manager-console) <!--510252--> 



## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Im Lieferumfang der neuen Technical Preview-Versionen enthaltene Funktionen
Nachfolgend sind die Funktionen der Vorgängerreleases von Technical Preview für Configuration Manager dargestellt, die weiterhin unterstützt werden. 

<!-- This is the full list of new features in the past three TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Funktion |Technical Preview-Version |Current Branch-Version|  
 |----------------|---------------------|--------------------|
 | Pullverteilungspunkte unterstützen Cloudverteilungspunkte als Quelle <!--1321554-->. | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | ![Nicht hinzugefügt](media/Red_X.gif) | 
 | Unterstützung von Teildownloads im Clientpeercache zum Reduzieren der WAN-Auslastung <!--1357346--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | ![Nicht hinzugefügt](media/Red_X.gif) | 
 | Wartungsfenster im Softwarecenter <!--1358131--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | ![Nicht hinzugefügt](media/Red_X.gif) | 
 | Registerkarte „Benutzerdefiniert“ für Webseite im Softwarecenter <!--1358132--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | ![Nicht hinzugefügt](media/Red_X.gif) | 
 | Aktivieren von Aktualisierungsunterstützung für Drittanbietersoftware auf Clients <!--1357605--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | ![Nicht hinzugefügt](media/Red_X.gif) | 
 | Aktivieren von Kopieren/Einfügen von Bestandsdetails von Überwachungsansichten <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | ![Nicht hinzugefügt](media/Red_X.gif) | 
 | SCAP-Erweiterungen <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | ![Nicht hinzugefügt](media/Red_X.gif) | 
 | Übertragen der Endpoint Protection-Workload auf Intune mithilfe der Co-Verwaltung <!-- 1357365 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#transition-endpoint-protection-workload-to-intune-using-co-management) | [Version 1802](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune) |  
 | Konfigurieren der Windows-Übermittlungsoptimierung für die Verwendung von Configuration Manager-Begrenzungsgruppen <!-- 1324696 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups) | [Version 1802](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization) |  
 | Tasksequenz für direktes Windows 10-Upgrade über das Cloudverwaltungsgateway <!-- 1357149 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway) | [Version 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg) |  
 | Verbesserungen an der Tasksequenz für direktes Windows 10-Upgrade <!-- 1357425 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-windows-10-in-place-upgrade-task-sequence) | [Version 1802](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system) |  
 | Verbesserungen an PXE-fähigen Verteilungspunkten <!-- 1357580 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | ![Nicht hinzugefügt](media/Red_X.gif) | 
 | Bereitstellungsvorlagen für Tasksequenzen <!-- 1357391 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#deployment-templates-for-task-sequences) | [Version 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS) |  
 | Dashboard für den Produktlebenszyklus <!--1319632 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | ![Nicht hinzugefügt](media/Red_X.gif) | 
 | Verbesserungen bei der Berichterstellung <!--1357653 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-reporting) | [Version 1802](/sccm/core/servers/manage/list-of-reports#operating-system) |  
 | Verbesserungen am Softwarecenter <!--1357592 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-software-center) | [Version 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideInstalled) |  
 | Fallback für Begrenzungsgruppen für Verwaltungspunkte <!-- 1324594 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#boundary-group-fallback-for-management-points) | [Version 1802](/sccm/core/servers/deploy/configure/boundary-groups#management-points) |  
 | Verbesserte Unterstützung für CNG-Zertifikate <!-- 1357314 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improved-support-for-cng-certificates) | [Version 1802](/sccm/core/plan-design/network/cng-certificates-overview) |  
 | Unterstützung für Cloudverwaltungsgateway für Azure Resource Manager <!-- 1324735 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#cloud-management-gateway-support-for-azure-resource-manager) | [Version 1802](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager) |  
 | Genehmigen von Anwendungsanforderungen für Benutzer pro Gerät <!-- 1357015 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#approve-application-requests-for-users-per-device) | [Version 1802](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) |  
 | Verwenden des Softwarecenter zum Durchsuchen und Installieren von Anwendungen, die für Benutzer verfügbar sein sollen, auf in Azure AD eingebundenen Geräten <!-- 1322613 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices) | [Version 1802](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices) |  
 | Melden von Windows AutoPilot-Geräteinformationen <!-- 1351442 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-on-windows-autopilot-device-information) | [Version 1802](/sccm/core/clients/manage/co-management-prepare#new-windows-10-devices) |  
 | Verbesserungen an Configuration Manager-Richtlinien für Windows Defender Exploit Guard <!-- 1356220 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard) | [Version 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |  
 | Richtlinien für den Microsoft Edge-Browser <!-- 1357310 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#microsoft-edge-browser-policies) | [Version 1802](/sccm/compliance/deploy-use/browser-profiles) | 
 | Bericht für Anzahl von Standardbrowsern <!-- 1357830 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-for-default-browser-counts) | [Version 1802](/sccm/core/servers/manage/list-of-reports#software---companies-and-products) | 
 | Unterstützung für Windows 10-ARM64-Geräte <!-- 1353704 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#support-for-windows-10-arm64-devices) | [Version 1802](/sccm/core/plan-design/configs/support-for-windows-10) |  
 | Bereitstellungen in Phasen erstellen <!-- 1356837 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#create-phased-deployments) | [Version 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) |
 | Berichterstellung zur Co-Verwaltung <!-- 1356648 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#co-management-reporting) | [Version 1802](\sccm\core\clients\manage\client-management-dashboard) |
 | Verbesserungen des Zeitplans für die Auswertung der automatischen Bereitstellungsregel <!-- 1357133 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-automatic-deployment-rule-evaluation-schedule) | [Version 1802](/sccm/sum/deploy-use/automatically-deploy-software-updates#BKMK_CreateAutomaticDeploymentRule) |
 | Verteilungspunkt neu zuweisen <!-- 1306937 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#reassign-distribution-point) | [Version 1802](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_reassign) |
 | Verbesserungen der Hardwareinventur <!-- 1357389 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-hardware-inventory) | [Version 1802](/sccm/core/clients/manage/inventory/extend-hardware-inventory#BKMK_GreaterThan255) |
 | Verbesserungen der Clienteinstellungen für das Softwarecenter <!-- 1355146 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-client-settings-for-software-center) | [Version 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideUnapproved) |
 | Neue Einstellungen für Windows Defender Application Guard <!-- 1356256 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#new-settings-for-windows-defender-application-guard) | [Version 1802](/sccm/protect/deploy-use/create-deploy-application-guard-policy#BKMK_HIS) |
 | Verbesserungen an der Funktion „Skripts ausführen“ <!-- 1236459 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-run-scripts) | [Version 1802](/sccm/apps/deploy-use/create-deploy-scripts) |
 
  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Von vorherigen Technical Preview-Versionen gebotene Funktionen
Nachstehend sind bestimmte Funktionen aufgeführt, die im Lieferumfang der Vorgängerreleases von Technical Preview für Configuration Manager enthalten sind. Diese Funktionen bleiben in späteren Versionen bestehen, sind aber in einem Current Branch-Release noch nicht verfügbar. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Funktion |Technical Preview-Version |  
 |----------------|---------------------|
 | Clientbasierter PXE-Antwortdienst <!-- 1357148 --> | [Technical Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
 |Hochverfügbarkeit der Standortserverrolle <!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |PXE-Netzwerkstartunterstützung für IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Verwenden von Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Bewertung der Kompatibilität für Updates von Windows Update for Business <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |Datenzugriff für OData-Endpunkt <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Verbesserungen bei Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |Benutzer können Apps über das Unternehmensportal installieren <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>Siehe auch  
[Neuerungen in System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Einführung in System Center Configuration Manager](../../core/understand/introduction.md)

> [!Tip]  
> Weitere Informationen zu Current Branch-Features, die Zustimmung für die Aktivierung erfordern, finden Sie in den [Features der Vorabversion](/sccm/core/servers/manage/pre-release-features).  
> Weitere Informationen zu Current Branch-Features, die Sie zuerst aktivieren müssen, finden Sie unter [Aktivieren optionaler Features von Updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

