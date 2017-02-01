---
title: Erstellen von VPN-Profilen in System Center Configuration Manager | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie VPN-Profile in System Center Configuration Manager erstellen.
ms.custom: 
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: 15
author: nbigman
caps.handback.revision: 0
ms.author: nbigman
ms.manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8a5dc7361da34f3e6b926acd35c72c0c0767ce70
ms.openlocfilehash: 73b8d28deb6e2c57c92ead2f0fee4d7a2d92f5d4


---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>Erstellen von VPN-Profilen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die für verschiedene Geräteplattformen verfügbaren Verbindungstypen werden unter [VPN-Profile in System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md) beschrieben.  

Verteilen Sie die VPN-App für Drittanbieter-VPN-Verbindungen vor der Bereitstellung des VPN-Profils. Wenn Sie die App nicht bereitstellen, werden die Benutzer dazu aufgefordert, sobald sie versuchen, sich mit dem VPN zu verbinden. Weitere Informationen zum Bereitstellen von Apps finden Sie unter [Bereitstellen von Anwendungen mit System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

### <a name="create-a-vpn-profile"></a>Erstellen eines VPN-Profils   

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Assets and Compliance** (Bestand und Konformität) > **Compliance Settings** (Konformitätseinstellungen) > **Company Resource Access** (Zugriff auf Unternehmensressourcen) > **VPN-Profiles** (VPN-Profile) aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Create VPN Profile** (VPN-Profil erstellen) aus.  


1.  Schließen Sie die Seite **Allgemein** ab. Beachten Sie dabei Folgendes:  

    - Verwenden Sie im Namen des VPN-Profils keines der Zeichen \\/:*?<>&#124;, und auch keine Leerzeichen. Diese Zeichen werden vom Windows Server-VPN-Profil nicht unterstützt.  

     -   Wählen Sie **Import an existing VPN profile item from a file** (Vorhandenes VPN-Profilelement aus einer Datei importieren) aus, um Informationen eines VPN-Profils zu importieren, das in eine XML-Datei exportiert wurde (nur Windows 8.1 oder Windows RT).  

1.  Geben Sie auf der Seite **Verbindung** Folgendes an:  

    -   **Verbindungstyp**: Wählen Sie den VPN-Verbindungstyp aus. Sie können aus den Verbindungstypen in der folgenden Tabelle wählen.  

    -   **Server list** (Serverliste): Fügen Sie einen neuen Server zur Verwendung für die VPN-Verbindung hinzu. Abhängig vom Verbindungstyp können Sie einen oder mehrere VPN-Server hinzufügen und den Standardserver angeben.  

        > [!NOTE]  
        >  Von iOS-Geräten wird die Verwendung mehrerer VPN-Server nicht unterstützt. Wenn Sie mehrere VPN-Server konfigurieren und dann das VPN-Profil auf einem iOS-Gerät bereitstellen, wird nur der Standardserver verwendet.  

     Diese Tabelle bietet Optionen für die Verbindungstypen. Weitere Informationen finden Sie in der Dokumentation zum VPN-Server.  

    |Option|Weitere Informationen|Verbindungstyp|  
    |------------|----------------------|---------------------|  
    |**Bereich**|Der Authentifizierungsbereich, den Sie verwenden möchten. Ein Authentifizierungsbereich ist eine Gruppe von Authentifizierungsressourcen, die vom Verbindungstyp „Pulse Secure“ verwendet werden.|Pulse Secure|  
    |**Rolle**|Die Benutzerrolle, die Zugriff auf diese Verbindung hat.|Pulse Secure|  
    |**Anmeldegruppe oder Domäne**|Der Name der Anmeldegruppe oder Domäne, mit der Sie eine Verbindung herstellen möchten.|Dell SonicWALL Mobile Connect|  
    |**Fingerabdruck**|Eine Zeichenfolge wie z.B. „Contoso-Fingerabdruckcode“, anhand der überprüft wird, ob der VPN-Server vertrauenswürdig ist.<br /><br /> Mit einem Fingerabdruck kann wie folgt verfahren werden:<br /><br /> – Er kann an den Client gesendet werden, damit dieser weiß, dass alle Server vertrauenswürdig sind, die beim Verbinden den betreffenden Fingerabdruck vorweisen.<br /><br /> – Wenn das Gerät nicht über den Fingerabdruck verfügt, wird der Benutzer aufgefordert, dem VPN-Server zu vertrauen, mit dem eine Verbindung hergestellt wird, während der Fingerabdruck angezeigt wird (der Benutzer überprüft den Fingerabdruck manuell und wählt **Vertrauen** aus, um die Verbindung herzustellen).|Prüfpunkt für mobiles VPN|  
    |**Gesamten Netzwerkdatenverkehr über die VPN-Verbindung senden**|Wenn diese Option nicht ausgewählt ist, können Sie zusätzliche Routen für die Verbindung angeben (für die Verbindungstypen **Microsoft SSL (SSTP)**, **Microsoft Automatic**, **IKEv2**, **PPTP** und **L2TP** ). Dies wird auch als getrenntes Tunneln oder VPN-Tunneln bezeichnet.<br /><br /> Nur Verbindungen mit dem Unternehmensnetzwerk werden über einen VPN-Tunnel gesendet. Beim Verbinden mit Ressourcen im Internet wird VPN-Tunneln nicht verwendet.|Alle|  
    |**Verbindungsspezifisches DNS-Suffix**|Das verbindungsspezifische DNS-Suffix (Domain Name System) für die Verbindung.|- <br />                            Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> - <br />                            IKEv2<br /><br /> - <br />                            PPTP<br /><br /> - <br />                            L2TP|  
    |**VPN beim Verbinden mit Unternehmens-WLAN-Netzwerk umgehen**|Die VPN-Verbindung wird nicht verwendet, wenn das Gerät mit dem Unternehmens-WLAN verbunden ist.|– Cisco AnyConnect<br /><br /> – Pulse Secure<br /><br /> – F5 Edge Client<br /><br /> – Dell SonicWALL Mobile Connect<br /><br /> – Prüfpunkt für mobiles VPN<br /><br /> – Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – IKEv2<br /><br /> – L2TP|  
    |**VPN beim Verbinden mit WLAN-Heimnetzwerk umgehen**|Die VPN-Verbindung wird nicht verwendet, wenn das Gerät mit einem WLAN-Heimnetzwerk verbunden ist.|Alle|  
    |**VPN pro App (iOS 7 und höher, Mac OS X 10.9 und höher)**|Ordnet diese VPN-Verbindung einer iOS-App zu, sodass die Verbindung geöffnet wird, wenn die Anwendung ausgeführt wird. Die Zuordnung des VPN-Profils zu einer App kann bei der Bereitstellung erfolgen.|- <br />                        Cisco AnyConnect<br /><br /> – Pulse Secure<br /><br /> – F5 Edge Client<br /><br /> – Dell SonicWALL Mobile Connect<br /><br /> – Prüfpunkt für mobiles VPN|  
    |**Benutzerdefiniertes XML (optional)**|Gibt benutzerdefinierte XML-Befehle zum Konfigurieren der VPN-Verbindung an.<br /><br /> Beispiele:<br /><br /> Für **Pulse Secure**:<br /><br /> **<pulse-schema><isSingleSignOnCredential\>true</isSingleSignOnCredential\></pulse-schema>**<br /><br /> Für **CheckPoint Mobile VPN**:<br /><br /> **&lt;CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" /\>**<br /><br /> Für **Dell SonicWALL Mobile Connect**:<br /><br /> **<MobileConnect\><Compression\>false</Compression\><debugLogging\>True</debugLogging\><packetCapture\>False</packetCapture\></MobileConnect\>**<br /><br /> Für **F5 Edge Client**:<br /><br /> **&lt;f5-vpn-conf&gt;&lt;single-sign-on-credential /&gt;&lt;/f5-vpn-conf&gt;**<br /><br /> Weitere Informationen über das Schreiben von benutzerdefinierten XML-Befehlen finden Sie in der VPN-Dokumentation der einzelnen Hersteller.|– Cisco AnyConnect<br /><br /> – Pulse Secure<br /><br /> – F5 Edge Client<br /><br /> – Dell SonicWALL Mobile Connect<br /><br /> – Prüfpunkt für mobiles VPN|  

    ###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Bei der Verwendung von Configuration Manager mit Intune verfügbare Windows 10-VPN-Features  


    > [!NOTE]  
    > Der Name eines VPN-Profils mit Windows 10-VPN-Features darf keine Unicode oder Sonderzeichen enthalten.


    |Option|Weitere Informationen|Verbindungstyp|  
    |------------|----------------------|---------------------|  
    |**VPN beim Verbinden mit Unternehmens-WLAN-Netzwerk umgehen**|Die VPN-Verbindung wird nicht verwendet, wenn das Gerät mit dem Unternehmens-WLAN verbunden ist. Geben Sie den Namen des vertrauenswürdigen Netzwerks ein, das zum Ermitteln verwendet wird, ob das Gerät mit dem Unternehmensnetzwerk verbunden ist.|Alle|  
    |**Regeln für den Netzwerkdatenverkehr**|Legen Sie die Protokolle, die lokalen und Remoteports sowie die Adressbereiche fest, die für die VPN-Verbindung aktiviert werden sollen.<br /><br /> **Hinweis:** Wenn Sie keine Regel für den Netzwerkdatenverkehr erstellen, werden alle Protokolle, Ports und Adressbereiche aktiviert. Nachdem Sie eine Regel erstellt haben, werden nur die in dieser oder weiteren Regeln festgelegten Protokolle, Ports und Adressbereiche von der VPN-Verbindung verwendet.|Alle|  
    |**Routen**|Die Routen, welche die VPN-Verbindung verwenden. Beachten Sie, dass die Erstellung von mehr als 60 Routen Richtlinienfehler herbeiführen kann. |Alle|  
    |**DNS-Server**|Die DNS-Server, die von der VPN-Verbindung verwendet werden, nachdem die Verbindung hergestellt wurde.|Alle|  
    |**Apps, die automatisch eine Verbindung mit dem VPN herstellen**|Sie können Apps hinzufügen oder App-Listen importieren, die automatisch die VPN-Verbindung verwenden. Der App-Typ bestimmt den App-Bezeichner. Stellen Sie für eine Desktop-App den Dateipfad der App bereit. Stellen Sie für eine universelle App den Paketfamiliennamen (package family name; PFN) bereit. Informationen dazu, wie Sie den PFN einer App herausfinden, finden Sie unter [Find a package family name for per-app VPN (Suchen eines Paktefamiliennamens für Pro-App-VPN)](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |Alle|

    > [!IMPORTANT]
    > Es wird empfohlen, alle Listen der zugeordneten Apps zu sichern, die Sie für die Konfiguration des Pro-App-VPN kompilieren. Wenn ein nicht autorisierter Benutzer die Liste ändert und Sie die Liste in die Pro-App-VPN-Liste importieren, gewähren Sie möglicherweise VPN-Zugriff auf Apps, auf die kein Zugriff bestehen sollte. Eine Möglichkeit, die App-Listen zu sichern, besteht in der Verwendung einer Zugriffssteuerungsliste (access control list; ACL).


1.  Geben Sie auf der Seite **Authentifizierungsmethode** des Assistenten Folgendes an:  

    -   **Authentifizierungsmethode:** Wählen Sie die Authentifizierungsmethode für die VPN-Verbindung aus. Verfügbare Methoden hängen vom Verbindungstyp ab, wie in dieser Tabelle gezeigt.  

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

        -   **Remember the user credentials at each logon** (Benutzeranmeldeinformationen bei jeder Anmeldung speichern): Benutzeranmeldeinformationen werden gespeichert, sodass der Benutzer sie nicht bei jeder Verbindung eingeben muss.  

        -   **Select a client certificate for client authentication** (Clientzertifikat für Clientauthentifizierung auswählen): Wählen Sie das [SCEP-Clientzertifikat aus](introduction-to-certificate-profiles.md), das Sie zuvor erstellt haben, und das zur Authentifizierung der VPN-Verbindung verwendet wird.   

            > [!NOTE]  
            >  Bei iOS-Geräten wird das von Ihnen ausgewählte SCEP-Profil in das VPN-Profil eingebettet. Bei anderen Plattformen wird eine Anwendbarkeitsregel hinzugefügt, um sicherzustellen, dass das VPN-Profil nicht installiert wird, wenn das Zertifikat nicht vorhanden oder nicht kompatibel ist.  
            >   
            >  Wenn das von Ihnen angegebene SCEP-Zertifikat nicht kompatibel ist oder noch nicht bereitgestellt wurde, wird das VPN-Profil nicht auf dem Gerät installiert.
            >  
            >  Geräte unter iOS unterstützen nur RSA SecurID und MSCHAP v2 als Authentifizierungsmethode, wenn der Verbindungstyp PPTP lautet. Um die Ausgabe von Fehlern zu vermeiden, stellen Sie auf Geräten unter IOS ein separates PPTP-VPN-Profil bereit.  

        - **Bedingter Zugriff**
            - Wählen Sie **Enable conditional access for this VPN connection** (Bedingten Zugriff für diese VPN-Verbindung aktivieren) aus, um sicherzustellen, dass Geräte, die eine Verbindung mit dem VPN herstellen, vor der Verbindung auf Konformität mit bedingtem Zugriff getestet werden. Weitere Informationen zu Konformitätsrichtlinien finden Sie unter [Device compliance policies in System Center Configuration Manager (Verwalten von Konformitätsrichtlinien für Geräte in System Center Configuration Manager)](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md)
            - Wählen Sie **Enable single sign-on (SSO) with alternate certificate** (Einmaliges Anmelden (SSO) mit alternativem Zertifikat aktivieren) aus, um ein anderes Zertifikat als das Zertifikat für die VPN-Authentifizierung für die Gerätekonformität auszuwählen. Wenn Sie diese Option wählen, geben Sie **EKU** (durch Komma getrennte Liste) und **Issuer Hash** (Ausstellerhash) an, um das korrekte Zertifikat auszuwählen, dass der VPN-Client suchen soll.

         - **Windows Information Protection**: Geben Sie die vom Unternehmen verwaltete Unternehmensidentität an. Diese ist normalerweise die primäre Domäne Ihres Unternehmens, z.B. *contoso.com*. Sie können mehrere Domänen angeben, die Ihrer Organisation gehören, indem Sie sie durch das Zeichen „|“ trennen. Beispiel: *contoso.com|newcontoso.com*.   
            Weitere Informationen zu Windows Information Protection finden Sie unter [Create a Windows Information Protection (WIP) policy using Microsoft Intune (Erstellen einer Windows Information Protection-Richtlinie (WIP) mit Microsoft Intune)](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Konfigurieren des bedingten Zugriffs für VPN](../media/vpn-conditional-access.png)


        > [!NOTE]  
        >
        >Bei manchen Authentifizierungsmethoden können Sie auf **Konfigurieren** klicken, um das Dialogfeld für Windows-Eigenschaften zu öffnen (falls die Windows-Version, unter der die Configuration Manager-Konsole ausgeführt wird, diese Authentifizierungsmethode unterstützt). Dort können Sie die Eigenschaften der Authentifizierungsmethode konfigurieren.  


1.  Aktivieren Sie auf der Seite **Proxyeinstellungen** des **Assistenten zum Erstellen von VPN-Profilen**das Kontrollkästchen **Proxyeinstellungen für dieses VPN-Profil konfigurieren** , wenn für Ihre VPN-Verbindung ein Proxyserver verwendet wird. Geben Sie dann die Proxyserverinformationen an. Weitere Informationen finden Sie in der Windows Server-Dokumentation.  

    > [!NOTE]  
    >  Auf Windows 8.1-Computern zeigt das VPN-Profil die Proxyinformationen erst an, wenn Sie mit dem betreffenden Computer eine Verbindung zu dem VPN herstellen.  


2. Konfigurieren weiterer DNS-Einstellungen (falls erforderlich)  
 Auf der Seite **Configure Automatic VPN connection (Automatische VPN-Verbindung konfigurieren)** können Sie Folgendes konfigurieren:  

    -   **Enable VPN on-demand** (VPN bedarfsgesteuert aktivieren): Verwenden Sie diese Option, wenn Sie weitere DNS-Einstellungen für Windows Phone 8.1-Geräte konfigurieren möchten. Diese Einstellung gilt nur für Windows Phone 8.1-Geräte und sollte nur auf VPN-Profilen aktiviert werden, die für Windows Phone 8.1-Geräte bereitgestellt werden.

    -   DNS-Suffixliste (nur Windows Phone 8.1-Geräte): Konfiguriert Domänen, die eine VPN-Verbindung herstellen. Fügen Sie für jede Domäne, die Sie angeben, das DNS-Suffix, die DNS-Serveradresse und eine der folgenden bedarfsgesteuerten Aktionen hinzu:  

        -   **Nie herstellen**: Es wird niemals eine VPN-Verbindung geöffnet.  

        -   **Bei Bedarf herstellen**: Es wird nur dann eine VPN-Verbindung geöffnet, wenn das Gerät eine Verbindung zu Ressourcen herstellen muss.  

        -   **Immer herstellen**: Die VPN-Verbindung wird immer geöffnet.  

    -   **Zusammenführen**: Kopiert jedes von Ihnen konfigurierte DNS-Suffixe in die **Liste vertrauenswürdiger Netzwerke**.  

    -   **Trusted network list** (Liste vertrauenswürdiger Netzwerke) (nur Windows Phone 8.1-Geräte): Geben Sie in jeder Zeile ein DNS-Suffix an. Wenn sich das Gerät in einem vertrauenswürdigen Netzwerk befindet, wird die VPN-Verbindung nicht geöffnet.  

    -   **Suffix search list** (Suffixsuchliste) (nur Windows Phone 8.1-Geräte): Geben Sie in jeder Zeile ein DNS-Suffix an. Jedes DNS-Suffix wird beim Verbinden mit einer Website unter Verwendung eines Kurznamens gesucht.  

     Beispiel: Sie geben die DNS-Suffixe **domain1.contoso.com** und **domain2.contoso.com** an und besuchen dann die URL **http://mywebsite**. Die folgenden Adressen werden gesucht.  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  Nur für Windows Phone 8.1-Geräte  
    >   
    >  Wenn die Option **Gesamten Netzwerkdatenverkehr über die VPN-Verbindung senden** ausgewählt ist und die VPN-Verbindung vollständiges Tunneln verwendet, wird beim ersten auf dem Gerät bereitgestellten Profil die VPN-Verbindung automatisch geöffnet. Wenn ein anderes Profil automatisch eine Verbindung öffnen soll, müssen Sie es auf dem Gerät als Standardprofil festlegen.  
    >   
    >  Wenn die Option **Gesamten Netzwerkdatenverkehr über die VPN-Verbindung senden** nicht ausgewählt ist und die VPN-Verbindung getrenntes Tunneln verwendet, kann eine VPN-Verbindung automatisch geöffnet werden, wenn Sie Routen oder ein verbindungsspezifisches DNS-Suffix konfigurieren.  


1. Wählen Sie auf der Seite **Unterstützte Plattformen** des **Assistenten zum Erstellen von VPN-Profilen**die Betriebssysteme aus, unter denen das VPN-Profil installiert wird, oder klicken Sie auf **Alle auswählen** , um das VPN-Profil unter allen verfügbaren Betriebssystemen zu installieren.  

2. Schließen Sie den Assistenten ab. Das neue VPN-Profil wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **VPN-Profile** angezeigt.  

### <a name="next-steps"></a>Nächste Schritte

- Verteilen Sie die VPN-App für Drittanbieter-VPN-Verbindungen vor der Bereitstellung des VPN-Profils. Wenn Sie die App nicht bereitstellen, werden die Benutzer dazu aufgefordert, sobald sie versuchen, sich mit dem VPN zu verbinden. Weitere Informationen zum Bereitstellen von Apps finden Sie unter [Bereitstellen von Anwendungen mit System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

- Stellen Sie die VPN-Profile wie in [Erstellen von VPN-Profilen in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md) beschrieben bereit.  



<!--HONumber=Dec16_HO5-->


