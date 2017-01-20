---
title: Konfigurieren von Endpoint Protection | System Center Configuration Manager
description: Erfahren Sie, wie Sie Sicherheit und Schadsoftware auf System Center Configuration Manager-Clientcomputern verwalten.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5905ab3f63a9956909f3d26136a377ca2f65b71c


---
# <a name="configuring-endpoint-protection-in-system-center-configuration-manager"></a>Konfigurieren von Endpoint Protection in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bevor Sie Endpoint Protection zum Verwalten von Sicherheit und Schadsoftware auf Configuration Manager-Clientcomputern verwenden können, müssen Sie die Konfigurationsschritte ausführen, die in diesem Thema erläutert werden.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Konfigurieren von Endpoint Protection in Configuration Manager  
 Endpoint Protection in Configuration Manager verfügt über externe Abhängigkeiten sowie Abhängigkeiten innerhalb des Produkts.  

### <a name="configure-endpoint-protection-in-configuration-manager"></a>Konfigurieren von Endpoint Protection in Configuration Manager  
Es gibt fünf Schritte zum Konfigurieren von Endpoint Protection

|Schritt|Details|
|---|----|
|Schritt 1|[Erstellen Sie eine Standortsystemrolle für einen Endpoint Protection-Punkt](endpoint-protection-site-role.md) – Installieren der Standortsystemrolle für den Endpoint Protection-Punkt |
|Schritt 2|[Konfigurieren von Warnungen für Endpoint Protection](endpoint-configure-alerts.md) – Konfigurieren von Endpoint Protection-Warnungen, um Administratoren zu benachrichtigen, wenn bestimmte Sicherheitsereignisse in Ihrer Hierarchie auftreten|
|Schritt 3 | [Konfigurieren von Definitionsupdatequellen für Endpoint Protection-Clients](endpoint-definition-updates.md) – Wählen Sie aus den verfügbaren Methoden aus, um auf den Clientcomputern Antischadsoftware-Definitionen auf dem neuesten Stand zu halten|
|Schritt 4|[Konfigurieren Sie die Standardrichtlinie für Antischadsoftware, und erstellen Sie benutzerdefinierte Richtlinien für Antischadsoftware](endpoint-antimalware-policies.md) – Die Standardrichtlinie für Antischadsoftware wird angewendet, wenn der Endpoint Protection-Client installiert ist; benutzerdefinierte Richtlinien gelten innerhalb von 60 Minuten nach der Bereitstellung des Clients|
|Schritt 5|[Konfigurieren Sie benutzerdefinierte Clienteinstellungen für Endpoint Protection](endpoint-protection-configure-client.md) – Konfigurieren Sie benutzerdefinierte Clienteinstellungen für Endpoint Protection für die Bereitstellung für Sammlungen von Computern|

> [!IMPORTANT]  
>  Wenn Sie Endpoint Protection für Windows 10-Computer verwalten, müssen Sie Configuration Manager so konfigurieren, dass Schadsoftwaredefinitionen für Windows Defender aktualisiert und bereitgestellt werden. Windows Defender ist in Windows 10 enthalten, aber SCEPInstall muss weiterhin installiert werden, und benutzerdefinierte Clienteinstellungen für Endpoint Protection (Schritt 5) sind weiterhin erforderlich.  



<!--HONumber=Nov16_HO1-->


