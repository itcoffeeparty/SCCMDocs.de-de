---
title: "Erstellen von Konfigurationselementen für iOS und Mac OS X-Geräte, die mit Intune verwaltet werden | Microsoft-Dokumentation"
description: "Verwenden Sie das Konfigurationselement für iOS und Mac OS X von System Center Configuration Manager, um Einstellungen für iOS und Mac OS X-Geräte zu verwalten."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 613a48ac-c55d-4c4a-94ea-d3747a1b10cb
caps.latest.revision: 15
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: bede390e30a0c92df6fcb33c0619ce67b15fc8af
ms.lasthandoff: 03/06/2017


---
# <a name="create-configuration-items-for-ios-and-mac-os-x-devices-managed-with-intune"></a>Erstellen von Konfigurationselementen für iOS und Mac OS X-Geräte, die mit Intune verwaltet werden

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie das Konfigurationselement **iOS und Mac OS X** von System Center Configuration Manager, um Einstellungen für iOS- und Mac OS X-Geräte zu verwalten, die bei Microsoft Intune registriert sind oder lokal von Configuration Manager verwaltet werden.  

## <a name="to-create-an-ios-and-mac-os-x-configuration-item"></a>So erstellen Sie ein Konfigurationselement für iOS und Mac OS X  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationselemente**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen**einen Namen und optional eine Beschreibung für das Konfigurationselement an.  

5.  Wählen Sie unter **Typ des zu erstellenden Konfigurationselements angeben**den Typ **iOS und Mac OS X**aus.  

6.  Klicken Sie auf **Kategorien**, wenn Sie Kategorien erstellen und zuweisen, um das Durchsuchen und Filtern von Konfigurationselementen in der Configuration Manager-Konsole zu erleichtern.  

7.  Wählen Sie auf der Seite **Unterstützte Plattformen** die jeweiligen iOS- oder Mac OS X-Plattformen zur Bewertung des Konfigurationselements aus.  

