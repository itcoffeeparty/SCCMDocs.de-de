---
title: Planen des Cloudverwaltungsgateways
titleSuffix: Configuration Manager
description: Planen und Entwerfen des Cloudverwaltungsgateways (Cloud Management Gateway, CMG) zur Vereinfachung der Verwaltung internetbasierter Clients.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e5274398b1a53b5a8dce8b854bccbe0e0d92081
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Planen von Cloud Management Gateway in Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*
 
<!--1101764-->
Das Cloudverwaltungsgateway (Cloud Management Gateway, CMG) bietet eine einfache Möglichkeit zum Verwalten von Configuration Manager-Clients im Internet. Durch die Bereitstellung des CMG als Clouddienst in Microsoft Azure können Sie herkömmliche Clients verwalten, die sich ohne zusätzliche Infrastruktur im Internet bewegen. Zudem müssen Sie Ihre lokale Infrastruktur nicht im Internet verfügbar machen. 

> [!Tip]  
> Diese Funktion wurde erstmals in Version 1610 als [Vorabfunktion](/sccm/core/servers/manage/pre-release-features) eingeführt. Ab Version 1802 ist dieses Feature kein Vorabfeature mehr.  


> [!Note]  
> Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Nachdem die Voraussetzungen geschaffen wurden, müssen für die Erstellung des CMG die folgenden drei Schritte in der Configuration Manager-Konsole ausgeführt werden:
1. Bereitstellen des CMG-Clouddiensts in Azure.
2. Hinzufügen der Rolle des CMG-Verbindungspunkts. 
3. Konfigurieren von Standort und Standortrollen für den Dienst. Nach Abschluss der Bereitstellung und der Konfiguration können Clients über das Intranet oder das Internet nahtlos auf lokale Standortrollen zugreifen.

Dieser Artikel befasst sich mit Grundkenntnissen des CMG, mit der Frage, wie das CMG in Ihre Umgebung passt, und mit der Planung der Implementierung. 



## <a name="scenarios"></a>Szenarien 

Es gibt verschiedene Szenarios, in denen ein CMG von Vorteil ist. Die folgenden Szenarios zählen zu den häufiger auftretenden Szenarios:  

- Verwalten herkömmlicher Windows-Clients mit einer mit der Active Directory-Domäne verknüpften Identität. Zu diesen Clients zählen Windows 7, Windows 8.1 und Windows 10. In dem Szenario werden PKI-Zertifikate zur Sicherung des Kommunikationskanals verwendet. Zu den Verwaltungsaktivitäten zählen:  
    - Softwareupdates und Endpoint Protection
    - Inventar- und Clientstatus
    - Kompatibilitätseinstellungen
    - Softwareverteilung für das Gerät
    - Tasksequenz für direktes Windows 10-Upgrade (ab Version 1802)

- Verwalten Sie herkömmliche Windows 10-Clients mit moderner Identität, die entweder in eine hybride oder eine reine Clouddomäne eingebunden sind, mit Azure Active Directory (Azure AD). Clients verwenden Azure AD eher für die Authentifizierung als für PKI-Zertifikate. Mit Azure AD ist die Einrichtung, Konfiguration und Verwaltung einfacher als mit komplexeren PKI-Systemen. Verwaltungsaktivitäten entsprechen denen aus dem ersten Szenario. Zusätzlich dazu gibt es folgende Aktivitäten:  
    - Softwareverteilung für den Benutzer  

- Installieren des Configuration Manager-Clients auf Windows 10-Geräten über das Internet. Mit Azure AD kann das Gerät sich beim CMG für die Clientregistrierung und -zuweisung authentifizieren. Sie können den Client manuell installieren oder eine andere Softwareverteilungsmethode verwenden, z.B. Microsoft Intune.  

- Neue Gerätebereitstellung bei Co-Verwaltung. Das CMG ist für die Co-Verwaltung nicht erforderlich. Es dient als Unterstützung bei der Ausführung eines End-to-End-Szenarios für neue Geräte mit Windows AutoPilot, Azure AD, Microsoft Intune und Configuration Manager.  

### <a name="specific-use-cases"></a>Spezifische Anwendungsfälle
In diesen Szenarios können folgende Anwendungsfälle für bestimmte Geräte gelten:

