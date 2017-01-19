---
title: Clientinstallationseigenschaften | Microsoft-Dokumentation
description: Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: 15
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: fa6a613bb2b69be923917399da6b45f0c5cfcc6f

---
# <a name="about-client-installation-properties-in-system-center-configuration-manager"></a>Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie den Befehl „CCMSetup.exe“ von System Center Configuration Manager, um die Configuration Manager-Clientsoftware auf Computern in Ihrem Unternehmen zu installieren.  

##  <a name="a-nameaboutccmsetupa-about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> Informationen zu „CCMSetup.exe“  
 Mit dem Befehl „CCMSetup.exe“ werden alle Dateien, die zum Abschließen der Clientinstallation erforderlich sind, vom angegebenen Verwaltungspunkt oder Quellspeicherort heruntergeladen. Dazu zählen unter anderem folgende Dateien:  

-   Windows Installer-Paket zur Installation der Configuration Manager-Clientsoftware  

-   BITS-Installationsdateien (Background Intelligent Transfer Service, intelligenter Hintergrundübertragungsdienst) von Microsoft bei Bedarf  

-   Windows Installer-Installationsdateien bei Bedarf  

-   Updates und Korrekturen für den Configuration Manager-Client bei Bedarf  

> [!NOTE]  
>  In Configuration Manager können Sie die Datei client.msi nicht direkt ausführen.  

 Die Datei CCMSetup.exe enthält mehrere Befehlszeileneigenschaften, mit denen das Installationsverhalten angepasst werden kann. Zusätzlich können Sie auch Eigenschaften angeben, um das Verhalten von Client.msi mithilfe der Befehlszeile CCMSetup.exe zu ändern.  

> [!IMPORTANT]  
>  Sie müssen alle erforderlichen CCMSetup-Eigenschaften angeben, bevor Sie die Eigenschaften für Client.msi angeben.  

 Die Datei CCMSetup.exe und die unterstützenden Dateien befinden sich auf dem -Standortserver im Ordner **Client** des Configuration Manager-Installationsordners. Dieser Ordner ist im Netzwerk unter **&lt;Standortservername\>\SMS_&lt;Standortcode\>\Client** freigegeben.  

 Bei der Eingabeaufforderung wird vom Befehl CCMSetup.exe das folgende Format verwendet:  

 **CCMSetup.exe [&lt;Ccmsetup-Eigenschaften\>] [&lt;client.msi-Setupeigenschaften>]**  

 Beispiel:  

 **CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01**  

 Mit diesem Beispielbefehl werden die folgenden Aktionen ausgeführt:  

-   Gibt den Verwaltungspunkt mit dem Namen SMSMP01 an, um eine Liste mit Verteilungspunkten zum Herunterladen der Quelldateien für die Clientinstallation anzufordern.  

-   Hiermit wird angegeben, dass die Installation beendet werden soll, wenn bereits eine Version des Configuration Manager-Client auf dem Computer vorhanden ist.  

-   Weist „client.msi“ an, den Client dem Standortcode „S01“ zuzuweisen.  

-   Weist „client.msi“ an, den Fallbackstatuspunkt „SMSFP01“ zu verwenden.  

> [!NOTE]  
>  Wenn die Eigenschaft Leerzeichen aufweist, setzen Sie sie in Anführungszeichen ("").  

 Die in der folgenden Tabelle beschriebenen Eigenschaften sind zum Ändern des Installationsverhaltens von „CCMSetup.exe“ verfügbar.  

> [!IMPORTANT]  
>  Wenn Sie das Active Directory-Schema für Configuration Manager erweitert haben, werden viele Clientinstallationseigenschaften in den Active Directory-Domänendiensten veröffentlicht und automatisch vom Configuration Manager-Client gelesen. Eine Liste der in den Active Directory-Domänendiensten veröffentlichten Clientinstallationseigenschaften finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager, die in Active Directory-Domänendiensten veröffentlicht wurden](about-client-installation-properties-published-to-active-directory-domain-services.md).  

##  <a name="a-namebkmkccmsetupcommandlinea-ccmsetupexe-command-line-properties"></a><a name="BKMK_CCMSetupCommandLine"></a> Befehlszeileneigenschaften der Datei „CCMSetup.exe“  

### <a name=""></a>/?  

Hiermit wird das Dialogfeld **CCMSetup** geöffnet, in dem Befehlszeileneigenschaften für "ccmsetup.exe" angezeigt werden.  

Beispiel: **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;Pfad\>  

 Hiermit wird der Speicherort angegeben, von dem die Installationsdateien heruntergeladen werden sollen. Sie können einen lokalen oder UNC-Installationspfad verwenden. Die Dateien werden mithilfe des SMB-Protokolls (Server Message Block) heruntergeladen.  

> [!NOTE]  
>  Sie können die Eigenschaft **/source** mehrmals in der Befehlszeile verwenden, um alternative Speicherorte zum Herunterladen der Installationsdateien anzugeben.  

> [!IMPORTANT]  
>  Die Befehlszeileneigenschaft **/source** kann nur verwendet werden, wenn dem Windows-Benutzerkonto, das für die Clientinstallation verwendet wird, die Berechtigung "Lesen" für den Installationsspeicherort erteilt wurde.  

 Beispiel: **ccmsetup.exe /source:"\\\Computer\Ordner"**  

### <a name="mpltcomputer"></a>/mp:&lt;Computer\>

 Gibt einen Quellverwaltungspunkt an, mit dem Computer eine Verbindung herstellen können, um den nächsten Verteilungspunkt zum Herunterladen der Dateien für die Clientinstallation zu ermitteln. Wenn keine Verteilungspunkte vorhanden sind oder Computer die Dateien auch nach Ablauf von vier Stunden nicht von den Verteilungspunkten herunterladen können, werden die Dateien von den Clients vom angegebenen Verwaltungspunkt heruntergeladen.  

 Computer laden die Dateien je nach Standortsystemrollen-Konfiguration für Clientverbindungen über eine HTTP- oder eine HTTPS-Verbindung herunter. Beim Herunterladen wird die BITS-Einschränkung verwendet, sofern sie konfiguriert ist. Wenn alle Verteilungspunkte und Verwaltungspunkte ausschließlich für HTTPS-Clientverbindungen konfiguriert sind, müssen Sie sicherstellen, dass für den Clientcomputer ein gültiges PKI-Clientzertifikat (Public Key Infrastructure) verfügbar ist.  

