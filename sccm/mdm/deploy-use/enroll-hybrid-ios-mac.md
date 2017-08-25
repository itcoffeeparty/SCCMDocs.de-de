---
title: "Einrichten einer hybriden Geräteverwaltung für iOS und Mac mit System Center Configuration Manager und Microsoft Intune | Microsoft-Dokumentation"
description: "Einrichten einer iOS-Geräteverwaltung mit System Center Configuration Manager und Microsoft Intune."
ms.custom: na
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
caps.latest.revision: "10"
caps.handback.revision: "0"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: d84d6f3dba65f1d8114ef2eef9f19a2bb5389027
ms.sourcegitcommit: 9a6f8e028fb5eb2e752da70f42a5b548339bd8f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/14/2017
---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Einrichten von iOS Hybrid-Geräte mit System Center Configuration Manager und Microsoft Intune einrichten

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit Configuration Manager und Intune können Sie die iOS- und macOS-Geräteregistrierung aktivieren, um iPhone-, iPad- und Mac-Benutzern Zugriff auf Unternehmens-E-Mails und -ressourcen zu gewähren. Nachdem Benutzer die Intune-Unternehmensportal-App installiert haben, können ihre Geräte unter Anwendung von Richtlinien angesprochen werden. Bevor Sie iOS- und Mac-Geräte verwalten können, müssen Sie ein APNS-Zertifikat (Apple Push Notification Service) von Apple importieren. Dieses Zertifikat ermöglicht Intune das Verwalten von iOS-und Mac-Geräten durch Herstellen einer Verbindung mit dem Geräteverwaltungsdienst von Apple.  

 Sie können außerdem firmeneigene iOS-Geräte registrieren.  Mehr unter [Registrieren von unternehmenseigenen Geräten](enroll-company-owned-devices.md).  

**Voraussetzungen**<br>
Bevor Sie die Registrierung einer Plattform einrichten können, müssen Sie die Voraussetzungen und Schritte in [Einrichten der hybriden Verwaltung mobiler Geräte](setup-hybrid-mdm.md) erfüllen und ausführen.

Zum Registrieren von iOS-Geräten müssen Sie die folgenden Schritte ausführen:  

## <a name="download-a-certificate-signing-request"></a>Laden Sie eine Zertifikatsignieranforderung herunter
Eine CSR-Datei (Zertifikatsignieranforderung) ist erforderlich, um ein APNS-Zertifikat von Apple anzufordern.  

1.  Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Clouddienste**> **Microsoft Intune-Abonnements**.  

2.  Klicken Sie auf der Registerkarte **Startseite** auf **APNs-Zertifikatanforderung erstellen**. Das Dialogfeld **APNs-Zertifikatsignieranforderung anfordern** wird geöffnet.  

3.  **Navigieren** Sie zum Pfad, um die neue CSR-Datei (Zertifikatsignieranforderung) zu speichern. Speichern Sie die Zertifikatsignierungsanforderung (CSR-Datei) lokal.  

4.  Klicken Sie auf **Herunterladen**. Die neue CSR-Datei von Microsoft Intune wird heruntergeladen und von Configuration Manager gespeichert. Die CSR-Datei wird verwendet, um ein Vertrauensstellungszertifikat vom Apple Push Certificates-Portal anzufordern.  

## <a name="request-an-mdm-push-certificate-from-apple"></a>Anfordern eines MDM-Push-Zertifikats von Apple
Das MDM-Push-Zertifikat dient zum Einrichten einer Vertrauensstellung zwischen dem Verwaltungsdienst, Intune und registrierten iOS-Mobilgeräten.  

1.  Navigieren Sie in einem Browser zum [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) , und melden Sie sich mit der Apple-ID Ihres Unternehmens an. Diese Apple-ID muss später verwendet werden, um das APNs-Zertifikat zu erneuern.  

2.  Schließen Sie den Assistenten mithilfe der Datei mit der Zertifikatsignierungsanforderung (CSR) ab. Laden Sie das MDM-Push-Zertifikat herunter, und speichern Sie die PEM-Datei lokal. Diese Zertifikatdatei (.pem) wird verwendet, um eine Vertrauensstellung zwischen dem Apple Push Notification-Server und der Verwaltungsautorität für mobile Geräte von Intune herzustellen.  

> [!NOTE]  
>  Laden Sie das Zertifikat des Apple Push Notification Service (APNs) erst auf Intune hoch, wenn Sie die iOS-Registrierung in der Configuration Manager-Konsole aktiviert haben.  

## <a name="enable-enrollment-and-upload-the-mdm-push-certificate"></a>Aktivieren Sie die Registrierung und laden Sie das MDM-Push-Zertifikat hoch.
Laden Sie das APNs-Zertifikat hoch, um die iOS-Registrierung zu aktivieren.  

1.  Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Clouddienste** > **Microsoft Intune-Abonnement**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Abonnement** auf **Plattformen konfigurieren** > **iOS**.  

3.  Wählen Sie im Dialogfeld **Eigenschaften von Microsoft Intune-Abonnement** die Registerkarte **iOS** aus, und aktivieren Sie das Kontrollkästchen **iOS-Anmeldung aktivieren** .  
4.  Klicken Sie auf **Durchsuchen**, und wechseln Sie zu der von Apple heruntergeladenen APNs-Zertifikatdatei (CER-Datei). Configuration Manager zeigt die APNs-Zertifikatinformationen an. Klicken Sie auf **OK** , um das APNs-Zertifikat in Intune zu speichern.  

Nachdem Sie die Einrichtung abgeschlossen haben, müssen Sie Ihre Benutzer darüber informieren, wie diese ihre Geräte registrieren sollen. Informationen hierzu finden Sie unter [Informieren der Benutzer über den Einsatz von Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate). Diese Informationen gelten für mobile Geräte, die mit Microsoft Intune und Configuration Manager verwaltet werden.

## <a name="configure-enrollment-restrictions"></a>Konfigurieren der Registrierungseinschränkungen

Sie können die Geräte begrenzen, die sich registrieren können, indem Sie Geräte in Privatbesitz blockieren. Dies verhindert, dass Benutzer ihre Geräte über das Unternehmensportal registrieren. Wenn Sie Geräte in Privatbesitz blockieren, können sich nur die folgenden Geräte registrieren:
- [Vorab deklarierte Geräte](predeclare-devices-with-hardware-id.md)
- [Durch Apple Configurator verwaltete Geräte](ios-hybrid-enrollment-using-apple-configurator.md)
- [Durch das Programm zur Geräteregistrierung (Device Enrollment Program, DEP) verwaltete Geräte](ios-device-enrollment-program-for-hybrid.md)
- Mit einem [Geräteregistrierungs-Manager-Konto](enroll-devices-with-device-enrollment-manager.md) registrierte Geräte

### <a name="to-enable-enrollment-restrictions"></a>So aktivieren Sie Registrierungseinschränkungen
1.  Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Clouddienste** > **Microsoft Intune-Abonnement**.
2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Abonnement** auf **Plattformen konfigurieren** > **iOS**.
3.  Wählen Sie **Geräte in Privatbesitz blockieren**, um die Registrierung auf unternehmenseigene Geräte zu begrenzen.

> [!div class="button"]
[< Vorheriger Schritt](create-service-connection-point.md) [Nächster Schritt >](set-up-additional-management.md)
