---
title: Voraussetzungen für Sammlungen
titleSuffix: Configuration Manager
description: Hier erhalten Sie Informationen zur Verwendung von Sammlungen in System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 12cbffb63ce449afedb9159174409fb5b1f7583f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Voraussetzungen für Sammlungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sammlungen in System Center Configuration Manager weisen nur Abhängigkeiten innerhalb des Produkts auf.  

## <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Reporting Services-Punkt|Die Standortsystemrolle des Reporting Services-Punkts muss installiert werden, bevor Berichte für Sammlungen ausgeführt werden können. Weitere Informationen finden Sie unter [Berichterstellung in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Für die Verwaltung von Sammlungen sind spezielle Sicherheitsberechtigungen erforderlich.|Zum Verwalten der Konformitätseinstellungen müssen Sie über folgende Sicherheitsberechtigungen verfügen:<br /><br /> - So erstellen und verwalten Sie Sammlungen: **Erstellen**, **Löschen**, **Ändern**, **Ordner ändern**, **Objekt verschieben**, **Lesen** und **Ressource lesen** für das Objekt **Sammlung**.<br /><br /> - So verwalten Sie Sammlungseinstellungen: **Sammlungseinstellung ändern** für das Objekt **Sammlung**.<br /><br /> Die Berechtigung **Ordner ändern** ist für alle Sammlungsordner, einschließlich der Stammordners, erforderlich.|  
