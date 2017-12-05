---
title: Planen der Standortdatenbank
titleSuffix: Configuration Manager
description: Beachten Sie bei der Planung Ihrer System Center Configuration Manager-Hierarchie die Standortdatenbank und den Standortdatenbankserver.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
caps.latest.revision: "5"
caps.handback.revision: "0"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 4366ea22ff654b787a3b350ed6a0b58dfbdd8e7d
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>Planen der Standortdatenbank für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Der Standortdatenbankserver ist ein Computer, auf dem eine unterstützte Version von Microsoft SQL Server ausgeführt wird. Von SQL Server werden Informationen für Configuration Manager-Standorte gespeichert. Jeder Standort in einer Configuration Manager-Hierarchie enthält eine Standortdatenbank und einen Server, dem die Rolle „Standortdatenbankserver“ zugewiesen wird.  

-   Für Standorte der zentralen Verwaltung und primäre Standorte können Sie SQL Server auf dem Standortserver oder auf einem anderen Computer installieren.  

-   Für sekundäre Standorte können Sie anstelle einer vollständigen SQL Server-Installation SQL Server Express verwenden. Der Datenbankserver muss jedoch auf dem sekundären Standortserver ausgeführt werden.  

Die folgenden SQL Server-Konfigurationen können zum Hosten der Standortdatenbank verwendet werden:  

-   Die Standardinstanz von SQL Server  

-   Eine benannte Instanz auf einem einzelnen Computer mit SQL Server  

-   Eine benannte Instanz auf einer gruppierten Instanz von SQL Server  

-   Eine SQL Server Always On-Verfügbarkeitsgruppe (ab Version 1602 von System Center Configuration Manager)


Der SQL Server muss zum Hosten der Standortdatenbank die unter [Unterstützung für SQL Server-Versionen für System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md) ausführlich beschriebenen Voraussetzungen erfüllen.  



## <a name="remote-database-server-location-considerations"></a>Beim Standort des Remotedatenbankservers zu berücksichtigen  

Wenn Sie einen Computer als Remotedatenbankserver verwenden, müssen Sie darauf achten, dass die beteiligte Netzwerkverbindung eine hohe Verfügbarkeit und Bandbreite aufweist. Der Standortserver und einige Standortsystemrollen müssen kontinuierlich mit dem Remoteserver kommunizieren, auf dem die Standortdatenbank gehostet wird.

-   Die für die Kommunikation mit dem Datenbankserver erforderliche Bandbreite hängt von einer Kombination vieler verschiedener Standort- und Clientkonfigurationen ab. Die tatsächlich erforderliche Bandbreite kann daher nicht genau vorhergesagt werden.  

-   Die Anforderungen an die Netzwerkbandbreite steigen mit jedem Computer, auf dem der SMS-Anbieter ausgeführt wird und von dem eine Verbindung mit der Standortdatenbank herstellt wird.  

-   Der Computer, auf dem SQL Server ausgeführt wird, muss sich in einer Domäne befinden, die eine bidirektionale Vertrauensstellung mit dem Standortserver und allen Computern hat, auf denen der SMS-Anbieter ausgeführt wird.  

-   Sie können für den Standortdatenbankserver keinen gruppierten SQL Server verwenden, wenn die Standortdatenbank sich auf dem gleichen Computer wie der Standortserver befindet.  


In der Regel unterstützt ein Standortsystemserver nur die Standortsystemrollen von einem einzigen Configuration Manager-Standort. Sie können jedoch verschiedene Instanzen von SQL Server auf gruppierten oder nicht gruppierten Servern mit SQL Server verwenden, um eine Datenbank von verschiedenen Configuration Manager-Standorten zu hosten. Die Unterstützung von Datenbanken von unterschiedlichen Standorten setzt voraus, dass Sie jede SQL Server-Instanz für die Verwendung eindeutiger Kommunikationsports konfigurieren.  
