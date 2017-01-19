---
title: "Voraussetzungsprüfung | Microsoft-Dokumentation"
description: "Gehen Sie die verfügbaren Voraussetzungsprüfungen für System Center Configuration Manager durch. Enthält Voraussetzungsprüfungen für Sicherheitsrechte."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 9ace6e8fa05122924daaeceddf097ce1db12cf39


---
# <a name="list-of-prerequisite-checks-for-system-center-configuration-manager"></a>Liste der Voraussetzungsprüfungen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In den folgenden Abschnitten werden die verfügbaren Voraussetzungsprüfungen ausführlich erläutert.  


 Informationen zum Verwenden der Voraussetzungsprüfung finden Sie unter [Voraussetzungsprüfung](prerequisite-checker.md).  

##  <a name="a-namebkmksecuritya-prerequisite-checks-for-security-rights"></a><a name="BKMK_Security"></a> Voraussetzungsprüfungen für Sicherheitsrechte  
 Die folgenden Voraussetzungsprüfungen werden für Sicherheitsrechte ausgeführt.  

 **Administratorrechte am Standort der zentralen Verwaltung** – Damit wird überprüft, ob das Benutzerkonto, unter dem das Configuration Manager-Setup ausgeführt wird, auf dem Computer des Standorts der zentralen Verwaltung über lokale **Administratorrechte** verfügt.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  
      -   Primärer Standort  

**Administratorrechte für den erweiterten primären Standort** – Damit wird überprüft, ob der Benutzer, der das Setup ausführt, am eigenständigen primären Standort, der erweitert wird, über lokale **Administratorrechte** verfügt.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung  

**Administratorrechte für das Standortsystem** – Damit wird überprüft, ob das Benutzerkonto, unter dem das Configuration Manager-Setup ausgeführt wird, auf dem Standortservercomputer über lokale **Administratorrechte** verfügt.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung  
    -   Primärer Standort  
    -   Sekundärer Standort  

**Administratorrechte für CAS-Computer am erweiterten primären Standort** – Damit wird überprüft, ob das Computerkonto des Standorts der zentralen Verwaltung am eigenständigen primären Standort, der erweitert wird, über lokale **Administratorrechte** verfügt.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung  

**Verbindung mit SQL Server am Standort der zentralen Verwaltung** – Damit wird überprüft, ob das Benutzerkonto, unter dem das Configuration Manager-Setup am primären Standort ausgeführt wird, um diesen einer bestehenden Hierarchie hinzuzufügen, auf der SQL Server-Instanz für den Standort der zentralen Verwaltung über die Rolle **sysadmin** verfügt.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Primärer Standort  

**Administratorrechte für das Computerkonto des Standortservers** – Damit wird überprüft, ob das Computerkonto des Standortservers auf dem Computer von SQL Server und dem Verwaltungspunkt über Administratorrechte verfügt.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Primärer Standort  
    -   SQL Server  

**Kommunikation zwischen Standortsystem und SQL Server** – Damit wird überprüft, ob ein gültiger Dienstprinzipalname (Service Principal Name, SPN) in Active Directory Domain Services für das Konto registriert ist, das für die Ausführung des SQL Server-Diensts der SQL Server-Instanz vorgesehen ist, die als Host für die Configuration Manager-Standortdatenbank verwendet wird. Zur Unterstützung der Kerberos-Authentifizierung muss ein gültiger SPN in den Active Directory-Domänendiensten registriert sein.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Sekundärer Standort  
    -   Verwaltungspunkt  

**SQL Server-Sicherheitsmodus** – Damit wird überprüft, ob SQL Server für die Windows-Authentifizierungssicherheit konfiguriert ist.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   SQL Server  

**Systemadministratorrechte für SQL Server** – Damit wird überprüft, ob das Benutzerkonto, unter dem das Configuration Manager-Setup ausgeführt wird, über die Rolle **sysadmin** für die SQL Server-Instanz verfügt, die für die Datenbankinstallation ausgewählt wurde. Bei dieser Überprüfung tritt auch dann ein Fehler auf, wenn vom Setup nicht auf die SQL Server-Instanz zugegriffen werden kann, um die Berechtigungen zu prüfen.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   SQL Server  

