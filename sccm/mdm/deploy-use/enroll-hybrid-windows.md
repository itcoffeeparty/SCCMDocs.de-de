---
title: "Einrichten einer hybriden Windows-Geräteverwaltung mit System Center Configuration Manager und Microsoft Intune | Microsoft-Dokumentation"
description: "Richten Sie eine Windows-Geräteverwaltung mit System Center Configuration Manager und Microsoft Intune ein."
ms.custom: na
ms.date: 03/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a8218e23743dafaf8ff1166142cf2dcca1212133
ms.openlocfilehash: 996d01d3c5d5be4544246a5f321f67b60a8f5508
ms.lasthandoff: 03/14/2017


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Einrichten einer hybriden Windows-Geräteverwaltung mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Diese Thema erklärt IT-Administratoren, wie sie Ihre Benutzer dazu bringen können, Windows-PCs und mobile Geräte mithilfe von Configuration Manager und Microsoft Intune zu verwalten. Zwei Registrierungsmethoden stehen hierbei zur Verfügung:
-  Die automatische Registrierung mit Azure Active Directory (AD), wenn Benutzer Ihr Konto mit einem Gerät verbinden
- Die Anmeldung über Installation und Registrierung in der Unternehmensportal-App

## <a name="choose-how-to-enroll-windows-devices"></a>Auswählen, wie Windows-Geräte registriert werden

Zwei Faktoren bestimmen, wie Sie Windows-Geräte registrieren können:
- **Verwenden Sie Azure Active Directory Premium?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) ist in Enterprise Mobility + Security und in anderen Lizenzierungsplänen enthalten.
- **Welche Versionen von Windows-Clients werden registriert?** <br>Windows 10-Geräte können automatisch durch Hinzufügen eines Geschäfts-oder Schulkontos registriert werden. Frühere Versionen müssen mithilfe der Unternehmensportal-App registriert werden.

