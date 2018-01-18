---
title: Clienteinstellungen
titleSuffix: Configuration Manager
description: Auswahl von Clienteinstellungen mithilfe der Verwaltungskonsole in System Center Configuration Manager.
ms.custom: na
ms.date: 01/05/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: "15"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 230d608c9ebc8126d7d8e18f7211875a2155bb7b
ms.sourcegitcommit: ac9268e31440ffe91b133c2ba8405d885248d404
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>Informationen zu Clienteinstellungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwalten Sie alle Clienteinstellungen in der Configuration Manager-Konsole über den Knoten **Clienteinstellungen** im Arbeitsbereich **Verwaltung**. Mit Configuration Manager wird ein Satz Standardeinstellungen geliefert. Wenn Sie die Clientstandardeinstellungen verändern, werden diese Einstellungen auf alle Clients in der Hierarchie angewendet. Sie können auch benutzerdefinierte Clienteinstellungen konfigurieren. Wenn Sie diese Einstellungen Sammlungen zuweisen, werden die Clientstandardeinstellungen überschrieben. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](../../../core/clients/deploy/configure-client-settings.md).  
 

## <a name="background-intelligent-transfer-service"></a>Background Intelligent Transfer Service  

-   **Maximale Netzwerkbandbreite für BITS-Übertragungen im Hintergrund begrenzen**   </br>
   Wenn diese Option auf **Ja** festgelegt ist, verwenden Clients die BITS-Bandbreiteneinschränkung. Sie müssen diese Einstellung aktivieren, um andere Einstellungen in dieser Gruppe zu konfigurieren. 

-   **Beginn des Einschränkungszeitfensters**   </br>
   Geben Sie die lokale Startzeit für das BITS-Einschränkungszeitfenster an.  

-   **Ende des Einschränkungszeitfensters**   </br>
   Geben Sie die lokale Endzeit für das BITS-Einschränkungszeitfenster an. Entspricht dieser Wert dem Wert von **Throttling window start time** (Beginn des Einschränkungszeitfensters), ist die BITS-Einschränkung immer aktiviert.  

-   **Maximale Übertragungsrate während des Einschränkungszeitfensters (KBit/s)** </br>
    Gibt die maximale Übertragungsrate an, die den Clients während des Zeitfensters zur Verfügung steht.  

-   **BITS-Downloads außerhalb des Einschränkungszeitfensters zulassen**   </br>
   Ermöglichen Sie Clients das Verwenden von separaten BITS-Einstellungen außerhalb des angegebenen Zeitfensters.  

-   **Maximale Übertragungsrate außerhalb des Einschränkungszeitfensters (KBit/s)**   </br>
   Geben Sie die maximale Übertragungsrate an, die Clients außerhalb des Zeitfensters der BITS-Bandbreiteneinschränkung verwenden können.  



## <a name="client-cache-settings"></a>Einstellungen des Clientcaches

- **BranchCache konfigurieren** </br>
  Verwenden Sie diese Einstellung, um den Clientcomputer für [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache) einzurichten. Um die BranchCache-Zwischenspeicherung auf dem Client zuzulassen, legen Sie **BranchCache aktivieren** auf **Ja** fest.

    - **BranchCache aktivieren** </br>
    aktiviert BranchCache auf Clientcomputern.

    - **Maximale BranchCache-Cachegröße (Prozentsatz des Datenträgers)** </br>
    Der Prozentsatz des Datenträgers, den BranchCache verwenden kann. 

- **Konfigurieren der Cachegröße des Clients** </br>
  Der Konfigurations-Manager-Clientcache auf Windows-Computern speichert temporäre Dateien, die zum Installieren von Anwendungen und Programmen verwendet werden. Wenn die Option **Nein** festgelegt ist, beträgt die Standardgröße 5.120 MB.</br>
    Klicken Sie auf **Ja**, und geben Sie Folgendes an:
    - **Maximale Cachegröße (MB)**
    - **Maximale Cachegröße (Prozentsatz des Datenträgers)** </br>
    Die Cachegröße kann auf die maximale Größe in Megabyte (MB) oder auf den Prozentsatz des Datenträgers erweitert werden, je nachdem, *welcher Wert kleiner ist*. 

- **Configuration Manager-Client in vollständigem Betriebssystem zur Freigabe von Inhalten aktivieren** </br>
    Aktiviert den [Peercache](/sccm/core/plan-design/hierarchy/client-peer-cache) für Konfigurations-Manager-Clients. Klicken Sie auf **Ja**, und geben Sie dann die Portinformationen ein, über die der Client mit dem Peercomputer kommuniziert. 
    - **Port für erste Netzwerkübertragung** (Standard: 8004)
    - **Port für den Download der Inhalte vom Peer** (Standard: 8003) </br>
    Configuration Manager konfiguriert die Regeln der Windows-Firewall automatisch so, dass dieser Datenverkehr zugelassen wird. Bei Verwendung einer anderen Firewall müssen Sie die Regeln manuell konfigurieren, um diesen Datenverkehr zuzulassen.




## <a name="client-policy"></a>Clientrichtlinie  

-   **Clientrichtlinien-Abrufintervall (Minuten)**  </br>
     Gibt an, wie häufig die Clientrichtlinie von folgenden Konfigurations-Manager-Clients heruntergeladen werden soll:  
      -   Windows-Computer (z. B. Desktops, Server, Laptops)  
      -   Von Configuration Manager registrierte mobile Geräte  
      -   Macintosh-Computer  
      -   Computer, auf denen Linux oder UNIX ausgeführt wird  

-   **Benutzerrichtlinie auf Clients aktivieren**   </br>
   Wenn Sie diese Option auf **Ja** festlegen und die [Benutzerermittlung](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) verwenden, erhalten die Clients die Anwendungen und Programme, die dem angemeldeten Benutzer zugeordnet sind.  

    Der Anwendungskatalog empfängt die Liste der für den Benutzer verfügbaren Software vom Standortserver. Daher muss diese Einstellung für Benutzer nicht auf **Ja** festgelegt werden, um Anwendungen im Anwendungskatalog anzuzeigen und von dort anzufordern. Wenn diese Einstellung auf **Nein** festgelegt ist, funktionieren folgende Verhaltensweisen nicht, wenn Benutzer den Anwendungskatalog verwenden:  

      -   Den Benutzern ist es nicht möglich, die im Anwendungskatalog angezeigten Anwendungen zu installieren.  

      -   Den Benutzern werden keine Benachrichtigungen zu ihren Genehmigungsanforderungen für Anwendungen angezeigt. Sie müssen stattdessen den Anwendungskatalog aktualisieren und den Genehmigungsstatus überprüfen.  

      -   Benutzer erhalten keine Revisionen und Updates für Anwendungen, die im Anwendungskatalog veröffentlicht werden. Den Benutzern werden im Anwendungskatalog jedoch die Änderungen an Anwendungsinformationen angezeigt.  

      -   Wenn Sie eine Anwendungsbereitstellung nach der Installation der Anwendung aus dem Anwendungskatalog entfernen, wird noch bis zu zwei Tage lang von den Clients geprüft, ob die Anwendung installiert ist.  

    Darüber hinaus empfangen Benutzer die erforderlichen Anwendungen nicht, die Sie für Benutzer bereitstellen, wenn diese Einstellung auf **Nein** festgelegt ist. Benutzer erhalten ebenfalls keine anderen Verwaltungsaufgaben in den Benutzerrichtlinien.  

    Diese Einstellung gilt für Benutzer, deren Computer mit dem Intranet und dem Internet verbunden sind. Die Einstellung muss auf **Ja** festgelegt sein, wenn Sie Benutzerrichtlinien im Internet aktivieren möchten.  

