---
title: Erstellen von PFX-Zertifikatprofilen | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie PFX-Dateien in System Center Configuration Manager verwenden, um benutzerspezifische Zertifikate zu generieren, die den verschlüsselten Datenaustausch unterstützen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0185ab18-663d-468a-ba54-4f3f232fd4d2
caps.latest.revision: 5
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 36c20af00e5a83be7038c3a0c01a33c546011427


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Erstellen von PFX-Zertifikatprofilen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager ermöglicht Ihnen die Bereitstellung von PFX-Dateien (Personal Information Exchange) für Geräte des Benutzers. PFX-Dateien können zum Generieren benutzerspezifischer Zertifikate zur Unterstützung eines verschlüsselten Datenaustausches verwendet werden. PFX-Zertifikate können in Configuration Manager erstellt oder importiert werden. Mit System Center Configuration Manager können importierte oder neue PFX-Zertifikate auf Geräten mit iOS, Android und Windows 10 bereitgestellt werden. Diese Dateien können dann auf mehreren Geräten zur Unterstützung der benutzerbasierten PKI-Kommunikation bereitgestellt werden.  

> [!TIP]  
>  Unter [Erstellen und Bereitstellen von PFX-Zertifikatprofilen in Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)finden Sie eine schrittweise exemplarische Vorgehensweise für diesen Vorgang.  

## <a name="create-and-deploy-personal-information-exchange-pfx-certificate-profiles"></a>Erstellen und Bereitstellen von PFX-Zertifikatprofilen (Personal Information Exchange)  

#### <a name="how-to-create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>So können Sie ein PFX-Zertifikatprofil (Personal Information Exchange) erstellen und bereitstellen  

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



<!--HONumber=Dec16_HO3-->


