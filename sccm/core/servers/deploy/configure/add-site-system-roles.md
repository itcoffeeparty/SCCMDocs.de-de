---
title: Hinzufügen von Standortsystemrollen
titleSuffix: Configuration Manager
description: Grundlegendes zu Configuration Manager-Standortsystemrollen und wie sie zum Erweitern der Funktionalität und der Kapazität Ihres Standorts hinzugefügt werden
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2959d2b97088a2d92b861f0ca4a4d37d0df3e726
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="add-site-system-roles-for-system-center-configuration-manager"></a>Hinzufügen von Standortsystemrollen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Jeder System Center Configuration Manager-Standort unterstützt mehrere Standortsystemrollen. Jede Rolle erweitert die Funktionalität und Kapazität Ihres Standorts, um dem Standort Dienste bereitzustellen und Benutzer und Geräten zu verwalten. Jede Standortsystemrolle auf einem Standortserver muss sich am selben Standort befinden.   

Von Configuration Manager werden keine Standortsystemrollen für mehrere Standorte auf einem einzigen Standortsystemserver unterstützt.  

> [!TIP]  
>  Wenn Sie mit den Grundlagen von Standortsystemrollen oder den Unterschieden zwischen Standortserver, Standortsystemserver und Standortsystemrollen nicht vertraut sind, lesen Sie [Grundlagen von System Center Configuration Manager](../../../../core/understand/fundamentals.md).  

 In den folgenden Themen werden Verfahren und die zugehörigen Details für die Installation von Standortsystemrollen ausführlich beschrieben:  

-   [Installieren von Standortsystemrollen für System Center Configuration Manager](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     Dieses Thema enthält grundlegende Hinweise zur Verwendung der beiden konsoleninternen Assistenten, die Sie zum Installieren neuer Standortsystemrollen verwenden können.  

-   [Installieren von cloudbasierten Verteilungspunkten in Microsoft Azure für System Center Configuration Manager.](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    Wenn Sie Microsoft Azure verwenden möchten, um Inhalte für die Bereitstellung auf Clients zu hosten, können Sie mithilfe der Informationen in diesem Thema die erforderlichen Zertifikatsdateien einrichten und Configuration Manager die Kommunikation mit Ihrem Microsoft Azure-Abonnement sowie dessen Verwendung ermöglichen. Darüber hinaus müssen Sie die Einrichtung der Namensauflösung so konfigurieren, dass Ihre Clients die cloudbasierten Verteilungspunkte finden können.  

-   [Installieren von Standortsystemrollen für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     Dieses Thema hilft Ihnen bei der erfolgreichen Einrichtung Ihrer Standortsystemrollen, damit diese die Verwaltung moderner Geräte mit der lokalen Configuration Manager-Verwaltung mobiler Geräte unterstützen.  

-   [Konfigurationsoptionen für Standortsystemrollen für System Center Configuration Manager](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     Einige Standortsystemrollen unterstützen Konfigurationen, für die mehr Details erforderlich sind als innerhalb der Benutzeroberfläche erklärt werden können. Diese Einzelheiten werden in diesem Thema ausgeführt.  
