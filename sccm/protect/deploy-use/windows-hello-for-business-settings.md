---
title: Windows Hello for Business-Einstellungen | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Windows Hello for Business in System Center Configuration Manager integrieren.
ms.custom: na
ms.date: 03/28/2017
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
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: c9a6842958e6fa3f740caabbaf20aabb9df4e8a8
ms.lasthandoff: 03/27/2017


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Windows Hello for Business-Einstellungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit System Center Configuration Manager können Sie die Integration in Windows Hello for Business (früher Microsoft Passport für Windows) durchführen, eine alternative Anmeldemethode für Windows 10-Geräte. Hello for Business verwendet Active Directory oder ein Azure Active Directory-Konto, um ein Kennwort, eine Smartcard oder eine virtuelle Smartcard zu ersetzen.  

Mit Hello for Business können Sie anstelle eines Kennworts eine **Benutzeraktion** zur Anmeldung verwenden. Eine Benutzeraktion kann eine einfache PIN, eine biometrische Authentifizierung oder ein externes Gerät wie ein Fingerabdruckleser sein.  

 Configuration Manager kann auf zwei Wegen in Windows Hello for Business integriert werden:  

-   Sie können mithilfe von Configuration Manager steuern, welche Aktionen von Benutzern zum Anmelden verwendet werden können.  

-   Sie können Authentifizierungszertifikate im Windows Hello for Business-Schlüsselspeicheranbieter (Key Storage Provider; KSP) speichern. Weitere Informationen finden Sie unter [Zertifikatprofile](introduction-to-certificate-profiles.md).  

- Sie können Richtlinien von „Windows Hello for Business“ für Windows 10-Geräte bereitstellen, die in eine Domäne eingebunden sind und auf denen der Configuration Manager-Client ausgeführt wird. Diese Konfiguration wird unter [Konfigurieren von Windows Hello for Business auf einer Domäne angehörenden Windows 10-Geräten](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices) weiter unten beschrieben. Bei Verwendung von Configuration Manager mit Intune (Hybrid) können Sie diese Einstellungen auf Windows 10- und Windows 10 Mobile-Geräten, aber nicht auf Geräten konfigurieren, die zu einer Domäne gehören und auf denen der Configuration Manager-Client ausgeführt wird. Weitere Informationen finden Sie unter [Configure Windows Hello for Business settings (hybrid) (So konfigurieren Sie Windows Hello for Business-Einstellungen (hybrid))](../../mdm/deploy-use/windows-hello-for-business-settings.md).

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Konfigurieren von Windows Hello for Business auf einer Domäne angehörenden Windows 10-Geräten
Sie können Windows Hello for Business-Einstellungen auf einer Domäne angehörenden Windows 10-Geräten auf drei Arten steuern:

- Sie können ein Windows Hello for Business-Profil erstellen und bereitstellen. Dies ist die empfohlene Option.
- Sie können Gruppenrichtlinien verwenden.  
- Sie können ein PowerShell-Skript verwenden.

Beachten Sie, dass Sie zusätzlich zu dieser Konfiguration, wie unter [Configure a certificate profile (Konfigurieren eines Zertifikatprofils)](#configure-a-certificate-profile) beschrieben, ein Zertifikatprofil bereitstellen müssen.

## <a name="recommended-approach----configure-a-windows-hello-for-business-profile"></a>Empfohlener Ansatz – Konfigurieren eines Windows Hello for Business-Profils  

Klicken Sie in der Configuration Manager-Konsole mit der rechten Maustaste unter **Zugriff auf Unternehmensressourcen** auf **Profile für Windows Hello für Unternehmen**, und wählen Sie **Neu** aus, um den Profilassistenten zu starten. Stellen Sie die Einstellungen bereit, die der Assistent anfordert, überprüfen und bestätigen Sie die Einstellungen auf der letzten Seite, und klicken Sie auf **Schließen**. Beispiel von möglichen Einstellungen:  

![Windows Hello for Business-Einstellungen](../media/Hello-for-Business-settings.png)

## <a name="configure-windows-hello-for-business-with-group-policy-in-active-directory"></a>Konfigurieren von Configure Windows Hello for Business mit Gruppenrichtlinie in Active Directory  

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

## <a name="configure-windows-hello-for-business-by-deploying-a-powershell-script-with-configuration-manager"></a>Konfigurieren von Windows Hello for Business durch Bereitstellen eines PowerShell-Skripts mit Configuration Manager    
Sie können das folgende PowerShell-Skript mithilfe der Configuration Manager-Anwendungsverwaltung erstellen und bereitstellen.    

**powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}"** 

