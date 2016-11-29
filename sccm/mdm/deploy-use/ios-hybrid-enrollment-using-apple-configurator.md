---
title: iOS-Hybridregistrierung mithilfe von Apple Configurator mit Configuration Manager
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 19f4880d6e7ba3da2e4bcfe725c1c806ee3b3334


---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>iOS-Hybridregistrierung mithilfe von Apple Configurator mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Unternehmen, die iOS-Geräte kaufen, die von Mitarbeitern verwendet werden, können diese mithilfe von Microsoft Intune verwalten. Sie können iOS-Geräte vorab registrieren, indem Sie sie über eine USB-Verbindung mit einem Mac-PC verbinden, der Apple Configurator ausführt. Vor der Registrierung müssen Sie ein firmeneigenes Intune-Geräteprofil in der Intune-Verwaltungskonsole vorbereiten und es auf den Macintosh-Computer exportieren. Der Registrierungsprozess setzt das Gerät auf Werkseinstellungen zurück und geht durch den Vorgang des Setup-Assistenten, um das Gerät zu konfigurieren. Das folgende Verfahren empfiehlt sich für dedizierte iOS-Geräte, die einen einzelnen Benutzer haben, der das Gerät verwendet, um auf Firmen-E-Mails und Unternehmensressourcen wie Apps und Daten zuzugreifen.  

##  <a name="a-namebkmksaea-apple-configurator-enrollment-via-setup-assistant"></a><a name="BKMK_SAE"></a> Apple Configurator-Registrierung über den Setup-Assistenten  
 Mit dem Apple Configurator können Sie iOS-Geräte auf die Werkseinstellungen zurücksetzen und für die Einrichtung durch den neuen Benutzer des Geräts vorbereiten.  Bei dieser Methode muss das iOS über USB mit einem Mac-Computer verbunden werden, um die Registrierung beim Unternehmen einzurichten. Vorausgesetzt wird die Verwendung von Apple Configurator 2.0.  

 **Voraussetzungen**  

-   Physischer Zugriff auf iOS-Geräte  

