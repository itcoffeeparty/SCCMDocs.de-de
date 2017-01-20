---
title: "Diagnosedaten für 1610 | System Center Configuration Manager"
description: "Erfahren Sie mehr über die Ebenen der Diagnose- und Nutzungsdaten, die System Center Configuration Manager-Version 1610 sammelt."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eb20eb90-bcc0-41de-bfea-638ea470c0dd
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: 6b4af705fa148261634d38dbb2df9988c5672180
ms.openlocfilehash: df8a4c84da8e73aae2455e5f5af26d097449cddd

---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1610-of-system-center-configuration-manager"></a>Ebenen der Sammlung von Nutzungsdaten zu Diagnosezwecken für System Center Configuration Manager-Version 1610

*Gilt für: System Center Configuration Manager (Current Branch)*

Die Version 1610 von System Center Configuration Manager sammelt drei Ebenen von Diagnose- und Nutzungsdaten: **Basic** (Basis), **Enhanced** (Erweitert) und **Full** (Vollständig). Standardmäßig ist dieses Feature auf die Ebene „Erweitert“ festgelegt. Die folgenden Abschnitte enthalten zusätzliche Details zu den auf den einzelnen Ebenen gesammelten Daten.

Änderungen gegenüber früheren Versionen sind mit ***[Neu]***, ***[Aktualisiert]***, ***[Entfernt]*** oder ***[Verschoben]*** gekennzeichnet.


> [!IMPORTANT]
>  Configuration Manager sammelt auf den Ebenen „Basis“ und „Erweitert“ keine Standortcodes, Standortnamen, IP-Adressen, Benutzer- oder Computernamen, physische Adressen oder E-Mail-Adressen. Die auf der Ebene „Vollständig“ erfassten Daten (möglicherweise in erweiterten Diagnoseinformationen wie Protokolldateien oder Arbeitsspeicher-Momentaufnahmen enthaltene Daten) werden nicht zielgerichtet gesammelt und von Microsoft nicht zu Werbezwecken oder dazu verwendet, Sie zu identifizieren bzw. Kontakt mit Ihnen aufzunehmen.

##  <a name="a-namebkmkchangea-how-to-change-the-level"></a><a name="bkmk_change"></a> Ändern der Ebene
 Administratoren mit einem rollenbasierten Verwaltungsbereich, der die Berechtigung **Ändern** für die **Standort**-Objektklasse umfasst, können in den Einstellungen der Configuration Manager-Konsole unter „Diagnose- und Nutzungsdaten“ die Ebene der erfassten Daten ändern.

Ab Version 1610 können Sie die Datensammlungsebene innerhalb der Konsole ändern, indem Sie zu **Verwaltung** > **Überblick** > **Standortkonfiguration** > **Standorte** navigieren. Öffnen Sie die **Hierarchieeinstellungen**, und wählen Sie die Datenebene aus, die Sie verwenden möchten.  

##  <a name="a-namebkmklevel1a-level-1---basic"></a><a name="bkmk_level1"></a> Ebene 1: Basis
 Die Ebene „Basis“ erfasst Daten über Ihre Hierarchie und wird für die Verbesserung Ihrer Installations- oder Upgradeerfahrung und zur Ermittlung der für Ihre Hierarchie infrage kommenden Configuration Manager-Updates benötigt.

 Bei System Center Configuration Manager-Version 1610 enthält diese Ebene Folgendes:


 -   Setupinformationen:
      - Build, Installationstyp, Sprachpakete, Funktionen, die Sie aktiviert haben  

      -   Aktualisieren des Paketbereitstellungsstatus und der Fehler, des Downloadstatus und der Prereq-Fehler    

      -  Skriptversion nach dem Upgrade

      -  Updateverwendung (Fast Ring)

    -  ***[Neu]*** Verwendung der Vorabversion, Setup Medientyp, Verzweigungstyp

    - ***[Neu]*** SA Ablaufdatum


