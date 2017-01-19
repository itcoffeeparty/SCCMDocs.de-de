---
title: "Einrichten der hybriden Verwaltung mobiler Geräte | Microsoft-Dokumentation"
description: "Richten Sie die Registrierung von Hybridgeräten mit Configuration Manager und Intune ein."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 48b91e88f78752cf7c05162b701ea2ca2f401de3
ms.openlocfilehash: 85df3df19f01f8ed6f5240851c47afce01a92880

---

# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Einrichten der hybriden Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*


Bevor Sie iOS, Windows und Android-Geräte mit Configuration Manager verwalten können, müssen sie mit Intune registriert werden. Verwenden Sie die folgenden Schritte, um die Registrierung von Hybridgeräten mit Configuration Manager und Intune einzurichten. Mithilfe der folgenden Schritte aktivieren Sie die BYOD-Registrierung (Bring Your Own Device) für Ihre Benutzer. Diese Schritte sind auch die Voraussetzung für die [Registrierung von unternehmenseigenen Geräten](enroll-company-owned-devices.md).

 |Schritte|Details|  
 |-----------|-------------|  
 |**Schritt 1:** [Erstellen einer MDM-Sammlung](#step-1-create-an-mdm-collection)|Erstellen Sie eine Configuration Manager-Benutzersammlung mit Benutzern, deren Geräte registriert werden können.|  
 |**Schritt 2:** [Anforderungen an den Domänennamen](#step-2-domain-name-requirements)|Bestätigen Sie, dass der Domain Name Service (DNS) Ihrer Organisation und die Active Directory-Benutzerverwaltung die MDM-Anforderungen erfüllen.|
 |**Schritt 3:** [Konfigurieren des Intune-Abonnements](#step-3-configure-intune-subscription)|Der Intune-Dienst ermöglicht die Verwaltung von Geräten über das Internet.|  
 |**Schritt 4:** [Hinzufügen von Geschäftsbedingungen](#step-4-add-terms-and-conditions)| Erstellen Sie Geschäftsbedingungen, die von Benutzern akzeptiert werden müssen, bevor die Unternehmensportal-App verwendet werden kann.|
 |**Schritt 5:** [Erstellen eines Dienstverbindungspunkts](#step-5-create-service-connection-point)|Vom Dienstverbindungspunkt werden Einstellungen und Softwarebereitstellungsinformationen an Configuration Manager gesendet sowie Status- und Inventurmeldungen von mobilen Geräten abgerufen. |  
 |**Schritt 6:** [Aktivieren der Plattformregistrierung](#step-6-enable-platform-enrollment)|Die MDM-Registrierung für [iOS](#ios-and-mac-enrollment-setup)- und [Windows](#windows-enrollment-setup)-Geräte erfordert zusätzliche Schritte für die Kommunikation zwischen dem Dienst und Geräten. Für Android ist keine weitere Konfiguration erforderlich.|  
 |**Schritt 7:** [Einrichten zusätzlicher Verwaltung](#step-7-set-up-additional-management)|(Optional) Richten Sie Konfigurationselemente und den bedingten Zugriff für registrierte Geräte ein.|
 |**Schritt 8:** [Überprüfen der MDM-Konfiguration](#step-8-verify-mdm-configuration)|Zeigen Sie Protokolldateien an, um zu bestätigen, dass der Dienstverbindungspunkt erfolgreich erstellt wurde und Benutzerkonten synchronisiert werden.|
 |**Schritt 9:** [Registrieren von Geräten](#step-9-enroll-devices)|Teilen Sie den Benutzern mit, wie sie ihre Geräte registrieren können, oder registrieren Sie unternehmenseigene Geräte, um den Anforderungen Ihrer Organisation gerecht zu werden.|

Möchten Sie Intune ohne Configuration Manager?
> [!div class="button"]
[Intune Dokumente anzeigen >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)

## <a name="step-1-create-an-mdm-collection"></a>Schritt 1: Erstellen einer MDM-Sammlung
Sie benötigen die Configuration Manager-Benutzersammlung, um Benutzer anzugeben, durch die Geräte zur Verwaltung registriert werden können. Nur Benutzersammlungen kommen in Frage, da Intune-Lizenzen Benutzern zugewiesen werden. Sie können zu Testzwecken eine **Direktregel** einrichten und bestimmte Benutzer hinzufügen, die Geräte registrieren können. Wählen Sie an der Configuration Manager-Konsole **Bestand und Kompatibilität** > **Benutzersammlungen** aus, und klicken Sie auf die Registerkarte **Startseite** > Gruppe **Erstellen** und dann auf **Benutzersammlung erstellen**. Verwenden Sie für eine größer angelegte Verteilung **Abfrageregeln**, um Benutzer zu definieren. Weitere Informationen zu Sammlungen finden Sie unter [Erstellen von Sammlungen](https://technet.microsoft.com/library/mt629371.aspx).

![Erstellen einer Benutzersammlung für MDM](../media/mdm-create-user-collection.png)

## <a name="step-2-domain-name-requirements"></a>Schritt 2: Anforderungen an den Domänennamen

Führen Sie gegebenenfalls folgende Schritte durch, um Abhängigkeiten außerhalb von Configuration Manager zu erfüllen:

1. Jedem Benutzer muss eine Intune-Lizenz zugewiesen werden, um Geräte zu registrieren. Um Intune-Lizenzen mit Benutzern zu verknüpfen, benötigt jeder Benutzer einen Benutzerprinzipalnamen (UPN), der öffentlich aufgelöst werden kann (z.B. johndoe@contoso.com) oder eine alternative Anmelde-ID, die in Azure Active Directory konfiguriert wurde. Das Konfigurieren einer alternativen ID ermöglicht Benutzern z.B. die Anmeldung mit einer E-Mail-Adresse, auch wenn ihr UPN in einem NetBIOS-Format (z.B. CONTOSO\johndoe) vorliegt.

  - Wenn Ihr Unternehmen öffentlich auflösbare UPNs verwendet (d.h. johndoe@contoso.com),, ist keine weitere Konfiguration erforderlich.
  - Wenn Ihr Unternehmen einen nicht auflösbaren UPN verwendet (d.h. CONTOSO\johndoe), müssen Sie [eine alternative ID in Azure Active Directory konfigurieren](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2.  Stellen Sie Active Directory-Verbunddienste (AD FS) bereit, und konfigurieren Sie diese. (Optional)

     Wenn Sie das einmalige Anmelden einrichten, können sich die Benutzer mit ihren normalen Unternehmensanmeldeinformationen anmelden, um auf die Dienste in Intune zuzugreifen.

     Weitere Informationen finden Sie unter den folgenden Themen:
    -   [Vorbereiten des einmaligen Anmeldens](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [Planen und Bereitstellen von AD FS 2.0 für die Verwendung mit dem einmaligen Anmelden](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  Stellen Sie die Verzeichnissynchronisierung bereit, und konfigurieren Sie sie.

     Mithilfe der Verzeichnissynchronisierung können Sie Intune mit synchronisierten Benutzerkonten auffüllen. Die synchronisierten Benutzerkonten und Sicherheitsgruppen werden Intune hinzugefügt. Ein Fehler beim Aktivieren der Verzeichnissynchronisierung ist eine häufige Ursache dafür, dass Geräte beim Einrichten von Configuration Manager-MDM mit Microsoft Intune nicht registriert werden können.

     Weitere Informationen finden Sie unter [Verzeichnisintegration](http://go.microsoft.com/fwlink/?LinkID=271120) in der Active Directory-Dokumentationsbibliothek.

4.  Optional, jedoch nicht empfohlen: Setzen Sie die Microsoft Online-Kennwörter von Benutzern zurück, wenn AD FS nicht verwendet wird.

     Wenn Sie AD FS nicht verwenden, müssen Sie für jeden Benutzer ein Microsoft Online-Kennwort festlegen.

## <a name="step-3-configure-intune-subscription"></a>Schritt 3: Konfigurieren des Intune-Abonnements
 Das Intune-Abonnement ermöglicht die Verwaltung von Geräten über das Internet. Dazu gehört auch, Benutzersammlungen anzugeben, die Geräte registrieren können, und Informationen zu definieren, die für Benutzer angezeigt werden. Die Intune-Abonnement dient zu folgenden Zwecken:

-   Abrufen des Zertifikats, das vom Dienstverbindungspunkt zum Herstellen einer Verbindung mit dem Intune-Dienst benötigt wird
-   Definieren der Benutzersammlung, die Benutzern das Anmelden ihrer mobilen Geräte ermöglicht
-   Definieren und Konfigurieren der mobilen Plattformen, die Sie unterstützen möchten

> [!IMPORTANT]
>  Durch das Erstellen eines Abonnements für Microsoft Intune in Configuration Manager wechselt der Dienstverbindungspunkt Ihres Standorts in den „Onlinemodus“. Weitere Informationen finden Sie unter [Informationen zum Dienstverbindungspunkt in System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).

### <a name="to-create-the-microsoft-intune-subscription"></a>So erstellen Sie das Microsoft Intune-Abonnement

1.  Registrieren Sie sich für ein Microsoft Intune-Konto bei [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216), falls dies noch nicht geschehen ist.  Nachdem Sie Ihr Intune-Konto erstellt haben, ist es nicht erforderlich, Benutzer dem Intune-Konto hinzuzufügen oder zusätzliche Einstellungen zu konfigurieren.

2.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.

3.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Clouddienste**, und klicken Sie auf **Microsoft Intune-Abonnements**. Klicken Sie auf der Registerkarte **Startseite** auf **Microsoft Intune-Abonnement hinzufügen**.

![Erstellen eines Intune-Abonnements](../media/mdm-set-intune.png)

4.  Lesen Sie im Assistenten zum Erstellen von Microsoft Intunes-Abonnements den Text auf der Seite **Einleitung** , und klicken Sie dann auf **Weiter**.

5.  Klicken Sie auf der Seite **Abonnement** auf **Anmelden** , und melden Sie sich mit Ihrem Geschäfts- oder Schulkonto an. Aktivieren Sie im Dialogfeld **Autorität für die Verwaltung mobiler Geräte festlegen** das Kontrollkästchen für die alleinige Verwaltung mobiler Geräte mit Configuration Manager über die Configuration Manager-Konsole. Sie müssen diese Option auswählen, um den Vorgang zum Erstellen Ihres Abonnements fortsetzen zu können.

    > [!IMPORTANT]
    >  Wenn Sie Configuration Manager als Autorität für die Verwaltung ausgewählt haben, können Sie die Autorität für die Verwaltung nachfolgend nicht mehr in Microsoft Intune ändern.

6.  Klicken Sie auf die Datenschutzlinks, um die entsprechenden Informationen zu lesen, und klicken Sie dann auf **Weiter**.

7.  Geben Sie auf der Seite **Allgemein** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.

  -   **Sammlung**: Geben Sie eine Benutzersammlung an, in der die Benutzer enthalten sind, die ihre mobilen Geräte anmelden dürfen.

      > [!NOTE]
      >  Wird ein Benutzer aus der Sammlung entfernt, wird das Gerät des Benutzers noch bis zu 24 Stunden verwaltet, nachdem der Benutzerdatensatz aus der Benutzerdatenbank entfernt wurde.

  -   **Firmenname**: Geben Sie den Namen Ihres Unternehmens ein.

  -   **Datenschutzdokumentations-URL des Untern.**: Wenn Sie die Datenschutzinformationen Ihres Unternehmens über einen Link veröffentlichen, auf den über das Internet zugegriffen werden kann, stellen Sie einen Link bereit, auf den die Benutzer über das Unternehmensportal zugreifen können, z. B. „http://www.contoso.com/CP_privacy.html“. Aus den Datenschutzinformationen geht hervor, welche Informationen Benutzer für Ihr Unternehmen freigeben.

  -   **Farbschema für Unternehmensportal**: Sie können optional die Standardfarbe Blau für Unternehmensportale ändern.

  -   **Configuration Manager-Standortcode**: Geben Sie einen Standortcode für einen primären Standort zum Verwalten der mobilen Geräte an.

    > [!NOTE]
    >  Das Ändern des Standortcodes wirkt sich nur auf neue Anmeldungen aus und beeinflusst gegenwärtig angemeldete Geräte nicht.

8.  Geben Sie auf der Seite **Kontaktdaten des Unternehmens** die Kontaktdaten des Unternehmens an, die unter **An IT-Abteilung wenden** in der Unternehmensportal-App angezeigt werden. Geben Sie Kontaktinformationen für Ihr Unternehmen ein, und klicken Sie dann auf **Weiter**.

9. Auf der Seite **Firmenlogo** können Sie wählen, ob Logos im Unternehmensportal angezeigt werden sollen. Klicken Sie dann auf **Weiter**.

10. Schließen Sie den Assistenten ab.

## <a name="step-4-add-terms-and-conditions"></a>Schritt 4: Hinzufügen von Geschäftsbedingungen
 Sobald Sie die Intune-Verwaltung für mobile Geräte konfiguriert haben, können Sie **allgemeine Geschäftsbedingungen**erstellen. Verwenden Sie die allgemeinen Geschäftsbedingungen, um Benutzern zu erklären, was geschieht, wenn sie ihre Geräte registrieren. Benutzer müssen die allgemeinen Geschäftsbedingungen akzeptieren, bevor sie ein Gerät registrieren können. Wechseln Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität** > **Übersicht** > **Kompatibilitätseinstellungen** > **Geschäftsbedingungen**, und klicken Sie dann auf **Geschäftsbedingungen erstellen**. Weitere Informationen finden Sie unter [Geschäftsbedingungen in System Center Configuration Manager](terms-and-conditions.md).

##  <a name="step-5-create-service-connection-point"></a>Schritt 5: Erstellen eines Dienstverbindungspunkts
Nachdem Sie Ihr Abonnement erstellt haben, können Sie die Standortsystemrolle „Dienstverbindungspunkt“ installieren, die es Ihnen ermöglicht, eine Verbindung mit dem Intune-Dienst herzustellen. Von dieser Standortsystemrolle werden Einstellungen und Anwendungen mittels Push an den Intune-Dienst übertragen.

 Vom Dienstverbindungspunkt werden Einstellungen und Softwarebereitstellungsinformationen an Configuration Manager gesendet sowie Status- und Inventurmeldungen von mobilen Geräten abgerufen. Der Configuration Manager-Dienst fungiert als Gateway, das mit mobilen Geräten kommuniziert und Einstellungen speichert.

> [!NOTE]
>  Die Standortsystemrolle „Dienstverbindungspunkt“ kann nur an einem Standort der zentralen Verwaltung oder an einem eigenständigen primären Standort installiert werden. Der Dienstverbindungspunkt muss über Internetzugriff verfügen.


### <a name="configure-the-service-connection-point-role"></a>Konfigurieren der Rolle „Dienstverbindungspunkt“

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standorte**, und klicken Sie dann auf **Server und Standortsystemrollen**.

3.  Fügen Sie einem neuen oder vorhandenen Standortsystemserver die Rolle **Dienstverbindungspunkt** wie folgt hinzu:

    -   Neuer Standortsystemserver: Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Standortsystemserver erstellen** , um den Assistenten zum Erstellen von Standortsystemservern zu starten.

    -   Bestehender Standortsystemserver: Klicken Sie auf den Server, auf dem die Rolle „Dienstverbindungspunkt“ installiert werden soll. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Server** auf **Standortsystemrollen hinzufügen** , um den Assistenten zum Hinzufügen von Standortsystemrollen zu starten.

4.  Wählen Sie auf der Seite **Systemrollenauswahl** die Option **Dienstverbindungspunkt**, und klicken Sie auf **Weiter**.

![Erstellen eines Dienstverbindungspunkts](../media/mdm-service-connection-point.png)

5.  Schließen Sie den Assistenten ab.

### <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>Wie authentifiziert sich der Dienstverbindungspunkt beim Microsoft Intune-Dienst?
 Der Systemverbindungspunkt erweitert den Configuration Manager, indem er eine Verbindung mit dem cloudbasierten Intune-Dienst herstellt, der mobile Geräte über das Internet verwaltet. Die Authentifizierung des Dienstverbindungspunkts beim Intune-Dienst geschieht auf folgende Weise:

1.  Beim Erstellen eines Intune-Abonnements in der Configuration Manager-Konsole wird der Configuration Manager-Administrator durch Herstellen einer Verbindung mit Azure Active Directory authentifiziert. Dadurch erfolgt eine Umleitung zum jeweiligen AD FS-Server, der zur Eingabe des Benutzernamens und Kennworts auffordert. Anschließend stellt Intune ein Zertifikat für den Mandanten aus.

2.  Das Zertifikat aus Schritt 1 wird in der Standortrolle „Dienstverbindungspunkt“ installiert und zum Authentifizieren und Autorisieren der gesamten weiteren Kommunikation mit dem Microsoft Intune-Dienst verwendet.

## <a name="step-6-enable-platform-enrollment"></a>Schritt 6: Aktivieren der Plattformregistrierung
  Verschiedene Geräteplattformen erfordern eine zusätzliche Konfiguration, damit Geräte registriert werden können:
  - [iOS- und Macintosh-Registrierungs-Setup](#ios-and-mac-enrollment-setup): Rufen Sie ein Apple-MDM-Push-Zertifikat ab.
  - [Windows-Registrierungs-Setup](#windows-enrollment-setup): Konfigurieren Sie DNS, und aktivieren Sie die Registrierung für Windows-PCs, Windows 10 Mobile- und Windows Phone-Geräte.
  - Android: Für Android-Geräte sind keine weiteren Schritte für die Aktivierung der Registrierung erforderlich.

Sobald Sie die MDM-Verwaltung aktiviert haben, können Sie die Anzahl der Geräte festlegen, die jeder Benutzer registrieren kann – max. 15 Geräte pro Benutzer.

### <a name="ios-and-mac-enrollment-setup"></a>iOS- und Macintosh-Registrierungs-Setup
  Mit den folgenden Schritten aktivieren Sie die Verwaltung für Apple-Geräte, indem Sie ein Apple-MDM-Push-Zertifikat in den Intune-Dienst hochladen.

  1.  **Herunterladen einer Zertifikatsignieranforderung** : Eine CSR-Datei (Zertifikatsignieranforderung) ist erforderlich, um ein APNs-Zertifikat von Apple anzufordern.  

      1.  Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Clouddienste**> **Microsoft Intune-Abonnements**.  

      2.  Klicken Sie auf der Registerkarte **Startseite** auf **APNs-Zertifikatanforderung erstellen**. Das Dialogfeld **APNs-Zertifikatsignieranforderung anfordern** wird geöffnet.  

      3.  **Navigieren** Sie zu dem Pfad, um die neue CSR-Datei (Zertifikatsignieranforderung) zu speichern. Speichern Sie die Zertifikatsignierungsanforderung (CSR-Datei) lokal.  

      4.  Klicken Sie auf **Herunterladen**. Die neue CSR-Datei von Microsoft Intune wird heruntergeladen und von Configuration Manager gespeichert. Die CSR-Datei wird verwendet, um ein Vertrauensstellungszertifikat vom Apple Push Certificates-Portal anzufordern.  

  2.  **Anfordern eines APNs-Zertifikats von Apple** : Das APNs-Zertifikat (Apple Push Notification Service) dient zum Einrichten einer Vertrauensstellung zwischen dem Verwaltungsdienst, Intune und registrierten iOS-Mobilgeräten.  

      1.  Navigieren Sie in einem Browser zum [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) , und melden Sie sich mit der Apple-ID Ihres Unternehmens an. Diese Apple-ID muss später verwendet werden, um das APNs-Zertifikat zu erneuern.  

      2.  Schließen Sie den Assistenten mithilfe der Datei mit der Zertifikatsignierungsanforderung (CSR) ab. Laden Sie das APNs-Zertifikat herunter, und speichern Sie die PEM-Datei lokal. Diese APNs-Zertifikatdatei (.pem) wird verwendet, um eine Vertrauensstellung zwischen dem Apple Push Notification-Server und der Verwaltungsautorität für mobile Geräte von Intune herzustellen.  

  3.  **Aktivieren der Registrierung und Hochladen des APNs-Zertifikats** : Zum Aktivieren der iOS-Registrierung laden Sie das APNs-Zertifikat hoch.  

      1.  Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Clouddienste** > **Microsoft Intune-Abonnement**.  

      2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Abonnement** auf **Plattformen konfigurieren** > **iOS**.  

          > [!NOTE]  
          >  Laden Sie das Zertifikat des Apple Push Notification Service (APNs) erst hoch, wenn Sie die iOS-Registrierung in der Configuration Manager-Konsole aktiviert haben.  

      3.  Wählen Sie im Dialogfeld **Eigenschaften von Microsoft Intune-Abonnement** die Registerkarte **iOS** aus, und aktivieren Sie das Kontrollkästchen **iOS-Anmeldung aktivieren** .  

      4.  Klicken Sie auf **Durchsuchen**, und wechseln Sie zu der von Apple heruntergeladenen APNs-Zertifikatdatei (CER-Datei). Configuration Manager zeigt die APNs-Zertifikatinformationen an. Klicken Sie auf **OK** , um das APNs-Zertifikat in Intune zu speichern.    


Weitere Informationen zur [iOS- und Macintosh-Registrierung](enroll-hybrid-ios-mac.md)

### <a name="windows-enrollment-setup"></a>Windows-Registrierungs-Setup  
Sie können Configuration Manager mit Intune verwenden, um Desktopcomputer, Laptops und andere Geräte mit Windows als mobile Geräte zu verwalten. Sie können auch Windows 10-Geräte so konfigurieren, dass [sie sich automatisch registrieren, wenn sie Azure Active Directory beitreten](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/enroll-hybrid-windows#azure-active-directory-enrollment), indem Sie ein Geschäfts-, Schul- oder Unikonto auf dem Gerät hinzufügen.

Wenn ein DNS-Alias (CNAME-Eintrag) vorhanden ist, können Benutzer ihre Geräte einfacher registrieren, da der Servername bei der Geräteregistrierung automatisch eingetragen wird. Anschließend können Sie die Registrierung für Windows-PCs und mobile Geräte aktivieren.  

1. Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Clouddienste** > **Microsoft Intune-Abonnements**, und führen Sie dann folgende Schritte durch:  
  - **Windows-PCs:** Klicken Sie auf der Registerkarte **Startseite** auf **Plattformen konfigurieren** und dann auf **Windows**. Wählen Sie auf der Registerkarte **Allgemeine** die Option **Windows-Registrierung aktivieren**aus.  
  - **Windows 10 Mobile und Windows Phone:** Klicken Sie auf der Registerkarte **Startseite** auf **Plattformen konfigurieren** und dann auf **Windows Phone**.  Klicken Sie auf der Registerkarte **Allgemein** auf  **Windows Phone 8.1 und Windows 10 Mobile**.

2.  Sie können Configuration Manager auch konfigurieren, um die Registrierung mit der Unternehmensportal-App zu vereinfachen.
(Optional) Erstellen Sie einen DNS-Alias (CNAME-Eintragstyp) in den DNS-Einträgen Ihres Unternehmens, der Anforderungen, die an eine URL Ihrer Unternehmensdomäne gesendet werden, an die Microsoft-Server für Clouddienste umleitet.  Wenn die Domäne Ihres Unternehmens beispielsweise „contoso.com“ heißt, sollten Sie einen CNAME im DNS erstellen, der „EnterpriseEnrollment.contoso.com“ an „EnterpriseEnrollment-s.manage.microsoft.com“ umleitet.  

|Typ|Hostname|Verweist auf|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  

Weitere Informationen finden Sie unter [Windows-Registrierung](enroll-hybrid-windows.md).

### <a name="android-enrollment-setup"></a>Android-Registrierungssetup
Sie können Configuration Manager mit Intune verwenden, um Android-Telefone und -Tablets zu verwalten.
1.  Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Clouddienste** > **Microsoft Intune-Abonnement**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Abonnement** auf **Plattformen konfigurieren** > **Android**.  

3.  Wählen Sie im Dialogfeld **Eigenschaften von Microsoft Intune-Abonnement** die Registerkarte **Android** aus, und klicken Sie, um das Kontrollkästchen **Android-Registrierung aktivieren** zu aktivieren.

Weitere Informationen finden Sie unter [Android](enroll-hybrid-android.md).

## <a name="step-7-set-up-additional-management"></a>Schritt 7: Einrichten zusätzlicher Verwaltung
(Optional) Sie können eine zusätzliche Verwaltung einrichten, bevor Geräte registriert werden. Diese Verwaltungslösungen können nach der Registrierung von Geräten erstellt und bereitgestellt werden, obwohl viele Organisationen Geräte bevorzugt bereitstellen, wenn sie in die Verwaltung eingebunden sind.

**Konfigurationselemente** ermöglichen Ihnen, Einstellungen, wie z.B. Erfordern einer PIN oder Erfordern von Verschlüsselung auf registrierten Geräten, auf der Grundlage der Geräteplattform zu verwalten:
- [Windows 10- und Windows 8.1-Geräte](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)
- [Windows Phone-Geräte](/sccm/compliance/deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client)
- [iOS- und Macintosh-Geräte](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)
- [Android- und Samsung KNOX Standard-Geräte](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)

**Anwendungen** können auf verwalteten Geräten bereitgestellt werden:
- [iOS-Anwendungen](/sccm/apps/get-started/creating-ios-applications)
- [Macintosh-Anwendungen](/sccm/apps/get-started/creating-mac-computer-applications)
- [Windows-PC-Anwendungen](/sccm/apps/get-started/creating-windows-applications)
- [Windows Phone-Anwendungen](/sccm/apps/get-started/creating-windows-phone-applications)
- [Android-Anwendungen](/sccm/apps/get-started/creating-android-applications)

**Bedingter Zugriff** ermöglicht die Verwaltung des Zugriffs auf Unternehmensressourcen, einschließlich:  
- [E-Mail-Zugriff](/sccm/protect/deploy-use/manage-email-access)
- [SharePoint-Zugriff](/sccm/protect/deploy-use/manage-sharepoint-online-access)
- [Skype for Business-Zugriff](/sccm/protect/deploy-use/manage-skype-for-business-online-access)
- [Dynamics CRM Online](/sccm/protect/deploy-use/manage-dynamics-crm-online-access)

## <a name="step-8-verify-mdm-configuration"></a>Schritt 8: Überprüfen der MDM-Konfiguration

 Bestimmte Komponenten der Geräteverwaltung können Sie überprüfen, indem Sie die folgenden Protokolldateien überprüfen:

-   Überprüfen Sie die Datei Cloudusersync.log, um sicherzustellen, dass die Synchronisierung von Benutzerkonten erfolgreich ist.

-   Überprüfen Sie die Datei „Sitecomp.log“, um sicherzustellen, dass die Erstellung des Dienstverbindungspunkts erfolgreich war.

## <a name="step-9-enroll-devices"></a>Schritt 9: Registrieren von Geräten
Das Hybridsetup ist jetzt abgeschlossen. Die Geräte können im Configuration Manager auf verschiedene Arten registriert werden:
- Benutzergeräte (BYOD): [Benutzer informieren, wie sie ihre Geräte registrieren](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) – Die Registrierungsanleitung ist für Intune- und hybrid verwaltete Geräte die gleiche.
- Unternehmenseigene Geräte (COD): [Registrieren von unternehmenseigenen Geräten](enroll-company-owned-devices.md) enthält Anleitungen für bestimmte Arten der Registrierung von unternehmenseigenen Geräten.

## <a name="managing-intune-subscriptions-associated-with-configuration-manager"></a>Verwalten von zu Configuration Manager zugeordneten Intune-Abonnements

Wenn Sie Configuration Manager ein Microsoft Intune-Abonnement (Testabonnement oder kostenpflichtiges Abonnement) hinzufügen und dann zu einem anderen Intune-Abonnement wechseln müssen, müssen Sie sowohl das **Microsoft Intune-Abonnement** als auch den **Dienstverbindungspunkt** aus der Configuration Manager-Konsole löschen, bevor Sie ein neues Abonnement hinzufügen können.

### <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Löschen eines Intune-Abonnements aus Configuration Manager

> [!IMPORTANT]
>  Alle Inhalte, einschließlich Benutzerregistrierungen, Richtlinien und App-Bereitstellungen, die für Geräte konfiguriert sind, die vom Intune-Abonnement verwaltet werden, werden beim Löschen des Abonnements entfernt.

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Übersicht** > **Clouddienste** > **Microsoft Intune-Abonnements** aus.

2.  Klicken Sie mit der rechten Maustaste auf das aufgeführte **Microsoft Intune-Abonnement**, und klicken Sie anschließend auf **Löschen**.

3.   Klicken Sie im Assistenten auf **Microsoft Intune-Abonnement aus Configuration Manager entfernen**, klicken Sie auf **Weiter**, und klicken Sie anschließend erneut auf **Weiter**, um das Abonnement zu entfernen.


### <a name="how-to-remove-the-service-connection-point-role"></a>So entfernen Sie die Rolle „Dienstverbindungspunkt“

1.  Wechseln Sie zu **Verwaltung** > **Übersicht** > **-Standortkonfiguration** > **Server und Standortsystemrollen**.

2.  Wählen Sie den Server aus, auf dem die Rolle **Dienstverbindungspunkt** gehostet wird.

3.  Wählen Sie in der Liste **Standortsystemrollen** die Option **Dienstverbindungspunkt** aus, und klicken Sie anschließend im Menüband auf **Rolle entfernen**. Bestätigen Sie, dass Sie die Rolle entfernen möchten. Der Dienstverbindungspunkt wird gelöscht.

Sie können jetzt einen neuen Dienstverbindungspunkt erstellen, Configuration Manager ein neues Intune-Abonnement hinzufügen und Configuration Manager als MDM-Autorität festlegen.

### <a name="how-to-change-mdm-authority-to-intune"></a>So stellen Sie die MDM-Autorität auf Intune um

Ab Version 1610 können Sie die MDM-Autorität von Configuration Manager auf Intune ändern. Informationen zu dieser Funktion sind in Kürze verfügbar.



<!--HONumber=Dec16_HO3-->


