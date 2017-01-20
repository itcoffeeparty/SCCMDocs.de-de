---
title: "Einrichten einer hybriden Windows-Geräteverwaltung mit System Center Configuration Manager und Microsoft Intune | Microsoft-Dokumentation"
description: "Richten Sie eine Windows-Geräteverwaltung mit System Center Configuration Manager und Microsoft Intune ein."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 808327495c66f4e6ad86ab144455014171a453b2


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Einrichten einer hybriden Windows-Geräteverwaltung mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können Configuration Manager mit Intune verwenden, um Desktopcomputer, Laptops und andere Geräte, die Windows ausführen, als mobile Geräte zu verwalten. Sie können Azure Active Directory einrichten, um die automatische Registrierung von Windows-PCs zu ermöglichen. Sie können Configuration Manager auch so konfigurieren, dass die Registrierung mit der Unternehmensportal-App vereinfacht werden kann.


Optionen für Windows-Registrierung:

- [Automatische Registrierung mit Azure AD](#azure-active-directory-enrollment)
- [Windows-PCs](#set-up-windows-device-enrollment)
- [Windows 10 Mobile- und Windows Phone-Geräte](#enable-windows-phone-devices)

## <a name="azure-active-directory-enrollment"></a>Registrierung mit Azure Active Directory

Die automatische Registrierung ermöglicht Benutzern das Registrieren von unternehmenseigenen oder persönlichen Windows 10-PCs und Windows 10-Mobilgeräten in Intune, indem ein Geschäfts-, Uni- oder Schulkonto hinzugefügt und die Verwaltung akzeptiert wird. Im Hintergrund registriert der Benutzer das Gerät und verknüpft Azure Active Directory. Nach der Registrierung kann das Gerät mit Intune verwaltet werden.

**Voraussetzungen**
- Azure Active Directory Premium-Abonnement ([Testabonnement](http://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune-Abonnement


### <a name="configure-automatic-mdm-enrollment"></a>Konfigurieren der automatischen MDM-Registrierung

1. Navigieren Sie im [Azure-Verwaltungsportal](https://manage.windowsazure.com) (https://manage.windowsazure.com) zum Knoten **Active Directory**, und wählen Sie Ihr Verzeichnis aus.

2. Klicken Sie auf die Registerkarte **Anwendungen**, und anschließend sollten Sie **Microsoft Intune** in der Liste der Anwendungen sehen.

    ![Azure AD-Apps mit Microsoft Intune](../media/aad-intune-app.png)

3. Klicken Sie auf den Pfeil für **Microsoft Intune**. Daraufhin sollte eine Seite angezeigt werden, auf der Sie Microsoft Intune konfigurieren können.

4. Klicken Sie auf **Konfigurieren**, um die automatische MDM-Registrierung mit Microsoft Intune zu konfigurieren.

5. Geben Sie die URLs für Intune an:

  - **MDM-Registrierungs-URL** – Verwenden Sie `https://enterpriseenrollment-s.manage.microsoft.com/EnrollmentServer/Discovery.svc` für die MDM-Registrierungs-URL.
  - **URL für MDM-Nutzungsbedingungen** – Verwenden Sie den Standardwert. Diese URL zeigt Nutzungsbedingungen für Benutzer bei der Registrierung von Geräten.
  - **URL für MDM-Kompatibilität** – Verwenden Sie den Standardwert. Wenn ein Gerät nicht kompatibel ist, wird die Nachricht **Zugriff verweigert** mit dieser URL angezeigt. Die URL verweist auf eine Seite, mit der Benutzer verstehen können, warum ihr Gerät nicht mit Richtlinien kompatibel ist, und wie sie die Kompatibilität wiederherstellen können.

6.  Geben Sie an, welche Geräte welcher Benutzer von Microsoft Intune verwaltet werden sollen. Die Windows 10-Geräte dieser Benutzer werden automatisch für die Verwaltung mit Microsoft Intune registriert.

  - **Alle**
  - **Gruppen**
  - **Keine**

7. Wählen Sie **Speichern** aus.

## <a name="configure-windows-pc-enrollment"></a>Konfigurieren der Windows-PC-Registrierung
 Sie müssen die Verwaltung für das Betriebssystem aktivieren, um die Verwaltung für mobile Windows-Geräte zu aktivieren.  Sie können auch einen DNS CNAME zur Vereinfachung der Registrierung für Benutzer hinzufügen.

### <a name="create-dns-alias-for-device-enrollment"></a>Erstellen eines DNS-Alias für die Geräteregistrierung  
 Wenn ein DNS-Alias (CNAME-Eintrag) vorhanden ist, können Benutzer ihre Geräte einfacher registrieren, da der Servername bei der Geräteregistrierung automatisch eingetragen wird. Zum Erstellen eines DNS-Alias (CNAME-Eintragstyp) müssen Sie einen CNAME in den DNS-Einträgen Ihres Unternehmens konfigurieren, der Anforderungen, die an eine URL Ihrer Unternehmensdomäne gesendet werden, an die Microsoft-Server für Clouddienste umleitet.  Wenn die Domäne Ihres Unternehmens beispielsweise „contoso.com“ heißt, sollten Sie einen CNAME im DNS erstellen, der „EnterpriseEnrollment.contoso.com“ an „EnterpriseEnrollment-s.manage.microsoft.com“ umleitet.  

|Typ|Hostname|Verweist auf|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  
### <a name="to-enable-enrollment-for-windows-devices"></a>So aktivieren Sie die Registrierung für Windows-Geräte  

1.  **Voraussetzungen** ‒ Bevor Sie die Registrierung einer Plattform einrichten können, müssen Sie die Voraussetzungen und Schritte in [Einrichten der hybriden Verwaltung mobiler Geräte](setup-hybrid-mdm.md) erfüllen und ausführen.  

2.  Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Clouddienste** > **Microsoft Intune-Abonnements**.  

    > [!WARNING]  
    >  Wenn andere Configuration Manager-Dialogfelder geöffnet sind, müssen Sie diese schließen, bevor Sie mit diesem Vorgang fortfahren.  

3.  Klicken Sie auf der Registerkarte **Startseite** auf **Plattformen konfigurieren**und dann auf **Windows**.  

4.  Wählen Sie auf der Registerkarte **Allgemeine** die Option **Windows-Registrierung aktivieren**aus.  

 Nachdem Sie die Einrichtung abgeschlossen haben, müssen Sie Ihre Benutzer informieren, wie sie ihre Geräte registrieren sollen. Informationen hierzu finden Sie unter [Informieren der Benutzer über den Einsatz von Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Diese Informationen gelten für mobile Geräte, die mit Microsoft Intune und Configuration Manager verwaltet werden.

## <a name="enable-windows-phone-devices"></a>Aktivieren der Windows Phone-Geräte  
  Wenn Ihre Benutzer nur Geräte mit Windows Phone 8.1 und höher registrieren werden und Sie keine Branchen-Apps auf Windows Phone-Geräten bereitstellen möchten, ist kein Symantec-Zertifikat erforderlich. Nach der Aktivierung der Windows Phone-Registrierung müssen Sie die Benutzer anweisen, die Unternehmensportal-App aus dem Windows Phone Store zu installieren, um ihre Geräte zu registrieren.  

  Führen Sie die folgenden Schritte für die Windows Phone-Geräte aus, die Sie verwalten.  

### <a name="to-enable-enrollment-for-windows-phone-81-and-later-devices"></a>So aktivieren Sie die Registrierung für Geräte mit Windows Phone 8.1 und höher  

 1.  **Voraussetzungen** ‒ Bevor Sie die Registrierung einer Plattform einrichten können, müssen Sie die Voraussetzungen und Schritte in [Einrichten der hybriden Verwaltung mobiler Geräte](setup-hybrid-mdm.md) erfüllen und ausführen.  

 2.  Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Clouddienste** > **Microsoft Intune-Abonnements**.  

     > [!WARNING]  
     >  Wenn andere Configuration Manager-Dialogfelder geöffnet sind, müssen Sie diese schließen, bevor Sie mit diesem Vorgang fortfahren.  

 3.  Klicken Sie auf der Registerkarte **Startseite** auf **Plattformen konfigurieren**und dann auf **Windows Phone**.  

 4.  Klicken Sie auf der Registerkarte **Allgemein** auf  **Windows Phone 8.1 und Windows 10 Mobile**. Sie können AET-Daten (Application Enrollment Token, Anwendungsregistrierungstoken) als XML-Datei oder alternativ eine PFX-Datei hochladen, um die Bereitstellung des Unternehmensportals zu unterstützen. Sie können aber auch die Benutzer auffordern, sich das Unternehmensportal vom Windows Phone Store herunterzuladen.  

      Klicken Sie auf **OK**.  

  Nachdem Sie die Einrichtung abgeschlossen haben, müssen Sie Ihre Benutzer informieren, wie sie ihre Geräte registrieren sollen. Informationen hierzu finden Sie unter [Informieren der Benutzer über den Einsatz von Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Diese Informationen gelten für mobile Geräte, die mit Microsoft Intune und Configuration Manager verwaltet werden.  



<!--HONumber=Dec16_HO3-->