-   Metriken zur Datenbankleistung (Informationen zur Replikationsverarbeitung, die wichtigsten gespeicherten SQL Server-Prozeduren nach Prozessor und Datenträgerverwendung)

-   Grundlegende Informationen zur Datenbankkonfiguration (Prozessoren, Clusterkonfiguration, Konfiguration verteilter Ansichten)

-   Configuration Manager-Datenbankschema (Hash aller Objektdefinitionen)

-   Anzahl der Configuration Manager-Client- und -Betriebssystemversionen

-   Anzahl und Betriebssystem der verwalteten Geräte und von Exchange Connector festgelegte Richtlinien

-   Anzahl der Sprachen und Gebietsschemas der Clients

-   Anzahl von Windows 10-Geräten nach Branch und Build

-   Grundlegende Daten zur Configuration Manager-Standorthierarchie (Standortliste, Typ, Version, Status, Anzahl der Clients und Zeitzone)

-   Grundlegende Informationen zum Standortsystemserver (verwendete Standortsystemrollen, Internet- und SSL-Status, Betriebssystem, Prozessoren, physischer oder virtueller Computer)

-   Grundlegende Statistiken zur Benutzerermittlung (Benutzerermittlungsanzahl, minimale/maximale/durchschnittliche Gruppengröße)

-   Grundlegende Informationen zu Endpoint Protection (Antischadsoftware-Clientversionen)

-   Anzahl der grundlegenden Anwendungs- und Bereitstellungstypen (Gesamtanzahl der Apps, Gesamtanzahl der Apps mit mehreren Bereitstellungstypen, Gesamtanzahl der Apps mit Abhängigkeiten, Gesamtanzahl der ersetzten Apps, Anzahl der verwendeten Bereitstellungstechnologien)

-   Grundlegende OSD-Anzahl (Images)

-   Informationen zu Verteilungspunkt- und Verwaltungspunkttypen sowie zur grundlegenden Konfiguration (geschützt, vorab bereitgestellt, PXE, Multicast, SSL-Status, Pull-/Peerverteilungspunkte, MDM-aktiviert, SSL-fähig usw.)

-   Telemetriestatistiken (Ausführungszeit, Laufzeit, Fehler)

-  Konfigurierte Telemetrieebene, Modus (online oder offline) und schnelle Updatekonfiguration

-  Verwenden der Netzwerkermittlung (aktiviert oder deaktiviert)
-  Verwaltungskonsole:

     -  Statistiken zu den Konsolenverbindungen (OS-Version, Sprache, SKU und Architektur; Systemspeicher, Anzahl der logischen Prozessoren, connect site-ID, installierte .NET-Releases und Sprachpakete für die Konsole)    


- SQL-Version, Service Pack-Ebene, Edition, Sortierungs-ID, Zeichensatz


##  <a name="a-namebkmklevel2a-level-2---enhanced"></a><a name="bkmk_level2"></a> Ebene 2: Erweitert
Die Ebene „Erweitert“ ist die Standardeinstellung nach dem Setup. Diese Ebene schließt die auf der Ebene „Basis“ erfassten Daten ein und enthält darüber hinaus featurespezifische Daten (Häufigkeit und Dauer der Verwendung), Configuration Manager-Clienteinstellungen (Name der Komponente, Status und bestimmte Einstellungen wie Abrufintervalle) sowie grundlegende Informationen zu Softwareupdates.

Diese Ebene wird empfohlen, weil sie Microsoft die Daten bereitstellt, die mindestens erforderlich sind, um in künftigen Versionen der Produkte und Dienste nützliche Verbesserungen vorzunehmen. Diese Ebene erfasst keine Objektnamen (Websites, Benutzer, Computer oder Objekte) und keine Details zu sicherheitsrelevanten Objekten oder Sicherheitsrisiken, wie etwa die Anzahl der Systeme, die Softwareupdates erfordern.

