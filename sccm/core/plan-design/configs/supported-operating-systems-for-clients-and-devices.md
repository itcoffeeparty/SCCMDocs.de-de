---
title: "Unterstützte Clients und Geräte | Microsoft-Dokumentation"
description: "Erfahren Sie, welche Betriebssysteme System Center Configuration Manager für Clients und Geräte unterstützt."
ms.custom: na
ms.date: 8/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
caps.latest.revision: "5"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 82be9b005ec87199f3191612f720f4cc267a4e5c
ms.sourcegitcommit: db7b7ec347638efd05cdba474e8a8f8535516116
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2017
---
# <a name="supported-operating-systems-for-clients-and-devices-for-system-center-configuration-manager"></a>Unterstützte Betriebssysteme für Clients und Geräte für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 System Center Configuration Manager unterstützt die Installation von Clientsoftware auf einer Vielzahl von Windows-, Macintosh-, Linux- und UNIX-Computern.  

 **Anforderungen und Einschränkungen für alle Clients:**  

-   Die Änderung der Einstellungen für den Starttyp und **Anmelden als** für beliebige Configuration Manager-Dienste wird nicht unterstützt. Wenn Sie die Einstellungen trotzdem ändern, werden wichtige Dienste möglicherweise nicht ordnungsgemäß ausgeführt.    

-   Die Installation oder Ausführung des Configuration Manager-Clients für Linux oder UNIX bzw. des Macintosh-Clients auf Computern unter einem anderen Konto als Root wird nicht unterstützt. Wenn Sie die Einstellungen trotzdem ändern, werden wichtige Dienste möglicherweise nicht ordnungsgemäß ausgeführt.  

##  <a name="windows-computers"></a>Windows-Computer  
 Die folgenden Windows-Computerbetriebssysteme können mit dem im Configuration Manager enthaltenen Configuration Manager-Client verwaltet werden. Weitere Informationen finden Sie unter [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

**Unterstützte Betriebssysteme:**  


-  **Windows Server 2016**: Standard, Datacenter <sup>1</sup>
  - Dieses Betriebssystem wird ab Configuration Manager Version 1606 mit dem Hotfixrollup von KB3186654 (oder der Baselineversion 1606, die im Oktober 2016 veröffentlicht wurde) unterstützt.  

-   **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64): Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **Windows Server 2008 R2 mit SP1** (x64): Standard, Enterprise, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2008 R2** (x86, x64): Workgroup, Standard, Enterprise    

-   **Windows  Server 2008 mit SP2** (x86, x64): Standard, Enterprise, Datacenter <sup>1</sup>    

-   **Windows 10**: Pro, Enterprise  
   Unter [Support für Versionen von Windows 10](/sccm/core/plan-design/configs/support-for-windows-10) finden Sie ausführliche Informationen zu den verschiedenen Versionen von Windows 10, die von den verschiedenen Versionen von Configuration Manager unterstützt werden.

-   **Windows 8.1** (x86, x64): Professional, Enterprise    

-   **Windows 8** (x86, x64): Professional, Enterprise    

-   **Windows 7 mit SP1** (x86, x64): Professional, Enterprise und Ultimate    

-   **Server Core-Installation von Windows Server 2016** (x64) <sup>2</sup>
  - Dieses Betriebssystem wird ab Version 1606 mit dem Hotfixrollup von KB3186654 (oder Baselineversion 1606, die im Oktober 2016 veröffentlicht wurde) unterstützt.


-   **The Server Core-Installation von Windows Server 2012 R2** (x64) <sup>2</sup>    

-   **Server Core-Installation von Windows Server 2012** (x64) <sup>2</sup>    

-   **Server Core-Installation von Windows Server 2008 R2**  
    **(ohne Service Pack oder mit SP1)** (x64)    

