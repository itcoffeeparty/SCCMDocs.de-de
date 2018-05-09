---
title: Überwachen der Migration
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie die Configuration Manager-Konsole verwenden, um den Fortschritt und Erfolg der Migrationsaufträge zu überwachen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2dfad7c9963862ff90934861973bf3862d745b98
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="planning-to-monitor-migration-activity-in-system-center-configuration-manager"></a>Planen der Überwachung der Migrationsaktivitäten in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit System Center Configuration Manager können Sie die Migration in der Configuration Manager-Konsole überwachen, die eine Verbindung zur Zielhierarchie herstellt. Verwenden Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Knoten **Migration**, um Fortschritt und Erfolg der Migrationsaufträge zu überwachen. Sie können für jeden Migrationsauftrag zusammenfassende Informationen darüber anzeigen, welche Objekte migriert wurden, welche Objekte noch nicht migriert wurden und wie viele Objekte vom Migrationsauftrag ausgeschlossen sind. Außerdem finden Sie hier Informationen zu Migrationsproblemen.  

## <a name="view-migration-progress"></a>Migrationsfortschritt anzeigen  
 Für die Fortschrittanzeigen in Bezug auf einen Migrationsauftrag führen Sie eine der folgenden Aktionen durch:  

-   Erweitern Sie im Arbeitsbereich **Verwaltung** der Configuration Manager-Konsole den Knoten **Migrationsaufträge**, und wählen Sie einen Migrationsauftrag und anschließend die Registerkarte **Objekte in Auftrag** aus.  

-   Zur Überprüfung des Migrationsfortschritts oder der Identifikation von Problemen können Sie auch die Configuration Manager-Protokolldateien verwenden. Der Migrations-Manager ist der Configuration Manager-Prozess zum Nachverfolgen der Migrationsaktionen und zu deren Aufzeichnung in der Datei „migmctrl.log“ im Ordner **\&lt;InstallationPath\>\\LOGS** auf dem Standortserver.  

    > [!NOTE]  
    >  Kann ein Migrationsauftrag nicht ausgeführt werden, überprüfen Sie umgehend die Informationen in der Datei "migmctrl.log". Es werden kontinuierlich Protokolleinträge zur Datei hinzugefügt. Alte Daten werden überschrieben. Wenn Daten überschrieben werden, können Sie möglicherweise nicht mehr herausfinden, ob Probleme mit migrierten Objekten in Zusammenhang mit Migrationsproblemen stehen. Unabhängig davon, mit welchem Standort eine Verbindung Ihrer Configuration Manager-Konsole beim Konfigurieren der Migration hergestellt wird, werden Migrationsaktivitäten auf dem Standort der obersten Ebene der Hierarchie protokolliert.  

-   Verwenden Sie die Berichterstellung in Configuration Manager. In Configuration Manager stehen mehrere integrierte Berichte für Migrationsaufträge zur Verfügung, die Sie bei Bedarf auch an Ihre Anforderungen anpassen können. Weitere Informationen zu Berichten in Configuration Manager finden Sie unter [Berichterstellung in System Center Configuration Manager](../../core/servers/manage/reporting.md).  
