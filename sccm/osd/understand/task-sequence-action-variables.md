---
title: Tasksequenz-Aktionsvariablen
titleSuffix: Configuration Manager
description: Verwenden Sie Sequenzaktionsvariablen, z.B. Variablen zur Netzwerkeinstellung, um Konfigurationseinstellungen für einen einzelnen Schritt in einer Configuration Manager-Tasksequenz anzugeben.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e2269031-0977-4f01-a274-420e00630575
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f66203e335524fa922ec1b6ab3dd4dc5fb917b0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>Tasksequenz-Aktionsvariablen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit den Tasksequenzaktionsvariablen werden Konfigurationseinstellungen angegeben, die von einem einzelnen Schritt einer System Center Configuration Manager-Tasksequenz verwendet werden. Standardmäßig werden die Einstellungen durch diesen Tasksequenzschritt vor der Ausführung initialisiert. Dabei sind diese Einstellungen nur verfügbar, solange der zugehörige Tasksequenzschritt ausgeführt wird. Mit anderen Worten, die Tasksequenz fügt den Wert für die Aktionsvariable zur Tasksequenzumgebung hinzu, bevor der Tasksequenzschritt ausgeführt wird. Nachdem der Schritt ausgeführt wurde, entfernt die Tasksequenz den Wert aus der Umgebung.  

## <a name="action-variable-example"></a>Beispiel für eine Aktionsvariable  
 Mit dem Tasksequenzschritt **Befehlszeile ausführen** können Sie beispielsweise ein Startverzeichnis für eine Befehlszeilenaktion angeben. Dieser Schritt umfasst die Eigenschaft **Starten in** , deren Standardwert in der Tasksequenzumgebung als Variable **WorkingDirectory** gespeichert wird. Die Umgebungsvariable **WorkingDirectory** wird initialisiert, bevor die Tasksequenzaktion **Befehlszeile ausführen** ausgeführt wird. Während des Schritts **Befehlszeile ausführen** kann über die Eigenschaft **Starten in** auf den Wert **WorkingDirectory** zugegriffen werden. Nach dem Schritt wird der Wert der Variablen **WorkingDirectory** aus der Umgebung entfernt. Falls die Sequenz einen weiteren Tasksequenzschritt **Befehlszeile ausführen** enthält, wird die neue Variable **WorkingDirectory** durch die Tasksequenz initialisiert und auf den Startwert für den aktuellen Schritt festgelegt.  

 Der *Standardwert* für eine Tasksequenz-Aktionsvariable ist vorhanden, wenn der Tasksequenzschritt ausgeführt wird. Wenn Sie einen *neuen Wert* festlegen, ist dieser für mehrere Schritte in der Tasksequenz verfügbar. Wenn Sie eine der Methoden zum Erstellen von Tasksequenzvariablen zum Überschreiben eines integrierten Variablenwerts verwenden, bleibt der neue Wert in der Umgebung erhalten und überschreibt den Standardwert für weitere Schritte in der Tasksequenz. Wenn Sie zum Beispiel als ersten Schritt der Tasksequenz den Schritt **Tasksequenzvariable festlegen** hinzufügen, der die Variable **WorkingDirectory** auf **C:\\** festlegt, verwenden alle Schritte **Befehlszeile ausführen** in der Tasksequenz den neuen Startverzeichniswert.  

