---
title: Windows Hello for Business-Einstellungen | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Windows Hello for Business in System Center Configuration Manager integrieren.
ms.custom: na
ms.date: 09/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: "17"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 43586e55f2c0c5cf117b94c61250f26ba4233f53
ms.sourcegitcommit: 4c3906cf9614420cb8527da9e48978eb0b8f0e7a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2017
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Windows Hello for Business-Einstellungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit System Center Configuration Manager können Sie die Integration in Windows Hello for Business (früher Microsoft Passport für Windows) durchführen, eine alternative Anmeldemethode für Windows 10-Geräte. Hello for Business verwendet Active Directory oder ein Azure Active Directory-Konto, um ein Kennwort, eine Smartcard oder eine virtuelle Smartcard zu ersetzen.  

Mit Hello for Business können Sie anstelle eines Kennworts eine **Benutzeraktion** zur Anmeldung verwenden. Eine Benutzeraktion kann eine einfache PIN, eine biometrische Authentifizierung oder ein externes Gerät wie ein Fingerabdruckleser sein.

[Erfahren Sie mehr über Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification).

 Configuration Manager kann auf zwei Wegen in Windows Hello for Business integriert werden:  

-   Sie können mithilfe von Configuration Manager steuern, welche Aktionen von Benutzern zum Anmelden verwendet werden können.  

-   Sie können Authentifizierungszertifikate im Windows Hello for Business-Schlüsselspeicheranbieter (Key Storage Provider; KSP) speichern. Weitere Informationen finden Sie unter [Zertifikatprofile](introduction-to-certificate-profiles.md).  

- Sie können Richtlinien von „Windows Hello for Business“ für Windows 10-Geräte bereitstellen, die in eine Domäne eingebunden sind und auf denen der Configuration Manager-Client ausgeführt wird. Diese Konfiguration wird unter [Konfigurieren von Windows Hello for Business auf einer Domäne angehörenden Windows 10-Geräten](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices) weiter unten beschrieben. Wenn Sie Configuration Manager mit Microsoft Intune (hybrid) verwenden, können Sie diese Einstellungen auf Windows 10- sowie Windows 10 Mobile-Geräten konfigurieren. Weitere Informationen finden Sie unter [Configure Windows Hello for Business settings (hybrid) (So konfigurieren Sie Windows Hello for Business-Einstellungen (hybrid))](../../mdm/deploy-use/windows-hello-for-business-settings.md).

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Konfigurieren von Windows Hello for Business auf einer Domäne angehörenden Windows 10-Geräten
Sie können Windows Hello for Business-Einstellungen auf in eine Domäne eingebundenen Windows 10-Geräten durch Erstellen und Bereitstellen eines Windows Hello for Business-Profils steuern. Dies ist die empfohlene Option.


