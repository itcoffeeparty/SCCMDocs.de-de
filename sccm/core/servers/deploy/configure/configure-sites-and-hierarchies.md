---
title: Konfigurieren von Standorten | System Center Configuration Manager
description: "Stellen Sie anhand dieser Prüfliste sicher, dass Sie die am häufigsten verwendeten Konfigurationen berücksichtigen, die Standorte und Hierarchien betreffen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: 15
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 470efc428045398588345f4546eb27831837715c


---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>Konfigurieren von Standorten und Hierarchien für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Nachdem Sie Ihren ersten System Center Configuration Manager-Standort installiert und Ihrer Hierarchie weitere Standorte hinzugefügt haben, nutzen Sie die folgende Prüfliste, um sicherzustellen, dass Sie die gängigsten Konfigurationen berücksichtigen, die sich sowohl auf Standorte als auch auf Hierarchien auswirken.  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>Prüfliste für gängige Konfigurationen neuer und zusätzlicher Standorte  
 Bei den meisten Bereitstellungen können Sie die folgenden Optionen in beliebiger Reihenfolge konfigurieren:  

-   Einige dieser Optionen, wie z. B. Ermittlung von Active Directory-Gesamtstrukturen, Grenzen und Begrenzungsgruppen, bauen allerdings aufeinander auf.  

-   Bei verschiedenen Konfigurationen können Sie, zumindest vorübergehend, die Standardwerte ohne Änderungen verwenden.  

-   Andere Konfigurationen, wie z. B. Begrenzungsgruppen und Verteilungspunktgruppen, müssen Sie dagegen konfigurieren, bevor Sie sie verwenden können.  

