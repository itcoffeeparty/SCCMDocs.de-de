---
title: Konfigurieren von Endpoint Protection | System Center Configuration Manager
description: "Erfahren Sie, wie Sie Configuration Manager einrichten, sodass Schadsoftwaredefinitionen für Windows Defender aktualisiert und verteilt werden."
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
ms.openlocfilehash: c13ea976057a4267eb6ed0d5c5852b165de868cb


---

# <a name="configure-endpoint-protection-in-system-center-configuration-manager"></a>Konfigurieren von Endpoint Protection in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bevor Sie Endpoint Protection zum Verwalten von Sicherheit und Schadsoftware auf Configuration Manager-Clientcomputern verwenden können, müssen Sie die Konfigurationsschritte ausführen, die in diesem Thema erläutert werden.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Konfigurieren von Endpoint Protection in Configuration Manager  
 Endpoint Protection in Configuration Manager hat externe Abhängigkeiten sowie Abhängigkeiten innerhalb des Produkts.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Schritte für das Konfigurieren von Endpoint Protection in Configuration Manager  
 In der folgenden Tabelle finden Sie die Schritte, Details und weitere Informationen zum Konfigurieren von Endpoint Protection.  

> [!IMPORTANT]  
>  Wenn Sie Endpoint Protection für Windows 10-Computer verwalten, müssen Sie Configuration Manager so konfigurieren, dass Schadsoftwaredefinitionen für Windows Defender aktualisiert und bereitgestellt werden. Windows Defender ist in Windows 10 enthalten, aber SCEPInstall muss weiterhin installiert werden, und benutzerdefinierte Clienteinstellungen für Endpoint Protection (**Schritt 5** unten) sind weiterhin erforderlich.  

|Schritte|Details|  
|-----------|-------------|  
|**Schritt 1:** Erstellen Sie eine Standortsystemrolle für den Endpoint Protection-Punkt.|Die Standortsystemrolle für den Endpoint Protection-Punkt muss installiert sein, bevor Sie Endpoint Protection verwenden können. Sie darf nur auf einem einzigen Standortsystemserver installiert sein, und sie muss auf der obersten Hierarchieebene eines zentralen Verwaltungsstandorts oder eines eigenständigen primären Standorts installiert sein. Siehe [Schritt 1: Erstellen Sie eine Standortsystemrolle für den Endpoint Protection-Punkt](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_Step1) in diesem Thema.|  
|**Schritt 2:** Konfigurieren Sie Warnungen für Endpoint Protection.|Von Warnungen wird der Administrator über bestimmte Ereignisse wie Infektionen mit Schadsoftware informiert. Die Warnungen werden im Knoten **Warnungen** des Arbeitsbereichs **Überwachung** angezeigt oder können optional per E-Mail an angegebene Benutzer versendet werden. Siehe [Schritt 2: Konfigurieren Sie Warnungen für Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_EPalerts).|  
|**Schritt 3:** Konfigurieren Sie Definitionsupdatequellen für Endpoint Protection-Clients.|Endpoint Protection kann so konfiguriert werden, dass verschiedene Quellen zum Herunterladen von Definitionsupdates verwendet werden. Siehe [Schritt 3: Konfigurieren Sie die Definitionsupdates für Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_EPdefs).|  
|**Schritt 4:** Konfigurieren Sie die Standardrichtlinie für Antischadsoftware, und erstellen Sie benutzerdefinierte Richtlinien für Antischadsoftware.|Bei der Installation des Endpoint Protection-Clients wird die Standardrichtlinie für Antischadsoftware angewendet. Alle benutzerdefinierten Richtlinien für Antischadsoftware, die Sie bereitgestellt haben, werden innerhalb von 60 Minuten nach der Bereitstellung des Clients in der Standardeinstellung angewendet. Stellen Sie sicher, dass Sie Richtlinien für Antischadsoftware konfiguriert haben, bevor Sie den Endpoint Protection-Client bereitstellen. Siehe [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/endpoint-antimalware-policies.md).|  
|**Schritt 5:** Konfigurieren Sie benutzerdefinierte Clienteinstellungen für Endpoint Protection.|Verwenden Sie benutzerdefinierte Clienteinstellungen, um Endpoint Protection-Einstellungen für Computersammlungen in Ihrer Hierarchie zu konfigurieren.<br /><br /> Hinweis: Konfigurieren Sie nicht die Standard-Endpoint Protection-Clienteinstellungen, es sei denn, Sie sind sicher, dass diese Einstellungen auf alle Computer in Ihrer Hierarchie angewendet werden sollen. Siehe [Schritt 5: Konfigurieren Sie benutzerdefinierte Clienteinstellungen für Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_EPclient) in diesem Thema.|  



<!--HONumber=Nov16_HO1-->


