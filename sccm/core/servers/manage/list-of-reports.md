---
title: Liste von Berichten | Microsoft-Dokumentation
description: "Prüfen Sie eine Liste von Berichten, die im Lieferumfang von Configuration Manager enthalten sind. Die Berichte werden in verschiedenen Kategorien angezeigt."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b7332ed3-8003-454b-bb12-1fdf8721425c
caps.latest.revision: 10
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 1480c38a6a3afef76b2e8759eaafd47d28f978f4


---
# <a name="list-of-reports-in-system-center-configuration-manager"></a>Liste der System Center Configuration Manager-Berichte

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit System Center Configuration Manager werden viele integrierte Berichte bereitgestellt, die zahlreiche Berichtstasks abdecken, die Sie möglicherweise ausführen möchten. Sie können die SQL-Anweisungen in diesen Berichten auch zur Unterstützung beim Erstellen eigener Berichte verwenden. Verwenden Sie die Informationen in diesem Thema, um die mit Configuration Manager bereitgestellten Berichte kennenzulernen.  

## <a name="list-of-built-in-configuration-manager-reports"></a>Liste der integrierten Configuration Manager-Berichte  
 Die folgenden Berichte sind in Configuration Manager enthalten. Die Berichte werden in verschiedenen Kategorien angezeigt.  

### <a name="administrative-security"></a>Administrative Sicherheit  
 Die folgenden Berichte sind unter der Kategorie **Administrative Sicherheit** aufgeführt.  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Verwaltungsaktivitätsprotokoll**|Zeigt einen Datensatz der für Administratoren, Sicherheitsrollen, Sicherheitsbereiche und Sammlungen vorgenommenen administrativen Änderungen an.|  
|**Sicherheitszuweisungen für Administratoren**|Zeigt Administratoren, deren zugeordneten Sicherheitsrollen und die jeder Sicherheitsrolle für die jeweiligen Benutzer zugeordneten Sicherheitsbereiche an.|  
|**Objekte, die von einem einzelnen Sicherheitsbereich gesichert sind**|Zeigt Objekte an, die durch einen angegebenen Sicherheitsbereich gesichert werden und nur diesem Sicherheitsbereich zugewiesen sind. Dieser Bericht zeigt keine Objekte an, die mehr als einem Sicherheitsbereich zugeordnet sind.|  
|**Sicherheit für ein bestimmtes oder mehrere Configuration Manager-Objekte**|Zeigt sicherungsfähige Objekte, die diesen Objekten zugeordneten Sicherheitsbereiche sowie die Administratoren an, die über Zugriffsrechte für diese Objekte verfügen.|  
|**Zusammenfassung der Sicherheitsrollen**|Zeigt die Sicherheitsrollen und die Configuration Manager-Administratoren an, die den jeweiligen Rollen zugeordnet sind|  
|**Zusammenfassung der Sicherheitsbereiche**|Zeigt die Sicherheitsbereiche und Configuration Manager-Administratoren sowie die jedem Bereich zugeordneten Sicherheitsgruppen an|  

### <a name="alerts"></a>Warnungen  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Warnungs-Scorecard**|Zeigt eine Zusammenfassung aller zurückgestellten Warnungen an, die zwischen dem angegebenen Start- und Enddatum generiert wurden.|  
|**Meisterzeugte Warnungen**|Zeigt eine Zusammenfassung der Warnungen an, die vom heutigen Datum bis zurück zum angegebenen Datum für den angegebenen Featurebereich am häufigsten generiert wurden.|  

### <a name="asset-intelligence"></a>Asset Intelligence  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Hardware 01A – Zusammenfassung von Computern in einer bestimmten Sammlung**|Zeigt eine Asset Intelligence-Zusammenfassungsansicht der Computer in einer von Ihnen angegebenen Sammlung an.|  
|**Hardware 03A – Primäre Computerbenutzer**|Zeigt Benutzer und die Anzahl der Computer an, auf denen diese die primären Benutzer sind.|  
|**Hardware 03B – Computer für einen bestimmten primären Konsolenbenutzer**|Zeigt alle Computer an, für die ein angegebener Benutzer der primäre Konsolenbenutzer ist.|  
|**Hardware 04A – Computer mit mehreren Benutzern (gemeinsam genutzt)**|Zeigt Computer an, die keinen primären Benutzer aufweisen. Dies sind Computer, auf denen keiner der Benutzer für mehr als 66 % der Anmeldezeit bei der %-Konsole verantwortlich ist.|  
|**Hardware 05A – Konsolenbenutzer auf einem bestimmten Computer**|Zeigt alle Konsolenbenutzer auf einem angegebenen Computer an.|  
|**Hardware 06A – Computer ohne ermittelte Konsolenbenutzer**|Unterstützt Administratoren beim Identifizieren von Computern, für die die Sicherheitsprotokollierung aktiviert sein muss.|  
|**Hardware 07A – USB-Geräte nach Hersteller**|Zeigt USB-Geräte nach Hersteller gruppiert an.|  
|**Hardware 07B – USB-Geräte nach Hersteller und Beschreibung**|Zeigt USB-Geräte nach Hersteller und Beschreibung gruppiert an.|  
|**Hardware 07C – Computer mit einem bestimmten USB-Gerät**|Zeigt alle Computer mit einem angegebenen USB-Gerät an.|  
|**Hardware 07D – USB-Geräte auf einem bestimmten Computer**|Zeigt alle USB-Geräte auf einem angegebenen Computer an.|  
|**Hardware 08A – Hardware, die für ein Softwareupdate nicht bereit ist**|Zeigt die Hardware an, die die Mindestanforderungen nicht erfüllt.|  
|**Hardware 09A – Suche nach Computern**|Zeigt eine Asset-Manager-Zusammenfassung von Computern an, die durch eine Schlüsselwortsuche nach Computername, Configuration Manager-Standort, Domäne, Hauptkonsolenbenutzer, Betriebssystem, Hersteller oder Modell gefunden wurden|  
|**Hardware 10A – Computer in einer angegebenen Sammlung mit Änderungen während eines angegebenen Zeitraums**|Zeigt eine Liste der Computer in einer angegebenen Sammlung an, in der während eines angegebenen Zeitraums eine Hardwareklasse geändert wurde.|  
|**Hardware 10B – Änderungen auf einem angegebenen Computer während eines angegebenen Zeitraums**|Zeigt die Klassen an, die auf einem angegebenen Computer während eines angegebenen Zeitraums geändert wurden.|  
|**Lizenz 01A – Microsoft-Volumenlizenzregister für Microsoft-Lizenzzusammenfassungen**|Zeigt ein Inventar aller Microsoft-Softwaretitel an, die im Microsoft-Volumenlizenzprogramm verfügbar sind.|  
|**Lizenz 01B – Microsoft-Volumenlizenzregisterprodukte nach Vertriebskanal**|Identifiziert den Vertriebskanal für inventarisierte Microsoft-Volumenlizenzsoftware und zeigt diesen an.|  
|**Lizenz 01C – Computer mit einem bestimmten Microsoft-Volumenlizenzregisterprodukt und Vertriebskanal**|Identifiziert Computer und zeigt diese an, die ein angegebenes Produkt aus dem Microsoft-Volumenlizenzregister aufweisen.|  
|**Lizenz 01D – Microsoft-Volumenlizenzregisterprodukte auf einem bestimmten Computer**|Identifiziert alle Microsoft-Volumenlizenzregisterprodukte auf einem angegebenen Computer und zeigt diese an.|  
|**Lizenz 02A – Anzahl der Lizenzen, die demnächst ablaufen, nach Zeitabschnitten**|Zeigt die Anzahl der Lizenzen, die demnächst ablaufen, nach einem angegebenen Zeitabschnitt an. Es werden die Produkte angezeigt, deren Lizenzen vom Softwarelizenzierungsdienst verwaltet werden.|  
|**Lizenz 02B – Computer mit ablaufenden Lizenzen**|Zeigt die angegebenen Computer mit Lizenzen an, die demnächst ablaufen.|  
|**Lizenz 02C – Lizenzinformationen für einen bestimmten Computer**|Zeigt Produkte auf einem angegebenen Computer an, deren Lizenzen vom Softwarelizenzierungsdienst verwaltet werden.|  
|**Lizenz 03A – Anzahl der Lizenzen, geordnet nach Lizenzstatus**|Zeigt Produkte nach Lizenzstatus an, deren Lizenzen vom Softwarelizenzierungsdienst verwaltet werden.|  
|**Lizenz 03B – Computer mit einem bestimmten Lizenzstatus**|Zeigt Produkte mit einem angegebenen Lizenzstatus an, deren Lizenzen vom Softwarelizenzierungsdienst verwaltet werden.|  
|**Lizenz 04A – Anzahl der mithilfe des Softwarelizenzierungsdiensts verwalteten Produkte**|Zeigt eine Anzahl von Produkten an, deren Lizenzen vom Softwarelizenzierungsdienst verwaltet werden.|  
|**Lizenz 04B – Computer mit einem bestimmten vom Softwarelizenzierungsdienst verwalteten Produkt**|Zeigt vom Softwarelizenzierungsdienst verwaltete Computer an, die ein angegebenes Produkt enthalten.|  
|**Lizenz 05A – Computer, auf denen Schlüsselverwaltungsdienste bereitgestellt werden**|Zeigt Computer an, die als Schlüsselverwaltungsserver fungieren.|  
|**Lizenz 06A – Anzahl von Prozessoren für Produkte mit Lizenzierung pro Prozessor**|Zeigt die Anzahl der Prozessoren auf Computern an, die Microsoft-Produkte verwenden, die die Lizenzierung pro Prozessor unterstützen.|  
|**Lizenz 06B – Computer mit einem bestimmten Produkt, das die Lizenzierung pro Prozessor unterstützt**|Zeigt eine Liste der Computer, auf denen ein angegebenes Microsoft-Produkt installiert ist, das die Lizenzierung pro Prozessor unterstützt.|  
|**Lizenz 14A – Bericht zum Microsoft-Volumenlizenzabgleich**|Zeigt einen Abgleich der über den Microsoft-Volumenlizenzvertrag gekauften Softwarelizenzen und die aktuelle Anzahl von Softwarelizenzen im Inventar an.|  
|**Lizenz 14B – Liste des nicht im MVLS gefundenen Microsoft-Softwareinventars**|Dieser Bericht zeigt die verwendeten Microsoft-Softwaretitel an, die nicht im Microsoft-Volumenlizenzvertrag gefunden wurden.|  
|**Lizenz 15A – Bericht zum allgemeinen Lizenzabgleich**|Zeigt einen Abgleich der gekauften allgemeinen Softwarelizenzen und die aktuelle Anzahl von Softwarelizenzen im Inventar an.|  
|**Lizenz 15B – Bericht zum Abgleich allgemeiner Lizenzen, geordnet nach Computer**|Zeigt Computer an, auf denen das lizenzierte Produkt mit einer bestimmten Version installiert ist.|  
|**Software 01A – Zusammenfassung der in einer bestimmten Sammlung installierten Software**|Zeigt eine Zusammenfassung der installierten Software geordnet nach Anzahl der Instanzen an, die im Inventar gefunden wurde.|  
|**Software 02A – Produktfamilien für eine bestimmte Sammlung**|Zeigt die Produktfamilien und die Anzahl der Software in der Familie für eine angegebene Sammlung an.|  
|**Software 02B – Produktkategorien für eine bestimmte Produktfamilie**|Zeigt die Produktkategorien in einer angegebenen Produktfamilie und die Anzahl der Software in der Kategorie an.|  
|**Software 02C – Software in einer bestimmten Produktfamilie und Produktkategorie**|Zeigt sämtliche Software an, die sich in der angegebenen Produktfamilie und Produktkategorie befindet.|  
|**Software 02D – Computer, auf denen eine bestimmte Software installiert ist**|Zeigt alle Computer an, auf denen eine angegebene Software installiert ist.|  
|**Software 02E – Installierte Software auf einem bestimmten Computer**|Zeigt die gesamte auf einem angegebenen Computer installierte Software an.|  
|**Software 03A – Nicht kategorisierte Software**|Zeigt die Software an, die entweder als „unbekannt“ oder nicht kategorisiert ist.|  
|**Software 04A – Software, die für die automatische Ausführung auf Computern konfiguriert ist**|Zeigt eine Liste der für die automatische Ausführung auf Computern konfigurierten Software an.|  
|**Software 04B – Computer mit bestimmter Software, die für die automatische Ausführung konfiguriert ist**|Zeigt alle Computer mit angegebener Software an, die für die automatische Ausführung konfiguriert ist.|  
|**Software 04C – Software, die für die automatische Ausführung auf einem bestimmten Computer konfiguriert ist**|Zeigt die installierte Software an, die für die automatische Ausführung auf einem angegebenen Computer konfiguriert ist.|  
|**Software 05A – Browserhilfsobjekte**|Zeigt die Browserhilfsobjekte an, die auf Computern in einer angegebenen Sammlung installiert sind.|  
|**Software 05B – Computer mit einem bestimmten Browserhilfsobjekt**|Zeigt alle Computer mit einem angegebenen Browserhilfsobjekt an.|  
|**Software 05C – Browserhilfsobjekte auf einem bestimmten Computer**|Zeigt alle Browserhilfsobjekte auf einem angegebenen Computer an.|  
|**Software 06A – Suche nach installierter Software**|Dieser Bericht enthält eine Zusammenfassung der installierten Software, geordnet nach der Anzahl von Instanzen, basierend auf Suchkriterien für Produktnamen, Herausgeber oder Version.|  
|**Software 06B – Software nach Produktname**|Zeigt eine Zusammenfassung der installierten Software, geordnet nach Anzahl der Instanzen, basierend auf einem angegebenen Produktnamen an.|  
|**Software 07A – Zuletzt verwendete ausführbare Programme, geordnet nach Anzahl von Computern**|Zeigt zuletzt verwendete ausführbare Programme und die Anzahl der Computer an, auf denen sie verwendet wurden. Damit diese Website diesen Bericht anzeigen kann, muss die Softwaremessung aktiviert sein.|  
|**Software 07B – Computer, auf denen ein angegebenes ausführbares Programm zuletzt verwendet wurde**|Wenn Sie die Einstellung für den Softwaremessungsclient aktivieren, werden die Computer angezeigt, auf denen ein angegebenes ausführbares Programm zuletzt verwendet wurde.|  
|**Software 07C – Zuletzt verwendete ausführbare Programme auf einem bestimmten Computer**|Wenn Sie die Einstellung für den Softwaremessungsclient aktivieren, werden die ausführbaren Dateien angezeigt, die auf einem angegebenen Computer zuletzt verwendet wurden.|  
|**Software 08A – Zuletzt verwendete ausführbare Programme, geordnet nach Anzahl von Benutzern**|Wenn Sie die Einstellung für den Softwaremessungsclient aktivieren, werden die zuletzt verwendeten ausführbaren Programme sowie die Anzahl der sie ausführenden Benutzer angezeigt.|  
|**Software 08B – Benutzer, die ein angegebenes ausführbares Programm zuletzt verwendet haben**|Wenn Sie die Einstellung für den Softwaremessungsclient aktivieren, werden die Benutzer angezeigt, die ein angegebenes ausführbares Programm zuletzt verwendet haben.|  
|**Software 08C – Zuletzt verwendete ausführbare Programme, geordnet nach angegebenem Benutzer**|Wenn Sie die Einstellung für den Softwaremessungsclient aktivieren, werden die ausführbaren Programme angezeigt, die von einem angegebenen Benutzer zuletzt verwendet wurden.|  
|**Software 09A – Selten verwendete Software**|Zeigt die Softwaretitel an, die innerhalb eines angegebenen Zeitraums nicht verwendet wurden.|  
|**Software 09B – Computer, auf denen selten verwendete Software installiert ist**|Zeigt Computer mit installierter Software an, die innerhalb eines angegebenen Zeitraums nicht verwendet wurde. Der angegebene Zeitraum basiert auf dem im Bericht „Software 09A – Selten verwendete Software“ angegebenen Wert.|  
|**Software 10A – Softwaretitel mit mehreren spezifischen benutzerdefinierten Bezeichnungen**|Zeigt Softwaretitel an, bei denen alle Kriterien für die ausgewählten benutzerdefinierten Bezeichnungen übereinstimmen. Zum Verfeinern der Suche nach Softwaretiteln können drei benutzerdefinierte Bezeichnungen ausgewählt werden.|  
|**Software 10B – Computer, auf denen Softwaretitel mit einer bestimmten benutzerdefinierten Bezeichnung installiert sind**|Zeigt alle Computer in dieser Sammlung an, auf denen Softwaretitel mit den angegebenen benutzerdefinierten Bezeichnungen installiert sind.|  
|**Software 11A – Softwaretitel, bei denen eine bestimmte benutzerdefinierte Bezeichnung definiert ist**|Zeigt Softwaretitel an, bei denen mindestens ein Kriterium für die ausgewählten benutzerdefinierten Bezeichnungen übereinstimmt.|  
|**Software 12A – Softwaretitel ohne benutzerdefinierte Bezeichnung**|Zeigt alle Softwaretitel an, für die keine benutzerdefinierte Bezeichnung festgelegt ist.|  
|**Software 14A – Suche nach softwareerkennungstagfähiger Software**|Zeigt die Anzahl installierter Software mit aktiviertem Softwareerkennungstag an.|  
|**Software 14B – Computer, auf denen eine bestimmte softwareerkennungstagfähige Software installiert ist**|Zeigt alle Computer an, auf denen Software mit angegebenem aktivierten Softwareerkennungstag installiert ist.|  
|**Software 14C – Installierte softwareerkennungstagfähige Software auf einem bestimmten Computer**|Zeigt sämtliche installierte Software mit einem angegebenem aktivierten Softwareerkennungstag auf einem angegebenen Computer an.|  

