---
title: Technical Preview-Releases
titleSuffix: Configuration Manager
description: "Erfahren Sie mehr über das Technical Preview-Release, mit der Sie neue Funktionen und Fähigkeiten in System Center Configuration Manager testen können."
ms.custom: na
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: "157"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 692cf74cbae3f176bab254aeec0e63c10929cfcc
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/04/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*

**Willkommen bei System Center Configuration Manager Technical Preview**. In diesem Artikel werden Details zur Preview-Version bereitgestellt, die konstant weiterentwickelt wird und mit der neue Funktionen eingeführt werden, an denen gearbeitet wird. Mir jeder Version der Technical Preview werden neue Funktionen eingeführt, die zum Zeitpunkt der Veröffentlichung der Technical Preview nicht in Current Branch von Configuration Manager enthalten sind. Diese Funktionen werden dem Current Branch möglicherweise zu einem späteren Zeitpunkt über ein Update hinzugefügt. Bevor wir diese Funktionen jedoch fertigstellen und sie hinzufügen, möchten wir Ihnen die Gelegenheit geben, sie auszuprobieren und uns Feedback zukommen zu lassen.  

 Da es sich hierbei um eine Technical Preview handelt, können Details und Funktionen noch Änderungen unterliegen.  

 Dieser Artikel enthält Informationen, die für sämtliche Versionen der Technical Preview gelten. Außerdem wird jede neue Funktion zusammen mit der Technical Preview-Version aufgeführt, in der sie zum ersten Mal verfügbar war, z.B. Version 1712 für Dezember 2017. Diese Funktionen werden in separaten Abschnitten zu jeder Preview-Version detailliert beschrieben.  

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

