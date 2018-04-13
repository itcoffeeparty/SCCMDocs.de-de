---
title: Anforderungen an die Infrastruktur für Betriebssystembereitstellungen
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zu den externen und produktspezifischen Abhängigkeiten und Anforderungen für die Betriebssystembereitstellung.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
caps.latest.revision: 24
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 36e49206154a1c061fb8266e0c8ed8691cc4d4f0
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="infrastructure-requirements-for-os-deployment-in-system-center-configuration-manager"></a>Anforderungen an die Infrastruktur für die Betriebssystembereitstellung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Für die Betriebssystembereitstellung in Configuration Manager sind sowohl externe als auch produktspezifische Abhängigkeiten vorhanden. Dieser Artikel unterstützt Sie bei der Planung der Infrastruktur für die Betriebssystembereitstellung.  



##  <a name="BKMK_ExternalDependencies"></a> Externe Abhängigkeiten von Configuration Manager  
 Im folgenden Abschnitt finden Sie Informationen zu externen Tools, Installationspaketen und Betriebssystemversionen, die für die Bereitstellung von Betriebssystemen in Configuration Manager erforderlich sind.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK für Windows 10  
 Das Windows Assessment and Deployment Kit (ADK) umfasst Tools und Dokumentationen zur Unterstützung der Konfiguration und Bereitstellung von Windows. Mit dem Windows ADK automatisiert Configuration Manager Aktionen wie z.B. das Installieren von Windows, das Erfassen von Images und das Migrieren von Benutzerprofilen und Daten.  

 Die folgenden Features des Windows ADK müssen auf dem Standortserver des obersten Standorts der Hierarchie, auf dem Standortserver jedes primären Standorts der Hierarchie und auf dem Standortsystemserver des SMS-Anbieters installiert sein:  

-   Migrationsprogramm für den Benutzerzustand (USMT) <sup>1</sup>  

-   Windows-Bereitstellungstools  

-   Windows-Vorinstallationsumgebung (Windows Preinstallation Environment, Windows PE)

