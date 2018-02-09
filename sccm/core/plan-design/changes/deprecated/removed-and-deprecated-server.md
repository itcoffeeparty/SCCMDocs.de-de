---
title: "Veraltete Elemente für Configuration Manager-Standortserver"
titleSuffix: Configuration Manager
description: "Hier finden Sie Informationen zu den Produkten und Betriebssystemen, die von System Center Configuration Manager für Standortserver nicht mehr unterstützt werden."
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 0124939ae1ea5c1244c5776973297727b292e028
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="removed-and-deprecated-for-system-center-configuration-manager-site-servers"></a>Entfernte und veraltete Elemente für System Center Configuration Manager-Standortserver

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Artikel werden Produkte und Betriebssysteme beschrieben, deren Support für System Center Configuration Manager-Standortserver eingestellt wird oder die bei einem zukünftigen Update entfernt werden (veraltet sind). Dieser Artikel dient als frühzeitige Warnung hinsichtlich zukünftiger Änderungen, die sich auf Ihre Verwendung von Configuration Manager auswirken können.  

Diese Informationen können sich bei zukünftigen Versionen ändern und enthalten möglicherweise nicht jedes veraltete Feature, Produkt oder Betriebssystem.  


## <a name="deprecated-server-operating-systems"></a>Veraltete Serverbetriebssysteme  

|**Betriebssysteme**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt** |  
|-|-|-| 
|Windows Server 2008 R2|10. Juli 2015| Version 1702 (siehe Hinweis 1)| 
|Windows Server 2008|10. Juli 2015|Version 1511 </br></br>Unterstützung als Standortsystem wird entfernt. (Siehe Hinweis 2).|  

>[!NOTE]
>-   Ab Version 1702 wird Windows Server 2008 R2 für Standortserver bzw. die meisten Standortsystemrollen nicht mehr unterstützt. Versionen vor 1702 unterstützen jedoch weiterhin dessen Verwendung. Dieses Betriebssystem wird jedoch weiterhin für die Verwendung der Standortsystemrolle „Verteilungspunkt“ unterstützt (einschließlich „Pullverteilungspunkt“, PXE und Multicast), bis der Support eingestellt wird oder der erweiterte Supportzeitraum für das Betriebssystem abläuft. Ab Version 1602 können Sie ein direktes Upgrade des Betriebssystems eines Standortservers von Windows Server 2008 R2 auf Windows Server 2012 R2 durchführen.  
>- Weitere Informationen zum direkten Upgrade des Betriebssystems eines Standortservers finden Sie im Artikel [Aktualisieren der lokalen Infrastruktur, die System Center Configuration Manager unterstützt](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2) im Abschnitt [Direktes Upgrade des Betriebssystems von Standortservern mit Windows Server 2008 R2](/sccm/core/servers/manage/upgrade-on-premises-infrastructure).

>[!NOTE]
>-   Windows Server 2008 wird für Standortserver- oder Standortsystemrollen mit Ausnahme des Verteilungspunkts und des Pullverteilungspunkts nicht unterstützt. Sie können dieses Betriebssystem weiterhin als Verteilungspunkt verwenden, bis die Einstellung des Supports angekündigt wird oder der erweiterte Support für das Betriebssystem abläuft. Weitere Informationen finden Sie unter [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008 (Bei der Installation von System Center Configuration Manager CB und LTSB auf Windows Server 2008 tritt ein Fehler auf)](https://support.microsoft.com/help/4015095).

## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Veralteter Support für SQL Server-Versionen als Standortdatenbank  

|**SQL Server-Versionen**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt**|   
|-|-|-| 
|SQL Server 2008 R2:|10. Juli 2015|Version 1702| 
|SQL Server 2008|10. Juli 2015|Version 1511|  


Wenn Sie ein Upgrade für Ihre Version von SQL Server durchführen müssen, werden folgende Methoden in der Reihenfolge ihrer Komplexität empfohlen.
1. [Direktes Upgrade von SQL Server](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (empfohlen).
2. Installieren Sie auf einem neuen Computer eine neue Version von SQL Server. [Verwenden Sie anschließend die Option zur Datenbankverschiebung](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) im Configuration Manager-Setup, um Ihren Standortserver auf den neuen Computer mit SQL Server zu verweisen.
3. Verwenden Sie [Sicherung und Wiederherstellung](/sccm/protect/understand/backup-and-recovery).


## <a name="more-information"></a>Weitere Informationen
Weitere Informationen finden Sie in folgenden Quellen:
 - [Entfernte und veraltete Elemente](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - Website [Microsoft Lifecycle-Richtlinie](https://support.microsoft.com/lifecycle)
 - [Support für die Current Branch-Versionen von Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)