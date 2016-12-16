---
title: Planen einer Migration | System Center Configuration Manager
description: "Erfahren Sie mehr über Standorte und Hierarchien, bevor Sie Daten in eine Zielhierarchie in System Center Configuration Manager migrieren."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a80c7af58f88f76afd00771778411a4842a204c8


---
# <a name="planning-for-migration-to-system-center-configuration-manager"></a>Planen der Migration zu System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Stellen Sie sicher, dass Sie mit Standorten und Hierarchien in Configuration Manager vertraut sind, bevor Sie Daten in eine System Center Configuration Manager-Zielhierarchie migrieren. Weitere Informationen zu Standorten und Hierarchien finden Sie unter [Grundlagen von System Center Configuration Manager](../../core/understand/fundamentals.md).  

 Sie müssen zuerst eine System Center Configuration Manager-Hierarchie als Zielhierarchie installieren, bevor Sie Daten aus einer unterstützten Quellhierarchie migrieren können.  

 Konfigurieren Sie nach dem Installieren der Zielhierarchie die Verwaltungsfunktionen, die Sie in der Zielhierarchie verwenden möchten, bevor Sie mit dem Migrieren von Daten beginnen.  

 Möglicherweise müssen Sie zusätzlich Vorkehrungen für eine Überlappung der Quellhierarchie mit der Zielhierarchie treffen. Beispielsweise können Sie beim Konfigurieren der Quellhierarchie angeben, dass die gleichen Netzwerkspeicherorte oder -grenzen wie für die Zielhierarchie verwendet werden sollen. Anschließend installieren Sie neue Clients für die Zielhierarchie und verwenden die automatische Standortzuweisung. Bei diesem Szenario ist es möglich, dass vom Client eine fehlerhafte Zuweisung zur Quellhierarchie vorgenommen wird, weil vom neu installierten Configuration Manager-Client aus beiden Hierarchien ein Standort für den Beitritt ausgewählt werden kann. Planen Sie daher die Zuweisung jedes neuen Clients in der Zielhierarchie zu einem bestimmten Standort dieser Hierarchie, anstatt die automatische Standortzuweisung zu verwenden.  

 Weitere Informationen zu Standortzuweisungen finden Sie im Abschnitt [Überlegungen zur Clientstandortzuweisung](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) des Themas [Interoperabilität zwischen verschiedenen Versionen von System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

## <a name="planning-topics"></a>Planungsthemen  
 Die folgenden Themen sind bei der Migration einer unterstützten Quellhierarchie in eine System Center Configuration Manager-Zielhierarchie hilfreich:  

-   [Voraussetzungen für die Migration in System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md)  

-   [Administratorchecklisten zur Migrationsplanung in System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Bestimmen, ob Daten zu System Center Configuration Manager migriert werden sollen](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Planen einer Strategie für Quellhierarchien in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Administratorchecklisten zur Migrationsplanung in System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Planen einer Strategie für die Clientmigration in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Planen einer Migrationsstrategie für die Inhaltsbereitstellung in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Planen der Migration von Configuration Manager-Objekten zu System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Planen der Überwachung der Migrationsaktivitäten in System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Planen des Abschließens der Migration in System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md)  



<!--HONumber=Nov16_HO1-->


