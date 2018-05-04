---
title: Unterstützte Standortsystemserver
titleSuffix: Configuration Manager
description: Erfahren Sie, welche Windows-Versionen Sie verwenden können, um einen System Center Configuration Manager-Standort oder eine entsprechende Standortsystemrolle zu hosten.
ms.custom: na
ms.date: 04/17/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 44
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 092fc9d47e0dc7bb7afe0e078bd835dd2d091226
ms.sourcegitcommit: e23350fe65ff99228274e465b24b5e163769f38f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/20/2018
---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>Unterstützte Betriebssysteme für System Center Configuration Manager-Standortsystemserver

*Gilt für: System Center Configuration Manager (Current Branch)*


In diesem Artikel wird beschrieben, welche Windows-Versionen Sie verwenden können, um einen Configuration Manager-Standort oder eine entsprechende Standortsystemrolle zu hosten.


Verwenden Sie die Informationen in diesem Artikel mit den Informationen in den folgenden Artikeln:
-   [Empfohlene Hardware für Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Site and site system prerequisites for Configuration Manager (Standort- und Standortsystemvoraussetzungen für Configuration Manager)](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Size and scale numbers for Configuration Manager (Größe und Skalierung von Zahlen für Configuration Manager)](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016-standard-and-datacenter"></a>Windows Server 2016: Standard und Datacenter
Mit dem Hotfixrollup aus KB3186654 wird dieses Betriebssystem für die folgenden Rollen unterstützt:

**Standortserver:**  

-   Standort der zentralen Verwaltung  

-   Primärer Standort  

-   Sekundärer Standort  

**Standortsystemserver:**  

-   Anwendungskatalog-Webdienstpunkt  

-   Anwendungskatalog-Websitepunkt  

-   Asset Intelligence-Synchronisierungspunkt  

-   Zertifikatregistrierungspunkt  

-   Verteilungspunkt  

     Verteilungspunkte unterstützen mehrere unterschiedliche Konfigurationen mit unterschiedlichen Anforderungen. In einigen Fällen unterstützen diese Konfigurationen die Installation nicht nur auf Servern, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den Optionen, die für Verteilungspunkte verfügbar sind, finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection-Punkt  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

-   Fallbackstatuspunkt  

-   Verwaltungspunkt

-   Reporting Services-Punkt  

-   Dienstverbindungspunkt  

-   Standortdatenbankserver  

     Standortdatenbankserver werden auf einem Domänencontroller ohne Schreibzugriff (Read-Only Domain Controller, RODC) nicht unterstützt. Weitere Informationen finden Sie unter [You may encounter problems when installing SQL Server on a domain controller (Beim Installieren eines SQL Servers auf einem Domänencontroller treten möglicherweise Probleme auf)](https://go.microsoft.com/fwlink/p/?LinkId=264856) in der Microsoft Knowledge Base. Darüber hinaus werden sekundäre Standortserver nicht auf jedem Domänencontroller unterstützt.  

-   SMS-Anbieter  

-   Softwareupdatepunkt  

-   Zustandsmigrationspunkt



## <a name="windows-storage-server-2016"></a>Windows Storage Server 2016

**Standortsystemserver:**  

-   Verteilungspunkt  



## <a name="windows-server-2012-r2-x64-standard-and-datacenter"></a>Windows Server 2012 R2 (x64): Standard und Datacenter  
**Standortserver:**  

-   Standort der zentralen Verwaltung  

-   Primärer Standort  

-   Sekundärer Standort  

**Standortsystemserver:**  

-   Anwendungskatalog-Webdienstpunkt  

-   Anwendungskatalog-Websitepunkt  

-   Asset Intelligence-Synchronisierungspunkt  

-   Zertifikatregistrierungspunkt  

-   Verteilungspunkt  

     Verteilungspunkte unterstützen mehrere unterschiedliche Konfigurationen mit unterschiedlichen Anforderungen. In einigen Fällen unterstützen diese Konfigurationen die Installation nicht nur auf Servern, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den Optionen, die für Verteilungspunkte verfügbar sind, finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection-Punkt  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

-   Fallbackstatuspunkt  

-   Verwaltungspunkt

-   Reporting Services-Punkt  

-   Dienstverbindungspunkt  

-   Standortdatenbankserver  

     Standortdatenbankserver werden auf einem Domänencontroller ohne Schreibzugriff (Read-Only Domain Controller, RODC) nicht unterstützt. Weitere Informationen finden Sie unter [You may encounter problems when installing SQL Server on a domain controller (Beim Installieren eines SQL Servers auf einem Domänencontroller treten möglicherweise Probleme auf)](https://go.microsoft.com/fwlink/p/?LinkId=264856) in der Microsoft Knowledge Base. Darüber hinaus werden sekundäre Standortserver nicht auf jedem Domänencontroller unterstützt.  

-   SMS-Anbieter  

-   Softwareupdatepunkt  

-   Zustandsmigrationspunkt  

## <a name="windows-server-2012-x64-standard-and-datacenter"></a>Windows Server 2012 (x64): Standard und Datacenter  
**Standortserver:**  

-   Standort der zentralen Verwaltung  

-   Primärer Standort  

-   Sekundärer Standort  

**Standortsystemserver:**  

-   Anwendungskatalog-Webdienstpunkt  

-   Anwendungskatalog-Websitepunkt  

-   Asset Intelligence-Synchronisierungspunkt  

-   Zertifikatregistrierungspunkt  

-   Verteilungspunkt  

     Verteilungspunkte unterstützen mehrere unterschiedliche Konfigurationen mit unterschiedlichen Anforderungen. In einigen Fällen unterstützen diese Konfigurationen die Installation nicht nur auf Servern, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den Optionen, die für Verteilungspunkte verfügbar sind, finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection-Punkt  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

-   Fallbackstatuspunkt  

-   Verwaltungspunkt

-   Reporting Services-Punkt  

-   Dienstverbindungspunkt  

-   Standortdatenbankserver  

     Standortdatenbankserver werden auf einem Domänencontroller ohne Schreibzugriff (Read-Only Domain Controller, RODC) nicht unterstützt. Weitere Informationen finden Sie unter [You may encounter problems when installing SQL Server on a domain controller (Beim Installieren eines SQL Servers auf einem Domänencontroller treten möglicherweise Probleme auf)](https://go.microsoft.com/fwlink/p/?LinkId=264856) in der Microsoft Knowledge Base. Darüber hinaus werden sekundäre Standortserver nicht auf jedem Domänencontroller unterstützt.  

-   SMS-Anbieter  

-   Softwareupdatepunkt  

-   Zustandsmigrationspunkt  



## <a name="windows-server-2008-r2-with-sp1-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 R2 mit SP1 (x64): Standard, Enterprise und Datacenter  
 Windows Server 2008 R2 unterliegt nun dem erweiterten Support und nicht mehr dem grundlegenden Support, wie im [Microsoft-Support-Lifecycle](https://support.microsoft.com/lifecycle) ausführlich erläutert. Weitere Informationen zum künftigen Support für diese Betriebssysteme als Standortsystemserver mit Configuration Manager finden Sie unter [Veraltete Serverbetriebssysteme](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

 Dieses Betriebssystem wird von Standortservern und den meisten Standortsystemrollen nicht unterstützt. Es wird allerdings weiterhin von den Verteilungspunkt-Standortsystemrollen, einschließlich Pullverteilungspunkten, und von PXE und Multicast unterstützt.

**Standortsystemserver:**  
-   Verteilungspunkt  

    -   Von Verteilungspunkten auf diesem Betriebssystem wird Multicast nicht unterstützt.  

    -   Von Verteilungspunkten auf diesem Betriebssystem wird PXE unterstützt.

    -   Verteilungspunkte unterstützen mehrere unterschiedliche Konfigurationen mit unterschiedlichen Anforderungen. In einigen Fällen unterstützen diese Konfigurationen die Installation nicht nur auf Servern, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den Optionen, die für Verteilungspunkte verfügbar sind, finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-server-2008-with-sp2-x86-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 mit SP2 (x86, x64): Standard, Enterprise und Datacenter  
 Windows Server 2008 unterliegt nun dem erweiterten Support und nicht mehr dem grundlegenden Support, wie im [Microsoft-Support-Lifecycle](https://support.microsoft.com/lifecycle) ausführlich erläutert. Weitere Informationen zum künftigen Support für diese Betriebssysteme als Standortsystemserver mit Configuration Manager finden Sie unter [Veraltete Serverbetriebssysteme](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

Dieses Betriebssystem wird von Standortserver- oder Standortsystemrollen mit Ausnahme des Verteilungspunkts und des Pullverteilungspunkts nicht unterstützt. Sie können dieses Betriebssystem weiterhin als Verteilungspunkt verwenden, bis die Einstellung dieses Supports angekündigt wird oder der erweiterte Support für dieses Betriebssystem abläuft. Weitere Informationen finden Sie unter [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008 (Bei der Installation von System Center Configuration Manager CB und LTSB auf Windows Server 2008 tritt ein Fehler auf)](https://support.microsoft.com/help/4015095).

**Standortsystemserver:**  
-   Verteilungspunkt  

    -   Von Verteilungspunkten auf diesem Betriebssystem wird Multicast nicht unterstützt.  

    -   Von Verteilungspunkten auf diesem Betriebssystem wird PXE, jedoch kein Netzwerkstart von Clientcomputern im EFI-Modus unterstützt. Clientcomputer mit BIOS oder EFI-Start im Legacymodus werden unterstützt.  

    -   Verteilungspunkte unterstützen mehrere unterschiedliche Konfigurationen mit unterschiedlichen Anforderungen. In einigen Fällen unterstützen diese Konfigurationen die Installation nicht nur auf Servern, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den Optionen, die für Verteilungspunkte verfügbar sind, finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-10-x86-x64-pro-and-enterprise"></a>Windows 10 (x86, x64): Pro und Enterprise  
**Standortsystemserver:**  

-   Verteilungspunkt  

    -   Von Verteilungspunkten auf diesem Betriebssystem wird PXE nicht unterstützt. 

    -   Von Verteilungspunkten unter dieser Betriebssystemversion wird Multicast nicht unterstützt.  

    -   Verteilungspunkte unterstützen mehrere unterschiedliche Konfigurationen mit unterschiedlichen Anforderungen. In einigen Fällen unterstützen diese Konfigurationen die Installation nicht nur auf Servern, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den Optionen, die für Verteilungspunkte verfügbar sind, finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-81-x86-x64-professional-and-enterprise"></a>Windows 8.1 (x86, x64): Professional und Enterprise  
**Standortsystemserver:**  

-   Verteilungspunkt  

    -   Von Verteilungspunkten auf diesem Betriebssystem wird PXE nicht unterstützt.  

    -   Von Verteilungspunkten unter dieser Betriebssystemversion wird Multicast nicht unterstützt.  

    -   Verteilungspunkte unterstützen mehrere unterschiedliche Konfigurationen mit unterschiedlichen Anforderungen. In einigen Fällen unterstützen diese Konfigurationen die Installation nicht nur auf Servern, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den Optionen, die für Verteilungspunkte verfügbar sind, finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-7-with-sp1-x86-x64-professional-enterprise-and-ultimate"></a>Windows 7 mit SP1 (x86, x64): Professional, Enterprise und Ultimate  
**Standortsystemserver:**  

-   Verteilungspunkt  

    -   Von Verteilungspunkten auf diesem Betriebssystem wird PXE nicht unterstützt.  

    -   Von Verteilungspunkten unter dieser Betriebssystemversion wird Multicast nicht unterstützt.  

    -   Verteilungspunkte unterstützen mehrere unterschiedliche Konfigurationen mit unterschiedlichen Anforderungen. In einigen Fällen unterstützen diese Konfigurationen die Installation nicht nur auf Servern, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den Optionen, die für Verteilungspunkte verfügbar sind, finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="the-server-core-installation-of-windows-server-version-1709"></a>Die Server Core-Installation von Windows Server, Version 1709
Ab Configuration Manager 1710 wird [Windows Server, Version 1709](https://docs.microsoft.com/windows-server/get-started/get-started-with-1709), mit folgenden Einschränkungen für die Verwendung als Verteilungspunkt unterstützt:  
  -   Nur die x64-Bit-Version wird unterstützt.
  -   Von Verteilungspunkten auf diesem Betriebssystem werden PXE und Multicast nicht unterstützt.  

## <a name="the-server-core-installation-of-windows-server-2016"></a>Die Server Core-Installation von Windows Server 2016
Dieses Betriebssystem wird durch das Hotfixrollup aus KB3186654 als Verteilungspunkt unterstützt. Dabei bestehen folgende Einschränkungen:  
  -   Nur die x64-Bit-Version wird unterstützt.
  -   Von Verteilungspunkten auf diesem Betriebssystem werden PXE und Multicast nicht unterstützt.  



## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>Die Server Core-Installation von Windows Server 2012 R2  
 Die Server Core-Installation von Windows Server 2012 R2 wird mit folgenden Einschränkungen für die Verwendung als Verteilungspunkte unterstützt:  

-   Nur die x64-Bit-Version wird unterstützt.

-   Von Verteilungspunkten auf diesem Betriebssystem werden PXE und Multicast nicht unterstützt.  



## <a name="the-server-core-installation-of-windows-server-2012"></a>Die Server Core-Installation von Windows Server 2012  
 Die Server Core-Installation von Windows Server 2012 wird mit folgenden Einschränkungen für die Verwendung als Verteilungspunkte unterstützt:  

-   Nur die 64-Bit-Version wird unterstützt.  

-   Von Verteilungspunkten auf diesem Betriebssystem werden PXE und Multicast nicht unterstützt.