-   Geräteseriennummern – [Abrufen einer iOS-Seriennummer](https://support.apple.com/en-us/HT204308)  

-   USB-Verbindungskabel  

-   Macintosh-Computer mit [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

#### <a name="enable-setup-assistant-enrollment-with-configuration-manager-and-intune"></a>Aktivieren der Registrierung über den Setup-Assistenten mit Configuration Manager und Intune  

1.  **Hinzufügen eines Profils für die Unternehmensgeräteregistrierung**   
    Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Bestand und Kompatibilität** die Option **Übersicht**, erweitern Sie **Alle Unternehmensgeräte**, erweitern Sie **iOS**, und klicken Sie anschließend auf **Registrierungsprofile**. Klicken Sie auf der Registerkarte **Startseite** auf **Profil erstellen** , um den Assistenten zum Erstellen von Profilen zu öffnen. Konfigurieren Sie die Einstellungen auf den folgenden Seiten:  

    1.  On the **Allgemein** die folgenden Informationen an, und klicken Sie anschließend auf **Weiter**verwaltet werden können.  

        -   **Name:** Name des Geräteregistrierungsprofils. (Für Benutzer nicht sichtbar)  

        -   **Beschreibung** : Beschreibung des Geräteanmeldungsprofils. (Für Benutzer nicht sichtbar)  

        -   **Benutzeraffinität:** Gibt an, wie Geräte registriert werden. Verwenden Sie in den meisten Szenarios mit dem Setup-Assistenten **Benutzeraffinität anfordern**.  

            -   **Eingabeaufforderung für Benutzeraffinität:**Das Gerät muss während der ersten Setup einem Benutzer zugewiesen werden und kann dann berechtigt sein, im Namen dieses Benutzers auf Unternehmensdaten und E-Mails zuzugreifen.  

            -   **Keine Benutzeraffinität**: Das Gerät ist keinem Benutzer zugeordnet. Verwenden Sie diese Zuweisung für Geräte, die Aufgaben ohne den Zugriff auf lokale Benutzerdaten ausführen. Apps, die eine Benutzerzuweisung erfordern, funktionieren nicht.  

    2.  Lassen Sie auf der Seite **Programm zur Geräteregistrierung** das Kontrollkästchen **Einstellungen des Programms zur Geräteregistrierung für dieses Profil konfigurieren** deaktiviert, und klicken Sie auf **Weiter**.  

    3.  Überprüfen Sie die Zusammenfassung, und klicken Sie dann auf „Weiter“.  

2.  **Hinzufügen von iOS-Geräten für die Registrierung mit dem Setup-Assistenten**   
    Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Bestand und Kompatibilität** die Option **Übersicht**, erweitern Sie **Alle Unternehmensgeräte**, erweitern Sie **iOS**, und klicken Sie anschließend auf **Geräteinformationen**. Klicken Sie anschließend auf **Geräte hinzufügen**. Sie können Geräte auf zwei Arten hinzufügen:  

    - Sie können **eine CSV-Datei mit Seriennummern hochladen** – Erstellen Sie eine durch Trennzeichen getrennte Liste von zwei Spalten ohne Header, beschränkt auf 5.000 Geräte oder 5 MB pro CSV-Datei. Für jede Zeile stellt die erste Zelle die Seriennummer des Geräts dar und die zweite Zelle stellt die Gerätedetails dar (optional).

  Diese CSV-Datei wird bei der Anzeige in einem Text-Editor folgendermaßen angezeigt:  

    ```  
    0000000,PO 1234  
    111111111,PO 1234  
    ```  

    - Sie können ebenso **Seriennummern und Details manuell hinzufügen** – Geben Sie die Seriennummer und Gerätedetails von bis zu fünf Geräten ein.  

    Klicken Sie dann auf **Weiter**.  

3.  **Auswählen der zu registrierenden Geräte**   
    Bestätigen Sie die zu registrierenden Geräte. Bereits registrierte oder anderweitig registrierte Seriennummern werden nicht importiert. Klicken Sie zum Fortfahren auf **Weiter** .  

4.  **Zuweisen eines Profils**   
    Geben Sie aus der Liste der verfügbaren Profile das Profil an, das hinzugefügten Geräten zugewiesen werden soll, überprüfen Sie die **Registrierungsprofildetails**, und klicken Sie anschließend auf **Fertig stellen**. Manuell hinzugefügte Geräte können einem Registrierungsprofil zugewiesen werden. Mit DEP synchronisierte Geräte müssen allerdings einem DEP-fähigen Profil zugeordnet sein.  

5.  **Auswählen eines Profils für die Bereitstellung auf iOS-Geräten**   
    Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Bestand und Kompatibilität** die Option **Übersicht**, dann **Alle unternehmenseigenen Geräte** und anschließend **iOS**. Klicken Sie dann auf **Registrierungsprofile**, und wählen Sie das Geräteprofil aus, das auf Mobilgeräten bereitgestellt werden soll. Klicken Sie auf **Exportieren...** in der Taskleiste. Kopieren Sie die **Profil-URL**, und speichern Sie sie. Sie werden sie später in Apple Configurator hochladen, um das von iOS-Geräten verwendete Intune-Profil zu definieren.  Die Registrierungsprofil-URL ist ab dem Zeitpunkt des Exports zwei Wochen gültig. Nach zwei Wochen müssen Sie eine neue URL-Datei exportieren, um iOS-Geräte zu registrieren.  

     Zur Unterstützung von Apple Configurator 2 muss die URL des 2.0-Profils bearbeitet werden. Ersetzen Sie:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     durch  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```  

6.  **Vorbereiten des Geräts mit Apple Configurator**   
    iOS-Geräte werden mit dem Mac-Computer verbunden und für die Verwaltung mobiler Geräte registriert.  

    > [!WARNING]  
    >  Während des Registrierungsprozesses werden die Geräte auf Werkseinstellungen zurückgesetzt.  

    1.  Öffnen Sie auf einem Macintosh-Computer **Apple Configurator 2**.  Klicken Sie auf der Menüleiste auf **Apple Configurator 2** und dann auf **Voreinstellungen**.  

    2.  Wählen Sie im Bereich „Voreinstellungen“ **Server** aus, und klicken Sie links unten auf das Symbol „+“, um den MDM-Server-Assistenten zu starten. Klicken Sie auf **Weiter**.  

    3.  Geben Sie den **Namen** und die **Registrierungs-URL** für den MDM-Server aus Schritt 5 oben ein. Klicken Sie auf **Weiter**.  

         Wenn Sie eine Warnung bezüglich Anforderungen eines vertrauenswürdigen Profils für Apple TV erhalten, können Sie die Option **Vertrauenswürdiges Profil** sicher abbrechen, indem Sie auf das graue „X“ klicken. Sie können auch Ankerzertifikatwarnungen einfach ignorieren. Um den Vorgang fortzusetzen, klicken Sie auf **Weiter**, bis der Assistent abgeschlossen ist.  

    4.  Klicken Sie im Bereich **Server** neben dem Profil des neuen Servers auf „Bearbeiten“. Stellen Sie sicher, dass die Registrierungs-URL exakt mit der aus Intune exportierten URL übereinstimmt. Geben Sie die ursprüngliche URL erneut ein, wenn sie sich unterscheidet, und klicken Sie auf **Speichern**, um das aus Intune exportierte Registrierungsprofil zu speichern.  

    5.  Verbinden Sie die mobilen iOS-Geräte über einen USB-Adapter mit dem Apple-Computer.  

        > [!WARNING]  
        >  Während des Registrierungsprozesses werden die Geräte auf Werkseinstellungen zurückgesetzt. Setzen Sie als bewährte Methode das Gerät zurück, und schalten Sie es ein. Wenn Sie den Setup-Assistenten starten, sollte der Begrüßungsbildschirm zu sehen sein.  

    6.  Klicken Sie auf **Vorbereiten**. Wählen Sie im Bereich **iOS-Gerät vorbereiten** die Option **Manuell** aus, und klicken Sie dann auf **Weiter**.  

    7.  Wählen Sie im Bereich **Bei MDM-Server registrieren** den Servernamen aus, den Sie erstellt haben, und klicken Sie auf **Weiter**.  

    8.  Wählen Sie im Bereich **Bei MDM-Server registrieren** den Servernamen aus, den Sie erstellt haben, und klicken Sie auf **Weiter**.  

    9. Wählen Sie im Bereich **Organisation erstellen** die **Organisation** aus, oder erstellen Sie eine neue Organisation, und klicken Sie auf **Weiter**.  

    10. Wählen Sie im Bereich **iOS-Setup-Assistenten konfigurieren** die dem Benutzer angezeigten Schritte aus, und klicken Sie dann auf **Vorbereiten**. Falls aufgefordert, authentifizieren Sie sich, um die Vertrauenseinstellungen zu aktualisieren.  

    11. Nach Abschluss der Vorbereitung des iOS-Geräts können Sie das USB-Kabel trennen.  

7.  **Verteilen von Geräten**   
    Die Geräte sind nun bereit zur Unternehmensregistrierung. Schalten Sie die Geräte aus, und verteilen Sie sie an Benutzer. Wenn das Gerät eingeschaltet wird, wird der Setup-Assistent gestartet und fragt die Benutzer nach ihrem Geschäfts- oder Schulkonto.



<!--HONumber=Nov16_HO1-->


