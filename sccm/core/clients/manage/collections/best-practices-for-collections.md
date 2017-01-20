---
title: "Bewährte Methoden für Sammlungen | System Center Configuration Manager"
description: "Erhalten Sie bewährte Methoden für Sammlungen in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8e22f353ba0803a3b1b4d387a8c00fdb98186bf5


---
# <a name="best-practices-for-collections-in-system-center-configuration-manager"></a>Bewährte Methoden für Sammlungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie die folgenden bewährten Methoden für Sammlungen in System Center Configuration Manager.  

## <a name="do-not-use-incremental-updates-for-a-large-number-of-collections"></a>Verwenden Sie keine inkrementellen Updates bei einer größeren Anzahl von Sammlungen  
 Wenn Sie die Option **Inkrementelle Updates für diese Sammlung verwenden** für zahlreiche Sammlungen aktivieren, können durch diese Konfiguration Bewertungsverzögerungen bewirkt werden. Dies gilt ab einem Schwellenwert von etwa 200 Sammlungen in Ihrer Hierarchie. Die genaue Anzahl hängt von folgenden Faktoren ab:  

-   Gesamtzahl der Sammlungen  

-   Häufigkeit, mit der neue Ressourcen der Hierarchie hinzugefügt und darin geändert werden  

-   Anzahl der Clients in Ihrer Hierarchie  

-   Komplexität der Sammlungsmitgliedschaftsregeln in Ihrer Hierarchie  

## <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Achten Sie darauf, dass die Wartungsfenster für die Bereitstellung wichtiger Softwareupdates groß genug sind.  
 Durch Wartungsfenster für Gerätesammlungen können Sie festlegen, dass Software nur zu bestimmten Zeiten von Configuration Manager auf diesen Geräten installiert werden kann. Wenn das Wartungsfenster zu klein ist, können wichtige Softwareupdates möglicherweise nicht vom Client installiert werden. Dies erhöht das Risiko eines Angriffs, der von diesem Softwareupdate verhindert würde.  



<!--HONumber=Nov16_HO1-->


