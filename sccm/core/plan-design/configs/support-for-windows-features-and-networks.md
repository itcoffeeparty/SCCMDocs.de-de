---
title: Unterstützung für Windows-Funktionen
titleSuffix: Configuration Manager
description: Hier erfahren Sie, welche Windows-und Netzwerkfeatures in System Center Configuration Manager unterstützt werden.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
caps.latest.revision: 8
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4a41efa9b4c33a77d6aa2fa9e806e24ae33cc330
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="support-for-windows-features-and-networks-in-system-center-configuration-manager"></a>Unterstützung für Windows-Features und -Netzwerke in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Artikel erfahren Sie mehr über die Configuration Manager-Unterstützung für übliche Windows- und Netzwerkfeatures.  


##  <a name="bkmk_branchcache"></a> BranchCache  
Sie können Windows BranchCache mit Configuration Manager verwenden, wenn Sie BranchCache auf Verteilungspunkten aktivieren und Clients zum Verwenden von BranchCache im Modus „Verteilter Cache“ konfigurieren.

Sie können die BranchCache-Einstellungen bei einem Bereitstellungstyp für Anwendungen, bei der Bereitstellung für ein Paket und für Tasksequenzen konfigurieren.  

Wenn die Voraussetzungen für BranchCache erfüllt sind, können mithilfe dieser Funktion Inhalte von lokalen Clients abgerufen werden, auf denen die Inhalte zwischengespeichert sind.  

Beispiel: Wenn der erste Client mit aktivierter BranchCache-Funktion Inhalt von einem Verteilungspunkt anfordert, der als BranchCache-Server konfiguriert ist, lädt der Client den Inhalt herunter und speichert ihn zwischen. Dieser Inhalt wird dann für Clients in dem Subnetz verfügbar, das den Inhalt auch angefordert hat.

Diese Clients führen auch eine Zwischenspeicherung des Inhalts durch. So müssen andere Clients im selben Subnetz den Inhalt nicht erneut vom Verteilungspunkt herunterladen. Der Inhalt ist für spätere Übertragungen über mehrere Clients verteilt.  

### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>Anforderungen für die Unterstützung von BranchCache mit Configuration Manager
-   **Verteilungspunkte konfigurieren:** Fügen Sie das Feature **BranchCache** zum Standortsystemserver hinzu, der als Verteilungspunkt konfiguriert ist.    
    -   Für Verteilungspunkte auf Servern, die für die Unterstützung von BranchCache konfiguriert sind, ist keine zusätzliche Konfiguration erforderlich.   
    -   Windows BranchCache kann keinem cloudbasierten Verteilungspunkt hinzugefügt werden. Der Download von Inhalt durch Clients, die für Windows BranchCache konfiguriert sind, wird von cloudbasierten Verteilungspunkten unterstützt.  

