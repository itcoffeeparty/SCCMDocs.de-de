---
title: Unbeaufsichtigte Wiederherstellung | Microsoft-Dokumentation
description: Stellen Sie Ihre Standorte in System Center Configuration Manager mithilfe eines Skripts wieder her.
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: f7cd9c71287d62c9f5d36e2f032bc2a6065572ae
ms.openlocfilehash: b5a1a1d165a6888bc26e809666d2331ff3c24d68
ms.contentlocale: de-de
ms.lasthandoff: 06/06/2017

---

# <a name="unattended-site-recovery-for-configuration-manager"></a>Unbeaufsichtigte Standortwiederherstellung für Configuration Manager   

*Gilt für: System Center Configuration Manager (Current Branch)*
 Wenn Sie eine [unbeaufsichtigte Wiederherstellung](/sccm/protect/understand/recover-sites#site-recovery-procedures) eines Standorts der zentralen Verwaltung oder eines primären Standorts für Configuration Manager ausführen möchten, können Sie ein Skript für eine unbeaufsichtigte Installation erstellen und das Setup mit der Befehlsoption **/script** ausführen. Mit dem Skript werden die gleichen Informationen bereitgestellt, die andernfalls über den Setup-Assistenten eingegeben werden müssten. Das Skript enthält jedoch keine Standardeinstellungen. Alle Werte müssen für die Setup-Schlüssel angegeben werden, die für den jeweils verwendeten Wiederherstellungstyp gelten.

 Damit Sie die Setup-Befehlszeilenoption /script verwenden können, müssen Sie eine Initialisierungsdatei erstellen und den Namen der Initialisierungsdatei nach der Setup-Befehlszeilenoption /script angeben. Der Name der Datei ist unerheblich. Wichtig ist, dass er die Dateinamenerweiterung **.ini** aufweist. Wenn Sie in der Befehlszeile auf die Setup-Initialisierungsdatei verweisen, müssen Sie den vollständigen Dateipfad angeben. Wenn sich beispielsweise die Initialisierungsdatei mit dem Namen *setup.ini* im Ordner *C:\setup* befindet, muss die Befehlszeile wie folgt lauten:

 **setup /script c:\setup\setup.ini**.

> [!IMPORTANT]  
>  Zum Ausführen von Setup benötigen Sie Administratorrechte. Wenn Sie Setup mit dem unbeaufsichtigten Skript ausführen, starten Sie die Eingabeaufforderung im Kontext eines Administrators mit **Als Administrator ausführen**.

 Das Skript enthält Abschnittsnamen, Schlüsselnamen und Werte. Welche Abschnitts- und Schlüsselnamen erforderlich sind, hängt vom Wiederherstellungstyp ab, für den Sie das Skript erstellen. Die Reihenfolge der Schlüssel in den Abschnitten und die Reihenfolge der Abschnitte in der Datei spielen keine Rolle. Bei Schlüsseln wird die Groß-/Kleinschreibung nicht beachtet. Wenn Sie Werte für Schlüssel angeben, müssen dem Namen des Schlüssels ein Gleichheitszeichen (=) und der Wert für den Schlüssel folgen.

 In den folgenden Abschnitten erfahren Sie, wie Sie ein Skript für die unbeaufsichtigte Standortwiederherstellung erstellen. In den Tabellen werden die verfügbaren Setupskriptschlüssel und die entsprechenden Werte aufgeführt. Außerdem wird angegeben, ob die Schlüssel erforderlich sind und für welchen Installationstyp sie verwendet werden. In der letzten Spalte finden Sie zudem eine kurze Beschreibung der einzelnen Schlüssel.

## <a name="recover-a-central-administration-site-unattended"></a>Unbeaufsichtigtes Wiederherstellen eines Standorts der zentralen Verwaltung
 Konfigurieren Sie mit den folgenden Informationen eine Setup-Skriptdatei zur unbeaufsichtigten Wiederherstellung eines Standorts der zentralen Verwaltung.

 **Identification**

-   **Schlüsselname:** Action

    -   **Erforderlich:** Ja
    -   **Werte:** RecoverCCAR
    -   **Details:** Mit diesem Schlüssel wird ein Standort der zentralen Verwaltung wiederhergestellt.


-   **Schlüsselname:** CDLatest

    -   **Erforderlich:** Ja; nur wenn Sie Medien aus dem Ordner „CD.Latest“ verwenden
    -   **Werte:** 1; bei jedem Wert außer 1 wird davon ausgegangen, dass er nicht „CD.Latest“ verwendet
    -   **Details:** Ihr Skript muss diesen Schlüssel und diesen Wert enthalten, wenn Sie das Setup von einem Medium in dem Ordner „CD.Latest“ ausführen, um einen Standort der primären oder zentralen Verwaltung zu installieren oder diesen wiederherstellen möchten. Dieser Wert informiert das Setup darüber, dass Medien aus „CD.Latest“ verwendet werden.

**RecoveryOptions**   
-   **Schlüsselname:** ServerRecoveryOptions   

    -   **Erforderlich:** Ja
    -   **Werte:** 1, 2 oder 4  
         1 = Wiederherstellung von Standortserver und SQL Server   
         2 = nur Wiederherstellung von Standortserver  
         4 = nur Wiederherstellung von SQL Server
    -   **Details:** Hiermit wird angegeben, ob von Setup der Standortserver, SQL Server oder beides wiederhergestellt wird. Die zugeordneten Schlüssel sind erforderlich, wenn Sie den folgenden Wert für die Einstellung ServerRecoveryOptions festlegen:  
        -   **Wert = 1:** Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.

             Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.

        -   **Wert = 2:** Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.

        -   **Wert = 4** Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **10** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.

-   **Schlüsselname:** DatabaseRecoveryOptions

    -   **Erforderlich:** Vielleicht
    -   **Werte:** 10, 20, 40, 80  
         10 = Wiederherstellen der Standortdatenbank aus einer Sicherung  
         20 = Verwenden einer Standortdatenbank, die mithilfe einer anderen Methode manuell wiederhergestellt wurde   
         40 = Erstellen einer neuen Datenbank für den Standort. Verwenden Sie diese Option, wenn keine Standortdatenbank verfügbar ist. Globale Daten und Standortdaten werden durch die Replikation von anderen Standorten wiederhergestellt.  
         80 = Datenbankwiederherstellung überspringen
    -   **Details:** Über diesen Schlüssel wird angegeben, wie Setup die Standortdatenbank in SQL Server wiederherstellen soll. Dieser Schlüssel ist erforderlich, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **4**konfiguriert wurde.


-   **Schlüsselname:** ReferenceSite  

    -   **Erforderlich:** Vielleicht
    -   **Werte:** &lt;ReferenceSiteFQDN\>
    -   **Details:** Hiermit wird der primäre Referenzstandort angegeben, der vom Standort der zentralen Verwaltung verwendet wird, um globale Daten wiederherzustellen, wenn die Datenbanksicherung älter ist als die Beibehaltungsdauer der Änderungsnachverfolgung, oder wenn Sie den Standort ohne Sicherung wiederherstellen.

         Wenn Sie keinen Referenzstandort angeben und die Sicherung älter als die Beibehaltungsdauer der Änderungsnachverfolgung ist, werden alle primären Standorte mit den wiederhergestellten Daten vom Standort der zentralen Verwaltung neu initialisiert.

         Wenn Sie keinen Referenzstandort angeben und die Sicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung liegt, werden nur Änderungen, die seit der Sicherung vorgenommen wurden, von den primären Standorten repliziert. Wenn Änderungen von verschiedenen primären Standorten vorliegen, die miteinander in Konflikt stehen, dann wird vom Standort der zentralen Verwaltung die zuerst empfangene verwendet.

         Dieser Schlüssel ist erforderlich, wenn für die Einstellung **DatabaseRecoveryOptions** der Wert **40**vorliegt.

-   **Schlüsselname:** SiteServerBackupLocation

    -   **Erforderlich:** Nein
    -   **Werte:** &lt;PathToSiteServerBackupSet\>
    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz des Standortservers angegeben. Dieser Schlüssel ist optional, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **2**konfiguriert wurde. Geben Sie einen Wert für den Schlüssel **SiteServerBackupLocation** an, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.


-   **Schlüsselname:** BackupLocation

    -   **Erforderlich:** Vielleicht
    -   **Werte:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz der Standortdatenbank angegeben. Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **ServerRecoveryOptions** den Wert **1** oder **4** konfigurieren und für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** .


**Optionen**

-   **Schlüsselname:** ProductID
    -   **Erforderlich:** Ja
    -   **Werte:**   
         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
          – Evaluierungsversion
    -   **Details:** Gibt den Product Key für die Configuration Manager-Installation einschließlich der Gedankenstriche an. Geben Sie **Eval** ein, um die Evaluierungsversion von Configuration Manager zu installieren.  


-   **Schlüsselname:** SiteCode

    -   **Erforderlich:** Ja
    -   **Werte:** &lt;Standortcode\>
    -   **Details:** Drei alphanumerische Zeichen, die den Standort in der Hierarchie eindeutig angeben. Sie müssen den Standortcode angeben, der vor dem Auftreten des Fehlers vom Standort verwendet wurde.


-   **Schlüsselname:** SiteName

    -   **Erforderlich:** Ja
    -   **Werte:** Standortname
    -   **Details:** Beschreibung für diesen Standort.


-   **Schlüsselname:** SMSInstallDir

    -   **Erforderlich:** Ja
    -   **Werte:** &lt;*ConfigMgrInstallationPath*>
    -   **Details:** Hiermit wird der Installationsordner für die Configuration Manager-Programmdateien angegeben.
        > [!NOTE]   
        >  Sie können den ursprünglichen oder einen neuen Pfad für die Configuration Manager-Installation angeben.

-   **Schlüsselname:** SDKServer

    -   **Erforderlich:** Ja
    -   **Werte:**&lt;*FQDN des SMS-Anbieters*>
    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird. Sie müssen den Server angeben, von dem der SMS-Anbieter vor Auftreten des Fehlers gehostet wurde.

         Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren.

-   **Schlüsselname:** PrerequisiteComp

    -   **Erforderlich:** Ja
    -   **Werte:** 0 oder 1  
         0 = herunterladen   
         1 = bereits heruntergeladen
    -   **Details:** Hiermit wird angegeben, ob die für Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert 0 angeben, werden die Dateien von Setup heruntergeladen.  


-   **Schlüsselname:** PrerequisitePath

    -   **Erforderlich:** Ja
    -   **Werte:**&lt;*PathToSetupPrerequisiteFiles*>
    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für Setup erforderlichen Dateien angegeben. Je nach dem Wert unter **PrerequisiteComp** wird dieser Pfad von Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.

-   **Schlüsselname:** AdminConsole

    -   **Erforderlich:** Vielleicht
    -   **Werte:** 0 oder 1 0 = Nicht installieren   
         1 = installieren
    -   **Details:** Hiermit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll. Dieser Schlüssel ist erforderlich, außer wenn für die Einstellung **ServerRecoveryOptions** der Wert **4**vorliegt.


-   **Schlüsselname:** JoinCEIP

    -   **Erforderlich:** Ja
    -   **Werte:** 0 oder 1  
         0 = nicht teilnehmen  
         1 = teilnehmen
    -   **Details:** Gibt an, ob am Programm zur Verbesserung der Benutzerfreundlichkeit teilgenommen wird.

**SQLConfigOptions**

-   **Schlüsselname:** SQLServerName

    -   **Erforderlich:** Ja
    -   **Werte:** *&lt;SQLServerName\>*
    -   **Details:** Der Name des Servers oder der gruppierten Instanz mit SQL Server, auf dem bzw. der die Standortdatenbank gehostet werden soll. Sie müssen den Server angeben, von dem die Standortdatenbank vor dem Auftreten des Fehlers gehostet wurde.


-   **Schlüsselname:** DatabaseName

    -   **Erforderlich:** Ja
    -   **Werte:** *&lt;SiteDatabaseName\>* oder *&lt;InstanceName\>*\\*&lt; SiteDatabaseName\>*
    -   **Details:** Gibt den Namen der SQL Server-Datenbank an, die bei der Installation der Datenbank für den Standort der zentralen Verwaltung erstellt oder verwendet werden soll. Sie müssen den gleichen Datenbanknamen angeben, der vor Auftreten des Fehlers verwendet wurde.

        > [!IMPORTANT]  
        >  Sie müssen den Instanznamen und den Namen der Standortdatenbank angeben, falls Sie die Standardinstanz nicht verwenden.

-   **Schlüsselname:** SQLSSBPort

    -   **Erforderlich:** Nein
    -   **Werte:** &lt;*SSBPortNumber*>
    -   **Details:** Gibt den Port des SQL Server-Service Brokers (SSB) an, der von SQL Server verwendet wird. Von SSB wird zwar in der Regel TCP-Port 4022 verwendet, aber es werden auch andere Ports unterstützt. Sie müssen den gleichen SSB-Port angeben, der vor Auftreten des Fehlers verwendet wurde.

## <a name="recover-a-primary-site-unattended"></a>Unbeaufsichtigtes Wiederherstellen eines primären Standorts
 Konfigurieren Sie mit den folgenden Informationen eine Setup-Skriptdatei zur unbeaufsichtigten Wiederherstellung eines Standorts der zentralen Verwaltung.

 **Identification**

-   **Schlüsselname:** Action

    -   **Erforderlich:** Ja
    -   **Werte:** RecoverPrimarySite
    -   **Details:** Mit diesem Schlüssel wird ein primärer Standort wiederhergestellt.


-   **Schlüsselname:** CDLatest

    -   **Erforderlich:** Ja; nur wenn Sie Medien aus dem Ordner „CD.Latest“ verwenden
    -   **Werte:** 1; bei jedem Wert außer 1 wird davon ausgegangen, dass er nicht „CD.Latest“ verwendet
    -   **Details:** Ihr Skript muss diesen Schlüssel und diesen Wert enthalten, wenn Sie das Setup von einem Medium in dem Ordner „CD.Latest“ ausführen, um einen Standort der primären oder zentralen Verwaltung zu installieren oder diesen wiederherstellen möchten. Dieser Wert informiert das Setup darüber, dass Medien aus „CD.Latest“ verwendet werden.

**RecoveryOptions**

-   **Schlüsselname:** ServerRecoveryOptions

    -   **Erforderlich:** Ja
    -   **Werte:** 1, 2 oder 4    
         1 = Wiederherstellung von Standortserver und SQL Server   
         2 = nur Wiederherstellung von Standortserver  
         4 = nur Wiederherstellung von SQL Server
    -   **Details:** Hiermit wird angegeben, ob von Setup der Standortserver, SQL Server oder beides wiederhergestellt wird. Die zugeordneten Schlüssel sind erforderlich, wenn Sie den folgenden Wert für die Einstellung ServerRecoveryOptions festlegen:

        -   **Wert = 1:** Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.

             Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.

        -   **Wert = 2:** Sie können einen Wert für den Schlüssel **SiteServerBackupLocation** angeben, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.

        -   **Wert = 4** Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **10** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.

-   **Schlüsselname:** DatabaseRecoveryOptions

    -   **Erforderlich:** Vielleicht
    -   **Werte:** 10, 20, 40, 80  
         10 = Wiederherstellen der Standortdatenbank aus einer Sicherung  
         20 = Verwenden einer Standortdatenbank, die mithilfe einer anderen Methode manuell wiederhergestellt wurde     
         40 = Erstellen einer neuen Datenbank für den Standort. Verwenden Sie diese Option, wenn keine Standortdatenbank verfügbar ist. Globale Daten und Standortdaten werden durch die Replikation von anderen Standorten wiederhergestellt.  
         80 = Datenbankwiederherstellung überspringen
    -   **Details:** Über diesen Schlüssel wird angegeben, wie Setup die Standortdatenbank in SQL Server wiederherstellen soll. Dieser Schlüssel ist erforderlich, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **4**konfiguriert wurde.


-   **Schlüsselname:** SiteServerBackupLocation

    -   **Erforderlich:** Nein
    -   **Werte:** &lt;PathToSiteServerBackupSet\>
    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz des Standortservers angegeben. Dieser Schlüssel ist optional, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **2**konfiguriert wurde. Geben Sie einen Wert für den Schlüssel **SiteServerBackupLocation** an, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, wird der Standort erneut installiert, ohne ihn aus einem Sicherungssatz wiederherzustellen.     


-   **Schlüsselname:** BackupLocation

    -   **Erforderlich:** Vielleicht
    -   **Werte:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Details:** Hiermit wird der Pfad zum Sicherungssatz der Standortdatenbank angegeben. Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **ServerRecoveryOptions** den Wert **1** oder **4** konfigurieren und für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** .

**Optionen**

-   **Schlüsselname:** ProductID

    -   **Erforderlich:** Ja
    -   **Werte:**     
         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         – Evaluierungsversion     
    -   **Details:** Gibt den Product Key für die Configuration Manager-Installation einschließlich der Gedankenstriche an. Geben Sie **Eval** ein, um die Evaluierungsversion von Configuration Manager zu installieren.  


-   **Schlüsselname:** SiteCode

    -   **Erforderlich:** Ja
    -   **Werte:** &lt;Standortcode\>
    -   **Details:** Drei alphanumerische Zeichen, die den Standort in der Hierarchie eindeutig angeben. Sie müssen den Standortcode angeben, der vor dem Auftreten des Fehlers vom Standort verwendet wurde.


-   **Schlüsselname:** SiteName

    -   **Erforderlich:** Ja
    -   **Werte:** Standortname
    -   **Details:** Beschreibung für diesen Standort.


-   **Schlüsselname:** SMSInstallDir

    -   **Erforderlich:** Ja
    -   **Werte:** &lt;*ConfigMgrInstallationPath*>
    -   **Details:** Hiermit wird der Installationsordner für die Configuration Manager-Programmdateien angegeben.

        > [!NOTE]   
        >  Sie können den ursprünglichen oder einen neuen Pfad für die Configuration Manager-Installation angeben.

-   **Schlüsselname:** SDKServer

    -   **Erforderlich:** Ja
    -   **Werte:**&lt;*FQDN des SMS-Anbieters*>
    -   **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird. Sie müssen den Server angeben, von dem der SMS-Anbieter vor Auftreten des Fehlers gehostet wurde.

         Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren.

-   **Schlüsselname:** PrerequisiteComp

    -   **Erforderlich:** Ja
    -   **Werte:** 0 oder 1    
         0 = herunterladen   
         1 = bereits heruntergeladen   
    -   **Details:** Hiermit wird angegeben, ob die für Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert 0 angeben, werden die Dateien von Setup heruntergeladen.


-   **Schlüsselname:** PrerequisitePath

    -   **Erforderlich:** Ja
    -   **Werte:**&lt;*PathToSetupPrerequisiteFiles*>
    -   **Details:** Über diesen Schlüssel wird der Pfad zu den für Setup erforderlichen Dateien angegeben. Je nach dem Wert unter **PrerequisiteComp** wird dieser Pfad von Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.


-   **Schlüsselname:** AdminConsole

    -   **Erforderlich:** Vielleicht
    -   **Werte:** 0 oder 1  
         0 = nicht installieren   
         1 = installieren  
    -   **Details:** Hiermit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll. Dieser Schlüssel ist erforderlich, außer wenn für die Einstellung **ServerRecoveryOptions** der Wert **4**vorliegt.

-   **Schlüsselname:** JoinCEIP

    -   **Erforderlich:** Ja
    -   **Werte:** 0 oder 1    
         0 = nicht teilnehmen  
         1 = teilnehmen
    -   **Details:** Gibt an, ob am Programm zur Verbesserung der Benutzerfreundlichkeit teilgenommen wird.


**SQLConfigOptions**

-   **Schlüsselname:** SQLServerName

    -   **Erforderlich:** Ja
    -   **Werte:** *&lt;SQLServerName\>*
    -   **Details:** Der Name des Servers oder der gruppierten Instanz mit SQL Server, auf dem bzw. der die Standortdatenbank gehostet werden soll. Sie müssen den Server angeben, von dem die Standortdatenbank vor dem Auftreten des Fehlers gehostet wurde.


-   **Schlüsselname:** DatabaseName

    -   **Erforderlich:** Ja
    -   **Werte:** *&lt;SiteDatabaseName\>* oder *&lt;InstanceName\>*\\*&lt; SiteDatabaseName\>*
    -   **Details:** Gibt den Namen der SQL Server-Datenbank an, die bei der Installation der Datenbank für den Standort der zentralen Verwaltung erstellt oder verwendet werden soll. Sie müssen den gleichen Datenbanknamen angeben, der vor Auftreten des Fehlers verwendet wurde.

        > [!IMPORTANT]    
        >  Sie müssen den Instanznamen und den Namen der Standortdatenbank angeben, falls Sie die Standardinstanz nicht verwenden.

-   **Schlüsselname:** SQLSSBPort

    -   **Erforderlich:** Nein
    -   **Werte:** &lt;*SSBPortNumber*>
    -   **Details:** Gibt den Port des SQL Server-Service Brokers (SSB) an, der von SQL Server verwendet wird. Von SSB wird zwar in der Regel TCP-Port 4022 verwendet, aber es werden auch andere Ports unterstützt. Sie müssen den gleichen SSB-Port angeben, der vor Auftreten des Fehlers verwendet wurde.

**Hierarchie-ExpansionOption**

-   **Schlüsselname:** CCARSiteServer

    -   **Erforderlich:** Vielleicht
    -   **Werte:** &lt;*SiteCodeForCentralAdministrationSite*>
    -   **Details:** Über diesen Schlüssel wird der Standort der zentralen Verwaltung angegeben, dem ein primärer Standort beim Hinzufügen zur Configuration Manager-Hierarchie zugeordnet wird. Diese Einstellung ist erforderlich, wenn der primäre Standort vor dem Fehler mit einem zentralen Verwaltungsstandort verbunden war. Sie müssen den Standortcode angeben, der vor dem Auftreten des Fehlers vom zentralen Verwaltungsstandort verwendet wurde.

-   **Schlüsselname:** CASRetryInterval

    -   **Erforderlich:** Nein
    -   **Werte:** &lt;*Intervall*>
    -   **Details:** Über diesen Schlüssel wird das Wiederholungsintervall angegeben (in Minuten), wenn beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler aufgetreten ist. Wenn beispielsweise beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler auftritt, wird der Verbindungsversuch auf dem primären Standort nach der für CASRetryInterval angegebenen Anzahl von Minuten wiederholt.


-   **Schlüsselname:** WaitForCASTimeout

    -   **Erforderlich:** Nein
    -   **Werte:** &lt;*Timeout*>
    -   **Details:** Über diesen Schlüssel wird der maximale Timeoutwert (in Minuten) für die Verbindung eines primären Standorts mit dem Standort der zentralen Verwaltung angegeben. Wenn beispielsweise beim Herstellen der Verbindung mit dem Standort der zentralen Verwaltung ein Fehler auftritt, wird der Verbindungsversuch auf dem primären Standort basierend auf dem Wert für CASRetryInterval solange wiederholt, bis der für WaitForCASTimeout angegebene Zeitraum abgelaufen ist. Sie können einen Wert von 0 bis 100 angeben.

