---
title: "Vorabdeklarieren von Geräten mit IMEI-Nummern oder iOS-Seriennummern | Microsoft-Dokumentation"
description: "Vorabdeklarieren von unternehmenseigenen Geräten mit ihrer IMEI- oder iOS-Seriennummer."
ms.custom: na
ms.date: 12/16/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fd410a6572acce685dc6cdb954c1c2d97d5ed8b
ms.openlocfilehash: 2aa9c8c65904e573b6a81ac865e09d1cf2458509

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Vorabdeklarieren von Geräten mit IMEI- oder iOS-Seriennummern

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können unternehmenseigene Geräte identifizieren, indem Sie deren IMEI-Nummern (International Station Mobile Equipment Identity) oder iOS-Seriennummern importieren. Sie können eine CSV-Datei (comma-separated values, durch Trennzeichen getrennte Datei) hochladen, die die IMEI-Nummern der Geräte enthält, oder Geräteinformationen manuell eingeben.  Importierte Informationen legen den **Besitz** der registrierten Geräte in der Liste der Geräte auf **Unternehmen** fest. Dennoch wird für jeden Benutzer, der auf den Dienst zugreift, eine Intune-Lizenz benötigt.  

## <a name="how-to-predeclare-corporate-owned-devices"></a>Vorgehensweise für das Vorabdeklarieren von unternehmenseigenen Geräten

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Bestand und Konformität** > **Übersicht** > **Alle unternehmenseigenen Geräte** > **Vorab deklarierte Geräte**.

2.  Klicken Sie auf **Vorab deklarierte Geräte erstellen**. Der Assistent für das Erstellen vorab deklarierter Geräte wird geöffnet.

3.  Wählen Sie aus, wie Sie Geräteinformationen hinzufügen möchten:

     -  **Upload a CSV file containing IMEI or serial numbers and details** (CSV-Datei mit IMEI-Nummern oder Seriennummern und Details hochladen)

        Klicken Sie für diese Option auf **Durchsuchen**, um die CSV-Datei anzugeben, die Informationen für das Vorabdeklarieren von unternehmenseigenen Geräten enthält. Die CSV-Datei muss korrekt formatiert sein. Weitere Informationen finden Sie unter [Format für das Hochladen von CSV-Dateien](#format-for-uploading-csv-files).

     -  **Manually add IMEI or serial numbers and details** (IMEI-Nummern oder Seriennummern und Details manuell hinzufügen)

        Um die Informationen manuell eingeben zu können, geben Sie IMEI-Nummer oder die iOS-Seriennummer und Details zu den Geräten ein. Korrigieren Sie etwaige Fehler oder Warnungen, bevor Sie fortfahren.

    Klicken Sie auf **Weiter**.

4. Wenn Sie eine CSV-Datei hochgeladen haben, prüfen Sie die Ergebnisse des Dateiimports. Wenn eine Gerätenummer bereits importiert wurde, zeigt Configuration Manager die betreffenden Geräte sowie **Details** zum Ersatz an. Wählen Sie die Geräte, deren Details Sie überschreiben möchten. Gerätedetails können nur durch einen erneuten Import der Geräte-ID oder der Seriennummer geändert werden.

  Wenn Sie die Nummer manuell eingeben möchten, füllen Sie das Formular für die Geräte aus, die Sie vorab deklarieren möchten.

  Klicken Sie zum Fortfahren auf **Weiter** .

4. Wenn Ihre Liste iOS-Seriennummern umfasst, wählen Sie aus der Liste der verfügbaren Profile **Registrierungsprofil für Zuweisung** aus, und klicken Sie dann auf **Weiter**.

5. Klicken Sie auf **Weiter**, um die Details zu überprüfen, und klicken Sie dann erneut auf **Weiter**, um die Daten hochzuladen.

6. Klicken Sie zum Fertigstellen auf **Schließen**.

## <a name="format-for-uploading-csv-files"></a>Format für das Hochladen von CSV-Dateien

Die CSV-Datei, die Sie verwenden, um Geräte anhand der IMEI-Nummer oder der Seriennummer zu identifizieren, muss das folgende Format aufweisen (außer der obersten Zeile, die lediglich Informationszwecken dient). Jede Zeile muss entweder eine IMEI-Nummer oder eine iOS-Seriennummer enthalten. Nur die Seriennummern der iOS-Geräte können vorab deklariert werden. Verwenden Sie IMEI-Nummern für andere Geräteplattformen. Diese Tabelle enthält Beispieldaten:

| IMEI #  | iOS Serial #  | OS | Details |
|------------ |---------------|-----|-----|
| 123456789012345    |   | WINDOWS | Unternehmenseigenes Windows-Gerät|
|   | A1B2C3D4E5C6 | IOS |  Unternehmenseigenes iOS-Gerät|
| 223456789012345 | E6D5C4B3A210 |   IOS |  Anderes iOS-Gerät|
| 323456789012345 |        |   IOS |    Ein drittes iOS-Gerät|
| 123456789012346 |         |   ANDROID |   Unternehmenseigenes Android-Gerät|

Nehmen Sie keine Kopfzeile in Ihre CSV-Datei auf. Das folgende Beispiel zeigt dieselben Beispieldaten im CSV-Format:

```
123456789012345,,WINDOWS,Company-owned Windows device
,A1B2C3D4E5C6,IOS,Company-owned iOS device
223456789012345,E6D5C4B3A210,IOS,Another iOS device
323456789012345,,IOS,A third iOS device
123456789012346,,ANDROID,Company-owned Android device
```

Die Spalten in der CSV-Datei akzeptieren die folgenden Werte:

| Spalte 1 | Spalte 2 | Spalte 3 | Spalte 4 |
|---|---|---|---|
|IMEI-Nummer ohne Leerzeichen | iOS-Seriennummer | iOS, WINDOWS oder ANDROID | Optionale Gerätedetails (maximal 1024 Zeichen) |



<!--HONumber=Dec16_HO3-->


