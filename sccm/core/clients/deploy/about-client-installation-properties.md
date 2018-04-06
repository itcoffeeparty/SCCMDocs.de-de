---
title: Eigenschaften der Clientinstallation
titleSuffix: Configuration Manager
description: Dieser Abschnitt enthält Informationen zu den ccmsetup-Befehlszeileneigenschaften für die Installation des Configuration Manager-Clients.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: 15
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 057b078767a08574a806cb6af1cdb3812148a457
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="about-client-installation-properties-in-system-center-configuration-manager"></a>Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie den Befehl CCMSetup.exe für die Installation des Configuration Manager-Clients. Wenn Sie diese Clientinstallationseigenschaften in der Befehlszeile angeben, wird durch die Eigenschaften das Installationsverhalten geändert.



##  <a name="aboutCCMSetup"></a> Informationen zu „CCMSetup.exe“  
 Der Befehl „CCMSetup.exe“ lädt die Dateien herunter, die zum Installieren des Clients über einen Verwaltungspunkt oder einen Quellspeicherort erforderlich sind. Dazu zählen unter anderem folgende Dateien:  

-   Das Windows Installer-Paket „client.msi“ für die Installation der Clientsoftware.  

-   BITS-Installationsdateien (Background Intelligent Transfer Service, intelligenter Hintergrundübertragungsdienst) von Microsoft  

-   Windows Installer-Installationsdateien  

-   Updates und Korrekturen für den Configuration Manager-Client.  

