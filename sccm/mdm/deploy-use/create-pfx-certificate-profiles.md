---
title: Erstellen von PFX-Zertifikatprofilen | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie PFX-Dateien in System Center Configuration Manager verwenden, um benutzerspezifische Zertifikate zu generieren, die den verschlüsselten Datenaustausch unterstützen."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: eddecee8886296fb6132d7477afebbfc7fd280d1
ms.lasthandoff: 03/06/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Erstellen von PFX-Zertifikatprofilen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Zertifikatprofile arbeiten mit Active Directory-Zertifikatdiensten und der Rolle „Registrierungsdienst für Netzwerkgeräte“, um Authentifizierungszertifikate für verwaltete Geräte bereitzustellen, damit Benutzer nahtlos auf Unternehmensressourcen zugreifen können. Sie können z. B. Zertifikatprofile erstellen und bereitstellen, um Benutzern die erforderlichen Zertifikate zum Initiieren von VPN- und Drahtlosverbindungen bereitzustellen.

Unter [Zertifikatprofile](../../protect/deploy-use/introduction-to-certificate-profiles.md) erhalten Sie allgemeine Informationen zum Erstellen und Konfigurieren von Zertifikatprofilen. In diesem Thema erfahren Sie Genaueres über Zertifikatprofile, die mit der Verwaltung mobiler Geräte in Verbindung stehen.

- Zertifikatprofile bieten Zertifikatregistrierung und -erneuerung einer Zertifizierungsstelle (certficate authority, CA) eines Unternehmens für Geräte mit iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop und Mobile sowie Android. Diese Zertifikate können dann für WLAN- und VPN-Verbindungen verwendet werden.

-  Um Zertifikatprofile für SCEP bereitzustellen, müssen Sie ein Richtlinienmodul für NDES auf einem Server installieren, der Windows Server 2012 R2 mit der Rolle „Active Directory-Zertifikatdienste“ und einem funktionsfähigen NDES ausführt, der für die Geräte verfügbar ist, welche die Zertifikate benötigen. Bei Geräten, die von Microsoft Intune registriert werden, muss der NDES über das Internet verfügbar sein, z.B. in einem Umkreisnetzwerk (auch als DMZ bezeichnet).

