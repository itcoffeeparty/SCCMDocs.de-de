---
title: Grundlagen der Sicherheit | Microsoft-Dokumentation
description: "Erfahren Sie mehr über die Sicherheitsebenen für System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: b4d12eaadaf0324515f6ae595a737f576bd5076c


---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>Grundlagen der Sicherheit für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sicherheit für System Center Configuration Manager besteht aus mehreren Ebenen. Die erste Ebene wird durch Windows-Sicherheitsfunktionen für Betriebssystem und Netzwerk bereitgestellt:  

-   Dateifreigabe zur Übertragung von Dateien zwischen Configuration Manager-Komponenten  

-   Zugriffssteuerungslisten (Access Control Lists, ACLs) zum Schutz von Dateien und Registrierungsschlüsseln  

-   IPsec zum Schutz der Kommunikation  

-   Gruppenrichtlinien zum Festlegen von Sicherheitsrichtlinien  

-   DCOM-Berechtigungen für verteilte Anwendungen, wie z. B. die Configuration Manager-Konsole  

-   Active Directory-Domänendienste zum Sichern von Sicherheitsprinzipalen  

-   Windows-Kontosicherheit einschließlich einiger Gruppen, die beim Configuration Manager-Setup erstellt werden  

Zusätzliche Sicherheitskomponenten wie Firewalls und Angriffserkennung ermöglichen einen umfassenden Schutz der gesamten Umgebung. Zertifikate, die über Industriestandard-PKI-Implementierungen ausgestellt werden, ermöglichen Authentifizierung, Signatur und Verschlüsselung.  

Zusätzlich zu der durch die Server- und Netzwerkinfrastruktur von Windows bereitgestellten Sicherheit steuert Configuration Manager den Zugriff auf die Configuration Manager-Konsole und die zugehörigen Ressourcen auf unterschiedliche Weise. Standardmäßig haben nur lokale Administratoren Zugriffsrechte für die Dateien und Registrierungsschlüssel, die zum Ausführen der Configuration Manager-Konsole auf den Computern erforderlich sind, auf denen sie installiert ist.  

Die nächste Sicherheitsebene basiert auf dem Zugriff über die Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI), speziell über den **SMS-Anbieter**. Der SMS-Anbieter ist eine Configuration Manager-Komponente, die einem Benutzer Zugriff gewährt, damit dieser Informationen aus der Standortdatenbank abfragen kann. Der Zugriff auf den Anbieter ist standardmäßig auf Mitglieder der lokalen Gruppe **SMS-Administratoren** beschränkt. Diese Gruppe enthält zunächst nur den Benutzer, der Configuration Manager installiert hat. Um anderen Konten die Berechtigung für den Zugriff auf das CIM-Repository (Common Information Model) und den SMS-Anbieter zu erteilen, fügen Sie die anderen Konten der Gruppe „SMS-Administratoren“ hinzu.  

Die letzte Sicherheitsebene basiert auf Berechtigungen für Objekte in der Standortdatenbank. Standardmäßig können mit dem lokalen Systemkonto und dem Benutzerkonto, das Sie für die Installation von Configuration Manager verwendet haben, alle Objekte in der Standortdatenbank verwaltet werden. Mithilfe von **rollenbasierter Verwaltung** können Sie weiteren Administratoren in der Configuration Manager-Konsole Berechtigungen erteilen und verwehren.  

Im weiteren Verlauf dieses Themas werden Sicherheitsaspekte in Bezug auf Configuration Manager erläutert.  