> [!NOTE]  
>  Sie können die Befehlszeileneigenschaft **/mp** verwenden, um mehrere Verwaltungspunkte anzugeben, damit Computer bei einem Fehler bei der ersten Verbindungsherstellung den nächsten Verwaltungspunkt verwenden können usw. Wenn Sie mehrere Verwaltungspunkte angeben, trennen Sie die Werte durch Semikolons.  

> [!IMPORTANT]  
>  Diese Eigenschaft wird nur zum Angeben eines ersten Verwaltungspunkts verwendet, damit die nächste Quelle zum Herunterladen der Clientinstallationsdateien ermittelt werden kann. Sie dient nicht zur Angabe des Verwaltungspunkts, dem der Client nach der Installation zugewiesen wird. Sie können einen beliebigen Configuration Manager-Verwaltungspunkt an einem beliebigen Standort angeben, um für Computer eine Liste mit Verteilungspunkten bereitzustellen, von denen diese die Clientinstallationsdateien herunterladen können.  

 Beispiel für die Verwendung des Computernamens: **ccmsetup.exe /mp:SMSMP01**  

 Beispiel für die Verwendung des vollqualifizierten Domänennamens: **ccmsetup.exe /mp:smsmp01.contoso.com**  

> [!TIP]  
>  Wenn der Client per HTTPS eine Verbindung zum Verwaltungspunkt herstellt, müssen Sie für diese Option anstelle des Computernamens in der Regel den vollqualifizierten Domänennamen (FQDN) angeben. Der angegebene Wert muss in den Antragstellernamen oder alternativen Antragstellernamen des PKI-Zertifikats für den Verwaltungspunkt eingefügt werden. Obwohl Configuration Manager als bewährte Sicherheitsmethode einen Computernamen für Verbindungen im Intranet nur in diesem PKI-Zertifikat unterstützt, wird die Verwendung eines vollqualifizierten Domänennamens empfohlen.  

### <a name="retryltminutes"></a>/retry:&lt;Minuten\>

Hiermit wird das Wiederholungsintervall angegeben für den Fall, dass die Installationsdateien nicht von CCMSetup.exe heruntergeladen werden können. Der Standardwert beträgt **10** Minuten. Der Vorgang wird von CCMSetup wiederholt, bis die in der Installationseigenschaft **downloadtimeout** angegebene Grenze erreicht ist.  

Beispiel: **ccmsetup.exe /retry:20**  

### <a name="noservice"></a>/noservice

Verhindert, dass CCMSetup als Dienst ausgeführt wird. Wenn CCMSetup als Dienst ausgeführt wird, erfolgt die Ausführung im Kontext des lokalen Systemkontos des Computers, das möglicherweise nicht über ausreichende Rechte für den Zugriff auf die für den Installationsvorgang erforderlichen Netzwerkressourcen verfügt. Wenn Sie die Option **/noservice** angeben, wird "CCMSetup.exe" im Kontext des Benutzerkontos ausgeführt, das Sie zum Starten des Installationsvorgangs verwenden. Wenn Sie zum Ausführen von "CCMSetup.exe" mit der Eigenschaft **/service** ein Skript verwenden, wird "CCMSetup.exe" nach dem Starten des Diensts beendet. In diesem Fall werden die Installationsdetails möglicherweise nicht ordnungsgemäß gemeldet, weil der CCMSetup-Dienst die Clientinstallation ausführt. Wenn diese Befehlszeileneigenschaft nicht angegeben wird, wird standardmäßig **/service** verwendet.  

Beispiel: **ccmsetup.exe /noservice**  

### <a name="service"></a>/service

Hiermit wird angegeben, dass CCMSetup mithilfe des lokalen Systemkontos als Dienst ausgeführt werden soll.  

Beispiel: **ccmsetup.exe /service**  

### <a name="uninstall"></a>/uninstall

Hiermit wird angegeben, dass die Configuration Manager-Clientsoftware deinstalliert werden soll. Weitere Informationen finden Sie unter [How to manage clients in System Center Configuration Manager](../manage/manage-clients.md).  

Beispiel: **ccmsetup.exe /uninstall**  

### <a name="logon"></a>/logon

Hiermit wird angegeben, dass die Clientinstallation beendet werden soll, wenn bereits eine Version des Configuration Manager- oder Configuration Manager-Clients installiert ist.  

Beispiel: **ccmsetup.exe /logon**  

### <a name="forcereboot"></a>/forcereboot

 Hiermit wird angegeben, dass ein Neustart des Clientcomputers erzwungen werden soll, wenn dies zum Abschließen der Clientinstallation erforderlich ist. Wenn diese Option nicht angegeben und ein Neustart erforderlich ist, wird CCMSetup beendet und nach dem nächsten manuellen Neustart fortgesetzt.  

 Beispiel: **CCMSetup.exe /forcereboot**  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;Priorität\>

 Hiermit wird die Downloadpriorität beim Herunterladen von Clientinstallationsdateien über eine HTTP-Verbindung angegeben. Es sind folgende Werte möglich:  

-   FOREGROUND (Vordergrund)  

-   HIGH (Hoch)  

-   NORMAL (Mittel)  

-   LOW (Niedrig)  

 Der Standardwert ist NORMAL.  

 Beispiel: **ccmsetup.exe /BITSPriority:HIGH**  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;Minuten\>

Hiermit wird die Zeitspanne in Minuten angegeben, in der versucht wird, die Clientinstallationsdateien herunterzuladen, bevor der Vorgang abgebrochen wird. Der Standardwert beträgt **1440** Minuten (1 Tag).  

Beispiel: **ccmsetup.exe /downloadtimeout:100**  

