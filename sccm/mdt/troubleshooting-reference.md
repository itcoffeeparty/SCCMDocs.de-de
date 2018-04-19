---
title: Problembehandlung für das MDT
titleSuffix: Microsoft Deployment Toolkit
description: 'Referenz zur Problembehandlung für das Microsoft Deployment Toolkit '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 91a7a69a-deac-4b0f-aac9-b7bd187c53fb
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: efb65086878a46bfb3485fdd8b0be6f613225261
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2018
---
# <a name="troubleshooting-reference-for-the-microsoft-deployment-toolkit"></a>Referenz zur Problembehandlung für das Microsoft Deployment Toolkit
 Die Bereitstellung von Betriebssystemen und Anwendungen sowie die Migration des Benutzerstatus kann ein anspruchsvolles Unterfangen sein, und zwar selbst dann, wenn Sie über die entsprechenden Tools und Leitfäden verfügen. Diese Referenz, die Teil des Microsoft® Deployment Toolkits (MDT) 2013 ist, enthält Informationen zu aktuellen bekannten Problemen, mögliche Umgehungen für diese Probleme sowie Informationen zur Problembehandlung.  

> [!NOTE]
>  In diesem Dokument bezieht sich *Windows* auf die Betriebssysteme Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2, sofern nicht anderes angegeben. Das MDT unterstützt keine Windows-Versionen, die auf ARM-Prozessoren basieren. Ferner bezieht sich *MDT* auf MDT 2013, sofern nicht anders angegeben.  

> [!NOTE]
>  Das Microsoft Diagnostics and Recovery Toolset (DaRT) enthält leistungsstarke Tools für die Wiederherstellung und Problembehandlung von Clientcomputern, die nicht gestartet werden oder nicht mehr stabil arbeiten. DaRT kann zum Ermitteln der Ursache eines Absturzes, zum Wiederherstellen verloren gegangener Dateien und für weitere Aufgaben verwendet werden. Sie können DaRT außerdem als ein Tool zur Problembehandlung bei der Entwicklung und Bereitstellung von Windows-Betriebssystemen verwenden. Wenn beispielsweise ein erstelltes Image nicht ordnungsgemäß gestartet wird, können Sie den Clientcomputer mit dem Image starten, indem Sie die Diagnoseumgebung ERD Commander verwenden. Sie können dann die Festplatte des Clientcomputers durchsuchen, das Ereignisprotokoll anzeigen, Updates entfernen, die Einstellungen des Betriebssystems ändern usw. DaRT ist Bestandteil des Microsoft Desktop Optimization Pack for Software Assurance. Weitere Informationen zu DaRT erhalten Sie unter [http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx](http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx).  

## <a name="understanding-logs"></a>Grundlegendes zu Protokollen  
 Bevor eine effektive Problembehandlung von MDT möglich ist, benötigen Sie genaue Kenntnisse der verschiedenen Protokolldateien, die während der Bereitstellung eines Betriebssystems verwendet werden. Wenn Sie wissen, in welchen Protokolldateien Sie für welche Fehlerbedingung zu welchem Zeitpunkt nachschlagen müssen, können Probleme, die zunächst rätselhaft und schwer verständlich erscheinen, klar und verständlich werden.  

 Das MDT-Protokolldateiformat wurde konzipiert, um von Trace32 gelesen zu werden, das zum System Center Configuration Manager 2007 Toolkit V2 gehört, welches im [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=9257) heruntergeladen werden kann. Die Protokolle können auch mit dem Configuration Manager Trace Log-Tool (CMTrace) gelesen werden, das in System Center 2012 Configuration Manager und höheren Versionen verfügbar ist. Verwenden Sie nach Möglichkeit stets diese Tools, um die Protokolldateien zu lesen, da sie die Suche nach Fehlern wesentlich erleichtern.  

 Im Folgenden wird im Detail auf die Protokolldateien eingegangen, die während der Bereitstellung sowie bei der Einrichtung von Windows erstellt werden. Dieser Abschnitt enthält ferner Beispiele dafür, wann die Dateien für die Problembehandlung verwendet werden sollten.  

### <a name="mdt-logs"></a>MDT-Protokolle  
 Jedes MDT-Skript erstellt automatisch Protokolldateien bei seiner Ausführung. Die Namen dieser Protokolldateien stimmen mit dem Namen des Skripts überein: „ZTIGather.wsf“ erstellt z.B. eine Protokolldatei namens *ZTIGather.log*. Jedes Skript aktualisiert auch eine allgemeine Masterprotokolldatei („BDD.log“), in der die Inhalte der Protokolldateien zusammengeführt werden, die von MDT-Skripts erstellt werden. MDT-Protokolldateien befinden sich während des Bereitstellungsvorgangs unter C:\MININT\SMSOSD\OSDLOGS. Je nach Art der ausgeführten Bereitstellung werden die Protokolldateien nach dem Abschluss der Bereitstellung entweder nach %WINDIR%\SMSOSD oder nach % WINDIR%\TEMP\SMSOSD verschoben. Für Lite Touch Installation-Bereitstellungen (LTI) starten die Protokolle unter C:\MININT\SMSOSD\OSDLogs. Sie enden unter %WINDIR%\TEMP\DeploymentLogs, wenn die Verarbeitung der Tasksequenz abgeschlossen ist.  

 MDT erstellt die folgenden Protokolldateien:  

-   **BDD.log**. Dies ist die aggregierte MDT-Protokolldatei, die am Ende der Bereitstellung an eine Netzwerkadresse kopiert wird, wenn Sie die **SLShare**-Eigenschaft in der Datei „CustomSettings.ini“ angeben.  

-   **LiteTouch.log**. Diese Datei wird bei LTI-Bereitstellungen erstellt. Sie befindet sich unter %WINDIR%\TEMP\DeploymentLogs, es sei denn, Sie geben die Option **/debug:true** an.  

-   **Skriptname*.log**. Diese Datei wird von jedem MDT-Skript erstellt. *Skriptname* steht für den Namen des betreffenden Skripts.  

-   **SMSTS.log**. Diese Datei wird vom Task-Sequencer erstellt und beschreibt alle Task-Sequencer-Transaktionen. Je nach Bereitstellungsszenario kann sie sich unter %TEMP%, %WINDIR%\System32\ccm\logs, C:\\\_SMSTaskSequence oder C:\SMSTSLog befinden.  

-   **Wizard.log**. Die Bereitstellungs-Assistenten erstellen und aktualisieren diese Datei.  

-   **WPEinit.log**. Diese Datei wird während des Windows PE-Initialisierungsprozesses erstellt und eignet sich zur Problembehandlung von Fehlern, die beim Starten von Windows PE auftreten.  

-   **DeploymentWorkbench_*id*.log**. Diese Protokolldatei wird im Ordner „%temp%“ erstellt, wenn Sie beim Starten der Deployment Workbench **/debug** angeben.  