### <a name="client-push"></a>Clientpush  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Details zum Clientpushinstallationsstatus**|Zeigt Informationen zum Clientpushinstallationsprozess für alle Standorte an.|  
|**Clientpushinstallationsstatus für einen bestimmten Standort**|Zeigt Informationen zum Clientpushinstallationsprozess für einen angegebenen Standort an.|  
|**Zusammenfassung des Clientpushinstallationsstatus**|Zeigt eine Zusammenfassungsansicht des Clientpushinstallationsstatus für alle Standorte an.|  
|**Zusammenfassung des Clientpushinstallationsstatus für einen bestimmten Standort**|Zeigt eine Zusammenfassungsansicht des Clientpushinstallationsstatus für einen angegebenen Standort an.|  

### <a name="client-status"></a>Clientstatus  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Clientwiederherstellungsdetails**|Zeigt die Wiederherstellungsdetails zu Clientaktionen für eine angegebene Sammlung an.|  
|**Clientwiederherstellungs-Zusammenfassung**|Zeigt eine Zusammenfassung zu den Clientwiederherstellungsaktionen für eine angegebene Sammlung an.|  
|**Clientstatus – Verlauf**|Zeigt eine Verlaufsansicht über den Clientstatus insgesamt am Standort an.|  
|**Clientstatus – Zusammenfassung**|Zeigt die Ergebnisse der Clientüberprüfung von aktiven Clients für eine angegebene Sammlung an.|  
|**Clientzeit zum Anfordern einer Richtlinie**|Zeigt den Prozentsatz der Clients an, von denen mindestens einmal innerhalb der letzten 30 Tage eine Richtlinie angefordert wurde. Jeder Tag stellt einen Prozentsatz der Gesamtanzahl der Clients dar, die seit dem ersten Zyklustag eine Richtlinie anforderten.|  
|**Details zu Clients mit Fehlern bei Clientprüfung**|Zeigt Details zu den Clients an, bei deren Clientüberprüfung für eine bestimmte Sammlung ein Fehler aufgetreten ist.|  
|**Details zu inaktiven Clients**|Zeigt eine detaillierte Liste der inaktiven Clients für eine angegebene Sammlung an.|  

### <a name="company-resource-access"></a>Zugriff auf Unternehmensressourcen  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Zertifikatausstellung – Verlauf**|Zeigt den Verlauf von Zertifikaten an, die vom Zertifikatregistrierungspunkt für Benutzer und Geräte für den angegebenen Zeitraum ausgestellt wurden.|  
|**Liste von Beständen nach Zertifikatausstellungsstatus**|Zeigt die Geräte oder Benutzer in einem angegebenen Zertifikatausstellungsstatus nach der Auswertung eines angegebenen Zertifikatprofils an.|  
|**Liste von Beständen mit Zertifikaten, die demnächst ablaufen**|Zeigt die Geräte oder Benutzer mit Zertifikaten an, die am oder vor dem angegebenen Datum ablaufen.|  

### <a name="compliance-and-settings-management"></a>Kompatibilitäts- und Einstellungsverwaltung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Kompatibilitätsverlauf einer Konfigurationsbaseline**|Zeigt den Kompatibilitätsverlauf einer Konfigurationsbasislinie für den angegebenen Datumsbereich an.|  
|**Kompatibilitätsverlauf eines Konfigurationselements**|Zeigt den Kompatibilitätsverlauf eines Konfigurationselements für den angegebenen Datumsbereich an.|  
|**Details zu kompatiblen Regeln von Konfigurationselementen in einer Konfigurationsbaseline für einen Bestand**|Zeigt Informationen zu den Regeln an, die als kompatibel mit einem angegebenen Konfigurationselement für ein angegebenes Gerät oder einen angegebenen Benutzer ausgewertet wurden.|  
|**Details zu konfliktverursachenden Regeln von Konfigurationselementen in einer Konfigurationsbaseline für einen Bestand**|Zeigt Informationen zu Regeln in einem Konfigurationselement an, die für einen angegebenen Benutzer oder auf einem angegebenen Gerät bereitgestellt wurden, und die mit anderen Regeln im gleichen oder einem anderen bereitgestellten Konfigurationselement in Konflikt stehen.|  
|**Details zu Fehlern von Konfigurationselementen in einer Konfigurationsbaseline für einen Bestand**|Zeigt Informationen zu Fehlern an, die durch ein angegebenes Konfigurationselement für ein angegebenes Gerät oder einen angegebenen Benutzer generiert wurden.|  
|**Details zu inkompatiblen Regeln von Konfigurationselementen in einer Konfigurationsbaseline für einen Bestand**|Zeigt Informationen zu Regeln an, die als nicht kompatibel mit einem angegebenen Konfigurationselement, einem angegebenen Gerät oder einem angegebenen Benutzer ausgewertet wurden.|  
|**Details zu wiederhergestellten Regeln von Konfigurationselementen in einer Konfigurationsbaseline für einen Bestand**|Zeigt Informationen zu Regeln an, die durch ein angegebenes Konfigurationselement für ein angegebenes Gerät oder einen angegebenen Benutzer wiederhergestellt wurden.|  
|**Liste von Beständen nach Kompatibilitätszustand für ein Konfigurationselement in einer Konfigurationsbaseline**|Zeigt die Geräte oder Benutzer an, die sich nach der Auswertung eines angegebenen Konfigurationselements in einem angegebenen Kompatibilitätszustand befinden.|  
|**Liste von Beständen nach Kompatibilitätszustand für eine Konfigurationsbaseline**|Zeigt die Geräte oder Benutzer an, die sich nach der Auswertung einer angegebenen Konfigurationsbasislinie in einem angegebenen Kompatibilitätszustand befinden.|  
|**Liste der Regeln, die mit einer angegebenen Regel für einen Bestand in Konflikt stehen**|Zeigt eine Liste der Regeln an, die mit einer angegebenen Regel für ein auf einem angegebenen Gerät bereitgestelltes Konfigurationselement in Konflikt stehen.|  
|**Liste unbekannter Bestände für eine Konfigurationsbaseline**|Zeigt eine Liste der Geräte oder Benutzer an, von denen bisher noch keine Kompatibilitätsinformationen für eine angegebene Konfigurationsbasislinie angegeben wurden.|  
|**Liste unbekannter Bestände für ein Konfigurationselement**|Zeigt eine Liste der Geräte oder Benutzer an, von denen bisher noch keine Kompatibilitätsinformationen für ein angegebenes Konfigurationselement angegeben wurden.|  
|**Zusammenfassung der Regeln und Fehler von Konfigurationselementen in einer Konfigurationsbaseline für einen Bestand**|Zeigt eine Zusammenfassung der Kompatibilitätszustände der Regeln und jeglicher Einstellungsfehler für ein angegebenes Konfigurationselement eines angegebenen Geräts oder Benutzers an.|  
|**Zusammenfassung zur Kompatibilität nach Konfigurationsbaseline**|Zeigt eine Zusammenfassung der Gesamtkompatibilität bereitgestellter Konfigurationsbasislinien in der Hierarchie an.|  
|**Zusammenfassung der Kompatibilität nach Konfigurationselementen für eine Konfigurationsbaseline**|Zeigt eine Zusammenfassung der Kompatibilität der Konfigurationselemente in einer angegebenen Konfigurationsbasislinie an.|  
|**Zusammenfassung zur Kompatibilität nach Konfigurationsrichtlinien**|Zeigt eine Zusammenfassung der Kompatibilität von Konfigurationsrichtlinien an.|  
|**Zusammenfassung zur Kompatibilität einer Konfigurationsbaseline für eine Sammlung**|Zeigt eine Zusammenfassung der Gesamtkompatibilität einer angegebenen Konfigurationsbasislinie an, die für eine bestimmte Sammlung bereitgestellt wird.|  
|**Liste der nicht kompatiblen Apps und Geräte für einen angegebenen Benutzer**|Zeigt Informationen zu Benutzern und Geräten an, die Apps installiert haben, die mit einer von Ihnen angegebenen Richtlinie nicht konform sind.|  
|**Zusammenfassung der Benutzer mit nicht kompatiblen Apps**|Zeigt Informationen zu Benutzern an, die Apps installiert haben, die mit einer von Ihnen angegebenen Richtlinie nicht konform sind.|  
|**Akzeptanz von Nutzungsbedingungen**|Zeigt Nutzungsbedingungen und die vom Benutzer akzeptierte Version hat.|  