-   Es gibt keine Unterstützung für ein Upgrade auf einen Erstellungs-Build (Current Branch) dieser Vorabversion. Wenn Updates für eine Vorschauversion verfügbar sind, finden Sie diese im Knoten **Updates und Wartung** der Configuration Manager-Konsole, von wo aus Sie sie installieren können. Ein Video zum Upgradeprozess über die Konsole finden Sie unter [Installieren von ConfigMgr-Updatepaketen](https://www.youtube.com/embed/KBd_EGFbUT8) auf „youtube.com“.  
-   Es wird nur ein eigenständiger primärer Standort unterstützt. In zentraler Verwaltungsstandort, mehrere primäre Standorte oder sekundäre Standorte werden nicht unterstützt.  

Die folgenden Produkte und Technologien werden von diesem Branch von Configuration Manager unterstützt. Die Tatsache, dass diese Produkte und Technologien hier beschrieben werden, bedeutet jedoch nicht, dass damit der Support über den Support Lifecycle der jeweiligen Produkte oder Versionen hinaus erweitert wurde. Produkte, deren Support Lifecycle überschritten ist, werden nicht für die Verwendung mit Configuration Manager unterstützt. Weitere Informationen zum Microsoft Support Lifecycle finden Sie auf der Website [Microsoft Support Lifecycle](http://go.microsoft.com/fwlink/p/?LinkId=208270).  

-   Es werden nur die folgenden Versionen von SQL Server unterstützt:  

    -   SQL Server 2016 (ohne Service Pack, und höher)
    -   SQL Server 2014 (mit Service Pack 1, und höher)
    -   SQL Server 2012 (mit Service Pack 3, oder höher)


-   Der Standort unterstützt bis zu 10 Clients mit einer der folgenden Windows-Version:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  

##  <a name="bkmk_install"></a> Installieren und Aktualisieren der Technical Preview-Version  
 System Center Configuration Manager Technical Preview unterscheidet sich von dem aktuellen Release von System Center Configuration Manager.  

 Sie müssen zum Verwenden der Technical Preview zunächst eine **Baselineversion** des Technical Preview-Builds installieren. Nach der Installation einer Basisversion können Sie Ihre Installation mithilfe **konsoleninterner Updates** auf den neuesten Stand der aktuellen Preview-Version bringen. In der Regel werden neue Technical Preview-Versionen jeden Monat zur Verfügung gestellt.

Jede Preview-Version wird unterstützt bis drei nachfolgende Versionen verfügbar sind. Das bedeutet, bei Freigabe von Version 1708 wird die Version 1704 nicht mehr unterstützt, die Unterstützung für die Versionen 1705, 1706 und 1707 bleibt aber bestehen. Wenn die Unterstützung für eine Baseline endet, wird die Baseline jedoch weiterhin für die Installation eines neuen Technical Preview-Standorts unterstützt, bis eine neue Baselineversion verfügbar ist, solange Sie diese Installation auf eine unterstützte Version aktualisieren. Führen Sie ein Update auf die neuste verfügbare Version aus, und wiederholen Sie diesen Vorgang dann solange, bis Sie die neuste Version der Technical Preview installieren können.

> [!TIP]  
>  Bei der Installation eines Updates für die Technical Preview-Version wird Ihre Installation auf die jeweils neueste Technical Preview-Version aktualisiert.    Eine Technical Preview-Installation bietet nie die Möglichkeit eines Upgrades auf eine aktuelle Branch-Installation und erhält keine Updates von der aktuellen Branch-Version.  

**Aktive Basisversionen der Technical Preview:**  
Sie können Baselineversionen bis zu ein Jahr nach der Veröffentlichung installieren. Wenn Sie einen neuen Technical Preview-Standort erstellen, empfiehlt es sich, die neueste verfügbare Baselineversion zu verwenden.
-  **Technical Preview 1711:** Die Technical Preview 1711 für Configuration Manager steht sowohl als konsoleninternes Update als auch als neue Baselineversion zur Verfügung. Laden Sie die Baselineversionen über das [TechNet-Evaluierungscenter](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) herunter.


##  <a name="BKMK_TPFeedback"></a> Übermitteln von Feedback  
 Wir würden uns über Ihr Feedback zu den Funktionen der Technical Preview freuen. Weitere Informationen finden Sie unter [Produktfeedback](../understand/find-help.md#product-feedback).

Außerdem interessieren uns Ihre Ideen zu neuen Funktionen, die Sie in Zukunft gerne nutzen möchten. Wenn Sie neue Ideen einreichen und über die von anderen Benutzern übermittelten Ideen abstimmen möchten, [besuchen Sie unsere User Voice-Seite](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Von der neuesten Technical Preview-Version gebotene Funktionen  
Nachfolgend sind die Funktionen der neusten Releases der Technical Preview für Configuration Manager dargestellt.  Funktionen, die in einer Vorgängerversion der Technical Preview verfügbar waren, bleiben auch in späteren Versionen enthalten. Ebenso bleiben Funktionen, die dem Current Branch von Configuration Manager hinzugefügt wurden, in weiteren Releases der Technical Preview enthalten.  Klicken Sie sich durch den Inhalt der einzelnen Preview-Version, um mehr über eine bestimmte Funktion zu erfahren.  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1712"></a>Technical Preview Version 1712
- [Führen Sie kein automatisches Upgrade für abgelöste Anwendungen aus](capabilities-in-technical-preview-1712.md#do-not-automatically-upgrade-superseded-applications) <!-- 1351266 --> 
- [Installieren mehrerer Anwendungen im Softwarecenter](capabilities-in-technical-preview-1712.md#install-multiple-applications-in-software-center) <!-- 1357126 --> 
- [Ändern im Configuration Manager Client Install](capabilities-in-technical-preview-1712.md#change-in-the-configuration-manager-client-install) <!-- 1356195 --> 
- [Ändern des Surface-Gerätedashboards](capabilities-in-technical-preview-1712.md#change-to-the-surface-device-dashboard) <!-- 1355788 --> 
- [Verbesserungen des Office 365 Client Management-Dashboards](capabilities-in-technical-preview-1712.md#improvements-to-office-365-client-management-dashboard) <!-- 1357281 --> 
- [Verbesserungen der Configuration Manager-Konsole](capabilities-in-technical-preview-1712.md#improvements-to-the-configuration-manager-console) <!-- 1357280,1357282 --> 
- [Verbesserung der Bereitstellung von Betriebssystemen](capabilities-in-technical-preview-1712.md#improvements-to-operating-system-deployment) <!-- SMS 500897 --> 
- [Integration der Feedback Hub-App für Windows 10](capabilities-in-technical-preview-1712.md#windows-10-feedback-hub-app-integration) <!-- NA -->




## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Im Lieferumfang der neuen Technical Preview-Versionen enthaltene Funktionen
Nachfolgend sind die Funktionen der Vorgängerreleases von Technical Preview für Configuration Manager dargestellt, die weiterhin unterstützt werden. 

<!-- This is the full list of new features in the past three TP releases. Each month, add features from the list above to the top of this table. Then remove the bottom of this list (and/or move individual items not in CB to the third table below). -->

 |Funktion |Technical Preview-Version |Current Branch-Version|  
 |----------------|---------------------|--------------------|
 |Schritt „Tasksequenz ausführen“ <!-- 1261338 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |[Version 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence)    |
 |Ermöglichen des Eingreifens des Benutzers beim Installieren einer Anwendung <!-- 1356976 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |![Nicht hinzugefügt](media/Red_X.gif)    |
 |Windows 10-Telemetrie für Windows Analytics-Geräteintegrität <!--1356148 --> | [Technical Preview 1710](capabilities-in-technical-preview-1710.md#limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health) |[Version 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#reporting)    |
 |Verbesserungen an Softwarecenter-Symbolen <!-- 1356194 --> | [Technical Preview 1710](capabilities-in-technical-preview-1710.md#software-center-no-longer-distorts-icons-larger-than-250x250) |[Version 1710](/sccm/apps/plan-design/plan-for-and-configure-application-management#supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center)    |
 |Überprüfen der Konformität über das Softwarecenter für co-verwaltete Geräte<!-- 1356374 -->|[Technical Preview 1710](capabilities-in-technical-preview-1710.md#check-compliance-from-software-center-for-co-managed-devices)|[Version 1710](/sccm/core/clients/manage/co-management-overview)    |
 |Eingeschränkte Unterstützung für CNG-Zertifikate<!-- 1356191 -->| [Technical Preview 1710](capabilities-in-technical-preview-1710.md#limited-support-for-cng-certificates)|[Version 1710](/sccm/core/plan-design/network/cng-certificates-overview)    |
 |Unterstützung für Exploit Guard <!--1355468 --> | [Technical Preview 1710](capabilities-in-technical-preview-1710.md#support-for-exploit-guard) |[Version 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)    |
 |Verbesserte Beschreibungen für ausstehende Computerneustarts <!-- 1356283  -->| [Technical Preview 1710](capabilities-in-technical-preview-1710.md)|[Version 1710](/sccm/core/clients/manage/manage-clients)    |
 |Änderungen an Device Guard-Richtlinien <!-- 1355092  -->| [Technical Preview 1710](capabilities-in-technical-preview-1710.md)|[Version 1710](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)    |
 |Konfigurieren und Bereitstellen von Windows Defender Application Guard-Richtlinien <!-- 1351960  -->| [Technical Preview 1710](capabilities-in-technical-preview-1710.md)|[Version 1710](/sccm/protect/deploy-use/create-deploy-application-guard-policy)    |
 |Verbesserungen für die Bereitstellung von PowerShell-Skripts aus Configuration Manager <!-- 1236459 -->| [Technical Preview 1710](capabilities-in-technical-preview-1710.md#improvements-for-deploying-powershell-scripts-from-configuration-manager) | [Version 1710](/sccm/apps/deploy-use/create-deploy-scripts)
 |Verbesserte Benutzeroberfläche für VPN-Profile in der Configuration Manager-Konsole <!-- 1313282 --> | [Tech Preview 1709](capabilities-in-technical-preview-1709.md) |[Version 1710](/sccm/protect/deploy-use/create-vpn-profiles)    |
 |Co-Verwaltung für Windows 10-Geräte|[Tech Preview 1709](capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices)|[Version 1710](/sccm/core/clients/manage/co-management-overview.md)|
 

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Von vorherigen Technical Preview-Versionen gebotene Funktionen
Nachstehend sind bestimmte Funktionen aufgeführt, die im Lieferumfang der Vorgängerreleases von Technical Preview für Configuration Manager enthalten sind. Diese Funktionen bleiben in späteren Versionen bestehen, sind aber in einem Current Branch-Release noch nicht verfügbar. 

<!-- This is the list of individual features that are still in TP (not in CB). Note there is no third column in this table! Each month review and remove from this list for anything that's now available in CB. Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column) -->

 |Funktion |Technical Preview-Version |  
 |----------------|---------------------|
 |Einblicke für die Verwaltung <!-- 1353967 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#management-insights)|
 |Surface-Gerätedashboard <!-- 1355788 --> |[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|
 |Hochverfügbarkeit der Standortserverrolle <!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |PXE-Netzwerkstartunterstützung für IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Bewertung des Integritätsnachweises für Geräte für Konformitätsrichtlinien für bedingten Zugriff <!-- 1235616 -->|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|
 |Verwenden von Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Bewertung der Kompatibilität für Updates von Windows Update for Business <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |Datenzugriff für OData-Endpunkt <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Verbesserungen bei Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |Benutzer können Apps über das Unternehmensportal installieren <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|





## <a name="see-also"></a>Siehe auch  
[Neuerungen in System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Einführung in System Center Configuration Manager](../../core/understand/introduction.md)
