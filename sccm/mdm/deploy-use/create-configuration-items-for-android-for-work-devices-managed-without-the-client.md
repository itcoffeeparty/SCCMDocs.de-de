---
title: "Erstellen von Konfigurationselementen für Android for Work-Geräte, die mit Intune verwaltet werden"
ms.custom: na
ms.date: 2017-03-28
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab6784fd-8c57-4be9-858f-50fe39f2ff5f
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
translation.priority.ht:
- cs-cz
- de-de
- en-gb
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: e6170339b8f3354c549579f127a5c3c618833943
ms.lasthandoff: 03/27/2017

---
# <a name="how-to-create-configuration-items-for-android-for-work-devices-managed-with-intune"></a>Erstellen von Konfigurationselementen für Android for Work-Geräte, die mit Intune verwaltet werden
  
 Verwenden Sie das System Center Configuration Manager-Konfigurationselement für **Android for Work**, um Einstellungen für Android for Work-Geräte zu verwalten, die in Microsoft Intune registriert sind oder lokal von Configuration Manager verwaltet werden.  
  
### <a name="to-create-an-android-for-work-configuration-item"></a>Erstellen eines Konfigurationselements für Android for Work  
  
1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Konformität**.  
  
2.  Erweitern Sie im Arbeitsbereich **Bestand und Konformität** die **Konformitätseinstellungen**, und klicken Sie auf **Konfigurationselemente**.  
  
3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  
  
4.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen**einen Namen und optional eine Beschreibung für das Konfigurationselement an.  
  
5.  Wählen Sie unter **Typ des zu erstellenden Konfigurationselements angeben** den Typ **Android for Work** aus.  
  
6.  Klicken Sie auf **Kategorien**, wenn Sie Kategorien erstellen und zuweisen, um das Durchsuchen und Filtern von Konfigurationselementen in der Configuration Manager-Konsole zu erleichtern.  
  
7.  Wählen Sie auf der Seite **Geräteeinstellungen** des Assistenten die Einstellungsgruppe aus, die Sie konfigurieren möchten. Informieren Sie sich in diesem Thema unter **Referenz zu Einstellungen des Konfigurationselements für Android und Samsung KNOX** über die Details, und klicken Sie dann auf **Weiter**.  
  
    > [!TIP]  
    >  Ist die gewünschte Einstellung nicht aufgeführt, aktivieren Sie das Kontrollkästchen **Zusätzliche Einstellungen konfigurieren, die in den Standardeinstellungsgruppen nicht enthalten sind**.  
  
9. Konfigurieren Sie auf jeder Einstellungsseite die erforderlichen Einstellungen, und legen Sie fest, ob sie korrigiert werden sollen, wenn sie auf Geräten nicht kompatibel sind (sofern unterstützt).  
  
10. Sie können für jede Einstellungsgruppe auch den Schweregrad konfigurieren, der gemeldet wird, wenn die Inkompatibilität eines Konfigurationselements festgestellt wird. Die Einstellungen lauten wie folgt:  
  
    -   **Keiner**: Von Geräten, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.  
  
    -   **Information**: Von Geräten, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.  
  
    -   **Warnung**: Von Geräten, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.  
  
    -   **Kritisch**: Von Geräten, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.  
  
    -   **Kritisch mit Ereignis**: Von Geräten, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.  
  
11. Überprüfen Sie auf der Seite **Plattformanwendbarkeit** des Assistenten alle Einstellungen, die mit den zuvor ausgewählten unterstützten Plattformen nicht kompatibel sind. Sie können zurückkehren und diese Einstellungen entfernen oder den Vorgang fortsetzen.  
  
    > [!TIP]  
    >  Nicht unterstützte Einstellungen werden nicht auf Kompatibilität überprüft.  
  
12. Schließen Sie den Assistenten ab.  
  
 Sie können das neue Konfigurationselement im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Konfigurationselemente** anzeigen.  
  
##  <a name="android-for-work-configuration-item-settings-reference"></a>Referenz zu den Einstellungen für Android for Work-Konfigurationselemente  
  
### <a name="password"></a>Kennwort  
   
|Einstellung|Details|  
|-------------|-------------|  
|**Kennworteinstellungen auf Geräten erforderlich**|Auf unterstützten Geräten ein Kennwort erfordern.|  
|**Minimale Kennwortlänge (Zeichen)**|Die Mindestlänge für das Kennwort.|  
|**Kennwortablauf in Tagen**|Die Anzahl der Tage, bevor ein Kennwort geändert werden muss.|  
|**Anzahl der gespeicherten Kennwörter**|Verhindert die Wiederverwendung zuvor verwendeter Kennwörter.|  
|**Anzahl der gescheiterten Anmeldeversuche vor dem Zurücksetzen eines Geräts**|Setzt das Gerät zurück, wenn diese Anzahl von Anmeldeversuchen fehlschlägt.|  
|**Leerlaufzeit vor dem Sperren des Geräts**|Legen Sie die Zeitspanne fest, nach der das Gerät bei Nichtverwendung gesperrt wird.|
|**Kennwortqualität**|Wählen Sie den erforderlichen Grad der Kennwortkomplexität aus. Wählen Sie zudem aus, ob biometrische Geräte zulässig sind.|  
|**Zulassen von Smart Lock und anderen Vertrauens-Agents**|Damit können Sie die Smart Lock-Funktion auf kompatiblen Android-Geräten steuern. Diese Telefonfunktion wird manchmal als Vertrauens-Agent bezeichnet und ermöglicht Ihnen das Deaktivieren oder Umgehen des Kennworts für den Gerätesperrbildschirm, wenn sich das Gerät an einem vertrauenswürdigen Standort befindet, z. B. wenn es mit einem bestimmten Bluetooth-Gerät verbunden ist oder sich in der Nähe eines NFC-Tags befindet. Mit dieser Einstellung können Sie verhindern, dass Endbenutzer Smart Lock konfigurieren.|
|**Fingerabdruck zum Entsperren**||
  
###  <a name="work-profile"></a>Arbeitsprofil  
 Diese Einstellungen gelten nur für Samsung KNOX-Geräte.  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Ermöglicht die Datenfreigabe zwischen Arbeits- und persönlichen Profilen**|Wählen Sie aus:<br>- **Nicht konfiguriert**<br>- **Verhindern der Freigabe über Grenzen hinweg**<br>- **Apps im Arbeitsprofil können Anforderung vom persönlichen Profil behandeln**<br>- **Keine Einschränkung für die Freigabe**<br>|  
|**Blenden Sie die Arbeitsprofilbenachrichtigungen aus, wenn das Gerät gesperrt ist (Android 6.0+)**||
|**Festlegen der Standard-App-Berechtigungsrichtlinie (Android 6.0+)**|Wählen Sie aus:<br>- **Nicht konfiguriert**<br>- **Immer bestätigen**<br>- **Automatisch gewähren**<br>- **Automatisch verweigern**|
  
 
## <a name="see-also"></a>Siehe auch  
 [Konfigurationselemente für Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
