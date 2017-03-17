---
title: Neue Version 1702 | Microsoft-Dokumentation
description: "Enthält Details zu Änderungen und neuen Funktionen, die in Version 1702 von System Center Configuration Manager eingeführt wurden."
ms.custom: na
ms.date: 03/27/2017
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: Brenduns
ms.author: brenduns
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: 473ba742bea74cbfdf8cab550244ccd522523718
ms.lasthandoff: 03/04/2017

---
# <a name="what39s-new-in-version-1702-of-system-center-configuration-manager"></a>Neues in Version 1702 von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Das Update 1702 für System Center Configuration Manager (Current Branch) ist als konsoleninternes Update für zuvor installierte Standorte verfügbar, die Version 1606 oder 1610 ausführen. Es steht auch als eine Baselineversion zur Verfügung, die Sie beim Installieren einer neuen Bereitstellung verwenden können.

> [!TIP]  
> Sie müssen eine Baselineversion von Configuration Manager verwenden, um einen neuen Standort zu installieren.  
>  Weitere Informationen:    
>  -   [Installieren von neuen Standorten](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [Installieren von Updates an Standorten](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [Baseline- und Updateversionen](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Die folgenden Abschnitte enthalten Details zu Änderungen und neuen Funktionen, die in Version 1702 von Configuration Manager eingeführt wurden.  


## <a name="data-warehouse-service-point"></a>Data Warehouse-Dienstpunkt
Verwenden Sie den Data Warehouse-Dienstpunkt, um langfristige Verlaufsdaten zur Bereitstellung für Configuration Manager zu speichern und hierfür Berichte zu erstellen.

Das Data Warehouse unterstützt ein Datenvolumen von bis zu 2 TB, inklusive der Zeitstempel für Änderungsnachverfolgung. Die Speicherung der Daten wird durch die automatisierte Synchronisierung der Configuration Manager-Standortdatenbank mit der Data Warehouse-Datenbank erreicht. Auf diese Informationen kann dann vom Reporting Services-Punkt aus zugegriffen werden.



Weitere Informationen finden Sie unter [The Data Warehouse service point (Der Data Warehouse-Dienstpunkt)](/sccm/core/servers/manage/data-warehouse).

