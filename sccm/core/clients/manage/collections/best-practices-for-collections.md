---
title: Bewährte Methoden für Sammlungen
titleSuffix: Configuration Manager
description: Erhalten Sie bewährte Methoden für Sammlungen in System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ab92f27e37113db88d1cadf5ff49870162206563
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
