---
title: Erstellen von Exchange ActiveSync-E-Mail-Profilen | System Center Configuration Manager
description: Erfahren Sie, wie Sie E-Mail-Profile in System Center Configuration Manager erstellen und konfigurieren, die mit Microsoft Intune verwendet werden.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 15f0fd50-e196-44e5-b435-234d7ff6a5cd
caps.latest.revision: 4
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 613ed15742322e2eb90eec3c9f493e3b1755d93a


---

# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Erstellen von Exchange ActiveSync-E-Mail-Profilen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

E-Mail-Profile tragen zusammen mit Microsoft Intune dazu bei, dass Sie Geräte mithilfe von E-Mail-Profilen und Einschränkungen unter Verwendung von Exchange ActiveSync bereitstellen können. Dies ermöglicht Benutzern bei minimal erforderlicher eigener Einrichtung den Zugriff auf E-Mails im Unternehmen über ihre Geräte.  

 Sie können die folgenden Gerätetypen mit E-Mail-Profilen konfigurieren:  

-   Geräte unter Windows Phone 8  

-   Geräte unter Windows Phone 8.1  

-   Geräte unter Windows 10 Mobile  

-   iPhone-Geräte unter iOS 5, iOS 6, iOS 7 und iOS 8  

-   iPad-Geräte unter iOS 5, iOS 6, iOS 7 und iOS 8  

> [!IMPORTANT]  
>  Um Profile für iOS-, Android-, Samsung KNOX-, Windows Phone- und Windows 8.1- oder Windows 10-Geräte bereitzustellen, müssen diese Geräte bei Microsoft Intune registriert sein. Informationen zum Registrieren von Geräten finden Sie unter [Verwalten mobiler Geräte mit Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 Zusätzlich zum Konfigurieren eines E-Mail-Kontos auf dem Gerät können Sie auch die Synchronisierungseinstellungen für Kontakte, Kalender und Aufgaben konfigurieren.  

 Wenn Sie ein E-Mail-Profil erstellen, können Sie eine Vielzahl von Sicherheitseinstellungen aufnehmen, darunter auch Zertifikate für Identität, Verschlüsselung und Signatur, die mit System Center Configuration Manager-Zertifikatprofilen bereitgestellt wurden. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](introduction-to-certificate-profiles.md).    


## <a name="create-a-new-exchange-activesync-email-profile"></a>Erstellen eines neuen Exchange ActiveSync-E-Mail-Profils  

Starten des Assistenten zum Erstellen von Exchange ActiveSync-E-Mail-Profilen  

1.  Klicken Sie in der System Center Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, den **Zugriff auf Unternehmensressourcen**, und klicken Sie dann auf **E-Mail-Profile**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Exchange ActiveSync-Profil erstellen**. 

4.  Befolgen Sie die Anweisungen im Assistenten.   

### <a name="to-configure-exchange-activesync-settings-for-the-exchange-activesync-email-profile"></a>So konfigurieren Sie Exchange ActiveSync-Einstellungen für das Exchange ActiveSync-E-Mail-Profil  

