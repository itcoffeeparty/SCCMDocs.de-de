---
title: Erstellen von WLAN-Profilen | System Center Configuration Manager
description: "Hier erfahren Sie, wie Sie in System Center Configuration Manager mit WLAN-Profilen Funknetzwerkeinstellungen für Benutzer in Ihrer Organisation bereitstellen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
caps.latest.revision: 13
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 295ccc2ce7c1dae55c45113cc8ff826e30f7079a


---
# <a name="how-to-create-wi-fi-profiles-in-system-center-configuration-manager"></a>Erstellen von WLAN-Profilen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Verwenden Sie WLAN-Profile in System Center Configuration Manager, um für Benutzer in Ihrer Organisation Einstellungen für Funknetzwerke bereitzustellen. Durch die Bereitstellung dieser Einstellungen erleichtern Sie den Benutzern das Herstellen einer WLAN-Verbindung.  

 Angenommen, Sie haben ein neues Funknetzwerk mit dem Namen **Contoso Wi-Fi**installiert. Nun möchten Sie für alle Geräte, auf denen das iOS-Betriebssystem ausgeführt wird, die erforderlichen Einstellungen für die Verbindung mit diesem Netzwerk bereitstellen. Sie können ein WLAN-Profil mit den Einstellungen erstellen, die zum Herstellen einer Verbindung zum Drahtlosnetzwerk **Contoso Wi-Fi** erforderlich sind. Dann können Sie dieses Profil für alle Benutzer bereitstellen, auf deren Geräten in Ihrer Hierarchie iOS ausgeführt wird. Benutzer von iOS-Geräten finden das Unternehmensnetzwerk in der Liste der Funknetzwerke und können leicht eine Verbindung mit diesem Netzwerk herstellen.  

 Sie können die folgenden Gerätetypen mit WLAN-Profilen konfigurieren:  

-   Geräte unter Windows 8.1 32-Bit  

-   Geräte unter Windows 8.1 64-Bit  

-   Geräte unter Windows RT 8.1  

-   Geräte unter Windows Phone 8.1  

-   Geräte unter Windows 10 Desktop oder Mobile  

-   iPhone-Geräte mit iOS 5, iOS 6, iOS 7 und iOS 8  

-   iPad-Geräte mit iOS 5, iOS 6, iOS 7 und iOS 8  

-   Android-Geräte mit Version 4  

> [!IMPORTANT]  
>  Um Profile für Android-, iOS-, Windows Phone- und registrierte Windows 8.1-Geräte (und höher) bereitzustellen, müssen diese Geräte bei [Microsoft Intune] registriert werden. Informationen zum Registrieren von Geräten finden Sie unter [Enroll devices for management in Intune (Registrieren von Geräten für die Verwaltung in Intune)](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).  

 Wenn Sie ein WLAN-Profil erstellen, können Sie eine Vielzahl von Sicherheitseinstellungen einfügen. Dazu gehören Zertifikate für die Serverüberprüfung und die Clientauthentifizierung, die mithilfe von Configuration Manager-Zertifikatprofilen bereitgestellt wurden. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

## <a name="steps-to-create-a-wi-fi-profile"></a>Schritte zum Erstellen eines WLAN-Profils  
 Führen Sie die folgenden erforderlichen Schritte aus, um mithilfe des **Assistenten zum Erstellen von WLAN-Profilen**ein WLAN-Profil zu erstellen.  

