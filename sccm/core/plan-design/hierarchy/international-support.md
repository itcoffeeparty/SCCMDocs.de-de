---
title: "Internationale Unterstützung | System Center Configuration Manager"
description: "Konfigurieren Sie System Center Configuration Manager, um spezifische, internationale Anforderungen zu erfüllen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 592ae2b8fbf55fa59afe909071a81b6bd3159ef7


---
# <a name="international-support-in-system-center-configuration-manager"></a>Internationale Unterstützung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In den folgenden Abschnitten finden Sie technische Details zu einer System Center Configuration Manager-Konfiguration, die mit spezifischen internationalen Anforderungen kompatibel ist.  

## <a name="gb18030-requirements"></a>GB18030-Anforderungen  
 Configuration Manager erfüllt die von GB18030 definierten Standards, sodass Sie Configuration Manager auch in China einsetzen können. Laut GB18030-Anforderungen müssen für eine Configuration Manager-Bereitstellung folgende Konfigurationen erfüllt sein:  

-   Auf allen Standortservercomputern und SQL Server-Computern, die mit Configuration Manager verwendet werden, ist die Ausführung eines chinesischen Betriebssystems erforderlich.  

-   Von jeder Standortdatenbank und jeder SQL Server-Instanz in der Hierarchie muss die gleiche Sortierung verwendet werden, und zwar eine der beiden folgenden:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Die Datenbanksortierungen sind eine Ausnahme in den unter [Unterstützung für SQL Server-Versionen für System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md) beschriebenen Voraussetzungen.  

-   Sie müssen eine Datei namens **GB18030.SMS** im Stammordner des Systemvolumes auf jedem Standortservercomputer in der Hierarchie ablegen. In dieser Datei sind keine Daten enthalten. Es kann sich um eine leere Textdatei handeln, die entsprechend dieser Anforderung benannt wurde.  



<!--HONumber=Nov16_HO1-->

