---
title: "Voraussetzungen für Standorte | System Center Configuration Manager"
description: "Erfahren Sie mehr zu den verschiedenen Voraussetzungen für die Installation der verschiedenen Arten von System Center Configuration Manager-Standorten."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bf3b1e4d87a972f530590bf94e38a5ec66c4fc9a

---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>Voraussetzungen für die Installation von System Center Configuration Manager-Standorten

*Gilt für: System Center Configuration Manager (Current Branch)*


Die folgenden Abschnitte enthalten Informationen zu den verschiedenen Voraussetzungen für die Installation der verschiedenen Arten von System Center Configuration Manager-Standorten.



## <a name="primary-sites-and-the-central-administration-site"></a>Primäre Standorte und Standort der zentralen Verwaltung
Die folgenden Voraussetzungen gelten für die Installation eines Standorts der zentralen Verwaltung als ersten Standort in einer Hierarchie, eines eigenständigen primären oder untergeordneten primären Standorts. Wenn Sie einen Standort der zentralen Verwaltung im Rahmen einer Hierarchieerweiterung installieren, lesen Sie den Abschnitt [Erweitern eines eigenständigen primären Standorts](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand
) in diesem Thema.

####  <a name="a-namebkmkprereqpria-prerequisites-to-install-a-primary-site-or-central-administration-site"></a><a name="bkmk_PrereqPri"></a> Voraussetzungen für die Installation eines primären Standorts oder eines Standorts der zentralen Verwaltung  

-   Der Benutzer, der den Standort installiert, benötigt die folgenden Berechtigungen:  

    -   **Lokaler Administrator** auf dem Standortservercomputer  

    -   **Lokaler Administrator** auf allen Computern, auf denen die **Standortdatenbank** oder eine Instanz des **SMS-Anbieters** des Standorts gehostet wird  

    -   **Sysadmin** für die SQL Server-Instanz, die die Standortdatenbank hostet  

        > [!IMPORTANT]  
        >  Nach Abschluss der Installation müssen sowohl das Benutzerkonto, das Setup ausführt, als auch das Standortserver-Computerkonto Sysadmin-Rechte für SQL Server beibehalten. Das Entfernen der Sysadmin-Rechte aus diesen Konten wird nicht unterstützt.  

-   Bei Installation eines primäres Standorts sind die folgenden zusätzlichen Berechtigungen erforderlich:  
    -  **Lokaler Administrator** auf weiteren Computern, auf denen Sie den ersten Verwaltungspunkt und Verteilungspunkt installieren, falls dies nicht auf dem Standortserver erfolgt.  

-   Bei Installation eines neuen untergeordneten primären Standorts unter einem Standort der zentralen Verwaltung sind die folgenden zusätzlichen Berechtigungen erforderlich:  

    -   **Lokaler Administrator** auf dem Computer, der den Standort der zentralen Verwaltung hostet.  

    -   Rollenbasierte Administratorrechte innerhalb von Configuration Manager, die der Sicherheitsrolle **Infrastrukturadministrator** oder **Hauptadministrator** entsprechen.  

-   Verwenden Sie die richtigen Installationsmedien (Quelldateien), und führen Sie Setup an diesem Speicherort aus. Informationen zu den richtigen Quelldateien für die Installation der unterschiedlichen Standorte finden Sie unter [Options for installing different types of sites (Optionen für die Installation der unterschiedlichen Arten von Standorten)](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) im Thema [Prepare to install sites (Vorbereitung zur Installation von Standorten)](../../../../core/servers/deploy/install/prepare-to-install-sites.md).

