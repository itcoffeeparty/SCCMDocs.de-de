---
title: Erstellen von PFX-Zertifikatprofilen | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie PFX-Dateien in System Center Configuration Manager verwenden, um benutzerspezifische Zertifikate zu generieren, die den verschlüsselten Datenaustausch unterstützen."
ms.custom: na
ms.date: 03/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3b1451edaed69a972551bd060293839aa11ec8b2
ms.openlocfilehash: 2495cef2442706b343bac6d510946c1226b64cfc
ms.lasthandoff: 03/28/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Erstellen von PFX-Zertifikatprofilen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Zertifikatprofile arbeiten mit Active Directory-Zertifikatdiensten und der Rolle „Registrierungsdienst für Netzwerkgeräte“, um Authentifizierungszertifikate für verwaltete Geräte bereitzustellen, damit Benutzer nahtlos auf Unternehmensressourcen zugreifen können. Sie können z. B. Zertifikatprofile erstellen und bereitstellen, um Benutzern die erforderlichen Zertifikate zum Initiieren von VPN- und Drahtlosverbindungen bereitzustellen.

Unter [Zertifikatprofile](../../protect/deploy-use/introduction-to-certificate-profiles.md) erhalten Sie allgemeine Informationen zum Erstellen und Konfigurieren von Zertifikatprofilen. In diesem Thema erfahren Sie Genaueres über Zertifikatprofile, die mit PFX-Zertifikatprofilen in Verbindung stehen.

-  Configuration Manager unterstützt die anforderungs-, gerätetyp- und betriebssystemabhängige Bereitstellung von Zertifikaten an unterschiedliche Zertifikatspeicher. Die folgenden Geräte werden unterstützt, wenn sie mit Intune registriert sind:

 -   iOS  

- Andere Voraussetzungen finden Sie unter [Voraussetzungen für Zertifikatprofile](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>PFX-Zertifikatprofile
System Center Configuration Manager ermöglicht Ihnen die Bereitstellung von PFX-Dateien (Personal Information Exchange) für Geräte des Benutzers. PFX-Dateien können zum Generieren benutzerspezifischer Zertifikate zur Unterstützung eines verschlüsselten Datenaustausches verwendet werden. PFX-Zertifikate können in Configuration Manager erstellt oder importiert werden.

> [!TIP]  
>  Unter [Erstellen und Bereitstellen von PFX-Zertifikatprofilen in Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)finden Sie eine schrittweise exemplarische Vorgehensweise für diesen Vorgang.  

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Erstellen und Bereitstellen eines PFX-Zertifikatprofils (Personal Information Exchange)  

### <a name="get-started"></a>Erste Schritte

1.  Klicken Sie in der System Center Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, den **Zugriff auf Unternehmensressourcen**, und klicken Sie dann auf **Zertifikatprofile**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Zertifikatprofil erstellen**.

4.  Geben Sie auf der Seite **Allgemein** des **** Assistenten zum Erstellen von Zertifikatprofilen die folgenden Informationen an:  

    -   **Name**: Geben Sie einen eindeutigen Namen für das Zertifikatprofil ein. Sie können maximal 256 Zeichen verwenden.  

    -   **Beschreibung**: Geben Sie eine Beschreibung mit einem Überblick über das Zertifikatprofil sowie weitere relevante Informationen ein, die der Identifikation des Profils in der System Center Configuration Manager-Konsole dienen. Sie können maximal 256 Zeichen verwenden.  

    -   **Geben Sie den Typ des Zertifikatprofils an, das Sie erstellen möchten**: Wählen Sie einen der folgenden Typen für das PFX-Zertifikatprofil aus:  

        -   **Privater Informationsaustausch – PKCS #12 (.PFX)-Einstellungen – Importieren**: Wählen Sie diese Option aus, um ein PFX-Zertifikat zu importieren.  
        -   **Privater Informationsaustausch – PKCS #12-Einstellungen (PFX) – Erstellen**: Wählen Sie diese Option aus, um ein PFX-Zertifikat zu erstellen.

### <a name="import-a-pfx-certificate"></a>Importieren eines PFX-Zertifikats

Sie benötigen das Configuration Manager-SDK, um ein PFX-Zertifikat zu importieren. Alle Zertifikate, die Sie für einen Benutzer importieren, werden für alle Geräte bereitgestellt werden, die der Benutzer anmeldet.

1. Geben Sie im Fenster **PFX-Zertifikat** des **Assistent zum Erstellen von Zertifikatprofilen** an, wo das Zertifikat auf den Geräten gespeichert wird, für die Sie es bereitstellen:
    -     **In Trusted Platform Module (TPM) installieren (sofern vorhanden)**  
    -   **In Trusted Platform Module (TPM) installieren (andernfalls Fehler)** 
    -   **In Windows Hello for Business installieren (andernfalls Fehler)** 
    -   **In Softwareschlüsselspeicher-Anbieter installieren** 
2. Klicken Sie auf **Weiter**. 
3. Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten die Geräteplattformen aus, auf dem das Zertifikat installiert werden soll, und klicken Sie dann **Weiter**.
4. Stellen Sie mithilfe des SDK für Windows 8.1, das im Download Center ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525)verfügbar ist, ein PFX-Erstellungsskript bereit. Mit dem PFX-Erstellungsskript, das in Configuration Manager 2012 SP2 hinzugefügt wurde, wird eine SMS_ClientPfxCertificate-Klasse zum SDK hinzugefügt. Diese Klasse enthält die folgenden Methoden:  

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

   -   blob\ = Das Base64-verschlüsselte Blob für PFX  
   -   $Password = Das Kennwort für die PFX-Datei  
   -   $ProfileName = Der Name des PFX-Profils  
   -   ComputerName = Der Name des Hostcomputers   

