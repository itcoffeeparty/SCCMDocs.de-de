---
title: "Firewalls und Domänen | Microsoft-Dokumentation"
description: "Konfigurieren Sie Firewalls, Ports und Domänen zur Vorbereitung von System Center Configuration Manager-Kommunikation."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: df0622164ae7784ccfedc0f4c3328c42c1d050c3


---
# <a name="configure-firewalls-ports-and-domains-for-system-center-configuration-manager"></a>Konfigurieren von Firewalls, Ports und Domänen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Planen Sie die Konfiguration von Infrastrukturkomponenten, z.B. Firewalls, um Ihr Netzwerk für die Unterstützung von System Center Configuration Manager vorzubereiten, damit die Kommunikation mit Configuration Manager gewährleistet ist.  

|Überlegung|Details|  
|-------------------|-------------|  
|Von verschiedenen Configuration Manager-Funktionen verwendete **Ports und Protokolle**. Einige Ports sind erforderlich, während andere **Domänen und Dienste** angepasst werden können.|Für einen Großteil der Configuration Manager-Kommunikation werden allgemeine Ports wie z.B. 80 für die HTTP- oder 443 für die HTTPS-Kommunikation verwendet. Allerdings [unterstützen einige Standortsystemrollen die Verwendung benutzerdefinierter Websites](/sccm/core/plan-design/network/websites-for-site-system-servers) und Ports.<br /><br /> Identifizieren Sie **vor der Bereitstellung von Configuration Manager** die Ports, die Sie verwenden möchten, und konfigurieren Sie die Firewalls entsprechend.<br /><br /> **Später, wenn Sie nach der Installation von Configuration Manager einen Port ändern müssen**, vergessen Sie nicht das Aktualisieren von Firewalls für Geräte und Netzwerk, und ändern Sie außerdem die Konfiguration des Ports in Configuration Manager.<br /><br /> Weitere Informationen finden Sie unter: </br>- [Konfigurieren von Clientkommunikationsports](../../../core/clients/deploy/configure-client-communication-ports.md) </br>- [In Configuration Manager verwendete Ports](../../../core/plan-design/hierarchy/ports.md) </br>- [Internetzugriffsanforderungen für den Dienstverbindungspunkt](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)|  
|**Domänen und Dienste** , auf die Standortserver und Clients möglicherweise zugreifen müssen.|Configuration Manager-Funktionen können Standortserver erfordern, und Clients haben Zugriff auf bestimmte Dienste und Domänen im Internet, wie z.B. „Windowsudpate.microsoft.com“ oder den Microsoft Intune-Dienst.<br /><br /> Wenn Sie Microsoft Intune zum Verwalten mobiler Geräte verwenden, müssen Sie auch den Zugriff auf [von Intune benötigte Ports und Domänen](https://docs.microsoft.com/en-us/intune/get-started/network-infrastructure-requirements-for-microsoft-intune) konfigurieren.|  
|**Proxyserver** für Standortsystemserver und die Clientkommunikation. Sie können separate Proxyserver für verschiedene Standortsystemserver und Clients angeben.|Da diese Konfigurationen bei der Installation einer Standortsystemrolle oder eines Clients erfolgen, müssen Sie lediglich mit den Proxyserverkonfigurationen vertraut sein, wenn Sie später Standortsystemrollen und Clients konfigurieren.<br /><br /> Wenn Sie nicht sicher sind, ob Sie in Ihrer Bereitstellung Proxyserver verwenden müssen, konsultieren Sie [Unterstützung von Proxyservern in System Center Configuration Manager](../../../core/plan-design/network/proxy-server-support.md), um sich über Standortsystemrollen und Clientaktionen zu informieren, die einen Proxyserver verwenden können.|  



<!--HONumber=Dec16_HO3-->


