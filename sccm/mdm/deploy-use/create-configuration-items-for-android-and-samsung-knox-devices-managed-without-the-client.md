---
title: "Erstellen von Konfigurationselementen für Android- und Samsung KNOX Standard-Geräte, die mit Intune verwaltet werden | Microsoft-Dokumentation"
description: "Verwenden Sie das Konfigurationselement von System Center Configuration Manager für Android- und Samsung KNOX Standard-Geräte, die Geräteeinstellungen zu verwalten."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66f3c4-e3bb-4f6a-abd5-55be649ff90d
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 67ea4d2a7c9753aa406a84157930564213b6cc0a
ms.lasthandoff: 03/06/2017


---
# <a name="create-configuration-items-for-android-and-samsung-knox-standard-devices-managed-with-intune"></a>Erstellen von Konfigurationselementen für Android- und Samsung KNOX Standard-Geräte, die mit Intune verwaltet werden

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie das System Center Configuration Manager Konfigurationselement für **Android und Samsung KNOX**, um Einstellungen für Android- und Samsung KNOX Standard-Geräte zu verwalten, die in Microsoft Intune registriert sind oder lokal von Configuration Manager verwaltet werden.  

## <a name="create-an-android-and-samsung-knox-standard-configuration-item"></a>Erstellen eines Konfigurationselements für Android und Samsung KNOX Standard  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationselemente**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen**einen Namen und optional eine Beschreibung für das Konfigurationselement an.  

5.  Wählen Sie unter **Typ des zu erstellenden Konfigurationselements angeben**den Typ **Android und Samsung KNOX**aus.  

6.  Klicken Sie auf **Kategorien**, wenn Sie Kategorien erstellen und zuweisen, um das Durchsuchen und Filtern von Konfigurationselementen in der Configuration Manager-Konsole zu erleichtern.  

7.  Wählen Sie auf der Seite **Unterstützte Plattformen** die jeweilige Android- oder Samsung KNOX Standard-Plattform zur Bewertung des Konfigurationselements aus.  