> [!NOTE]  
>  In Configuration Manager können Sie die Datei „Client.msi“ nicht direkt ausführen.  

 Die Datei CCMSetup.exe enthält mehrere [Befehlszeileneigenschaften](#ccmsetup-exe-command-line-properties), mit denen das Installationsverhalten angepasst werden kann. Sie können auch Eigenschaften angeben, um das Verhalten von „client.msi“ mithilfe der Befehlszeile CCMSetup.exe zu ändern.  

> [!IMPORTANT]  
>  Geben Sie alle erforderlichen CCMSetup-Eigenschaften an, bevor Sie die Eigenschaften für „client.msi“ angeben.  

 Die Datei CCMSetup.exe und die unterstützenden Dateien befinden sich auf dem Standortserver im Ordner **Client** des Configuration Manager-Installationsordners. Dieser Ordner ist im Netzwerk unter **&lt;Standortservername\>\SMS_&lt;Standortcode\>\Client** freigegeben.  

 Bei der Eingabeaufforderung wird vom Befehl CCMSetup.exe das folgende Format verwendet:  

 `CCMSetup.exe [<Ccmsetup properties>] [<client.msi setup properties>]`  

 Zum Beispiel:  

   `CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

 Dieses Beispiel dient zu Folgendem:  

-   Gibt den Verwaltungspunkt mit dem Namen SMSMP01 an, um eine Liste mit Verteilungspunkten zum Herunterladen der Clientinstallationsdateien anzufordern.  

-   Gibt an, dass die Installation beendet wird, wenn bereits eine Version des Clients auf dem Computer vorhanden ist.  

-   Weist „client.msi“ an, den Client dem Standortcode „S01“ zuzuweisen.  

-   Weist „client.msi“ an, den Fallbackstatuspunkt „SMSFP01“ zu verwenden.  

> [!NOTE]  
>  Wenn eine Eigenschaft Leerzeichen enthält, setzen Sie diese zwischen Anführungszeichen.  


> [!IMPORTANT]  
>  Wenn Sie das Active Directory-Schema für Configuration Manager erweitert haben, werden viele Clientinstallationseigenschaften in den Active Directory Domain Services auf der Site veröffentlicht. Der Configuration Manager-Client liest diese Eigenschaften automatisch. Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften, die in Active Directory Domain Services veröffentlicht wurden](about-client-installation-properties-published-to-active-directory-domain-services.md)  



##  <a name="ccmsetupexe-command-line-properties"></a>Befehlszeileneigenschaften der Datei „CCMSetup.exe“  

### <a name=""></a>/?  

Hiermit wird das Dialogfeld **CCMSetup** geöffnet, in dem Befehlszeileneigenschaften für "ccmsetup.exe" angezeigt werden.  

Beispiel: **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;Pfad\>  

 Gibt den Speicherort für den Dateidownload an. Verwenden Sie einen lokalen oder einen UNC-Pfad. Die Dateien werden mithilfe des SMB-Protokolls (Server Message Block) heruntergeladen. Zum Verwenden von **/source** muss das Windows-Benutzerkonto der Clientinstallation über Leseberechtigungen für den Speicherort verfügen.

> [!NOTE]  
>  Sie können die Eigenschaft **/source** mehrmals in der Befehlszeile verwenden, um alternative Downloadspeicherorte anzugeben.  

 Beispiel: **ccmsetup.exe /source:"\\\Computer\Ordner"**  

### <a name="mpltserver"></a>/mp:&lt;Server\>

 Gibt einen Quellenverwaltungspunkt für Computer an, mit denen eine Verbindung hergestellt werden soll. Computer suchen über diesen Verwaltungspunkt nach dem nächstgelegenen Verteilungspunkt für die Installationsdateien. Wenn keine Verteilungspunkte vorhanden sind oder Computer die Dateien auch nach Ablauf von vier Stunden nicht von den Verteilungspunkten herunterladen können, werden die Dateien vom angegebenen Verwaltungspunkt heruntergeladen.  

> [!IMPORTANT]  
>  Mit dieser Eigenschaft wird ein erster Verwaltungspunkt für Computer angegeben, um eine Downloadquelle zu ermitteln. Hierfür kommt jeder Verwaltungspunkt jedes Standorts in Frage. Der Client wird keinem Verwaltungspunkt *zugewiesen*.   

 Computer laden die Dateien je nach Standortsystemrollen-Konfiguration für Clientverbindungen über eine HTTP- oder eine HTTPS-Verbindung herunter. Beim Herunterladen wird die BITS-Einschränkung verwendet, sofern sie konfiguriert ist. Wenn alle Verteilungspunkte und Verwaltungspunkte ausschließlich für HTTPS-Clientverbindungen konfiguriert sind, stellen Sie sicher, dass für den Clientcomputer ein gültiges Clientzertifikat verfügbar ist.  

Sie können mit der Befehlszeileneigenschaft **/mp** mehrere Verwaltungspunkte angeben. Wenn der Computer keine Verbindung mit dem ersten Verwaltungspunkt herstellen kann, versucht er es mit dem nächsten in der Liste angegebenen Verwaltungspunkt. Wenn Sie mehrere Verwaltungspunkte angeben, trennen Sie die Werte durch Semikolons.

Wenn der Client per HTTPS eine Verbindung mit einem Verwaltungspunkt herstellt, müssen Sie anstelle des Computernamens normalerweise den vollqualifizierten Domänennamen (FQDN) angeben. Der Wert muss mit dem Antragstellernamen oder alternativen Antragstellernamen des PKI-Zertifikats für den Verwaltungspunkt übereinstimmen. Obwohl Configuration Manager einen Computernamen im Zertifikat für Verbindungen im Intranet unterstützt, wird als bewährte Sicherheitsmethode die Verwendung eines vollqualifizierten Domänennamens empfohlen.

Beispiel für die Verwendung des Computernamens: `ccmsetup.exe /mp:SMSMP01`  

Beispiel für die Verwendung des vollqualifizierten Domänennamens: `ccmsetup.exe /mp:smsmp01.contoso.com`  

Diese Eigenschaft kann die URL eines Cloudverwaltungsgateways angeben. Verwenden Sie diese URL, um den Client auf einem internetbasierten Gerät zu installieren. Führen Sie die folgenden Schritte aus, um den Wert für diese Eigenschaft abzurufen:
- Erstellen Sie ein Cloudverwaltungsgateway.
- Öffnen Sie auf einem aktiven Client als Administrator eine Windows PowerShell-Eingabeaufforderung. 
- Führen Sie den folgenden Befehl aus: `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
- Fügen Sie das Präfix „https://“ für die Verwendung mit der Eigenschaft **/mp** an.

Beispiel für die Verwendung der Cloudverwaltungsgateway-URL: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > Wenn die URL eines Cloudverwaltungsgateways für die Eigenschaft **/mp** angegeben wird, muss diese mit **https://** beginnen.


### <a name="retryltminutes"></a>/retry:&lt;Minuten\>

Wiederholungsintervall, wenn „CCMSetup.exe“ die Installationsdateien nicht herunterladen kann. Der Vorgang wird von CCMSetup wiederholt, bis die in der Eigenschaft **downloadtimeout** angegebene Grenze erreicht ist.  

Beispiel: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Verhindert, dass CCMSetup als Dienst ausgeführt wird, was das Standardverhalten ist. Wenn CCMSetup als Dienst ausgeführt wird, erfolgt die Ausführung im Kontext des lokalen Systemkontos des Computers. Dieses Konto besitzt möglicherweise nicht ausreichend Rechte für den Zugriff auf die erforderlichen Netzwerkressourcen für die Installation. Mit **/noservice** wird „CCMSetup.exe“ im Kontext des Benutzerkontos ausgeführt, mit dem Sie die Installation starten. Wenn Sie zum Ausführen von „CCMSetup.exe“ mit der Eigenschaft **/service** ein Skript verwenden, wird „CCMSetup.exe“ nach dem Starten des Diensts beendet und meldet die Installationsdetails möglicherweise nicht ordnungsgemäß.   

Beispiel: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Hiermit wird angegeben, dass CCMSetup mithilfe des lokalen Systemkontos als Dienst ausgeführt werden soll.  

Beispiel: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Gibt an, dass die Clientsoftware deinstalliert werden soll. Weitere Informationen finden Sie unter [Verwalten von Clients](../manage/manage-clients.md).  

Beispiel: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Wenn eine Version des Clients bereits installiert wurde, gibt diese Eigenschaft an, dass die Clientinstallation angehalten werden sollte.  

Beispiel: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

 Gibt an, dass CCMSetup einen Neustart des Clientcomputers erzwingen soll, wenn dies zum Abschließen der Installation erforderlich ist. Wenn diese Eigenschaft nicht angegeben ist, wird CCMSetup beendet, wenn ein Neustart erforderlich ist. Nach dem nächsten manuellen Neustart wird CCMSetup fortgesetzt.  

 Beispiel: `CCMSetup.exe /forcereboot`  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;Priorität\>

 Hiermit wird die Downloadpriorität beim Herunterladen von Clientinstallationsdateien über eine HTTP-Verbindung angegeben. Es sind folgende Werte möglich:  

-   FOREGROUND (Vordergrund)  

-   HIGH (Hoch)  

-   NORMAL (Mittel)  

-   LOW (Niedrig)  

 Der Standardwert ist NORMAL.  

 Beispiel: `ccmsetup.exe /BITSPriority:HIGH`  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;Minuten\>

Die Zeitspanne in Minuten, in der CCMSetup versucht, die Installationsdateien herunterzuladen, bevor der Vorgang angehalten wird. Der Standardwert beträgt **1440** Minuten (ein Tag).  

Beispiel: `ccmsetup.exe /downloadtimeout:100`  

### <a name="usepkicert"></a>/UsePKICert

 Wenn diese Option angegeben ist, verwendet der Client ein PKI-Zertifikat mit Clientauthentifizierung, sofern vorhanden. Wenn der Client kein gültiges Zertifikat finden kann, verwendet er eine HTTP-Verbindung mit einem selbstsignierten Zertifikat. Dieses Verhalten ist identisch, wenn Sie diese Eigenschaft nicht verwenden.

> [!NOTE]  
>  In einigen Szenarios müssen Sie diese Eigenschaft nicht angeben, wenn Sie einen Client installieren und dennoch ein Clientzertifikat verwenden. Dazu gehören die Installation eines Clients mithilfe von Clientpushinstallation sowie die Installation eines Clients mithilfe eines Softwareupdatepunkts. Sie müssen diese Eigenschaft jedoch immer angeben, wenn Sie einen Client manuell installieren und die Eigenschaft **/mp** verwenden, um einen Verwaltungspunkt anzugeben, der ausschließlich für Clientverbindungen über HTTPS konfiguriert ist. Diese Eigenschaft muss auch angegeben werden, wenn Sie einen Client für die reine Internetkommunikation installieren. Verwenden sie die Eigenschaft CCMALWAYSINF=1 gemeinsam mit den Eigenschaften für den internetbasierten Verwaltungspunkt und den Standortcode. Weitere Informationen zur internetbasierten Clientverwaltung finden Sie unter [Überlegungen zur Clientkommunikation aus dem Internet oder einer nicht vertrauenswürdigen Gesamtstruktur](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

 Beispiel: `CCMSetup.exe /UsePKICert`  

### <a name="nocrlcheck"></a>/NoCRLCheck

 Gibt an, dass ein Client die Zertifikatssperrlisten nicht überprüfen sollte, wenn dieser über HTTPS unter Verwendung eines PKI-Zertifikats kommuniziert.  

 Wenn diese Option nicht angegeben ist, überprüft der Client die Zertifikatssperrliste, bevor er eine Verbindung über HTTPS herstellt.  

 Weitere Informationen zur Client CRL-Prüfung finden Sie unter [Planen der PKI-Zertifikatsperrung](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

 Beispiel: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="configltconfiguration-file"></a>/config:&lt;Konfigurationsdatei\>

Gibt den Namen einer Textdatei mit den Clientinstallationseigenschaften an.

- Wenn Sie die CCMSetup-Eigenschaft **/noservice** nicht angeben, muss diese Datei im Ordner „CCMSetup“ abgelegt sein, d.h. bei 32-Bit- und 64-Bit-Betriebssystemen unter „%Windir%\\Ccmsetup“.
- Wenn Sie die Eigenschaft **/noservice** angeben, muss sich diese Datei in dem Ordner befinden, von dem aus Sie "CCMSetup.exe" ausführen.  

Beispiel: `CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

Das richtige Dateiformat entnehmen Sie der Datei „mobileclienttemplate.tcf“, die sich auf dem Standortservercomputer im &lt;Configuration Manager-Verzeichnis\>\\bin\\&lt;Plattform\> befindet. Die Datei enthält auch Kommentare zu den Abschnitten und deren Verwendung. Geben Sie die Clientinstallationseigenschaften im Abschnitt [Client Install] nach folgendem Text ein: **Install=INSTALL=ALL**.  

Beispiel für einen Abschnitteintrag [Client Install]: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;Dateiname\>

 Gibt an, dass das angegebene erforderliche Programm von „CCMSetup.exe“ nicht installiert werden darf, wenn der Configuration Manager-Client installiert wird. Diese Eigenschaft unterstützt die Eingabe mehrerer Werte. Verwenden Sie zum Trennen der Werte jeweils ein Semikolon (;).  


 Beispiele: `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe` oder `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`  

### <a name="forceinstall"></a>/forceinstall

 Gibt an, dass „CCMSetup.exe“ einen vorhandenen Client deinstalliert und einen neuen Client installiert.  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;Funktion\>

Gibt an, dass „CCMSetup.exe“ das angegebene Feature nicht installiert, wenn der Client installiert wird.  

Beispiel: `CCMSetup.exe /ExcludeFeatures:ClientUI` installiert das Softwarecenter nicht auf dem Client.  

> [!NOTE]  
>  **ClientUI** ist der einzige Wert, der für die Eigenschaft **/ExcludeFeatures** unterstützt wird.  



##  <a name="ccmsetupReturnCodes"></a> Rückgabecodes von „CCMSetup.exe“  
 Der Befehl „CCMSetup.exe“ gibt die im Folgenden aufgeführten Rückgabecodes aus. Zur Problembehandlung informieren Sie sich in der Datei „ccmsetup.log“ auf dem Clientcomputer über den jeweiligen Kontext und weitere Details zu Rückgabecodes.  

|Rückgabecode|Bedeutung|  
|-----------------|-------------|  
|0|Erfolgreich|  
|6|Fehler|  
|7|Neustart erforderlich|  
|8|Setup wird bereits ausgeführt|  
|9|Fehler beim Auswerten der Voraussetzungen|  
|10|Fehler beim Überprüfen des Hashs für das Setup-Manifest|  



##  <a name="clientMsiProps"></a> Eigenschaften der Datei „Client.msi“  
 Mit den folgenden Eigenschaften können Sie das Installationsverhalten von „client.msi“ ändern. Wenn Sie die Clientpushinstallationsmethode verwenden, können Sie außerdem die Eigenschaften im Dialogfeld **Eigenschaften von Clientpushinstallation** auf der Registerkarte **Client** angeben.  


### <a name="aadclientappid"></a>AADCLIENTAPPID

Gibt den Clientanwendungsbezeichner von Azure Active Directory (Azure AD) an. Die Client-App wird bei der [Konfiguration der Azure-Dienste](/sccm/core/servers/deploy/configure/azure-services-wizard) für die Cloudverwaltung erstellt oder importiert. Ein Azure-Administrator kann den Wert für diese Eigenschaft vom Azure-Portal abrufen. Weitere Informationen finden Sie unter [Abrufen der Anwendungs-ID](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key). Bei der Eigenschaft **AADCLIENTAPPID** ist diese Anwendungs-ID für den Anwendungstyp „Nativ“ bestimmt.

Beispiel: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`


### <a name="aadresourceuri"></a>AADRESOURCEURI

Gibt den Serveranwendungsbezeichner von Azure AD an. Die Server-App wird bei der [Konfiguration der Azure-Dienste](/sccm/core/servers/deploy/configure/azure-services-wizard) für die Cloudverwaltung erstellt oder importiert. Bei der Erstellung der Server-App lautet diese Eigenschaft im Dialogfeld „Serveranwendung erstellen“ **App-ID-URI**.

Ein Azure-Administrator kann den Wert für diese Eigenschaft vom Azure-Portal abrufen. Suchen Sie auf dem Blatt **Azure Active Directory** unter **App-Registrierungen** nach der Server-App. Diese App ist vom Anwendungstyp „Web-App/API“. Öffnen Sie die App, klicken Sie auf **Einstellungen** und anschließend auf **Eigenschaften**. Verwenden Sie den Wert **App-ID-URI** für die Eigenschaft AADRESOURCEURI für die Clientinstallation.

Beispiel: `ccmsetup.exe AADRESOURCEURI=https://contososerver`


### <a name="aadtenantid"></a>AADTENANTID

Gibt die ID des Azure AD-Mandanten an. Dieser Mandant wird bei der [Konfiguration der Azure-Dienste](/sccm/core/servers/deploy/configure/azure-services-wizard) für Cloud Management mit Configuration Manager verknüpft. Führen Sie die folgenden Schritte aus, um den Wert für diese Eigenschaft abzurufen:
- Öffnen Sie auf einem Windows 10-Gerät, das mit demselben Azure AD-Mandanten verknüpft ist, eine Eingabeaufforderung.
- Führen Sie den folgenden Befehl aus: `dsregcmd.exe /status`
- Suchen Sie im Abschnitt „Gerätestatus“ nach dem Wert **TenantId**. Beispiel: `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

 > [!Note]
 > Ein Azure-Administrator kann diesen Wert auch im Azure-Portal abrufen. Weitere Informationen finden Sie unter [Abrufen der Mandanten-ID](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-tenant-id)

Beispiel: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`


### <a name="aadtenantname"></a>AADTENANTNAME

Gibt den Namen des Azure AD-Mandanten an. Dieser Mandant wird bei der [Konfiguration der Azure-Dienste](/sccm/core/servers/deploy/configure/azure-services-wizard) für Cloud Management mit Configuration Manager verknüpft. Führen Sie die folgenden Schritte aus, um den Wert für diese Eigenschaft abzurufen:
- Öffnen Sie auf einem Windows 10-Gerät, das mit demselben Azure AD-Mandanten verknüpft ist, eine Eingabeaufforderung.
- Führen Sie den folgenden Befehl aus: `dsregcmd.exe /status`
- Suchen Sie im Abschnitt „Gerätestatus“ nach dem Wert **TenantName**. Beispiel: `TenantName : Contoso`

Beispiel: `ccmsetup.exe AADTENANTNAME=Contoso`


### <a name="ccmadmins"></a>CCMADMINS  

Gibt eine oder mehrere Windows-Benutzerkonten oder -Gruppen an, denen der Zugriff auf die Clienteinstellungen und -richtlinien erlaubt werden soll. Diese Eigenschaft ist nützlich, wenn der Configuration Manager-Administrator über keine lokalen Administratoranmeldeinformationen auf dem Clientcomputer verfügt. Geben Sie eine Liste von Konten an, die Sie durch Semikolons trennen.  

Beispiel: `CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Gibt an, dass ein Neustart des Computers nach der Clientinstallation bei Bedarf zulässig ist.  

> [!IMPORTANT]  
>  Der Computer führt den Neustart ohne vorherige Warnung aus, auch wenn ein Benutzer angemeldet ist.  

Beispiel: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 Legen Sie **1** fest, um anzugeben, dass der Client immer internetbasiert ist und keine Verbindung mit dem Intranet herstellt. Der angezeigte Clientverbindungstyp lautet **Immer Internet**.  

 Verwenden Sie diese Eigenschaft in Verbindung mit der Eigenschaft CCMHOSTNAME, die den FQDN des internetbasierten Verwaltungspunkts angibt. Verwenden Sie sie zudem mit der Eigenschaft CCMSetup/UsePKICert und mit dem Standortcode.  

 Weitere Informationen zur internetbasierten Clientverwaltung finden Sie unter [Überlegungen zur Clientkommunikation aus dem Internet oder einer nicht vertrauenswürdigen Gesamtstruktur](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

 Beispiel: `CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Hiermit wird die Liste der Zertifikataussteller angegeben. Dies ist eine Liste von Zertifikaten vertrauenswürdiger Zertifizierungsstellen (CA), denen vom Configuration Manager-Standort vertraut wird.  

 Weitere Informationen zur Liste der Zertifikataussteller und deren Verwendung durch Clients beim Zertifikatauswahlvorgang finden Sie unter [Planen der PKI-Clientzertifikatauswahl](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

 Bei dieser Suche nach Übereinstimmungen für Antragstellerattribute im Stamm-Zertifizierungsstellenzertifikat wird die Groß-/Kleinschreibung beachtet. Attribute können durch ein Komma (,) oder ein Semikolon (;) getrennt werden. Mehrere Stamm-Zertifizierungsstellenzertifikate können mithilfe einer Trennlinie angegeben werden. Beispiel:  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  Wenn Sie den für den Standort konfigurierten Eintrag **CertificateIssuers=&lt;Zeichenfolge\>** kopieren möchten, verweisen Sie auf die Datei „mobileclient.tcf“ im Ordner &lt;Configuration Manager-Verzeichnis\>\bin\\&lt;Plattform\> auf dem Standortserver.  

### <a name="ccmcertsel"></a>CCMCERTSEL

 Gibt die Zertifikatauswahlkriterien an, wenn der Client mehrere Zertifikate für die HTTPS-Kommunikation besitzt. Bei diesem Zertifikat handelt es sich um ein gültiges Zertifikat, das die Clientauthentifizierungsfunktionen beinhaltet.  

 Sie können in den Feldern „Antragstellername“ oder „Alternativer Antragstellername“ nach einer genauen Übereinstimmung (verwenden Sie **Subject:**:) oder nach einer teilweisen Übereinstimmung suchen (verwenden Sie **SubjectStr:)**. Beispiele:  

 `CCMCERTSEL="Subject:computer1.contoso.com"` sucht nach einem Zertifikat, das im Antragstellernamen oder im alternativen Antragstellernamen genau mit dem Computernamen „computer1.contoso.com“ übereinstimmt.  

 `CCMCERTSEL="SubjectStr:contoso.com"` sucht nach einem Zertifikat, das im Antragstellernamen oder alternativen Antragstellernamen „contoso.com“ aufweist.  

 Sie können für die Attribute „Antragstellername“ und „Alternativer Antragstellername“ auch Objekt-IDs (OIDs) oder einen definierten Namen verwenden. Beispiel:  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` sucht nach dem Organisationseinheitenattribut, das als Objektbezeichner angegeben wird und „Computers“ heißt.  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` sucht nach dem Organisationseinheitenattribut, das als definierter Name angegeben wird und „Computers“ heißt.  

> [!IMPORTANT]  
>  Wenn Sie das Feld „Antragstellername“ verwenden, muss bei **Subject:** die Groß-/Kleinschreibung beachtet werden, bei **SubjectStr:** dagegen nicht.  
>   
>  Wenn Sie das Feld „Alternativer Antragstellername“ verwenden, spielt die Groß-/Kleinschreibung bei **Subject:** und bei **SubjectStr:** keine Rolle.  

 Eine vollständige Liste der Attribute, die für die Zertifikatauswahl verwendet werden können, finden Sie unter [Unterstützte Attributwerte für die PKI-Zertifikatauswahlkriterien](#BKMK_attributevalues).  

 Wenn mehrere Zertifikate mit der Suche übereinstimmen und die Eigenschaft CCMFIRSTCERT auf 1 festgelegt ist, wird das PKI-Zertifikat mit der längsten Gültigkeitsdauer vom Client ausgewählt.  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 Gibt einen alternativen Zertifikatspeichernamen an, wenn das Clientzertifikat für HTTPS nicht im Standardzertifikatspeicher **Persönlich** im Computerspeicher abgelegt ist.  

 Beispiel: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  Aktiviert die Debugprotokollierung. Die Werte können auf 0 (aus, Standardeinstellung) oder 1 (ein) festgelegt werden. Mit dieser Eigenschaft protokolliert der Client Basisinformationen für die Problembehandlung. Es hat sich als bewährte Methode erwiesen, die Verwendung dieser Eigenschaft an Produktionsstandorten zu vermeiden. Es kann zu einer übermäßigen Protokollierung kommen, wodurch es möglicherweise schwierig wird, die relevanten Informationen in den Protokolldateien zu finden. Zudem muss CCMENABLELOGGING zur Aktivierung der Debugprotokollierung auf TRUE festgelegt sein.  

  Beispiel: `CCMSetup.exe CCMDEBUGLOGGING=1`  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  Diese Eigenschaft ist zur Aktivierung der Protokollierung standardmäßig auf TRUE festgelegt. Die Protokolldateien werden im Configuration Manager-Clientinstallationsorder im Ordner **Logs** gespeichert. Standardmäßig ist dies der Ordner %Windir%\CCM\Logs.  

  Beispiel: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 Die Ausführungshäufigkeit des Tools zur Clientintegritätsauswertung (ccmeval.exe). Ein Wert zwischen **1** und **1440** Minuten ist hier möglich. Standardmäßig wird das Tool einmal täglich ausgeführt.  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 Der Ausführungszeitpunkt des Tools zur Clientintegritätsauswertung (ccmeval.exe) in Stunden, d.h. zwischen **0** (Mitternacht) und **23** (23 Uhr). Standardmäßig wird das Tool um Mitternacht ausgeführt.  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 Wenn für diese Eigenschaft der Wert 1 festgelegt ist, wird vom Client das PKI-Zertifikat mit der längsten Gültigkeitsdauer ausgewählt. Diese Einstellung ist möglicherweise erforderlich, wenn Sie Netzwerkzugriffsschutz mit IPsec-Erzwingung verwenden.  

 Beispiel: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  


### <a name="ccmhostname"></a>CCMHOSTNAME

 Wenn der Client über das Internet verwaltet wird, gibt diese Eigenschaft den FQDN des internetbasierten Verwaltungspunkts an.  

 Geben Sie diese Option nicht mit der Installationseigenschaft SMSSITECODE=AUTO an. Internetbasierte Clients müssen direkt ihrem internetbasierten Standort zugewiesen werden.  

 Beispiel: `CCMSetup.exe  /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

Diese Eigenschaft kann die Adresse eines Cloudverwaltungsgateways angeben. Führen Sie die folgenden Schritte aus, um den Wert für diese Eigenschaft abzurufen:
- Erstellen Sie ein Cloudverwaltungsgateway.
- Öffnen Sie auf einem aktiven Client als Administrator eine Windows PowerShell-Eingabeaufforderung. 
- Führen Sie den folgenden Befehl aus: `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
- Verwenden Sie den zurückgegebenen Wert wie bei der Eigenschaft **CCMHOSTNAME**.

Beispiel: `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > Wenn Sie die Adresse eines Cloudverwaltungsgateways für die Eigenschaft **CCMHOSTNAME** angeben, sollten Sie *kein* Präfix wie **https://** anhängen. Dieses Präfix wird nur mit der URL **/mp** eines Cloudverwaltungsgateways verwendet.



### <a name="ccmhttpport"></a>CCMHTTPPORT

 Hiermit wird der Port angegeben, der vom Client für die Kommunikation mit den Standortsystemservern über HTTP verwendet werden soll. Standardmäßig auf Port 80 festgelegt.  

 Beispiel: `CCMSetup.exe CCMHTTPPORT=80`  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Hiermit wird der Port angegeben, der vom Client für die Kommunikation mit den Standortsystemservern über HTTPS verwendet werden soll. Standardmäßig auf Port 443 festgelegt.  

Beispiel: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Weist den Ordner aus, in dem die Configuration Manager-Clientdateien installiert sind. Standardmäßig ist dies *%Windir%*\CCM. Unabhängig vom Installationsort dieser Dateien wird die Datei „Ccmcore.dll“ stets im Ordner *%Windir%\System32* installiert. Zudem ist auf einem 64-Bit-Betriebssystem im Ordner *%Windir%*\SysWOW64 immer eine Kopie der Datei „Ccmcore.dll“ installiert. Diese Datei unterstützt 32-Bit-Anwendungen, welche die 32-Bit-Version der Client-APIs vom Configuration Manager SDK verwenden.  

 Beispiel: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Gibt die Detailebene für das Schreiben in die Configuration Manager-Protokolldateien an. Geben Sie eine ganze Zahl zwischen 0 und 3 an, wobei 0 für die ausführlichste Protokollierung und 3 für die reine Fehlerprotokollierung steht. Der Standardwert lautet 1.  

Beispiel: `CCMSetup.exe CCMLOGLEVEL=3`  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Wenn eine Configuration Manager-Protokolldatei die maximale Größe erreicht, benennt der Client diese als Sicherungsdatei um und erstellt eine neue Protokolldatei. Die maximale Größe beträgt standardmäßig 250.000 Bytes, der von der Eigenschaft angegebene Wert CCMLOGMAXSIZE.

Diese Eigenschaft gibt an, wie viele vorherige Versionen der Protokolldatei beibehalten werden sollen. Der Standardwert lautet 1. Wird der Wert auf 0 festgelegt, werden keine alten Protokolldateien beibehalten.  

Beispiel: `CCMSetup.exe CCMLOGMAXHISTORY=0`  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Die maximale Protokolldateigröße in Bytes. Wenn ein Protokoll die angegebene Größe erreicht, benennt der Client diese als Verlaufsdatei um und erstellt eine neue Datei. Diese Eigenschaft muss auf mindestens 10.000 Bytes festgelegt werden. Der Standardwert beträgt 250.000 Bytes.  

Beispiel: `CCMSetup.exe CCMLOGMAXSIZE=300000`  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 Wenn diese Eigenschaft auf TRUE festgelegt ist, können Administratoren den zugewiesenen Standort in den Einstellungen von **Configuration Manager** nicht mehr ändern.  

 Beispiel: **CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Wenn diese Eigenschaft auf TRUE festgelegt ist, können Administratoren die Einstellungen für Clientcacheordner in den Einstellungen von **Configuration Manager** nicht mehr ändern.  

Beispiel: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

 Hiermit wird die DNS-Domäne angegeben, über die Clients Verwaltungspunkten finden können, die in DNS veröffentlicht wurden. Nachdem ein Verwaltungspunkt gefunden wurde, wird der Client über andere Verwaltungspunkte in der Hierarchie informiert. Dies bedeutet, dass der Verwaltungspunkt, der mittels der DNS-Veröffentlichung gefunden wird, nicht am Standort des Clients vorliegen muss, sondern dass jeder beliebige Verwaltungspunkt in der Hierarchie in Frage kommt.  

> [!NOTE]  
>  Sie müssen diese Eigenschaft nicht angeben, wenn der Client der gleichen Domäne angehört wie ein veröffentlichter Verwaltungspunkt. In diesem Fall wird die Clientdomäne automatisch verwendet, um DNS nach Verwaltungspunkten zu durchsuchen.  

 Weitere Informationen zur DNS-Veröffentlichung als Dienstidentifizierungsmethode für Configuration Manager-Clients finden Sie unter [Dienstidentifizierung und wie Clients den ihnen zugewiesenen Verwaltungspunkt ermitteln](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

> [!NOTE]  
>  Die DNS-Veröffentlichung ist in Configuration Manager standardmäßig nicht aktiviert.  

 Beispiel: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### <a name="fsp"></a>FSP

Gibt den Fallbackstatuspunkt an, von dem die von Configuration Manager-Clientcomputern gesendeten Zustandsmeldungen empfangen und verarbeitet werden.  

Weitere Informationen zum Fallbackstatuspunkt finden Sie unter [Bestimmen, ob ein Fallbackstatuspunkt erforderlich ist](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point).  

Beispiel: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 Gibt an, dass vor der Clientinstallation nicht geprüft wird, ob die erforderliche Mindestversion von Microsoft Application Virtualization (App-V) vorhanden ist.  

> [!IMPORTANT]  
>  Wenn Sie den Configuration Manager-Client installieren, ohne App-V zu installieren, können Sie keine virtuellen Anwendungen bereitstellen.  

 Beispiel: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### <a name="notifyonly"></a>NOTIFYONLY

Gibt an, dass der Client einen Status meldet, gefundene Probleme jedoch nicht behebt.  

Beispiel: `CCMSetup.exe NOTIFYONLY=TRUE`  

Weitere Informationen finden Sie unter [Konfigurieren des Clientstatus](configure-client-status.md).  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 Wenn ein Client den falschen vertrauenswürdigen Configuration Manager-Stammschlüssel aufweist und keine Verbindung mit dem vertrauenswürdigen Verwaltungspunkt herstellen kann, um eine gültige Kopie des neuen vertrauenswürdigen Stammschlüssels abzurufen, müssen Sie den alten vertrauenswürdigen Stammschlüssel manuell mithilfe dieser Eigenschaft entfernen. Dieser Fall tritt möglicherweise ein, wenn Sie einen Client aus einer Standorthierarchie in eine andere verschieben. Diese Eigenschaft gilt für Clients, von denen HTTP- und HTTPS-Clientkommunikation verwendet wird.  

 Beispiel: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Ermöglicht eine automatische Standortneuzuordnung für Clientupgrades bei Verwendung mit [SMSSITECODE](#smssitecode)=AUTO.

Beispiel: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Hiermit wird der Speicherort des Clientcacheordners angegeben, in dem temporäre Dateien auf dem Clientcomputer gespeichert werden. Der Speicherort lautet standardmäßig *%Windir%\ccmcache*.  

Beispiel: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Diese Eigenschaft kann in Verbindung mit der Eigenschaft SMSCACHEFLAGS verwendet werden, um den Speicherort des Clientcacheordners zu steuern.  

Beispiel: Mit `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` wird der Clientcacheordner auf dem größten verfügbaren Laufwerk des Clients installiert.  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Hiermit werden weitere Installationsdetails für den Clientcacheordner angegeben. Sie können die SMSCACHEFLAGS-Eigenschaften einzeln oder zusammen durch Kommas getrennt verwenden. Wenn diese Eigenschaft nicht angegeben wird, wird der Clientcacheordner der Eigenschaft SMSCACHEDIR entsprechend installiert und nicht komprimiert, und der Wert der Eigenschaft SMSCACHESIZE wird als Größe des Ordners in MB verwendet.  

Diese Einstellung wird ignoriert, wenn ein Upgrade eines vorhandenen Clients ausgeführt wird.  

Eigenschaften:  

-   PERCENTDISKSPACE: Gibt die Ordnergröße als Prozentsatz des gesamten Speicherplatzes an. Wenn Sie diese Eigenschaft angeben, müssen Sie auch die Eigenschaft SMSCACHESIZE als Prozentwert angeben.  

-   PERCENTFREEDISKSPACE: Gibt die Ordnergröße als Prozentsatz des freien Speicherplatzes an. Wenn Sie diese Eigenschaft angeben, müssen Sie auch die Eigenschaft SMSCACHESIZE als Prozentwert angeben. Wenn der Datenträger z. B. über 10 MB freien Speicherplatz verfügt und für SMSCACHESIZE 50 angegeben ist, wird die Ordnergröße auf 5 MB festgelegt. Diese Eigenschaft kann nicht in Verbindung mit der Eigenschaft PERCENTDISKSPACE verwendet werden.  

-   MAXDRIVE: Gibt an, dass der Ordner auf dem größten verfügbaren Datenträger installiert werden soll. Dieser Wert wird ignoriert, wenn ein Pfad mit der Eigenschaft SMSCACHEDIR angegeben wurde.  

-   MAXDRIVESPACE: Gibt an, dass der Ordner auf dem Laufwerk mit dem meisten verfügbaren Speicherplatz installiert werden soll. Dieser Wert wird ignoriert, wenn ein Pfad mit der Eigenschaft SMSCACHEDIR angegeben wurde.  

-   NTFSONLY: Gibt an, dass der Ordner nur auf NTFS-Laufwerken installiert werden kann. Dieser Wert wird ignoriert, wenn ein Pfad mit der Eigenschaft SMSCACHEDIR angegeben wurde.  

-   COMPRESS: Gibt an, dass der Ordner komprimiert gespeichert werden soll.  

-   FAILIFNOSPACE: Gibt an, dass die Clientsoftware entfernt werden soll, wenn ausreichend Speicherplatz zum Installieren des Ordners verfügbar ist.  

Beispiel: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Für die Angabe der Größe des Clientcacheordners sind Clienteinstellungen verfügbar. Das Hinzufügen dieser Clienteinstellungen ersetzt SMSCACHESIZE als client.msi-Eigenschaft, um die Größe des Clientcaches anzugeben. Weitere Informationen zu den Clienteinstellungen finden Sie unter [client settings for cache size](about-client-settings.md#client-cache-settings) (Clienteinstellungen für Cachegröße).  

<!-- For 1602 and earlier, SMSCACHESIZE specifies the size of the client cache folder in megabyte (MB) or as a percentage when used with the PERCENTDISKSPACE or PERCENTFREEDISKSPACE property. If this property isn't set, the folder defaults to a maximum size of 5120 MB. The lowest value that you can specify is 1 MB.  -->

> [!NOTE]  
>  Wenn für den Download eines neuen Pakets die maximale Ordnergröße überschritten würde, der Ordnerinhalt jedoch nicht zur Freigabe von Speicherplatz geleert werden kann, wird der Downloadvorgang abgebrochen, und das Programm bzw. die Anwendung kann nicht ausgeführt werden.  

Diese Einstellung wird ignoriert, wenn ein Upgrade eines vorhandenen Clients ausgeführt wird und wenn Softwareupdates vom Client heruntergeladen werden.  

Beispiel: `CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  Wenn Sie einen Client neu installieren, können Sie die Installationseigenschaften SMSCACHESIZE und SMSCACHEFLAGS nicht verwenden, um die Cachegröße auf einen niedrigeren Wert als vorher festzulegen. Wenn Sie versuchen, diese Aktion auszuführen, wird Ihr Wert ignoriert. Die Cachegröße wird automatisch auf die vorherige Größe festgelegt.  

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Gibt den zu überprüfenden Speicherort und die Reihenfolge an, die das Configuration Manager-Installationsprogramm für die Überprüfung der Konfigurationseinstellungen verwendet. Bei der Eigenschaft handelt es sich um eine Zeichenfolge mit einem oder mehreren Zeichen, die jeweils eine spezielle Konfigurationsquelle angeben. Verwenden Sie die Zeichenwerte R, P, M und U alleine oder zusammen:  

-   R: Überprüfung der Konfigurationseinstellungen in der Registrierung.  

   Weitere Informationen finden Sie unter [Informationen zum Speichern von Clientinstallationseigenschaften in der Registrierung](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

-   P: Überprüfung der Konfigurationseinstellungen in den Installationseigenschaften an der Eingabeaufforderung  

-   M: Überprüfung der vorhandenen Einstellungen beim Aktualisieren eines älteren Clients mit der Configuration Manager-Clientsoftware  

-   U: Upgrade des installierten Clients auf eine neuere Version (unter Verwendung des zugewiesenen Standortcodes)  

 Bei der Clientinstallation wird standardmäßig `PU` verwendet, um zuerst die Installationseinstellungen und dann die vorhandenen Einstellungen zu überprüfen.  

 Beispiel: `CCMSetup.exe SMSCONFIGSOURCE=RP`  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 Hiermit wird angegeben, ob Windows Internet Name Service (WINS) vom Client verwendet werden kann, um einen Verwaltungspunkt zu finden, von dem HTTP-Verbindungen zugelassen werden. Diese Methode wird von den Clients verwendet, wenn kein Verwaltungspunkt in den Active Directory-Domänendiensten oder in DNS gefunden werden kann.  

 Diese Eigenschaft beeinflusst nicht, ob der Client WINS für die Namensauflösung verwendet.  

 Sie können zwei verschiedene Modi für diese Eigenschaft konfigurieren:  

-   NOWINS: Dieser Wert stellt die sicherste Einstellung für diese Eigenschaft dar. Es wird verhindert, dass von Clients ein Verwaltungspunkt in WINS gefunden wird. Wenn Sie diese Einstellung verwenden, ist eine alternative Methode für die Clients erforderlich, mit der ein Verwaltungspunkt im Intranet gefunden werden kann, beispielsweise Active Directory-Domänendienste oder DNS-Veröffentlichung.  

-   WINSSECURE (Standardeinstellung): In diesem Modus kann ein Client, der HTTP-Kommunikation verwendet, mithilfe von WINS einen Verwaltungspunkt suchen. Für den Client ist jedoch eine Kopie des vertrauenswürdigen Stammschlüssels erforderlich, bevor eine Verbindung mit dem Verwaltungspunkt hergestellt werden kann. Weitere Informationen finden Sie unter [Planning for the trusted root key (Planen des vertrauenswürdigen Stammschlüssels)](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  


 Beispiel: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Hiermit wird ein erster Verwaltungspunkt für die Verwendung durch den Configuration Manager-Client angegeben.  

> [!IMPORTANT]  
>  Wenn der Verwaltungspunkt nur Clientverbindungen über HTTPS akzeptiert, müssen Sie dem Namen des Verwaltungspunkts das Präfix „https://“ voranstellen.  

Beispiel: `CCMSetup.exe SMSMP=smsmp01.contoso.com`

Beispiel: `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  


### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Gibt den vertrauenswürdigen Configuration Manager-Stammschlüssel für den Fall an, dass dieser nicht aus den Active Directory-Domänendiensten abgerufen werden kann. Diese Eigenschaft gilt für Clients, von denen HTTP- und HTTPS-Clientkommunikation verwendet wird. Weitere Informationen finden Sie unter [Planning for the trusted root key (Planen des vertrauenswürdigen Stammschlüssels)](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 Beispiel: `CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Diese Eigenschaft wird verwendet, um den vertrauenswürdigen Configuration Manager-Stammschlüssel neu zu installieren. Hiermit werden der vollständige Pfad und der Dateiname einer Datei mit dem vertrauenswürdigen Stammschlüssel angegeben. Diese Eigenschaft gilt für Clients, von denen HTTP- und HTTPS-Clientkommunikation verwendet wird. Weitere Informationen finden Sie unter [Planning for the trusted root key (Planen des vertrauenswürdigen Stammschlüssels)](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 Beispiel: 'CCMSetup.exe SMSROOTKEYPATH=&lt;Vollständiger Pfad und Dateiname\>`  

### <a name="smssigncert"></a>SMSSIGNCERT

 Hiermit werden der vollständige Pfad und der CER-Dateiname des exportierten selbstsignierten Zertifikats auf dem Standortserver angegeben.  

 Dieses Zertifikat ist im **SMS** -Zertifikatspeicher unter dem Antragstellernamen **Standortserver** und dem Anzeigenamen **Signaturzertifikat des Standortservers**gespeichert.  

 Beispiel: **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;Vollständiger Pfad und Dateiname\>**  

### <a name="smssitecode"></a>SMSSITECODE

 Gibt den Configuration Manager-Standort an, dem der Client zugewiesen werden soll. Dieser Wert kann entweder ein dreistelliger Standortcode oder das Wort AUTO sein. Wenn Sie AUTO angeben oder Sie diese Eigenschaft nicht angeben, wird vom Client versucht, die Standortzuweisung anhand der Active Directory-Domänendienste oder anhand eines angegebenen Verwaltungspunkts zu bestimmen. Um AUTO für Clientupgrades festzulegen, müssen Sie ferner [SITEREASSIGN](#sitereassign) auf TRUE setzen.    

> [!NOTE]  
>  Verwenden Sie AUTO nicht, wenn Sie auch den internetbasierten Verwaltungspunkt angebe (CCMHOSTNAME). In diesem Fall müssen Sie den Client direkt dem Standort zuweisen.  

 Beispiel: `CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> Unterstützte Attributwerte für die PKI-Zertifikatauswahlkriterien  
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
