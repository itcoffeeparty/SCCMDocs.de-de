---
title: "Erstellen von Konfigurationselementen für Windows 10-Geräte, die mit dem System Center Configuration Manager-Client verwaltet werden | System Center Configuration Manager"
description: "Verwenden Sie das System Center Configuration Manager-Konfigurationselement für Windows 10, um Einstellungen für Windows 10-Geräte zu verwalten, die mit dem Configuration Manager-Client verwaltet werden"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d5248e7262f758c2de2a1deaf42282d4e77e3e0c


---
# <a name="create-configuration-items-for-windows-10-devices-managed-with-the-system-center-configuration-manager-client"></a>Erstellen von Konfigurationselementen für Windows 10-Geräte, die mit dem System Center Configuration Manager-Client verwaltet werden

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie das System Center Configuration Manager-Konfigurationselement für **Windows 10**, um Einstellungen für Windows 10-Geräte zu verwalten, die mit dem Configuration Manager-Client verwaltet werden.  

> [!IMPORTANT]  
>  Wenn Sie in diesem Release eine **Kennwort**-Einstellung als Teil eines Konfigurationselements vom Typ **Windows 10** erstellt haben (für ein durch den Configuration Manager-Client verwaltetes Gerät), dann wird die Einstellung fälschlicherweise auch als kompatibel ausgewertet, wenn sie noch nicht vorhanden ist oder auf dem Windows 10-Gerät nicht konfiguriert wurde.  
>   
>  Um das Problem beim Erstellen einer Einstellung für diese Geräte zu umgehen, stellen sicher, dass auf den Einstellungsseiten des Assistenten zum Erstellen von Konfigurationselementen **Nicht kompatible Einstellungen wiederherstellen** ausgewählt ist. Wenn Sie darüber hinaus eine Konfigurationsbasislinie mit einem Windows 10-Konfigurationselement bereitstellen, das Kennworteinstellungen enthält, wählen Sie im Dialogfeld "Konfigurationsbasislinien bereitstellen" die Option **Nicht kompatible Regeln wiederherstellen, falls dies unterstützt wird** aus. Bei dieser Problemumgehung wird die Einstellung überwacht und korrigiert, falls sie nicht kompatibel ist. Nach der Wiederherstellung wird die Einstellung ordnungsgemäß als **Kompatibel** angegeben (es sei denn, aufgrund eines Problems wird ein **Fehler**festgestellt).  

## <a name="create-a-windows-10-configuration-item"></a>Erstellen eines Windows 10-Konfigurationselements  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationselemente**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen**einen Namen und optional eine Beschreibung für das Konfigurationselement an.  

5.  Wählen Sie unter **Typ des zu erstellenden Konfigurationselements angeben**den Typ **Windows 10**aus.  

6.  Klicken Sie auf **Kategorien**, wenn Sie Kategorien erstellen und zuweisen, um das Durchsuchen und Filtern von Konfigurationselementen in der Configuration Manager-Konsole zu erleichtern.  

7.  Wählen Sie auf der Seite **Unterstützte Plattformen** die jeweiligen Windows 10-Plattformen zur Bewertung des Konfigurationselements aus.  

