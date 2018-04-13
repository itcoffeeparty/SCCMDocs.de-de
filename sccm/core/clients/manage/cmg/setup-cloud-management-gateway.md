---
title: Einrichten von Cloud Management Gateway
titleSuffix: System Center Configuration Manager
description: Mithilfe dieses Prozesses können Sie Schritt für Schritt den Cloud Management Gateway-Dienst einrichten.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: fb2a44897064e88f7ab6fd4f4b293520f54f1db7
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Einrichten des Cloudverwaltungsgateways für Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*  

Dieser Prozess umfasst die erforderlichen Schritte für die Einrichtung eines Cloud Management Gateway-Diensts. 

> [!Tip]
> Diese Funktion wurde erstmals in Version 1610 als [Vorabfunktion](/sccm/core/servers/manage/pre-release-features) eingeführt. Ab Version 1802 ist dieses Feature kein Vorabfeature mehr.



## <a name="before-you-begin"></a>Vorbereitung

Lesen Sie zunächst den Artikel [Planen von Cloud Management Gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway). Mithilfe dieses Artikels können Sie Ihren CMG-Entwurf bestimmen. 

Verwenden Sie die folgende Prüfliste, um sicherzustellen, dass Sie über die erforderlichen Informationen und Voraussetzungen für die Erstellung eines CMG verfügen:  

- Die zu verwendende Azure-Umgebung. Beispiel: die Azure Public Cloud oder die Azure US Government Cloud.  

- Abhängig von Ihrem Entwurf benötigen Sie mindestens ein Zertifikat für das CMG. Weitere Informationen finden Sie unter [Zertifikate für Cloud Management Gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).  

- Ab Version 1802 können Sie auswählen, ob Sie die **Azure Resource Manager-Bereitstellung** oder eine **klassische Dienstbereitstellung** verwenden möchten. Weitere Informationen finden Sie unter [Azure Resource Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager). Für eine Azure Resource Manager-Bereitstellung des CMG müssen folgende Voraussetzungen erfüllt sein:  

    - Integration in [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) für die **Cloudverwaltung**. Die Azure AD-Benutzerermittlung ist nicht erforderlich.  

    - Ein Abonnementadministrator muss sich anmelden.  

- Für eine klassische Dienstbereitstellung des CMG müssen folgende Voraussetzungen erfüllt sein:  

    - Azure-Abonnement-ID  

    - Azure-Verwaltungszertifikat  

- Ein global eindeutiger Name für den Dienst. Dieser Name stammt aus dem [CMG-Serverauthentifizierungszertifikat](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate).  

- Die Azure-Region für diese CMG-Bereitstellung.  

- Die Anzahl der VM-Instanzen für die Skalierung und Redundanz.  



## <a name="set-up-a-cmg"></a>Einrichten eines CMG

Führen Sie diese Prozedur am Standort der obersten Ebene aus. Bei diesem Standort handelt es sich entweder um einen eigenständigen primären Standort oder um den Standort der zentralen Verwaltung.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Cloud Services**, und wählen Sie **Cloudverwaltungsgateway** aus.  

2. Klicken Sie im Menüband auf **Cloudverwaltungsgateway erstellen**.  

3. Ab Version 1802 können Sie auf der Seite „Allgemein“ des Assistenten zunächst die Bereitstellungsmethode für das CMG auswählen: die **Azure Resource Manager-Bereitstellung** oder die **Klassische Dienstbereitstellung**.  

    1. Bei der **Azure Resource Manager-Bereitstellung**: Klicken Sie auf **Anmelden**, um sich bei dem Administratorkonto eines Azure-Abonnements zu authentifizieren. Der Assistent füllt die verbleibenden Felder automatisch aus den Informationen auf, die im Rahmen der Voraussetzungen für die Azure AD-Integration gespeichert wurden. Wenn Sie mehrere Abonnements besitzen, wählen Sie die **Abonnement-ID** des Abonnements aus, das Sie verwenden möchten.  

    2. Bei der **klassischen Dienstbereitstellung** und den *Configuration Manager-Versionen 1706 und 1710*: Geben Sie Ihre **Azure-Abonnement-ID** ein. Klicken Sie anschließend auf **Durchsuchen**, und wählen Sie die PFX-Datei für das Azure-Verwaltungszertifikat aus. 