### <a name="configuration-manager-operating-system-deployment-logs"></a>Betriebssystembereitstellungsprotokolle in Configuration Manager  
 Informationen darüber, welche Betriebssystem-Bereitstellungsprotokolldateien von Microsoft System Center 2012 R2 Configuration Manager erstellt werden, finden Sie unter [Technische Referenz zu Protokolldateien in Configuration Manager](http://technet.microsoft.com/library/hh427342.aspx).  

 Wenn das Windows User State Migration Tool (USMT) ausgeführt wird, fügt das MDT automatisch die Protokollierungsoptionen hinzu, um die USMT-Protokolldateien an den MDT-Protokolldateispeicherorten zu speichern. Folgende Protokolldateien werden zu folgenden Zeitpunkten erstellt:  

-   **USMTEstimate.log**. Wird erstellt, wenn die USMT-Anforderungen geschätzt werden  

-   **USMTCapture.log**. Wird vom USMT beim Erfassen von Daten erstellt  

-   **USMTRestore.log**. Wird vom USMT beim Wiederherstellen von Daten erstellt  

 Das Skript „ZeroTouchInstallation.vbs“ überprüft automatisch die USMT-Fortschrittsprotokolldateien auf Fehler und Warnungen. Das Skript generiert die Ereignis-ID 41010 für Microsoft System Center Operations Manager mit der folgenden Zusammenfassung (wobei *usmt_type* **ESTIMATE**, **SCANSTATE** oder **LOADSTATE** ist; *error_count* ist die Gesamtzahl der gefundenen Fehler, und *warning_count* ist die Gesamtzahl der gefundenen Warnungen):  

```  
ZTI USMT <usmt_type> reported <error_count> errors and <warning_count> warnings  
```  

 Wenn die Zahl der Fehler größer als 0 ist, handelt es sich bei dem Ereignis um einen Fehlertypen. Wenn die Zahl der Warnungen größer als 0 ohne Fehler ist, handelt es sich bei dem Ereignis um einen Warnungstypen. Andernfalls ist das Ereignis ein Informationstyp.  

## <a name="identifying-error-codes"></a>Identifizieren von Fehlercodes  
In Tabelle 1 werden die von den MDT-Skripts erstellten Fehlercodes einschließlich einer Beschreibung aufgelistet. Diese Fehlercodes werden in der Datei „BDD.log“ erfasst.  

### <a name="table-1-error-codes-and-their-description"></a>Tabelle 1. Fehlercodes und deren Beschreibung  

|**Fehlercode**|**Beschreibung**|  
|-|-|  
|5201|Es konnte keine Verbindung zur Bereitstellungsfreigabe hergestellt werden. Die Bereitstellung wird nicht fortgesetzt.|  
|5203|Es konnte keine Verbindung zur Bereitstellungsfreigabe hergestellt werden. Die Bereitstellung wird nicht fortgesetzt.|  
|5205|Es konnte keine Verbindung zur Bereitstellungsfreigabe hergestellt werden. Die Bereitstellung wird nicht fortgesetzt.|  
|5206|Der Bereitstellungs-Assistent wurde abgebrochen oder wurde nicht erfolgreich abgeschlossen. Die Bereitstellung wird nicht fortgesetzt.|  
|5207|Es konnte keine Verbindung zur Bereitstellungsfreigabe hergestellt werden. Die Bereitstellung wird nicht fortgesetzt.|  
|5208|**DeploymentType** wurde nicht festgelegt. Es muss ein Wert für **SkipWizard** festgelegt werden.|  
|5208|Der SMS-Task-Sequencer wurde nicht gefunden. Die Bereitstellung wird nicht fortgesetzt.|  
|5400|Objekt erstellen: ***class_instance* = Neuer *class_name* festlegen**|  
|5490|MSXML2.DOMDocument erstellen.|  
|5495|MSXML2.DOMDocument.ParseErr.ErrCode erstellen.|  
|5496|LoadControlFile.FindFile: *ConfigFile*|  
|5601|Sicherstellen, dass OS guid: %OSGUID% vorhanden ist.|  
|5602|XML mit OSGUID: %OSGUID% öffnen.|  
|5610|Datei überprüfen.|  
|5630|Datei überprüfen: *ImagePath*.|  
|5640|Datei überprüfen: *ImagePath*.|  
|5641|„ImageX.exe“ suchen.|  
|5643|„BootSect.exe“ suchen.|  
|5650|Verzeichnis überprüfen: *SourcePath*.|  
|5651|Verzeichnis überprüfen: *SourcePath*\Platform.|  
|5652|„bootsect.exe“ suchen.|  
|6001|Laufwerk überprüfen.|  
|6002|Laufwerk überprüfen.|  
|6010|Auf TSGUID testen.|  
|6020|Von Robocopy zurückgegebener Wert: *Wert*.|  
|6021|Von Robocopy zurückgegebener Wert: *Wert*.|  
|6101|Auf Datei überprüfen: *DeployCab*.|  
|6102|Sysprep-Dateien aus „DEPLOY.CAB“ erweitern.|  
|6111|„Sysprep.exe“ ausführen.|  
|6121|Sysprep ausführen.|  
|6191|Auf **CloneTag** in der Registrierung testen, um zu prüfen, ob Sysprep abgeschlossen ist.|  
|6192|Auf **SystemSetupInProgress** in der Registrierung testen, um zu prüfen, ob Sysprep abgeschlossen ist.|  
|6401|Autorisierter DHCP-Server.|  
|6501|Computersicherung nicht möglich, kein Netzwerkpfad (**BackupShare**, **BackupDir**) angegeben.|  
|6502|Fehler: IMAGEX wurde nicht gefunden, Sicherung konnte nicht durchgeführt werden.|  
|6601|GetObject(... root/wmi:BCDStore).|  
|6602|BCD.OpenStore (*BCDStore*).|  
|6701|Konfigurierte Schutzvorrichtungen.|  
|6702|Startdateien verschoben.|  
|6703|BDE-Partition erstellen.|  
|6704|Laufwerk defragmentieren.|  
|6705|Laufwerk verkleinern.|  
|6706|Testen auf mehrere Partitionen.|  
|6707|Startdateien erstellen.|  
|6708|Datenträger verschlüsseln.|  
|6709|Verbindung zu MicrosoftVolumeEncryption WMI-Anbieter herstellen.|  
|6710|Verschlüsseln des Datenträgers.|  
|6711|**ProtectKeyWithTPM**.|  
|6712|**ProtectKeyWithTPMAndPIN**.|  
|6713|**ProtectKeyWithTPMAndStartupKey**.|  
|6714|Externen Schlüssel in Datei speichern.|  
|6715|Mit externem Schlüssel schützen.|  
|6716|Externen Schlüssel in Datei speichern.|  
|6717|Schlüssel mit numerischem Kennwort schützen.|  
|6718|**GetKeyProtectorNumberialP@ssword.**|  
|6718|Kennwort in Datei speichern.|  
|6719|*PasswordFile* öffnen.|  
|6720|Datenträger verschlüsseln.|  
|6721|*DiskPartFile* öffnen.|  
|6722|Partition erstellen.|  
|6723|Vorhandenes BDE-Laufwerk abrufen.|  
|6724|*DiskPartFile* öffnen.|  
|6727|Versuchen, *DiskPartFile* zu öffnen.|  
|6729|Textdatei *DiskPartFile* erstellen.|  
|6730|**cmd /c DISKPART.EXE /s *DiskPartFile* >> *LogPath*\ZTIMarkActive_diskpart.log 2>&1** ausführen.|  
|6731|„bcdboot.exe“ suchen.|  
|6732|Mit Microsoft TPM-Anbieter verbinden.|  
|6733|TPM-Instanz in der Anbieterklasse abrufen.|  
|6734|TPM-Instanz abrufen.|  
|6735|Prüfen, ob das TPM aktiviert ist.|  
|6736|Prüfen, ob das TPM aktiviert ist.|  
|6737|Prüfen, ob TPM einen Besitzer hat.|  
|6738|Prüfen, ob der TPM-Besitz zulässig ist.|  
|6739|Prüfen, ob das TPM aktiviert ist.|  
|6740|Prüfen, ob das TPM aktiviert ist.|  
|6741|Prüfen, ob TPM einen Besitzer hat und der TPM-Besitz zulässig ist.|  
|6741|TMP-Besitzerkennwort festgelegt.|  
|6742|TPM-Besitzer-P@ssword auf **AdminP@ssword** festgelegt.|  
|6743|TPM-Besitzer P@ssword auf Wert festlegen.|  
|6744|Prüfen, ob das TPM aktiviert ist.|  
|6745|TPM-Besitzer prüfen.|  
|6746|Auf Endorsement Key-Paar prüfen.|  
|6747|Prüfen, ob das TPM aktiviert ist.|  
|6748|Prüfen, ob der TPM-Besitz zulässig ist.|  
|6749|Besitzer p@ssword in Besitzerautorisierung umwandeln.|  
|6750|Endorsement Key-Paar erstellen.|  
|6751|Besitzerautorisierung ändern.|  
|6752|**Cmd** ausführen.|  
|6753|TPM überprüfen.|  
|6754|BDE-Instanz abrufen.|  
|6755|Schlüssel mit TPM schützen.|  
|6756|Auf zu konfigurierende Wechselmedien überprüfen. **ProtectKeyWithTpmAndStartupKey**.|  
|6757|Schlüssel mit TPM und Startschlüssel schützen.|  
|6758|BDE-PIN suchen.|  
|6759|Schlüssel mit TPM und PIN schützen.|  
|6760|Wechselmedien für **BDEKeyLocation** suchen.|  
|6761|Mit externem Schlüssel schützen.|  
|6762|Wiederherstellungs-P@ssword wird in *PasswordFile* gespeichert.|  
|6764|BitLocker-Richtlinie konfigurieren.|  
|7000|„ZTIConfigure.xml“ wurde nicht gefunden; wird abgebrochen.|  
|7001|Unbeaufsichtigte „AnswerFile“ wird gesucht.|  
|7100|FEHLER: Dieses Skript sollte nur in der Vollversion des Betriebssystems ausgeführt werden.|  
|7101|FEHLER: Nicht genügend Werte für das Generieren der DCPromo-Antwortdatei bereitgestellt.|  
|7102|FEHLER: Für das Erstellen eines neuen Replikatdomänencontrollers erforderliche Eigenschaften wurden nicht angegeben.|  
|7103|FEHLER: Für das Erstellen einer neuen untergeordneten Domäne erforderliche Eigenschaften wurden nicht angegeben.|  
|7104|FEHLER: Für das Erstellen einer neuen Gesamtstruktur erforderliche Eigenschaften wurden nicht angegeben.|  
|7105|FEHLER: Für das Erstellen einer neuen Gesamtstruktur erforderliche Eigenschaften wurden nicht angegeben.|  
|7200|DHCP-Server kann nicht konfiguriert werden, da der Dienst nicht installiert ist.|  
|7201|Bereichsdetails können nicht gelesen werden; `GetScopeDetails()` fehlgeschlagen.|  
|7202|Nicht genügend Werte für Bereichserstellung angegeben.|  
|7203|Nicht genügend Werte bereitgestellt, um IP-Bereich für diesen Bereich festzulegen.|  
|7204|Kein Wert für Bereichsausschlussbereich angegeben.|  
|7300|DNS-Befehle können nicht ausgegeben werden.|  
|7700|Kein Neucomputerszenario; Datenträgerpartition wird beendet.|  
|7701|Datenträger nicht groß genug für System- und BDE-Partitionen, erforderlich = 1,5 GB.|  
|7702|Datenträger nicht groß genug für System- und WinRE-Partitionen, erforderlich = 10 GB.|  
|7703|DeployRoot befindet sich auf Datenträger # *DiskIndex*. Ausführen eines OEM-Szenarios: Überspringen.|  
|7704|Ausführen eines OEM-Szenarios: Überspringen.|  
|7704|Erweiterte und logische Partitionen sind bei BitLocker nicht zulässig.|  
|7712|Sicherstellen, dass Laufwerk/*Volumelaufwerk* vorhanden ist. Formatieren.|  
|7900|„Microsoft.BDD.PnpEnum.exe“ suchen.|  
|7901|**AllDrivers.Exists("*GUID*").**|  
|7904|**AllDrivers.Exists("*GUID*").**|  
|9200|„PkgMgr.exe“ suchen.|  
|9601|FEHLER: ZTITatoo-Task „Status wiederherstellen“ muss in der Vollversion des Betriebssystems ausgeführt werden; wird abgebrochen.|  
|9701|Rückgabecode von USMT-Schätzung ungleich null (0), rc = *Fehler*.|  
|9702|Erfassung des Benutzerstatus nicht möglich; nicht genügend lokaler Speicherplatz und keine Netzwerkpfade (UDShare, UDDir) angegeben.|  
|9703|Rückgabecode von USMT-Erfassung ungleich null, rc = *Fehler*.|  
|9704|Keine gültige Befehlszeilenoption angegeben.|  
|9801|FEHLER: Clientbetriebssystem soll auf einem Computer mit Serverbetriebssystem bereitgestellt werden.|  
|9802|FEHLER: Serverbetriebssystem soll auf einem Computer mit Clientbetriebssystem bereitgestellt werden.|  
|9803|FEHLER: Computer ist nicht für das Upgrade autorisiert (OSInstall=*OSInstall*); wird abgebrochen.|  
|9804|FEHLER: *Speicher* MB Speicher unzureichend. Mindestens *Speicher* MB Speicher erforderlich.|  
|9805|FEHLER: *Prozessorgeschwindigkeit* MHz Prozessorgeschwindigkeit unzureichend.  Prozessor mit mindestens *Prozessorgeschwindigkeit* MHz erforderlich.|  
|9806|FEHLER: unzureichender Speicherplatz auf *Laufwerk*. Zusätzlich *Größe* MB erforderlich.|  
|9807|FEHLER: unzureichender Speicherplatz auf *Laufwerk*. Zusätzlich *Größe* MB erforderlich.|  
|9901|Das Skript „ZTIWindowsUpdate“ darf nicht in Windows PE ausgeführt werden.|  
|9902|ZTIWindowsUpdate wurde ausgeführt und schlug zu oft fehl. Anzahl = *Anzahl*.|  
|9903|Unerwartetes Problem bei der Installation des aktualisierten Windows Update-Agents, rc = *Fehler*.|  
|9904|Fehler beim Erstellen des Objekts: **Microsoft.Update.Session**.|  
|9905|Fehler beim Erstellen des Objekts: **Microsoft.Update.UpdateColl**.|  
|9906|Kritische Datei *Datei* wurde nicht gefunden; wird abgebrochen.|  
|10000|Objekt erstellen: **Set oLTICleanup = New LTICleanup**.|  
|10201|Beitritt zur Domäne *Domäne* nicht möglich. Installation beenden.|  
|10203|„LTISuspend.wsf“ suchen.|  
|10204|Programm *LTISuspend* ausführen.|  
|41024|ImageX ausführen.|  
|52012|Keine Assistentenparameter festgelegt.|  

 Liste 1 enthält einen Auszug aus einer Protokolldatei, die veranschaulicht, wie Sie den Fehlercode ermitteln. In diesem Ausschnitt lautet der gemeldete Fehlercode 5001.  

 **Liste 1. Auszug aus der Datei „SMSTS.log“, die den Fehlercode 5001 enthält**  

```  
.  
.  
.  
The operating system installation failed. Please contact your system administrator for assistance.  

The action "Zero Touch Installation - Validation" failed with exit code 5001  
.  
.  
.  

```  

### <a name="converting-error-codes"></a>Konvertieren von Fehlercodes  
 Viele Fehlercodes in den Protokolldateien wirken mysteriös und lassen sich nur schwer einer tatsächlichen Fehlerbedingung zuordnen. Der folgende Prozess veranschaulicht jedoch, wie ein Fehlercode konvertiert wird, um sinnvolle Informationen zu erhalten, die bei der Problembehebung helfen können.  

 **Problem**: Eine Imageerfassung schlägt mit Fehlercode 0x80070040 fehl.  

 **Erste mögliche Lösung**: Der angezeigte Fehlercode weist ein Hexadezimalformat auf, das Sie in ein Dezimalformat konvertieren müssen. Hierzu benötigen Sie einen wissenschaftlichen Rechner. Der von Windows-Betriebssystemen bereitgestellte Rechner eignet sich gut für diese Aufgabe.  

 **So wird ein Fehlercode konvertiert**  

1.  Klicken Sie auf **Start**, und zeigen Sie auf **Alle Programme**. Zeigen Sie auf **Zubehör**, und klicken Sie dann auf **Rechner**.  

2.  Klicken Sie im Menü **Ansicht** auf **Wissenschaftlich**.  

3.  Wählen Sie **Hex** aus, und geben Sie dann die letzten vier Ziffern des Codes wie in Abbildung 1 gezeigt an – in diesem Fall **0040**.  

     ![ProblembehandlungReferenz1](media/TroubleshootingReference1.jpg "TroubleshootingReference1")  
Abbildung 1: Fehlerkonvertierung  

     **Abbildung 1. Fehlerkonvertierung**  

     Beachten Sie, dass keine führenden Nullen angezeigt werden, wenn sich der Rechner im Hexadezimalmodus befindet.  

4.  Wählen Sie **Dez** aus.  

     Der Hexadezimalwert *40* wird in den Dezimalwert *64* konvertiert.  

5.  Öffnen Sie ein Eingabeaufforderungsfenster, geben Sie **NET HELPMSG 64** ein, und drücken Sie dann die EINGABETASTE.  

     Der Befehl **NET HELPMSG** übersetzt den numerischen Fehlercode in aussagekräftigen Text. Für den hier gezeigten Fehlercode lautet die Übersetzung: „Der angegebene Netzwerkname ist nicht mehr verfügbar.“  

 Diese Information verweist auf ein mögliches Netzwerkproblem auf dem Zielcomputer oder zwischen dem Zielcomputer und dem Server, auf dem sich die Bereitstellungsfreigabe befindet. Mögliche Probleme sind nicht ordnungsgemäß installierte Netzwerktreiber oder ein Konflikt bei den Geschwindigkeits- und Duplexeinstellungen.  

 **Zweite mögliche Lösung:** Verwenden Sie das Hilfsprogramm für die Fehlercodesuche von Microsoft Exchange Server. Dieses Befehlszeilen-Hilfsprogramm ist hilfreich für die Übersetzung von Fehlercodes. Es kann im [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=985) heruntergeladen werden.  

### <a name="review-of-sample-logs"></a>Prüfung von Beispielprotokollen  
 MDT erstellt Protokolldateien, die Sie zur Problembehandlung während des MDT-Bereitstellungsprozesses verwenden können. Der folgende Abschnitt enthält Beispiele, wie Sie die MDT-Protokolldateien verwenden, um Probleme beim Bereitstellungsprozess zu beheben:  

-   Probleme, die sich auf Fehler beim Zugriff auf die MDT-Datenbank (MDT DB) beziehen, wie unter [Fehler beim Zugriff auf die Datenbank](#FailuretoAccesstheDatabase) beschrieben  

####  <a name="FailuretoAccesstheDatabase"></a> Fehler beim Zugriff auf die Datenbank  
 **Problem:** Ein Fehler tritt während einer Bereitstellung auf, die die Datei „CustomSettings.ini“ verwendet, die mehrere Abschnitte enthält und über die Eigenschaft **Priorität** die Priorität der einzelnen zu verarbeitenden Abschnitte angibt. „BDD.log“ enthält die folgenden Fehlermeldungen:  

-   ```  
    ERROR - Opening Record Set (Error Number = -2147217911) (Error Description: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'.)  
    ```  

-   ```  
    ADO error: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'. (Error #-2147217911; Source: Microsoft OLE DB Provider for SQL Server; SQL State: 42000; NativeError: 229  
    ```  

-   ```  
    ERROR - Unhandled error returned by ZTIGather: Object required (424)  
    ```  

> [!NOTE]
>  Aus Gründen der Übersichtlichkeit wurde der Inhalt der Protokolldatei oben so dargestellt, wie er bei Verwendung des Programms Trace32 angezeigt wird.  

 **Mögliche Lösung:** Wie aus der ersten Zeile der Beispielprotokolldatei hervorgeht, besteht das Problem darin, dass die Zugriffsberechtigung für die Datenbank verweigert wurde. Daher kann das Skript keine sichere Verbindung zur Datenbank herstellen, da möglicherweise keine Benutzer-ID und kein Kennwort zur Verfügung stehen. Daher wurde ein Zugriff auf die Datenbank mithilfe des Computerkontos versucht. Die einfachste Möglichkeit zum Umgehen dieses Problems besteht darin, allen Benutzern Lesezugriff auf die Datenbank zu gewähren.  

## <a name="troubleshooting"></a>Problembehandlung  
 Prüfen Sie vor einer eingehenden Problembehandlung die folgenden Elemente, und stellen Sie sicher, dass alle zugehörigen Anforderungen erfüllt sind:  

-   Bei der Installation kann es zu Problemen kommen, wenn nicht alle Hardware- und Softwarevoraussetzungen erfüllt sind.  

### <a name="application-installation"></a>Anwendungsinstallation  
 Überprüfen Sie die möglichen Probleme bei der Anwendungsinstallation und die zugehörigen Lösungen:  

-   Installationsquelldateien, die aus Sicherheitsgründen gesperrt sind, wie unter [Blockierte ausführbare Dateien](#BlockedExecutables) beschrieben  

-   Verlust der Netzwerkverbindung, wie unter [Verlust von Netzwerkverbindungen](#LostNetworkConnections) beschrieben  

-   Installationsfehler 30029 während der Installation von 2007 Microsoft Office System oder zugehörigen Dateien, wie unter [2007 Microsoft Office System](#MicrosoftOfficeSystem) beschrieben  

####  <a name="BlockedExecutables"></a> Blockierte ausführbare Dateien  
 **Problem:** Wenn Installationsquelldateien aus dem Internet heruntergeladen werden, ist es wahrscheinlich, dass sie mit mindestens einem NTFS-Dateisystemdatenstrom markiert sind. Weitere Informationen zu NTFS-Dateidatenströmen finden Sie unter [File Streams (Dateidatenströme)](http://msdn2.microsoft.com/library/aa364404\(VS.85\).aspx). Das Vorhandensein von NTFS-Dateisystemdatenströmen kann dazu führen, dass die Eingabeaufforderung **Datei öffnen > Sicherheitswarnung** angezeigt wird. Die Installation wird erst dann fortgesetzt, wenn Sie bei der Eingabeaufforderung auf **Ausführen** klicken.  

 Wie Abbildung 2 zeigt, können Sie die NTFS-Dateisystemdatenströme mit dem Befehl **Weitere** und dem [Datenstromhilfsprogramm](http://technet.microsoft.com/sysinternals/bb897440.aspx) anzeigen.  

 ![ProblembehandlungReferenz2](media/TroubleshootingReference2.jpg "TroubleshootingReference2")  
Abbildung 2. NTFS-Dateidatenströme  

 **Abbildung 2. NTFS-Dateidatenströme**  

 **Erste mögliche Lösung:** Führen Sie einen Rechtsklick auf die Installationsquelldatei durch, und klicken Sie dann auf **Eigenschaften**. Klicken Sie auf **Zulassen**, und klicken Sie dann auf **OK**, um die NTFS-Dateisystemdatenströme aus der Datei zu entfernen. Wiederholen Sie diesen Vorgang für jede Installationsquelldatei, die durch das Vorhandensein von mindestens einem NTFS-Dateisystemdatenstrom blockiert wird.  

 **Zweite mögliche Lösung:** Verwenden Sie – wie REF \_Ref308173670 \\h Abbildung 2 zeigt – das Datenstromhilfsprogramm, um die NTFS-Dateisystemdatenströme aus der Installationsquelldatei zu entfernen. Das Datenstromhilfsprogramm kann NTFS-Dateisystemdatenströme aus mehreren Dateien oder Ordnern gleichzeitig entfernen.  

####  <a name="LostNetworkConnections"></a> Verlust von Netzwerkverbindungen  
 **Problem:** Eine Installation schlägt möglicherweise fehl, wenn sie Gerätetreiber installiert oder Geräte- und Netzwerkkonfigurationen ändert. Diese Änderungen können die Netzwerkkonnektivität beeinträchtigen, was dazu führt, dass die Installation fehlschlägt.  

 **Mögliche Lösung:** Implementieren Sie das Skript „ZTICacheUtil.vbs“, um das Herunterladen und Ausführen für die Installation zu aktivieren. Dieses Skript optimiert die Ankündigung, um das Herunterladen und Ausführen zu aktivieren. Beim Herunterladen wird der Background Intelligent Transfer Service \(BITS\) verwendet, wenn der Configuration Manager-Verteilungspunkt für webbasiertes Distributed Authoring and Versioning aktiviert und BITS-fähig ist. Gleichzeitig ändert er Configuration Manager dahingehend, dass das Skript „ZTICache.vbs“ zuerst ausgeführt wird, wodurch sichergestellt wird, dass sich das Programm während der Bereitstellung nicht selbst löscht.  

####  <a name="MicrosoftOfficeSystem"></a> 2007 Microsoft Office System  
 **Problem:** Während der Bereitstellung von 2007 Office System und des Einschließens einer Windows Installer-\(MSP\)-Patchdatei schlägt die Installation möglicherweise mit Fehlercode 30029 fehl.  

 Eine weitere Untersuchung der Datei „ZTIApplications.log“ ergibt die folgenden Meldungen:  

-   ```  
    About to run command: \\Server\Deployment$\Tools\X86\bddrun.exe \\Server\Share\Microsoft\Office\2007\Professional\setup.exe /adminfile \\Server\Share\Microsoft\Office\2007\Professional\file.msp  
    ```  

-   ```  
    ZTI Heartbeat: command has been running for 12 minutes (process ID 1600) Return code from command = 30029  
    ```  

-   ```  
    Application Microsoft Office 2007 Professional returned an unexpected return code: 30029  
    ```  

 **Erste mögliche Lösung:** Verschieben Sie die MSP-Datei in das Verzeichnis „Updates“, und führen Sie dann „setup.exe“ ohne Angabe der Option **\/adminfile** aus. Weitere Informationen zum Bereitstellen von Updates während der Installation finden Sie unter [Bereitstellen von 2007 Office System](http://technet.microsoft.com/library/cc303395\(v=Office.12\).aspx).  

 **Zweite mögliche Lösung:** Stellen Sie sicher, dass für die MSP-Datei nicht das Kontrollkästchen **Modalen Dialog unterdrücken** aktiviert wurde. Weitere Informationen zum Konfigurieren dieser Einstellung finden Sie unter [Überblick über die Bereitstellung von 2007 Office System](http://technet.microsoft.com/library/bb490141.aspx).  

### <a name="autologon"></a>Automatische Anmeldung  
 Überprüfen Sie die möglichen Probleme bei der automatischen Anmeldung und die zugehörigen Lösungen:  

-   Unterbrechung des LTI- und des Zero Touch Installation-Bereitstellungsprozesses \(ZTI\) aufgrund von Anmeldenachrichten für die Sicherheit, wie unter [Anmeldenachrichten für die Sicherheit](#LogonSecutiryBanners) beschrieben  

-   Unterbrechung der LTI- und ZTI-Bereitstellungsprozesse aufgrund von Eingabeaufforderungen für Benutzeranmeldeinformationen, wie unter [Angeforderte Benutzeranmeldeinformationen](#PromtedforUserCredentials) beschrieben  

####  <a name="LogonSecutiryBanners"></a> Anmeldesicherheitsbanner  
 **Problem:** MDT-Tasksequenzen werden während einer interaktiven Benutzersitzung verarbeitet, weshalb es dem Zielcomputer gestattet sein muss, sich automatisch mit einem angegebenen Administratorkonto anzumelden. Wenn ein Gruppenrichtlinienobjekt \(GPO\) vorhanden ist, das ein Anmeldesicherheitsbanner erzwingt, ist es dieser automatischen Anmeldung nicht gestattet fortzufahren, da das Sicherheitsbanner den Anmeldevorgang anhält, während es darauf wartet, dass ein Benutzer die genannte Richtlinie akzeptiert.  

 **Mögliche Lösung:** Achten Sie darauf, dass das GPO auf bestimmte Organisationseinheiten \(OE\) angewendet wird und nicht im Standarddomänen-GPO enthalten ist. Wenn Sie Computer zur Domäne hinzufügen, geben Sie an, dass diese zu einer Organisationseinheit hinzugefügt werden, die nicht von einem GPO betroffen ist, das ein Anmeldesicherheitsbanner erzwingt. Schließen Sie im Tasksequenz-Editor als einen der letzten Tasksequenzschritte ein Skript ein, welches das Computerkonto zu der gewünschten Organisationseinheit verschiebt.  

> [!NOTE]
>  Bei der Wiederverwendung vorhandener Konten der Active Directory®-Domänendienste \(AD DS\) müssen Sie sicherstellen, dass Sie vor der Bereitstellung auf dem Zielcomputer das Konto des Zielcomputers auf eine Organisationseinheit verschoben haben, die nicht von dem GPO betroffen ist, welches das Anmeldesicherheitsbanner erzwingt.  

####  <a name="PromtedforUserCredentials"></a> Angeforderte Benutzeranmeldeinformationen  
 **Problem:** Sie haben ein Image eines Computers erstellt, der der Domäne hinzugefügt wurde. Beim Bereitstellen des neuen Images auf einem Zielcomputer wird der Bereitstellungsprozess angehalten, da keine automatische Anmeldung erfolgt und der Benutzer aufgefordert wird, die entsprechenden Anmeldeinformationen einzugeben. Der Bereitstellungsprozess wird fortgesetzt, nachdem die Anmeldeinformationen bereitgestellt wurden und der Benutzer angemeldet ist.  

 **Mögliche Lösung:** Beim Erfassen von Images darf der Quellcomputer nicht zu einer Domäne hinzugefügt worden sein. Wenn der Computer zu einer Domäne hinzugefügt wurde, fügen Sie den Computer zu einer Arbeitsgruppe hinzu, erfassen Sie das Image erneut, und versuchen Sie die Bereitstellung auf einem Zielcomputer, um festzustellen, ob das Problem behoben wurde.  

### <a name="bios"></a>BIOS  
 **Problem:** Bei der Bereitstellung auf einem Zielcomputer, der mit der Intel vPro-Technologie ausgestattet ist, kann die Bereitstellung mit einem Abbruchfehler enden. Obwohl alle aktualisierten Treiber als standardisierte Treiber in die Deployment Workbench aufgenommen wurden, startet der Zielcomputer nicht.  

 Mögliche Lösung: Überprüfen Sie die Einstellungen im Basic Input\/Output System \(BIOS\) des Zielcomputers, um festzustellen, ob der Standardmodus für Serial Advanced Technology Attachment als Advanced Host Controller Interface \(AHCI\) konfiguriert ist. Leider unterstützen bestimmte Windows-Betriebssysteme AHCI nicht standardmäßig.  

### <a name="database-problems"></a>Datenbankprobleme  
 Überprüfen Sie Probleme und Lösungen, die Datenbanken betreffen:  

-   Fehler, die durch nicht ordnungsgemäß generierte Firewalls auf dem Datenbankserver verursacht werden, wie unter [Blockierte SQL Server-Browseranforderungen](#BlockedSQLServerBrowserRequests) beschrieben  

-   Fehler, die durch unterbrochene Verbindungen zum Datenbankserver verursacht werden, wie unter [Named Pipe-Verbindungen](#NamedPipeConnections) beschrieben  

####  <a name="BlockedSQLServerBrowserRequests"></a> Blockierte SQL Server-Browseranforderungen  
 **Problem:** Während der MDT-Bereitstellung können Informationen aus Microsoft SQL Server®-Datenbanken abgerufen werden. Möglicherweise werden jedoch Fehler generiert, die auf eine nicht ordnungsgemäß konfigurierte Firewall auf dem Datenbankserver zurückzuführen sind.  

 **Mögliche Lösung:** Die Windows-Firewall in Windows Server verhindert einen nicht autorisierten Zugriff auf Computerressourcen. Wenn die Firewall jedoch nicht ordnungsgemäß konfiguriert ist, können Versuche, eine Verbindung zu einer SQL Server-Instanz herzustellen, blockiert werden. Um auf eine Instanz von SQL Server zuzugreifen, die sich hinter der Firewall befindet, konfigurieren Sie die Firewall auf dem Computer, auf dem SQL Server ausgeführt wird. Weitere Informationen zum Konfigurieren der Firewallports für SQL Server finden Sie im Microsoft-Support-Artikel [How do I open the firewall port for SQL Server on Windows Server 2008? (Wie wird der Firewallport für SQL Server auf Windows Server 2008 geöffnet?)](http://support.microsoft.com/kb/968872)  

####  <a name="NamedPipeConnections"></a> Named Pipe-Verbindungen  
 **Problem:** Während der MDT-Bereitstellung können Informationen aus SQL Server-Datenbanken abgerufen werden. Allerdings werden möglicherweise Fehler generiert, die auf unterbrochene SQL Server-Verbindungen zurückzuführen sind. Diese können dadurch verursacht werden, dass Named Pipe-Verbindungen in Microsoft SQL Server nicht aktiviert werden.  

 **Mögliche Lösung:** Um diese Probleme zu beheben, aktivieren Sie Named Pipes in SQL Server. Geben Sie auch die **SQLShare**-Eigenschaft an, die beim Herstellen einer Verbindung zu einer externen Datenbank mithilfe von Named Pipes erforderlich ist. Verwenden Sie beim Herstellen einer Verbindung mithilfe von Named Pipes die integrierte Sicherheit, um die Verbindung zur Datenbank herzustellen. Bei LTI-Bereitstellungen stellt das von Ihnen angegebene Benutzerkonto die Verbindung zu der Datenbank her. Bei ZTI-Bereitstellungen, die Configuration Manager verwenden, stellt das Netzwerkzugriffskonto die Verbindung zur Datenbank her. Da Windows PE standardmäßig keinen Sicherheitskontext besitzt, müssen Sie eine Netzwerkverbindung zum Datenbankserver herstellen, um einen Sicherheitskontext für den Benutzer einzurichten, der die Verbindung herstellen wird.  

 Die Netzwerkfreigabe, die die **SQLShare**-Eigenschaft angibt, bietet eine Möglichkeit, eine Verbindung zum Server herzustellen, um einen richtigen Sicherheitskontext zu erhalten. Sie benötigen Lesezugriff auf die Freigabe. Nachdem die Verbindung hergestellt wurde, können Sie anschließend die Named Pipe-Verbindung zur Datenbank einrichten. Die **SQLShare**-Eigenschaft ist nicht erforderlich und sollte nicht verwendet werden, wenn eine TCP\/IP-Verbindung zur Datenbank hergestellt wird.  

 Aktivieren Sie Named Pipe-Verbindungen, indem Sie die folgenden Aufgaben basierend auf der von Ihnen verwendeten Version von SQL Server ausführen:  

-   Aktivieren Sie Named Pipe-Verbindungen für SQL Server 2008 R2 wie dies unter [Named Pipe-Verbindungen in SQL Server 2008 R2 aktivieren](#EnableNamedPipeConnectionsinSQLServer) beschrieben wird.  

-   Aktivieren Sie Named Pipe-Verbindungen für SQL Server 2005 wie unter [Named Pipe-Verbindungen in SQL Server 2005 aktivieren](#EnableNamedPipeConnectionsinSQL) beschrieben.  

#####  <a name="EnableNamedPipeConnectionsinSQLServer"></a> Named Pipe-Verbindungen in SQL Server 2008 R2 aktivieren  
 Führen Sie die folgenden Schritte aus, um Named Pipe-Verbindungen in SQL Server 2008 R2 zu aktivieren:  

1.  Klicken Sie auf dem Computer mit SQL Server 2008 R2, auf dem sich die abzufragende Datenbank befindet, auf **Starten**, und zeigen Sie dann auf **Alle Programme**. Zeigen Sie auf **Microsoft SQL Server 2008 R2**, und klicken Sie dann auf **SQL Server Management Studio**.  

2.  Klicken Sie in der **Microsoft SQL Server Management Studio**-Konsole im **Objekt-Explorer**  mit der rechten Maustaste auf ***sql\_server\_name***, und klicken Sie dann auf **Eigenschaften** \(wobei *sql\_server\_name* der Name des Computers ist, auf dem der zu konfigurierende SQL Server ausgeführt wird\).  

3.  Das Dialogfeld Servereigenschaften \- ***sql\_server\_name*** wird angezeigt.  

4.  Klicken Sie im Dialogfeld **Servereigenschaften** \- ***sql\_server\_name*** unter **Seite auswählen** auf **Verbindungen**.  

5.  Vergewissern Sie sich auf der Seite **Verbindungen**, dass das Kontrollkästchen **Remoteverbindungen mit diesem Server zulassen** aktiviert ist, und klicken Sie dann auf **OK**.  

6.  Beenden Sie die Microsoft SQL Server Management Studio-Konsole.  

7.  Klicken Sie auf dem Computer mit SQL Server 2008 R2, auf dem sich die abzufragende Datenbank befindet, auf **Starten**, und zeigen Sie dann auf **Alle Programme**. Zeigen Sie auf **Microsoft SQL Server 2008 R2**, zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  

8.  Wechseln Sie in der **SQL Server-Konfigurations-Manager**-Konsole zu SQL Server-Konfigurations-Manager \(Lokal\) \/ SQL Server-Netzwerkkonfiguration \/ Protokolle für  *sql\_instance* \(wobei *sql\_instance* der Name der zu konfigurierenden SQL Server-Instanz ist\).  

9. Klicken Sie im Detailbereich mit der rechten Maustaste auf **Named Pipes**, und klicken Sie dann auf **Aktivieren**.  

     Das Dialogfeld „Warnung“ wird angezeigt und informiert Sie, dass die Änderungen gespeichert werden, jedoch erst dann wirksam werden, wenn der Dienst beendet und neu gestartet wird.  

10. Klicken Sie im Dialogfeld **Warnung** auf **OK**.  

11. Wechseln Sie in der **SQL Server-Konfigurations-Manager**-Konsole zu SQL Server-Konfigurations-Manager \(Lokal\) \/ SQL Server-Dienste.  

12. Klicken Sie im Detailbereich mit der rechten Maustaste auf **SQL Server*\(sql\_instance\)***, und klicken Sie dann auf **Neu starten**, \(wobei *sql\_instance* der Name der SQL Server-Instanz ist, die Sie in Schritt 2 konfiguriert haben\).  

     Die SQL Server-Konfigurations-Manager-Statusanzeige erscheint und zeigt den Status des Neustarts der Dienste an. Nach dem Neustart des Dienstes wird die Statusanzeige geschlossen.  

13. Schließen Sie die SQL Server-Konfigurations-Manager-Konsole.  

 Weitere Informationen finden Sie unter [How to enable remote connections in SQL Server 2008 (Aktivieren von Remoteverbindungen in SQL Server 2008)](http://blogs.msdn.com/b/walzenbach/archive/2010/04/14/how-to-enable-remote-connections-in-sql-server-2008.aspx).  

#####  <a name="EnableNamedPipeConnectionsinSQL"></a> Named Pipe-Verbindungen in SQL Server 2005 aktivieren  
 Führen Sie die folgenden Schritte aus, um Named Pipe-Verbindungen in SQL Server 2005 zu aktivieren:  

1.  Klicken Sie auf dem Computer mit SQL Server 2005, auf dem sich die abzufragende Datenbank befindet, auf **Starten**, und zeigen Sie dann auf **Alle Programme**. Zeigen Sie auf **Microsoft SQL Server 2005**, zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Oberflächenkonfiguration**.  

2.  Klicken Sie im Dialogfeld **SQL Server 2005-Oberflächenkonfiguration** auf **Oberflächenkonfiguration für Dienste und Verbindungen**.  

3.  Navigieren Sie im Dialogfeld **Oberflächenkonfiguration für Dienste und Verbindungen – *server\_name***, \(wobei *server\_name* der Name des Computers ist, auf dem SQL Server 2005 ausgeführt wird\) unter **Wählen Sie eine Komponente aus, und konfigurieren Sie ihre Dienste und Verbindungen** zu MSSQLSERVER\\Database Engine, und klicken Sie dann auf **Remoteverbindungen**.  

4.  Klicken Sie auf **Lokale Verbindungen und Remoteverbindungen**, klicken Sie auf **TCP\/IP und Named Pipes verwenden**, und klicken Sie dann auf **Übernehmen**.  

5.  Gehen Sie im Dialogfeld **Oberflächenkonfiguration für Dienste und Verbindungen – *server\_name*** \(wobei *server\_name* der Name des Computers ist, auf dem SQL Server 2005 ausgeführt wird\) unter **Wählen Sie eine Komponente aus, und konfigurieren Sie ihre Dienste und Verbindungen** zu MSSQLSERVER\\Database Engine, und klicken Sie dann auf **Dienst**.  

6.  Klicken Sie auf **Beenden**.  

     Der MSSQLSERVER-Dienst wird beendet.  

7.  Klicken Sie auf **Start**.  

     Der MSSQLSERVER-Dienst wird gestartet.  

8.  Klicken Sie auf **OK**.  

9. Schließen Sie die SQL Server 2005-Oberflächenkonfiguration.  

 Weitere Informationen finden Sie im Microsoft-Support-Artikel [Konfigurieren von SQL Server 2005 für Remoteverbindungen](http://support.microsoft.com/kb/914277).  

### <a name="deployment-scripts"></a>Bereitstellungsskripts  
 Überprüfen Sie Probleme und Lösungen, die MDT betreffen:  

-   Benutzeranmeldeinformationen werden angefordert, und möglicherweise wird Fehler 0x80070035 ausgegeben, wie unter [Credentials_script](#Credentials_script) beschrieben  

-   Fehlermeldung „‘Wuredist.cab‘ wurde nicht gefunden“ wird angezeigt, wie unter [ZTIWindowsUpdate](#ZTIWindowsUpdate) beschrieben  

####  <a name="Credentials_script"></a> Credentials\_script  
 **Problem:** Beim letzten Start eines neu bereitgestellten Computers wird der Benutzer aufgefordert, Anmeldeinformationen bereitzustellen, und möglicherweise wird Fehler 0x80070035 angezeigt, der angibt, dass der Netzwerkpfad nicht gefunden wurde.  

 **Mögliche Lösung:** Achten Sie darauf, dass die WIM-Datei keinen MININT- oder \_SMSTaskSequence-Ordner beinhaltet. Verwenden Sie zum Löschen dieser Ordner zuerst das ImageX-Hilfsprogramm, um die WIM-Datei bereitzustellen, und löschen Sie dann die Ordner.  

> [!NOTE]
>  Wenn der Fehler „Zugriff verweigert“ auftritt, während Sie versuchen, den Ordner aus der WIM-Datei zu löschen, öffnen Sie ein Eingabeaufforderungsfenster, wechseln Sie in das Stammverzeichnis des in der WIM-Datei enthaltenen Images, und führen Sie dann **RD MININT** und **RD \_ SMSTaskSequence** aus.  

####  <a name="ZTIWindowsUpdate"></a> ZTIWindowsUpdate  
 **Problem:** Wenn Sie das Skript „ZTIWindowsUpdate.wsf“ verwenden, um während der Bereitstellung Softwareupdates anzuwenden, müssen Sie beachten, dass dieses Skript möglicherweise direkt mit der Microsoft Update-Website kommuniziert, um die erforderlichen Windows Update-Agent-Binärdateien herunterzuladen und zu installieren, nach anwendbaren Softwareupdates zu suchen, die Binärdateien für die anwendbaren Softwareupdates herunterzuladen und anschließend die heruntergeladenen Binärdateien zu installieren. Dieser Vorgang setzt voraus, dass Ihre Netzwerkinfrastruktur so konfiguriert ist, dass der Zielcomputer auf die Microsoft Update-Website zugreifen darf.  

 Wenn die Bereitstellungsfreigabe nicht die Windows Update-Agent-Installationsdateien enthält und der Zielcomputer keinen entsprechenden Zugriff auf das Internet hat, wird in den Dateien „ZTIWindowsUpdate.log“ und „BDD.log“ der Fehler „‘wuredist.cab‘ wurde nicht gefunden“ gemeldet.  

 **Mögliche Lösung:** Befolgen Sie die Schritte im Abschnitt „ZTIWindowsUpdate.wsf“ im MDT-Dokument *Toolkit-Referenz*.  

### <a name="deployment-shares"></a>Bereitstellungsfreigaben  
 Überprüfen Sie Probleme und Lösungen, die Bereitstellungsfreigaben betreffen:  

-   Das Aktualisieren von WIM-Dateien schlägt beim Aktualisieren einer Bereitstellungsfreigabe fehl, wie dies unter [Fehler beim Aktualisieren von WIM-Dateien](#FailuretoUpdateWIMFiles) beschrieben wird.  

####  <a name="FailuretoUpdateWIMFiles"></a> Fehler beim Aktualisieren von WIM-Dateien  
 In einer „einfachen“ Umgebung:  

-   MDT übernimmt in der Regel „WIMGAPI.DLL“ aus C:\\Windows\\system32 \(stets im Pfad\). Die Version dieser „WIMGAPI.DLL“ muss mit der Version \((dem Build)\) des Betriebssystems übereinstimmen.  

-   Bei einem 64\-Bit-Betriebssystem verwendet MDT stets die X64-WIMGAPI.DLL-Datei. Nur diese Datei sollte sich im Systempfad befinden. Bei einem 32\-Bit-Betriebssystem verwendet MDT stets die x86-WIMGAPI.DLL-Datei. Nur diese Datei sollte sich im System-PFAD befinden. \(Andere Produkte wie Configuration Manager verwenden die 32\-Bit-Version von „WIMGAPI. DLL“, auch auf einem 64\-Bit-Betriebssystem, aber sie verwalten und installieren diese Version.\)  

 **Problem:** Beim Versuch, eine Bereitstellungsfreigabe zu aktualisieren, erhält der Benutzer die Information, dass die Bereitstellung einer oder mehrerer WIM-Dateien nicht erfolgreich war.  

 **Mögliche Lösung:** Öffnen Sie ein Eingabeaufforderungsfenster, und führen Sie **where WIMGAPI. DLL** aus. Stellen Sie für den ersten Eintrag in der Liste \(dem ersten beim Durchsuchen des Pfads gefundenen Standort\) sicher, dass die Eigenschaft **Version** mit dem installierten Build des Windows Assessment and Deployment Kit \(Windows ADK\) übereinstimmt. Stellen Sie außerdem sicher, dass die Eigenschaft der Buildnummer des Betriebssystems entspricht.  

### <a name="the-windows-deployment-wizard"></a>Der Windows-Bereitstellungs-Assistent  
 Überprüfen Sie Probleme und Lösungen, die den Windows-Bereitstellungs-Assistenten betreffen:  

-   Seiten des Windows-Bereitstellungs-Assistenten werden auch dann angezeigt, wenn LTI so konfiguriert ist, dass die Seiten des Assistenten übersprungen werden sollen. Dies wird unter [Seiten des Assistenten werden nicht übersprungen](#WizardPagesareNotSkipped) beschrieben.  

####  <a name="WizardPagesareNotSkipped"></a> Seiten des Assistenten werden nicht übersprungen  
 **Problem:** Eine Seite des Assistenten wird angezeigt, obwohl die MDT DB oder die Datei „CustomSettings.ini“ angeben, dass der Assistent übersprungen werden soll.  

 **Mögliche Lösung:** Um eine Seite des Assistenten ordnungsgemäß zu überspringen, müssen Sie alle Eigenschaften, die auf dieser Seite des Assistenten angegeben würden, in der MDT DB bzw. in der Datei „CustomSettings.ini“ mit den entsprechenden Werten angeben. Wenn eine Eigenschaft für eine übersprungene Assistentenseite nicht ordnungsgemäß konfiguriert ist, wird diese Seite angezeigt. Weitere Informationen darüber, welche Eigenschaften erforderlich sind, um sicherzustellen, dass eine Seite des Assistenten übersprungen wird, finden Sie im Abschnitt „Providing Properties for Skipped Deployment Wizard Pages“ (Bereitstellen von Eigenschaften für übersprungene Seiten des Bereitstellungs-Assistenten) in der MDT-Dokumentation *Toolkit-Referenz*.  

### <a name="disks-and-partitioning"></a>Datenträger und Partitionierung  
 Überprüfen Sie Probleme und Lösungen, die die Datenträgerpartitionierung betreffen:  

-   Probleme mit der BitLocker®-Laufwerkverschlüsselung, wie unter [BitLocker-Laufwerkverschlüsselung](#BitLockerDriveEncryption) beschrieben  

-   Fehler bei der Datenträgerpartitionierung, wie unter „Fehler bei der Datenträgerpartitionierung“ beschrieben  

-   Durch logische oder dynamische Datenträger verursachte Fehler bei Bereitstellungsszenarios, die den Computer aktualisieren, wie unter [Unterstützung für logische und dynamische Datenträger](#SupportforLoogicalandDynamicDisks) beschrieben  

####  <a name="BitLockerDriveEncryption"></a> BitLocker-Laufwerkverschlüsselung  
 Für eine ordnungsgemäße Bereitstellung von BitLocker ist eine bestimmte Konfiguration erforderlich. Die folgenden potenziellen Probleme können mit der Konfiguration des Zielcomputers zusammenhängen:  

-   Bei ZTI- und UDI-Bereitstellungen schlägt das Skript ZTIBde.wsf fehl, und es wird ein Fehler ausgegeben, der besagt, dass der Registrierungsschlüssel „HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName“ nicht zum Lesen geöffnet werden kann. Dies wird unter [ZTIBde.wsf-Skript schlägt mit dem Fehler „Unable to open registry key ‚HKEY_CURRENT_USER\Control Panel\International\LocaleName‘ for reading“](#ZTIBde.wsf) beschrieben.  

-   USB-Geräte, CD-Laufwerke, DVD-Laufwerke oder andere Wechselmediengeräte auf dem Zielcomputer, die mit mehreren Laufwerkbuchstaben angezeigt werden, wie in [Devices Appear as Multiple Drive Letters (Geräte werden mit mehreren Laufwerkbuchstaben angezeigt)](#DevicesAppearasMultipleDriveLetters) beschrieben  

-   Verkleinern von Laufwerk C: auf dem Zielcomputer, um ausreichend freien Speicherplatz auf dem Datenträger bereitzustellen, wie unter [Probleme beim Verkleinern von Datenträgern](#ProblemswithShrinkingDisks) beschrieben  

#####  <a name="ZTIBde.wsf"></a> ZTIBde.wsf-Skript schlägt mit dem Fehler „Unable to open registry key ‚HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName‘ for reading“ fehl  
 **Problem:** Beim Versuch, BitLocker auf dem Zielcomputer in ZTI oder UDI bereitzustellen, schlägt das ZTIBde.wsf-Skript mit dem Fehler „Unable to open registry key ‚HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName‘ for reading” (Registrierungsschlüssel „HKEY_CURRENT_USER\Control Panel\International\LocaleName“ kann nicht zum Lesen geöffnet werden) fehl.  

 **Mögliche Lösung:** Geben Sie in der Eigenschaft **UILanguage** das Gebietsschema an. In ZTI und UDI wird das ZTIBde.wsf-Skript in der Systemsteuerung ausgeführt, weshalb kein vollständiges Benutzerprofil geladen wird. Wenn das ZTIBde.wsf-Skript versucht, die Gebietsschemainformationen zu lesen, befinden sich diese nicht in der Registrierung, da die Registrierung \(Benutzerprofil\) nicht vollständig geladen wurde. Geben Sie zur Problemumgehung in der Eigenschaft **UILanguage** das Gebietsschema an.  

#####  <a name="DevicesAppearasMultipleDriveLetters"></a> Geräte werden mit mehreren Laufwerkbuchstaben angezeigt  
 **Problem:** Einige Geräte werden unter Umständen je nach ihrer Partitionierung mit mehreren logischen Laufwerkbuchstaben angezeigt. In einigen Fällen können sie ein 1,44\-Megabyte \(MB\) Diskettenlaufwerk und ein Speicherlaufwerk emulieren. Daher weist Windows möglicherweise dieselben Laufwerkbuchstaben A und B für die Diskettenlaufwerksemulation und F für das Speicherlaufwerk zu. MDT-Skripts verwenden standardmäßig den niedrigsten Laufwerkbuchstaben \(in diesem Beispiel A\).  

 **Mögliche Lösung:** Überschreiben Sie die Standardeinstellung auf der Seite **Specify the BitLocker recovery details (BitLocker-Wiederherstellungsdetails angeben)** im Windows-Bereitstellungs-Assistenten. Die Zusammenfassungsseite für den Windows-Bereitstellungs-Assistenten zeigt eine Warnung an, um den Benutzer zu informieren, welcher Laufwerkbuchstabe ausgewählt wurde, um BitLocker-Wiederherstellungsinformationen zu speichern. Darüber hinaus erfassen die Dateien „BDD.log“ und „ZTIBDE.log“ die erkannten Wechselmediengeräte sowie das Gerät, das ausgewählt wurde, um die BitLocker-Wiederherstellungsinformationen zu speichern.  

#####  <a name="ProblemswithShrinkingDisks"></a> Probleme beim Verkleinern von Datenträgern  
 **Problem:** Auf dem Zielcomputer ist nicht genügend freier Speicherplatz vorhanden, um BitLocker zu aktivieren. Zum Bereitstellen von BitLocker auf einem Zielcomputer sind mindestens 2 Gigabyte \(GB\) freier Speicherplatz erforderlich ist, um das Systemvolume zu erstellen. Das *Systemvolume* ist das Volume, das die hardwarespezifischen Dateien enthält, die notwendig sind, um Windows zu laden, nachdem das BIOS den Computer gestartet hat.  

 **Erste mögliche Lösung:** Verwenden Sie auf vorhandenen Computern das Tool Diskpart, um Laufwerk C: so zu verkleinern, dass das Systemvolume erstellt werden kann. In einigen Fällen kann das Tool Diskpart jedoch Laufwerk C: möglicherweise nicht ausreichend verkleinern, um 2 GB freien Speicherplatz bereitzustellen (möglicherweise aufgrund von fragmentiertem Speicherplatz auf Laufwerk C:).  

 Eine mögliche Lösung für dieses Problem besteht darin, Laufwerk C: zu defragmentieren. Führen Sie hierzu die folgenden Schritte aus:  

1.  Führen Sie den Diskpart-Befehl **shrink querymax** aus, um die maximale Menge an Festplattenspeicher zu ermitteln, die freigegeben werden kann.  

2.  Wenn der in Schritt 1 zurückgegebene Wert kleiner als 2 GB ist, löschen Sie auf Laufwerk C: alle nicht benötigten Dateien und defragmentieren Sie dann das Laufwerk.  

3.  Führen Sie den Diskpart-Befehl **shrink querymax** erneut aus, um sich zu vergewissern, dass mehr als 2 GB Speicherplatz freigegeben werden können.  

4.  Wenn der in Schritt 3 zurückgegebene Wert immer noch kleiner als 2 GB ist, führen Sie eine der folgenden Aufgaben aus:  

    -   Defragmentieren Sie Laufwerk C: mehrere Male, um sicherzustellen, dass es vollständig optimiert ist.  

    -   Sichern Sie die Daten auf Laufwerk C:, löschen Sie die vorhandene Partition, erstellen Sie eine neue Partition, und stellen Sie dann die Daten auf der neuen Partition wieder her.  

 **Zweite mögliche Lösung:** Das ZTIBDE.wsf-Skript führt das Datenträgervorbereitungstool \(bdehdcfg.exe\) aus und konfiguriert standardmäßig die Partitionsgröße des Systemvolume mit 2 GB. Sie können das ZTIBDE.wsf-Skript bei Bedarf anpassen, um den Standardwert zu ändern. Ein Ändern des MDT-Skripts wird jedoch nicht empfohlen.  

####  <a name="SupportforLoogicalandDynamicDisks"></a> Unterstützung für logische und dynamische Datenträger  
 **Problem:** Bei der Ausführung eines Bereitstellungsszenarios, bei dem der Computer aktualisiert wird, kann der Bereitstellungsprozess fehlschlagen, wenn die Bereitstellung auf einem Zielcomputer erfolgt, der logische Laufwerke oder dynamische Datenträger verwendet.  

 **Mögliche Lösung:** MDT unterstützt keine Bereitstellung von Betriebssystemen auf logischen Laufwerken oder dynamischen Datenträgern.  

### <a name="domain-join"></a>Domäne beitreten  
 **Problem:** Während der Bereitstellung verwenden Sie den Windows-Bereitstellungs-Assistenten, um alle erforderlichen Informationen für den Zielcomputer bereitzustellen, einschließlich der Anmeldeinformationen, der Domänenbeitrittsinformationen und der statischen IP-Konfiguration. Nachdem das Setup abgeschlossen ist, stellen Sie fest, dass das System nicht der Domäne beigetreten ist und sich noch in einer Arbeitsgruppe befindet.  

 **Mögliche Lösung:** Eine LTI-Bereitstellung von MDT konfiguriert die statischen IP-Informationen, sobald das Betriebssystem ausgeführt wird. Wenn sich der Zielcomputer in einem Netzwerksegment befindet, das nicht über ein Dynamic Host Configuration Protocol \(DHCP\) verfügt, schlägt ein automatischer Domänenbeitritt in „Unattend.xml“ fehl, wenn kein DHCP vorhanden ist.  

 Konfigurieren Sie „Unattend.xml“ für den Beitritt zu einer Arbeitsgruppe. Verwenden Sie anschließend den integrierten Tasksequenzschritt **Wiederherstellen aus Domäne**, um in der Tasksequenz einen Schritt hinzuzufügen, mit dem der Beitritt zur Domäne erfolgt, nachdem die statische IP-Adresse angewendet wurde.  

### <a name="driver-installation"></a>Treiberinstallation  
 Um eine bestmögliche Benutzererfahrung zu gewährleisten, sollte die Installation von Hardwaregeräten und Softwaretreibern möglichst nahtlos erfolgen, d.h. mit geringem oder ohne Benutzereingriff. Microsoft bietet Tools und Richtlinien, die die Erstellung von Installationspaketen erleichtern, die dieses Ziel erfüllen. Allgemeine Informationen zur Installation von Treibern finden Sie unter [Geräte- und Treiberinstallation](http://www.microsoft.com/whdc/driver/install/default.mspx).  

 Überprüfen Sie Probleme und Lösungen, die die Installation von Gerätetreibern betreffen:  

-   Probleme, die auftreten, wenn $OEM$-Massenspeichertreiber mit MDT verwendet werden (wie unter „Kombinieren von $OEM$-Massenspeichertreibern mit MDT-Massenspeicherlogik“ beschrieben)  

-   Problembehandlung bei der Installation von Gerätetreibern mit „SetupAPI.log“, wie unter [Problembehandlung bei der Geräteinstallation mit „SetupAPI.log“](#TroubleshootDeviceInstallationwithSetupAPI.log) beschrieben  

####  <a name="TroubleshootDeviceInstallationwithSetupAPI.log"></a> Problembehandlung bei der Geräteinstallation mit „SetupAPI.log“  
 Das Whitepaper [Troubleshooting Device Installation with the SetupAPI Log File (Problembehandlung bei der Geräteinstallation mit der SetupAPI-Protokolldatei)](http://msdn.microsoft.com/windows/hardware/gg463393.aspx) enthält Informationen zum Debuggen der Windows-Geräteinstallation. Dieses Dokument stellt insbesondere Richtlinien für Treiberentwickler und -tester bezüglich der Auslegung der SetupAPI-Protokolldatei bereit.  

 Eine der nützlichsten Protokolldateien für Debug-Zwecke ist die Datei „SetupAPI.log“. Es handelt sich dabei um eine reine Textdatei, in der die Informationen verwaltet werden, die die Setup-API zu Geräteinstallationen, Service Pack-Installationen und Update-Installationen erfasst. Insbesondere verwaltet die Datei einen Datensatz der Geräte- und Treiberänderungen sowie wichtiger Systemänderungen ab der neuesten Windows-Installation. Dieses Dokument konzentriert sich auf die Verwendung der SetupAPI-Protokolldatei für die Problembehandlung bei der Geräteinstallation. Es beschreibt nicht die Abschnitte der Protokolldatei, die Service Pack- und Update-Installationen betreffen.  

### <a name="new-computer-deployments"></a>Bereitstellungen auf neuen Computern  
 Überprüfen Sie die Probleme und Lösungen, die eine Bereitstellung auf neuen Computern betreffen:  

-   Probleme beim Starten des Bereitstellungsprozesses mit Pre\-Boot Execution Environment \(PXE\), wie unter [PXE-Start](#PXEBoot) beschrieben  

####  <a name="PXEBoot"></a> PXE-Start  
 Das PXE-Protokoll funktioniert im Prinzip wie folgt: Der Clientcomputer initiiert das Protokoll durch Senden eines DHCP Discover-Pakets, das eine Erweiterung enthält, anhand derer erkennbar ist, dass die Anforderung von einem Clientcomputer stammt, der das PXE-Protokoll implementiert. Indem er voraussetzt, dass ein Startserver verfügbar ist, der dieses erweiterte Protokoll implementiert, sendet der Startserver ein Angebot, das die IP-Adresse des Servers enthält, auf dem der Client verarbeitet werden wird. Der Client verwendet das Trivial File Transfer Protocol, um die ausführbare Datei vom Startserver herunterzuladen. Schließlich wird auf dem Clientcomputer das heruntergeladene Bootstrap-Programm ausgeführt.  

 Die erste Phase dieses Protokolls wird mittels Piggyback mit einer Teilmenge der DHCP-Meldungen ausgeführt, sodass der Client einen Startserver ermitteln kann \(d.h. einen Server, der ausführbare Dateien für ein Setup auf einem neuen Computer bereitstellt\). Der Clientcomputer nutzt möglicherweise die Gelegenheit, um eine IP-Adresse abzurufen \(dies ist das erwartete Verhalten\), was jedoch nicht erforderlich ist.  

 Die zweite Phase dieses Protokolls findet zwischen dem Clientcomputer und einem Startserver statt und verwendet das DHCP-Meldungsformat als praktisches Kommunikationsformat. Ansonsten hat diese zweite Phase keinen Bezug zu den Standard-DHCP-Diensten. Auf den nächsten Seiten werden die Schritte des Prozesses während der PXE-Clientcomputerinitialisierung beschrieben.  

 Weitere Informationen zur Problembehandlung beim PXE-Start bei im Legacy- oder gemischten Modus ausgeführten Windows-Bereitstellungsdiensten finden Sie im Microsoft-Support-Artikel [Description of PXE Interaction Among PXE Client, DHCP, and RIS Server (Beschreibung der PXE-Interaktion zwischen PXE-Client, DHCP und RIS-Server)](http://support.microsoft.com/kb/244036).  

 Prüfen Sie die folgenden Lösungen zur Behebung von Problemen beim PXE-Start:  

-   Deaktivieren Sie die Windows PE-Protokollierung in „SetupAPI.log“, wie dies unter [Deaktivieren der Windows PE-Protokollierung in Windows-Bereitstellungsdiensten](#DisableWindowsPELogginginWindowsDeploymentServices) beschrieben wird.  

-   Stellen Sie sicher, dass DHCP ordnungsgemäß konfiguriert ist, wie dies unter [Sicherstellen einer ordnungsgemäßen DHCP-Konfiguration](#EnsuretheProperDHCPConfiguration) beschrieben wird.  

-   Verbessern Sie die Antwortzeiten für die Zuweisung von IP-Adressen für PXE-Clientcomputer, wie dies unter [Verbessern der Antwortzeit für die PXE-IP-Adresszuweisung](#ImprovePXEIPAddressAssignmentResponseTime) beschrieben wird.  

#####  <a name="DisableWindowsPELogginginWindowsDeploymentServices"></a> Deaktivieren der Windows PE-Protokollierung in Windows-Bereitstellungsdiensten  
 Das erste empfohlene Verfahren besteht darin sicherzustellen, dass die Protokollierung in „setupapi.log“ deaktiviert wurde.  

#####  <a name="EnsuretheProperDHCPConfiguration"></a> Sicherstellen einer ordnungsgemäßen DHCP-Konfiguration  
 Je nach den verwendeten Routermodellen unterstützt die konkrete Routerkonfiguration der DHCP-Broadcastweiterleitung entweder ein Subnetz \(bzw. eine Routerschnittstelle\) oder einen bestimmten Host. Wenn es sich bei den DHCP-Servern und dem Computer, auf dem Windows-Bereitstellungsdienste ausgeführt werden, um unterschiedliche Computer handelt, müssen Sie sicherstellen, dass die Router, die DHCP-Broadcasts weiterleiten, so konzipiert sind, dass die DHCP- und die Windows-Bereitstellungsdienste-Server die Client-Broadcasts erhalten. Ansonsten erhält der Clientcomputer keine Antwort auf seine Remotestartanforderung.  

 Gibt es einen Router zwischen dem Clientcomputer und dem Remoteinstallationsserver, der die DHCP\-basierten Anforderungen oder Antworten nicht durchlässt? Wenn sich der Windows-Bereitstellungsdienste-Clientcomputer und der Windows-Bereitstellungsdiensteserver in separaten Subnetzen befinden, konfigurieren Sie den Router zwischen den beiden Systemen so, dass DHCP-Pakete an den Windows-Bereitstellungsdiensteserver weitergeleitet werden. Diese Anordnung ist notwendig, da die Windows-Bereitstellungsdienste-Clientcomputer einen Windows-Bereitstellungsdiensteserver ermitteln, indem sie eine DHCP-Broadcastnachricht verwenden. Wenn auf einem Router keine DHCP-Weiterleitung eingerichtet ist, erreichen die DHCP-Broadcasts der Clientcomputer nicht die Windows-Bereitstellungsdiensteserver. Dieser DHCP-Weiterleitungsprozess wird manchmal in Handbüchern zur Routerkonfiguration als *DHCP-Proxy* oder *IP-Hilfsprogrammadresse* bezeichnet. Lesen Sie die Routeranweisungen durch, um weitere Informationen für das Einrichten der DHCP-Weiterleitung auf einem bestimmten Router zu erhalten.  

#####  <a name="ImprovePXEIPAddressAssignmentResponseTime"></a> Verbessern der Antwortzeit für die PXE-IP-Adresszuweisung  
 Überprüfen Sie die folgenden Elemente, wenn es lange \(15 bis 20 Sekunden\) dauert, bis der PXE-Clientcomputer eine IP-Adresse abruft:  

-   Sind der Netzwerkadapter auf dem Zielcomputer und der Switch bzw. Router auf die gleiche Geschwindigkeit eingestellt \(Automatisch, Duplex, Voll usw.\)?  

-   Befindet sich die IP-Adresse für den Windows-Bereitstellungsdiensteserver in der IP-Hilfsprogrammdatei auf dem Router, über den die Verbindung hergestellt wird? Wenn die Liste der IP-Adressen in der IP-Hilfsprogrammdatei lang ist, können Sie die Adresse für den Windows-Bereitstellungsdiensteserver weiter nach oben verschieben.  

### <a name="restarting-the-deployment-process"></a>Neustarten des Bereitstellungsprozesses  
 **Problem:** Beim Testen und bei der Problembehandlung einer neuen oder geänderten Tasksequenz müssen Sie möglicherweise den Zielcomputer neu starten, sodass der Bereitstellungsprozess von vorn beginnen kann. Es können unerwartete Ergebnisse auftreten, da MDT seinen Fortschritt nachverfolgt, indem es Daten auf die Festplatte schreibt. Bei jedem Neustart des Zielcomputers fährt MDT an der Stelle fort, an der es beim vorherigen Neustart abgebrochen wurde.  

 **Mögliche Lösung:** Damit der Bereitstellungsprozess nochmals von Anfang an gestartet wird, löschen Sie vor dem Neustart des Zielcomputers die Ordner C:\\MININT und C:\\\_SMSTaskSequence.  

### <a name="sysprep"></a>Sysprep  
 Überprüfen Sie Probleme und Lösungen, die Sysprep betreffen:  

-   Der Zielcomputer wird nicht in der richtigen AD DS-Organisationseinheit angezeigt, wie dies unter [Computerkonto befindet sich in falscher Organisationseinheit](#ComputerAccountisintheWrongOU) beschrieben wird.  

####  <a name="ComputerAccountisintheWrongOU"></a> Computerkonto befindet sich in falscher Organisationseinheit  
 **Problem:** Der Zielcomputer wurde ordnungsgemäß zur Domäne hinzugefügt, das Computerkonto befindet sich jedoch in der falschen Organisationseinheit.  

 **Erste mögliche Lösung:** Wenn bereits ein Konto für den Zielcomputer vorhanden ist, verbleibt das Konto in der ursprünglichen Organisationseinheit. Um das Konto in die angegebene Organisationseinheit zu verschieben, fügen Sie einen Tasksequenzschritt hinzu, der ein Automatisierungstool wie Microsoft Visual Basic® Scripting Edition verwendet, um das Konto zu verschieben.  

 **Mögliche Lösung 2:** Stellen Sie sicher, dass die angegebene Organisationseinheit das richtige Format aufweist und vorhanden ist. Das richtige Format für die Organisationseinheit lautet `OU=Reception,OU=NYC,DC=Woodgrovebank,DC=com`.  

### <a name="configuration-manager"></a>Configuration Manager  
 **Problem:** Die in REF \_Ref308174600 \\h Abbildung 3 gezeigte Fehlermeldung wird ausgegeben, wenn Sie versuchen, mithilfe der Option **Selbst signiertes PXE-Zertifikat erstellen** einen Configuration Manager-PXE-Dienstpunkt zu erstellen.  

 ![ProblembehandlungReferenz3](media/TroubleshootingReference3.jpg "ProblembehandlungReferenz3")  
Abbildung  SEQ Abbildung \\ \* ARABISCH 3. PXE-Dienstpunktfehler  

 **Abbildung  SEQ Abbildung\\\* ARABISCH 3. PXE-Dienstpunktfehler**  

 **Mögliche Lösung:** Wenn sich auf dem von Ihnen konfigurierten Server bereits ein PXE-Dienstpunkt befand, hat der PXE-Dienstpunkt bei der Deinstallation möglicherweise nicht die eigenständig erstellten Zertifikate gelöscht. Löschen Sie den PXE-Zertifikatordner aus C:\\Dokumente und Einstellungen\\*Benutzername*\\Anwendungsdaten\\Microsoft\\Crypto\\RSA, wobei *Benutzername* der Name des Benutzers ist, der die aktuelle Konfiguration vornimmt oder die vorherige Konfiguration vorgenommen hat. Der Assistent für neue Standortrollen in der Configuration Manager-Konsole sollte erfolgreich abgeschlossen werden, nachdem Sie den Ordner gelöscht haben.  

### <a name="task-sequences"></a>Tasksequenzen  
 Überprüfen Sie Probleme und Lösungen, die die Tasksequenz betreffen:  

-   Tasksequenz wird nicht erfolgreich abgeschlossen oder weist ein unvorhersehbares Verhalten auf, wie dies unter [Tasksequenz wird nicht erfolgreich abgeschlossen](#TaskSequenceDoesNotFinishSuccessfully) beschrieben wird.  

-   Tasksequenzen von Originalgeräteherstellern \(OEM\) in LTI werden in Startimages mit der entgegengesetzten Prozessorarchitektur aufgeführt, wie dies unter [OEM-Tasksequenz wird für ein Startimage, das für eine andere Prozessorarchitektur erstellt wurde, fehlerhaft angezeigt](#OEMTaskSequenceIncorrectlyAppearsforBootImage) beschrieben wird.  

-   Der Windows-Bereitstellungs-Assistent zeigt die Fehlermeldung „Bad Task Sequence Item \(Invalid OS GUID\)“ an, wie dies unter [Bad Task Sequence Item (Invalid OS GUID) Message in the Windows Deployment Wizard (Meldung „Fehlerhaftes Tasksequenzelement (Ungültige OS GUID)“ im Windows-Bereitstellungs-Assistenten)](#BadTaskSequenceItem) beschrieben wird.  

-   Beim Konfigurieren des Namens einer Netzwerkverbindung wird die Meldung „Geben Sie einen gültigen Namen für den Netzwerkadapter ein“ angezeigt, wie dies unter [Netzwerkeinstellungen anwenden](#ApplyNetworkSettings) beschrieben wird.  

-   Probleme, die durch eine nicht ordnungsgemäße Konfiguration von „Bei Fehler fortsetzen“-Konfigurationseinstellungen für Tasksequenzschritte verursacht werden, wie dies unter [Verwendung von „Bei Fehler fortsetzen“](#UseContinueonError) beschrieben wird.  

####  <a name="TaskSequenceDoesNotFinishSuccessfully"></a> Tasksequenz wird nicht erfolgreich abgeschlossen  
 **Problem:** Tasksequenz kann nicht erfolgreich abgeschlossen werden oder hat ein unvorhersehbares Verhalten.  

 **Mögliche Lösung:** Der Tasksequenzschritt **Betriebssystem installieren** \(LTI\) bzw. **Betriebssystemimage anwenden** \(UDI und ZTI\) wurde möglicherweise geändert, nachdem der Tasksequenzschritt erstellt wurde. Dies kann zu unvorhersehbaren Ergebnissen führen. Wenn beispielsweise eine Tasksequenz erstellt wurde, um ein 32\-Bit-Windows 8.1-Image bereitzustellen und zu einem späteren Zeitpunkt der Tasksequenzschritt **Betriebssystem installieren** oder **Betriebssystemimage anwenden** dahingehend geändert wurde, dass er auf ein 64\-Bit-Windows 8.1-Image verweist, wird die Tasksequenz möglicherweise nicht erfolgreich ausgeführt.  

 Es wird empfohlen, eine neue Tasksequenz zu erstellen, um ein anderes Betriebssystemimage bereitzustellen.  

####  <a name="OEMTaskSequenceIncorrectlyAppearsforBootImage"></a> OEM-Tasksequenz wird fälschlicherweise für ein Startimage angezeigt, das für eine andere Prozessorarchitektur erstellt wurde  
 **Problem:** Eine Tasksequenz auf Basis einer LTI OEM-Tasksequenzvorlage wird für ein Startimage mit einer anderen Prozessorarchitektur angezeigt. Eine OEM-Tasksequenz, die ein 64\-Bit-Betriebssystem bereitstellt, wird beispielsweise bei einem 32\-Bit-Startimage angezeigt.  

 **Mögliche Lösung:** Dies ist ein erwartetes Verhalten, da OEM-Tasksequenzen in LTI nicht als „plattformspezifisch“ angesehen werden. Sie werden daher unabhängig von der Prozessorarchitektur des Startimages stets aufgelistet.  

####  <a name="BadTaskSequenceItem"></a> Meldung „Ungültiges Tasksequenzelement \(Ungültige OS-GUID\)“ im Windows-Bereitstellungs-Assistenten  
 **Problem:** Wenn der Windows-Bereitstellungs-Assistent ausgeführt wird, zeigt der Assistent die Fehlermeldung „Bad Task Sequence Item \(Invalid OS-GUID\) (Ungültiges Tasksequenzelement (Ungültige OS GUID))“ an. Das Betriebssystem wird in der Datei „OperatingSystem.xml“ aufgelistet, das Betriebssystem wird jedoch nicht in der Deployment Workbench angezeigt.  

 **Mögliche Lösung:** Mit der Originalbetriebssystemquelle sind zwei oder mehr WIM-Dateien verknüpft. Eine SKU, die einer Tasksequenz zugeordnet ist, wird gelöscht. Es sind jedoch noch andere SKUs für die Betriebssystemquelle vorhanden. Wenn die Tasksequenz, die auf die gelöschte SKU verweist, auf der Seite **Tasksequenz für die Ausführung auf diesem Computer auswählen** des Windows-Bereitstellungs-Assistenten ausgewählt wird, wird die Fehlermeldung „Ungültiges Tasksequenzelement \( Ungültige OS-GUID\)“ angezeigt, nachdem Sie auf der Seite des Assistenten auf **Weiter** geklickt haben.  

 Führen Sie zum Beheben dieses Problems eine der folgenden Aufgaben aus:  

-   Entfernen Sie alle SKUs von der Betriebssystemquelle. Der Windows-Bereitstellungs-Assistent verhält sich normal, und die Fehlermeldung wird nicht angezeigt.  

-   Ändern Sie die Tasksequenz, um ein anderes Betriebssystemabbild zu verwenden.  

####  <a name="ApplyNetworkSettings"></a> Anwenden von Netzwerkeinstellungen  
 **Problem:** Beim Konfigurieren des Netzwerkverbindungsnamens in der Deployment Workbench wird ein Überprüfungsfehler mit folgender Meldung angezeigt: „Geben Sie einen gültigen Namen für den Netzwerkadapter ein.“  

 **Mögliche Lösung:** Entfernen Sie alle Leerzeichen und ungültigen Zeichen aus dem angegebenen Verbindungsnamen.  

####  <a name="UseContinueonError"></a> Verwendung von „Bei Fehler fortsetzen“  
 Wenn eine MDT-Tasksequenz so konfiguriert ist, dass sie bei einem Fehler nicht fortgesetzt wird, und diese Tasksequenz einen Fehler zurückgibt, werden alle verbleibenden Tasksequenzen in dieser Tasksequenzgruppe übersprungen. Die verbleibenden Tasksequenzgruppen werden jedoch verarbeitet. Beachten Sie Folgendes:  

 Es wurden zwei Tasksequenzgruppen erstellt, und jede der Gruppen enthält mehrere Tasksequenzschritte:  

-   Gruppe A  

    -   Schritt A  

    -   Schritt B  

-   Gruppe B  

    -   Schritt A  

    -   Schritt B  

 Wenn Gruppe A\\Schritt A so konfiguriert ist, dass bei einem Fehler keine Fortsetzung erfolgt, wird Gruppe A\\Schritt B nicht verarbeitet. Alle Tasksequenzschritte in Gruppe B werden jedoch verarbeitet.  

### <a name="the-user-state-migration-tool"></a>Das Migrationstool für den Benutzerstatus (USMT)  
 Überprüfen Sie Probleme und Lösungen, die das USMT betreffen:  

-   Verknüpfungen, die auf Dokumente verweisen, die in freigegebenen Netzwerkordnern gespeichert sind, können möglicherweise nicht ordnungsgemäß wiederhergestellt werden, wie dies unter [Fehlende Desktopverknüpfungen](#MissingDesktopShortcuts) beschrieben wird.  

####  <a name="MissingDesktopShortcuts"></a> Fehlende Desktopverknüpfungen  
 **Problem:** Bei der Verwendung von USMT zum Migrieren von Benutzerdaten werden Verknüpfungen, die auf Netzwerkdokumente zeigen, möglicherweise nicht wiederhergestellt. Die Verknüpfungen werden beim ScanState erfasst, jedoch beim LoadState nie auf dem Zielcomputer wiederhergestellt.  

 **Mögliche Lösung:** Bearbeiten Sie die Datei „MigUser.xml“, und kommentieren Sie die folgende Zeile aus:  

 Original:  

```  
<include> filter='MigXmlHelper.IgnoreIrrelevantLinks()'>  
```  

 Geändert:  

```  
<include> <!-- filter='MigXmlHelper.IgnoreIrrelevantLinks()'> -->  
```  

### <a name="windows-imaging-format-files"></a>Windows Imaging Format-Dateien  
 Überprüfen Sie Probleme und Lösungen, die WIM betreffen:  

-   LTI- und ZTI-Bereitstellungen schlagen mit WIM-Dateifehlern in der Datei „BDD.log“ fehl, wie dies unter [Beschädigte WIM-Datei](#CorruptWIMFile) beschrieben wird.  

####  <a name="CorruptWIMFile"></a> Beschädigte WIM-Datei  
 **Problem:** Beim Bereitstellen eines Images schlägt die Bereitstellung fehl, und die Datei „BDD.log“ enthält die folgenden Einträge:  

-   ```  
    The image \\Server\Deployment$\Operating Systems\Windows\version1.wim was not applied successfully by ImageX, rc = 2  
    ```  

-   ```  
    LTIApply COMPLETED.  Return Value = 2  
    ```  

-   ```  
    ZTI ERROR - Non-zero return code by LTIApply, rc = 2  
    ```  

 Wenn zur Untersuchung des Problems die WIM-Datei mit ImageX bereitgestellt wird, führt dies zu folgendem Fehler: „Die Daten sind ungültig.“ Die weitere Untersuchung ergibt, dass der Zeitstempel der WIM-Datei viele Jahre vor dem aktuellen Datum liegt. Es ist möglich, dass ein anderer Prozess, z.B. ein Virenscanner, die WIM-Datei offen gehalten hat, nachdem sie zuvor nach Abschluss eines Lese- oder Schreibvorgangs geschlossen wurde.  

 **Mögliche Lösung:** Stellen Sie die WIM-Datei von einem Sicherungsmedium wieder her.  

### <a name="windows-pe"></a>Windows PE  
 Überprüfen Sie Probleme und Lösungen, die Windows PE betreffen:  

-   Der LTI- oder ZTI-Bereitstellungsprozess wird aufgrund von unzureichendem RAM oder Drahtlosnetzwerkadaptern nicht initiiert, wie dies unter [Bereitstellungsprozess nicht initiiert – begrenzter RAM oder Drahtlosnetzwerkadapter](#LimitedRamorWirelessNetworkAdapter) beschrieben wird.  

-   Der LTI- oder ZTI-Bereitstellungsprozess wird wegen fehlender Windows PE-Komponenten nicht initiiert, wie dies unter [Bereitstellungsprozess nicht initiiert – fehlende Komponenten](#MissingComponents) beschrieben wird.  

-   Der LTI- oder ZTI-Bereitstellungsprozess wird wegen fehlender oder falscher Gerätetreiber nicht initiiert, wie dies unter [Bereitstellungsprozess nicht initiiert – fehlende oder falsche Treiber](#MissingorIncorrectDrivers) beschrieben wird.  

####  <a name="LimitedRamorWirelessNetworkAdapter"></a> Bereitstellungsprozess nicht initiiert – begrenzter RAM oder Drahtlosnetzwerkadapter  
 **Problem:** Beim Bereitstellen eines Images auf bestimmten Zielcomputern wird Windows PE gestartet. Es führt **wpeinit** aus, öffnet ein Eingabeaufforderungsfenster, der eigentliche Bereitstellungsprozess wird aber nicht gestartet. Bei der Problembehandlung durch Zuordnen eines Netzlaufwerks vom Zielcomputern wird erkennbar, dass die Netzwerkadaptertreiber nicht geladen werden.  

 **Erste Möglich Lösung:** Der Bereitstellungs-Assistent wird nicht gestartet, weil nicht genügend RAM vorhanden ist. Stellen Sie sicher, dass der Zielcomputer über mindestens 512 MB RAM verfügt und kein freigegebener Videospeicher mehr als 64 MB dieser 512 MB beansprucht.  

 Die Versionen von Windows PE, die von MDT unterstützt werden, können nicht auf einem Zielcomputer ausgeführt werden, der über weniger als 512 MB RAM verfügt.  

 **Mögliche Lösung 2:** Schließen Sie die Drahtlostreiber nicht in das Windows PE-Image ein.  

####  <a name="MissingComponents"></a> Bereitstellungsprozess nicht initiiert – fehlende Komponenten  
 **Problem:** Bei der Problembehandlung einer fehlgeschlagenen Bereitstellung wird bei einer Überprüfung der Datei „BDD.log“ der folgende Eintrag aufgelistet:  

```  
ERROR - Unable to create ADODB.Connection object, impossible to query SQL Server: ActiveX component can't create object (429).  
```  

 **Mögliche Lösung:** Dieser Fehler kann darauf hindeuten, dass das Windows PE-Image nicht mit MDT erstellt wurde. Wenn Sie Configuration Manager verwenden, dürfen Sie keines der vorhandenen Windows PE-Images verwenden, die von Configuration Manager erstellt wurden. Erstellen Sie stattdessen ein Image mit dem Assistenten für das Importieren von Microsoft Bereitstellungstasksequenzen.  

> [!NOTE]
>  Die von Configuration Manager erstellten Windows PE-Images enthalten Komponenten, die Skripting, XML und die Windows-Verwaltungsinstrumentation (WMI) unterstützen. Sie enthalten jedoch keine Komponenten, die Microsoft ActiveX® Data Objects (ADO) unterstützen.  

####  <a name="MissingorIncorrectDrivers"></a> Bereitstellungsprozess nicht initiiert – fehlende oder falsche Treiber  
 **Problem:** Bei der Bereitstellung auf bestimmten Zielcomputern wird Windows PE gestartet. Es führt **wpeinit** aus, öffnet ein Eingabeaufforderungsfenster, der eigentliche Bereitstellungsprozess wird aber nicht gestartet. Bei der Problembehandlung durch Zuordnen eines Netzlaufwerks vom Zielcomputern wird erkennbar, dass die Netzwerkadaptertreiber nicht geladen werden. Eine Prüfung der Datei „SetupAPI.log“ unter *X*:\Windows\System32\Inf ergibt, dass Windows PE Fehler generiert, wenn es den Netzwerkadapter konfiguriert. Einer dieser Fehler besagt, der Treiber sei nicht für diese Plattform vorgesehen. Die Treiber in der Liste **Standardtreiber** wurden in das Image eingefügt.  

 **Mögliche Lösung:** Möglicherweise besteht in Windows PE ein Treiberkonflikt mit einem anderen Treiber. Beim Konfigurieren der Einstellungen für das Windows PE-Image in der Deployment Workbench erstellen Sie eine Windows PE-Treibergruppe, die nur Netzwerkadapter und Speichertreiber enthält. Anschließend konfigurieren Sie die Bereitstellungsfreigabe so, dass nur die Windows PE-Treibergruppe verwendet wird.  

## <a name="deployment-process-flow-charts"></a>Flussdiagramme des Bereitstellungsprozesses  
 Dieser Abschnitt enthält zwei Sätze von MDT-Flussdiagrammen: einen für LTI-Bereitstellungen und einen für ZTI-Bereitstellungen mit Configuration Manager. Jedes Flussdiagramm veranschaulicht die Aufgaben, die bei diesem Bereitstellungstyp ausgeführt werden.  

 Machen Sie sich wie folgt mit den Flussdiagrammen des Bereitstellungsprozesses vertraut:  

-   Prüfen der Flussdiagramme zur LTI-Bereitstellung, wie unter [Flussdiagramme für den LTI-Bereitstellungsprozess](#LTIDeploymentProcessFlowcharts) beschrieben  

-   Prüfen der Flussdiagramme zur ZTI-Bereitstellung, wie unter [Flussdiagramme für den ZTI-Bereitstellungsprozess](#ZTIDevelopmentProcessFlowcharts) beschrieben  

###  <a name="LTIDeploymentProcessFlowcharts"></a> Flussdiagramme für den LTI-Bereitstellungsprozess  
 Flussdiagramme werden für die folgenden Phasen bereitgestellt:  

-   Überprüfung (Abbildung 4)  

-   Zustandserfassung (Abbildung 5 und Abbildung 6)  

-   Vorinstallation (Abbildung 7, Abbildung 8 und Abbildung 9)  

-   Installation (Abbildung 10)  

-   Nachinstallation (Abbildung 11 und Abbildung 12)  

-   Zustandswiederherstellung (Abbildung 13, Abbildung 14, Abbildung 15 und Abbildung 16)  

 ![ProblembehandlungReferenz4](media/TroubleshootingReference4.jpg "ProblembehandlungReferenz4")  
Abbildung 4: Flussdiagramm für die Überprüfungsphase  

 **Abbildung 4. Flussdiagramm für die Überprüfungsphase**  

 ![ProblembehandlungReferenz5](media/TroubleshootingReference5.jpg "ProblembehandlungReferenze5")  
Abbildung 5. Flussdiagramm für die Zustandserfassungsphase (1 von 2)  

 **Abbildung 5. Flussdiagramm für die Zustandserfassungsphase (1 von 2)**  

 ![ProblembehandlungReferenz6](media/TroubleshootingReference6.jpg "ProblembehandlungReferenz6")  
Abbildung 6. Flussdiagramm für die Zustandserfassungsphase (2 von 2)  

 **Abbildung 6. Flussdiagramm für die Zustandserfassungsphase (2 von 2)**  

 ![ProblembehandlungReferenz7](media/TroubleshootingReference7.jpg "ProblembehandlungReferenz7")  
Abbildung 7. Flussdiagramm für die Vorinstallationsphase (1 von 3)  

 **Abbildung 7. Flussdiagramm für die Vorinstallationsphase (1 von 3)**  

 ![ProblembehandlungReferenz8](media/TroubleshootingReference8.jpg "ProblembehandlungReferenz8")  
Abbildung 8. Flussdiagramm für die Vorinstallationsphase (2 von 3)  

 **Abbildung 8. Flussdiagramm für die Vorinstallationsphase (2 von 3)**  

 ![ProblembehandlungReferenz9](media/TroubleshootingReference9.jpg "ProblembehandlungReferenz9")  
Abbildung 9. Flussdiagramm für die Vorinstallationsphase (3 von 3)  

 **Abbildung 9. Flussdiagramm für die Vorinstallationsphase (3 von 3)**  

 ![ProblembehandlungReferenz10](media/TroubleshootingReference10.jpg "ProblembehandlungReferenz10")  
Abbildung 10. Flussdiagramm für die Installationsphase  

 **Abbildung 10. Flussdiagramm für die Installationsphase**  

 ![ProblembehandlungReferenz11](media/TroubleshootingReference11.jpg "ProblembehandlungReferenz11")  
Abbildung 11. Flussdiagramm für die Nachinstallationsphase (1 von 2)  

 **Abbildung 11. Flussdiagramm für die Nachinstallationsphase (1 von 2)**  

 ![ProblembehandlungReferenz12](media/TroubleshootingReference12.jpg "ProblembehandlungReferenz12")  
Abbildung 12 Flussdiagramm für die Nachinstallationsphase (2 von 2)  

 **Abbildung 12. Flussdiagramm für die Nachinstallationsphase (2 von 2)**  

 ![ProblembehandlungReferenz13](media/TroubleshootingReference13.jpg "ProblembehandlungReferenz13")  
Abbildung 13. Flussdiagramm für die Zustandswiederherstellungsphase (1 von 4)  

 **Abbildung 13. Flussdiagramm für die Zustandswiederherstellungsphase (1 von 4)**  

 ![ProblembehandlungReferenz14](media/TroubleshootingReference14.jpg "ProblembehandlungReferenz14")  
Abbildung 14. Flussdiagramm für die Zustandswiederherstellungsphase (2 von 4)  

 **Abbildung 14. Flussdiagramm für die Zustandswiederherstellungsphase (2 von 4)**  

 ![ProblembehandlungReferenz15](media/TroubleshootingReference15.jpg "ProblembehandlungReferenz15")  
Abbildung 15. Flussdiagramm für die Zustandswiederherstellungsphase (3 von 4)  

 **Abbildung 15. Flussdiagramm für die Zustandswiederherstellungsphase (3 von 4)**  

 ![ProblembehandlungReferenz16](media/TroubleshootingReference16.jpg "ProblembehandlungReferenz16")  
Abbildung 16. Flussdiagramm für die Zustandswiederherstellungsphase (4 von 4)  

 **Abbildung 16. Flussdiagramm für die Zustandswiederherstellungsphase (4 von 4)**  

###  <a name="ZTIDevelopmentProcessFlowcharts"></a> Flussdiagramme für den ZTI-Bereitstellungsprozess  
 Flussdiagramme stehen für die folgenden Phasen der ZTI-Bereitstellung mit Configuration Manager zur Verfügung:  

-   Initialisierung (Abbildung 17)  

-   Überprüfung (Abbildung 18)  

-   Zustandserfassung (Abbildung 19)  

-   Vorinstallation (Abbildung 20)  

-   Installation (Abbildung 21)  

-   Nachinstallation (Abbildung 22)  

-   Zustandswiederherstellung (Abbildung 23 und Abbildung 24)  

-   Erfassung (Abbildung 25)  

 ![ProblembehandlungReferenz17](media/TroubleshootingReference17.jpg "ProblembehandlungReferenz17")  
Abbildung 17. Flussdiagramm für die Initialisierungsphase  

 **Abbildung 17. Flussdiagramm für die Initialisierungsphase**  

 ![ProblembehandlungReferenz18](media/TroubleshootingReference18.jpg "ProblembehandlungReferenz18")  
Abbildung 18. Flussdiagramm für die Überprüfungsphase  

 **Abbildung 18. Flussdiagramm für die Überprüfungsphase**  

 ![ProblembehandlungReferenz19](media/TroubleshootingReference19.jpg "ProblembehandlungReferenz19")  
Abbildung 19. Flussdiagramm für die Zustandserfassungsphase  

 **Abbildung 19. Flussdiagramm für die Zustandserfassungsphase**  

 ![ProblembehandlungReferenz20](media/TroubleshootingReference20.jpg "ProblembehandlungReferenz20")  
Abbildung 20. Flussdiagramm für die Vorinstallationsphase  

 **Abbildung 20. Flussdiagramm für die Vorinstallationsphase**  

 ![ProblembehandlungReferenz21](media/TroubleshootingReference21.jpg "ProblembehandlungReferenz21")  
Abbildung 21. Flussdiagramm für die Installationsphase  

 **Abbildung 21. Flussdiagramm für die Installationsphase**  

 ![ProblembehandlungReferenz22](media/TroubleshootingReference22.jpg "ProblembehandlungReferenz22")  
Abbildung 22. Flussdiagramm für die Nachinstallationsphase  

 **Abbildung 22. Flussdiagramm für die Nachinstallationsphase**  

 ![ProblembehandlungReferenz23](media/TroubleshootingReference23.jpg "ProblembehandlungReferenz23")  
Abbildung 23. Flussdiagramm für die Zustandswiederherstellungsphase (1 von 2)  

 **Abbildung 23. Flussdiagramm für die Zustandswiederherstellungsphase (1 von 2)**  

 ![ProblembehandlungReferenz24](media/TroubleshootingReference24.jpg "ProblembehandlungReferenz24")  
Abbildung 24. Flussdiagramm für die Zustandswiederherstellungsphase (2 von 2)  

 **Abbildung 24. Flussdiagramm für die Zustandswiederherstellungsphase (2 von 2)**  

 ![ProblembehandlungReferenz25](media/TroubleshootingReference25.jpg "ProblembehandlungReferenz25")  
Abbildung 25. Flussdiagramm für die Erfassungsphase  

 **Abbildung 25. Flussdiagramm für die Erfassungsphase**  

## <a name="finding-additional-help"></a>Finden zusätzlicher Hilfe  
 Sie können wie folgt zusätzliche Hilfe für die Problembehandlung bei der MDT-Bereitstellung finden:  

-   Wenden Sie sich an den Microsoft-Support, wie unter [Microsoft-Support](#MicrosoftSupport) beschrieben  

-   Beziehen Sie zusätzliche Unterstützung über Blogs und andere Ressourcen im Internet, wie unter [Internetunterstützung](#InternetSupport) beschrieben  

###  <a name="MicrosoftSupport"></a> Microsoft-Support  
 Microsoft bietet für das Microsoft Deployment Toolkit Support auf Premier- und Professional-Ebene.  

 Professioneller Support: [http://support.microsoft.com/](http://support.microsoft.com/)  

 Support auf Premier-Ebene: [https://premier.microsoft.com/](https://premier.microsoft.com/)  

> [!NOTE]
>  Geben Sie bei der Kontaktaufnahme mit dem Support nicht nur an, dass es sich um ein Problem mit MDT handelt, sondern nennen Sie auch die jeweilige Version.  

###  <a name="InternetSupport"></a> Internetunterstützung  
 Viele Onlinequellen bieten zusätzliche Unterstützung für die Problembehandlung bei MDT, die über den Inhalt dieser Referenz hinausgeht. Zu diesen Onlinequellen gehören:  

-   Von Microsoft gehostete Blogs  

    -   [MDT-Teamblog](http://blogs.technet.com/b/msdeployment/)  

    -   [Teamblog zu Configuration Manager](http://blogs.technet.com/b/configmgrteam/)  

    -   [Blog von Michael Niehaus](http://blogs.technet.com/b/mniehaus/) (Michael Niehaus schreibt zur Windows- und Microsoft Office-Bereitstellung.)  

-   Von Microsoft gehostete Newsgroups und Foren:  

     Die folgenden Newsgroups und Foren stehen zur Verfügung und bieten Unterstützung von Microsoft-Mitarbeitern, Kollegen aus der Branche und Microsoft Valued Professionals:  

    -   [Configuration Manager – Betriebssystembereitstellung](http://social.technet.microsoft.com/Forums/home?forum=configmanagerosd)  

    -   [Windows 8-Installation, Setup und Bereitstellung](http://social.technet.microsoft.com/Forums/windows/home?forum=w8itproinstall)  

-   Informationsquellen zur Bereitstellung außerhalb von Microsoft:  

    -   [DeployVista.com](http://www.deployvista.com/)  

    -   [myITforum.com](http://www.myitforum.com/)