## <a name="role-based-administration"></a>Rollenbasierte Verwaltung  
 In Configuration Manager wird die rollenbasierte Verwaltung verwendet, um Objekte wie Sammlungen, Bereitstellungen und Standorte zu sichern. Über dieses Verwaltungsmodell werden Sicherheitszugriffseinstellungen für alle Standorte und Standorteinstellungen hierarchieweit zentral definiert und verwaltet. Sicherheitsrollen werden Administratoren zugewiesen. Sie dienen dazu, Berechtigungen für verschiedene Configuration Manager-Objekttypen zu gruppieren, z.B. die Berechtigungen zum Erstellen oder Ändern von Clienteinstellungen. Mithilfe von Sicherheitsbereichen werden bestimmte Instanzen von Objekten gruppiert, für deren Verwaltung ein Administrator verantwortlich ist, z. B. eine Anwendung zum Installieren von Microsoft Office. Durch die Kombination von Sicherheitsrollen, Sicherheitsbereichen und Sammlungen wird definiert, welche Objekte ein Administrator anzeigen und verwalten kann. Von Configuration Manager werden einige Standardsicherheitsrollen für häufige Verwaltungsaufgaben installiert. Sie können jedoch auch eigene Sicherheitsrollen für ihre speziellen Geschäftsanforderungen erstellen.  

 Weitere Informationen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung für System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="securing-client-endpoints"></a>Sichern von Clientendpunkten  
 Die Kommunikation zwischen Clients und Standortsystemrollen wird entweder mithilfe von selbstsignierten Zertifikaten oder mithilfe von PKI-Zertifikaten (Public Key-Infrastruktur) gesichert. Für Computerclients, die von Configuration Manager im Internet erkannt werden, sowie für Clients für mobile Geräte müssen PKI-Zertifikate verwendet werden, damit die Clientendpunkte mithilfe von HTTPS gesichert werden können. Die Standortsystemrollen, mit denen von Clients eine Verbindung hergestellt wird, können für Clientverbindungen über HTTPS oder HTTP konfiguriert werden. Die Kommunikation von Clientcomputern erfolgt immer über die sicherste verfügbare Methode. Dabei wird nur dann im Intranet auf die weniger sichere HTTP-Kommunikation zurückgegriffen, wenn Sie über Standortsystemrollen verfügen, die eine HTTP-Kommunikation zulassen.  

 Weitere Informationen finden Sie unter [Kryptographische Steuerelemente – Technische Referenz für System Center Configuration Manager](../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

## <a name="configuration-manager-accounts-and-groups"></a>Konten und Gruppen in Configuration Manager  
 In Configuration Manager wird das **lokale Systemkonto** für den Großteil der Standortvorgänge verwendet. Für einige Verwaltungstasks kann es jedoch erforderlich sein, zusätzliche Konten zu erstellen und zu warten. Beim Setup werden mehrere Standardgruppen und SQL Server-Rollen erstellt. Es kann erforderlich sein, diesen Standardgruppen und Rollen manuell Computer- oder Benutzerkonten hinzuzufügen.  

 Weitere Informationen finden Sie unter [In System Center Configuration Manager verwendete Konten](../../core/plan-design/hierarchy/accounts.md).  

## <a name="privacy"></a>Datenschutz  
 Zwar bieten Verwaltungsprodukte für Unternehmen zahlreiche Vorteile, da sie viele Clients effektiv verwalten können. Sie müssen sich jedoch der möglichen Auswirkungen dieser Software auf den Datenschutz der Benutzer in Ihrer Organisation bewusst sein. System Center Configuration Manager enthält viele Tools zum Sammeln von Daten und Überwachen von Geräten, von denen einige Bedenken hinsichtlich des Datenschutzes auslösen könnten.  

 Beim Installieren des Configuration Manager-Clients werden z.B. viele Verwaltungseinstellungen standardmäßig aktiviert. Dies führt dazu, dass von der Clientsoftware Informationen an den Configuration Manager-Standort gesendet werden. Clientinformationen werden in der Configuration Manager-Datenbank gespeichert und nicht an Microsoft gesendet. Berücksichtigen Sie beim Konfigurieren des System Center Configuration Manager Ihre Datenschutzanforderungen.  



<!--HONumber=Dec16_HO3-->


