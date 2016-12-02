---
title: "Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem | Configuration Manager"
description: "Mit den Tasksequenzen in System Center Configuration Manager kann für ein Betriebssystem automatisch ein Upgrade von Windows 7 oder höher auf Windows 10 durchgeführt werden."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fe70a3bfddcc0638a27eccb04324c4e6e2ace1d4


---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie die Tasksequenzen in System Center Configuration Manager, um für ein Betriebssystem automatisch ein Upgrade von Windows 7 oder höher auf Windows 10 auf einem Zielcomputer durchzuführen. Sie erstellen eine Tasksequenz, die auf das Betriebssystemimage, das Sie auf dem Zielcomputer installieren möchten, und auf alle anderen zu installierenden zusätzlichen Inhalte verweist, z. B. Anwendungen oder Softwareupdates. Die Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem ist Teil des Szenarios [Upgrade von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md).  

##  <a name="a-namebkmkupgradeosa-create-a-task-sequence-to-upgrade-an-operating-system"></a><a name="BKMK_UpgradeOS"></a> Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem  
 Um für das Betriebssystem auf Computern ein Upgrade auf Windows 10 durchzuführen, können Sie eine Tasksequenz erstellen und im Assistenten zum Erstellen von Tasksequenzen die Option zum **Durchführen eines Upgrades für ein Betriebssystem mit einem Upgradepaket** auswählen. Vom Assistenten werden die Schritte zum Durchführen des Upgrades für das Betriebssystem, zum Anwenden von Softwareupdates und zum Installieren von Anwendungen hinzugefügt. Bevor Sie die Tasksequenz erstellen, müssen Folgendes verfügbar sein:  

-   **Erforderlich**  

     - Das [Upgradepaket für das Betriebssystem](../get-started/manage-operating-system-upgrade-packages.md) für Windows 10 muss in der Configuration Manager-Konsole verfügbar sein.  

-   **Erforderlich (sofern verwendet)**  

    -   [Softwareupdates](../../sum/get-started/synchronize-software-updates.md) müssen in der Configuration Manager-Konsole synchronisiert werden.  

    -   [Anwendungen](../../apps/deploy-use/create-applications.md) müssen zur Configuration Manager-Konsole hinzugefügt werden.  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>So erstellen Sie eine Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenz erstellen** , um den Tasksequenzerstellungs-Assistenten zu starten.  

4.  Klicken Sie auf der Seite **Neue Tasksequenz erstellen** auf die Option zum **Durchführen eines Upgrades für ein Betriebssystem mit einem Upgradepaket**, und klicken Sie dann auf **Weiter**.  

5.  Geben Sie auf der Seite **Informationen zur Tasksequenz** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Tasksequenzname**: Geben Sie einen Namen zur Identifikation der Tasksequenz an.  

    -   **Beschreibung**: Geben Sie eine Beschreibung der Aufgabe an, die von der Tasksequenz ausgeführt wird.  