Weitere Informationen zur Configuration Manager-Anwendungsverwaltung finden Sie unter [Einführung in die Anwendungsverwaltung mit System Center Configuration Manager (Introduction to Application Management in Configuration Manager)](/sccm/apps/understand/introduction-to-application-management).  

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Konfigurieren eines Zertifikatprofils für die Registrierung des Windows Hello for Business-Registrierungszertifikats in Configuration Manager  
 Wenn Sie die zertifikatbasierte Anmeldung für Windows Hello for Business oder Microsoft Hello verwenden möchten, konfigurieren Sie Folgendes:  

-   Ein Configuration Manager-Zertifikatprofil.  

-   Wählen Sie im Zertifikatprofil eine Vorlage aus, die die Smartcard-Anmeldung für die erweiterte Schlüsselverwendung verwendet.  

-    Wenn Sie Zertifikatprofile im Schlüsselcontainer von Windows Hello for Business speichern möchten, und das Zertifikatprofil **Smartcard-Anmeldung** für die erweiterte Schlüsselverwendung verwendet, müssen Sie die folgenden Berechtigungen für die Schlüsselregistrierung konfigurieren, um sicherzustellen, dass das Zertifikat ordnungsgemäß überprüft wurde.
Vorher müssen Sie die Gruppe **Schlüsseladministratoren** erstellt und alle Verwaltungspunktcomputer von Configuration Manager als Member dieser Gruppe hinzugefügt haben.

    1.    Melden Sie sich in einem Domänencontroller oder einer Verwaltungsarbeitsstation mit Anmeldeinformationen des Domänenadministrators oder äquivalenten Anmeldeinformationen an.
    2.    Öffnen Sie **Active Directory-Benutzer und -Computer**.
    3.    Klicken Sie im Navigationsbereich mit der rechten Maustaste auf Ihren Domänennamen, und klicken anschließend auf **Eigenschaften**.
    4.    Klicken Sie auf der Registerkarte **Sicherheit** des Dialogfelds *<domain name>* **Eigenschaften** auf **Erweitert**. Wenn die Registerkarte **Sicherheit** nicht angezeigt wird, aktivieren Sie **Erweiterte Funktionen** im Menü **Ansicht** von **Active Directory-Benutzer und -Computer**.
    5.    Klicken Sie auf **Hinzufügen**.
    6.    Klicken Sie im Dialogfeld **Permission Entry for** (Berechtigungseintrag für) *<domain name>* auf **Prinzipal auswählen**.
    7.    Geben Sie im Dialogfeld **Select User, Computer, Service Account, or Group (Benutzer, Computer, Dienstkonto oder Gruppe auswählen** **Schlüsseladministratoren** in das Textfeld **Enter the object name to select (Geben Sie den auszuwählenden Objektnamen ein)** ein.  Klicken Sie auf **OK**.
    8.    Wählen Sie aus der Liste **Gilt für** **Descendant User objects (Nachfolgerbenutzerobjekte)** aus.
    9.    Scrollen Sie bis ans Ende der Seite und klicken Sie auf **Auswahl aufheben**.
    10.    Wählen Sie im Bereich **Eigenschaften** **Read msDS-KeyCredentialLink (msDS-KeyCredentialLink lesen)** aus.
    11.    Klicken Sie dreimal auf **OK**, um die Aufgabe abzuschließen.


 Weitere Informationen finden Sie unter [Zertifikatprofile](introduction-to-certificate-profiles.md).  

## <a name="see-also"></a>Weitere Informationen:  
 [Schützen der Daten und Standortinfrastruktur mit System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)

 [Verwalten der Überprüfung der Identität mit Windows Hello for Business](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport).  

