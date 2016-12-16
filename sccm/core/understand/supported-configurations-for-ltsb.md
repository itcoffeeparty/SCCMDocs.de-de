---
title: "Unterstützte Konfigurationen für LTSB | System Center Configuration Manager"
description: "Hier finden Sie Informationen dazu, welche Betriebssysteme und abhängigen Produkte mit LTSB (Long-Term Servicing Branch) von System Center Configuration Manager verwendet werden."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 275d94b0596f04d2339ffb7aa315b4afdd237678
ms.openlocfilehash: 25dbdd401d0f6e955e5dcc704a0c756c74c64773


---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Unterstützte Konfigurationen für LTSB (Long-Term Servicing Branch) von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Long-Term Servicing Branch)*

Dieses Thema enthält Informationen dazu, welche Betriebssysteme und Produktabhängigkeiten von LTSB (Long-Term Servicing Branch) von Configuration Manager unterstützt werden.
Wenn in diesem oder in anderen Themen zum LTSB nicht anders angegeben, gelten die Konfigurationen und Einschränkungen für die Current Branch-Version 1606 auch für den LTSB.  Wenn Konflikte auftreten, verwenden Sie die Informationen zur jeweils verwendeten Edition. In der Regel gelten für den LTSB dieselben Einschränkungen wie für Current Branch.

