---
title: Grundlagen zu Configuration Manager-as-a-Service und Windows-as-a-Service
titleSuffix: Configuration Manager
description: "Erhalten Sie Informationen dazu, wie Sie Configuration Manager-as-a-Service anpassen, sodass Windows-as-a-Service unterstützt wird."
ms.custom: na
ms.date: 01/04/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 90542085af2a1e5cf0701c5eac6d2625c23eb8c6
ms.sourcegitcommit: db9978135d7a6455d83dbe4a5175af2bdeaeafd8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2018
---
# <a name="keep-windows-10-up-to-date-in-the-enterprise-using-configuration-manager"></a>Halten Sie Windows 10 unternehmensweit über Configuration Manager aktuell

*Gilt für: System Center Configuration Manager (Current Branch), Windows 10 (halbjährlicher Kanal)*

System Center Configuration Manager bietet eine umfassende Kontrolle über Featureupdates für Windows 10. Damit Sie das Modell „Windows-as-a-Service“ vollständig übernehmen können, müssen Sie auch Configuration Manager-as-a-Service übernehmen. Wenn Sie Ihre Windows 10-Version aktuell halten möchten, achten Sie darauf, dass stets die aktuelle Version von Configuration Manager installiert ist. Damit Sie von den praktischen neuen Unternehmensfeatures für Windows 10 profitieren können, müssen Sie immer die neuste Version von Configuration Manager installieren. In diesem Artikel wird auf die wichtigsten Artikel verwiesen, die Ihnen dabei helfen, Configuration Manager-as-a-Service anzupassen. Configuration Manager-as-a-Service hilft Ihnen dabei, Windows-as-a-Service zu etablieren.

## <a name="key-topics-about-adopting-configuration-manager-as-a-service"></a>Wichtige Artikel zum Thema „Configuration Manager-as-a-Service“

| Thema        | Beschreibung          | 
| ------------- |-------------|
|[Übersicht über Configuration Manager-as-a-Service](/sccm/core/plan-design/changes/whats-new-incremental-versions)|Kurze Zusammenfassung der wichtigsten Punkte zum neuen Servicemodell für Configuration Manager (Current Branch)|
|[Lifecycle-Unterstützung](/sccm/core/servers/manage/current-branch-versions-supported)|Erläutert die neue Unterstützung und das Dienstmodell.|
|[Entfernte und veraltete Features](/sccm/core/plan-design/changes/removed-and-deprecated-features)|Dies dient als frühzeitige Warnung hinsichtlich zukünftiger Änderungen, die sich auf die Verwendung von Configuration Manager auswirken können.|
|[Configuration Manager-as-a-Service](/sccm/core/servers/manage/updates)|Erläutert die einfache konsoleninterne Methode zum Anwenden von Featureupdates für Configuration Manager.|
|[Abrufen von verfügbaren Updates](/core/servers/manage/install-in-console-updates#get-available-updates)|Erläutert die beiden verfügbaren Modi zum Abrufen neuer Featureupdates für Configuration Manager.|
|[Updatecheckliste](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall)|Versionsspezifische Updatecheckliste, falls vorhanden.| 
|[Installieren der neuen Featureupdates für Configuration Manager](/sccm/core/servers/manage/install-in-console-updates#bkmk_install)|Erläutert die einfachen Schritte zur Installation von Featureupdates.|
|[Unterstützung für Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)|Stellt eine Unterstützungsmatrix für Windows 10-Versionen (und ADK-Versionen) zur Verfügung.|
|[Technical Previews für Configuration Manager](/sccm/core/get-started/technical-preview)|Stellt Informationen zum Technical Preview-Programm für Configuration Manager zur Verfügung.|


## <a name="key-topics-about-adopting-windows-as-a-service"></a>Wichtige Themen zur Übernahme von Windows-as-a-Service
| Thema        | Beschreibung          | 
| ------------- |-------------|
|[Verwalten von Windows as a Service](/sccm/osd/deploy-use/manage-windows-as-a-service)|Erläuterungen zur Verwendung von Wartungsplänen zum Bereitstellen von Featureupdates für Windows 10.|
|[Windows Update for Business-Integration (optional)](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|Erläuterungen zum Definieren und Bereitstellen von Richtlinien für Windows Update for Business mithilfe von Configuration Manager.|
|[Verwenden der Co-Verwaltung mit Microsoft Intune und Windows Update for Business (optional)](/sccm/core/clients/manage/co-management-overview)|Überblick über die Co-Verwaltung| 


## <a name="related-articles"></a>Verwandte Artikel

- [Direktes Upgrade von Configuration Manager 2012 auf System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [Planen einer Migration von Configuration Manager 2007 auf System Center Configuration Manager (Current Branch)](/sccm/core/migration/planning-for-migration)