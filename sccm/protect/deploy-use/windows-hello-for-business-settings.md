---
title: Windows Hello for Business-Einstellungen | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Windows Hello for Business in System Center Configuration Manager integrieren.
ms.custom: na
ms.date: 10/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: 17
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 1f254ee31bae1c3d7b1506e68c40baf78793bf66


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Windows Hello for Business-Einstellungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit System Center Configuration Manager können Sie die Integration in Windows Hello for Business (früher Microsoft Passport für Windows) durchführen, eine alternative Anmeldemethode für Windows 10-Geräte. Hello for Business verwendet Active Directory oder ein Azure Active Directory-Konto, um ein Kennwort, eine Smartcard oder eine virtuelle Smartcard zu ersetzen.  

Mit Hello for Business können Sie anstelle eines Kennworts eine **Benutzeraktion** zur Anmeldung verwenden. Eine Benutzeraktion kann eine einfache PIN, eine biometrische Authentifizierung oder ein externes Gerät wie ein Fingerabdruckleser sein.  

 Configuration Manager kann auf zwei Wegen in Windows Hello for Business integriert werden:  

-   Sie können mithilfe von Configuration Manager steuern, welche Aktionen von Benutzern zum Anmelden verwendet werden können.  

-   Sie können Authentifizierungszertifikate im Windows Hello for Business-Schlüsselspeicheranbieter (Key Storage Provider; KSP) speichern. Weitere Informationen finden Sie unter [Zertifikatprofile](introduction-to-certificate-profiles.md).  

- Sie können Richtlinien von „Windows Hello for Business“ für Windows 10-Geräte bereitstellen, die in eine Domäne eingebunden sind und auf denen der Configuration Manager-Client ausgeführt wird. Diese Konfiguration wird unter [Konfigurieren von Windows Hello for Business auf einer Domäne angehörenden Windows 10-Geräten](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices) weiter unten beschrieben. Bei Verwendung von Configuration Manager mit Intune (Hybrid) können Sie diese Einstellungen auf Windows 10- und Windows 10 Mobile-Geräten, aber nicht auf Geräten konfigurieren, die zu einer Domäne gehören und auf denen der Configuration Manager-Client ausgeführt wird.   

## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Konfigurieren von Windows Hello for Business-Einstellungen (hybrid)  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Clouddienste** > **Microsoft Intune-Abonnements**.  

3.  Wählen Sie aus der Liste Ihr Microsoft Intune-Abonnement aus. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Abonnement** auf **Plattformen konfigurieren** > **Windows (MDM)**.  