Bei System Center Configuration Manager-Version 1610 enthält diese Ebene Folgendes:

-   **Anwendungsverwaltung:**  

    -    Grundlegende Informationen zu Verwendung/Zielgruppenadressierung für innerhalb der Organisation verwendete Bereitstellungstypen (adressierter Benutzer/adressiertes Gerät, erforderlich/verfügbar, universelle Apps)  

    -   Informationen zur Anwendungsbereitstellung (Installieren/Deinstallieren, Genehmigung erforderlich, Benutzerinteraktion aktiviert/deaktiviert, Abhängigkeit, Ablösung)  

    -   Statistiken zur Anforderung verfügbarer Anwendungen  

    -   Anzahl der Pakete nach Typ  

    -   Anzahl der Anwendungsanwendbarkeit nach Betriebssystem  

    -   Anzahl der Paket-/Programmbereitstellungen  

    -   Anzahl von App-V-Umgebungen und Bereitstellungseigenschaften  

    -   Anzahl von Windows 10-lizenzierten Anwendungslizenzen  

    -   Minimale/maximale/durchschnittliche Anzahl von Anwendungsbereitstellungen pro Benutzer/Gerät in einem bestimmten Zeitraum

    -   Wartungsfenstertyp und -dauer  

    -  Größe der Anwendungsrichtlinie und Komplexitätsstatistiken

    - ***[Aktualisiert]*** Anzahl der Apps im Windows Store für Unternehmen (Windows Store for Business, WSfB) und Synchronisierungsstatistiken (einschließlich zusammengefasste App-Typen und die Anzahl der Online- und Offline-lizenzierten Apps)  

    - Statistiken für Begrenzungsgruppen (wie viele schnelle, langsame pro Gruppe)

    - Konfigurationsoptionen für und Anzahl von MSI

    - App-Anforderungen (Anzahl der integrierten Bedingungen wird von welcher Bereitstellungstechnologie referenziert)

    - App-Ablösung, maximale Kettentiefe

    - UDA-Verwendung, wie erstellt

    - ***[Neu] *** Statistiken über Genehmigungen für Anwendungen und Häufigkeit der Nutzung



-   **Client:**  

    -   Liste/Anzahl der aktivierten Client-Agents  

    -   Anzahl der Clientinstallationen von jedem Quellspeicherorttyp  

    -   Anzahl der Fehler bei der Clientinstallation  

    -  ***[Aktualisiert]*** Automatisches Upgrade des Client: Konfigurierung der Bereitstellung einschließlich Pilottests von Clients, Verwendung des Ausschlusses (erweiterter Interoperabilitätsclient)

    -  Clientintegritätsstatistiken und Zusammenfassung wichtiger Probleme

    - BIOS-Alter in Jahren

    - OS-Alter in Monaten

    - Anzahl der Softwarecenteraktionen

    - Clientversion von Active Management Technology (AMT)

    - Downloadfehler in der Clientbereitstellung

    - Status der Aktion der Clientbenachrichtigung (wie oft jede ausgeführt wird, max. Anzahl von Zielclients, durchschnittliche Erfolgsrate)

    - Bereitstellungsmethoden für Clients, Anzahl der Clients pro Bereitstellungsmethode

    - Konfigurieren der Cachegrößen des Clients

    - ***[Neu] *** Anzahl der Hardwareinventurklassen, Softwareinventurregeln und Dateisammlungsregeln




- **Cloud Services:**

  - Die Anzahl der Sammlungen, die mit OMS synchronisiert sind

  -  Ist der OMS-Cloud-Connector aktiviert

  - ***[Neu] *** Statistiken zur Konfigurierung und Verwendung des Cloudverwaltungsgateways

  - ***[Neu] *** Anzahl von Upgrade Analytics-Connectors