## <a name="general-statement-of-support"></a>Allgemeine Unterstützungserklärung
Die in den folgenden Abschnitten beschriebenen Produkte und Technologien werden von Configuration Manager unterstützt. Die Tatsache, dass diese Produkte und Technologien hier beschrieben werden, bedeutet jedoch nicht, dass damit der Support über den Support Lifecycle der jeweiligen Produkte hinaus erweitert wurde. Produkte, deren Support Lifecycle überschritten ist, werden nicht für die Verwendung mit Configuration Manager unterstützt. Weitere Informationen finden Sie auf der Website [Microsoft Lifecycle-Richtlinie](http://go.microsoft.com/fwlink/p/?LinkId=208270) und unter [Support Lifecycle-Richtlinie – FAQ](http://go.microsoft.com/fwlink/p/?LinkId=31976).

Darüber hinaus werden auch Produkte und Produktversionen, die in den folgenden Themen nicht aufgeführt sind, nur dann unterstützt, wenn sie im [Enterprise Mobility + Security-Blog](https://blogs.technet.microsoft.com/enterprisemobility/) angekündigt wurden.

**Einschränkungen für zukünftigen Support:** Der LTSB bietet für zukünftige Server- und Clientbetriebssysteme sowie Produktabhängigkeiten nur eingeschränkten Support. Die Liste der Plattformen für den LTSB ist für die Lebensdauer des Releases festgeschrieben:

**Windows:**
- Nur Qualitäts- und Sicherheitsupdates für Windows werden unterstützt.
- Current Branches (CB), Current Branches for Business (CBB) oder LTSB von Windows 10 werden nicht unterstützt.
-   Neue Hauptversionen von Windows Server werden nicht unterstützt.

**SQL Server:**
- Nur Qualitäts- und Sicherheitsupdates bzw. kleinere Updates für SQL Server wie Service Packs werden unterstützt.
- Neue Hauptversionen von SQL Server werden nicht unterstützt.  

## <a name="site-systems-and-servers"></a>Standortsysteme und Server
Der LTSB bietet Unterstützung unter Verwendung der folgenden Windows-Computerbetriebssysteme als Standortsysteme.  Für jedes Betriebssystem gelten dieselben Anforderungen und Einschränkungen wie im entsprechenden Eintrag unter [Unterstützte Betriebssysteme für Standortsystemserver](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers) beschrieben.  So muss es sich bei der Server Core-Installation von Windows 2012 R2 beispielsweise um eine x64-Version handeln. Zudem wird für diese Installation nur das Hosten eines Verteilungspunkts unterstützt. PXE bzw. Multicast wird nicht unterstützt.

**Unterstützte Betriebssysteme:**
- **Windows Server 2016**
- **Windows Server 2012** (x64) – Standard, Datacenter
- **Windows Server 2008 R2 mit SP1** (x64) – Standard, Enterprise, Datacenter
- **Windows Server 2008 mit SP2** (x86, x64) – Standard, Enterprise, Datacenter
- **Windows 10 Enterprise 2015 LTSB** (x86, x64)
- **Windows 10 Enterprise 2016 LTSB** (x86, x64)
- **Windows 8.1** (x86, x64) – Professional, Enterprise
- **Windows 7 mit SP1** (x86, x64) – Professional, Enterprise, Ultimate
- **Die Server Core-Installation von Windows Server 2012**
- **Die Server Core-Installation von Windows Server 2012 R2**  

## <a name="client-management"></a>Clientverwaltung
In den folgenden Abschnitten sind die Clientbetriebssysteme aufgeführt, die mit LTSB verwaltet werden können. Vom LTSB werden neue, als unterstützte Clients hinzugefügte Betriebssysteme nicht unterstützt.

### <a name="windows-computers"></a>Windows-Computer
Die folgenden Windows-Computerbetriebssysteme können vom LTSB mit der in Configuration Manager enthaltenen Configuration Manager-Clientsoftware verwaltet werden. Weitere Informationen finden Sie unter [How to deploy clients to Windows computers in System Center Configuration Manager (Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager)](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

**Unterstützte Betriebssysteme:**
- **Windows Server 2016**
- **Windows Server 2012 R2** (x64) – Standard, Datacenter (Hinweis 1)
- **Windows Server 2012** (x64) – Standard, Datacenter (Note 1)
- **Windows Storage Server 2012 R2** (x64)
- **Windows Storage Server 2012** (x64)
- **Windows Server 2008 R2 with SP1** (x64) – Standard, Enterprise, Datacenter (Hinweis 1)
- **Windows Storage Server 2008 R2** (x86, x64) – Workgroup, Standard, Enterprise
- **Windows Server 2008 with SP2** (x86, x64) – Standard, Enterprise, Datacenter (Hinweis 1)
- **Windows 10 Enterprise 2015 LTSB** (x86, x64)
- **Windows 10 Enterprise 2016 LTSB** (x86, x64)
- **Windows 8.1** (x86, x64) – Professional, Enterprise
- **Windows 7 mit SP1** (x86, x64) – Professional, Enterprise, Ultimate
- **Die Server Core-Installation von Windows Server 2012 R2** (x64) (Hinweis 2)
- **Die Server Core-Installation von Windows Server 2012** (x64) (Hinweis 2)
- **Die Server Core-Installation von Windows Server 2008 R2 SP1** (x64)
- **Die Server Core-Installation von Windows Server 2008 SP2** (x86, x64)

**(Hinweis 1)** Datacenter-Releases werden von Configuration Manager zwar unterstützt, sind jedoch nicht dafür zertifiziert.  
**(Hinweis 2)** Zur Unterstützung der Clientpushinstallation muss auf dem Computer, auf dem diese Betriebssystemversion ausgeführt wird, der Dateiserver-Rollendienst für die Serverrolle „Datei- und Speicherdienste“ ausgeführt werden. Informationen zum Installieren von Windows-Features auf einem Server Core-Computer finden Sie unter „Install Server Roles and Features on a Server Core Server (Installieren von Serverrollen und -features auf einem Server Core-Server)“ in der TechNet-Bibliothek für Windows Server 2012.

### <a name="windows-embedded"></a>Windows Embedded:
Sie können den LTSB zum Verwalten der folgenden Windows Embedded-Geräte verwenden, indem Sie die Clientsoftware auf dem Gerät installieren.  Weitere Informationen finden Sie unter [Planning for client deployment to Windows Embedded devices in System Center Configuration Manager (Planen der Clientbereitstellung auf Windows Embedded-Geräten in System Center Configuration Manager)](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices).

**Anforderungen und Einschränkungen:**  

-   Alle Clientfeatures werden auf unterstützten Windows Embedded-Systemen ohne aktivierte Schreibfilter unterstützt.  

-   Clients, die einen der folgenden Filter verwenden, werden für alle Features (ausgenommen Energieverwaltung) unterstützt:  

    -   Erweiterte Schreibfilter (Enhanced Write Filters, EWF)    

    -   RAM-dateibasierte Schreibfilter (File Based Write Filters, FBWF)    

    -   Vereinheitlichte Schreibfilter (Unified Write Filters, UWF)  

-   Der Anwendungskatalog wird für Windows Embedded-Geräte grundsätzlich nicht unterstützt.  

-   Bevor Sie erkannte Schadsoftware auf Windows XP-basierten Windows Embedded-Geräten überwachen können, müssen Sie das Microsoft Windows-WMI-Skriptpaket auf dem eingebetteten Gerät installieren. Verwenden Sie Windows Embedded Target Designer zur Installation dieses Pakets. Die Dateien **WBEMDISP.DLL** und **WBEMDISP.TLB** müssen vorhanden und im Ordner **%windir%\System32\WBEM** auf dem Embedded-Gerät registriert sein, um sicherzustellen, dass die erkannte Schadsoftware gemeldet wird.  

**Unterstützte Betriebssysteme:**  
-   **Windows 10 Enterprise 2016 LTSB** (x86, x64)  
-   **Windows 10 Enterprise 2015 LTSB** (x86, x64)  
-   **Windows Embedded 8.1 Industry** (x86, x64)    
-   **Windows Thin PC** (x86, x64)    
-   **Windows Embedded POSReady 7** (x86, x64)    
-   **Windows Embedded Standard 7 mit SP1** (x86, x64)    
-   **Windows Embedded POSReady 2009** (x86)   
-   **Windows Embedded Standard 2009** (x86)  

### <a name="windows-ce"></a>Windows CE  
 Sie können Windows CE-Geräte mit dem Configuration Manager-Legacyclient für mobile Geräte verwalten, der im Configuration Manager enthalten ist.  

**Anforderungen und Einschränkungen:**  

-   Zur Installation des Clients für mobile Geräte sind 0,78 MB Speicherplatz erforderlich. Die Protokollierung auf dem mobilen Gerät kann bis zu 256 KB zusätzlichen Speicherplatz erfordern.    

-   Die für diese mobilen Geräte verfügbaren Funktionen sind von Plattform und Clienttyp abhängig. Informationen dazu, welche Verwaltungsfunktionen Configuration Manager für den Legacyclient für mobile Geräte unterstützt, finden Sie unter [Choose a device management solution for System Center Configuration Manager (Wählen einer Geräteverwaltungslösung für System Center Configuration Manager)](/sccm/core/plan-design/choose-a-device-management-solution).  

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

### <a name="mac-computers"></a>Macintosh-Computer  
 Sie können den LTSB verwenden, um Mac OS X-Computer mit dem Configuration Manager-Client für Macintosh zu verwalten.

Das Macintosh-Clientinstallationspaket wird nicht mit den Configuration Manager-Medien geliefert. Sie können es als Teil des Clients für zusätzliche Betriebssysteme im [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184) herunterladen.  

Bei den Mac-Betriebssystemen werden nur die in diesem Abschnitt aufgeführten Betriebssysteme unterstützt. Andere Betriebssysteme, die möglicherweise von einem zukünftigen Update für Mac-Clientinstallationspakete für den Current Branch unterstützt werden, werden nicht unterstützt.

Weitere Informationen finden Sie unter [How to deploy clients to Macs in System Center Configuration Manager (Bereitstellen von Clients auf Macs in System Center Configuration Manager)](/sccm/core/clients/deploy/deploy-clients-to-macs).

**Unterstützte Versionen:**  
-   **Mac OS X 10.9** (Mavericks)  
-   **Mac OS X 10.10** (Yosemite)  
-   **Mac OS X 10.11** (El Capitan)  

## <a name="linux-and-unix-servers"></a>Linux- und UNIX-Server
Sie können LTSB verwenden, um Linux- und UNIX-Server mit dem Configuration Manager-Client für Linux und UNIX zu verwalten.

Die Clientinstallationspakete für Linux und UNIX werden nicht mit den Configuration Manager-Medien geliefert. Sie können sie als Teil des Clients für weitere Betriebssysteme im [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184) herunterladen. Zusätzlich zu den Clientinstallationspaketen umfasst der Clientdownload das Installationsskript zur Verwaltung der Clientinstallation auf den einzelnen Computern.

Bei den Linux- und UNIX-Betriebssystemen werden nur die in diesem Abschnitt aufgeführten Betriebssysteme unterstützt. Andere Betriebssysteme, die möglicherweise von einem zukünftigen Update für Linux- und UNIX-Pakete für den Current Branch unterstützt werden, werden nicht unterstützt.

**Anforderungen und Einschränkungen:**  

-   Informationen zum Überprüfen von Betriebssystemdateiabhängigkeiten für den Client für Linux und UNIX finden Sie unter [Prerequisites for Client Deployment to Linux and UNIX Servers (Voraussetzungen für die Clientbereitstellung auf Linux- und UNIX-Servern)](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#bkmk_clientdeployprereqforlnu).  
-   Eine Übersicht über die Verwaltungsfunktionen, die für Computer unterstützt werden, auf denen Linux oder UNIX ausgeführt wird, finden Sie unter [How to deploy clients to UNIX and Linux servers in System Center Configuration Manager (Bereitstellen von Clients auf UNIX- und Linux-Servern in System Center Configuration Manager)](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  
-   Für unterstützte Versionen von Linux- und UNIX-Clients schließt die aufgeführte Version alle nachfolgenden Nebenversionen ein. Wenn beispielsweise Unterstützung für CentOS Version 6 angegeben ist, schließt dies alle nachfolgenden Nebenversionen von CentOS 6 ein, z. B. CentOS 6.3. Wenn die Unterstützung für ein Betriebssystem angegeben ist, das Service Packs verwendet (z. B. SUSE Linux Enterprise Server 11 SP1), schließt die Unterstützung entsprechend alle nachfolgenden Service Packs für diese Betriebssystemversion ein.
-   Informationen zu Clientinstallationspaketen und zum universellen Agent finden Sie unter [How to deploy clients to UNIX and Linux servers in System Center Configuration Manager (Bereitstellen von Clients auf UNIX- und Linux-Servern in System Center Configuration Manager)](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).


**Unterstützte Versionen:**   
Die folgenden Versionen werden mit der angegebenen TAR-Datei unterstützt.  
### <a name="aix"></a>AIX  

|Version|Datei|  
|-|-|  
|Version 5.3 (Power)|ccm-Aix53ppc.&lt;build\>.tar|  
|Version 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Version 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

### <a name="centos"></a>CentOS  

|Version|Datei|  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="debian"></a>Debian  

|Version|Datei|    
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

|Version|Datei|  
|-|-|  
|Version 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;build\>.tar|  
|Version 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;build\>.tar|  
|Version 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  
|Version 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;build\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|Version|Datei|    
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Version|Datei|  
|-|-|  
|Version 4 x86|ccm-RHEL4x86.&lt;build\>.tar|  
|Version 4 x64|ccm-RHEL4x64.&lt;build\>.tar|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="solaris"></a>Solaris  

|Version|Datei|   
|-|-|  
|Version 9 SPARC|ccm-Sol9sparc.&lt;build\>.tar|  
|Version 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Version 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Version 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Version 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Version|Datei|  
|-|-|  
|Version 9 x86|ccm-SLES9x86.&lt;build\>.tar|  
|Version 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 12 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|Version|Datei|    
|-|-|  
|Version 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="exchange-server-connector"></a>Exchange Server-Connector
 Vom LTSB wird die Verwaltung der Geräte, die Sie mit Ihrem Exchange-Server verbinden, ohne die Clientsoftware zu installieren, mit Einschränkungen unterstützt. Weitere Informationen finden Sie unter [Manage mobile devices with System Center Configuration Manager and Exchange (Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange)](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).

 **Anforderungen und Einschränkungen:**  

-   Configuration Manager bietet eingeschränkte Verwaltungsfunktionen für mobile Geräte, wenn Sie den Exchange Server-Connector für EAS-fähige (Exchange Active Sync) Geräte verwenden, die mit einem Server kommunizieren, auf dem Exchange Server oder Exchange Online ausgeführt wird.  

-   Weitere Informationen dazu, welche Verwaltungsfunktionen von Configuration Manager für mobile Geräte unterstützt, die vom Exchange Server-Connector verwaltet werden, finden Sie unter [Choose a device management solution for System Center Configuration Manager (Wählen einer Geräteverwaltungslösung für System Center Configuration Manager)](/sccm/core/plan-design/choose-a-device-management-solution).  

**Unterstützte Versionen von Exchange Server:**  
-   **Exchange Server 2010 SP1**  
-   **Exchange Server 2010 SP2**  
-   **Exchange Server 2013**  

> [!NOTE]
> Der LTSB bietet keine Unterstützung für die Verwaltung von Geräten, die über einen Onlinedienst wie Exchange Online (Office 365) eine Verbindung herstellen.


## <a name="configuration-manager-console"></a>Configuration Manager-Konsole
Vom LTSB wird die Ausführung der Configuration Manager-Konsole unter den folgenden Betriebssystemen unterstützt. Auf einem Computer, auf dem die Konsole gehostet wird, muss mindestens .NET Framework Version 4.5.2 installiert sein, für Windows 10 mindestens .NET Framework 4.6.

**Unterstützte Betriebssysteme:**
- **Windows Server 2016**
- **Windows Server 2012 R2** (x64) – Standard, Datacenter
- **Windows Server 2012** (x64) – Standard, Datacenter
- **Windows Server 2008 R2 mit SP1** (x64) – Standard, Enterprise, Datacenter
- **Windows Server 2008 mit SP2** (x86, x64) – Standard, Enterprise, Datacenter
- **Windows 10 Enterprise 2016 LTSB** (x86, x64)
- **Windows 10 Enterprise 2015 LTSB** (x86, x64)
- **Windows 8.1** (x86, x64) – Professional, Enterprise Windows 7 mit SP1** (x86, x64) – Professional, Enterprise, Ultimate

## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>Für die Standortdatenbank und den Berichterstattungspunkt unterstützte SQL Server-Versionen
Vom LTSB wird das Hosten der Standortdatenbank und des Berichterstattungspunkts durch die folgenden Versionen von SQL Server unterstützt. Für die unterstützten Versionen gelten für den LTSB die Konfigurationsanforderungen und -einschränkungen, die unter [Unterstützung für SQL Server-Versionen](/sccm/core/plan-design/configs/support-for-sql-server-versions) für Current Branch beschrieben werden.  Dies schließt die Verwendung eines SQL Server-Clusters oder einer SQL Server-Always On-Verfügbarkeitsgruppe ein.  

**Unterstützte Versionen:**

- **SQL Server 2016** – Standard, Enterprise
- **SQL Server 2014 SP2** – Standard, Enterprise
- **SQL Server 2014 SP1** – Standard, Enterprise
- **SQL Server 2012 SP3** – Standard, Enterprise
- **SQL Server 2012 SP2** – Standard, Enterprise
- **SQL Server 2008 R2 SP3** – Standard, Enterprise, Datacenter
- **SQL Server 2016 Express**
- **SQL Server 2014 Express SP2**
- **SQL Server 2014 Express SP1**
- **SQL Server 2012 Express SP3**
- **SQL Server 2012 Express SP2**

## <a name="support-for-active-directory-domains"></a>Unterstützung für Active Directory-Domänen
Alle LTSB-Standortsysteme müssen Mitglieder einer unterstützten Windows Active Directory-Domäne sein. Für die Unterstützung von Active Directory-Domänen gelten die Anforderungen und Einschränkungen, die unter [Unterstützung für Active Directory-Domänen](/sccm/core/plan-design/configs/support-for-active-directory-domains) aufgeführt sind. Die Unterstützung ist jedoch auf die folgenden Domänenfunktionsebenen beschränkt:

**Unterstützte Ebenen:**
- **Windows Server 2008**
- **Windows Server 2008 R2**
- **Windows Server 2012**
- **Windows Server 2012 R2**

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Weitere Themen zur Unterstützung, die für Long-Term Servicing Branch gelten
Die Informationen in den folgenden Current Branch-Themen gelten für den LTSB:
- [Size and scale numbers (Anpassen und Skalieren von Zahlen)](/sccm/core/plan-design/configs/size-and-scale-numbers)
- [Voraussetzungen für Standorte und Standortsysteme](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
- [High availability options (Optionen für hohe Verfügbarkeit)](/sccm/protect/understand/high-availability-options)
- [Empfohlene Hardware](/sccm/core/plan-design/configs/recommended-hardware)
- [Unterstützung für Windows-Features und -Netzwerke](/sccm/core/plan-design/configs/support-for-windows-features-and-networks)
- [Support for Virtualization Environments (Unterstützung für Virtualisierungsumgebungen)](/sccm/core/plan-design/configs/support-for-virtualization-environments)



<!--HONumber=Nov16_HO1-->


