---
title: "Diagnosedaten für 1606 | Microsoft-Dokumentation"
description: Erfahren Sie mehr zu den Ebenen der Diagnose- und Nutzungsdaten, die System Center Configuration Manager Version 1606 sammelt.
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7350d03-f440-4744-82d4-75f8c6c25028
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
ms.sourcegitcommit: 688e05aae0e0b15b54835f8d64a98487f4d7b64d
ms.openlocfilehash: 27eb4225b7e907772fa5ed8b209fc04fa9f3a677

---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1606-of-system-center-configuration-manager"></a>Ebenen der Sammlung von Nutzungsdaten zu Diagnosezwecken für System Center Configuration Manager Version 1606

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager Version 1606 sammelt drei Ebenen von Diagnose- und Nutzungsdaten: **Basis**, **Erweitert** und **Vollständig**. Standardmäßig ist dieses Feature auf die Ebene „Erweitert“ festgelegt. Die folgenden Abschnitte enthalten zusätzliche Details zu den auf den einzelnen Ebenen gesammelten Daten.

Änderungen gegenüber früheren Versionen sind mit ***[Neu]***, ***[Aktualisiert]***, ***[Entfernt]*** oder ***[Verschoben]*** gekennzeichnet.


> [!IMPORTANT]
>  Configuration Manager sammelt auf den Ebenen „Basis“ und „Erweitert“ keine Standortcodes, Standortnamen, IP-Adressen, Benutzer- oder Computernamen, physischen Adressen oder E-Mail-Adressen. Die auf der Ebene „Vollständig“ erfassten Daten (möglicherweise in erweiterten Diagnoseinformationen wie Protokolldateien oder Arbeitsspeicher-Momentaufnahmen enthaltene Daten) werden nicht zielgerichtet gesammelt. Sie werden von Microsoft auch nicht zu Werbezwecken oder dazu verwendet, Sie zu identifizieren bzw. Kontakt mit Ihnen aufzunehmen.

##  <a name="a-namebkmkchangea-how-to-change-the-level"></a><a name="bkmk_change"></a> Ändern der Ebene
 Administratoren mit einem rollenbasierten Verwaltungsbereich, der **Ändern**-Berechtigungen für die **Standort**-Objektklasse umfasst, können in den Einstellungen der Configuration Manager-Konsole unter „Diagnose- und Nutzungsdaten“ die Ebene der erfassten Daten ändern.

   Wechseln Sie dazu in der Konsole zur Registerkarte „Backstage“ (die obere linke Registerkarte mit Dropdownpfeil), und wählen Sie **Nutzungsdaten** und anschließend die Datenebene aus, die Sie benutzen möchten.  

##  <a name="a-namebkmklevel1a-level-1---basic"></a><a name="bkmk_level1"></a> Ebene 1: Basis
 Die Ebene „Basis“ umfasst Daten über Ihre Hierarchie, Daten, die für die Verbesserung Ihrer Installations- oder Upgradeerfahrung nötig sind, sowie Daten, die zur Ermittlung der für Ihre Hierarchie infrage kommenden Configuration Manager-Updates benötigt werden.

 Ab System Center Configuration Manager-Version 1606 enthält diese Ebene Folgendes:


 -   Setupinformationen:
      - Build, Installationstyp, Sprachpakete, Funktionen, die Sie aktiviert haben  

      -   Aktualisieren des Paketbereitstellungsstatus und der Fehler, des Downloadstatus und der Voraussetzungsfehler  

      -  Skriptversion nach dem Upgrade

      -  Updateverwendung (Fast Ring)

-   Metriken zur Datenbankleistung (Informationen zur Replikationsverarbeitung, die wichtigsten gespeicherten SQL Server-Prozeduren nach Prozessor und Datenträgerverwendung)

-   Grundlegende Informationen zur Datenbankkonfiguration (Prozessoren, Clusterkonfiguration und Konfiguration verteilter Ansichten)

-   Configuration Manager-Datenbankschema (Hash aller Objektdefinitionen)

-   Anzahl der Configuration Manager-Client- und -Betriebssystemversionen

-   Anzahl der Betriebssysteme für verwaltete Geräte und der von Exchange Connector festgelegten Richtlinien

-   Anzahl der Clientsprachen und -gebietsschemas