-   Der Standortserver-Computer muss Zugriff auf aktualisierte Setupdateien von Microsoft haben:
    -  Bevor Sie mit der Installation beginnen, können Sie mit dem [Setup-Downloadprogramm](../../../../core/servers/deploy/install/setup-downloader.md) eine Kopie dieser Dateien in Ihr lokales Netzwerk herunterladen und speichern.
    -  Wenn keine lokale Kopie dieser Datei verfügbar ist, muss der Standortserver Zugriff auf das Internet haben, damit diese Dateien während der Installation von Microsoft heruntergeladen werden können.

  - Bevor Sie einen eigenständigen primären Standort erweitern können, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ installiert ist, müssen Sie den Dienstverbindungspunkt deinstallieren. In einer Hierarchie ist nur eine Instanz dieser Rolle zulässig, und zwar nur für den obersten Standort der Hierarchie. Sie haben die Möglichkeit, die Rolle während der Installation des Standorts der zentralen Verwaltung erneut zu installieren.
  - Der Standortserver- und Standortdatenbankcomputer müssen alle Konfigurationsvoraussetzungen erfüllen. Vor dem Start von Setup können Sie zum Erkennen und Beheben von Problemen die [Voraussetzungsprüfung manuell ausführen](../../../../core/servers/deploy/install/prerequisite-checker.md).  


## <a name="a-namebkmkexpanda-expanding-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Erweitern eines eigenständigen primären Standorts
Die folgenden Voraussetzungen müssen erfüllt sein, damit ein eigenständiger primärer Standort in eine Hierarchie mit einem Standort der zentralen Verwaltung erweitert werden kann:


-   **Installieren Sie die Installationsmedien (Quelldateien) für den neuen Standort der zentralen Verwaltung, die der Version des eigenständigen primären Standorts entsprechen:**  
     Um eine Versionsübereinstimmung sicherzustellen, installieren Sie den neuen Standort mit den Quelldateien aus dem Ordner [CD.latest](../../../../core/servers/manage/the-cd.latest-folder.md) auf dem eigenständigen primären Standort.

     Weitere Informationen zu den richtigen Quelldateien für die Installation der unterschiedlichen Standorte finden Sie unter [Options for installing different types of sites (Optionen für die Installation der unterschiedlichen Arten von Standorten)](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) im Thema [Prepare to install sites (Vorbereitung zur Installation von Standorten)](../../../../core/servers/deploy/install/prepare-to-install-sites.md).


