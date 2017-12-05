---
title: Planen der Migration
titleSuffix: Configuration Manager
description: "Erfahren Sie mehr über Standorte und Hierarchien, bevor Sie Daten in eine Zielhierarchie in System Center Configuration Manager migrieren."
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
caps.latest.revision: "7"
caps.handback.revision: "0"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 76ee1377f0ee555f9a939c5282df16cee73ecf61
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="plan-for-migration-to-system-center-configuration-manager"></a>Planen der Migration zu System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Stellen Sie sicher, dass Sie mit Standorten und Hierarchien in Configuration Manager vertraut sind, bevor Sie Daten in eine System Center Configuration Manager-Zielhierarchie migrieren. Weitere Informationen zu Standorten und Hierarchien finden Sie unter [Grundlagen von System Center Configuration Manager](../../core/understand/fundamentals.md).  

 Sie müssen zuerst eine System Center Configuration Manager-Hierarchie als Zielhierarchie installieren, bevor Sie Daten aus einer unterstützten Quellhierarchie migrieren können.  

 Richten Sie nach dem Installieren der Zielhierarchie die Verwaltungsfeatures und -funktionen ein, die Sie in Ihrer Zielhierarchie verwenden möchten, bevor Sie mit dem Migrieren von Daten beginnen.  

 Möglicherweise müssen Sie zusätzlich Vorkehrungen für eine Überlappung der Quellhierarchie mit der Zielhierarchie treffen. Beispielsweise können Sie beim Einrichten der Quellhierarchie angeben, dass die gleichen Netzwerkspeicherorte oder -grenzen wie für die Zielhierarchie verwendet werden sollen. Anschließend installieren Sie neue Clients für Ihre Zielhierarchie und verwenden die automatische Standortzuweisung. Bei diesem Szenario ist es möglich, dass vom Client eine fehlerhafte Zuweisung zur Quellhierarchie vorgenommen wird, weil vom neu installierten Configuration Manager-Client aus beiden Hierarchien ein Standort für den Beitritt ausgewählt werden kann. Planen Sie daher die Zuweisung jedes neuen Clients in der Zielhierarchie zu einem bestimmten Standort dieser Hierarchie, anstatt die automatische Standortzuweisung zu verwenden.  

 Weitere Informationen zu Standortzuweisungen finden Sie im Abschnitt [Überlegungen zur Clientstandortzuweisung](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) des Themas [Interoperabilität zwischen verschiedenen Versionen von System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

## <a name="plan-topics"></a>Planen von Themen  
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
