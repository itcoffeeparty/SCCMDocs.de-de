---
title: Planen der Standortdatenbank | System Center Configuration Manager
description: Beachten Sie bei der Planung Ihrer System Center Configuration Manager-Hierarchie die Standortdatenbank und den Standortdatenbankserver.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 40ebfaa9b82a65a6265f0c031dbbd0bcdb85da6e


---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>Planen der Standortdatenbank für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Der Standortdatenbankserver ist ein Computer, auf dem eine unterstützte Version von Microsoft SQL Server ausgeführt wird, auf der Informationen für Configuration Manager-Standorte gespeichert werden. Jeder Standort in einer Configuration Manager-Hierarchie enthält eine Standortdatenbank und einen Server, dem die Rolle „Standortdatenbankserver“ zugewiesen wird.  

-   Für Standorte der zentralen Verwaltung und primäre Standorte können Sie SQL Server auf dem Standortserver oder auf einem anderen Computer installieren.  

-   Für sekundäre Standorte können Sie anstelle einer vollständigen SQL Server-Installation SQL Server Express verwenden. Allerdings muss der Datenbankserver auf dem sekundären Standortserver ausgeführt werden.  

Wenn Sie einen Computer als Remote-Datenbankserver verwenden, müssen Sie darauf achten, dass die beteiligte Netzwerkverbindung eine hohe Verfügbarkeit und Bandbreite aufweist. Der Grund hierfür ist, dass der Standortserver und einige Standortsystemrollen kontinuierlich mit dem SQL Server, auf dem die Standortdatenbank gehostet wird, kommunizieren müssen.  


**Beachten Sie bei der Auswahl des Standorts für den Remote-Datenbankserver Folgendes:**  

-   Die für die Kommunikation mit dem Datenbankserver erforderliche Bandbreite hängt von der jeweiligen Kombination vieler verschiedener Standort- und Clientkonfigurationen ab. Die tatsächlich erforderliche Bandbreite kann daher nicht genau vorhergesagt werden.  

-   Die Anforderungen an die Netzwerkbandbreite steigen mit jedem Computer, auf dem der SMS-Anbieter ausgeführt wird und von dem eine Verbindung mit der Standortdatenbank herstellt wird.  

-   Der Computer, auf dem SQL Server ausgeführt wird, muss sich in einer Domäne befinden, die eine bidirektionale Vertrauensstellung mit dem Standortserver und allen Computern hat, auf denen der SMS-Anbieter ausgeführt wird.  

-   Sie können für den Standortdatenbankserver keinen gruppierten SQL Server verwenden, wenn die Standortdatenbank sich auf dem gleichen Computer wie der Standortserver befindet.  


In der Regel werden von einem Standortsystemserver nur Standortsystemrollen von einem einzelnen Configuration Manager-Standort unterstützt. Allerdings können Sie mithilfe unterschiedlicher SQL Server-Instanzen auf gruppierten oder nicht gruppierten Servern, auf denen SQL Server ausgeführt wird, eine Datenbank von verschiedenen Configuration Manager-Standorten aus hosten. Die Unterstützung von Datenbanken von unterschiedlichen Standorten setzt voraus, dass Sie jede SQL Server-Instanz für die Verwendung eindeutiger Kommunikationsports konfigurieren.  


**Die folgenden SQL Server-Konfigurationen können zum Hosten der Standortdatenbank verwendet werden:**  

-   Die Standardinstanz von SQL Server  

-   Eine benannte Instanz auf einem einzelnen Computer mit SQL Server  

-   Eine benannte Instanz auf einer gruppierten Instanz von SQL Server  

-   Eine SQL Server Always On-Verfügbarkeitsgruppe (ab Version 1602)


**Voraussetzungen für die Standortdatenbank:**  

-   Der SQL Server muss zum Hosten der Standortdatenbank die unter [Unterstützung für SQL Server-Versionen für System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md) ausführlich beschriebenen Voraussetzungen erfüllen.  



<!--HONumber=Nov16_HO1-->


