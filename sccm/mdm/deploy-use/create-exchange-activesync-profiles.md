---
title: Erstellen von Exchange ActiveSync-E-Mail-Profilen | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie E-Mail-Profile in System Center Configuration Manager erstellen und konfigurieren, die mit Microsoft Intune verwendet werden.
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: 4
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: aa8924a013ebdbee888cab33001fddbe7ad2d67e
ms.openlocfilehash: a0353c49360cd99bc92b4546e12a52c3d13d1d14
ms.lasthandoff: 03/30/2017


---

# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Erstellen von Exchange ActiveSync-E-Mail-Profilen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

E-Mail-Profile tragen zusammen mit Microsoft Intune dazu bei, dass Sie Geräte mithilfe von E-Mail-Profilen und Einschränkungen unter Verwendung von Exchange ActiveSync bereitstellen können. Dies ermöglicht Benutzern bei minimal erforderlicher eigener Einrichtung den Zugriff auf E-Mails im Unternehmen über ihre Geräte.  

 Sie können die folgenden Gerätetypen mit E-Mail-Profilen konfigurieren:  

- Windows 10
- Windows Phone 8.1
- Windows Phone 8.0
- iPhones unter iOS 5, iOS 6, iOS 7 und iOS 8  
- iPads unter iOS 5, iOS 6, iOS 7 und iOS 8  
- Samsung KNOX Standard (4 und höher)
- Android for Work

E-Mail-Profile müssen in Intune registriert werden, um sie für Geräte bereitzustellen. Informationen zum Registrieren von Geräten finden Sie unter [Verwalten mobiler Geräte mit Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).

>[!NOTE]
>Intune stellt zwei Android for Work-E-Mail-Profile bereit: eines für die Gmail-E-Mail-App und eines für die Nine Work-E-Mail-App. Diese Apps sind im Google Play Store erhältlich und unterstützen Verbindungen mit Exchange. Stellen Sie auf den Geräten der Benutzer eine dieser E-Mail-Apps bereit, erstellen Sie das entsprechende Profil, und stellen Sie dieses bereit, um die E-Mail-Konnektivität zu aktivieren. E-Mail-Apps wie Nine Work sind möglicherweise nicht frei. Lesen Sie dazu die Details der App-Lizenzierung, oder wenden Sie sich mit Ihren Fragen an das App-Unternehmen.

 Zusätzlich zum Konfigurieren eines E-Mail-Kontos auf dem Gerät können Sie auch die Synchronisierungseinstellungen für Kontakte, Kalender und Aufgaben konfigurieren.  

 Wenn Sie ein E-Mail-Profil erstellen, können Sie eine Vielzahl von Sicherheitseinstellungen aufnehmen, darunter auch Zertifikate für Identität, Verschlüsselung und Signatur, die mit System Center Configuration Manager-Zertifikatprofilen bereitgestellt wurden. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).    

## <a name="create-a-new-exchange-activesync-email-profile"></a>Erstellen eines neuen Exchange ActiveSync-E-Mail-Profils  

Starten des Assistenten zum Erstellen von Exchange ActiveSync-E-Mail-Profilen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, den **Zugriff auf Unternehmensressourcen**, und klicken Sie dann auf **E-Mail-Profile**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Exchange ActiveSync-E-Mail-Profil erstellen**.
4.  Konfigurieren Sie auf der Seite „Allgemein“ des Assistenten die folgenden Informationen:
    - **Name**: Geben Sie einen aussagekräftigen Namen für das E-Mail-Profil ein.
    - **Beschreibung**: Wenn Sie möchten, können Sie eine Beschreibung des E-Mail-Profils eingeben, anhand derer Sie es in der Configuration Manager-Konsole erkennen können.
    - **Dieses E-Mail-Profil ist für Android for Work bestimmt**: Wählen Sie diese Option aus, wenn Sie nur dieses E-Mail-Profil für Android for Work-Geräte bereitstellen möchten. Wenn Sie dieses Kontrollkästchen aktivieren, wird die Assistentenseite **Unterstützte Plattformen** nicht angezeigt. Nur Android for Work-E-Mail-Profile sind konfiguriert.
4.  Geben Sie auf der Seite **Exchange ActiveSync** des Assistenten zum Erstellen von Exchange ActiveSync-E-Mail-Profilen die folgenden Informationen an:  

    -   **Exchange ActiveSync-Host:** Geben Sie den Hostnamen des Exchange-Servers Ihres Unternehmens an, der die Exchange ActiveSync-Dienste hostet.  

    -   **Kontoname:** Geben Sie den Anzeigenamen für das E-Mail-Konto so an, wie er Benutzern auf ihren Geräten angezeigt wird.  

    -   **Kontobenutzername:** Wählen Sie aus, wie der Benutzername des E-Mail-Kontos auf Clientgeräten konfiguriert wird. Sie können eine der folgenden Optionen aus der Dropdownliste wählen:  

        -   **Benutzerprinzipalname** – Der vollständige Benutzerprinzipalname wird zum Anmelden bei Exchange verwendet.  

        -   **AccountName**: Verwenden Sie den vollständigen Benutzerkontonamen von Active Directory.

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
        >  Bevor Sie das Identitätszertifikat auswählen können, müssen Sie es zuerst als SCEP-Zertifikatprofil (Simple Certificate Enrollment Protocol) konfigurieren. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

         Diese Option ist nur verfügbar, wenn Sie unter **Authentifizierungsmethode** **Zertifikate**ausgewählt haben.  

    -   **S/MIME verwenden** (nur für iOS-Geräte): Ausgehende E-Mails werden mit S/MIME-Verschlüsselung gesendet. Wählen Sie aus den folgenden Optionen:


        -   **Verschlüsselungszertifikate:** Klicken Sie auf **Auswählen** , und wählen Sie dann ein Zertifikat für die Verschlüsselung aus. Diese Option steht nur für iOS-Geräte zur Verfügung. Sie können ein PFX-Zertifikat nur für die Verwendung als Verschlüsselungszertifikat auswählen.

        Wenn Sie sowohl ein Verschlüsselungszertifikat als auch ein Signaturzertifikat auswählen, müssen sie beide im PFX-Format sein.

        > [!NOTE]  
        >  Bevor Sie Zertifikate auswählen können, müssen Sie sie zuerst als SCEP- oder PFX-Zertifikatprofil konfigurieren. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  




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

Informationen zum Bereitstellen von Exchange ActiveSync-E-Mail-Profilen finden Sie unter [Bereitstellen von E-Mail-Profilen in System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).  

