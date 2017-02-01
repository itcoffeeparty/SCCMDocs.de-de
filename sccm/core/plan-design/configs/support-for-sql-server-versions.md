---
title: "Unterstützte Versionen von SQL Server | Microsoft-Dokumentation"
description: Abrufen der SQL Server-Version und Konfigurationsanforderungen zum Hosten einer System Center Configuration Manager-Standortdatenbank.
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
caps.latest.revision: 21
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 25aa013896ca118f0689b71e5cddcb8baf049c66
ms.openlocfilehash: 9bf4c1d9ee12da6801470165d33df50b2d08a810


---
# <a name="supported-sql-server-versions-for-system-center-configuration-manager"></a>Unterstützte SQL Server-Versionen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Jeder System Center Configuration Manager-Standort erfordert zum Hosten der Standortdatenbank eine unterstützte Version und Konfiguration von SQL Server.  

##  <a name="a-namebkmkinstancesa-sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> SQL Server-Instanzen und -Speicherorte  
 **Standort der zentralen Verwaltung und primäre Standorte:**  
Die Standortdatenbank muss eine vollständige Installation von SQL Server verwenden.  

 SQL Server kann auf den folgenden Computern installiert sein:  

-   Standortservercomputer  
-   Remotecomputer des Standortservers  

Die folgenden Instanzen werden unterstützt:  