### <a name="device-management"></a>-Geräteverwaltung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle Clients der mobilen Geräte**|Zeigt Informationen zu allen Clients für mobile Geräte an. Geräte, die vom Exchange Server-Connector verwaltet werden, sind nicht eingeschlossen.|  
|**Zertifikatsprobleme auf nicht fehlerfreien mobilen Geräten, die vom Configuration Manager-Client für Windows CE verwaltet werden**|Zeigt detaillierte Informationen zu Zertifikatsproblemen auf mobilen Geräten an, die vom Configuration Manager-Client für Windows CE verwaltet werden.|  
|**Client-Bereitstellungsfehler auf mobilen Geräten, die vom Configuration Manager-Client für Windows CE verwaltet werden**|Zeigt detaillierte Informationen zu Bereitstellungsfehlern auf mobilen Geräten an, die vom Configuration Manager-Client für Windows CE verwaltet werden|  
|**Details zum Status der Client-Bereitstellung auf mobilen Geräten, die vom Configuration Manager-Client für Windows CE verwaltet werden**|Zeigt Informationen zum Status der mobilen Geräte an, die vom Configuration Manager-Client für Windows CE verwaltet werden|  
|**Erfolgreiche Client-Bereitstellung auf mobilen Geräten, die vom Configuration Manager-Client für Windows CE verwaltet werden**|Zeigt detaillierte Informationen zur erfolgreichen Bereitstellung auf mobilen Geräten an, die vom Configuration Manager-Client für Windows CE verwaltet werden|  
|**Kommunikationsprobleme auf nicht fehlerfreien mobilen Geräten, die vom Configuration Manager-Client für Windows CE verwaltet werden**|Dieser Bericht enthält detaillierte Informationen zu Kommunikationsproblemen auf mobilen Geräten, die vom Configuration Manager-Client für Windows CE verwaltet werden.|  
|**Kompatibilitätsstatus für mobile Geräte, die vom Exchange Server-Connector verwaltet werden**|Zeigt eine Zusammenfassung des Kompatibilitätsstatus mit der Standard-Exchange ActiveSync-Postfachrichtlinie für mobile Geräte an, die vom Exchange Server-Connector verwaltet werden.|  
|**Anzahl von mobilen Geräten nach Anzeigekonfigurationen**|Dieser Bericht enthält die Anzahl der mobilen Geräte nach Anzeigeeinstellungen.|  
|**Anzahl von mobilen Geräten nach Betriebssystem**|Zeigt die Anzahl der mobilen Geräte nach Betriebssystem an.|  
|**Anzahl von mobilen Geräten nach Programmspeicher**|Zeigt die Anzahl der mobilen Geräte nach Programmspeicher an.|  
|**Anzahl von mobilen Geräte nach Konfiguration des Wechselmedienspeichers**|Anzahl der mobilen Geräte nach Konfiguration des Wechselmedienspeichers|  
|**Integritätsinformationen für mobile Geräte, die vom Configuration Manager-Client für Windows CE verwaltet werden**|Zeigt Integritätsinformationen für mobile Geräte an, die vom Configuration Manager-Client für Windows CE verwaltet werden|  
|**Integritätszusammenfassung für mobile Geräte, die vom Configuration Manager-Client für Windows CE verwaltet werden**|Zeigt Integritätsinformationen für mobile Geräte an, die vom Configuration Manager-Client für Windows CE verwaltet werden|  
|**Inaktive mobile Geräte, die vom Exchange Server-Connector verwaltet werden**|Zeigt eine Liste der von Exchange Server-Connector verwalteten mobilen Geräte an, von denen in der angegebenen Anzahl von Tagen keine Verbindung mit Exchange Server hergestellt wurde.|  
|**Liste der pro Benutzer in Microsoft Intune registrierten Geräte**|Zeigt alle Geräte an, die ein Benutzer mit Microsoft Intune registriert hat|  
|**Liste der Geräte nach bedingtem Zugriffsstatus**|Zeigt Informationen zum aktuellen Kompatibilitätszustand und bedingten Zugriffsstatus von Geräten an. Sie können diesen Bericht mit Richtlinien für den bedingten Zugriff verwenden. Dieser Bericht steht ab Version 1602 von Configuration Manager zur Verfügung.|  
|**Kompatibilität mit bedingtem Zugriff für Benutzer**|Stellt detaillierte Kompatibilitätsinformationen zum bedingten Zugriff für einen bestimmten Benutzer bereit, einschließlich Gerätename und Plattform, ob das Gerät kompatibel ist und wann das Gerät zuletzt bewertet wurde. Dieser Bericht steht ab Version 1602 von Configuration Manager zur Verfügung.|  
|**Probleme lokaler Clients auf nicht fehlerfreien mobilen Geräten, die vom Configuration Manager-Client für Windows CE verwaltet werden**|Dieser Bericht enthält detaillierte Informationen zu Problemen lokaler Clients auf mobilen Geräten, die vom Configuration Manager-Client für Windows CE verwaltet werden.|  
|**Clientinformationen des mobilen Geräts**|Zeigt Informationen zu mobilen Geräten an, auf denen der Configuration Manager-Client installiert ist Sie können mithilfe dieses Berichts überprüfen, welche mobilen Geräte erfolgreich mit einem Verwaltungspunkt kommunizieren können.|  
|**Kompatibilitätsdetails der mobilen Geräte für den Exchange Server-Connector**|Zeigt die Kompatibilitätsdetails der mobilen Geräte für eine Standard-Exchange ActiveSync-Postfachrichtlinie an, die mithilfe des Exchange Server-Connectors konfiguriert wurde.|  
|**Mobile Geräte nach Betriebssystem**|Zeigt die mobilen Geräte nach Betriebssystem an.|  
|**Mobile Geräte, die ein Jailbreak aufweisen oder ein Stammgerät sind**|Zeigt die mobilen Geräte an, die ein Jailbreak aufweisen oder ein Stammgerät sind.|  
|**Nicht verwaltete mobile Geräte, die zwar angemeldet sind, aber keinem Standort zugewiesen wurden**|Zeigt die mobilen Geräte an, deren Registrierung bei Configuration Manager abgeschlossen ist und die über ein Zertifikat verfügen, bei deren Standortzuweisung jedoch ein Fehler aufgetreten ist|  
|**Mobile Geräte, die über den angegebenen freien Programmspeicher verfügen**|Zeigt alle mobilen Geräte mit ihren angegebenem freien Programmspeicher an.|  
|**Mobile Geräte, die über den angegebenen freien Wechselmedienspeicher verfügen**|Zeigt alle mobilen Geräte mit dem angegebenen freien Wechselmedienspeicher an.|  
|**Mobile Geräte mit Problemen bei der Zertifikatserneuerung**|Zeigt die Liste angemeldeter mobiler Geräte mit Fehlern bei der Zertifikatserneuerung an. Wenn das Zertifikat nicht vor dem Ablaufdatum erneuert wird, werden die mobilen Geräte nicht verwaltet.|  
|**Mobile Geräte mit nicht genügend verfügbarem Programmspeicher (weniger freie KB als angegeben)**|Zeigt eine Liste mobiler Geräte an, deren Programmspeicher kleiner als die in KB angegebene Größe ist.|  
|**Mobile Geräte mit nicht genügend verfügbarem Wechselmedienspeicher (weniger freie KB als angegeben)**|Zeigt eine Liste mobiler Geräte an, deren Wechselmedienspeicher kleiner als die in KB angegebene Größe ist.|  
|**Anzahl der pro Benutzer in Windows Intune registrierten Geräte**|Dieser Bericht enthält die Benutzer mit Microsoft Intune-Abonnement und die Anzahl der pro Benutzer insgesamt registrierten Geräte.|  
|**Ausstehende Anforderungen zum Zurücksetzen mobiler Geräte**|Zeigt die Anforderungen zum Zurücksetzen an, die für mobile Geräte ausstehen.|  
|**Vor Kurzem angemeldete und zugewiesene mobile Geräte**|Zeigt eine Liste mobiler Geräte an, die kürzlich bei Configuration Manager angemeldet und einem Standort erfolgreich zugewiesen wurden|  
|**Zuletzt zurückgesetzte mobile Geräte**|Zeigt die Liste der mobilen Geräte an, die zuletzt erfolgreich zurückgesetzt wurden.|  
|**Zusammenfassung der Einstellungen für mobile Geräte, die vom Exchange Server-Connector verwaltet werden**|Zeigt die Anzahl der mobilen Geräte an, von denen die Einstellungen für jede vom Exchange Server-Connector verwaltete Standard-ActiveSync-Postfachrichtlinie angewendet werden.|  
|**Statusdetails zu Windows RT-Sideload-Schlüsseln**|Zeigt ausführliche Statusinformationen für einen angegebenen Windows RT-Sideload-Schlüssel an.|  
|**Zusammenfassung zu Windows RT-Sideload-Schlüsseln**|Zeigt den Status von Windows RT-Sideload-Schlüsseln an.|  

### <a name="driver-management"></a>Treiberverwaltung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle Treiber**|Zeigt eine Liste aller Treiber an.|  
|**Alle Treiber für eine bestimmte Plattform**|Zeigt alle Treiber für eine bestimmte Plattform an.|  
|**Alle Treiber in einem bestimmten Startimage**|Zeigt alle Treiber in einem angegebenen Startabbild an.|  
|**Alle Treiber einer bestimmten Kategorie**|Zeigt alle Treiber in einer angegebenen Kategorie an.|  
|**Alle Treiber in einem bestimmten Paket**|Zeigt alle Treiber in einem angegebenen Paket an.|  
|**Kategorien für einen bestimmten Treiber**|Zeigt Kategorien für einen angegebenen Treiber an.|  
|**Computer, auf denen Treiber für eine bestimmte Sammlung nicht installiert werden konnten**|Zeigt Computer an, auf denen Treiber für eine angegebene Sammlung nicht installiert werden konnten.|  
|**Bericht über Treiberkatalogabgleich für eine bestimmte Sammlung**|Zeigt den Bericht über Treiberkatalogabgleich für eine angegebene Sammlung an.|  
|**Bericht über Treiberkatalogabgleich für einen bestimmten Computer**|Zeigt den Bericht über Treiberkatalogabgleich für einen angegebenen Computer an.|  
|**Bericht über Treiberkatalogabgleich für ein bestimmtes Gerät auf einem bestimmten Computer**|Zeigt den Bericht über Treiberkatalogabgleich für ein angegebenes Gerät auf einem angegebenen Computer an.|  
|**Bericht über Treiberkatalogabgleich für Computer in einer bestimmten Sammlung mit einem bestimmten Gerät**|Zeigt den Bericht über Treiberkatalogabgleich für Computer in einer angegebenen Sammlung mit einem angegebenen Gerät an.|  
|**Treiber, die auf einem bestimmten Computer nicht installiert werden konnten**|Zeigt Treiber an, die auf einem angegebenen Computer nicht installiert werden konnten.|  
|**Unterstützte Plattformen für einen bestimmten Treiber**|Zeigt unterstützte Plattformen für einen angegebenen Treiber an.|  

### <a name="endpoint-protection"></a>Endpoint Protection  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Aktivitätsbericht für Antischadsoftware**|Zeigt eine Übersicht über die Antischadsoftware-Aktivität an.|  
|**Gesamtstatus und Verlauf der Antischadsoftware**|Zeigt den Gesamtstatus und Verlauf der Antischadsoftware an.|  
|**Details zur Schadsoftware auf dem Computer**|Zeigt Details zu einem angegebenen Computer und die Liste der Schadsoftware an, die darauf gefunden wurde.|  
|**Infizierte Computer**|Zeigt eine Liste von Computern an, auf denen eine angegebene Bedrohung erkannt wurde.|  
|**Benutzer nach häufigsten Bedrohungen**|Zeigt die Liste der Benutzer mit der höchsten Anzahl an erkannten Bedrohungen an.|  
|**Benutzerspezifische Bedrohungsliste**|Zeigt die Liste der erkannten Bedrohungen für ein angegebenes Benutzerkonto an.|  

### <a name="hardware---cd-rom"></a>Hardware – CD-ROM  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**CD-ROM-Informationen für einen bestimmten Computer**|Zeigt Informationen zu den CD-ROM-Laufwerken eines angegebenen Computers an.|  
|**Computer für einen bestimmten CD-ROM-Hersteller**|Zeigt eine Liste der Computer an, die ein CD-ROM-Laufwerk enthalten, das von einem angegebenen Hersteller stammt.|  
|**Anzahl von CD-ROM-Laufwerken nach Hersteller**|Zeigt die Anzahl der pro Hersteller inventarisierten CD-ROM-Laufwerke an.|  
|**Verlauf – CD-ROM-Verlauf für einen bestimmten Computer**|Zeigt den Inventarverlauf für CD-ROM-Laufwerke eines angegebenen Computers an.|  

### <a name="hardware---disk"></a>Hardware – Datenträger  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Computer mit einer bestimmten Festplattengröße**|Zeigt eine Liste von Computern an, die mit Festplatten mit einer angegebenen Größe ausgestattet sind.|  
|**Computer mit wenig verfügbarem Speicherplatz (weniger als die angegebenen % frei)**|Zeigt eine Liste der Computer in einer angegebenen Sammlung an, die über weniger als den angegebenen freien Speicherplatz verfügen.|  
|**Computer mit wenig verfügbarem Speicherplatz (weniger als die angegebenen MB frei)**|Zeigt eine Liste von Computern und Datenträgern an, bei denen wenig freier Datenträgerspeicherplatz vorhanden ist. Die zu überprüfende Größe des verfügbaren Speicherplatzes ist in Prozent der Datenträgerkapazität angegeben.|  
|**Konfigurationen physischer Datenträger zählen**|Zeigt die Anzahl der inventarisierten Festplatten nach Kapazität an.|  
|**Datenträgerinformationen für einen bestimmten Computer – logische Datenträger**|Zeigt zusammenfassende Informationen zu den logischen Datenträgern auf einem angegebenen Computer an.|  
|**Datenträgerinformationen für einen bestimmten Computer – Partitionen**|Zeigt zusammenfassende Informationen zu den Datenträgerpartitionen auf einem angegebenen Computer an.|  
|**Datenträgerinformationen für einen bestimmten Computer – physische Datenträger**|Zeigt zusammenfassende Informationen zu den physischen Datenträgern auf einem angegebenen Computer an.|  
|**Verlauf – Verlauf des Speicherplatzes auf logischen Datenträgern für einen bestimmten Computer**|Zeigt den Inventarverlauf für logische Datenträger eines angegebenen Computers an.|  

### <a name="hardware---general"></a>Hardware – Allgemein  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Computerinformationen für einen bestimmten Computer**|Zeigt zusammenfassende Informationen zu einem angegebenen Computer an.|  
|**Computer in einer bestimmten Arbeitsgruppe oder Domäne**|Zeigt eine Liste der Computer in einer angegebenen Arbeitsgruppe oder Domäne an.|  
|**Einer bestimmten Sammlung zugewiesene Inventarklassen**|Zeigt die Inventarklassen an, die einer angegebenen Sammlung zugewiesen sind.|  
|**Für einen bestimmten Computer aktivierte Inventarklassen**|Zeigt die Inventarklassen an, die auf einem angegebenen Computer aktiviert sind.|  