-   Anzahl von Windows 10-Geräten nach Branch und Build

-   Grundlegende Daten zur Configuration Manager-Standorthierarchie (Standortliste, Typ, Version, Status, Anzahl der Clients und Zeitzone)

-   Grundlegende Informationen zum Standortsystemserver (verwendete Standortsystemrollen, Internet- und SSL-Status, Betriebssystem, Prozessoren sowie physischer oder virtueller Computer)

-   Grundlegende Statistiken zur Benutzerermittlung (Benutzerermittlungsanzahl und minimale/maximale/durchschnittliche Gruppengröße)

-   Grundlegende Informationen zu Endpoint Protection (Antischadsoftware-Clientversionen)

-   Anzahl der grundlegenden Anwendungs- und Bereitstellungstypen (Gesamtzahl der Apps, Gesamtzahl der Apps mit mehreren Bereitstellungstypen, Gesamtzahl der Apps mit Abhängigkeiten, Gesamtzahl der ersetzten Apps und Anzahl der verwendeten Bereitstellungstechnologien)

-   Anzahl der grundlegenden Betriebssystembereitstellungen (OSDs) (Images)

-   Informationen zu Verteilungspunkt- und Verwaltungspunkttypen sowie zur grundlegenden Konfiguration (geschützt, vorab bereitgestellt, PXE, Multicast, SSL-Status, Pull-/Peerverteilungspunkte, MDM-aktiviert, SSL-fähig usw.)

-   Telemetriestatistiken (Ausführungszeit, Laufzeit und Fehler)

-  Konfigurierte Telemetrieebene, Modus (online oder offline) und schnelle Updatekonfiguration

-  Verwenden der Netzwerkermittlung (aktiviert oder deaktiviert)
-  Verwaltungskonsole:

     -  Statistiken zu den Konsolenverbindungen (Betriebssystemversion, Sprache, SKU und Architektur, Systemspeicher, Anzahl der logischen Prozessoren, Connect-Website-ID, installierte .NET-Versionen und Konsolensprachpakete)    


- ***[Neu]*** SQL-Version, Service Pack-Ebene, Edition, Sortierungs-ID und Zeichensatz


##  <a name="a-namebkmklevel2a-level-2---enhanced"></a><a name="bkmk_level2"></a> Ebene 2: Erweitert
Die Ebene „Erweitert“ ist die Standardeinstellung nach dem Setup. Diese Ebene enthält die auf der Ebene „Basis“ erfassten Daten und featurespezifische Daten (Häufigkeit und Dauer der Verwendung), Configuration Manager-Clienteinstellungen (Name der Komponente, Status und bestimmte Einstellungen wie Abrufintervalle) sowie grundlegende Informationen zu Softwareupdates.

Diese Ebene wird empfohlen, weil sie Microsoft die Daten bereitstellt, die mindestens erforderlich sind, um in künftigen Versionen der Produkte und Dienste nützliche Verbesserungen vorzunehmen. Diese Ebene erfasst keine Objektnamen (Websites, Benutzer, Computer oder Objekte) und keine Details zu sicherheitsrelevanten Objekten oder Sicherheitsrisiken, wie etwa die Anzahl der Systeme, die Softwareupdates erfordern.

Ab System Center Configuration Manager-Version 1606 enthält diese Ebene Folgendes:

