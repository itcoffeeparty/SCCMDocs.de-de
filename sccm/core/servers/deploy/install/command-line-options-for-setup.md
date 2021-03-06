---
title: Setup-Befehlszeilenoptionen
titleSuffix: Configuration Manager
description: Erstellen Sie Automatisierungsskripts, um System Center Configuration Manager über die Befehlszeile zu installieren.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fa8e3bf572ced8a2394099bbb59532502ef3b019
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="command-line-options-for-setup-in-system-center-configuration-manager"></a>Befehlszeilenoptionen für das Setup in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 Verwenden Sie die folgenden Informationen, um Skripts zu konfigurieren oder System Center Configuration Manager über die Befehlszeile zu installieren.  

##  <a name="bkmk_setup"></a> Befehlszeilenoptionen für das Setup  
 **/DEINSTALL**  
 Damit wird der Standort deinstalliert. Führen Sie das Setup vom Standortservercomputer aus.  

 **/DONTSTARTSITECOMP**  
 Installiert einen Standort, ohne dass der Standortkomponenten-Manager-Dienst gestartet wird. Der Standort wird erst beim Start des Standortkomponenten-Manager-Diensts aktiv. Der Standortkomponenten-Manager ist für die Installation und den Start des Diensts SMS_Executive und für weitere Prozesse am Standort verantwortlich. Wenn Sie den Standortkomponenten-Manager-Dienst nach Abschluss der Standortinstallation starten, werden der Dienst SMS_Executive sowie weitere Prozesse installiert, die für den Betrieb des Standorts erforderlich sind.  

 **/HIDDEN**  
 Damit wird die Benutzeroberfläche beim Setup ausgeblendet. Verwenden Sie diese Option nur in Verbindung mit der Option **/SCRIPT**. Die Skriptdatei zur unbeaufsichtigten Installation muss alle erforderlichen Optionen bereitstellen, oder das Setup schlägt fehl.  

 **/NOUSERINPUT**  
 Deaktiviert die Benutzereingabe während des Setups, zeigt aber den Setup-Assistenten an. Verwenden Sie diese Option nur in Verbindung mit der Option **/SCRIPT**. Die Skriptdatei zur unbeaufsichtigten Installation muss alle erforderlichen Optionen bereitstellen, oder das Setup schlägt fehl.  

 **/RESETSITE**  
 Damit wird eine Standortrücksetzung ausgeführt, wobei auch die Datenbank und Dienstkonten des Standorts zurückgesetzt werden. Sie müssen das Setup über **<*Configuration Manager-Installationspfad*>\BIN\X64** auf dem Standortserver ausführen. Weitere Informationen zum Zurücksetzen des Standorts finden Sie im Abschnitt [Ausführen einer Standortrücksetzung](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) des Themas [Ändern Ihrer System Center Configuration Manager-Infrastruktur](../../../../core/servers/manage/modify-your-infrastructure.md).  

 **/TESTDBUPGRADE <*Instanzname*>\\<*Datenbankname*>**  
 Testet eine Sicherung der Standortdatenbank daraufhin, ob für die Datenbank ein Upgrade durchgeführt werden kann. Stellen Sie den Instanznamen und den Datenbanknamen der Standortdatenbank bereit. Wenn Sie nur den Datenbanknamen angeben, wird automatisch der Standardinstanzname verwendet.  