### <a name="hardware---memory"></a>Hardware – Arbeitsspeicher  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Computer, bei denen sich der physische Speicher geändert hat**|Zeigt eine Liste von Computern an, bei denen sich seit dem letzten Inventurzyklus die Größe des Arbeitsspeichers geändert hat.|  
|**Computer mit einer bestimmten Speichergröße**|Zeigt eine Liste von Computern mit der angegebenen RAM-Größe (gesamter physischer Speicher gerundet auf MB) an.|  
|**Computer mit wenig Arbeitsspeicher (kleiner oder gleich angegebene MB)**|Zeigt eine Liste von Computern an, die über wenig Arbeitsspeicher verfügen. Die zu überprüfende Größe des Arbeitsspeichers ist in MB angegeben.|  
|**Arbeitsspeicherkonfigurationen zählen**|Zeigt die Anzahl der inventarisierten Computer nach Größe des Arbeitsspeichers an.|  
|**Arbeitsspeicherinformationen für einen bestimmten Computer**|Zeigt zusammenfassende Informationen zum Arbeitsspeicher auf einem angegebenen Computer an.|  

### <a name="hardware---modem"></a>Hardware – Modem  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Computerinformationen für einen bestimmten Modemhersteller**|Zeigt eine Liste von Computern an, die mit einem Modem eines angegebenen Herstellers ausgestattet sind.|  
|**Modems nach Hersteller zählen**|Zeigt die Anzahl der für jeden Modemhersteller inventarisierten Modems an.|  
|**Modeminformationen für einen bestimmten Computer**|Zeigt zusammenfassende Informationen zum Modem auf einem angegebenen Computer an.|  

### <a name="hardware---network-adapter"></a>Hardware – Netzwerkkarte  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Computer mit einer bestimmten Netzwerkkarte**|Zeigt eine Liste von Computern an, die mit einer angegebenen Netzwerkkarte ausgestattet sind.|  
|**Netzwerkkarten nach Typ zählen**|Zeigt die Anzahl der inventarisierten Netzwerkkarten für die einzelnen Typen an.|  
|**Netzwerkkarteninformationen für einen bestimmten Computer**|Zeigt Informationen zu den in einem angegebenen Computer installierten Netzwerkkarten an.|  

### <a name="hardware---processor"></a>Hardware – Prozessor  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Computer mit einer bestimmten Prozessorgeschwindigkeit**|Zeigt eine Liste von Computern an, die mit einem Prozessor mit der angegebenen Geschwindigkeit ausgestattet sind.|  
|**Computer mit schnellen Prozessoren (Taktfrequenz größer oder gleich der angegebenen)**|Zeigt eine Liste von Computern an, die mit Prozessoren mit einer Geschwindigkeit ausgestattet sind, die schneller als die angegebene Geschwindigkeit ist.|  
|**Computer mit langsamen Prozessoren (Taktfrequenz kleiner oder gleich der angegebenen)**|Zeigt eine Liste von Computern an, die mit Prozessoren ausgestattet sind, die mit der angegebenen Taktfrequenz oder langsamer arbeiten.|  
|**Prozessorgeschwindigkeiten zählen**|Zeigt die Anzahl von inventarisierten Computern nach Prozessorgeschwindigkeit an.|  
|**Prozessorinformationen für einen bestimmten Computer**|Zeigt Informationen zu den in einem angegebenen Computer installierten Prozessoren an.|  

### <a name="hardware---scsi"></a>Hardware – SCSI  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Computer mit einem bestimmten SCSI-Kartentyp**|Zeigt eine Liste von Computern an, in denen eine angegebene SCSI-Karte installiert ist.|  
|**SCSI-Kartentypen zählen**|Zeigt die Anzahl der inventarisierten SCSI-Karten nach Kartentyp an.|  
|**SCSI-Karteninformationen für einen bestimmten Computer**|Zeigt Informationen zu den in einem angegebenen Computer installierten SCSI-Karten an.|  

### <a name="hardware---sound-card"></a>Hardware – Soundkarte  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Computer mit einer bestimmten Soundkarte**|Zeigt eine Liste von Computern an, die mit einer angegebenen Soundkarte ausgestattet sind.|  
|**Soundkarten zählen**|Zeigt die Anzahl von inventarisierten Computern nach Soundkartentyp an.|  
|**Soundkarteninformationen für einen bestimmten Computer**|Zeigt zusammenfassende Informationen zur Soundkarte eines angegebenen Computers an.|  

### <a name="hardware---video-card"></a>Hardware – Grafikkarte  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Computer mit einer bestimmten Grafikkarte**|Zeigt eine Liste von Computern an, die mit einer angegebenen Grafikkarte ausgestattet sind.|  
|**Grafikkarten nach Typ zählen**|Zeigt eine Liste aller in Computern installierter Grafikkarten sowie die Anzahl der einzelnen Grafikkartentypen an.|  
|**Grafikkarteninformationen für einen bestimmten Computer**|Zeigt Informationen zu den in einem angegebenen Computer installierten Grafikkarten an.|  

### <a name="migration"></a>Migration  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Clients in der Ausschlussliste**|Zeigt die von der Migration ausgeschlossenen Clients an.|  
|**Abhängigkeit von einer Configuration Manager-Sammlung**|Zeigt die Objekte an, die von einer Sammlung der Quellhierarchie abhängen.|  
|**Eigenschaften des Migrationsauftrags**|Dieser Bericht zeigt die Inhalte eines angegebenen Migrationsauftrags an.|  
|**Migrationsaufträge**|Dieser Bericht zeigt die Liste der Migrationsaufträge an.|  
|**Objekte mit Fehlern beim Migrieren**|Zeigt die Liste der Objekte an, die beim letzten Versuch nicht migriert werden konnten.|  

### <a name="network"></a>Netzwerk  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**IP-Adressen nach Subnetz zählen**|Zeigt die Anzahl der für die einzelnen IP-Subnetze inventarisierten IP-Adressen an.|  
|**IP – Alle Subnetze nach Subnetzmaske**|Zeigt eine Liste von IP-Subnetzen und Subnetzmasken an.|  
|**IP – Computer in einem bestimmten Subnetz**|Zeigt eine Liste von Computern und IP-Informationen für ein angegebenes IP-Subnetz an.|  
|**IP – Informationen für einen bestimmten Computer**|Zeigt zusammenfassende IP-Informationen zu einem angegebenen Computer an.|  
|**IP – Informationen für eine bestimmte IP-Adresse**|Zeigt zusammenfassende Informationen zu einer angegebenen IP-Adresse an.|  
|**MAC – Computer für eine bestimmte MAC-Adresse**|Zeigt den Computernamen und die IP-Adresse der Computer mit der angegebenen MAC-Adresse an.|  

### <a name="network-access-protection"></a>Netzwerkzugriffsschutz  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Vergleich der installierten Softwareupdates, geordnet nach Softwareupdatebereitstellung und NAP-Wiederherstellung**|Zeigt eine vergleichende Zusammenfassung über die von der Softwareupdatebereitstellung und der NAP-Wiederherstellung installierten Softwareupdates an.|  
|**Anzahl der an einem Computer durchgeführten Wiederherstellungen innerhalb eines bestimmten Zeitraums**|In diesem Bericht wird angegeben, wie häufig ein Computer in einem angegebenen Zeitraum wiederhergestellt wurde.|  
|**Liste der Computer, auf denen innerhalb eines bestimmten Zeitraums im Rahmen der Wiederherstellung ein bestimmtes Softwareupdate installiert wurde**|Zeigt die Computer an, auf denen innerhalb eines bestimmten Zeitraums (Tage) im Rahmen der Wiederherstellung ein angegebenes Softwareupdate installiert wurde.|  
|**Liste der Computer, die basierend auf den ausgewählten Softwareupdates als nicht kompatibel zu betrachten sind**|Zeigt die einzelnen Computer an, die basierend auf den ausgewählten Softwareupdates als nicht kompatibel zu betrachten sind.|  
|**Liste von Computern, auf denen der NAP-Dienst nicht erkannt wurde**|Zeigt eine Liste von Computern an, auf denen der NAP-Dienst nicht erkannt wurde.|  
|**Liste von Computern, die NAP unterstützen**|Zeigt eine Liste der Computer an, auf denen der NAP-Dienst nicht ausgeführt wird oder auf denen sein Status unbekannt ist.|  
|**Liste der NAP-Richtlinien**|Zeigt eine Liste von NAP-Richtlinien mit ihren Gültigkeitsdaten an.|  
|**Liste der nicht kompatiblen Computer, die seit dem letzten Abrufintervall wiederhergestellt wurden**|Zeigt eine Liste nicht kompatibler, wiederhergestellter Computer mit dem Zeitpunkt der jeweils letzten bekannten Auswertung an.|  
|**Liste der nicht kompatiblen Computer, die innerhalb eines angegebenen Zeitraums wiederhergestellt wurden**|Zeigt eine Liste von nicht kompatiblen Computern an, die innerhalb eines angegebenen Zeitraums wiederhergestellt wurden.|  
|**Liste der Fehler bei der Wiederherstellung innerhalb eines bestimmten Zeitraums**|Zeigt eine Liste der Fehler bei der Wiederherstellung für eine angegebene Anzahl von Tagen an.|  
|**Liste der im Rahmen der Wiederherstellung installierten Softwareupdates**|Zeigt die Softwareupdates an, die im Rahmen der Wiederherstellung für einen angegebenen Zeitraum installiert wurden.|  
|**Zusammenfassung der nicht kompatiblen Computer, die seit dem letzten Abrufintervall wiederhergestellt wurden**|Zeigt eine Zusammenfassung von nicht kompatiblen Computern an, die seit dem letzten Abrufintervall wiederhergestellt wurden.|  
|**Zusammenfassung der nicht kompatiblen Computer, die innerhalb eines bestimmten Zeitraums wiederhergestellt wurden**|Zeigt eine Zusammenfassung der nicht kompatiblen Computer an, die innerhalb eines angegebenen Zeitraums wiederhergestellt wurden.|  

### <a name="operating-system"></a>Betriebssystem  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Verlauf – Version des Computerbetriebssystems**|Zeigt den Inventurverlauf für das Betriebssystem eines angegebenen Computers an.|  
|**Computer mit einem bestimmten Betriebssystem**|Zeigt Computer mit einem angegebenen Betriebssystem an.|  
|**Computer mit einem bestimmten Betriebssystem und Service Pack**|Zeigt Computer mit einem angegebenen Betriebssystem und Service Pack an.|  
|**Betriebssystemversionen zählen**|Zeigt die Anzahl von inventarisierten Computern nach Betriebssystem an.|  
|**Betriebssysteme und Service Packs zählen**|Zeigt die Anzahl von inventarisierten Computern nach Kombination von Betriebssystem und Service Pack an.|  
|**Dienste – Computer, auf denen ein bestimmter Dienst ausführt wird**|Zeigt eine Liste der Computer an, auf denen ein angegebener Dienst ausgeführt wird.|  
|**Dienste – Computer, auf denen RAS-Server ausgeführt wird**|Zeigt eine Liste der Computer an, auf denen RAS-Server ausführt wird.|  
|**Dienste – Diensteinformationen für einen bestimmten Computer**|Zeigt zusammenfassende Informationen zu den Diensten auf einem angegebenen Computer an.|  
|**Windows Server-Computer**|Zeigt eine Liste der Computer an, auf denen Windows Server-Betriebssysteme ausgeführt werden.|  

### <a name="out-of-band-management"></a>Out-of-Band-Verwaltung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Computer mit Out-of-Band-Verwaltungscontrollern**|Zeigt eine Liste von Computern an, auf denen sich Out-of-Band-Verwaltungscontroller befinden.|  
|**Aktivität der Out-of-Band-Verwaltungskonsole**|Zeigt eine Liste von Statusmeldungen für die Aktivität der Out-of-Band-Verwaltungskonsole an.|  
|**Bereitstellungsstatus zur Out-of-Band-Verwaltung von Clients**|Zeigt eine Liste von Computern an, die für die Out-of-Band-Verwaltung bereitgestellt wurden.|  

