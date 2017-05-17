---
title: "Voraussetzungen für Sammlungen | Microsoft-Dokumentation"
description: Hier erhalten Sie Informationen zur Verwendung von Sammlungen in System Center Configuration Manager.
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
caps.latest.revision: 7
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 81342ab0d064e3f2da19126819bdd048270a4320
ms.contentlocale: de-de
ms.lasthandoff: 12/16/2016


---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Voraussetzungen für Sammlungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sammlungen in System Center Configuration Manager weisen nur Abhängigkeiten innerhalb des Produkts auf.  

## <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Reporting Services-Punkt|Die Standortsystemrolle des Reporting Services-Punkts muss installiert werden, bevor Berichte für Sammlungen ausgeführt werden können. Weitere Informationen finden Sie unter [Berichterstellung in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Für die Verwaltung von Sammlungen sind spezielle Sicherheitsberechtigungen erforderlich.|Zum Verwalten der Kompatibilitätseinstellungen müssen Sie über folgende Sicherheitsberechtigungen verfügen:<br /><br /> - So erstellen und verwalten Sie Sammlungen: **Erstellen**, **Löschen**, **Ändern**, **Ordner ändern**, **Objekt verschieben**, **Lesen** und **Ressource lesen** für das Objekt **Sammlung**.<br /><br /> - So verwalten Sie Sammlungseinstellungen: **Sammlungseinstellung ändern** für das Objekt **Sammlung**.<br /><br /> Die Berechtigung **Ordner ändern** ist für alle Sammlungsordner, einschließlich der Stammordners, erforderlich.|  