-   **Der eigenständige primäre Standort kann nicht dahingehend konfiguriert werden, dass Daten aus einer anderen Configuration Manager-Hierarchie migriert werden:**  

     Beenden Sie die aktive Migration zum eigenständigen primären Standort aus anderen Configuration Manager-Hierarchien, und entfernen Sie alle Konfigurationen für die Migration. Hierzu gehören Migrationsaufträge, die nicht abgeschlossen wurden, das Sammeln von Daten und die Konfiguration der aktiven Quellhierarchie.  

     Dies ist erforderlich, weil Migrationsvorgänge vom Standort auf der obersten Ebene der Hierarchie ausgeführt und die Migrationskonfigurationen bei der Erweiterung eines eigenständigen primären Standorts nicht an den Standort der zentralen Verwaltung übertragen werden.  

     Wenn Sie nach der Erweiterung des eigenständigen primären Standorts die Migration am primären Standort erneut konfigurieren, werden die migrationsbezogenen Vorgänge vom Standort der zentralen Verwaltung ausgeführt. Weitere Informationen zum Konfigurieren der Migration finden Sie unter [Configuring source hierarchies and source sites for migration to System Center Configuration Manager (Konfigurieren von Quellhierarchien und Quellstandorten für die Migration zu System Center Configuration Manager)](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

-   **Das Computerkonto des Computers, auf dem der neue Standort der zentralen Verwaltung gehostet wird, muss dem eigenständigen primären Standort der Gruppe „Administratoren“ angehören:**  

     Das Computerkonto des neuen Standorts der zentralen Verwaltung muss am eigenständigen primären Standort der Gruppe **Administratoren** angehören. Anderenfalls kann der eigenständige primäre Standort nicht erfolgreich erweitert werden. Diese Voraussetzung gilt nur während der Standorterweiterung. Nach Abschluss der Standorterweiterung kann das Konto am primären Standort aus der Gruppe entfernt werden.  

-   **Dem Benutzerkonto, unter dem Setup zur Installation eines neuen Standorts der zentralen Verwaltung installiert wird, müssen rollenbasierte Verwaltungsberechtigungen am eigenständigen primären Standort gewährt sein:**  

     Zum Installieren eines Standorts der zentralen Verwaltung in einem Standorterweiterungsszenario muss das Benutzerkonto, unter dem Setup zur Installation des Standorts der zentralen Verwaltung ausgeführt wird, in der rollenbasierten Verwaltung am eigenständigen primären Standort entweder als **Hauptadministrator** oder als **Infrastrukturadministrator**definiert sein.  

-   **Sie müssen die folgenden Standortsystemrollen am eigenständigen primären Standort installieren, damit der Standort erweitert werden kann:**  

    -   Asset Intelligence-Synchronisierungspunkt  

    -   Endpoint Protection-Punkt  

    -   Dienstverbindungspunkt  

     Diese Standortsystemrollen werden nur am Standort auf der obersten Ebene der Hierarchie unterstützt. Sie müssen diese Standortsystemrollen daher deinstallieren, ehe Sie den eigenständigen primären Standort erweitern. Nach der Standorterweiterung können Sie diese Standortsystemrollen am Standort der zentralen Verwaltung erneut installieren.  

    Alle anderen Standortsystemrollen können am primären Standort installiert bleiben.  

-   **Der Port für den SQL Server Service Broker muss offen sein zwischen dem eigenständigen primären Standort und dem Computer, auf dem der Standort der zentralen Verwaltung installiert wird:**  

     Für die erfolgreiche Replikation von Daten zwischen einem Standort der zentralen Verwaltung und einem primären Standort muss in Configuration Manager ein Port für die Nutzung durch den SQL Server Service Broker zwischen den beiden Standorten offen sein. Beim Installieren einer zentralen Verwaltung und beim Erweitern eines eigenständigen, primären Standorts wird durch die Voraussetzungsprüfung nicht ermittelt, ob der von Ihnen für den SQL Server Service Broker angegebene Port am primären Standort offen ist.  


## <a name="a-namebkmksecondarya-secondary-sites"></a><a name="bkmk_secondary"></a> Sekundäre Standorte
Im Folgenden werden die Voraussetzungen für die Installation von sekundären Standorten aufgeführt:
-   Der Administrator, der die Installation des sekundären Standorts in der Configuration Manager-Konsole konfiguriert, muss über rollenbasierte Administratorrechte verfügen, die der Sicherheitsrolle **Infrastrukturadministrator** oder **Hauptadministrator** entsprechen.  

-   Das Computerkonto des übergeordneten primären Standorts muss auf dem sekundären Standortservercomputer **Lokaler Administrator** lauten.  

-   Vom sekundären Standort wird zum Hosten der Datenbank des sekundären Standorts eine zuvor installierte SQL Server-Instanz verwendet:  

    -   Das **Computerkonto** des übergeordneten primären Standorts muss über **Sysadmin** -Rechte für die SQL Server-Instanz auf dem sekundären Standortservercomputer verfügen.  

    -   Das **lokale Systemkonto** des Servercomputers des sekundären Standorts muss über **Sysadmin** -Rechte für die SQL Server-Instanz auf dem sekundären Standortservercomputer verfügen.  

        > [!IMPORTANT]  
        >  Nach Abschluss von Setup müssen beide Konten Sysadmin-Rechte für SQL Server beibehalten. Das Entfernen der Sysadmin-Rechte aus diesen Konten wird nicht unterstützt.  

-   Der sekundäre Standortservercomputer muss alle vorausgesetzten Konfigurationen erfüllen. Dazu zählen SQL Server und die standardmäßigen Standortsystemrollen des Verwaltungspunkts und Verteilungspunkts.  



<!--HONumber=Nov16_HO1-->