- **Sammlungen:**

    -  Statistiken zur Sammlungsauswertung (Abfragezeit, zugewiesene/nicht zugewiesene Anzahl, Anzahl nach Typ, ID-Rollover und Verwendung von Regeln)

    - Sammlungen ohne eine Bereitstellung

    - Verwendung der Sammlungs-ID (nicht genügend IDs)



-   **Kompatibilitätseinstellungen:**  

    -   Anzahl der Konfigurationselemente nach Typ  

    -   Grundlegende Informationen zur Konfigurationsbaseline (Zählerwert, Anzahl von Bereitstellungen und Anzahl der Verweise)  

    -   Anzahl von Bereitstellungen, die auf integrierte Einstellungen verweisen (wiederhergestellte Einstellungen werden jetzt erfasst)  

    -   Anzahl von Regeln und Bereitstellungen, die für benutzerdefinierte Einstellungen erstellt wurden (wiederhergestellte Einstellungen werden jetzt erfasst)  
    -   Anzahl der bereitgestellten Simple Certificate Enrollment-Protokollvorlagen, VPN-, WLAN-, Zertifikat- (.pfx) und Kompatibilitätsrichtlinienvorlagen

    -  Anzahl von SCEP-, VPN- WLAN-Zertifikaten (.pfx) und Bereitstellungen von Kompatibilitätsrichtlinien je Plattform

    - Passport for Work-Richtlinie (erstellt, bereitgestellt)



-   **Inhalt:**  

    -   Anzahl der Grenzen nach Typ  

    -   Informationen zur Begrenzungsgruppe (Anzahl der jeder Begrenzungsgruppe zugewiesenen Grenzen und Standortsysteme)  

    - ***[Neu] *** Begrenzungsgruppenbeziehungen und Fallbackkonfiguration

    -   Informationen zur Verteilungspunktgruppe (Anzahl der jeder Verteilungspunktgruppe zugewiesenen Pakete und Verteilungspunkte)  

    -   Informationen zur Verteilungspunktkonfiguration (Verwenden von Branch-Cache, Verteilungspunktüberwachung)  

    -   Informationen zur Verteilungs-Manager-Konfiguration (Threads, Wiederholungsverzögerung, Anzahl der Wiederholungsversuche, Einstellungen für Pullverteilungspunkte)  

    - ***[Neu] *** Anzahl von Peercacheclients und Nutzungsstatistiken

    - ***[Neu] *** Statistiken über Downloads von Clients


-   **Endpoint Protection:**  

    -   Verwendung der Endpoint Protection-Antischadsoftware- und der Windows-Firewall-Richtlinie (Anzahl der einer Gruppe zugewiesenen eindeutigen Richtlinien; dies schließt keine Informationen zu den in der Richtlinie enthaltenen Einstellungen ein)  

    -   Fehler bei der Endpoint Protection-Bereitstellung (Anzahl der Endpoint Protection-Bereitstellungsfehlercodes)  

    -   Anzahl der ausgewählten Sammlungen, die im Endpoint Protection-Dashboard angezeigt werden sollen  

    -   Anzahl der Warnungen für das konfigurierte Endpoint Protection-Feature  

    - ATP-Richtlinien (Anzahl der Richtlinien, ist es bereitgestellt)


- **Migration:**

  -   Anzahl der migrierten Objekte (Migrations-Assistent verwenden)



-   **Verwaltung mobiler Geräte (MDM):**  

    -   ***[Aktualisiert]*** Anzahl der Aktionen für mobile Geräte (Sperren, PIN zurücksetzen, Zurücksetzen, Außerkraftsetzen, und Jetzt synchronisieren), ausgegebene Befehle  

    -   Anzahl der von Configuration Manager und Microsoft Intune verwalteten mobilen Geräte und ihre Registrierungsweise (Massenregistrierung, benutzerbasierte Registrierung)  

    -   Zeitplan und Statistiken zu Abrufvorgängen für mobile Geräte, Eincheckdauer mobiler Geräte  

    -   Anzahl der Richtlinien für mobile Geräte  

    -   Anzahl der Benutzer mit mehreren registrierten mobilen Geräten  

