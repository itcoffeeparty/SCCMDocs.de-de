---
title: "Der Ordner „CD.Latest“ | Microsoft-Dokumentation"
description: "Enthält Informationen über den neuen Updatevorgang, in dem Updates des Produkts aus der Configuration Manager-Konsole heraus bereitstellt werden."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: dcf56f6b82f89e81d636ea920f36133e245cbb1e


---
# <a name="the-cdlatest-folder-for-system-center-configuration-manager"></a>Der Ordner „CD.Latest“ für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager wird ein neuer Updatevorgang eingeführt, der Updates des Produkts aus der Configuration Manager-Konsole heraus bereitstellt. Zur Unterstützung dieser neuen Methode zur Aktualisierung von Configuration Manager wird ein neuer Ordner namens **CD.Latest** erstellt, der eine Kopie der Configuration Manager-Installationsdateien für die aktualisierte Version der Website enthält.  

Ab dem Update 1606 enthält der Ordner „CD.Latest“ einen Ordner namens **Redist** , der die verteilbaren Dateien enthält, die während des Setupvorgangs heruntergeladen und verwendet werden. Diese Dateien sind der Version der Configuration Manager-Dateien zugeordnet, die sich im Ordner „CD.Latest“ befinden. Wenn Sie den Setupvorgang aus einem „CD.Latest“-Ordner ausführen, müssen Sie Dateien verwenden, die zu dieser Setup-Version passen. Dazu können sie Setup anweisen, neue und aktuelle Dateien von Microsoft herunterzuladen, oder die Dateien aus dem „Redist“-Ordner verwenden, der sich im „CD.Latest“-Ordner befindet.

Baselinemedien beinhalten genau wie die Baselineversion 1606, die im Oktober 2016 herausgegeben wurde, keinen Redist-Ordner. Der Ordner „Redist“ wird nicht erstellt, bis Sie ein Update in der Konsole installieren. Verwenden Sie in der Zwischenzeit den Redist-Ordner, den Sie auch bei der Installation von Standorten mit dem Baselinemedium verwendet haben.  

> [!TIP]
> Wenn Sie Version 1606 noch nicht installiert haben, stellen Sie sicher, dass die von Ihnen verwendeten „Redist“-Dateien aktuell sind. Falls Sie die „Redist“-Dateien noch nicht heruntergeladen haben, weisen Sie das Setup an, diese von Microsoft herunterzuladen.   

 In den folgenden Szenarien wird der Ordner „CD.Latest“ an einem Standort der zentralen Verwaltung oder auf dem primären Standortserver erstellt oder aktualisiert:  

-   Sie installieren ein Update oder Hotfix aus der Configuration Manager-Konsole heraus: Der Ordner wird im Configuration Manager-Installationsordner erstellt oder aktualisiert.  

-   Sie führen den integrierten Configuration Manager-Sicherungstask aus: Der Ordner wird im angegebenen Sicherungsordner erstellt oder aktualisiert.  

Die Quelldateien aus dem Ordner „CD.Latest“ werden für Folgendes unterstützt:  

1.  **Sicherung und Wiederherstellung:** Der Ordner „CD.Latest“ enthält Quelldateien, die Sie verwenden, um Ihren Standort als Teil einer Standortwiederherstellung neu zu installieren. Zur Wiederherstellung eines Configuration Manager-Standorts muss Ihre Standortsicherung den Ordner „CD.Latest“ enthalten (der integrierte Standortsicherungstask enthält automatisch diesen Ordner als Teil der Standortsicherung).  

    -   **Wenn Sie den Standort im Rahmen einer Standortwiederherstellung neu installieren,** wird der Standort aus dem Ordner „CD.Latest“ installiert, der in der Sicherung enthalten ist. Dadurch wird der Standort anhand der Dateiversionen installiert, die der Standortsicherung und der Standortdatenbank entsprechen.  

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



<!--HONumber=Dec16_HO3-->


