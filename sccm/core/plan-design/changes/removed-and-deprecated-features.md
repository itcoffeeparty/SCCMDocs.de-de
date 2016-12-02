---
title: Veraltete Features | System Center Configuration Manager
description: "Hier finden Sie Informationen zu den Features, Produkten und Betriebssystemen, die von System Center Configuration Manager nicht mehr unterstützt werden."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0f1e1070fd5b56b1abf22159e9f95b3b4bd8a8c6


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Entfernte und veraltete Features für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Thema werden Features, Produkte und Betriebssysteme beschrieben, deren Support bei System Center Configuration Manager eingestellt wird oder die bei einem zukünftigen Update entfernt werden (veraltet sind). Dies dient als frühzeitige Warnung hinsichtlich zukünftiger Änderungen, die sich auf Ihre Verwendung von Configuration Manager auswirken können.  

 Diese Informationen können sich bei zukünftigen Versionen ändern und enthalten möglicherweise nicht jedes veraltete Feature, Produkt oder Betriebssystem.  

## <a name="deprecated-features-products-and-operating-systems"></a>Veraltete Features, Produkte und Betriebssysteme  
 Für Microsoft-Produkte und Betriebssysteme, die als veraltet aufgelistet sind, besteht entweder erweiterter Support oder sie haben das Ende ihrer Lebensdauer erreicht. Microsoft-Produkte und Betriebssysteme, die als veraltet aufgelistet sind, werden weiterhin mit aktuellen Versionen von Configuration Manager getestet, bis der Microsoft Support Lifecycle abgelaufen ist.  Weitere Informationen finden Sie auf der Website zu [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle) .  

 **Veraltete Features:**  


|**Feature**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt**|  
|-|-|-|  
|Netzwerkzugriffsschutz (Network Access Protection, NAP) wie in System Center 2012 Configuration Manager|10.7.2015|√|  
|Out-of-Band-Verwaltung wie in System Center 2012 Configuration Manager|16.10.2015|√|  

 **Veraltete Serverbetriebssysteme:**  

 |**Betriebssysteme**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt**|  
|-|-|-|  
|Windows Server 2008|10.7.2015|Der Support endet mit dem ersten Update, das nach dem 31.12.2016 veröffentlicht wird (siehe Hinweis 1).|  
|Windows Server 2008 R2|10.7.2015|Der Support endet mit dem ersten Update, das nach dem 31.12.2016 veröffentlicht wird (siehe Hinweis 2).|  

-   Hinweis 1:   Nach Ende des Supports wird dieses Betriebssystem nicht mehr für Standortserver bzw. die meisten Standortsystemrollen unterstützt. Es wird jedoch weiterhin für die Verwendung der Standortsystemrolle „Verteilungspunkt“ (einschließlich Pullverteilungspunkt) unterstützt, bis die Einstellung dieses Supports angekündigt wird, oder der erweiterte Support für dieses Betriebssystem abläuft.  

-   Hinweis 2:   Nach Ende des Supports wird dieses Betriebssystem nicht mehr für Standortserver bzw. die meisten Standortsystemrollen unterstützt. Es wird jedoch weiterhin für die Verwendung der Standortsystemrollen „Zustandsmigrationspunkt“ und „Verteilungspunkt“ unterstützt (einschließlich „Pullverteilungspunkt“, PXE und Multicast), bis der Support eingestellt wird oder der erweiterte Supportzeitraum für dieses Betriebssystem abläuft.  Ab Version 1602 können Sie ein direktes Upgrade des Betriebssystems eines Standortservers von Windows Server 2008 R2 auf Windows Server 2012 R2 durchführen.  

     Weitere Informationen zum direkten Upgrade des Betriebssystems eines Standortservers finden Sie im Abschnitt [In-place upgrade the operating system of site servers that run Windows Server 2008 R2 (Direktes Upgraden des Betriebssystems von Standortservern unter Windows Server 2008 R2)](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) des Themas [What's changed in System Center Configuration Manager (Neues in System Center Configuration Manager)](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



 **Veraltete Clientbetriebssysteme:**  

 Sofern nicht anders angegeben, wird jedes als Configuration Manager-Client unterstützte Betriebssystem bis zum Enddatum seines erweiterten Supports unterstützt, wie ausführlich unter [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle) beschrieben.  Wenn der Configuration Manager-Support für ein Betriebssystem vor dem Enddatum seines erweiterten Supports endet, wird hier ein Datum für das Veralten und für die Einstellung des Supports für das Betriebssystem aufgeführt.  

|**Betriebssysteme**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt**|  
|-|-|-|  
|Windows XP|10.7.2015|√|  
|Windows XP Embedded|10.7.2015|Der Support endet mit dem ersten Update, das nach dem 31.12.2016 veröffentlicht wird.|  
|Windows Server 2003|10.7.2015|√|  
|Windows Server 2003 R2|10.7.2015|√|  
|Windows Vista|10.7.2015|√|  
|Mac OS X 10.6 bis 10.8|10.7.2015|√|  
|Windows Mobile 6.0 bis 6.5|10.7.2015|√|  
|Nokia Symbian Belle|10.7.2015|√|  
|Windows CE 5.0 bis 6.0|10.7.2015|√|  


 **Veralteter Support für SQL Server-Versionen als Standortdatenbank:**  

|**SQL Server-Versionen**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt**|   
|-|-|-|  
|SQL Server 2008|10.7.2015|√|  
|SQL Server 2008 R2|10.7.2015|Der Support endet mit dem ersten Update, das nach dem 31.12.2016 veröffentlicht wird.|  

## <a name="features-removed-in-system-center-configuration-manager"></a>Aus System Center Configuration Manager entfernte Features  
 Mit dem ersten System Center Configuration Manager-Release werden folgende Features entfernt:

###  <a name="a-namebkmkamta-out-of-band-management"></a><a name="bkmk_amt"></a> Out-of-Band-Verwaltung  
 Mit Configuration Manager wurde der native Support für AMT-basierte Computer in der Configuration Manager-Konsole entfernt.  

-   AMT-basierte Computer werden vollständig verwaltet, wenn Sie das [Intel SCS-Add-On für Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)verwenden.  

-   Über das Add-On haben Sie Zugriff auf die neuesten AMT-Verwaltungsfunktionen. Gleichzeitig werden die Beschränkungen aufgehoben, die vor der Einbindung dieser Änderungen durch Configuration Manager eingeführt wurden.  

-   Die Out-Band-Verwaltung in System Center 2012 Configuration Manager ist von dieser Änderung nicht betroffen.  

###  <a name="a-namebkmknapa-network-access-protection"></a><a name="bkmk_nap"></a> Netzwerkzugriffsschutz  
 System Center Configuration Manager hat den Support für den Netzwerkzugriffsschutz eingestellt. Das Feature wurde in Windows Server 2012 R2 als veraltet markiert und aus Windows 10 entfernt.  

 Alternativen für den Netzwerkzugriffsschutz finden Sie im Abschnitt **Veraltete Funktionalität** unter [Netzwerkrichtlinien- und Zugriffsdienste: Übersicht](https://technet.microsoft.com/library/hh831683.aspx).  



<!--HONumber=Nov16_HO1-->


