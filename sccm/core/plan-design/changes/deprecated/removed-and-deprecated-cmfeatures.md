---
title: Veraltete Configuration Manager-Features
titleSuffix: Configuration Manager
description: "Hier finden Sie Informationen zu den Features, die von System Center Configuration Manager nicht mehr unterstützt werden."
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: d49e0f839106af652f7b49227b6c4f8c957347d9
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Entfernte und veraltete Features für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Artikel werden Features beschrieben, deren Support für System Center Configuration Manager eingestellt wird oder die bei einem zukünftigen Update entfernt werden (veraltet sind). Dieser Artikel dient als frühzeitige Warnung hinsichtlich zukünftiger Änderungen, die sich auf Ihre Verwendung von Configuration Manager auswirken können.  

Diese Informationen können sich bei zukünftigen Versionen ändern und enthalten möglicherweise nicht jedes veraltete Configuration Manager-Feature.

## <a name="deprecated-features"></a>Veraltete Features  

|**Feature**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt**|  
|-|-|-|  
|Mit der Einführung der neuen Softwarecenter-Benutzeroberfläche in Version 1511 werden Apps, die bisher nur im Anwendungskatalog angezeigt wurden (für Benutzer verfügbare Apps), jetzt im Softwarecenter angezeigt. </br></br>Da diese primäre Funktionalität des Anwendungskatalogs jetzt im Softwarecenter enthalten ist, wird die internetbasierte Anwendungskatalog-Benutzeroberfläche in den nächsten Monaten nicht mehr verfügbar sein.|11. August 2017| Unterstützung für die Anwendungskatalog-Website-Benutzeroberfläche endet mit dem ersten Update, das nach dem 1. Juni 2018 veröffentlicht wird.|
|Das Softwarecenter weist einen neuen, modernen Look auf. In den kommenden Monaten wird die vorherige Version des Softwarecenters nicht länger zur Verfügung stehen.<br><br>Sie können Clients für die Verwendung des neuen Softwarecenters konfigurieren, indem Sie die Clienteinstellung **Computer-Agent** > **Neues Softwarecenter verwenden** aktivieren.<br><br>Weitere Informationen zum Softwarecenter finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung in System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13. Dezember 2016|Die Unterstützung der vorherigen Version des Softwarecenters endet mit dem ersten Update, das nach dem 1. Januar 2018 veröffentlicht wird.|
|Verwaltung von virtuellen Festplatten (VHDs) mit Configuration Manager. </br></br>Dies schließt das Entfernen von Optionen zum Erstellen einer neuen virtuellen Festplatte oder Verwalten einer virtuellen Festplatte mithilfe einer Tasksequenz und das Entfernen des Knotens „Virtuelle Festplatten“ über die Configuration Manager-Konsole ein. </br></br>Wenn dieser Support eingestellt wird, werden vorhandene virtuelle Festplatten nicht gelöscht, es kann aber nicht mehr in der Configuration Manager-Konsole darauf zugegriffen werden.  |6. Januar 2017 |Version 1710|
|Tasksequenzen: <br /> - In dynamischen Datenträger konvertieren <br /> - Bereitstellungstools installieren |18. November 2016|Version 1710|
|System Center Configuration Manager-Upgradebewertungstool </br></br>Das Upgradebewertungstool ist sowohl von System Center Configuration Manager als auch vom Anwendungskompatibilitäts-Toolkit (Application Compatibility Toolkit, ACT) 6.x abhängig. Die letzte Version von ACT war im Windows 10 v1511 ADK enthalten. Da es keine weiteren Updates für ACT geben wird, wird auch der entsprechende Support für das Upgradebewertungstool eingestellt. </br></br>Das Upgradebewertungstool wird durch das Feature [Upgradebereitschaft](/sccm/core/clients/manage/upgrade/upgrade-analytics) ersetzt. Hinweise zu veralteten Funktionen wurden am 12. September 2016 auf der [Downloadseite des Upgradebewertungstools](https://www.microsoft.com/download/details.aspx?id=37145) hinzugefügt. | 12. September 2016  | 11. Juli 2017 |
|Tasksequenzen: <br /> – OSDPreserveDriveLetter  <br /><br /> Während einer standardmäßigen Betriebssystembereitstellung bestimmt Windows Setup den Laufwerkbuchstaben, der am besten zur Verwendung geeignet ist (in der Regel C:). Wenn Sie ein anderes Laufwerk zur Verwendung angeben möchten, können Sie den Speicherort im Tasksequenzschritt „Betriebssystem anwenden“ ändern. Wechseln Sie zu der Einstellung **Wählen Sie den Standort aus, an dem Sie dieses Betriebssystem anwenden möchten**. Wählen Sie **Bestimmter Buchstabe für logisches Laufwerk** und anschließend das Laufwerk, das Sie verwenden möchten. |20. Juni 2016 |Version 1606 |
|Netzwerkzugriffsschutz (Network Access Protection, NAP) wie in System Center 2012 Configuration Manager|10. Juli 2015|Version 1511|  
|Out-of-Band-Verwaltung wie in System Center 2012 Configuration Manager|16. Oktober 2015|Version 1511|



<br></br>
Zusätzliche Informationen zu Features, die mit Version 1511 der System Center Configuration Manager-Version entfernt wurden:

###  <a name="bkmk_amt"></a> Out-of-Band-Verwaltung  
 Mit Configuration Manager wurde der native Support für AMT-basierte Computer in der Configuration Manager-Konsole entfernt.  

-   AMT-basierte Computer werden weiterhin vollständig verwaltet, wenn Sie das [Intel SCS-Add-On für Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html) verwenden. Über das Add-On haben Sie Zugriff auf die neuesten AMT-Verwaltungsfunktionen. Gleichzeitig werden die Beschränkungen aufgehoben, die vor der Einbindung dieser Änderungen durch Configuration Manager eingeführt wurden.  

-   Die Out-Band-Verwaltung in System Center 2012 Configuration Manager ist von dieser Änderung nicht betroffen.  

###  <a name="bkmk_nap"></a> Netzwerkzugriffsschutz  
 System Center Configuration Manager hat den Support für den Netzwerkzugriffsschutz eingestellt. Das Feature wurde in Windows Server 2012 R2 als veraltet markiert und aus Windows 10 entfernt.  

 Alternativen für den Netzwerkzugriffsschutz finden Sie im Abschnitt *Veraltete Funktionalität* unter [Netzwerkrichtlinien- und Zugriffsdienste: Übersicht](https://technet.microsoft.com/library/hh831683.aspx).

## <a name="more-information"></a>Weitere Informationen
Weitere Informationen finden Sie in folgenden Quellen:
 - [Entfernte und veraltete Elemente](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - Website [Microsoft Lifecycle-Richtlinie](https://support.microsoft.com/lifecycle)
 - [Support für die Current Branch-Versionen von Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)