**SQL Server-Systemadministratorrechte für Referenzstandort** – Damit wird überprüft, ob das Benutzerkonto, unter dem das Configuration Manager-Setup ausgeführt wird, über die Rolle **sysadmin** für die SQL Server-Rolleninstanz verfügt, die als Datenbank des Referenzstandorts ausgewählt wurde.  SQL Server **sysadmin** -Rollenberechtigungen sind erforderlich, um Standortdatenbanken zu ändern.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   SQL Server  

##  <a name="a-namebkmkdependenciesa-prerequisite-checks-for-configuration-manager-dependencies"></a><a name="BKMK_Dependencies"></a> Voraussetzungsprüfungen für Configuration Manager-Abhängigkeiten  
 Die folgenden Voraussetzungsprüfungen werden für Configuration Manager-Abhängigkeiten ausgeführt.  

**Am primären Zielstandort sind aktive Migrationszuordnungen vorhanden**  

 Damit wird überprüft, ob am primären Zielstandort aktive Migrationszuordnungen vorhanden sind.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung  

**Aktives MP-Replikat** – Damit wird auf ein aktives Verwaltungspunktreplikat geprüft.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Primärer Standort  

**Administratorrechte für den Verteilungspunkt** – Damit wird überprüft, ob der Benutzer, der das Setup ausführt, über lokale **Administratorrechte** für den Verteilungspunktcomputer verfügt.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Verteilungspunkt  

**Administratorrechte für den Verwaltungspunkt** – Damit wird überprüft, ob das Computerkonto des Standortservers über **Administratorrechte** für den Verwaltungspunkt- und Verteilungspunktcomputer verfügt.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Verwaltungspunkt  

**Administrative Freigabe (Standortsystem)** – Damit wird überprüft, ob die erforderlichen administrativen Freigaben auf dem Standortsystemcomputer vorhanden sind.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Verwaltungspunkt  

**Anwendungskompatibilität** – Damit wird überprüft, ob alle aktuellen Anwendungen mit dem Anwendungsschema kompatibel sind.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort  

**BITS aktiviert** – Damit wird überprüft, ob BITS (Background Intelligent Transfer Service) auf dem Standortsystemcomputer des Verwaltungspunkts installiert wurde. Fehler bei dieser Prüfung können folgende Ursachen haben: BITS ist nicht installiert, die IIS 6-WMI-Kompatibilitätskomponente für IIS7 ist auf dem Computer oder dem Remote-IIS-Host nicht installiert, oder die IIS-Remoteeinstellungen konnten von Setup nicht überprüft werden, weil gemeinsame IIS-Komponenten nicht auf dem Standortservercomputer installiert wurden.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Verwaltungspunkt  

**BITS installiert** – Damit wird überprüft, ob BITS (Background Intelligent Transfer Service) in IIS (Internet Information Services) installiert ist.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Verwaltungspunkt  

**Sortierung ohne Beachtung der Groß-/Kleinschreibung bei SQL Server** – Damit wird überprüft, ob die SQL Server-Installation eine Sortierung ohne Beachtung der Groß-/Kleinschreibung verwendet (Beispiel: SQL_Latin1_General_CP1_CI_AS).  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   SQL Server  

**Version und Standortcode des vorhandenen eigenständigen primären Standorts prüfen** – Überprüfen Sie, ob der primäre Standort, den Sie erweitern möchten, ein eigenständiger primärer Standort ist und die gleiche Version wie Configuration Manager hat, aber einen anderen Standortcode als der zu installierende zentrale Verwaltungsstandort aufweist.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort  

**Auf inkompatible Auflistungsverweise überprüfen** – Bei einem Upgrade wird damit überprüft, ob Sammlungen nur auf Sammlungen des gleichen Typs verweisen.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung  

**Clientversion auf Verwaltungspunktcomputer** – Damit wird überprüft, ob Sie den Verwaltungspunkt auf einem Computer installieren, auf dem keine andere Version des Configuration Manager-Clients installiert ist.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Verwaltungspunkt  

**Konfiguration der Speichernutzung durch SQL Server** – Damit wird überprüft, ob für SQL Server ein Speicherlimit konfiguriert wurde. Sie sollten einen Maximalwert für den SQL Server-Speicher festlegen.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   SQL Server  

