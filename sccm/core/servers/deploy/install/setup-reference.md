---
title: Einrichten der Referenz | Microsoft-Dokumentation
description: "Überprüfen Sie diese Referenz zur Vorbereitung der Installation eines Configuration Manager-Standorts oder einer Configuration Manager-Hierarchie."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc9c8c1e6d57e886e5208d8b8968cb936c269a01
ms.openlocfilehash: beddcdb0349af4d232cd75ae742f02074abc350d


---
# <a name="reference-for-system-center-configuration-manager-setup"></a>Referenz für System Center Configuration Manager-Setup

*Gilt für: System Center Configuration Manager (Current Branch)*

Das System Center Configuration Manager-Setup stellt Links zu verschiedenen Themen bereit, die in den folgenden Abschnitten erläutert werden. Die hier aufgeführten Informationen helfen Ihnen beim Vorbereiten der Installation eines Configuration Manager-Standorts oder einer Hierarchie und bereiten Sie auf einige Entscheidungen vor, die Sie während der Installation treffen müssen.  

-   [Vorbereitung](#bkmk_start)  
-   [Bewerten der Serverbereitschaft](#bkmk_assess)  
-   [Clients für weitere Betriebssysteme](#bkmk_Addclients)  
-   [Diagnose- und Nutzungsdaten für System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)  

##  <a name="a-namebkmkstarta-before-you-begin"></a><a name="bkmk_start"></a> Vorbereitung  
Stellen Sie vor der Installation neuer Configuration Manager-Standorte sicher, dass Sie die folgenden Informationen gelesen haben, die als Grundlage für den Entwurf einer erfolgreichen Bereitstellung dienen können:  

-   [Grundlagen von System Center Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Planen Ihrer System Center Configuration Manager-Infrastruktur](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Prepare to install System Center Configuration Manager sites (Vorbereiten der Installation von System Center Configuration Manager-Standorten)](prepare-to-install-sites.md)  

##  <a name="a-namebkmkassessa-assess-server-readiness"></a><a name="bkmk_assess"></a> Bewerten der Serverbereitschaft  
Stellen Sie vor Beginn der Installation eines neuen Standorts sicher, dass der Standortserver und die Remote-Standortsystemserver, die Sie für den Standort verwenden möchten (wie z.B. der Server, der die Standortdatenbank hostet), alle Konfigurationsvoraussetzungen erfüllen. Diese Themen in der Dokumentationsbibliothek können dabei behilflich sein:  

-   [Unterstützte Konfigurationen für System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Voraussetzungsprüfung](prerequisite-checker.md)  

##  <a name="a-namebkmkaddclientsa-clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> Clients für weitere Betriebssysteme  
Sie können Clientsoftware für Configuration Manager für die folgenden Betriebssysteme aus dem Microsoft Download Center herunterladen:  

-   Mac (Apple)  
-   UNIX  
-   Linux  

Verwenden Sie die folgenden Links zum Herunterladen von Clients für Ihre verwendete Version von Configuration Manager:  

-   [System Center Configuration Manager (aktueller Branch)](http://www.microsoft.com/download/details.aspx?id=47719)  
-   [System Center 2012 R2 Configuration Manager SP1 und System Center 2012 Configuration Manager SP2](http://go.microsoft.com/fwlink/?LinkID=626550)  
-   [System Center 2012 R2 Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=316448)  
-   [System Center 2012 Configuration Manager SP1](http://www.microsoft.com/en-pk/download/details.aspx?id=36212)  

##  <a name="a-namebkmkusagea-usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> Ebenen und Einstellungen für Nutzungsdaten  
Bei der Installation des ersten System Center Configuration Manager-Standorts wird von Configuration Manager automatisch eine neue Standortsystemrolle, der **Dienstverbindungspunkt**, auf dem Standortserver installiert und konfiguriert. Der Dienstverbindungspunkt weist die folgenden Standardeinstellungen auf:  

-   **Onlinemodus** (ein Offlinemodus ist ebenfalls verfügbar)  
-   **Erweiterte** Datensammlungsebene (zwei weitere Datensammlungsebenen, „Grundlegend“ und „Vollständig“, sind ebenfalls verfügbar)  

Wenn die Rolle „Dienstverbindungspunkt“ online ist, kann Microsoft automatisch Diagnose- und Nutzungsinformationen über das Internet sammeln. Die gesammelten Informationen geben uns folgende Möglichkeiten:  

-   Erkennen und Beheben von Problemen  
-   Verbesserung unserer Produkte und Dienste  
-   Ermitteln von Updates für Configuration Manager, die für die von Ihnen verwendete Configuration Manager-Version gelten  

### <a name="levels-of-data-collection"></a>Datensammlungsebenen  
Die drei Ebenen der Datensammlung:

-   **Grundlegend** umfasst Daten zu Setup und Upgrade, wie z.B. die Anzahl der Standorte und welche Configuration Manager-Features aktiviert sind. Es werden keine personenbezogenen Informationen übertragen.  

-   **Erweitert** umfasst die Daten der Ebeneneinstellung „Grundlegend“ und zusätzlich Daten zur Hierarchie, zur Verwendung der einzelnen Funktionen (Häufigkeit und Dauer) sowie erweiterte Diagnoseinformationen, wie z.B. den Speicherzustand des Servers bei einem System- oder Anwendungsabsturz. Es werden keine personenbezogenen Daten übertragen.  

-   **Vollständig** umfasst die Daten der Ebeneneinstellungen „Grundlegend“ und „Erweitert“ und sendet zusätzlich erweiterte Diagnoseinformationen wie z.B. Systemdateien und Momentaufnahmen des Arbeitsspeichers. Diese Option kann personenbezogene Informationen enthalten, die jedoch nicht dazu verwendet werden, Sie zu identifizieren, Kontakt mit Ihnen aufzunehmen oder Ihnen Werbung zukommen zu lassen.  

Weitere Informationen, z.B. bezüglich der Offenlegung der auf den einzelnen Ebenen erfassten Details, finden Sie unter [Diagnose- und Nutzungsdaten für System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

[Datenschutzbestimmungen für System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626527)



<!--HONumber=Feb17_HO2-->