Wenn Sie zertifikatbasierte Authentifizierung verwenden, müssen Sie auch, wie unter [Configure a certificate profile](#configure-a-certificate-profile) (Konfigurieren eines Zertifikatprofils) beschrieben, ein Zertifikatprofil bereitstellen. Wenn Sie schlüsselbasierte Authentifizierung verwenden, müssen Sie kein Zertifikatprofil bereitstellen.

## <a name="configure-a-windows-hello-for-business-profile"></a>Konfigurieren eines Windows Hello for Business-Profils  

Klicken Sie in der Configuration Manager-Konsole mit der rechten Maustaste unter **Zugriff auf Unternehmensressourcen** auf **Profile für Windows Hello für Unternehmen**, und wählen Sie **Neu** aus, um den Profilassistenten zu starten. Stellen Sie die Einstellungen bereit, die der Assistent anfordert, überprüfen und bestätigen Sie die Einstellungen auf der letzten Seite, und klicken Sie auf **Schließen**. Beispiel von möglichen Einstellungen:  

![Windows Hello for Business-Einstellungen](../media/Hello-for-Business-settings.png)

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Konfigurieren eines Zertifikatprofils für die Registrierung des Windows Hello for Business-Registrierungszertifikats in Configuration Manager  
 Wenn Sie die zertifikatbasierte Anmeldung für Windows Hello for Business verwenden möchten, konfigurieren Sie Folgendes:  

-   Ein Configuration Manager-Zertifikatprofil.  

-   Wählen Sie im Zertifikatprofil eine Vorlage aus, die die Smartcard-Anmeldung für die erweiterte Schlüsselverwendung verwendet.  

-   Wenn Sie Zertifikatprofile im Schlüsselcontainer von Windows Hello for Business speichern möchten, und das Zertifikatprofil **Smartcard-Anmeldung** für die erweiterte Schlüsselverwendung verwendet, müssen Sie die folgenden Berechtigungen für die Schlüsselregistrierung konfigurieren, um sicherzustellen, dass das Zertifikat ordnungsgemäß überprüft wurde.
Vorher müssen Sie die Gruppe **Schlüsseladministratoren** erstellt und alle Verwaltungspunktcomputer von Configuration Manager als Member dieser Gruppe hinzugefügt haben.

Für einige Konfigurationen müssen Sie möglicherweise keine Berechtigungen konfigurieren, oder sie erfordern möglicherweise weitere Konfigurationen. Weitere Hilfe finden Sie in der folgenden Tabelle:

|||||
|-|-|-|-|
|Windows-Clientversion|Configuration Manager 1602 oder 1606|Configuration Manager 1610|Configuration Manager 1702 oder höher|
|Windows 10 Anniversary Update|Kein Hotfix erforderlich<br><br>Keine Berechtigungen erforderlich<br><br>Kein Windows-Schemaupdate erforderlich|Kein Hotfix erforderlich (siehe **Warnung**)<br><br>Keine Berechtigungen erforderlich<br><br>Kein Windows-Schemaupdate erforderlich|Berechtigungen konfigurieren<br><br>Windows Server 2016-Schema auf Active Directory anwenden|
|Windows 10 Creators Update oder höher|Nicht unterstützt|[Dieses Hotfix](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v) installieren<br><br>Berechtigungen konfigurieren<br><br>Windows Server 2016-Schema auf Active Directory anwenden|Berechtigungen konfigurieren<br><br>Windows Server 2016-Schema auf Active Directory anwenden|

> [!WARNING]
> [Der Hotfix](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v) ist zwar nicht für Configuration Manager 1610 und Windows 10 Anniversary-Update erforderlich, kann jedoch installiert werden.  Wenn der Hotfix installiert ist, müssen Sie Berechtigungen konfigurieren und das Windows Server 2016-Schema für Active Directory übernehmen.

## <a name="to-configure-permissions"></a>So konfigurieren Sie Berechtigungen

1.  Melden Sie sich in einem Domänencontroller oder einer Verwaltungsarbeitsstation mit Anmeldeinformationen des Domänenadministrators oder äquivalenten Anmeldeinformationen an.
2.  Öffnen Sie **Active Directory-Benutzer und -Computer**.
3.  Klicken Sie im Navigationsbereich mit der rechten Maustaste auf Ihren Domänennamen, und klicken anschließend auf **Eigenschaften**.
4.  Klicken Sie auf der Registerkarte **Sicherheit** des Dialogfelds *<domain name>* **Eigenschaften** auf **Erweitert**. Wenn die Registerkarte **Sicherheit** nicht angezeigt wird, aktivieren Sie **Erweiterte Funktionen** im Menü **Ansicht** von **Active Directory-Benutzer und -Computer**.
5.  Klicken Sie auf **Hinzufügen**.
6.  Klicken Sie im Dialogfeld **Permission Entry for** (Berechtigungseintrag für) *<domain name>* auf **Prinzipal auswählen**.
7.  Geben Sie im Dialogfeld **Select User, Computer, Service Account, or Group (Benutzer, Computer, Dienstkonto oder Gruppe auswählen** **Schlüsseladministratoren** in das Textfeld **Enter the object name to select (Geben Sie den auszuwählenden Objektnamen ein)** ein.  Klicken Sie auf **OK**.
8.  Wählen Sie aus der Liste **Gilt für** **Descendant User objects (Nachfolgerbenutzerobjekte)** aus.
9.  Scrollen Sie bis ans Ende der Seite und klicken Sie auf **Auswahl aufheben**.
10. Wählen Sie im Bereich **Eigenschaften** **Read msDS-KeyCredentialLink (msDS-KeyCredentialLink lesen)** aus.
11. Klicken Sie dreimal auf **OK**, um die Aufgabe abzuschließen.


## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie unter [Zertifikatprofile](introduction-to-certificate-profiles.md).  