-   [Schritt 1: Starten des Assistenten zum Erstellen von WLAN-Profilen](#BKMK_Step1)  

-   [Schritt 2: Bereitstellen von allgemeinen Informationen zum WLAN-Profil](#BKMK_Step2)  

-   [Schritt 3: Bereitstellen von Informationen zum Funknetzwerk](#BKMK_Step3)  

-   [Schritt 4: Konfigurieren der Sicherheit für das WLAN-Profil](#BKMK_Step4)  

-   [Schritt 5: Konfigurieren erweiterter Einstellungen für das WLAN-Profil](#BKMK_Step5)  

-   [Schritt 6: Konfigurieren von Proxyeinstellungen für das WLAN-Profil](#BKMK_Step6)  

-   [Schritt 7: Konfigurieren unterstützter Plattformen für das WLAN-Profil](#BKMK_Step7)  

-   [Schritt 8: Abschließen des Assistenten](#BKMK_Step8)  

##  <a name="a-namebkmkstep1a-step-1-start-the-create-wi-fi-profile-wizard"></a><a name="BKMK_Step1"></a> Schritt 1: Starten des Assistenten zum Erstellen von WLAN-Profilen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, den **Zugriff auf Unternehmensressourcen**, und klicken Sie dann auf **WLAN-Profile**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **WLAN-Profil erstellen**.  

##  <a name="a-namebkmkstep2a-step-2-provide-general-information-about-the-wi-fi-profile"></a><a name="BKMK_Step2"></a> Schritt 2: Bereitstellen von allgemeinen Informationen zum WLAN-Profil  

1.  Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von WLAN-Profilen einen eindeutigen Namen und eine Beschreibung für das WLAN-Profil ein. Sie können maximal 256 Zeichen verwenden.  

2.  Wenn Sie eine Einstellungen aus einem anderen WLAN-Profil übernehmen möchten, wählen Sie **Vorhandenes WLAN-Profil aus einer Datei importieren** aus.  

    > [!IMPORTANT]  
    >  Stellen Sie sicher, dass das importierte WLAN-Profil gültigen XML-Code für ein WLAN-Profil enthält. Das Profil wird beim Importieren der Datei von Configuration Manager nicht überprüft.  

3.  In  
                            **Schweregrad der Nichtkompatibilität für Berichte** geben Sie den berichteten Schweregrad an, wenn die Nichtkompatibilität eines WLAN-Profils auf Clientgeräten festgestellt wird (beispielsweise bei einem Fehler der Profilinstallation). Die folgenden Schweregrade sind verfügbar:  

    -   **Keine**: Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.  

    -   **Information**: Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.  

    -   **Warnung**: Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.  

    -   **Kritisch**: Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.  

    -   **Kritisch mit Ereignis**: Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.  

##  <a name="a-namebkmkstep3a-step-3-provide-information-about-the-wireless-network"></a><a name="BKMK_Step3"></a> Schritt 3: Bereitstellen von Informationen zum Funknetzwerk  

1.  Geben Sie auf der Seite **WLAN-Profil** des Assistenten zum Erstellen von WLAN-Profilen den beschreibenden Namen für die Funkverbindung mit dem Internet mit maximal 32 Zeichen an. Dieser Name wird auf Geräten als Netzwerkname angezeigt.  

    > [!IMPORTANT]  
    >  Configuration Manager unterstützt weder den Apostroph (**‘**) noch das Komma (**,**) im Netzwerknamen.  

2.  Geben Sie in **SSID**den Namen (SSID) des Funknetzwerks an, mit dem Geräte eine Verbindung herstellen können sollen. Sie können maximal 32 Zeichen verwenden. Bei dem SSID-Namen wird die Groß-/Kleinschreibung beachtet, daher müssen Sie ihn genau so eingeben, wie er konfiguriert ist.  

3.  Wenn Sie es Geräten gestatten möchten, die Verbindung mit dem Funknetzwerk automatisch wiederherzustellen, wählen Sie **Automatisch verbinden, wenn dieses Netzwerk in Reichweite ist**aus.  

4.  Wenn Sie es Geräten gestatten möchten, weiterhin nach anderen Funknetzwerken zu suchen, während sie mit diesem Netzwerk verbunden sind, wählen Sie  
                            **Bei hergestellter Verbindung mit diesem Netzwerk andere Funknetzwerke suchen**.  

5.  Wenn Sie es Geräten gestatten möchten, eine Verbindung mit dem Netzwerk herzustellen, wenn es nicht in der Liste der Netzwerke angezeigt wird (da es ausgeblendet ist oder seinen Namen nicht sendet), wählen Sie **Verbinden, wenn das Netzwerk seinen Namen (SSID) nicht sendet**aus.  

##  <a name="a-namebkmkstep4a-step-4-configure-security-for-the-wi-fi-profile"></a><a name="BKMK_Step4"></a> Schritt 4: Konfigurieren der Sicherheit für das WLAN-Profil  

> [!IMPORTANT]  
>  Wenn Sie für die lokale Verwaltung mobiler Geräte ein WLAN-Profil erstellen, unterstützt Current Branch von Configuration Manager nur die folgenden WLAN-Sicherheitskonfigurationen:  
>   
>  Sicherheitstypen: **WPA2-Enterprise** oder **WPA2-Personal**  
> Verschlüsselungstypen: **AES** oder **TKIP**  
> EAP-Typen: **Smartcard- oder anderes Zertifikat** oder **PEAP**  

1.  Wählen Sie auf der Seite **Sicherheitskonfiguration** des Assistenten zum Erstellen von WLAN-Profilen das Sicherheitsprotokoll aus, das vom Funknetzwerk verwendet wird, oder wählen Sie **Keine Authentifizierung (Offen)** aus, wenn das Netzwerk nicht gesichert ist.  

     Nur für Android-Geräte: Die Sicherheitstypen **WPA-Personal**, **WPA2-Personal** und **WEP** werden nicht unterstützt.  

2.  Wählen Sie die Verschlüsselungsmethode aus, die vom Funknetzwerk verwendet wird.  

3.  Wählen Sie den EAP-Typ aus, der zur Authentifizierung beim Funknetzwerk verwendet wird.  

     Nur für Windows Phone-Geräte: Die EAP-Typen **LEAP** und **EAP-FAST** werden nicht unterstützt.  

4.  Klicken Sie auf **Konfigurieren** , um Eigenschaften für den ausgewählten EAP-Typ anzugeben. Diese Option steht möglicherweise für einige ausgewählte EAP-Typen nicht zur Verfügung.  

    > [!IMPORTANT]  
    >  Wenn Sie auf **Konfigurieren**klicken, wird ein Windows-Dialogfeld geöffnet. Daher müssen Sie sicherstellen, dass die Konfiguration des ausgewählten EAP-Typs vom Betriebssystem des Computers unterstützt wird, auf dem die Configuration Manager-Konsole ausgeführt wird.  
    >   
    >  Wenn Sie für iOS-Geräte eine EAP-fremde Methode für die Authentifizierung gewählt haben, wird unabhängig von der ausgewählten Methode MS-CHAP v2 für die Verbindung verwendet.  

5.  Wenn Sie Benutzeranmeldeinformationen speichern möchten, damit Benutzer bei der Anmeldung keine Anmeldeinformationen eingeben müssen, wählen Sie **Benutzeranmeldeinformationen bei jeder Anmeldung speichern**aus.  

### <a name="for-ios-devices-only"></a>Nur für iOS-Geräte:  
 Konfigurieren Sie die Informationen für alle Zertifikate, die für die WLAN-Verbindung erforderlich sind. Sie müssen wie folgt das Clientzertifikat und entweder den Namen des vertrauenswürdigen Serverzertifikats oder das Stammzertifikat konfigurieren:  

-   **Namen vertrauenswürdiger Serverzertifikate**: Wenn auf dem Server, mit dem das Gerät eine Verbindung herstellt, ein Serverauthentifizierungszertifikat für die Identifikation des Servers und zur Unterstützung bei der Absicherung des Kommunikationskanals verwendet wird, geben Sie den oder die Namen für den Antragstellernamen oder den alternativen Antragstellernamen dieses Zertifikats ein. Die Namen sind normalerweise die vollqualifizierten Domänennamen des Servers. Beispiel: Wenn für den Zertifikatantragsteller der allgemeine Name des Serverzertifikats „srv1.contoso.com“ lautet, geben Sie **srv1.contoso.com**ein. Wenn für das Serverzertifikat mehrere Namen als alternative Antragstellernamen angegeben sind, geben Sie die einzelnen Namen getrennt durch ein Semikolon ein.  

    > [!TIP]  
    >  Wenn das Clientzertifikat, das Sie für die EAP- oder Clientauthentifizierung für ein iOS-Gerät auswählen, zur Authentifizierung bei einem RADIUS-Server (Remote Authentication Dial-In User Service) wie etwa einem Server, auf dem ein Netzwerkrichtlinienserver ausgeführt wird, verwendet wird, müssen Sie als alternativen Antragstellername den Benutzerprinzipalnamen festlegen.  

-   **Stammzertifikate für die Serverüberprüfung auswählen**: Wenn auf dem Server, mit dem das Gerät eine Verbindung herstellt, ein für das Gerät nicht vertrauenswürdiges Serverauthentifizierungszertifikat verwendet wird, wählen Sie das Zertifikatprofil aus, das das Stammzertifikat für das Serverzertifikat enthält, um auf dem Gerät eine Kette vertrauenswürdiger Zertifikate zu erstellen.  

-   **Clientzertifikat für Clientauthentifizierung auswählen**: Wenn für den Server oder das Netzwerkgerät ein Clientzertifikat erforderlich ist, um das verbindende Gerät zu authentifizieren, wählen Sie das Zertifikatprofil aus, das das Clientauthentifizierungszertifikat enthält.  

> [!NOTE]  
>  Damit Sie das Stammzertifikat und das Clientzertifikat auswählen können, müssen Sie sie zuerst als Zertifikatprofil konfigurieren und bereitstellen. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

##  <a name="a-namebkmkstep5a-step-5-configure-advanced-settings-for-the-wi-fi-profile"></a><a name="BKMK_Step5"></a> Schritt 5: Konfigurieren erweiterter Einstellungen für das WLAN-Profil  
 Geben Sie auf der Seite **Erweiterte Einstellungen** des Assistenten zum Erstellen von WLAN-Profilen erweiterte Einstellungen für das WLAN-Profil an. Dazu gehören der Authentifizierungsmodus, Optionen für einmaliges Anmelden und Einstellungen der FIPS-Kompatibilität (Federal Information Processing Standards). Weitere Informationen zu diesen Optionen finden Sie in der Windows-Dokumentation.  

> [!NOTE]  
>  Die verfügbaren erweiterten Einstellungen sind abhängig von den auf der Seite **Sicherheitskonfiguration** des Assistenten ausgewählten Optionen.  

##  <a name="a-namebkmkstep6a-step-6-configure-proxy-settings-for-the-wi-fi-profile"></a><a name="BKMK_Step6"></a> Schritt 6: Konfigurieren von Proxyeinstellungen für das WLAN-Profil  

1.  Aktivieren Sie auf der Seite **Proxyeinstellungen** des Assistenten zum Erstellen von WLAN-Profilen das Kontrollkästchen **Proxyeinstellungen für dieses WLAN-Profil konfigurieren** , wenn für Ihr Funknetzwerk ein Proxyserver verwendet wird.  

2.  Geben Sie Details zu Ihrem Proxyserver und dessen Einstellungen an. Weitere Informationen finden Sie in der Windows Server-Dokumentation.  

##  <a name="a-namebkmkstep7a-step-7-configure-supported-platforms-for-the-wi-fi-profile"></a><a name="BKMK_Step7"></a> Schritt 7: Konfigurieren unterstützter Plattformen für das WLAN-Profil  
 Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten zum Erstellen von WLAN-Profilen die Betriebssysteme aus, unter denen das WLAN-Profil installiert wird. Alternativ klicken Sie auf **Alle auswählen** , um das WLAN-Profil unter allen verfügbaren Betriebssystemen zu installieren.  

##  <a name="a-namebkmkstep8a-step-8-complete-the-wizard"></a><a name="BKMK_Step8"></a> Schritt 8: Abschließen des Assistenten  
 Überprüfen Sie auf der Seite **Zusammenfassung** des Assistenten die auszuführenden Aktionen, und schließen Sie dann den Assistenten ab. Das neue WLAN-Profil wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **WLAN-Profile** angezeigt.  

 Weitere Informationen zum Bereitstellen des WLAN-Profils finden Sie unter [Bereitstellen von WLAN-Profilen in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  



<!--HONumber=Nov16_HO1-->


