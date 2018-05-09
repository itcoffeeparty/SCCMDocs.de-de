---
title: Neues in Version 1802
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Änderungen und neue Funktionen, die in Version 1802 von Configuration Manager eingeführt wurden.
ms.date: 04/11/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 776db45fe64cc54e6209ba3fc45737a053613c83
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="whats-new-in-version-1802-of-system-center-configuration-manager"></a>Neuerungen in Version 1802 von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Update 1802 für Configuration Manager (Current Branch) ist als konsoleninternes Update verfügbar. Wenden Sie dieses Update auf Standorte an, an denen Version 1702, 1706 oder 1710 ausgeführt wird. <!-- baseline only statement: -->Beim Installieren eines neuen Standorts steht das Update auch als Baselineversion zur Verfügung.

Neben neuen Features umfasst dieses Release auch weitere Änderungen, beispielsweise Fehlerbehebungen. Weitere Informationen finden Sie unter [Zusammenfassung der Änderungen im aktuellen Branch von System Center Configuration Manager, Version 1802](https://support.microsoft.com/help/4101375).

<!--
The following additional updates to this release are also now available:
- [Update rollup for System Center Configuration Manager current branch, version 1710](https://support.microsoft.com/help/4057517)
-->

> [!TIP]  
> Sie müssen eine Baselineversion von Configuration Manager verwenden, um einen neuen Standort zu installieren.  
>
>  Weitere Informationen:    
>   - [Installieren von neuen Standorten](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Installieren von Updates an Standorten](/sccm/core/servers/manage/updates)  
>   - [Baseline- und Updateversionen](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Die folgenden Abschnitte enthalten Details zu den Änderungen und neuen Funktionen in Version 1802 von Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infrastruktur von Standorten

### <a name="reassign-distribution-point"></a>Verteilungspunkt neu zuweisen
<!-- 1306937 -->
Viele Kunden verfügen über eine ausgeprägte Configuration Manager-Infrastruktur und verringern die Anzahl von primären und sekundären Standorten, um ihre Umgebung einfacher zu gestalten. Sie benötigen allerdings weiterhin Verteilungspunkte für die Standorte ihrer Zweigstellen, um Inhalte für verwaltete Clients bereitzustellen. Diese Verteilungspunkte enthalten häufig mehrere Terabytes an Inhalt. Dieser Inhalt nimmt viel Zeit in Anspruch, und es wird eine hohe Netzwerk-Bandbreite benötigt, um die Daten an die Remoteserver zu übermitteln. Mithilfe dieses Features können Sie einen Verteilungspunkt einem anderen primären Standort neu zuweisen, ohne dabei den Inhalt neu zuweisen zu müssen. Über diese Aktion wird ein Update für die Standortsystemzuweisung ausgeführt. Gleichzeitig wird der gesamte Inhalt dauerhaft auf dem Server gespeichert. Weitere Informationen finden Sie unter [Reassign a distribution point](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_reassign) (Neuzuweisen eines Verteilungspunkts).

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Konfigurieren der Windows-Übermittlungsoptimierung für die Verwendung von Configuration Manager-Begrenzungsgruppen
<!-- 1324696 -->
Sie verwenden Configuration Manager-Begrenzungsgruppen, um die Inhaltsverteilung über Ihr gesamtes Unternehmensnetzwerk und Remotebüros hinweg zu definieren und zu regulieren. [Windows-Übermittlungsoptimierung](/windows/deployment/update/waas-delivery-optimization) ist eine cloudbasierte Peer-zu-Peer-Technologie zum gemeinsamen Nutzen von Inhalten auf Windows 10-Geräten. Ab diesem Release können Sie die Übermittlungsoptimierung so konfigurieren, dass bei der Freigabe von Inhalten für Peers Ihre Begrenzungsgruppen verwendet werden. Eine neue Clienteinstellung wendet die Begrenzungsgruppen-ID als Gruppen-ID für die Übermittlungsoptimierung auf dem Client an. Wenn der Client mit dem Übermittlungsoptimierungs-Clouddienst kommuniziert, wird diese ID zum Ermitteln von Peers verwendet, auf denen sich der gewünschte Inhalt befindet. Weitere Informationen finden Sie unter [Fundamental concepts for content management in System Center Configuration Manager (Grundlegende Konzepte für das Content Management)](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization).

### <a name="support-for-windows-10-arm64-devices"></a>Unterstützung für Windows 10-ARM64-Geräte
<!-- 1353704 -->
Ab diesem Release wird der Configuration Manager-Client auf Windows 10-ARM64-Geräten unterstützt. Vorhandene Clientverwaltungsfeatures sollten jetzt mit diesen neuen Geräten funktionieren. Beispiele: Hardware- und Softwareinventur, Softwareupdates und Anwendungsverwaltung. Die Betriebssystembereitstellung wird zurzeit nicht unterstützt. 

### <a name="improved-support-for-cng-certificates"></a>Verbesserte Unterstützung für CNG-Zertifikate
<!-- 1357314 -->
Configuration Manager in Version 1710 (aktueller Branch) unterstützt[CNG-Zertifikate (Cryptography: Next Generation)](/sccm/core/plan-design/network/cng-certificates-overview). In Version 1710 ist die Unterstützung auf Clientzertifikate in verschiedenen Szenarien begrenzt. 

Ab diesem Release können Sie CNG-Zertifikate für die folgenden HTTPS-fähigen Serverrollen verwenden:
- Verwaltungspunkt
- Verteilungspunkt
- Softwareupdatepunkt
- Zustandsmigrationspunkt  


### <a name="boundary-group-fallback-for-management-points"></a>Fallback für Begrenzungsgruppen für Verwaltungspunkte
<!-- 1324594 -->
Konfigurieren Sie Fallbackbeziehungen für Verwaltungspunkte zwischen [Begrenzungsgruppen](/sccm/core/servers/deploy/configure/boundary-groups). Dieses Verhalten ermöglicht eine bessere Steuerung der von Clients verwendeten Verwaltungspunkte. Weitere Informationen finden Sie unter [Configure boundary groups](/sccm/core/servers/deploy/configure/boundary-groups#management-points) (Konfigurieren von Begrenzungsgruppen).


### <a name="cloud-distribution-point-site-affinity"></a>Standortaffinität für Cloudverteilungspunkte
<!--503719-->
Dieses Feature ist für Kunden mit einer geografisch verteilten Hierarchie mit mehreren Standorten, die Cloudverteilungspunkte verwenden, von Vorteil. Wenn ein internetbasierter Client nach Inhalten sucht, gab es bisher für die vom Client empfangene Liste der Cloudverteilungspunkte keine Reihenfolge. Dies könnte dazu führen, dass internetbasierte Clients Inhalte von geografisch entfernten Cloudverteilungspunkten empfangen. Das Herunterladen von Inhalten von solch einem entfernten Server nimmt in der Regel mehr Zeit in Anspruch als bei einem näher gelegenen Server.
 
Mit der Standortaffinität für Cloudverteilungspunkte empfängt ein internetbasierter Client eine sortierte Liste. In dieser Liste werden Cloudverteilungspunkte von dem zugewiesenen Standort des Clients priorisiert. Dadurch kann der Administrator die Entwurfsabsicht für Downloads von Inhalten von Standortressourcen wahren.
 

## <a name="management-insights"></a>Einblicke für die Verwaltung
<!-- 1353967 -->
Das Feature „Einblicke für die Verwaltung“ in System Center Configuration Manager stellt Informationen zum aktuellen Zustand Ihrer Umgebung bereit. Die Informationen basieren auf der Analyse von Daten aus der Standortdatenbank. Diese Einblicke vermitteln Ihnen ein genaueres Verständnis Ihrer Umgebung, sodass Sie entsprechende Maßnahmen ergreifen können. Weitere Einzelheiten finden Sie unter [Management Insights](/sccm/core/servers/manage/management-insights)

In Configuration Manager 1802 sind folgende Einblicke verfügbar:
- Anwendungen:
    - Anwendungen ohne Bereitstellungen
- Clouddienste: <!--1356412-->
    - Bewerten Sie die Bereitschaft der Co-Verwaltung 
    - Aktivieren Sie Ihre Geräte für die hybride Verknüpfung mit Azure Active Directory
    - Modernisieren Sie Ihre Identitäts- und Zugriffsinfrastruktur
    -  Führen Sie ein Upgrade für Ihre Clients auf Windows 10, ab Version 1709 durch 
- Sammlungen:
    - Leere Sammlungen
- Vereinfachte Verwaltung: <!--1355148-->
    - Veraltete Clientversionen  
- Softwarecenter: 
    - Leiten Sie Benutzer statt zum Anwendungskatalog zum Softwarecenter weiter  
    - Verwenden Sie die neue Version von Softwarecenter 
- Windows 10: <!--1357421-->
    - Konfigurieren Sie die Windows-Telemetrie und den kommerziellen ID-Schlüssel 
    - Verbinden von Configuration Manager mit Upgradebereitschaft 
   
<!-- ## Migration  -->



## <a name="client-management"></a>Clientverwaltung

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Unterstützung für Cloudverwaltungsgateway für Azure Resource Manager
<!-- 1324735 -->
Beim Erstellen einer Instanz des [Cloudverwaltungsgateways](/sccm/core/clients/manage/plan-cloud-management-gateway) (Cloud Management Gateway, CMG) bietet der Assistent jetzt die Option, eine **Azure Resource Manager-Bereitstellung** zu erstellen. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) ist eine moderne Plattform zum Verwalten aller Lösungsressourcen als eine einzige Entität, die als [Ressourcengruppe](/azure/azure-resource-manager/resource-group-overview#resource-groups) bezeichnet wird. Beim Bereitstellen eines Cloudverwaltungsgateways mit Azure Resource Manager verwendet der Standort Azure Active Directory (Azure AD), um die erforderlichen Cloudressourcen zu authentifizieren und zu erstellen. Für diese modernisierte Bereitstellung ist kein klassisches Azure-Verwaltungszertifikat erforderlich. Weitere Informationen finden Sie unter [CMG topology design (CMG-Topologieentwurf)](/sccm/core/clients/manage/plan-cloud-management-gateway#azure-resource-manager).

> [!IMPORTANT]
> Mit dieser Funktion wird nicht die Unterstützung für Azure-Clouddienstanbieter (Cloud Service Providers, CSP) aktiviert. Die CMG-Bereitstellung mit Azure Resource Manager unterstützt weiterhin den klassischen Clouddienst, der von CSP nicht unterstützt wird. Weitere Informationen finden Sie unter [Available Azure services in Azure CSP (Verfügbare Azure-Dienste in Azure-CSP)](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="improvements-to-cloud-management-gateway"></a>Verbesserungen am Cloudverwaltungsgateway  

- Ab diesem Release ist das **Cloudverwaltungsgateway** kein Vorabfeature mehr.  

- Die Featuredokumentation wurde überarbeitet und verbessert. Weitere Informationen finden Sie in den folgenden Artikeln:
    - [Planen des Cloudverwaltungsgateways](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
    - [Größe und Skalierungszahlen für das Cloudverwaltungsgateway](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
    - [Sicherheit und Datenschutz für Cloud Management Gateway](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
    - [Frequently asked questions about the cloud management gateway (Häufig gestellte Fragen zu Cloud Management Gateway)](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
    - [Zertifikate für Cloud Management Gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
    - [Einrichten des Cloudverwaltungsgateways](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>Konfigurieren der Hardwareinventur zum Sammeln von Zeichenfolgen mit mehr als 255 Zeichen
<!-- 1357389 -->
Sie können Zeichenfolgen in Eigenschaften der Hardwareinventur so konfigurieren, dass sie mehr als 255 Zeichen umfassen. Diese Änderung gilt nur für neu hinzugefügte Klassen und Eigenschaften der Hardwareinventur, bei denen es sich nicht um Schlüssel handelt. Weitere Einzelheiten finden Sie im Artikel [Extend hardware inventory (Erweitern der Hardwareinventur)](/sccm/core/clients/manage/inventory/extend-hardware-inventory#BKMK_GreaterThan255). 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Deprecation Announcement für Linux- und Unix-Clientunterstützung
 <!--510139-->
Microsoft wird die Unterstützung für Linux- und UNIX-Clients in System Center Configuration Manager in etwa einem Jahr einstellen, sodass die Clients im Release von SCCM 1902 Anfang 2019 nicht mehr enthalten sein werden.  Das Release von Configuration Manager 1810 Ende 2018 wird das letzte Release mit den Linux- und UNIX-Clients sein. Sie werden für den gesamten Lebenszyklus von Configuration Manager 1810 unterstützt.  Nach Configuration Manager 1810 sollten Kunden für die Verwaltung von Linux-Servern die Microsoft Operations Management Suite in Betracht ziehen.  OMS verfügt über umfangreiche Linux-Unterstützung, die in den meisten Fällen über die Funktionen von Configuration Manager (einschließlich der End-to-End-Patchverwaltung für Linux) hinausgehen.

### <a name="surface-device-dashboard"></a>Surface-Gerätedashboard
<!--1355788-->
Das Gerätedashboard von Surface enthält Informationen zu den Surface-Geräten in Ihrer Umgebung. Navigieren Sie in der Konsole zu **Überwachung** > **Surface Devices** (Surface-Geräte). Sie können folgende Elemente anzeigen:
- Prozent von Surfaces
- Prozent von Surface-Modellen
- Die fünf beliebtesten Firmwareversion

Weitere Einzelheiten finden Sie im Artikel [Surface dashboard (Surface-Dashboard)](/sccm/core/clients/manage/surface-device-dashboard).

### <a name="change-in-the-configuration-manager-client-install"></a>Ändern im Configuration Manager Client Install
<!--1356195-->
Ab diesem Release wird Silverlight nicht mehr automatisch auf Clientgeräten installiert. Weitere Informationen finden Sie unter [Voraussetzungen für die Bereitstellung von Clients auf Windows-Computern](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#bkmk_ExternalDependencies).

## <a name="co-management"></a>Co-Verwaltung

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Übertragen der Endpoint Protection-Workload auf Intune mithilfe der Co-Verwaltung
<!-- 1357365 -->
 Die Endpoint Protection-Workload kann nach der Aktivierung der Co-Verwaltung auf Intune umgestellt werden. Um die Endpoint Protection-Workload zu übertragen, öffnen Sie die Seite mit den Eigenschaften der Co-Verwaltung, und schieben Sie den Schieberegler von „Configuration Manager“ auf **Pilot** oder **Alle**. Weitere Einzelheiten zu den Workloads finden Sie unter [Workloads able to be transitioned to Intune (Auf Intune umstellbare Workloads)](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune). Weitere Informationen zur Co-Verwaltung finden Sie unter [Co-Verwaltung für Windows 10-Geräte](/sccm/core/clients/manage/co-management-overview).
 
### <a name="co-management-dashboard-in-system-center-configuration-manager"></a>Dashboard für die Co-Verwaltung in System Center Configuration Manager
<!--1356648-->
Ab diesem Release können Sie ein Dashboard mit Informationen zur Co-Verwaltung anzeigen. Mithilfe des Dashboards können Sie die Computer überprüfen, die in Ihrer Umgebung gemeinsam verwaltet werden. Mithilfe der Diagramme können Geräte identifiziert werden, bei denen möglicherweise ein Eingriff erforderlich ist. Weitere Einzelheiten finden Sie im Artikel [Co-management dashboard (Dashboard für die Co-Verwaltung)](\sccm\core\clients\manage\client-management-dashboard). 


## <a name="compliance-settings"></a>Kompatibilitätseinstellungen

### <a name="microsoft-edge-browser-policies"></a>Richtlinien für den Microsoft Edge-Browser
<!-- 1357310 -->
Kunden, die den [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256)-Webbrowser auf Windows 10-Clients verwenden, erstellen eine Richtlinie für Configuration Manager-Konformitätseinstellungen, um verschiedene Microsoft Edge-Einstellungen zu konfigurieren. Weitere Informationen finden Sie unter [Create Microsoft Edge browser profile (Erstellen eines Microsoft Edge-Browserprofils)](/sccm/compliance/deploy-use/browser-profiles). 



## <a name="application-management"></a>Anwendungsverwaltung

### <a name="allow-user-interaction-when-installing-an-application"></a>Ermöglichen der Benutzerinteraktion beim Installieren einer Anwendung
<!-- 1356976 -->
Erlauben Sie einem Benutzer, während der Ausführung der Tasksequenz mit einer Anwendungsinstallation zu interagieren. Führen Sie beispielsweise einen Setupvorgang aus, der den Endbenutzer nach verschiedenen Optionen befragt. Einige Anwendungsinstallationsprogramme können Eingabeaufforderungen an Benutzer nicht deaktivieren, oder der Installationsprozess fordert bestimmte Konfigurationswerte an, die nur dem Benutzer bekannt sind. Mithilfe dieser Funktion behalten Sie diese Installationsszenarien im Griff. Weitere Informationen finden Sie unter [Angeben von Optionen für die Benutzerfreundlichkeit des Bereitstellungstyps](/sccm/apps/deploy-use/create-applications#specify-user-experience-options-for-the-deployment-type).

### <a name="do-not-automatically-upgrade-superseded-applications"></a>Führen Sie kein automatisches Upgrade für abgelöste Anwendungen aus
<!-- 1351266 -->
Konfigurieren Sie eine Anwendungsbereitstellung so, dass eine abgelöste Version nicht automatisch aktualisiert wird. Wenn Sie dann die Bereitstellung erstellen, können Sie auf der Seite **Bereitstellungseinstellungen** des **Assistenten zum Bereitstellen von Software** die Option **Automatisch ein Upgrade aller abgelösten Versionen dieser Anwendung ausführen** für **verfügbare** oder **erforderliche** Installationen aktivieren oder deaktivieren. Weitere Informationen finden Sie unter [Specify deployment settings (Angeben von Bereitstellungseinstellungen)](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings).

### <a name="approve-application-requests-for-users-per-device"></a>Genehmigen von Anwendungsanforderungen für Benutzer pro Gerät
<!-- 1357015 -->
Ab diesem Release ist der Name des Geräts jetzt Teil der Anforderung, wenn ein Benutzer eine Anwendung anfordert, für die eine Genehmigung erforderlich ist. Wenn ein Administrator die Anforderung genehmigt, kann der Benutzer die Anwendung nur auf diesem spezifischen Gerät installieren. Der Benutzer muss eine weitere Anforderung senden, um die Anwendung auf einem anderen Gerät installieren zu können. Weitere Informationen finden Sie unter [Specify deployment settings (Angeben von Bereitstellungseinstellungen)](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings).

 > [!Note]  
 > Dies ist ein optionales Feature. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  


### <a name="run-scripts-improvements"></a>Verbesserungen an der Funktion „Skripts ausführen“ 
<!-- 1236459 -->
 Ab diesem Release ist **Skripts ausführen** kein Vorabfeature mehr. Die Skriptausgabe wird jetzt mithilfe von JSON-Formatierung zurückgegeben. Weitere Informationen finden Sie unter [Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole](/sccm/apps/deploy-use/create-deploy-scripts).


## <a name="operating-system-deployment"></a>Betriebssystembereitstellung

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Tasksequenz für direktes Windows 10-Upgrade über das Cloudverwaltungsgateway
<!-- 1357149 -->
Die [Tasksequenz für direktes Windows 10-Upgrade](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version) unterstützt jetzt die Bereitstellung auf internetbasierten Clients, die über das [Cloudverwaltungsgateway](/sccm/core/clients/manage/plan-cloud-management-gateway) verwaltet werden. Mit dieser Funktion können Remotebenutzer einfacher ein Upgrade auf Windows 10 durchführen, ohne eine Verbindung mit dem Unternehmensnetzwerk herstellen zu müssen. Weitere Informationen finden Sie unter [Deploy a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg).

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Verbesserungen an der Tasksequenz für direktes Windows 10-Upgrade
<!-- 1357425 -->
Die Standardvorlage der Tasksequenz für das direkte Windows 10-Upgrade enthält jetzt zusätzliche Gruppen mit empfohlenen Aktionen, die vor und nach dem Upgradevorgang hinzugefügt werden können. Diese Aktionen werden häufig von Kunden eingesetzt, die erfolgreiche Upgrades ihrer Geräte auf Windows 10 durchführen. Weitere Informationen finden Sie unter [Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-to-prepare-for-upgrade).

### <a name="improvements-to-operating-system-deployment"></a>Verbesserungen bei der Betriebssystembereitstellung
Dieses Release umfasst die folgenden Verbesserungen an der Betriebssystembereitstellung:
 - In Windows PE werden Sie beim Starten der Datei „cmtrace.exe“ nicht mehr aufgefordert, zu entscheiden, ob dieses Programm die Standardanzeige für Protokolldateien sein soll. <!-- SMS 500897 -->
 - Fügen Sie Startimages zum Tasksequenzschritt [Paketinhalt herunterladen](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent) hinzu.
 - Verbesserungen am Schritt [Tasksequenz ausführen](/sccm/osd/understand/task-sequence-steps#child-task-sequence): <!-- 1261338 -->   
     - Unterstützung für alle Szenarien der Betriebssystembereitstellung mithilfe von Softwarecenter, PXE und Medien.
     - Verbesserungen bei Konsolenaktionen wie Kopieren, Importieren, Exportieren und Warnung beim Löschen von Objekten.
     - Unterstützung für den Assistenten zum [Erstellen von vorab bereitgestellten Inhaltsdateien](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).
     - Integration in die Überprüfung der Bereitstellung. Weitere Informationen finden Sie unter [Risikoreiche Tasksequenzbereitstellungen](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS). 
     - Der Schritt "Tasksequenz ausführen" kann nun über mehrere Ebenen von Tasksequenzen hinweg verwendet werden, nicht nur für eine einzelne Beziehung zwischen über- und untergeordneten Elementen. Bei Beziehungen mit mehreren Ebenen erhöht sich die Komplexität, daher ist Vorsicht geboten. Diese Beziehungen werden nach wie vor auf Zirkelbezüge geprüft.
    
### <a name="deployment-templates-for-task-sequences"></a>Bereitstellungsvorlagen für Tasksequenzen
<!-- 1357391 -->
Der [Bereitstellungs-Assistent für Tasksequenzen](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS) kann jetzt eine Bereitstellungsvorlage erstellen. Die Bereitstellungsvorlage kann gespeichert und auf eine vorhandene oder neue Tasksequenz angewendet werden, um eine Bereitstellung zu erstellen. 

### <a name="phased-deployments-for-task-sequences"></a>Bereitstellung in Phasen für Tasksequenzen
<!--1356837-->
 Bei Bereitstellungen in Phasen handelt es sich um ein [Vorabfeature](/sccm/core/servers/manage/pre-release-features). Bereitstellungen in Phasen automatisieren ein koordiniertes Rollout einer Tasksequenz in einer bestimmten Reihenfolge über mehrere Sammlungen hinweg. Sie können [stufenweise Bereitstellungen](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) mit einer von zwei Standardphasen erstellen oder mehrere Phasen manuell konfigurieren. Die stufenweise Bereitstellung von Tasksequenzen unterstützt keine PXE- oder Medieninstallation.




## <a name="software-center"></a>Software Center

### <a name="install-multiple-applications-in-software-center"></a>Installieren mehrerer Anwendungen im Softwarecenter
<!-- 1357126 -->
Falls ein Benutzer oder Techniker mehrere Anwendungen auf einem Gerät installieren muss, unterstützt das Softwarecenter jetzt die Installation mehrerer ausgewählter Anwendungen. Durch dieses Verhalten kann der Benutzer effizienter arbeiten und muss nicht mehr darauf warten, dass eine Installation abgeschlossen wird, bevor er mit der nächsten beginnen kann. Weitere Informationen finden Sie unter [Install multiple applications (Installieren mehrerer Anwendungen)](/sccm/core/understand/software-center#install-multiple-applications) im neuen Softwarecenter-Benutzerleitfaden.

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Verwenden des Softwarecenters zum Durchsuchen und Installieren von Anwendungen, die für Benutzer verfügbar sein sollen, auf in Azure AD eingebundenen Geräten
<!-- 1322613 -->
Wenn Sie Anwendungen als für Benutzer verfügbar bereitstellen, können diese die Anwendungen über das Softwarecenter auf Azure Active Directory-Geräten durchsuchen und installieren. Weitere Informationen finden Sie unter [Deploy user-available applications on Azure AD-joined devices (Bereitstellen von für Benutzer verfügbare Anwendungen auf in Azure AD eingebundenen Geräten)](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).

### <a name="hide-installed-applications-in-software-center"></a>Installierte Anwendungen im Softwarecenter ausblenden
<!--1357592-->
Installierte Anwendungen können jetzt im Softwarecenter ausgeblendet werden. Bereits installierte Anwendungen werden auf der Registerkarte „Anwendungen“ nicht mehr angezeigt, wenn diese Option unter „Clienteinstellungen“ aktiviert wurde. Diese Option ist als Standard festgelegt, wenn Sie Configuration Manager 1802 installieren oder ein Upgrade auf diese Version durchführen.  Installierte Anwendungen können weiterhin auf der Registerkarte „Installationsstatus“ überprüft werden. [Installierte Anwendungen im Softwarecenter ausblenden](/sccm/core/clients/deploy/about-client-settings#BKMK_HideInstalled) verfügt über zusätzliche Details.   

### <a name="hide-unapproved-applications-in-software-center"></a>Nicht genehmigte Anwendungen im Softwarecenter ausblenden
 <!--1355146-->
Wenn diese Option der Clienteinstellungen aktiviert ist, werden Anwendungen, die zwar für den Benutzer verfügbar sind, für die aber eine Genehmigung benötigt wird, im Softwarecenter ausgeblendet.  [Nicht genehmigte Anwendungen im Softwarecenter ausblenden](/sccm/core/clients/deploy/about-client-settings#BKMK_HideUnapproved) verfügt über zusätzliche Details.  

### <a name="software-center-shows-user-additional-compliance-information"></a>Das Softwarecenter zeigt zusätzliche Konformitätsinformationen für Benutzer an
<!-- 1235616 -->
 Bei Verwendung des Status „Integritätsnachweis für Geräte“ als Konformitätsrichtlinienregel für bedingten Zugriff auf Unternehmensressourcen wird dem Benutzer im Softwarecenter jetzt die Einstellung „Integritätsnachweis für Geräte“ angezeigt, die nicht kompatibel ist.


 ## <a name="software-updates"></a>Softwareupdates 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>Planen Sie die Auswertung der automatischen Bereitstellungsregel so, dass sie nicht an einem Basistag erfolgt. 
<!--1357133-->
Automatische Bereitstellungsregeln können so geplant werden, dass sie nicht an einem Basistag ausgewertet werden. Wenn der Patchvorgang, der am Dienstag ausgeführt werden soll, bei Ihnen auf einen Mittwoch fällt, kann der Zeitplan für die Auswertung für den zweiten Dienstag des Monats versetzt um einen Tag festgelegt werden. Weitere Einzelheiten finden Sie unter [Automatisches Bereitstellen von Softwareupdates](/sccm/sum/deploy-use/automatically-deploy-software-updates#BKMK_CreateAutomaticDeploymentRule). 



## <a name="reporting"></a>Berichterstellung

### <a name="report-for-default-browser-counts"></a>Bericht für Anzahl von Standardbrowsern
<!-- 1357830 -->
Es gibt jetzt einen neuen Bericht, der die Anzahl von Clients anzeigt, auf denen ein bestimmter Webbrowser als Windows-Standardeinstellung festgelegt ist. Siehe den Bericht **Anzahl von Standardbrowsern** in der Berichtsgruppe **Software – Unternehmen und Produkte**. Weitere Informationen finden Sie in der [Berichtsliste](/sccm/core/servers/manage/list-of-reports#software---companies-and-products).

### <a name="report-on-windows-autopilot-device-information"></a>Melden von Windows AutoPilot-Geräteinformationen
<!-- 1351442 -->
Windows AutoPilot ist eine moderne Lösung für das Onboarding und Konfigurieren neuer Windows 10-Geräte. Weitere Informationen finden Sie unter [Übersicht über Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Eine Methode, vorhandene Geräte bei Windows AutoPilot zu registrieren, ist das Hochladen von Geräteinformationen in den Microsoft Store für Unternehmen und Bildungseinrichtungen. Zu diesen Informationen gehört die Seriennummer des Geräts, der Windows-Produktbezeichner und eine Hardwarebezeichner. In Configuration Manager können Sie diese Geräteinformationen mit dem neuen Bericht, **Windows AutoPilot-Geräteinformationen**, im Berichtsknoten **Hardware – Allgemein** erfassen und melden. Weitere Informationen finden Sie unter [Neue Windows 10-Geräte](/sccm/core/clients/manage/co-management-prepare#new-windows-10-devices) bei der Vorbereitung auf die Co-Verwaltung.

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>Bericht „Windows 10-Wartungsdetails für eine bestimmte Sammlung“
<!--1357653-->
Der Bericht **Windows 10-Wartungsdetails für eine bestimmte Sammlung** zeigt allgemeine Informationen zur Windows 10-Wartung für eine bestimmte Sammlung an. Dieser Bericht die Ressourcen-ID, den NetBIOS-Namen, den Betriebssystemnamen, den Namen der Betriebssystemversion, den Build, den Betriebssystembranch und den Wartungsstatus für Windows 10-Geräte. Weitere Informationen finden Sie in der [Berichtsliste](/sccm/core/servers/manage/list-of-reports#operating-system)



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>Schützen von Geräten

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Verbesserungen an Configuration Manager-Richtlinien für Windows Defender Exploit Guard
<!-- 1356220 -->
In Configuration Manager für [Windows Defender Exploit Guard](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy#BKMK_ASR) wurden zusätzliche Richtlinieneinstellungen für die Komponenten für die [Verringerung der Angriffsfläche](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy#BKMK_CFA) und den [überwachten Ordnerzugriff](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) hinzugefügt.

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Neue Einstellungen für die Hostinteraktion für Windows Defender Application Guard
<!-- 1356256 -->
Es gibt zwei neue Einstellungen für die Hostinteraktion für [Windows Defender Application Guard](/sccm/protect/deploy-use/create-deploy-application-guard-policy#BKMK_HIS) für Windows 10 ab Version 1709: 
- Sie können Websites Zugriff auf den virtuellen Grafikprozessor des Hosts erteilen. 
- Dateien, die im Container heruntergeladen werden, können dauerhaft auf dem Host gespeichert werden. 




## <a name="configuration-manager-console"></a>Configuration Manager-Konsole

### <a name="improvements-to-the-configuration-manager-console"></a>Verbesserungen der Configuration Manager-Konsole 
Dieses Release umfasst folgende Verbesserungen an der Configuration Manager-Konsole.
- Gerätelisten unter „Bestand und Kompatibilität“ > „Geräte“ werden jetzt standardmäßig dem primären Benutzer angezeigt. Diese Spalte wird nur im Knoten „Geräte“ angezeigt. Der Benutzer, der als letztes angemeldet war, kann auch als optionale Spalte hinzugefügt werden.<!-- 1357280 --> Aktivieren Sie Clienteinstellungen [Affinität zwischen Benutzer und Gerät](/sccm/core/clients/deploy/about-client-settings#user-and-device-affinity) für den Standort, um einem primären Benutzer ein Gerät zuzuordnen.
- Wenn eine Sammlung Mitglied einer anderen Sammlung ist und umbenannt wird, wird der neue Name unter den Mitgliedschaftsregeln aktualisiert.<!--1357282--> 
- Bei Verwendung von Remotesteuerung für einen Client mit mehreren Monitoren mit unterschiedlicher DPI-Skalierung kann der Mauscursor die Zuordnung dazwischen jetzt dazwischen ordnungsgemäß ausführen. <!--433170-->
- Im [Office 365 Client Management-Dashboard](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard) wird eine Liste von relevanten Geräten angezeigt, wenn die Diagrammabschnitte ausgewählt werden. <!--1357281 --> 



## <a name="next-steps"></a>Nächste Schritte
Wenn Sie zum Installieren dieser Version bereit sind, sehen Sie sich [Updates für Configuration Manager](/sccm/core/servers/manage/updates) an.
