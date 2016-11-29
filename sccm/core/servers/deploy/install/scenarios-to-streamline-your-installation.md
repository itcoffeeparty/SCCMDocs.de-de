---
title: Installationsszenarios | System Center Configuration Manager
description: "Lernen Sie Verfahren für die Installation einer neuen Configuration Manager-Hierarchie kennen, wenn Sie ein Update oder ein Upgrade durchführen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 90a802cbdfd6d0acd60ec462ffbf2a08c012eaeb


---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>Szenarien für die Optimierung Ihrer Installation von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit dem Release von Updateversionen für System Center Configuration Manager (Current Branch) gibt es neue Szenarios für die Optimierung der Installation einer neuen Hierarchie mit einer Updateversion (wie Update 1602) und für ein Upgrade von Microsoft System Center 2012 Configuration Manager.  

Unterstützte Szenarien:  

**Installieren einer neuen System Center Configuration Manager-Hierarchie (Current Branch)**, in der eine Updateversion ausgeführt wird:  

-   Sie installieren nur den Standort auf oberster Ebene und unmittelbar danach ein Update, um diesen Standort mit der gewünschten Updateversion zu versehen. Anschließend können Sie zusätzliche Standorte direkt mit dieser Updateversion installieren.  

-   Bei diesem Szenario wird das Installieren zusätzlicher Standorte auf einer Baselinestufe übersprungen, die dann anschließend auf die gewünschte Updateversion aktualisiert werden müssen.  

-   Dieses Szenario überspringt die Installation von Clients mit einer Baselineversion, die dann anschließend neu installiert werden müssen, wenn Sie ein Update auf eine spätere Version durchführen.  

**Upgrade von System Center 2012 Configuration Manager** auf eine Updateversion von System Center Configuration Manager:  

-   Sie aktualisieren Ihren Standort der zentralen Verwaltung und alle primären Standorte auf eine Baselineversion (wie 1511), bevor Sie eine Updateversion (wie 1602) installieren können.  

-   Sie führen erst dann ein Upgrade für sekundäre Standorte von Microsoft System Center 2012 Configuration Manager durch, wenn Ihre primären Standorte die gewünschte Updateversion ausführen.  

-   Sie führen erst dann ein Upgrade für Clients von Microsoft System Center 2012 Configuration Manager durch, wenn Ihre primären Standorte die gewünschte Updateversion ausführen.  

## <a name="scenario---install-a-new-hierarchy-to-an-update-version"></a>Szenario – Installieren einer neuen Hierarchie mit einer Updateversion  
In diesem Beispielszenario installieren Sie den ersten Standort einer Hierarchie mit einer Baselineversion von System Center Configuration Manager, Version 1511. Danach installieren Sie das Update 1602, bevor Sie zusätzliche Standorte oder Clients bereitstellen.  

-   Da Sie planen, eine Updateversion (z. B. 1602) zu verwenden, und keine Baselineversion (z. B. 1511) beibehalten wollen, müssen Sie keine zusätzliche Standorte installieren und diese dann aktualisieren oder Clients installieren und dann aktualisieren.  

-   Sie installieren keine sekundären Standorte mit Version 1511, die Sie dann auf 1602 aktualisieren. Stattdessen installieren Sie sie, sobald Ihre primären Standorte Version 1602 ausführen.  

**Verwenden Sie die folgende Schrittfolge:**  

1.  **Installieren Sie einen Standort auf oberster Ebene für Ihre neue Hierarchie** mithilfe der Baselinemedien.  

    -   Mithilfe der Baselinemedien kann nur der erste Standort einer neuen Hierarchie installiert werden.  

    -   Installieren Sie beispielsweise einen Standort auf oberster Ebene mit der Baselineversion 1511. Weitere Informationen finden Sie unter [Use the Setup Wizard to install sites (Verwenden des Setup-Assistenten zum Installieren von Standorten)](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)  

    Nach diesem Schritt wird der Standort auf oberster Ebene mit Version 1511 ausgeführt.  