### <a name="create-a-new-pfx-certificate"></a>Erstellen eines neuen PFX-Zertifikats

Wenn Sie ein PFX-Zertifikat erstellen und bereitstellen, wird dasselbe Zertifikat auf allen Geräten installiert werden, die der Benutzer registriert.

1. Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten die Geräteplattformen aus, auf dem das Zertifikat installiert werden soll, und klicken Sie dann auf **Weiter**.
2. Konfigurieren Sie Folgendes auf der Seite **Zertifizierungsstellen** des Assistenten:
    - **Primärer Standort**: Wählen Sie den primären Standort von Configuration Manager, von dem Sie eine Zertifizierungsstelle auswählen möchten.
    - **Zertifizierungsstellen**: Nachdem Sie einen primären Standort ausgewählt haben, wählen Sie die gewünschte Zertifizierungsstelle aus der Liste aus, und klicken Sie anschließend auf **Weiter**.
3. Konfigurieren Sie auf der Seite **PFX-Zertifikat** des Assistenten die folgenden Informationen:
    - **Erneuerungsschwellenwert (%)**: Geben Sie den Prozentsatz der Zertifikatgültigkeitsdauer an, die verbleibt, bevor das Gerät eine Erneuerung des Zertifikats anfordert.
    - **Name der Zertifikatvorlage**: Klicken Sie auf **Durchsuchen**, um den Namen der Zertifikatvorlage auszuwählen, der einer ausstellenden Zertifizierungsstelle hinzugefügt wurde. Damit Sie Zertifikatvorlagen durchsuchen können, muss das Benutzerkonto, mit dem Sie die Configuration Manager-Konsole ausführen, über die **Lese**-Berechtigung für die Zertifikatvorlage verfügen. Geben Sie alternativ den Namen der Zertifikatvorlage ein. 
    - **Format des Antragstellernamens**: Wählen Sie in der Liste aus, wie Configuration Manager den Antragstellernamen in der Zertifikatanforderung automatisch erstellt. Wenn das Zertifikat für einen Benutzer bestimmt ist, können Sie auch die E-Mail-Adresse des Benutzers im Antragstellernamen einschließen. Wählen Sie aus **Allgemeiner Name**, oder **Vollständiger definierter Name** aus.
    - **Alternativer Antragstellername**: Geben Sie an, wie die Werte für den alternativen Antragstellernamen (Subject Alternative Name, SAN) in der Zertifikatanforderung von Configuration Manager automatisch erstellt werden sollen. Beispiel: Wenn Sie einen Benutzerzertifikattyp ausgewählt haben, könnten Sie in den alternativen Antragstellernamen den Benutzerprinzipalnamen (User Principal Name, UPN) aufnehmen. Wählen Sie aus:
        - **E-Mail-Adresse** 
        - **Benutzerprinzipalname (UPN)** 
    - **Gültigkeitsdauer des Zertifikats** - 
    - **Windows-Schlüsselspeicheranbieter** (wird nur angezeigt, wenn Sie Windows als unterstützte Plattform ausgewählt haben) - 
        -     **In Trusted Platform Module (TPM) installieren (sofern vorhanden)**  
        -   **In Trusted Platform Module (TPM) installieren (andernfalls Fehler)** 
        -   **In Windows Hello for Business installieren (andernfalls Fehler)** 
        -   **In Softwareschlüsselspeicher-Anbieter installieren** 
4. Klicken Sie auf **Weiter**.

### <a name="finish-up"></a>Fertig stellen

1.  Klicken Sie auf **Weiter**, überprüfen Sie die Seite **Zusammenfassung** , und schließen Sie dann den Assistenten.  
2.  Das Zertifikatprofil mit der PFX-Datei steht nun im Arbeitsbereich **Zertifikatprofile** bereit. 
3.  Um das Profil bereitzustellen, öffnen Sie im Arbeitsbereich **Bestand und Konformität** **Konformitätseinstellungen** > **Zugriff auf Unternehmensressourcen** > **Zertifikatprofile**, klicken Sie mit der rechten Maustaste auf das gewünschte Zertifikat und anschließend auf **Bereitstellen**. 



## <a name="see-also"></a>Weitere Informationen:
[Create a new certificate profile (Erstellen eines neuen Zertifikatprofils)](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) begleitet Sie im Assistenten für das Erstellen eines Zertifikatprofils.

[Bereitstellen von WLAN-, VPN-, E-Mail- und Zertifikatprofilen](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) bietet Informationen zum Bereitstellen von Zertifikatprofilen.
