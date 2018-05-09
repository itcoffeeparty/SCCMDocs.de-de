---
title: Internationale Unterstützung
titleSuffix: Configuration Manager
description: Konfigurieren Sie System Center Configuration Manager, um spezifische, internationale Anforderungen zu erfüllen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bce6abd57cd50ff19339c29b97bda165109b79b1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="international-support-in-system-center-configuration-manager"></a>Internationale Unterstützung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In den folgenden Abschnitten finden Sie technische Details dazu, wie Sie System Center Configuration Manager mit bestimmten internationalen Anforderungen kompatibel machen können.  

## <a name="gb18030-requirements"></a>GB18030-Anforderungen  
 Configuration Manager erfüllt die von GB18030 definierten Standards, sodass Sie Configuration Manager auch in China einsetzen können. Laut GB18030-Anforderungen müssen für eine Configuration Manager-Bereitstellung folgende Konfigurationen erfüllt sein:  

-   Auf allen Standortservercomputern und SQL Server-Computern, die mit Configuration Manager verwendet werden, ist die Ausführung eines chinesischen Betriebssystems erforderlich.  

-   Von jeder Standortdatenbank und jeder SQL Server-Instanz in der Hierarchie muss die gleiche Sortierung verwendet werden, und zwar eine der beiden folgenden:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Die Datenbanksortierungen sind eine Ausnahme in den unter [Unterstützung für SQL Server-Versionen für System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md) beschriebenen Voraussetzungen.  

-   Sie müssen eine Datei namens **GB18030.SMS** im Stammordner des Systemvolumes auf jedem Standortservercomputer in der Hierarchie ablegen. In dieser Datei sind keine Daten enthalten. Es kann sich um eine leere Textdatei handeln, die entsprechend dieser Anforderung benannt wurde.  
