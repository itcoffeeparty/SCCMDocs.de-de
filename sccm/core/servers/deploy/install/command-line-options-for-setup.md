---
title: Setup der Befehlszeilenoptionen | System Center Configuration Manager
description: "Verwenden Sie die Informationen in diesem Artikel, um Skripts zu konfigurieren oder System Center Configuration Manager über die Befehlszeile zu installieren."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7d1f55786a42650395fcb66ee4917434feecb630

---
# <a name="command-line-options-for-setup-for-system-center-configuration-manager"></a>Befehlszeilenoptionen für das Setup für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 Verwenden Sie die Informationen in den folgenden Tabellen, wenn Sie Skripts konfigurieren oder System Center Configuration Manager über die Befehlszeile installieren.  

##  <a name="a-namebkmksetupa-command-line-options-for-setup"></a><a name="bkmk_setup"></a> Befehlszeilenoptionen für Setup  
 **/DEINSTALL**  
 Damit wird der Standort deinstalliert. Sie müssen Setup vom Standortservercomputer ausführen.  

 **/DONTSTARTSITECOMP**  
 Installieren Sie einen Standort, ohne dass der Standortkomponenten-Manager-Dienst gestartet wird. Der Standort wird erst beim Start des Standortkomponenten-Manager-Diensts aktiv. Der Standortkomponenten-Manager ist dafür verantwortlich, dass der Dienst SMS_Executive sowie weitere Prozesse am Standort installiert und gestartet werden. Wenn Sie den Standortkomponenten-Manager-Dienst nach Abschluss der Standortinstallation starten, werden der Dienst SMS_Executive sowie weitere Prozesse installiert, die für den Betrieb des Standorts erforderlich sind.  

 **/HIDDEN**  
 Damit wird die Benutzeroberfläche beim Setup ausgeblendet. Diese Option muss mit der Option **/SCRIPT** kombiniert werden, und in der Skriptdatei für die unbeaufsichtigte Installation müssen alle erforderlichen Optionen angegeben werden, da andernfalls ein Setupfehler auftritt.  

 **/NOUSERINPUT**  
 Damit wird beim Setup die Benutzereingabe deaktiviert, aber die Benutzeroberfläche des **Setup-Assistenten** wird angezeigt. Diese Option muss mit der Option **/SCRIPT** kombiniert werden, und in der Skriptdatei für die unbeaufsichtigte Installation müssen alle erforderlichen Optionen angegeben werden, da andernfalls ein Setupfehler auftritt.  

 **/RESETSITE**  
 Damit wird eine Standortrücksetzung ausgeführt, wobei auch die Datenbank und Dienstkonten des Standorts zurückgesetzt werden. Sie müssen das Setup vom Ordner **&lt;ConfigMgrInstallationPath\>\BIN\X64** auf dem Standortserver ausführen. Weitere Informationen zum Zurücksetzen des Standorts finden Sie im Abschnitt [Einen Standort zurücksetzen](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) des Themas [Ändern Sie Ihre System Center Configuration Manager-Infrastruktur](../../../../core/servers/manage/modify-your-infrastructure.md).  

 **/TESTDBUPGRADE &lt;*InstanceName\DatabaseName*>**  
 Damit wird eine Sicherung der Standortdatenbank daraufhin getestet, ob für sie ein Upgrade durchgeführt werden kann. Sie müssen den Instanznamen und den Datenbanknamen der Standortdatenbank angeben. Wenn Sie nur den Datenbanknamen angeben, wird automatisch der Standardinstanzname verwendet.  