4.  Wählen Sie auf der Registerkarte **Windows Hello for Business** des Dialogfelds **Microsoft Intune-Abonnementeigenschaften** aus folgenden Werten aus, die Auswirkungen auf alle registrierten Windows 10- und Windows 10 Mobile-Geräte haben:  

    -   **Windows Hello for Business auf registrierten Geräten deaktivieren** oder **Windows Hello for Business auf registrierten Geräten aktivieren** : Aktiviert oder deaktiviert die Verwendung von Windows Hello for Business auf allen registrierten Windows 10 und Windows 10 Mobile-Geräten.  

    -   **Trusted Platform Module (TPM) verwenden** : Ein Trusted Platform Module-Chip (TPM) bietet eine zusätzliche Sicherheitsebene für Daten. Wählen Sie einen der folgenden Werte aus:  

        -   **Erforderlich** (Standard) – Nur Geräte mit verfügbarem TPM können Windows Hello for Business bereitstellen.  

        -   **Bevorzugt** – Geräte versuchen zunächst, ein TPM zu verwenden. Wenn diese Option nicht verfügbar ist, können sie die Softwareverschlüsselung verwenden.  

    -   **Mindestlänge für PIN anfordern** : Geben Sie die Mindestanzahl von Zeichen an, die für die Windows Hello for Business-PIN erforderlich ist. Sie müssen mindestens vier Zeichen verwenden (der Standardwert ist sechs Zeichen).  

    -   **Höchstlänge für PIN anfordern** : Geben Sie die maximale Anzahl von Zeichen an, die für die Windows Hello for Business-PIN zulässig ist. Sie können bis zu 127 Zeichen verwenden.  

    -   **Kleinbuchstaben in PIN vorschreiben** : Gibt an, ob in der Windows Hello for Business-PIN Kleinbuchstaben verwendet werden müssen. Wählen Sie aus:  

        -   **Zulässig** – Benutzer können in ihrer PIN Kleinbuchstaben verwenden.  

        -   **Erforderlich** – Benutzer müssen in ihre PIN mindestens einen Kleinbuchstaben einbeziehen.  

        -   **Nicht zulässig** – (Standardeinstellung) Benutzer dürfen in ihrer PIN keine Kleinbuchstaben verwenden.  

    -   **Großbuchstaben in PIN vorschreiben** : Gibt an, ob in der Windows Hello for Business-PIN Großbuchstaben verwendet werden müssen. Wählen Sie aus:  

        -   **Zulässig** – Benutzer können in ihrer PIN Großbuchstaben verwenden.  

        -   **Erforderlich** – Benutzer müssen in ihre PIN mindestens einen Großbuchstaben einbeziehen.  

        -   **Nicht zulässig** – (Standardeinstellung) Benutzer dürfen in ihrer PIN keine Großbuchstaben verwenden.  

    -   **Sonderzeichen anfordern** : Gibt die Verwendung von Sonderzeichen in der PIN an. Wählen Sie aus:  

        -   **Zulässig** – Benutzer können in ihrer PIN Sonderzeichen verwenden.  

        -   **Erforderlich** – Benutzer müssen in ihre PIN mindestens ein Sonderzeichen einbeziehen.  

        -   **Nicht zulässig,** (Standard) – Benutzer dürfen keine Sonderzeichen in ihrer PIN verwenden (dies trifft auch zu, wenn die Einstellung nicht konfiguriert ist).  

         Sonderzeichen umfassen: **! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**.  

    -   **PIN-Ablauf (in Tagen) anfordern** : Gibt die Anzahl der Tage an, bevor die Geräte-PIN geändert werden muss. Die Standardeinstellung ist 41 Tage.  

    -   **Wiederverwendung vorheriger PINs verhindern** : Verwenden Sie diese Einstellung, um die Wiederverwendung zuvor verwendeter PINs einzuschränken. Standardmäßig können die letzten fünf PINs nicht erneut verwendet werden.  

    -   **Biometrische Erkennung aktivieren** : Aktiviert die biometrische Authentifizierung, z.B. die Gesichtserkennung oder Fingerabdrücke, als Alternative zu einer PIN für Windows Hello for Business. Benutzer müssen für den Fall dennoch eine PIN konfigurieren, dass die biometrische Authentifizierung fehlschlägt.  

         Wenn diese Eigenschaft auf **Aktiviert**festgelegt ist, lässt Windows Hello for Business die biometrische Authentifizierung zu.  Wenn diese Eigenschaft auf **Deaktiviert**festgelegt ist, verhindert Windows Hello for Business die biometrische Authentifizierung (für alle Kontotypen).  

    -   **Erweitertes Antispoofing verwenden, falls verfügbar** : Konfiguriert, ob das erweiterte Antispoofing auf Geräten verwendet wird, die diese Option unterstützen.  

         Wenn diese Option auf **Aktiviert**festgelegt ist, fordert Windows von allen Benutzern die Verwendung von Antispoofing für Gesichtsmerkmale, sofern dies unterstützt wird.  

    -   **** : Wenn diese Option auf **Aktiviert**festgelegt ist, können die Benutzer eine Remote-Version von Hello for Business als tragbares Begleitgerät für die Authentifizierung von Desktopcomputern verwenden. Der Desktopcomputer muss mit Azure Active Directory verknüpft sein, und das Begleitgerät muss mit einer Windows Hello for Business-PIN konfiguriert werden.  

5.  Klicken Sie zum Abschluss auf **OK**.  


## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Konfigurieren von Windows Hello for Business auf einer Domäne angehörenden Windows 10-Geräten
Sie können Windows Hello for Business-Einstellungen auf einer Domäne angehörenden Windows 10-Geräten auf drei Arten steuern:

- Sie können ein Windows Hello for Business-Profil erstellen und bereitstellen. Dies ist die empfohlene Option.
- Sie können Gruppenrichtlinien verwenden.  
- Sie können ein PowerShell-Skript verwenden.