-   **Benutzerrichtlinienanforderungen von Internetclients aktivieren**   </br>
   Legen Sie diese Einstellung auf **Ja** fest, damit Benutzer die Benutzerrichtlinie auf internetbasierten Computern empfangen. Folgende Anforderungen müssen ebenfalls erfüllt sein:  

      -   Der Client und der Standort wurden für die internetbasierte Clientverwaltung konfiguriert.

      -   Die Einstellung **Benutzerrichtlinie auf Clients aktivieren** wurde auf **Ja** festgelegt.  

      -   Der Benutzer wird vom internetbasierten Verwaltungspunkt erfolgreich mithilfe der Windows-Authentifizierung (Kerberos oder NTLM) authentifiziert.  

       Wenn Sie diese Option auf **Nein** festlegen oder eine der vorherigen Anforderungen nicht erfüllt ist, empfängt ein internetbasierter Computer nur Computerrichtlinien. In diesem Fall können Benutzer weiterhin Anwendungen über einen internetbasierten Anwendungskatalog anzeigen, anfordern und installieren. Wenn diese Einstellung auf **Nein**, aber **Benutzerrichtlinie auf Clients aktivieren** auf **Ja** festgelegt ist, empfangen Benutzer keine Benutzerrichtlinien, bis der Computer mit dem Intranet verbunden ist.  

       Weitere Informationen zum Verwalten von Clients im Internet finden Sie unter [Überlegungen zur Clientkommunikation aus dem Internet oder einer nicht vertrauenswürdigen Gesamtstruktur](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

      > [!NOTE]  
      >  Genehmigungsanforderungen für Anwendungen von Benutzern erfordern keine Benutzerrichtlinien oder Benutzerauthentifizierung.  


## <a name="cloud-services"></a>Cloud Services

-   **Zugriff auf Cloudverteilungspunkt zulassen** </br>
    Legen Sie diese Einstellung für Clients auf **Ja** fest, um Inhalte von einem Cloudverteilungspunkt abzurufen. Diese Einstellung erfordert keine internetbasierten Geräte.

-    **Registrieren Sie neue, in die Domäne eingebundene Windows 10-Geräte automatisch bei Azure Active Directory.** </br> Wenn Sie Azure Active Directory dafür konfigurieren, hybride Verknüpfungen zu unterstützen, konfiguriert Configuration Manager Windows 10-Geräte für diese Funktionalität. Weitere Informationen finden Sie unter [Konfigurieren von in Azure Active Directory eingebundenen Hybridgeräten](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

-   **Ermöglichen Sie Clients die Verwendung eines Cloudverwaltungsgateways.** </br>
    Standardmäßig verwenden alle Clients für Internetroaming jeden verfügbaren [Cloudverwaltungsgateway](/sccm/core/clients/manage/plan-cloud-management-gateway). Sie müssen diese Einstellung beispielsweise auf **Nein** festlegen, wenn Sie die Nutzung des Diensts während eines Pilotprojekts oder aus Kostengründen einschränken möchten.



##  <a name="compliance-settings"></a>Kompatibilitätseinstellungen  

-   **Konformitätsauswertung auf Clients aktivieren** </br>
    Legen Sie diese Einstellung auf **Ja** fest, um die anderen Einstellungen in dieser Gruppe zu konfigurieren.
 
-   **Konformitätsauswertung planen**   </br>
     Klicken Sie auf **Zeitplan**, um den Standardzeitplan für Bereitstellungen von Konfigurationsbaselines zu erstellen. Dieser Wert kann im Dialogfeld **Konfigurationsbaseline bereitstellen** für jede Baseline konfiguriert werden.  

-   **Benutzerdaten und Profile aktivieren**   </br>
     Wählen Sie **Ja** aus, wenn Sie Konfigurationselemente für [Benutzerdaten und Profile](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) bereitstellen möchten.



## <a name="computer-agent"></a>Computer-Agent  
-   Benutzerbenachrichtigungen für erforderliche Bereitstellungen </br>
    Weitere Informationen zu den folgenden drei Einstellungen finden Sie unter [Benutzerbenachrichtigungen für erforderliche Bereitstellungen](/sccm/apps/deploy-use/deploy-applications#user-notifications-for-required-deployments):
    -   **Bereitstellungsstichtag in mehr als 24 Stunden, Erinnerung alle (Stunden)**
    -   **Bereitstellungsstichtag in weniger als 24 Stunden, Erinnerung alle (Stunden)**  </br>
    -   **Bereitstellungsstichtag in weniger als 1 Stunde, Erinnerung alle (Minuten)**  </br>

-   **Websitepunkt des Standardanwendungskatalogs**   </br>
     Diese Einstellung wird von Configuration Manager verwendet, um Benutzer über das Softwarecenter mit dem Anwendungskatalog zu verbinden. Klicken Sie auf **Website festlegen**, um einen Server festzulegen, der den Anwendungskatalog-Websitepunkt hostet. Geben Sie den NetBIOS-Namen oder den vollqualifizierten Domänennamen des Servers ein, und legen Sie die automatische Erkennung oder eine URL für benutzerdefinierte Bereitstellungen fest. Die automatische Erkennung stellt aus folgenden Gründen meist die beste Lösung dar:  

    -   Clients wird automatisch ein Anwendungskatalog-Websitepunkt von ihrem Standort zugewiesen, sofern ihr Standort über einen Anwendungskatalog-Websitepunkt verfügt.  

    -   Der Client bevorzugt HTTPS-fähige Anwendungskatalog-Websitepunkte im Intranet vor HTTP-Servern. Durch diese Funktion wird der Schutz vor nicht autorisierten Servern verstärkt.

    -   Der Verwaltungspunkt weist internetbasierten Clients einen internetbasierten Anwendungskatalog-Websitepunkt zu. Der Verwaltungspunkt weist intranetbasierten Clients einen intranetbasierten Anwendungskatalog-Websitepunkt zu.  

     Bei der automatischen Ermittlung kann nicht gewährleistet werden, dass Clients der nächstgelegene Anwendungskatalog-Websitepunkt zugewiesen wird. Aus den folgenden Gründen ist die Verwendung von **Automatisch ermitteln** für Ihre Zwecke möglicherweise nicht geeignet:  

     -   Sie möchten den nächstgelegenen Server für Clients manuell konfigurieren oder dafür sorgen, dass die Verbindung mit dem Server nicht über eine langsame Netzwerkverbindung erfolgt.  

     -   Sie möchten steuern, von welchen Clients mit welchen Servern eine Verbindung hergestellt wird. Dies kann zu Testzwecken bzw. aus leistungsbezogenen oder geschäftlichen Gründen erforderlich sein.  

     -   Sie sollten keine 25 Stunden auf eine Netzwerkänderung für Clients warten müssen, um einen anderen Anwendungskatalog-Websitepunkt zu verwenden.  

     Wenn Sie den Anwendungskatalog-Websitepunkt angeben, anstatt die automatische Erkennung zu verwenden, geben Sie anstelle des Intranet-FQDN den NetBIOS-Namen an. Diese Konfiguration verringert die Wahrscheinlichkeit, dass der Webbrowser den Benutzer zum Eingeben von Anmeldeinformationen auffordert, wenn dieser auf einen intranetbasierten Anwendungskatalog zugreift. Sie können den NetBIOS-Namen nur verwenden, wenn die folgenden Bedingungen erfüllt sind:  

     -   Der NetBIOS-Name ist in den Eigenschaften des Anwendungskatalog-Websitepunkts angegeben.  

     -   Sie verwenden WINS, oder alle Clients befinden sich in der gleichen Domäne wie der Anwendungskatalog-Websitepunkt.  

     -   Sie konfigurieren den Anwendungskatalog-Websitepunkt für HTTP- oder den Server für HTTPS-Clientverbindungen. Das Webserverzertifikat enthält den NetBIOS-Namen.  

     Benutzer werden in der Regel zur Eingabe von Anmeldeinformationen aufgefordert, wenn die URL über einen FQDN verfügt. Dies ist nicht der Fall, wenn die URL ein NetBIOS-Name ist. Sie können davon ausgehen, dass Benutzer beim Herstellen einer Verbindung über das Internet immer zur Eingabe von Anmeldeinformationen aufgefordert werden, da für diese Verbindung der Internet-FQDN verwendet werden muss. Wenn ein internetbasierter Client verwendet wird und der Webbrowser den Benutzer zum Eingeben von Anmeldeinformationen auffordert, stellen Sie sicher, dass der Anwendungskatalog-Websitepunkt eine Verbindung zu einem Domänencontroller für das Benutzerkonto herstellen kann. Diese Konfiguration ermöglicht es dem Benutzer, eine Authentifizierung mithilfe von Kerberos durchzuführen.  

    > [!NOTE]  
    >  Funktionsweise der automatischen Erkennung:  
    >   
    >  Vom Client wird eine Dienstidentifizierungsanforderung an einen Verwaltungspunkt gesendet. Wenn es an dem Standort, an dem der Client sich befindet, einen Anwendungskatalog-Websitepunkt gibt, wird der Client angewiesen, diesen Server als Anwendungskatalog-Server zu verwenden. Wenn an dem Standort mehrere Anwendungskatalog-Websitepunkte verfügbar sind, hat ein HTTPS-fähiger Server Vorrang vor einem Server, der nicht für HTTPS aktiviert ist. Nach dieser Filterung wird allen Clients einer der Server als Anwendungskatalog zugewiesen. In Configuration Manager wird kein Lastenausgleich zwischen mehreren Servern ausgeführt. Wenn der Standort des Clients nicht über einen Anwendungskatalog-Websitepunkt verfügt, wird vom Verwaltungspunkt auf nicht deterministische Weise ein Anwendungskatalog-Websitepunkt aus der Hierarchie zurückgegeben.  
    >   
    >  Wenn Sie bei intranetbasierten Clients den Anwendungskatalog-Websitepunkt mit einem NetBIOS-Namen für die URL des Anwendungskatalogs konfigurieren, weist der Verwaltungspunkt den Clients diesen NetBIOS-Namen statt dem vollqualifizierten Domänennamen des Intranets zu. Bei internetbasierten Clients übergibt der Verwaltungspunkt nur den Internet-FQDN an den Client.  
    >   
    >  Diese Dienstidentifizierungsanforderung wird vom Client alle 25 Stunden sowie bei jeder Netzwerkänderung gestellt. Wenn der Client beispielsweise vom Intranet zum Internet verschoben und ein internetbasierter Verwaltungspunkt gefunden wird, werden den Clients vom internetbasierten Verwaltungspunkt Server für internetbasierte Anwendungskatalog-Websitepunkte zugewiesen.  

-   **Standardanwendungskatalog-Website zur Internet Explorer-Zone der vertrauenswürdigen Sites hinzufügen**   </br>
     Wenn diese Option auf **Ja** festgelegt wurde, fügt der Client die aktuelle URL der Website des Anwendungskatalogs automatisch zur Zone der vertrauenswürdigen Websites von Internet Explorer hinzugefügt.  

     Durch diese Einstellung wird sichergestellt, dass die Internet Explorer-Einstellung für Geschützter Modus nicht aktiviert wird. Ist der geschützte Modus aktiviert, können vom Configuration Manager-Client möglicherweise keine Anwendungen aus dem Anwendungskatalog installiert werden. Von der Zone der vertrauenswürdigen Sites wird standardmäßig auch die Benutzeranmeldung beim Anwendungskatalog unterstützt, für die die Windows-Authentifizierung erforderlich ist.  

     Wenn Sie diese Option bei **Nein** belassen, können Konfigurations-Manager-Clients möglicherweise keine Anwendungen aus dem Anwendungskatalog installieren. Eine alternative Methode besteht im Konfigurieren dieser Internet Explorer-Eigenschaften für die URL des Anwendungskatalogs, die Clients verwenden, in einer anderen Zone.  

    > [!NOTE]  
    >  Wenn von Configuration Manager ein Standardanwendungskatalog zur Zone der vertrauenswürdigen Standorte hinzugefügt wird, entfernt Configuration Manager alle zuvor hinzugefügten URLs des Anwendungskatalogs.  
    >   
    >  Wenn die URL bereits in einer der Sicherheitszonen festgelegt ist, kann Configuration Manager diese nicht hinzufügen. In diesem Fall müssen Sie entweder die URL aus der anderen Zone entfernen, oder die erforderlichen Internet Explorer-Einstellungen manuell konfigurieren.  

-   **Ausführen von Silverlight-Anwendungen im Modus mit höherer Vertrauensstellung zulassen**   </br>
     Diese Einstellung muss auf **Ja** festgelegt sein, damit der Anwendungskatalog von Benutzern verwendet werden kann.  

     Eine Änderung dieser Einstellung wird wirksam, wenn Benutzer ihren Browser das nächste Mal laden oder wenn sie das gegenwärtig geöffnete Browserfenster aktualisieren.  

     Weitere Informationen zu dieser Einstellung finden Sie unter [Zertifikate für Microsoft Silverlight 5 und für den Anwendungskatalog erforderlicher Modus mit höherer Vertrauensstellung](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

-   **Im Softwarecenter angezeigter Organisationsname**   </br>
     Geben Sie den Namen ein, den Benutzer im Softwarecenter sehen. Diese Branding-Informationen helfen den Benutzern, diese Anwendung als vertrauenswürdige Quelle zu identifizieren.  

-   **Verwenden des neuen Softwarecenters**   </br>
     Wenn Sie diese Clienteinstellung auf **Ja** festlegen, verwenden alle Clientcomputer das neue Softwarecenter. Das Softwarecenter zeigt für Benutzer verfügbare Apps an, auf die vorher nur im Anwendungskatalog zugegriffen werden konnte. Der Anwendungskatalog erfordert Silverlight. Dies ist jedoch keine Voraussetzung für das neue Softwarecenter.   

     Die Standortsystemrollen „Anwendungskatalog-Websitepunkt“ und „Anwendungskatalog-Webdienstpunkt“ sind nach wie vor erforderlich, damit für Benutzer verfügbare Apps im Softwarecenter angezeigt werden.  

     Weitere Informationen finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Aktivieren Sie die Kommunikation mit dem Integritätsnachweisdienst**  </br>
    Legen Sie diese Einstellung auf **Ja** fest, damit Windows 10-Geräte den [Integritätsnachweis](/sccm/core/servers/manage/health-attestation) verwenden. Wenn Sie diese Einstellung aktivieren, kann folgende Einstellung ebenfalls konfiguriert werden.

    -   **Lokalen Integritätsnachweisdienst verwenden** </br>
        Legen Sie diese Einstellung auf **Ja** fest, damit Geräte einen lokalen Dienst verwenden. Legen Sie diese Einstellung auf **Nein** fest, damit Geräte einen cloudbasierten Microsoft-Dienst verwenden.  

-   **Installationsberechtigungen**   </br>
    > [!WARNING]  
    >  Diese Einstellung gilt für den Anwendungskatalog und das Softwarecenter. Diese Einstellung hat keine Auswirkungen, wenn Benutzer das Unternehmensportal verwenden.  

     Konfigurieren Sie, wie Benutzer die Installation von Software, Softwareupdates und Tasksequenzen initiieren können:  

    -   **Alle Benutzer:** Benutzer mit einer beliebigen Berechtigung (außer „Gast“)  

    -   **Nur Administratoren:** Benutzer müssen Mitglied der lokalen Administratorgruppe sein.  

    -   **Nur Administratoren und primäre Benutzer:** Benutzer müssen Mitglied der lokalen Administratorgruppe oder primärer Benutzer des Computers sein.  

    -   **Keine Benutzer**: Keiner der Benutzer, die sich bei einem Clientcomputer angemeldet haben, kann die Installation von Software, Softwareupdates und Tasksequenzen initiieren. Erforderliche Bereitstellungen für den Computer werden immer am Stichtag installiert. Benutzer können die Installation von Software über den Anwendungskatalog oder das Softwarecenter nicht initiieren.  

-   **BitLocker-PIN-Eingabe bei Neustart anhalten**  </br>
     Wenn die Computer eine BitLocker-PIN-Eingabe erfordern, kann mit dieser Option die notwendige Eingabe einer PIN umgangen werden, wenn der Computer nach der Installation von Software neu gestartet wird.  

    -   **Immer**: BitLocker wird von Configuration Manager nach der Installation von Software, für die ein Neustart erforderlich ist, und der Initiierung eines Computerneustarts vorübergehend ausgesetzt. Diese Einstellung gilt nur, wenn der Neustart eines Computers von Configuration Manager initiiert wird. Wenn der Benutzer den Computer neu startet, ist es trotz dieser Einstellung weiterhin erforderlich, die BitLocker-PIN einzugeben. Die BitLocker-Anforderung zur Eingabe einer PIN wird nach dem Start von Windows wieder eingesetzt.

    -   **Nie**: BitLocker wird von Configuration Manager nach der Installation von Software, für die ein Neustart erforderlich ist, nicht ausgesetzt. In diesem Fall kann die Softwareinstallation erst abgeschlossen werden, wenn der Benutzer die PIN eingibt, um den Standardstartprozess abzuschließen und Windows zu laden.

-   **Bereitstellung von Anwendungen und Softwareupdates wird von zusätzlicher Software verwaltet**  </br>
     Aktivieren Sie diese Option nur, wenn eine der folgenden Bedingungen zutrifft:  

    -   Sie verwenden eine Anbieterlösung, für die diese Einstellung aktiviert werden muss.  

    -   Sie verwalten Client-Agent-Benachrichtigungen und die Installation von Anwendungen und Softwareupdates mit dem Configuration Manager SDK (Software Development Kit).  

    > [!WARNING]  
    >  Wenn Sie diese Option auswählen, obwohl keine dieser Bedingungen erfüllt ist, installiert der Client keine Softwareupdates und keine erforderlichen Anwendungen. Durch diese Einstellung wird nicht verhindert, dass Benutzer Anwendungen über den Anwendungskatalog installieren, oder dass Pakete, Programme und Tasksequenzen installiert werden.  

-   **PowerShell-Ausführungsrichtlinie**  </br>
     Konfigurieren Sie, wie Windows PowerShell-Skripts von Configuration Manager-Clients ausgeführt werden können. Diese Skripts werden oft zur Erkennung von Konformitätseinstellungen in Konfigurationselementen eingesetzt. Sie können aber auch als Standardskripts in einer Bereitstellung gesendet werden.  

    -   **Umgehen**: Die Windows PowerShell-Konfiguration auf dem Clientcomputer wird vom Configuration Manager-Client umgangen, sodass nicht signierte Skripts ausgeführt werden können.  

    -   **Eingeschränkt**: Der Configuration Manager-Client verwendet die aktuelle Windows PowerShell-Konfiguration auf dem Client-Computer. Diese Konfiguration bestimmt, ob nicht signierte Skripts ausgeführt werden können.  

    -   **Alle signiert**: Nur die von einem vertrauenswürdigen Herausgeber signierten Skripts werden vom Configuration Manager-Client ausgeführt. Diese Einschränkung gilt unabhängig von der aktuellen Windows PowerShell-Konfiguration auf dem Clientcomputer.  

     Für diese Option ist mindestens Windows PowerShell 2.0 erforderlich. Der Standardwert ist **Alle Signiert**.  

    > [!TIP]  
    >  Wenn nicht signierte Skripts wegen dieser Clienteinstellung nicht ausgeführt werden können, wird dieser Fehler von Configuration Manager wie folgt gemeldet:  
    >   
    > -   Der Arbeitsbereich **Überwachung** in der Konsole zeigt die Fehler-ID **0x87D00327** für den Bereitstellungsstatus und die Beschreibung **Das Skript wurde nicht signiert.** an.  
    > -   In den Berichten wird der Fehlertyp **Ermittlungsfehler** und entweder der Fehlercode **0x87D00327** und die Beschreibung **Das Skript wurde nicht signiert.** oder der Fehlercode **0x87D00320** und die Beschreibung **Der Skripthost wurde noch nicht installiert.** angezeigt. Einen Beispielbericht finden Sie unter **Details zu Fehlern von Konfigurationselementen in einer Konfigurationsbaseline für einen Bestand**.  
    > -   Die Datei **DcmWmiProvider.log** zeigt die Meldung **Das Skript wurde nicht signiert. (Fehler: 87D00327; Quelle: CCM)** an.  

-   **Benachrichtigung für neue Bereitstellungen anzeigen**  </br>
     Wählen Sie **Ja** aus, um eine Benachrichtigung für Bereitstellungen anzuzeigen, die seit weniger als einer Woche verfügbar sind.  Diese Nachricht wird jedes Mal angezeigt, wenn der Client-Agent gestartet wird.

-   **Zufällige Stichtaganordnung deaktivieren**  </br>
     Nach dem Stichtag der Bereitstellung bestimmt diese Einstellung, ob der Client eine Aktivierungsverzögerung von bis zu zwei Stunden verwendet, um erforderliche Softwareupdates zu installieren. Die Aktivierungsverzögerung ist standardmäßig deaktiviert.  

     Bei Szenarios für virtuelle Desktopinfrastrukturen (VDI) können durch diese Verzögerung die Prozessorauslastung und die Datenübertragung für einen Hostcomputer auf mehrere virtuelle Computer verteilt werden. Selbst wenn Sie VDI nicht verwenden und die gleichen Updates von vielen Clients gleichzeitig installiert werden, kann dies zu einer negativen Steigerung der CPU-Auslastung auf dem Standortserver führen. Außerdem kann es durch dieses Verhalten zu einer Verlangsamung der Verteilungspunkte und einer erheblichen Verringerung der verfügbaren Netzwerkbandbreite kommen.  

     Wenn Clients erforderliche Softwareupdates zum Stichtag der Bereitstellung ohne Verzögerung installieren müssen, legen Sie diese Einstellung auf **Ja** fest. 

-   **Karenzzeit für Erzwingung nach Bereitstellungsfrist (Stunden)** </br>
     Wenn Sie den Benutzern mehr Zeit zum Installieren erforderlicher Anwendungsbereitstellungen oder Softwareupdates vor dem Stichtag gewähren möchten, legen Sie diese Einstellung auf **Ja** fest. Diese Toleranzperiode gilt für einen Computer, der für einen längeren Zeitraum ausgeschaltet ist, und für den der Benutzer viele Anwendungs- oder Updatebereitstellungen installieren muss. Dieser Fall kann eintreten, wenn ein Benutzer beispielsweise aus dem Urlaub zurückkehrt und lange warten muss, während der Client überfällige Anwendungsbereitstellungen installiert. 

     Legen Sie eine Karenzzeit von 1 bis 120 Stunden fest. Verwenden Sie diese Einstellung mit der Bereitstellungseigenschaft **Erzwingung für diese Bereitstellung basierend auf den Benutzereinstellungen innerhalb der Karenzzeit verzögern, die in den Clienteinstellungen definiert ist**. Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](/sccm/apps/deploy-use/deploy-applications).



##  <a name="computer-restart"></a>Computerneustart  
 Die folgende Einstellung muss eine kürzere Dauer als das kürzeste Wartungsfenster aufweisen, das auf den Computer angewendet wird.  

 Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern in System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

-   **Temporäre Benachrichtigung für Benutzer anzeigen, in der auf das Intervall (in Minuten) bis zum Abmelden des Benutzers oder Neustart des Computers hingewiesen wird**
-   **Nicht vom Benutzer schließbares Dialogfeld anzeigen, in der das Countdownintervall (in Minuten) bis zum Abmelden des Benutzers oder Neustart des Computers angezeigt wird**



##  <a name="endpoint-protection"></a>Endpoint Protection  
>  [!Tip]   
> Im [Beispielszenario: Verwenden von System Center Endpoint Protection zum Schutz von Computern vor Schadsoftware in System Center Configuration Manager](/sccm/protect/deploy-use/scenarios-endpoint-protection) finden Sie zusätzlich zu den folgenden Informationen weitere Informationen zur Verwendung der Endpoint Protection-Clienteinstellungen.

-   **Verwalten des Endpoint Protection-Clients auf Clientcomputern**  </br>
     Wählen Sie **Ja** aus, wenn Sie vorhandene Endpoint Protection- und Windows Defender-Clients auf den Computern in Ihrer Hierarchie verwalten möchten.  

     Wählen Sie diese Option aus, wenn der Endpoint Protection-Client bereits installiert ist, und Sie ihn mit Configuration Manager verwalten möchten.  Diese separate Installation umfasst einen skriptgesteuerten Prozess, der eine Anwendung oder ein Paket und ein Programm von Configuration Manager verwendet.

-   **Installieren des Endpoint Protection-Clients auf Clientcomputern**   </br>
     Wählen Sie **Ja** aus, um den Endpoint Protection-Client auf Clientcomputern zu installieren, auf denen der Client noch nicht ausgeführt wird.  

    > [!NOTE]  
    >  Wenn der Endpoint Protection-Client bereits installiert ist, wird dieser durch die Auswahl von **Nein** nicht deinstalliert. Legen Sie zum Deinstallieren des Endpoint Protection-Clients die Clienteinstellung **Endpoint Protection-Client auf Clientcomputern verwalten** auf **Nein** fest. Stellen Sie dann ein Paket und Programm zum Deinstallieren des Endpoint Protection-Clients bereit.  

-   **Vor der Installation von Endpoint Protection zuvor installierte Antischadsoftware anderer Hersteller automatisch entfernen** </br>
    Legen Sie diese Einstellung für den Endpoint Protection-Client auf **Ja** fest, damit versucht wird, andere Antischadsoftwareanwendungen zu deinstallieren. Mehrere Antischadsoftwareclients auf demselben Gerät können zu Konflikten führen und die Systemleistung beeinträchtigen.

-   **Endpoint Protection-Clientinstallation und Neustarts außerhalb der Wartungsfenster zulassen. Wartungsfenster müssen für die Clientinstallation mindestens 30 Minuten lang sein.** </br>
    Legen Sie diese Einstellung auf **Ja** fest, um typische Installationsverhaltensweisen mit Wartungsfenstern zu überschreiben. Diese Einstellung entspricht den geschäftlichen Anforderungen für die Priorität der Systemwartung aus Sicherheitsgründen. 

-   **Für Windows Embedded-Geräte mit Schreibfiltern Commit für Endpoint Protection-Clientinstallation ausführen (hierdurch werden Neustarts erforderlich)**  </br>
     Wählen Sie **Ja** aus, um den Schreibfilter auf dem Windows Embedded-Gerät zu deaktivieren und das Gerät neu zu starten. Hierdurch wird für die Installation auf dem Gerät ein Commit ausgeführt.  

     Wenn Sie diese Einstellung auf **Nein** festlegen, führt der Client die Installation auf einer temporären Überlagerung durch, die bei einem Neustart des Geräts gelöscht wird. In diesem Szenario wird der Endpoint Protection-Client nicht vollständig installiert, bis eine andere Installation Änderungen an das Gerät committet. Dies ist die Standardkonfiguration.  

-   **Erforderliche Neustarts nach der Installation des Endpoint Protection-Clients unterdrücken**  </br>
     Wählen Sie **Ja** aus, um einen Computerneustart zu unterdrücken, falls dies nach der Installation des Endpoint Protection-Clients erforderlich ist.  

    > [!IMPORTANT]  
    >  Wenn der Endpoint Protection-Client einen Computerneustart erfordert und diese Einstellung auf **Nein** festgelegt ist, startet der Computer unabhängig von den konfigurierten Wartungsfenstern neu.  

-   **Zulässiges Zeitintervall (Stunden), um das Benutzer einen für den Abschluss der Installation von Endpoint Protection erforderlichen Neustart verschieben können**  </br>
     Wenn ein Neustart nach der Installation eines Endpoint Protection-Clients erforderlich ist, gibt diese Einstellung an, um wie viele Stunden der Benutzer den erforderlichen Neustart verschieben kann. Für diese Einstellung ist es erforderlich, dass die Einstellung **Erforderliche Neustarts nach der Installation des Endpoint Protection-Clients unterdrücken** auf **Nein** festgelegt ist.  

-   **Alternative Quellen (wie z.B. Microsoft Windows Update, Microsoft Windows Server Update Services oder UNC-Freigaben) für das erste Definitionsupdate auf Clientcomputern deaktivieren**  </br>
     Wählen Sie **Ja** aus, wenn durch Configuration Manager nur das erste Definitionsupdate auf Clientcomputern installiert werden soll. Diese Einstellung kann hilfreich sein, um bei der ersten Installation des Definitionsupdates überflüssige Netzwerkverbindungen zu vermeiden und die Auslastung der Netzwerkbandbreite zu verringern.  



##  <a name="enrollment"></a>Anmeldung

-   **Abrufintervall für Legacyclients mobiler Geräte** </br>
    Klicken Sie auf **Intervall festlegen**, um die Zeitdauer in Minuten oder Stunden festzulegen, für die ältere mobile Geräte Richtlinien abrufen. Zu diesen Geräten zählen Plattformen wie Windows CE, Mac OS X und Unix oder Linux.

-   **Abrufintervall für moderne Geräte (Minuten)** </br>
    Geben Sie die Anzahl von Minuten ein, für die moderne Geräte Richtlinien abrufen. Diese Einstellung gilt für Windows 10-Geräte, die über die lokale Verwaltung mobiler Geräte verwaltet werden.

-   **Benutzern die Anmeldung mobiler Geräte und von Macintosh-Computern gestatten** </br>
    Legen Sie diese Einstellung auf **Ja** fest, und konfigurieren Sie folgende Einstellung, um die benutzerbasierte Registrierung älterer Geräte zu aktivieren:

    -   **Anmeldungsprofil** </br>
        Klicken Sie auf **Profil festlegen**, um ein Registrierungsprofil zu erstellen oder auszuwählen. Weitere Informationen finden Sie unter [Configure client settings for enrollment (Konfigurieren der Clienteinstellungen für die Registrierung)](/sccm/core/clients/deploy/deploy-clients-to-macs#configure-client-settings-for-enrollment).

-   **Benutzern ermöglichen, moderne Geräte anzumelden** </br>
    Legen Sie diese Einstellung auf **Ja** fest, und konfigurieren Sie folgende Einstellung, um die benutzerbasierte Registrierung moderner Geräte zu aktivieren:

    -   **Registrierungsprofil für modernes Gerät** </br>
        Klicken Sie auf **Profil festlegen**, um ein Registrierungsprofil zu erstellen oder auszuwählen. Weitere Informationen finden Sie unter [Erstellen Sie ein Registrierungsprofil, mit dem Benutzer moderne Geräte registrieren können](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm#bkmk_createProf).



##  <a name="hardware-inventory"></a>Hardwareinventur  

-   **Hardwareinventur auf Clients aktivieren** </br>
    Diese Einstellung ist standardmäßig auf **Ja** festgelegt. Weitere Informationen finden Sie unter [Einführung in die Hardwareinventur](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).

-   **Hardwareinventur-Zeitplan** </br>
    Klicken Sie auf **Zeitplan**, um die Häufigkeit anzupassen, mit der Clients den Hardwareinventurzyklus ausführen. Standardmäßig erfolgt dieser Zyklus alle sieben Tage.

-   **Maximale zufällige Verzögerung (Minuten)** </br>
    Geben Sie die maximale Anzahl von Minuten für den Konfigurations-Manager-Client an, um den Hardwareinventurzyklus abweichend vom definierten Zeitplan zufällig festzulegen. Durch diese zufällige Anordnung für alle Clients wird ein Lastenausgleich für die Verarbeitung der Inventur auf dem Standortserver unterstützt. Sie können einen Wert von 0 bis 480 Minuten angeben. Standardmäßig ist dieser Wert auf 240 Minuten (vier Stunden) festgelegt.

-   **Maximale benutzerdefinierte MIF-Dateigröße (KB)**  </br>
     Geben Sie die maximale zulässige Größe einer einzelnen benutzerdefinierten MIF-Datei (Management Information Format) in Kilobyte (KB) an, die ein Client während eines Hardwareinventurzyklus sammelt. Der Hardwareinventur-Agent von Configuration Manager verarbeitet keine benutzerdefinierten MIF-Dateien, die diese Größe überschreiten. Sie können eine Größe von 1 bis 5.120 KB angeben. Standardmäßig ist diese Option auf 250 KB festgelegt. Diese Einstellung wirkt sich nicht auf die Größe der regulären Hardwareinventur-Datendatei aus.  

    > [!NOTE]  
    >  Diese Einstellung ist nur in den Clientstandardeinstellungen verfügbar.  

-   **Hardwareinventurklassen**  </br>
     Klicken Sie auf **Klassen festlegen**, um die von Clients gesammelten Hardwareinformationen ohne manuelles Bearbeiten der Datei „sms_def.mof“ zu erweitern. Weitere Informationen finden Sie unter [Konfigurieren der Hardwareinventur](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **MIF-Dateien sammeln**  </br>
     Mit dieser Einstellung können Sie angeben, ob bei der Hardwareinventur MIF-Dateien von Configuration Manager-Clients gesammelt werden sollen.  

     Damit eine MIF-Datei durch die Hardwareinventur gesammelt werden kann, muss sie sich am korrekten Speicherort auf dem Clientcomputer befinden. Die Dateien befinden sich standardmäßig in folgendem Pfad:  

    -   **IDMIF-Dateien** sollten sich im Ordner „Windows\System32\CCM\Inventory\Idmif“ befinden. 

    -   **NOIDMIF-Dateien** sollten sich im Ordner „Windows\System32\CCM\Inventory\Noidmif“ befinden.

    > [!NOTE]  
    >  Diese Einstellung ist nur in den Clientstandardeinstellungen verfügbar.

   

##  <a name="metered-internet-connections"></a>Getaktete Internetverbindungen  
 Verwalten Sie, wie Computer mit Windows 8 und höher getaktete Internetverbindungen verwenden, um mit Configuration Manager zu kommunizieren. Bei getakteten Internetverbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie senden und empfangen.  

> [!NOTE]  
>  Die konfigurierte Clienteinstellung wird in folgenden Szenarios nicht angewendet:  
>   
> -   Der Computer befindet sich in einer Roamingdatenverbindung: Vom Configuration Manager-Client werden keine Vorgänge ausgeführt, bei denen Daten an Configuration Manager-Standorte übertragen werden müssen.  
> -   Die Eigenschaften der Windows-Netzwerkverbindung sind als nicht getaktet konfiguriert: Der Konfigurations-Manager-Client verhält sich wie bei einer nicht getakteten Verbindung und überträgt dementsprechend Daten an den Standort.  

-   **Clientkommunikation über getaktete Internetverbindungen**  </br>
     Wählen Sie eine der folgenden Optionen für diese Einstellung aus:  

    -   **Zulassen**: Die gesamte Clientkommunikation kann über die getaktete Internetverbindung stattfinden, es sei denn, vom Clientgerät wird eine Roamingdatenverbindung verwendet.  

    -   **Grenzwert**: Nur die folgende Clientkommunikation ist über die getaktete Internetverbindung zulässig:  

        -   Clientrichtlinienabruf  

        -   An den Standort zu sendende Meldungen zum Clientzustand  

        -   Softwareinstallationsanforderungen über den Anwendungskatalog  

        -   Erforderliche Bereitstellungen (bei Erreichen des Installationsstichtags)  

        > [!IMPORTANT]  
        >  Der Client lässt Softwareinstallationen über das Softwarecenter oder den Anwendungskatalog unabhängig von den Einstellungen für die getaktete Internetverbindung immer zu.  

         Wenn das Datenübertragungslimit der getakteten Internetverbindung erreicht wurde, wird vom Client nicht mehr versucht, mit Configuration Manager-Standorten zu kommunizieren.  

    -   **Blockieren**: Vom Configuration Manager-Client wird nicht versucht, mit Configuration Manager-Standorten zu kommunizieren, wenn eine getaktete Internetverbindung vorliegt. Dies ist die Standardoption.  



##  <a name="power-management"></a>Energieverwaltung  

-   **Energieverwaltung von Geräten zulassen** </br>
    Legen Sie diese Einstellung auf **Ja** fest, um die Energieverwaltung auf Clients zu aktivieren. Weitere Informationen finden Sie unter [Einführung in die Energieverwaltung](/sccm/core/clients/manage/power/introduction-to-power-management).

-   **Benutzern das Ausschließen ihres Geräts aus der Energieverwaltung gestatten**  </br>
     Wählen Sie **Ja** aus, damit Softwarecenter-Benutzer ihre Computer von den konfigurierten Energieverwaltungseinstellungen ausschließen können.  

-   **Aktivierungsproxy zulassen** </br> 
     Geben Sie **Ja** an, um die Wake-On-LAN-Einstellung des Standorts zu ergänzen, wenn diese für Unicastpakete konfiguriert ist.  

     Weitere Informationen zum Aktivierungsproxy finden Sie unter [Plan how to wake up clients in System Center Configuration Manager (Planen der Aktivierung von Clients in System Center Configuration Manager)](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  Machen Sie sich mit der Funktionsweise eines Aktivierungsproxys vertraut, und bewerten Sie ihn in einer Testumgebung, bevor Sie ihn in einem Produktionsnetzwerk aktivieren.  

    Konfigurieren Sie dann bei Bedarf folgende zusätzliche Einstellungen:

    -   **Portnummer für Aktivierungsproxy (UDP)**  </br>
         Die Portnummer, die Clients verwenden, um Aktivierungspakete an Computer im Energiesparmodus zu senden. Behalten Sie den Standardport 25536 bei, oder ersetzen Sie die Nummer durch einen beliebigen Wert.  

    -   **Wake-On-LAN-Portnummer (UDP)** </br> 
         Behalten Sie den Standardwert 9 bei, es sei denn, Sie haben die Wake-On-LAN-Portnummer (UDP) in den **Eigenschaften** des Standorts auf der Registerkarte **Ports** geändert.  

        > [!IMPORTANT]  
        >  Dieser Wert muss mit dem Wert in den **Eigenschaften**des Standorts übereinstimmen. Wenn Sie den Wert an einem Ort ändern, wird er am anderen Ort nicht automatisch aktualisiert.  

    -   **Windows Defender Firewall-Ausnahme für Aktivierungsproxy** </br>
         Der Konfigurations-Manager-Client konfiguriert die Portnummer des Aktivierungsproxys automatisch auf Geräten, die Windows Defender Firewall ausführen. Klicken Sie auf **Konfigurieren**, um die gewünschten Firewallprofile anzugeben.

        Falls auf Clients eine andere Firewall ausgeführt wird, müssen Sie diese manuell so konfigurieren, dass die **Portnummer des Aktivierungsproxys (UDP)** zugelassen wird.  
        
    -   **IPv6-Präfixe, sofern für DirectAccess oder andere zwischengeschaltete Netzwerkgeräte erforderlich. Verwenden Sie ein Komma, um mehrere Einträge anzugeben.** </br>
        Geben Sie die notwendigen IPv6-Präfixe für den Aktivierungsproxy ein, damit dieser in Ihrem Netzwerk funktioniert.



##  <a name="remote-tools"></a>Remotetools  

-   **Remotesteuerung auf Clients aktivieren** mit der Beschreibung **Firewallausnahmeprofile**  </br>
     Klicken Sie auf **Konfigurieren**, um die Remotesteuerungsfunktion von Configuration Manager zu aktivieren. Konfigurieren Sie optional die Firewall-Einstellungen zum Zulassen der Remotesteuerung auf Clientcomputern.  

     Die Remotesteuerung ist standardmäßig deaktiviert.  

    > [!IMPORTANT]  
    >  Wenn die Firewall-Einstellungen nicht konfiguriert werden, funktioniert die Remotesteuerung möglicherweise nicht ordnungsgemäß.  

-   **Benutzer können Richtlinien- oder Benachrichtigungseinstellungen im Softwarecenter ändern**  </br>
     Wählen Sie aus, ob Benutzer die Remotesteuerungsoptionen im Softwarecenter ändern können.  

-   **Remotesteuerung eines unbeaufsichtigten Computers zulassen**  </br>
     Wählen Sie aus, ob ein Administrator die Remotesteuerung verwenden kann, um auf einen abgemeldeten oder gesperrten Computer zuzugreifen. Wenn diese Option deaktiviert ist, können nur angemeldete und nicht gesperrte Computer remote gesteuert werden.  

-   **Benutzer zur Vergabe der Berechtigung für Remotesteuerung auffordern**  </br>
     Wählen Sie aus, ob vom Clientcomputer eine Meldung angezeigt werden soll, in der die Zustimmung des Benutzers angefordert wird, bevor eine Remotesteuerungssitzung zugelassen wird.  

-   **Benutzer zum Erteilen der Berechtigung zur Übertragung von Inhalten aus der freigegebenen Zwischenablage auffordern** </br>
    Geben Sie Benutzern die Möglichkeit, Datenübertragungen zu akzeptieren oder zu verweigern, bevor Inhalt aus der freigegebenen Zwischenablage in einer Remotesteuerungssitzung übertragen wird. Benutzer müssen nur einmal pro Sitzung die Berechtigung erteilen, und die anzeigenden Benutzer können sich nicht selbst die Erlaubnis erteilen, mit der Datenübertragung fortzufahren.

-   **Der lokalen Administratorgruppe Berechtigung zur Remotesteuerung gewähren**  </br>
     Wählen Sie aus, ob lokale Administratoren auf dem Server, von dem die Remotesteuerungsverbindung initiiert wurde, Remotesteuerungssitzungen auf Clientcomputern herstellen können.  

-   **Zulässige Zugriffsstufe**  </br>
     Geben Sie die zulässige Zugriffsstufe für die Remotesteuerung an. Wählen Sie eine der folgenden Einstellungen aus:  
    - **Kein Zugriff**
    - **Nur anzeigen**
    - **Vollzugriff**  

-   **Zugelassene Viewer für Remotesteuerung und Remoteunterstützung**  </br>
     Klicken Sie auf **Betrachter festlegen**, um die Namen der Windows-Benutzer anzugeben, die Remotesteuerungssitzungen auf Clientcomputern herstellen können.  

-   **Benachrichtigungssymbol für Sitzung auf Taskleiste anzeigen**  </br>
     Legen Sie diese Einstellung auf **Ja** fest, um ein Symbol für eine aktive Remotesteuerungssitzung auf der Windows-Taskleiste des Clients anzuzeigen.  

-   **Sitzungsverbindungsleiste anzeigen**  </br>
     Legen Sie diese Einstellung auf **Ja** fest, um eine deutlich sichtbare Sitzungsverbindungsleiste auf Clients anzuzeigen, die eine aktive Remotesteuerungssitzung angibt.  

-   **Sound auf Client wiedergeben**  </br>
     Legen Sie diese Einstellung fest, damit über einen Sound angegeben wird, dass eine Remotesteuerungssitzung auf einem Clientcomputer aktiv ist. Wählen Sie eine der folgenden Optionen aus:
    - **Kein Sound**
    - **Beginning and send of session** (Am Anfang und Ende der Sitzung) (Standardeinstellung)
    - **Wiederholt während der Sitzung**  

-   **Einstellungen für nicht angeforderte Remoteunterstützung verwalten**  </br>
     Legen Sie diese Einstellung auf **Ja** fest, um die Verwaltung nicht angeforderter Remoteunterstützungssitzungen durch Configuration Manager zuzulassen.  

     Bei nicht angeforderten Remoteunterstützungssitzungen hat der Benutzer am Clientcomputer keine Unterstützung zum Initiieren einer Sitzung angefordert.  

-   **Einstellungen für angeforderte Remoteunterstützung verwalten**  </br>
     Legen Sie diese Einstellung auf **Ja** fest, um die Verwaltung angeforderter Remoteunterstützungssitzungen durch Configuration Manager zuzulassen.  

     Bei angeforderten Remoteunterstützungssitzungen hat der Benutzer am Clientcomputer Unterstützung zum Initiieren einer Sitzung angefordert.  

-   **Zugriffsstufe für Remoteunterstützung**  </br>
     Wählen Sie die Zugriffsstufe für Remoteunterstützungssitzungen aus, die über die Configuration Manager-Konsole initiiert werden.  Wählen Sie eine der folgenden Optionen aus:
    - **Keine** (Standard)
    - **Remoteansicht**
    - **Vollzugriff**

    > [!NOTE]  
    >  Vor jeder Remoteunterstützungssitzung muss der Benutzer am Clientcomputer dafür die Berechtigung gewähren.  

-   **Einstellungen für Remotedesktop verwalten**  </br>
     Legen Sie diese Einstellung auf **Ja** fest, um die Verwaltung von Remotedesktopsitzungen für Computer durch Configuration Manager zuzulassen.  

-   **Zugelassenen Betrachtern das Herstellen einer Verbindung über Remotedesktopverbindung erlauben**  </br>
     Legen Sie diese Einstellung auf **Ja** fest, um Benutzer, die in der Liste der zugelassenen Betrachter angegeben sind, zur lokalen Remotedesktop-Benutzergruppe auf Clients hinzuzufügen.  

-   **Bei Computern mit Windows Vista oder höher Authentifizierung auf Netzwerkebene verlangen**  </br>
     Legen Sie diese Einstellung auf **Ja** fest, um die Authentifizierung auf Netzwerkebene (NLA) zum Herstellen von Remotedesktopverbindungen mit Clientcomputern zu verwenden. Für die Authentifizierung auf Netzwerkebene werden anfangs weniger Remotecomputerressourcen verbraucht, da die Benutzerauthentifizierung abgeschlossen ist, bevor eine Remotedesktopverbindung hergestellt wird. Die Verwendung von NLA stellt eine sicherere Konfiguration dar. Durch NLA kann der Computer vor böswilligen Benutzern oder Schadsoftware besser geschützt werden, und das Risiko von DoS-Angriffen wird verringert.  



## <a name="software-center"></a>Software Center

-   **Wählen Sie diese neuen Einstellungen aus, um Unternehmensinformationen anzugeben** </br>
    Legen Sie diese Einstellung auf **Ja** fest, und geben Sie dann folgende Einstellungen an, um das Softwarecenter für Ihre Organisation zu kennzeichnen:

    - **Firmenname** </br>
        Geben Sie den Namen der Organisation ein, der Benutzern im Softwarecenter angezeigt wird.
    - **Farbschema für Softwarecenter** </br>
        Klicken Sie auf **Farbe auswählen**, um die vom Softwarecenter verwendete primäre Farbe zu definieren.
    - **Logo für Softwarecenter auswählen** </br>
        Klicken Sie auf **Durchsuchen**, um ein Bild auszuwählen, das im Softwarecenter angezeigt werden soll. Das Logo muss eine JPEG-, PNG oder BMP-Datei mit 400 × 100 Pixeln und einer Größe von maximal 750 KB sein. Der Dateiname des Logos darf keine Leerräume enthalten. <!--SMS.503731 space in filename, noticed BMP missing as filetype-->

-   Sichtbarkeit der Registerkarten im Softwarecenter </br>
    Legen Sie die zusätzlichen Einstellungen in dieser Gruppe auf **Ja** fest, um folgende Registerkarten im Softwarecenter anzuzeigen:
    - **Anwendungen**
    - **Updates**
    - **Betriebssysteme**
    - **Installationsstatus**
    - **Gerätekonformität**
    - **Optionen**

    Wenn Ihre Organisation beispielsweise keine Konformitätsrichtlinien verwendet und Sie die Registerkarte „Gerätekonformität“ im Softwarecenter ausblenden möchten, legen Sie die Einstellung **Registerkarte „Gerätekonformität“ aktivieren** auf **Nein** fest.



## <a name="software-deployment"></a>Softwarebereitstellung  

-   **Erneute Auswertung für Bereitstellungen planen**  </br>
     Konfigurieren Sie einen Zeitplan für die Neuauswertung der Anforderungsregeln für alle Bereitstellungen durch Configuration Manager. Diese erfolgt standardmäßig alle sieben Tage.  

    > [!IMPORTANT]  
    >  Es wird empfohlen, diesen Wert nicht auf einen niedrigeren Wert als den Standardwert zu ändern. Ein aggressiverer Zeitplan für die erneute Auswertung wirkt sich negativ auf die Leistung Ihrer Netzwerk- und Clientcomputer aus.  

     Initiieren Sie diese Aktion auf einem Client, indem Sie auf der Registerkarte **Aktionen** der **Configuration Manager**-Systemsteuerung **Evaluationszyklus für die Anwendungsbereitstellung** auswählen.  



##  <a name="software-inventory"></a>Softwareinventur  

-   **Softwareinventur auf Clients aktivieren** </br>
    Diese Einstellung ist standardmäßig auf **Ja** festgelegt. Weitere Informationen finden Sie unter [Einführung in die Softwareinventur](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

-   **Softwareinventur- und Dateisammlung planen** </br>
    Klicken Sie auf **Zeitplan**, um die Häufigkeit anzupassen, mit der Clients die Zyklen für die Softwareinventur- und Dateisammlung ausführen. Standardmäßig erfolgt dieser Zyklus alle sieben Tage.

-   **Inventurberichtsdetail**  </br>
     Geben Sie eine der folgenden Ebenen der zu inventarisierenden Dateiinformationen an:
    - **Nur Datei**
    - **Nur Produkt**
    - **Vollständige Details** (Standardeinstellung)

-   **Diese Dateitypen inventarisieren**  </br>
     Wenn Sie die Typen der zu inventarisierenden Dateien festlegen möchten, klicken Sie auf **Typen festlegen**, und konfigurieren Sie dann folgende Optionen:  

    > [!NOTE]  
    >  Wenn mehr als eine benutzerdefinierte Clienteinstellung auf einen Computer angewendet wurde, werden die von allen Einstellungen zurückgegebenen Inventare zusammengeführt.  

    -   Klicken Sie auf das Symbol **Neu**, um einen neuen Dateityp zum Inventar hinzuzufügen. Geben Sie anschließend im Dialogfeld **Eigenschaften für inventarisierte Datei(en)** die folgenden Informationen an:  

        -   **Name**: Geben Sie einen Namen für die Datei an, die Sie inventarisieren möchten. Verwenden Sie ein Sternchen (*****) als Platzhalter, um eine beliebige Textzeichenfolge darzustellen, und ein Fragezeichen (**?**), um ein beliebiges einzelnes Zeichen darzustellen. Geben Sie als Dateinamen z.B. **\*.doc** an, um alle Dateien mit der Erweiterung „.doc“ zu inventarisieren.  

        -   **Ort:** Klicken Sie auf **Festlegen**, um das Dialogfeld **Pfadeigenschaften** zu öffnen. Konfigurieren Sie die Softwareinventur so, dass alle Clientfestplatten nach der angegebenen Datei, nach einem angegebenen Pfad (z.B. **C:\Ordner**) oder nach einer angegebenen Variablen (z.B. *%windir%*) durchsucht werden. Sie können auch alle Unterordner unter dem angegebenen Pfad durchsuchen.  

        -   **Verschlüsselte und komprimierte Dateien ausschließen:** Wenn Sie diese Option aktivieren, werden keine komprimierten oder verschlüsselten Dateien inventarisiert.  

        -   **Dateien im Windows-Ordner ausschließen:** Wenn Sie diese Option aktivieren, werden keine Dateien im Windows-Ordner und in dessen Unterordnern inventarisiert.  

    -   Klicken Sie auf **OK** , um das Dialogfeld **Eigenschaften für inventarisierte Datei(en)** zu schließen.  

    -   Fügen Sie alle zu inventarisierenden Dateien hinzu, und klicken Sie dann auf **OK**, um das Dialogfeld **Clienteinstellung konfigurieren** zu schließen.  

-   **Dateien sammeln**  </br>
     Wenn Sie Dateien von Clientcomputern sammeln möchten, klicken Sie auf **Dateien festlegen**, und konfigurieren Sie dann folgende Einstellungen:  

    > [!NOTE]  
    >  Wenn mehr als eine benutzerdefinierte Clienteinstellung auf einen Computer angewendet wurde, werden die von allen Einstellungen zurückgegebenen Inventare zusammengeführt.  

    -   Klicken Sie im Dialogfeld **Clienteinstellung konfigurieren** auf das Symbol **Neu**, um eine zu sammelnde Datei hinzuzufügen.  

    -   Geben Sie im Dialogfeld **Eigenschaften für gesammelte Datei(en)** die folgenden Informationen an:  

        -   **Name**: Geben Sie einen Namen für die Datei an, die Sie sammeln möchten. Verwenden Sie ein Sternchen (*****) als Platzhalter, um eine beliebige Textzeichenfolge darzustellen, und ein Fragezeichen (**?**), um ein beliebiges einzelnes Zeichen darzustellen.  

        -   **Ort:** Klicken Sie auf **Festlegen**, um das Dialogfeld **Pfadeigenschaften** zu öffnen. Konfigurieren Sie die Softwareinventur so, dass alle Clientfestplatten nach der zu sammelnden Datei, nach einem angegebenen Pfad (z.B. **C:\Ordner**) oder nach einer angegebenen Variable (z.B. *%windir%*) durchsucht werden. Sie können auch alle Unterordner unter dem angegebenen Pfad durchsuchen.  

        -   **Verschlüsselte und komprimierte Dateien ausschließen:** Wenn Sie diese Option aktivieren, werden keine komprimierten oder verschlüsselten Dateien gesammelt.  

        -   **Dateisammlung beenden, wenn die Gesamtgröße der Dateien folgenden Wert (KB) überschreitet**: Geben Sie die Dateigröße (in KB) an, ab der der Client aufhört, die angegebenen Dateien zu sammeln.  

          > [!NOTE]  
          >  Die fünf zuletzt geänderten Versionen von gesammelten Dateien werden vom Standortserver gesammelt und im Verzeichnis *&lt;ConfigMgr-Installationsverzeichnis\>*\Inboxes\Sinv.box\Filecol gespeichert. Wenn eine Datei seit dem letzten Softwareinventurzyklus nicht geändert wurde, wird die Datei nicht noch einmal gesammelt.  
          >   
          >  Dateien mit mehr als 20 MB werden von der Softwareinventur nicht gesammelt.  
          >   
          >  Im Dialogfeld **Clienteinstellung konfigurieren** wird mit dem Wert **Maximale Größe aller gesammelten Dateien (KB)** die maximale Größe für alle gesammelten Dateien angezeigt. Wenn diese Größe erreicht ist, wird die Dateisammlung beendet. Alle bereits gesammelten Dateien werden beibehalten und an den Standortserver gesendet.  

          > [!IMPORTANT]
          >  Wenn Sie die Softwareinventur so konfigurieren, dass viele große Dateien gesammelt werden, kann diese Konfiguration sich nachteilig auf die Leistung des Netzwerks und Standortservers auswirken.  

        Informationen zum Anzeigen gesammelter Dateien finden Sie unter [Anzeigen des Softwareinventars mit dem Ressourcen-Explorer](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Klicken Sie auf **OK** , um das Dialogfeld **Eigenschaften für gesammelte Datei(en)** zu schließen.  

    -   Fügen Sie alle zu sammelnden Dateien hinzu, und klicken Sie dann auf **OK**, um das Dialogfeld **Clienteinstellung konfigurieren** zu schließen.  

-   **Namen festlegen**  </br>
     Der Softwareinventur-Agent ruft die Hersteller- und Produktnamen aus den Headerinformationen der Datei ab. Diese Namen sind in den Headerinformationen der Datei nicht immer standardisiert. Wenn Sie die Softwareinventur im Ressourcen-Explorer anzeigen, können verschiedene Versionen des gleichen Hersteller- oder Produktnamens auftreten. Klicken Sie auf **Namen festlegen**, und konfigurieren Sie folgende Einstellungen, um diese Anzeigenamen zu standardisieren:  

    -   **Namenstyp**: Von der Softwareinventur werden Informationen zu Herstellern und Produkten gesammelt. Wählen Sie aus, ob Sie die Anzeigenamen für einen **Hersteller** oder für ein **Produkt** konfigurieren möchten.  

    -   **Anzeigename**: Dient zum Festlegen des Anzeigenamens, den Sie anstelle der Namen in der Liste **Inventarisierte Namen** verwenden möchten. Klicken Sie auf das Symbol **Neu**, um einen neuen Anzeigenamen anzugeben.  

    -   **Inventarisierte Namen:** Klicken Sie auf das Symbol **Neu**, um einen inventarisierten Namen hinzuzufügen. Dieser Name wird in der Softwareinventur durch den Namen ersetzt, der in der Liste **Anzeigename** ausgewählt wurde. Sie können mehrere Namen hinzufügen, die ersetzt werden sollen.  



##  <a name="software-metering"></a>Softwaremessung

-   **Softwaremessung auf Clients aktivieren** </br>
    Diese Einstellung ist standardmäßig auf **Ja** festgelegt. Weitere Informationen finden Sie unter [Softwaremessung](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering#configure-software-metering).

-   **Datensammlung planen** </br>
    Klicken Sie auf **Zeitplan**, um die Häufigkeit anzupassen, mit der Clients den Softwaremessungszyklus ausführen. Standardmäßig erfolgt dieser Zyklus alle sieben Tage.



##  <a name="software-updates"></a>Softwareupdates  

-   **Softwareupdates auf Clients aktivieren**  </br>
     Verwenden Sie diese Einstellung, um Softwareupdates auf Configuration Manager-Clients zu aktivieren. Wenn Sie diese Einstellung deaktivieren, werden die vorhandenen Bereitstellungsrichtlinien von Configuration Manager vom Client entfernt. Wenn Sie diese Einstellung wieder aktivieren, wird vom Client die aktuelle Bereitstellungsrichtlinie heruntergeladen.  

    > [!IMPORTANT]  
    >  Wenn Sie diese Einstellung deaktivieren, funktionieren Konformitätsrichtlinien nicht mehr, die auf Softwareupdates basieren.  

-   **Zeitplan für Softwareupdateprüfung**  </br>
     Klicken Sie auf **Zeitplan**, um anzugeben, wie oft der Client eine Konformitätsüberprüfung initiiert. Bei dieser Überprüfung wird der Zustand von Softwareupdates auf dem Client (z.B. „Erforderlich“ oder „Installiert“) bestimmt. Weitere Informationen zur Konformitätsbewertung finden Sie unter [Software updates compliance assessment (Bewertung der Konformität von Softwareupdates)](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

     Diese Überprüfung verwendet standardmäßig einen einfachen Zeitplan und wird alle sieben Tage initiiert. Sie können einen benutzerdefinierten Zeitplan erstellen, um einen exakten Starttag und eine exakte Startzeit anzugeben. Verwenden Sie die koordinierte Weltzeit (Universal Coordinated Time, UTC), und konfigurieren Sie das Wiederholungsintervall für einen bestimmten Tag der Woche.  

    > [!NOTE]  
    >  Wenn Sie ein Intervall von weniger als einem Tag angeben, wird in Configuration Manager automatisch der Standardwert von einem Tag festgelegt.  

    > [!WARNING]  
    >  Die tatsächliche Startzeit auf Clientcomputern ist die Startzeit plus ein zufälliger Zeitraum von maximal zwei Stunden. Durch diese zufällige Anordnung wird verhindert, dass Clientcomputer die Überprüfung initiieren und gleichzeitig eine Verbindung mit dem aktiven Softwareupdatepunkt herstellen.  

-   **Bereitstellungsneuauswertung planen**  </br>
     Klicken Sie auf **Zeitplan**, um zu konfigurieren, wie oft der Client-Agent für Softwareupdates den Installationsstatus der Softwareupdates auf Konfigurations-Manager-Clientcomputern neu bewertet. Wenn bereits installierte Softwareupdates nicht mehr auf Clientcomputern vorhanden, aber weiterhin erforderlich sind, werden diese durch den Client erneut installiert.

     Passen Sie diesen Zeitplan gemäß der Konformitätsrichtlinie für Softwareupdates an, und legen Sie fest, ob Benutzer Softwareupdates deinstallieren können. Jeder Zyklus für eine Neuauswertung der Bereitstellung führt zu Aktivitäten des Netzwerks und des Prozessors des Clientcomputers. Diese Einstellung verwendet standardmäßig einen einfachen Zeitplan und initiiert die Überprüfung der Neuauswertung für die Bereitstellung alle sieben Tage.  

    > [!NOTE]  
    >  Wenn Sie ein Intervall von weniger als einem Tag angeben, wird in Configuration Manager automatisch der Standardwert von einem Tag festgelegt.  

-   **Wenn der Stichtag für eine beliebige Softwareupdatebereitstellung erreicht wird, auch alle anderen Softwarebereitstellungen mit Stichtag innerhalb eines angegebenen Zeitraums installieren**  </br>
     Legen Sie diese Einstellung auf **Ja** fest, um alle Softwareupdates von erforderlichen Bereitstellungen zu installieren, deren Stichtage innerhalb eines angegebenen Zeitraums liegen. Wenn der Stichtag für eine erforderliche Bereitstellung für ein Softwareupdate erreicht wird, initiiert der Client die Installation der Softwareupdates in der Bereitstellung. Diese Einstellung bestimmt, ob Softwareupdates von anderen erforderlichen Bereitstellungen installiert werden sollen, deren Stichtag innerhalb der angegebenen Zeit liegt.  

     Verwenden Sie diese Einstellung, um die Installation von erforderlichen Softwareupdates zu beschleunigen. Diese Einstellung kann ebenfalls die Sicherheit des Clients erhöhen sowie Benachrichtigungen für den Benutzer und Neustarts des Clients reduzieren. Standardmäßig ist diese Einstellung auf **Nein** (nicht aktiviert) festgelegt.  

-   **Alle anstehenden Bereitstellungen mit Stichtag in diesem Zeitraum werden auch installiert**  </br>
     Verwenden Sie diese Einstellung, um den Zeitraum für die vorherige Einstellung anzugeben. Sie können einen Wert von 1 bis 23 Stunden und von 1 bis 365 Tagen eingeben. Standardmäßig ist diese Einstellung auf sieben Tage festgelegt.  

-   **Installation von Express-Installationsdateien auf Clients aktivieren** </br>
    Legen Sie diese Einstellung auf **Ja** fest, um Clients das Verwenden von Express-Installationsdateien zu ermöglichen. Weitere Informationen finden Sie unter [Verwalten von Expressinstallationsdateien für Windows 10-Updates](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

    -   **Port zum Herunterladen von Inhalten für Express-Installationsdateien** </br>
        Diese Einstellung konfiguriert den lokalen Port dafür, dass Expressinhalte durch den HTTP-Listener heruntergeladen werden können. Standardmäßig ist die Einstellung auf 8005 festgelegt. Sie müssen diesen Port nicht in der Clientfirewall öffnen.

-   **Verwaltung des Office 365-Client-Agents aktivieren** </br>
    Verwenden Sie diese Einstellung zum Aktivieren der Verwaltung des Office 365-Client-Agents. Wenn Sie den Wert auf **Ja** festlegen, können Sie Office 365-Installationseinstellungen konfigurieren, Dateien aus Office Content Delivery Networks (CDNs) herunterladen und die Dateien als Anwendung in Configuration Manager bereitstellen. Weitere Informationen finden Sie unter [Verwalten von Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).



## <a name="state-messaging"></a>Zustandsmeldung

-   **Zustandsmeldungs-Berichtszyklus (Minuten)**  </br>
     Gibt an, wie häufig Clients Zustandsmeldungen ausgeben. Diese Einstellung ist standardmäßig auf 15 Minuten festgelegt.



##  <a name="user-and-device-affinity"></a>Affinität zwischen Benutzer und Gerät  

-   **Nutzungsschwellenwert (Minuten) für Affinität zwischen Benutzer und Gerät**  </br>
     Geben Sie die Nutzungsdauer in Minuten an, nach der von Configuration Manager eine Affinität zwischen Benutzer und Gerät erstellt wird.  Standardmäßig ist dieser Wert auf 2880 Minuten (zwei Tage) festgelegt.

-   **Nutzungsschwellenwert (Tage) für Affinität zwischen Benutzer und Gerät**  </br>
     Geben Sie die Anzahl von Tagen an, über die der Client den Schwellenwert für Affinität zwischen Benutzer und Gerät misst.  Standardmäßig beträgt dieser Wert 30 Tage.

    > [!NOTE]  
    >  Legen Sie beispielsweise den **Nutzungsschwellenwert (Minuten) für Affinität zwischen Benutzer und Gerät** auf **60** Minuten und den **Nutzungsschwellenwert (Tage) für Affinität zwischen Benutzer und Gerät** auf **5** Tage fest. Der Benutzer muss das Gerät dann über einen Zeitraum von fünf Tagen jeweils 60 Minuten verwenden, um eine automatische Affinität mit dem Gerät zu erstellen.  

-   **Affinität zwischen Benutzer und Gerät automatisch aus Verwendungsdaten konfigurieren**  </br>
     Wählen Sie **Ja** aus, um eine automatische Affinität zwischen Benutzer und Gerät zu erstellen, die auf den von Configuration Manager gesammelten Verwendungsinformationen basiert.  

-   **Benutzer das Festlegen primärer Geräte gestatten** </br>
    Wenn diese Einstellung auf **Ja** festgelegt ist, können Benutzer eigene primäre Geräte im Softwarecenter identifizieren.



## <a name="windows-analytics"></a>Windows Analytics

Weitere Informationen zu diesen Einstellungen finden Sie unter [Konfigurieren von Clients zum Senden von Daten an Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).
    