### <a name="power-management"></a>Energieverwaltung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Energieverwaltung – Computeraktivität**|Zeigt die Monitor-, Computer- und Benutzeraktivität einer angegebenen Sammlung innerhalb eines angegebenen Zeitraums in Diagrammform an.|  
|**Energieverwaltung – Computeraktivität nach Computer**|Zeigt die Monitor-, Computer und Benutzeraktivität für einen angegebenen Computer an einem angegebenen Datum in Diagrammform an.|  
|**Energieverwaltung – Computeraktivitätsdetails**|Zeigt eine Liste der Standby- und Aktivierungsfunktionen von Computern einer angegebenen Sammlung zu einem angegebenen Zeitpunkt (Datum und Uhrzeit) an.|  
|**Energieverwaltung – Computerdetails**|Zeigt detaillierte Informationen zu Energiesparfunktionen, -einstellungen und -plänen eines angegebenen Computers an.|  
|**Energieverwaltung – Computer meldet keine Details**|Zeigt eine Liste von Computern ohne jegliche Energieaktivität für einen angegebenen Zeitpunkt (Datum und Uhrzeit) an.|  
|**Energieverwaltung – Ausgeschlossene Computer**|Zeigt eine Liste von Computern an, die vom Energiesparplan ausgeschlossen wurden.|  
|**Energieverwaltung – Computer mit mehreren Energiesparplänen**|Zeigt eine Liste von Computern an, auf denen mehrere in Konflikt stehende Energieeinstellungen angewendet werden.|  
|**Energieverwaltung – Stromverbrauch**|Zeigt den monatlichen Gesamtstromverbrauch einer bestimmten Sammlung während eines bestimmten Zeitraums (in kWh) an.|  
|**Energieverwaltung – Stromverbrauch nach Tag**|Zeigt den monatlichen Gesamtstromverbrauch einer angegebenen Sammlung für die letzten 31 Tage (in kWh) an.|  
|**Energieverwaltung – Stromkosten**|Zeigt die monatlichen Gesamtstromverbrauchskosten einer bestimmten Sammlung für einen angegebenen Zeitraum an.|  
|**Energieverwaltung – Stromkosten nach Tag**|Zeigt die Gesamtstromkosten einer angegebenen Sammlung während der letzten 31 Tage an.|  
|**Energieverwaltung – Umweltbelastung**|Zeigt die durch eine bestimmte Sammlung während eines bestimmten Zeitraums erzeugte Kohlendioxidemission (CO2) in Form eines Diagramms an.|  
|**Energieverwaltung – Umweltbelastung nach Tag**|Zeigt die durch eine bestimmte Sammlung während der letzten 31 Tage erzeugte Kohlendioxidemission (CO2) in Form eines Diagramms an.|  
|**Energieverwaltung – Störungsdetails für Computer**|Zeigt detaillierte Informationen zu Computern an, für die während eines bestimmten Zeitraums weder Standbymodus noch Ruhezustand aktiviert wurde.|  
|**Energieverwaltung – Störungsbericht**|Zeigt eine Liste der häufigsten Ursachen an, deretwegen für Computer weder der Standbymodus noch der Ruhezustand aktiviert werden konnte, sowie die Anzahl von Computern, die für einen angegebenen Zeitraum von den jeweiligen Ursachen betroffen waren.|  
|**Energieverwaltung – Energiefunktionen**|Zeigt die Energieverwaltungsfunktionen von Computern in der angegebenen Sammlung an.|  
|**Energieverwaltung – Energieeinstellungen**|Zeigt eine aggregierte Liste aller Energieeinstellungen an, die von Computern in einer angegebenen Sammlung verwendet werden.|  
|**Energieverwaltung – Energieeinstellungsdetails**|Zeigt weitere Informationen zu Computern an, die im Bericht **Energieverwaltung – Energieeinstellungen** angegeben wurden.|  

### <a name="replication-traffic"></a>Replikationsdatenverkehr  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Replikationsdatenverkehr für globale Daten je Verbindung (Liniendiagramm)**|Zeigt den gesamten Replikationsdatenverkehr für globale Daten für eine angegebene Verbindung für eine angegebene Anzahl von Tagen an.|  
|**Replikationsdatenverkehr für globale Daten je Verbindung (Kreisdiagramm)**|Zeigt den gesamten Replikationsdatenverkehr für globale Daten für eine angegebene Verbindung für eine angegebene Anzahl von Tagen an.|  
|**Replikationsdatenverkehr in der Hierarchie je Verbindung**|Zeigt den gesamten Replikationsdatenverkehr für jede Verbindung in der Hierarchie für eine angegebene Anzahl von Tagen an.|  
|**Datenverkehr für die zehn wichtigsten Replikationsgruppen in der Hierarchie je Verbindung (Kreisdiagramm)**|Zeigt den Replikationsdatenverkehr für die zehn wichtigsten Replikationsgruppen in der gesamten Hierarchie an, ermittelt nach Verbindung.|  
|**Replikationsdatenverkehr für Verbindung**|Zeigt den gesamten Replikationsdatenverkehr für alle Daten für eine angegebene Anzahl von Tagen an.|  
|**Datenverkehr für Replikationsgruppe je Verbindung**|Zeigt den Netzwerkdatenverkehr für Replikationsgruppen über eine angegebene Datenbankreplikationsverbindung für eine angegebene Anzahl von Tagen an.|  
|**Replikationsdatenverkehr für Standortdaten je Verbindung (Liniendiagramm)**|Zeigt den gesamten Replikationsdatenverkehr für Standortdaten für eine angegebene Verbindung für eine angegebene Anzahl von Tagen an.|  
|**Replikationsdatenverkehr für Standortdaten je Verbindung (Kuchendiagramm)**|Zeigt den gesamten Replikationsdatenverkehr für Standortdaten für eine angegebene Verbindung für eine angegebene Anzahl von Tagen an.|  
|**Replikationsdatenverkehr in der Hierarchie gesamt (Liniendiagramm)**|Zeigt die summierte globale und standortbezogene Datenreplikation für jede Richtung und für jede Verbindung in der Hierarchie für eine angegebene Anzahl von Tagen an.|  
|**Replikationsdatenverkehr in der Hierarchie gesamt (Kreisdiagramm)**|Zeigt die summierte globale und standortbezogene Datenreplikation für jede Richtung und für jede Verbindung in der Hierarchie für eine angegebene Anzahl von Tagen an.|  

### <a name="site---client-information"></a>Standort – Clientinformationen  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Detaillierter Statusbericht zur Clientzuweisung**|Zeigt ausführliche Informationen zum Clientzuweisungsstatus an.|  
|**Details zu Fehlern bei der Clientzuweisung**|Zeigt ausführliche Informationen zu Fehlern bei der Clientzuweisung an.|  
|**Details zum Clientzuweisungsstatus**|Zeigt eine Übersicht über den Clientzuweisungsstatus an.|  
|**Details zur erfolgreichen Clientzuweisung**|Zeigt ausführliche Informationen zu erfolgreich zugewiesenen Clients an.|  
|**Bericht über Fehler bei der Clientbereitstellung**|Zeigt detaillierte Informationen für Clients an, die nicht bereitgestellt werden konnten.|  
|**Details zum Clientbereitstellungsstatus**|Zeigt zusammenfassende Informationen zum Status von Clientinstallationen an.|  
|**Bericht zur erfolgreichen Clientbereitstellung**|Zeigt ausführliche Informationen für Clients an, die erfolgreich bereitgestellt wurden.|  
|**Clients, die die HTTPS-Kommunikation nicht unterstützen**|Zeigt detaillierte Informationen zu jedem Client eines Standorts an, von dem nach dem Ausführen des Programms zur Überprüfung der HTTPS-Kommunikation gemeldet wurde, dass die Kommunikation über HTTPS nicht unterstützt wird.|  
|**Computer, die einem bestimmten Standort zugeordnet, aber nicht dort installiert sind**|Zeigt eine Liste von Computern an, die einem bestimmten Standort zugewiesen wurden, aber nicht an den Standort berichten.|  
|**Computer mit einer bestimmten Configuration Manager-Clientversion**|Zeigt eine Liste von Computern an, auf denen eine einzelne angegebene Version der Configuration Manager-Clientsoftware ausgeführt wird.|  
|**Anzahl der Clients und für die Kommunikation verwendeten Protokolle**|Zeigt eine Zusammenfassung der von Clients verwendeten Kommunikationsmethoden (HTTP oder HTTPS) an.|  
|**Anzahl der zugeordneten und installierten Clients für jeden Standort**|Zeigt die Anzahl der zugeordneten und installierten Computer für jeden Standort an. Clients mit einem Netzwerkpfad, der mehreren Standorten zugeordnet ist, werden nur als installiert gezählt, wenn von ihnen an den betreffenden Standort Bericht erstattet wird.|  
|**Anzahl der Clients, die die Kommunikation über HTTPS unterstützen**|Zeigt detaillierte Informationen zu jedem Client eines Standorts an, von dem nach dem Ausführen des Programms zur Überprüfung der HTTPS-Kommunikation gemeldet wurde, ob die Kommunikation über HTTPS unterstützt wird.|  
|**Anzahl der Clients für jeden Standort**|Zeigt die Anzahl von installierten Configuration Manager-Clients nach Standortcode an|  
|**Anzahl der Configuration Manager-Clients nach Clientversionen**|Zeigt die Anzahl der ermittelten Computer nach Configuration Manager-Clientversion an|  
|**Details zu Problemen einer bestimmten Sammlung, die dem Fallbackstatuspunkt gemeldet wurden**|Zeigt detaillierte Informationen über die Probleme an, die von Clients in einer bestimmten Sammlung gemeldet wurden, wenn diese einem Fallbackstatuspunkt zugewiesen wurden.|  
|**Details zu Problemen eines bestimmten Standorts, die dem Fallbackstatuspunkt gemeldet wurden**|Zeigt detaillierte Informationen über die Probleme an, die von Clients eines bestimmten Standorts gemeldet wurden, wenn diese einem Fallbackstatuspunkt zugewiesen wurden.|  
|**Zusammenfassung der Probleme, die dem Fallbackstatuspunkt gemeldet wurden**|Zeigt Informationen über alle Probleme an, die von Clients gemeldet wurden, wenn diese einem Fallbackstatuspunkt zugewiesen wurden.|  
|**Zusammenfassung der Probleme einer bestimmten Sammlung, die dem Fallbackstatuspunkt gemeldet wurden**|Zeigt zusammenfassende Informationen über die Probleme an, die von Clients in einer bestimmten Sammlung gemeldet wurden, wenn diese einem Fallbackstatuspunkt zugewiesen wurden.|  

### <a name="site---discovery-and-inventory-information"></a>Standort – Ermittlungs- und Inventarinformationen  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Clients, von denen in letzter Zeit (innerhalb einer angegebenen Anzahl von Tagen) kein Bericht gesendet wurde**|Zeigt eine Liste von Clients an, für die in der angegebenen Anzahl von Tagen keine Ermittlungsdaten oder Hardware- und Softwareinventuren gemeldet wurden.|  
|**Ermittelte Computer nach bestimmtem Standort**|Zeigt eine Liste aller von einem bestimmten Standort ermittelten Computer und das Datum der letzten Ermittlung an.|  
|**Computer, die vor Kurzem ermittelt wurden, nach Ermittlungsmethode**|Zeigt eine Liste von Computern an, die in der angegebenen Anzahl von Tagen ermittelt wurden, zusammen mit den Agents, durch die sie ermittelt wurden. Wenn ein Computer von mehreren Agents ermittelt wurde, wird er möglicherweise mehrmals in der Liste angezeigt.|  
|**Computer, die in letzter Zeit nicht ermittelt wurden (Anzahl von Tagen)**|Zeigt eine Liste von Computern an, die in letzter Zeit nicht ermittelt worden sind, sowie die Anzahl der Tage seit ihrer letzten Ermittlung.|  
|**Computer, die in letzter Zeit nicht inventarisiert wurden (Anzahl von Tagen)**|Zeigt eine Liste von Computern an, die in letzter Zeit nicht inventarisiert worden sind, sowie die Zeitpunkte ihrer letzten Inventarisierung.|  
|**Computer, deren eindeutige Configuration Manager-Kennungen möglicherweise übereinstimmen**|Zeigt eine Liste von Computern an, deren Namen geändert wurden. Eine Namensänderung kann z.B. bedeuten, dass die eindeutigen Configuration Manager-Bezeichner für zwei Computer übereinstimmen.|  
|**Computer mit doppelten MAC-Adressen**|Zeigt Computer an, die sich eine MAC-Adresse teilen.|  
|**Anzahl von Computern in Ressourcendomänen oder Arbeitsgruppen**|Zeigt die Anzahl der Computer in den einzelnen Ressourcendomänen oder Arbeitsgruppen an.|  
|**Ermittlungsinformationen für einen bestimmten Computer**|Zeigt eine Liste aller Agents und Standorte an, die einen angegebenen Computer ermittelt haben.|  
|**Inventurdaten für einen bestimmten Computer**|Zeigt das Datum und die Uhrzeit für die letzte Ausführung einer Inventur auf einem angegebenen Computer an.|  

### <a name="site---general"></a>Standort – Allgemein  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Computer an einem bestimmten Standort**|Zeigt eine Liste der Computer an einem angegebenen Standort an.|  
|**Standortstatus für die Hierarchie**|Zeigt die Liste der Standorte in der Hierarchie mit Standortversion und Standortstatusinformationen an.|  
|**Status des Configuration Manager-Updates innerhalb der Hierarchie**|Zeigt Informationen zu Configuration Manager-Standortupdates für die Hierarchie an|  

### <a name="site---server-information"></a>Standort – Serverinformationen  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Standortsystemrollen und -server für einen bestimmten Standort**|Zeigt eine Liste der Standortsystemserver und ihrer Standortsystemrollen für einen angegebenen Standort an.|  