-   Standard- oder benannte Instanz von SQL Server  
-   Konfigurationen mit mehreren Instanzen  
-   SQL Server-Cluster Weitere Informationen finden Sie unter [Hosten der Standortdatenbank mit einem SQL Server-Cluster](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
-   SQL Server Always On-Verfügbarkeitsgruppe. Diese Option setzt Configuration Manager Version 1602 oder höher voraus. Einzelheiten finden Sie unter [SQL Server Always On für eine hoch verfügbare Standortdatenbank für System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

> [!NOTE]  
>  Ein SQL Server-Cluster in einer NLB-Clusterkonfiguration (Network Load Balancing, Netzwerklastenausgleich) wird nicht unterstützt. Auch Technologien zur SQL Server-Datenbankspiegelung und Peer-to-Peer-Replikation werden nicht unterstützt. Die standardmäßige SQL Server-Transaktionsreplikation wird nur für das Replizieren von Objekten an Verwaltungspunkte unterstützt, die für die Verwendung von [Datenbankreplikaten](https://technet.microsoft.com/library/mt608546.aspx)konfiguriert sind.  


 **Sekundäre Standorte:**  
 Die Standortdatenbank kann die Standardinstanz einer vollständigen Installation von SQL Server oder SQL Server Express verwenden.  

 SQL Server muss auf dem Standortservercomputer installiert sein.  

##  <a name="a-namebkmksqlversionsa-supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> Unterstützte Versionen von SQL Server  
 In einer Hierarchie mit mehreren Standorten kann jeder Standort eine unterschiedliche SQL Server-Version zum Hosten der Standortdatenbank verwenden, solange Configuration Manager die von Ihnen verwendeten Versionen von SQL Server unterstützt.  

 Sofern nicht anders angegeben, werden die folgenden SQL Server-Versionen von System Center Configuration Manager-Versionen ab 1511 unterstützt.  

> [!IMPORTANT]  
>  Wenn Sie SQL Server Standard für die Datenbank am Standort der zentralen Verwaltung verwenden, ist die Gesamtanzahl der Clients begrenzt, die eine Hierarchie unterstützen kann. Informationen hierzu finden Sie unter [Size and scale numbers for System Center Configuration Manager](../../../core/plan-design/configs/size-and-scale-numbers.md) (Anpassen und Skalieren von Zahlen für System Center Configuration Manager).

### <a name="sql-server-2016-sp1-standard-enterprise"></a>SQL Server 2016 SP1: Standard, Enterprise  
Sie können diese Version von SQL Server ohne minimale kumulative Updateversion für Folgendes verwenden:  

-   Ein Standort der zentralen Verwaltung  
-   Primären Standort  
-   Sekundären Standort  

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard, Enterprise  
Sie können diese Version von SQL Server ohne minimale kumulative Updateversion für Folgendes verwenden:  

-   Ein Standort der zentralen Verwaltung  
-   Primären Standort  
-   Sekundären Standort  


### <a name="sql-server-2014-sp2-standard-enterprise"></a>SQL Server 2014 SP2: Standard, Enterprise  
Sie können diese Version von SQL Server ohne minimale kumulative Updateversion für Folgendes verwenden:  

-   Ein Standort der zentralen Verwaltung  
-   Primären Standort  
-   Sekundären Standort



### <a name="sql-server-2014-sp1-standard-enterprise"></a>SQL Server 2014 SP1: Standard, Enterprise  
 Sie können diese Version von SQL Server ohne minimale kumulative Updateversion für Folgendes verwenden:  

-   Ein Standort der zentralen Verwaltung  
-   Primären Standort  
-   Sekundären Standort


### <a name="sql-server-2012-sp3-standard-enterprise"></a>SQL Server 2012 SP3: Standard, Enterprise  
 Sie können diese Version von SQL Server ohne minimale kumulative Updateversion für Folgendes verwenden:  

-   Ein Standort der zentralen Verwaltung  
-   Primären Standort  
-   Sekundären Standort  


### <a name="sql-server-2012-sp2-standard-enterprise"></a>SQL Server 2012 SP2: Standard, Enterprise   
 Sie können diese Version von SQL Server ohne minimale kumulative Updateversion für Folgendes verwenden:  

-   Ein Standort der zentralen Verwaltung  
-   Primären Standort  
-   Sekundären Standort  


### <a name="sql-server-2008-r2-sp3-standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3: Standard, Enterprise, Datacenter     
Sie können diese Version von SQL Server ohne minimale kumulative Updateversion für Folgendes verwenden:  

-   Ein Standort der zentralen Verwaltung  
-   Primären Standort
-   Sekundären Standort



### <a name="sql-server-2016-express-sp1"></a>SQL Server 2016 Express SP1  
Sie können diese Version von SQL Server ohne minimale kumulative Updateversion für Folgendes verwenden:
-   Sekundären Standort

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
Sie können diese Version von SQL Server ohne minimale kumulative Updateversion für Folgendes verwenden:
-   Sekundären Standort


### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2   
Sie können diese Version von SQL Server ohne minimale kumulative Updateversion für Folgendes verwenden:  

-   Sekundären Standort  


### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1   
 Sie können diese Version von SQL Server ohne minimale kumulative Updateversion für Folgendes verwenden:  

-   Sekundären Standort  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
Sie können diese Version von SQL Server ohne minimale kumulative Updateversion für Folgendes verwenden:  

-   Sekundären Standort  

### <a name="sql-server-2012-express-sp2"></a>SQL Server 2012 Express SP2   
 Sie können diese Version von SQL Server ohne minimale kumulative Updateversion für Folgendes verwenden:  

-   Sekundären Standort  

##  <a name="a-namebkmksqlconfiga-required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> Erforderliche Konfigurationen für SQL Server  
 Folgendes ist für alle Installationen von SQL Server erforderlich, die Sie für eine Standortdatenbank verwenden (einschließlich SQL Server Express). Wenn SQL Server Express von Configuration Manager als Teil einer Installation eines sekundären Standorts installiert wird, werden diese Konfigurationen für Sie automatisch erstellt.  

 **Version der SQL Server-Architektur:**  
 Configuration Manager erfordert eine 64-Bit-Version von SQL Server, um die Standortdatenbank zu hosten.  

 **Datenbanksortierung:**  
 An jedem Standort muss sowohl die für den Standort als auch die für die Standortdatenbank verwendete Instanz von SQL Server die folgende Sortierung verwenden: **SQL_Latin1_General_CP1_CI_AS**.  

 Configuration Manager unterstützt zwei Sortierungsausnahmen, um die in GB18030 für die Nutzung in China definierten Standards zu erfüllen. Weitere Informationen finden Sie unter [Internationale Unterstützung in System Center Configuration Manager](../../../core/plan-design/hierarchy/international-support.md).  

 **SQL Server-Funktionen:**  
 Nur die Funktion **Datenbankmoduldienste** ist für jeden Standortserver erforderlich.  

 Für die Configuration Manager-Datenbankreplikation ist die Funktion **SQL Server-Replikation** nicht erforderlich. Diese SQL Server-Konfiguration ist jedoch erforderlich, wenn Sie [Datenbankreplikate für Verwaltungspunkte für System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) verwenden.  

 **Windows-Authentifizierung:**  
 Configuration Manager setzt die **Windows-Authentifizierung** zur Überprüfung von Verbindungen mit der Datenbank voraus.  

 **SQL Server-Instanz:**  
 Sie müssen für jeden Standort eine dedizierte Instanz von SQL Server verwenden. Sie können entweder die **benannte Instanz** oder eine **Standardinstanz**verwenden.  

 **SQL Server-Arbeitsspeicher:**  
 Reservieren Sie Arbeitsspeicher für SQL Server mithilfe von SQL Server Management Studio durch Festlegen der Einstellung **Minimaler Serverarbeitsspeicher** unter **Arbeitsspeicheroptionen für den Server**. Weitere Informationen zum Festlegen einer festen Arbeitsspeichergröße finden Sie unter [Festlegen einer festen Arbeitsspeichergröße (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

-   **Für einen auf demselben Computer wie der Standortserver installierten Datenbankserver:** Begrenzen Sie den Arbeitsspeicher für SQL Server auf 50 bis 80 Prozent des verfügbaren adressierbaren Systemspeicherns.  

-   **Für einen dedizierten Datenbankserver (remote vom Standortserver):** Begrenzen Sie den Arbeitsspeicher für SQL Server auf 80 bis 90 Prozent des verfügbaren adressierbaren Systemspeichers.  

-   **Für eine Arbeitsspeicherreserve für den Pufferpool jeder verwendeten SQL Server-Instanz:**  

    -   Für einen Standortserver der zentralen Verwaltung: Legen Sie mindestens 8 Gigabyte (GB) fest.  
    -   Für einen primären Standort: Legen Sie mindestens 8 Gigabyte (GB) fest.  
    -   Für einen sekundären Standort: Legen Sie mindestens 4 Gigabyte (GB) fest.  

**Geschachtelte SQL-Trigger:**  
 [Geschachtelte SQL-Trigger](http://go.microsoft.com/fwlink/?LinkId=528802) muss aktiviert sein.  

 **SQL Server-CLR-Integration**  
  Die Standortdatenbank erfordert, dass die CLR (Common Language Runtime) von SQL Server aktiviert ist. Dies wird automatisch bei der Installation von Configuration Manager aktiviert. Weitere Informationen zur CLR finden Sie unter [Einführung in die CLR-Integration für SQL Server](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx).  

##  <a name="a-namebkmkoptionala-optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> Optionale Konfigurationen für SQL Server  
 Die folgenden Konfigurationen sind für jede Datenbank optional, die eine vollständige SQL Server-Installation verwendet.  

 **SQL Server-Dienst:**  
 Sie können den SQL Server-Dienst für die Ausführung mit den folgenden Konten konfigurieren:  

-   Konto **Lokaler Domänenbenutzer**:  

    -   Dies ist eine bewährte Methode und erfordert möglicherweise die manuelle Registrierung des SPN (Service Principal Name, Dienstprinzipalname) des Kontos.  

-   Konto **Lokales System** des Computers, auf dem SQL Server ausgeführt wird:  

    -   Verwenden Sie das lokale Systemkonto, um den Konfigurationsvorgang zu vereinfachen.  
    -   Wenn Sie das lokale Systemkonto verwenden, wird der SPN von Configuration Manager automatisch für den SQL Server-Dienst registriert.  
    -   Die Verwendung des lokalen Systemkontos für den SQL Server-Dienst ist keine bewährte Methode im Zusammenhang mit SQL Server.  

Wenn der Computer, auf dem SQL Server ausgeführt wird, nicht sein lokales Systemkonto zum Ausführen des SQL Server-Diensts verwendet, müssen Sie den SPN des Kontos, unter dem SQL Server-Dienste ausgeführt werden, in den Active Directory-Domänendiensten konfigurieren. (Bei Verwendung des Systemkontos wird der SPN automatisch für Sie registriert.)

Informationen zu SPNs für die Standortdatenbank finden Sie unter [Verwalten des SPN für den Standortdatenbankserver](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN) im Thema [Ändern Ihrer System Center Configuration Manager-Infrastruktur](../../../core/servers/manage/modify-your-infrastructure.md).  

Informationen zum Ändern des vom SQL Server-Dienst verwendeten Kontos finden Sie unter [Ändern des Dienststartkontos für SQL Server (SQL Server-Konfigurations-Manager)](http://go.microsoft.com/fwlink/p/?LinkId=237661).  

**SQL Server Reporting Services:**  
SQL Server Reporting Services sind Voraussetzung für die Installation eines Reporting Services-Punkts, mit dem Sie Berichte ausführen können.  

> [!IMPORTANT]  
> Nach dem Aktualisieren von SQL Server von einer früheren Version wird möglicherweise der folgende Fehler angezeigt: *Report Builder Does Not Exist* (Berichts-Generator nicht vorhanden).    
> Zum Beheben dieses Fehlers müssen Sie die Reporting Services-Standortsystemrolle neu installieren.

**SQL Server-Ports:**  
Für die Kommunikation mit dem SQL Server-Datenbankmodul und die standortübergreifende Replikation können Sie die Standardkonfigurationen für SQL Server-Ports verwenden oder benutzerdefinierte Ports angeben:  

-   Die **standortübergreifende Kommunikation** erfolgt über den SQL Server Service Broker, der standardmäßig TCP-Port 4022 verwendet.  
-   Die **standortinterne Kommunikation** zwischen dem SQL Server-Datenbankmodul und verschiedenen Configuration Manager-Standortsystemrollen erfolgt standardmäßig über TCP-Port 1433. Die folgenden Standortsystemrollen kommunizieren direkt mit der SQL Server-Datenbank:  

    -   Verwaltungspunkt  
    -   SMS-Anbietercomputer  
    -   Reporting Services-Punkt  
    -   Standortserver  

Wenn ein Computer, auf dem SQL Server ausgeführt wird, Datenbanken von mehreren Standorten hostet, muss jede Datenbank eine separate SQL Server-Instanz verwenden. Außerdem muss jede dieser Instanzen mit einem eindeutigen Portsatz konfiguriert sein.  

> [!WARNING]  
>  Dynamische Ports werden von Configuration Manager nicht unterstützt. Da von benannten SQL Server-Instanzen standardmäßig dynamische Ports für die Verbindung mit dem Datenbankmodul verwendet werden, müssen Sie bei der Verwendung einer benannten Instanz den statischen Port, den Sie für die standortinterne Kommunikation einsetzen möchten, manuell konfigurieren.  

Wenn auf dem Computer, auf dem SQL Server ausgeführt wird, eine Firewall aktiviert ist, achten Sie darauf, dass die von Ihrer Bereitstellung verwendeten Ports überall im Netzwerk zwischen Computern, die mit SQL Server kommunizieren, von dieser Firewall zugelassen werden.  

Wie Sie SQL Server für die Verwendung eines bestimmten Ports konfigurieren, wird in der TechNet-Bibliothek unter [Konfigurieren eines Servers zur Überwachung eines bestimmten TCP-Ports (SQL Server-Konfigurations-Manager)](http://go.microsoft.com/fwlink/p/?LinkID=226349) anhand eines Beispiels erläutert.  



<!--HONumber=Jan17_HO1-->