**Dedizierte SQL Server-Instanz** – Damit wird überprüft, ob eine dedizierte Instanz von SQL Server zum Hosten der Configuration Manager-Standortdatenbank konfiguriert wurde. Wenn die Instanz von einem anderen Standort verwendet wird, müssen Sie eine andere Instanz für den neuen Standort auswählen. Alternativ können Sie den anderen Standort deinstallieren oder dessen Datenbank zu einer anderen SQL Server-Instanz verschieben.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort  

**Bestehende Configuration Manager-Serverkomponenten auf Server** – Damit wird überprüft, ob auf dem für die Installation des Standorts ausgewählten Computer bereits ein Standortserver oder eine Standortsystemrolle installiert wurde.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort  

**Firewallausnahme für SQL Server** – Damit wird überprüft, ob die Windows-Firewall deaktiviert ist oder eine relevante Windows-Firewallausnahme für SQL Server eingerichtet wurde. Erlauben Sie einen Remotezugriff auf sqlservr.exe bzw. die TCP-Ports. Standardmäßig wird TCP-Port 1433 von SQL Server überwacht, und TCP-Port 4022 wird vom SQL-Broker-Dienst verwendet.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort    
    -   Verwaltungspunkt  

**Firewallausnahme für SQL Server (eigenständiger primärer Standort)** – Damit wird überprüft, ob die Windows-Firewall deaktiviert ist oder eine relevante Windows-Firewallausnahme für SQL Server eingerichtet wurde. Erlauben Sie einen Remotezugriff auf sqlservr.exe bzw. die TCP-Ports. Standardmäßig wird TCP-Port 1433 von SQL Server überwacht, und TCP-Port 4022 wird vom SQL-Broker-Dienst verwendet.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Primärer Standort (nur eigenständige)  

**Firewallausnahme bei SQL Server für Verwaltungspunkt** – Damit wird überprüft, ob die Windows-Firewall deaktiviert ist oder eine relevante Windows-Firewallausnahme für SQL Server eingerichtet wurde.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Verwaltungspunkt  

**IIS-HTTPS-Konfiguration** – Hiermit werden die IIS-Websitebindungen (Internet Information Services) für das HTTPS-Kommunikationsprotokoll geprüft. Wenn Sie die Installation von Standortrollen, für die HTTPS erforderlich ist, ausgewählt haben, konfigurieren Sie die IIS-Websitebindungen auf dem angegebenen Server mit einem gültigen PKI-Serverzertifikat.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Verwaltungspunkt    
    -   Verteilungspunkt  

**IIS-Dienst wird ausgeführt** – Damit wird überprüft, ob IIS (Internet Information Services) installiert wurde und auf dem Computer ausgeführt wird, auf dem der Verwaltungs- oder Verteilungspunkt installiert werden soll.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Verwaltungspunkt    
    -   Verteilungspunkt  

**Sortierung des erweiterten primären Standorts vergleichen** – Überprüfen Sie, ob die Standortdatenbank für den eigenständigen primären Standort, den Sie erweitern, die gleiche Sortierung aufweist wie die Standortdatenbank am Standort der zentralen Verwaltung.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung  

**Microsoft Remote Differential Compression-Bibliothek (RDC) registriert** – Damit wird überprüft, ob die Microsoft Remote Differential Compression-Bibliothek (RDC) auf dem Computer registriert ist, auf dem der Configuration Manager-Standortserver installiert werden soll.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort  

**Microsoft Windows Installer** – Hiermit wird die Version von Windows Installer geprüft. Wenn bei dieser Überprüfung Fehler auftreten, konnte die Version von Setup nicht geprüft werden, oder die installierte Version erfüllt nicht die Mindestanforderungen von Windows Installer Version 4.5.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort  

**Microsoft XML Core Services 6.0 (MSXML60)** – Damit wird überprüft, ob auf dem Computer Microsoft XML Core Services (MSXML) Version 6.0 oder höher installiert ist.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort    
    -   Configuration Manager-Konsole    
    -   Verwaltungspunkt    
    -   Verteilungspunkt  

