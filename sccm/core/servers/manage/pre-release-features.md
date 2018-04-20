---
title: Features der Vorabversion
titleSuffix: Configuration Manager
description: Features der Vorabversion sind Features, die in Current Branch enthalten sind, um sie in einem frühen Stadium in einer Produktionsumgebung zu testen.
ms.custom: na
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: 36
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e3a6a8dd437238a9dd08b07494b51333283f41c
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>Features der Vorabversion in System Center Configuration Manager
*Gilt für: System Center Configuration Manager (Current Branch)*

Features der Vorabversion sind Features, die in Current Branch enthalten sind, um sie in einem frühen Stadium in einer Produktionsumgebung zu testen. Diese Features werden vollständig unterstützt, unterliegen aber noch der Entwicklung und könnten möglicherweise geändert werden, bis sie die Vorabversionskategorie verlassen.

 Bevor Sie Features der Vorabversion verwenden können, müssen Sie der Verwendung von Features der Vorabversion von der Configuration Manager-Konsole aus zustimmen, bevor Sie deren Verwendung auswählen und aktivieren können.  

Die Zustimmung ist eine einmalige Aktion pro Hierarchie, die nicht rückgängig gemacht werden kann. Sie können bis zu Ihrer Zustimmung keine neuen Features der Vorabversion aktivieren, die in Updates enthalten sind. Nachdem Sie ein Feature der Vorabversion aktiviert haben, können Sie es nicht wieder deaktivieren.

Sie geben Ihre Zustimmung, indem Sie in der Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**navigieren, und anschließend **Hierarchieeinstellungen**auswählen. Wählen Sie auf der Registerkarte **Allgemein** **Verwendung von Featurevorabversionen zustimmen** aus.

Wenn Sie ein Update installieren, das Features der Vorabversion enthält, sind diese Features im Assistenten für Updates und Wartung zusammen mit den regulären Funktionen sichtbar, die im Update enthalten sind:
  - **Wenn Sie Ihre Zustimmung gegeben haben:** Sie können Featurevorabversionen innerhalb des Assistenten für Updates und Wartung aktivieren, wenn Sie das Update installieren. Wählen Sie dazu die Featurevorabversionen aus, so wie Sie jede andere Funktion auswählen würden.     

    Optional können Sie die Features der Vorabversionen auch später über den Knoten **Verwaltung** > **Updates und Wartung** > **Features** der Konsole aktivieren. Wählen Sie unter dem Knoten **Features** das Feature aus, und wählen Sie anschließend **Aktivieren** aus. Diese Option ist bis zu Ihrer Zustimmung deaktiviert. (Vor Version 1702 befand sich „Updates und Wartung“ unter **Verwaltung** > **Clouddienste**.)
  -   **Wenn Sie nicht Ihre Zustimmung gegeben haben:** Beim Installieren eines Updates sind Features der Vorabversion im Assistenten für Updates und Wartung sichtbar; sie sind jedoch deaktiviert und können nicht aktiviert werden. Nachdem das Update installiert wurde, können Sie diese Features im Knoten **Features** anzeigen. Allerdings können Sie sie erst aktivieren, nachdem Sie die Zustimmung in den **Hierarchieeinstellungen** erteilt haben.


> [!Important]  
> In einer Hierarchie mit mehreren Standorten können Sie nur optionale Features oder Features der Vorabversion vom Standort der zentralen Verwaltung aus aktivieren. Dieses Verhalten stellt sicher, dass keine Konflikte in der Hierarchie auftreten. <!--507197-->  
> Wenn Sie an einem eigenständigen primären Standort Ihre Zustimmung erteilt haben und die Hierarchie durch die Installation eines neuen Standorts der zentralen Verwaltung erweitern, müssen Sie am Standort der zentralen Verwaltung erneut Ihre Zustimmung geben.  

 Wenn Sie ein Feature der Vorabversion aktivieren, muss der Hierarchie-Manager von Configuration Manager (HMAN) die Änderung verarbeiten, bevor Sie das Feature nutzen können. Das Verarbeiten der Änderung wird oftmals direkt abgeschlossen; es kann aber bis zu 30 Minuten in Anspruch nehmen, abhängig vom Verarbeitungszyklus des HMAN. Nachdem die Änderung verarbeitet wurde, müssen Sie Ihre Konsole neu starten, bevor die zu diesem Feature gehörige UI angezeigt wird.

**Die folgenden vorab veröffentlichten Features sind verfügbar:**

 |Komponente          |Als Vorabversion hinzugefügt | Als vollständiges Feature hinzugefügt|  
|------------------|---------------------|---------------------|
|Bereitstellung in Phasen<!--1356837-->|[Version 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence.md)|![Noch nicht](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Schritt „Tasksequenz ausführen“ <!-- 1261338 --> |  [Version 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |[Version 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence)|
| Windows Defender Exploit Guard <!-- 1355468 --> |  [Version 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |[Version 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)|
| Bewertung für den Integritätsnachweis von Geräten für die Konformitätsrichtlinien des bedingten Zugriffs <!-- 1235616 --> |  [Version 1710](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) |[Version 1802](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)|
| Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole <!-- 1236459 --> |  [Version 1706](/sccm/apps/deploy-use/create-deploy-scripts)|[Version 1802](/sccm/apps/deploy-use/create-deploy-scripts)|
| Verwalten von Microsoft Surface-Treiberupdates <!-- 1098490 --> |  [Version 1706](/sccm/sum/get-started/configure-classifications-and-products) | [Version 1710](/sccm/sum/get-started/configure-classifications-and-products)|
| Device Guard-Verwaltung mit Configuration Manager <!-- 1319346 --> |  [Version 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Noch nicht](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Speichern von Tasksequenzinhalten in vorgeschaltetem Cache <!-- 1021244 --> |  [Version 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [Version 1710](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| Suchen nach ausgeführten ausführbaren Dateien vor der Installation einer Anwendung <!-- 1284624 --> |   [Version 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[Version 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| Data Warehouse-Dienstpunkt <!-- 1277922 --> |  [Version 1702](/sccm/core/servers/manage/data-warehouse) |[Version 1706](/sccm/core/servers/manage/data-warehouse)|
| Peercache zur Inhaltsverteilung auf Clients <!-- 1101436 --> |  [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [Version 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| Cloud Management Gateway <!-- 1101764 --> |  [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |[Version 1802](/sccm/core/clients/manage/plan-cloud-management-gateway)|
| Microsoft Operations Management Suite-Connector <!-- 1236739 --> | [Version 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |[Version 1802](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md)|
| Warten einer clusterfähigen Sammlung (Warten einer Servergruppe) <!-- 1081776 --> | [Version 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Noch nicht](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Bedingter Zugriff für von System Center Configuration Manager verwalteten PCs <!--  --> | [Version 1602](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)     | [Version 1702](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)                     |
<!--Image used = ![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif) -->

> [!Tip]  
> Weitere Informationen zu nicht vorab veröffentlichten Features, die Sie zunächst aktivieren müssen, finden Sie unter [Aktivieren optionaler Features von Updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> Weitere Informationen zu Features, die nur im Technical Preview-Branch verfügbar sind, finden Sie unter [Technical Preview](/sccm/core/get-started/technical-preview).  