- Roaminggeräte wie z.B. Laptops  

- Remote-/Filialengeräte, die kostengünstiger sind und die effizienter über das Internet statt über ein WAN oder VPN verwaltet werden können.  

- Fusionen und Übernahmen, bei denen eine Einbindung von Geräten in Azure AD und eine Verwaltung über ein CMG möglicherweise am einfachsten ist.  

> [!Important]
> Standardmäßig erhalten alle Clients eine Richtlinie für ein CMG und beginnen mit ihrer Verwendung, sobald sie internetbasiert sind. Abhängig von dem Szenario und dem Anwendungsfall, der für Ihre Organisation gilt, müssen Sie die Nutzung des CMG möglicherweise eingrenzen. Weitere Informationen finden Sie unter der Clienteinstellung [Ermöglichen Sie Clients die Verwendung eines Cloudverwaltungsgateways](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway).


## <a name="topology-design"></a>Topologieentwurf

### <a name="cmg-components"></a>CMG-Komponenten
Die Bereitstellung und der Betrieb des CMG umfassen folgende Komponenten:  

- Der **CMG-Clouddienst** in Azure authentifiziert Clientanforderungen von Configuration Manager und leitet sie an den CMG-Verbindungspunkt weiter.  
 
- Die Standortsystemrolle **CMG-Verbindungspunkt** ermöglicht eine konsistente Hochleistungsverbindung zwischen dem lokalen Netz und dem CMG-Dienst in Azure. Sie veröffentlicht zudem Einstellungen im Cloudverwaltungsgateway, einschließlich Verbindungsinformationen und Sicherheitseinstellungen. Der CMG-Verbindungspunkt leitet Clientanforderungen entsprechend den URL-Zuordnungen vom CMG zu lokalen Rollen weiter.

- Die Standortsystemrolle [**Serviceverbindungspunkt**](/sccm/core/servers/deploy/configure/about-the-service-connection-point) führt die Clouddienst-Manager-Komponente aus, die alle CMG-Bereitstellungstasks verarbeitet. Darüber hinaus überwacht die Komponente alle Informationen von Azure AD zu Dienstintegrität und -protokollierung und erstellt entsprechende Berichte. Stellen Sie sicher, dass sich Ihr Dienstverbindungspunkt im [Onlinemodus](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes) befindet.  

- Die Standortsystemrolle **Verwaltungspunkt** wartet Clientanforderungen regulär.  

- Die Standortsystemrolle **Softwareupdatepunkt** wartet Clientanforderungen regulär.  

- **Internetbasierte Clients** stellen eine Verbindung mit dem CMG her, um auf lokale Configuration Manager-Komponenten Zugriff zu haben.

- Das CMG verwendet einen **zertifikatbasierten HTTPS**-Webdienst für eine sichere Netzwerkkommunikation mit Clients.  

- Internetbasierte Clients verwenden **PKI-Zertifikate oder Azure AD** für Identität und Authentifizierung.  

- Ein [**Cloudverteilungspunkt**](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) stellt ggf. Inhalte für internetbasierte Clients bereit.  


