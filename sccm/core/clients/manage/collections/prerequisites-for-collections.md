---
title: "Voraussetzungen für Sammlungen"
titleSuffix: Configuration Manager
description: Hier erhalten Sie Informationen zur Verwendung von Sammlungen in System Center Configuration Manager.
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
caps.latest.revision: "7"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 5696a4cc81d8be889f6040a2f9610e1aec17d271
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/12/2017
---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Voraussetzungen für Sammlungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sammlungen in System Center Configuration Manager weisen nur Abhängigkeiten innerhalb des Produkts auf.  

## <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Reporting Services-Punkt|Die Standortsystemrolle des Reporting Services-Punkts muss installiert werden, bevor Berichte für Sammlungen ausgeführt werden können. Weitere Informationen finden Sie unter [Berichterstellung in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Für die Verwaltung von Sammlungen sind spezielle Sicherheitsberechtigungen erforderlich.|Zum Verwalten der Kompatibilitätseinstellungen müssen Sie über folgende Sicherheitsberechtigungen verfügen:<br /><br /> - So erstellen und verwalten Sie Sammlungen: **Erstellen**, **Löschen**, **Ändern**, **Ordner ändern**, **Objekt verschieben**, **Lesen** und **Ressource lesen** für das Objekt **Sammlung**.<br /><br /> - So verwalten Sie Sammlungseinstellungen: **Sammlungseinstellung ändern** für das Objekt **Sammlung**.<br /><br /> Die Berechtigung **Ordner ändern** ist für alle Sammlungsordner, einschließlich der Stammordners, erforderlich.|  