**Mindestversion von .NET Framework für die Configuration Manager-Konsole** – Damit wird überprüft, ob Microsoft .NET Framework Version 4.0 auf dem Computer mit der Configuration Manager-Konsole installiert ist. Microsoft .NET Framework 4.0 steht im [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=189149)für den Download zur Verfügung.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Configuration Manager-Konsole  

**Mindestversion von .NET Framework für den Configuration Manager-Standortserver** – Damit wird überprüft, ob Microsoft .NET Framework Version 3.5 auf dem Configuration Manager-Standortserver installiert ist. Für Windows Server 2008 steht Microsoft .NET Framework 3.5 im [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=185604)zum Download zur Verfügung. Für Windows Server 2008 R2 können Sie Microsoft .NET Framework 3.5 als Funktion in Server-Manager aktivieren.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort  

**Mindestversion von .NET Framework für die Installation der SQL Server Express-Edition an sekundären Configuration Manager-Standorten** – Damit wird überprüft, ob Microsoft .NET Framework Version 4.0 auf Configuration Manager-Computern des sekundären Standorts für die Installation der SQL Server Express-Edition installiert ist.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Sekundärer Standort  

**Sortierung übergeordnete/untergeordnete Datenbank** – Damit wird überprüft, ob die Sortierung der Standortdatenbank der Sortierung der Datenbank des übergeordneten Standorts entspricht. Für alle Standorte in einer Hierarchie muss die gleiche Datenbanksortierung verwendet werden.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Primärer Standort    
    -   Sekundärer Standort  