8.  Wählen Sie auf der Seite **Geräteeinstellungen** die Einstellungsgruppe aus, die Sie konfigurieren möchten. Informieren Sie sich in diesem Thema unter [Einstellungen für Windows 10-Konfigurationselemente](/sccm/compliance/deploy-use/create-configuration-items-for-windows-10-devices-managed-with-the-client#windows-10-configuration-item-settings-reference) über die Details, und klicken Sie dann auf **Weiter**.  

    > [!TIP]  
    >  Ist die gewünschte Einstellung nicht aufgeführt, aktivieren Sie das Kontrollkästchen **Zusätzliche Einstellungen konfigurieren, die in den Standardeinstellungsgruppen nicht enthalten sind**.  

9. Konfigurieren Sie auf jeder Einstellungsseite die erforderlichen Einstellungen, und legen Sie fest, ob sie korrigiert werden sollen, wenn sie auf Geräten nicht kompatibel sind (sofern unterstützt).  

10. Sie können für jede Einstellungsgruppe auch den Schweregrad konfigurieren, der (in Configuration Manager-Berichten) gemeldet wird, wenn die Inkompatibilität eines Konfigurationselements festgestellt wird:  

    -   **Keine** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad gemeldet.  

    -   **Information** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** gemeldet.  

    -   **Warnung** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** gemeldet.  

    -   **Kritisch** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** gemeldet.  

    -   **Kritisch mit Ereignis** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.  

11. Überprüfen Sie auf der Seite **Plattformanwendbarkeit** alle Einstellungen, die mit den zuvor ausgewählten unterstützten Plattformen nicht kompatibel sind. Sie können zurückkehren und diese Einstellungen entfernen oder den Vorgang fortsetzen.  

    > [!TIP]  
    >  Nicht unterstützte Einstellungen werden nicht auf Kompatibilität überprüft.  

12. Schließen Sie den Assistenten ab.  

 Sie können das neue Konfigurationselement im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Konfigurationselemente** anzeigen.  

##  <a name="windows-10-configuration-item-settings-reference"></a>Referenz zu Einstellungen des Konfigurationselements für Windows 10  

### <a name="password"></a>Kennwort  

|Einstellung|Details|  
|-------------|-------------|  
|**Kennworteinstellungen auf Geräten erforderlich**|Auf unterstützten Geräten ein Kennwort erfordern.|  
|**Minimale Kennwortlänge (Zeichen)**|Die Mindestlänge für das Kennwort in Zeichen.|  
|**Kennwortablauf in Tagen**|Die Anzahl der Tage, bevor ein Kennwort geändert werden muss.|  
|**Anzahl der gespeicherten Kennwörter**|Verhindert die Wiederverwendung vorheriger Kennwörter.|  
|**Anzahl der gescheiterten Anmeldeversuche vor dem Zurücksetzen eines Geräts**|Setzt das Gerät zurück, wenn die angegebene Anzahl fehlgeschlagener Anmeldeversuche erreicht ist.|  
|**Leerlaufzeit vor dem Sperren des mobilen Geräts**|Gibt an, wie viele Minuten das Gerät inaktiv sein muss, bevor es automatisch gesperrt wird.|  
|**Kennwortkomplexität**|Wählen Sie aus, ob Sie eine PIN wie „1234“ angeben können oder, ob ein sicheres Kennwort erforderlich ist.|  

###  <a name="device"></a>Gerät  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Bluetooth**|Ermöglicht die Verwendung des Bluetooth-Features auf dem Gerät.|  

### <a name="cloud"></a>Cloud  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Synchronisierung der Einstellungen**|Ermöglicht die Synchronisierung von Einstellungen zwischen Geräten.|  
|**Synchronisierung der Anmeldeinformationen**|Ermöglicht die Synchronisierung von Anmeldeinformationen zwischen Geräten.|  
|**Synchronisierung von Einstellungen über getaktete Verbindungen**|Ermöglicht die Synchronisierung von Einstellungen, wenn die Internetverbindung getaktet ist.|  

### <a name="roaming"></a>Roaming  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Datenroaming**|Ermöglicht beim Zugriff auf Daten das Roaming zwischen Netzwerken.|  

### <a name="encryption"></a>Verschlüsselung  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Dateiverschlüsselung auf Gerät**|Erfordert die Verschlüsselung der Dateien auf dem Gerät.|  

### <a name="system-security"></a>Systemsicherheit  

|Name der Einstellung|Details|  
|------------------|-------------|  
|**Benutzerkontensteuerung**|Konfiguriert die Funktionsweise der Windows-Benutzerkontensteuerung auf dem Gerät.<br />Sie können sie z. B. deaktivieren oder die Stufe festlegen, bei der Sie benachrichtigt werden.|  
|**Netzwerkfirewall**|Aktiviert oder deaktiviert die Windows-Firewall.|  
|**SmartScreen**|Aktivieren oder deaktivieren von Windows SmartScreen.|  
|**Virenschutz**|Erfordert, dass Antivirensoftware installiert und konfiguriert ist.|  
|**Virenschutzsignaturen sind aktuell**|Erfordert, dass die Signaturdateien für die Antivirensoftware auf dem Gerät auf dem aktuellen Stand sind|  

### <a name="windows-information-protection-formerly-enterprise-data-protection"></a>Windows Information Protection (zuvor als Unternehmensdatenschutz bezeichnet)

Mit dem Anstieg von Geräten im Besitz der Mitarbeiter im Unternehmen entsteht auch ein höheres Risiko unbeabsichtigter Datenpreisgabe durch Apps und Dienste, z.B. E-Mail, soziale Medien und die öffentliche Cloud, die sich außerhalb der Kontrolle des Unternehmens befinden. Wenn ein Mitarbeiter beispielsweise die aktuellsten technischen Zeichnungen von seinem privaten E-Mail-Konto versendet, Produktinformationen kopiert und in einen Tweet einfügt oder einen Verkaufsbericht, der sich in Bearbeitung befindet, im öffentlichen Cloudspeicher speichert.

Windows Information Protection (WIP) bietet hierbei einen Schutz gegen potenzielle Datenlecks, ohne dass die Benutzerfreundlichkeit für die Mitarbeiter darunter leidet. WIP schützt auch Unternehmens-Apps und -daten vor unbeabsichtigter Datenpreisgabe auf unternehmenseigenen und privaten Geräten, die Mitarbeiter mit zur Arbeit bringen, ohne dass Änderungen in Ihrer Umgebung oder anderen Apps nötig sind.

 Configuration Manager WIP-Konfigurationselemente verwalten die Liste der von WIP geschützten Apps, Unternehmens-Netzwerkadressen, Schutzebenen und Verschlüsselungseinstellungen.

Weitere Informationen zum Konfigurieren von WIP mit Configuration Manager finden Sie unter [Schützen von Unternehmensdaten mit Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).



<!--HONumber=Nov16_HO1-->

