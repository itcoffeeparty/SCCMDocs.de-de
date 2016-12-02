---
title: Erstellen von VPN-Profilen in System Center Configuration Manager
description: Erfahren Sie, wie Sie VPN-Profile in System Center Configuration Manager erstellen.
ms.custom: na
ms.date: 10/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: 15
caps.handback.revision: 0
ms.author: nbigman
ms.manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a65de5feae2ff44f938ce8b7e3c8d23d560bb180
ms.openlocfilehash: bcea8676c163a8aba1bc7f3364fde52375f52429


---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>Erstellen von VPN-Profilen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


> [!NOTE]  
>
> - Informationen zu den für verschiedene Geräteplattformen verfügbaren Verbindungstypen finden Sie unter [VPN-Profile in System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  
> - Verteilen Sie die VPN-App für Drittanbieter-VPN-Verbindungen vor der Bereitstellung des VPN-Profils. Wenn Sie die App nicht bereitstellen, werden die Benutzer dazu aufgefordert, sobald sie versuchen, sich mit dem VPN zu verbinden. Weitere Informationen zum Bereitstellen von Apps finden Sie unter [Bereitstellen von Anwendungen mit System Center Configuration Manager](../../apps/deploy-use/deploy-applications).

### <a name="start-the-create-vpn-profile-wizard"></a>Starten des Assistenten zum Erstellen von VPN-Profilen  

1.  Klicken Sie in der System Center Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** der System Center Configuration Manager-Konsole die **Kompatibilitätseinstellungen** und den **Zugriff auf Unternehmensressourcen**, und klicken Sie anschließend auf **VPN-Profile**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **VPN-Profil erstellen**.  

### <a name="provide-general-information-about-the-vpn-profile"></a>Bereitstellen von allgemeinen Informationen zum VPN-Profil  

1.  Geben Sie auf der Seite **Allgemein** des ** **Assistenten zum Erstellen von VPN-Profilen die folgenden Informationen an:  

    -   **Name** : Geben Sie einen eindeutigen Namen für das VPN-Profil ein (bis zu 256 Zeichen).  

        > [!IMPORTANT]  
        >  Verwenden Sie im Namen des VPN-Profils keines der Zeichen \\/:*?<>&#124;, und auch keine Leerzeichen, da diese Zeichen vom Windows Server-VPN-Profil nicht unterstützt werden.  

    -   **Beschreibung:** Geben Sie eine Beschreibung ein, um das Profil in der System Center Configuration Manager-Konsole leichter zu finden (bis zu 256 Zeichen).  

    -   **Vorhandenes VPN-Profilelement aus einer Datei importieren:** Wenn Sie diese Option auswählen, wird die Seite **VPN-Profil importieren** angezeigt. Auf dieser Seite können Sie VPN-Profilinformationen importieren, die zuvor in eine XML-Datei exportiert wurden (nur Betriebssysteme Windows 8.1 und Windows RT).  

### <a name="provide-connection-information-for-the-vpn-profile"></a>Bereitstellen von Verbindungsinformationen für das VPN-Profil  

1.  Geben Sie auf der Seite **Verbindung** des Assistenten die folgenden Informationen an:  

    -   **Verbindungstyp:** Wählen Sie aus der Dropdownliste den Verbindungstyp für die VPN-Verbindung aus. Sie haben die Auswahl zwischen den Verbindungstypen in der folgenden Tabelle mit unterstützten Plattformen.  

        > [!IMPORTANT]  
        >  Bevor Sie auf einem Gerät bereitgestellte VPN-Profile verwenden können, sollten Sie alle erforderlichen VPN-Apps von Drittanbietern installieren. Informationen zum Bereitstellen der App mithilfe von System Center Configuration Manager finden Sie im Thema [Erstellen von Anwendungen mit System Center Configuration Manager](../../apps/deploy-use/create-applications.md).  

    -   **Serverliste:** Klicken Sie auf **Hinzufügen** , um einen neuen Server zur Verwendung für die VPN-Verbindung hinzuzufügen. Abhängig vom Verbindungstyp können Sie einen oder mehrere VPN-Server hinzufügen. Zudem können Sie kennzeichnen, welcher der angegebenen Server der Standardserver sein soll.  

        > [!NOTE]  
        >  Von iOS-Geräten wird die Verwendung mehrerer VPN-Server nicht unterstützt. Wenn Sie mehrere VPN-Server konfigurieren und dann das VPN-Profil auf einem iOS-Gerät bereitstellen, wird nur der Standardserver verwendet.  

     Abhängig vom ausgewählten Verbindungstyp werden die weiteren Optionen in der folgenden Tabelle möglicherweise angezeigt. Weitere Informationen finden Sie in der Dokumentation zum VPN-Server.  

    |Option|Weitere Informationen|Verbindungstyp|  
    |------------|----------------------|---------------------|  
    |**Bereich**|Geben Sie den Namen des gewünschten Authentifizierungsbereichs an. Ein Authentifizierungsbereich ist eine Gruppe von Authentifizierungsressourcen, die vom Verbindungstyp „Pulse Secure“ verwendet werden.|Pulse Secure|  
    |**Rolle**|Geben Sie den Namen der Benutzerrolle an, die Zugriff auf diese Verbindung hat.|Pulse Secure|  
    |**Anmeldegruppe oder Domäne**|Geben Sie den Namen der Anmeldegruppe oder Domäne an, mit der Sie eine Verbindung herstellen möchten.|Dell SonicWALL Mobile Connect|  
    |**Fingerabdruck**|Geben Sie eine Zeichenfolge wie z. B. „Contoso-Fingerabdruckcode“ an, anhand der überprüft wird, ob der VPN-Server vertrauenswürdig ist.<br /><br /> Mit einem Fingerabdruck kann wie folgt verfahren werden:<br /><br /> – Er kann an den Client gesendet werden, damit dieser weiß, dass alle Server vertrauenswürdig sind, die beim Verbinden den betreffenden Fingerabdruck vorweisen.<br /><br /> – Wenn das Gerät noch nicht über den Fingerabdruck verfügt, wird der Benutzer aufgefordert, dem VPN-Server zu vertrauen, mit dem Verbindung hergestellt wird, während der Fingerabdruck angezeigt wird (der Benutzer überprüft den Fingerabdruck manuell und klickt auf „Vertrauen“, um die Verbindung herzustellen).|Prüfpunkt für mobiles VPN|  
    |**Gesamten Netzwerkdatenverkehr über die VPN-Verbindung senden**|Wenn diese Option nicht ausgewählt ist, können Sie zusätzliche Routen für die Verbindung angeben (für die Verbindungstypen **Microsoft SSL (SSTP)**, **Microsoft Automatic**, **IKEv2**, **PPTP** und **L2TP** ). Dies wird auch als getrenntes Tunneln oder VPN-Tunneln bezeichnet.<br /><br /> Nur Verbindungen mit dem Unternehmensnetzwerk werden über einen VPN-Tunnel gesendet. Beim Verbinden mit Ressourcen im Internet wird VPN-Tunneln nicht verwendet.|Alle|  
    |**Verbindungsspezifisches DNS-Suffix**|Geben Sie optional das verbindungsspezifische DNS-Suffix (Domain Name System) für die Verbindung an.|- <br />                            Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> - <br />                            IKEv2<br /><br /> - <br />                            PPTP<br /><br /> - <br />                            L2TP|  
    |**VPN beim Verbinden mit Unternehmens-WLAN-Netzwerk umgehen**|Gibt an, dass die VPN-Verbindung nicht verwendet wird, wenn das Gerät mit dem Unternehmens-WLAN verbunden ist.|– Cisco AnyConnect<br /><br /> – Pulse Secure<br /><br /> – F5 Edge Client<br /><br /> – Dell SonicWALL Mobile Connect<br /><br /> – Prüfpunkt für mobiles VPN<br /><br /> – Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – IKEv2<br /><br /> – L2TP|  
    |**VPN beim Verbinden mit WLAN-Heimnetzwerk umgehen**|Gibt an, dass die VPN-Verbindung nicht verwendet wird, wenn das Gerät mit einem WLAN-Heimnetzwerk verbunden ist.|Alle|  
    |**VPN pro App (iOS 7 und höher, Mac OS X 10.9 und höher)**|Mit dieser Option können Sie diese VPN-Verbindung einer iOS-App zuzuordnen, sodass die Verbindung geöffnet wird, wenn die Anwendung ausgeführt wird. Die Zuordnung des VPN-Profils zu einer App kann bei der Bereitstellung erfolgen.|- <br />                        Cisco AnyConnect<br /><br /> – Pulse Secure<br /><br /> – F5 Edge Client<br /><br /> – Dell SonicWALL Mobile Connect<br /><br /> – Prüfpunkt für mobiles VPN|  
    |**Benutzerdefiniertes XML (optional)**|Ermöglicht Ihnen die Angabe benutzerdefinierter XML-Befehle zum Konfigurieren der VPN-Verbindung.<br /><br /> Beispiele:<br /><br /> Für **Pulse Secure**:<br /><br /> **<pulse-schema><isSingleSignOnCredential\>true</isSingleSignOnCredential\></pulse-schema>**<br /><br /> Für **CheckPoint Mobile VPN**:<br /><br /> **&lt;CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" /\>**<br /><br /> Für **Dell SonicWALL Mobile Connect**:<br /><br /> **<MobileConnect\><Compression\>false</Compression\><debugLogging\>True</debugLogging\><packetCapture\>False</packetCapture\></MobileConnect\>**<br /><br /> Für **F5 Edge Client**:<br /><br /> **&lt;f5-vpn-conf&gt;&lt;single-sign-on-credential /&gt;&lt;/f5-vpn-conf&gt;**<br /><br /> Weitere Informationen über das Schreiben von benutzerdefinierten XML-Befehlen finden Sie in der VPN-Dokumentation der einzelnen Hersteller.|– Cisco AnyConnect<br /><br /> – Pulse Secure<br /><br /> – F5 Edge Client<br /><br /> – Dell SonicWALL Mobile Connect<br /><br /> – Prüfpunkt für mobiles VPN|  

####   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Bei der Verwendung von Configuration Manager mit Intune verfügbare Windows 10-VPN-Features  


> [!NOTE]  
> Der Name eines VPN-Profils mit Windows 10-VPN-Features darf keine Unicode oder Sonderzeichen enthalten.


|Option|Weitere Informationen|Verbindungstyp|  
|------------|----------------------|---------------------|  
|**VPN beim Verbinden mit Unternehmens-WLAN-Netzwerk umgehen**|Gibt an, dass die VPN-Verbindung nicht verwendet wird, wenn das Gerät mit dem Unternehmens-WLAN verbunden ist. Geben Sie den Namen des vertrauenswürdigen Netzwerks ein, das zum Ermitteln verwendet wird, ob das Gerät mit dem Unternehmensnetzwerk verbunden ist.|Alle|  
|**Regeln für den Netzwerkdatenverkehr**|Legen Sie die Protokolle, die lokalen und Remoteports sowie die Adressbereiche fest, die für die VPN-Verbindung aktiviert werden sollen.<br /><br /> **Hinweis:** Wenn Sie keine Regel für den Netzwerkdatenverkehr erstellen, werden alle Protokolle, Ports und Adressbereiche aktiviert. Nachdem Sie eine Regel erstellt haben, werden nur die in dieser oder weiteren Regeln festgelegten Protokolle, Ports und Adressbereiche von der VPN-Verbindung verwendet.|Alle|  
|**Routen**|Die Routen, welche die VPN-Verbindung verwenden. Beachten Sie, dass die Erstellung von mehr als 60 Routen Richtlinienfehler herbeiführen kann. |Alle|  
|**DNS-Server**|Die DNS-Server, die von der VPN-Verbindung verwendet werden, nachdem die Verbindung hergestellt wurde.|Alle|  
|**Apps, die automatisch eine Verbindung mit dem VPN herstellen**|Sie können Apps hinzufügen oder App-Listen importieren, die automatisch die VPN-Verbindung verwenden. Der App-Typ bestimmt den App-Bezeichner. Stellen Sie für eine Desktop-App den Dateipfad der App bereit. Stellen Sie für eine universelle App den Paketfamiliennamen (package family name; PFN) bereit. Informationen dazu, wie Sie den PFN einer App herausfinden, finden Sie unter [Find a package family name for per-app VPN (Suchen eines Paktefamiliennamens für Pro-App-VPN)](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |Alle|

> [!IMPORTANT]
> Es wird empfohlen, alle Listen der zugeordneten Apps zu sichern, die Sie für die Konfiguration des Pro-App-VPN kompilieren. Wenn ein nicht autorisierter Benutzer die Liste ändert und Sie die Liste in die Pro-App-VPN-Liste importieren, gewähren Sie möglicherweise VPN-Zugriff auf Apps, auf die kein Zugriff bestehen sollte. Eine Möglichkeit, die App-Listen zu sichern, besteht in der Verwendung einer Zugriffssteuerungsliste (access control list; ACL).


### <a name="configure-the-authentication-method-for-the-vpn-profile"></a>Konfigurieren der Authentifizierungsmethode für das VPN-Profil  

1.  Geben Sie auf der Seite **Authentifizierungsmethode** des Assistenten die folgenden Informationen an:  

    -   **Authentifizierungsmethode:** Wählen Sie aus der Dropdownliste die Authentifizierungsmethode für die VPN-Verbindung aus. Abhängig vom zuvor ausgewählten Verbindungstyp können die Elemente in der Dropdownliste variieren. In der folgenden Tabelle sind die verfügbaren Authentifizierungsmethoden und die unterstützten Verbindungstypen aufgeführt.  

        |Authentifizierungsmethode|Unterstützte Verbindungstypen|  
        |---------------------------|--------------------------------|  
        |**Zertifikate**<br /><br /> **Hinweis:** Wenn das Clientzertifikat für die Authentifizierung bei einem RADIUS-Server, z.B. ein Netzwerkrichtlinienserver, verwendet wird, muss der alternative Antragstellername im Zertifikat auf den Benutzerprinzipalnamen festgelegt werden.|- <br />                            Cisco AnyConnect<br /><br /> – Pulse Secure<br /><br /> – F5 Edge Client<br /><br /> – Dell SonicWALL Mobile Connect<br /><br /> – Prüfpunkt für mobiles VPN|  
        |**Benutzername und Kennwort**|- <br />                            Pulse Secure<br /><br /> – F5 Edge Client<br /><br /> – Dell SonicWALL Mobile Connect<br /><br /> – Prüfpunkt für mobiles VPN|  
        |**Microsoft EAP-TTLS**|– Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – PPTP<br /><br /> – IKEv2<br /><br /> – L2TP|  
        |**Microsoft-gesichertes EAP (PEAP)**|– Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – IKEv2<br /><br /> – PPTP<br /><br /> – L2TP|  
        |**Microsoft-gesichertes Kennwort (EAP-MSCHAP v2)**|– Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – IKEv2<br /><br /> – PPTP<br /><br /> – L2TP|  
        |**Smartcard- oder anderes Zertifikat**|– Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – IKEv2<br /><br /> – PPTP<br /><br /> – L2TP|  
        |**MSCHAP v2**|– Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – IKEv2<br /><br /> – PPTP<br /><br /> – L2TP|  
        |**RSA SecurID** (nur iOS)|– Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – PPTP<br /><br /> – L2TP|  
        |**Computerzertifikate verwenden**|IKEv2|  

         Je nach ausgewählten Optionen werden Sie möglicherweise gebeten, weitere Informationen wie beispielsweise die folgenden anzugeben:  

        -   **Benutzeranmeldeinformationen bei jeder Anmeldung speichern**: Aktivieren Sie diese Option, um sicherzustellen, dass die Benutzeranmeldeinformationen gespeichert werden, sodass der Benutzer die Anmeldeinformationen nicht bei jeder Verbindungsherstellung erneut eingeben muss.  

        -   **Clientzertifikat für Clientauthentifizierung auswählen** : Wählen Sie das SCEP-Clientzertifikat aus, das Sie zuvor erstellt haben und das zur Authentifizierung der VPN-Verbindung verwendet wird. Weitere Informationen zum Erstellen von Zertifikatprofilen in System Center Configuration Manager finden Sie unter [Zertifikatprofile in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

            > [!NOTE]  
            >  Bei iOS-Geräten wird das von Ihnen ausgewählte SCEP-Profil in das VPN-Profil eingebettet. Bei anderen Plattformen wird eine Anwendbarkeitsregel hinzugefügt, um sicherzustellen, dass das VPN-Profil nicht installiert wird, wenn das Zertifikat nicht vorhanden oder nicht kompatibel ist.  
            >   
            >  Wenn das von Ihnen angegebene SCEP-Zertifikat nicht kompatibel ist oder noch nicht bereitgestellt wurde, wird das VPN-Profil nicht auf dem Gerät installiert.
            >  
            >  Geräte unter iOS unterstützen nur RSA SecurID und MSCHAP v2 als Authentifizierungsmethode, wenn der Verbindungstyp PPTP lautet. Um die Ausgabe von Fehlern zu vermeiden, stellen Sie auf Geräten unter IOS ein separates PPTP-VPN-Profil bereit.  

               - Die Einstellungen für den **bedingten Zugriff** und die **primäre Domäne für den Unternehmensdatenschutz:** Werden nur bei Verwendung von Configuration Manager ohne Intune unterstützt und können über die Option **Erweitert** ausgewählt werden Weitere Informationen zum Unternehmensdatenschutz finden Sie unter [Create a Windows Information Protection (WIP) policy using Microsoft Intune (Erstellen einer Windows Information Protection-Richtlinie (WIP) mit Microsoft Intune)](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).
        
        ![Konfigurieren des bedingten Zugriffs für VPN](../media/vpn-conditional-access.png)

        -   Bei manchen Authentifizierungsmethoden können Sie auf **Konfigurieren** klicken, um das Dialogfeld für Windows-Eigenschaften zu öffnen (falls die Windows-Version, unter der die System Center Configuration Manager-Konsole ausgeführt wird, diese Authentifizierungsmethode unterstützt). Dort können Sie die Eigenschaften der Authentifizierungsmethode konfigurieren.  

### <a name="configure-proxy-settings-for-the-vpn-profile"></a>Konfigurieren von Proxyeinstellungen für das VPN-Profil  

1.  Aktivieren Sie auf der Seite **Proxyeinstellungen** des **Assistenten zum Erstellen von VPN-Profilen**das Kontrollkästchen **Proxyeinstellungen für dieses VPN-Profil konfigurieren** , wenn für Ihre VPN-Verbindung ein Proxyserver verwendet wird.  

2.  Geben Sie Details zu Ihrem Proxyserver und dessen Einstellungen an. Weitere Informationen finden Sie in der Windows Server-Dokumentation.  

> [!NOTE]  
>  Auf Windows 8.1-Computern zeigt das VPN-Profil die Proxyinformationen erst an, wenn Sie mit dem betreffenden Computer eine Verbindung zu dem VPN herstellen.  


### <a name="configure-further-dns-settings-if-required"></a>Konfigurieren weiterer DNS-Einstellungen (falls erforderlich)  
 Auf der Seite **Automatische VPN-Verbindung konfigurieren** des Assistenten können Sie die folgenden Einstellungen konfigurieren:  

-   **VPN bedarfsgesteuert aktivieren:** Wählen Sie diese Option aus, wenn Sie weitere DNS-Einstellungen auf dieser Seite des Assistenten für Windows Phone 8.1-Geräte konfigurieren möchten.

> [!Note]  
> Diese Einstellung gilt nur für Windows Phone 8.1-Geräte und sollte nur auf VPN-Profilen aktiviert werden, die für Windows Phone 8.1-Geräte bereitgestellt werden.


-   DNS-Suffixliste (nur für Windows Phone 8.1-Geräte): Konfiguriert Domänen, die eine VPN-Verbindung herstellen. Fügen Sie für jede Domäne, die Sie angeben, das DNS-Suffix, die DNS-Serveradresse und eine der folgenden bedarfsgesteuerten Aktionen hinzu:  

    -   **Nie herstellen**: Es wird niemals eine VPN-Verbindung geöffnet.  

    -   **Bei Bedarf herstellen**: Es wird nur dann eine VPN-Verbindung geöffnet, wenn das Gerät eine Verbindung zu Ressourcen herstellen muss.  

    -   **Immer herstellen**: Die VPN-Verbindung wird immer geöffnet.  

-   **Zusammenführen**: Kopiert jedes von Ihnen konfigurierte DNS-Suffixe in die **Liste vertrauenswürdiger Netzwerke**.  

-   **Liste vertrauenswürdiger Netzwerke** (nur für Windows Phone 8.1-Geräte): Geben Sie in jeder Zeile ein DNS-Suffix an. Wenn sich das Gerät in einem vertrauenswürdigen Netzwerk befindet, wird die VPN-Verbindung nicht geöffnet.  

-   **Suffixsuchliste** (nur für Windows Phone 8.1-Geräte): Geben Sie in jeder Zeile ein DNS-Suffix an. Jedes angegebene DNS-Suffix wird beim Verbinden mit einer Website unter Verwendung eines Kurznamens gesucht.  

     Beispiel: Sie geben die DNS-Suffixe **domain1.contoso.com** und **domain2.contoso.com** an und besuchen dann die URL **http://mywebsite**. Die folgenden Adressen werden gesucht.  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

> [!NOTE]  
>  Nur für Windows Phone 8.1-Geräte  
>   
>  Wenn die Option **Gesamten Netzwerkdatenverkehr über die VPN-Verbindung senden** ausgewählt ist und die VPN-Verbindung vollständiges Tunneln verwendet, wird beim ersten auf dem Gerät bereitgestellten Profil die VPN-Verbindung automatisch geöffnet. Wenn ein anderes Profil automatisch eine Verbindung öffnen soll, müssen Sie es auf dem Gerät als Standardprofil festlegen.  
>   
>  Wenn die Option **Gesamten Netzwerkdatenverkehr über die VPN-Verbindung senden** nicht ausgewählt ist und die VPN-Verbindung getrenntes Tunneln verwendet, kann eine VPN-Verbindung automatisch geöffnet werden, wenn Sie Routen oder ein verbindungsspezifisches DNS-Suffix konfigurieren.  


### <a name="configure-supported-platforms-for-the-vpn-profile"></a>Konfigurieren unterstützter Plattformen für das VPN-Profil  
 Unterstützte Plattformen sind die Betriebssysteme, unter denen das VPN-Profil installiert wird.  

Wählen Sie auf der Seite **Unterstützte Plattformen** des **Assistenten zum Erstellen von VPN-Profilen**die Betriebssysteme aus, unter denen das VPN-Profil installiert wird, oder klicken Sie auf **Alle auswählen** , um das VPN-Profil unter allen verfügbaren Betriebssystemen zu installieren.  

### <a name="complete-the-wizard"></a>Abschließen des Assistenten  
 Überprüfen Sie auf der Seite **Zusammenfassung** des Assistenten die durchzuführenden Aktionen, und klicken Sie dann auf **Fertig stellen**. Das neue VPN-Profil wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **VPN-Profile** angezeigt.  

### <a name="next-steps"></a>Nächste Schritte

- Verteilen Sie die VPN-App für Drittanbieter-VPN-Verbindungen vor der Bereitstellung des VPN-Profils. Wenn Sie die App nicht bereitstellen, werden die Benutzer dazu aufgefordert, sobald sie versuchen, sich mit dem VPN zu verbinden. Weitere Informationen zum Bereitstellen von Apps finden Sie unter [Bereitstellen von Anwendungen mit System Center Configuration Manager](../../apps/deploy-use/deploy-applications).

- Stellen Sie die VPN-Profile wie in [Erstellen von VPN-Profilen in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md) beschrieben bereit.  



<!--HONumber=Nov16_HO1-->