**PowerShell 2.0 auf dem Standortserver** – Damit wird überprüft, ob Windows PowerShell Version 2.0 oder eine neuere Version auf dem Standortserver für den Configuration Manager-Exchange-Connector installiert ist. Weitere Informationen über PowerShell 2.0 finden Sie im [Artikel 968930](http://go.microsoft.com/fwlink/p/?LinkId=226450) der Microsoft Knowledge Base.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Primärer Standort  

**Primärer FQDN** – Damit wird überprüft, ob der NetBIOS-Name des Computers dem lokalen Hostnamen des Computers (erste Bezeichnung im FQDN) entspricht.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort    
    -   SQL Server  

**Remoteverbindung mit WMI am sekundären Standort** – Damit wird überprüft, ob von Setup eine Remoteverbindung mit WMI auf dem sekundären Standortserver hergestellt werden kann.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Sekundärer Standort  

**Erforderliche SQL Server-Sortierung** – Damit wird überprüft, ob die SQL Server-Instanz und die Configuration Manager-Standortdatenbank (falls vorhanden) zur Verwendung der Sortierung „SQL_Latin1_General_CP1_CI_AS“ konfiguriert sind. Ausnahme: Es wird ein chinesisches Betriebssystem verwendet, und GB18030-Unterstützung ist erforderlich.  

 Weitere Informationen zum Ändern der Sortierung Ihrer SQL Server-Instanz und -Datenbank finden Sie unter [Festlegen und Ändern von Sortierungen](http://go.microsoft.com/fwlink/p/?LinkID=234541) in der Onlinedokumentation zu SQL Server 2008 R2.  Informationen zur Aktivierung der GB18030-Unterstützung finden Sie unter [Internationale Unterstützung in System Center Configuration Manager](../../../../core/plan-design/hierarchy/international-support.md).  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort  

**Setupquellordner** – Damit wird überprüft, ob das Computerkonto für den sekundären Standort über die NTFS-Dateisystemberechtigungen **Lesen** und Freigabeberechtigungen **Lesen** für den Setupquellordner und die Freigabe verfügt.  

> [!NOTE]  
>  Wenn Sie administrative Freigaben verwenden (z. B. C$ und D$), muss das Computerkonto des sekundären Standorts ein Administrator auf dem Computer sein.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Sekundärer Standort  

**Version der Setupquelle** – Damit wird überprüft, ob die Configuration Manager-Version im Quellordner, den Sie für die Installation des sekundären Standorts angegeben haben, der Configuration Manager-Version des primären Standorts entspricht.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Sekundärer Standort  

**Verwendeter Standortcode** – Damit wird überprüft, ob der von Ihnen angegebene Standortcode in der Configuration Manager-Hierarchie bereits verwendet wird. Sie müssen für diesen Standort einen eindeutigen Code angeben.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Primärer Standort  

**Die Domäne des SMS-Anbietercomputers ist mit der des Standortsservers identisch.** – Damit wird überprüft, ob ein Computer, auf dem eine Instanz des SMS-Anbieters ausgeführt wird, über die gleiche Domäne verfügt wie der Standortserver.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   SMS-Anbieters  

**SQL Server Edition** – Damit wird überprüft, ob es sich bei der SQL Server-Edition am Standort nicht um SQL Server Express handelt.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   SQL Server  

**SQL Server Express an sekundärem Standort** – Damit wird überprüft, ob SQL Server Express auf dem Standortservercomputer für einen sekundären Standort installiert werden kann.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Sekundärer Standort  

**SQL Server auf Computer des sekundären Standorts** – Damit wird überprüft, ob SQL Server auf dem Computer des sekundären Standorts installiert ist. Die Installation von SQL Server auf einem Remote-Standortsystem wird nicht unterstützt.  

> [!WARNING]  
>  Diese Prüfung gilt nur dann, wenn Sie auswählen, dass von Setup eine vorhandene Instanz von SQL Server verwendet werden soll.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Sekundärer Standort  

**SQL Server-Prozessspeicherzuweisung** – Damit wird sichergestellt, dass von SQL Server mindestens 8 GB Speicherplatz für den Standort der zentralen Verwaltung und den primären Standort reserviert werden und mindestens 4 GB für den sekundären Standort. Weitere Informationen zum Festlegen einer festen Speichergröße mit SQL Server Management Studio finden Sie unter [Vorgehensweise: Festlegen einer festen Arbeitsspeichergröße (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

> [!NOTE]  
>  Diese Prüfung steht für SQL Server Express auf einem sekundären Standort nicht zur Verfügung, da dieser auf 1 GB reservierter Speicherplatz begrenzt ist.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   SQL Server  

**Laufendes Konto für SQL Server-Dienst** – Damit wird sichergestellt, dass das Anmeldekonto für den SQL Server-Dienst kein lokales Benutzerkonto oder LOCAL SERVICE ist. Sie müssen den SQL Server-Dienst konfigurieren, um ein gültiges Domänenkonto, NETWORK SERVICE oder LOCAL SYSTEM verwenden zu können.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort  

**SQL Server-TCP-Port** – Damit wird überprüft, ob TCP für SQL Server aktiviert und die Verwendung eines statischen Ports eingestellt ist.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   SQL Server  

**SQL Server-Version** – Damit wird sichergestellt, dass eine unterstützte Version von SQL Server auf dem angegebenen Standortdatenbankserver installiert ist. Weitere Informationen finden Sie unter [Unterstützung für SQL Server-Versionen für System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   SQL Server  

**Nicht unterstützte Standortsystem-Betriebssystemversion für das Upgrade** – Während eines Upgrades überprüft diese Regel, ob Standortsystemrollen, die keine Verteilungspunkte sind, auf Computern mit Windows Server 2008 oder früher installiert sind.  

> [!NOTE]  
>  Diese Überprüfung kann den Status von Standortsystemrollen nicht auflösen, die in Azure oder für den Cloudspeicher installiert werden, der von Microsoft Intune verwendet wird, wenn Sie Intune in Configuration Manager integrieren. Daher können Sie Warnungen für diese Rollen als falsche positive Werte ignorieren.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Primärer Standort    
    -   Sekundärer Standort  

**Die nicht unterstützte Standortsystemrolle „Asset Intelligence-Synchronisierungspunkt“ ist am erweiterten primären Standort vorhanden** – Damit wird überprüft, ob die Asset Intelligence-Synchronisierungspunkt-Standortsystemrolle nicht an dem eigenständigen primären Standort installiert ist, den Sie erweitern.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung  

**Die nicht unterstützte Standortsystemrolle „Endpoint Protection-Punkt“ ist am erweiterten primären Standort vorhanden.** – Damit wird überprüft, ob die Endpoint Protection-Punkt-Standortsystemrolle nicht an dem eigenständigen primären Standort installiert ist, den Sie erweitern.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung  

<a name="-head"></a><<<<<<< KOPF
=======

>>>>>>> 5e8e486ea74f66a92696c65e3367aec2e592b001 **Die nicht unterstützte Standortsystemrolle „Microsoft Intune Connector“ ist am erweiterten primären Standort vorhanden.** – Damit wird überprüft, ob die „Microsoft Intune-Connector“-Standortsystemrolle nicht an dem eigenständigen primären Standort installiert ist, den Sie erweitern.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung  

**Das Migrationstool für den Benutzerstatus (USMT) ist installiert.** – Damit wird überprüft, ob die Komponente „Migrationstool für den Benutzerstatus“ (USMT) des Assessment and Deployment Kits (ADK) für Windows 8.1 installiert ist.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort (nur eigenständige)  

**FQDN des SQL Server-Computers überprüfen** – Damit wird überprüft, ob der FQDN, den Sie für den SQL Server-Computer angegeben haben, gültig ist.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   SQL Server  

**Version des zentralen Verwaltungsstandorts überprüfen** – Damit wird überprüft, ob der Standort der zentralen Verwaltung die gleiche Version wie Configuration Manager hat.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Primärer Standort  

**Berechtigungen des Standortservers zum Veröffentlichen in Active Directory prüfen** – Damit wird sichergestellt, dass das Computerkonto für den Standortserver über die Berechtigung **Vollzugriff** für den Container **Systemverwaltung** in der Active Directory-Domäne verfügt. Weitere Informationen zu Ihren Optionen beim Konfigurieren der erforderlichen Berechtigungen finden Sie unter [Extend the Active Directory schema for System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) (Erweitern des Active Directory-Schemas für System Center Configuration Manager).  

> [!NOTE]  
>  Sie können diese Warnung ignorieren, wenn Sie die Berechtigungen manuell überprüft haben.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort  

**Die Windows-Bereitstellungstools sind installiert** – Damit wird überprüft, ob die Komponente „Windows-Bereitstellungstools“ des Assessment and Deployment Kits (ADK) für Windows 10 installiert ist.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   SMS-Anbieters  

**Windows-Failovercluster** – Damit wird sichergestellt, dass Computer mit einem Verwaltungs- oder Verteilungspunkt nicht zum Windows-Cluster gehören.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Verwaltungspunkt    
    -   Verteilungspunkt  

**Windows Preinstallation Environment ist installiert** – Damit wird überprüft, ob die Komponente „Windows-Vorinstallationsumgebung“ des Assessment and Deployment Kits (ADK) für Windows 10 installiert ist.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   SMS-Anbieters  

**Windows Remote Management (WinRM) Version 1.1** – Damit wird sichergestellt, dass WinRM Version 1.1 auf dem Computer des primären Standortservers oder der Configuration Manager-Konsole installiert ist, um die Out-of-Band-Verwaltungskonsole auszuführen. Weitere Informationen zum Herunterladen von WinRM 1.1 finden Sie im [Artikel 936059](http://go.microsoft.com/fwlink/p/?LinkId=247166) der Microsoft Knowledge Base.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Primärer Standort    
    -   Configuration Manager-Konsole  

**WSUS auf Standortserver** – Damit wird sichergestellt, dass die Windows Server Update Services (WSUS) der Version 3.0 Service Pack 2 auf dem Standortserver installiert sind. Wenn Sie einen Softwareupdatepunkt auf einem Computer verwenden, der von dem des Standortservers abweicht, müssen Sie auf dem Standortserver die WSUS-Administrationskonsole installieren. Weitere Informationen über WSUS finden Sie auf der Website [Windows Server Update Services](http://go.microsoft.com/fwlink/p/?LinkID=79477) .  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort  

##  <a name="a-namebkmkrequirementsa-prerequisite-checks-for-system-requirements"></a><a name="BKMK_Requirements"></a> Voraussetzungsprüfungen für Systemanforderungen  
 Die folgenden Voraussetzungsprüfungen werden für die Systemanforderungen ausgeführt.  

**Überprüfung der Active Directory-Domänenfunktionsebene** – Damit wird sichergestellt, dass die Active Directory-Domänenfunktionsebene mindestens Windows Server 2008 R2 entspricht.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort  

**Es wird überprüft, ob der Serverdienst ausgeführt wird.** – Damit wird überprüft, ob der Serverdienst gestartet wurde.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort  

**Domänenmitgliedschaft** – Damit wird sichergestellt, dass der Configuration Manager-Computer Mitglied einer Windows-Domäne ist.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort    
    -   SMS-Anbieter    
    -   SQL Server  

**Domänenmitgliedschaft** – Damit wird sichergestellt, dass der Configuration Manager-Computer Mitglied einer Windows-Domäne ist.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Verwaltungspunkt    
    -   Verteilungspunkt  

**FAT-Laufwerk an Standortserver** – Damit wird überprüft, ob das Laufwerk mit dem FAT-Dateisystem formatiert ist. Installieren der Standortserverkomponenten auf Laufwerken, die mit dem NTFS-Dateisystem für mehr Sicherheit formatiert sind.  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Primärer Standort  

**Freier Speicherplatz auf Standortserver** – Dem Standortservercomputer müssen mindestens 5 GB freier Speicherplatz für die Installation des Standortservers zur Verfügung stehen. Wenn Sie die Standortsystemrolle SMS-Anbieter auf demselben Computer installieren, benötigen Sie zusätzlich 1 GB freien Speicherplatz.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort  

**Ausstehender Systemneustart** – Damit wird überprüft, ob ein anderes Programm einen Serverneustart benötigt, bevor Sie das Setup ausführen.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort  
    -   Configuration Manager-Konsole    
    -   SMS-Anbieters    
    -   SQL Server    
    -   Verwaltungspunkt    
    -   Verteilungspunkt  

**Domänencontroller ohne Schreibzugriff** – Standortdatenbankserver und sekundäre Standortserver werden auf einem Domänencontroller ohne Schreibzugriff (read-only domain controller, RODC) nicht unterstützt. Weitere Informationen finden Sie unter [You may encounter problems when installing SQL Server on a domain controller (Beim Installieren eines SQL Servers auf einem Domänencontroller treten möglicherweise Probleme auf)](http://go.microsoft.com/fwlink/p/?LinkId=264856) in der Microsoft Knowledge Base.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort  

**Schemaerweiterungen** – Damit wird festgestellt, ob das Active Directory Domain Services-Schema erweitert wurde, und, wenn dies der Fall ist, die Version der verwendeten Schemaerweiterungen ermittelt. Configuration Manager-Active Directory-Schemaerweiterungen sind nicht für die Standortserverinstallation erforderlich. Sie werden jedoch empfohlen, damit die Verwendung aller Configuration Manager-Features vollständig unterstützt wird. Weitere Informationen zu den Vorteilen einer Schemaerweiterung finden Sie unter [Extend the Active Directory schema for System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) (Erweitern des Active Directory-Schemas für System Center Configuration Manager).  

-   **Schweregrad:** Warnung  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort  

**Länge des FQDN des Standortservers** – Hiermit wird die Länge des FQDN des Standortservercomputers geprüft.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort  

**Von der Configuration Manager-Konsole nicht unterstütztes Betriebssystem** – Hiermit wird sichergestellt, dass die Configuration Manager-Konsolen auf Computern installiert werden können, auf denen eine unterstützte Betriebssystemversion ausgeführt wird. Weitere Informationen finden Sie unter [Supported operating systems for sites and clients for System Center Configuration Manager (Unterstützte Betriebssysteme für Standorte und Clients für System Center Configuration Manager)](/sccm/core/plan-design/configs/supported-operating-systems-consoles).  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Configuration Manager-Konsole  

**Von Setup nicht unterstützte Betriebssystemversion des Standortservers** – Hiermit wird sichergestellt, dass ein unterstütztes Betriebssystem auf dem Server ausgeführt wird. Weitere Informationen finden Sie unter [Supported operating systems for sites and clients for System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers) (Unterstützte Betriebssysteme für Standorte und Clients für System Center Configuration Manager).  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort    
    -   Sekundärer Standort    
    -   Configuration Manager-Konsole    
    -   Verwaltungspunkt    
    -   Verteilungspunkt  

**Datenbankkonsistenz überprüfen** – Hiermit wird ab Version 1602 die Konsistenz der Datenbank geprüft.  

-   **Schweregrad:** Fehler  

-   **Anwendbarkeit:**  

    -   Standort der zentralen Verwaltung    
    -   Primärer Standort  



<!--HONumber=Dec16_HO3-->


