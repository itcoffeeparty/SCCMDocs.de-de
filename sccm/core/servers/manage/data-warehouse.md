---
title: Data Warehouse
titleSuffix: Configuration Manager
description: Data Warehouse-Dienstpunkt und -Datenbank für System Center Configuration Manager
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6d6e1850c07207205cad696918f7cd4eb97d3ec8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
#  <a name="the-data-warehouse-service-point-for-system-center-configuration-manager"></a>Der Data Warehouse-Dienstpunkt für System Center Configuration Manager
*Gilt für: System Center Configuration Manager (Current Branch)*

<!--1277922-->
Verwenden Sie den Data Warehouse-Dienstpunkt, um langfristige Verlaufsdaten zur Bereitstellung für Configuration Manager zu speichern und hierfür Berichte zu erstellen.

> [!TIP]
> Dieses Feature wurde erstmals in Version 1702 als [Vorabfeature](/sccm/core/servers/manage/pre-release-features) eingeführt. Ab Version 1706 können ist diese Funktion kein vorab veröffentlichtes Feature mehr.  


> [!Note]  
> Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Das Data Warehouse unterstützt ein Datenvolumen von bis zu 2 TB, inklusive der Zeitstempel für Änderungsnachverfolgung. Die Speicherung der Daten wird durch die automatisierte Synchronisierung der Configuration Manager-Standortdatenbank mit der Data Warehouse-Datenbank erreicht. Auf diese Informationen kann dann vom Reporting services-Punkt aus zugegriffen werden. Mit der Data Warehouse-Datenbank synchronisierte Daten werden drei Jahre lang aufbewahrt. Daten, die älter als drei Jahre sind, werden in regelmäßigen Abständen mithilfe einer eingebauten Aufgabe entfernt.

Zu synchronisierten Daten zählen folgende Gruppen von globalen und Standortdaten:
- Infrastrukturintegrität
- Sicherheit
- Konformität
- Malware   
- Softwarebereitstellungen
- Inventurdetails (Der Inventurverlauf wird allerdings nicht synchronisiert)

Bei der Installation der Standortsystemrolle wird auch die Data Warehouse-Datenbank installiert und konfiguriert. Außerdem werden mehrere Berichte installiert, damit Sie leicht nach diesen Daten suchen und über diese berichten können.



## <a name="prerequisites-for-the-data-warehouse-service-point"></a>Voraussetzungen für den Data Warehouse-Dienstpunkt
- Die Data Warehouse-Standortsystemrolle wird nur am Standort auf der obersten Ebene der Hierarchie unterstützt. Dabei handelt es sich um einen zentralen Verwaltungsstandort oder einen eigenständigen primären Standort.
- Der Computer, auf dem die Standortsystemrolle installiert ist, erfordert .NET Framework 4.5.2 oder höher.
- Geben Sie dem **Konto des Reporting Services-Punkts** die Berechtigung **db_datareader** für die Data Warehouse-Datenbank. 
- Das Computerkonto des Computers, auf dem Sie die Standortsystemrolle installieren, wird verwendet, um Daten mit der Data Warehouse-Datenbank zu synchronisieren. Für dieses Konto sind folgende Berechtigungen erforderlich:  
  - Ein **Administrator** auf dem Computer, auf dem die Data Warehouse-Datenbank gehostet wird.
  - Die Berechtigung **DB_Creator** in der Data Warehouse-Datenbank.
  - **DB_owner** oder **DB_reader** mit der Berechtigung **Ausführen** für die Standortdatenbank der Standorte auf oberster Ebene.
- Für die Data Warehouse-Datenbank wird SQL Server 2012 oder neuer benötigt. Sie können die Editionen Standard, Enterprise oder Datacenter verwenden.
- Die folgenden SQL Server-Konfigurationen können zum Hosten der Warehouse-Datenbank verwendet werden:  
  - Standardinstanz
  - Benannte Instanz
  - SQL Server Always On-Verfügbarkeitsgruppe
  - SQL Server-Failovercluster
