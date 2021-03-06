---
title: Ordner „CD.Latest“
titleSuffix: Configuration Manager
description: Enthält Informationen über den neuen Updatevorgang, in dem Updates des Produkts aus der Configuration Manager-Konsole heraus bereitstellt werden.
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35a8e1356306815503f2c153a12139e06dd27be2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="the-cdlatest-folder-for-system-center-configuration-manager"></a>Der Ordner „CD.Latest“ für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager wird ein neuer Updatevorgang eingeführt, der Updates des Produkts aus der Configuration Manager-Konsole heraus bereitstellt. Zur Unterstützung dieser neuen Methode zur Aktualisierung von Configuration Manager wird ein neuer Ordner namens **CD.Latest** erstellt, der eine Kopie der Configuration Manager-Installationsdateien für die aktualisierte Version der Website enthält.  

Der Ordner „CD.Latest“ enthält einen Ordner namens **Redist** , der die verteilbaren Dateien enthält, die während des Setupvorgangs heruntergeladen und verwendet werden. Diese Dateien sind der Version der Configuration Manager-Dateien zugeordnet, die sich im Ordner „CD.Latest“ befinden. Wenn Sie den Setupvorgang aus einem „CD.Latest“-Ordner ausführen, müssen Sie Dateien verwenden, die zu dieser Setup-Version passen. Dazu können sie Setup anweisen, neue und aktuelle Dateien von Microsoft herunterzuladen, oder die Dateien aus dem „Redist“-Ordner verwenden, der sich im „CD.Latest“-Ordner befindet.

Baselinemedien beinhalten genau wie die Baselineversion 1802, die im März 2018 veröffentlicht wurde, keinen „Redist“-Ordner. Der Ordner „Redist“ wird nicht erstellt, bis Sie ein Update in der Konsole installieren. Verwenden Sie in der Zwischenzeit den Redist-Ordner, den Sie auch bei der Installation von Standorten mit dem Baselinemedium verwendet haben.  

> [!TIP]
> Achten Sie darauf, aktuelle verteilbare Dateien zu verwenden. Falls Sie die Dateien noch nicht heruntergeladen haben, weisen Sie das Setupprogramm an, diese von Microsoft herunterzuladen.   

 In den folgenden Szenarien wird der Ordner „CD.Latest“ an einem Standort der zentralen Verwaltung oder auf dem primären Standortserver erstellt oder aktualisiert:  

-   Sie installieren ein Update oder Hotfix aus der Configuration Manager-Konsole heraus: Der Ordner wird im Configuration Manager-Installationsordner erstellt oder aktualisiert.  

-   Sie führen den integrierten Configuration Manager-Sicherungstask aus: Der Ordner wird im angegebenen Sicherungsordner erstellt oder aktualisiert.  

-  Der Ordner „CD.Latest“ wird erstellt, wenn Sie mithilfe des Baselinemediums (z.B. Version 1802) einen neuen Standort installieren.

Die Quelldateien aus dem Ordner „CD.Latest“ werden für Folgendes unterstützt:  

1.  **Sicherung und Wiederherstellung:** Zum Wiederherstellen eines Standorts müssen Sie die Quelldateien aus einem CD.Latest-Ordner verwenden, die zu Ihrem Standort passen. Wenn Sie eine Standortsicherung mithilfe des integrierten Standortsicherungstask ausführen, wird der CD.Latest-Ordner als Teil der Sicherung eingeschlossen.

    -   **Wenn Sie den Standort im Rahmen einer Standortwiederherstellung neu installieren,** wird der Standort aus dem Ordner „CD.Latest“ installiert, der in der Sicherung enthalten ist. Dadurch wird der Standort anhand der Dateiversionen installiert, die der Standortsicherung und der Standortdatenbank entsprechen.  Wenn Sie keinen Zugriff auf die richtige CD.Latest-Ordnerversion haben, können Sie einen CD.Latest-Ordner mit den richtigen Dateiversionen erhalten, indem Sie einen Standort in einer Testumgebung erstellen und diesen Standort dann aktualisieren, sodass er mit der Version, die Sie wiederherstellen möchten, übereinstimmt.

        > [!IMPORTANT]  
        >  Wenn Sie nicht über den richtigen Ordner „CD.Latest“ und dessen Inhalte verfügen, können Sie einen Standort nicht wiederherstellen, und er muss neu installiert werden.  

    -   Wenn Sie keinen Ordner „CD.Latest“ haben, aber einen funktionierenden untergeordneten primären Standort oder Standort der zentralen Verwaltung, können Sie diesen Standort als Referenzstandort für eine Standortwiederherstellung verwenden.  

2.  **So installieren Sie einen untergeordneten primären Standort:** Wenn Sie einen neuen untergeordneten primären Standort unterhalb eines Standorts der zentralen Verwaltung installieren möchten, auf dem ein oder mehrere In-Console-Updates installiert sind, müssen Sie Setup und die Quelldateien des Ordners „CD.Latest“ vom Standort der zentralen Verwaltung verwenden. Wenn Setup von einer Kopie des Ordners „CD.Latest“ vom Standort der zentralen Verwaltung ausgeführt wird, werden Installationsquelldateien verwendet, die mit der Version des Standorts der zentralen Verwaltung übereinstimmen. Weitere Informationen finden Sie unter [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) (Verwenden des Setup-Assistenten zum Installieren von Standorten).  

3.  **So erweitern Sie einen eigenständigen primären Standort:** Wenn Sie einen eigenständigen primären Standort durch Installation eines neuen Standorts der zentralen Verwaltung erweitern, müssen Sie das Setup und die Quelldateien des Ordners „CD.Latest“ vom primären Standort verwenden, um den neuen Standort der zentralen Verwaltung zu installieren. Bei Ausführung von einer Kopie des Ordners „CD.Latest“ vom primären Standort werden Installationsquelldateien verwendet, die der Version des primären Standorts entsprechen. Weitere Informationen finden Sie unter [Expand a stand-alone primary site](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) (Erweitern eines eigenständigen primären Standorts) im Thema [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) (Verwenden des Setup-Assistenten zum Installieren von Standorten).

> [!IMPORTANT]  
>  Die aktualisierten „CD.Latest“-Quelldateien werden nicht unterstützt für:  
>   
>  -   Installieren eines neuen Standorts für eine neue Hierarchie  
>  -   Upgrade eines System Center 2012 Configuration Manager-Standorts auf System Center Configuration Manager
>  -   Installieren des Konfigurations-Manager-Clients
>  -   Installieren der Configuration Manager-Verwaltungskonsole