-   **Clients konfigurieren:**    
    -   Die Clients, die BranchCache unterstützen können, müssen für den BranchCache-Modus „Verteilter Cache“ konfiguriert werden.  
    -   Die Betriebssystemeinstellung für BITS-Clienteinstellungen muss zur Unterstützung von BranchCache aktiviert sein.   <br /> <br />

    Weitere Informationen finden Sie in der Windows-Dokumentation unter [Konfigurieren von Clients für BranchCache](https://docs.microsoft.com/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache).


### <a name="configuration-manager-supported-os-versions-with-windows-branchcache"></a>Von Configuration Manager unterstützte Versionen des Betriebssystems mit Windows BranchCache

|Betriebssystem|Details zur Unterstützung|  
|----------------------|---------------------|  
|Windows 7 mit SP1|Standardmäßig unterstützt|  
|Windows 8|Standardmäßig unterstützt|  
|Windows 8.1|Standardmäßig unterstützt|  
|Windows 10|Standardmäßig unterstützt|  
|Windows Server 2008 mit SP2|**Erfordert BITS 4.0**: Sie können BITS 4.0 mithilfe von Softwareupdates oder Softwareverteilung auf Configuration Manager-Clients installieren. Weitere Informationen finden Sie unter [Windows Management Framework (Windows PowerShell 2.0 WinRM 2.0 und BITS 4.0)](https://support.microsoft.com/help/968929/windows-management-framework-windows-powershell-2-0-winrm-2-0-and-bits).<br /><br /> Die BranchCache-Clientfunktion wird unter diesem Betriebssystem für die Softwareverteilung, die vom Netzwerk aus ausgeführt wird, oder für SMB-Dateiübertragungen nicht unterstützt. Darüber hinaus kann dieses Betriebssystem nicht die BranchCache-Funktionalität mit cloudbasierten Verteilungspunkten verwenden.|  
|Windows Server 2008 R2|Standardmäßig unterstützt|  
|Windows Server 2012|Standardmäßig unterstützt|  
|Windows Server 2012 R2|Standardmäßig unterstützt|  
|Windows Server 2016|Standardmäßig unterstützt|  

 Weitere Informationen zu BranchCache finden Sie in der Dokumentation zu Windows Server unter [BranchCache für Windows](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache).  



##  <a name="bkmk_Workgroups"></a> Computer in Arbeitsgruppen  
Configuration Manager stellt Unterstützung für Clients in Arbeitsgruppen bereit.  

-   Configuration Manager unterstützt das Verschieben eines Clients aus einer Arbeitsgruppe in eine Domäne bzw. aus einer Domäne in eine Arbeitsgruppe. Weitere Informationen finden Sie im Artikel [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md) im Abschnitt [Installieren von Clients auf Arbeitsgruppencomputern](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup).  

> [!NOTE]  
>  Obwohl Clients in Arbeitsgruppen unterstützt werden, müssen alle Standortsysteme Mitglieder einer unterstützten Active Directory-Domäne sein.  



##  <a name="bkmmk_datadedup"></a> Datendeduplizierung  
Configuration Manager unterstützt die Verwendung der Datendeduplizierung mit Verteilungspunkten unter den folgenden Betriebssystemen:  

-   Windows Server 2016
-   Windows Server 2012 R2  
-   Windows Server 2012  


> [!IMPORTANT]  
>  Das Volume, das Paketquelldateien hostet, kann nicht für die Datendeduplizierung gekennzeichnet werden. Dies liegt daran, dass die Datendeduplizierung Analysepunkte verwendet und Configuration Manager keinen Inhaltsquellspeicherort mit Dateien unterstützt, die auf Analysepunkten gespeichert sind.  

Weitere Informationen finden Sie unter [Configuration Manager Distribution Points and Windows Server 2012 Data Deduplication (Configuration Manager-Verteilungspunkte und Windows Server 2012-Datendeduplizierung)](https://cloudblogs.microsoft.com/enterprisemobility/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication/) auf dem Configuration Manager-Teamblog und in der Windows Server-Dokumentation unter [Datendeduplizierung (Übersicht)](https://docs.microsoft.com/windows-server/storage/data-deduplication/overview).  



##  <a name="bkmk_DA"></a> DirectAccess  
Configuration Manager unterstützt das DirectAccess-Feature für die Kommunikation zwischen Clients und Standortserversystemen.  

-   Wenn alle Voraussetzungen für DirectAccess erfüllt sind, ermöglicht DirectAccess Configuration Manager-Clients, im Internet mit ihrem zugewiesenen Standort zu kommunizieren, als befänden sie sich im Intranet.  

-   Für serverseitig initiierte Aktionen, z.B. die Remotesteuerung und Clientpushinstallation, muss auf dem initiierenden Computer IPv6 ausgeführt werden. Dieses Protokoll muss auf allen beteiligten Netzwerkgeräten unterstützt werden.  

Configuration Manager bietet keine DirectAccess-Unterstützung für folgende Funktionalität:  

-   Bereitstellung von Betriebssystemen  

-   Kommunikation zwischen Configuration Manager-Standorten  

-   Kommunikation zwischen Configuration Manager-Standortsystemservern innerhalb eines Standorts  



##  <a name="bkmk_dualboot"></a> Dual-Boot-Computer  
 Configuration Manager kann nur jeweils ein Betriebssystem pro Computer verwalten. Wenn auf einem zu verwaltenden Computer mehr als ein Betriebssystem installiert ist, müssen Sie die Ermittlungs- und Installationsmethoden des Standorts so anpassen, dass gewährleistet wird, dass der Configuration Manager-Client nur unter dem zu verwaltenden Betriebssystem installiert wird.  



##  <a name="bkmk_IPv6"></a> Internet Protocol, Version 6  
 Configuration Manager unterstützt sowohl Internetprotokoll Version 4 (IPv4) als auch Internetprotokoll Version 6 (IPv6). Dabei gelten folgende Ausnahmen:  

|Funktion| Ausnahmen bei der IPv6-Unterstützung|  
|--------------|-------------------------------|  
|Cloudbasierte Verteilungspunkte|IPv4 ist erforderlich, um Microsoft Azure- und cloudbasierte Verteilungspunkte zu unterstützen.|  
|Cloudverwaltungsgateway|IPv4 ist erforderlich, um Microsoft Azure- und Cloud Management Gateway zu unterstützen.|  
|Mobilgeräte, die von Microsoft Intune und dem Microsoft-Dienstconnector registriert werden|IPv4 ist für die Unterstützung mobiler Geräte erforderlich, die von Microsoft Intune und dem Microsoft-Dienstconnector registriert werden.|  
|Netzwerkermittlung|IPv4 ist erforderlich, wenn Sie für die Suche bei der Netzwerkermittlung einen DHCP-Server konfigurieren.|  
|Bereitstellung des Betriebssystems|IPv4 ist für die Unterstützung des Betriebssystems erforderlich. |  
|Aktivierungsproxykommunikation|IPv4 ist für die Unterstützung von Aktivierungsproxypaketen auf dem Client erforderlich.|  
|Windows CE|IPv4 ist für die Unterstützung des Configuration Manager-Clients auf Windows CE-Geräten erforderlich.|  



##  <a name="bkmk_NAT"></a> Netzwerkadressübersetzung (Netzwerkadressübersetzung (Network Address Translation, NAT), NAT)  
 Die Netzwerkadressenübersetzung wird in Configuration Manager nicht unterstützt, es sei denn, der Standort unterstützt Clients aus dem Internet, und der Client erkennt, dass er mit dem Internet verbunden ist. Weitere Informationen zur internetbasierten Clientverwaltung finden Sie unter [Planen der internetbasierten Clientverwaltung in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-for-managing-internet-based-clients.md).  



##  <a name="bkmk_storage"></a> Spezielle Speichertechnologien  
 Configuration Manager ist für die Hardware ausgelegt, die auf der Windows-Hardwarekompatibilitätsliste für die unterstützte Version des Betriebssystems zertifiziert ist, auf dem die Configuration Manager-Komponente installiert ist.

Für Standortserverrollen ist NTFS erforderlich, damit Configuration Manager Verzeichnis- und Dateiberechtigungen festlegen kann. Configuration Manager geht davon aus, dass es das logische Laufwerk vollständig besitzt. Standortsysteme auf separaten Computern können in keiner Speichertechnologie logische Partitionen gemeinsam nutzen. Allerdings kann von jedem Computer eine separate logische Partition auf der gleichen physischen Partition eines gemeinsam genutzten Speichergeräts verwendet werden.  

 ### <a name="support-considerations"></a>Überlegungen zur Unterstützung

-   **Storage Area Network (SAN)**: Ein SAN wird unterstützt, wenn ein unterstützter Windows-basierter Server direkt mit dem vom SAN gehosteten Volume verbunden ist.  

-   **Single Instance Storage (SIS)**: Das Konfigurieren von Verteilungspunktpaketen und Signaturordnern in einem SIS-fähigen (Single Instance Storage) Volume wird von Configuration Manager nicht unterstützt.  

     Darüber hinaus wird der Configuration Manager-Clientcache auf einem SIS-fähigen Volume nicht unterstützt.  

-   **Laufwerk mit Wechselmedien**: Die Installation von Configuration Manager-Standortsystemen oder -Clients auf einem Laufwerk mit Wechselmedien wird von Configuration Manager nicht unterstützt.  
