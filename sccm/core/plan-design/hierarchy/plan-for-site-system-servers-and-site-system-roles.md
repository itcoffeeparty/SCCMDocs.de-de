---
title: Planen von Standortsystemrollen | Microsoft Docs
description: Betrachten Sie die Standortsystemserver und Standortsystemrollen bei der Planung Ihrer System Center Configuration Manager-Hierarchie.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
caps.latest.revision: 11
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2b00cfcec0959716d69a1605018f33d30287fee9
ms.openlocfilehash: a2e57aac01fff3c28b4acfcf58bcd786bd3e62c4


---
# <a name="plan-for-site-system-servers-and-site-system-roles-for-system-center-configuration-manager"></a>Planen für Standortsystemserver und Standortsystemrollen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Jeder System Center Configuration Manager-Standort, den Sie installieren, umfasst einen Standortserver, bei dem es sich um einen **Standortsystemserver** handelt. Der Standort kann auch weitere Standortsystemserver auf Computern umfassen, die sich geografisch getrennt vom Standortserver befinden.   Die Standortsystemserver (der Standortserver oder ein Remotestandortsystemserver) unterstützen **Standortsystemrollen**.


##  <a name="a-namebkmksiteserversa-site-system-servers"></a><a name="bkmk_siteservers"></a> Standortsystemserver  
 Wenn Sie eine Standortsystemrolle auf einem Computer installieren, wird dieser Computer zu einem Standortsystemserver. Sie können an jedem Standortsystem mehrere zusätzliche Standortsystemserver installieren. Sie haben auch die Möglichkeit, keine weiteren Standortsystemserver zu installieren und alle Standortsystemrollen direkt auf dem Standortservercomputer auszuführen.  Jeder Standortsystemserver unterstützt mindestens eine Standortsystemrolle und erweitert die Funktionalität und Kapazität eines Standorts durch Aufteilen der CPU-Verarbeitungslast, die durch Standortsystemrollen auf einem Server entsteht.  

 Wenn Sie in Erwägung ziehen, einen Standortsystemserver hinzuzufügen, stellen Sie sicher, dass der Server die Voraussetzungen für die beabsichtigte Verwendung erfüllt und sich an einer Netzwerkadresse befindet, die über genügend Bandbreite zur Kommunikation mit den erwarteten Endpunkten verfügt. Zu diesen Endpunkten gehören der Standortserver, Domänenressourcen, cloudbasierte Speicherorte, Standortsystemserver sowie Clients.  

 Weitere Informationen zum Konfigurieren eines Standortsystemservers mit einem Proxy zur Verwendung durch die Standortsystemrollen finden Sie unter [Standortsystemrollen, die einen Proxyserver verwenden können](#bkmk_proxy).  

##  <a name="a-namebkmkplanrolesa-site-system-roles"></a><a name="bkmk_planroles"></a> Site system roles  
 Standortsystemrollen werden auf einem Computer installiert, um zusätzliche Funktionen am Standort bereitzustellen. Beispiele:  

-   Zusätzliche Verwaltungspunkte, damit ein Standort mehr Geräte verwalten kann (bis die unterstützte Kapazität des Standorts erreicht ist)  

-   Zusätzliche Verteilungspunkte für die Erweiterung Ihrer Inhaltsinfrastruktur, wodurch die Leistung bei der Verteilung Inhalt auf Geräte und Benutzer verbessert wird  

-   Eine oder mehrere featurespezifische Standortsystemrollen, z.B. ein Softwareupdatepunkt, die Sie zur Verwaltung von Softwareupdates für verwaltete Geräte verwenden, oder ein Reporting Services-Punkt, mit dem Sie Berichte zur Überwachung ausführen und Informationen über Ihre Bereitstellung sammeln oder freigeben können.  


Verschiedene Configuration Manager-Standorte können unterschiedliche Sätze von Standortsystemrollen unterstützen. Welche Standortsystemrollen unterstützt werden, richtet sich nach dem Typ des Standorts (Standort der zentralen Verwaltung, primärer Standort oder sekundärer Standort). Die Topologie Ihrer Hierarchie kann die Platzierung einiger Rollen bei bestimmten Standorttypen einschränken. Der Dienstverbindungspunkt wird z. B. nur am Standort auf der obersten Ebene der Hierarchie unterstützt – hierbei kann es sich um einen Standort der zentralen Verwaltung oder einen eigenständigen primären Standort handeln. Diese Rolle wird an einem untergeordneten primären Standort oder an sekundären Standorten nicht unterstützt.  

Nach der Installation eines Standorts können Sie einige Standortsystemrollen von ihrem ursprünglichen Speicherort auf dem Standortserver auf einen anderen Server verschieben (z.B. den Verwaltungs- oder den Verteilungspunkt, die standardmäßig auf einem primären oder einem sekundären Standortserver installiert werden). Sie können auch zusätzliche Instanzen einiger Standortsystemrollen installieren, um die Funktionalität Ihres Standorts zu erweitern (um mehr Dienste für Clients bereitzustellen) und Ihre geschäftlichen Anforderungen zu erfüllen. Einige Rollen sind erforderlich, andere dagegen optional:  

-   **Configuration Manager-Standortserver:** Diese Rolle identifiziert den Server, auf dem das Configuration Manager-Setup ausgeführt wird, um einen Standort oder den Server zu installieren, auf dem Sie einen sekundären Standort installieren. Diese Rolle kann nur verschoben oder deinstalliert werden, wenn der gesamte Standort deinstalliert wird.  

-   **Configuration Manager-Standortsystem:** Diese Rolle wird jedem Computer zugewiesen, auf dem Sie einen Standort oder eine Standortsystemrolle installieren.  Diese Rolle kann erst verschoben oder deinstalliert werden, wenn die letzte Standortsystemrolle von dem Computer entfernt wurde.  

-   **Configuration Manager-Komponenten:** Diese Rolle identifiziert ein Standortsystem, in dem eine Instanz des SMS-Executive-Diensts ausgeführt wird, und ist zur Unterstützung anderer Rollen erforderlich, z.B. von Verwaltungspunkten. Diese Rolle kann erst verschoben oder deinstalliert werden, wenn die letzte anwendbare Standortsystemrolle von dem Computer entfernt wurde.  

-   **Configuration Manager-Standortdatenbankserver:** Diese Rolle wird Standortsystemservern zugeordnet, auf denen sich eine Instanz der Standortdatenbank eines Standorts befindet.  Diese Rolle kann erst auf einen neuen Server verschoben werden, wenn der Standort für die Verwendung eines anderen SQL Servers zum Hosten der Standortdatenbank modifiziert wurde.  

-   **SMS-Anbieter:** Die SMS-Anbieterrolle wird jedem Computer zugewiesen, der eine Instanz des SMS-Anbieters hostet, der die Schnittstelle zwischen einer Configuration Manager-Konsole und der Standortdatenbank darstellt.  Diese Rolle wird standardmäßig automatisch auf dem Standortserver eines Standorts der zentralen Verwaltung und der primären Standorte installiert. Sie können an jedem Standort zusätzliche Instanzen installieren, um weiteren Administratoren Administratorzugriff auf den Standort zu gewähren.  

     Im Gegensatz zu den meisten Standortsystemrollen, die über die Konsole installiert werden, müssen Sie zum Verwalten des [SMS-Anbieters](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) das Setup für Configuration Manager-Setup ausführen, und die zusätzlichen Anbieter anschließend auf zusätzlichen Computern installieren. Sie können nur eine Instanz des SMS-Anbieters auf einem Computer installieren, und dieser Computer muss sich in derselben Domäne wie der Standortserver befinden.  

-   **Der Anwendungskatalog-Webdienstpunkt:** Über diese Standortsystemrolle werden der Anwendungskatalogwebsite Softwareinformationen aus der Softwarebibliothek bereitgestellt. Diese Rolle wird zwar nur an primären Standorten unterstützt, Sie können jedoch mehrere Instanzen dieser Rolle an einem Standort oder an mehreren Standorten in der gleichen Hierarchie installieren.  

-   **Der Anwendungskatalog-Websitepunkt:** Über diese Standortsystemrolle wird Benutzern eine Liste der im Anwendungskatalog verfügbaren Software bereitgestellt. Diese Rolle wird zwar nur an primären Standorten unterstützt, Sie können jedoch mehrere Instanzen dieser Rolle an einem Standort oder an mehreren Standorten in der gleichen Hierarchie installieren.  

     Wenn vom Anwendungskatalog Clientcomputer im Internet unterstützt werden, installieren Sie den Anwendungskatalog-Websitepunkt aus Sicherheitsgründen in einem Umkreisnetzwerk und den Anwendungskatalog-Webdienstpunkt im Intranet.  

-   **Der Asset Intelligence-Synchronisierungspunkt:** Über diese Standortsystemrolle wird eine Verbindung mit Microsoft hergestellt, um Asset Intelligence-Kataloginformationen herunterzuladen und nicht kategorisierte Titel zur künftigen Berücksichtigung im Katalog hochzuladen.  Eine Hierarchie unterstützt nur eine einzige Instanz dieser Rolle und diese muss sich am Standort der obersten Ebene Ihrer Hierarchie befinden (einem Standort der zentralen Verwaltung oder dem eigenständigen primären Standort). Wenn Sie einen eigenständigen primären Standort in eine größere Hierarchie erweitern, müssen Sie diese Rolle am primären Standort deinstallieren und können sie dann am Standort der zentralen Verwaltung installieren.   Weitere Informationen finden Sie unter [Asset Intelligence in System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Der Zertifikatregistrierungspunkt:** Diese Standortsystemrolle kommuniziert mit einem Server, auf dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird, um Gerätezertifikatanforderungen zu verwalten, für die das Simple Certificate Enrollment-Protokoll (SCEP) verwendet wird.  Diese Rolle wird nur an primären Standorten und am Standort der zentralen Verwaltung unterstützt.   Zwar kann ein einzelner Zertifikatregistrierungspunkt die erforderliche Funktionalität für die gesamte Hierarchie bereitstellen, um jedoch einen Lastenausgleich für Zertifikatsanforderungen bereitzustellen, können Sie mehrere Instanzen dieser Rolle an einem Standort sowie an mehreren Standorten in der gleichen Hierarchie installieren. Wenn in einer Hierarchie mehrere Instanzen vorhanden sind, werden Clients nach dem Zufallsprinzip einem der Zertifikatregistrierungspunkte zugewiesen.  

     Jeder Zertifikatregistrierungspunkt benötigt Zugriff auf eine separate Instanz eines Registrierungsdiensts für Netzwerkgeräte. Sie können die Verwendung desselben Registrierungsdiensts für Netzwerkgeräte nicht für zwei oder mehr Zertifikatregistrierungspunkte konfigurieren. Der Zertifikatregistrierungspunkt darf außerdem nicht auf dem Server installiert sein, auf dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird.  

- Der **Cloudverwaltungsgateway-Connectorpunkt** ist eine neue Standortsystemrolle für die Kommunikation mit dem [Cloudverwaltungsgateway](/sccm/core/clients/manage/setup-cloud-management-gateway). 

-   **Der Verteilungspunkt:** Dies ist eine Standortsystemrolle mit Quelldateien, die von Clients heruntergeladen werden können, darunter Anwendungsinhalt, Softwarepakete, Softwareupdates, Betriebssystemimages und Startimages. Diese Rolle wird bei der Installation neuer primärer und sekundärer Standorte standardmäßig auf dem Standortservercomputer dieser Standorte installiert. An einem Standort der zentralen Verwaltung wird diese Rolle jedoch nicht unterstützt.  Sie können mehrere Instanzen dieser Rolle an einem unterstützten Standort oder an mehreren Standorten in der gleichen Hierarchie installieren.  Weitere Informationen finden Sie unter [Fundamental concepts for content management in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) (Grundlegende Konzepte von Content Management in System Center Configuration Manager) und [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   **Der Fallbackstatuspunkt:** Über diese Standortsystemrolle können Sie die Clientinstallation überwachen und Clients ermitteln, die nicht verwaltet werden, weil die Kommunikation mit dem zugehörigen Verwaltungspunkt nicht möglich ist.  Diese Rolle wird zwar nur an primären Standorten unterstützt, Sie können jedoch mehrere Instanzen dieser Rolle an einem Standort oder an mehreren Standorten in der gleichen Hierarchie installieren.  Weitere Informationen finden Sie unter [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).


-   **Endpoint Protection-Punkt:** Mithilfe dieser Standortsystemrolle werden die Endpunkt Protection-Lizenzbedingungen in Configuration Manager akzeptiert und die Standardmitgliedschaft für Cloud Protection Service (ehemals MAPS) konfiguriert. Eine Hierarchie unterstützt nur eine einzige Instanz dieser Rolle und diese muss sich am Standort der obersten Ebene Ihrer Hierarchie befinden (einem Standort der zentralen Verwaltung oder dem eigenständigen primären Standort). Wenn Sie einen eigenständigen primären Standort in eine größere Hierarchie erweitern, müssen Sie diese Rolle am primären Standort deinstallieren und können sie dann am Standort der zentralen Verwaltung installieren. Weitere Informationen finden Sie unter [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   **Registrierungspunkt:** Diese Standortsystemrolle verwendet die PKI-Zertifikate für Configuration Manager, um mobile Geräte und Macintosh-Computer zu registrieren. Diese Rolle wird zwar nur an primären Standorten unterstützt, Sie können jedoch mehrere Instanzen dieser Rolle an einem Standort oder an mehreren Standorten in der gleichen Hierarchie installieren.  

     Wenn ein Benutzer mobile Geräte bei Configuration Manager registriert und sein Active Directory-Konto sich in einer Gesamtstruktur befindet, die von der Gesamtstruktur des Standortservers als nicht vertrauenswürdig eingestuft wird, müssen Sie in der Gesamtstruktur des Benutzers einen Registrierungspunkt installieren, damit der Benutzer authentifiziert werden kann.  

-   **Registrierungsproxypunkt:** Eine Standortsystemrolle, mit der Configuration Manager-Registrierungsanforderungen von mobilen Geräten und Macintosh-Computern verwaltet werden. Diese Rolle wird zwar nur an primären Standorten unterstützt, Sie können jedoch mehrere Instanzen dieser Rolle an einem Standort oder an mehreren Standorten in der gleichen Hierarchie installieren.  

     Wenn Sie mobile Geräte im Internet unterstützen, installieren Sie den Anmeldungsproxypunkt aus Sicherheitsgründen in einem Umkreisnetzwerk und den Anmeldungspunkt im Intranet.  

-   **Der Exchange Server-Connector:** Weitere Informationen finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

-   **Der Verwaltungspunkt:** Über diese Standortsystemrolle werden für Clients Informationen zu Richtlinien und der Dienstidentifizierung bereitgestellt. Darüber hinaus erhält sie Konfigurationsdaten von Clients.  
    Diese Rolle wird bei der Installation neuer primärer und sekundärer Standorte standardmäßig auf dem Standortservercomputer dieser Standorte installiert. Primäre Standorte unterstützen mehrere Instanzen dieser Rolle, und sekundäre Standorte unterstützen einen einzelnen Verwaltungspunkt, um einen lokalen Kontaktpunkt bereitzustellen, von dem Clients Computer- und Benutzerrichtlinien abrufen können (ein Verwaltungspunkt an einem sekundären Standort wird als Proxyverwaltungspunkt bezeichnet).  

     Verwaltungspunkte können zur Unterstützung von HTTP oder HTTPs sowie zur Unterstützung mobiler Geräte konfiguriert werden, die Sie mit der Verwaltung mobiler Geräte von System Center Configuration Manager verwalten. Sie können [Datenbankreplikate für Verwaltungspunkte für System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) verwenden, um die CPU-Last des Standortdatenbankservers mithilfe von Verwaltungspunkten zu verringern, da Verwaltungspunkte Anforderungen von Clients erfüllen.  

-   **Reporting Services-Punkt:** Diese Standortsystemrolle wird in SQL Server Reporting Services integriert, um Berichte für Configuration Manager zu erstellen und zu verwalten. Diese Rolle wird an primären Standorten und dem Standort der zentralen Verwaltung unterstützt, und Sie können mehrere Instanzen dieser Rolle an einem unterstützten Standort installieren. Weitere Informationen finden Sie unter [Planen der Berichterstellung in System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md).  

-   **Dienstverbindungspunkt:** Über diese Standortsystemrolle werden mobile Geräte mit Microsoft Intune und lokalem MDM verwaltet. Diese Rolle lädt auch Nutzungsdaten von Ihrem Standort hoch und ist erforderlich, um Updates für Configuration Manager durchzuführen, die in der Configuration Manager verfügbar sind. Eine Hierarchie unterstützt nur eine einzige Instanz dieser Rolle und diese muss sich am Standort der obersten Ebene Ihrer Hierarchie befinden (einem Standort der zentralen Verwaltung oder dem eigenständigen primären Standort). Wenn Sie einen eigenständigen primären Standort in eine größere Hierarchie erweitern, müssen Sie diese Rolle am primären Standort deinstallieren und können sie dann am Standort der zentralen Verwaltung installieren. Weitere Informationen finden Sie unter [Informationen zum Dienstverbindungspunkt in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   **Softwareupdatepunkt:** Diese Standortsystemrolle ist in Windows Server Update Services (WSUS) integriert, um Softwareupdates für Configuration Manager-Clients bereitzustellen. Diese Rolle wird an allen Standorten unterstützt:  

    -   Installieren Sie dieses Standortsystem am Standort der zentralen Verwaltung, um eine Synchronisierung mit Windows Server Update Services zu ermöglichen.  

    -   Konfigurieren Sie jede Instanz dieser Rolle an den primären untergeordneten Standorten so, dass eine Synchronisierung mit dem Standort der zentralen Verwaltung erfolgt.  

    -   Erwägen Sie, einen Softwareupdatepunkt an sekundären Standorten zu installieren, wenn die Datenübertragung über das Netzwerk langsam ist.  

    Weitere Informationen finden Sie unter [Planen von Softwareupdates in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

-   **Der Zustandsmigrationspunkt:** Über diese Standortsystemrolle wird der Benutzerzustandsdaten gespeichert, wenn ein Computer zu einem neuen Betriebssystem migriert wird. Diese Rolle wird an primären und sekundären Standorten unterstützt, und Sie können mehrere Instanzen dieser Rolle an einem Standort oder an mehreren Standorten in der gleichen Hierarchie installieren. Weitere Informationen zum Speichern des Benutzerzustands beim Bereitstellen eines Betriebssystems finden Sie unter [Verwalten des Benutzerzustands in System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   **Systemintegritätsprüfungspunkt:** Diese Standortsystemrolle wird mit System Center Configuration Manager nicht mehr verwendet, obwohl sie in der Configuration Manager-Konsole sichtbar bleibt.  

##  <a name="a-namebkmkproxya-site-system-roles-that-can-use-a-proxy-server"></a><a name="bkmk_proxy"></a> Standortsystemrollen, die einen Proxyserver verwenden können  
 Einige Configuration Manager-Standortsystemrollen erfordern eine Verbindung mit dem Internet und verwenden einen Proxyserver, wenn der Standortsystemserver, der die Rolle hostet, für einen Proxyserver konfiguriert ist. Normalerweise wird diese Verbindung im **Systemkontext** des Computers hergestellt, auf dem die Standortsystemrolle installiert ist. Für die Verbindung kann für die typischen Benutzerkonten keine Proxykonfiguration verwendet werden. Wenn für die Herstellung einer Internetverbindung ein Proxyserver erforderlich ist, müssen Sie den Computer für die Verwendung eines Proxyservers konfigurieren.  

-   Sie können während der Installation einer Standortsystemrolle einen Proxyserver konfigurieren.  

-   Sie können eine Proxyserverkonfiguration hinzufügen oder ändern, wenn Sie die Configuration Manager-Konsole verwenden.  

-   Alle Standortsystemrollen auf einem Standortsystemserver, die eine Proxyserverkonfiguration verwenden können, verwenden die gleiche Proxyserverkonfiguration. Wenn Sie andere Standortsystemrollen mit anderen Proxyservern benötigen, müssen Sie die Standortsystemrollen auf anderen Computern des Standortsystemservers installieren.  

-   Wenn Sie die Proxyserverkonfiguration ändern oder eine neue Standortsystemrolle auf einem Computer installieren, auf dem bereits eine Proxyserverkonfiguration vorhanden ist, wird die ursprüngliche Konfiguration durch die neue Konfiguration überschrieben.  


Informationen zu Prozeduren zum Konfigurieren des Proxyservers für Standortsystemrollen finden Sie im Thema [Hinzufügen von Standortsystemrollen für System Center Configuration Manager](../../../core/servers/deploy/configure/add-site-system-roles.md).  

Nachfolgend finden Sie die Standortsystemrollen, die einen Proxyserver verwenden können:  

-   **Der Asset Intelligence-Synchronisierungspunkt:** Diese Standortsystemrolle stellt eine Verbindung mit Microsoft her und verwendet eine Proxyserverkonfiguration auf dem Computer, auf dem der Asset Intelligence-Synchronisierungspunkt gehostet wird.  

-   **Der cloudbasierte Verteilungspunkt:** Wenn Sie einen cloudbasierten Verteilungspunkt verwenden, muss der primäre Standort, der den cloudbasierten Verteilungspunkt verwaltet, eine Verbindung zu Microsoft Azure herstellen können, um Inhalte auf dem Verteilungspunkt bereitstellen, überwachen und verteilen zu können. Wenn für diese Verbindung ein Proxyserver erforderlich ist, müssen Sie den Proxyserver auf dem primären Standortserver konfigurieren. Das Konfigurieren des Proxyservers auf einem cloudbasierten Verteilungspunkt unter Windows Azure ist nicht möglich.  Weitere Informationen finden Sie im Abschnitt [Configure proxy settings for primary sites that manage cloud services](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud) (Konfigurieren von Proxyeinstellungen für primäre Standorte, die Clouddienste verwalten) des Themas [Install cloud-based distribution points in Microsoft Azure for System Center Configuration Manager](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md) (Installieren von cloudbasierten Verteilungspunkten in Microsoft Azure für System Center Configuration Manager).  

-   **Der Exchange Server-Connector:** Diese Standortsystemrolle stellt eine Verbindung mit einem Exchange Server her und verwendet eine Proxyserverkonfiguration auf dem Computer, auf dem der Exchange Server-Connector gehostet wird.  

-   **Der Softwareupdatepunkt:** Diese Standortsystemrolle erfordert eventuell eine Verbindung zu Microsoft Update, um Patches herunterzuladen und Informationen zu Updates zu synchronisieren. Wenn Sie den Proxyserver konfigurieren, dann wird der Proxyserver in der Regel von jeder Standortsystemrolle auf dem Computer verwendet, der die Verwendung des Proxyservers unterstützt, ohne dass weitere Konfigurationen erforderlich sind. Eine Ausnahme ist hier der Softwareupdatepunkt. Standardmäßig werden von einem Softwareupdatepunkt keine verfügbaren Proxyserver verwendet, es sei denn, Sie haben die folgenden Optionen beim Konfigurieren des Softwareupdatepunkts aktiviert:  

    -   **Verwenden von Proxyserver beim Synchronisieren von Softwareupdates**  

    -   **Verwenden von Proxyserver beim Herunterladen von Inhalt mit automatischen Bereitstellungsregeln**  

    > [!TIP]  
    >  Ein Proxyserver muss auf dem Standortsystemserver konfiguriert werden, auf dem der Softwareupdatepunkt gehostet wird, bevor Sie eine Option auswählen können. Der Proxyserver wird nur für bestimmte Optionen verwendet, die Sie auswählen.  

 Weitere Informationen zu Proxyservern für Softwareupdatepunkte finden Sie im Abschnitt zu Proxyservereinstellungen im Thema [Softwareupdatepunkt installieren](../../../sum/get-started/install-a-software-update-point.md).  

-   **Dienstverbindungspunkt:** Wenn diese Standortsystemrolle nicht für die Offline-, sondern für die Onlineverwendung konfiguriert ist, stellt sie eine Verbindung zu Microsoft Intune und dem Microsoft-Clouddienst her.  



<!--HONumber=Jan17_HO4-->