-   **Anwendungsverwaltung:**  

    -    Grundlegende Informationen zu Verwendung/Zielgruppenadressierung für innerhalb der Organisation verwendete Bereitstellungstypen (adressierter Benutzer/adressiertes Gerät, erforderlich/verfügbar und universelle Apps)  

    -   Informationen zur Anwendungsbereitstellung (Installieren/Deinstallieren, Genehmigung erforderlich, Benutzerinteraktion aktiviert/deaktiviert, Abhängigkeit und Ablösung)  

    -   Statistiken zur Anforderung verfügbarer Anwendungen  

    -   Anzahl der Pakete nach Typ  

    -   Anzahl der Anwendungsanwendbarkeit nach Betriebssystem  

    -   Anzahl der Paket-/Programmbereitstellungen  

    -   Anzahl von App-V-Umgebungen und Bereitstellungseigenschaften  

    -   Anzahl von Windows 10-lizenzierten Anwendungslizenzen  

    -   Minimale/maximale/durchschnittliche Anzahl von Anwendungsbereitstellungen pro Benutzer/Gerät in einem bestimmten Zeitraum

    -   Wartungsfenstertyp und -dauer  

    -  Größe der Anwendungsrichtlinie und Komplexitätsstatistiken

    - ***[Neu]*** Anzahl der Windows Store für Unternehmen-Apps und Synchronisierungsstatistiken (einschließlich zusammengefasster App-Typen)  

    - ***[Neu]*** Statistiken für Begrenzungsgruppen (wie viele schnelle, langsame sowie Anzahl pro Gruppe)

    - ***[Neu]*** Konfigurationsoptionen für und Anzahl von MSI

    - ***[Neu]*** App-Anforderungen (Anzahl der integrierten Bedingungen wird von der Bereitstellungstechnologie referenziert)

    - ***[Neu]*** App-Ablösung, maximale Kettentiefe

    - ***[Neu] *** Nutzung des Universal Data Access (UDA) und Art der Erstellung



-   **Client:**  

    -   Liste/Anzahl der aktivierten Client-Agents  

    -   Anzahl der Clientinstallationen von jedem Quellspeicherorttyp  

    -   Anzahl der Fehler bei der Clientinstallation  

    -  ***[Neu]*** Automatisches Upgrade der Clientbereitstellungskonfiguration einschließlich Clientpilottests

    -  ***[Neu]*** Clientintegritätsstatistiken und Zusammenfassung wichtiger Probleme

    - ***[Neu]*** BIOS-Alter in Jahren

    - ***[Neu] *** Alter des Betriebssystems in Monaten

    - ***[Neu]*** Anzahl der Softwarecenteraktionen

    - ***[Neu]*** Clientversion von Active Management Technology (AMT)

    - ***[Neu]*** Downloadfehler in der Clientbereitstellung

    - ***[Neu]*** Status der Clientbenachrichtigungsaktion (wie oft jede Aktion ausgeführt wird, max. Anzahl von Zielclients und durchschnittliche Erfolgsrate)

    - ***[Neu]*** Bereitstellungsmethoden für Clients und Anzahl der Clients pro Bereitstellungsmethode

    - ***[Neu]*** Konfigurieren der Cachegrößen des Clients



- ***[Neu]*** **Clouddienste:**

  - ***[Neu] *** Anzahl der Sammlungen, die mit Operations Management Suite synchronisiert werden

  - ***[Neu] *** Angabe, ob der Operations Management Suite-Cloud-Connector aktiviert ist



- ***[Neu] Sammlungen:***

    -  ***[Verschoben]*** Statistiken zur Sammlungsauswertung (Abfragezeit, zugewiesene/nicht zugewiesene Anzahl, Anzahl nach Typ, ID-Rollover und Verwendung von Regeln)

    - ***[Neu]*** Sammlungen ohne eine Bereitstellung

    - ***[Neu]*** Verwendung der Sammlungs-ID (nicht genügend IDs)



-   **Kompatibilitätseinstellungen:**  

    -   Anzahl der Konfigurationselemente nach Typ  

    -   Grundlegende Informationen zur Konfigurationsbaseline (Zählerwert, Anzahl von Bereitstellungen und Anzahl der Verweise)  

    -   ***[Aktualisiert]*** Anzahl von Bereitstellungen, die auf integrierte Einstellungen verweisen (wiederhergestellte Einstellungen werden jetzt erfasst)  

    -   ***[Aktualisiert]*** Anzahl von Regeln und Bereitstellungen, die für benutzerdefinierte Einstellungen erstellt wurden (wiederhergestellte Einstellungen werden jetzt erfasst)  
    -   Anzahl der bereitgestellten Simple Certificate Enrollment-Protokollvorlagen (SCEP) und der VPN-, WLAN-, Zertifikat- (.PFX) und Konformitätsrichtlinienvorlagen

    -  Anzahl der SCEP-Zertifikat-, VPN-, WLAN-, Zertifikat- (.PFX) und Konformitätsrichtlinienbereitstellungen je Plattform

    - ***[Neu]*** Passport for Work-Richtlinie (erstellt, bereitgestellt)



