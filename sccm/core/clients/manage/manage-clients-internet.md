---
title: Verwalten von Clients im Internet
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zum Verwalten von Clients mithilfe von Cloud Management Gateway (CMG) und zur internetbasierten Clientverwaltung in Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 31d43d855c1e7062e62a3d15fa5a79c4e4de915f
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Verwalten von Clients im Internet mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In der Regel befinden sich in Configuration Manager die meisten verwalteten Computer und Server in demselben internen Netzwerk wie die Standortsystemserver, die Verwaltungsfunktionen ausführen. Sie können jedoch auch Clients außerhalb des internen Netzwerks verwalten, wenn sie mit dem Internet verbunden sind. Hierbei müssen Clients keine VPN-Verbindung aufbauen, um mit den Standortsystemservern zu kommunizieren.

Configuration Manager bietet zwei Methoden, mit dem Internet verbundene Clients zu verwalten:

-   Cloudverwaltungsgateway

-   Internetbasierte Clientverwaltung


## <a name="cloud-management-gateway"></a>Cloudverwaltungsgateway

Mit Cloud Management Gateway (CMG) lassen sich internetbasierte Clients verwalten. Dabei wird eine neue Standortsystemrolle verwendet, die mit einem Microsoft Azure-Clouddienst kommuniziert. Internetbasierte Clients verwenden den Clouddienst, um mit dem lokalen Configuration Manager zu kommunizieren.

#### <a name="advantages"></a>Vorteile  

-   Keine zusätzlichen Infrastrukturinvestitionen erforderlich.  

-   Lokale Infrastruktur bleibt vom Internet getrennt.  

-   Virtuelle Computer in der Cloud, auf denen der Dienst ausgeführt wird, werden vollständig von Azure verwaltet und erfordern keine Wartung.  

-   Einfache Einrichtung und Konfiguration in der Configuration Manager-Konsole.  

#### <a name="disadvantages"></a>Nachteile  

-   Cloud-Abonnement-Kosten.  

-   Verwaltungsdaten werden über Cloud-Dienst gesendet.  

Weitere Informationen finden Sie unter [Planen des Cloudverwaltungsgateways](plan-cloud-management-gateway.md).  



## <a name="internet-based-client-management"></a>Internetbasierte Clientverwaltung

Diese Methode beruht auf mit dem Internet verbundenen Standortsystemservern, mit denen Clients zu Verwaltungszwecken kommunizieren. Bei dieser Methode müssen Clients und Standortsystemserver für die internetbasierte Verwaltung konfiguriert werden.

#### <a name="advantages"></a>Vorteile  

-   Keine Abhängigkeit von einem Cloud-Dienst.  

-   Ohne zusätzliche Kosten eines Cloud-Abonnements.  

-   Vollständige Kontrolle von Servern und Rollen, die den Dienst bereitstellen.  

#### <a name="disadvantages"></a>Nachteile  

-   Zusätzliche Infrastrukturinvestitionen erforderlich.  

-   Gemeinkosten und Betriebskosten der zusätzlichen Infrastruktur.  

-   Infrastruktur muss mit dem Internet verbunden sein.  

Weitere Informationen finden Sie unter [Planen der internetbasierten Clientverwaltung](plan-internet-based-client-management.md).  