||**Azure AD Premium**|**AD (Sonstiges)**|
|----------|---------------|---------------|  
|**Windows 10**|[Automatische Registrierung](#automatic-enrollment) |[Unternehmensportal-Registrierung](#company-portal-enrollment)|
|**Frühere Windows-Versionen**|[Unternehmensportal-Registrierung](#company-portal-enrollment)|[Unternehmensportal-Registrierung](#company-portal-enrollment)|

## <a name="automatic-enrollment"></a>Automatische Registrierung

Die automatische Registrierung ermöglicht Benutzern das Registrieren von unternehmenseigenen oder persönlichen Windows 10-Geräten in Intune, indem ein Geschäfts-, Uni- oder Schulkonto hinzugefügt und die Verwaltung akzeptiert wird. Im Hintergrund registriert der Benutzer das Gerät und verknüpft Azure Active Directory. Nach der Registrierung kann das Gerät mit Intune verwaltet werden. Verwaltete Geräte können weiterhin das Unternehmensportal für Aufgaben verwenden, müssen es jedoch nicht installieren, um registriert zu werden.

**Voraussetzungen**
- Azure Active Directory Premium-Abonnement ([Testabonnement](http://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune-Abonnement

### <a name="configure-automatic-enrollment"></a>Konfigurieren der automatischen Registrierung

1. Melden Sie sich im [Azure-Portal](https://manage.windowsazure.com) an, navigieren Sie zum Knoten **Active Directory** im linken Bereich, und wählen Sie Ihr Verzeichnis aus.
2. Wählen Sie die Registerkarte **Konfigurieren** aus, und scrollen Sie zum Abschnitt **Geräte**.
3. Wählen Sie **Alle** für **Users may workplace join devices** (Benutzer dürfen eine Arbeitsbereichverknüpfung für Geräte durchführen) aus.
4. Wählen Sie die maximale Anzahl der Geräte aus, die Sie pro Benutzer autorisieren möchten.

Standardmäßig ist die zweistufige Authentifizierung für den Dienst nicht aktiviert. Die zweistufige Authentifizierung wird jedoch empfohlen, wenn Sie ein Gerät registrieren. Bevor die zweistufige Authentifizierung für diesen Dienst erforderlich ist, müssen Sie einen Anbieter für die zweistufige Authentifizierung in Azure Active Directory und Ihre Benutzerkonten konfigurieren. Weitere Informationen finden Sie unter [Erste Schritte mit Azure Multi-Factor Authentication-Server](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="company-portal-enrollment"></a>Unternehmensportal-Registrierung
Ihre Endbenutzer oder ein [Geräteregistrierungs-Manager](enroll-devices-with-device-enrollment-manager.md) können Windows-Geräte registrieren, indem Sie die Unternehmensportal-App installieren und sich dann mit ihren Unternehmensanmeldeinformationen anmelden. Um die Registrierung für Ihre Endbenutzer zu vereinfachen, sollten Sie Ihrer DNS-Registrierung einen CNAME-Eintrag hinzufügen.

### <a name="enable-windows-device-management"></a>Aktivieren der Windows-Geräteverwaltung
Um die Windows-Geräteverwaltung entweder für PCs oder mobile Geräte zu aktivieren, führen Sie die folgenden Schritte aus:

1.  Bevor Sie die Registrierung einer Plattform einrichten, müssen Sie die Voraussetzungen und Schritte in [Einrichten der hybriden Verwaltung mobiler Geräte](setup-hybrid-mdm.md) erfüllen und ausführen.  
2.  Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Übersicht** > **Clouddienste** > **Microsoft Intune-Abonnements**.  
3.  Klicken Sie im Menüband auf **Plattformen konfigurieren**, und wählen Sie anschließend die Windows-Plattform aus:
    - **Windows** für Windows-PCs und -Laptops, führen Sie dann die folgenden Schritte aus:
      1. Klicken Sie auf der Registerkarte **Allgemeine** auf das Kontrollkästchen **Windows-Registrierung aktivieren**.
      2. Wenn Sie ein Zertifikat zur Codesignatur verwenden und die Unternehmensportal-App bereitstellen, navigieren Sie zum **Codesignaturzertifikat**. Gerätebenutzer können auch die Unternehmensportal-App aus dem Windows Store installieren, oder Sie können die App aus dem Windows Store für Unternehmen ohne Codesignatur bereitstellen.
      3. Sie können auch die [Windows Hello for Business-Einstellungen](windows-hello-for-business-settings.md) konfigurieren.
    - **Windows Phone** für Windows-Telefone und -Tablets, führen Sie dann die folgenden Schritte aus:
      1. Klicken Sie auf der Registerkarte **Allgemein** auf das Kontrollkästchen **Windows Phone 8.1 und Windows 10 Mobile**. Windows Phone 8.0 wird nicht mehr unterstützt.
      2. Wenn Ihr Unternehmen Unternehmens-Apps per Sideload übertragen muss, können Sie das erforderliche Token oder die erforderliche Datei hochladen. Weitere Informationen zum Sideloaden von Apps finden Sie unter [Erstellen von Windows-Anwendungen mit System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Anwendungsregistrierungstoken**
        - **PFX-Datei**
        - **Keine** Wenn Sie ein Symantec-Zertifikat verwenden, können Sie **Show an alert before Symantec certificates expire** (Warnung anzeigen, bevor Symantec-Zertifikate ablaufen) angeben.
4. Klicken Sie auf **OK** , um das Dialogfeld zu schließen.  Um die Registrierung über das Unternehmensportal zu vereinfachen, sollten Sie einen DNS-Alias für die Registrierung des Geräts erstellen. Sie können Benutzern dann mitteilen, wie sie ihre Geräte registrieren.

### <a name="create-dns-alias-for-device-enrollment"></a>Erstellen eines DNS-Alias für die Geräteregistrierung  
Ein DNS-Alias (CNAME-Eintragstyp) erleichtert den Benutzern das Registrieren ihrer Geräte durch eine Verbindung mit dem Dienst, ohne dass die Eingabe einer Serveradresse nötig ist. Zum Erstellen eines DNS-Alias (CNAME-Eintragstyp) müssen Sie einen CNAME in den DNS-Einträgen Ihres Unternehmens konfigurieren, der Anforderungen, die an eine URL Ihrer Unternehmensdomäne gesendet werden, an die Microsoft-Server für Clouddienste umleitet.  Wenn die Domäne Ihres Unternehmens beispielsweise „contoso.com“ heißt, sollten Sie einen CNAME im DNS erstellen, der „EnterpriseEnrollment.contoso.com“ an „EnterpriseEnrollment-s.manage.microsoft.com“ umleitet.  

 Obwohl das Erstellen eines CNAME-DNS-Eintrags optional ist, ist die Registrierung mit einem CNAME-Eintrag für den Benutzer leichter. Wenn kein CNAME-Eintrag für die Registrierung gefunden wurde, werden Benutzer aufgefordert, manuell den MDM-Servernamen „enrollment.manage.microsoft.com“ einzugeben.

|Typ|Hostname|Verweist auf|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 Stunde|

Wenn Sie mehr als ein UPN-Suffix haben, müssen Sie einen CNAME für jeden Domänennamen erstellen und jeden auf EnterpriseEnrollment-s.manage.microsoft.com zeigen. Wenn z.B. Benutzer unter Contoso name@contoso.com aber auch name@us.contoso.com und name@eu.constoso.com als ihre E-Mail/UPN verwenden, muss der Contoso-DNS-Administrator die folgenden CNAMEs erstellen.

|Typ|Hostname|Verweist auf|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 Stunde|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 Stunde|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 Stunde|

## <a name="tell-users-how-to-enroll-devices"></a>Benutzern erklären, wie sie Geräte registrieren  

 Nachdem Sie die Einrichtung abgeschlossen haben, müssen Sie Ihre Benutzer informieren, wie sie ihre Geräte registrieren sollen. Anleitungen hierzu finden Sie unter [Informieren der Benutzer über den Einsatz von Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Sie können Benutzer an [Registrieren Ihres Windows-Geräts bei Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows) weiterleiten. Diese Informationen gelten für mobile Geräte, die mit Microsoft Intune und Configuration Manager verwaltet werden.

> [!div class="button"]
[< Vorheriger Schritt](create-service-connection-point.md) [Nächster Schritt >](set-up-additional-management.md)

