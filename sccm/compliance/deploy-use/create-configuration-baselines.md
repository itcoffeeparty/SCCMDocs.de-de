---
title: Erstellen von Konfigurationsbaselines
titleSuffix: Configuration Manager
description: Erstellen Sie in System Center Configuration Manager Konfigurationsbaselines, die Sie in einer Sammlung bereitstellen können.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1a6d09e4a5552770a71dc44f473cebd13ba0715c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-configuration-baselines-in-system-center-configuration-manager"></a>Erstellen von Konfigurationsbaselines in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Konfigurationsbaselines in System Center Configuration Manager enthalten vordefinierte Konfigurationselemente und gegebenenfalls andere Konfigurationsbaselines. Nachdem eine Konfigurationsbasislinie erstellt wurde, können Sie sie für eine Sammlung bereitstellen. Auf diese Weise wird die Konfigurationsbasislinie von Geräten in dieser Sammlung heruntergeladen und deren Konformität mit der Konfigurationsbasislinie ausgewertet.  

 Konfigurationsbaselines können in Configuration Manager bestimmte Revisionen von Konfigurationselementen enthalten, oder sie können so konfiguriert werden, dass sie immer die neueste Version eines Konfigurationselements verwenden. Weitere Informationen zu Konfigurationselementrevisionen finden Sie unter [Verwaltungstasks für Konfigurationsdaten](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

 Es gibt zwei Methoden, mit denen Sie Konfigurationsbaselines erstellen können:  

-   Importieren Sie Konfigurationsdaten aus einer Datei. Klicken Sie zum Starten des **Assistenten zum Importieren von Konfigurationsdaten**im Arbeitsbereich **Bestand und Kompatibilität** auf den Knoten **Konfigurationselemente** oder **Konfigurationsbasislinien** , und klicken Sie dann auf **Konfigurationsdaten importieren**.  

-   Verwenden Sie zum Erstellen einer neuen Konfigurationsbasislinie das Dialogfeld **Konfigurationsbasislinie erstellen** .  

 Gehen Sie wie folgt vor, um eine Konfigurationsbasislinie mithilfe des Dialogfelds **Konfigurationsbasislinie erstellen** zu erstellen.  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Assets und Konformität** > **Konformitätseinstellungen** > **Konfigurationsbaselines**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationsbaseline erstellen**.  

4.  Geben Sie im Dialogfeld **Konfigurationsbasislinie erstellen** einen eindeutigen Namen und eine Beschreibung für die Konfigurationsbasislinie ein. Sie können für den Namen maximal 255 Zeichen verwenden, für die Beschreibung sind maximal 512 Zeichen zulässig.  

5.  In der Liste **Konfigurationsdaten** werden alle Konfigurationselemente oder Konfigurationsbasislinien angezeigt, die in dieser Konfigurationsbasislinie enthalten sind. Klicken Sie auf **Hinzufügen** , um der Liste ein neues Konfigurationselement oder eine neue Konfigurationsbasislinie hinzuzufügen. Folgende Optionen stehen Ihnen zur Auswahl:  

    -   **Bestand und Kompatibilität**  

    -   **Softwareupdates**  

    -   **Konfigurationselemente**  
      > [!IMPORTANT]
      > Sie müssen jede Konfigurationsbaseline auf nicht mehr als 1.000 Softwareupdates begrenzen.
6.  Verwenden Sie zum Angeben des Verhaltens eines Konfigurationselements, das Sie in der Liste **Konfigurationsdaten** angegeben haben, die Liste **Zweck ändern** . Folgende Optionen stehen Ihnen zur Auswahl:  

    -   **Erforderlich** Die Konfigurationsbasislinie wird als nicht kompatibel ausgewertet, wenn das Konfigurationselement nicht auf einem Clientgerät erkannt wird. Wenn es erkannt wird, wird es als kompatibel ausgewertet.  

    -   **Optional** Das Konfigurationselement wird nur auf Kompatibilität ausgewertet, wenn die Anwendung, auf die es verweist, auf Clientcomputern gefunden wird. Wird die Anwendung nicht gefunden, wird die Konfigurationsbasislinie nicht als nicht kompatibel markiert (gilt nur für Anwendungskonfigurationselemente).  

    -   **Nicht zugelassen** Die Konfigurationsbasislinie wird als nicht kompatibel ausgewertet, wenn das Konfigurationselement auf Clientcomputern erkannt wird (gilt nur für Anwendungskonfigurationselemente).  

    > [!NOTE]
    >  Die Liste **Zweck ändern** ist nur verfügbar, wenn Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen** auf die Option **Dieses Konfigurationselement enthält Anwendungseinstellungen**geklickt haben.  

7.  Verwenden Sie die Liste **Revision ändern** , um eine bestimmte oder die aktuelle Revision des Konfigurationselements für die Auswertung der Kompatibilität auf Clientgeräten auszuwählen, oder wählen Sie **Immer aktuelle verwenden** aus, damit immer die aktuelle Revision verwendet wird. Weitere Informationen zu Konfigurationselementrevisionen finden Sie unter [Verwaltungstasks für Konfigurationsdaten](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

8.  Wählen Sie zum Entfernen eines Konfigurationselements aus der Konfigurationsbaseline ein Konfigurationselement aus, und klicken Sie auf **Entfernen**.  

9. Klicken Sie auf **OK** , um das Dialogfeld **Konfigurationsbasislinie erstellen** zu schließen und die Konfigurationsbasislinie zu erstellen.  