4. Geben Sie die **Azure-Umgebung** für dieses CMG an. Die Optionen in der Dropdownliste können je nach Bereitstellungsmethode variieren.  

5. Klicken Sie auf **Weiter**. Warten Sie, bis der Standort die Verbindung mit Azure getestet hat.  

4. Klicken Sie auf der Seite „Einstellungen“ des Assistenten zunächst auf **Durchsuchen**, und wählen Sie anschließend die PFX-Datei für das CMG-Serverauthentifizierungszertifikat aus. Mit dem Namen dieses Zertifikats werden die erforderlichen Felder **Dienst-FQDN** und **Dienstname** aufgefüllt.  

   > [!NOTE]  
   > Das CMG-Serverauthentifizierungszertifikat unterstützt ab Version 1802 auch Platzhalter. Wenn Sie ein Platzhalterzertifikat verwenden, ersetzen Sie das Sternchen (\*) in dem Feld **Dienst-FQDN** durch den gewünschten Hostnamen für das CMG.  
   <!--491233-->  

5. Klicken Sie auf die Dropdownliste **Region**, um die Azure-Region für dieses CMG auszuwählen.  

6. Wählen Sie in Version 1802, wenn Sie eine Azure Resource Manager-Bereitstellung verwenden, die Option **Ressourcengruppe** aus. 
   1. Wenn Sie **Vorhandene verwenden** auswählen, wählen Sie anschließend aus der Dropdownliste eine vorhandene Ressourcengruppe aus.
   2. Wenn Sie **Neu erstellen** auswählen, geben Sie anschließend den Namen der neuen Ressourcengruppe ein.

6. Geben Sie in das Feld **VM-Instanz** die Anzahl der virtuellen Computer für diesen Dienst ein. Der Standardwert ist 1, er kann jedoch zentral auf bis zu 16 virtuelle Computer pro CMG hochskaliert werden.  

7. Klicken Sie auf **Zertifikate**, um ein vom Client als vertrauenswürdig eingestuftes Stammzertifikat hinzuzufügen. Sie können bis zu zwei vertrauenswürdige Stammzertifizierungsstellen und vier Zwischenzertifizierungsstellen (untergeordnete Zertifizierungsstellen) hinzufügen.  

8. Die Option **Clientzertifikatsperre überprüfen** wird vom Assistenten standardmäßig aktiviert. Eine Zertifikatsperrliste (Certificate Revocation List, CRL) muss öffentlich veröffentlicht werden, damit diese Überprüfung durchgeführt werden kann. Deaktivieren Sie diese Option, wenn Sie keine Zertifikatsperrliste veröffentlichen.  

9. Klicken Sie auf **Weiter**.  

10. Zur Überwachung des Cloudverwaltungsgateway-Datenverkehrs mit einem Schwellenwert von 14 Tagen müssen Sie das Kontrollkästchen für Schwellenwertwarnungen aktivieren. Legen Sie dann die Schwellenwerte und Prozentsätze für die verschiedenen Warnungsebenen fest. Klicken Sie auf **Weiter**, wenn Sie fertig sind.  

