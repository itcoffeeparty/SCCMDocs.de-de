---
title: "Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI | Configuration Manager"
description: "Erfahren Sie mehr über das Anpassen einer Betriebssystembereitstellungs-Tasksequenz, um eine FAT32-Partition auf die Konvertierung zu UEFI vorzubereiten."
ms.custom: na
ms.date: 11/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 54089ac8aa95154534d010bee8c7e2cbd70d1c7e
ms.openlocfilehash: 30838ed3ad045f781a748f96c874bf543ea05462


---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI
In Configuration Manager Version 1610 können Sie eine Tasksequenz einer Betriebssystembereitstellung nun mit der neuen Variablen „TSUEFIDrive“ so anpassen, dass durch den Schritt **Computer neu starten** auf der Festplatte eine FAT32-Partition für die Konvertierung zu UEFI vorbereitet wird. Das folgende Verfahren stellt ein Beispiel dar, wie Sie Tasksequenzschritte erstellen können, um die Festplatte auf die Konvertierung von BIOS zu UEFI vorzubereiten.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>So bereiten Sie die FAT32-Partition für die Konvertierung zu UEFI vor:
Fügen Sie in einer vorhandenen Tasksequenz zum Installieren eines Betriebssystems eine neue Gruppe mit Schritten zum Konvertieren von BIOS zu UEFI hinzu.

1. Erstellen Sie eine neue Tasksequenzgruppe nach den Schritten zum Erfassen von Dateien und Einstellungen und vor den Schritten zum Installieren des Betriebssystems. Erstellen Sie z.B. eine Gruppe nach der Gruppe **Dateien und Einstellungen erfassen** namens **BIOS zu UEFI**.
2. Fügen Sie auf der Registerkarte **Optionen** der neuen Gruppe eine neue Tasksequenzvariable als Bedingung hinzu, wobei **_SMSTSBootUEFI** **ungleich** **TRUE** ist. Dadurch wird verhindert, dass die Schritte in der Gruppe ausgeführt werden, wenn sich ein Computer bereits im UEFI-Modus befindet.
![Gruppe „BIOS zu UEFI“](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Fügen Sie der neuen Gruppe den Tasksequenzschritt **Computer neu starten** hinzu. Wählen Sie unter **Geben Sie an, was nach dem Neustart ausgeführt werden soll** **The boot image assigned to this task sequence is selected** (Das dieser Tasksequenz zugewiesene Startimage wird ausgewählt) aus, um den Computer in Windows PE zu starten.  
4. Fügen Sie auf der Registerkarte **Optionen** eine Tasksequenzvariable als Bedingung hinzu, wobei **_SMSTSInWinPE ist gleich FALSE**. Dadurch wird verhindert, dass dieser Schritt ausgeführt, wenn sich der Computer bereits in Windows PE befindet.

    ![Schritt „Computer neu starten“](../../core/get-started/media/restart-in-windows-pe.png)
5. Fügen Sie einen Schritt zum Starten des OEM-Tools hinzu, das die Firmware von BIOS in UEFI konvertiert. Dabei handelt es sich normalerweise um einen Tasksequenzschritt **Befehlszeile ausführen** mit einer Befehlszeile zum Starten des OEM-Tools.
6.  Fügen Sie den Tasksequenzschritt „Datenträger formatieren und partitionieren“ hinzu, durch den die Festplatte formatiert und partitioniert wird. Führen Sie im Schritt Folgendes aus:
    1.  Erstellen Sie die FAT32-Partition, die in UEFI konvertiert wird, bevor das Betriebssystem installiert wird. Wählen Sie **GPT** als **Datenträgertyp** aus.
    ![Schritt „Datenträger formatieren und partitionieren“](../../core/get-started/media/format-and-partition-disk.png)
    2.  Wechseln Sie zu den Eigenschaften für die FAT32-Partition. Geben Sie **TSUEFIDrive** in das Feld **Variable** ein. Wenn diese Variable von der Tasksequenz erkannt wird, wird diese sich vor dem Neustart des Computers auf den Übergang zu UEFI vorbereiten.
    ![Partitionseigenschaften](../../core/get-started/media/partition-properties.png)
    3. Erstellen Sie eine NTFS-Partition, die vom Tasksequenzmodul verwendet wird, um dessen Zustand sowie Protokolldateien zu speichern.
6.  Fügen Sie den Tasksequenzschritt **Computer neu starten** hinzu. Wählen Sie unter **Geben Sie an, was nach dem Neustart ausgeführt werden soll** **The boot image assigned to this task sequence is selected** (Das dieser Tasksequenz zugewiesene Startimage wird ausgewählt) aus, um den Computer in Windows PE zu starten.  



<!--HONumber=Dec16_HO3-->