### <a name="usepkicert"></a>/UsePKICert

 Wenn diese Option angegeben ist, wird vom Client ein PKI-Zertifikat einschließlich Clientauthentifizierung verwendet, sofern vorhanden. Wird kein gültiges Zertifikat gefunden, wird vom Client auf eine HTTP-Verbindung ausgewichen, und ein selbstsigniertes Zertifikat wird verwendet. Wenn diese Option nicht angegeben ist, wird vom Client ein selbstsigniertes Zertifikat verwendet, und die gesamte Kommunikation mit Standortsystemen erfolgt über HTTP.  

> [!NOTE]  
>  In einigen Szenarien muss diese Eigenschaft bei der Clientinstallation für die Verwendung eines PKI-Zertifikats nicht angegeben werden. Dazu gehören die Installation eines Clients mithilfe von Clientpushinstallation sowie die Installation eines Clients mithilfe eines Softwareupdatepunkts. Sie müssen diese Eigenschaft jedoch immer angeben, wenn Sie einen Client manuell installieren und die Eigenschaft **/mp** verwenden, um einen Verwaltungspunkt anzugeben, der ausschließlich für Clientverbindungen über HTTPS konfiguriert ist. Dies gilt auch beim Installieren eines Clients mit dem Kommunikationsstatus Nur Internet mithilfe der Eigenschaft CCMALWAYSINF=1 (zusammen mit den Eigenschaften des internetbasierten Verwaltungspunkts sowie dem Standortcode). Weitere Informationen zur internetbasierten Clientverwaltung finden Sie unter [Überlegungen zur Clientkommunikation aus dem Internet oder aus einer nicht vertrauenswürdigen Gesamtstruktur](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in [Datenübertragungen zwischen Endpunkten in System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Beispiel: **CCMSetup.exe /UsePKICert**  

### <a name="nocrlcheck"></a>/NoCRLCheck

 Hiermit wird angegeben, dass die Überprüfung der Zertifikatsperrlisten von einem Client nicht ausgeführt werden soll, wenn die Kommunikation über HTTPS unter Verwendung eines PKI-Zertifikats erfolgt.  

 Wenn diese Option nicht angegeben ist, wird die Zertifikatsperrliste vom Client geprüft, bevor eine Verbindung über HTTPS unter Verwendung von PKI-Zertifikaten hergestellt wird.  

 Weitere Informationen zur Überprüfung der Zertifikatsperrlisten finden Sie unter [Planning for PKI certificate revocation](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs) in[Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Beispiel: **CCMSetup.exe /UsePKICert /NoCRLCheck**  

### <a name="configltconfiguration-file"></a>/config:&lt;Konfigurationsdatei\>

Gibt den Namen der Textdatei mit den Clientinstallationseigenschaften an. Diese Datei muss sich im Ordner „CCMSetup“ befinden, es sei denn, Sie geben auch die CCMSetup-Eigenschaft **/noservice** an. Der Ordner befindet sich bei 32-Bit-Betriebssystemen und 64-Bit-Betriebssystemen unter „%Windir%\\Ccmsetup“. Wenn Sie die Eigenschaft **/noservice** angeben, muss sich diese Datei in dem Ordner befinden, von dem aus Sie "CCMSetup.exe" ausführen.  

Beispiel: **CCMSetup.exe /config:&lt;Konfigurationsdateiname.txt\>**  

Das richtige Format für die Datei entnehmen Sie bitte der Datei „mobileclienttemplate.tcf“, die sich auf dem Standortservercomputer im &lt;Verzeichnis Configuration Manager\>\\bin\\&lt;Plattform\> befindet. Diese Datei enthält auch Informationen in Kommentarform zu den Abschnitten und deren Verwendung. Geben Sie die Clientinstallationseigenschaften im Abschnitt [Client Install] nach folgendem Text ein: **Install=INSTALL=ALL**.  

Beispiel für einen Abschnitteintrag [Client Install]: **Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100**  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;Dateiname\>

 Hiermit wird angegeben, dass das angegebene erforderliche Programm von „CCMSetup.exe“ nicht installiert werden darf, wenn der Configuration Manager-Client installiert wird.  

 Beispiele: **CCMSetup.exe /skipprereq:silverlight.exe** oder **CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;Silverlight.exe**  

> [!NOTE]  
>  Diese Eigenschaft unterstützt die Eingabe mehrerer Werte. Verwenden Sie zum Trennen der Werte jeweils ein Semikolon (;).  

### <a name="forceinstall"></a>/forceinstall

 Gibt an, dass alle vorhandenen Clients deinstalliert werden und dann ein neuer Client installiert wird.  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;Funktion\>

Hiermit wird festgelegt, dass die angegebene Funktion bei der Configuration Manager-Clientinstallation von „CCMSetup.exe“ nicht installiert wird.  

Beispiel: **CCMSetup.exe /ExcludeFeatures:ClientUI** installiert das Softwarecenter nicht auf dem Client.  

> [!NOTE]  
>  In dieser Version ist **ClientUI** die einzige Option, die für die Eigenschaft **/ExcludeFeatures** unterstützt wird.  

##  <a name="a-nameccmsetupreturncodesa-ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a> Rückgabecodes von „CCMSetup.exe“  
 Nach Ausführung des Befehls „CCMSetup.exe“ werden die im Folgenden aufgeführten Rückgabecodes ausgegeben. Wenn Sie Probleme im Zusammenhang mit dem Befehl beheben müssen, informieren Sie sich in der Datei „ccmsetup.log“ auf dem Clientcomputer über den jeweiligen Kontext und weitere Details wie z. B. die Rückgabecodes.  

|Rückgabecode|Bedeutung|  
|-----------------|-------------|  
|0|Erfolgreich|  
|6|Fehler|  
|7|Neustart erforderlich|  
|8|Setup wird bereits ausgeführt|  
|9|Fehler beim Auswerten der Voraussetzungen|  
|10|Fehler beim Überprüfen des Hashs für das Setup-Manifest|  

##  <a name="a-nameclientmsipropsa-clientmsi-properties"></a><a name="clientMsiProps"></a> Eigenschaften der Datei „Client.msi“  
 Mit den folgenden Eigenschaften können Sie das Installationsverhalten von „client.msi“ ändern. Wenn Sie die Clientpushinstallationsmethode verwenden, können Sie außerdem die Eigenschaften im Dialogfeld **Eigenschaften von Clientpushinstallation** auf der Registerkarte **Client** angeben.  

### <a name="ccmadmins"></a>CCMADMINS  

Gibt eine oder mehrere Windows-Benutzerkonten oder -Gruppen an, denen der Zugriff auf die Clienteinstellungen und -richtlinien erlaubt werden soll. Dies ist nützlich, wenn der Configuration Manager-Administrator über keine lokalen Administratoranmeldeinformationen auf dem Clientcomputer verfügt. Sie können eine Reihe von Konten angeben, die Sie durch Semikolons trennen.  

Beispiel: **CCMSetup.exe CCMADMINS="Domäne\Konto1;Domäne\Konto1"**  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Hiermit wird angegeben, dass ggf. ein Neustart des Computers nach der Clientinstallation zulässig ist.  

> [!IMPORTANT]  
>  Der Computer führt den Neustart ohne vorherige Warnung aus, auch wenn ein Benutzer angemeldet ist.  

Beispiel: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 Legen Sie 1 fest, um anzugeben, dass der Client immer internetbasiert ist und keine Verbindung mit dem Intranet herstellt. Der angezeigte Clientverbindungstyp lautet **Immer Internet**.  

 Verwenden Sie diese Eigenschaft in Verbindung mit der Eigenschaft CCMHOSTNAME, die den FQDN des internetbasierten Verwaltungspunkts angibt. Sie sollte auch in Verbindung mit der CCMSetup-Eigenschaft /UsePKICert und mit dem Standortcode verwendet werden.  

 Weitere Informationen zur internetbasierten Clientverwaltung finden Sie unter [Überlegungen zur Clientkommunikation aus dem Internet oder aus einer nicht vertrauenswürdigen Gesamtstruktur](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in [Datenübertragungen zwischen Endpunkten in System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Beispiel: **CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC**  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Hiermit wird die Liste der Zertifikataussteller angegeben. Dies ist eine Liste von Zertifikaten vertrauenswürdiger Zertifizierungsstellen (CA), denen vom Configuration Manager-Standort vertraut wird.  

 Weitere Informationen zur Liste der Zertifikataussteller und deren Verwendung durch Clients beim Zertifikatauswahlvorgang finden Sie unter [Planning for PKI client certificate selection](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Bei dieser Suche nach Übereinstimmungen für Antragstellerattribute im Stamm-Zertifizierungsstellenzertifikat wird die Groß-/Kleinschreibung beachtet. Attribute können durch ein Komma (,) oder ein Semikolon (;) getrennt werden. Mehrere Stamm-Zertifizierungsstellenzertifikate können mithilfe einer Trennlinie angegeben werden. Beispiel:  

 **CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &amp;#124; CN=Litware Corporate Root CA; O=Litware, Inc.”**  

> [!TIP]  
>  Verweisen Sie auf die Datei „mobileclient.tcf“ im &lt;Configuration Manager-Verzeichnis\>\bin\\&lt;Plattform\> auf dem Standortservercomputer, um den für den Standort konfigurierten Eintrag **CertificateIssuers=&lt;Zeichenfolge\>** zu kopieren.  

### <a name="ccmcertsel"></a>CCMCERTSEL

 Hiermit werden die Zertifikatauswahlkriterien angegeben, wenn der Client mehr als ein Zertifikat aufweist, das für die HTTPS-Kommunikation verwendet werden kann (ein gültiges Zertifikat mit Clientauthentifizierungsfunktionen).  

 Sie können in den Feldern "Antragstellername" oder "Alternativer Antragstellername" nach einer genauen Übereinstimmung (verwenden Sie **Subject:**:) oder nach einer teilweisen Übereinstimmung suchen (verwenden Sie **SubjectStr:)**. Beispiele:  

 **CCMCERTSEL="Subject:computer1.contoso.com"** sucht nach einem Zertifikat, das im Antragstellernamen oder im alternativen Antragstellernamen genau mit dem Computernamen „computer1.contoso.com“ übereinstimmt.  

 **CCMCERTSEL="SubjectStr:contoso.com"** sucht nach einem Zertifikat, das im Antragstellernamen oder alternativen Antragstellernamen „contoso.com“ aufweist.  

 Sie können für die Attribute „Antragstellername“ und „Alternativer Antragstellername“ auch Objekt-IDs (OIDs) oder einen definierten Namen verwenden. Beispiel:  

 Mit**CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"** wird nach dem Attribut von Organisationseinheiten gesucht, das als Objekt-ID angegeben wird und „Computers“ heißt.  

 **CCMCERTSEL="SubjectAttr:OU = Computers"** sucht nach dem Organisationseinheitenattribut, das als definierter Name angegeben wird und „Computers“ heißt.  

> [!IMPORTANT]  
>  Wenn Sie das Feld Antragstellername verwenden, wird die Groß-/Kleinschreibung bei der Suche nach Übereinstimmungen beachtet, wenn Sie das Auswahlkriterium **Subject:** angeben, nicht jedoch, wenn Sie das Auswahlkriterium **SubjectStr:** angeben.  
>   
>  Wenn Sie das Feld „Alternativer Antragstellername“ verwenden, wird bei der Suche nach Übereinstimmungen für beide Auswahlkriterien ( **Subject:** und **SubjectStr:** ) zwischen Groß-/Kleinschreibung unterschieden.  

 Eine vollständige Liste der Attribute, die für die Zertifikatauswahl verwendet werden können, finden Sie unter [Unterstützte Attributwerte für die PKI-Zertifikatauswahlkriterien](#BKMK_attributevalues).  

 Wenn mehrere Zertifikate mit der Suche übereinstimmen und die Eigenschaft CCMFIRSTCERT auf 1 festgelegt ist, wird das PKI-Zertifikat mit der längsten Gültigkeitsdauer vom Client ausgewählt.  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 Hiermit wird ein alternativer Zertifikatsspeichername angegeben, wenn das Clientzertifikat, das für die HTTPS-Kommunikation verwendet werden soll, nicht im Standardzertifikatspeicher **Persönlich** im Computerspeicher gespeichert ist.  

 Beispiel: **CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"**  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  Aktiviert die Debugprotokollierung. Die Werte können auf  0 (deaktiviert) oder 1 (aktiviert) festgelegt werden. Der Standardwert lautet 0. Hierdurch protokolliert der Client Basisinformationen, die für die Fehlerbehandlung bei Problemen nützlich sein können. Zur Vermeidung einer zu umfangreichen Protokollierung, durch die es schwierig werden kann, relevante Informationen in den Protokolldateien finden, sollte diese Eigenschaft an Produktionsstandorten möglichst nicht verwendet werden. CCMENABLELOGGING muss auf TRUE festgelegt sein, damit die Debugprotokollierung aktiviert wird.  

  Beispiel: **CCMSetup.exe CCMDEBUGLOGGING=1**  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  Aktiviert die Protokollierung, wenn die Eigenschaft auf TRUE festgelegt ist. Standardmäßig ist die Protokollierung aktiviert. Die Protokolldateien werden im Configuration Manager-Clientinstallationsorder im Ordner **Logs** gespeichert. Standardmäßig ist dies der Ordner %Windir%\CCM\Logs.  

  Beispiel: **CCMSetup.exe CCMENABLELOGGING=TRUE**  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 Hiermit wird die Ausführungshäufigkeit des Tools zur Clientintegritätsauswertung (ccmeval.exe) angegeben. Sie können einen Wert zwischen **1** und **1440** Minuten angeben. Wenn Sie diese Eigenschaft nicht angeben oder einen ungültigen Wert angeben, wird die Auswertung einmal täglich ausgeführt.  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 Hiermit wird der Ausführungszeitpunkt des Tools zur Clientintegritätsauswertung (ccmeval.exe) in Stunden angegeben. Sie können einen Wert zwischen **0** Uhr (Mitternacht) und **23** Uhr angeben. Wenn Sie diese Eigenschaft nicht angeben oder einen ungültigen Wert angeben, wird die Auswertung um Mitternacht ausgeführt.  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 Wenn für diese Eigenschaft der Wert 1 festgelegt ist, wird vom Client das PKI-Zertifikat mit der längsten Gültigkeitsdauer ausgewählt. Diese Einstellung ist möglicherweise erforderlich, wenn Sie Netzwerkzugriffsschutz mit IPsec-Erzwingung verwenden.  

 Beispiel: **CCMSetup.exe /UsePKICert CCMFIRSTCERT=1**  

### <a name="ccmhostname"></a>CCMHOSTNAME

 Gibt den FQDN des internetbasierten Verwaltungspunkts an, wenn der Client über das Internet verwaltet wird.  

 Geben Sie diese Option nicht mit der Installationseigenschaft „SMSSITECODE=AUTO“ an. Internetbasierte Clients müssen direkt ihrem internetbasierten Standort zugewiesen werden.  

 Beispiel: **CCMSetup.exe  /UsePKICert/ CCMHOSTNAME="SMSMP01.corp.contoso.com"**  

### <a name="ccmhttpport"></a>CCMHTTPPORT

 Hiermit wird der Port angegeben, der vom Client für die Kommunikation mit den Standortsystemservern über HTTP verwendet werden soll.  

 Wenn kein Port angegeben ist, wird der Standardwert 80 verwendet.  

 Beispiel: **CCMSetup.exe CCMHTTPPORT=80**  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Hiermit wird der Port angegeben, der vom Client für die Kommunikation mit den Standortsystemservern über HTTPS verwendet werden soll. Wenn kein Port angegeben ist, wird der Standardwert 443 verwendet.  

Beispiel: **CCMSetup.exe /UsePKICert CCMHTTPSPORT=443**  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Hiermit wird der Ordner identifiziert, in dem die Configuration Manager-Clientdateien installiert sind. Wenn diese Eigenschaft nicht festgelegt ist, wird die Clientsoftware im Ordner *%Windir%*\CCM installiert. Unabhängig vom Installationsort dieser Dateien wird die Datei "Ccmcore.dll" immer im Ordner *%Windir%\System32* installiert. Bei 64-Bit-Betriebssystemen wird außerdem immer eine Kopie der Datei „Ccmcore.dll“ im Ordner *%Windir%*\SysWOW64 installiert, um 32-Bit-Anwendungen zu unterstützen, von denen die 32-Bit-Version der Configuration Manager-Client-APIs aus dem Configuration Manager-Software Developer Kit (SDK) verwendet wird.  

 Beispiel: **CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"**  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Gibt die Anzahl der Details an, die in die Configuration Manager-Protokolldateien geschrieben werden. Geben Sie eine ganze Zahl zwischen 0 und 3 an, wobei 0 für die ausführlichste Protokollierung und 3 für die reine Fehlerprotokollierung steht. Der Standardwert lautet 1.  

Beispiel: **CCMSetup.exe CCMLOGLEVEL=3**  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Wenn eine Configuration Manager-Protokolldatei die Größe von 250000 Bytes erreicht (oder den Wert, der von der Eigenschaft CCMLOGMAXSIZE angegeben wird), wird sie als Sicherungsdatei umbenannt, und eine neue Protokolldatei wird erstellt.  

Diese Eigenschaft gibt an, wie viele vorherige Versionen der Protokolldatei beibehalten werden sollen. Der Standardwert lautet 1. Wird der Wert auf 0 festgelegt, werden keine alten Protokolldateien beibehalten.  

Beispiel: **CCMSetup.exe CCMLOGMAXHISTORY=0**  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Gibt die maximale Protokolldateigröße in Bytes an. Wenn ein Protokoll die angegebene Größe erreicht, wird es als Verlaufsdatei umbenannt, und eine neue Datei wird erstellt. Diese Eigenschaft muss auf mindestens 10000 Bytes festgelegt werden. Der Standardwert beträgt 250000 Bytes.  

Beispiel: **CCMSetup.exe CCMLOGMAXSIZE=300000**  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 Wenn diese Eigenschaft auf TRUE festgelegt ist, wird verhindert, dass Endbenutzer mit Administratoranmeldeinformationen auf dem Clientcomputer den für den Configuration Manager-Client zugewiesenen Standort mithilfe von Configuration Manager in der Systemsteuerung des Clientcomputers ändern können.  

 Beispiel: **CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Wenn für diese Eigenschaft der Wert TRUE festgelegt wurde, können Endbenutzer, die über Administratoranmeldeinformationen auf dem Clientcomputer verfügen, die Einstellungen des Clientcacheordners für den Configuration Manager-Client nicht mithilfe von Configuration Manager in der Systemsteuerung des Clientcomputers ändern.  

Beispiel: **CCMSetup.exe DISABLECACHEOPT=TRUE**  

### <a name="dnssuffix"></a>DNSSUFFIX

 Hiermit wird die DNS-Domäne angegeben, über die Clients Verwaltungspunkten finden können, die in DNS veröffentlicht wurden. Nachdem ein Verwaltungspunkt gefunden wurde, wird der Client über andere Verwaltungspunkte in der Hierarchie informiert. Dies heißt, dass der Verwaltungspunkt, der mittels der DNS-Veröffentlichung gefunden wird, nicht am Standort des Clients vorliegen muss, sondern dass jeder beliebige Verwaltungspunkt in der Hierarchie in Frage kommt.  

> [!NOTE]  
>  Sie müssen diese Eigenschaft nicht angeben, wenn der Client der gleichen Domäne angehört wie ein veröffentlichter Verwaltungspunkt. In diesem Fall wird die Clientdomäne automatisch verwendet, um DNS nach Verwaltungspunkten zu durchsuchen.  

 Weitere Informationen zur DNS-Veröffentlichung als Dienstidentifizierungsmethode für Configuration Manager-Clients finden Sie unter [Service Location and how clients determine their assigned management point (Dienstidentifizierung und wie Clients den ihnen zugewiesenen Verwaltungspunkt ermitteln)](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) in [Understand how clients find site resources and services for System Center Configuration Manager (Verstehen, wie Clients Standortressourcen und -dienste für System Center Configuration Manager suchen)](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

> [!NOTE]  
>  Die DNS-Veröffentlichung ist in Configuration Manager standardmäßig nicht aktiviert.  

 Beispiel: **CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com**  

### <a name="fsp"></a>FSP

Gibt den Fallbackstatuspunkt an, von dem die von Configuration Manager-Clientcomputern gesendeten Zustandsmeldungen empfangen und verarbeitet werden.  

Weitere Informationen zum Fallbackstatuspunkt, finden Sie unter [Bestimmen, ob ein Fallbackstatuspunkt erforderlich ist](plan/determine-the-site-system-roles-for-clients.md#BKMK_Determine_FSP) im Artikel [Ermitteln der Standortsystemrollen für System Center Configuration Manager-Clients](plan/determine-the-site-system-roles-for-clients.md).  

Beispiel: **CCMSetup.exe FSP=SMSFP01**  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 Hiermit wird angegeben, dass vor der Clientinstallation nicht geprüft wird, ob die minimal erforderliche Version von Microsoft Application Virtualization (App-V) vorhanden ist.  

> [!IMPORTANT]  
>  Wenn Sie den Configuration Manager-Client installieren, ohne App-V zu installieren, können Sie keine virtuellen Anwendungen bereitstellen.  

 Beispiel: **CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE**  

### <a name="notifyonly"></a>NOTIFYONLY

Gibt an, dass der Clientstatus gemeldet wird, jedoch keine Probleme behoben werden, die für den Configuration Manager-Client auftreten.  

Beispiel: **CCMSetup.exe NOTIFYONLY=TRUE**  

Weitere Informationen finden Sie unter [Konfigurieren des Clientstatus in System Center Configuration Manager](configure-client-status.md).  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 Wenn ein Configuration Manager-Client den falschen vertrauenswürdigen Configuration Manager-Stammschlüssel aufweist und keine Verbindung mit dem vertrauenswürdigen Verwaltungspunkt herstellen kann, um eine gültige Kopie des neuen vertrauenswürdigen Stammschlüssels abzurufen, müssen Sie den alten vertrauenswürdigen Stammschlüssel manuell mithilfe dieser Eigenschaft entfernen. Diese Situation tritt häufig auf, wenn Sie einen Client in eine andere Standorthierarchie verschieben. Diese Eigenschaft gilt für Clients, von denen HTTP- und HTTPS-Clientkommunikation verwendet wird.  

 Beispiel: **CCMSetup.exe RESETKEYINFORMATION=TRUE**  

### <a name="sitereassign"></a>SITEREASSIGN

Ermöglicht eine automatische Standortneuzuordnung für Clientupgrades bei Verwendung mit [SMSSITECODE](#smssitecode)=AUTO.

Beispiel: **CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE**

### <a name="smscachedir"></a>SMSCACHEDIR

Hiermit wird der Speicherort des Clientcacheordners angegeben, in dem temporäre Dateien auf dem Clientcomputer gespeichert werden. Standardmäßig ist dies der Speicherort *%Windir \ccmcache*.  

Beispiel: **CCMSetup.exe SMSCACHEDIR="C:\Temp"**  

Diese Eigenschaft kann in Verbindung mit der Eigenschaft SMSCACHEFLAGS verwendet werden, um den Speicherort des Clientcacheordners genauer zu steuern.  

Beispiel: Mit **CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE** wird der Clientcacheordner auf dem größten verfügbaren Laufwerk des Clients installiert.  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Hiermit wird der Configuration Manager-Cacheordner konfiguriert, in dem temporäre Dateien gespeichert werden. Sie können die SMSCACHEFLAGS-Eigenschaften einzeln oder zusammen durch Kommas getrennt verwenden. Wenn diese Eigenschaft nicht angegeben wird, wird der Clientcacheordner der Eigenschaft SMSCACHEDIR entsprechend installiert und nicht komprimiert, und der Wert der Eigenschaft SMSCACHESIZE wird als Größe des Ordners in MB verwendet.  

Hiermit werden weitere Installationsdetails für den Clientcacheordner angegeben. Die folgenden Eigenschaften können angegeben werden:  

-   PERCENTDISKSPACE: Gibt die Ordnergröße als Prozentsatz des gesamten Speicherplatzes an. Wenn Sie diese Eigenschaft angeben, müssen Sie auch die Eigenschaft SMSCACHESIZE als Prozentwert angeben.  

-   PERCENTFREEDISKSPACE: Gibt die Ordnergröße als Prozentsatz des freien Speicherplatzes an. Wenn Sie diese Eigenschaft angeben, müssen Sie auch die Eigenschaft SMSCACHESIZE als Prozentwert angeben. Wenn der Datenträger z. B. über 10 MB freien Speicherplatz verfügt und für SMSCACHESIZE 50 angegeben ist, wird die Ordnergröße auf 5 MB festgelegt. Diese Eigenschaft kann nicht in Verbindung mit der Eigenschaft PERCENTDISKSPACE verwendet werden.  

-   MAXDRIVE: Gibt an, dass der Ordner auf dem größten verfügbaren Datenträger installiert werden soll. Dieser Wert wird ignoriert, wenn ein Pfad mit der Eigenschaft SMSCACHEDIR angegeben wurde.  

-   MAXDRIVESPACE: Gibt an, dass der Ordner auf dem Laufwerk mit dem meisten verfügbaren Speicherplatz installiert werden soll. Dieser Wert wird ignoriert, wenn ein Pfad mit der Eigenschaft SMSCACHEDIR angegeben wurde.  

-   NTFSONLY: Gibt an, dass der Ordner nur auf Laufwerken installiert werden kann, die mit NTFS formatiert sind. Dieser Wert wird ignoriert, wenn ein Pfad mit der Eigenschaft SMSCACHEDIR angegeben wurde.  

-   COMPRESS: Gibt an, dass der Ordner komprimiert gespeichert werden soll.  

-   FAILIFNOSPACE: Gibt an, dass die Clientsoftware entfernt werden soll, wenn ausreichend Speicherplatz zum Installieren des Ordners verfügbar ist.  

> [!NOTE]  
>  Für diese Eigenschaft können mehrere Eigenschaften angegeben werden, indem diese mit einem Strichpunkt getrennt eingegeben werden.  

Wenn diese Eigenschaft nicht angegeben wird, wird der Clientcacheordner der Eigenschaft SMSCACHEDIR entsprechend erstellt und nicht komprimiert, und seine Größe entspricht dem für die Eigenschaft SMSCACHESIZE angegebenen Wert.  

Beispiel: **CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS**  

> [!NOTE]  
>  Diese Einstellung wird ignoriert, wenn ein Upgrade eines vorhandenen Clients ausgeführt wird.  

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> In Configuration Manager Version 1606 sind neue Clienteinstellungen für die Angabe der Größe des Clientcacheordners verfügbar. Das Hinzufügen dieser Clienteinstellungen ersetzt SMSCACHESIZE als client.msi-Eigenschaft, um die Größe des Clientcaches anzugeben. Weitere Informationen zu den Clienteinstellungen finden Sie unter [client settings for cache size](about-client-settings.md#client-cache-settings) (Clienteinstellungen für Cachegröße).  

Wenn diese Eigenschaft für 1602 und früher in Verbindung mit der Eigenschaft PERCENTDISKSPACE oder PERCENTFREEDISKSPACE verwendet wird, gibt SMSCACHESIZE hiermit die Größe des Clientcacheordners in Megabyte (MB) oder als Prozentsatz an. Wenn diese Eigenschaft nicht festgelegt ist, wird für den Ordner standardmäßig die maximale Größe von 5120 MB verwendet. Der niedrigste Wert, den Sie angeben können, beträgt 1 MB.  

> [!NOTE]  
>  Wenn für den Download eines neuen Pakets die maximale Ordnergröße überschritten würde, der Ordnerinhalt jedoch nicht zur Freigabe von Speicherplatz geleert werden kann, wird der Downloadvorgang abgebrochen, und das Programm bzw. die Anwendung kann nicht ausgeführt werden.  

Diese Einstellung wird ignoriert, wenn ein Upgrade eines vorhandenen Clients ausgeführt wird und wenn Softwareupdates vom Client heruntergeladen werden.  

Beispiel: **CCMSetup.exe SMSCACHESIZE=100**  

> [!NOTE]  
>  Wenn Sie einen Client neu installieren, können Sie die Installationseigenschaften SMSCACHESIZE und SMSCACHEFLAGS nicht verwenden, um die Cachegröße auf einen niedrigeren Wert als vorher festzulegen. Wenn Sie dies versuchen, wird der Wert ignoriert und die Cachegröße automatisch auf die letzte Größe festgelegt.  
>   
>  Wenn Sie den Client z. B. mit der standardmäßigen Cachegröße von 5120 MB installieren und den Client dann mit einer Cachegröße von 100 MB neu installieren, wird die Cacheordnergröße auf dem neu installierten Client auf 5120 MB festgelegt.  


### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Gibt den zu überprüfenden Speicherort und die Reihenfolge an, die das Configuration Manager-Installationsprogramm für die Überprüfung der Konfigurationseinstellungen verwendet. Bei der Eigenschaft handelt es sich um eine Zeichenfolge aus einem oder mehreren Zeichen, die jeweils eine spezielle Konfigurationsquelle angibt. Verwenden Sie die Zeichenwerte R, P, M und U wie in den folgenden Beispielen allein oder zusammen:  

-   R: Überprüfung der Konfigurationseinstellungen in der Registrierung.  

   Weitere Informationen finden Sie unter [Informationen zum Speichern von Clientinstallationseigenschaften in der Registrierung](https://technet.microsoft.com/library/gg712298.aspx#BKMK_Provision).  

-   P: Überprüfung der Konfigurationseinstellungen in den Installationseigenschaften an der Eingabeaufforderung  

-   M: Überprüfung der vorhandenen Einstellungen beim Aktualisieren eines älteren Clients mit der Configuration Manager-Clientsoftware  

-   U: Upgrade des installierten Clients auf eine neuere Version (unter Verwendung des zugewiesenen Standortcodes)  

 Bei der Clientinstallation wird standardmäßig `PU` verwendet, um zuerst die Installationseinstellungen und dann die vorhandenen Einstellungen zu überprüfen.  

 Beispiel: **CCMSetup.exe SMSCONFIGSOURCE=RP**  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 Hiermit wird angegeben, ob Windows Internet Name Service (WINS) vom Client verwendet werden kann, um einen Verwaltungspunkt zu finden, von dem HTTP-Verbindungen zugelassen werden. Diese Methode wird von den Clients verwendet, wenn kein Verwaltungspunkt in den Active Directory-Domänendiensten oder in DNS gefunden werden kann.  

 Diese Eigenschaft ist unabhängig davon, ob vom Client WINS für die Namensauflösung verwendet wird.  

 Sie können zwei verschiedene Modi für diese Eigenschaft konfigurieren:  

-   NOWINS: Dies ist die sicherste Einstellung für diese Eigenschaft. Es wird verhindert, dass von Clients ein Verwaltungspunkt in WINS gefunden wird.  Wenn Sie diese Einstellung verwenden, ist eine alternative Methode für die Clients erforderlich, mit der ein Verwaltungspunkt im Intranet gefunden werden kann, beispielsweise Active Directory-Domänendienste oder DNS-Veröffentlichung.  

-   WINSSECURE: In diesem Modus kann WINS von einem Client, von dem HTTP-Kommunikation verwendet wird, zum Finden eines Verwaltungspunkts verwendet werden. Für den Client ist jedoch eine Kopie des vertrauenswürdigen Stammschlüssels erforderlich, bevor eine Verbindung mit dem Verwaltungspunkt hergestellt werden kann. Weitere Informationen finden Sie unter [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Wenn diese Eigenschaft nicht angegeben ist, wird der Standardwert WINSSECURE verwendet.  

 Beispiel: **CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS**  

### <a name="smsmp"></a>SMSMP

Hiermit wird ein erster Verwaltungspunkt für die Verwendung durch den Configuration Manager-Client angegeben.  

> [!IMPORTANT]  
>  Wenn vom Verwaltungspunkt nur Clientverbindungen über HTTPS akzeptiert werden (keine HTTP-Clientverbindungen), müssen Sie dem Namen des Verwaltungspunkts das Präfix „https://“ voranstellen.  

Beispiel: **CCMSetup.exe SMSMP=smsmp01.contoso.com**  

Beispiel: **CCMSetup.exe SMSMP=smsmp01.contoso.com**  

Beispiel: **CCMSetup.exe SMSMP=https://smsmp01.contoso.com**  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Hiermit wird der vertrauenswürdige Configuration Manager-Stammschlüssel angegeben für den Fall, dass dieser nicht aus den Active Directory-Domänendiensten abgerufen werden kann. Diese Eigenschaft gilt für Clients, von denen HTTP- und HTTPS-Clientkommunikation verwendet wird. Weitere Informationen finden Sie unter [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Beispiel: **CCMSetup.exe SMSPUBLICROOTKEY=&lt;Schlüssel\>**  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Diese Eigenschaft wird verwendet, um den vertrauenswürdigen Configuration Manager-Stammschlüssel neu zu installieren. Hiermit werden der vollständige Pfad und der Dateiname einer Datei mit dem vertrauenswürdigen Stammschlüssel angegeben. Diese Eigenschaft gilt für Clients, von denen HTTP- und HTTPS-Clientkommunikation verwendet wird. Weitere Informationen finden Sie unter [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Beispiel: CCMSetup.exe **SMSROOTKEYPATH=&lt;Vollständiger Pfad und Dateiname\>**  

### <a name="smssigncert"></a>SMSSIGNCERT

 Hiermit werden der vollständige Pfad und der CER-Dateiname des exportierten selbstsignierten Zertifikats auf dem Standortserver angegeben.  

 Dieses Zertifikat ist im **SMS** -Zertifikatspeicher unter dem Antragstellernamen **Standortserver** und dem Anzeigenamen **Signaturzertifikat des Standortservers**gespeichert.  

 Beispiel: **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;Vollständiger Pfad und Dateiname\>**  

### <a name="smssitecode"></a>SMSSITECODE

 Gibt den Configuration Manager-Standort an, um diesem den Configuration Manager-Client zuzuweisen. Dies kann entweder ein dreistelliger Standortcode oder das Wort AUTO sein. Wenn AUTO angegeben ist oder diese Eigenschaft nicht angegeben ist, wird vom Client versucht, die Configuration Manager-Standortzuweisung anhand der Active Directory-Domänendienste oder eines angegebenen Verwaltungspunkts zu bestimmen. Um AUTO für Clientupgrades festzulegen, müssen Sie ferner [SITEREASSIGN](#sitereassign) auf TRUE setzen.    

> [!NOTE]  
>  Verwenden Sie nicht „Automatisch“, wenn Sie auch den internetbasierten Verwaltungspunkt (CCMHOSTNAME) angegeben. In diesen Fällen müssen Sie den Client direkt dem Standort zuweisen.  

 Beispiel: **CCMSetup.exe SMSSITECODE=XZY**  

##  <a name="a-namebkmkattributevaluesa-supported-attribute-values-for-the-pki-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a> Unterstützte Attributwerte für die PKI-Zertifikatauswahlkriterien  
 Configuration Manager unterstützt die folgenden Attributwerte für die PKI-Zertifikatauswahlkriterien:  

|OID-Attribut|DN-Attribut (Distinguished Name)|Attributdefinition|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Domänenkomponente|  
|1.2.840.113549.1.9.1|E oder E-mail|E-Mail-Adresse|  
|2.5.4.3|CN|Allgemeiner Name|  
|2.5.4.4|SN|Antragstellername|  
|2.5.4.5|SERIALNUMBER|Seriennummer|  
|2.5.4.6|C|Ländercode|  
|2.5.4.7|L|Ort|  
|2.5.4.8|S oder ST|Name des Bundeslands bzw. des Kantons|  
|2.5.4.9|STREET|Straße|  
|2.5.4.10|O|Organisationsname|  
|2.5.4.11|OU|Organisationseinheit|  
|2.5.4.12|T oder Title|Titel|  
|2.5.4.42|G oder GN oder GivenName|Vorname|  
|2.5.4.43|I oder Initials|Initialen|  
|2.5.29.17|(kein Wert)|Alternativer Antragstellername|  



<!--HONumber=Dec16_HO3-->