### <a name="software---companies-and-products"></a>Software – Unternehmen und Produkte  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle inventarisierten Produkte für ein bestimmtes Softwareunternehmen**|Zeigt eine Liste der inventarisierten Softwareprodukte und -versionen für ein angegebenes Softwareunternehmen an.|  
|**Alle Softwareunternehmen**|Zeigt eine Liste aller Herstellerunternehmen der inventarisierten Software an.|  
|**Alle Windows-Apps**|Zeigt eine Zusammenfassung der installierten Windows-Apps an, geordnet nach der Anzahl von Instanzen, basierend auf Suchkriterien für Anwendungsnamen, Architektur oder Herausgeber.|  
|**Computer mit einem bestimmten Produkt**|Zeigt eine Liste von Computern an, auf denen ein angegebenes Produkt inventarisiert ist, sowie die Versionen des Produkts.|  
|**Computer mit bestimmten Produktnamen und bestimmter Produktversion**|Zeigt eine Liste von Computern an, auf denen eine angegebene Version eines Produkts inventarisiert ist.|  
|**Computer, bei denen eine bestimmte Software unter „Software“ registriert ist**|Zeigt eine Zusammenfassung aller Computer mit der angegebenen Software an, die unter „Software“ oder „Programme und Features“ registriert ist.|  
|**Alle inventarisierten Produkte und Versionen zählen**|Zeigt eine Liste von inventarisierten Softwareprodukten und -versionen sowie die Anzahl von Computern an, auf denen sie jeweils installiert sind.|  
|**Inventarisierte Produkte und Versionen für ein bestimmtes Produkt zählen**|Zeigt eine Liste von inventarisierten Versionen eines angegebenen Produkts sowie die Anzahl von Computern an, auf denen sie jeweils installiert sind.|  
|**Alle Instanzen der Software zählen, die unter „Software“ registriert ist**|Zeigt eine Zusammenfassung aller Instanzen, der mit „Software“ oder „Programme und Features“ installierten und registrierten Software auf Computern in der angegebenen Sammlung an.|  
|**Instanzen einer bestimmten Software zählen, die unter „Software“ registriert ist**|Zeigt die Anzahl der Instanzen für die angegebenen Softwarepakete an, die über „Software“ oder „Programme und Features“ installiert und registriert wurden.|  
|**Installationen bestimmter Windows-Apps**|Dieser Bericht listet alle Computer mit einer angegebenen Windows-App auf.|  
|**Produkte auf einem bestimmten Computer**|Zeigt eine Zusammenfassung der inventarisierten Softwareprodukte und ihrer Hersteller auf einem angegebenen Computer an.|  
|**Software, die unter „Software“ auf einem bestimmten Computer registriert ist**|Zeigt eine Zusammenfassung der auf einem angegebenen Computer installierten Software an, die über „Software“ oder „Programme und Features“ registriert wurde.|  
|**Für den angegebenen Benutzer installierte Windows-Apps**|Zeigt alle für den angegebenen Benutzer installierten Windows-Apps an.|  

### <a name="software---files"></a>Software – Dateien  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle inventarisierten Dateien für ein bestimmtes Produkt**|Zeigt eine Zusammenfassung der inventarisierten Dateien an, die einem angegebenen Softwareprodukt zugeordnet sind.|  
|**Alle inventarisierten Dateien für einen bestimmten Computer**|Zeigt eine Zusammenfassung aller Dateien an, die auf einem angegebenen Computer inventarisiert sind.|  
|**Softwareinventar auf zwei Computern vergleichen**|Zeigt die Unterschiede zwischen dem Softwareinventar, das für zwei angegebene Computer gemeldet wurde.|  
|**Computer mit einer bestimmten Datei**|Zeigt eine Liste von Computern an, die Softwareinventar für einen angegebenen Dateinamen erfasst haben. Wenn ein Computer mehrere Kopien der Datei enthält, wird er möglicherweise mehrmals in der Liste angezeigt.|  
|**Computer mit einem bestimmten Dateinamen zählen**|Zeigt eine Liste von Computern an, die Softwareinventar für eine angegebene Datei erfasst haben.|  

### <a name="software-distribution---application-monitoring"></a>Softwareverteilung – Anwendungsüberwachung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle Anwendungsbereitstellungen (erweitert)**|Zeigt eine ausführliche Zusammenfassung für alle Anwendungsbereitstellungen an.|  
|**Alle Anwendungsbereitstellungen (Standard)**|Zeigt eine Zusammenfassung für alle Anwendungsbereitstellungen an.|  
|**Anwendungskompatibilität**|Zeigt Kompatibilitätsinformationen für die angegebene Anwendung in der angegebenen Sammlung an.|  
|**Anwendungsbereitstellungen pro Bestand**|Zeigt Anwendungen an, die auf einem angegebenen Gerät oder für einen angegebenen Benutzer bereitgestellt wurden.|  
|**Anwendungsinfrastrukturfehler**|Zeigt Anwendungsinfrastrukturfehler an.  Diese können interne Infrastrukturfehler sowie Fehler aufgrund ungültiger Anforderungsregeln umfassen.|  
|**Detaillierter Status der Anwendungsverwendung**|Zeigt Nutzungsdetails zu installierten Anwendungen an.|  
|**Statusübersicht der Anwendungsverwendung**|Zeigt eine Nutzungszusammenfassung für installierte Anwendungen an.|  
|**Tasksequenzbereitstellungen mit Anwendung**|Zeigt Tasksequenzbereitstellungen an, die eine angegebene Anwendung installieren.|  
|**Android-Anwendungsanforderungen durch Benutzer**|Zeigt die Benutzer an, die die Installation einer Android-Anwendung angefordert haben.|  
|**iOS-Apps mit Bereitstellungsfehlern (App bereits installiert)**|Zeigt Kompatibilitätsinformationen für die ausgewählte iOS-App an, die Sie als "App-Paket für iOS aus dem App-Store" bereitgestellt haben, das mit einer Verwaltungsrichtlinie für mobile Anwendungen verknüpft wurde. In diesem Bericht werden Benutzer und Geräte angezeigt, für die die App nicht installiert werden konnte, weil sie vom Benutzer bereits manuell installiert wurde.|  

### <a name="software-distribution---collections"></a>Softwareverteilung – Sammlungen  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle Sammlungen**|Zeigt alle Sammlungen in der Hierarchie an.|  
|**Alle Ressourcen in einer bestimmten Sammlung**|Zeigt alle Ressourcen in einer angegebenen Sammlung an.|  
|**Für einen angegebenen Client verfügbare Wartungsfenster**|Zeigt alle Wartungsfenster an, die für den angegebenen Client gelten.|  

### <a name="software-distribution---content"></a>Softwareverteilung – Inhalt  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle aktiven Inhaltsverteilungen**|Zeigt alle Verteilungspunkte an, auf denen zurzeit Inhalte installiert oder entfernt werden.|  
|**Alle Inhalte**|Zeigt alle Anwendungen und Pakete an einem Standort an.|  
|**Gesamter Inhalt auf einem bestimmten Verteilungspunkt**|Zeigt alle Inhalte an, die zurzeit auf einem angegebenen Verteilungspunkt installiert sind.|  
|**Alle Verteilungspunkte**|Zeigt Informationen zu den Verteilungspunkten für die einzelnen Standorte an.|  
|**Alle Statusmeldungen für ein bestimmtes Paket auf einem bestimmten Verteilungspunkt**|Zeigt alle Statusmeldungen für ein angegebenes Paket auf einem angegebenen Verteilungspunkt an.|  
|**Status der Anwendungsinhaltsverteilung**|Zeigt Informationen zum Verteilungsstatus für Anwendungsinhalte an.|  
|**Anwendungen, die auf die Verteilungspunktgruppe gerichtet sind**|Zeigt Informationen zum Anwendungsinhalt an, der auf einer angegebenen Verteilungspunktgruppe bereitgestellt wurde.|  
|**Nicht mit der angegebenen Verteilungspunktgruppe synchronisierte Anwendungen**|Zeigt die Anwendungen an, für die zugehörige Inhaltsdateien auf einer angegebenen Verteilungspunktgruppe nicht mit der neuesten Version aktualisiert wurden.|  
|**Verteilungspunktgruppe**|Zeigt Informationen zu einer angegebenen Verteilungspunktgruppe an.|  
|**Zusammenfassung zur Verteilungspunktnutzung**|Zeigt die Zusammenfassung zur Verteilungspunktnutzung für die einzelnen Verteilungspunkte an.|  
|**Verteilungsstatus des angegebenen Pakets**|Zeigt den Verteilungsstatus des angegebenen Paketinhalts für die einzelnen Verteilungspunkte an.|  
|**Pakete, die auf die Verteilungspunktgruppe gerichtet sind**|Zeigt Informationen zu Paketen an, die auf eine angegebene Verteilungspunktgruppe ausgerichtet sind.|  
|**Nicht mit der angegebenen Verteilungspunktgruppe synchronisierte Pakete**|Zeigt Pakete an, für die zugehörige Inhaltsdateien auf einer angegebenen Verteilungspunktgruppe nicht mit der neuesten Version aktualisiert wurden.|  

### <a name="software-distribution---package-and-program-deployment"></a>Softwareverteilung – Paket- und Programmbereitstellung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle Bereitstellungen für ein angegebenes Paket bzw. Programm**|Zeigt Informationen zu allen Bereitstellungen für ein angegebenes Paket bzw. Programm an.|  
|**Alle Paket- und Programmbereitstellungen**|Zeigt alle Paket- und Programmbereitstellungen für diesen Standort an.|  
|**Alle Paket- und Programmbereitstellungen für eine angegebene Sammlung**|Zeigt alle Paket- und Programmbereitstellungen für eine angegebene Sammlung an.|  
|**Alle Paket- und Programmbereitstellungen für einen angegebenen Computer**|Zeigt alle Paket- und Programmbereitstellungen an, die für einen angegebenen Computer gelten.|  
|**Alle Paket- und Programmbereitstellungen des angegebenen Benutzers**|Zeigt alle Paket- und Programmbereitstellungen des angegebenen Benutzers an.|  

### <a name="software-distribution---package-and-program-deployment-status"></a>Softwareverteilung – Status der Paket- und Programmbereitstellung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle Paket- und Programmbereitstellungen für Systemressourcen mit Status**|Zeigt alle Paket- und Programmbereitstellungen für den Standort mit einer Statusübersicht für die einzelnen Bereitstellungen an.|  
|**Alle Systemressourcen für eine angegebene Paket- und Programmbereitstellung in einem angegebenen Zustand**|Zeigt eine Liste von Ressourcen an, die einen angegebenen Zustand für eine angegebene Paket- und Programmbereitstellung aufweisen.|  
|**Diagramm – Status über abgeschlossene stündliche Paket- und Programmbereitstellungen**|Zeigt den Prozentsatz der Computer an, die das Paket in jeder Stunde seit der Erstellung der Paket- und Programmbereitstellung erfolgreich installiert haben. Dieser kann dazu verwendet werden, die durchschnittliche Zeit für eine Paket- und Programmbereitstellung zu verfolgen.|  
|**Status der Paket- und Programmbereitstellung für einen angegebenen Client und eine angegebene Bereitstellung**|Zeigt die Statusmeldungen an, die für einen angegebenen Computer und eine angegebene Paket- und Programmbereitstellung gemeldet wurden.|  
|**Status einer angegebenen Paket- und Programmbereitstellung**|Zeigt die Statusübersicht für eine angegebene Paket- und Programmbereitstellung an.|  

### <a name="software-metering"></a>Softwaremessung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle auf diesen Standort angewendeten Softwaremessungsregeln**|Zeigt eine Liste aller auf diesen Standort angewendeten Softwaremessungsregeln an.|  
|**Computer, auf denen ein gemessenes Programm installiert ist, das aber seit dem angegebenen Datum nicht mehr ausgeführt wurde**|Zeigt alle Computer an, auf denen gemäß der Meldung des Softwareinventars eine gemessene Anwendung installiert ist, die aber seit dem angegebenen Datum nicht ausgeführt wurde.|  
|**Computer, die ein bestimmtes gemessenes Softwareprogramm ausgeführt haben**|Zeigt eine Liste von Computern an, die Programme innerhalb des angegebenen Monats und Jahrs ausgeführt haben, die der angegebenen Softwaremessungsregel entsprechen.|  
|**Gleichzeitige Verwendung für alle gemessenen Softwareprogramme**|Zeigt die maximale Anzahl von Benutzern an, die während des angegebenen Monats und Jahrs das jeweilige gemessene Softwareprogramm gleichzeitig ausgeführt haben.|  
|**Trendanalyse der gleichzeitigen Verwendung eines bestimmten gemessenen Softwareprogramms**|Zeigt die maximale Anzahl von Benutzern an, die in jedem Monat des vergangenen Jahres das angegebene gemessene Softwareprogramm gleichzeitig ausgeführt haben.|  
|**Installationsbasis für alle gemessenen Softwareprogramme**|Zeigt die Anzahl der Computer an, auf denen gemäß des Softwareinventars gemessene Softwareprogramme installiert sind. Dieser Bericht setzt voraus, dass das Softwareinventar auf den gemessenen Computern erfasst wird.|  
|**Status des Zusammenfassungsvorgangs der Softwaremessung**|Zeigt den Zeitpunkt an, an dem die zuletzt zusammengefassten Messungsdaten auf dem Standortserver verarbeitet wurden.  Nur die vor diesen Datumsangaben verarbeiteten Messungsdaten werden in den Berichten zur Softwaremessung berücksichtigt.|  
|**Zusammenfassung Tageszeit der Verwendung eines bestimmten gemessenen Softwareprogramms**|Zeigt die durchschnittliche Anzahl von Verwendungen eines bestimmten Programms in den vergangenen 90 Tagen an, aufgeschlüsselt nach Stunde und Tag.|  
|**Gesamtverwendung für alle gemessenen Softwareprogramme**|Zeigt die Anzahl von Benutzern an, die während des angegebenen Monats und Jahrs Programme lokal oder über Terminaldienste ausgeführt haben, die allen Softwaremessungsregeln entsprechen.|  
|**Gesamtverwendung für alle gemessenen Softwareprogramme auf Windows-Terminalservern**|Zeigt die Anzahl von Benutzern an, die während des angegebenen Monats und Jahrs Programme über Terminaldienste ausgeführt haben, die allen Softwaremessungsregeln entsprechen.|  
|**Trendanalyse der Gesamtverwendung eines bestimmten gemessenen Softwareprogramms**|Zeigt die Anzahl von Benutzern an, die jeden Monat während des vergangenen Jahrs Programme lokal oder über Terminaldienste ausgeführt haben, die der angegebenen Softwaremessungsregel entsprechen.|  
|**Trendanalyse der Gesamtverwendung eines bestimmten gemessenen Softwareprogramms auf Windows-Terminalservern**|Zeigt die Anzahl von Benutzern an, die jeden Monat während des vergangenen Jahrs Programme über Terminaldienste ausgeführt haben, die der angegebenen Softwaremessungsregel entsprechen.|  
|**Benutzer, die ein bestimmtes gemessenes Softwareprogramm ausgeführt haben**|Zeigt eine Liste von Benutzern an, die Programme innerhalb des angegebenen Monats und Jahrs ausgeführt haben, die der angegebenen Softwaremessungsregel entsprechen.|  

