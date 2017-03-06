---
title: "Registrieren von iOS-Geräten mithilfe von Apple Configurator – Configuration Manager | Microsoft-Dokumentation"
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 991eff171dce95590a7f050e0d3b07f98c0224b3
ms.openlocfilehash: 6c6e9edbc7b2fca3d1be4feabb238efab80465fa
ms.lasthandoff: 01/24/2017


---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>iOS-Hybridregistrierung mithilfe von Apple Configurator mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Unternehmen, die iOS-Geräte kaufen, die von Mitarbeitern verwendet werden, können diese mithilfe von Microsoft Intune verwalten. Zur Vorbereitung unternehmenseigener iOS-Geräte für die Registrierung konfigurieren Sie ein Anmeldungsprofil in der Configuration Manager-Konsole, und exportieren die URL des Profils zur Benutzung durch Apple Configurator. Sie bereiten das iOS-Gerät für die Registrierung vor, indem Sie es mit einem USB-Kabel mit einem Macintosh-Computer verbinden, und Apple Configurator verwenden, um es einzurichten. Apple Configurator Factory setzt das Gerät zurück und fügt das Anmeldungsprofil hinzu, sodass das Gerät registriert werden kann, wenn der Benutzer es zum ersten Mal einschaltet und die Erstkonfiguration durchläuft.

Das folgende Verfahren empfiehlt sich für dedizierte iOS-Geräte, die einen einzelnen Benutzer haben, der das Gerät verwendet, um auf Firmen-E-Mails und Unternehmensressourcen wie Apps und Daten zuzugreifen.  

## <a name="prerequisites"></a>Voraussetzungen  

-   Physischer Zugriff auf iOS-Geräte  