11. Überprüfen Sie die Einstellungen, und klicken Sie auf **Weiter**. Configuration Manager beginnt mit der Einrichtung des Diensts. Nach dem Schließen des Assistenten dauert es 5 bis 15 Minuten, bis der Dienst vollständig in Azure bereitgestellt ist. Überprüfen Sie die Spalte **Status** für das neue CMG, um zu bestimmen, wann der Dienst bereit ist.  

 > [!Note]  
 > Verwenden Sie **CloudMgr.log** und **CMGSetup.log** für die Problembehandlung von CMG-Bereitstellungen. Weitere Informationen finden Sie in den [Protokolldateien](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="configure-primary-site-for-client-certificate-authentication"></a>Konfigurieren des primären Standorts für die Clientzertifikatauthentifizierung

Führen Sie die hier beschriebene Prozedur zum Konfigurieren der einzelnen primären Standorte durch, wenn Sie für die Authentifizierung von Clients beim CMG [Clientauthentifizierungszertifikate](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate) verwenden.  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie **Standorte** aus.  

2. Wählen Sie den primären Standort, dem Ihre internetbasierten Clients zugewiesen sind, und wählen Sie **Eigenschaften** aus.  

3. Wechseln Sie zur Registerkarte **Clientcomputerkommunikation** im Eigenschaftenblatt für den primären Standort, und aktivieren Sie **Use PKI client certificate (client authentication) when available** (PKI-Clientzertifikat (Clientauthentifizierung) verwenden, sofern verfügbar).  

4. Wenn Sie keine Zertifikatsperrliste veröffentlichen, deaktivieren Sie die Option **Die Zertifikatsperrliste für Standortsysteme wird von Clients überprüft**.  



## <a name="add-the-cmg-connection-point"></a>Hinzufügen des CMG-Verbindungspunkts

Bei dem CMG-Verbindungspunkt handelt es sich um die Standortsystemrolle für die Kommunikation mit dem CMG. Befolgen Sie die allgemeinen Anweisungen zum [Installieren von Standortsystemrollen](/sccm/core/servers/deploy/configure/install-site-system-roles), um den CMG-Verbindungspunkt hinzuzufügen. Wählen Sie auf der Seite „Systemrollenauswahl“ des Assistenten zum Hinzufügen von Standortsystemrollen den Eintrag **Verbindungspunkt für Cloudverwaltungsgateway** aus. Wählen Sie anschließend den **Namen des Cloudverwaltungsgateways** aus, mit dem dieser Server eine Verbindung herstellt. Der Assistent zeigt die Region für das ausgewählte CMG an. 

> [!Important]
> Der CMG-Verbindungspunkt muss in einigen Szenarios über ein [Clientauthentifizierungszertifikat](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate) verfügen. 

 > [!Note]  
 > Verwenden Sie **CMGService.log** und **SMS_Cloud_ProxyConnector.log** für die Problembehandlung der CMG-Dienstintegrität. Weitere Informationen finden Sie in den [Protokolldateien](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="configure-client-facing-roles-for-cmg-traffic"></a>Konfigurieren von Rollen mit Clientkontakt für den CMG-Datenverkehr

Konfigurieren Sie die Verwaltungspunkt- und Softwareupdatepunkt-Standortsysteme, um CMG-Datenverkehr zu akzeptieren. Führen Sie diese Prozedur für alle Verwaltungspunkte und Softwareupdatepunkte am primären Standort durch, die Dienste für internetbasierte Clients bereitstellen.  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, klicken Sie mit der rechten Maustaste auf **Server und Standortsystemrollen**, und wählen Sie aus der Liste **Verwaltungspunkt** aus.  

2. Wählen Sie den Standortsystemserver aus, den Sie für den CMG-Datenverkehr konfigurieren möchten. Wählen Sie im Detailbereich die Rolle **Verwaltungspunkt** aus, und klicken Sie anschließend im Menüband auf **Eigenschaften**.  

3. Aktivieren Sie auf dem Eigenschaftenblatt „Verwaltungspunkt“ unter „Clientverbindungen“ das Kontrollkästchen neben **Allow Configuration Manager cloud management gateway traffic** (Datenverkehr über Cloud Management Gateway von Configuration Manager zulassen). 
    - Abhängig von Ihrem CMG-Entwurf und der Configuration Manager-Version müssen Sie möglicherweise die Option **HTTPS** aktivieren. Weitere Informationen finden Sie unter [Verwaltungspunkt für HTTPS aktivieren](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https).  

4. Klicken Sie auf **OK**.   

Wiederholen Sie diese Schritte ggf. für weitere Verwaltungspunkte und für Softwareupdatepunkte. 



## <a name="configure-clients-for-cmg"></a>Konfigurieren von Clients für das CMG

Sobald das CMG und die Standortsystemrollen ausgeführt werden, empfangen die Clients bei der nächsten Anforderung des Speicherorts automatisch den Speicherort des CMG-Diensts. Clients müssen sich im Intranet befinden, um den Speicherort des CMG-Diensts empfangen zu können, sofern Sie nicht [Windows 10-Clients mithilfe von Azure AD für die Authentifizierung installieren und zuweisen](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Der Abfragezyklus für Standortanfragen beträgt 24 Stunden. Wenn Sie nicht auf die normal geplante Standortanfragen warten möchten, können Sie sie erzwingen, indem Sie den SMS-Agent-Hostdienst (ccmexec.exe) auf dem Computer neustarten.  

> [!Note]
> Standardmäßig empfangen alle Clients die CMG-Richtlinie. Sie können dieses Verhalten mit der Clienteinstellung [Enable clients to use a cloud management gateway](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway) (Clients die Verwendung eines Cloud Management Gateway-Diensts ermöglichen) steuern.

Der Configuration Manager-Client bestimmt automatisch, ob er sich im Intranet oder im Internet befindet. Wenn der Client einen Domänencontroller oder einen lokalen Verwaltungspunkt kontaktieren kann, wird der Verbindungstyp auf **Derzeit Intranet** festgelegt. Andernfalls wechselt er zu **Derzeit Internet** und verwendet den Speicherort des CMG-Diensts für die Kommunikation mit dem Standort.

>[!NOTE]
> Sie können erzwingen, dass der Client immer das CMG verwendet, und zwar unabhängig davon, ob er sich im Intranet oder im Internet befindet. Diese Konfiguration eignet sich für Testzwecke oder für die Clients in Remotebüros, bei denen Sie die Verwendung des CMG erzwingen möchten. Legen Sie folgenden Registrierungsschlüssel für den Client fest:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> Sie können diese Einstellung auch während der Clientinstallation mithilfe der Eigenschaft [CCMALWAYSINF](/sccm/core/clients/deploy/about-client-installation-properties#ccmalwaysinf) angeben.

Öffnen Sie eine Windows PowerShell-Eingabeaufforderung als Administrator auf dem Clientcomputer, und führen Sie den folgenden Befehl aus, um zu überprüfen, ob Clients über die Richtlinie verfügen, in der das CMG angegeben ist: `Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

Dieser Befehl zeigt alle internetbasierten Verwaltungspunkte an, die dem Client bekannt sind. Das CMG ist technisch gesehen kein internetbasierter Verwaltungspunkt, wird Clients jedoch als solcher angezeigt.

 > [!Note]  
 > Verwenden Sie **CMGHttpHandler.log**, **CMGService.log** und **SMS_Cloud_ProxyConnector.log** für die Problembehandlung des CMG-Clientdatenverkehrs. Weitere Informationen finden Sie in den [Protokolldateien](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="modify-a-cmg"></a>Ändern eines CMG

Nach der Erstellung eines CMG können Sie einige der zugehörigen Einstellungen ändern. Wählen Sie das CMG in der Configuration Manager-Konsole aus, und klicken Sie auf **Eigenschaften**. Die folgenden Einstellungen sind konfigurierbar:  

- **Allgemein**  

    - **Azure-Verwaltungszertifikat**: Ändern des Azure-Verwaltungszertifikats für das CMG. Diese Option ist nützlich, wenn das Zertifikat vor Ablauf aktualisiert wird.  

- **Einstellungen**  

    - **Zertifikatsdatei**: Ändern des Serverauthentifizierungszertifikats für das CMG. Diese Option ist nützlich, wenn das Zertifikat vor Ablauf aktualisiert wird.  

    - **VM-Instanz**: Ändern der Anzahl der virtuellen Computer, die der Dienst in Azure verwendet. Mit dieser Einstellung können Sie den Dienst basierend auf Nutzung und Kostenüberlegungen dynamisch hoch- oder herunterskalieren.  

    - **Zertifikate**: Hinzufügen oder Entfernen vertrauenswürdiger Stamm- oder Zwischenzertifizierungsstellenzertifikate Diese Option ist nützlich, wenn neue Zertifizierungsstellen hinzugefügt werden oder abgelaufene Zertifikate zurückgezogen werden.  

    - **Clientzertifikatsperre überprüfen**: Wenn Sie diese Einstellung bei der Erstellung des CMG nicht ursprünglich aktiviert haben, können Sie dies machen, sobald Sie die Zertifikatsperrliste veröffentlicht haben.  

- **Warnungen**: Sie können die Warnungen nach der Erstellung des CMG jederzeit neu konfigurieren. 

Bei wichtigeren Änderungen, wie z.B. den folgenden Konfigurationen, muss der Dienst erneut bereitgestellt werden:
- Klassische Bereitstellungsmethode in Azure Resource Manager
- Abonnement
- Dienstname
- Für öffentliche PKI privat
- Region

Bewahren Sie immer mindestens ein aktives CMG für internetbasierte Clients auf, um die aktualisierte Richtlinie empfangen zu können. Internetbasierte Clients können nicht mit einem entfernten CMG kommunizieren. Client erfahren erst dann von einer neuen Richtlinie, wenn sie ins Intranet wechseln. Bei der Erstellung einer zweiten CMG-Instanz zum Löschen der ersten Instanz müssen Sie auch einen weiteren CMG-Verbindungspunkt erstellen.

Clients aktualisieren eine Richtlinie standardmäßig alle 24 Stunden. Daher sollten Sie mindestens einen Tag nach Erstellung eines neuen CMG warten, bis Sie das alte CMG löschen. Wenn Clients deaktiviert oder ohne Internetverbindung sind, müssen Sie möglicherweise etwas länger warten. 

Ab Version 1802 müssen Sie für die Verwendung der Azure Resource Manager-Bereitstellungsmethode ein neues CMG bereitstellen, wenn Sie über ein vorhandenes CMG der klassischen Bereitstellungsmethode verfügen.<!--509753--> Es stehen zwei Optionen zur Verfügung:
- Wenn Sie den gleichen Dienstnamen wiederverwenden möchten:
    1. Löschen Sie zunächst das klassische CMG, und berücksichtigen Sie dabei die Anweisung, dass immer mindestens ein aktives CMG für internetbasierte Clients vorhanden sein sollte.
    2. Erstellen Sie mithilfe einer Resource Manager-Bereitstellung ein neues CMG. Verwenden Sie dasselbe CMG-Serverauthentifizierungszertifikat wieder.
    3. Konfigurieren Sie den CMG-Verbindungspunkt neu, um die neue CMG-Instanz verwenden zu können.
- Wenn Sie einen neuen Dienstnamen verwenden möchten:
    1. Erstellen Sie mithilfe einer Resource Manager-Bereitstellung ein neues CMG. Verwenden Sie ein neues CMG-Serverauthentifizierungszertifikat.
    2. Erstellen Sie einen neuen CMG-Verbindungspunkt, und verbinden Sie diesen mit dem neuen CMG.
    3. Warten Sie mindestens einen Tag, bis internetbasierte Clients eine Richtlinie zum neuen CMG empfangen.
    4. Löschen Sie das klassische CMG.

Ändern Sie das CMG nur über die Configuration Manager-Konsole. Änderungen an dem Dienst oder zugrunde liegenden VM können nicht direkt in Azure vorgenommen werden. Änderungen gehen möglicherweise ohne Ankündigung verloren. Wie einen PaaS kann der Dienst auch die VM jederzeit neu erstellen. Diese Neuerstellungen können für die Wartung von Back-End-Hardware oder für die Anwendung von Updates für das VM-Betriebssystem erfolgen.

Wenn Sie das CMG löschen müssen, machen Sie auch dies über die Configuration Manager-Konsole. Durch das manuelle Entfernen von Komponenten in Azure wird das System in einen inkonsistenten Zustand versetzt. Dieser Zustand hinterlässt verwaiste Informationen. Zudem kann es zu unerwartetem Verhalten kommen. 



## <a name="next-steps"></a>Nächste Schritte

- [Überwachen von Clients für das Cloudverwaltungsgateway](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway)
- [Frequently asked questions about the cloud management gateway (Häufig gestellte Fragen zu Cloud Management Gateway)](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