### <a name="software-updates---a-compliance"></a>Softwareupdates – A Kompatibilität  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Kompatibilität 1 – Gesamtkompatibilität**|Zeigt die Gesamtkompatibilitätsinformationen zu einer Softwareupdategruppe an.|  
|**Kompatibilität 2 – Bestimmtes Softwareupdate**|Zeigt die Kompatibilitätsinformationen bezüglich eines angegebenen Softwareupdates an.|  
|**Kompatibilität 3 – Updategruppe (pro Update)**|Zeigt die Kompatibilitätsinformationen bezüglich eines in einer Softwareupdategruppe definierten Softwareupdates an.|  
|**Kompatibilität 4 – Updates geordnet nach Hersteller/Monat/Jahr**|Zeigt die Kompatibilitätsdaten für Softwareupdates an, die von einem Hersteller in einem angegebenen Monat und Jahr veröffentlicht wurden.|  
|**Kompatibilität 5 – Bestimmter Computer**|In diesem Bericht werden die Kompatibilitätsdaten eines Softwareupdates für einen angegebenen Computer angezeigt.  Wenn Sie die Anzahl der angezeigten Informationen begrenzen möchten, können Sie die Hersteller- und Softwareupdateklassifikation angeben.|  
|**Kompatibilität 6 – Bestimmte Softwareupdatezustände (sekundär)**|Zeigt die Anzahl und den Prozentsatz aller Computer für die jeweiligen Kompatibilitätszustände für das angegebene Softwareupdate an.|  
|**Kompatibilität 7 – Computer in einem bestimmten Kompatibilitätszustand für eine Updategruppe (sekundär)**|Zeigt alle Computer in einer Sammlung an, die einen angegebenen Gesamtkompatibilitätszustand für eine Softwareupdategruppe aufweisen.|  
|**Kompatibilität 8 – Computer in einem bestimmten Kompatibilitätszustand bezüglich eines Updates (sekundär)**|Zeigt alle Computer in einer Sammlung an, die einen angegebenen Kompatibilitätszustand für ein Softwareupdate aufweisen.|  

### <a name="software-updates---b-deployment-management"></a>Softwareupdates – B Bereitstellungsverwaltung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Verwaltung 1 – Bereitstellungen einer Updategruppe**|Zeigt alle Bereitstellungen an, die alle in einer angegebenen Softwareupdategruppe definierten Softwareupdates enthalten.|  
|**Verwaltung 2 – Erforderliche, aber nicht bereitgestellte Updates**|Zeigt alle herstellerspezifischen Softwareupdates an, die auf Clients als erforderlich ermittelt, jedoch nicht für eine angegebene Sammlung bereitgestellt wurden.|  
|**Verwaltung 3 – Updates in einer Bereitstellung**|Zeigt die Softwareupdates an, die in einer angegebenen Bereitstellung enthalten sind.|  
|**Verwaltung 4 – Bereitstellungen für eine Sammlung**|Zeigt alle Softwareupdatebereitstellungen an, die auf eine angegebene Sammlung ausgerichtet sind.|  
|**Verwaltung 5 – Bereitstellungen für einen Computer**|Zeigt alle Softwareupdatebereitstellungen an, die auf einem angegebenen Computer bereitgestellt werden.|  
|**Verwaltung 6 – Bereitstellungen mit einem bestimmten Update**|Zeigt alle Bereitstellungen an, die ein angegebenes Softwareupdate und die zugehörige Zielsammlung für die Bereitstellung enthalten.|  
|**Verwaltung 7 – Updates in einer Bereitstellung mit fehlendem Inhalt**|Zeigt die Softwareupdates in einer angegebenen Bereitstellung an, für die nicht alle erforderlichen Inhalte abgerufen wurden, sodass Clients das Update nicht installieren konnten und somit keine hundertprozentige Kompatibilität für die Bereitstellung erreicht wurde.|  
|**Verwaltung 8 – Computer mit fehlendem Inhalt (sekundär)**|Zeigt alle Computer an, die ein angegebenes Softwareupdate erfordern, das in einer bestimmten Bereitstellung enthalten ist, die an einem Verteilungspunkt nicht bereitgestellt wurde.|  

### <a name="software-updates---c-deployment-states"></a>Softwareupdates – C Bereitstellungszustände  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Zustände 1 – Erzwingungszustände für eine Bereitstellung**|Zeigt die Erzwingungszustände für eine angegebene Softwareupdatebereitstellung an, normalerweise die zweite Phase einer Bereitstellungsbewertung.|  
|**Zustände 2 – Bewertungszustände für eine Bereitstellung**|Zeigt den Bewertungszustand für eine angegebene Softwareupdatebereitstellung an, normalerweise die erste Phase einer Bereitstellungsbewertung.|  
|**Zustände 3 – Zustände für Bereitstellung und Computer**|Zeigt die Zustände aller Softwareupdates der angegebenen Bereitstellung für einen angegebenen Computer an.|  
|**Zustände 4 – Computer in einem bestimmten Zustand für eine Bereitstellung (sekundär)**|Zeigt alle Computer in einem bestimmten Zustand für eine Softwareupdatebereitstellung an.|  
|**Zustände 5 – Zustände für ein Update in einer Bereitstellung (sekundär)**|Zeigt eine Zustandszusammenfassung für ein bestimmtes Softwareupdate an, das für eine angegebene Bereitstellung vorgesehen ist.|  
|**Zustände 6 – Computer in einem bestimmten Erzwingungszustand für ein Update (sekundär)**|Zeigt alle Computer in einem angegebenen Erzwingungszustand für ein angegebenes Softwareupdate an.|  

### <a name="software-updates---d-scan"></a>Softwareupdates – D Überprüfung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Überprüfung 1 – Letzte Überprüfungszustände, geordnet nach Sammlung**|Zeigt die Anzahl der Computer für eine angegebene Sammlung in den jeweiligen Kompatibilitätsüberprüfungszuständen an, die von Clients während der letzten Kompatibilitätsüberprüfung zurückgegeben wurden.|  
|**Überprüfung 2 – Letzte Überprüfungszustände, geordnet nach Standort**|Zeigt die einem Standort zugeordnete Anzahl der Computer in den jeweiligen Kompatibilitätsüberprüfungszuständen an, die von Clients während der letzten Kompatibilitätsüberprüfung zurückgegeben wurden.|  
|**Überprüfung 3 – Clients einer Sammlung, die einen bestimmten Zustand melden (sekundär)**|Zeigt alle Computer für eine angegebene Sammlung und einen angegebenen Kompatibilitätsüberprüfungszustand während der letzten Kompatibilitätsüberprüfung an.|  
|**Überprüfung 4 – Clients eines Standorts, die einen bestimmten Zustand melden (sekundär)**|Zeigt alle einem angegebenen Standort zugeordneten Computer mit einem angegebenen Kompatibilitätsüberprüfungszustand während der letzten Kompatibilitätsüberprüfung an.|  

### <a name="software-updates---e-troubleshooting"></a>Softwareupdates – E Problembehandlung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Problembehandlung 1 – Überprüfungsfehler**|Zeigt die Überprüfungsfehler am Standort sowie die Anzahl der von den einzelnen Fehlern betroffenen Computer an.|  
|**Problembehandlung 2 – Bereitstellungsfehler**|Zeigt die Bereitstellungsfehler am Standort sowie die Anzahl der von den einzelnen Fehlern betroffenen Computer an.|  
|**Problembehandlung 3 – Computer mit einem bestimmten Überprüfungsfehler (sekundär)**|Zeigt eine Liste der Computer an, bei denen eine Überprüfung aufgrund eines angegebenen Fehlers nicht erfolgreich ausgeführt werden konnte.|  
|**Problembehandlung 4 – Computer mit einem bestimmten Bereitstellungsfehler (sekundär)**|Zeigt eine Liste der Computer an, auf denen die Bereitstellung des Updates aufgrund einer angegebenen Fehlers nicht erfolgreich ausgeführt werden konnte.|  

### <a name="state-migration"></a>Zustandsmigration  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Zustandsmigrationsinformationen für einen bestimmten Quellcomputer**|Zeigt Zustandsmigrationsinformationen für einen angegebenen Computer an.|  
|**Zustandsmigrationsinformationen für einen bestimmten Zustandsmigrationspunkt**|Zeigt Zustandsmigrationsinformationen für einen angegebenen Zustandsmigrationspunkt an.|  
|**Zustandsmigrationspunkte für einen bestimmten Standort**|Zeigt Zustandsmigrationspunkte für einen angegebenen Standort an.|  

### <a name="status-messages"></a>Statusmeldungen  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle Meldungen mit einer bestimmten Meldungs-ID**|Zeigt eine Liste der Statusmeldungen an, die eine angegebene Meldungs-ID aufweisen.|  
|**Clients, die in letzten 12 Stunden Fehler für einen bestimmten Standort gemeldet haben**|Zeigt eine Liste von Computern und Komponenten, die in den letzten 12 Stunden Fehler gemeldet haben, und die Anzahl der gemeldeten Fehler an.|  
|**Komponentenmeldungen der letzten 12 Stunden**|Zeigt eine Liste der Komponentenmeldungen der letzten 12 Stunden für einen angegebenen Standortcode, einen Computer und eine Komponente an.|  
|**Komponentenmeldungen in der letzten Stunde**|Zeigt eine Liste der Statusmeldungen an, die in der letzten Stunde durch eine angegebene Komponente auf einem angegebenen Computer an einem angegebenen Configuration Manager-Standort erstellt wurden|  
|**Komponentenmeldungen in der letzten Stunde für einen bestimmten Standort zählen**|Zeigt die Anzahl der in der letzten Stunde an einem angegebenen Standort gemeldeten Komponentenmeldungen nach Komponente sowie den Schweregrad an.|  
|**Fehler der letzten 12 Stunden zählen**|Zeigt die Anzahl von Fehlerstatusmeldungen für Serverkomponenten in den letzten 12 Stunden an.|  
|**Schwerwiegende Fehler (nach Komponente)**|Zeigt eine nach Komponenten sortierte Liste von Computern mit schwerwiegenden Fehlern an.|  
|**Schwerwiegende Fehler (nach Computername)**|Zeigt eine nach Computernamen sortierte Liste von Computern mit schwerwiegenden Fehlern an.|  
|**Die letzten 1000 Meldungen für einen bestimmten Computer (Fehler und Warnungen)**|Zeigt eine Zusammenfassung der letzten 1000 Komponentenstatusmeldungen (Fehler und Warnungen) für einen angegebenen Computer an.|  
|**Die letzten 1000 Meldungen für einen bestimmten Computer (Fehler-, Warn- und Informationsmeldungen)**|Zeigt eine Zusammenfassung der letzten 1000 Komponentenstatusmeldungen (Fehler-, Warn- und Informationsmeldungen) für einen angegebenen Computer an.|  
|**Die letzten 1000 Meldungen für einen bestimmten Computer (Fehler)**|Zeigt eine Zusammenfassung der letzten 1000 Statusmeldungen (Fehler) der Serverkomponente für einen angegebenen Computer an.|  
|**Die letzten 1000 Meldungen für eine bestimmte Serverkomponente**|Zeigt eine Zusammenfassung der letzten 1000 Statusmeldungen für eine angegebene Serverkomponente an.|  

### <a name="status-messages---audit"></a>Status Messages – Überwachung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle Überwachungsmeldungen für einen bestimmten Benutzer**|Zeigt eine Zusammenfassung aller Überwachungsstatusmeldungen für einen angegebenen Benutzer an. Überwachungsmeldungen beschreiben die Aktionen, die in der Configuration Manager-Konsole ausgeführt werden und Objekte in Configuration Manager hinzufügen, ändern oder löschen.|  
|**Remotesteuerung – Alle Computer, die von einem bestimmten Benutzer remote gesteuert werden**|Zeigt eine Zusammenfassung der Statusmeldungen an, die eine Remotesteuerung von Clientcomputern durch einen angegebenen Benutzer anzeigen.|  
|**Remotesteuerung – Alle Remotesteuerungsinformationen**|Zeigt eine Zusammenfassung der Statusmeldungen an, die sich auf die Remotesteuerung von Clientcomputern beziehen.|  