-   **Server Core-Installation von Windows Server 2008 SP2** (x86, x64)  

 <sup>1</sup> Datacenter-Releases werden von Configuration Manager zwar unterstützt, sind jedoch nicht dafür zertifiziert. Es wird keine Hotfixunterstützung für Probleme bereitgestellt, die ausschließlich Windows Server Datacenter Edition betreffen.  

 <sup>2</sup> Zur Unterstützung der Clientpushinstallation muss auf dem Computer, auf dem diese Betriebssystemversion ausgeführt wird, der Dateiserver-Rollendienst für die Serverrolle „Datei- und Speicherdienste“ ausgeführt werden. Informationen zum Installieren von Windows-Features auf einem Server Core-Computer finden Sie unter [Installieren von Serverrollen und -features auf einem Server Core-Server](http://go.microsoft.com/fwlink/p/?LinkId=299359) in der TechNet-Bibliothek für Windows Server 2012.  


##  <a name="windows-embedded-computers"></a>Windows Embedded-Computer  
 Sie können die Windows Embedded-Geräte durch die Installation von Configuration Manager-Clientsoftware auf dem Gerät verwalten.  Weitere Informationen finden Sie unter [Planen der Clientbereitstellung auf Windows Embedded-Geräten in System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

**Anforderungen und Einschränkungen:**  

-   Alle Clientfeatures werden auf Windows Embedded-Systemen ohne aktivierte Schreibfilter unterstützt.  

-   Clients, die einen der folgenden Filter verwenden, werden für alle Features (ausgenommen Energieverwaltung) unterstützt:  

    -   Erweiterte Schreibfilter (Enhanced Write Filters, EWF)    

    -   RAM-dateibasierte Schreibfilter (File Based Write Filters, FBWF)    

    -   Vereinheitlichte Schreibfilter (Unified Write Filters, UWF)  

-   Der Anwendungskatalog wird für Windows Embedded-Geräte grundsätzlich nicht unterstützt.  

-   Bevor Sie erkannte Schadsoftware auf Windows XP-basierten Windows Embedded-Geräten überwachen können, müssen Sie das Microsoft Windows-WMI-Skriptpaket auf dem Gerät installieren. Verwenden Sie Windows Embedded Target Designer zur Installation dieses Pakets.
Die Dateien **WBEMDISP.DLL** und **WBEMDISP.TLB** müssen vorhanden und im Ordner **%windir%\System32\WBEM** auf dem Embedded-Gerät registriert sein, um sicherzustellen, dass die erkannte Schadsoftware gemeldet wird.  

**Unterstützte Betriebssysteme:**  

-   **Windows 10 Enterprise** (x86, x64)  

-   **Windows 10 IoT Enterprise** (x86, x64)  

-   **Windows Embedded 8.1 Industry** (x86, x64)    

-   **Windows Embedded 8 Industry** (x86, x64)    

-   **Windows Embedded 8 Standard** (x86, x64)    

-   **Windows Embedded 8 Pro** (x86, x64)    

-   **Windows Thin PC** (x86, x64)    

-   **Windows Embedded POSReady 7** (x86, x64)    

-   **Windows Embedded Standard 7 mit SP1** (x86, x64)    

Die folgenden Betriebssysteme basieren auf Windows XP Embedded und werden nur mit Configuration Manager Version 1610 und früher unterstützt. [Ab Version 1702 werden diese eingebetteten Betriebssysteme nicht mehr unterstützt](/sccm/core/plan-design/changes/removed-and-deprecated-features#client-operating-systems).  

-   **WEPOS 1.1 mit SP3** (x86)    

-   **Windows Embedded POSReady 2009** (x86)    

-   **Windows Fundamentals für ältere PCs (WinFLP)** (x86)    

-   **Windows XP Embedded SP3** (x86)    

-   **Windows Embedded Standard 2009** (x86)  

## <a name="windows-ce-computers"></a>Windows CE-Computer
 Sie können Windows CE-Geräte mit dem Configuration Manager-Legacyclient für mobile Geräte verwalten, der im Configuration Manager enthalten ist.  

**Anforderungen und Einschränkungen:**  

-   Zur Installation des Clients für mobile Geräte sind 0,78 MB Speicherplatz erforderlich. Die Anmeldung auf dem mobilen Gerät kann bis zu 256 KB zusätzlichen Speicherplatz erfordern.    

-   Die für diese mobilen Geräte verfügbaren Funktionen sind von Plattform und Clienttyp abhängig. Informationen dazu, welche Verwaltungsfunktionen unterstützt werden, finden Sie unter [Wählen einer Geräteverwaltungslösung für System Center Configuration Manager](../../../core/plan-design/choose-a-device-management-solution.md).  

**Unterstützte Betriebssysteme:**  

-   Windows CE 7.0 (ARM- und x86-Prozessoren)  

**Zu den unterstützten Sprachen zählen:**  

-   Chinesisch (vereinfacht und traditionell)    

-   Englisch (USA)    

-   Französisch (Frankreich)    

-   Deutsch    

-   Italienisch    

-   Japanisch  

-   Koreanisch  

-   Portugiesisch (Brasilien)  

-   Russisch  

-   Spanisch (Spanien)  

## <a name="mac-computers"></a>Macintosh-Computer  
 Sie können Macintosh OS X-Computer mit dem Configuration Manager-Client für Macintosh verwalten.  

 Das Macintosh-Clientinstallationspaket wird nicht mit den Configuration Manager-Medien geliefert. Laden Sie die **Clients für weitere Betriebssysteme** aus dem [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184) herunter.  

 Weitere Informationen finden Sie unter [How to deploy clients to Macs in System Center Configuration Manager (Bereitstellen von Clients auf Macs in System Center Configuration Manager)](../../../core/clients/deploy/deploy-clients-to-macs.md).  

**Unterstützte Versionen:**  

-   **Mac OS X 10.6** (Snow Leopard)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)

##  <a name="linux-and-unix-servers"></a>Linux- und UNIX-Server  
 Sie können Linux- und UNIX-Server mit dem Configuration Manager-Client für Linux und UNIX verwalten.  

 Die Clientinstallationspakete für Linux und UNIX werden nicht mit den Configuration Manager-Medien geliefert. Laden Sie die **Clients für weitere Betriebssysteme** aus dem [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184) herunter. Zusätzlich zu den Clientinstallationspaketen umfasst der Clientdownload das Skript zur Verwaltung der Clientinstallation auf den einzelnen Computern.  

**Anforderungen und Einschränkungen:**  

-   Informationen zum Überprüfen von Betriebssystemdateiabhängigkeiten für den Client für Linux und UNIX finden Sie unter [Prerequisites for Client Deployment to Linux and UNIX Servers (Voraussetzungen für die Clientbereitstellung auf Linux- und UNIX-Servern)](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  

-   Eine Übersicht über die Verwaltungsfunktionen, die für Computer unterstützt werden, auf denen Linux oder UNIX ausgeführt wird, finden Sie unter [Bereitstellen von Clients auf UNIX- und Linux-Servern in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

-   Für unterstützte Versionen von Linux- und UNIX-Clients schließt die aufgeführte Version alle nachfolgenden Nebenversionen ein. Beispielsweise enthält die CentOS-Version 6 CentOS 6.3. Ebenso schließt die Unterstützung für ein Betriebssystem, das Service Packs verwendet (z.B. SUSE Linux Enterprise Server 11 SP1), die Unterstützung für alle nachfolgenden Service Packs für diese Betriebssystemversion ein.  

-   Informationen zu Clientinstallationspaketen und dem Universal Agent finden Sie unter [Bereitstellen von Clients auf UNIX- und Linux-Servern in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

**Unterstützte Versionen**: Die folgenden Versionen werden mit der angegebenen TAR-Datei unterstützt.  

### <a name="aix"></a>AIX  

|||  
|-|-|  
|Version 5.3 (Power)|ccm-Aix53ppc.&lt;build\>.tar|  
|Version 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Version 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

### <a name="centos"></a>CentOS  

|||  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="debian"></a>Debian  

|||  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 8 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|||  
|-|-|  
|Version 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;build\>.tar|  
|Version 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;build\>.tar|  
|Version 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  
|Version 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;build\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|||  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|||  
|-|-|  
|Version 4 x86|ccm-RHEL4x86.&lt;build\>.tar|  
|Version 4 x64|ccm-RHEL4x64.&lt;build\>.tar|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="solaris"></a>Solaris  

|||  
|-|-|  
|Version 9 SPARC|ccm-Sol9sparc.&lt;build\>.tar|  
|Version 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Version 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Version 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Version 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|||  
|-|-|  
|Version 9 x86|ccm-SLES9x86.&lt;build\>.tar|  
|Version 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 12 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|||  
|-|-|  
|Version 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  

##  <a name="mobile-devices-enrolled-by-microsoft-intune"></a>Durch Microsoft Intune registrierte mobile Geräte  
 Ausführliche Informationen über die Computer und Geräte, die Sie verwalten können, wenn Sie Microsoft Intune in Configuration Manager integrieren, finden Sie unter den folgenden beiden Themen in der Microsoft Intune-Dokumentationsbibliothek:  

-   [Verwaltungsfunktionen für mobile Geräte in Microsoft Intune](https://docs.microsoft.com/intune/get-started/choose-how-to-manage-devices)  
-   [Funktionen für die Windows-PC-Verwaltung in Microsoft Intune](https://docs.microsoft.com/intune/get-started/windows-pc-management-capabilities-in-microsoft-intune)  

##  <a name="bkmk_OnpremOS"></a> Lokale Verwaltung mobiler Geräte  
 Configuration Manager verfügt über integrierte Funktionen zum Verwalten von lokalen Geräten ohne Installation der Clientsoftware.  Weitere Informationen finden Sie unter [Verwalten mobiler Geräte mithilfe lokaler Infrastruktur in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Anforderungen und Einschränkungen:**  

-   Sie müssen den **Dienstverbindungspunkt** am Standort auf der obersten Ebene Ihrer Hierarchie konfigurieren.  

**Unterstützte Betriebssysteme:**  

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

- **Windows 10 IoT Mobile Enterprise**

- **Windows 10 Team für Surface Hub**

##  <a name="bkmk_ExSrvConOS"></a> Exchange Server-Connector  
Configuration Manager unterstützt mit Einschränkungen die Verwaltung der Geräte, die Sie mit Ihrem Exchange-Server verbinden, ohne den Configuration Manager-Client zu installieren. Weitere Informationen finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Microsoft Intune](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

 **Anforderungen und Einschränkungen:**  

-   Configuration Manager bietet eingeschränkte Verwaltungsfunktionen für mobile Geräte, wenn Sie Geräte mit dem Exchange Server-Connector für Exchange Active Sync verwenden, die mit einem Server kommunizieren, auf dem Exchange Server oder Exchange Online ausgeführt wird.  

-   Weitere Informationen dazu, welche Verwaltungsfunktionen von Configuration Manager für mobile Geräte unterstützt werden, die vom Exchange Server-Connector verwaltet werden, finden Sie unter „Bestimmen, wie mobile Geräte in Configuration Manager verwaltet werden“.  

**Unterstützte Versionen von Exchange Server:**  

-   **Exchange Server 2010 SP1**  

-   **Exchange Server 2010 SP2**  

-   **Exchange Server 2013**  

-   **Exchange Online (Office 365)**: Dies beinhaltet die Business Productivity Online Standard Suite  
