---
title: Veraltete Features | Microsoft Docs
description: "Hier finden Sie Informationen zu den Features, Produkten und Betriebssystemen, die von System Center Configuration Manager nicht mehr unterstützt werden."
ms.custom: na
ms.date: 12/05/2016
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
ms.sourcegitcommit: ffebee1e85008611a9841dc849bea735d15a88c6
ms.openlocfilehash: 888b6de9fd2b70e8b4f58e32cca7cf5e615d1dca


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Entfernte und veraltete Features für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Thema werden Features, Produkte und Betriebssysteme beschrieben, deren Support bei System Center Configuration Manager eingestellt wird oder die bei einem zukünftigen Update entfernt werden (veraltet sind). Dies dient als frühzeitige Warnung hinsichtlich zukünftiger Änderungen, die sich auf Ihre Verwendung von Configuration Manager auswirken können.  

 Diese Informationen können sich bei zukünftigen Versionen ändern und enthalten möglicherweise nicht jedes veraltete Feature, Produkt oder Betriebssystem.  

## <a name="how-to-use-this-information"></a>Verwenden dieser Informationen  
Wenn ein Feature oder Betriebssystem erstmalig als veraltet aufgeführt ist, ist die Einstellung des Supports für seine Verwendung mit Configuration Manager in einer späteren Version von Configuration Manager geplant. Diese Informationen werden bereitgestellt, damit Sie Alternativen für die Verwendung dieses Features oder Betriebssystems planen können.  Bei der Veröffentlichung der ersten Version von Configuration Manager, in der der Support eingestellt wird, werden die Informationen in diesem Thema geändert, und die spezifische Version wird angegeben.  

Wenn der Support für ein Feature oder Betriebssystem eingestellt wird, wird das Feature oder Betriebssystem bei Verwendung einer früheren Version von Configuration Manager weiterhin unterstützt, solange der Support für diese Version von Configuration Manager weiterhin besteht. Wenn Sie jedoch eine Version von Configuration Manager verwenden, die nach dem angegebenen Datum oder der angegebenen Version veröffentlicht wurde, wird diese Version von Configuration Manager nicht unterstützt.

**Beispiel:** Wenn die Einstellung des Supports für ein Feature für das erste nach September 2016 veröffentliche Update geplant ist, bedeutet dies, dass der Support für das Feature im Update 1610, das im Oktober 2016 veröffentlicht wurde, nicht mehr enthalten ist.
-  Mit dem Update 1610 wird das Feature nicht mehr unterstützt.
-  Im aktualisierten Inhalt dieses Themas wird angegeben, dass der Support mit Version 1610 eingestellt wurde.
Wenn Sie aber weiterhin eine frühere Version verwenden, in der das Feature unterstützt wird, z.B. Version 1602 oder 1606, können Sie das Feature weiter verwenden, bis der Support für die verwendete Version endet.

