---
title: Installieren mittels Befehlszeile | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie das System Center Configuration Manager-Setup über eine Eingabeaufforderung für eine Vielzahl von Standortinstallationen ausführen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: a148fd1fd438efc01418c30b059874cfdfa09725

---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>Verwenden einer Befehlszeile zum Installieren von System Center Configuration Manager-Standorten

*Gilt für: System Center Configuration Manager (Current Branch)*

 Wenn Sie möchten, können Sie das Setup des System Center Configuration Managers über eine Eingabeaufforderung für eine Vielzahl von Standortinstallationen ausführen.

 ## <a name="supported-tasks-for-command-line-installs"></a>Unterstützte Tasks für Befehlszeileninstallationen
 Diese Methode zum Ausführen des Setups unterstützt die folgenden Standortinstallations- und Standortwartungstasks:

-   **Installieren Sie einen Standort der zentralen Verwaltung oder einen primären Standort über eine Befehlszeile:**  
  Anzeigen von [Befehlszeilenoptionen für Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

 -  **Ändern Sie die an einem Standort der zentralen Verwaltung oder einem primären Standort verwendeten Sprachen:**  
    Um die an einem Standort installierten Sprachen über die Befehlszeile zu ändern (einschließlich Sprachen für Mobilgeräte), verfahren Sie wie folgt:  

     -   Führen Sie das Setup im Ordner **&lt;ConfigMgr-Installationspfad\>\Bin\X64** auf dem Standortserver aus.
     -   Verwenden Sie die Befehlszeilenoption **/MANAGELANGS** .
     -   Geben Sie eine Sprachskriptdatei an, die die Sprachen bestimmt, die Sie hinzufügen oder entfernen möchten.  

    Verwenden Sie z.B. die folgende Befehlssyntax: **setupwpf.exe /MANAGELANGS &lt;Sprachskriptdatei\>**  

    Um die Sprachskriptdatei zu erstellen, verwenden Sie die Informationen unter [Befehlszeilenoptionen zum Verwalten von Sprachen](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang).  

 -  **Verwenden Sie eine Skriptdatei für die unbeaufsichtigte Installation oder Wiederherstellung von Standorten:**  
    Sie können Setup über eine Befehlszeile ausführen und anweisen, ein Installationsskript zu verwenden, um eine unbeaufsichtigte Standortinstallation auszuführen. Sie können diese Option auch zur Wiederherstellung eines Standorts verwenden.    

    So verwenden Sie ein Skript mit Setup:  

    -   Führen Sie das Setup mit der Befehlszeilenoption **/SCRIPT** aus, und geben Sie eine Skriptdatei an.  

    -   Die Skriptdatei muss mit den erforderlichen Schlüsseln und Werten konfiguriert werden.  

    Für eine unbeaufsichtigte Installation eines Standorts der zentralen Verwaltung oder eines primären Standorts muss die Skriptdatei mit den folgenden Abschnitten konfiguriert werden:  

    -   Identification    
    -   Optionen    
    -   SQLConfigOptions    
    -   HierarchyOptions    

    -   CloudConnectorOptions  

    Zum Wiederherstellen eines Standorts müssen Sie die folgenden Abschnitte der Skriptdatei verwenden:  

    -   Identification  

    -   Wiederherstellung

     Weitere Informationen zur Sicherung und Wiederherstellung finden Sie im Abschnitt „Skriptdateischlüssel für unbeaufsichtigte Standortwiederherstellung“ im Thema „Sicherung und Wiederherstellung in Configuration Manager“.  

    [Skriptdateischlüssel für die unbeaufsichtigte Installation](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended) zeigt eine Liste von Schlüsseln und Werten an, die in einer unbeaufsichtigten Installationsskriptdatei verwendet werden sollen.  

## <a name="about-the-command-line-script-file"></a>Informationen zur Befehlszeilen-Skriptdatei  

 Für unbeaufsichtigte Installationen von Configuration Manager können Sie Setup mit der Befehlszeilenoption **/SCRIPT** ausführen und eine Skriptdatei angeben, die Installationsoptionen enthält. Die folgenden Aufgaben werden von dieser Methode unterstützt:  

-   Installieren eines Standorts der zentralen Verwaltung  

-   Installieren eines primären Standorts  

-   Installieren einer Configuration Manager-Konsole  

-   Wiederherstellen eines Standorts  

> [!NOTE]  
>  Sie können die Skriptdatei für die unbeaufsichtigte Installation nicht verwenden, um ein Upgrade einer Evaluierungsversion auf eine lizenzierte Version von Configuration Manager auszuführen.  

**So erstellen Sie das Skript**:  
Das Installationsskript wird automatisch erstellt, wenn Sie das [Setup ausführen, um einen Standort über die Benutzeroberfläche](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) zu installieren.  Wenn Sie die Einstellungen auf der Seite **Zusammenfassung** des Assistenten bestätigen, geschieht Folgendes:  

-   Setup erstellt das Skript **%TEMP%\ConfigMgrAutoSave.ini**.  Sie können diese Datei vor dem Verwenden umbenennen, müssen aber die Dateierweiterung „.ini“ beibehalten.  

-   Das Skript für die unbeaufsichtigte Installation enthält die Einstellungen, die Sie im Assistenten ausgewählt haben.  

-   Nach der Erstellung des Skripts können Sie es ändern, um andere Standorte in Ihrer Hierarchie zu installieren.  

-   Anschließend können Sie das Skript verwenden, um eine unbeaufsichtigte Installation von Configuration Manager durchzuführen.  

Mit der Skriptdatei werden die gleichen Informationen bereitgestellt, die vom Setup-Assistenten angefordert werden. Das Skript enthält jedoch keine Standardeinstellungen.   
Alle Werte müssen für die Setup-Schlüssel angegeben werden, die für den jeweils verwendeten Installationstyp gelten.  

Bei der Erstellung des Skripts für die unbeaufsichtigte Installation durch Setup wird dort der Wert für den Product Key eingetragen, den Sie während des Setups eingegeben haben. Dies kann ein gültiger Product Key oder der Wert EVAL sein, wenn Sie eine Evaluierungsversion von Configuration Manager installieren. Der Product Key-Wert im Skript wird eingetragen, damit die Voraussetzungsprüfung abgeschlossen werden kann.  

Wenn von Setup die Installation des tatsächlichen Standorts gestartet wird, wird erneut in das automatisch erstellte Skript geschrieben, um den Product Key-Wert im erstellten Skript zu löschen. Bevor Sie das Skript für die unbeaufsichtigte Installation eines neuen Standorts verwenden, können Sie es bearbeiten und einen gültigen Product Key eingeben oder eine Evaluierungsinstallation von Configuration Manager angeben.  

**Das Skript enthält Abschnittsnamen, Schlüsselnamen und Werte:**  

-   Welche Abschnitts- und Schlüsselnamen erforderlich sind, hängt von der Installationsart ab, für die Sie das Skript erstellen.  

-   Die Reihenfolge der Schlüssel in den Abschnitten und die Reihenfolge der Abschnitte in der Datei spielen keine Rolle.  

-   Bei Schlüsseln wird die Groß-/Kleinschreibung nicht beachtet.  

-   Wenn Sie Werte für Schlüssel angeben, müssen dem Namen des Schlüssels ein Gleichheitszeichen (=) und der Wert des Schlüssels folgen.  

> [!TIP]  
>  Eine vollständige Übersicht über die Optionen finden Sie unter [Befehlszeilenoptionen für Setup und Skripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="to-use-the-script-setup-command-line-option"></a>So verwenden Sie die Setup-Befehlszeilenoption /SCRIPT:

-   Sie müssen eine Setupskriptdatei verwenden und den Namen der Datei nach der Setup-Befehlszeilenoption **/SCRIPT** angeben.  

    -   Der Name der Datei muss die Dateinamenerweiterung **.ini** aufweisen.  

    -   Wenn Sie an der Eingabeaufforderung auf die Setupskriptdatei verweisen, muss der vollständige Dateipfad angegeben werden. Wenn die Setup-Initialisierungsdatei beispielsweise „Setup.ini“ heißt und sich im Ordner „C:\Setup“ befindet, geben Sie an der Eingabeaufforderung Folgendes ein:  **setup /script c:\setup\setup.ini**  

-   Das Konto für die Ausführung von Setup benötigt Administratorrechte auf dem Computer. Wenn Sie Setup mit dem Skript für die unbeaufsichtigte Installation ausführen, starten Sie die Eingabeaufforderung mit **Run as administrator**.  



<!--HONumber=Dec16_HO3-->