-   **Problembehandlung für Microsoft Intune:**

    -   Anzahl und Größe der von Microsoft Intune heruntergeladenen Meldungen zum Zustand, Status und Mandantenzustand, zur Inventur und Kompatibilität und zu RDR, DDR, UDX, POL, LOG, Cert, CRP, Resync, CFD, RDO, BEX und ISM

    -   Anzahl und Größe von Geräteaktionen (Zurücksetzen, Außerkraftsetzen, Sperren), Telemetrie und Datenmeldungen, die auf Microsoft Intune repliziert wurden

    -   Statistiken zur vollständigen und Deltabenutzersynchronisierung für Microsoft Intune


-   **Lokale Verwaltung mobiler Geräte (MDM):**  

    -   Statistiken zu erfolgreichen und fehlerhaften lokalen MDM-Anwendungsbereitstellungen  

    -   Anzahl von Windows 10-Massenregistrierungspaketen und -profilen  



-   **Betriebssystembereitstellung:**  

    -   Anzahl der Startimages, Treiber, Treiberpakete, multicastfähigen Verteilungspunkte, PXE-fähigen Verteilungspunkte und Tasksequenzen  

    -   Anzahl der Tasksequenzschrittnutzung

    - ***[Neu] *** Anzahl der Editionsaktualisierungsrichtlinien



-   **Standortupdates:**

    - Versionen installierter Configuration Manager-Hotfixes




-   **Softwareupdates:**  

    -   Gesamtanzahl bzw. durchschnittliche Anzahl von Sammlungen mit Softwareupdatebereitstellungen sowie maximale/durchschnittliche Anzahl der bereitgestellten Updates  

    -   Anzahl der an die Synchronisierung gebundenen Regeln zur automatischen Bereitstellung  

    -   Anzahl der Regeln zur automatischen Bereitstellung, die neue Updates erstellen oder Updates zu einer vorhandenen Gruppe hinzufügen  

    -   Verfügbare und Stichtagdeltawerte, die in Regeln zur automatischen Bereitstellung verwendet werden  

    -   Durchschnittliche und maximale Anzahl von Zuweisungen pro Update  

    -   Anzahl der mit System Center Updates Publisher erstellten und bereitgestellten Updates  

    -   Anzahl der Updategruppen und -zuweisungen  

    -   Anzahl der Updatepakete und maximale/minimale/durchschnittliche Anzahl der von den Paketen angesprochenen Verteilungspunkte  

    -   Anzahl der Updategruppen und minimale/maximale/durchschnittliche Anzahl der Updates pro Gruppe  

    -   Anzahl von Updates und Prozentsatz der bereitgestellten, abgelaufenen, ersetzten und heruntergeladenen Updates sowie von Updates mit EULAs  

    -   Updateüberprüfungs-Fehlercodes und Anzahl der Computer  

    -   Clientupdateauswertung und Überprüfungszeitpläne  

    -   Softwareupdatepunkt-Synchronisierungszeitplan  

    -   Anzahl der Regeln zur automatischen Bereitstellung mit mehreren Bereitstellungen  

    -   Konfigurationen, die für aktive Windows 10-Wartungspläne verwendet werden  

    -   Windows 10-Dashboardinhaltsversionen  

    -   Anzahl von Windows 10-Clients, die Windows Update für Unternehmen verwenden  

    -   Statistiken zu Clusterpatches  

    -   Anzahl der bereitgestellten Office 365-Updates  

    -   Vom Softwareupdatepunkt synchronisierte Klassifikationen

    -   Statistiken für den Lastenausgleich des Softwareupdatepunkts

    -  ***[Neu] *** Konfiguration von Windows 10-Express-Updates