> [!IMPORTANT]  
>  Führen Sie diese Befehlszeilenoption nicht für die Datenbank des Produktionsstandorts aus. Wenn Sie diese Befehlszeilenoption für die Datenbank des Produktionsstandorts ausführen, wird ein Upgrade auf die Standortdatenbank durchgeführt und Ihr Standort kann außer Funktion gesetzt werden.  

 **/UPGRADE**  
 Damit wird ein unbeaufsichtigtes Upgrade eines Standorts ausgeführt. Wenn Sie **/UPGRADE** verwenden, müssen Sie den Product Key einschließlich der Bindestriche (-) angeben. Darüber hinaus müssen Sie den Pfad zu den zuvor heruntergeladenen und für das Setup erforderlichen Dateien angeben.  

 Beispiel: `setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

 Weitere Informationen zu den für das Setup erforderlichen Dateien finden Sie unter [Setup-Downloadprogramm](setup-downloader.md).  

 **/SCRIPT <*Pfad zum Setupskript*>**  
 Damit werden unbeaufsichtigte Installationen ausgeführt. Bei Verwendung der Option **/SCRIPT** ist eine Setup-Initialisierungsdatei erforderlich. Weitere Informationen zur unbeaufsichtigten Installation finden Sie unter [Verwenden einer Befehlszeile zum Installieren von System Center Configuration Manager-Standorten](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).  

 **/SDKINST <*FQDN des SMS-Anbieters*>**  
 Damit wird der SMS-Anbieter auf dem angegebenen Computer installiert. Stellen Sie den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) für den SMS-Anbietercomputer bereit. Weiter Informationen zum SMS-Anbieter finden Sie unter [Planen des SMS-Anbieters](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

 **/SDKDEINST <*FQDN des SMS-Anbieters*>**  
 Damit wird der SMS-Anbieter auf dem angegebenen Computer deinstalliert. Stellen Sie den FQDN für den SMS-Anbietercomputer bereit.  

 **/MANAGELANGS <*Pfad zum Sprachskript*>**  
 Damit werden die Sprachen verwaltet, die an einem zuvor installierten Standort installiert wurden. Um diese Option zu verwenden, müssen Sie das Setup über **<*Configuration Manager-Installationspfad*>\BIN\X64** auf dem Standortserver ausführen. Stellen Sie den Speicherort der Sprachskriptdatei bereit, die die Spracheinstellungen enthält. Weitere Informationen zu den in der Skriptdatei für das Sprachsetup verfügbaren Sprachoptionen finden Sie unter [Befehlszeilenoptionen zum Verwalten von Sprachen](#bkmk_Lang) in diesem Thema.  

##  <a name="bkmk_Lang"></a> Befehlszeilenoptionen zum Verwalten von Sprachen  
 **Identification**  

-   **Schlüsselname:** Aktion  

    -   **Erforderlich:** Ja  

    -   **Werte:** ManageLanguages  

    -   **Details:** Verwaltet die Server-, Client- und mobile Clientsprache an einem Standort.  

**Optionen**  

-   **Schlüsselname:** AddServerLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit werden die Serversprachen angegeben, die für die Configuration Manager-Konsole, Berichte und Configuration Manager-Objekte verfügbar sein werden. Englisch ist standardmäßig verfügbar.  

-   **Schlüsselname:** AddClientLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit werden die Sprachen angegeben, die auf Clientcomputern zur Verfügung stehen werden. Englisch ist standardmäßig verfügbar.  

-   **Schlüsselname:** DeleteServerLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit werden die zu entfernenden Sprachen angegeben, die dann nicht mehr für die Configuration Manager-Konsole, Berichte und Configuration Manager-Objekte verfügbar sind. Englisch ist standardmäßig verfügbar und kann nicht entfernt werden.  

-   **Schlüsselname:** DeleteClientLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit werden die zu entfernenden Sprachen angegeben, die dann nicht mehr für Clientcomputer verfügbar sind. Englisch ist standardmäßig verfügbar und kann nicht entfernt werden.  

-   **Schlüsselname:** MobileDeviceLanguage  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Hiermit wird angegeben, ob die Sprachen für mobile Geräteclients installiert sind.  

-   **Schlüsselname:** PrerequisiteComp  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Herunterladen  

         1 = Bereits heruntergeladen  

    -   **Details:** Hiermit wird angegeben, ob die für das Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert **0** angeben, werden die Dateien beim Setup heruntergeladen.  

-   **Schlüsselname:** PrerequisitePath  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Pfad zu den für das Setup erforderlichen Dateien*>  

    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für das Setup erforderlichen Dateien angegeben. Je nach **PrerequisiteComp**-Wert wird dieser Pfad beim Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

##  <a name="bkmk_Unattended"></a> Skriptdateischlüssel für eine unbeaufsichtigte Installation  
 In den folgenden Abschnitten erfahren Sie, wie Sie ein Skript für die unbeaufsichtigte Installation erstellen. In den Listen werden die verfügbaren Setupskriptschlüssel und die entsprechenden Werte aufgeführt. Außerdem wird angegeben, ob die Schlüssel erforderlich sind und für welchen Installationstyp sie verwendet werden. In der letzten Spalte finden Sie zudem eine kurze Beschreibung der einzelnen Schlüssel.  

### <a name="unattended-install-for-a-central-administration-site"></a>Unbeaufsichtigtes Installieren eines Standorts der zentralen Verwaltung  
 Im folgenden Abschnitt finden Sie Detailinformationen eines Standorts der zentralen Verwaltung mithilfe einer Skriptdatei zur unbeaufsichtigten Installation.  

**Identification**  

-   **Schlüsselname:** Aktion  

    -   **Erforderlich:** Ja  

    -   **Werte:** InstallCAS  

    -   **Details:** Hiermit wird ein Standort der zentralen Verwaltung installiert.  

-   **Schlüsselname:** CDLatest  

    -   **Erforderlich:** Ja; nur wenn Sie Medien aus dem Ordner „CD.Latest“ verwenden    

    -   **Werte:** 1; bei jedem Wert außer 1 wird davon ausgegangen, dass er nicht „CD.Latest“ verwendet

    -   **Details:** Ihr Skript muss diesen Schlüssel und diesen Wert enthalten, wenn Sie das Setup von einem Medium in dem Ordner „CD.Latest“ ausführen, um einen Standort der primären oder zentralen Verwaltung zu installieren oder diesen wiederherstellen möchten. Dieser Wert informiert das Setup darüber, das Medien aus „CD.Latest“ verwendet werden.

**Optionen**  

-   **Schlüsselname:** ProductID  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *oder* Eval  

    -   **Details:** Gibt den Product Key für die Configuration Manager-Installation, einschließlich der Gedankenstriche, an. Geben Sie **Eval** ein, um die Evaluierungsversion von Configuration Manager zu installieren.  

-   **Schlüsselname:** SiteCode  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Standortcode*>  

    -   **Details:** Hiermit werden drei alphanumerische Zeichen angegeben, durch die der Standort in der Hierarchie eindeutig angegeben wird.  

-   **Schlüsselname:** Standortname  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Standortname*>  

    -   **Details:** Hiermit wird der Name für diesen Standort angegeben.  

-   **Schlüsselname:** SMSInstallDir  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Configuration Manager-Installationspfad*>  

    -   **Details:** Hiermit wird der Installationsordner für die Configuration Manager-Programmdateien angegeben.  

-   **Schlüsselname:** SDKServer  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*SMS-Anbieter-FQDN*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird. Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren.  

-   **Schlüsselname:** PrerequisiteComp  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Herunterladen  

         1 = Bereits heruntergeladen  

    -   **Details:** Hiermit wird angegeben, ob die für das Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert **0** angeben, werden die Dateien beim Setup heruntergeladen.  

-   **Schlüsselname:** PrerequisitePath  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Pfad zu den für das Setup erforderlichen Dateien*>  

    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für das Setup erforderlichen Dateien angegeben. Je nach **PrerequisiteComp**-Wert wird dieser Pfad beim Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

-   **Schlüsselname:** AdminConsole  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Hiermit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll.  

-   **Schlüsselname:** JoinCEIP  
    > [!Note]  
    > Ab Configuration Manager Version 1802 ist das CEIP-Feature nicht mehr im Produkt enthalten.

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht teilnehmen  

         1 = Teilnehmen  

    -   **Details:** Gibt an, ob am Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP) teilgenommen wird.  

-   **Schlüsselname:** AddServerLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit werden die Serversprachen angegeben, die für die Configuration Manager-Konsole, Berichte und Configuration Manager-Objekte verfügbar sein werden. Englisch ist standardmäßig verfügbar.  

-   **Schlüsselname:** AddClientLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit werden die Sprachen angegeben, die auf Clientcomputern zur Verfügung stehen werden. Englisch ist standardmäßig verfügbar.  

-   **Schlüsselname:** DeleteServerLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit wird ein Standort nach der Installation geändert. Gibt die zu entfernenden Sprachen an, die dann nicht mehr für die Configuration Manager-Konsole, Berichte und Configuration Manager-Objekte verfügbar sind. Englisch ist standardmäßig verfügbar und kann nicht entfernt werden.  

-   **Schlüsselname:** DeleteClientLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit wird ein Standort nach der Installation geändert. Gibt die zu entfernenden Sprachen an, die dann nicht mehr für Clientcomputer verfügbar sind. Englisch ist standardmäßig verfügbar und kann nicht entfernt werden.  

-   **Schlüsselname:** MobileDeviceLanguage  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Hiermit wird angegeben, ob die Sprachen für mobile Geräteclients installiert sind.  

**SQLConfigOptions**  

-   **Schlüsselname:** SQLServerName  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*SQL Server-Name*>  

    -   **Details:** Gibt den Namen des Servers oder der gruppierten Instanz an, die SQL Server ausführen, auf dem die Standortdatenbank gehostet werden soll.  

-   **Schlüsselname:** DatabaseName  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Standortdatenbankname*> oder <*Instanzname*>\\<*Standortdatenbankname*>  

    -   **Details:** Gibt den Namen der zu erstellenden SQL Server-Datenbank oder der SQL Server-Datenbank an, die bei der Installation der Datenbank für den Standort der zentralen Verwaltung verwendet werden soll.  

        > [!IMPORTANT]  
        >  Falls Sie nicht die Standardinstanz verwenden, müssen Sie den Instanznamen und den Namen der Standortdatenbank angeben.  

-   **Schlüsselname:** SQLSSBPort  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*SSB-Portnummer*>  

    -   **Details:** Hiermit wird der SQL Server Service Broker (SSB)-Port angegeben, der von SQL Server verwendet wird. SSB ist normalerweise für die Verwendung von Port 4022 konfiguriert, aber Sie können einen anderen Port verwenden.  

-   **Schlüsselname:** SQLDataFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*Pfad zur .mdb-Datenbankdatei*>  

    -   **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der .mdb-Datei für die Datenbank angegeben.  

-   **Schlüsselname:** SQLLogFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:**  <*Pfad zur .ldf-Datenbankdatei*>  

    -   **Details:** Gibt einen alternativen Speicherort zum Erstellen der .ldf-Datei für die Datenbank an.  

**CloudConnectorOptions**  

-   **Schlüsselname:** CloudConnector  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Gibt an, ob ein Dienstverbindungspunkt an diesem Standort installiert werden soll. Da der Dienstverbindungspunkt in einer Standorthierarchie nur am Standort der obersten Ebene installiert werden kann, muss dieser Wert für einen untergeordneten primären Standort **0** sein.  

-   **Schlüsselname:** CloudConnectorServer  

    -   **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    -   **Werte:** <*FQDN des Servers für den Dienstverbindungspunkt*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird.  

-   **Schlüsselname:** UseProxy  

    -   **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Gibt an, ob der Dienstverbindungspunkt einen Proxyserver verwendet.  

-   **Schlüsselname:** ProxyName  

    -   **Erforderlich:** Erforderlich, wenn **UseProxy** gleich 1 ist  

    -   **Werte:**  <*Proxyserver-FQDN*>  

    -   **Details:** Hiermit wird der FQDN des Proxyservers angegeben, der von dem Dienstverbindungspunkt verwendet wird.  

-   **Schlüsselname:** ProxyPort  

    -   **Erforderlich:** Erforderlich, wenn **UseProxy** gleich 1 ist  

    -   **Werte:** <*Portnummer*>  

    -   **Details:** Gibt die für den Proxyport zu verwendende Portnummer an.  

### <a name="unattended-install-for-a-primary-site"></a>Unbeaufsichtigtes Installieren eines primären Standorts  
Im folgenden Abschnitt finden Sie Detailinformationen eines primären Standorts mithilfe einer Skriptdatei zur unbeaufsichtigten Installation.  

**Identification**  

-   **Schlüsselname:** Aktion  

    -   **Erforderlich:** Ja  

    -   **Werte:** InstallPrimarySite  

    -   **Details:** Hiermit wird ein primärer Standort installiert.  

-   **Schlüsselname:** CDLatest  

    -   **Erforderlich:** Ja; nur wenn Sie Medien aus dem Ordner „CD.Latest“ verwenden    

    -   **Werte:** 1; bei jedem Wert außer 1 wird davon ausgegangen, dass er nicht „CD.Latest“ verwendet

    -   **Details:** Ihr Skript muss diesen Schlüssel und diesen Wert enthalten, wenn Sie das Setup von einem Medium in dem Ordner „CD.Latest“ ausführen, um einen Standort der primären oder zentralen Verwaltung zu installieren oder diesen wiederherstellen möchten. Dieser Wert informiert das Setup darüber, das Medien aus „CD.Latest“ verwendet werden.

**Optionen**  

-   **Schlüsselname:** ProductID  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *oder* Eval  

    -   **Details:** Gibt den Product Key für die Configuration Manager-Installation, einschließlich der Gedankenstriche, an. Geben Sie **Eval** ein, um die Evaluierungsversion von Configuration Manager zu installieren.  

-   **Schlüsselname:** SiteCode  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Standortcode*>  

    -   **Details:** Hiermit werden drei alphanumerische Zeichen angegeben, durch die der Standort in der Hierarchie eindeutig angegeben wird.  

-   **Schlüsselname:** SiteName  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Standortname*>  

    -   **Details:** Hiermit wird der Name für diesen Standort angegeben.  

-   **Schlüsselname:** SMSInstallDir  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Configuration Manager-Installationspfad*>

    -   **Details:** Hiermit wird der Installationsordner für die Configuration Manager-Programmdateien angegeben.  

-   **Schlüsselname:** SDKServer  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*SMS-Anbieter-FQDN*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird. Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren.  

-   **Schlüsselname:** PrerequisiteComp  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Herunterladen  

         1 = Bereits heruntergeladen  

    -   **Details:** Hiermit wird angegeben, ob die für das Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert **0** angeben, werden die Dateien beim Setup heruntergeladen.  

-   **Schlüsselname:** PrerequisitePath  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Pfad zu den für das Setup erforderlichen Dateien*>  

    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für das Setup erforderlichen Dateien angegeben. Je nach **PrerequisiteComp**-Wert wird dieser Pfad beim Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

-   **Schlüsselname:** AdminConsole  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Hiermit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll.  

-   **Schlüsselname:** JoinCEIP  
    > [!Note]  
    > Ab Configuration Manager Version 1802 ist das CEIP-Feature nicht mehr im Produkt enthalten.

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht teilnehmen  

         1 = Teilnehmen  

    -   **Details:** Gibt an, ob am CEIP teilgenommen werden soll.  

-   **Schlüsselname:** ManagementPoint  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*FQDN des Verwaltungspunkt-Standortservers*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Verwaltungspunkt“ gehostet wird.  

-   **Schlüsselname:** ManagementPointProtocol  

    -   **Erforderlich:** Nein  

    -   **Werte:** HTTPS *oder* HTTP  

    -   **Details:** Hiermit wird das Protokoll angegeben, das für den Verwaltungspunkt verwendet werden soll.  

-   **Schlüsselname:** DistributionPoint  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*FQDN des Verteilungspunkt-Standortservers*>  

    -   **Details:** Hiermit wird das Protokoll angegeben, das für den Verteilungspunkt verwendet werden soll.  

-   **Schlüsselname:** DistributionPointProtocol  

    -   **Erforderlich:** Nein  

    -   **Werte:** HTTPS *oder* HTTP  

    -   **Details:** Hiermit wird das Protokoll angegeben, das für den Verteilungspunkt verwendet werden soll.  

-   **Schlüsselname:** RoleCommunicationProtocol  

    -   **Erforderlich:** Ja  

    -   **Werte:** EnforceHTTPS *oder* HTTPorHTTPS  

    -   **Details:** Hiermit wird angegeben, ob von allen Standortsystemen ausschließlich die HTTPS-Kommunikation mit Clients zugelassen werden soll, oder ob die Kommunikationsmethode für jede Standortsystemrolle konfiguriert werden muss. Wenn Sie **EnforceHTTPS** auswählen, muss auf dem Clientcomputer ein gültiges Public-Key-Infrastructure-Zertifikat (PKI) für die Clientauthentifizierung vorliegen.  

-   **Schlüsselname:** ClientsUsePKICertificate  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht verwenden  

         1 = Verwenden  

    -   **Details:** Hiermit wird angegeben, ob für die Kommunikation zwischen Clients und Standortsystemrollen ein PKI-Clientzertifikat verwendet werden soll.  

-   **Schlüsselname:** AddServerLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit werden die Serversprachen angegeben, die für die Configuration Manager-Konsole, Berichte und Configuration Manager-Objekte verfügbar sein werden. Englisch ist standardmäßig verfügbar.  

-   **Schlüsselname:** AddClientLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit werden die Sprachen angegeben, die auf Clientcomputern zur Verfügung stehen werden. Englisch ist standardmäßig verfügbar.  

-   **Schlüsselname:** DeleteServerLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit wird ein Standort nach der Installation geändert. Gibt die zu entfernenden Sprachen an, die dann nicht mehr für die Configuration Manager-Konsole, Berichte und Configuration Manager-Objekte verfügbar sind. Englisch ist standardmäßig verfügbar und kann nicht entfernt werden.  

-   **Schlüsselname:** DeleteClientLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit wird ein Standort nach der Installation geändert. Gibt die zu entfernenden Sprachen an, die dann nicht mehr für Clientcomputer verfügbar sind. Englisch ist standardmäßig verfügbar und kann nicht entfernt werden.  

-   **Schlüsselname:** MobileDeviceLanguage  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Hiermit wird angegeben, ob die Sprachen für mobile Geräteclients installiert sind.  

**SQLConfigOptions**  

-   **Schlüsselname:** SQLServerName  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*SQL Server-Name*>  

    -   **Details:** Gibt den Namen des Servers oder der gruppierten Instanz an, die SQL Server ausführen, auf dem die Standortdatenbank gehostet werden soll.  

-   **Schlüsselname:** DatabaseName  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Standortdatenbankname*> oder <*Instanzname*>\\<*Standortdatenbankname*>  

    -   **Details:** Gibt den Namen der SQL Server-Datenbank an, der bei der Installation der primären Standortdatenbank erstellt oder verwendet werden soll.  

        > [!IMPORTANT]  
        >  Falls Sie nicht die Standardinstanz verwenden, müssen Sie den Instanznamen und den Namen der Standortdatenbank angeben.  

-   **Schlüsselname:** SQLSSBPort  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*SSB-Portnummer*>  

    -   **Details:** Gibt den SSB-Port an, der von SQL Server verwendet wird. SSB ist normalerweise für die Verwendung von Port 4022 konfiguriert, aber Sie können einen anderen Port verwenden.  

-   **Schlüsselname:** SQLDataFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*Pfad zur .mdb-Datenbankdatei*>  

    -   **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der .mdb-Datei für die Datenbank angegeben.  

-   **Schlüsselname:** SQLLogFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:**  <*Pfad zur .ldf-Datenbankdatei*>  

    -   **Details:** Gibt einen alternativen Speicherort zum Erstellen der .ldf-Datei für die Datenbank an.  

**HierarchyExpansionOption**  

-   **Schlüsselname:** CCARSiteServer  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*FQDN des Standorts der zentralen Verwaltung*>  

    -   **Details:** Über diesen Schlüssel wird der Standort der zentralen Verwaltung angegeben, dem ein primärer Standort beim Hinzufügen zur Configuration Manager-Hierarchie zugeordnet wird. Geben Sie den Standort der zentralen Verwaltung beim Setup an.  

-   **Schlüsselname:** CASRetryInterval  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*Intervall*>  

    -   **Details:** Über diesen Schlüssel wird das Wiederholungsintervall angegeben (in Minuten), wenn beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler aufgetreten ist. Wenn beispielsweise beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler auftritt, wird der Verbindungsversuch am primären Standort nach der für den Wert für **CASRetryInterval** angegebenen Anzahl von Minuten wiederholt.  

-   **Schlüsselname:** WaitForCASTimeout  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*Timeout*>  

         Ein Wert zwischen **0** und **100**  

    -   **Details:** Über diesen Schlüssel wird der maximale Timeoutwert (in Minuten) für die Verbindung eines primären Standorts mit dem Standort der zentralen Verwaltung angegeben. Wenn beispielsweise beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler auftritt, wird der Verbindungsversuch auf dem primären Standort basierend auf dem Wert für **CASRetryInterval** solange wiederholt, bis der für **WaitForCASTimeout** angegebene Zeitraum abgelaufen ist. Sie können einen Wert von **0** bis **100** angeben.  

**CloudConnectorOptions**  

-   **Schlüsselname:** CloudConnector  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Gibt an, ob ein Dienstverbindungspunkt an diesem Standort installiert werden soll. Da der Dienstverbindungspunkt in einer Standorthierarchie nur am Standort der obersten Ebene installiert werden kann, muss dieser Wert für einen untergeordneten primären Standort **0** sein.  

-   **Schlüsselname:** CloudConnectorServer  

    -   **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    -   **Werte:** <*FQDN des Servers für den Dienstverbindungspunkt*\>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird.  

-   **Schlüsselname:** UseProxy  

    -   **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Gibt an, ob der Dienstverbindungspunkt einen Proxyserver verwendet.  

-   **Schlüsselname:** ProxyName  

    -   **Erforderlich:** Erforderlich, wenn **UseProxy** gleich 1 ist  

    -   **Werte:**  <*Proxyserver-FQDN*>  

    -   **Details:** Hiermit wird der FQDN des Proxyservers angegeben, der von dem Dienstverbindungspunkt verwendet wird.  

-   **Schlüsselname:** ProxyPort  

    -   **Erforderlich:** Erforderlich, wenn **UseProxy** gleich 1 ist  

    -   **Werte:** <*Portnummer*>  

    -   **Details:** Gibt die für den Proxyport zu verwendende Portnummer an.  

### <a name="unattended-recovery-for-a-central-administration-site"></a>Unbeaufsichtigtes Wiederherstellen eines Standorts der zentralen Verwaltung  
 Verwenden Sie die folgenden Details zur Wiederherstellung eines Standorts der zentralen Verwaltung mithilfe einer Skriptdatei zur unbeaufsichtigten Installation.  

**Identification**  

-   **Schlüsselname:** Aktion  

    -   **Erforderlich:** Ja  

    -   **Werte:** RecoverCCAR  

    -   **Details:** Hiermit wird ein Standort der zentralen Verwaltung wiederhergestellt.  

-   **Schlüsselname:** CDLatest  

    -   **Erforderlich:** Ja; nur wenn Sie Medien aus dem Ordner „CD.Latest“ verwenden    

    -   **Werte:** 1; bei jedem Wert außer 1 wird davon ausgegangen, dass er nicht „CD.Latest“ verwendet

    -   **Details:** Ihr Skript muss diesen Schlüssel und diesen Wert enthalten, wenn Sie das Setup von einem Medium in dem Ordner „CD.Latest“ ausführen, um einen Standort der primären oder zentralen Verwaltung zu installieren oder diesen wiederherstellen möchten. Dieser Wert informiert das Setup darüber, dass Medien aus „CD.Latest“ verwendet werden.

**RecoveryOptions**  

-   **Schlüsselname:** ServerRecoveryOptions  

    -   **Erforderlich:** Ja  

    -   **Werte:** 1, 2 oder 4  

         1 = Wiederherstellung von Standortserver und SQL Server  

         2 = nur Wiederherstellung von Standortserver  

         4 = nur Wiederherstellung von SQL Server  

    -   **Details:** Hiermit wird angegeben, ob der Standortserver, SQL Server oder beides beim Setup wiederhergestellt wird. Die zugeordneten Schlüssel sind erforderlich, wenn Sie den folgenden Wert für die Einstellung **ServerRecoveryOptions** festlegen:  

        -   Wert = 1: Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

        -   Wert = 1: Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

        -   Wert= 4: Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.  

-   **Schlüsselname:** DatabaseRecoveryOptions  

    -   **Erforderlich**: Dieser Schlüssel ist erforderlich, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **4** konfiguriert wurde.  

    -   **Werte:** 10, 20, 40 oder 80  

         10 = Wiederherstellen der Standortdatenbank aus einer Sicherung  

         20 = Verwenden einer Standortdatenbank, die mithilfe einer anderen Methode manuell wiederhergestellt wurde  

         40 = Erstellen einer neuen Datenbank für den Standort. Verwenden Sie diese Option, wenn keine Standortdatenbank verfügbar ist. Globale Daten und Standortdaten werden durch die Replikation von anderen Standorten wiederhergestellt.  

         80 = Überspringen der Datenbankwiederherstellung.  

    -   **Details:** Hiermit wird angegeben, wie die Standortdatenbank in SQL Server durch das Setup wiederhergestellt wird.  

-   **Schlüsselname:** ReferenceSite  

    -   **Erforderlich:** Dieser Schlüssel ist erforderlich, wenn für die Einstellung **DatabaseRecoveryOptions** der Wert **40** festgelegt wurde.  

    -   **Werte:** <*FQDN des Referenzstandorts*>  

    -   **Details:** Hiermit wird der primäre Referenzstandort angegeben, der vom Standort der zentralen Verwaltung verwendet wird, um globale Daten wiederherzustellen, wenn die Datenbanksicherung älter ist als die Beibehaltungsdauer der Änderungsnachverfolgung oder wenn Sie den Standort ohne Sicherung wiederherstellen.  

         Wenn Sie keinen Referenzstandort angeben und die Sicherung älter als die Beibehaltungsdauer der Änderungsnachverfolgung ist, dann werden alle primären Standorte mit den wiederhergestellten Daten vom Standort der zentralen Verwaltung neu initialisiert.  

         Wenn Sie keinen Referenzstandort angeben und die Sicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung liegt, dann werden nur Änderungen, die nach der Sicherung vorgenommen wurden, von den primären Standorten repliziert. Wenn Änderungen von verschiedenen primären Standorten vorliegen, die miteinander in Konflikt stehen, dann wird vom Standort der zentralen Verwaltung die zuerst empfangene verwendet.  

-   **Schlüsselname:** SiteServerBackupLocation  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*Pfad zum Sicherungssatz des Standortservers*>  

    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz des Standortservers angegeben. Dieser Schlüssel ist optional, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **2**konfiguriert wurde. Geben Sie einen Wert für den Schlüssel **SiteServerBackupLocation** an, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

-   **Schlüsselname:** BackupLocation  

    -   **Erforderlich:** Dieser Schlüssel ist erforderlich, wenn Sie für den Schlüssel **ServerRecoveryOptions** den Wert **1** oder **4** und für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren.  

    -   **Werte:** <*Pfad zum Sicherungssatz der Standortdatenbank*>  

    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz der Standortdatenbank angegeben.  

**Optionen**  

-   **Schlüsselname:** ProductID  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *oder* Eval  

    -   **Details:** Gibt den Product Key für die Configuration Manager-Installation, einschließlich der Gedankenstriche, an. Geben Sie **Eval** ein, um die Evaluierungsversion von Configuration Manager zu installieren.  

-   **Schlüsselname:** SiteCode  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Standortcode*>  

    -   **Details:** Hiermit werden drei alphanumerische Zeichen angegeben, durch die der Standort in der Hierarchie eindeutig angegeben wird. Geben Sie den Standortcode an, der vor dem Auftreten des Fehlers vom Standort verwendet wurde.

-   **Schlüsselname:** SiteName  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*Standortname*>  

    -   **Details:** Hiermit wird der Name für diesen Standort angegeben.  

-   **Schlüsselname:** SMSInstallDir  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Configuration Manager-Installationspfad*>  

    -   **Details:** Hiermit wird der Installationsordner für die Configuration Manager-Programmdateien angegeben.  

-   **Schlüsselname:** SDKServer  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*SMS-Anbieter-FQDN*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird. Geben Sie den Server an, auf dem der SMS-Anbieter vor Auftreten des Fehlers gehostet wurde.  

         Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren. Weitere Informationen zum SMS-Anbieter finden Sie im Abschnitt [Planen des SMS-Anbieters für System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Schlüsselname:** PrerequisiteComp  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Herunterladen  

         1 = Bereits heruntergeladen  

    -   **Details:** Hiermit wird angegeben, ob die für das Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert **0** angeben, werden die Dateien beim Setup heruntergeladen.  

-   **Schlüsselname:** PrerequisitePath  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Pfad zu den für das Setup erforderlichen Dateien*>  

    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für das Setup erforderlichen Dateien angegeben. Je nach **PrerequisiteComp**-Wert wird dieser Pfad beim Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

-   **Schlüsselname:** AdminConsole  

    -   **Erforderlich:** Dieser Schlüssel ist erforderlich, außer wenn für die Einstellung **ServerRecoveryOptions** der Wert **4** festgelegt wurde.  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Hiermit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll.  

-   **Schlüsselname:** JoinCEIP  
    > [!Note]  
    > Ab Configuration Manager Version 1802 ist das CEIP-Feature nicht mehr im Produkt enthalten.

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht teilnehmen  

         1 = Teilnehmen  

    -   **Details:** Gibt an, ob am CEIP teilgenommen werden soll.  

**SQLConfigOptions**  

-   **Schlüsselname:** SQLServerName  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*SQL Server-Name*>  

    -   **Details:** Gibt den Namen des Servers oder der gruppierten Instanz an, der bzw. die SQL Server ausführt und auf dem bzw. der die Standortdatenbank gehostet wird. Geben Sie denselben Server an, auf dem die Standortdatenbank vor Auftreten des Fehlers gehostet wurde.  

-   **Schlüsselname:** DatabaseName  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Standortdatenbankname*> oder <*Instanzname*>\\<*Standortdatenbankname*>  

    -   **Details:** Gibt den Namen der SQL Server-Datenbank an, der bei der Installation der Datenbank für den Standort der zentralen Verwaltung erstellt oder verwendet werden soll. Geben Sie denselben Datenbanknamen an, der vor Auftreten des Fehlers verwendet wurde.  

        > [!IMPORTANT]  
        >  Falls Sie nicht die Standardinstanz verwenden, müssen Sie den Instanznamen und den Namen der Standortdatenbank angeben.  

-   **Schlüsselname:** SQLSSBPort  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*SSB-Portnummer*>  

    -   **Details:** Gibt den SSB-Port an, der von SQL Server verwendet wird. SSB ist normalerweise für die Verwendung von TCP-Port 4022 konfiguriert. Geben Sie denselben SSB-Port an, der vor Auftreten des Fehlers verwendet wurde.  

-   **Schlüsselname:** SQLDataFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*Pfad zur .mdb-Datenbankdatei*>  

    -   **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der .mdb-Datei für die Datenbank angegeben.  

-   **Schlüsselname:** SQLLogFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:**  <*Pfad zur .ldf-Datenbankdatei*>  

    -   **Details:** Gibt einen alternativen Speicherort zum Erstellen der .ldf-Datei für die Datenbank an.  

**CloudConnectorOptions**  

-   **Schlüsselname:** CloudConnector  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Gibt an, ob ein Dienstverbindungspunkt an diesem Standort installiert werden soll. Da der Dienstverbindungspunkt in einer Standorthierarchie nur am Standort der obersten Ebene installiert werden kann, muss dieser Wert für einen untergeordneten primären Standort **0** sein.  

-   **Schlüsselname:** CloudConnectorServer  

    -   **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    -   **Werte:** <*FQDN des Servers für den Dienstverbindungspunkt*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird.  

-   **Schlüsselname:** UseProxy  

    -   **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Gibt an, ob der Dienstverbindungspunkt einen Proxyserver verwendet.  

-   **Schlüsselname:** ProxyName  

    -   **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    -   **Werte:**  <*Proxyserver-FQDN*>  

    -   **Details:** Hiermit wird der FQDN des Proxyservers angegeben, der von dem Dienstverbindungspunkt verwendet wird.  

-   **Schlüsselname:** ProxyPort  

    -   **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    -   **Werte:** <*Portnummer*>  

    -   **Details:** Gibt die für den Proxyport zu verwendende Portnummer an.  

### <a name="unattended-recovery-for-a-primary-site"></a>Unbeaufsichtigte Wiederherstellung eines primären Standorts  
 Im folgenden Abschnitt finden Sie Detailinformationen Wiederherstellung eines primären Standorts mithilfe einer Skriptdatei zur unbeaufsichtigten Installation.  

**Identification**  

-   **Schlüsselname:** Aktion  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*RecoverPrimarySite*>  

    -   **Details:** Hiermit wird ein primärer Standort wiederhergestellt.  

-   **Schlüsselname:** CDLatest  

    -   **Erforderlich:** Ja; nur wenn Sie Medien aus dem Ordner „CD.Latest“ verwenden    

    -   **Werte:** 1; bei jedem Wert außer 1 wird davon ausgegangen, dass er nicht „CD.Latest“ verwendet

    -   **Details:** Ihr Skript muss diesen Schlüssel und diesen Wert enthalten, wenn Sie das Setup von einem Medium in dem Ordner „CD.Latest“ ausführen, um einen Standort der primären oder zentralen Verwaltung zu installieren oder diesen wiederherstellen möchten. Dieser Wert informiert das Setup darüber, dass Medien aus „CD.Latest“ verwendet werden.    

**RecoveryOptions**  

-   **Schlüsselname:** ServerRecoveryOptions  

    -   **Erforderlich:** Ja  

    -   **Werte:** 1, 2 oder 4  

         1 = Wiederherstellung von Standortserver und SQL Server  

         2 = nur Wiederherstellung von Standortserver  

         4 = nur Wiederherstellung von SQL Server  

    -   **Details:** Hiermit wird angegeben, ob der Standortserver, SQL Server oder beides beim Setup wiederhergestellt wird. Die zugeordneten Schlüssel sind erforderlich, wenn Sie den folgenden Wert für die Einstellung **ServerRecoveryOptions** festlegen:  

        -   Wert = 1: Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

        -   Wert = 1: Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

        -   Wert= 4: Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.  

-   **Schlüsselname:** DatabaseRecoveryOptions  

    -   **Erforderlich**: Dieser Schlüssel ist erforderlich, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **4** konfiguriert wurde.  

    -   **Werte:** 10, 20, 40 oder 80  

         10 = Wiederherstellen der Standortdatenbank aus einer Sicherung  

         20 = Verwenden einer Standortdatenbank, die mithilfe einer anderen Methode manuell wiederhergestellt wurde  

         40 = Erstellen einer neuen Datenbank für den Standort. Verwenden Sie diese Option, wenn keine Standortdatenbank verfügbar ist. Globale Daten und Standortdaten werden durch die Replikation von anderen Standorten wiederhergestellt.  

         80 = Überspringen der Datenbankwiederherstellung.  

    -   **Details:** Hiermit wird angegeben, wie die Standortdatenbank in SQL Server durch das Setup wiederhergestellt wird.  

-   **Schlüsselname:** SiteServerBackupLocation  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*Pfad zum Sicherungssatz des Standortservers*>  

    -   **Details:**  

         Über diesen Schlüssel wird der Pfad zum Sicherungssatz des Standortservers angegeben. Dieser Schlüssel ist optional, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **2**festgelegt wurde. Geben Sie einen Wert für den Schlüssel **SiteServerBackupLocation** an, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

-   **Schlüsselname:** BackupLocation  

    -   **Erforderlich:** Dieser Schlüssel ist erforderlich, wenn Sie für den Schlüssel **ServerRecoveryOptions** den Wert **1** oder **4** und für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren.  

    -   **Werte:** <*Pfad zum Sicherungssatz der Standortdatenbank*>  

    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz der Standortdatenbank angegeben.  

**Optionen**  

-   **Schlüsselname:** ProductID  

    -   **Erforderlich:** Ja  

    -   **Werte:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* oder *Eval*  

    -   **Details:** Gibt den Product Key für die Configuration Manager-Installation, einschließlich der Gedankenstriche, an. Geben Sie **Eval** ein, um die Evaluierungsversion von Configuration Manager zu installieren.  

-   **Schlüsselname:** SiteCode  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Standortcode*>  

    -   **Details:** Hiermit werden drei alphanumerische Zeichen angegeben, durch die der Standort in der Hierarchie eindeutig angegeben wird. Geben Sie den Standortcode an, der vor dem Auftreten des Fehlers vom Standort verwendet wurde.

-   **Schlüsselname:** SiteName  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*Standortname*>  

    -   **Details:** Hiermit wird der Name für diesen Standort angegeben.  

-   **Schlüsselname:** SMSInstallDir  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Configuration Manager-Installationspfad*>  

    -   **Details:** Hiermit wird der Installationsordner für die Configuration Manager-Programmdateien angegeben.  

-   **Schlüsselname:** SDKServer  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*SMS-Anbieter-FQDN*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird. Geben Sie den Server an, auf dem der SMS-Anbieter vor Auftreten des Fehlers gehostet wurde. Konfigurieren Sie nach der Erstinstallation zusätzliche SMS-Anbieter für den Standort. Weiter Informationen zum SMS-Anbieter finden Sie unter [Planen des SMS-Anbieters](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Schlüsselname:** PrerequisiteComp  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Herunterladen  

         1 = Bereits heruntergeladen  

    -   **Details:** Hiermit wird angegeben, ob die für das Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert **0** angeben, werden die Dateien beim Setup heruntergeladen.  

-   **Schlüsselname:** PrerequisitePath  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Pfad zu den für das Setup erforderlichen Dateien*>  

    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für das Setup erforderlichen Dateien angegeben. Je nach **PrerequisiteComp**-Wert wird dieser Pfad beim Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

-   **Schlüsselname:** AdminConsole  

    -   **Erforderlich:** Dieser Schlüssel ist erforderlich, außer wenn für die Einstellung **ServerRecoveryOptions** der Wert **4** festgelegt wurde.  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Hiermit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll.  

-   **Schlüsselname:** JoinCEIP  
    > [!Note]  
    > Ab Configuration Manager Version 1802 ist das CEIP-Feature nicht mehr im Produkt enthalten.

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht teilnehmen  

         1 = Teilnehmen  

    -   **Details:** Gibt an, ob am CEIP teilgenommen werden soll.  

**SQLConfigOptions**  

-   **Schlüsselname:** SQLServerName  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*SQL Server-Name*>  

    -   **Details:** Gibt den Namen des Servers oder der gruppierten Instanz an, der bzw. die SQL Server ausführt und auf dem bzw. der die Standortdatenbank gehostet wird. Geben Sie denselben Server an, auf dem die Standortdatenbank vor Auftreten des Fehlers gehostet wurde.  

-   **Schlüsselname:** DatabaseName  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*Standortdatenbankname*> oder <*Instanzname*>\\<*Standortdatenbankname*>

    -   **Details:**  

         Gibt den Namen der SQL Server-Datenbank an, der bei der Installation der Datenbank für den Standort der zentralen Verwaltung erstellt oder verwendet werden soll. Geben Sie denselben Datenbanknamen an, der vor Auftreten des Fehlers verwendet wurde.  

        > [!IMPORTANT]  
        >  Falls Sie nicht die Standardinstanz verwenden, müssen Sie den Instanznamen und den Namen der Standortdatenbank angeben.  

-   **Schlüsselname:** SQLSSBPort  

    -   **Erforderlich:** Ja  

    -   **Werte:** <*SSB-Portnummer*>  

    -   **Details:** Gibt den SSB-Port an, der von SQL Server verwendet wird. SSB ist normalerweise für die Verwendung von TCP-Port 4022 konfiguriert. Geben Sie denselben SSB-Port an, der vor Auftreten des Fehlers verwendet wurde.  

-   **Schlüsselname:** SQLDataFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*Pfad zur .mdb-Datenbankdatei*>  

    -   **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der .mdb-Datei für die Datenbank angegeben.  

-   **Schlüsselname:** SQLLogFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:**  <*Pfad zur .ldf-Datenbankdatei*>  

    -   **Details:** Gibt einen alternativen Speicherort zum Erstellen der .ldf-Datei für die Datenbank an.  

**HierarchyExpansionOptions**  

-   **Schlüsselname:** CCARSiteServer  

    -   **Erforderlich:** Siehe Details.  

    -   **Werte:** <*Standortcode für den Standort der zentralen Verwaltung*>  

    -   **Details:** Hiermit wird der Standort der zentralen Verwaltung angegeben, dem ein primärer Standort beim Verknüpfen mit der Configuration Manager-Hierarchie zugeordnet wird. Diese Einstellung ist erforderlich, wenn der primäre Standort vor dem Fehler mit einem zentralen Verwaltungsstandort verbunden war. Geben Sie den Standortcode an, der vor Auftreten des Fehlers vom Standort der zentralen Verwaltung verwendet wurde.  

-   **Schlüsselname:** CASRetryInterval  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*Intervall*>  

    -   **Details:** Über diesen Schlüssel wird das Wiederholungsintervall angegeben (in Minuten), wenn beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler aufgetreten ist. Wenn beispielsweise beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler auftritt, wird der Verbindungsversuch auf dem primären Standort nach der für den Wert für **CASRetryInterval** angegebenen Anzahl von Minuten erneut wiederholt.  

-   **Schlüsselname:** WaitForCASTimeout  

    -   **Erforderlich:** Nein  

    -   **Werte:** <*Timeout*>  

    -   **Details:** Über diesen Schlüssel wird der maximale Timeoutwert (in Minuten) für die Verbindung eines primären Standorts mit dem Standort der zentralen Verwaltung angegeben. Wenn beispielsweise beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler auftritt, wird der Verbindungsversuch auf dem primären Standort basierend auf dem Wert für **CASRetryInterval** solange wiederholt, bis der für **WaitForCASTimeout** angegebene Zeitraum abgelaufen ist. Sie können einen Wert von **0** bis **100** angeben.  

**CloudConnectorOptions**  

-   **Schlüsselname:** CloudConnector  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Gibt an, ob ein Dienstverbindungspunkt an diesem Standort installiert werden soll. Da der Dienstverbindungspunkt in einer Standorthierarchie nur am Standort der obersten Ebene installiert werden kann, muss dieser Wert für einen untergeordneten primären Standort **0** sein.  

-   **Schlüsselname:** CloudConnectorServer  

    -   **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    -   **Werte:** <*FQDN des Servers für den Dienstverbindungspunkt*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird.  

-   **Schlüsselname:** UseProxy  

    -   **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    -   **Werte:** 0 oder 1  

         0 = Nicht installieren  

         1 = Installieren  

    -   **Details:** Gibt an, ob der Dienstverbindungspunkt einen Proxyserver verwendet.  

-   **Schlüsselname:** ProxyName  

    -   **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    -   **Werte:**  <*Proxyserver-FQDN*>  

    -   **Details:** Hiermit wird der FQDN des Proxyservers angegeben, der von dem Dienstverbindungspunkt verwendet wird.  

-   **Schlüsselname:** ProxyPort  

    -   **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    -   **Werte:** <*Portnummer*>  

    -   **Details:** Gibt die für den Proxyport zu verwendende Portnummer an.  