|Aktion|Details|  
|------------|-------------|  
|Konfigurieren der rollenbasierten Verwaltung|Die rollenbasierte Verwaltung dient zum Trennen administrativer Zuständigkeiten, um zu steuern, welche Administratoren verschiedene Objekte und Daten in Ihrer Configuration Manager-Umgebung anzeigen und verwalten können.<br /><br /> Konfigurationen der rollenbasierten Verwaltung werden von allen Standorten der Hierarchie gemeinsam genutzt.   <br />Weitere Informationen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung für System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).|  
|Veröffentlichen von Standortdaten in Active Directory-Domänendienste (AD DS)|Durch Veröffentlichen von Daten in AD DS erleichtern Sie Clients das Auffinden von Diensten und effiziente Nutzen von Standortressourcen.<br /><br /> Sie müssen [das Active Directory-Schema für System Center Configuration Manager zunächst erweitern](../../../../core/plan-design/network/extend-the-active-directory-schema.md) und anschließend jeden Standort einzeln konfigurieren, um [Standortdaten für System Center Configuration Manager zu veröffentlichen](../../../../core/servers/deploy/configure/publish-site-data.md).|  
|Konfigurieren eines Dienstverbindungspunkts|Für den Standort auf der obersten Ebene Ihrer Hierarchie müssen Sie die Installation und Konfiguration des Dienstverbindungspunkts planen. Informationen hierzu finden Sie unter [Informationen zum Dienstverbindungspunkt in System Center Configuration Manager](../../../../core/servers/deploy/configure/about-the-service-connection-point.md).|  
|Hinzufügen von Standortsystemrollen|Installieren und konfigurieren Sie für einzelne Standorte zusätzliche Standortsystemrollen.  Informationen finden Sie unter [Add site system roles for System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md).|  
|Konfigurieren von Grenzen und Begrenzungsgruppen für Standorte|Legen Sie Grenzen fest, die Netzwerkadressen in Ihrem Intranet definieren und zu verwaltende Geräte enthalten können. Konfigurieren Sie anschließend Begrenzungsgruppen, damit Clients mit diesen Netzwerkadressen Ressourcen von Configuration Manager-Diensten finden können. Informationen hierzu finden Sie unter [Definieren von Standortgrenzen und Begrenzungsgruppen für Configuration Manager](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).|  
|Konfigurieren von Verteilungspunktgruppen|Konfigurieren Sie logische Gruppen von Verteilungspunkten, um das Verwalten von Bereitstellungen zu vereinfachen. Informationen hierzu finden Sie im Abschnitt [Manage distribution point groups](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) (Verwalten von Verteilungspunktgruppen) in dem Artikel [Install and configure distribution points for System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) (Installieren und Konfigurieren von Verteilungspunkten für Configuration Manager).|  
|Ausführen der Ermittlung|Führen Sie die Ermittlung aus, um Ressourcen in Ihrem Netzwerk zu finden, z. B. Netzwerkinfrastruktur, Geräte und Benutzer.<br /><br /> Informationen finden Sie unter [Run discovery for System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md).|  
|Hinzufügen von Redundanz und Kapazität für Administratoren Ihrer Infrastruktur|Sie können zusätzliche SMS-Anbieter und Configuration Manager-Konsolen installieren, um Administratoren mehr Kapazität für das Verwalten Ihrer Infrastruktur zu bieten:<br /><br /> **Installieren Sie zusätzliche SMS-Anbieter** , um Redundanz für Kontaktpunkte zur Verwaltung des Standorts und der Hierarchie bereitzustellen. Siehe [Manage the SMS Provider](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) in [Modify your System Center Configuration Manager infrastructure](../../../../core/servers/manage/modify-your-infrastructure.md).<br /><br /> **Installieren Sie zusätzliche Configuration Manager-Konsolen** , um weiteren Administratoren einen gleichzeitigen Zugriff zu bieten. Informationen hierzu finden Sie unter [Install Configuration Manager consoles](../../../../core/servers/deploy/install/install-consoles.md) (Installieren von Configuration Manager-Konsolen).|  
|Konfigurieren von Standortkomponenten|An jedem Standort können Sie Standortkomponenten konfigurieren, um das Verhalten von Standortsystemrollen und die Statusberichterstattung des Standorts zu ändern. Informationen finden Sie unter [Site components for System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md).|  
|Erstellen benutzerdefinierter Sammlungen|Erstellen Sie anhand ermittelter Informationen zu Geräten und Benutzern benutzerdefinierte Sammlungen von Objekten zum Vereinfachen künftiger Verwaltungsaufgaben. Informationen hierzu finden Sie unter [Erstellen von Sammlungen in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|Konfigurieren von Einstellungen zum Verwalten risikoreicher Bereitstellungen|Sie können Einstellungen an einem Standort konfigurieren, über die Administratoren gewarnt werden, wenn sie eine Bereitstellung mit risikoreicher Tasksequenz erstellen.  Informationen finden Sie unter [Settings to manage high-risk deployments for System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md).|  
|Konfigurieren von Datenbankreplikaten für Verwaltungspunkte|Konfigurieren Sie ein Datenbankreplikat zum Verringern der CPU-Last des Standortdatenbankservers mithilfe von Verwaltungspunkten, die Anforderungen von Clients erfüllen. Informationen finden Sie unter [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).|  
|Konfigurieren einer SQL Server-AlwaysOn-Verfügbarkeitsgruppe zum Hosten der Standortdatenbank|Ab Version 1602 können Sie Verfügbarkeitsgruppen als Lösung für hohe Verfügbarkeit und Notfallwiederherstellung zum Hosten der Standortdatenbank an primären Standorten und am Standort der zentralen Verwaltung nutzen. Informationen hierzu finden Sie unter [SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) (SQL Server Always On für eine hoch verfügbare Standortdatenbank für System Center Configuration Manager).|  
|Ändern der Replikation zwischen Standorten|Lesen Sie den Artikel [Datenübertragungen zwischen Standorten in System Center Configuration Manager](../../../../core/servers/manage/data-transfers-between-sites.md), um mehr über die folgenden Themen zu erfahren:<br /><br /> Konfigurieren von [File-based replication](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute) zwischen sekundären Standorten<br /><br /> Konfigurieren von [Database replication links](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> Konfigurieren von [Distributed views](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  



<!--HONumber=Nov16_HO1-->