8.  Wählen Sie auf der Seite **Geräteeinstellungen** die Einstellungsgruppe aus, die Sie konfigurieren möchten. Informieren Sie sich in diesem Thema unter [Referenz zu Einstellungen des Konfigurationselements für iOS und Mac OS X](#ios-and-mac-os-x-configuration-item-settings-reference) über die Details, und klicken Sie dann auf **Weiter**.  

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

##  <a name="ios-and-mac-os-x-configuration-item-settings-reference"></a>Referenz zu Einstellungen des Konfigurationselements für iOS und Mac OS X  

###  <a name="password"></a>Kennwort  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Kennworteinstellungen auf mobilen Geräten erforderlich**|Auf unterstützten Geräten ein Kennwort erfordern.|  
|**Minimale Kennwortlänge (Zeichen)**|Die Mindestlänge für das Kennwort.|  
|**Kennwortablauf in Tagen**|Die Anzahl der Tage, bevor ein Kennwort geändert werden muss.|  
|**Anzahl der gespeicherten Kennwörter**|Verhindert die Wiederverwendung zuvor verwendeter Kennwörter.|  
|**Anzahl der gescheiterten Anmeldeversuche vor dem Zurücksetzen eines Geräts**|Setzt das Gerät zurück, wenn diese Anzahl von Anmeldeversuchen fehlschlägt.<br>(nur iOS)|
|**Leerlaufzeit vor dem Sperren des Geräts**|Legt fest, nach wie vielen Minuten Inaktivität das Gerät automatisch gesperrt wird.|
|**Kennwortkomplexität**|Wählen Sie aus, ob Sie eine PIN wie „1234“ angeben können oder ob ein sicheres Kennwort erforderlich ist.|
|**Einfache Kennwörter zulassen**|Erlaubt die Verwendung einfacher Kennwörter wie „0000“ und „1234“.|
|**Fingerabdruck zum Entsperren**|Ermöglicht das Entsperren des Geräts mittels Fingerabdruck.|

###  <a name="device"></a>Gerät  
 Diese Einstellungen gelten für iOS- und Mac OS X-Geräte.  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Sprachwahlverfahren**|Ermöglicht die Verwendung des Features „Sprachwahlverfahren“ auf dem Gerät.|  
|**Sprach-Assistent**|Ermöglicht die Verwendung eines Sprach-Assistenten wie Siri.|  
|**Sprach-Assistent im gesperrten Modus**|Ermöglicht die Verwendung eines Sprach-Assistenten wie Siri, wenn das Gerät gesperrt ist.|  
|**Bildschirmaufnahme**|Ermöglicht die Aufnahme eines Screenshots der Geräteanzeige.|  
|**Videochat-Client**|Ermöglicht die Verwendung von Videochat-Apps wie Facetime.|  
|**Gamecenter-Freunde hinzufügen**|Ermöglicht das Hinzufügen von Freunden in der Gamecenter-App.|  
|**Multiplayerspiele**|Ermöglicht Ihnen das Spielen mit anderen Spielern über das Internet.|  
|**Persönliche Brieftaschensoftware im gesperrten Modus**|Ermöglicht die Verwendung einer persönlichen Brieftaschensoftware wie Passbook.|  
|**Übermittlung von Diagnosedaten**|Ermöglicht die Übermittlung von Protokolldateien der App.|  

###  <a name="store"></a>Speicher  
 Diese Einstellungen gelten nur für iOS-Geräte.  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Anwendungsstore**|Ermöglicht den Zugriff auf den App Store auf dem Gerät.|  
|**Geben Sie ein Kennwort für den Zugriff auf den Anwendungsstore ein.**|Benutzer müssen ein Kennwort für den Zugriff auf den App Store eingeben.|  
|**In-App-Käufe**|Bietet Benutzern die Möglichkeit zu In-App-Käufen.|  

###  <a name="browser"></a>Browser  
 Diese Einstellungen gelten nur für iOS-Geräte.  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Webbrowser zulassen**|Der Benutzer kann den Standardwebbrowser des Geräts verwenden.|  
|**Automatisch ausfüllen**|Benutzer können die Einstellungen für AutoVervollständigen im Browser ändern.|  
|**Active Scripting**|Browser können Skripts ausführen, z. B. ActiveX-Skripts.|  
|**Popupblocker**|Aktiviert oder deaktiviert den Popupblocker des Browsers.|  
|**Cookies**|Ermöglicht das Speichern von Cookies auf dem Gerät.|  
|**Betrugswarnung**|Aktivieren oder deaktivieren von Warnungen zu potenziell betrügerischen Websites.|  

###  <a name="content-rating"></a>Inhaltsbewertung  
 Diese Einstellungen gelten nur für iOS-Geräte.  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Anstößiger Inhalt im Medienstore**|Geben Sie an, ob der Zugriff auf nicht jugendfreie Inhalte über den App Store zulässig ist.|  
|**Bewertungsregion**|Gibt das Land an, für das Sie Bewertungseinschränkungen anwenden möchten.|  
|**Filmbewertung**|Geben Sie die maximale Bewertung für Filminhalte an, die Sie zulassen möchten.|  
|**Bewertung des TV-Programms**|Geben Sie die maximale Bewertung für TV-Programminhalte an, die Sie zulassen möchten.|  
|**App-Bewertung**|Geben Sie die maximale Bewertung für App-Inhalte an, die Sie zulassen möchten.|  

> [!NOTE]  
>  Die Bewertungen, die Sie auswählen können, variieren je nach **Bewertungsregion** , die Sie ausgewählt haben.  

###  <a name="cloud"></a>Cloud  
 Diese Einstellungen gelten nur für iOS-Geräte.  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Cloudsicherung**|Ermöglicht die Sicherung in einem Clouddienst wie iCloud.|  
|**Verschlüsselte Sicherung**|Ermöglicht das Verschlüsseln der Sicherung in einem Clouddienst.|  
|**Dokumentsynchronisierung**|Ermöglicht die Dokumentsynchronisierung mit einem Clouddienst.|  
|**Fotosynchronisierung**|Ermöglicht die Fotosynchronisierung mit einem Clouddienst.|  

###  <a name="security"></a>Sicherheit  
 Diese Einstellungen gelten nur für iOS-Geräte.  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Kamera**|Ermöglicht die Verwendung der Gerätekamera.|  

###  <a name="roaming"></a>Roaming  
 Diese Einstellungen gelten nur für iOS-Geräte.  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Sprachroaming**|Ermöglicht Sprachanrufe beim Roaming.|  
|**Automatische Synchronisierung beim Roaming**|Ermöglicht dem Gerät die automatische Synchronisierung beim Roaming.|  
|**Datenroaming**|Ermöglicht beim Zugriff auf Daten das Roaming zwischen Netzwerken.|  

###  <a name="system-security"></a>Systemsicherheit  
 Diese Einstellungen gelten nur für iOS-Geräte.  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Benutzer akzeptiert nicht vertrauenswürdige TLS-Zertifikate**|Bei **Zulässig**kann der Benutzer diese Zertifikate akzeptieren. Bei **Nicht zulässig**werden nicht vertrauenswürdige Zertifikate automatisch abgelehnt.|
|**Aktivierungssperre zulassen (nur überwachter Modus)**|Verwenden Sie diese Einstellung, um die iOS-Aktivierungssperre auf den von Ihnen **überwachten** iOS-Geräten zu aktivieren. Weitere Informationen zur Aktivierungssperre finden Sie unter [Verwalten der iOS-Aktivierungssperre](../../mdm/deploy-use/manage-ios-activation-lock.md).
|**Kontrollzentrum für den Sperrbildschirm**|Steuert, ob auf die Kontrollcenter-App zugegriffen werden kann, wenn das Gerät gesperrt ist.|  
|**Ansicht „Benachrichtigung“ für den Sperrbildschirm**|Steuert, ob Benachrichtigungen angezeigt werden können, wenn das Gerät gesperrt ist.|  
|**Ansicht „Heute“ für den Sperrbildschirm**|Steuert, ob die Ansicht „Heute“ angezeigt werden kann, wenn das Gerät gesperrt ist.|   

###  <a name="data-protection"></a>Datenschutz  
 Diese Einstellungen gelten nur für iOS-Geräte.  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Dokumente in verwalteten Apps in anderen nicht verwalteten Apps öffnen**|Zur Verwendung mit Apps, die nach Anwendungsverwaltungsrichtlinien von Configuration Manager verwaltet werden|  
|**Dokumente in nicht verwalteten Apps in anderen verwalteten Apps öffnen**|Zur Verwendung mit Apps, die nach Anwendungsverwaltungsrichtlinien von Configuration Manager verwaltet werden|  

###  <a name="compliant-and-noncompliant-apps-ios"></a>Kompatible und nicht kompatible Apps (iOS)  
 Dient zum Angeben einer Liste von iOS-Apps, die in Ihrem Unternehmen kompatibel oder nicht kompatibel sind. Anschließend können Sie mithilfe von Berichten Geräte, auf denen nicht kompatible Apps installiert sind, und dazugehörige Benutzer bestimmen.  

 Es ist nicht möglich, kompatible und nicht kompatible Apps im selben Konfigurationselement anzugeben.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>So geben Sie eine Liste mit kompatiblen bzw. nicht kompatiblen Apps an  

1.  Geben Sie auf der Seite **Kompatible und nicht kompatible Apps (iOS)** die folgenden Informationen ein:  

    -   **Liste nicht kompatibler Apps** – Wählen Sie diese Option aus, wenn Sie eine Liste von Apps angeben möchten, die als nicht kompatibel gemeldet werden, wenn sie von Benutzern installiert werden.  

    -   **Liste kompatibler Apps** – Wählen Sie diese Option aus, wenn Sie eine Liste von Apps angeben möchten, die Benutzer installieren dürfen. Alle anderen installierten Apps werden als nicht kompatibel gemeldet.  

    -   **Hinzufügen** – Fügt eine App zur ausgewählten Liste hinzu. Geben Sie einen Namen Ihrer Wahl sowie die URL zur App im App-Store und optional den Herausgeber der App an.  

         Zum Angeben der URL suchen Sie im iTunes App Store die App, die Sie verwenden möchten.  

         Öffnen Sie die Seite der App, und kopieren Sie die URL in die Zwischenablage. Jetzt können Sie diese als URL in der Liste mit kompatiblen oder nicht kompatiblen Apps verwenden.  

         **Beispiel:** Suchen Sie im Store die App **Microsoft Word für iPad** . Die URL, die Sie verwenden, ist **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**.  

    -   **Bearbeiten** – Ermöglicht Ihnen das Bearbeiten von Name, Herausgeber und URL der ausgewählten App.  

    -   **Entfernen** – Löscht die ausgewählte App aus der Liste.  

    -   **Importieren** – Importiert eine Liste von Apps, die Sie in einer CSV-Datei angegeben haben. Verwenden Sie in der Datei das Format Anwendungsname, Herausgeber und App-URL.  

2.  Klicken Sie danach auf **Weiter**.  

 Sie können auch einen der folgenden Berichte verwenden, um kompatible und nicht kompatible Apps zu überwachen:  

-   **Liste nicht kompatibler Apps und Geräte für einen angegebenen Benutzer** – Zeigt Informationen zu Benutzern und Geräten, die über App-Installationen verfügen, die mit einer von Ihnen angegebenen Richtlinie nicht konform sind.  

-   **Übersicht der Benutzer mit nicht kompatiblen Apps** – Zeigt Informationen zu Benutzern, die Apps installiert haben, die einer von Ihnen angegebenen Richtlinie nicht entsprechen.  

 Weitere Informationen zur Verwendung von Berichten finden Sie unter [Berichterstattung in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

###  <a name="compliant-and-noncompliant-apps-mac-os-x"></a>Kompatible und nicht kompatible Apps (Mac OS X)  
 Dient zum Angeben einer Liste von Max OS X-Apps, die in Ihrem Unternehmen kompatibel oder nicht kompatibel sind. Anschließend können Sie mithilfe von Berichten Geräte, auf denen nicht kompatible Apps installiert sind, und dazugehörige Benutzer bestimmen.  

 Es ist nicht möglich, kompatible und nicht kompatible Apps im selben Konfigurationselement anzugeben.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>So geben Sie eine Liste mit kompatiblen bzw. nicht kompatiblen Apps an  

1.  Geben Sie auf der Seite **Kompatible und nicht kompatible Apps (Mac OS X)** die folgenden Informationen an:  

    -   **Liste nicht kompatibler Apps** – Wählen Sie diese Option aus, wenn Sie eine Liste von Apps angeben möchten, die als nicht kompatibel gemeldet werden, wenn sie von Benutzern installiert werden.  

    -   **Liste kompatibler Apps** – Wählen Sie diese Option aus, wenn Sie eine Liste von Apps angeben möchten, die Benutzer installieren dürfen. Alle anderen installierten Apps werden als nicht kompatibel gemeldet.  

    -   **Hinzufügen** – Fügt eine App zur ausgewählten Liste hinzu. Geben Sie einen Namen Ihrer Wahl, optional den Herausgeber der App sowie die Paket-ID der App an.  

        > [!TIP]  
        >  Zum Ermitteln der Paket-ID einer App führen Sie auf einem Mac-Computer, auf dem die App installiert ist, die folgenden Schritte aus:  
        >   
        >  1.  Öffnen Sie den Ordner, in dem die App installiert ist (z. B. **/Programme**).  
        > 2.  Wählen Sie das Paket *<App-Name\>***.app** und anschließend **Paketinhalt anzeigen** aus.  
        > 3.  Öffnen Sie die Datei **Info.plist** .  
        > 4.  Überprüfen Sie den Wert, der dem Schlüssel **CFBundleIdentifier**zugewiesen ist.  
        >   
        >  Die Paket-ID weist das Format **com.contoso.appname**auf.  

    -   **Bearbeiten** – Ermöglicht Ihnen das Bearbeiten des Namens, Herausgebers und der Paket-ID der ausgewählten App.  

    -   **Entfernen** – Löscht die ausgewählte App aus der Liste.  

    -   **Importieren** – Importiert eine Liste von Apps, die Sie in einer CSV-Datei angegeben haben. Verwenden Sie das Format, den App-Namen, den Herausgeber und die Paket-ID der App in der Datei.  

2.  Klicken Sie danach auf **Weiter**. Konfigurationselemente mit kompatiblen und nicht kompatiblen App-Einstellungen müssen für Sammlungen von Benutzern bereitgestellt werden.

 Sie können auch einen der folgenden Berichte verwenden, um kompatible und nicht kompatible Apps zu überwachen:  

-   **Liste nicht kompatibler Apps und Geräte für einen angegebenen Benutzer** – Zeigt Informationen zu Benutzern und Geräten, die über App-Installationen verfügen, die mit einer von Ihnen angegebenen Richtlinie nicht konform sind.  

-   **Übersicht der Benutzer mit nicht kompatiblen Apps** – Zeigt Informationen zu Benutzern, die Apps installiert haben, die einer von Ihnen angegebenen Richtlinie nicht entsprechen.  

 Weitere Informationen zur Verwendung von Berichten finden Sie unter [Berichterstattung in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="ios-and-mac-os-x-custom-profile-settings"></a>Einstellungen für benutzerdefinierte iOS- und Mac OS X-Profile  
 Verwenden Sie **Benutzerdefinierte iOS-und Mac OS X-Profile** zum Bereitstellen von Einstellungen, die Sie mit dem [Apple Configurator-Tool](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) für iOS- und Mac OS X-Geräte erstellt haben. Mit diesem Tool können Sie zahlreiche Einstellungen zur Betriebssteuerung dieser Geräte erstellen und in ein Konfigurationsprofil exportieren. Sie können dieses Konfigurationsprofil anschließend in ein benutzerdefiniertes iOS-und Mac OS X-Profil importieren und die Einstellungen für Benutzer und Geräte in Ihrer Organisation bereitstellen.  

> [!NOTE]  
>  Stellen Sie sicher, dass die Einstellungen, die Sie aus dem Apple Configurator-Tool exportieren, mit der iOS- oder Mac OS X-Version auf den Geräten kompatibel sind, für die Sie das Profil bereitstellen. Um Informationen zum Korrigieren inkompatibler Einstellungen zu erhalten, suchen Sie nach der Konfigurationsprofilreferenz und der Verwaltungsprotokollreferenz für mobile Geräte auf der [Apple Developer](https://developer.apple.com/) -Website.  

### <a name="to-create-an-ios-and-mac-os-x-custom-profile"></a>So erstellen Sie ein benutzerdefiniertes iOS- und Mac OS X-Profil  

1.  Geben Sie auf der Seite **Einstellungen für benutzerdefiniertes iOS- und Mac OS X-Profil konfigurieren** des ** **Assistenten zum Erstellen von Konfigurationselementen die folgenden Informationen an:  

    -   **Name des benutzerdefinierten Konfigurationsprofils (wird Benutzern angezeigt)** – Geben Sie einen Namen für die Richtlinie an, der auf dem Gerät und in Configuration Manager-Berichten angezeigt wird.  

    -   **Importieren** – Wählen Sie eine Datei aus, die Sie aus dem Apple Configurator-Tool exportiert haben.  

    -   **Konfigurationsprofildetails** – Zeigt die Datei an, die Sie importiert haben.  

    -   **Nicht kompatible Einstellungen wiederherstellen** -  

         Wählen Sie diese Option aus, wenn Sie nicht kompatible Einstellungen wiederherstellen möchten (sofern unterstützt).  

    -   **Schweregrad der Nichtkompatibilität für Berichte** – Geben Sie den Schweregrad an, der gemeldet wird, wenn diese Kompatibilitätsrichtlinie als nicht kompatibel ausgewertet wird. Die folgenden Schweregrade sind verfügbar:  

        > [!NOTE]  
        >  Wenn sich ein Mac OS X-Gerät im Energiesparmodus befindet, können keine Richtlinien oder Profile bereitgestellt oder inventarisiert werden. Infolgedessen zeigt die Configuration Manager-Konsole möglicherweise vorübergehend den Status „Richtlinieneinstellungen mit Fehlern“ an, bis der Energiesparmodus beendet wird.  

        -   **Keiner** Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.  

        -   **Information** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.  

        -   **Warnung** Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.  

        -   **Kritisch** Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.  

        -   **Kritisch mit Ereignis** Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.  

## <a name="how-to-create-a-configuration-profile-file"></a>Erstellen einer Konfigurationsprofildatei  
 Die Konfigurationsprofildatei, die von der benutzerdefinierten Richtlinie verwendet wird, kann auf zwei Weisen erstellt werden:  

-   Exportieren Sie die Datei (mit der Erweiterung **.mobileconfig**) aus dem Apple Configurator-Tool.  

-   Erstellen Sie die Datei selbst unter Verwendung des entsprechenden Schemas aus der [Apple Configuration Profile Key Reference](https://developer.apple.com/library/ios/featuredarticles/iPhoneConfigurationProfileRef/Introduction/Introduction.html).  

###  <a name="kiosk-mode-ios"></a>Kioskmodus (iOS)  
 Über den Kioskmodus können Sie ein Gerät sperren, damit nur bestimmte Features funktionieren. Beispielsweise können Sie festlegen, dass auf einem Gerät nur eine von Ihnen angegebene verwaltete App ausgeführt werden kann, oder Sie können die Lautstärkeregler eines Geräts deaktivieren. Diese Einstellungen können für ein Demomodell eines Geräts oder ein Gerät nützlich sein, das nur eine bestimmte Funktion ausführen soll, wie z. B. ein Point-of-Sale-Gerät.  

#### <a name="to-configure-kiosk-mode-for-ios-devices"></a>So konfigurieren Sie den Kioskmodus für iOS-Geräte  

1.  Geben Sie auf der Seite zum **Konfigurieren der Kioskmoduseinstellungen für iOS-Geräte** des **Assistenten zum Erstellen von Konfigurationselementen**die folgenden Informationen an:  

    -   **App auswählen** – Wählen Sie die App aus, die ausgeführt werden darf, während sich das Gerät im Kioskmodus befindet. Andere Apps dürfen auf dem Gerät nicht ausgeführt werden. Wählen Sie aus:  

        -   **Managed App** : Klicken Sie auf „Durchsuchen“, und wählen Sie dann eine verwaltete App aus.  

        -   **Store App** : Geben Sie die URL zu einer App im App Store an, und klicken Sie dann auf **Get App ID** , um das Feld **App ID** zu füllen.  

         So finden Sie die URL der App:  

        -   Suchen Sie mithilfe einer Suchmaschine die gewünschte App im iTunes App Store, und öffnen Sie die Seite für die App.  

        -   Kopieren Sie die URL der Seite, und verwenden Sie diese als URL zur Angabe der App, die Sie im Kioskmodus ausführen möchten.  

        -   **Beispiel:** Suchen Sie nach **Microsoft Word für iPad**. Die URL, die Sie verwenden, ist **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**.  

    -   **Toucheingabe** – Aktiviert oder deaktiviert den Touchscreen des Geräts.  

    -   **Automatische Ausrichtung** – Aktiviert oder deaktiviert die Funktion zum Ändern der Bildschirmausrichtung, wenn Sie das Gerät drehen.  

    -   **Lautstärketasten** – Aktiviert oder deaktiviert die Verwendung der Lautstärketasten am Gerät.  

    -   **Stummschalter** – Aktiviert oder deaktiviert die Stummschaltung (Ruftonschalter) am Gerät.  

    -   **Bildschirm-Standby-Taste** – Aktiviert oder deaktiviert die Taste für Standby/Aktivierung des Bildschirms am Gerät.  

    -   **Automatisch sperren** – Aktiviert oder deaktiviert die automatische Sperrung des Geräts.  

    -   **Mono-Audio** – Aktiviert oder deaktiviert die Barrierefreiheitseinstellung **Mono-Audio**.  

    -   **VoiceOver** – Aktiviert oder deaktiviert die Barrierefreiheitseinstellung **VoiceOver**, die den Text auf dem Gerätedisplay laut vorliest.  

    -   **VoiceOver-Anpassungen** – Aktiviert oder deaktiviert VoiceOver-Anpassungen, die Ihnen das Anpassen der VoiceOver-Funktion ermöglichen (z.B. wie schnell Bildschirmtext vorgelesen wird).  

    -   **Zoom** – Aktiviert oder deaktiviert die Barrierefreiheitseinstellung **Zoom**, die Ihnen das Vergrößern des Texts auf dem Gerätedisplay durch Toucheingabe ermöglicht.  

    -   **Zoomanpassungen** – Aktiviert oder deaktiviert Zoomanpassungen zum individuellen Einrichten der Zoomfunktion.  

    -   **Farben umkehren** – Aktiviert oder deaktiviert die Barrierefreiheitseinstellung **Farben umkehren**, die die Anzeige für Benutzer mit eingeschränkter Sehfähigkeit anpasst.  

    -   **Anpassungen für „Farben umkehren“** – Aktiviert oder deaktiviert Anpassungen für die Farbumkehr, mit denen Sie die Funktion zur Farbumkehr individuell einrichten können.  

    -   **AssistiveTouch** – Aktiviert oder deaktiviert die Barrierefreiheitseinstellung **AssistiveTouch**, die Benutzer bei der Ausführung von Bildschirmgesten unterstützt, die ihnen Schwierigkeiten bereiten können.  

    -   **AssistiveTouch-Anpassungen** – Aktiviert oder deaktiviert AssistiveTouch-Anpassungen, mit denen Sie die AssistiveTouch-Funktion individuell einrichten können.  

    -   **Sprachauswahl** – Aktiviert oder deaktiviert die Barrierefreiheitseinstellung **Sprachauswahl**, mit der ausgewählter Text vorgelesen werden kann.  

    -   **Nicht kompatible Einstellungen wiederherstellen** – Wählen Sie diese Option aus, wenn Sie nicht kompatible Einstellungen wiederherstellen möchten (sofern unterstützt).  

    -   **Schweregrad der Nichtkompatibilität für Berichte** – Geben Sie den (in Configuration Manager-Berichten) gemeldeten Schweregrad an, wenn diese Kompatibilitätsrichtlinie als nicht kompatibel ausgewertet wird. Die verfügbaren Schweregrade sind:  

        -   **Keiner**: Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad gemeldet.  

        -   **Information**: Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** gemeldet.  

        -   **Warnung**: Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** gemeldet.  

        -   **Kritisch** Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** gemeldet.  

        -   **Kritisch mit Ereignis**: Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** gemeldet.  