2.  **Verwenden Sie Updates in der Konsole, um Ihren Standort auf oberster Ebene auf eine spätere Version zu aktualisieren.**  

    -   Vor der Installation untergeordneter Standorte oder Clients aktualisieren Sie Ihren Standort auf oberster Ebene in die Updateversion, die Sie verwenden möchten.  

    -   Beispielsweise können Sie Ihren Standort auf oberster Ebene mit Version 1511 auf Version 1602 aktualisieren. Informationen hierzu finden Sie unter [Updates für System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

    Nach diesem Schritt wird der Standort auf oberster Ebene mit Version 1602 ausgeführt.  

3.  **Installieren Sie neue untergeordnete Standorte unter einem Standort der zentralen Verwaltung.**  

    -   Verwenden Sie das Installationsmedium im Ordner „CD.Latest“ auf dem Standortserver der zentralen Verwaltung, um untergeordnete primäre Standorte zu installieren.  (Siehe [Der Ordner „CD.Latest“ für System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md))  

        -   Dieses Quellmedium ist erforderlich, um sicherzustellen, dass neue untergeordnete primäre Standorte der Version des Standorts der zentralen Verwaltung entsprechen.  

    Nach diesem Schritt führen Ihre neuen untergeordneten primären Standorte Version 1602 aus.  

4.  **Verwenden Sie an jedem primären Standort die Option in der Konsole, um neue sekundäre Standorte zu installieren.**  

    -   Da Sie keine sekundären Standorte installiert haben, als die primären Standorte Version 1511 aufwiesen, müssen Sie für die sekundären Standorte kein Upgrade durchführen.  

    -   Stattdessen installieren Sie neue sekundäre Standorte, die Version 1602 ausführen. Weitere Informationen finden Sie unter *Installieren eines sekundären Standorts* in [Use the Setup Wizard to install sites (Verwenden des Setup-Assistenten zum Installieren von Standorten)](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

    Nach diesem Schritt werden neue sekundäre Standorte installiert, die Version 1602 ausführen.  

5.  **Installieren Sie neue Clients am primären Standort.**  

    -   Da Sie keine Clients installiert haben, als die primären Standorte Version 1511 aufwiesen, müssen Sie für die Clients kein Upgrade von 1511 auf 1602 durchführen.  

    -   Stattdessen installieren Sie neue Clients, die Version 1602 ausführen. Informationen hierzu finden Sie unter [Bereitstellen von Clients in System Center Configuration Manager](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

    Nach diesem Schritt werden neue Clients installiert, die Version 1602 ausführen.  

## <a name="scenario---upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>Szenario: Aktualisieren von System Center 2012 Configuration Manager auf eine Updateversion von System Center Configuration Manager (Current Branch)  
In diesem Beispielszenario führen Sie für Ihre System Center 2012 Configuration Manager-Infrastruktur ein Upgrade auf eine Updateversion von System Center Configuration Manager durch, z.B. Version 1602.  

-   Der Standort der zentralen Verwaltung und alle primären Standorte müssen auf die Baselineversion 1511 aktualisiert werden, ehe Sie das Update für Version 1602 installieren.  

-   Für sekundäre Standorte und Clients erfolgt kein Upgrade auf bzw. keine Installation von Version 1511. Stattdessen werden sie direkt von Microsoft System Center 2012 Configuration Manager auf System Center Configuration Manager Version 1602 aktualisiert.  

**Verwenden Sie die folgende Schrittfolge:**  

1.  **Führen Sie für den Microsoft System Center 2012 Configuration Manager-Standort der obersten Ebene ein Upgrade** auf eine Baselineversion (Current Branch) durch, indem Sie Quellmedien für System Center Configuration Manager (wie Version 1511) verwenden. Informationen hierzu finden Sie unter [Upgrade to System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) (Upgrade auf System Center Configuration Manager).  

    -   Wie bei herkömmlichen Upgradeszenarien aktualisieren Sie stets zuerst den Standort auf oberster Ebene einer Hierarchie und anschließend untergeordnete Standorte.  

    Nach diesem Schritt wird der Standort auf oberster Ebene mit Version 1511 ausgeführt.  

2.  **Upgraden Sie jeden untergeordneten primären Standort in Ihrer Hierarchie** ebenfalls auf diese Baselineversion.  

    -   Wenn Sie ein Upgrade von Microsoft System Center 2012 Configuration Manager durchführen, müssen Sie für jeden primären Standort manuell ein Upgrade auf eine Baselineversion von Current Branch durchführen.  

    -   Zu diesem Zeitpunkt aktualisieren Sie keine sekundären Standorte.  

    Nach diesem Schritt wird an jedem primären Standort Version 1511 ausgeführt.  

3.  **Legen Sie Wartungsfenster für untergeordnete primäre Standorte fest.** Nach dem Upgrade aller primären Standorte auf die Baselineversion planen Sie die Konfiguration von Wartungsfenstern, um zu steuern, wann für diese Standorte Infrastruktur-Updates installiert werden sollen. Informationen hierzu finden Sie unter [Verwenden von Wartungsfenstern in System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).  (Wartungsfenster werden in Version 1511 als Servicezeitfenster bezeichnet.)  

    -   Ein untergeordneter primärer Standort installiert automatisch dieselben Updates, die Sie an einem Standort der zentralen Verwaltung installieren.  

    -   An sekundären Standorten werden neue Versionen nicht automatisch installiert, weshalb diese in der Konsole manuell aktualisiert werden müssen.  

    > [!NOTE]  
    >  Wenn Sie Version 1511 nutzen und Servicezeitfenster verwenden möchten, müssen Sie zunächst den Hotfix aus dem [Microsoft Knowledge Base-Artikel 3142341](http://support.microsoft.com/kb/3142341)installieren. Dieses Problem wird durch Installation des Updates 1602 behoben.  

    Wenn Sie nach diesem Schritt Updates am Standort der zentralen Verwaltung installieren, installieren untergeordnete primäre Standorte dieses Update, sobald ihr Wartungsfenster es zulässt.  

4.  **Installieren Sie die Updateversion am Standort auf oberster Ebene.** Dadurch wird der Standort auf oberster Ebene aktualisiert. Nachdem die Updateversion am Standort der zentralen Verwaltung installiert wurde, wird an allen untergeordneten primären Standorten das Update automatisch installiert, es sei denn, dies wird durch ein Wartungsfenster verhindert.  

    -   Beispielsweise können Sie Ihren Standort auf oberster Ebene von Version 1511 auf Version 1602 aktualisieren. Informationen hierzu finden Sie unter [Updates für System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

    Nach diesem Schritt wird an Ihrem Standort der zentralen Verwaltung und allen primären Standorten Version 1602 ausgeführt.  

5.  **Führen Sie ein Upgrade sekundärer Standorten durch.** Sobald an einem primären Standort das Update installiert wurde und Version 1602 ausgeführt wird, können Sie mithilfe der Option in der Konsole sekundäre Standorte aktualisieren.  

    -   Dabei werden sekundäre Standorte direkt von Microsoft System Center 2012 Configuration Manager auf die Updateversion upgegradet, die Sie am primären Standort installiert haben.  

    -   Weitere Informationen zum Upgraden eines sekundären Standorts finden Sie unter [Upgrade sites](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) (Upgraden von Standorten) in [Upgrade to System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) (Aktualisieren auf System Center Configuration Manager).  

6.  **Aktualisieren von Clients** Verwenden Sie die Informationen unter [Aktualisieren von Clients für Windows-Computer in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

    -   Dabei werden Clients direkt von Microsoft System Center 2012 Configuration Manager auf die Updateversion upgegradet, die Sie am primären Standort installiert haben.  

    Nach diesem Schritt werden die Clients auf Version 1602 aktualisiert, ohne dass zuvor ein Upgrade auf Version 1511 erfolgt.



<!--HONumber=Nov16_HO1-->


