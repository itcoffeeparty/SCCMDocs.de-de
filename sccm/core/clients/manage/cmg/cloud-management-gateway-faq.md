---
title: CMG-FAQ
description: In diesem Artikel finden Sie Antworten auf häufig gestellte Fragen zu Cloud Management Gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: 8615b28735165650a0ec25e3d3114263835803d6
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Häufig gestellte Fragen zu Cloud Management Gateway

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Artikel finden Sie Antworten auf häufig gestellte Fragen zu Cloud Management Gateway (CMG). Weitere Informationen finden Sie unter [Planen von Cloud Management Gateway in Configuration Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

### <a name="what-certificates-do-i-need"></a>Welche Zertifikate benötige ich?

Weitere Informationen finden Sie unter [Zertifikate für Cloud Management Gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).


### <a name="do-i-need-azure-expressroute"></a>Benötige ich Azure ExpressRoute?

Mit [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) können Sie Ihr lokales Netzwerk mit der Microsoft-Cloud verbinden und dadurch erweitern. ExpressRoute oder andere virtuelle Netzwerkverbindungen sind nicht für das Configuration Manager-CMG erforderlich. Mit dem CMG können internetbasierte Clients ohne zusätzliche Netzwerkkonfiguration über den Azure-Dienst mit lokalen Standortsystemen kommunizieren. Weitere Informationen finden Sie unter [Planen von Cloud Management Gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).

Wenn Ihre Organisation ExpressRoute verwendet, besteht eine bewährte Sicherheitsmethode darin, das Azure-Abonnement für das CMG zu isolieren. Durch diese Konfiguration wird verhindert, dass der Dienst des CMG versehentlich eine Verbindung herstellt. Weitere Informationen finden Sie unter [Security and privacy for cloud management gateway (Sicherheit und Datenschutz für Cloud Management Gateway)](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway).


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Muss ich virtuelle Azure-Computer warten?

Eine Wartung ist nicht erforderlich. Das CMG nutzt die PaaS-Hostingoption (Platform-as-a-Service) von Azure. Mit dem von Ihnen bereitgestellten Abonnement erstellt Configuration Manager die notwendigen virtuellen Computer (VMs), den Speicher und das Netzwerk. Azure sichert und aktualisiert die virtuellen Computer. Anders als bei Infrastructure-as-a-Service (IaaS) sind diese VMs kein Teil Ihrer lokalen Umgebung. Das CMG ist ein PaaS-Dienst, mit der die Configuration Manager-Umgebung mit der Cloud verbunden und dadurch erweitert wird. 


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Ich verwende bereits IBCM. Wie ändert sich das Clientverhalten, wenn ich zusätzlich das CMG nutze?

Wenn Sie bereits einen [IBCM-Dienst](/sccm/core/clients/manage/plan-internet-based-client-management) (internet-based client management, internetbasierte Clientverwaltung) bereitgestellt haben, können Sie zusätzlich auch das CMG bereitstellen. Clients empfangen für beide Dienste Richtlinien. Sobald die Clients mit dem Internet verbunden sind, wählen sie zufällig einen dieser internetbasierten Dienste aus und nutzen diesen.


## <a name="next-steps"></a>Nächste Schritte

- [Planen des Cloudverwaltungsgateways](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Einrichten des Cloudverwaltungsgateways](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Zertifikate für Cloud Management Gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Sicherheit und Datenschutz für Cloud Management Gateway](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Größe und Skalierungszahlen für das Cloudverwaltungsgateway](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)