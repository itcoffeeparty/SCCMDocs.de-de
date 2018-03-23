---
title: Voraussetzungen für Softwareupdates
titleSuffix: Configuration Manager
description: Hier finden Sie Informationen über die Voraussetzungen für Softwareupdates in System Center Configuration Manager.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 02/02/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: f64647447d206a2dd53e300b143e79719cf516c5
ms.sourcegitcommit: 52080ef1b0f9a27c123711ef274ac3ffe070e8e0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>Voraussetzungen für Softwareupdates in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Artikel werden die Voraussetzungen für Softwareupdates in System Center Configuration Manager beschrieben. Die externen und internen Abhängigkeiten sind jeweils in separaten Tabellen aufgeführt.  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Externe Softwareupdateabhängigkeiten von Configuration Manager  
 In den folgenden Abschnitten sind die externen Abhängigkeiten für Softwareupdates aufgeführt.  

### <a name="internet-information-services"></a>Internetinformationsdienste  
 Die Internetinformationsdienste (Internet Information Services, IIS) müssen zum Ausführen von Softwareupdatepunkt, Verwaltungspunkt und Verteilungspunkt auf den Standortsystemservern installiert sein. Weitere Informationen finden Sie unter [Prerequisites for site system roles (Voraussetzungen für Standortsystemrollen)](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 WSUS (Windows Server Update Services) ist zur Synchronisierung von Softwareupdates und für die Anwendbarkeit von Softwareupdates auf Clients erforderlich. Der WSUS-Server muss installiert werden, bevor Sie die Rolle „Softwareupdatepunkt“ erstellen können. Für einen Softwareupdatepunkt werden die folgenden Versionen von WSUS unterstützt:  

-   WSUS 10.0 (Rolle in Windows Server 2016)
-   WSUS 6.2 und 6.3 (Rolle in Windows Server 2012 und Windows Server 2012 R2)  
-   WSUS 3.2 (Rolle in Windows Server 2008 R2)  

Stellen Sie bei Verwendung mehrerer Softwareupdatepunkte an einem Standort sicher, dass jeweils die gleiche WSUS-Version ausgeführt wird.  

> [!WARNING]  
>  Die Klassifizierung **Upgrades** für Softwareupdates wird erst ab WSUS 4.0 unterstützt. Bevor Sie diese neue Klassifizierung synchronisieren und Windows 10-Computer in einem Windows 10-Wartungsplan evaluieren können, müssen Sie den [Hotfix 3095113](https://support.microsoft.com/kb/3095113) für WSUS auf Ihren Softwareupdatepunkten und Standortservern installieren. Dieser Hotfix aktiviert WSUS auf einem Windows Server 2012- oder Windows Server 2012 R2-basierten Server, um Featureupgrades für Windows 10 zu synchronisieren und zu verteilen. Weitere Informationen finden Sie unter [Manage Windows as a service (Verwalten von Windows as a Service)](../../osd/deploy-use/manage-windows-as-a-service.md).  
>   
>  Wenn Sie Softwareupdates mit der Klassifikation **Upgrades** synchronisieren, bevor Sie [Hotfix 3095113](https://support.microsoft.com/kb/3095113)installieren, gehen Sie zu [Wiederherstellen nach Synchronisieren der Kategorie „Upgrades“ vor der Installation von KB 3095113](#BKMK_RecoverUpgrades)aufgeführt.  

### <a name="wsus-administration-console"></a>WSUS-Verwaltungskonsole  
 Die WSUS-Verwaltungskonsole wird auf dem Configuration Manager-Standortserver benötigt, wenn sich der Softwareupdatepunkt auf einem Remote-Standortsystemserver befindet und auf dem Standortserver noch keine WSUS-Installation vorhanden ist.  

> [!IMPORTANT]  
> Die WSUS-Version auf dem Standortserver muss der WSUS-Version entsprechen, die auf den Softwareupdatepunkten ausgeführt wird.
>
> Verwenden Sie nicht die WSUS-Verwaltungskonsole zum Konfigurieren der WSUS-Einstellungen. Configuration Manager stellt eine Verbindung mit der WSUS-Instanz auf dem Softwareupdatepunkt her, und die entsprechenden Einstellungen werden konfiguriert.  



### <a name="windows-update-agent"></a>Windows Update-Agent  
 Der Client vom Windows Update-Agent (WUA) ist auf Clients erforderlich, damit sie eine Verbindung mit dem WSUS-Server herstellen können. WUA ruft die Liste der Softwareupdates ab, die auf Konformität überprüft werden müssen.  

 Während der Installation von Configuration Manager wird die aktuelle WUA-Version heruntergeladen. Bei Bedarf wird für WUA ein Upgrade ausgeführt, wenn Sie den Configuration Manager-Client installieren. Wenn bei der Installation jedoch Fehler auftreten, müssen Sie ein anderes Verfahren zum Ausführen des WUA-Upgrades verwenden.  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Interne Softwareupdateabhängigkeiten von Configuration Manager  
 In der folgenden Abschnitten sind die internen Abhängigkeiten für Softwareupdates in Configuration Manager aufgeführt.  

### <a name="management-points"></a>Verwaltungspunkte  
 Informationen zwischen Clientcomputern und dem Configuration Manager-Standort werden über Verwaltungspunkte übertragen. Diese Verwaltungspunkte sind für Softwareupdates erforderlich.  

### <a name="software-update-points"></a>Softwareupdatepunkte  
 Sie müssen einen Softwareupdatepunkt auf dem WSUS-Server installieren, um Softwareupdates in Configuration Manager bereitzustellen. Weitere Informationen finden Sie unter [Install and configure a software update point (Installieren und Konfigurieren eines Softwareupdatepunkts)](../get-started/install-a-software-update-point.md).

### <a name="distribution-points"></a>Verteilungspunkte  
 Verteilungspunkte sind erforderlich, um den Inhalt für Softwareupdates zu speichern. Weitere Informationen zum Installieren von Verteilungspunkten und Verwalten von Inhalt finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="client-settings-for-software-updates"></a>Clienteinstellungen für Softwareupdates  
 Standardmäßig sind Softwareupdates für Clients aktiviert. Es stehen jedoch noch weitere Einstellungen zur Verfügung, mit denen gesteuert wird, wie und wann von Clients die Kompatibilität für die Softwareupdates überprüft wird und wie die Softwareupdates installiert werden.  

 Weitere Informationen finden Sie in den folgenden Artikeln:  

-   [Clienteinstellungen für Softwareupdates](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

-   [Softwareupdates-Clienteinstellungen](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Reporting Services-Punkte  
 Mithilfe der Standortsystemrolle Reporting Services-Punkt können Berichte für Softwareupdates angezeigt werden. Diese Rolle ist optional. Ihre Verwendung wird jedoch empfohlen. Weitere Informationen zum Erstellen eines Reporting Services-Punkts finden Sie unter [Konfigurieren der Berichterstellung](../../core/servers/manage/configuring-reporting.md).  

##  <a name="BKMK_RecoverUpgrades"></a> Wiederherstellen nach Synchronisieren der Kategorie „Upgrades“ vor der Installation von KB 3095113  
 Sie müssen [Hotfix 3095113](https://support.microsoft.com/kb/3095113) für WSUS auf Ihren Softwareupdatepunkten und Standortservern installieren, bevor Sie die Klassifikation **Upgrades** synchronisieren. Wenn der Hotfix zum Zeitpunkt der Aktivierung der Klassifizierung **Upgrades** nicht installiert ist, wird das Funktionsupgrade Windows 10 Build 1511 für WSUS angezeigt, WSUS kann die zugehörigen Pakete allerdings nicht ordnungsgemäß herunterladen und bereitstellen. 
 
 Wenn Sie Upgrades synchronisieren, ohne zuerst den [Hotfix 3095113](https://support.microsoft.com/kb/3095113) installiert zu haben, füllen Sie die WSUS-Datenbank (SUSDB) mit unbrauchbaren Daten auf. Diese Daten müssen gelöscht werden, bevor Upgrades ordnungsgemäß bereitgestellt werden können. Verwenden Sie das folgende Verfahren, um dieses Problem zu beheben.  

#### <a name="to-recover-from-synchronizing-the-upgrades-classification-before-you-install-kb-3095113"></a>Wiederherstellen nach Synchronisieren der Klassifizierung „Upgrades“ vor der Installation von KB 3095113  

1.  Löschen Sie Softwareupdates mit der Klassifizierung **Upgrades**. Sie können ein PowerShell-Skript ähnlich dem folgenden Beispielskript verwenden:  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  Sie müssen das Skript auf allen Softwareupdatepunkten in Ihrer Configuration Manager-Hierarchie ausführen, bevor Sie mit dem nächsten Schritt fortfahren.  

     Zum Löschen von Softwareupdates mit der Klassifizierung **Upgrades** per Massenvorgang, können Sie das PowerShell-Skript so ändern, dass mehrere GUIDs aus einer Textdatei gelesen werden.  

2.  Deaktivieren Sie die **Upgrades**-Klassifizierung in den Eigenschaften der Softwareupdatepunkt-Komponente. (Weitere Informationen finden Sie unter [Konfigurieren von Klassifizierungen und Produkten](../get-started/configure-classifications-and-products.md).) Initiieren Sie dann die Softwareupdatesynchronisierung. (Weitere Informationen finden Sie unter [Synchronisieren von Softwareupdates](../get-started/synchronize-software-updates.md).)  

3.  Installieren Sieieren Sie [Hotfix 3095113](https://support.microsoft.com/kb/3095113) für WSUS auf Ihren Softwareupdatepunkten und Standortservern installieren.  

4.  Wählen Sie die **Upgrades**-Klassifizierung in den Softwareupdatepunkt-Komponenteneigenschaften aus. (Weitere Informationen finden Sie unter [Konfigurieren von Klassifizierungen und Produkten](../get-started/configure-classifications-and-products.md).) Initiieren Sie dann die Softwareupdatesynchronisierung. (Weitere Informationen finden Sie unter [Synchronisieren von Softwareupdates](../get-started/synchronize-software-updates.md).)  

## <a name="next-steps"></a>Nächste Schritte
[Vorbereiten der Softwareupdateverwaltung](../get-started/prepare-for-software-updates-management.md)