Weitere Informationen finden Sie in folgenden Quellen:
 - Website [Microsoft Lifecycle-Richtlinie](https://support.microsoft.com/lifecycle)
 - [Support für die Current Branch-Versionen von Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)

**Veraltete Features:**  


|**Feature**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt**|  
|-|-|-|  
|Netzwerkzugriffsschutz (Network Access Protection, NAP) wie in System Center 2012 Configuration Manager|10.7.2015|Version 1511|  
|Out-of-Band-Verwaltung wie in System Center 2012 Configuration Manager|16.10.2015|Version 1511|
|Tasksequenzen: <br /> - In dynamischen Datenträger konvertieren <br /> - Bereitstellungstools installieren |18.11.2016|Der Support für diese Tasksequenzen endet mit dem ersten Update, das nach dem 1. Juni 2017 veröffentlicht wird.|
|Das neue Softwarecenter weist einen neuen, modernen Look auf, und Apps, die bisher nur im von Silverlight abhängigen Anwendungskatalog angezeigt wurden (für Benutzer verfügbare Apps), werden jetzt im Softwarecenter auf der Registerkarte **Anwendungen** angezeigt. Auf den Anwendungskatalog kann weiterhin über den Link unter der Registerkarte **Installationsstatus** im Softwarecenter zugegriffen werden.<br><br>In den kommenden Monaten wird die vorherige Version des Softwarecenters entfernt, und sie wird Ihnen nicht länger zur Verfügung stehen.<br><br>Sie können Clients für die Verwendung des neuen Softwarecenters konfigurieren, indem Sie die Clienteinstellung **Computer-Agent** > **Neues Softwarecenter verwenden**.<br><br>Weitere Informationen zum Softwarecenter finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung in System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|12/13/2016|Wird bekanntgegeben| 

 **Veraltete Serverbetriebssysteme:**  

 |**Betriebssysteme**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt** |  
|-|-|-|  
|Windows Server 2008|10.7.2015|Der Support endet mit dem ersten Update, das nach dem 31.12.2016 veröffentlicht wird *(siehe Hinweis 1)*.|  
|Windows Server 2008 R2|10.7.2015|Der Support endet mit dem ersten Update, das nach dem 31.12.2016 veröffentlicht wird *(siehe Hinweis 2)*.|  

-   *Hinweis 1:* Nach Ende des Supports wird dieses Betriebssystem nicht mehr für Standortserver bzw. die meisten Standortsystemrollen unterstützt. Es wird jedoch weiterhin für die Verwendung der Standortsystemrolle „Verteilungspunkt“ (einschließlich Pullverteilungspunkt) unterstützt, bis die Einstellung dieses Supports angekündigt wird, oder der erweiterte Support für dieses Betriebssystem abläuft.  

-   *Hinweis 2:* Nach Ende des Supports wird dieses Betriebssystem nicht mehr für Standortserver bzw. die meisten Standortsystemrollen unterstützt. Es wird jedoch weiterhin für die Verwendung der Standortsystemrollen „Zustandsmigrationspunkt“ und „Verteilungspunkt“ unterstützt (einschließlich „Pullverteilungspunkt“, PXE und Multicast), bis der Support eingestellt wird oder der erweiterte Supportzeitraum für dieses Betriebssystem abläuft.  Ab Version 1602 können Sie ein direktes Upgrade des Betriebssystems eines Standortservers von Windows Server 2008 R2 auf Windows Server 2012 R2 durchführen.  

     Weitere Informationen zum direkten Upgrade des Betriebssystems eines Standortservers finden Sie im Abschnitt [In-place upgrade the operating system of site servers that run Windows Server 2008 R2 (Direktes Upgraden des Betriebssystems von Standortservern unter Windows Server 2008 R2)](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) des Themas [What's changed in System Center Configuration Manager (Neues in System Center Configuration Manager)](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



 **Veraltete Clientbetriebssysteme:**  

 Sofern nicht anders angegeben, wird jedes als Configuration Manager-Client unterstützte Betriebssystem bis zum Enddatum seines erweiterten Supports unterstützt, wie ausführlich unter [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle) beschrieben.  Wenn der Configuration Manager-Support für ein Betriebssystem vor dem Enddatum seines erweiterten Supports endet, wird hier ein Datum für das Veralten und für die Einstellung des Supports für das Betriebssystem aufgeführt.  

|**Betriebssysteme**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt**|  
|-|-|-|  
|Windows XP|10.7.2015|Version 1511|  
|Windows XP Embedded|10.7.2015|Der Support endet mit dem ersten Update, das nach dem 31.12.2016 veröffentlicht wird.|  
|Windows Server 2003|10.7.2015|Version 1511|  
|Windows Server 2003 R2|10.7.2015|Version 1511|  
|Windows Vista|10.7.2015|Version 1511|  
|Mac OS X 10.6 bis 10.8|10.7.2015|Version 1511|  
|Windows Mobile 6.0 bis 6.5|10.7.2015|Version 1511|  
|Nokia Symbian Belle|10.7.2015|Version 1511|  
|Windows CE 5.0 bis 6.0|10.7.2015|Version 1511|  


 **Veralteter Support für SQL Server-Versionen als Standortdatenbank:**  

|**SQL Server-Versionen**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt**|   
|-|-|-|  
|SQL Server 2008|10.7.2015|Version 1511|  
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



<!--HONumber=Dec16_HO3-->