8.  Wählen Sie auf der Seite **Geräteeinstellungen** die Einstellungsgruppe aus, die Sie konfigurieren möchten. Informieren Sie sich in diesem Thema unter [Referenz zu Einstellungen des Konfigurationselements für Android und Samsung KNOX Standard](#android-and-samsung-knox-standard-configuration-item-settings-reference) über die Details, und klicken Sie dann auf **Weiter**.  

    > [!TIP]  
    >  Ist die gewünschte Einstellung nicht aufgeführt, aktivieren Sie das Kontrollkästchen **Zusätzliche Einstellungen konfigurieren, die in den Standardeinstellungsgruppen nicht enthalten sind**.  

9. Konfigurieren Sie auf jeder Einstellungsseite die erforderlichen Einstellungen, und legen Sie fest, ob sie korrigiert werden sollen, wenn sie auf Geräten nicht kompatibel sind (sofern unterstützt).  

10. Sie können für jede Einstellungsgruppe auch den Schweregrad konfigurieren, der (in Configuration Manager-Berichten) gemeldet wird, wenn die Inkompatibilität eines Konfigurationselements festgestellt wird:  

    -   **Keine** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad gemeldet.  

    -   **Information** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** gemeldet.  

    -   **Warnung** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** gemeldet.  

    -   **Kritisch** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** gemeldet.  

    -   **Kritisch mit Ereignis** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** gemeldet.   

11. Überprüfen Sie auf der Seite **Plattformanwendbarkeit** alle Einstellungen, die mit den zuvor ausgewählten, unterstützten Plattformen nicht kompatibel sind. Sie können zurückkehren und diese Einstellungen entfernen oder den Vorgang fortsetzen.  

    > [!TIP]  
    >  Nicht unterstützte Einstellungen werden nicht auf Kompatibilität überprüft.  

12. Schließen Sie den Assistenten ab.  

 Sie können das neue Konfigurationselement im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Konfigurationselemente** anzeigen.  

##  <a name="android-and-samsung-knox-standard-configuration-item-settings-reference"></a>Referenz zu Einstellungen des Konfigurationselements für Android und Samsung KNOX Standard  

### <a name="password"></a>Kennwort  
 Diese Einstellungen gelten für Android- und Samsung KNOX Standard-Geräte.  

|Einstellung|Details|  
|-------------|-------------|  
|**Kennworteinstellungen auf Geräten erforderlich**|Auf unterstützten Geräten ein Kennwort erfordern.|  
|**Minimale Kennwortlänge (Zeichen)**|Die Mindestlänge für das Kennwort.|  
|**Kennwortablauf in Tagen**|Die Anzahl der Tage, bevor ein Kennwort geändert werden muss.|  
|**Anzahl der gespeicherten Kennwörter**|Verhindert die Wiederverwendung zuvor verwendeter Kennwörter.|  
|**Anzahl der gescheiterten Anmeldeversuche vor dem Zurücksetzen eines Geräts**|Setzt das Gerät zurück, wenn diese Anzahl von Anmeldeversuchen fehlschlägt.|  
|**Leerlaufzeit vor dem Sperren des Geräts**|Legen Sie die Zeitspanne fest, nach der das Gerät bei Nichtverwendung gesperrt wird.|
|**Kennwortqualität**|Wählen Sie den erforderlichen Grad der Kennwortkomplexität aus. Wählen Sie zudem aus, ob biometrische Geräte zulässig sind.|  
|**Zulassen von Smart Lock und anderen Vertrauens-Agents**|Damit können Sie das Smart Lock-Feature auf kompatiblen Android-Geräten steuern. Diese Telefonfunktion wird manchmal als Vertrauens-Agent bezeichnet und ermöglicht Ihnen das Deaktivieren oder Umgehen des Kennworts für den Gerätesperrbildschirm, wenn sich das Gerät an einem vertrauenswürdigen Standort befindet, z. B. wenn es mit einem bestimmten Bluetooth-Gerät verbunden ist oder sich in der Nähe eines NFC-Tags befindet. Mit dieser Einstellung können Sie verhindern, dass Endbenutzer Smart Lock konfigurieren.|
|Fingerabdruck zum Entsperren (KNOX 5.0+)|Ermöglicht Benutzern, einen Fingerabdruck zum Entsperren kompatibler Geräte zu verwenden.|

###  <a name="device"></a>Gerät  
 Diese Einstellungen gelten nur für Samsung KNOX Standard-Geräte.  

|Name der Einstellung|Details|  
|------------------|-------------|
|**Sprachwahlverfahren**|Aktiviert oder deaktiviert das Feature „Sprachwahlverfahren“ auf dem Gerät.|
|**Sprach-Assistent**|Ermöglicht die Verwendung von Sprach-Assistent-Software auf dem Gerät.|
|**Bildschirmaufnahme**|Ermöglicht dem Benutzer, den Bildschirminhalt als Image zu erfassen.|
|**Übermittlung von Diagnosedaten**|Erlaubt dem Gerät, Diagnoseinformationen an Google zu senden.|
|**Geolocation**|Erlaubt dem Gerät die Nutzung von Standortinformationen.|
|**Kopieren und Einfügen**|Erlaubt die Verwendung der Funktionen zum Kopieren und Einfügen auf dem Gerät.|  
|**Zurücksetzen auf Werkseinstellungen**|Ermöglicht dem Benutzer das Zurücksetzen des Geräts auf die Werkseinstellungen.|  
|**Freigabe der Zwischenablage zwischen Anwendungen**|Verwenden Sie die Zwischenablage zum Kopieren und Einfügen zwischen Apps.|
|**Bluetooth**|Ermöglicht die Verwendung der Bluetooth-Funktion des Geräts.|

### <a name="store"></a>Speicher
|Einstellung|Details|  
|-------------|-------------|  
|**Anwendungsstore**|Erlaubt den Zugriff auf die Google Play Store-App auf dem Gerät.|

### <a name="browser"></a>Browser
|Einstellung|Details|  
|-------------|-------------|
|**Webbrowser zulassen**|Legt fest, ob der Standardwebbrowser des Geräts verwendet werden kann.|
|**Automatisch ausfüllen**|Erlaubt die Verwendung der AutoAusfüllen-Funktion des Webbrowsers.|
|**Active Scripting**|Ermöglicht dem Webbrowser des Geräts die Verwendung von Active Scripting.|
|**Popupblocker**|Ermöglicht die Verwendung des Popupblockers im Webbrowser.|
|**Cookies**|Ermöglicht dem Webbrowser des Geräts die Verwendung von Cookies.|

### <a name="cloud"></a>Cloud  
 Diese Einstellungen gelten nur für Samsung KNOX Standard-Geräte.  

|Einstellung|Details|  
|-------------|-------------|  
|**Google-Sicherung**|Ermöglicht die Verwendung der Google-Sicherung.|  
|**Automatische Synchronisierung mit Google-Konto**|Ermöglicht die automatische Synchronisierung der Einstellungen von Google-Konten.|  



### <a name="security"></a>Sicherheit  

|Einstellung|Details|  
|-------------|-------------|  
|**SMS- und MMS-Nachrichten**|Ermöglicht die Verwendung von SMS- und MMS-Nachrichten auf dem Gerät.|
|**Wechselmedien**|Ermöglicht dem Gerät die Verwendung von Wechselmedien, z.B. SD-Karten.|
|**Kamera**|Ermöglicht die Verwendung der Gerätekamera.<br /><br /> Gilt für Android- und Samsung KNOX Standard-Geräte.|  
|**NFC (Near Field Communication)**|Erlaubt Vorgänge, die NFC (Near Field Communication) verwenden, wenn dies vom Gerät unterstützt wird.|
|**YouTube**|Ermöglicht die Verwendung der YouTube-App auf dem Gerät.<br /><br /> Gilt nur für Samsung KNOX Standard-Geräte.|  
|**Ausschalten**|Ermöglicht das Ausschalten des Geräts.<br /><br /> Gilt nur für Samsung KNOX Standard-Geräte.|

### <a name="roaming"></a>Roaming
|Einstellung|Details|  
|-------------|-------------|
|**Sprachroaming**|Lässt Sprachroaming über das Mobilfunknetz zu.|
|**Datenroaming**|Lässt Datenroaming über das Mobilfunknetz zu.|

### <a name="encryption"></a>Verschlüsselung  
 Diese Einstellungen gelten für Android- und Samsung KNOX Standard-Geräte.  

|Einstellung|Details|  
|-------------|-------------|  
|**Speicherkartenverschlüsselung**|Legt fest, ob die Speicherkarte des Geräts verschlüsselt werden soll.|
|**Dateiverschlüsselung auf Gerät**|Erfordert die Verschlüsselung von Dateien auf dem mobilen Gerät.|  

### <a name="wireless-communications"></a>Funkkommunikation
|Einstellung|Details|  
|-------------|-------------|
|**Drahtlosnetzwerkverbindung**|Ermöglicht die Verwendung der WLAN-Funktionen des Geräts.|
|**WLAN-Tethering**|Ermöglicht die Verwendung von WLAN-Tethering auf dem Gerät.|


### <a name="kiosk-mode-samsung-knox-standard-only"></a>Kioskmodus (nur Samsung KNOX Standard)  
 Über den Kioskmodus können Sie ein Gerät sperren, damit nur bestimmte Features funktionieren. Beispielsweise können Sie festlegen, dass auf einem Gerät nur eine von Ihnen angegebene verwaltete App ausgeführt werden kann, oder Sie können die Lautstärkeregler eines Geräts deaktivieren. Diese Einstellungen können für ein Demomodell eines Geräts oder ein Gerät nützlich sein, das nur eine bestimmte Funktion ausführen soll, wie z. B. ein Point-of-Sale-Gerät.  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-standard-device"></a>So konfigurieren Sie den Kioskmodus für ein Samsung KNOX Standard-Gerät  

Geben Sie im **Assistenten zum Erstellen von Konfigurationselementen** auf der Seite **Kioskmoduseinstellungen für Samsung KNOX-Geräte konfigurieren** die folgenden Informationen an:  

- **App auswählen:** Klicken Sie auf **Durchsuchen**, um eine Configuration Manager-Android-Anwendung (mit der Erweiterung **.apk**) auszuwählen, die beim Betrieb des Geräts im Kioskmodus ausgeführt werden darf. Andere Apps dürfen auf dem Gerät nicht ausgeführt werden.
- **Lautstärketasten** – Aktiviert oder deaktiviert die Verwendung der Lautstärketasten am Gerät.
- **Bildschirm-Standby-Taste:** Aktiviert oder deaktiviert die Taste für Standby/Aktivierung des Bildschirms am Gerät.  

###  <a name="compliant-and-noncompliant-apps-android"></a>Kompatible und nicht kompatible Apps (Android)  
 Dient zum Angeben einer Liste von Android-Apps, die in Ihrem Unternehmen kompatibel oder nicht kompatibel sind. Anschließend können Sie mithilfe von Berichten Geräte, auf denen nicht kompatible Apps installiert sind, und dazugehörige Benutzer bestimmen.  

 Es ist nicht möglich, kompatible und nicht kompatible Apps im selben Konfigurationselement anzugeben.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>So geben Sie eine Liste mit kompatiblen bzw. nicht kompatiblen Apps an  

1.  Geben Sie auf der Seite **Kompatible und nicht kompatible Apps (Android)** die folgenden Informationen ein:  

    |Einstellung|Weitere Informationen|  
    |-------------|----------------------|  
    |**Liste nicht kompatibler Apps**|Wählen Sie diese Option aus, wenn Sie eine Liste von Apps angeben möchten, die als nicht kompatibel gemeldet werden, wenn sie von Benutzern installiert werden.|  
    |**Liste kompatibler Apps**|Wählen Sie diese Option aus, wenn Sie eine Liste von Apps angeben möchten, die Benutzer installieren dürfen. Alle anderen installierten Apps werden als nicht kompatibel gemeldet.|  
    |**Hinzufügen**|Fügt eine App zur ausgewählten Liste hinzu. Geben Sie einen Namen Ihrer Wahl sowie die URL zur App im App-Store und optional den Herausgeber der App an.<br /><br /> Zum Angeben der URL suchen Sie im [Bereich "Apps" von Google Play](https://play.google.com/store/apps)die App, die Sie verwenden möchten.<br /><br /> Öffnen Sie die Seite der App, und kopieren Sie die URL in die Zwischenablage. Jetzt können Sie diese als URL in der Liste mit kompatiblen oder nicht kompatiblen Apps verwenden.<br /><br /> **Beispiel:** Suchen Sie in Google Play nach **Microsoft Office Mobile**. Die URL, die Sie verwenden, ist **https://play.google.com/store/apps/details?id=com.microsoft.office.officehub**.|  
    |**Bearbeiten**|Ermöglicht Ihnen das Bearbeiten von Name, Herausgeber und URL der ausgewählten App.|  
    |**Entfernen**|Löscht die ausgewählte App aus der Liste.|  
    |**Importierenieren**|Importiert eine Liste von Apps, die Sie in einer CSV-Datei angegeben haben. Verwenden Sie in der Datei das Format Anwendungsname, Herausgeber und App-URL.|  

2.  Klicken Sie danach auf **Weiter**. Konfigurationselemente mit kompatiblen und nicht kompatiblen App-Einstellungen müssen für Sammlungen von Benutzern bereitgestellt werden.

 Sie können auch einen der folgenden Berichte verwenden, um kompatible und nicht kompatible Apps zu überwachen:  

-   **Liste nicht kompatibler Apps und Geräte für einen angegebenen Benutzer** – Zeigt Informationen zu Benutzern und Geräten, die über App-Installationen verfügen, die mit einer von Ihnen angegebenen Richtlinie nicht konform sind.  

-   **Übersicht der Benutzer mit nicht kompatiblen Apps** – Zeigt Informationen zu Benutzern, die Apps installiert haben, die einer von Ihnen angegebenen Richtlinie nicht entsprechen.  

 Weitere Informationen zur Verwendung von Berichten finden Sie unter [Berichterstattung in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