-   **SQL-/Leistungsdaten:**  

    -   Anzahl der größten Datenbanktabellen  

    -   ***[Aktualisiert] *** Informationen zu SQL Always On-Replikat, Nutzung und Integrationsstatus

    -  Beibehaltungsdauer der verfolgten SQL-Änderungen

    - Ermittlungstypen, aktiviert und Zeitplan (vollständig, inkrementell)

    - Operative Ermittlungsstatistik (Anzahl der gefundenen Objekte)

    - Leistungsprobleme der verfolgten SQL-Änderungen, Beibehaltungsdauer und Status der automatischen Bereinigung



- **Verschiedenes**

    - Anzahl der WOL-Standorte

    - ***[Neu] *** Berichte von Nutzungs- und Leistungsstatistiken  



##  <a name="a-namebkmklevel3a-level-3---full"></a><a name="bkmk_level3"></a> Ebene 3: Vollständig
Die Ebene „Vollständig“ umfasst alle Daten der Ebenen „Basis“ und „Erweitert“. Darüber hinaus werden zusätzliche Informationen zu Endpoint Protection, die Prozentsätze zur Updatekompatibilität sowie Informationen zu Softwareupdates erfasst.  Diese Ebene kann auch erweiterte Diagnoseinformationen wie Systemdateien und Momentaufnahmen des Arbeitsspeichers einschließen. Darin können wiederum personenbezogene Informationen enthalten sein, die zum Zeitpunkt der Erfassung im Arbeitsspeicher oder in den Protokolldateien vorhanden waren.

Bei System Center Configuration Manager-Version 1610 enthält diese Ebene Folgendes:

-   Statistiken zur Sammlungsauswertung und -aktualisierung

-   Zusammenfassung zur Endpoint Protection-Integrität (einschließlich Anzahl der geschützten, gefährdeten, unbekannten und nicht unterstützten Clients)

-   Endpoint Protection-Richtlinienkonfiguration

-   Informationen zur Softwareupdatebereitstellung (Prozentsatz der Zielbereitstellungen mit Client- bzw. UTC-Zeit, erforderlich bzw. optional bzw. automatisch, Neustartunterdrückung)

-   Gesamtkompatibilität der Softwareupdatebereitstellungen

-   Informationen zum Zeitplan für die Auswertung der automatischen Bereitstellungsregel

-   Codes und Anzahl der Fehler bei der Softwareupdatebereitstellung

-   Minimale/maximale/durchschnittliche Anzahl der inaktiven Clients in Softwareupdate-Bereitstellungssammlungen

-   Anzahl der Gruppen mit abgelaufenen Softwareupdates

-   Minimale/maximale/durchschnittliche Anzahl von Softwareupdates pro Paket

-   Prozentsätze der erfolgreichen Überprüfungen auf Softwareupdates

-   Minimale/maximale/durchschnittliche Anzahl von Stunden seit der letzten Überprüfung auf Softwareupdates

-    Vom Softwareupdatepunkt synchronisierte Softwareupdateprodukte
-    Kompatibilitätseinstellungen: Konfigurationsdetails zu SCEP-, VPN-, WLAN- und Kompatibilitätsrichtlinienvorlagen

-    Typ der EAS-Richtlinien für den bedingten Zugriff (blockiert oder in Quarantäne) für mit Intune verwaltete Geräte

-   Die besten 50 CPUs in der Umgebung

-   DCM-Config-Pack für die SCCM-Verwendung

-   MSI-Produktcode (welche sind die gängigen Apps, die Kunden bereitstellen)

-   Zusammenfassung zur ATP-Integrität

-   Detaillierte Installationsfehler der Client-Bereitstellung

- ***[Neu]*** Anwendungsdetails zu Windows Store für Unternehmen (nicht-aggregierte Liste synchronisierter Anwendungen, darunter App-ID, Status – Online oder Offline, und die Gesamtzahl erworbener Lizenzen)



<!--HONumber=Dec16_HO3-->