Beachten Sie, dass Sie zusätzlich zu dieser Konfiguration, wie unter [Configure a certificate profile (Konfigurieren eines Zertifikatprofils)](#configure-a-certificate-profile) beschrieben, ein Zertifikatprofil bereitstellen müssen.

### <a name="recommended-approach----configure-a-windows-hello-for-business-profile"></a>Empfohlener Ansatz – Konfigurieren eines Windows Hello for Business-Profils  

Klicken Sie in der Verwaltungskonsole mit der rechten Maustaste unter **Zugriff auf Unternehmensressourcen** auf **Profile für Windows Hello für Unternehmen**, und wählen Sie **Neu** aus, um den Profilassistenten zu starten. Stellen Sie die Einstellungen bereit, die der Assistent anfordert, überprüfen und bestätigen Sie die Einstellungen auf der letzten Seite, und klicken Sie auf **Schließen**. Beispiel von möglichen Einstellungen:  

![Windows Hello for Business-Einstellungen](../media/Hello-for-Business-settings.png)

### <a name="configure-windows-hello-for-business-with-group-policy-in-active-directory"></a>Konfigurieren von Configure Windows Hello for Business mit Gruppenrichtlinie in Active Directory  

Sie können Ihre Windows 10-Geräte, die einer Domäne angehören, mit einer Active Directory-Gruppenrichtlinie konfigurieren, um beim Anmelden eines Benutzers bei Windows Hello for Business-Anmeldeinformationen bereitzustellen:

1.  Öffnen Sie auf einem Windows Server-Computer den Server-Manager, und navigieren Sie zu **Extras** > **Gruppenrichtlinienverwaltung**.    

2.  Erweitern Sie im Dialogfeld **Gruppenrichtlinienverwaltung** die Domäne, in der Sie die automatische Arbeitsbereichseinbindung aktivieren möchten.    

3.  Klicken Sie mit der rechten Maustaste auf **Gruppenrichtlinienobjekte**, und klicken Sie dann auf **Neu**.  

4.  Geben Sie im Dialogfeld **Neues Gruppenrichtlinienobjekt** einen Namen für das neue Gruppenrichtlinienobjekt ein, z.B. **Windows Hello für Unternehmen aktivieren**, und klicken Sie dann auf **OK**.  

5.  Klicken Sie im Knoten **Gruppenrichtlinienobjekt** mit der rechten Maustaste auf das soeben erstellte Objekt, und klicken Sie dann auf **Bearbeiten**.  

6.  Wechseln Sie im Dialogfeld **Gruppenrichtlinienverwaltungs-Editor** zu **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Hello for Business**.  

7.  Klicken Sie mit der rechten Maustaste auf **Windows Hello für Unternehmen aktivieren**, und klicken Sie dann auf **Bearbeiten**.   

8.  Wählen Sie **Aktiviert**aus, klicken Sie auf **Übernehmen**, und klicken Sie dann auf **OK**.

Sie können jetzt das soeben erstellte Gruppenrichtlinienobjekt mit einem Speicherort Ihrer Wahl verknüpfen. Beispiel:    

   Eine bestimmte Organisationseinheit (OU) in Active Directory, in der sich Windows 10-Computer befinden, die einer Domäne angehören.    

   Eine bestimmte Sicherheitsgruppe, die Windows 10-Computer enthält, die einer Domäne angehören und automatisch mit Azure Active Directory registriert werden.    

#### <a name="configure-windows-hello-for-business-by-deploying-a-powershell-script-with-configuration-manager"></a>Konfigurieren von Windows Hello for Business durch Bereitstellen eines PowerShell-Skripts mit Configuration Manager    
Sie können das folgende PowerShell-Skript mithilfe der Configuration Manager-Anwendungsverwaltung erstellen und bereitstellen.    

```    
powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}"  
```  

Weitere Informationen zur Configuration Manager-Anwendungsverwaltung finden Sie unter [Einführung in die Anwendungsverwaltung mit System Center Configuration Manager (Introduction to Application Management in Configuration Manager)](/sccm/apps/understand/introduction-to-application-management).  

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Konfigurieren eines Zertifikatprofils für die Registrierung des Windows Hello for Business-Registrierungszertifikats in Configuration Manager  
 Wenn Sie die zertifikatbasierte Anmeldung für Windows Hello for Business oder Microsoft Hello verwenden möchten, konfigurieren Sie Folgendes:  

-   Ein Configuration Manager-Zertifikatprofil.  

-   Wählen Sie im Zertifikatprofil eine Vorlage aus, die die Smartcard-Anmeldung für die erweiterte Schlüsselverwendung verwendet.  

 Weitere Informationen finden Sie unter [Zertifikatprofile](introduction-to-certificate-profiles.md).  

### <a name="see-also"></a>Weitere Informationen:  
 [Schützen der Daten und Standortinfrastruktur mit System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)

 [Verwalten der Überprüfung der Identität mit Windows Hello for Business](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport).  



<!--HONumber=Dec16_HO3-->