- Bei Verwendung von [verteilten Ansichten](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews) muss die Standortsystemrolle des Data Warehouse-Dienstpunkts auf dem Server installiert sein, auf dem die Standortdatenbank des zentralen Administrationsstandorts gehostet wird.

Informationen zur SQL Server-Lizenzierung für die Data Warehouse-Datenbank finden Sie unter [Häufig gestellte Fragen zum Produkt und zur Lizenzierung](/sccm/core/understand/product-and-licensing-faq). <!-- sms500967 -->


> [!IMPORTANT]  
> Das Data Warehouse wird nicht unterstützt, wenn der Computer, der den Data Warehouse-Dienstpunkt ausführt oder die Data Warehouse-Datenbank hostet, eine der folgenden Sprachen ausführt:
> - JPN – Japanisch
> - KOR – Koreanisch
> - CHS – Einfaches Chinesisch
> - CHT – Traditionelles Chinesisch. Dieses Problem wird in einem zukünftigen Release behoben.


## <a name="install-the-data-warehouse"></a>Installieren des Data Warehouse
Jede Hierarchie unterstützt auf jedem Standortsystem des obersten Standorts eine einzelne Instanz dieser Rolle. Der SQL Server, der die Datenbank für Warehouse hostet, kann für die Standortsystemrolle sowohl lokal als auch remote sein. Das Data Warehouse arbeitet mit dem Reporting Services-Punkt, der am gleichen Standort installiert ist. Die Installation der zwei Standortsystemrollen auf demselben Server ist nicht erforderlich.   

Um die Rolle zu installieren, verwenden Sie den **Assistent zum Hinzufügen von Standortsystemrollen** oder den **Assistent zum Erstellen von Standortsystemservern**. Weitere Informationen finden Sie unter [Installieren von Standortsystemrollen](/sccm/core/servers/deploy/configure/install-site-system-roles).  