> [!IMPORTANT]  
>  Das Verwenden dieser Befehlszeilenoption für die Produktionsstandortdatenbank wird nicht empfohlen. Dadurch würde ein Upgrade der Standortdatenbank durchgeführt, und Ihr Standort wäre möglicherweise nicht mehr betriebsfähig.  

 **/UPGRADE**  
 Damit wird ein unbeaufsichtigtes Upgrade eines Standorts ausgeführt. Wenn Sie /UPGRADE verwenden, müssen Sie auch den Product Key einschließlich der Bindestriche (-) angeben. Darüber hinaus müssen Sie den Pfad zu den zuvor für Setup erforderlichen Dateien angeben.  

 Beispiel: **setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx &lt;Pfad zu externen Komponentendateien\>**  

 Weitere Informationen zu den für Setup erforderlichen Dateien finden Sie unter  [Setup-Downloadprogramm](#bkmk_SetupDownloader) in diesem Thema.  

 **/SCRIPT &lt;*SetupScriptPath*>**  
 führt unbeaufsichtigte Installationen aus. Bei Verwendung der Option **/SCRIPT** ist eine Initialisierungsdatei für das Setup erforderlich. Weitere Informationen zur unbeabsichtigten Ausführung von Setup finden Sie unter [Install sites using a command line (Installieren von Standorten mit einer Befehlszeilenoptionen)](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).  

 **/SDKINST &lt;*FQDN*>**  
 Damit wird der SMS-Anbieter auf dem angegebenen Computer installiert. Sie müssen den FQDN für den SMS-Anbietercomputer bereitstellen. Weitere Informationen zum SMS-Anbieter finden Sie im Abschnitt [Planen des SMS-Anbieters für System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

 **/SDKDEINST &lt;*FQDN*>**  
 Damit wird der SMS-Anbieter auf dem angegebenen Computer deinstalliert. Sie müssen den FQDN für den SMS-Anbietercomputer bereitstellen.  

 **/MANAGELANGS &lt;*LanguageScriptPath*>**  
Verwaltet die Sprachen, die an einem zuvor installierten Standort installiert wurden. Zur Verwendung dieser Option müssen Sie das Setup im Ordner **&lt;ConfigMgrInstallationPath\>\BIN\X64 auf dem Standortserver ausführen, und den Speicherort der Sprachskriptdatei angeben, die die Spracheinstellungen enthält. Weitere Informationen zu den in der Skriptdatei für das Sprachsetup verfügbaren Sprachoptionen finden Sie im Abschnitt [Befehlszeilenoption zum Verwalten von Sprachen](#bkmk_Lang) in diesem Thema.  

##  <a name="a-namebkmklanga-command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a> Befehlszeilenoptionen zum Verwalten von Sprachen  
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

    -   **Details:** Hiermit werden die Sprachen angegeben, die nicht mehr länger für die Configuration Manager-Konsole, Berichte und Configuration Manager Objekte verfügbar sein werden. Englisch ist standardmäßig verfügbar und kann nicht entfernt werden.  

-   **Schlüsselname:** DeleteClientLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit werden die Sprachen angegeben, die entfernt werden und nicht mehr auf Clientcomputern verfügbar sein werden. Englisch ist standardmäßig verfügbar und kann nicht entfernt werden.  

-   **Schlüsselname:** MobileDeviceLanguage  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Über diesen Schlüssel wird angegeben, ob die Sprachen für mobile Geräteclients installiert werden.  

-   **Schlüsselname:** PrerequisiteComp  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = herunterladen  

         1 = bereits heruntergeladen  

    -   **Details:** Hiermit wird angegeben, ob die für Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert 0 angeben, werden die Dateien von Setup heruntergeladen.  

-   **Schlüsselname:** PrerequisitePath  

    -   **Erforderlich:** Ja  

    -   **Werte:**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für Setup erforderlichen Dateien angegeben. Je nach dem Wert unter **PrerequisiteComp** wird dieser Pfad von Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

##  <a name="a-namebkmkunattendeda-unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a> Skriptdateischlüssel für unbeaufsichtigtes Setup  
 In den folgenden Abschnitten erfahren Sie, wie Sie ein Skript für die unbeaufsichtigte Installation erstellen. In den Tabellen werden die verfügbaren Setupskriptschlüssel und die entsprechenden Werte aufgeführt. Außerdem wird angegeben, ob die Schlüssel erforderlich sind und für welchen Installationstyp sie verwendet werden. In der letzten Spalte finden Sie zudem eine kurze Beschreibung der einzelnen Schlüssel.  

### <a name="unattended-install-for-a-central-administration-site"></a>Unbeaufsichtigtes Installieren eines Standorts der zentralen Verwaltung  
 Im folgenden Abschnitt finden Sie Detailinformationen zur unbeaufsichtigten Installation eines Standorts der zentralen Verwaltung mithilfe einer Skriptdatei.  

**Identification**  

-   **Schlüsselname:** Aktion  

    -   **Erforderlich:** Ja  

    -   **Werte:** InstallCAS  

    -   **Details:** Hiermit wird ein Standort der zentralen Verwaltung installiert.  

**Optionen**  

-   **Schlüsselname:** ProductID  

    -   **Erforderlich:** Ja  

    -   **Werte:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* oder *Eval*  

    -   **Details:** Gibt den Product Key für die Configuration Manager-Installation, einschließlich der Gedankenstriche, an. Geben Sie **Eval** ein, um die Evaluierungsversion von Configuration Manager zu installieren.  

-   **Schlüsselname:** SiteCode  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;*SiteCode*>  

    -   **Details:** Hiermit werden drei alphanumerische Zeichen angegeben, durch die der Standort in der Hierarchie eindeutig angegeben wird.  

-   **Schlüsselname:** SiteName  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;*SiteName*>  

    -   **Details:** Hiermit wird der Name für diesen Standort angegeben.  

-   **Schlüsselname:** SMSInstallDir  

    -   **Erforderlich:** Ja  

    -   **Werte:** *ConfigMgrInstallationPath*  

    -   **Details:** Hiermit wird der Installationsordner für die Configuration Manager-Programmdateien angegeben.  

-   **Schlüsselname:** SDKServer  

    -   **Erforderlich:** Ja  

    -   **Werte:**&lt;*FQDN des SMS-Anbieters*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird.  
        Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren.  

-   **Schlüsselname:** PrerequisiteComp  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = herunterladen  

         1 = bereits heruntergeladen  

    -   **Details:** Hiermit wird angegeben, ob die für Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert 0 angeben, werden die Dateien von Setup heruntergeladen.  

-   **Schlüsselname:** PrerequisitePath  

    -   **Erforderlich:** Ja  

    -   **Werte:**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für Setup erforderlichen Dateien angegeben. Je nach dem Wert für PrerequisiteComp werden in diesem Pfad heruntergeladene Dateien gespeichert oder bereits heruntergeladene Dateien gesucht.  

-   **Schlüsselname:** AdminConsole  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll.  

-   **Schlüsselname:** JoinCEIP  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht teilnehmen  

         1 = teilnehmen  

    -   **Details:** Gibt an, ob am Programm zur Verbesserung der Benutzerfreundlichkeit teilgenommen wird.  

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

    -   **Details:** Hiermit wird ein Standort nach der Installation geändert.  
        Hiermit werden die Sprachen angegeben, die für die Configuration Manager-Konsole, Berichte und Configuration-Manager Objekte entfernt werden und nicht mehr verfügbar sein sollen. Englisch ist standardmäßig verfügbar und kann nicht entfernt werden.  

-   **Schlüsselname:** DeleteClientLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit wird ein Standort nach der Installation geändert.  
        Damit werden die Sprachen angegeben, die entfernt werden und nicht mehr auf Clientcomputern verfügbar sein sollen. Englisch ist standardmäßig verfügbar und kann nicht entfernt werden.  

-   **Schlüsselname:** MobileDeviceLanguage  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob die Sprachen für mobile Geräteclients installiert sind.  

**SQLConfigOptions**  

-   **Schlüsselname:** SQLServerName  

    -   **Erforderlich:** Ja  

    -   **Werte:** *SQLServerName*  

    -   **Details:** Hiermit wird der Name des Servers oder der gruppierten Instanz, die den SQL Server ausführen, angegeben. Von diesem Computer wird die Standortdatenbank gehostet.  

-   **Schlüsselname:** DatabaseName  

    -   **Erforderlich:** Ja  

    -   **Werte:** *&lt;SiteDatabaseName\>* oder *&lt;InstanceName\>\&lt;SiteDatabaseName \>*  

    -   **Details:**  

         Gibt den Namen der SQL Server-Datenbank an, der bei der Installation der Datenbank für den Standort der zentralen Verwaltung erstellt oder verwendet werden soll.  

        > [!IMPORTANT]  
        >  Sie müssen den Instanznamen und den Namen der Standortdatenbank angeben, falls Sie die Standardinstanz nicht verwenden.  

-   **Schlüsselname:** SQLSSBPort  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*SSBPortNumber*>  

    -   **Details:** Hiermit wird der SQL Server Service Broker (SSB)-Port angegeben, der von SQL Server verwendet wird. Von SSB wird zwar in der Regel TCP-Port 4022 verwendet, aber es werden auch andere Ports unterstützt.  

-   **Schlüsselname:** SQLDataFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*FilePath to database .MDB file*>  

    -   **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der MDB-Datei für die Datenbank angegeben.  

-   **Schlüsselname:** SQLLogFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*FilePath to database .LDF file*>  

    -   **Details:** Gibt einen alternativen Speicherort zum Erstellen der LDF-Datei für die Datenbank an.  

**CloudConnectorOptions**  

-   **Schlüsselname:** CloudConnector  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob Sie einen Dienstverbindungspunkt an diesem Standort installieren werden. Da der Dienstverbindungspunkt in einer Standorthierarchie nur am Standort der obersten Ebene installiert werden kann, muss dieser Wert für einen untergeordneten primären Standort 0 sein.  

-   **Schlüsselname:** CloudConnectorServer  

    -   **Erforderlich:** Erforderlich, wenn CloudConnector gleich 1 ist  

    -   **Werte:** &lt;*FQDN des Servers für den Dienstverbindungspunkt*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird.  

-   **Schlüsselname:** UseProxy  

    -   **Erforderlich:** Erforderlich, wenn CloudConnector gleich 1 ist  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob der Dienstverbindungspunkt einen Proxyserver verwenden wird.  

-   **Schlüsselname:** ProxyName  

    -   **Erforderlich:** Erforderlich, wenn UseProxy dem Wert 1 entspricht  

    -   **Werte:** &lt;*Proxyserver-FQDN*>  

    -   **Details:** Hiermit wird der FQDN des Proxyservers angegeben, der von der Standortsystemrolle „Dienstverbindungspunkt“ verwendet werden wird.  

-   **Schlüsselname:** ProxyPort  

    -   **Erforderlich:** Erforderlich, wenn UseProxy dem Wert 1 entspricht  

    -   **Werte:** &lt;*PortNumber *>  

    -   **Details:** Gibt die zu verwendende Portnummer an.  

### <a name="unattended-install-for-a-primary-site"></a>Unbeaufsichtigtes Installieren eines primären Standorts  
Im folgenden Abschnitt finden Sie Detailinformationen zur unbeaufsichtigten Installation eines primären Standorts mithilfe einer Skriptdatei.  

Im folgenden Abschnitt finden Sie Detailinformationen zur unbeaufsichtigten Installation eines Standorts der zentralen Verwaltung mithilfe einer Skriptdatei.  

**Identification**  

-   **Schlüsselname:** Aktion  

    -   **Erforderlich:** Ja  

    -   **Werte:** InstallPrimarySite  

    -   **Details:** Hiermit wird ein primärer Standort installiert.  

**Optionen**  

-   **Schlüsselname:** ProductID  

    -   **Erforderlich:** Ja  

    -   **Werte:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* oder *Eval*  

    -   **Details:** Gibt den Product Key für die Configuration Manager-Installation, einschließlich der Gedankenstriche, an. Geben Sie **Eval** ein, um die Evaluierungsversion von Configuration Manager zu installieren.  

-   **Schlüsselname:** SiteCode  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;*SiteCode*>  

    -   **Details:** Hiermit werden drei alphanumerische Zeichen angegeben, durch die der Standort in der Hierarchie eindeutig angegeben wird.  

-   **Schlüsselname:** SiteName  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;*SiteName*>  

    -   **Details:** Hiermit wird der Name für diesen Standort angegeben.  

-   **Schlüsselname:** SMSInstallDir  

    -   **Erforderlich:** Ja  

    -   **Werte:** *ConfigMgrInstallationPath*  

    -   **Details:** Hiermit wird der Installationsordner für die Configuration Manager-Programmdateien angegeben.  

-   **Schlüsselname:** SDKServer  

    -   **Erforderlich:** Ja  

    -   **Werte:**&lt;*FQDN des SMS-Anbieters*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird.  
        Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren.  

-   **Schlüsselname:** PrerequisiteComp  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = herunterladen  

         1 = bereits heruntergeladen  

    -   **Details:** Hiermit wird angegeben, ob die für Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert 0 angeben, werden die Dateien von Setup heruntergeladen.  

-   **Schlüsselname:** PrerequisitePath  

    -   **Erforderlich:** Ja  

    -   **Werte:**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für Setup erforderlichen Dateien angegeben. Je nach dem Wert unter **PrerequisiteComp** wird dieser Pfad von Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

-   **Schlüsselname:** AdminConsole  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll.  

-   **Schlüsselname:** JoinCEIP  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht teilnehmen  

         1 = teilnehmen  

    -   **Details:** Gibt an, ob am Programm zur Verbesserung der Benutzerfreundlichkeit teilgenommen wird.  

-   **Schlüsselname:** ManagementPoint  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*Verwaltungspunkt-FQDN des Standortservers*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Verwaltungspunkt“ gehostet wird.  

-   **Schlüsselname:** ManagementPointProtocol  

    -   **Erforderlich:** Nein  

    -   **Werte:** HTTPS oder HTTP  

    -   **Details:** Hiermit wird das Protokoll angegeben, das für den Verwaltungspunkt verwendet werden soll.  

-   **Schlüsselname:** DistributionPoint  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*FQDN des Verteilungspunkt-Standortservers*>  

    -   **Details:** Hiermit wird das Protokoll angegeben, das für den Verwaltungspunkt verwendet werden soll.  

-   **Schlüsselname:** DistributionPointProtocol  

    -   **Erforderlich:** Nein  

    -   **Werte:** HTTPS oder HTTP  

    -   **Details:** Hiermit wird das Protokoll angegeben, das für den Verteilungspunkt verwendet werden soll.  

-   **Schlüsselname:** RoleCommunicationProtocol  

    -   **Erforderlich:** Ja  

    -   **Werte:** EnforceHTTPS oder HTTPorHTTPS  

    -   **Details:** Hiermit wird angegeben, ob von allen Standortsystemen ausschließlich die HTTPS-Kommunikation mit Clients zugelassen werden soll, oder ob die Kommunikationsmethode für jede Standortsystemrolle konfiguriert werden muss. Bei Auswahl von **EnforceHTTPS**muss auf dem Clientcomputer ein gültiges PKI-Zertifikat für die Clientauthentifizierung vorliegen.  

-   **Schlüsselname:** ClientsUsePKICertificate  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht verwenden  

         1 = verwenden  

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

    -   **Details:** Hiermit wird ein Standort nach der Installation geändert.  
        Hiermit werden die Sprachen angegeben, die für die Configuration Manager-Konsole, Berichte und Configuration-Manager Objekte entfernt werden und nicht mehr verfügbar sein sollen. Englisch ist standardmäßig verfügbar und kann nicht entfernt werden.  

-   **Schlüsselname:** DeleteClientLanguages  

    -   **Erforderlich:** Nein  

    -   **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    -   **Details:** Hiermit wird ein Standort nach der Installation geändert.  
        Damit werden die Sprachen angegeben, die entfernt werden und nicht mehr auf Clientcomputern verfügbar sein sollen. Englisch ist standardmäßig verfügbar und kann nicht entfernt werden.  

-   **Schlüsselname:** MobileDeviceLanguage  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob die Sprachen für mobile Geräteclients installiert sind.  

**SQLConfigOptions**  

-   **Schlüsselname:** SQLServerName  

    -   **Erforderlich:** Ja  

    -   **Werte:** *SQLServerName*  

    -   **Details:** Hiermit wird der Name des Servers oder der gruppierten Instanz, die den SQL Server ausführen, angegeben. Von diesem Computer wird die Standortdatenbank gehostet.  

-   **Schlüsselname:** DatabaseName  

    -   **Erforderlich:** Ja  

    -   **Werte:** *&lt;SiteDatabaseName\>* oder *&lt;InstanceName\>\&lt;SiteDatabaseName \>*  

    -   **Details:**  

         Gibt den Namen der SQL Server-Datenbank an, die für die Installation der primären Standortdatenbank erstellt oder verwendet werden soll.  

        > [!IMPORTANT]  
        >  Sie müssen den Instanznamen und den Namen der Standortdatenbank angeben, falls Sie die Standardinstanz nicht verwenden.  

-   **Schlüsselname:** SQLSSBPort  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*SSBPortNumber*>  

    -   **Details:** Hiermit wird der SQL Server Service Broker (SSB)-Port angegeben, der von SQL Server verwendet wird. Von SSB wird zwar in der Regel TCP-Port 4022 verwendet, aber es werden auch andere Ports unterstützt.  

-   **Schlüsselname:** SQLDataFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*FilePath to database .MDB file*>  

    -   **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der MDB-Datei für die Datenbank angegeben.  

-   **Schlüsselname:** SQLLogFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*FilePath to database .LDF file*>  

    -   **Details:** Gibt einen alternativen Speicherort zum Erstellen der LDF-Datei für die Datenbank an.  

**HierarchyExpansionOption**  

-   **Schlüsselname:** CCARSiteServer  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*FQDN des Standorts der zentralen Verwaltung*>  

    -   **Details:** Hiermit wird der Standort der zentralen Verwaltung angegeben, dem ein primärer Standort hinzugefügt, wenn er der Configuration Manager-Hierarchie zugeordnet wird. Sie müssen den Standort der zentralen Verwaltung beim Setup angeben.  

-   **Schlüsselname:** CASRetryInterval  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*Intervall*>  

    -   **Details:** Über diesen Schlüssel wird das Wiederholungsintervall angegeben (in Minuten), wenn beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler aufgetreten ist. Wenn beispielsweise beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler auftritt, wird der Verbindungsversuch auf dem primären Standort nach der für CASRetryInterval angegebenen Anzahl von Minuten wiederholt.  

-   **Schlüsselname:** WaitForCASTimeout  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*Timeout*>  

         Ein Wert zwischen 0 und 100.  

    -   **Details:** Hiermit wird der maximale Timeoutwert (in Minuten) für die Verbindung eines primären Standorts mit dem Standort der zentralen Verwaltung angegeben. Wenn beispielsweise beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler auftritt, wird der Verbindungsversuch auf dem primären Standort basierend auf dem Wert für CASRetryInterval solange wiederholt, bis der für WaitForCASTimeout angegebene Zeitraum abgelaufen ist. Sie können einen Wert von 0 bis 100 angeben.  

**CloudConnectorOptions**  

-   **Schlüsselname:** CloudConnector  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob Sie einen Dienstverbindungspunkt an diesem Standort installieren werden. Da der Dienstverbindungspunkt in einer Standorthierarchie nur am Standort der obersten Ebene installiert werden kann, muss dieser Wert für einen untergeordneten primären Standort 0 sein.  

-   **Schlüsselname:** CloudConnectorServer  

    -   **Erforderlich:** Erforderlich, wenn CloudConnector gleich 1 ist  

    -   **Werte:** &lt;*FQDN des Servers für den Dienstverbindungspunkt*\>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird.  

-   **Schlüsselname:** UseProxy  

    -   **Erforderlich:** Erforderlich, wenn CloudConnector gleich 1 ist  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob der Dienstverbindungspunkt einen Proxyserver verwenden wird.  

-   **Schlüsselname:** ProxyName  

    -   **Erforderlich:** Erforderlich, wenn UseProxy dem Wert 1 entspricht  

    -   **Werte:** &lt;*Proxyserver-FQDN*>  

    -   **Details:** Hiermit wird der FQDN des Proxyservers angegeben, der von der Standortsystemrolle „Dienstverbindungspunkt“ verwendet werden wird.  

-   **Schlüsselname:** ProxyPort  

    -   **Erforderlich:** Erforderlich, wenn UseProxy dem Wert 1 entspricht  

    -   **Werte:** &lt;*PortNumber *>  

    -   **Details:** Gibt die zu verwendende Portnummer an.  

### <a name="unattended-recovery-for-a-central-administration-site"></a>Unbeaufsichtigtes Wiederherstellen eines Standorts der zentralen Verwaltung  
 Verwenden Sie die folgenden Details zur Wiederherstellung eines Standorts der zentralen Verwaltung mithilfe einer unbeaufsichtigten Setup-Skriptdatei.  

**Identification**  

-   **Schlüsselname:** Aktion  

    -   **Erforderlich:** Ja  

    -   **Werte:** RecoverCCAR  

    -   **Details:** Hiermit wird ein Standort der zentralen Verwaltung wiederhergestellt.  

**RecoveryOptions**  

-   **Schlüsselname:** ServerRecoveryOptions  

    -   **Erforderlich:** Ja  

    -   **Werte:** 1, 2 oder 4  

         1 = Wiederherstellung von Standortserver und SQL Server  

         2 = nur Wiederherstellung von Standortserver  

         4 = nur Wiederherstellung von SQL Server  

    -   **Details:** Hiermit wird angegeben, ob von Setup der Standortserver, SQL Server oder beides wiederhergestellt wird. Die zugeordneten Schlüssel sind erforderlich, wenn Sie den folgenden Wert für die Einstellung ServerRecoveryOptions festlegen:  

        -   Wert = 1: Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

        -   Wert = 1: Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

        -   Wert= 4: Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.  

-   **Schlüsselname:** DatabaseRecoveryOptions  

    -   **Erforderlich:** Dieser Schlüssel ist erforderlich, wenn für die Einstellung „ServerRecoveryOptions“ der Wert **1** oder **4** konfiguriert wurde.  

    -   **Werte:** 10, 20, 40, 80  

         10 = Wiederherstellen der Standortdatenbank aus einer Sicherung  

         20 = Verwenden einer Standortdatenbank, die mithilfe einer anderen Methode manuell wiederhergestellt wurde  

         40 = Erstellen einer neuen Datenbank für den Standort. Verwenden Sie diese Option, wenn keine Standortdatenbank verfügbar ist. Globale Daten und Standortdaten werden durch die Replikation von anderen Standorten wiederhergestellt.  

         80 = Datenbankwiederherstellung überspringen  

    -   **Details:** Hiermit wird angegeben, wie die Standortdatenbank in SQL Server durch Setup wiederhergestellt wird.  

-   **Schlüsselname:** ReferenceSite  

    -   **Erforderlich:** Dieser Schlüssel ist erforderlich, wenn für die Einstellung **DatabaseRecoveryOptions** der Wert **40** festgelegt wurde.  

    -   **Werte:** &lt;*ReferenceSiteFQDN*>  

    -   **Details:** Hiermit wird der primäre Referenzstandort angegeben, der vom Standort der zentralen Verwaltung verwendet wird, um globale Daten wiederherzustellen, wenn die Datenbanksicherung älter ist als die Beibehaltungsdauer der Änderungsnachverfolgung, oder wenn Sie den Standort ohne Sicherung wiederherstellen.  

         Wenn Sie keinen Referenzstandort angeben und die Sicherung älter als die Beibehaltungsdauer der Änderungsnachverfolgung ist, dann werden alle primären Standorte mit den wiederhergestellten Daten vom Standort der zentralen Verwaltung neu initialisiert.  

         Wenn Sie keinen Referenzstandort angeben und die Sicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung liegt, dann werden nur Änderungen, die nach der Sicherung vorgenommen wurden, von den primären Standorten repliziert. Wenn Änderungen von verschiedenen primären Standorten vorliegen, die miteinander in Konflikt stehen, dann wird vom Standort der zentralen Verwaltung die zuerst empfangene verwendet.  

-   **Schlüsselname:** SiteServerBackupLocation  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*PathToSiteServerBackupSet*>  

    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz des Standortservers angegeben. Dieser Schlüssel ist optional, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **2**konfiguriert wurde. Geben Sie einen Wert für den Schlüssel **SiteServerBackupLocation** an, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

-   **Schlüsselname:** BackupLocation  

    -   **Erforderlich:** Dieser Schlüssel ist erforderlich, wenn Sie für den Schlüssel **ServerRecoveryOptions** den Wert **1** oder **4** und für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren.  

    -   **Werte:** &lt;*PathToSiteDatabaseBackupSet*>  

    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz der Standortdatenbank angegeben.  

**Optionen**  

-   **Schlüsselname:** ProductID  

    -   **Erforderlich:** Ja  

    -   **Werte:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* oder *Eval*  

    -   **Details:** Gibt den Product Key für die Configuration Manager-Installation, einschließlich der Gedankenstriche, an. Geben Sie **Eval** ein, um die Evaluierungsversion von Configuration Manager zu installieren.  

-   **Schlüsselname:** SiteCode  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;*SiteCode*>  

    -   **Details:** Hiermit werden drei alphanumerische Zeichen angegeben, durch die der Standort in der Hierarchie eindeutig angegeben wird. Sie müssen den Standortcode angeben, der vor dem Auftreten des Fehlers vom Standort verwendet wurde. Weitere Informationen zu Einschränkungen bei Standortcodes finden Sie im Abschnitt [Informationen zu Standortnamen und Standortcodes](#bkmk_codes) in diesem Thema.  

-   **Schlüsselname:** SiteName  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*SiteName*>  

    -   **Details:** Hiermit wird der Name für diesen Standort angegeben.  

-   **Schlüsselname:** SMSInstallDir  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;*ConfigMgrInstallationPath*>  

    -   **Details:** Hiermit wird der Installationsordner für die Configuration Manager-Programmdateien angegeben.  

-   **Schlüsselname:** SDKServer  

    -   **Erforderlich:** Ja  

    -   **Werte:**&lt;*FQDN des SMS-Anbieters*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird. Sie müssen den Server angeben, von dem der SMS-Anbieter vor Auftreten des Fehlers gehostet wurde.  

         Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren. Weitere Informationen zum SMS-Anbieter finden Sie im Abschnitt [Planen des SMS-Anbieters für System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Schlüsselname:** PrerequisiteComp  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = herunterladen  

         1 = bereits heruntergeladen  

    -   **Details:** Hiermit wird angegeben, ob die für Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert **0**angeben, werden die Dateien von Setup heruntergeladen.  

-   **Schlüsselname:** PrerequisitePath  

    -   **Erforderlich:** Ja  

    -   **Werte:**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für Setup erforderlichen Dateien angegeben. Je nach dem Wert unter **PrerequisiteComp** wird dieser Pfad von Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

-   **Schlüsselname:** AdminConsole  

    -   **Erforderlich:** Dieser Schlüssel ist erforderlich, außer wenn für die Einstellung **ServerRecoveryOptions** der Wert **4** festgelegt wurde.  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll.  

-   **Schlüsselname:** JoinCEIP  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht teilnehmen  

         1 = teilnehmen  

    -   **Details:** Gibt an, ob am Programm zur Verbesserung der Benutzerfreundlichkeit teilgenommen wird.  

**SQLConfigOptions**  

-   **Schlüsselname:** SQLServerName  

    -   **Erforderlich:** Ja  

    -   **Werte:** *SQLServerName*  

    -   **Details:** Hiermit wird der Name des Servers oder der gruppierten Instanz angegeben, die den SQL Server ausführen, auf dem die Standortdatenbank gehostet werden soll. Sie müssen den Server angeben, von dem die Standortdatenbank vor dem Auftreten des Fehlers gehostet wurde.  

-   **Schlüsselname:** DatabaseName  

    -   **Erforderlich:** Ja  

    -   **Werte:** *&lt;SiteDatabaseName\>* oder *&lt;InstanceName\>\&lt;SiteDatabaseName \>*  

    -   **Details:**  

         Gibt den Namen der SQL Server-Datenbank an, der bei der Installation der Datenbank für den Standort der zentralen Verwaltung erstellt oder verwendet werden soll. Sie müssen den gleichen Datenbanknamen angeben, der vor Auftreten des Fehlers verwendet wurde.  

        > [!IMPORTANT]  
        >  Sie müssen den Instanznamen und den Namen der Standortdatenbank angeben, falls Sie die Standardinstanz nicht verwenden.  

-   **Schlüsselname:** SQLSSBPort  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;*SSBPortNumber*>  

    -   **Details:** Hiermit wird der SQL Server Service Broker (SSB)-Port angegeben, der von SQL Server verwendet wird. SSB ist normalerweise für die Verwendung von TCP-Port 4022 konfiguriert. Sie müssen den gleichen SSB-Port angeben, der vor Auftreten des Fehlers verwendet wurde.  

-   **Schlüsselname:** SQLDataFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*FilePath to database .MDB file*>  

    -   **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der MDB-Datei für die Datenbank angegeben.  

-   **Schlüsselname:** SQLLogFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*FilePath to database .LDF file*>  

    -   **Details:** Gibt einen alternativen Speicherort zum Erstellen der LDF-Datei für die Datenbank an.  

**CloudConnectorOptions**  

-   **Schlüsselname:** CloudConnector  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob Sie einen Dienstverbindungspunkt an diesem Standort installieren werden. Da der Dienstverbindungspunkt in einer Standorthierarchie nur am Standort der obersten Ebene installiert werden kann, muss dieser Wert für einen untergeordneten primären Standort 0 sein.  

-   **Schlüsselname:** CloudConnecorServer  

    -   **Erforderlich:** Erforderlich, wenn CloudConnector gleich 1 ist  

    -   **Werte:** &lt;*FQDN des Servers für den Dienstverbindungspunkt*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird.  

-   **Schlüsselname:** UseProxy  

    -   **Erforderlich:** Erforderlich, wenn CloudConnector gleich 1 ist  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob der Dienstverbindungspunkt einen Proxyserver verwenden wird.  

-   **Schlüsselname:** ProxyName  

    -   **Erforderlich:** Erforderlich, wenn CloudConnector gleich 1 ist  

    -   **Werte:** &lt;*Proxyserver-FQDN*>  

    -   **Details:** Hiermit wird der FQDN des Proxyservers angegeben, der von der Standortsystemrolle „Dienstverbindungspunkt“ verwendet werden wird.  

-   **Schlüsselname:** ProxyPort  

    -   **Erforderlich:** Erforderlich, wenn CloudConnector gleich 1 ist  

    -   **Werte:** &lt;*PortNumber *>  

    -   **Details:** Gibt die zu verwendende Portnummer an.  

### <a name="unattended-recovery-for-a-primary-site"></a>Unbeaufsichtigte Wiederherstellung eines primären Standorts  
 Im folgenden Abschnitt finden Sie Detailinformationen zur unbeaufsichtigten Wiederherstellung eines primären Standorts mithilfe einer Skriptdatei.  

**Identification**  

-   **Schlüsselname:** Aktion  

    -   **Erforderlich:** Ja  

    -   **Werte:** RecoverPrimarySite  

    -   **Details:** Hiermit wird ein primärer Standort wiederhergestellt.  

**RecoveryOptions**  

-   **Schlüsselname:** ServerRecoveryOptions  

    -   **Erforderlich:** Ja  

    -   **Werte:** 1, 2 oder 4  

         1 = Wiederherstellung von Standortserver und SQL Server  

         2 = nur Wiederherstellung von Standortserver  

         4 = nur Wiederherstellung von SQL Server  

    -   **Details:** Hiermit wird angegeben, ob von Setup der Standortserver, SQL Server oder beides wiederhergestellt wird. Die zugeordneten Schlüssel sind erforderlich, wenn Sie den folgenden Wert für die Einstellung ServerRecoveryOptions festlegen:  

        -   Wert = 1: Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

        -   Wert = 1: Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

        -   Wert= 4: Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.  

-   **Schlüsselname:** DatabaseRecoveryOptions  

    -   **Erforderlich:** Dieser Schlüssel ist erforderlich, wenn für die Einstellung „ServerRecoveryOptions“ der Wert **1** oder **4** konfiguriert wurde.  

    -   **Werte:** 10, 20, 40, 80  

         10 = Wiederherstellen der Standortdatenbank aus einer Sicherung  

         20 = Verwenden einer Standortdatenbank, die mithilfe einer anderen Methode manuell wiederhergestellt wurde  

         40 = Erstellen einer neuen Datenbank für den Standort. Verwenden Sie diese Option, wenn keine Standortdatenbank verfügbar ist. Globale Daten und Standortdaten werden durch die Replikation von anderen Standorten wiederhergestellt.  

         80 = Datenbankwiederherstellung überspringen  

    -   **Details:** Hiermit wird angegeben, wie die Standortdatenbank in SQL Server durch Setup wiederhergestellt wird.  

-   **Schlüsselname:** SiteServerBackupLocation  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*PathToSiteServerBackupSet*>  

    -   **Details:**  

         Über diesen Schlüssel wird der Pfad zum Sicherungssatz des Standortservers angegeben. Dieser Schlüssel ist optional, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **2**festgelegt wurde. Geben Sie einen Wert für den Schlüssel **SiteServerBackupLocation** an, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

-   **Schlüsselname:** BackupLocation  

    -   **Erforderlich:** Dieser Schlüssel ist erforderlich, wenn Sie für den Schlüssel **ServerRecoveryOptions** den Wert **1** oder **4** und für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren.  

    -   **Werte:** &lt;*PathToSiteDatabaseBackupSet*>  

    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz der Standortdatenbank angegeben.  

**Optionen**  

-   **Schlüsselname:** ProductID  

    -   **Erforderlich:** Ja  

    -   **Werte:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* oder *Eval*  

    -   **Details:** Gibt den Product Key für die Configuration Manager-Installation, einschließlich der Gedankenstriche, an. Geben Sie **Eval** ein, um die Evaluierungsversion von Configuration Manager zu installieren.  

-   **Schlüsselname:** SiteCode  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;*SiteCode*>  

    -   **Details:** Hiermit werden drei alphanumerische Zeichen angegeben, durch die der Standort in der Hierarchie eindeutig angegeben wird. Sie müssen den Standortcode angeben, der vor dem Auftreten des Fehlers vom Standort verwendet wurde. Weitere Informationen zu Einschränkungen bei Standortcodes finden Sie im Abschnitt [Informationen zu Standortnamen und Standortcodes](#bkmk_codes) in diesem Thema.  

-   **Schlüsselname:** SiteName  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*SiteName*>  

    -   **Details:** Hiermit wird der Name für diesen Standort angegeben.  

-   **Schlüsselname:** SMSInstallDir  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;*ConfigMgrInstallationPath*>  

    -   **Details:** Hiermit wird der Installationsordner für die Configuration Manager-Programmdateien angegeben.  

-   **Schlüsselname:** SDKServer  

    -   **Erforderlich:** Ja  

    -   **Werte:**&lt;*FQDN des SMS-Anbieters*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird. Sie müssen den Server angeben, von dem der SMS-Anbieter vor Auftreten des Fehlers gehostet wurde. Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren. Weitere Informationen zum SMS-Anbieter finden Sie im Abschnitt [Planen des SMS-Anbieters für System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Schlüsselname:** PrerequisiteComp  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = herunterladen  

         1 = bereits heruntergeladen  

    -   **Details:** Hiermit wird angegeben, ob die für Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert **0**angeben, werden die Dateien von Setup heruntergeladen.  

-   **Schlüsselname:** PrerequisitePath  

    -   **Erforderlich:** Ja  

    -   **Werte:**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für Setup erforderlichen Dateien angegeben. Je nach dem Wert unter **PrerequisiteComp** wird dieser Pfad von Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

-   **Schlüsselname:** AdminConsole  

    -   **Erforderlich:** Dieser Schlüssel ist erforderlich, außer wenn für die Einstellung **ServerRecoveryOptions** der Wert **4** festgelegt wurde.  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll.  

-   **Schlüsselname:** JoinCEIP  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht teilnehmen  

         1 = teilnehmen  

    -   **Details:** Gibt an, ob am Programm zur Verbesserung der Benutzerfreundlichkeit teilgenommen wird.  

**SQLConfigOptions**  

-   **Schlüsselname:** SQLServerName  

    -   **Erforderlich:** Ja  

    -   **Werte:** *SQLServerName*  

    -   **Details:** Hiermit wird der Name des Servers oder der gruppierten Instanz angegeben, die den SQL Server ausführen, auf dem die Standortdatenbank gehostet werden soll. Sie müssen den Server angeben, von dem die Standortdatenbank vor dem Auftreten des Fehlers gehostet wurde.  

-   **Schlüsselname:** DatabaseName  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;*SiteDatabaseName*\> oder &lt;*InstanceName*\>\\&lt;* SiteDatabaseName*\>

    -   **Details:**  

         Gibt den Namen der SQL Server-Datenbank an, der bei der Installation der Datenbank für den Standort der zentralen Verwaltung erstellt oder verwendet werden soll. Sie müssen den gleichen Datenbanknamen angeben, der vor Auftreten des Fehlers verwendet wurde.  

        > [!IMPORTANT]  
        >  Sie müssen den Instanznamen und den Namen der Standortdatenbank angeben, falls Sie die Standardinstanz nicht verwenden.  

-   **Schlüsselname:** SQLSSBPort  

    -   **Erforderlich:** Ja  

    -   **Werte:** &lt;*SSBPortNumber*>  

    -   **Details:** Hiermit wird der SQL Server Service Broker (SSB)-Port angegeben, der von SQL Server verwendet wird. SSB ist normalerweise für die Verwendung von TCP-Port 4022 konfiguriert. Sie müssen den gleichen SSB-Port angeben, der vor Auftreten des Fehlers verwendet wurde.  

-   **Schlüsselname:** SQLDataFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*FilePath to database .MDB file*>  

    -   **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der MDB-Datei für die Datenbank angegeben.  

-   **Schlüsselname:** SQLLogFilePath  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*FilePath to database .LDF file*>  

    -   **Details:** Gibt einen alternativen Speicherort zum Erstellen der LDF-Datei für die Datenbank an.  

**HierarchyExpansionOptions**  

-   **Schlüsselname:** CCARSiteServer  

    -   **Erforderlich:** Siehe Details.  

    -   **Werte:** &lt;*SiteCodeForCentralAdministrationSite*>  

    -   **Details:** Hiermit wird der Standort der zentralen Verwaltung angegeben, dem ein primärer Standort beim Verknüpfen mit der Configuration Manager-Hierarchie zugeordnet wird. Diese Einstellung ist erforderlich, wenn der primäre Standort vor dem Fehler mit einem zentralen Verwaltungsstandort verbunden war. Sie müssen den Standortcode angeben, der vor dem Auftreten des Fehlers vom zentralen Verwaltungsstandort verwendet wurde.  

-   **Schlüsselname:** CASRetryInterval  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*Intervall*>  

    -   **Details:** Über diesen Schlüssel wird das Wiederholungsintervall angegeben (in Minuten), wenn beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler aufgetreten ist. Wenn beispielsweise beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler auftritt, wird der Verbindungsversuch auf dem primären Standort nach der für **CASRetryInterval**angegebenen Anzahl von Minuten wiederholt.  

-   **Schlüsselname:** WaitForCASTimeout  

    -   **Erforderlich:** Nein  

    -   **Werte:** &lt;*Timeout*>  

    -   **Details:** Hiermit wird der maximale Timeoutwert (in Minuten) für die Verbindung eines primären Standorts mit dem Standort der zentralen Verwaltung angegeben. Wenn beispielsweise beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler auftritt, wird der Verbindungsversuch auf dem primären Standort basierend auf dem Wert für **CASRetryInterval** solange wiederholt, bis der für **WaitForCASTimeout** angegebene Zeitraum abgelaufen ist. Sie können einen Wert von 0 bis 100 angeben.  

**CloudConnectorOptions**  

-   **Schlüsselname:** CloudConnector  

    -   **Erforderlich:** Ja  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob Sie einen Dienstverbindungspunkt an diesem Standort installieren werden. Da der Dienstverbindungspunkt in einer Standorthierarchie nur am Standort der obersten Ebene installiert werden kann, muss dieser Wert für einen untergeordneten primären Standort 0 sein.  

-   **Schlüsselname:** CloudConnecorServer  

    -   **Erforderlich:** Erforderlich, wenn CloudConnector gleich 1 ist  

    -   **Werte:** &lt;*FQDN des Servers für den Dienstverbindungspunkt*>  

    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird.  

-   **Schlüsselname:** UseProxy  

    -   **Erforderlich:** Erforderlich, wenn CloudConnector gleich 1 ist  

    -   **Werte:** 0 oder 1  

         0 = nicht installieren  

         1 = installieren  

    -   **Details:** Hiermit wird angegeben, ob der Dienstverbindungspunkt einen Proxyserver verwenden wird.  

-   **Schlüsselname:** ProxyName  

    -   **Erforderlich:** Erforderlich, wenn CloudConnector gleich 1 ist  

    -   **Werte:** &lt;*Proxyserver-FQDN*>  

    -   **Details:** Hiermit wird der FQDN des Proxyservers angegeben, der von der Standortsystemrolle „Dienstverbindungspunkt“ verwendet werden wird.  

-   **Schlüsselname:** ProxyPort  

    -   **Erforderlich:** Erforderlich, wenn CloudConnector gleich 1 ist  

    -   **Werte:** &lt;*PortNumber *>  

    -   **Details:** Gibt die zu verwendende Portnummer an.  



<!--HONumber=Nov16_HO1-->