### <a name="azure-resource-manager"></a>Azure Resource Manager
<!-- 1324735 -->
Ab Version 1802 können Sie das CMG mit einer **Azure Resource Manager-Bereitstellung** erstellen. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) ist eine moderne Plattform zum Verwalten aller Lösungsressourcen als eine einzige Entität, die als [Ressourcengruppe](/azure/azure-resource-manager/resource-group-overview#resource-groups) bezeichnet wird. Beim Bereitstellen eines Cloudverwaltungsgateways mit Azure Resource Manager verwendet der Standort Azure Active Directory (Azure AD), um die erforderlichen Cloudressourcen zu authentifizieren und zu erstellen. Diese modernisierte Bereitstellung benötigt kein klassisches Azure-Verwaltungszertifikat.  

Der CMG-Assistent bietet weiterhin die Option einer **klassischen Dienstbereitstellung** mit einem Azure-Verwaltungszertifikat. Um die Bereitstellung und Verwaltung von Ressourcen zu vereinfachen, wird die Verwendung des Azure Resource Manager-Bereitstellungsmodells für alle neuen CMG-Instanzen empfohlen. Stellen Sie nach Möglichkeit vorhandene CMG-Instanzen über Resource Manager erneut bereit. Weitere Informationen finden Sie unter [Ändern eines CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).

> [!IMPORTANT]  
> Diese Funktion aktiviert nicht die Unterstützung für Azure-Clouddienstanbieter (Cloud Service Providers, CSPs). Die CMG-Bereitstellung mit Azure Resource Manager unterstützt weiterhin den klassischen Clouddienst, der von CSPs nicht unterstützt wird. Weitere Informationen finden Sie unter [verfügbare Azure-Dienste in Azure-CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services). 


### <a name="hierarchy-design"></a>Hierarchieentwurf

Erstellen Sie das CMG am Standort der obersten Ebene in Ihrer Hierarchie. Wenn es sich dabei um einen Standort der zentralen Verwaltung handelt, sollten Sie an untergeordneten primären Standorten CMG-Verbindungspunkte erstellen. Die Clouddienst-Manager-Komponente befindet sich am Dienstverbindungspunkt, der sich ebenfalls am Standort der zentralen Verwaltung befindet. Mit diesem Entwurf kann der Dienst ggf. über verschiedene primäre Standorte hinweg geteilt werden.

Sie können mehrere CMG-Dienste in Azure und mehrere CMG-Verbindungspunkte erstellen. Mehrere CMG-Verbindungspunkte bieten einen Lastenausgleich des Clientdatenverkehrs vom CMG zu den lokalen Rollen. Weisen Sie zur Reduzierung der Netzwerklatenz das zugeordnete CMG derselben geografischen Region wie den primären Standort zu.

 > [!Note]  
 > Internetbasierte Clients und das CMG fallen nicht in eine Begrenzungsgruppe.

Andere Faktoren, wie z.B. die Anzahl der zu verwaltenden Clients, haben ebenfalls Auswirkungen auf den CMG-Entwurf. Weitere Informationen finden Sie unter [Leistung und Skalierbarkeit](#performance-and-scale).

#### <a name="example-1-standalone-primary-site"></a>Beispiel 1: Eigenständiger primärer Standort

Contoso verfügt an seinem Hauptsitz in New York City über einen eigenständigen primären Standort in einem lokalen Datacenter. 
- Das Unternehmen erstellt zur Reduzierung der Netzwerklatenz ein CMG in der Azure-Region im Osten der USA. 
- Es erstellt zwei CMG-Verbindungspunkte, die beide mit dem CMG-Einzeldienst verknüpft sind.  

Wenn sich Clients im Internet bewegen, kommunizieren sie mit dem CMG in der Azure-Region im Osten der USA. Der CMG leitet diese Kommunikation über beide CMG-Verbindungspunkte weiter.

#### <a name="example-2-hierarchy-with-site-specific-cmg"></a>Beispiel 2: Hierarchie mit standortspezifischem CMG

Fourth Coffee verfügt an seinem Hauptsitz in Seattle über einen Standort der zentralen Verwaltung in einem lokalen Datacenter. Ein primärer Standort befindet sich in demselben Datacenter, und der andere primäre Standort befindet sich in der europäischen Zentrale in Paris. 
- Am Standort der zentralen Verwaltung werden zwei CMG-Dienste erstellt:
     - Ein CMG in der Azure-Region im Westen der USA.
     - Ein CMG in der Azure-Region in Westeuropa.
- Am primären Standort in Seattle wird ein CMG-Verbindungspunkt erstellt, der mit dem CMG im Westen der USA verknüpft ist.
- Am primären Standort in Paris wird ein CMG-Verbindungspunkt erstellt, der mit dem CMG in Westeuropa verknüpft ist.

Wenn sich Clients in Seattle im Internet bewegen, kommunizieren sie mit dem CMG in der Azure-Region im Westen der USA. Der CMG leitet diese Kommunikation an den CMG-Verbindungspunkt in Seattle weiter.

Gleichermaßen kommunizieren Clients aus Paris, wenn sich diese im Internet bewegen, mit dem CMG in der Azure-Region in Westeuropa. Der CMG leitet diese Kommunikation an den CMG-Verbindungspunkt in Paris weiter. Wenn Benutzer aus Paris zum Hauptsitz des Unternehmens in Seattle reisen, kommunizieren ihre Computer weiterhin mit dem CMG in der Azure-Region in Westeuropa. 

 > [!Note]  
 > Fourth Coffee hat in Betracht gezogen, einen weiteren CMG-Verbindungspunkt am primären Standort in Paris zu erstellen, der mit dem CMG im Westen der USA verknüpft ist. Clients aus Paris würden dann beide CMGs verwenden, unabhängig von ihrem Standort. Diese Konfiguration ist zwar beim Lastenausgleich des Datenverkehrs hilfreich und bietet Dienstredundanz, sie kann aber auch Verzögerungen verursachen, wenn Clients aus Paris mit dem CMG in den USA kommunizieren. Configuration Manager-Clients kennen ihre geografische Region derzeit nicht und bevorzugen daher keinen CMG, der geografisch näher liegt. Clients verwenden einen verfügbaren CMG nach dem Zufallsprinzip.



## <a name="requirements"></a>Anforderungen

- Ein **Azure-Abonnement** zum Hosten des CMG.  

    - Ein **Azure-Administrator** muss, abhängig von Ihrem Entwurf, an der Ersterstellung bestimmter Komponenten teilnehmen. Für diese Persona sind keine Berechtigungen in Configuration Manager erforderlich.  

- Mindestens ein lokaler Windows-Server zum Hosten des **CMG-Verbindungspunkts**. Sie können diese Rolle mit anderen Configuration Manager-Standortsystemrollen zusammenstellen.  

- Der **Dienstverbindungspunkt** muss sich im [Onlinemodus](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes) befinden.   

- Ein [**Serverauthentifizierungszertifikat**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate) für das CMG.  

- Wenn Sie die klassische Azure-Bereitstellungsmethode verwenden, müssen Sie ein [**Azure-Verwaltungszertifikat**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#azure-management-certificate) verwenden.  

    > [!TIP]  
    > Ab Configuration Manager Version 1802 wird die Verwendung des **Azure Resource Manager**-Bereitstellungsmodells empfohlen. Dieses Verwaltungszertifikat ist dafür nicht erforderlich.  

- Abhängig von der Betriebssystemversion Ihres Clients und dem Authentifizierungsmodell sind möglicherweise **weitere Zertifikate** erforderlich. Weitere Informationen finden Sie unter [CMG-Zertifikate](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).  

    - Ab Version 1802 müssen Sie alle für das CMG aktivierten [**Verwaltungspunkte für die Verwendung von HTTPS**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https) konfigurieren.  

- Bei Windows 10-Clients ist möglicherweise eine Integration in **Azure AD** erforderlich. Weitere Informationen finden Sie unter [Konfigurieren von Azure-Diensten](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- Clients müssen **IPv4** verwenden.  



## <a name="specifications"></a>Spezifikationen

- Alle unter [Unterstützte Betriebssysteme für Clients und Geräte](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) aufgeführten Windows-Versionen werden für das CMG unterstützt.  

- Das CMG unterstützt nur die Rollen „Verwaltungspunkt“ und „Softwareupdatepunkt“.  

- Das CMG unterstützt keine Clients, die nur mit IPv6-Adressen kommunizieren.<!--495606-->  

- Softwareupdatepunkte, die ein Netzwerklastenausgleichsmodul verwenden, können nicht mit dem CMG ausgeführt werden. <!--505311-->  

- Ab Version 1802 wird durch CMG-Bereitstellungen mit dem Azure Resource Model nicht die Unterstützung für Azure Cloud-Dienstanbieter aktiviert. Die CMG-Bereitstellung mit Azure Resource Manager unterstützt weiterhin den klassischen Clouddienst, der von CSPs nicht unterstützt wird. Weitere Informationen finden Sie unter [Verfügbare Azure-Dienste in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)  


### <a name="support-for-configuration-manager-features"></a>Unterstützung für Configuration Manager-Features
Die folgende Tabelle enthält die CMG-Unterstützung für Configuration Manager-Features:


|Komponente  |Unterstützung  |
|---------|---------|
| Softwareupdates     | ![Unterstützt](media/green_check.png) |
| Endpoint Protection     | ![Unterstützt](media/green_check.png) |
| Hardware- und Softwareinventur     | ![Unterstützt](media/green_check.png) |
| Clientstatus und Benachrichtigungen     | ![Unterstützt](media/green_check.png) |
| Skripts ausführen     | ![Unterstützt](media/green_check.png) |
| Kompatibilitätseinstellungen     | ![Unterstützt](media/green_check.png) |
| Clientinstallation</br>(mit Azure AD-Integration)     | ![Unterstützt](media/green_check.png)  (1706) |
| Softwareverteilung (geräteorientiert)     | ![Unterstützt](media/green_check.png) |
| Softwareverteilung (benutzerorientiert, erforderlich)</br>(mit Azure AD-Integration)     | ![Unterstützt](media/green_check.png)  (1710) |
| Softwareverteilung (benutzerorientiert, verfügbar)</br>([alle Anforderungen](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)) | ![Unterstützt](media/green_check.png)  (1802) |
| Tasksequenz für direktes Windows 10-Upgrade     | ![Unterstützt](media/green_check.png)  (1802) |
| Alle anderen Tasksequenzszenarios     | ![Nicht unterstützt](media/Red_X.png) |
| Clientpush     | ![Nicht unterstützt](media/Red_X.png) |
| Automatische Standortzuweisung     | ![Nicht unterstützt](media/Red_X.png) |
| Anwendungskatalog     | ![Nicht unterstützt](media/Red_X.png) |
| Genehmigungsanforderungen für Software     | ![Nicht unterstützt](media/Red_X.png) |
| Configuration Manager-Konsole     | ![Nicht unterstützt](media/Red_X.png) |
| Remotetools     | ![Nicht unterstützt](media/Red_X.png) |
| Berichterstellungswebsite     | ![Nicht unterstützt](media/Red_X.png) |
| Wake-On-LAN     | ![Nicht unterstützt](media/Red_X.png) |
| Mac-, Linux- und UNIX-Clients     | ![Nicht unterstützt](media/Red_X.png) |
| Peercache     | ![Nicht unterstützt](media/Red_X.png) |
| Lokale Verwaltung mobiler Geräte     | ![Nicht unterstützt](media/Red_X.png) |


|Schlüssel|
|--|
|![Unterstützt](media/green_check.png) = Dieses Feature wird mit dem CMG von allen unterstützten Versionen von Configuration Manager unterstützt  |
|![Unterstützt](media/green_check.png) (*JJMM*) = Dieses Feature wird mit dem CMG ab Version *JJMM* von Configuration Manager unterstützt  |
|![Nicht unterstützt](media/Red_X.png) = Dieses Feature wird nicht mit dem CMG unterstützt |



## <a name="cost"></a>Kosten

>[!IMPORTANT]  
>Die nachfolgenden Kosteninformationen stellen lediglich Schätzwerte dar. Ihre Umgebung weist möglicherweise andere Variablen auf, die sich auf die Gesamtkosten für die Verwendung des CMG auswirken.

Das CMG verwendet folgende Azure-Komponenten, durch die Gebühren für das Azure-Abonnementkonto anfallen:

#### <a name="virtual-machine"></a>Virtuelle Maschine

- Das CMG verwendet Azure Cloud-Dienste als Platform-as-a-Service (PaaS). Dieser Dienst verwendet virtuelle Computer (Virtual Machines, VM), durch die Computekosten anfallen.  

- In Configuration Manager Version 1706 verwendet das CMG die Standard-VM A2.  

- Ab Configuration Manager Version 1710 verwendet das CMG die Standard-VM A2 V2.  

- Sie wählen aus, von wie vielen VM-Instanzen das CMG unterstützt wird. Der Standardwert ist 1, und 16 ist die Höchstwert. Diese Zahl wird bei der Erstellung des CMG festgelegt und kann nachträglich geändert werden, um den Dienst nach Bedarf zu skalieren.

- Weitere Informationen darüber, wie viele VMs Sie für die Unterstützung Ihrer Clients benötigen, finden Sie unter [Leistung und Skalierung](#performance-and-scale).

- Der [Azure-Preisrechner](https://azure.microsoft.com/pricing/calculator/) hilft Ihnen, die potenziellen Kosten zu ermitteln.

    > [!NOTE]  
    > Die Kosten für virtuelle Computer variieren je nach Region.

#### <a name="outbound-data-transfer"></a>Ausgehende Datenübertragungen

- Die aus Azure fließenden Daten (ausgehender Datenverkehr oder Download) bilden die Grundlage für die Gebühren. Alle Datenflüsse in Azure sind kostenlos (eingehender Datenverkehr oder Upload). CMG-Datenflüsse aus Azure umfassen eine Richtlinie für den Client, Clientbenachrichtigungen und vom CMG an den Standort weitergeleitete Clientantworten. Diese Antworten enthalten Inventurberichte, Statusmeldungen und den Kompatibilitätsstatus.  

- Selbst wenn kein Client mit einem CMG kommuniziert, verursacht Kommunikation im Hintergrund Netzwerkdatenverkehr zwischen dem CMG und dem lokalen Standort.  

- Zeigen Sie die **ausgehende Datenübertragungen (GB)** in der Configuration Manager-Konsole an. Weitere Informationen finden Sie unter [Überwachen von Clients auf dem CMG](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway).  

- Beachten Sie die [Preisübersicht „Bandbreite“ für Azure](https://azure.microsoft.com/pricing/details/bandwidth/), um die potenziellen Kosten zu ermitteln. Die Preise für Datenübertragungen sind gestaffelt. Je größer die Datennutzung ist, desto weniger zahlen Sie pro Gigabyte.  

- Rechnen Sie *als Schätzwert* mit ca. 100 bis 300 MB pro Client und Monat für internetbasierte Clients. Die untere Schätzung ist für eine Standardclientkonfiguration. Die obere Schätzung ist für eine dynamischere Clientkonfiguration. Ihre tatsächliche Datennutzung kann abhängig von der Konfiguration der Clienteinstellungen variieren.  

   > [!NOTE]  
   > Durch das Ausführen weiterer Aktionen, wie z.B. die Bereitstellung von Softwareaktualisierungen oder Anwendungen, erhöht sich die Menge der ausgehenden Datenübertragungen aus Azure.

#### <a name="content-storage"></a>Inhaltsspeicher

- Internetbasierte Clients erhalten gebührenfrei Inhalte der Microsoft-Softwareupdates von Windows Update. Verteilen Sie keine Updatepakete mit Inhalten von Microsoft-Updates auf einen Cloudverteilungspunkt. Andernfalls entstehen Kosten für den Speicher und abgehende Daten.  

- Bei allen anderen notwendigen Inhalten, wie z.B. Anwendungen oder Updates von Drittanbietersoftware, müssen die Updatepakete auf einen cloudbasierten Verteilungspunkt verteilt werden. Das CMG unterstützt derzeit nur den Cloudverteilungspunkt für das Senden von Inhalten an Clients.  

- Weitere Informationen finden Sie bei den Nutzungskosten einer [cloudbasierten Verteilung](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution).  

#### <a name="other-costs"></a>Sonstige Kosten

- Jeder Clouddienst verfügt über eine dynamische IP-Adresse. Jedes andere CMG verwendet eine neue dynamische IP-Adresse. Durch das Hinzufügen zusätzlicher VMs pro CMG wird die Anzahl dieser Adressen nicht erhöht.  



## <a name="performance-and-scale"></a>Leistung und Skalierbarkeit

Weitere Informationen zur CMG-Skalierbarkeit finden Sie unter [Anpassen und Skalieren von Zahlen](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg).

Mithilfe der folgenden Empfehlungen können Sie die CMG-Leistung verbessern:

- Konfigurieren Sie Cloud Management Gateway, den CMG-Verbindungspunkt und den Configuration Manager-Standortserver nach Möglichkeit in der gleichen Netzwerkregion, um die Latenz zu verringern.  

- Zurzeit wird bei der Verbindung zwischen dem Configuration Manager-Client und Cloud Management Gateway nicht zwischen Regionen unterschieden.  

- Erstellen Sie für eine Hochverfügbarkeit des Diensts pro Standort mindestens zwei CMG-Dienste und zwei CMG-Verbindungspunkte.  

- Skalieren Sie das Cloudverwaltungsgateway, um durch Hinzufügen weiterer VM-Instanzen mehr Clients zu unterstützen. Mit dem Azure-Lastenausgleich werden Clientverbindungen mit dem Dienst gesteuert.  

- Erstellen Sie weitere CMG-Verbindungspunkte, um die Last auf diese aufzuteilen. Das CMG verteilt den Datenverkehr per Roundrobin an die verbundenen CMG-Verbindungspunkte.  

- Wenn das CMG unter hoher Beanspruchung steht, da die unterstützte Anzahl der Clients überschritten wurde, werden Anforderungen weiterhin verarbeitet, jedoch möglicherweise mit Verzögerungen.  


> [!Note]  
> Während der Configuration Manager im Hinblick auf die Anzahl der Clients für einen CMG-Verbindungspunkt keine harte Grenze aufweist, ist in Windows Server standardmäßig ein Maximalwert von 16.384 für den dynamischen TCP-Portbereich festgelegt. Wenn an einem Configuration Manager-Standort mehr als 16.384 Clients mit einem einzelnen CMG-Verbindungspunkt verwaltet werden, müssen Sie den Windows Server-Grenzwert erhöhen. Alle Clients verwalten einen Kanal für Clientbenachrichtigungen, in dem ein Port für den CMG-Verbindungspunkt offen gehalten wird. Weitere Informationen zur Verwendung des Befehls „netsh“ zur Erhöhung dieses Grenzwerts finden Sie im [Microsoft Support-Artikel 929851](https://support.microsoft.com/help/929851).



## <a name="ports-and-data-flow"></a>Ports und Datenflüsse

Sie müssen keine eingehenden Ports für Ihr lokales Netzwerk öffnen. Der Dienstverbindungspunkt und der CMG-Verbindungspunkt starten sämtliche Kommunikation mit Azure und dem CMG. Diese beiden Standortsystemrollen müssen ausgehende Verbindungen zur Microsoft-Cloud erstellen können. Der Dienstverbindungspunkt sorgt für die Bereitstellung und Überwachung des Diensts in Azure und muss daher im Onlinemodus sein. Der CMG-Verbindungspunkt stellt eine Verbindung mit dem CMG her, um die Kommunikation zwischen dem CMG und lokalen Standortsystemrollen zu verwalten.

Bei dem folgenden Diagramm handelt es sich um einen grundlegenden konzeptuellen Datenfluss für das CMG: ![CMG-Datenfluss](media/cmg-data-flow.png)
   1. Der Dienstverbindungspunkt stellt über den HTTPS-Port 443 eine Verbindung zu Azure her. Die Authentifizierung erfolgt über Azure AD oder das Azure-Verwaltungszertifikat. Der Dienstverbindungspunkt stellt das CMG in Azure bereit. Das CMG erstellt den HTTPS-Clouddienst mithilfe des Serverauthentifizierungszertifikats.  

   2. Der CMG-Verbindungspunkt stellt über TCP-TLS oder HTTPS eine Verbindung mit dem CMG in Azure her. Es hält die Verbindung geöffnet und erstellt den Kanal für die zukünftige bidirektionale Kommunikation.   

   3. Der Client stellt über den HTTPS-Port 443 eine Verbindung mit dem CMG her. Die Authentifizierung erfolgt über Azure AD oder das Clientauthentifizierungszertifikat.  

   4. Das CMG leitet die Clientkommunikation über die bestehende Verbindung an den lokalen CMG-Verbindungspunkt weiter. Sie müssen keine eingehenden Firewall-Ports öffnen.  

   5. Der CMG-Verbindungspunkt leitet die Clientkommunikation an den lokalen Verwaltungspunkt und den Softwareupdatepunkt weiter.  

### <a name="required-ports"></a>Erforderliche Ports
In dieser Tabelle werden die erforderlichen Netzwerkports und -protokolle aufgeführt. Der *Client* ist das Gerät zum Initiieren der Verbindung. Hierfür ist ein ausgehender Port erforderlich. Der *Server* ist das Gerät zum Akzeptieren der Verbindung. Hierfür ist ein eingehender Port erforderlich. 

| Client  | Protokoll | Port  | Server  | Beschreibung  |
|---------|---------|---------|---------|---------|
| Dienstverbindungspunkt     | HTTPS | 443        | Azure        | CMG-Bereitstellung |
| CMG-Verbindungspunkt     |  TCP-TLS | 10140-10155        | CMG-Dienst        | Bevorzugtes Protokoll für die Erstellung des CMG-Kanals <sup>1</sup> |
| CMG-Verbindungspunkt     | HTTPS | 443        | CMG-Dienst       | Fallback zur Erstellung eines CMG-Kanals für nur eine VM-Instanz<sup>2</sup> |
| CMG-Verbindungspunkt     |  HTTPS   | 10124-10139     | CMG-Dienst       | Fallback zur Erstellung eines CMG-Kanals für mindestens zwei VM-Instanzen<sup>3</sup> |
| Client     |  HTTPS | 443         | CMG        | Allgemeine Clientkommunikation |
| CMG-Verbindungspunkt      | HTTPS oder HTTP | 443 oder 80         | Verwaltungspunkt</br>(Version 1706 oder 1710) | Lokaler Datenverkehr, Port hängt von der Konfiguration des Verwaltungspunkts ab |
| CMG-Verbindungspunkt      | HTTPS | 443      | Verwaltungspunkt</br>(Version 1802) | Lokaler Datenverkehr muss HTTPS sein |
| CMG-Verbindungspunkt      | HTTPS oder HTTP | 443 oder 80         | Softwareupdatepunkt | Lokaler Datenverkehr, Port hängt von der Konfiguration des Softwareupdatepunkts ab |

<sup>1</sup> Der CMG-Verbindungspunkt versucht zunächst, eine langlebige TCP-TLS-Verbindung mit den einzelnen CMG-VM-Instanzen herzustellen. Er stellte eine Verbindung mit der ersten VM-Instanz an Port 10140 her. Die zweite VM-Instanz verwendet Port 10141, bis zur 16. an Port 10155. Eine TCP-TLS-Verbindung erbringt beste Leistung, sie unterstützt jedoch keinen Internetproxy. Wenn der CMG-Verbindungspunkt über TCP-TLS keine Verbindung herstellen kann, greift er auf HTTPS<sup>2</sup> zurück.  

<sup>2</sup> Wenn der CMG-Verbindungspunkt über TCP-TLS<sup>1</sup> keine Verbindung zum CMG herstellen kann, stellt er über HTTPS 443 nur für eine VM-Instanz eine Verbindung zum Azure-Netzwerklastenausgleich her.  

<sup>3</sup> Wenn mindestens zwei VM-Instanzen vorhanden sind, verwendet der CMG-Verbindungspunkt für die erste VM-Instanz HTTPS 10124, nicht HTTPS 443. Er stellt an HTTPS-Port 10125 eine Verbindung zur zweiten VM-Instanz her, bis zur 16. an HTTPS-Port 10139.


### <a name="internet-access-requirements"></a>Erforderliche Berechtigungen für den Internetzugriff

Das CMG-Verbindungspunktstandortsystem unterstützt die Verwendung eines Web-Proxys. Weitere Informationen zum Konfigurieren dieser Rolle für einen Proxy finden Sie unter [Proxyserverunterstützung](/sccm/core/plan-design/network/proxy-server-support#to-set-up-the-proxy-server-for-a-site-system-server). Für den CMG-Verbindungspunkt ist eine Konnektivität mit folgenden Endpunkten erforderlich:  

- Abhängig von der Konfiguration können bestimmte Azure-Endpunkte in einzelnen Umgebungen unterschiedlich sein. Configuration Manager speichert diese Endpunkte in der Standortdatenbank. Fragen sie die Tabelle **AzureEnvironments** in SQL Server nach der Liste der Azure-Endpunkte ab.  

- ServiceManagementEndpoint (https://management.core.windows.net/)  

- StorageEndpoint (core.windows.net)  

- Für das Abrufen von Azure AD-Tokens über die Configuration Manager-Konsole und den -Client: ActiveDirectoryEndpoint (https://login.microsoftonline.com/)  

- For Azure AD-Benutzerermittlung: AAD Graph-Endpunkt (https://graph.windows.net/)  



## <a name="next-steps"></a>Nächste Schritte

- [Zertifikate für Cloud Management Gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Sicherheit und Datenschutz für Cloud Management Gateway](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Größe und Skalierungszahlen für das Cloudverwaltungsgateway](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
- [Frequently asked questions about the cloud management gateway (Häufig gestellte Fragen zu Cloud Management Gateway)](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Einrichten des Cloudverwaltungsgateways](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