Bei der Installation einer Rolle erstellt Configuration Manager die Data Warehouse-Datenbank auf der von Ihnen bestimmten Instanz von SQL Server für Sie. Wenn Sie den Namen einer bereits vorhandenen Datenbank angeben (wie bei [Verschieben der Data Warehouse-Datenbank auf einen neuen SQL Server](#move-the-data-warehouse-database)), wird Configuration Manager keine neue Datenbank erstellen, sondern stattdessen die von Ihnen bestimmte verwenden.

### <a name="configurations-used-during-installation"></a>Konfigurationen, die während der Installation verwendet werden.
Seite **Auswahl der Systemrolle**:  

Seite **Allgemein**:
-   **Datenbankverbindungseinstellungen für das Configuration Manager-Data Warehouse**:
     - **Vollqualifizierter SQL Server-Domänenname**: Geben Sie den vollqualifizierten Domänennamen (Full Qualified Domain Name; FQDN) des Servers an, der den Data Warehouse-Dienstpunkt hostet.
     - **SQL Server-Instanzname (falls zutreffend)**: Wenn Sie keine Standardinstanz des SQL Servers verwenden, müssen Sie die Instanz festlegen.
     - **Datenbankname**: Geben Sie den Namen für die Data Warehouse-Datenbank an. Der Name der Datenbank darf nicht länger als 10 Zeichen sein. (Die unterstützte Länge wird in einer zukünftigen Version erhöht werden).
     Configuration Manager erstellt die Data Warehouse-Datenbank mit diesem Namen. Wenn ein Datenbankname angegeben wird, der bereits in der Instanz von SQL Server existiert, verwendet Configuration Manager diese Datenbank.
     - **Verwendeter SQL Server-Port für die Verbindung**: Geben Sie die TCP/IP-Portnummer an, die für den SQL Server konfiguriert ist, der die Data Warehouse-Datenbank hostet. Dieser Port wird vom Data Warehouse-Synchronisierungsdienst verwendet, um eine Verbindung mit der Data Warehouse-Datenbank herzustellen.  
     - **Konto für Data Warehouse-Dienstpunkt:** Ab Version 1802 geben Sie hiermit das Konto an, das von SQL Server Reporting Services beim Herstellen einer Verbindung mit der Data Warehouse-Datenbank verwendet wird. 

Seite **Synchronisierungszeitplan**:   
- **Synchronisierungszeitplan**:
    - **Startzeit**: Geben Sie die Zeit an, zu der mit der Synchronisierung von Data Warehouse begonnen werden soll.
    - **Wiederholungsmuster**:
         - **Täglich**: Legen Sie fest, dass die Synchronisierung täglich durchgeführt wird.
         - **Wöchentlich**: Legen Sie einen Tag in der Woche fest, an dem die Synchronisierung wöchentlich durchgeführt werden soll.


## <a name="reporting"></a>Berichterstellung
Nachdem Sie einen Data Warehouse-Dienstpunkt installiert haben, sind mehrere Berichte unter dem Reporting Services-Punkt verfügbar, der am gleichen Standort installiert ist. Wenn Sie den Data Warehouse-Dienstpunkt vor der Installation eines Reporting Services-Punkts installieren, werden die Berichte automatisch mit der späteren Installation des Reporting Services-Punkt hinzugefügt.

>[!WARNING]
>Ab Configuration Manager Version 1802 werden alternative Anmeldeinformationen für den Data Warehouse-Punkt unterstützt. <!--507334-->Wenn Sie für eine frühere Version von Configuration Manager ein Upgrade durchgeführt haben, müssen Sie Anmeldeinformationen angeben, mit denen SQL Server Reporting Services eine Verbindung mit der Data Warehouse-Datenbank herstellen kann. Data Warehouse-Berichte können erst nach Angabe der Anmeldeinformationen geöffnet werden. Navigieren Sie zum Angeben eines Kontos zu **Verwaltung** >**Standortkonfiguration** >**Servers and Site System Roles** (Server und Standortsystemrollen). Klicken Sie auf den Server mit dem Data Warehouse-Dienstpunkt, und klicken Sie anschließend mit der rechten Maustaste auf die Data Warehouse-Dienstpunktrolle. Klicken Sie auf **Eigenschaften**, und geben Sie dann das **Konto für Data Warehouse-Dienstpunkt** an.

Die Data Warehouse-Standortsystemrolle beinhaltet folgende Berichte in der Kategorie **Data Warehouse**:
 - **Anwendungsbereitstellungsbericht – Verlauf**: Anzeigen von Details zur Anwendungsbereitstellung für eine bestimmte Anwendung und einen bestimmten Computer
 - **Endpoint Protection und Software Update-Kompatibilitätsbericht – Verlauf**: Anzeigen von Computern mit fehlenden Softwareupdates.  
 - **Bestandsbericht zur gesamten Hardware – Verlauf**: Anzeigen des gesamten Hardwarebestands für einen bestimmten Computer
 - **Bestandsbericht zur gesamten Software – Verlauf**: Anzeigen des gesamten Softwarebestands für einen bestimmten Computer
 - **Übersicht der Infrastrukturintegrität – Verlauf**: Anzeigen einer Übersicht der Integrität der Configuration Manager-Infrastruktur
 - **Liste der erkannten Malware – Verlauf**: Anzeigen von in der Organisation gefundenen Malware
 - **Übersicht der Softwareverteilung – Verlauf**: Eine Zusammenfassung der Softwareverteilung für eine bestimmte Ankündigung und einen bestimmten Computer


## <a name="expand-an-existing-stand-alone-primary-into-a-hierarchy"></a>Erweitern eines vorhandenen eigenständigen primären Standorts in eine Hierarchie
Bevor Sie einen Standort der zentralen Verwaltung installieren können, um einen vorhandenen eigenständigen primären Standort zu erweitern, müssen Sie zunächst die Rolle „Data Warehouse-Dienstpunkt“ installieren. Nach der Installation des Standorts der zentralen Verwaltung können Sie die Standortsystemrolle am Standort der zentralen Verwaltung installieren.  

Im Gegensatz zum Bewegen der Data Warehouse-Datenbank führt diese Änderung zum Verlust aller Verlaufsdaten, die vorher am primären Standort synchronisiert wurden. Eine Sicherung der Datenbank am primären Standort und eine Wiederherstellung am Standort der zentralen Verwaltung werden nicht unterstützt.




## <a name="move-the-data-warehouse-database"></a>Verschieben der Data Warehouse-Datenbank
Führen Sie zum Verschieben der Data Warehouse-Datenbank auf einen neuen Server von SQL Server die folgenden Schritte aus:

1.  Verwenden Sie SQL Server Management Studio, um die Datawarehouse-Datenbank zu sichern. Stellen Sie dann die Datenbank in einem SQL Server auf einem Computer wieder her, auf dem das Data Warehouse gehostet wird.   
> [!NOTE]     
> Nachdem Sie die Datenbank auf dem neuen Server wiederhergestellt haben, stellen Sie sicher, dass die Zugriffsberechtigungen der neuen Data Warehouse-Datenbank identisch zu den ursprüngliche Data Warehouse-Datenbank sind.  

2.  Verwenden Sie die Configuration Manager-Konsole, um die Standortsystemrolle des Data Warehouse-Dienstpunkts vom aktuellen Server zu entfernen.
3.  Installieren Sie den Data Warehouse-Dienstpunkt neu. Geben Sie den Namen des neuen Servers von SQL Server und der Instanz an, die die von Ihnen wiederhergestellte Data Warehouse-Datenbank hosten.
4.  Nach der Installation der Standortsystemrolle ist der Verschiebevorgang abgeschlossen.

## <a name="troubleshooting-data-warehouse-issues"></a>Problembehandlung von Data Warehouse-Problemen
**Protokolldateien**  
Verwenden Sie die folgenden Protokolle zur Untersuchung von Problemen bei der Installation des Data Warehouse-Dienstpunkts oder der Synchronisierung von Daten:
 - *DWSSMSI.log* und *DWSSSetup.log*: Verwenden Sie diese Protokolle, um Fehler bei der Installation des Data Warehouse-Dienstpunkts zu untersuchen.
 - *Microsoft.ConfigMgrDataWarehouse.log*: Verwenden Sie dieses Protokoll, um die Datensynchronisation zwischen der Standortdatenbank und der Data Warehouse-Datenbank zu untersuchen.

**Fehler beim Einrichten**  
 Die Installation des Data Warehouse-Dienstpunkts schlägt auf einem Remote-Standortsystemserver fehl, wenn Data Warehouse die erste Standortsystemrolle ist, die auf diesem Computer installiert wird.  
  - **Lösung**: Stellen Sie sicher, das der Computer, auf dem Sie den Data Warehouse-Dienstpunkt installieren möchten, bereits mindestens eine Standortsystemrolle hostet.  


**Bekannte Probleme beim Synchronisieren**:   
Die Synchronisierung schlägt mit folgender Meldung im *Microsoft.ConfigMgrDataWarehouse.log* fehl: „**failed to populate schema objects**“ (Auffüllen der Schemaobjekte fehlgeschlagen)  
 - **Lösung**: Stellen Sie sicher, dass das Computerkonto des Computers, der die Standortsystemrolle hostet, in der Data Warehouse-Datenbank ein **db_owner** ist.

Data Warehouse-Berichte können nicht geöffnet werden, wenn die Data Warehouse-Datenbank und der Reporting Services-Punkt sich auf unterschiedlichen Standortsystemen befinden.  

 - **Lösung**: Weisen Sie dem **Konto des Reporting Services-Punkts** die Berechtigung **db_datareader** für die Data Warehouse-Datenbank zu.

Beim Öffnen eines Data Warehouse-Berichts wird folgender Fehler zurückgegeben:

*Fehler bei der Berichtsverarbeitung. (rsProcessingAborted) Es kann keine Verbindung mit der „AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_“-Datenquelle hergestellt werden. (rsErrorOpeningConnection) Es konnte eine Verbindung mit dem Server hergestellt werden, doch während des Handshakes vor der Anmeldung trat ein Fehler auf. (Anbieter: SSL-Anbieter, Fehler: 0 – Die Zertifikatkette wurde von einer nicht vertrauenswürdigen Zertifizierungsstelle ausgestellt.)*

- **Lösung**: So konfigurieren Sie Zertifikate:

  1. Auf dem Computer, auf dem der Serverteil des Data Warehouse gehostet wird:

    1. Öffnen Sie IIS, klicken Sie auf **Serverzertifikate**, klicken Sie mit der rechten Maustaste auf **Selbstsigniertes Zertifikat erstellen**, und geben Sie dann den „geeigneten Namen“ des Zertifikatnamens als **Data Warehouse SQL Server Identification Certificate** (Data Warehouse SQL Server-Idenfikationszertifikat) an. Wählen Sie für Zertifikatspeicher **Persönlich** aus.
    2. Öffnen Sie unter **SQL Server-Netzwerkkonfiguration** **SQL Server Configuration Manager**, und klicken Sie unter **Protocols for MSSQLSERVER** (Protokolle für MMSSQLSERVER) mit der rechten Maustaste auf **Eigenschaften**. Wählen Sie dann auf der Registerkarte **Zertifikate** **Data Warehouse SQL Server Identification Certificate** (Data Warehouse SQL Server-Idenfikationszertifikat) als Zertifikat aus, und speichern Sie dann die Änderungen.  
    3. Öffnen Sie **SQL Server Configuration Manager**. Starten Sie unter **SQL Server-Dienste** den **SQL Server-Dienst** und den **Berichtsdienst** neu.
    4.  Öffnen Sie die Microsoft Management Console (MMC), und fügen Sie das Snap-In für **Zertifikate** hinzu; wählen Sie dann aus, dass Sie die **Computerkonten** des lokalen Computer verwalten möchten. Erweitern Sie dann in der MMC den Ordner **Persönlich** > **Zertifikate**, und exportieren Sie das **Data Warehouse SQL Server Identification Certificate** (Data Warehouse SQL Server-Idenfikationszertifikat) als **DER-codierte binäre X.509 (.CER)**.Datei.    
  2.    Öffnen Sie auf dem Computer, der SQL Server-Reporting Services hostet, die MMC, und fügen Sie das Snap-In für **Zertifikate** hinzu. Wählen Sie dann aus, dass Sie Zertifikate für das **Computerkonto** verwalten möchten. Importieren Sie im Ordner **Als vertrauenswürdig eingestufte Stammzertifizierungsstelle** das **Data Warehouse SQL Server Identification Certificate** (Data Warehouse SQL Server-Idenfikationszertifikat).


## <a name="data-warehouse-dataflow"></a>Data Warehouse-Datenfluss   
![Diagramm, auf dem der logische Datenfluss zwischen den Standortkomponenten für das Data Warehouse dargestellt wird](./media/datawarehouse.png)

**Datenspeicher und Synchronisierung**

| Schritt   | Details  |
|:------:|-----------|  
| **1**  |  Der Standortserver überträgt und speichert Daten in der Standortdatenbank.  |  
| **2**  |      Basierend auf Zeitplan und Konfiguration, ruft der Data Warehouse-Dienstpunkt Daten aus der Standortdatenbank ab.  |  
| **3**  |  Der Data Warehouse-Dienstpunkt überträgt und speichert eine Kopie der synchronisierten Daten in der Data Warehouse-Datenbank. |  
**Berichterstellung**

| Schritt   | Details  |
|:------:|-----------|  
| **A**  |  Mithilfe integrierter Berichte fordert ein Benutzer Daten an. Diese Anforderung wird mittels SQL Server Reporting Services an den Reporting Services-Punkt übertragen. |  
| **B**  |      Die meisten Berichte gelten für aktuelle Informationen. Diese Anfragen werden in der Standortdatenbank ausgeführt. |  
| **C**  | Wenn ein Bericht über einen der Berichte mit der *Kategorie* **Data Warehouse** alte Daten anfordert, ist die Data Warehouse-Datenbank das Ziel der Anfrage.   |  
