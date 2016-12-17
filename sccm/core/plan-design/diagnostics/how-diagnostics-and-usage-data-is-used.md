---
title: Verwenden von Diagnosedaten | System Center Configuration Manager
description: "Erfahren Sie mehr darüber, wie Microsoft die Diagnose- und Nutzungsdaten verwendet, die System Center Configuration Manager sammelt."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 68e2a6b5baeaf9ab9e74e771bbc3d755d1388779


---
# <a name="how-diagnostics-and-usage-data-is-used-for-system-center-configuration-manager"></a>Nutzung von Diagnose- und Verwendungsdaten für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die für System Center Configuration Manager erfassten Diagnose- und Nutzungsdaten stellen Microsoft ein fast unmittelbares Feedback zum Betrieb des Produkts oder zu Fehlern im Betrieb bereit und dienen zur Anpassung zukünftiger Updates. Außerdem werden Konfigurationsdaten bereitgestellt, mit deren Hilfe in der Produktion befindliche Konfigurationen entwickelt und getestet werden können. Beispiel:  

-   Die vom Standortserver verwendeten Windows Server-Versionen  

-   Die installierten Sprachpakete  

-   Das Delta zwischen SQL-Schema und Standardwert des Produkts  

Mithilfe dieser Daten kann das Entwicklungsteam zukünftige Tests planen, um die beste Lösung für die am häufigsten verwendeten Konfigurationen zu finden. Da Updates für Configuration Manager in kürzeren Intervallen veröffentlicht werden (um eine bessere Unterstützung für Technologien zu bieten, die schnellen Veränderungen unterliegen, wie Windows 10 und Microsoft Intune), sind diese Daten für eine rasche Anpassung und Optimierung von entscheidender Bedeutung.  

Gleichermaßen wichtig ist, wofür die Diagnose- und Verwendungsdaten nicht eingesetzt werden. Microsoft verwendet diese Daten nicht zu folgenden Zwecken:  

-   Lizenzierungsüberwachung, z.B. Vergleich der Verwendung mit Lizenzverträgen  

-   Überwachung von Produkten, die nicht mehr unterstützt werden  

-   Werbung basierend auf verfügbaren Daten wie z.B. Featureverwendung oder geografischem Standort (Zeitzone)  

##  <a name="a-namebkmkimprovea-examples-of-how-diagnostics-and-usage-data-is-improving-the-product"></a><a name="bkmk_improve"></a> Beispiele für die Verbesserung des Produkts anhand von Diagnose und Verwendungsdaten  
Microsoft verwendet die verfügbaren Daten zur Verbesserung des Produkts. Im Folgenden sind einige Beispiele aufgeführt:  

-   **Überarbeitete Unterstützung für ältere Serverbetriebssysteme:**  

     In der anfänglichen Unterstützung, die von Current Branch von System Center Configuration Manager angeboten wurde, war der Unterstützungszeitraum für Windows Server 2008 R2 eingeschränkt. Nach der Untersuchung der Nutzungsdaten von Kunden, die ein Upgrade auf Current Branch von Configuration Manager durchgeführt haben, stellten wir fest, dass dieser Zeitraum überarbeitet und erweitert werden musste, um für die große Kundenanzahl, die dieses Serverbetriebssystem noch immer zum Hosten von Standortservern und Standortsystemrollen verwenden, einen Support anzubieten.  

-   **Verbesserte Voraussetzungsprüfungen:**  

     Basierend auf den Verwendungsdaten haben wir die Voraussetzungsprüfungen für die Installation eines Updates verbessert und veraltete Regeln entfernt sowie zusätzliche Fälle berücksichtigt. In einigen Fällen werden Probleme automatisch behoben.  



<!--HONumber=Nov16_HO1-->

