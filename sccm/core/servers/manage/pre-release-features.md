---
title: "Vorab veröffentlichte Funktionen | Microsoft-Dokumentation"
description: Features der Vorabversion in System Center Configuration Manager
ms.custom: na
ms.date: 3/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6accec2d356861b273b25ba2b6338d9684a46ff6
ms.openlocfilehash: c1c8cf505bbc5cab1b6dfb7637eda4a87941c722
ms.lasthandoff: 03/29/2017


---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>Features der Vorabversion in System Center Configuration Manager
*Gilt für: System Center Configuration Manager (Current Branch)*

 Features der Vorabversion sind Funktionen, die in Current Branch enthalten sind, um sie in einem frühen Stadium in einer Produktionsumgebung zu testen. Diese Features sollten nicht als produktionsbereit angesehen werden, können aber in der Produktionsumgebung verwendet werden.

 Bevor Sie Features der Vorabversion verwenden können, müssen Sie der Verwendung von Features der Vorabversion von der Configuration Manager-Konsole aus zustimmen, bevor Sie deren Verwendung auswählen und aktivieren können.  

Die Zustimmung ist eine einmalige Aktion pro Hierarchie, die nicht rückgängig gemacht werden kann. Sie können bis zu Ihrer Zustimmung keine neuen Features der Vorabversion aktivieren, die in Updates enthalten sind.

Sie geben Ihre Zustimmung, indem Sie in der Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**navigieren, und anschließend **Hierarchieeinstellungen**auswählen. Wählen Sie auf der Registerkarte **Allgemein** **Verwendung von Featurevorabversionen zustimmen** aus.

 > [!NOTE]
 > Wenn Sie zuvor die Features der Vorabversion von Update 1602 aktiviert haben, bleiben diese Features bis zur Installation einer höheren Updateversion für die Verwendung aktiviert, auch wenn Sie keine Zustimmung zur Verwendung von Features der Vorabversion gegeben haben.

Wenn Sie ein Update installieren, das Features der Vorabversion enthält, sind diese Features im Assistenten für Updates und Wartung zusammen mit den regulären Funktionen sichtbar, die im Update enthalten sind:
  - **Wenn Sie Ihre Zustimmung gegeben haben:** Sie können Featurevorabversionen innerhalb des Assistenten für Updates und Wartung aktivieren, wenn Sie das Update installieren. Wählen Sie dazu die Featurevorabversionen aus, so wie Sie jede andere Funktion auswählen würden.     

    Optional können Sie die Features der Vorabversionen auch später über den Knoten **Verwaltung** > **Updates und Wartung** > **Features** der Konsole aktivieren. Wählen Sie unter dem Knoten **Features** das Feature aus, und wählen Sie anschließend **Aktivieren** aus. Diese Option ist bis zu Ihrer Zustimmung deaktiviert. (Vor Version 1702 befand sich „Updates und Wartung“ unter **Verwaltung** > **Clouddienste**.)
  -   **Wenn Sie nicht Ihre Zustimmung gegeben haben:** Beim Installieren eines Updates sind Features der Vorabversion im Assistenten für Updates und Wartung sichtbar; sie sind jedoch deaktiviert und können nicht aktiviert werden. Nach der Installation des Updates können Sie diese Features auf dem Knoten **Features** anzeigen, diese jedoch nicht aktivieren, bis sie Ihre Zustimmung in den **Hierarchieeinstellungen** gegeben haben.

Wenn Sie an einem eigenständigen primären Standort Ihre Zustimmung erteilt haben und die Hierarchie durch die Installation eines neuen Standorts der zentralen Verwaltung erweitern, müssen Sie am Standort der zentralen Verwaltung erneut Ihre Zustimmung geben.

**Die folgenden vorab veröffentlichten Features sind verfügbar:**

 |Komponente          |Als Vorabversion hinzugefügt | Als vollständiges Feature hinzugefügt|  
|------------------|---------------------|---------------------|
| Prüfen Sie auf ausgeführte ausführbare Dateien, bevor Sie eine Anwendung installieren  |   [Version 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |![Noch nicht](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Data Warehouse-Dienstpunkt  |  [Version 1702](/sccm/core/servers/manage/data-warehouse) |![Noch nicht](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Peercache zur Verteilung von Inhalten an Clients |  [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![Noch nicht](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Cloudverwaltungsgateway |  [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![Noch nicht](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Dashboard „Clientdatenquellen“ |  [Version 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![Noch nicht](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Microsoft Operations Management Suite-Connector  | [Version 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Noch nicht](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Warten einer clusterfähigen Sammlung (Warten einer Servergruppe)| [Version 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Noch nicht](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Bedingten Zugriffs für PCs, die von System Center Configuration Manager verwaltet werden | [Version 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     | [Version 1702](/sccm/mdm/deploy-use/manage-access-to-services)                     |

