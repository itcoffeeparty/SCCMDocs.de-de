---
title: Veraltete Features | Microsoft Docs
description: "Hier finden Sie Informationen zu den Features, Produkten und Betriebssystemen, die von System Center Configuration Manager nicht mehr unterstützt werden."
ms.custom: na
ms.date: 3/27/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 57b9ab13bda0bb5fa5139e52a4c55ef9524e4097
ms.contentlocale: de-de
ms.lasthandoff: 05/17/2017


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Entfernte und veraltete Features für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Thema werden Features, Produkte und Betriebssysteme beschrieben, deren Support bei System Center Configuration Manager eingestellt wird oder die bei einem zukünftigen Update entfernt werden (veraltet sind). Dies dient als frühzeitige Warnung hinsichtlich zukünftiger Änderungen, die sich auf Ihre Verwendung von Configuration Manager auswirken können.  

Diese Informationen können sich bei zukünftigen Versionen ändern und enthalten möglicherweise nicht jedes veraltete Feature, Produkt oder Betriebssystem.  

## <a name="how-to-use-this-information"></a>Verwenden dieser Informationen  
Wenn ein Feature oder Betriebssystem erstmalig als veraltet aufgeführt ist, ist die Einstellung des Supports für seine Verwendung mit Configuration Manager in einer späteren Version von Configuration Manager geplant. Diese Informationen werden bereitgestellt, damit Sie Alternativen für die Verwendung dieses Features oder Betriebssystems planen können. Bei der Veröffentlichung der ersten Version von Configuration Manager, in der der Support eingestellt wird, wird dieses Thema geändert, und die spezifische Version wird angegeben.  

Wenn der Support für ein Feature oder Betriebssystem eingestellt wird, wird das Feature oder Betriebssystem bei Verwendung einer früheren Version von Configuration Manager weiterhin unterstützt, solange der Support für diese Version von Configuration Manager weiterhin besteht. Wenn Sie jedoch eine Version von Configuration Manager verwenden, die nach dem angegebenen Datum oder der angegebenen Version veröffentlicht wurde, wird diese Version von Configuration Manager nicht unterstützt.

Beispiel: Wenn die Einstellung des Supports für ein Feature für das erste nach September 2016 veröffentliche Update geplant ist, bedeutet dies, dass der Support für das Feature im Update 1610, das im Oktober 2016 veröffentlicht wird, nicht mehr enthalten ist.
-  Mit dem Update 1610 wird das Feature nicht mehr unterstützt.
-  Dieses Thema wird dann aktualisiert und angegeben, dass der Support mit Version 1610 eingestellt wurde.
Wenn Sie aber weiterhin eine frühere Version verwenden, in der das Feature unterstützt wird, z.B. Version 1602 oder 1606, können Sie das Feature weiter verwenden, bis der Support für die verwendete Version endet.

