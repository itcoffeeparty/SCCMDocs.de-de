---
title: Voraussetzungen für die Energieverwaltung
titleSuffix: Configuration Manager
description: Hier erhalten Sie Informationen über die Voraussetzungen für die Energieverwaltung in System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c6630ef07c0b7947875ea2adac4e6612143aaee8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="prerequisites-for-power-management-in-system-center-configuration-manager"></a>Voraussetzungen für die Energieverwaltung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die Energieverwaltung in System Center Configuration Manager weist externe Abhängigkeiten sowie Abhängigkeiten innerhalb des Produkts auf.  

## <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager  
 In der folgenden Tabelle sind die Abhängigkeiten aufgelistet, die außerhalb von Configuration Manager für die Energieverwaltung bestehen.  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Clientcomputer müssen die erforderlichen Energiezustände unterstützen.|Um alle Funktionen der Energieverwaltung nutzen zu können, müssen Clientcomputer die Zustände "Standbymodus" und "Ruhezustand" sowie die Aktionen "Aktivierung nach Standbymodus" und "Aktivierung nach Ruhezustand" unterstützen. Klären Sie anhand des Berichts **Energiefunktionen** , ob die Computer diese Modi und Aktionen unterstützen. Weitere Informationen finden Sie unter [Power Capabilities Report (Bericht über Energiefunktionen)](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) im Thema [How to Monitor and Plan for Power Management in Configuration Manager (Überwachen und Planen der Energieverwaltung in Configuration Manager)](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  
 In der folgenden Tabelle sind die Abhängigkeiten aufgelistet, die innerhalb von Configuration Manager für die Energieverwaltung bestehen.  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Die Energieverwaltung muss aktiviert sein, damit Energiesparpläne erstellt und überwacht werden können.|Informationen zum Aktivieren und Konfigurieren der Energieverwaltung finden Sie unter [Configuring power management in System Center Configuration Manager (Konfigurieren der Energieverwaltung in System Center Configuration Manager)](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Reporting Services-Punkt|Es muss ein Reporting Services-Punkt erstellt werden, bevor Energieverwaltungsberichte angezeigt werden können. Weitere Informationen finden Sie unter [Berichterstellung in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