-  Configuration Manager unterstützt die anforderungs-, gerätetyp- und betriebssystemabhängige Bereitstellung von Zertifikaten an unterschiedliche Zertifikatspeicher. Folgende Geräte und Betriebssysteme werden unterstützt:
 -   Windows RT 8.1  
 -   Windows 8.1  
 -   Windows Phone 8.1  
 -   Windows 10 Desktop und Mobile  
 -   iOS  
 -   Android  
 > [!IMPORTANT]  
 >  Um Profile für Android-, iOS-, Windows Phone- und registrierte Windows 8.1-Geräte (und höher) bereitzustellen, müssen diese Geräte [bei Microsoft Intune registriert](https://technet.microsoft.com/en-us/library/dn646962.aspx) werden.   

- Andere Voraussetzungen finden Sie unter [Voraussetzungen für Zertifikatprofile](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>PFX-Zertifikatprofile
System Center Configuration Manager ermöglicht Ihnen die Bereitstellung von PFX-Dateien (Personal Information Exchange) für Geräte des Benutzers. PFX-Dateien können zum Generieren benutzerspezifischer Zertifikate zur Unterstützung eines verschlüsselten Datenaustausches verwendet werden. PFX-Zertifikate können in Configuration Manager erstellt oder importiert werden. Mit System Center Configuration Manager können importierte oder neue PFX-Zertifikate auf Geräten mit iOS, Android und Windows 10 bereitgestellt werden. Diese Dateien können dann auf mehreren Geräten zur Unterstützung der benutzerbasierten PKI-Kommunikation bereitgestellt werden.  

> [!TIP]  
>  Unter [Erstellen und Bereitstellen von PFX-Zertifikatprofilen in Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)finden Sie eine schrittweise exemplarische Vorgehensweise für diesen Vorgang.  

### <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Erstellen und Bereitstellen eines PFX-Zertifikatprofils (Personal Information Exchange)  

1.  Klicken Sie in der System Center Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, den **Zugriff auf Unternehmensressourcen**, und klicken Sie dann auf **Zertifikatprofile**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Zertifikatprofil erstellen**. Der ** ** Assistent zum Erstellen von Zertifikatprofilen wird geöffnet.  

4.  Geben Sie auf der Seite **Allgemein** des ** ** Assistenten zum Erstellen von Zertifikatprofilen die folgenden Informationen an:  

    -   **Name**: Geben Sie einen eindeutigen Namen für das Zertifikatprofil ein. Sie können maximal 256 Zeichen verwenden.  

    -   **Beschreibung**: Geben Sie eine Beschreibung mit einem Überblick über das Zertifikatprofil sowie weitere relevante Informationen ein, die der Identifikation des Profils in der System Center Configuration Manager-Konsole dienen. Sie können maximal 256 Zeichen verwenden.  

    -   **Geben Sie den Typ des Zertifikatprofils an, das Sie erstellen möchten**: Wählen Sie einen der folgenden Typen für das Zertifikatprofil aus:  

        -   **Vertrauenswürdiges Zertifikat der Zertifizierungsstelle**: Wählen Sie diesen Typ für das Zertifikatprofil aus, falls Sie ein Zertifikat einer vertrauenswürdigen Stamm- oder Zwischenzertifizierungsstelle bereitstellen möchten, um eine Vertrauenskette zu bilden, wenn der Benutzer oder das Gerät ein anderes Gerät authentifizieren muss. Hierbei könnte es sich etwa um einen RADIUS-Server (Remote Authentication Dial-In User Service) oder einen VPN-Server (Virtual Private Network) handeln. Darüber hinaus müssen Sie ein Profil mit einem vertrauenswürdigen Zertifikat der Zertifizierungsstelle konfigurieren, bevor Sie ein SCEP-Zertifikatprofil erstellen können. In diesem Fall muss das vertrauenswürdige Zertifikat der Zertifizierungsstelle das vertrauenswürdige Stammzertifikat für die Zertifizierungsstelle sein, von der das Zertifikat für den Benutzer oder das Gerät ausgestellt wird.  

        -   **Einstellungen für Simple Certificate Enrollment-Protokoll (SCEP)**: Wählen Sie diesen Typ für das Zertifikatprofil aus, wenn Sie mit dem Simple Certificate Enrollment-Protokoll und dem Rollendienst „Registrierungsdienst für Netzwerkgeräte“ ein Zertifikat für einen Benutzer oder ein Gerät anfordern möchten.  

        -   **Privater Informationsaustausch – PKCS #12 (.PFX)-Einstellungen – Importieren**: Wählen Sie diese Option aus, um ein PFX-Zertifikat zu importieren.  

5.  Geben Sie im Fenster **Zertifikateigenschaften** des ** ** Assistenten zum Erstellen von Zertifikatprofilen an, wo das PFX-Zertifikat auf den Zielgeräten gespeichert wird.  

    -   **In Trusted Platform Module (TPM) installieren (sofern vorhanden)**  

    -   **In Trusted Platform Module (TPM) installieren (andernfalls Fehler)**  

    -   **In Softwareschlüsselspeicher-Anbieter installieren**  

     Klicken Sie auf **Weiter**.  

6.  Geben Sie im Fenster **Unterstützte Plattformen** des ** ** Assistenten zum Erstellen von Zertifikatprofilen an, welche Betriebssysteme oder Plattformen die importierte PFX-Datei empfangen können.  

    -   **Windows 10**  

    -   **iPhone**  

    -   **iPad**  

    -   **Android**  

7.  Klicken Sie auf **Weiter**, überprüfen Sie die Seite **Zusammenfassung** , und schließen Sie dann den Assistenten.  

8.  Das Zertifikatprofil mit der PFX-Datei steht nun im Arbeitsbereich **Zertifikatprofile** bereit. Klicken Sie in der **Bestand und Kompatibilität** zu **Kompatibilitätseinstellungen** > **Zugriff auf Unternehmensressourcen** > **Zertifikatprofile** , und klicken Sie mit der rechten Maustaste, um das neue Zertifikat für Benutzersammlungen bereitzustellen.  

9. Stellen Sie mithilfe des SDK für Windows 8.1, das im Download Center ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525)verfügbar ist, ein PFX-Erstellungsskript bereit. Mit dem PFX-Erstellungsskript, das in Configuration Manager 2012 SP2 hinzugefügt wurde, wird eine SMS_ClientPfxCertificate-Klasse zum SDK hinzugefügt. Diese Klasse enthält die folgenden Methoden:  

    -   ImportForUser  

    -   DeleteForUser  

     Beispielskript:  

    ```  
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  

    ```  

     Die folgenden Skriptvariablen müssen für das Skript geändert werden:  

    -   <blob\> = Das Base64-verschlüsselte Blob für PFX  

    -   $Password = Das Kennwort für die PFX-Datei  

    -   $ProfileName = Der Name des PFX-Profils  

    -   ComputerName = Der Name des Hostcomputers  

### <a name="see-also"></a>Weitere Informationen:
[Create a new certificate profile (Erstellen eines neuen Zertifikatprofils)](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) begleitet Sie im Assistenten für das Erstellen eines Zertifikatprofils.

[Bereitstellen von WLAN-, VPN-, E-Mail- und Zertifikatprofilen](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) bietet Informationen zum Bereitstellen von Zertifikatprofilen.