-   **Inhalt:**  

    -   Anzahl der Grenzen nach Typ  

    -   Informationen zur Begrenzungsgruppe (Anzahl der jeder Begrenzungsgruppe zugewiesenen Grenzen und Standortsysteme)  

    -   Informationen zur Verteilungspunktgruppe (Anzahl der jeder Verteilungspunktgruppe zugewiesenen Pakete und Verteilungspunkte)  

    -   Informationen zur Verteilungspunktkonfiguration (Verwenden von Branch-Cache und Verteilungspunktüberwachung)  

    -   Informationen zur Verteilungs-Manager-Konfiguration (Threads, Wiederholungsverzögerung, Anzahl der Wiederholungsversuche und Einstellungen für Pullverteilungspunkte)  


-   **Endpoint Protection:**  

    -   Endpoint Protection-Antischadsoftware und Windows-Firewall-Richtliniennutzung (Anzahl der eindeutigen der Gruppe zugewiesenen Richtlinien)<br /><br /> Dies umfasst keine Informationen über in der Richtlinie enthaltene Einstellungen.  

    -   Fehler bei der Endpoint Protection-Bereitstellung (Anzahl der Endpoint Protection-Richtlinien-Bereitstellungsfehlercodes)  

    -   Anzahl der ausgewählten Sammlungen, die im Endpoint Protection-Dashboard angezeigt werden sollen  

    -   Anzahl der Warnungen, die für das Endpoint Protection-Feature konfiguriert sind  

    - ***[Neu] *** Advanced Threat Protection-Richtlinien (ATP) (Anzahl der Richtlinien und Angabe, ob Richtlinien bereitgestellt werden)


-   ***[Entfernt]*** **Verwaltung mobiler Anwendungen (MAM):**  

    -   ***[Entfernt]*** Anzahl der MAM-fähigen Office- und Branchenanwendungen und -richtlinien je Betriebssystem  

    -   ***[Entfernt]*** Anzahl der MAM-Anwendungsbereitstellung/-Richtlinienbereitstellung  

    -   ***[Entfernt]*** Anzahl der pro MAM-Einstellung erstellten Regeln  


- ***[Neu]*** **Migration:**

  -  ***[Neu]*** Anzahl der migrierten Objekte (Migrations-Assistent verwenden)



-   **Verwaltung mobiler Geräte (MDM):**  

    -   Anzahl der ausgegebenen Aktionen für mobile Geräte: Sperr-, PIN-Rücksetzungs-, Zurücksetzungs- und Außerkraftsetzungsbefehle  

    -   Anzahl der von Configuration Manager und Microsoft Intune verwalteten mobilen Geräte und Art ihrer Registrierung (Massenregistrierung oder benutzerbasierte Registrierung)  

    -   Zeitplan zu Abrufvorgängen für mobile Geräte und Statistiken zur Eincheckdauer mobiler Geräte  

    -   Anzahl der Richtlinien für mobile Geräte  

    -   Anzahl der Benutzer mit mehreren registrierten mobilen Geräten  

-   **Problembehandlung für Microsoft Intune:**

    -   Anzahl und Größe der von Microsoft Intune heruntergeladenen Meldungen zum Zustand, Status und Mandantenzustand, zur Inventur und Konformität und zu RDR, DDR, UDX, POL, LOG, Cert, CRP, Resync, CFD, RDO, BEX und ISM

    -   Anzahl und Größe von Geräteaktionen (Zurücksetzen, Außerkraftsetzen, Sperren), Telemetrie und Datenmeldungen, die auf Microsoft Intune repliziert wurden

    -   Statistiken zur vollständigen und Deltabenutzersynchronisierung für Microsoft Intune


-   **Lokale Verwaltung mobiler Geräte (MDM):**  

    -   Statistiken zu erfolgreichen und fehlerhaften lokalen MDM-Anwendungsbereitstellungen  

    -   Anzahl von Windows 10-Massenregistrierungspaketen und -profilen  



-   **Betriebssystembereitstellung:**  

    -   Anzahl der Startimages, Treiber, Treiberpakete, multicastfähigen Verteilungspunkte, PXE-fähigen Verteilungspunkte und Tasksequenzen  

    -   ***[Neu]*** Anzahl der Tasksequenzschrittnutzung



-   **Standortupdates:**

    - Versionen installierter Configuration Manager-Hotfixes