1.  Geben Sie auf der Seite **Exchange ActiveSync** des Assistenten zum Erstellen von Exchange ActiveSync-E-Mail-Profilen die folgenden Informationen an:  

    -   **Exchange ActiveSync-Host:** Geben Sie den Hostnamen des Exchange-Servers Ihres Unternehmens an, der die Exchange ActiveSync-Dienste hostet.  

    -   **Kontoname:** Geben Sie den Anzeigenamen für das E-Mail-Konto so an, wie er Benutzern auf ihren Geräten angezeigt wird.  

    -   **Kontobenutzername:** Wählen Sie aus, wie der Benutzername des E-Mail-Kontos auf Clientgeräten konfiguriert wird. Sie können eine der folgenden Optionen aus der Dropdownliste wählen:  

        -   **Benutzerprinzipalname** – Der vollständige Benutzerprinzipalname wird zum Anmelden bei Exchange verwendet.  

        -   **sAMAccountName** – Verwendet  

        -   **Primäre SMTP-Adresse** – Die primäre SMTP-Adresse von Benutzern wird zum Anmelden bei Exchange verwendet.  

    -   **E-Mail-Adresse:** Wählen Sie aus, wie die E-Mail-Adresse für den Benutzer auf jedem Clientgerät generiert wird. Sie können eine der folgenden Optionen aus der Dropdownliste wählen:  

        -   **Primäre SMTP-Adresse** – Die primäre SMTP-Adresse von Benutzern wird zum Anmelden bei Exchange verwendet.  

        -   **Benutzerprinzipalname** – Der vollständige Benutzerprinzipalname wird als E-Mail-Adresse verwendet.  

    -   **Kontodomäne:** Sie können eine der folgenden Optionen auswählen:  

        -   **Von Active Directory abrufen**  

        -   **Benutzerdefiniert**  

         Dieses Feld ist nur anwendbar, wenn **sAMAccountName** in der Dropdownliste **Kontobenutzername** ausgewählt wird.  

    -   **Authentifizierungsmethode:** Wählen Sie eine der folgenden Authentifizierungsmethoden aus, die zum Authentifizieren der Verbindung mit Exchange ActiveSync verwendet wird:  

        -   **Zertifikate** – Ein Identitätszertifikat wird für die Authentifizierung der Exchange ActiveSync-Verbindung verwendet.  

        -   **Benutzername und Kennwort** – Der Gerätebenutzer muss ein Kennwort für die Verbindung mit Exchange ActiveSync angeben (der Benutzername ist als Teil des E-Mail-Profils konfiguriert).  

    -   **Identitätszertifikat:** Klicken Sie auf **Auswählen** , und wählen Sie dann ein Zertifikat für die Identität aus.  

        > [!NOTE]  
        >  Bevor Sie das Identitätszertifikat auswählen können, müssen Sie es zuerst als SCEP-Zertifikatprofil (Simple Certificate Enrollment Protocol) konfigurieren. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

         Diese Option ist nur verfügbar, wenn Sie unter **Authentifizierungsmethode** **Zertifikate**ausgewählt haben.  

    -   **S/MIME verwenden** – Ausgehende E-Mails werden mit S/MIME-Verschlüsselung gesendet. Diese Option steht nur für iOS-Geräte zur Verfügung.  

    -   **Verschlüsselungszertifikate:** Klicken Sie auf **Auswählen** , und wählen Sie dann ein Zertifikat für die Verschlüsselung aus. Diese Option steht nur für iOS-Geräte zur Verfügung.  

        > [!NOTE]  
        >  Bevor Sie das Verschlüsselungszertifikat auswählen können, müssen Sie es zuerst als SCEP-Zertifikatprofil (Simple Certificate Enrollment Protocol) konfigurieren. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

         Diese Option ist nur verfügbar, wenn Sie **S/MIME verwenden**ausgewählt haben.  

    -   **Signaturzertifikate:** Klicken Sie auf **Auswählen** , und wählen Sie dann ein Zertifikat für das Signieren aus. Diese Option steht nur für iOS-Geräte zur Verfügung.  

        > [!NOTE]  
        >  Bevor Sie das Signaturzertifikat auswählen können, müssen Sie es zuerst als SCEP-Zertifikatprofil (Simple Certificate Enrollment Protocol) konfigurieren. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

         Diese Option ist nur verfügbar, wenn Sie **S/MIME verwenden**ausgewählt haben.  

###   <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>Konfigurieren der Synchronisierungseinstellungen für das Exchange ActiveSync-E-Mail-Profil  

