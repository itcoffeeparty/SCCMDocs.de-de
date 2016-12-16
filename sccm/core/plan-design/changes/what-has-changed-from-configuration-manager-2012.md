---
title: "Änderungen im Vergleich zu Configuration Manager 2012 | System Center Configuration Manager "
description: "Identifizieren Sie die Änderungen und neuen Funktionen in System Center Configuration Manager im Vergleich zu System Center 2012 Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
caps.latest.revision: 51
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0f3b68fb17920b0abacc1428c8763ec8c06e6b22


---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>Änderungen in System Center Configuration Manager im Vergleich zu System Center 2012 Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 System Center Configuration Manager Current Branch bringt wichtige Änderungen von System Center 2012 Configuration Manager mit sich. Die Informationen dieses Themas geben die wichtigsten Änderungen und neue Funktionen in der Baselineversion 1511 von System Center Configuration Manager an. Informationen zu zusätzlichen Änderungen, die in nachfolgenden Updates für System Center Configuration Manager eingeführt werden, finden Sie unter [Neuerungen in inkrementellen Versionen von System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).



 Das Dezember 2015-Release von System Center Configuration Manager (Release 1511) ist das neueste Produktrelease von Configuration Manager von Microsoft.   Er wird in der Regel als System Center Configuration Manager (Current Branch) bezeichnet. *Current Branch* gibt an, dass es sich hierbei um eine Version handelt, die inkrementelle Updates für das Produkt unterstützt und als wichtiger Unterschied zwischen diesem Release und alten Releases von Configuration Manager fungiert.  

 Bei diesem Release von System Center Configuration Manager gilt:  

-   Im Produktnamen wird kein Jahr und keine Produkt-ID verwendet, wie bei früheren Versionen wie Configuration Manager 2007 oder System Center 2012 Configuration Manager.

-   Unterstützt inkrementelle produktinterne Updates, sogenannte Upateversionen. Das erste Release ist Version 1511. Nachfolgende Versionen werden mehrmals im Jahr als konsoleninterne Updates veröffentlicht, z.B. Version 1602 oder 1606.




##  <a name="a-namebkmkupdatesa-in-console-updates-for-configuration-manager"></a><a name="bkmk_updates"></a> Konsoleninterne Updates für Configuration Manager  
 System Center Configuration Manager verwendet eine konsoleninterne Wartungsmethode namens **Updates und Wartung**, mit der Sie empfohlene Updates für Configuration Manager leicht finden und installieren können.  

 Einige Versionen stehen nur als Updates für vorhandene Standorte (innerhalb der Configuration Manager-Konsole) zur Verfügung und können nicht zur Installation neuer Configuration Manager-Standorte verwendet werden.   
Das Update 1602 ist z.B. nur in der Configuration Manager-Konsole verfügbar und dient zum Aktualisieren eines Standorts, an dem die Baselineversion 1511 ausgeführt wird, auf Version 1602.  

Eine Updateversion wird in regelmäßigen Abständen auch als neue Baselineversion veröffentlicht (z.B. Update 1606), die zur Installation einer neuen Hierarchie verwendet werden kann, sodass Sie mit keiner älteren Baselineversion (z.B. 1511) beginnen müssen und viele Upgrades bis hin zur neuesten Version durchführen müssen.


 Weitere Informationen zum Verwenden von Updates finden Sie unter [Updates für System Center Configuration Manager](../../../core/servers/manage/updates.md).  

##  <a name="a-namebkmkservicepointa-service-connection-point-replaces-microsoft-intune-connector"></a><a name="bkmk_servicepoint"></a> Dienstverbindungspunkt ersetzt Microsoft Intune-Connector  
 Der **Microsoft Intune-Connector** wird durch eine neue Standortsystemrolle ersetzt, die zusätzliche Funktionalität ermöglicht, den **Dienstverbindungspunkt**. Aufgaben des Dienstverbindungspunkts:  

-   Ersetzt den Microsoft Intune-Connector, wenn Sie Intune in die lokale Verwaltung mobiler Geräte von System Center Configuration Manager integrieren  

-   Dient als Kontaktpunkt für Geräte, die Sie mit verwalten  

-   Lädt Nutzungsdaten zu Ihrer Bereitstellung in den Microsoft-Clouddienst hoch  

-   Macht Updates, die für Ihre Bereitstellung gelten, innerhalb der Configuration Manager-Konsole verfügbar  

