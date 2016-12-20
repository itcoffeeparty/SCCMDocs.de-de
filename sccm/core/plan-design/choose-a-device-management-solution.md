---
title: "Wählen einer Geräteverwaltungslösung für System Center Configuration Manager | Microsoft Docs"
description: "Erfahren Sie mehr über Lösungen, die System Center Configuration Manager zum Verwalten von PCs, Servern und Geräten anbietet."
ms.custom: na
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
caps.latest.revision: 14
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 099e0001c01713224988e5b49d02cb358e3015d6
ms.openlocfilehash: f4f0a8e8b1b5aae2586cc885734f405f7e7f9ff5


---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>Wählen einer Geräteverwaltungslösung für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager (auch als ConfgMgr oder SCCM bekannt) bietet verschiedene Lösungen für die Verwaltung von PCs, Servern und Geräten. Sie können die Lösung passend zur verwalteten Geräteplattform und den benötigten Verwaltungsfunktionen auswählen.  


##  <a name="overview-of-device-management-solutions"></a>Übersicht über Geräteverwaltungslösungen  
 Dieser Übersicht folgen zwei Tabellen, in denen die Verwaltungslösungen verglichen werden: einmal [basierend auf unterstützten Mobilgeräteplattformen](#compare-device-management-solutions-based-on-supported-mobile-device-platforms) und einmal [basierend auf Verwaltungsfunktionen](#compare-mobile-device-management-solutions-based-on-management-functionality).
  

-   **Verwalten von Geräten mit dem Configuration Manager-Client**  

     Diese Option, bei der die Configuration Manager-Clientanwendung auf den Geräten installiert werden muss, bietet die meisten Features und Funktionen für die Verwaltung von PCs, Servern und anderen Geräten in Ihrer Umgebung.   

     Weitere Informationen finden Sie unter [Clientinstallationsmethoden in System Center Configuration Manager](/sccm/core/client/deploy/plan/client-installation-methods).  

-   **Verwalten mobiler Geräte mithilfe lokaler Configuration Manager-Infrastruktur**  

     Diese Option verwendet die Geräteverwaltungsfunktionen, die in die Betriebssysteme einiger Geräteplattformen integriert sind. Die lokale Lösung zur Verwaltung mobiler Geräte bietet zwar nicht den gleichen Funktionsumfang wie die clientbasierte Verwaltung, ist jedoch eine schlankere Verwaltungslösung, die Geräte mithilfe lokaler Configuration Manager-Ressourcen erreicht und verwaltet. Die lokale Lösung zur Verwaltung mobiler Geräte wird derzeit nur für Windows 10-PCs und Windows 10 Mobile-Geräte unterstützt.  

     Weitere Informationen zu dieser Lösung finden Sie unter [On-premises Mobile Device Management (MDM) in System Center Configuration Manager (Lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) in System Center Configuration Manager)](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

-   **Verwalten von mobilen Geräten mit Microsoft Intune (hybrid)**  

     Diese Option verwendet zum Registrieren und Verwalten von Geräten Microsoft Intune anstelle von lokalen Configuration Manager-Ressourcen. Obwohl Intune die Geräte verwaltet, können Sie über die Configuration Manager-Konsole auf die Verwaltungsaufgaben zugreifen. Die Option unterstützt alle wichtigen Betriebssysteme für mobile Geräte, einschließlich Windows 10 Mobile, Windows Phone, iOS, Mac OS X und Android. Darüber hinaus unterstützt sie die Verwaltung von Windows 8.1- und Windows 10-Computern in Ihrer Organisation.  

     Weitere Informationen zu dieser Lösung finden Sie unter [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune (Hybride Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune)](../../mdm/understand/hybrid-mobile-device-management.md).  

-   **Verwalten mobiler Geräte mit Exchange**  

     Diese Option ermöglicht Configuration Manager über Exchange Server-Connector die Verbindung mit mehreren Exchange-Servern, und zentralisiert die Verwaltung von Geräten, die sich mit Exchange ActiveSync verbinden können. Sie können in der Configuration Manager-Konsole Exchange-Verwaltungsfunktionen für mobile Geräte konfigurieren, wie z.B. das Remotezurücksetzen von Geräten und Einstellungen zum Steuern mehrerer Exchange-Server.  

     Weitere Informationen zu dieser Lösung finden Sie unter [Manage mobile devices with System Center Configuration Manager and Exchange (Verwalten mobiler Geräte mit System Center Configuration Manager und Exchange)](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

 Sie können diese Geräteverwaltungslösungen eigenständig oder in Kombination miteinander verwenden. Beispielsweise können Sie die clientbasierte Verwaltungslösung für die Verwaltung von Computern und Servern in der Organisation und Intune für die Verwaltung mobiler Geräte verwenden. Durch diese Kombination können Sie alle Anforderungen der Geräteverwaltung über die Configuration Manager-Konsole abdecken.  

## <a name="compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a>Vergleichen von Geräteverwaltungslösungen basierend auf unterstützten Plattformen für mobile Geräte  

|Plattform|Mit dem Configuration Manager-Client|Configuration Manager mit Microsoft Intune (hybrid)|Lokale Verwaltung mobiler Geräte|Configuration Manager mit Exchange|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||Ja||Ja|  
|iOS||Ja||Ja|  
|Mac OS X|Ja|||Ja|  
|UNIX/Linux|Ja|||Ja|  
|Windows 10|Ja|Ja|Ja|Ja|  
|Windows 10 Mobile||Ja|Ja|Ja|  
|Windows (frühere Versionen)|Ja|Ja||Ja|  
|Windows CE|Ja (mit Legacyclient für mobile Geräte)|||Ja|  
|Windows Embedded|Ja||||  
|Windows Phone||Ja||Ja|  
|Windows Server|Ja|||Ja|  

 Eine vollständige Liste unterstützter Plattformen finden Sie unter [Supported operating systems for clients and devices for System Center Configuration Manager (Unterstützte Betriebssysteme für Clients und Geräte für System Center Configuration Manager)](configs\supported-operating-systems-for-clients-and-devices.md).

##  <a name="a-namebkmkcomp2a-compare-mobile-device-management-solutions-based-on-management-functionality"></a><a name="bkmk_comp2"></a> Vergleichen von Lösungen zur Verwaltung mobiler Geräte basierend auf der Verwaltungsfunktionalität  

|Verwaltungsfunktion|Mit dem Configuration Manager-Client|Configuration Manager mit Microsoft Intune (hybrid)|Lokale Verwaltung mobiler Geräte|Configuration Manager mit Exchange|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|PKI-Sicherheit (Public Key-Infrastruktur) zwischen dem mobilen Gerät und Configuration Manager mithilfe gegenseitiger Authentifizierung und SSL zur Verschlüsselung von Datenübertragungen|Ja|Ja|Ja||  
|Clientinstallation|Ja||||  
|Support über das Internet|Ja||||  
|-Ermittlung|Ja|||Ja|  
|Hardwareinventur|Ja|Ja|Ja|Ja|  
|Softwareinventur|Ja|||Ja|  
|Einstellung|Ja|Ja|Ja|Ja|  
|Softwarebereitstellung|Ja|Ja|Ja||  
|Überwachen mit dem Fallbackstatuspunkt|Ja||||  
|Verbindungen mit Verwaltungspunkten|Ja||Ja||  
|Verbindungen mit Verteilungspunkten|Ja|Ja|Ja||  
|Blockieren von Configuration Manager aus|Ja|Ja|Ja||  
|Unter Quarantäne Stellen und Blockieren von Exchange Server (und Configuration Manager) aus||||Ja|  
|Remotezurücksetzung|Ja|Ja|Ja|Ja|  



<!--HONumber=Dec16_HO3-->