-   Geräteseriennummern – [Abrufen einer iOS-Seriennummer](https://support.apple.com/en-us/HT204308)  

-   Macintosh-Computer mit [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

-   USB-Kabel für die Verbindung von Geräten mit dem Macintosh-Computer  

## <a name="step-1-add-a-corporate-owned-device-enrollment-profile"></a>Schritt 1: Hinzufügen eines Anmeldungsprofils für die Unternehmensgeräteregistrierung

1.  Gehen Sie in der Configuration Manager-Konsole zu **Bestand und Konformität** > **Übersicht** > **All Corporate-owned Devices** (Alle firmeneigenen Geräte)  > **iOS** > **Enrollment Profiles** (Anmeldungsprofile). Klicken Sie auf **Profil erstellen**, um den Assistenten zum Erstellen von Profilen zu öffnen. Konfigurieren Sie die Einstellungen auf den folgenden Seiten:  

2.  Geben Sie auf der Seite **Allgemein** die folgenden Informationen an:  

    -   **Name** (Für Benutzer nicht sichtbar)  

    -   **Beschreibung** (Für Benutzer nicht sichtbar)  

    -   **Benutzeraffinität:** Gibt an, wie Geräte registriert werden. Verwenden Sie in den meisten Szenarios mit dem Setup-Assistenten **Benutzeraffinität anfordern**.  

        -   **Eingabeaufforderung für Benutzeraffinität:**Das Gerät muss während der ersten Setup einem Benutzer zugewiesen werden und kann dann berechtigt sein, im Namen dieses Benutzers auf Unternehmensdaten und E-Mails zuzugreifen.  

        -   **Keine Benutzeraffinität**: Das Gerät ist keinem Benutzer zugeordnet. Verwenden Sie diese Zuweisung für Geräte, die Aufgaben ohne den Zugriff auf lokale Benutzerdaten ausführen. Apps, die eine Benutzerzuweisung erfordern, funktionieren nicht.

    Klicken Sie zum Fortfahren auf **Weiter** .  

3.  Lassen Sie auf der Seite **Programm zur Geräteregistrierung** das Kontrollkästchen **Einstellungen des Programms zur Geräteregistrierung für dieses Profil konfigurieren** deaktiviert, und klicken Sie auf **Weiter**.  

4.  Überprüfen Sie die Zusammenfassung, und klicken Sie dann auf **Weiter**, um das Anmeldungsprofil zu erstellen. Klicken Sie zum Beenden des Assistenten auf **Schließen**. Sie sind jetzt bereit, die IMEI-Nummern oder Seriennummern für die Geräte hinzuzufügen, die Sie registrieren wollen.  

## <a name="step-2-predeclare-devices-to-enroll-with-setup-assistant"></a>Schritt 2: Vorabdeklarieren von iOS-Geräten für die Registrierung mit dem Setup-Assistenten

In diesem Schritt deklarieren Sie Geräte vorab als unternehmenseigen, indem Sie eine Liste von Hardware-IDs angeben (IMEI- oder Seriennummern).

Einzelheiten finden Sie unter [Vorabdeklarieren von Geräten mit IMEI- oder iOS-Seriennummern](predeclare-devices-with-hardware-id.md). Wenn Sie diese Aufgabe abgeschlossen haben, kehren Sie zu dieser Seite zurück, um mit dem nächsten Schritt fortzufahren.

## <a name="step-3-export-the-profile-to-deploy-to-ios-devices"></a>Schritt 3: Exportieren des Profils für die Bereitstellung auf iOS-Geräten

1.  Gehen Sie in der Configuration Manager-Konsole zu **Bestand und Konformität** > **Übersicht** > **All Corporate-owned Devices** (Alle firmeneigenen Geräte)  > **iOS** > **Enrollment Profiles** (Anmeldungsprofile).

2.  Wählen Sie das Anmeldungsprofil aus, das Sie für mobile Geräte bereitstellen möchten, und klicken Sie auf **Exportieren...**.

3.  Kopieren und speichern Sie die **Profil-URL** in einer Datei, die Sie bearbeiten können.   

4.  Zur Unterstützung von Apple Configurator 2 muss die URL des 2.0-Profils bearbeitet werden. Ersetzen Sie den folgenden Teil der URL:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     durch  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  Speichern Sie die bearbeitete Profil-URL. Sie benötigen sie zum Hinzufügen der URL des Anmeldungsprofils in Apple Configurator im [nächsten Abschnitt](#step-4-prepare-the-device-with-apple-configurator).  

> [!NOTE]
> Die Registrierungsprofil-URL ist ab dem Zeitpunkt des Exports zwei Wochen gültig. Nach zwei Wochen müssen Sie eine neue URL exportieren, um iOS-Geräte zu registrieren.

## <a name="step-4-prepare-the-device-with-apple-configurator"></a>Schritt 4: Vorbereiten des Geräts mit Apple Configurator

Verbinden Sie jedes Gerät mit einem Macintosh-Computer, und laden Sie das Anmeldungsprofil hoch, um iOS-Geräte für die Registrierung vorzubereiten.  

> [!WARNING]  
>  Apple Configurator setzt Geräte auf Werkseinstellungen zurück.  

1.  Öffnen Sie auf einem Macintosh-Computer **Apple Configurator 2**.  

2.  Klicken Sie auf der Menüleiste auf **Apple Configurator 2** > **Voreinstellungen**.  

2.  Wählen Sie im Bereich „Voreinstellungen“ **Server** aus, und klicken Sie links unten auf das Symbol „+“, um den MDM-Server-Assistenten zu starten. Klicken Sie auf **Weiter**.  

3.  Geben Sie den **Namen** und die **Registrierungs-URL** ein, die Sie [vorher](#step-3-export-the-profile-to-deploy-to-ios-devices) gespeichert haben. Klicken Sie auf **Weiter**.  

   > [!NOTE]
   > Wenn Sie eine Warnung bezüglich Anforderungen eines vertrauenswürdigen Profils für Apple TV erhalten, können Sie die Option **Trust Profile** (Vertrauenswürdiges Profil) sicher abbrechen, indem Sie auf das graue „X“ klicken. Sie können auch Ankerzertifikatwarnungen einfach ignorieren.

   Um den Vorgang fortzusetzen, klicken Sie auf **Weiter**, bis der Assistent abgeschlossen ist.  

4.  Klicken Sie im Bereich **Server** neben dem Profil des neuen Servers auf „Bearbeiten“. Stellen Sie sicher, dass die Registrierungs-URL exakt mit der übereinstimmt, die Sie vorher eingegeben haben. Geben Sie die URL erneut ein, wenn sie sich unterscheidet, und klicken Sie auf **Speichern**.  

5.  Verbinden Sie ein iOS-Gerät über ein USB-Kabel mit dem Macintosh-Computer.  

  > [!WARNING]  
  >  Durch diesen Vorgang werden Geräte auf Werkseinstellungen zurückgesetzt. Setzen Sie das Gerät zurück und schalten Sie es ein, bevor Sie das Gerät verbinden. Als bewährte Methode sollte der Begrüßungsbildschirm zu sehen sein, bevor Sie fortfahren.  

6.  Klicken Sie auf **Vorbereiten**. Wählen Sie im Bereich **Prepare iOS Device** (iOS-Gerät vorbereiten) die Option **Manuell** aus, und klicken Sie dann auf **Weiter**.  

7.  Wählen Sie im Bereich **Enroll in MDM Server** (Bei MDM-Server registrieren) den Servernamen aus, den Sie erstellt haben, und klicken Sie auf **Weiter**.  

9. Wählen Sie im Bereich **Organisation erstellen** die **Organisation** aus, oder erstellen Sie eine neue Organisation, und klicken Sie auf **Weiter**.  

10. Wählen Sie im Bereich **Configure iOS Setup Assistant** (iOS-Setup-Assistenten konfigurieren) die dem Benutzer angezeigten Schritte aus, und klicken Sie dann auf **Vorbereiten**. Falls aufgefordert, authentifizieren Sie sich, um die Vertrauenseinstellungen zu aktualisieren.  

11. Wenn Sie fertig sind, können Sie das USB-Kabel trennen.  

Wiederholen Sie diese Schritte für alle Geräte, die Sie für die Registrierung vorbereiten möchten.

## <a name="step-5-distribute-devices"></a>Schritt 5: Verteilen von Geräten

Die Geräte sind nun bereit zur Unternehmensregistrierung. Schalten Sie die Geräte aus, und verteilen Sie sie an Benutzer. Wenn das Gerät eingeschaltet wird, wird der Setup-Assistent gestartet, und fragt die Benutzer nach ihrem Geschäfts- oder Schulkonto, um mit der Registrierung zu beginnen.

