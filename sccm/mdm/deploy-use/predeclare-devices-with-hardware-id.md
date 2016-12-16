---
title: "Vorabdeklarieren von Geräten mit IMEI- oder iOS-Seriennummern"
description: "Vorabdeklarieren von unternehmenseigenen Geräten mit ihrer IMEI- oder iOS-Seriennummer."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6cd640085e90b2945326e3fa942ae9bd7b8f7e24
ms.openlocfilehash: 2550fef062b5ef508e4c0492a5a9c63ffcb9084a

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Vorabdeklarieren von Geräten mit IMEI- oder iOS-Seriennummern

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können unternehmenseigene Geräte identifizieren, indem Sie deren IMEI-Nummern (International Station Mobile Equipment Identity) oder iOS-Seriennummern importieren. Sie können eine CSV-Datei (comma-separated values, durch Trennzeichen getrennte Datei) hochladen, die die IMEI-Nummern der Geräte enthält, oder Geräteinformationen manuell eingeben.  Importierte Informationen legen den **Besitz** der registrierten Geräte in der Liste der Geräte auf „**Unternehmen**“ fest. Dennoch wird für jeden Benutzer, der auf den Dienst zugreift, eine Intune-Lizenz benötigt.  

## <a name="predeclare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Vorabdeklarieren von unternehmenseigenen Geräten mit IMEI- oder iOS-Seriennummer

1.  Navigieren Sie in der Configuration Manager-Konsole zu „Bestand und Kompatibilität“ > „Übersicht“ > „Alle unternehmenseigenen Geräte“ > „Vorab deklarierte Geräte“, und klicken Sie dann auf „Vorab deklarierte Geräte hinzufügen“. Der Assistent für vorab deklarierte Geräte wird geöffnet.
2.  Geben Sie an, wie Sie Geräteinformationen hinzufügen möchten:
     -  Laden Sie eine CSV-Datei mit IMEI-Seriennummern und Details hoch
     -  Fügen Sie IMEI-Nummern und Details manuell hinzu. Um die Informationen manuell eingeben zu können, geben Sie IMEI-Nummer oder die iOS-Seriennummer und Details zu den Geräten ein.

      Für hochgeladene Dateien navigieren Sie zu der CSV-Datei, die Informationen zu unternehmenseigenen, vorab deklarierten Geräten enthält. Die Datei muss das folgende Format aufweisen, ausgenommen der obersten Zeile, die nur zur Erklärung zur Verfügung gestellt wurde. Jede Zeile muss entweder eine IMEI-Nummer oder eine iOS-Seriennummer enthalten. Nur die Seriennummern der iOS-Geräte können vorab deklariert werden. Verwenden Sie IMEI-Nummern für andere Geräteplattformen. Diese Tabelle enthält Beispieldaten:
      | IMEI #  | iOS Serial #  | OS | Details |
      | :------------ |:---------------|:-----|:-----|
      | 123456789012345    |   | WINDOWS | Unternehmenseigenes Windows-Gerät|
      |       | A1B2C3D4E5C6 |   iOS |  Unternehmenseigenes iOS-Gerät|
      | 223456789012345 | E6D5C4B3A210 |   iOS |    Anderes iOS-Gerät|
      | 323456789012345 |        |   iOS |  Ein drittes iOS-Gerät|
      | 123456789012346 |         |   Android |     Unternehmenseigenes Android-Gerät|

    Nehmen Sie keine Kopfzeile in Ihre CSV-Datei auf. Das obige Beispiel enthält einen Header nur zur Verdeutlichung.

    **Die Spalten akzeptieren die folgenden Werte:**    
      - Spalte 1: IMEI-Nummer ohne Leerzeichen
      - Spalte 2: iOS-Seriennummer
      - Spalte 3: Betriebssystem des Geräts:
         - IOS – Alle iOS-Geräte
         - WINDOWS – Umfasst Windows Phone, Windows 10 Mobile und Windows-PCs
         - ANDROID – Alle Android-Geräte
      - Spalte 4: Details (optional) – Zusätzliche Geräteinformationen, die in der Configuration Manager-Konsole angezeigt werden. Maximal 1024 Zeichen.

    Klicken Sie auf **Weiter**.

3. Überprüfen Sie die Ergebnisse des Dateiimports. Wenn eine Gerätenummer im Voraus importiert wurde, zeigt Configuration Manager diese Geräte sowie den Ersatz **Details** an. Wählen Sie die Geräte, deren Details Sie überschreiben möchten. Gerätedetails können nur durch einen erneuten Import der Geräte-ID oder der Seriennummer geändert werden. Klicken Sie auf **Weiter**, um fortzufahren, oder auf **Zurück**, um aktualisierte Informationen beizubehalten und dann den Assistenten abzuschließen.

4. Wenn Ihr Import iOS-Seriennummern enthält, müssen Sie diese Geräte einem Registrierungsprofil zuweisen. Wählen Sie **Registrierungsprofil für Zuweisung** aus der Liste der verfügbaren Profile aus, und klicken Sie dann auf **Weiter**.

5. Klicken Sie auf **Weiter**, um die Zusammenfassung zu sehen, und schließen Sie dann den Assistenten ab.



<!--HONumber=Nov16_HO1-->