Diese Standortsystemrolle unterstützt sowohl eine Online- als auch Offlinevorgehensweise, die sich auf ihre weitere Verwendung auswirken kann. Weitere Informationen finden Sie unter [Informationen zum Dienstverbindungspunkt in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

##  <a name="a-namebkmkusagea-usage-data-collection"></a><a name="bkmk_usage"></a> Sammeln von Verwendungsdaten  
 System Center Configuration Manager sammelt Nutzungsdaten zu Ihren Standorten und Ihrer Infrastruktur. Diese Informationen werden zusammengestellt und über den Dienstverbindungspunkt (eine neue Standortsystemrolle) an den Microsoft-Clouddienst übermittelt. Sie sind erforderlich, um Configuration Manager für das Herunterladen von Updates für Ihre Bereitstellung zu aktivieren, die für die von Ihnen verwendete Version von Configuration Manager gelten. Wenn Sie den Dienstverbindungspunkt konfigurieren, können Sie Folgendes konfigurieren: die Ebene der Daten, die gesammelt werden, und ob diese Daten automatisch (Onlinemodus) oder manuell (Offlinemodus) übermittelt werden.  

 Weitere Informationen finden Sie unter [Usage data levels and settings](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

##  <a name="a-namebkmkamta-support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Unterstützung für Intel Active Management Technology (AMT)  
 Mit System Center Configuration Manager wurde der native Support für AMT-basierte Computer in der Configuration Manager-Konsole entfernt.  

-   AMT-basierte Computer werden vollständig verwaltet, wenn Sie das [Intel SCS-Add-On für Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)verwenden.  

-   Über das Add-On haben Sie Zugriff auf die neuesten AMT-Verwaltungsfunktionen. Gleichzeitig werden die Beschränkungen aufgehoben, die vor der Einbindung dieser Änderungen durch Configuration Manager eingeführt wurden.  

-   Die Out-Band-Verwaltung in System Center 2012 Configuration Manager ist von dieser Änderung nicht betroffen.  

Das Entfernen integrierter AMT für System Center Configuration Manager umfasst Folgendes:  

-   Die Standortsystemrolle des Out-of-Band-Verwaltungspunkts wird nicht mehr verwendet und ist nicht mehr verfügbar.  

##  <a name="a-namebkmkouta-deprecated-functionality"></a><a name="bkmk_out"></a> Veraltete Funktionalität  
 Mit System Center Configuration Manager werden einige Funktionen, wie z.B. native auf [Unterstützung für Intel Active Management Technology (AMT)](#bkmk_AMT) basierende Computer aus der Configuration Manager-Konsole entfernt, während andere Funktionen wie der Netzwerkzugriffsschutz vollständig entfernt wurden. Darüber hinaus werden einige ältere Microsoft-Produkte wie Windows Vista, Windows Server 2008 und SQL Server 2008 nicht mehr unterstützt.  

 Eine Liste der veralteten Features finden Sie unter [Entfernte und veraltete Features für System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

 Details zu unterstützten Produkten, Betriebssystemen und Konfigurationen finden Sie unter [Unterstützte Konfigurationen für System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md).  

## <a name="client-deployment"></a>Clientbereitstellung  
 System Center Configuration Manager führt eine neue Funktion zum Testen neuer Versionen des Configuration Manager-Clients ein, bevor der Rest des Standorts einem Upgrade mit der neuen Software unterzogen wird.  Diese neue Funktion bietet Ihnen die Möglichkeit zum Einrichten einer Präproduktionssammlung, in der ein neuer Client als Pilot getestet werden kann. Sobald Sie mit der neuen Clientsoftware in der Präproduktion zufrieden sind, können Sie den Client heraufstufen, um den Rest des Standorts mit der neuen Version zu aktualisieren.  

 Weitere Informationen zum Testen von Clients finden Sie unter [Testen von Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

## <a name="operating-system-deployment"></a>Betriebssystembereitstellung  

-   Im Tasksequenzerstellungs-Assistenten steht ein neuer Tasksequenztyp zum  **Durchführen eines Upgrades für ein Betriebssystem mit einem Upgradepaket**zur Verfügung, der die Schritte für das Upgrade von Computern von Windows 7, Windows 8 oder Windows 8.1 auf Windows 10 erstellt.  Weitere Informationen finden Sie unter [Upgrade Windows to the latest version with System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Der Windows PE-Peercache ist jetzt verfügbar, wenn Sie Betriebssysteme bereitstellen. Computer, auf denen eine Tasksequenz zum Bereitstellen eines Betriebssystems ausgeführt wird, können den Windows PE-Peercache verwenden, um Inhalte von einem lokalen Peer (einer Peercachequelle) abzurufen, statt sie von einem Verteilungspunkt herunterzuladen. Auf diese Weise können Sie WAN-Datenverkehr in Zweigstellenszenarios minimieren, wenn kein lokaler Verteilungspunkt vorhanden ist. Weitere Informationen finden Sie unter [Prepare Windows PE peer cache to reduce WAN traffic in System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

-   Sie können den Zustand von Windows als Dienst in Ihrer Umgebung anzeigen, Wartungspläne zur Bildung von Bereitstellungsringen erstellen und sicherstellen, dass Windows 10 Current Branch-Computer auf dem neuesten Stand gehalten werden, wenn neue Builds veröffentlicht werden. Außerdem können Sie Warnungen anzeigen, wenn sich Windows 10-Clients dem Ende des Supports für ihren Build des Current Branch (CB) oder des Current Branch for Business (CBB) nähern. Weitere Informationen finden Sie unter [Manage Windows as a service using System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

## <a name="application-management"></a>Anwendungsverwaltung  

-   System Center Configuration Manager ermöglicht Ihnen das Bereitstellen von UWP-Apps (universelle Windows-Plattform) für Geräte mit Windows 10 und höher. Informationen finden Sie unter [Erstellen von Windows-Anwendungen mit System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Softwarecenter weist einen neuen, modernen Look auf, und Apps, die bisher nur im Anwendungskatalog angezeigt wurden (für Benutzer verfügbare Apps), werden jetzt im Software Center auf der Registerkarte „Anwendungen“ angezeigt. Dadurch sind diese Bereitstellungen für Benutzer leichter zu finden, und die Verwendung des Anwendungskatalogs bleibt ihnen erspart. Außerdem ist kein Browser mit Silverlight-Unterstützung mehr erforderlich. Informationen finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung in System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   Mit dem neuen Anwendungstyp „Windows Installer über MDM“ können Sie Windows Installer-basierte Apps auf registrierten PCs unter Windows 10 erstellen und bereitstellen. Informationen finden Sie unter [Erstellen von Windows-Anwendungen mit System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Wenn Sie eine Anwendung für eine unternehmensinterne iOS-App entwickeln, müssen Sie nur die Installationsdatei (.ipa) für die App angeben. Sie müssen nicht mehr eine entsprechende Eigenschaftenlistendatei (.plist) angeben. Informationen finden Sie unter [Erstellen von iOS-Anwendungen mit System Center Configuration Manager](../../../apps/get-started/creating-ios-applications.md).  

-   Um in Configuration Manager 2012 einen Link zu einer App im Windows Store anzugeben, können Sie entweder den Link direkt angeben oder zu einem Remotecomputer navigieren, auf dem die App installiert ist. In System Center Configuration Manager können Sie weiterhin den Link direkt eingeben. Doch anstatt zu einem Referenzcomputer zu navigieren, können Sie nun in der Configuration Manager-Konsole den Store direkt nach der App durchsuchen.  

## <a name="software-updates"></a>Softwareupdates  

-   System Center Configuration Manager bietet jetzt die Möglichkeit der Unterscheidung eines Computers mit Windows 10, der sich für die Verwaltung von Softwareupdates mit Windows Update for Business (WUfB) verbindet, von Computern, die für die Verwaltung von Softwareupdates mit WSUS verbunden sind. Das **UseWUServer**-Attribut ist neu und gibt an, ob der Computer mit WUfB verwaltet wird. Sie können diese Einstellung in einer Sammlung verwenden, um diese Computer aus der Verwaltung von Softwareupdates zu entfernen. Weitere Informationen finden Sie unter [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   Jetzt können Sie den WSUS-Bereinigungstask von der Configuration Manager-Konsole aus planen und ausführen.  
    Sie können die WSUS-Bereinigungsaufgabe jetzt manuell aus den Eigenschaften der Softwareupdatepunkt-Komponente ausführen. Wenn Sie die Ausführung der WSUS-Bereinigungsaufgabe auswählen, wird sie bei der nächsten Softwareupdatesynchronisierung ausgeführt. Die abgelaufenen Softwareupdates werden auf dem WSUS-Server auf den Status „Abgelehnt“ festgelegt, und der Windows Update-Agent auf Computern durchsucht diese Softwareupdates daraufhin nicht mehr. Weitere Informationen finden Sie unter [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md).  

## <a name="compliance-settings"></a>Kompatibilitätseinstellungen  

-   System Center Configuration Manager bietet einen verbesserten Workflow zum Erstellen von Gerätekonfigurationselementen. Wenn Sie jetzt ein Konfigurationselement erstellen und unterstützte Plattformen auswählen, sind nur die für die Plattform relevanten Einstellungen verfügbar. Informationen finden Sie unter [Erste Schritte mit Kompatibilitätseinstellungen in System Center Configuration Manager](../../../compliance/get-started/get-started-with-compliance-settings.md).  

-   Der Assistent zum Erstellen von Konfigurationselementen erleichtert die Wahl des Konfigurationselementtyps, den Sie erstellen möchten. Darüber hinaus sind neue und aktualisierte Konfigurationselemente für Folgendes verfügbar:  

    -   Mit dem Configuration Manager-Client verwaltete Windows 10-Geräte  

    -   Mit dem Configuration Manager-Client verwaltete Max OS X-Geräte  

    -   Mit dem Configuration Manager-Client verwaltete Windows Desktop- und Servercomputer  

    -   Ohne den Configuration Manager-Client verwaltete Windows 8.1- und Windows 10-Geräte  

    -   Ohne den Configuration Manager-Client verwaltete Windows Phone-Geräte  

    -   Ohne den Configuration Manager-Client verwaltete iOS- und Mac OS X-Geräte  

    -   Ohne den Configuration Manager-Client verwaltete Android- und Samsung KNOX-Geräte  

     Informationen finden Sie unter [Erstellen von Konfigurationselementen in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items.md).  

-   Unterstützung für die Verwaltung von Einstellungen auf Mac OS X-Computern, die entweder mit Microsoft Intune registriert oder mithilfe des Configuration Manager-Clients verwaltet werden. Informationen finden Sie unter [Erstellen von Konfigurationselementen für iOS- und Mac OS X-Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md).  

## <a name="protect-data-and-site-infrastructure"></a>Schützen der Daten und Standortinfrastruktur  
-   System Center Configuration Manager ermöglicht die Integration in Windows Hello for Business (ehemals Microsoft Passport for Work), eine alternative Anmeldemethode, die Active Directory oder ein Azure Active Directory-Konto verwendet, um ein Kennwort, eine Smartcard oder eine virtuelle Smartcard auf Geräten mit Windows 10 zu ersetzen. Informationen finden Sie unter [Windows Hello for Business-Einstellungen in System Center Configuration Manager](../../../protect/deploy-use/windows-hello-for-business-settings.md).

## <a name="mobile-device-management-with-microsoft-intune"></a>Verwaltung mobiler Geräte mit Microsoft Intune  
 System Center Configuration Manager bietet Verbesserungen an der Umgebung zur Verwaltung mobiler Geräte, wie z.B.:  

-   Begrenzen der Anzahl der Geräte, die ein Benutzer registrieren kann  

-   Angeben von Geschäftsbedingungen, die Benutzer im Unternehmensportal akzeptieren müssen, ehe sie die App registrieren oder nutzen können  

-   Hinzufügen einer Verwaltungsrolle für die Geräteregistrierung zur Unterstützung der Verwaltung einer großen Anzahl von Geräten  

Weitere Informationen zu Funktionen zur Verwaltung mobiler Geräte mit Configuration Manager und Intune finden Sie unter [Hybride Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune](../../../mdm/plan-design/hybrid-mobile-device-management.md).  

## <a name="on-premises-mobile-device-management"></a>Lokale Verwaltung mobiler Geräte  
 Mit System Center Configuration Manager können Sie jetzt mobile Geräte mit einer lokalen Configuration Manager-Infrastruktur verwalten. Alle Geräteverwaltungs- und sonstigen Verwaltungsdaten werden lokal verarbeitet und sind nicht Teil von Microsoft Intune oder anderer Clouddienste. Diese Art von Geräteverwaltung erfordert keine Clientsoftware, da die von Configuration Manager zum Verwalten der Geräte verwendeten Funktionen in die Gastbetriebssysteme integriert sind.  

 Weitere Informationen finden Sie unter [Verwalten mobiler Geräte mithilfe lokaler Infrastruktur in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).



<!--HONumber=Nov16_HO1-->