### <a name="task-sequence---deployment-status"></a>Tasksequenz – Bereitstellungsstatus  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle Systemressourcen für eine Tasksequenzbereitstellung in einem bestimmten Zustand**|Zeigt eine Liste der Zielcomputer für die angegebene Tasksequenzbereitstellung in einem angegebenen Bereitstellungszustand an.|  
|**Alle Systemressourcen für eine Tasksequenzbereitstellung, die sich in einem bestimmten Zustand befindet und die für unbekannte Computer verfügbar ist**|Zeigt eine Liste der Zielcomputer für die angegebene Tasksequenzbereitstellung an, die sich im angegebenen Bereitstellungszustand befindet.|  
|**Anzahl der Systemressourcen, denen Tasksequenzbereitstellungen zugewiesen sind, die aber noch nicht ausgeführt wurden**|Zeigt die Anzahl der Computer an, die Tasksequenzen akzeptiert, aber noch nicht ausgeführt haben.|  
|**Verlauf einer Tasksequenzbereitstellung auf einem Computer**|Zeigt den Status der einzelnen Schritte der angegebenen Tasksequenzbereitstellung auf dem angegebenen Zielcomputer an. Wenn kein Datensatz zurückgegeben wird, wurde die Tasksequenz nicht auf dem Computer gestartet.|  
|**Liste der Computer, die bei der Ausführung einer Tasksequenzbereitstellung einen bestimmten Zeitraum überschritten haben**|Zeigt die Liste der Zielcomputer an, die die angegebene Zeitdauer zum Ausführen einer Tasksequenz überschritten haben.|  
|**Laufzeit einer bestimmten Tasksequenzbereitstellung auf einem bestimmten Zielcomputer**|Zeigt die zum erfolgreichen Abschließen einer angegebenen Tasksequenz auf einem angegebenen Computer erforderliche Gesamtzeit an.|  
|**Laufzeit jedes Schritts einer Tasksequenzbereitstellung auf einem bestimmten Zielcomputer**|Zeigt die zum Abschließen der einzelnen Schritte der angegebenen Tasksequenzbereitstellung auf dem angegebenen Zielcomputer erforderliche Zeit an.|  
|**Status einer bestimmten Tasksequenzbereitstellung für einen bestimmten Computer**|Zeigt die Statuszusammenfassung für eine angegebene Tasksequenzbereitstellung auf einem angegebenen Computer an.|  
|**Status einer Tasksequenzbereitstellung auf einem unbekannten Zielcomputer**|Zeigt den Status der angegebenen Tasksequenzbereitstellung auf dem angegebenen unbekannten Zielcomputer an.|  
|**Statuszusammenfassung für eine bestimmte Tasksequenzbereitstellung**|Zeigt eine Statuszusammenfassung für alle Ressourcen an, die Ziel einer Bereitstellung sind.|  
|**Statuszusammenfassung einer bestimmten Tasksequenzbereitstellung, die für unbekannte Computer verfügbar ist**|Zeigt die Statuszusammenfassung für alle Ressourcen an, die Ziel einer angegebenen Bereitstellung sind, die für eine Sammlung zur Verfügung steht, die unbekannte Computer enthält.|  

### <a name="task-sequence---deployments"></a>Tasksequenz – Bereitstellungen  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle Systemressourcen, die sich derzeit in einer bestimmten Gruppe oder Phase einer bestimmten Tasksequenzbereitstellung befinden**|Zeigt eine Liste aller Computer an, die aktuell in einer angegebenen Gruppe oder Phase einer angegebenen Tasksequenzbereitstellung ausgeführt werden.|  
|**Alle Systemressourcen mit Fehlern bei der Tasksequenzbereitstellung in einer bestimmten Gruppe oder Phase**|Zeigt eine Liste der Computer mit Fehlern in einer angegebenen Gruppe/Phase der angegebenen Tasksequenzbereitstellung an.|  
|**Alle Tasksequenzbereitstellungen**|Zeigt Details zu allen Tasksequenzbereitstellungen an, die vom aktuellen Standort initiiert wurden.|  
|**Alle für unbekannte Computer verfügbaren Tasksequenzbereitstellungen**|Zeigt Details zu allen Tasksequenzbereitstellungen an, die vom Standort initiiert und in Sammlungen bereitgestellt wurden, die unbekannte Computer enthalten.|  
|**Anzahl von Fehlern in jeder Phase oder Gruppe einer bestimmten Tasksequenz**|Zeigt die Anzahl von Fehlern in jeder Phase oder Gruppe einer angegebenen Tasksequenz an.|  
|**Anzahl von Fehlern in jeder Phase oder Gruppe einer bestimmten Tasksequenzbereitstellung**|Zeigt die Anzahl von Fehlern in jeder Phase oder Gruppe der angegebenen Tasksequenzbereitstellung an.|  
|**Bereitstellungsstatus aller Tasksequenzbereitstellungen**|Zeigt den Gesamtstatus aller Tasksequenzbereitstellungen an.|  
|**Status einer ausgeführten Tasksequenz**|Zeigt den Status der angegebenen Tasksequenz an.|  
|**Status einer ausgeführten Tasksequenzbereitstellung**|Zeigt die zusammenfassenden Informationen für die angegebene Tasksequenzbereitstellung an.|  
|**Status alle Bereitstellungen für eine bestimmte Tasksequenz**|Zeigt den Status aller Bereitstellungen für die angegebene Tasksequenz an.|  
|**Zusammenfassung zu einer Tasksequenzbereitstellung**|Zeigt die zusammenfassenden Informationen für die angegebene Tasksequenzbereitstellung an.|  

### <a name="task-sequence---progress"></a>Tasksequenz – Status  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Diagramm – Wöchentlicher Status einer Tasksequenz**|Zeigt den wöchentlichen Status einer Tasksequenz an, beginnend ab dem Bereitstellungsdatum.|  
|**Status einer Tasksequenz**|Zeigt den Status der angegebenen Tasksequenz an.|  
|**Status aller Tasksequenzen**|Zeigt eine Zusammenfassung zum Status aller Tasksequenzen an.|  
|**Status von Tasksequenzen für Betriebssystembereitstellungen**|Zeigt den Status aller Tasksequenzen an, die Betriebssysteme bereitstellen.|  
|**Status aller unbekannten Computer**|Zeigt eine Liste der zum Zeitpunkt der Ausführung einer Tasksequenzbereitstellung unbekannten Computer sowie die Information an, ob es sich jetzt um bekannte Computer handelt.|  

### <a name="task-sequences---references"></a>Tasksequenzen – Verweise  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Inhalt, auf den von einer bestimmten Tasksequenz verwiesen wird**|Zeigt Inhalt an, auf den von einer angegebenen Tasksequenz verwiesen wird.|  

### <a name="upgrade-assessment"></a>Upgradebewertung  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Anwendungsstatus für einen bestimmten Computer**|Zeigt die Kompatibilität von Anwendungen, die für ein angegebenes Betriebssystem auf einem Computer installiert werden.|  
|**Anwendungsstatus für Computer in einer bestimmten Sammlung**|Zeigt den Gesamtstatus für Computer in einer Sammlung an. Hiermit können Sie basierend auf den Anwendungen auf den jeweiligen Computern bewerten, wie für diese Computer ein Upgrade durchgeführt werden soll. Mithilfe des Berichts können Sie ermitteln, auf welchen Computern kompatible Anwendungen vorhanden sind, bevor Sie ein Betriebssystem bereitstellen.|  
|**Anwendungsstatuszusammenfassung**|Zeigt eine Zusammenfassung des Anwendungsstatus für ein angegebenes Betriebssystem an. Mithilfe dieses Berichts können Sie die Anwendungskompatibilität ermitteln, bevor Sie ein Betriebssystem bereitstellen.|  
|**Computer, auf denen eine bestimmte Anwendung installiert ist**|Zeigt Computer an, auf denen eine bestimmte Anwendung installiert ist.|  
|**Computer mit einem bestimmten Hardwaregerät**|Zeigt Computer mit einem angegebenen Hardwaregerät an.|  
|**Hardwaregerätestatus für einen bestimmten Computer**|Zeigt den Kompatibilitätsstatus von Hardwaregeräten für ein angegebenes Betriebssystem an, die auf einem angegebenen Computer gefunden werden.|  
|**Hardwaregerätestatus für Computer in einer bestimmten Sammlung**|Zeigt den Gesamtstatus für Hardwaregeräte für ein angegebenes Betriebssystem für Computer in einer angegebenen Sammlung an. Sie können mithilfe dieses Berichts die Hardwarekompatibilität ermitteln, bevor Sie ein Betriebssystem bereitstellen.|  
|**Statuszusammenfassung für Hardwaregeräte**|Zeigt eine Statuszusammenfassung für Hardwaregeräte für ein angegebenes Betriebssystem an. Sie können mithilfe dieses Berichts die Kompatibilität von Hardwaregeräten ermitteln, bevor Sie ein Betriebssystem bereitstellen.|  
|**Hardwareanforderungen für Betriebssysteme**|Zeigt die minimalen und empfohlenen Hardwarekriterien für Betriebssysteme an.|  
|**Status der Betriebssystemanforderungen für Computer in einer bestimmten Sammlung**|Zeigt den Status von Betriebssystemanforderungen für das angegebene Betriebssystem für Computer in einer angegebenen Sammlung an. Sie können mithilfe dieses Berichts ermitteln, ob die Anforderungen des angegebenen Betriebssystems hinsichtlich CPU-Prozessorgeschwindigkeit, Arbeitsspeichergröße und Festplattengröße eines Computers erfüllt werden.|  
|**Zusammenfassung zur Upgradebewertung**|Zeigt die Zusammenfassung zur Upgradebewertung an. Sie können mithilfe dieses Berichts den Gesamtstatus für die Upgradekompatibilität bewerten.|  

### <a name="user---device-affinity"></a>Affinität zwischen Benutzer und Gerät  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Ausstehende Affinitätszuordnungen zwischen Benutzer und Gerät nach Sammlung**|Dieser Bericht enthält alle ausstehenden Affinitätszuordnungen zwischen Benutzer und Gerät für Mitglieder einer Sammlung basierend auf den Nutzungsdaten.|  
|**Affinitätszuordnungen zwischen Benutzer und Gerät pro Sammlung**|Zeigt alle Zuordnungen zwischen Benutzer und Gerät für die angegebene Sammlung an und gruppiert die Ergebnisse nach Sammlungstyp (z. B. Benutzer oder Gerät).|  

### <a name="user-data-and-profiles-health"></a>Integrität von Benutzerdaten und Profilen  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Bericht zur Integrität der Ordnerumleitung – Details**|Zeigt die Details des Integritätszustands der Ordnerumleitung für jeden umgeleiteten Ordner eines gegebenen Benutzers an.|  
|**Bericht zur Integrität servergespeicherter Benutzerprofile – Details**|Zeigt Details zum Integritätszustand für servergespeicherte Benutzerprofile für einen angegebenen Benutzer an.|  
|**Bericht zur Integrität von Benutzerdaten und Profilen – Details**|Zeigt die Details zu Fehlern oder Warnungen für die Ordnerumleitung oder das servergespeicherte Benutzerprofil an, wenn Detailinformationen zur Anzahl aus dem Zusammenfassungsbericht angezeigt werden.|  
|**Bericht zur Integrität von Benutzerdaten und Profilen – Zusammenfassung**|Zeigt die Zusammenfassung zu den Integritätszuständen für die Ordnerumleitung und für servergespeicherte Benutzerprofile an.|  

### <a name="users"></a>-Benutzer  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Computer für einen bestimmten Benutzernamen**|Zeigt eine Liste von Computern an, die von einem angegebenen Benutzer verwendet wurden.|  
|**Benutzer pro Domäne zählen**|Zeigt die Anzahl der Benutzer in den einzelnen Domänen an.|  
|**Benutzer in einer bestimmten Domäne**|Zeigt eine Liste der Benutzer und ihrer Computer in einer angegebenen Domäne an.|  

### <a name="virtual-applications"></a>Virtuelle Anwendungen  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Ergebnisse zur virtuellen App-V-Umgebung**|Zeigt Informationen zu einer angegebenen virtuellen Umgebung an, die sich für eine angegebene Sammlung in einem angegebenen Zustand befindet.|  
|**Ergebnisse zur virtuellen App-V-Umgebung für Bestand**|Zeigt Informationen zu einer angegebenen virtuellen Umgebung für einen angegebenen Bestand sowie sämtliche Bereitstellungstypen für die angegebene virtuelle Umgebung an.|  
|**Status der virtuellen App-V-Umgebung**|Zeigt Kompatibilitätsinformationen für eine angegebene virtuelle Umgebung für eine angegebene Sammlung an.|  
|**Computer mit einer bestimmten virtuellen Anwendung**|Zeigt eine Zusammenfassung der Computer mit der angegebenen App-V-Verknüpfung an, die mit dem Application Virtualization Management Sequencer erstellt wurde.|  
|**Computer mit einem bestimmten virtuellen Anwendungspaket**|Zeigt eine Zusammenfassung der Computer an, auf denen das angegebene App-V-Anwendungspaket installiert ist.|  
|**Anzahl aller Instanzen von virtuellen Anwendungspaketen**|Zeigt die Anzahl der erkannten App-V-Anwendungspakete an.|  
|**Anzahl aller Instanzen virtueller Anwendungen**|Zeigt die Anzahl der erkannten App-V-Anwendungen an.|  

### <a name="wake-on-lan"></a>-Wake-On-LAN  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Alle für Wake-On-LAN-Aktivitäten vorgesehenen Computer**|Zeigt eine Liste von Computern an, die während der Bereitstellung mit dem von Ihnen angegebenen Typ für eine Wake-On-LAN-Aktivität vorgesehen sind.|  
|**Alle Objekte, die auf Reaktivierungsaktivitäten warten**|Zeigt Objekte an, die für die Reaktivierung geplant sind.|  
|**Alle Standorte, die für Wake-On-LAN aktiviert sind**|Zeigt eine Liste aller Standorte in der Hierarchie an, die für Wake-On-LAN aktiviert sind.|  
|**Fehlermeldungen, die innerhalb eines bestimmten Zeitraums während des Sendens von Reaktivierungspaketen empfangen wurden**|Zeigt Fehlermeldungen an, die innerhalb eines definierten Zeitraums während des Sendens von Reaktivierungspaketen empfangen wurden.|  
|**Verlauf der Remoteaktivierungs-Aktivität über LAN**|Zeigt einen Verlauf der innerhalb eines bestimmten Zeitraums aufgetretenen Reaktivierungsaktivität an.|  
|**Details zum Aktivierungsproxy-Bereitstellungszustand**|Zeigt Informationen zum Bereitstellungsstatus des Aktivierungsproxys für jedes Gerät in einer angegebenen Sammlung an.|  
|**Zusammenfassung des Aktivierungsproxy-Bereitstellungszustands**|Zeigt eine Zusammenfassung zum Bereitstellungsstatus des Reaktivierungsproxys in einer angegebenen Sammlung an.|  



<!--HONumber=Dec16_HO3-->