1.  Geben Sie auf der Seite **Synchronisierungseinstellungen konfigurieren** des Assistenten zum Erstellen von Exchange ActiveSync-E-Mail-Profilen die folgenden Informationen an:  

    -   **Zeitplan:** Wählen Sie den Zeitplan aus, nach dem Geräte mit Daten vom Exchange-Server synchronisiert werden. Diese Option steht nur für Windows Phone-Geräte zur Verfügung. Wählen Sie aus:  

        -   **Nicht konfiguriert** – Es wird kein Synchronisierungszeitplan erzwungen. Dies ermöglicht es Benutzern, ihren eigenen Synchronisierungszeitplan zu konfigurieren.  

        -   **Wenn Nachrichten eintreffen** – Daten wie E-Mails und Kalendereinträge werden bei ihrer Ankunft automatisch synchronisiert.  

        -   **15 Minuten** – Daten wie E-Mails und Kalendereinträge werden automatisch alle 15 Minuten synchronisiert.  

        -   **30 Minuten** – Daten wie E-Mails und Kalendereinträge werden automatisch alle 30 Minuten synchronisiert.  

        -   **60 Minuten** – Daten wie E-Mails und Kalendereinträge werden automatisch alle 60 Minuten synchronisiert.  

        -   **Manuell** – Die Synchronisierung muss manuell vom Gerätebenutzer initiiert werden.  

    -   **Anzahl der Tage für die E-Mail-Synchronisierung:** Wählen Sie in der Dropdownliste die Anzahl von Tagen aus, für die E-Mails synchronisiert werden sollen. Wählen Sie einen der folgenden Werte aus:  

        -   **Nicht konfiguriert** – Die Einstellung wird nicht erzwungen. Damit können Benutzer konfigurieren, wie viele E-Mails auf ihr Gerät heruntergeladen werden.  

        -   **Unbegrenzt** – Alle verfügbaren E-Mails werden synchronisiert.  

        -   **1 Tag**  

        -   **3 Tage**  

        -   **1 Woche**  

        -   **2 Wochen**  

        -   **1 Monat**  

    -   **Verschieben von Nachrichten an andere E-Mail-Konten zulassen** – Wählen Sie diese Option aus, damit Benutzer E-Mail-Nachrichten zwischen verschiedenen Konten verschieben können, die auf ihrem Gerät konfiguriert sind. Diese Option steht nur für iOS-Geräte zur Verfügung.  

    -   **E-Mail-Versand aus Anwendungen von Drittanbietern zulassen** – Wählen Sie diese Option aus, um Benutzern das Senden von E-Mails von bestimmten nicht standardmäßigen E-Mail-Anwendungen von Drittanbietern zu ermöglichen. Diese Option steht nur für iOS-Geräte zur Verfügung.  

    -   **Zuletzt verwendete E-Mail-Adressen synchronisieren** – Wählen Sie diese Option aus, um die Liste der E-Mail-Adressen zu synchronisieren, die zuletzt auf dem Gerät verwendet wurden. Diese Option steht nur für iOS-Geräte zur Verfügung.  

    -   **SSL verwenden** – Wählen Sie diese Option aus, um die SSL-Kommunikation (Secure Sockets Layer) beim Senden von E-Mails, beim Empfangen von E-Mails und für die Kommunikation mit dem Exchange-Server zu verwenden.  

    -   **Zu synchronisierender Inhaltstyp:** Wählen Sie die Inhaltstypen aus, die auf Geräten synchronisiert werden sollen. Diese Option steht nur für Windows Phone-Geräte zur Verfügung. Wählen Sie aus:  

        -   **E-Mail**  

        -   **Kontakte**  

        -   **Kalender**  

        -   **Aufgaben**  

###  <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>Angeben der unterstützten Plattformen für das Exchange ActiveSync-E-Mail-Profil  
 
1.  Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten zum Erstellen von Exchange ActiveSync-E-Mail-Profilen die Betriebssysteme aus, unter denen das E-Mail-Profil installiert wird, oder klicken Sie auf **Alle auswählen** , um das E-Mail-Profil unter allen verfügbaren Betriebssystemen zu installieren.  

2.  Schließen Sie den Assistenten ab.

Informationen zum Bereitstellen von Exchange ActiveSync-E-Mail-Profilen finden Sie unter [Bereitstellen von E-Mail-Profilen in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  



<!--HONumber=Nov16_HO1-->


