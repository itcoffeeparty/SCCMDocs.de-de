---
title: "Einrichten einer hybriden Geräteverwaltung für iOS und Mac mit System Center Configuration Manager und Microsoft Intune"
description: "Einrichten einer iOS-Geräteverwaltung mit System Center Configuration Manager und Microsoft Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
caps.latest.revision: 10
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 3754f0e49d8393aed51bb6519af99b9eb728402f


---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Einrichten von iOS Hybrid-Geräte mit System Center Configuration Manager und Microsoft Intune einrichten

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit Configuration Manager und Intune können Sie die BYOD-Geräteregistrierung („Bring Your Own Device“) für iOS- und Mac OS X-Geräte aktivieren, um iPhone-, iPad- und Mac-Benutzern Zugriff auf Unternehmens-E-Mails und -ressourcen zu gewähren. Nachdem Benutzer die Intune-Unternehmensportal-App installiert haben, können ihre Geräte unter Anwendung von Richtlinien angesprochen werden. Bevor Sie iOS- und Mac-Geräte verwalten können, müssen Sie ein APNS-Zertifikat (Apple Push Notification Service) von Apple importieren. Dieses Zertifikat ermöglicht Intune das Verwalten von iOS- und Mac-Geräten und das Einrichten einer akkreditierten und verschlüsselten IP-Verbindung mit den Diensten für die Verwaltungsautorität für mobile Geräte.  

 Sie können außerdem firmeneigene iOS-Geräte registrieren.  Mehr unter [Registrieren von unternehmenseigenen Geräten](enroll-company-owned-devices.md).  

## <a name="enable-ios-device-enrollment"></a>Aktivieren der Registrierung von iOS-Geräten  
 Zum Registrieren von iOS-Geräten müssen Sie die folgenden Schritte ausführen:  

#### <a name="set-up-ios-device-enrollment-in-configuration-manager"></a>Einrichten der Registrierung von iOS-Geräten in Configuration Manager  

1.  **Voraussetzungen** ‒ Bevor Sie die Registrierung einer Plattform einrichten können, müssen Sie die Voraussetzungen und Schritte in [Einrichten der hybriden Verwaltung mobiler Geräte](setup-hybrid-mdm.md) erfüllen und ausführen.    

2.  **Herunterladen einer Zertifikatsignieranforderung** : Eine CSR-Datei (Zertifikatsignieranforderung) ist erforderlich, um ein APNs-Zertifikat von Apple anzufordern.  

    1.  Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Clouddienste**> **Microsoft Intune-Abonnements**.  

    2.  Klicken Sie auf der Registerkarte **Startseite** auf **APNs-Zertifikatanforderung erstellen**. Das Dialogfeld **APNs-Zertifikatsignieranforderung anfordern** wird geöffnet.  

    3.  **Navigieren** Sie zu dem Pfad, um die neue CSR-Datei (Zertifikatsignieranforderung) zu speichern. Speichern Sie die Zertifikatsignierungsanforderung (CSR-Datei) lokal.  

    4.  Klicken Sie auf **Herunterladen**. Die neue CSR-Datei von Microsoft Intune wird heruntergeladen und von Configuration Manager gespeichert. Die CSR-Datei wird verwendet, um ein Vertrauensstellungszertifikat vom Apple Push Certificates-Portal anzufordern.  

3.  **Anfordern eines APNs-Zertifikats von Apple** : Das APNs-Zertifikat (Apple Push Notification Service) dient zum Einrichten einer Vertrauensstellung zwischen dem Verwaltungsdienst, Intune und registrierten iOS-Mobilgeräten.  

    1.  Navigieren Sie in einem Browser zum [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) , und melden Sie sich mit der Apple-ID Ihres Unternehmens an. Diese Apple-ID muss später verwendet werden, um das APNs-Zertifikat zu erneuern.  

    2.  Schließen Sie den Assistenten mithilfe der Datei mit der Zertifikatsignierungsanforderung (CSR) ab. Laden Sie das APNs-Zertifikat herunter, und speichern Sie die PEM-Datei lokal. Diese APNs-Zertifikatdatei (.pem) wird verwendet, um eine Vertrauensstellung zwischen dem Apple Push Notification-Server und der Verwaltungsautorität für mobile Geräte von Intune herzustellen.  

4.  **Aktivieren der Registrierung und Hochladen des APNs-Zertifikats** : Zum Aktivieren der iOS-Registrierung laden Sie das APNs-Zertifikat hoch.  

    1.  Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Clouddienste** > **Microsoft Intune-Abonnement**.  

    2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Abonnement** auf **Plattformen konfigurieren** > **iOS**.  

        > [!NOTE]  
        >  Laden Sie das Zertifikat des Apple Push Notification Service (APNs) erst hoch, wenn Sie die iOS-Registrierung in der Configuration Manager-Konsole aktiviert haben.  

    3.  Wählen Sie im Dialogfeld **Eigenschaften von Microsoft Intune-Abonnement** die Registerkarte **iOS** aus, und aktivieren Sie das Kontrollkästchen **iOS-Anmeldung aktivieren** .  

    4.  Klicken Sie auf **Durchsuchen**, und wechseln Sie zu der von Apple heruntergeladenen APNs-Zertifikatdatei (CER-Datei). Configuration Manager zeigt die APNs-Zertifikatinformationen an. Klicken Sie auf **OK** , um das APNs-Zertifikat in Intune zu speichern.  

 Nachdem Sie die Einrichtung abgeschlossen haben, müssen Sie Ihre Benutzer informieren, wie sie ihre Geräte registrieren sollen. Informationen hierzu finden Sie unter [Informieren der Benutzer über den Einsatz von Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Diese Informationen gelten für mobile Geräte, die mit Microsoft Intune und Configuration Manager verwaltet werden.



<!--HONumber=Nov16_HO1-->

