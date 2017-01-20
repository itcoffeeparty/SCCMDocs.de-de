---
title: Konfigurieren von Asset Intelligence | Microsoft-Dokumentation
description: Richten Sie Asset Intelligence in System Center Configuration Manager ein.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: ed62dd273dfa5896c0bc0a8f6216755f44ce3513


---
# <a name="configure-asset-intelligence-in-system-center-configuration-manager"></a>Konfigurieren von Asset Intelligence in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie müssen mehrere Konfigurationsschritte ausführen, bevor Sie Asset Intelligence in System Center Configuration Manager dazu verwenden können, Softwarelizenzen unternehmensübergreifend zu inventarisieren und zu verwalten.  

## <a name="steps-to-configure-asset-intelligence"></a>Schritte zum Konfigurieren von Asset Intelligence  
 Um die Inventurdaten zu sammeln, die für Asset Intelligence-Berichte benötigt werden, muss der Hardwareinventurclient-Agent aktiviert werden. Informationen zum Aktivieren des Hardwareinventur-Clientagents finden Sie unter [How to extend hardware inventory in System Center Configuration Manager (Erweitern der Hardwareinventur in System Center Configuration Manager)](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

|Schritt|Details|Weitere Informationen|  
|----------|-------------|----------------------|  
|**Schritt 1**: Aktivieren von Asset Intelligence-Hardwareinventur-Berichtsklassen|Die Asset Intelligence-Informationssammlung ist nicht aktiviert, wenn Configuration Manager erstmalig installiert wird. Wenn Sie Asset Intelligence aktivieren möchten, muss mindestens eine der erforderlichen Hardwareinventur-Berichtsklassen aktiviert sein, auf die sich die Asset Intelligence-Berichte stützen.|Weitere Informationen finden Sie im folgenden Verfahren dieses Themas: [Enable Asset Intelligence hardware inventory reporting classes](#BKMK_EnableAssetIntelligence).|  
|**Schritt 2**: Installieren eines Asset Intelligence-Synchronisierungspunkts|Die Standortsystemrolle des Asset Intelligence-Synchronisierungspunkts wird verwendet, um eine Verbindung von Configuration Manager-Standorten zu System Center Online herstellen und Asset Intelligence-Kataloginformationen synchronisieren zu können. Der Asset Intelligence-Synchronisierungspunkt kann nur auf einem Standortsystem installiert werden, das sich am Standort der obersten Ebene in der Configuration Manager-Hierarchie befindet, und erfordert für die Synchronisierung mit System Center Online über TCP-Port 443 eine Internetverbindung.<br /><br /> Zusätzlich zum Herunterladen neuer Asset Intelligence-Kataloginformationen können vom Asset Intelligence-Synchronisierungspunkt Informationen zu benutzerdefinierten Softwaretiteln zur Kategorisierung in System Center Online hochgeladen werden. Microsoft behandelt alle Softwaretitel, die zur Kategorisierung in System Center Online hochgeladen wurden, als öffentliche Informationen. Achten Sie daher darauf, dass Ihre benutzerdefinierten Softwaretitel keine vertraulichen oder proprietären Informationen enthalten. Weitere Informationen zu Kategorisierungsanforderungen für Softwaretitel finden Sie unter [Request a catalog update for uncategorized software titles (Anfordern eines Katalogupdates für nicht kategorisierte Softwaretitel)](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).|Weitere Informationen finden Sie im folgenden Verfahren dieses Themas: [Install an Asset Intelligence Synchronization Point](#BKMK_InstallAssetIntelligenceSynchronizationPoint).|  
|**Schritt 3**: Aktivieren der Überwachung erfolgreicher Anmeldeereignisse|In vier Asset Intelligence-Berichten werden Informationen angezeigt, die aus den Windows-Sicherheitsereignisprotokollen auf den Clientcomputern zusammengestellt werden. Wenn die Einstellungen des Sicherheitsereignisprotokolls nicht so konfiguriert sind, dass alle erfolgreichen Anmeldeereignisse protokolliert werden, enthalten diese Berichte selbst dann keine Daten, wenn die entsprechende Hardwareinventur-Berichterstattungsklasse aktiviert ist. Damit der Hardwareinventurclient-Agent die zur Unterstützung dieser Berichte erforderlichen Informationen inventarisieren kann, müssen Sie zunächst die Einstellungen für das Windows-Sicherheitsereignisprotokoll auf Clients so ändern, dass alle erfolgreichen Anmeldeereignisse protokolliert werden, und Sie müssen die Hardwareinventur-Berichterstattungsklasse **SMS_SystemConsoleUser** aktivieren.|Weitere Informationen finden Sie in den folgenden Verfahren dieses Themas: [Enable auditing of success logon events](#BKMK_EnableSuccessLogonEvents).|  
|**Schritt 4**: Importieren von Softwarelizenzinformationen|Der Assistent zum Importieren von Softwarelizenzen wird verwendet, um Microsoft-Volumenlizenzierungsinformationen (Microsoft Volume Licensing, MVLS) und allgemeine Lizenzübersichten in den Asset Intelligence-Katalog zu importieren.<br /><br /> Die MVLS-Lizenzübersicht enthält Informationen über die Lizenzberechtigungen bzw. die Anzahl erworbener Lizenzen für Produkte von Microsoft.<br /><br /> Allgemeine Lizenzübersichten enthalten Informationen über die erworbenen Lizenzen aller Herausgeber.|Weitere Informationen finden Sie in den folgenden Verfahren dieses Themas: [Import software license information](#BKMK_ImportSoftwareLicenseInformation).|  
|**Schritt 5**: Konfigurieren von Asset Intelligence-Wartungstasks|Die folgenden Wartungstasks werden Asset Intelligence zugeordnet. In der Standardeinstellung sind beide Wartungstasks aktiviert und nach einem Standardzeitplan konfiguriert.<br /><br /> **Anwendungstitel mit Inventurinformationen prüfen**: Mit diesem Wartungstask wird überprüft, ob ein im Softwareinventar gemeldeter Softwaretitel mit dem Softwaretitel im Asset Intelligence-Katalog abgestimmt ist.<br /><br /> **Daten installierter Software zusammenfassen**: Dieser Wartungstask stellt die Informationen zur Verfügung, die im Arbeitsbereich **Bestand und Kompatibilität** unter dem Knoten **Asset Intelligence** im Knoten **Inventarisierte Software** angezeigt werden. Wenn der Task ausgeführt wird, wird die Anzahl aller inventarisierten Softwaretitel am primären Standort von Configuration Manager gesammelt.|Weitere Informationen finden Sie in den folgenden Verfahren dieses Themas: [Configure Asset Intelligence maintenance tasks](#BKMK_ConfigureMaintenanceTasks).|  

> [!NOTE]  
>  Der Wartungstask **Daten installierter Software zusammenfassen** ist nur an primären Standorten verfügbar.  

## <a name="supplemental-procedures-for-configuring-asset-intelligence"></a>Zusätzliche Verfahren zum Konfigurieren von Asset Intelligence  
 Verwenden Sie die folgenden Informationen, um die Schritte in der obigen Tabelle auszuführen.  

###  <a name="a-namebkmkenableassetintelligencea-enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Zum Aktivieren von Asset Intelligence in Configuration Manager-Standorten müssen Sie mindestens eine Asset Intelligence-Hardwareinventur-Berichtsklasse aktivieren. Sie können die Klassen auf der **Asset Intelligence** -Startseite oder im Arbeitsbereich **Verwaltung** im Knoten **Clienteinstellungen** in den Eigenschaften der Clienteinstellungen aktivieren. Verwenden Sie eins der folgenden Verfahren, um die Asset Intelligence-Hardwareinventur-Berichtsklassen zu aktivieren.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>So aktivieren Sie Asset Intelligence-Hardwareinventur-Berichtsklassen von der Asset Intelligence-Startseite aus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Asset Intelligence**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Asset Intelligence** auf **Inventurklassen bearbeiten**. Das Dialogfeld **Inventurklassen bearbeiten** wird geöffnet.  

4.  Zum Aktivieren der Asset Intelligence-Berichterstattung wählen Sie **Alle Asset Intelligence-Berichtsklassen aktivieren** oder **Nur die ausgewählten Asset Intelligence-Berichtsklassen aktivieren**und mindestens eine der angezeigten Berichtsklassen aus.  

    > [!NOTE]  
    >  In den von den Hardwareinventurklassen abhängigen Asset Intelligence-Berichten, die mit diesem Verfahren aktiviert werden, werden erst dann Daten angezeigt, wenn die Hardwareinventurdaten von den Clients überprüft und zurückgegeben wurden.  

5.  Klicken Sie auf **OK** , um die ausgewählten Asset Intelligence-Hardwareinventur-Berichtsklassen zu aktivieren.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>So aktivieren Sie Asset Intelligence-Hardwareinventur-Berichtsklassen in den Eigenschaften der Clienteinstellungen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Clienteinstellungen**, und wählen Sie dann **Client-Agent-Standardeinstellungen**.  

    > [!NOTE]  
    >  Wenn Sie benutzerdefinierte Clienteinstellungen erstellt haben, können Sie diese anstatt der Standardclienteinstellungen auswählen.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**. Das Dialogfeld **Eigenschaften der Clienteinstellungen** wird geöffnet.  

4.  Klicken Sie auf **Hardwareinventur**und dann auf **Klassen festlegen**. Das Dialogfeld **Hardwareinventurklassen** wird geöffnet.  

5.  Klicken Sie auf **Nach Kategorie filtern**und dann auf **Asset Intelligence-Berichtsklassen**. In der aktualisierten Liste werden nur Asset Intelligence-Hardwareinventur-Berichtsklassen angezeigt.  

6.  Wählen Sie mindestens eine Berichtsklasse aus der Liste der Asset Intelligence-Berichtsklassen aus.  

    > [!NOTE]  
    >  In den von den Hardwareinventurklassen abhängigen Asset Intelligence-Berichten, die mit diesem Verfahren aktiviert werden, werden erst dann Daten angezeigt, wenn die Hardwareinventurdaten von den Clients überprüft und zurückgegeben wurden.  

7.  Klicken Sie auf **OK** , um die ausgewählten Asset Intelligence-Hardwareinventur-Berichtsklassen zu aktivieren.  

###  <a name="a-namebkmkinstallassetintelligencesynchronizationpointa-install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  
 Gehen Sie zum Installieren einer Asset Intelligence-Synchronisierungspunkt-Standortsystemrolle wie folgt vor.  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>So installieren Sie eine Asset Intelligence-Synchronisierungspunkt-Standortsystemrolle  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Server und Standortsystemrollen**.  

3.  Fügen Sie die Standortsystemrolle für den Asset Intelligence-Synchronisierungspunkt mit dem folgenden Schritt zu einem neuen oder bestehenden Standortsystemserver hinzu:  

    -   **Neuer Standortsystemserver**: Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Standortsystemserver erstellen**. Der Assistent zum Erstellen von Standortsystemservern wird geöffnet.  

        > [!NOTE]  
        >  Wenn eine Standortsystemrolle von Configuration Manager in der Standardeinstellung installiert wird, erfolgt die Installation auf dem ersten verfügbaren NTFS-formatierten Festplattenlaufwerk, das genügend Speicherplatz bietet. Soll die Installation durch Configuration Manager nicht auf einem bestimmten Laufwerk vorgenommen werden, erstellen Sie eine leere Datei mit dem Namen „No_sms_on_drive.sms“, und kopieren Sie sie in den Stammordner des Laufwerks, bevor Sie den Standortsystemserver installieren.  

    -   **Bestehender Standortsystemserver**: Klicken Sie auf den Server, auf dem die Standortsystemrolle "Asset Intelligence-Synchronisierungspunkt" installiert werden soll. Wenn Sie auf einen Server klicken, wird im Detailbereich eine Liste der Standortsystemrollen angezeigt, die bereits auf dem Server installiert sind.  

         Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Server** auf **Standortsystemrollen hinzufügen**. Der Assistent zum Hinzufügen von Standortsystemrollen wird geöffnet.  

4.  Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für den Standortsystemserver an. Soll der Asset Intelligence-Synchronisierungspunkt zu einem bestehenden Standortsystemserver hinzugefügt werden, überprüfen Sie die zuvor konfigurierten Werte.  

5.  Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen **Asset Intelligence-Synchronisierungspunkt** aus, und klicken Sie dann auf **Weiter**.  

6.  Klicken Sie auf der Seite **Asset Intelligence-Synchronisierungspunkteinstellungen** auf **Weiter**.  

     Die Einstellung **Diesen Asset Intelligence-Synchronisierungspunkt verwenden** ist in der Standardeinstellung ausgewählt und kann auf dieser Seite nicht konfiguriert werden. Von System Center Online wird Netzwerkverkehr nur über TCP-Port 443 akzeptiert, daher können die Einstellungen für die **SSL-Portnummer** auf dieser Seite des Assistenten nicht konfiguriert werden.  

7.  Sie können optional einen Pfad zur System Center Online-Authentifizierungszertifikatdatei (.pfx) angeben und dann auf **Weiter**klicken. Normalerweise geben Sie keinen Pfad für das Zertifikat an, weil das Verbindungszertifikat bei der Standortrolleninstallation automatisch bereitgestellt wird.  

8.  Geben Sie auf der Seite **Proxyservereinstellungen** an, ob vom Asset Intelligence-Synchronisierungspunkt ein Proxyserver für die Verbindung mit System Center Online verwendet werden soll, um den Katalog zu synchronisieren, und ob bei der Verbindung mit dem Proxyserver Anmeldeinformationen verwendet werden sollen. Klicken Sie dann auf **Weiter**.  

    > [!WARNING]  
    >  Wenn zur Verbindung mit System Center Online ein Proxyserver erforderlich ist, kann das Verbindungszertifikat auch dann gelöscht werden, wenn das Benutzerkontokennwort für das zur Proxyserverauthentifizierung konfigurierte Konto abläuft.  

9. Geben Sie auf der Seite **Synchronisierungszeitplan** an, ob der Asset Intelligence-Katalog nach einem Zeitplan synchronisiert werden soll. Wenn Sie den Synchronisierungszeitplan aktivieren, geben Sie einen einfachen oder einen benutzerdefinierten Synchronisierungszeitplan an. Bei der geplanten Synchronisierung wird vom Asset Intelligence-Synchronisierungspunkt eine Verbindung mit System Center Online hergestellt, um den aktuellsten Asset Intelligence-Katalog abzurufen. Sie können den Asset Intelligence-Katalog im Knoten „Asset Intelligence“ in der Configuration Manager-Konsole manuell synchronisieren. Die Schritte für die manuelle Synchronisierung des Asset Intelligence-Katalogs finden Sie im Abschnitt [To manually synchronize the Asset Intelligence catalog (So führen Sie eine manuelle Synchronisierung des Asset Intelligence-Katalogs durch)](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) in [Operations for Asset Intelligence in System Center Configuration Manager (Vorgänge für Asset Intelligence in System Center Configuration Manager)](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. Überprüfen Sie vor dem Fortfahren auf der Seite **Zusammenfassung** des Assistenten die angegebenen Einstellungen. Um Änderungen an den Einstellungen vorzunehmen, klicken Sie so lange auf **Zurück** , bis Sie die entsprechende Seite aufgerufen haben, ändern Sie die Einstellungen, und kehren Sie zur Seite **Zusammenfassung** zurück.  

###  <a name="a-namebkmkenablesuccesslogoneventsa-enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Gehen Sie folgendermaßen vor, um Sicherheitsrichtlinien für die Anmeldungseinstellungen zur Überprüfung erfolgreicher Anmeldeereignisse zu konfigurieren.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>So aktivieren Sie die Protokollierung von erfolgreichen Anmeldeereignissen mithilfe einer lokalen Sicherheitsrichtlinie  

1.  Klicken Sie auf einem Configuration Manager-Clientcomputer auf **Starten**, zeigen Sie auf **Verwaltungstools**, und klicken Sie auf **Lokale Sicherheitsrichtlinie**.  

2.  Erweitern Sie im Dialogfeld **Lokale Sicherheitsrichtlinie** unter **Sicherheitseinstellungen** **Lokale Richtlinien**, und klicken Sie auf **Überwachungsrichtlinie**.  

3.  Doppelklicken Sie im Ergebnisbereich auf **Anmeldeereignisse überwachen**, vergewissern Sie sich, dass das Kontrollkästchen **Erfolg** aktiviert ist, und klicken Sie auf **OK**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>So aktivieren Sie die Protokollierung von erfolgreichen Anmeldeereignissen mithilfe einer Active Directory-Domänensicherheitsrichtlinie  

1.  Klicken Sie auf einem Domänencontrollercomputer auf **Starten**, zeigen Sie auf **Verwaltungstools**, und klicken Sie auf **Domänensicherheitsrichtlinie**.  

2.  Erweitern Sie im Dialogfeld **Lokale Sicherheitsrichtlinie** unter **Sicherheitseinstellungen** **Lokale Richtlinien**, und klicken Sie auf **Überwachungsrichtlinie**.  

3.  Doppelklicken Sie im Ergebnisbereich auf **Anmeldeereignisse überwachen**, vergewissern Sie sich, dass das Kontrollkästchen **Erfolg** aktiviert ist, und klicken Sie auf **OK**.  

###  <a name="a-namebkmkimportsoftwarelicenseinformationa-import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 In den folgenden Abschnitten werden die erforderlichen Vorgehensweisen zum Importieren von Microsoft- und allgemeinen Softwarelizenzierungsinformationen in die Configuration Manager-Standortdatenbank mithilfe des Assistenten zum Importieren von Softwarelizenzen beschrieben. Beim Importieren von Softwarelizenzinformationen aus Lizenzübersichtsdateien in die Standortdatenbank wird für das Computerkonto des Standortservers **Vollzugriff** im NTFS-Dateisystem auf die Dateifreigabe benötigt, die zum Importieren der Softwarelizenzinformationen verwendet wird.  

> [!IMPORTANT]  
>  Beim Import von Softwarelizenzinformationen in die Standortdatenbank werden vorhandene Softwarelizenzinformationen überschrieben. Vergewissern Sie sich, dass die mit dem Assistenten zum Importieren von Softwarelizenzen verwendete Datei mit Softwarelizenzinformationen eine vollständige Liste aller erforderlichen Softwarelizenzinformationen enthält.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>So importieren Sie Softwarelizenzinformationen in den Asset Intelligence-Katalog  

1.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Asset Intelligence**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Asset Intelligence** auf **Softwarelizenzen importieren**. Der Assistent zum Importieren von Softwarelizenzen wird geöffnet.  

3.  Klicken Sie auf der Seite **Willkommen** auf **Weiter**.  

4.  Geben Sie auf der Seite **Importieren** an, ob eine Microsoft-Volumenlizenzierungsdatei (MVLS) (.xml oder .csv) oder eine allgemeine Lizenzzusammenfassung (.csv) importiert werden soll. Weitere Informationen zum Erstellen einer allgemeinen Lizenzübersichtsdatei finden Sie unter [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) weiter unten in diesem Thema.  

    > [!WARNING]  
    >  Informationen zum Herunterladen einer MVLS-Datei im CSV-Format, die in den Asset Intelligence-Katalog importiert werden kann, finden Sie im [Microsoft Volume Licensing Service Center](http://go.microsoft.com/fwlink/p/?LinkId=226547). Für den Zugriff auf diese Informationen benötigen Sie ein registriertes Konto auf der Website. Wenden Sie sich an Ihren Microsoft-Kontobeauftragten, um sich zu informieren, wie Sie Ihre MVLS-Datei im XML-Format erhalten.  

5.  Geben Sie den UNC-Pfad zur Lizenzzusammenfassungsdatei ein, oder klicken Sie auf **Durchsuchen** , um einen freigegebenen Netzwerkordner und die entsprechende Datei auszuwählen.  

    > [!NOTE]  
    >  Der freigegebene Ordner muss ordnungsgemäß gesichert sein, um nicht autorisierte Zugriffe auf die Lizenzinformationsdatei zu verhindern. Außerdem muss das Computerkonto des Computers, auf dem der Assistent ausgeführt wird, Vollzugriff auf die Freigabe haben, in der sich die Lizenzimportdatei befindet.  

6.  Vergewissern Sie sich auf der Seite **Zusammenfassung** , dass die angegebenen Informationen korrekt sind, bevor Sie fortfahren. Wenn Änderungen erforderlich sind, klicken Sie auf **Zurück** , um zur Seite **Importieren** zurückzukehren.  

###  <a name="a-namebkmkcreategenerallicensestatementa-create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
 Eine allgemeine Lizenzübersicht kann auch mithilfe einer manuell im kommagetrennten CSV-Dateiformat erstellten Lizenzimportdatei in den Asset Intelligence-Katalog importiert werden.  

> [!NOTE]  
>  Obwohl nur in den Feldern **Name**, **Herausgeber**, **Version**und **Tatsächliche Menge** Daten enthalten sein müssen, ist die Eingabe in alle Felder der ersten Zeile der Lizenzimportdatei obligatorisch. Alle Datumsfelder müssen das folgende Format aufweisen: Monat/Tag/Jahr, z. B. 08/04/2008.  

 Von Asset Intelligence werden die Produkte, die Sie in der allgemeinen Lizenzerklärung angeben, anhand von Produktnamen und Produktversion abgeglichen, jedoch nicht anhand des Namens des Herausgebers. Sie müssen in der allgemeinen Lizenzerklärung einen Produktnamen verwenden, der exakt mit dem in der Standortdatenbank gespeicherten Produktnamen übereinstimmt. Von Asset Intelligence wird der Wert **Tatsächliche Menge**, der in der allgemeinen Lizenzerklärung angegeben ist, mit der Anzahl installierter Produkte verglichen, die bei der Configuration Manager-Inventur gefunden werden.  

> [!TIP]  
>  Für eine vollständige Liste der in der Configuration Manager-Standortdatenbank gespeicherten Produktnamen können Sie in der Standortdatenbank die folgende Abfrage ausführen: SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE.  

 Sie können die exakte Version oder einen Teil der Version (z. B. die Hauptversion) für ein Produkt angeben. Die folgenden Beispiele sind die Übereinstimmungen der Version mit einem Versionseintrag einer allgemeinen Lizenzzusammenfassung für ein bestimmtes.  

|Eintrag der allgemeinen Lizenzzusammenfassung|Übereinstimmende Standortdatenbankeinträge|  
|-------------------------------------|------------------------------------|  
|Name: "MeineSoftware", ProductVersion0: "2"|ProductName0: "MeineSoftware", ProductVersion0: "2.01.1234"<br /><br /> ProductName0: "MeineSoftware", ProductVersion0: "2.02.5678"<br /><br /> ProductName0: "MeineSoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MeineSoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MeineSoftware", ProductVersion0: "2.05.3579.000"<br /><br /> ProductName0: "MeineSoftware", ProductVersion0: "2.10.1234"|  
|Name: "MeineSoftware", Version "2.05"|ProductName0: "MeineSoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MeineSoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MeineSoftware", ProductVersion0: "2.05.3579.000"|  
|Name: "MeineSoftware", Version "2"<br /><br /> Name: "MeineSoftware", Version "2.05"|Fehler beim Importieren. Beim Import tritt ein Fehler auf, wenn mehr als ein Eintrag mit derselben Produktversion übereinstimmt.|  

 Im Folgenden wird eine mögliche Vorgehensweise zum Erstellen einer Importdatei für die allgemeine Lizenzzusammenfassung unter Verwendung von Microsoft Excel beschrieben.  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>So erstellen sie eine Importdatei für die allgemeine Lizenzzusammenfassung unter Verwendung von Microsoft Excel  

1.  Öffnen Sie Microsoft Excel, und erstellen Sie ein neues Arbeitsblatt.  

2.  Geben Sie in die erste Zeile der neuen Kalkulationstabelle die Namen aller Softwarelizenz-Datenfelder ein.  

3.  Geben Sie in die zweite sowie die folgenden Zeilen der neuen Kalkulationstabelle die notwendigen Softwarelizenzinformationen ein. Stellen Sie sicher, dass in den darauf folgenden Zeilen für alle zu importierenden Softwarelizenzen mindestens die obligatorischen Softwarelizenz-Datenfelder eingegeben werden. Der in der Kalkulationstabelle eingegebene Softwaretitel muss identisch mit dem Titel sein, der im Anschluss an die Ausführung der Hardwareinventur für einen Client im Ressourcen-Explorer angezeigt wird.  

4.  Klicken Sie im Menü **Datei** auf **Speichern unter**, und speichern Sie die Datei im CSV-Format.  

5.  Kopieren Sie die CSV-Datei in die Dateifreigabe, die für den Import von Softwarelizenzinformationen in den Asset Intelligence-Katalog verwendet wird.  

6.  Verwenden Sie in der Configuration Manager-Konsole den „Assistenten zum Importieren von Softwarelizenzen“, um die neu erstellte CSV-Lizenzinformationsdatei zu importieren.  

7.  Führen Sie den **Asset Intelligence-MVLS-Abstimmungsbericht für Lizenz 15A** aus, um sicherzustellen, dass die Lizenzinformationen erfolgreich in den Asset Intelligence-Katalog importiert wurden.  

> [!NOTE]  
>  Ein Beispiel für eine allgemeine Softwarelizenzdatei, die für Testzwecke verwendet werden kann, finden Sie unter [Operations for Asset Intelligence in System Center Configuration Manager (Beispiel für eine allgemeine Asset Intelligence-Lizenzimportdatei in System Center Configuration Manager)](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Tabelle mit Beispielen zur Beschreibung von Softwarelizenzen  
 Bei der Erstellung einer Importdatei für die allgemeine Lizenzzusammenfassung können die Informationen in der folgenden Tabelle zum Beschreiben der in den Asset Intelligence-Katalog zu importierenden Softwarelizenzen verwendet werden.  

|Spaltenname|Datentyp|Erforderlich|Beispiel|  
|-----------------|---------------|--------------|-------------|  
|Name|Bis zu 255 Zeichen|Ja|Softwaretitel|  
|Herausgeber|Bis zu 255 Zeichen|Ja|Softwareherausgeber|  
|Version|Bis zu 255 Zeichen|Ja|Version des Softwaretitels|  
|Sprache|Bis zu 255 Zeichen|Ja|Sprache des Softwaretitels|  
|Tatsächliche Menge|Ganzzahliger Wert|Ja|Anzahl erworbener Lizenzen|  
|Bestellnummer|Bis zu 255 Zeichen|Nein|Bestellinformationen|  
|Name des Wiederverkäufers|Bis zu 255 Zeichen|Nein|Informationen zum Vertragshändler|  
|Kaufdatum|Datumswert in folgendem Format: TT.MM.JJJJ|Nein|Datum des Lizenzerwerbs|  
|Support erworben|Bitwert|Nein|0 oder 1. Geben Sie 0 für Ja oder 1 für Nein ein.|  
|Ablaufdatum Support|Datumswert in folgendem Format: TT.MM.JJJJ|Nein|Enddatum des erworbenen Supports|  
|Kommentare|Bis zu 255 Zeichen|Nein|Optionale Kommentare|  

###  <a name="a-namebkmkconfiguremaintenancetasksa-configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 Die folgenden Wartungstasks sind für Asset Intelligence verfügbar:  

-   **Anwendungstitel mit Inventurinformationen prüfen**: Mit diesem Wartungstask wird überprüft, ob ein im Softwareinventar gemeldeter Softwaretitel mit dem Softwaretitel im Asset Intelligence-Katalog abgestimmt ist. Dieser Task ist standardmäßig aktiviert und zur Ausführung an Samstagen nach 0:00 Uhr und vor 5:00 Uhr eingeplant. Dieser Wartungstask ist nur am Standort der obersten Ebene in der Configuration Manager-Hierarchie verfügbar.  

-   **Daten installierter Software zusammenfassen**: Dieser Wartungstask stellt die Informationen zur Verfügung, die im Arbeitsbereich **Bestand und Kompatibilität** unter dem Knoten **Asset Intelligence** im Knoten **Inventarisierte Software** angezeigt werden. Wenn der Task ausgeführt wird, wird die Anzahl aller inventarisierten Softwaretitel am primären Standort von Configuration Manager gesammelt. Dieser Task ist standardmäßig aktiviert und zur täglichen Ausführung nach 0:00 Uhr und vor 5:00 Uhr eingeplant. Dieser Wartungstask ist nur an primären Standorten verfügbar.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>So konfigurieren Sie Wartungstasks für Asset Intelligence  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.  

3.  Wählen Sie den Standort aus, an dem der Wartungstask für Asset Intelligence konfiguriert werden soll.  

    > [!NOTE]  
    >  Der Wartungstask **Daten installierter Software zusammenfassen** ist nur an primären Standorten verfügbar.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Standortwartung**. Eine Liste aller verfügbaren Standortwartungstasks wird angezeigt.  

5.  Wählen Sie den gewünschten Wartungstask aus, und klicken Sie dann zum Ändern der Einstellungen auf **Bearbeiten** .  

6.  Aktivieren und konfigurieren Sie den Wartungstask. Es wird empfohlen, den Zeitraum außerhalb der Hauptzeitstunden des Standorts festzulegen, um Beeinträchtigungen des Standortbetriebs zu minimieren. Der Zeitraum ist das Zeitintervall, in dem der Task ausgeführt werden kann. Er wird über die Optionen **Start nach** und **Spätester Startzeitpunkt** im Dialogfeld **Taskeigenschaften** definiert.  

    > [!WARNING]  
    >  Sie können den Task direkt initiieren, indem Sie den aktuellen Tag auswählen und für die Option **Start nach** eine Zeit wenige Minuten nach der aktuellen Zeit festlegen.  

7.  Klicken Sie auf **OK** , um die Einstellungen zu speichern. Der Task wird nun gemäß dem Zeitplan ausgeführt.  

    > [!NOTE]  
    >  Wenn beim ersten Versuch, den Task auszuführen, ein Fehler auftritt, wird von Configuration Manager versucht, den Task solange erneut auszuführen, bis der Task entweder erfolgreich ausgeführt wird oder der Zeitraum, in dem der Task ausgeführt werden kann, verstrichen ist.  



<!--HONumber=Dec16_HO3-->