Eine Liste der Versionen des Windows 10 ADK, die Sie mit verschiedenen Versionen von Configuration Manager verwenden können, finden Sie unter [Unterstützung für Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

 <sup>1</sup> USMT ist auf dem Standortsystemserver des SMS-Anbieters nicht erforderlich.  

> [!NOTE]  
>  Sie müssen das Windows ADK manuell auf allen Standortservern installieren, bevor Sie den Configuration Manager-Standort installieren.  

 Weitere Informationen finden Sie in folgenden Quellen:  

-   [Windows ADK für Windows 10-Szenarien für IT-Experten](/windows/deployment/windows-adk-scenarios-for-it-pros)  

-   [Windows ADK für Windows 10 herunterladen](/windows-hardware/get-started/adk-install)  

-   [Unterstützung für Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


### <a name="user-state-migration-tool-usmt"></a>Migrationsprogramm für den Benutzerzustand (USMT)  
 Configuration Manager verwendet ein USMT-Paket mit den USMT 10-Quelldateien, die zum Erfassen und Wiederherstellen des Benutzerzustands als Teil Ihrer Betriebssystembereitstellung verwendet werden. Das Configuration Manager-Setup erstellt am Standort der obersten Ebene das USMT-Paket automatisch. USMT 10 erfasst den Benutzerzustand von Windows 7, Windows 8, Windows 8.1 und Windows 10.  

 Weitere Informationen finden Sie in folgenden Quellen:  

-   [Allgemeine Migrationsszenarien für USMT 10](/windows/deployment/usmt/usmt-common-migration-scenarios)  

-   [Verwalten des Benutzerzustands](../get-started/manage-user-state.md)  

### <a name="windows-pe"></a>Windows PE  
 Windows PE wird für Startabbilder verwendet, um einen Computer zu starten. Es handelt sich um eine Windows-Version mit bestimmten Diensten, die vor der Installation und während der Bereitstellung von Windows verwendet wird. In der folgenden Liste sind die unterstützten Versionen des Windows ADK für Configuration Manager (Current Branch) aufgeführt:  

-   **Windows ADK-Version**  

     Windows ADK für Windows 10. Weitere Informationen finden Sie unter [Unterstützung für Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

-   **Windows PE-Versionen für Startimages, die über die Configuration Manager-Konsole angepasst werden können**  

     Windows PE 10  

-   **Unterstützte Windows PE-Versionen für Startimages, die nicht über die Configuration Manager-Konsole angepasst werden können**  

     Windows PE 3.1<sup>1</sup> und Windows PE 5  

     <sup>1</sup> Sie können zu Configuration Manager nur dann ein Startimage hinzufügen, wenn es auf Windows PE 3.1 basiert. Installieren Sie die Ergänzung zu Windows AIK für Windows 7 SP1, um ein Upgrade von Windows AIK für Windows 7 (basierend auf Windows PE 3) mit der Ergänzung zu Windows AIK für Windows 7 SP1 (basierend auf Windows PE 3.1) durchzuführen. Sie können die Ergänzung zu Windows AIK für Windows 7 SP1 aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188)herunterladen.  

     Im Fall von Configuration Manager etwa können Sie Startimages aus Windows ADK für Windows 10 (das auf Windows PE 10 basiert) über die Configuration Manager-Konsole anpassen. Zwar werden auf Windows PE 5 basierende Startabbilder unterstützt, doch müssen Sie sie von einem anderen Computer aus anpassen und die mit dem Windows ADK für Windows 8 installierte DISM-Version verwenden. Danach können Sie das Startimage der Configuration Manager-Konsole hinzufügen. Weitere Informationen und Vorgehensweisen zum Anpassen eines Startimages (Hinzufügen von optionalen Komponenten und Treibern), zum Aktivieren der Befehlsunterstützung für das Startimage, zum Hinzufügen des Startimages zur Configuration Manager-Konsole und zum Aktualisieren der Verteilungspunkte mit dem Startimage finden Sie unter[Anpassen von Startimages](../get-started/customize-boot-images.md). Weitere Informationen zu Startabbildern finden Sie im Thema [Verwalten von Startabbildern (Startimages)](../get-started/manage-boot-images.md).  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
 WSUS wird vom Softwareupdatepunkt benötigt, der zum Installieren von Softwareupdates bei der Betriebssystembereitstellung erforderlich ist. Weitere Informationen finden Sie unter [Installieren und Konfigurieren eines Softwareupdatepunkts](/sccm/sum/get-started/install-a-software-update-point).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>Internetinformationsdienste (IIS) auf den Standortsystemservern  
 IIS ist für den Verteilungspunkt, Zustandsmigrationspunkt und Verwaltungspunkt erforderlich. Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).  


### <a name="windows-deployment-services-wds"></a>Windows-Bereitstellungsdienste (Windows Deployment Services, WDS)  
 Für PXE-Bereitstellungen sowie bei Verwendung von Multicast zur Bandbreitenoptimierung in Ihren Bereitstellungen sind Windows-Bereitstellungsdienste (WDS) erforderlich. Weitere Informationen finden Sie unter [Windows-Bereitstellungsdienste](#BKMK_WDS) in diesem Artikel.  


### <a name="dynamic-host-configuration-protocol-dhcp"></a>Dynamic Host Configuration-Protokoll (DHCP)  
 DHCP ist für PXE-Bereitstellungen erforderlich. Sie müssen über einen betriebsbereiten DHCP-Server mit einem aktiven Host verfügen, um Betriebssysteme per PXE bereitstellen zu können. Weitere Informationen zu PXE-Bereitstellungen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Unterstützte Betriebssysteme und Festplattenkonfigurationen  
 Weitere Informationen zu den Betriebssystemversionen und Festplattenkonfigurationen, die Configuration Manager bei der Betriebssystembereitstellung unterstützt, finden Sie unter [Unterstützte Betriebssysteme](#BKMK_SupportedOS) und [Unterstützte Festplattenkonfigurationen](#BKMK_SupportedDiskConfig).  


### <a name="windows-device-drivers"></a>Windows-Gerätetreiber  
 Bei der Installation des Betriebssystems auf dem Zielcomputer können Windows-Gerätetreiber verwendet werden. Diese werden auch verwendet, wenn Sie Windows PE über ein Startimage ausführen. Weitere Informationen finden Sie unter [Verwalten von Treibern](../get-started/manage-drivers.md).  



##  <a name="BKMK_InternalDependencies"></a> Abhängigkeiten in Configuration Manager  
 Im folgenden Abschnitt finden Sie Informationen zu den Voraussetzungen für die Configuration Manager-Betriebssystembereitstellung.  


### <a name="os-image"></a>Betriebssystemimage  
 Betriebssystemimages in Configuration Manager werden im WIM-Dateiformat (Windows Imaging) gespeichert. Sie stellen eine komprimierte Sammlung von Verweisdateien und Ordnern dar. Diese Images sind für die erfolgreiche Installation und Konfiguration eines Betriebssystems auf einem Computer erforderlich. Weitere Informationen finden Sie unter [Manage operating system images (Verwalten von Betriebssystemimages)](../get-started/manage-operating-system-images.md).  


### <a name="driver-catalog"></a>Treiberkatalog  
 Zur Bereitstellung eines Gerätetreibers müssen Sie den Gerätetreiber importieren, aktivieren und auf einem Verteilungspunkt verfügbar machen, auf den der Configuration Manager-Client zugreifen kann. Weitere Informationen finden Sie unter [Verwalten von Treibern](../get-started/manage-drivers.md).  


### <a name="management-point"></a>Verwaltungspunkt  
 Daten zwischen Clients und dem Configuration Manager-Standort werden über Verwaltungspunkte übertragen. Der Client verwendet einen Verwaltungspunkt zum Ausführen der Tasksequenz, um die Bereitstellung des Betriebssystems abzuschließen. Weitere Informationen zu Tasksequenzen finden Sie unter [Planungsüberlegungen für das Automatisieren von Tasks](planning-considerations-for-automating-tasks.md).  


### <a name="distribution-point"></a>Verteilungspunkt  
 Verteilungspunkte werden in den meisten Bereitstellungen verwendet, um Daten für die Betriebssystembereitstellung wie das Image oder Treiberpakete zu speichern. In Tasksequenzen werden Daten normalerweise von einem Verteilungspunkt abgerufen, um das Betriebssystem bereitzustellen. Weitere Informationen zum Installieren von Verteilungspunkten und Verwalten von Inhalt finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="pxe-enabled-distribution-point"></a>PXE-fähiger Verteilungspunkt  
 Für PXE-initiierte Bereitstellungen müssen Sie einen Verteilungspunkt so konfigurieren, dass die von Clients gestellten PXE-Anforderungen vom Verteilungspunkt akzeptiert werden. Weitere Informationen finden Sie unter [Konfigurieren eines Verteilungspunkts](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).


### <a name="multicast-enabled-distribution-point"></a>Multicast-fähiger Verteilungspunkt  
 Wenn Sie Ihre Betriebssystembereitstellungen mithilfe von Multicast optimieren möchten, müssen Sie einen Verteilungspunkt für die Unterstützung von Multicast konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren eines Verteilungspunkts](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast).   


### <a name="state-migration-point"></a>Zustandsmigrationspunkt  
 Wenn Sie Benutzerzustandsdaten für parallele oder aktualisierte Bereitstellungen erfassen und wiederherstellen möchten, müssen Sie einen Zustandsmigrationspunkt zum Speichern der Benutzerzustandsdaten auf einem anderen Computer konfigurieren.  

 Weitere Informationen zum Konfigurieren des Zustandsmigrationspunkts finden Sie unter [Zustandsmigrationspunkt](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

 Informationen zum Erfassen und Wiederherstellen des Benutzerzustands finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  


### <a name="reporting-services-point"></a>Reporting Services-Punkt  
 Zur Verwendung von Configuration Manager-Berichten für Betriebssystembereitstellungen müssen Sie einen Reporting Services-Punkt installieren und konfigurieren. Weitere Informationen finden Sie unter [Berichterstattung](../../core/servers/manage/reporting.md).  


### <a name="security-permissions-for-os-deployments"></a>Sicherheitsberechtigungen für Betriebssystembereitstellungen  
 Die Sicherheitsrolle **Betriebssystembereitstellungs-Manager** ist eine integrierte Rolle und kann nicht geändert werden. Sie können jedoch eine Kopie dieser Sicherheitsrolle erstellen, ändern und als neue benutzerdefinierte Sicherheitsrolle speichern. Zu den Berechtigungen, die direkt auf Betriebssystembereitstellungen angewendet werden, gehören die folgenden:  

-   **Startabbildpaket**: Erstellen, Löschen, Ändern, Ordner ändern, Objekt verschieben, Lesen, Sicherheitsbereich festlegen  

-   **Gerätetreiber**: Erstellen, Löschen, Ändern, Ordner ändern, Bericht ändern, Objekt verschieben, Lesen, Bericht ausführen  

-   **Treiberpaket**: Erstellen, Löschen, Ändern, Ordner ändern, Objekt verschieben, Lesen, Sicherheitsbereich festlegen  

-   **Betriebssystemabbild**: Erstellen, Löschen, Ändern, Ordner ändern, Objekt verschieben, Lesen, Sicherheitsbereich festlegen  

-   **Installationspakete für Betriebssystem**: Erstellen, Löschen, Ändern, Ordner ändern, Objekt verschieben, Lesen, Sicherheitsbereich festlegen  

-   **Tasksequenzpaket**: Erstellen, Tasksequenzmedien erstellen, Löschen, Ändern, Ordner ändern, Bericht ändern, Objekt verschieben, Lesen, Bericht ausführen, Sicherheitsbereich festlegen  

 Weitere Informationen finden Sie unter [Erstellen benutzerdefinierter Sicherheitsrollen](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  


### <a name="security-scopes-for-os-deployments"></a>Sicherheitsbereiche für Betriebssystembereitstellungen  
 Verwenden Sie Sicherheitsbereiche, um Administratoren Zugriff auf in Betriebssystembereitstellungen verwendete sicherungsfähige Objekte wie Betriebssystemimages, Startimages, Treiberpakete und Tasksequenzpakete zu gewähren. Weitere Informationen finden Sie unter [Sicherheitsbereiche](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  



##  <a name="BKMK_WDS"></a> Windows-Bereitstellungsdienste  
 Die Windows-Bereitstellungsdienste (Windows Deployment Services, WDS) müssen auf dem gleichen Server installiert sein wie die Verteilungspunkte, die Sie für die Unterstützung von PXE oder Multicast konfigurieren. Der Windows-Bereitstellungsdienst ist im Betriebssystem des Servers enthalten. Bei PXE-Bereitstellungen wird der PXE-Start von den Windows-Bereitstellungsdiensten ausgeführt. Wenn der Verteilungspunkt installiert und PXE-fähig ist, erstellt Configuration Manager einen Anbieter in WDS, von dem die PXE-Startfunktionen der Windows-Bereitstellungsdienste verwendet werden.  

> [!NOTE]  
>  Wenn der Server einen Neustart fordert, kann die Installation der WDS fehlschlagen. 


### <a name="wds-requirements"></a>WDS-Anforderungen  

-   Zur Installation von WDS auf dem Server muss der Administrator Mitglied der lokalen Administratorgruppe sein.  

-   Der WDS-Server muss entweder Mitglied einer Active Directory-Domäne oder ein Domänencontroller für eine Active Directory-Domäne sein. Alle Windows-Domänen- und Gesamtstrukturkonfigurationen unterstützen WDS.  

-   Wenn der Anbieter auf einem Remoteserver installiert ist, müssen Sie WDS auf dem Standortserver und dem Remoteanbieter installieren.  


###  <a name="BKMK_WDSandDHCP"></a> Aspekte, wenn sich Windows-Bereitstellungsdienst und DHCP auf demselben Server befinden  
 Wenn Sie planen, einen PXE-Verteilungspunkt auf dem gleichen Server zu hosten, auf dem DHCP ausgeführt wird, sollten Sie die folgenden Konfigurationsoptionen in Erwägung ziehen.  

-   Sie benötigen einen funktionsfähigen DHCP-Server mit einem aktiven Bereich. WDS verwendet PXE, wofür ein DHCP-Server erforderlich ist.  

-   Sowohl für DHCP als auch für WDS muss die Portnummer 67 verwendet werden. Wenn Sie WDS und DHCP zusammen hosten, können Sie den DHCP-Server oder den für PXE konfigurierten Verteilungspunkt auf einen separaten Server verschieben. Alternativ können Sie mit den folgenden Schritten den WDS-Server so konfigurieren, dass dieser auf einem anderen Port lauscht.  

    #### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>So konfigurieren Sie den WDS-Server zum Lauschen auf einem anderen Port:  

    1.  Ändern Sie den folgenden Registrierungsschlüssel:  

         `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

    2.  Legen Sie den Registrierungswert **UseDHCPPorts** auf **0** fest.  

    3.  Damit die neue Konfiguration wirksam wird, führen Sie den folgenden Befehl auf dem Server aus:  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   Für das Ausführen von WDS wird ein DNS-Server benötigt.  

-   Folgende UDP-Ports müssen auf dem WDS-Server geöffnet sein:  

    -   Port 67 (DHCP)  

    -   Port 69 (TFTP)  

    -   Port 4011 (PXE)  

    > [!NOTE]  
    >  Falls eine DHCP-Autorisierung auf dem Server erforderlich ist, muss auf diesem der DHCP-Clientport 68 geöffnet sein.  



##  <a name="BKMK_SupportedOS"></a> Unterstützte Betriebssysteme  
 Alle Windows-Betriebssysteme, die unter [Unterstützte Betriebssysteme für Clients und Geräte](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) aufgeführt sind, werden für Betriebssystembereitstellungen unterstützt.  



##  <a name="BKMK_SupportedDiskConfig"></a> Unterstützte Festplattenkonfigurationen  
 In der folgenden Tabelle sind die für die Configuration Manager-Betriebssystembereitstellung unterstützten Kombinationen der Festplattenkonfiguration auf dem Referenz- und Zielcomputer aufgelistet:  

|Festplattenkonfiguration auf Referenzcomputer|Festplattenkonfiguration auf Zielcomputer|  
|------------------------------------------------|--------------------------------------------------|  
|Basisfestplatte|Basisfestplatte|  
|Einfaches Volume auf einer dynamischen Festplatte|Einfaches Volume auf einer dynamischen Festplatte|  

 Configuration Manager unterstützt das Erfassen eines Betriebssystemimages nur über Computer, die mit einfachen Volumes konfiguriert sind. Die folgenden Festplattenkonfigurationen werden nicht unterstützt:  

-   Übergreifende Volumes  

-   Stripesetvolumes (RAID 0)  

-   Gespiegelte Volumes (RAID 1)  

-   Paritätsvolumes (RAID 5)  

 Die zusätzliche, in der folgenden Tabelle angegebene Festplattenkonfiguration auf dem Referenz- und Zielcomputer wird in Configuration Manager bei der Betriebssystembereitstellung nicht unterstützt.  

|Festplattenkonfiguration auf Referenzcomputer|Festplattenkonfiguration auf Zielcomputer|  
|------------------------------------------------|--------------------------------------------------|  
|Basisfestplatte|Dynamische Festplatte|  



## <a name="next-steps"></a>Nächste Schritte
- [Vorbereiten von Standortsystemrollen für Betriebssystembereitstellungen](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments)
- [Prepare for OS deployment (Vorbereiten der Betriebssystembereitstellung)](../get-started/prepare-for-operating-system-deployment.md)