## <a name="action-variables-for-task-sequence-actions"></a>Aktionsvariablen für Tasksequenzaktionen  
 Configuration Manager-Tasksequenzvariablen sind nach der zugehörigen Tasksequenzaktion gruppiert. Weitere Informationen zu den Aktionsvariablen, die einer bestimmten Aktion zugeordnet sind, finden Sie unter den folgenden Links. Über die Tasksequenzvariablen wird die Funktionsweise der Tasksequenzaktion gesteuert. Von der Tasksequenzaktion werden die von Ihnen als Eingabevariablen gekennzeichneten Variablen gelesen und verwendet. Alternativ können Sie die Variablen mithilfe des Schritts [Tasksequenzvariable festlegen](task-sequence-steps.md#BKMK_SetTaskSequenceVariable) oder des Objekts „TSEnvironment COM“ zur Laufzeit festlegen. Nur die Tasksequenzaktion kennzeichnet Variablen als Ausgabevariablen. Diese Ausgabevariablen werden von später in der Tasksequenz auftretenden Aktionen gelesen.  

> [!NOTE]  
>  Nicht alle Tasksequenzaktionen sind einem Satz Tasksequenzvariablen zugeordnet. Beispielsweise gibt es zwar Variablen, die der Aktion BitLocker aktivieren zugeordnet sind, aber der Aktion BitLocker deaktivieren sind keine Variablen zugeordnet.  



###  <a name="BKMK_ApplyDataImage"></a> Anwenden von Datenimages   
 Weitere Informationen finden Sie unter [Anwenden von Datenimages](task-sequence-steps.md#BKMK_ApplyDataImage). 

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (Eingabe)|Hiermit wird der Indexwert des Abbilds angegeben, das auf den Zielcomputer angewendet wird.|  
|OSDWipeDestinationPartition<br /><br /> (Eingabe)|Hiermit wird angegeben, ob die auf der Zielpartition vorhandenen Dateien gelöscht werden sollen.<br /><br /> Gültige Werte:<br /><br /> **true** (Standard)<br /><br /> **false**|  



###  <a name="BKMK_ApplyDriverPackage"></a> Treiberpaket anwenden   
Weitere Informationen finden Sie unter [Treiberpaket anwenden](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (Eingabe)|Hiermit wird die Inhalts-ID des Treibers für Massenspeichergeräte angegeben, der aus dem Treiberpaket installiert werden soll. Wenn diese Variable nicht angegeben ist, wird kein Massenspeichertreiber installiert.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (Eingabe)|Hiermit wird die INF-Datei des zu installierenden Massenspeichertreibers angegeben.<br /><br /> <br /><br /> Diese Tasksequenzvariable ist erforderlich, wenn ein Wert für OSDApplyDriverBootCriticalContentUniqueID festgelegt ist.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (Eingabe)|Hiermit wird angegeben, ob ein Treiber für Massenspeichergeräte installiert wird. Diese Variable muss **SCSI** sein.<br /><br /> Diese Tasksequenzvariable ist erforderlich, wenn ein Wert für OSDApplyDriverBootCriticalContentUniqueID festgelegt ist.|  
|OSDApplyDriverBootCriticalID<br /><br /> (Eingabe)|Hiermit wird die für den Start erforderliche ID des Treibers für Massenspeichergeräte angegeben, der installiert werden soll. Diese ID wird im Abschnitt **SCSI** der Gerätetreiberdatei „txtsetup.oem“ aufgeführt.<br /><br /> Diese Tasksequenzvariable ist erforderlich, wenn ein Wert für OSDApplyDriverBootCriticalContentUniqueID festgelegt ist.|  
|OSDAllowUnsignedDriver<br /><br /> (Eingabe)|Hiermit wird angegeben, ob Windows so konfiguriert werden soll, dass die Installation nicht signierter Gerätetreiber zugelassen wird. Diese Tasksequenzvariable wird bei der Bereitstellung von Windows Vista und späteren Betriebssystemen nicht verwendet.<br /><br /> Gültige Werte:<br /><br /> **true**<br /><br /> **false** (Standard)|  



###  <a name="BKMK_ApplyNetworkSettings"></a> Anwenden von Netzwerkeinstellungen   
 Weitere Informationen finden Sie unter [Anwenden von Netzwerkeinstellungen](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (Eingabe)|Bei dieser Tasksequenzvariablen handelt es sich um die Arrayvariable. Die einzelnen Elemente im Array stellen die Einstellungen für eine einzelne Netzwerkkarte im Computer dar. Greifen Sie auf die Einstellungen für den jeweiligen Adapter zu, indem Sie den Namen der Arrayvariablen mit dem nullbasierten Netzwerkadapterindex und dem Eigenschaftennamen kombinieren.<br /><br />Wenn in diesem Schritt mehrere Netzwerkadapter konfiguriert werden, werden die Eigenschaften für den zweiten Netzwerkadapter mithilfe des Indexes im Variablennamen definiert. Beispielsweise OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList und OSDAdapter1EnableWINS.<br /><br />Verwenden Sie beispielsweise die folgenden Variablennamen, wenn Sie die Eigenschaften des ersten Netzwerkadapters für diesen Tasksequenzschritt definieren, um Folgendes zu konfigurieren:<br /><br /> <ul><li>**OSDAdapter0EnableDHCP**: **true** aktiviert Dynamic Host Configuration Protocol (DHCP) für den Adapter.<br />    Diese Einstellung ist erforderlich. Mögliche Werte: **true** oder **false**.</li><li>**OSDAdapter0IPAddressList**: durch Trennzeichen getrennte Liste der IP-Adressen für den Adapter; diese Eigenschaft wird ignoriert, es sei denn, **EnableDHCP** ist auf **false**festgelegt.<br />    Diese Einstellung ist erforderlich.</li><li>**OSDAdapter0SubnetMask**: durch Trennzeichen getrennte Liste der Subnetzmasken; diese Eigenschaft wird ignoriert, es sei denn, **EnableDHCP** ist auf **false**festgelegt.<br />    Diese Einstellung ist erforderlich.</li><li>**OSDAdapter0Gateways**: durch Trennzeichen getrennte Liste der IT-Gatewayadressen; diese Eigenschaft wird ignoriert, es sei denn, **EnableDHCP** ist auf **false**festgelegt.<br />    Diese Einstellung ist erforderlich.</li><li>**OSDAdapter0DNSDomain**: DNS-Domäne (Domain Name System) für den Adapter.</li><li>**OSDAdapter0DNSServerList**: durch Trennzeichen getrennte Liste der DNS-Server für den Adapter.<br />    Diese Einstellung ist erforderlich.</li><li>**OSDAdapter0EnableDNSRegistration**: **true** registriert die IP-Adresse für den Adapter in DNS.</li><li>**OSDAdapter0EnableFullDNSRegistration**: **true** registriert die IP-Adresse für den Adapter unter dem vollständigen DNS-Namen des Computers in DNS.</li><li>**OSDAdapter0EnableIPProtocolFiltering**: **true** aktiviert die IP-Protokollfilterung für den Adapter.</li><li>**OSDAdapter0IPProtocolFilterList**: durch Trennzeichen getrennte Liste der Protokolle, die über IP ausgeführt werden dürfen; diese Eigenschaft wird ignoriert, wenn **EnableIPProtocolFiltering** auf **false**festgelegt ist.</li><li>**OSDAdapter0EnableTCPFiltering**: **true** aktiviert TCP-Portfilterung für den Adapter.</li><li>**OSDAdapter0TCPFilterPortList**: durch Trennzeichen getrennte Liste der Ports, denen Zugriffsberechtigungen für TCP zu erteilen sind; diese Eigenschaft wird ignoriert, wenn **EnableTCPFiltering** auf **false**festgelegt ist.</li><li>**OSDAdapter0TcpipNetbiosOptions**: Optionen für NetBIOS über TCP/IP. Es sind folgende Werte möglich:<br /><br /> <ul><li>**0**: NetBIOS-Einstellungen von DHCP-Server verwenden</li><li>**1**: NetBIOS über TCP/IP aktivieren</li><li>**2**: NetBIOS über TCP/IP deaktivieren</li></ul></li><li>**OSDAdapter0EnableWINS**: **true** verwendet WINS für die Namensauflösung.</li><li>**OSDAdapter0WINSServerList**: durch Trennzeichen getrennte Liste der WINS-Server-IP-Adressen; diese Eigenschaft wird ignoriert, es sei denn, **EnableWINS** ist auf **true**festgelegt.</li><li>**OSDAdapter0MacAddress**: Mithilfe der MAC-Adresse werden Einstellungen des physischen Netzwerkadapters zugeordnet.</li><li>**OSDAdapter0Name**: Name der Netzwerkverbindung, der in der Systemsteuerung unter „Netzwerkverbindungen“ angezeigt wird; der Name ist zwischen 0 und 255 Zeichen lang.</li><li>**OSDAdapter0Index**: Index der Netzwerkadaptereinstellungen im Array der Einstellungen.<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (Eingabe)|Hiermit wird die Anzahl der Netzwerkkarten angegeben, die auf dem Zielcomputer installiert sind. Wenn der **OSDAdapterCount** -Wert festgelegt wird, müssen alle Konfigurationsoptionen für die einzelnen Adapter festgelegt werden. Wenn Sie z. B. den **OSDAdapterTCPIPNetbiosOptions** -Wert für einen bestimmten Adapter festlegen, müssen auch alle anderen Werte für diesen Adapter konfiguriert werden.<br /><br />Wenn dieser Wert nicht angegeben wird, werden alle **OSDAdapter** -Werte ignoriert.|  
|OSDDNSDomain<br /><br /> (Eingabe)|Hiermit wird der primäre DNS-Server angegeben, der vom Zielcomputer verwendet wird.|  
|OSDDomainName<br /><br /> (Eingabe)|Hiermit wird der Name der Windows-Domäne angegeben, der der Zielcomputer hinzugefügt wird. Der angegebene Wert muss ein gültiger Active Directory-Domänendienste-Domänenname sein.|  
|OSDDomainOUName<br /><br /> (Eingabe)|Hiermit wird der Name der Organisationseinheit, der der Zielcomputers hinzugefügt wird, im RFC 1779-Format angegeben. Wenn dieser Parameter angegeben wird, muss die Zeichenfolge einen vollständigen Pfad enthalten.<br /><br /> Beispiel:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (Eingabe)|Hiermit wird angegeben, ob der TCP/IP-Filter aktiviert wird.<br /><br /> Gültige Werte:<br /><br /> **true**<br /><br /> **false** (Standard)|  
|OSDJoinAccount<br /><br /> (Eingabe)|Hiermit wird das Netzwerkkonto angegeben, über das der Zielcomputer einer Windows-Domäne hinzugefügt wird.|  
|OSDJoinPassword<br /><br /> (Eingabe)|Hiermit wird das Netzwerkkennwort angegeben, über das der Zielcomputer einer Windows-Domäne hinzugefügt wird.|  
|OSDNetworkJoinType<br /><br /> (Eingabe)|Hiermit wird angegeben, ob der Zielcomputer einer Windows-Domäne oder einer Arbeitsgruppe hinzugefügt wird.<br /><br /> **0** bedeutet, dass der Zielcomputer einer Windows-Domäne hinzugefügt wird. **1** bedeutet, dass der Computer einer Arbeitsgruppe hinzugefügt wird.<br /><br /> Gültige Werte:<br /><br /> **0**<br /><br /> **1**|  
|OSDDNSSuffixSearchOrder<br /><br /> (Eingabe)|Hiermit wird die DNS-Suchreihenfolge für den Zielcomputer angegeben.|  
|OSDWorkgroupName<br /><br /> (Eingabe)|Hiermit wird der Name der Arbeitsgruppe angegeben, der der Zielcomputer hinzugefügt wird.<br /><br /> Geben Sie entweder diesen Wert oder den Wert **OSDDomainName** an. Der Name der Arbeitsgruppe darf maximal 32 Zeichen umfassen.<br /><br /> Beispiel:<br /><br /> **Buchhaltung**|  



###  <a name="BKMK_ApplyOperatingSystem"></a> Betriebssystemimage anwenden   
 Weitere Informationen finden Sie unter [Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (Eingabe)|Gibt den Dateinamen der Antwortdatei für die Betriebssystembereitstellung an, die zum Bereitstellungspaket des Betriebssystems gehört.|  
|OSDImageIndex<br /><br /> (Eingabe)|Hiermit wird der Abbildindexwert der WIM-Datei angegeben, die auf den Zielcomputer angewendet wird.|  
|OSDInstallEditionIndex<br /><br /> (Eingabe)|Hiermit wird die Version von Windows Vista oder einem späteren Betriebssystem angegeben, die bzw. das installiert wird. Wenn keine Version festgelegt ist, bestimmt Windows Setup anhand des referenzierten Product Keys, welche Version installiert werden soll.<br /><br /> Verwenden Sie den Wert null (0) nur, wenn Folgendes zutrifft:<br /><br /> Sie installieren ein Betriebssystem vor Windows Vista.<br />Sie installieren eine Volumenlizenzedition von Windows Vista oder höher, und es wird kein Product Key angegeben.<br /><br /> Gültige Werte:<br /><br /> **0** (Standard)|  
|OSDTargetSystemDrive (Ausgabe)|Hiermit wird der Laufwerksbuchstabe der Partition angegeben, die die Betriebssystemdateien enthält.|  



###  <a name="BKMK_ApplyWindowsSettings"></a> Windows-Einstellungen anwenden   
 Weitere Informationen finden Sie unter [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (Eingabe)|Hiermit wird der Name des Zielcomputers angegeben.<br /><br /> Beispiel:<br /><br /> **%_SMSTSMachineName%** (Standard)|  
|OSDProductKey<br /><br /> (Eingabe)|Gibt den Windows-Product Key an. Der angegebene Wert darf zwischen 1 und 255 Zeichen enthalten.|  
|OSDRegisteredUserName<br /><br /> (Eingabe)|Gibt den registrierten Standardbenutzernamen im neuen Betriebssystem an. Der angegebene Wert darf zwischen 1 und 255 Zeichen enthalten.|  
|OSDRegisteredOrgName<br /><br /> (Eingabe)|Gibt den registrierten Standardorganisationsnamen im neuen Betriebssystem an. Der angegebene Wert darf zwischen 1 und 255 Zeichen enthalten.|  
|OSDTimeZone<br /><br /> (Eingabe)|Hiermit wird die Standardeinstellung für die Zeitzone angegeben, die im neuen Betriebssystem verwendet wird.|  
|OSDServerLicenseMode<br /><br /> (Eingabe)|Hiermit wird der verwendete Windows Server-Lizenzmodus angegeben.<br /><br /> Gültige Werte:<br /><br /> **PerSeat**<br /><br /> **PerServer**|  
|OSDServerLicenseConnectionLimit<br /><br /> (Eingabe)|Gibt die Anzahl der maximal zulässigen Verbindungen an. Die angegebene Zahl muss zwischen 5 und 9999 liegen.|  
|OSDRandomAdminPassword<br /><br /> (Eingabe)|Gibt ein zufällig erstelltes Kennwort für das Administratorkonto im neuen Betriebssystem an. Wenn **true** festgelegt ist, deaktiviert Windows Setup das lokale Administratorkonto auf dem Zielcomputer. Wenn **false** festgelegt ist, aktiviert Windows Setup das lokale Administratorkonto auf dem Zielcomputer und setzt das Kontokennwort auf den Wert von **OSDLocalAdminPassword**.<br /><br /> Gültige Werte:<br /><br /> **true** (Standard)<br /><br /> **false**|  
|OSDLocalAdminPassword<br /><br /> (Eingabe)|Gibt das lokale Administratorkennwort an. Wenn Sie die Option **Lokales Administratorkennwort zufällig erstellen und das Konto auf allen unterstützten Plattformen deaktivieren** aktivieren, wird diese Variable in dem Schritt ignoriert. Der angegebene Wert darf zwischen 1 und 255 Zeichen enthalten.|  



###  <a name="BKMK_AutoApplyDrivers"></a> Treiber automatisch anwenden   
 Weitere Informationen finden Sie unter [Treiber automatisch anwenden](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (Eingabe)|Eine durch Kommas getrennte Liste der eindeutigen IDs der Treiberkatalogkategorie. Im Schritt **Treiber automatisch anwenden** werden nur die Treiber in mindestens einer der angegebenen Kategorien berücksichtigt. Dieser Wert ist optional und wird standardmäßig nicht festgelegt. Rufen Sie die verfügbaren Kategorie-IDs ab, indem Sie die Objekte **SMS_CategoryInstance** am Standort auflisten.|  
|OSDAllowUnsignedDriver<br /><br /> (Eingabe)|Hiermit wird angegeben, ob Windows so konfiguriert wird, dass die Installation nicht signierter Gerätetreiber zugelassen wird. Diese Tasksequenzvariable wird bei der Bereitstellung von Windows Vista und späteren Betriebssystemen nicht verwendet.<br /><br /> Gültige Werte:<br /><br /> **true**<br /><br /> **false** (Standard)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (Eingabe)|Wenn der Treiberkatalog mehrere mit einem Hardwaregerät kompatible Gerätetreiber enthält, legt diese Variable die im Schritt auszuführende Aktion fest. Wenn **true** festgelegt ist, wird in dem Schritt nur der optimale Gerätetreiber installiert. Wenn der Wert **false** ist, werden in dem Schritt alle kompatiblen Gerätetreiber installiert und der optimale Treiber wird von Windows ausgewählt.<br /><br /> Gültige Werte:<br /><br /> **true** (Standard)<br /><br /> **false**|  
|SMSTSDriverRequestConnectTimeOut|Bei der Anforderung des Treiberkatalogs ist diese Variable die Anzahl der Sekunden, die die Tasksequenz auf die HTTP-Serververbindung wartet. Wenn das Timeout beim Herstellen der Verbindung überschritten wird, wird die Anforderung durch die Tasksequenz abgebrochen. Standardmäßig ist das Timeout auf **60** Sekunden festgelegt.|  
|SMSTSDriverRequestReceiveTimeOut|Bei der Anforderung des Treiberkatalogs ist diese Variable die Anzahl der Sekunden, die die Tasksequenz auf eine Antwort wartet. Wenn das Timeout beim Herstellen der Verbindung überschritten wird, wird die Anforderung durch die Tasksequenz abgebrochen. Standardmäßig ist das Timeout auf **480** Sekunden festgelegt.|
|SMSTSDriverRequestResolveTimeOut|Bei der Anforderung des Treiberkatalogs ist diese Variable die Anzahl der Sekunden, die die Tasksequenz auf die HTTP-Namensauflösung wartet. Wenn das Timeout beim Herstellen der Verbindung überschritten wird, wird die Anforderung durch die Tasksequenz abgebrochen. Standardmäßig ist das Timeout auf **60** Sekunden festgelegt.|
|SMSTSDriverRequestSendTimeOut|Beim Senden einer Anforderung an den Treiberkatalog ist diese Variable die Anzahl der Sekunden, die die Tasksequenz auf das Senden der Anforderung wartet. Wenn das Timeout beim Senden der Anforderung überschritten wird, wird die Anforderung durch die Tasksequenz abgebrochen. Standardmäßig ist das Timeout auf **60** Sekunden festgelegt.|



###  <a name="BKMK_CaptureNetworkSettings"></a> Netzwerkeinstellungen erfassen   
 Weitere Informationen finden Sie unter [Netzwerkeinstellungen erfassen](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (Eingabe)|Hiermit wird angegeben, ob die Konfigurationsinformationen für die Netzwerkkarteneinstellungen (TCP/IP, DNS und WINS) erfasst werden.<br /><br /> Beispiele:<br /><br /> **true** (Standard)<br /><br /> **false**|  
|OSDMigrateNetworkMembership<br /><br /> (Eingabe)|Hiermit wird angegeben, ob die Informationen zur Arbeitsgruppen- oder Domänenmitgliedschaft im Rahmen der Betriebssystembereitstellung migriert werden.<br /><br /> Beispiele:<br /><br /> **true** (Standard)<br /><br /> **false**|  



###  <a name="BKMK_CaptureOperatingSystemImage"></a> Betriebssystemabbild erfassen   
 Weitere Informationen finden Sie unter [Betriebssystemabbild erfassen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDCaptureAccount<br /><br /> (Eingabe)|Hiermit wird ein Windows-Kontoname mit der Berechtigung, das erfasste Abbild in einer Netzwerkfreigabe zu speichern, angegeben.|  
|OSDCaptureAccountPassword<br /><br /> (Eingabe)|Gibt das Kennwort für das Windows-Konto an, das zum Speichern des erfassten Abbilds in einem freigegebenen Netzwerkordner verwendet wird.|  
|OSDCaptureDestination<br /><br /> (Eingabe)|Hiermit wird der Speicherort angegeben, an dem das erfasste Betriebssystemabbild gespeichert wird. Die maximale Länge für den Verzeichnisnamen beträgt 255 Zeichen.|  
|OSDImageCreator<br /><br /> (Eingabe)|Dies ist ein optionaler Name des Benutzers, der das Abbild erstellt hat. Dieser Name wird in der WIM-Datei gespeichert. Die maximale Länge des Benutzernamens beträgt 255 Zeichen.|  
|OSDImageDescription<br /><br /> (Eingabe)|Dies ist eine optionale benutzerdefinierte Beschreibung des erfassten Betriebssystemabbilds. Diese Beschreibung wird in der WIM-Datei gespeichert. Die maximale Länge der Beschreibung beträgt 255 Zeichen.|  
|OSDImageVersion<br /><br /> (Eingabe)|Eine optionale benutzerdefinierte Versionsnummer, die dem erfassten Betriebssystemabbild zugewiesen wird. Diese Versionsnummer wird in der WIM-Datei gespeichert. Bei diesem Wert kann es sich um eine beliebige Zeichenkombination mit einer maximalen Länge von 32 Zeichen handeln.|  
|OSDTargetSystemRoot<br /><br /> (Eingabe)|Gibt den Pfad zum Windows-Verzeichnis des installierten Betriebssystems auf dem Referenzcomputer an. Es wird dann geprüft, ob das Betriebssystem die Erfassung durch Configuration Manager unterstützt.|  



###  <a name="BKMK_CaptureUserState"></a> Benutzerzustand erfassen   
 Weitere Informationen finden Sie unter [Benutzerstatus erfassen](task-sequence-steps.md#BKMK_CaptureUserState).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (Eingabe)|Dies ist der UNC- oder lokale Pfadname des Ordners, in dem der Benutzerzustand gespeichert wird. Kein Standardwert.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (Eingabe)|Zusätzliche Befehlszeilenoptionen für Windows-EasyTransfer (früher USMT), die von der Tasksequenz zum Erfassen des Benutzerstatus verwendet werden. In dem Schritt werden diese Einstellungen im Tasksequenz-Editor nicht zur Verfügung gestellt. Geben Sie diese Optionen als Zeichenfolge an, die die Tasksequenz an die automatisch generierte USMT-Befehlszeile angehängt.<br /><br />Die USMT-Optionen, die mit dieser Tasksequenzvariablen angegeben werden, werden vor dem Ausführen dieser Tasksequenz nicht auf Genauigkeit überprüft.|  
|OSDMigrateMode<br /><br /> (Eingabe)|Ermöglicht das Anpassen der Dateien, die mit USMT erfasst wurden. Wenn diese Variable auf **Einfach** festgelegt ist, verwendet die Tasksequenz nur die USMT-Standardkonfigurationsdateien. Wenn diese Variable auf **Erweitert** festgelegt ist, werden durch die Tasksequenzvariable „OSDMigrateConfigFiles“ die von USMT verwendeten Konfigurationsdateien angegeben.<br /><br /> Gültige Werte:<br /><br /> **Einfach**<br /><br /> **Erweitert**|  
|OSDMigrateConfigFiles<br /><br /> (Eingabe)|Gibt die Konfigurationsdateien an, mit denen die Erfassung von Benutzerprofilen gesteuert wird. Diese Variable wird nur verwendet, wenn „OSDMigrateMode“ auf „Erweitert“ festgelegt wurde. Dieser durch Kommas getrennte Listenwert wird festgelegt, um die Migration benutzerdefinierter Benutzerprofile auszuführen.<br /><br /> Beispiel: miguser.xml, migsys.xml, migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (Eingabe)|Wenn USMT einige Dateien nicht erfassen kann, erlaubt diese Variable, dass die Erfassung des Benutzerstatus fortgesetzt wird.<br /><br /> Gültige Werte:<br /><br /> **true** (Standard)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (Eingabe)|Aktiviert die ausführliche Protokollierung für USMT.<br /><br /> Gültige Werte:<br /><br /> **true**<br /><br /> **false** (Standard)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (Eingabe)|Hiermit wird angegeben, ob verschlüsselte Dateien erfasst werden.<br /><br /> Gültige Werte:<br /><br /> **true**<br /><br /> **false** (Standard)|  
|_OSDMigrateUsmtPackageID<br /><br /> (Eingabe)|Gibt die Paket-ID des Configuration Manager-Pakets an, das die USMT-Dateien enthält. Diese Variable ist erforderlich.|  



###  <a name="BKMK_CaptureWindowsSettings"></a> Windows-Einstellungen erfassen   
 Weitere Informationen finden Sie unter [Windows-Einstellungen erfassen](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (Eingabe)|Hiermit wird angegeben, ob der Computername migriert wird.<br /><br /> Gültige Werte:<br /><br /> **true** (Standard)<br /><br /> **false**<br /><br /> Wenn der Wert **true** lautet, wird die Variable „OSDComputerName“ auf den NetBIOS-Namen des Computers festgelegt.|  
|OSDComputerName<br /><br /> (Ausgabe)|Auf den NetBIOS-Namen des Computers festlegen. Der Wert wird nur festgelegt, wenn die Variable „OSDMigrateComputerName“ auf **true** festgelegt ist.|  
|OSDMigrateRegistrationInfo<br /><br /> (Eingabe)|Gibt an, ob in dem Schritt Benutzer- und Organisationsinformationen migriert werden.<br /><br /> Gültige Werte:<br /><br /> **true** (Standard)<br /><br /> **false**<br /><br /> Wenn der Wert **true** lautet, wird die Variable „OSDRegisteredOrgName“ auf den registrierten Organisationsnamen des Computers festgelegt.|  
|OSDRegisteredOrgName<br /><br /> (Ausgabe)|Auf den registrierten Organisationsnamen des Computers festlegen. Der Wert wird nur festgelegt, wenn die Variable „OSDMigrateRegistrationInfo“ auf **true** festgelegt ist.|  
|OSDMigrateTimeZone<br /><br /> (Eingabe)|Hiermit wird angegeben, ob die Zeitzone des Computers migriert wird.<br /><br /> Gültige Werte:<br /><br /> **true** (Standard)<br /><br /> **false**<br /><br /> Wenn der Wert **true** zurückgegeben wird, wird die Variable „OSDTimeZone“ auf die Zeitzone des Computers festgelegt.|  
|OSDTimeZone<br /><br /> (Ausgabe)|Diese Variable wird auf die Zeitzone des Computers festgelegt. Der Wert wird nur festgelegt, wenn die Variable „OSDMigrateTimeZone“ auf **true** festgelegt ist.|  



###  <a name="BKMK_ConnecttoNetworkFolder"></a>Verbindung mit Netzwerkordner herstellen   
 Weitere Informationen finden Sie unter [Verbindung mit Netzwerkordner herstellen](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (Eingabe)|Hiermit wird das Administratorkonto angegeben, über das eine Verbindung mit der Netzwerkfreigabe hergestellt wird.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (Eingabe)|Gibt den Laufwerkbuchstaben des Netzwerks an, mit dem eine Verbindung hergestellt werden soll. Dieser Wert ist optional. Wenn er nicht angegeben ist, wird die Netzwerkverbindung keinem Laufwerkbuchstaben zugeordnet. Wenn der Wert angegeben wird, muss er im Bereich von D: bis Z: liegen. Sie dürfen außerdem X: nicht verwenden, da dieser Laufwerksbuchstabe während der Windows PE-Phase von Windows PE verwendet wird.<br /><br /> Beispiele:<br /><br /> **D:**<br /><br /> **E:**|  
|SMSConnectNetworkFolderPassword<br /><br /> (Eingabe)|Hiermit wird das Netzwerkkonto angegeben, über das eine Verbindung mit der Netzwerkfreigabe hergestellt wird.|  
|SMSConnectNetworkFolderPath<br /><br /> (Eingabe)|Gibt den Netzwerkpfad für die Verbindung an.<br /><br /> Beispiel:<br /><br /> **\\\servername\sharename**|  



###  <a name="BKMK_EnableBitLocker"></a> BitLocker aktivieren   
 Weitere Informationen finden Sie unter [BitLocker aktivieren](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (Eingabe)|Von der Tasksequenzaktion **BitLocker aktivieren** wird kein zufälliges Wiederherstellungskennwort generiert, sondern der angegebene Wert als Wiederherstellungskennwort verwendet. Dieser Wert muss ein gültiges numerisches BitLocker-Wiederherstellungskennwort sein.|  
|OSDBitLockerStartupKey<br /><br /> (Eingabe)|Von dem Schritt **BitLocker aktivieren** wird kein zufälliger Systemstartschlüssel für die Schlüsselverwaltungsoption **Nur Schlüssel zum Systemstart auf USB** generiert, sondern das Trusted Platform Module (TPM) als Systemstartschlüssel verwendet. Bei dem Wert muss es sich um einen gültigen, 256-Bit Base64-codierten BitLocker-Systemstartschlüssel handeln.|  



###  <a name="BKMK_FormatPartitionDisk"></a> Datenträger formatieren und partitionieren   
 Weitere Informationen finden Sie unter [Datenträger formatieren und partitionieren](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (Eingabe)|Gibt die Anzahl der zu partitionierenden physischen Datenträger an.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (Eingabe)|Wenn die Festplatte für die Kompatibilität mit bestimmten BIOS-Typen partitioniert wird, gibt diese Variable an, ob die Cacheausrichtungsoptimierung deaktiviert werden soll. Dies ist beim Bereitstellen der Betriebssysteme Windows XP- oder Windows Server 2003 erforderlich. Weitere Informationen hierzu finden Sie im [Artikel 931760](http://go.microsoft.com/fwlink/?LinkId=134081) und im [Artikel 931761](http://go.microsoft.com/fwlink/?LinkId=134082) der Microsoft Knowledge Base.<br /><br /> Gültige Werte:<br /><br /> **true**<br /><br /> **false** (Standard)| 
|OSDGPTBootDisk<br /><br /> (Eingabe)|Gibt an, ob eine EFI-Partition auf einer GPT-Festplatte erstellt werden soll. EFI-basierte Computer verwenden diese Partition als Startdatenträger.<br /><br /> Gültige Werte:<br /><br /> **true**<br /><br /> **false** (Standard)|  
|OSDPartitions<br /><br /> (Eingabe)|Gibt ein Array von Partitionseinstellungen an. Informationen zum Zugriff auf Arrayvariablen in der Tasksequenzumgebung finden Sie im Abschnitt über SDK.<br /><br /> Bei dieser Tasksequenzvariablen handelt es sich um die Arrayvariable. Die einzelnen Elemente im Array stellen die Einstellungen für eine einzelne Partition auf der Festplatte dar. Die Einstellungen, die für jede Partition definiert sind, können aufgerufen werden, indem der Name der Arrayvariablen mit der Null-basierten Nummer der Festplattenpartition und dem Eigenschaftennamen kombiniert wird.<br /><br /> Verwenden Sie beispielsweise die folgenden Variablennamen, um die Eigenschaften für die erste Partition zu definieren, die in diesem Schritt auf der Festplatte erstellt werden:<br /><br /> - **OSDPartitions0Type**: Gibt den Partitionstyp an. Diese Eigenschaft ist erforderlich. Gültige Werte lauten **Primär**, **Erweitert**, **Logisch** und **Versteckt**.<br />-   **OSDPartitions0FileSystem**: Gibt den Typ des Dateisystems an, das zum Formatieren der Partition verwendet wird. Diese Eigenschaft ist optional. Wenn Sie kein Dateisystem angeben, wird die Partition in diesem Schritt auch nicht formatiert. Gültige Werte sind **FAT32** und **NTFS**.<br />-   **OSDPartitions0Bootable**: Gibt an, ob die Partition startbar sein soll. Diese Eigenschaft ist erforderlich. Wenn der Wert für MBR-Datenträger auf **TRUE** festgelegt ist, wird diese Partition in dem Schritt als „aktiv“ gekennzeichnet.<br />-   **OSDPartitions0QuickFormat**: Gibt den Typ des verwendeten Formats an. Diese Eigenschaft ist erforderlich. Wenn dieser Wert auf **TRUE** festgelegt ist, wird in dem Schritt eine Schnellformatierung ausgeführt. Andernfalls umfasst der Schritt eine vollständige Formatierung.<br />-   **OSDPartitions0VolumeName**: Gibt den Namen an, der dem Volume bei der Formatierung zugewiesen wird. Diese Eigenschaft ist optional.<br />-   **OSDPartitions0Size**: Gibt die Größe der Partition an. Einheiten werden von der Variablen **OSDPartitions0SizeUnits** angegeben. Diese Eigenschaft ist optional. Wenn diese Eigenschaft nicht angegeben wird, wird die Partition mit dem gesamten verbleibenden freien Speicherplatz erstellt.<br />-   **OSDPartitions0SizeUnits**: Diese Einheiten werden in dem Schritt zum Interpretieren der Variable **OSDPartitions0Size** verwendet. Diese Eigenschaft ist optional. Gültige Werte sind **MB** (Standard), **GB** und **Prozent**.<br />-   **OSDPartitions0VolumeLetterVariable**: Bei der Erstellung von Partitionen wird in diesem Schritt für diese immer der nächste verfügbare Laufwerkbuchstabe in Windows PE verwendet. Verwenden Sie diese optionale Eigenschaft, um den Namen einer anderen Tasksequenzvariablen anzugeben. Mithilfe dieser Variablen wird in dem Schritt der neue Laufwerkbuchstabe zur späteren Referenz gespeichert.<br /><br />Wenn Sie mit dieser Tasksequenzaktion mehrere Partitionen definieren, werden die Eigenschaften für die zweite Partition über ihren Index im Variablennamen definiert. Zum Beispiel: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat** und **OSDPartitions1VolumeName**.|  
|OSDPartitionStyle<br /><br /> (Eingabe)|Gibt den bei der Partitionierung des Datenträgers zu verwendenden Partitionsstil an. **MBR** steht für den Partitionsstil „Master Boot Record“ und **GPT** für den Stil „GUID-Partitionstabelle“.<br /><br /> Gültige Werte:<br /><br /> **GPT**<br /><br /> **MBR**|  



###  <a name="BKMK_InstallApplication"></a> Anwendung installieren   
 Weitere Informationen finden Sie unter [Anwendung installieren](task-sequence-steps.md#BKMK_InstallApplication).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen<br /><br /> (Eingabe)|Beschreibung|  
|----------------------------------------|-----------------|  
| TSErrorOnWarning |Geben Sie an, ob das Tasksequenzmodul eine erkannte Warnung als Fehler während dieses Schritts betrachten soll. Die Tasksequenz legt die Variable „_TSAppInstallStatus“ auf **Warnung** fest, wenn mindestens eine Anwendung oder eine erforderliche Abhängigkeit aufgrund der Nichterfüllung einer Voraussetzung nicht installiert wurde. Wenn Sie diese Variable auf **True** festlegen und die Tasksequenz die Variable „_TSAppInstallStatus“ auf „Warnung“ setzt, ist das Ergebnis eine Fehlermeldung. Der Wert **False** entspricht dem Standardverhalten.| 
|SMSTSMPListRequestTimeoutEnabled|Verwenden Sie diese Variable, um wiederholte MPList-Anforderungen bei der Clientaktualisierung zu ermöglichen, wenn der Client sich nicht im Intranet befindet. <br />Dieser Wert ist standardmäßig auf **True** festgelegt. Wenn Clients sich im Internet befinden, können Sie diese Variable auf **False** festlegen, um unnötige Verzögerungen zu vermeiden. Diese Variable gilt nur für die Tasksequenzschritte „Anwendung installieren“ und „Softwareupdates installieren“.|  
|SMSTSMPListRequestTimeout|Geben Sie an, wie viele Millisekunden eine Tasksequenz nach dem erfolglosen Abrufen der Verwaltungspunktliste von Standortdiensten warten soll, bevor sie erneut versucht, die Anwendung zu installieren. Standardmäßig wartet die Tasksequenz **60000** Millisekunden (60 Sekunden), bevor sie diesen Schritt wiederholt, und führt die Wiederholung bis zu drei Mal durch.|  



###  <a name="BKMK_InstallSoftwareUpdates"></a> Softwareupdates installieren   
Weitere Informationen finden Sie unter [Softwareupdates installieren](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen<br /><br /> (Eingabe)|Beschreibung|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (Eingabe)|Hiermit wird angegeben, ob sämtliche Updates oder nur obligatorische Updates installiert werden sollen.<br /><br /> Gültige Werte:<br /><br /> **Alle**<br /><br /> **Obligatorisch**|  
|SMSTSSoftwareUpdateScanTimeout| Steuern Sie das Timeout für die Überprüfung auf Softwareupdates während dieses Schritts. Erhöhen Sie beispielsweise den Wert, wenn Sie zahlreiche Updates während der Überprüfung erwarten. Der Standardwert beträgt **1800** Sekunden (30 Minuten). Der Variablenwert ist in Sekunden festgelegt. |
|SMSTSWaitForSecondReboot|Diese optionale Tasksequenzvariable steuert das Clientverhalten, wenn die Installation eines Softwareupdates zwei Neustarts erfordert. Legen Sie diese Variable vor dem Ausführen dieses Schritts fest. So verhindern Sie, dass ein zweiter Neustart während der Installation des Softwareupdates einen Fehler bei der Tasksequenz verursacht.<br /><br /> Legen Sie den Wert „SMSTSWaitForSecondReboot“ in Sekunden fest, um anzugeben, für wie lange die Tasksequenz in diesem Schritt nach dem Neustart des Computers angehalten wird. Planen Sie genügend Zeit für einen zweiten Neustart ein. <br />Wenn Sie „SMSTSWaitForSecondReboot“ z.B. auf den Wert „600“ festlegen, wird die Tasksequenz nach einem Neustart für 10 Minuten angehalten, bevor weitere Schritte ausgeführt werden. Diese Variable ist hilfreich, wenn in einem einzigen Tasksequenzschritt „Softwareupdates installieren“ Hunderte von Softwareupdates installiert werden.| 
|SMSTSMPListRequestTimeoutEnabled|Verwenden Sie diese Variable, um wiederholte MPList-Anforderungen bei der Clientaktualisierung zu ermöglichen, wenn der Client sich nicht im Intranet befindet. <br />Dieser Wert ist standardmäßig auf **True** festgelegt. Wenn Clients sich im Internet befinden, können Sie diese Variable auf **False** festlegen, um unnötige Verzögerungen zu vermeiden. Diese Variable gilt nur für die Tasksequenzschritte „Anwendung installieren“ und „Softwareupdates installieren“.|  
|SMSTSMPListRequestTimeout|Geben Sie an, wie viele Millisekunden eine Tasksequenz nach dem erfolglosen Abrufen der Verwaltungspunktliste aus lokalen Diensten warten soll, bevor sie erneut versucht, das Softwareupdate zu installieren. Standardmäßig wartet die Tasksequenz **60000** Millisekunden (60 Sekunden), bevor sie diesen Schritt wiederholt, und führt die Wiederholung bis zu drei Mal durch.|  



###  <a name="BKMK_JoinDomainWorkgroup"></a> Einer Domäne oder Arbeitsgruppe beitreten   
 Weitere Informationen finden Sie unter [Einer Domäne oder Arbeitsgruppe beitreten](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (Eingabe)|Gibt das Konto an, über das der Beitritt des Zielcomputers zur Active Directory-Domäne erfolgt. Diese Variable ist für den Beitritt zu einer Domäne erforderlich.|  
|OSDJoinDomainName<br /><br /> (Eingabe)|Gibt den Namen einer Active Directory-Domäne an, der der Zielcomputer hinzugefügt wird. Der Domänenname muss zwischen 1 und 255 Zeichen enthalten.|  
|OSDJoinDomainOUName<br /><br /> (Eingabe)|Hiermit wird der Name der Organisationseinheit, der der Zielcomputers hinzugefügt wird, im RFC 1779-Format angegeben. Wenn dieser Parameter angegeben wird, muss die Zeichenfolge einen vollständigen Pfad enthalten. Der Name der Organisationseinheit muss zwischen 0 und 32.767 Zeichen enthalten. Dieser Wert wird nicht festgelegt, wenn die Variable **OSDJoinType** den Wert **1** (Arbeitsgruppe beitreten) aufweist.<br /><br /> Beispiel:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (Eingabe)|Gibt das Netzwerkkennwort an, über das der Beitritt des Zielcomputers zur Active Directory-Domäne erfolgt. Wenn diese Variable in der Tasksequenzumgebung nicht enthalten ist, versucht Windows Setup die Eingabe eines leeren Kennworts. Dieser Wert ist erforderlich, wenn die Variable **OSDJoinType** den Wert **0** (Domäne beitreten) aufweist.|  
|OSDJoinSkipReboot<br /><br /> (Eingabe)|Hiermit wird angegeben, ob der Neustart des Zielcomputers nach dessen Beitritt zur Domäne oder Arbeitsgruppe übersprungen werden soll.<br /><br /> Gültige Werte:<br /><br /> **true**<br /><br /> **false**|  
|OSDJoinType<br /><br /> (Eingabe)|Hiermit wird angegeben, ob der Zielcomputer einer Windows-Domäne oder einer Arbeitsgruppe hinzugefügt wird. Geben Sie **0** an, wenn der Zielcomputer einer Windows-Domäne hinzugefügt werden soll. Geben Sie **1** an, wenn der Zielcomputer einer Arbeitsgruppe hinzugefügt werden soll.<br /><br /> Gültige Werte:<br /><br /> **0**<br /><br /> **1**|  
|OSDJoinWorkgroupName<br /><br /> (Eingabe)|Hiermit wird der Name einer Arbeitsgruppe angegeben, der der Zielcomputer hinzugefügt wird. Der Name der Arbeitsgruppe muss zwischen 1 und 32 Zeichen enthalten.<br /><br /> Beispiel:<br /><br /> **Buchhaltung**|  



###  <a name="BKMK_PrepareWindowsCapture"></a> Windows für die Erfassung vorbereiten   
 Weitere Informationen finden Sie unter [Windows für die Erfassung vorbereiten](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (Eingabe)|Gibt an, ob Sysprep eine Liste der Gerätetreiber für Massenspeicher erstellen soll. Diese Einstellung gilt nur für Windows XP and Windows Server 2003. Diese Variable dient dazu, in der Datei „sysprep.inf“ den Abschnitt „[SysprepMassStorage]“ mit Informationen zu allen Massenspeichertreibern aufzufüllen, die von dem zu erfassenden Image unterstützt werden.<br /><br /> Gültige Werte:<br /><br /> **true**<br /><br /> **false** (Standard)|  
|OSDKeepActivation<br /><br /> (Eingabe)|Hiermit wird angegeben, ob das Produktaktivierungskennzeichen von Sysprep zurückgesetzt wird.<br /><br /> Gültige Werte:<br /><br /> **true**<br /><br /> **false** (Standard)|  
|OSDTargetSystemRoot<br /><br /> (Ausgabe)|Gibt den Pfad zum Windows-Verzeichnis des installierten Betriebssystems auf dem Referenzcomputer an. Es wird dann geprüft, ob das Betriebssystem die Erfassung durch Configuration Manager unterstützt.|  



###  <a name="BKMK_ReleaseStateStore"></a> Zustandsspeicher freigeben   
 Weitere Informationen finden Sie unter [Statusspeicher freigeben](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (Eingabe)|Dies ist der UNC- oder lokale Pfadname des Speicherorts, von dem aus der Benutzerzustand wiederhergestellt wird. Dieser Wert wird von den Tasksequenzaktionen **Benutzerzustand erfassen** und **Benutzerzustand wiederherstellen** verwendet.|  



###  <a name="BKMK_RequestState"></a> Zustandsspeicher anfordern   
  Weitere Informationen finden Sie unter [Statusspeicher freigeben](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (Eingabe)|Wenn das Computerkonto keine Verbindung mit dem Statusmigrationspunkt herstellen kann, gibt diese Variable an, ob die Tasksequenz das Netzwerkzugriffskonto als Ausweichmöglichkeit verwenden soll.<br /><br /> Gültige Werte:<br /><br /> **true**<br /><br /> **false** (Standard)|  
|OSDStateSMPRetryCount<br /><br /> (Eingabe)|Hiermit wird angegeben, wie viele Wiederholungsversuche des Tasksequenzschritts zum Suchen eines Zustandsmigrationspunkts ausgeführt werden, bevor der Schritt mit einem Fehler abgebrochen wird. Die angegebene Anzahl muss zwischen 0 und 600 liegen.|  
|OSDStateSMPRetryTime<br /><br /> (Eingabe)|Hiermit wird angegeben, wie viele Sekunden zwischen den einzelnen Versuchen des Tasksequenzschritts gewartet werden soll. Die Anzahl der Sekunden darf maximal 30 Zeichen umfassen.|  
|OSDStateStorePath<br /><br /> (Ausgabe)|Dies ist der UNC-Pfad des Ordners auf dem Zustandsmigrationspunkt, in dem der Benutzerzustand gespeichert ist.|  



###  <a name="BKMK_RestartComputer"></a> Computer neu starten   
 Weitere Informationen finden Sie unter [Computer neu starten](task-sequence-steps.md#BKMK_RestartComputer).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (Eingabe)|Hiermit wird die Nachricht angegeben, die den Benutzern vor dem Neustart des Zielcomputers angezeigt wird. Wenn diese Variable nicht festgelegt ist, wird die Standardnachricht angezeigt. Die angegebene Meldung darf nicht länger als 512 Zeichen sein.<br /><br /> Beispiel:<br /><br /> **Speichern Sie Ihre Arbeit, bevor der Computer neu gestartet wird.**|  
|SMSRebootTimeout<br /><br /> (Eingabe)|Gibt die Anzeigedauer der Warnmeldung an den Benutzer in Sekunden an, bis der Computer neu gestartet wird. Geben Sie null Sekunden an, wenn keine Neustartmeldung angezeigt werden soll.<br /><br /> Beispiele:<br /><br /> **0** (Standard)<br /><br />  **60**|  



###  <a name="BKMK_RestoreUserState"></a> Benutzerzustand wiederherstellen   
  Weitere Informationen finden Sie unter [Benutzerstatus wiederherstellen](task-sequence-steps.md#BKMK_RestoreUserState).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (Eingabe)|Dies ist der UNC-Pfadname oder der lokale Pfadname des Ordners, von dem aus der Benutzerzustand wiederhergestellt wird.|  
|OSDMigrateContinueOnRestore<br /><br /> (Eingabe)|Der Prozess wird fortgesetzt, auch wenn USMT einige Dateien nicht wiederherstellen konnte.<br /><br /> Gültige Werte:<br /><br /> **true** (Standard)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (Eingabe)|Aktiviert die ausführliche Protokollierung für USMT. Dieser Wert ist für die Aktion erforderlich.<br /><br /> Gültige Werte:<br /><br /> **true**<br /><br /> **false** (Standard)|  
|OSDMigrateLocalAccounts<br /><br /> (Eingabe)|Hiermit wird angegeben, ob das lokale Computerkonto wiederhergestellt werden soll.<br /><br /> Gültige Werte:<br /><br /> **true**<br /><br /> **false** (Standard)|  
|OSDMigrateLocalAccountPassword<br /><br /> (Eingabe)|Wenn für die Variable **OSDMigrateLocalAccounts** der Wert „true“ festgelegt ist, muss diese Variable das Kennwort enthalten, das allen migrierten lokalen Konten zugewiesen ist. USMT weist allen migrierten lokalen Konten das gleiche Kennwort zu. Betrachten Sie dieses als vorübergehendes Kennwort, und ändern Sie es später mit einer anderen Methode.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (Eingabe)|Gibt zusätzliche Befehlszeilenoptionen für USMT an, die beim Wiederherstellen des Benutzerstatus verwendet werden. Die zusätzlichen Optionen werden im Format einer Zeichenfolge angegeben, die der automatisch generierten USMT-Befehlszeile hinzugefügt wird. Die USMT-Optionen, die mit dieser Tasksequenzvariablen angegeben werden, werden vor dem Ausführen dieser Tasksequenz nicht auf Genauigkeit überprüft.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (Eingabe)|Gibt die Paket-ID des Configuration Manager-Pakets an, das die USMT-Dateien enthält. Diese Variable ist erforderlich.|  



###  <a name="BKMK_RunCommand"></a> Befehlszeile ausführen   
  Weitere Informationen finden Sie unter [Befehlszeile ausführen](task-sequence-steps.md#BKMK_RunCommandLine).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (Eingabe)|Mithilfe der Tasksequenz wird das Programm gesucht und standardmäßig auf einem 64-Bit-Betriebssystem in der Befehlszeile unter Verwendung des WOW64-Dateisystemredirectors ausgeführt. Durch dieses Verhalten kann der Befehl zum Ermitteln der 32-Bit-Versionen der Betriebssystemprogramme und DLLs verwendet werden. Ist diese Variable auf **true** gesetzt, wird die Verwendung des WOW64-Dateisystemredirectors deaktiviert. Mithilfe des Befehls lassen sich native 64-Bit-Versionen der Betriebssystemprogramme und DLLs ermitteln. Unter einem 32-Bit-Betriebssystem hat diese Variable keine Auswirkungen.|  
|WorkingDirectory<br /><br /> (Eingabe)|Gibt das Startverzeichnis für eine Befehlszeilenaktion an. Der angegebene Verzeichnisname darf nicht länger als 255 Zeichen sein.<br /><br /> Beispiele:<br /><br /> -   **C:\\**<br />-   **%SystemRoot%**|  
|SMSTSRunCommandLineUserName<br /><br /> (Eingabe)|Hiermit wird das Konto angegeben, mit dem die Befehlszeile ausgeführt wird. Der Wert ist eine Zeichenfolge in der Form Benutzername oder Domäne\Benutzername.|  
|SMSTSRunCommandLinePassword<br /><br /> (Eingabe)|Hiermit wird das Kennwort für das mit der Variablen SMSTSRunCommandLineUserName angegebene Konto angegeben.|  



### <a name="set-dynamic-variables"></a>Dynamische Variablen festlegen  
Weitere Informationen finden Sie unter [Dynamische Variablen festlegen](task-sequence-steps.md#BKMK_SetDynamicVariables).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen<br /><br /> (Eingabe)|Beschreibung|  
|----------------------------------------|-----------------|  
|_SMSTSMake|Gibt den Hersteller des Computers an.|  
|_SMSTSModel|Gibt das Modell des Computers an.|  
|_SMSTSMacAddresses|Gibt die vom Computer verwendeten MAC-Adressen an.|  
|_SMSTSIPAddresses|Gibt die vom Computer verwendeten IP-Adressen an.|  
|_SMSTSSerialNumber|Gibt die Seriennummer des Computers an.|  
|_SMSTSAssetTag|Gibt das Bestandskennzeichen für den Computer an.|  
|_SMSTSUUID|Gibt die UUID des Computers an.|  
|_SMSTSDefaultGateways|Gibt die vom Computer verwendeten Standardgateways an.|  



###  <a name="BKMK_SetupWindows"></a> Windows und ConfigMgr einrichten   
  Weitere Informationen finden Sie unter [Windows und ConfigMgr einrichten](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen<br /><br /> (Eingabe)|Beschreibung|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (Eingabe)|Hiermit werden die Eigenschaften der Clientinstallation angegeben, die bei der Installation des Configuration Manager-Clients verwendet werden.|  



### <a name="upgrade-operating-system"></a>Betriebssystem aktualisieren  
 Weitere Informationen finden Sie unter [Betriebssystem aktualisieren](task-sequence-steps.md#BKMK_UpgradeOS).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen<br /><br /> (Eingabe)|Beschreibung|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (Eingabe)|Gibt die zusätzlichen Befehlszeilenoptionen an, die während eines Windows 10-Upgrades zu Windows Setup hinzugefügt werden. Die Befehlszeilenoptionen werden während der Tasksequenz nicht überprüft.<br /><br /> Weitere Informationen finden Sie unter [Windows Setup-Befehlszeilenoptionen](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).|  