-   **Softwareupdates:**  

    -   Gesamtzahl bzw. durchschnittliche Anzahl von Sammlungen mit Softwareupdatebereitstellungen sowie maximale/durchschnittliche Anzahl der bereitgestellten Updates  

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

    -   ***[Neu]*** Statistiken für den Lastenausgleich des Softwareupdatepunkts



-   **SQL-/Leistungsdaten:**  

    -   Anzahl der größten Datenbanktabellen  

    -   Informationen zum SQL Always-On-Replikat  

    -  Beibehaltungsdauer der verfolgten SQL-Änderungen

    - ***[Neu]*** Ermittlungstypen, aktiviert und Zeitplan (vollständig, inkrementell)

    - ***[Neu]*** Operative Ermittlungsstatistik (Anzahl der gefundenen Objekte)

    - ***[Neu]*** Leistungsprobleme der verfolgten SQL-Änderungen, Beibehaltungsdauer und Status der automatischen Bereinigung



- ***[New]*** **Verschiedenes**

    - ***[Neu]*** Anzahl der Wake-On-LAN-Standorte (WOL)



##  <a name="a-namebkmklevel3a-level-3---full"></a><a name="bkmk_level3"></a> Ebene 3: Vollständig
Die Ebene „Vollständig“ umfasst alle Daten der Ebenen „Basis“ und „Erweitert“. Darüber hinaus werden zusätzliche Informationen zu Endpoint Protection, die Prozentsätze zur Updatekompatibilität sowie Informationen zu Softwareupdates erfasst. Diese Ebene kann auch erweiterte Diagnoseinformationen wie Systemdateien und Momentaufnahmen des Arbeitsspeichers einschließen. Darin können wiederum personenbezogene Informationen enthalten sein, die zum Zeitpunkt der Erfassung im Arbeitsspeicher oder in Protokolldateien vorhanden waren.

Ab System Center Configuration Manager-Version 1606 enthält diese Ebene Folgendes:

-   Statistiken zur Sammlungsauswertung und -aktualisierung

-   Zusammenfassung zur Endpoint Protection-Integrität (einschließlich Anzahl der geschützten, gefährdeten, unbekannten und nicht unterstützten Clients)

-   Endpoint Protection-Richtlinienkonfiguration

-   Informationen zur Softwareupdatebereitstellung (Prozentsatz der Zielbereitstellungen mit Client- bzw. UTC-Zeit, erforderlich bzw. optional bzw. automatisch und Neustartunterdrückung)

-   Gesamtkompatibilität der Softwareupdatebereitstellungen

-   Informationen zum Zeitplan für die Auswertung der automatischen Bereitstellungsregel

-   ***[ENTFERNT]*** Anzahl der Clients mit Netzwerkzugriffsschutz-Richtlinien

-   Codes und Anzahl der Fehler bei der Softwareupdatebereitstellung

-   Minimale/maximale/durchschnittliche Anzahl der inaktiven Clients in Softwareupdate-Bereitstellungssammlungen

-   Anzahl der Gruppen mit abgelaufenen Softwareupdates

-   Minimale/maximale/durchschnittliche Anzahl von Softwareupdates pro Paket

-   Prozentsätze der erfolgreichen Überprüfungen auf Softwareupdates

-   Minimale/maximale/durchschnittliche Anzahl von Stunden seit der letzten Überprüfung auf Softwareupdates

-    Vom Softwareupdatepunkt synchronisierte Softwareupdateprodukte
-    Konformitätseinstellungen: Konfigurationsdetails zu SCEP-, VPN-, WLAN- und Konformitätsrichtlinienvorlagen

-    Typ der EAS-Richtlinien für den bedingten Zugriff (blockiert oder in Quarantäne) für mit Intune verwaltete Geräte

-   ***[Neu]*** Die besten 50 CPUs in der Umgebung

-   ***[Neu]*** DCM-Konfigurationspaket für die System Center Configuration Manager-Nutzung

-   ***[Neu]*** MSI-Produktcode (gängige Apps, die Kunden bereitstellen)

-   ***[Neu]*** Zusammenfassung zur ATP-Integrität

-   ***[Neu]*** Detaillierte Installationsfehler bei der Client-Bereitstellung



<!--HONumber=Dec16_HO5-->