6.  Geben Sie auf der Seite zum **Durchführen eines Upgrades für das Windows-Betriebssystem** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Upgradepaket**: Geben Sie die Upgradepaket, das die Quelldateien für das Upgrade des Betriebssystems enthält. Sie können überprüfen, ob Sie das richtige Paket ausgewählt haben, indem Sie die Informationen im **Eigenschaften** -Bereich betrachten. Weitere Informationen finden Sie unter [Manage operating system upgrade packages (Verwalten von Betriebssystem-Upgradepaketen)](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Editionsindex**: Wenn mehrere Editionsindizes für das Betriebssystem im Paket verfügbar sind, wählen Sie den gewünschten Editionsindex aus. Standardmäßig wird das erste Element ausgewählt.  

    -   **Product key**: Geben Sie den Product Key für das zu installierende Windows-Betriebssystem an. Sie können codierte Volumenlizenzschlüssel und standardmäßige Product Keys angeben. Wenn Sie einen nicht codierten Product Key verwenden, muss jede Gruppe aus 5 Zeichen mit einen Bindestrich (-) getrennt werden. Beispiel: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Wenn das Upgrade für eine Volumenlizenzedition vorgesehen ist, ist der Product Key nicht erforderlich. Sie benötigen nur einen Product Key, wenn das Upgrade für eine Verkaufsversion von Windows vorgesehen ist.  

7.  Geben Sie auf der Seite **Updates einschließen** an, ob erforderliche Softwareupdates, alle Softwareupdates oder keine Softwareupdates installiert werden sollen, und klicken Sie dann auf **Weiter**. Wenn Sie angeben, dass Softwareupdates installiert werden sollen, werden von Configuration Manager nur Softwareupdates installiert, die für Sammlungen bestimmt sind, in denen der Zielcomputer Mitglied ist.  

8.  Geben Sie auf der Seite **Anwendungen installieren** die Anwendungen an, die auf dem Zielcomputer installiert werden sollen, und klicken Sie dann auf **Weiter**. Wenn Sie mehrere Anwendungen angeben, können Sie auch angeben, dass die Tasksequenz fortgesetzt werden soll, wenn bei der Installation einer bestimmten Anwendung ein Fehler auftritt.  

9. Schließen Sie den Assistenten ab.  

## <a name="download-package-content-task-sequence-step"></a>Herunterladen der Paketinhalte – Tasksequenzschritt  
 Der [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)-Schritt kann in den folgenden Szenarios vor dem Schritt **Upgrade für Betriebssystem durchführen** verwendet werden:  

-   Sie verwenden eine einzige Upgradetasksequenz, die sowohl für x86- als auch für x64-Plattformen verwendet werden kann. Um dies zu erreichen, fügen Sie zwei **Paketinhalt herunterladen** -Schritte zur Gruppe **Vorbereitung auf das Upgrade** hinzu, und geben Sie Bedingungen an, um die Clientarchitektur zu ermitteln und nur das entsprechende Betriebssystemupgradepaket herunterzuladen. Konfigurieren Sie jeden **Paketinhalt herunterladen** -Schritt zur Verwendung derselben Variablen, und verwenden Sie die Variable für den Medienpfad im Schritt **Betriebssystem aktualisieren** .  

-   Um dynamisch ein passendes Treiberpaket herunterzuladen, verwenden Sie zwei **Paketinhalt herunterladen** -Schritte mit Bedingungen zum Ermitteln des geeigneten Hardwaretyps für jedes Treiberpaket. Konfigurieren Sie jeden **Paketinhalt herunterladen** -Schritt zur Verwendung derselben Variablen, und verwenden Sie die Variable für den **Bereitgestellter Inhalt** -Wert im Bereich „Treiber“ im Schritt **Betriebssystem aktualisieren** .  

   > [!NOTE]
   > Wenn es mehrere Pakete gibt, fügt Configuration Manager dem Variablennamen ein numerisches Suffix hinzu. Wenn Sie beispielsweise eine Variable %mycontent% als eine benutzerdefinierte Variable angeben, ist dies das Stammverzeichnis, in dem alle referenzierten Inhalte gespeichert werden (dies können mehrere Pakete sein). Wenn Sie in einem Untersequenzschritt auf die Variable verweisen, z. B. „Betriebssystem aktualisieren“, wird sie mit einem numerischen Suffix verwendet. In diesem Beispiel %mycontent01% oder %mycontent02%, wobei die Nummer der Reihenfolge entspricht, in der das Paket in diesem Schritt aufgelistet ist.

## <a name="optional-post-processing-task-sequence-steps"></a>Optionale Nachbearbeitung – Tasksequenzschritte  
 Nachdem Sie die Tasksequenz erstellt haben, können Sie zusätzliche Schritte zum Deinstallieren von Anwendungen mit bekannten Kompatibilitätsproblemen oder Maßnahmen zur Nachbearbeitung hinzufügen, die nach einem Neustart des Computers und der erfolgreichen Durchführung des Upgrades auf Windows 10 ausgeführt werden. Fügen Sie diese zusätzlichen Schritte in der Nachbearbeitungsgruppe der Tasksequenz hinzu.  

> [!NOTE]  
>  Da diese Tasksequenz nicht linear verläuft, gibt es Situationen bei den einzelnen Schritten, die sich auf die Ergebnisse der Tasksequenz auswirken können, je nachdem, ob der Clientcomputer erfolgreich aktualisiert wurde oder ob ein Rollback des Clientcomputers auf die ursprüngliche Betriebssystemversion durchgeführt werden muss.  

## <a name="optional-rollback-task-sequence-steps"></a>Optionales Rollback – Tasksequenzschritte  
 Wenn beim Upgradeprozess nach dem Neustart des Computers ein Fehler auftritt, führt Setup eine Rollback für das Upgrade auf das vorherige Betriebssystem durch und die Tasksequenz wird mit den Schritten in der Rollbackgruppe fortgesetzt. Nach dem Erstellen der Tasksequenz können Sie optionale Schritte zur Rollbackgruppe hinzufügen.  

## <a name="folder-and-files-removed-after-computer-restart"></a>Nach Computerneustart entfernte Ordner und Dateien  
 Wenn die Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem auf Windows 10 und alle anderen Schritte in der Tasksequenz durchgeführt wurden, werden die Nachbearbeitungs- und Rollback-Skripts erst nach dem Neustart des Computers entfernt.  Diese Skriptdateien enthalten keine vertraulichen Informationen.  



<!--HONumber=Nov16_HO1-->


