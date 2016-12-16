---
title: "Unterstützte Standortsystemserver | System Center Configuration Manager"
description: "Erfahren Sie, welche Windows-Versionen Sie verwenden können, um einen System Center Configuration Manager-Standort oder eine entsprechende Standortsystemrolle zu hosten."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 44
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 00d5d8d9ce90b2da79485250d25f943ca1c4547b


---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>Unterstützte Betriebssysteme für System Center Configuration Manager-Standortsystemserver

*Gilt für: System Center Configuration Manager (Current Branch)*


In diesem Artikel wird beschrieben, welche Windows-Versionen Sie verwenden können, um einen System Center Configuration Manager-Standort oder eine entsprechende Standortsystemrolle zu hosten.


Verwenden Sie die Informationen in diesem Thema mit den Informationen in den folgenden Artikeln:
-   [Empfohlene Hardware für Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Site and site system prerequisites for Configuration Manager (Standort- und Standortsystemvoraussetzungen für Configuration Manager)](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Size and scale numbers for Configuration Manager (Größe und Skalierung von Zahlen für Configuration Manager)](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016---standard-datacenter"></a>Windows Server 2016 – Standard, Datacenter
Windows Server 2016 wird ab Configuration Manager Release 1606 mit dem Hotfixrollup von KB3186654 (oder Baselineversion 1606, die im Oktober 2016 veröffentlicht wurde) unterstützt.

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

     Verteilungspunkte können unter mehreren unterschiedlichen Konfigurationen mit jeweils verschiedenen Anforderungen verwendet werden. In einigen Fällen ist die Installation nicht nur auf Servern möglich, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den für Verteilungspunkte verfügbaren Optionen finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection-Punkt  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

-   Fallbackstatuspunkt  

-   Reporting Services-Punkt  

-   Dienstverbindungspunkt  

-   Standortdatenbankserver  

     Standortdatenbankserver werden auf einem Domänencontroller ohne Schreibzugriff (Read-Only Domain Controller, RODC) nicht unterstützt. Weitere Informationen finden Sie unter [You may encounter problems when installing SQL Server on a domain controller (Beim Installieren eines SQL Servers auf einem Domänencontroller treten möglicherweise Probleme auf)](http://go.microsoft.com/fwlink/p/?LinkId=264856) in der Microsoft Knowledge Base. Darüber hinaus werden sekundäre Standortserver nicht auf jedem Domänencontroller unterstützt.  

-   SMS-Anbieter  

-   Softwareupdatepunkt  

-   Zustandsmigrationspunkt

## <a name="windows-server-2012-r2-x64---standard-datacenter"></a>Windows Server 2012 R2 (x64) – Standard, Datacenter  
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

     Verteilungspunkte können unter mehreren unterschiedlichen Konfigurationen mit jeweils verschiedenen Anforderungen verwendet werden. In einigen Fällen ist die Installation nicht nur auf Servern möglich, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den für Verteilungspunkte verfügbaren Optionen finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection-Punkt  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

-   Fallbackstatuspunkt  

-   Reporting Services-Punkt  

-   Dienstverbindungspunkt  

-   Standortdatenbankserver  

     Standortdatenbankserver werden auf einem Domänencontroller ohne Schreibzugriff (Read-Only Domain Controller, RODC) nicht unterstützt. Weitere Informationen finden Sie unter [You may encounter problems when installing SQL Server on a domain controller (Beim Installieren eines SQL Servers auf einem Domänencontroller treten möglicherweise Probleme auf)](http://go.microsoft.com/fwlink/p/?LinkId=264856) in der Microsoft Knowledge Base. Darüber hinaus werden sekundäre Standortserver nicht auf jedem Domänencontroller unterstützt.  

-   SMS-Anbieter  

-   Softwareupdatepunkt  

-   Zustandsmigrationspunkt  

## <a name="windows-server-2012-x64---standard-datacenter"></a>Windows Server 2012 (x64) – Standard, Datacenter  
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

     Verteilungspunkte können unter mehreren unterschiedlichen Konfigurationen mit jeweils verschiedenen Anforderungen verwendet werden. In einigen Fällen ist die Installation nicht nur auf Servern möglich, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den für Verteilungspunkte verfügbaren Optionen finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection-Punkt  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

-   Fallbackstatuspunkt  

-   Reporting Services-Punkt  

-   Dienstverbindungspunkt  

-   Standortdatenbankserver  

     Standortdatenbankserver werden auf einem Domänencontroller ohne Schreibzugriff (Read-Only Domain Controller, RODC) nicht unterstützt. Weitere Informationen finden Sie unter [You may encounter problems when installing SQL Server on a domain controller (Beim Installieren eines SQL Servers auf einem Domänencontroller treten möglicherweise Probleme auf)](http://go.microsoft.com/fwlink/p/?LinkId=264856) in der Microsoft Knowledge Base. Darüber hinaus werden sekundäre Standortserver nicht auf jedem Domänencontroller unterstützt.  

-   SMS-Anbieter  

-   Softwareupdatepunkt  

-   Zustandsmigrationspunkt  

## <a name="windows-server-2008-r2-with-sp1-x64---standard-enterprise-datacenter"></a>Windows Server 2008 R2 mit SP1 (x64) – Standard, Enterprise, Datacenter  
 Windows Server 2008 R2 unterliegt nun dem erweiterten Support und nicht mehr dem grundlegenden Support, wie im  [Microsoft-Support-Lifecycle](https://support.microsoft.com/lifecycle)ausführlich erläutert. Weitere Informationen bezüglich des zukünftigen Supports für diese Betriebssysteme als Standortsysteme mit Configuration Manager finden Sie unter [Entfernte und veraltete Features für System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

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

     Verteilungspunkte können unter mehreren unterschiedlichen Konfigurationen mit jeweils verschiedenen Anforderungen verwendet werden. In einigen Fällen ist die Installation nicht nur auf Servern möglich, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den für Verteilungspunkte verfügbaren Optionen finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection-Punkt  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

-   Fallbackstatuspunkt  

-   Reporting Services-Punkt  

-   Dienstverbindungspunkt  

-   Standortdatenbankserver  

     Standortdatenbankserver werden auf einem Domänencontroller ohne Schreibzugriff (Read-Only Domain Controller, RODC) nicht unterstützt. Weitere Informationen finden Sie unter [You may encounter problems when installing SQL Server on a domain controller (Beim Installieren eines SQL Servers auf einem Domänencontroller treten möglicherweise Probleme auf)](http://go.microsoft.com/fwlink/p/?LinkId=264856) in der Microsoft Knowledge Base. Darüber hinaus werden sekundäre Standortserver nicht auf jedem Domänencontroller unterstützt.  

-   SMS-Anbieter  

-   Softwareupdatepunkt  

-   Zustandsmigrationspunkt  

## <a name="windows-server-2008-with-sp2-x86-x64---standard-enterprise-datacenter"></a>Windows Server 2008 mit SP2 (x86, x64) – Standard, Enterprise, Datacenter  
 Windows Server 2008 unterliegt nun dem erweiterten Support und nicht mehr dem grundlegenden Support, wie im  [Microsoft-Support-Lifecycle](https://support.microsoft.com/lifecycle)ausführlich erläutert. Weitere Informationen bezüglich des zukünftigen Supports für diese Betriebssysteme als Standortsysteme mit Configuration Manager finden Sie unter [Entfernte und veraltete Features für System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

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

    -   Von Verteilungspunkten unter diesem Betriebssystem wird Multicast nicht unterstützt.  

    -   Verteilungspunkte unter dieser Betriebssystemversion werden für PXE unterstützt, sie unterstützen jedoch keinen Netzwerkstart von Clientcomputern im EFI-Modus. Clientcomputer mit BIOS oder EFI-Start im Legacymodus werden unterstützt.  

    -   Verteilungspunkte können unter mehreren unterschiedlichen Konfigurationen mit jeweils verschiedenen Anforderungen verwendet werden. In einigen Fällen ist die Installation nicht nur auf Servern möglich, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den für Verteilungspunkte verfügbaren Optionen finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection-Punkt  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

-   Fallbackstatuspunkt  

-   Reporting Services-Punkt  

-   Dienstverbindungspunkt  

-   Standortdatenbankserver  

     Standortdatenbankserver werden auf einem Domänencontroller ohne Schreibzugriff (Read-Only Domain Controller, RODC) nicht unterstützt. Weitere Informationen finden Sie unter [You may encounter problems when installing SQL Server on a domain controller (Beim Installieren eines SQL Servers auf einem Domänencontroller treten möglicherweise Probleme auf)](http://go.microsoft.com/fwlink/p/?LinkId=264856) in der Microsoft Knowledge Base. Darüber hinaus werden sekundäre Standortserver nicht auf jedem Domänencontroller unterstützt.  

-   SMS-Anbieter  

-   Softwareupdatepunkt  

-   Zustandsmigrationspunkt  

## <a name="windows-10-x86-x64---pro-enterprise"></a>Windows 10 (x86, x64) – Pro, Enterprise  
**Standortsystemserver:**  

-   Verteilungspunkt  

    -   Für PXE werden Verteilungspunkte unter diesem Betriebssystem nicht unterstützt.  

    -   Von Verteilungspunkten unter dieser Betriebssystemversion wird Multicast nicht unterstützt.  

    -   Verteilungspunkte können unter mehreren unterschiedlichen Konfigurationen mit jeweils verschiedenen Anforderungen verwendet werden. In einigen Fällen ist die Installation nicht nur auf Servern möglich, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den für Verteilungspunkte verfügbaren Optionen finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-81-x86-x64---professional-enterprise"></a>Windows 8.1 (x86, x64) – Professional, Enterprise  
**Standortsystemserver:**  

-   Verteilungspunkt  

    -   Für PXE werden Verteilungspunkte unter diesem Betriebssystem nicht unterstützt.  

    -   Von Verteilungspunkten unter dieser Betriebssystemversion wird Multicast nicht unterstützt.  

    -   Verteilungspunkte können unter mehreren unterschiedlichen Konfigurationen mit jeweils verschiedenen Anforderungen verwendet werden. In einigen Fällen ist die Installation nicht nur auf Servern möglich, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den für Verteilungspunkte verfügbaren Optionen finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-8-x86-x64---professional-enterprise-distribution-point"></a>Windows 8 (x86, x64) – Professional, Enterprise Verteilungspunkt  
**Standortsystemserver:**  

-   Verteilungspunkt  

    -   Für PXE werden Verteilungspunkte unter diesem Betriebssystem nicht unterstützt.  

    -   Von Verteilungspunkten unter dieser Betriebssystemversion wird Multicast nicht unterstützt.  

    -   Verteilungspunkte können unter mehreren unterschiedlichen Konfigurationen mit jeweils verschiedenen Anforderungen verwendet werden. In einigen Fällen ist die Installation nicht nur auf Servern möglich, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den für Verteilungspunkte verfügbaren Optionen finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-7-with-sp1-x86-x64---professional-enterprise-ultimate"></a>Windows 7 mit SP1 (x86, x64) – Professional, Enterprise, Ultimate  
**Standortsystemserver:**  

-   Verteilungspunkt  

    -   Für PXE werden Verteilungspunkte unter diesem Betriebssystem nicht unterstützt.  

    -   Von Verteilungspunkten unter dieser Betriebssystemversion wird Multicast nicht unterstützt.  

    -   Verteilungspunkte können unter mehreren unterschiedlichen Konfigurationen mit jeweils verschiedenen Anforderungen verwendet werden. In einigen Fällen ist die Installation nicht nur auf Servern möglich, sondern auch auf Clientbetriebssystemen. Weitere Informationen zu den für Verteilungspunkte verfügbaren Optionen finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="the-server-core-installation-of-windows-server-2012"></a>Die Server Core-Installation von Windows Server 2012  
 Zusätzlich zu den vorherigen Betriebssystemen wird die Server Core-Installation von Windows Server 2012 mit folgenden Einschränkungen für die Verwendung als Verteilungspunkte unterstützt:  

-   Nur x64 wird unterstützt.  

-   Von Verteilungspunkten unter diesem Betriebssystem wird PXE oder Multicast nicht unterstützt.  

## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>Die Server Core-Installation von Windows Server 2012 R2  
 Zusätzlich zu den vorherigen Betriebssystemen wird die Server Core-Installation von Windows Server 2012 R2 mit folgenden Einschränkungen für die Verwendung als Verteilungspunkte unterstützt:  

-   Nur x64 wird unterstützt.  

-   Von Verteilungspunkten unter diesem Betriebssystem wird PXE oder Multicast nicht unterstützt.  



<!--HONumber=Nov16_HO1-->