Weitere Informationen finden Sie in folgenden Quellen:
 - Website [Microsoft Lifecycle-Richtlinie](https://support.microsoft.com/lifecycle)
 - [Support für die Current Branch-Versionen von Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)




## <a name="deprecated-operating-systems"></a>Veraltete Betriebssysteme
### <a name="server-operating-systems"></a>Serverbetriebssysteme  

|**Betriebssysteme**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt** |  
|-|-|-|  
|Windows Server 2008|10. Juli 2015|Version 1511 </br></br>Unterstützung als Standortsystem wird entfernt. (Siehe Hinweis 1).|  
|Windows Server 2008 R2|10. Juli 2015| Version 1702 (siehe Hinweis 2)|  

-   Hinweis 1: Dieses Betriebssystem wird für Standortserver oder Standortsystemrollen mit Ausnahme des Verteilungspunkts und des Pullverteilungspunkts nicht unterstützt. Sie können dieses Betriebssystem weiterhin als Verteilungspunkt verwenden, bis die Einstellung dieses Supports angekündigt wird oder der erweiterte Support für dieses Betriebssystem abläuft. Weitere Informationen finden Sie unter [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008 (Bei der Installation von System Center Configuration Manager CB und LTSB auf Windows Server 2008 tritt ein Fehler auf)](https://support.microsoft.com/help/4015095).

-   Hinweis 2: Ab Version 1702 wird dieses Betriebssystem für Standortserver und die meisten Standortsystemrollen nicht unterstützt. Alle Versionen vor 1702 unterstützen das Betriebssystem auch weiterhin. Dieses Betriebssystem wird jedoch weiterhin für die Verwendung der Standortsystemrollen „Zustandsmigrationspunkt“ und „Verteilungspunkt“ unterstützt (einschließlich „Pullverteilungspunkt“, PXE und Multicast), bis der Support eingestellt wird oder der erweiterte Supportzeitraum für dieses Betriebssystem abläuft. Ab Version 1602 können Sie ein direktes Upgrade des Betriebssystems eines Standortservers von Windows Server 2008 R2 auf Windows Server 2012 R2 durchführen.  

     Weitere Informationen zum direkten Upgrade des Betriebssystems eines Standortservers finden Sie im Abschnitt [In-place upgrade the operating system of site servers that run Windows Server 2008 R2 (Direktes Upgraden des Betriebssystems von Standortservern unter Windows Server 2008 R2)](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) des Themas [What's changed in System Center Configuration Manager (Neues in System Center Configuration Manager)](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



### <a name="client-operating-systems"></a>Clientbetriebssysteme  

 Sofern nicht anders angegeben, wird jedes als Configuration Manager-Client unterstütztes Betriebssystem bis zum Enddatum seines erweiterten Supports unterstützt. Weitere Informationen zu den Enddaten des erweiterten Supports finden Sie unter [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). Wenn der Configuration Manager-Support für ein Betriebssystem vor dem Enddatum seines erweiterten Supports endet, wird hier ein Datum für das Veralten und für die Einstellung des Supports für das Betriebssystem aufgeführt.  

|**Betriebssysteme**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt**|  
|-|-|-|  
|Windows XP|10. Juli 2015|Version 1511|  
|Windows XP Embedded|10. Juli 2015|Version 1702|  
|Windows Server 2003|10. Juli 2015|Version 1511|  
|Windows Server 2003 R2|10. Juli 2015|Version 1511|  
|Windows Vista|10. Juli 2015|Version 1511|  
|Mac OS X 10.6 bis 10.8|10. Juli 2015|Version 1511|  
|Windows Mobile 6.0 bis 6.5|10. Juli 2015|Version 1511|  
|Nokia Symbian Belle|10. Juli 2015|Version 1511|  
|Windows CE 5.0 bis 6.0|10. Juli 2015|Version 1511|  


## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Veralteter Support für SQL Server-Versionen als Standortdatenbank  

|**SQL Server-Versionen**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt**|   
|-|-|-|  
|SQL Server 2008|10. Juli 2015|Version 1511|  
|SQL Server 2008 R2|10. Juli 2015|Version 1702|  

Wenn Sie Ihre Version von SQL Server aktualisieren müssen, werden folgende Methoden in der Reihenfolge ihrer Komplexität empfohlen.
1. [Direktes Upgrade von SQL Server](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (empfohlen).
2. Installieren Sie eine neue Version von SQL Server auf einem neuen Computer, und [verwenden Sie die Option „Datenbankverschiebung“](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) von Configuration Manager-Setup, um Ihren Standortserver auf den neuen SQL Server auszurichten.
3. Verwenden Sie [Sicherung und Wiederherstellung](/sccm/protect/understand/backup-and-recovery).


## <a name="deprecated-features"></a>Veraltete Features  

|**Feature**|**Erste Ankündigung als veraltetes Feature**|**Support eingestellt**|  
|-|-|-|  
|Netzwerkzugriffsschutz (Network Access Protection, NAP) wie in System Center 2012 Configuration Manager|10. Juli 2015|Version 1511|  
|Out-of-Band-Verwaltung wie in System Center 2012 Configuration Manager|16. Oktober 2015|Version 1511|
|Tasksequenzen: <br /> – OSDPreserveDriveLetter  <br /><br /> Während einer standardmäßigen Betriebssystembereitstellung bestimmt Windows Setup den Laufwerkbuchstaben, der am besten zur Verwendung geeignet ist (in der Regel C:). Wenn Sie ein anderes Laufwerk zur Verwendung angeben möchten, können Sie den Speicherort im Tasksequenzschritt „Betriebssystem anwenden“ ändern. Wechseln Sie zur Einstellung **Wählen Sie den Standort aus, an dem Sie dieses Betriebssystem anwenden möchten.**, wählen Sie **Bestimmter Buchstabe für logisches Laufwerk ** aus und wählen Sie das Laufwerk aus, das Sie verwenden möchten. |20. Juni 2016 |Version 1606 |
|Tasksequenzen: <br /> - In dynamischen Datenträger konvertieren <br /> - Bereitstellungstools installieren |18. November 2016|Der Support für diese Tasksequenzen endet mit dem ersten Update, das nach dem 1. Juni 2017 veröffentlicht wird.|
|Das Softwarecenter erhält ein neues, modernes Aussehen. Apps, die bisher nur im von Silverlight abhängigen Anwendungskatalog angezeigt wurden (für Benutzer verfügbare Apps), werden jetzt im Softwarecenter auf der Registerkarte **Anwendungen** angezeigt. Auf den Anwendungskatalog kann weiterhin über den Link auf der Registerkarte **Installationsstatus** im Softwarecenter zugegriffen werden.<br><br>In den kommenden Monaten wird die vorherige Version des Softwarecenters nicht länger zur Verfügung stehen.<br><br>Sie können Clients für die Verwendung des neuen Softwarecenters konfigurieren, indem Sie die Clienteinstellung **Computer-Agent** > **Neues Softwarecenter verwenden** aktivieren.<br><br>Weitere Informationen zum Softwarecenter finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung in System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13. Dezember 2016|Wird bekanntgegeben|
|Verwaltung von virtuellen Festplatten (VHDs) mit Configuration Manager. </br></br>Dies schließt das Entfernen von Optionen zum Erstellen einer neuen virtuellen Festplatte oder Verwalten einer virtuellen Festplatte mithilfe einer Tasksequenz und das Entfernen des Knotens „Virtuelle Festplatten“ über die Configuration Manager-Konsole ein. </br></br>Wenn dieser Support eingestellt wird, werden vorhandene virtuelle Festplatten nicht gelöscht, es kann aber nicht mehr in der Configuration Manager-Konsole darauf zugegriffen werden.  |6. Januar 2017 |Der Support für virtuelle Festplatten endet mit dem ersten Update, das nach dem 1. Juni 2017 veröffentlicht wird.|
|System Center Configuration Manager-Upgradebewertungstool </br></br>Das Upgradebewertungstool ist sowohl von System Center Configuration Manager als auch vom Anwendungskompatibilitäts-Toolkit (Application Compatibility Toolkit, ACT) 6.x abhängig. Die letzte Version von ACT war im Windows 10 v1511 ADK enthalten. Da es keine weiteren Updates für ACT geben wird, wird auch der entsprechende Support für das Upgradebewertungstool eingestellt. </br></br>Das Upgradebewertungstool wird durch das Feature [Upgradebereitschaft](/sccm/core/clients/manage/upgrade/upgrade-analytics) ersetzt. Hinweise zu veralteten Funktionen wurden am 9. Dezember 2016 auf der [Downloadseite des Upgradebewertungstools](https://www.microsoft.com/download/details.aspx?id=37145) hinzugefügt. |9. Dezember 2016  | 11. Juli 2017 |  


<br></br>
Zusätzliche Informationen zu Features, die mit Version 1511 der System Center Configuration Manager-Version entfernt wurden:

###  <a name="bkmk_amt"></a> Out-of-Band-Verwaltung  
 Mit Configuration Manager wurde der native Support für AMT-basierte Computer in der Configuration Manager-Konsole entfernt.  

-   AMT-basierte Computer werden weiterhin vollständig verwaltet, wenn Sie das [Intel SCS-Add-On für Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html) verwenden. Über das Add-On haben Sie Zugriff auf die neuesten AMT-Verwaltungsfunktionen. Gleichzeitig werden die Beschränkungen aufgehoben, die vor der Einbindung dieser Änderungen durch Configuration Manager eingeführt wurden.  

-   Die Out-Band-Verwaltung in System Center 2012 Configuration Manager ist von dieser Änderung nicht betroffen.  

###  <a name="bkmk_nap"></a> Netzwerkzugriffsschutz  
 System Center Configuration Manager hat den Support für den Netzwerkzugriffsschutz eingestellt. Das Feature wurde in Windows Server 2012 R2 als veraltet markiert und aus Windows 10 entfernt.  

 Alternativen für den Netzwerkzugriffsschutz finden Sie im Abschnitt *Veraltete Funktionalität* unter [Netzwerkrichtlinien- und Zugriffsdienste: Übersicht](https://technet.microsoft.com/library/hh831683.aspx).

