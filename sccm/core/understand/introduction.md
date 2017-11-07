---
title: "Einführung"
titleSuffix: Configuration Manager
description: "Erhalten Sie grundlegende Informationen als Einführung in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
caps.latest.revision: "16"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 012d81b6a27d55c4a286bab6edaa7bad3f93cf46
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/12/2017
---
# <a name="introduction-to-system-center-configuration-manager"></a>Einführung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Als Produkt der Microsoft System Center-Suite von Verwaltungslösungen kann System Center Configuration Manager Sie sowohl bei der lokalen als auch bei der cloudbasierten Verwaltung von Geräten und Benutzern unterstützen.  

**Configuration Manager ermöglicht Ihnen Folgendes:**   
-   Steigern der IT-Produktivität und -Effizienz durch weniger manuelle Aufgaben und Fokussierung auf wertschöpfende Projekte  
-   Maximieren des Nutzens von Hardware- und Softwareinvestitionen  
-   Steigern der Benutzerproduktivität durch die richtige Software zum richtigen Zeitpunkt  

**Configuration Manager unterstützt Sie wie folgt bei der Bereitstellung effizienterer IT-Dienste:**  

-   Sichere und skalierbare Softwarebereitstellung  
-   Verwaltung von Konformitätseinstellungen  
-   Umfassende Inventarverwaltung von Servern, Desktops, Laptops und mobilen Geräten.  

**Configuration Manager erweitert vorhandene Technologien und Lösungen von Microsoft und arbeitet reibungslos mit diesen zusammen.**  

Configuration Manager arbeitet z.B. mit folgenden Komponenten zusammen:  

-   Microsoft Intune zur Verwaltung zahlreicher Plattformen für mobile Geräte  
-   Windows Server Update Services (WSUS) zur Verwaltung von Softwareupdates  
-   Zertifikatdiensten  
-   Exchange Server und Exchange Online  
-   Windows-Gruppenrichtlinie.
-   DNS   
-   Windows Automated Deployment Kit (Windows ADK) und Migrationstool für den Benutzerstatus (USMT)  
-   Windows-Bereitstellungsdiensten (WDS)  
-   Remotedesktop und Remoteunterstützung  

Configuration Manager verwendet auch:  

-   Active Directory-Domänendienste, um Sicherheit, Dienstidentifizierung und Konfiguration zu gewährleisten sowie zu verwaltende Benutzer und Geräte zu ermitteln.  
-   Microsoft SQL Server als verteilte Änderungsmanagementdatenbank. Durch die Integration in SQL Server Reporting Services (SSRS) werden Berichte zur Überwachung und Nachverfolgung von Verwaltungsaktivitäten erstellt.  
-   Standortsystemrollen, die Verwaltungsfunktionen erweitern und die Webdienste von Internetinformationsdiensten (Information Services, IIS) verwenden.
-   Background Intelligent Transfer Service (BITS) und BranchCache zur einfachen Verwaltung der verfügbaren Netzwerkbandbreite.  

Damit Sie Configuration Manager in einer Produktionsumgebung erfolgreich verwenden können, müssen Sie einen detaillierten Plan aufstellen und die Verwaltungsfunktionen von Configuration Manager sorgfältig testen. Configuration Manager ist eine leistungsfähige Verwaltungsanwendung, die sich potenziell auf jeden Computer in Ihrer Organisation auswirken kann. Durch eine Bereitstellung und Verwaltung von Configuration Manager bei sorgfältiger Planung und Berücksichtigung Ihrer Unternehmensanforderungen können Sie mithilfe von Configuration Manager Ihren Verwaltungsaufwand und die Gesamtbetriebskosten beträchtlich senken.  

Anhand der folgenden Themen und zusätzlichen Abschnitte in diesem Thema erfahren Sie mehr über Configuration Manager:  


**Verwandte Themen in dieser Dokumentationsbibliothek:**  

-   [Features und Funktionen von System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md)  
-   [Wählen einer Geräteverwaltungslösung für System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  
-   [Neuerungen in System Center Configuration Manager seit System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)
-   [Grundlagen von System Center Configuration Manager](../../core/understand/fundamentals.md)  
-   [Auswerten von System Center Configuration Manager durch Einrichtung Ihrer eigenen Laborumgebung](/sccm/core/get-started/set-up-your-lab)
-   [Suchen nach Hilfe für die Verwendung von System Center Configuration Manager](../../core/understand/find-help.md)  
-   [Entfernte und veraltete Features für System Center Configuration Manager](../../core/plan-design/changes/removed-and-deprecated-features.md)  

##  <a name="BKMK_Console"></a> Die Configuration Manager-Konsole  
 Nach der Installation von Configuration Manager, verwenden Sie die Configuration Manager-Konsole, um Standorte und Clients zu konfigurieren und Verwaltungstasks auszuführen und zu überwachen. Diese Konsole ist die zentrale Verwaltungsschnittstelle, über die Sie mehrere Standorte verwalten können.  

 Über die Konsole können Sie sekundäre Konsolen ausführen, die bestimmte Tasks zur Clientverwaltung zu unterstützen wie:  

-   **Ressourcen-Explorer**: Anzeige von Informationen zu Hardware- und Softwareinventur  
-   **Remotesteuerung**: Herstellen einer Remoteverbindung mit einem Clientcomputer, um Problembehandlungstasks ausführen  

Sie können die Configuration Manager-Konsole auf zusätzlichen Computern installieren, mithilfe der rollenbasierten Verwaltung in Configuration Manager den Zugriff beschränken und die Elemente begrenzen, die Administratoren angezeigt werden.  

Weitere Informationen finden Sie unter [Install System Center Configuration Manager consoles](../../core/servers/deploy/install/install-consoles.md) (Installieren von System Center Configuration Manager-Konsolen).

##  <a name="BKMK_ApplicationCatalog"></a> Der Anwendungskatalog, Softwarecenter und das Unternehmensportal  
 Der **Anwendungskatalog** ist eine Website, über die Benutzer nach Software für ihre Windows-basierten PCs suchen und diese anfordern können. Sie müssen den Anwendungskatalog-Webdienstpunkt und den Anwendungskatalog-Websitepunkt installieren, um den Anwendungskatalog verwenden zu können.  

 Das **Softwarecenter** ist eine Anwendung, die bei der Installation des Configuration Manager-Clients auf Windows-basierten Computern installiert wird. Benutzer führen diese Anwendung aus, um Software anzufordern und die Software zu verwalten, die ihnen von Configuration Manager bereitgestellt wird. Mithilfe von Softwarecenter können Benutzer folgende Aktionen ausführen:  

-   Durchsuchen des Anwendungskatalogs nach Software und Installieren dieser Software  
-   Anzeigen ihres Softwareanforderungsverlaufs  
-   Konfigurieren, wann Configuration Manager Software auf ihren Geräten installieren darf  
-   Konfigurieren der Zugriffseinstellungen für die Remotesteuerung, wenn die Remotesteuerung von einem Administrator aktiviert wurde  

Das **Unternehmensportal** ist eine App oder Website, die ähnliche Funktionen erfüllt wie der Anwendungskatalog, aber für mobile Geräte ausgelegt ist, die bei Microsoft Intune registriert sind.  

Weitere Informationen finden Sie unter [Einführung in die Anwendungsverwaltung in System Center Configuration Manager](../../apps/understand/introduction-to-application-management.md).  

###  <a name="BKMK_Client"></a> Configuration Manager-Eigenschaften (auf Windows-PCs)  
 Wenn der Configuration Manager-Client auf Windows-Computern installiert ist, wird Configuration Manager in der Systemsteuerung installiert. In der Regel müssen Sie diese Anwendung nicht konfigurieren, da die Clientkonfiguration in der Configuration Manager-Konsole ausgeführt wird. Mithilfe dieser Anwendung können Administratoren und Helpdeskmitarbeiter Probleme mit einzelnen Clients beheben.  

 Weitere Informationen zur Clientbereitstellung finden Sie unter [Clientinstallationsmethoden in System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md).  

##  <a name="BKMK_ExampleScenarios"></a> Beispielszenarien für Configuration Manager  
 In den folgenden Beispielszenarios wird veranschaulicht, wie ein Unternehmen namens Trey Research seinen Benutzern durch System Center Configuration Manager folgende Vorteile verschafft:  

-   Höhere Produktivität  
-   Vereinheitlichte Konformitätsverwaltung für Geräte, um eine optimierte Administration zu ermöglichen
-   Einfachere Geräteverwaltung zur Senkung der IT-Betriebskosten  

In allen Szenarios ist Adam der Hauptadministrator für Configuration Manager.  

###  <a name="BKMK_ScenarioEmpower"></a> Beispielszenario: Steigern der Benutzerproduktivität durch Sicherstellen des Zugriffs auf Anwendungen über jedes Gerät  
 Bei Trey Research soll sichergestellt werden, dass die Mitarbeiter möglichst effizient auf die von ihnen benötigten Anwendungen zugreifen können. Adam weist diese Unternehmensanforderungen den folgenden Szenarien zu:  

|Anforderungen|Aktueller Zustand der Clientverwaltung|Zukünftiger Zustand der Clientverwaltung|  
|-----------------|-------------------------------------|------------------------------------|  
|Neue Mitarbeiter können vom ersten Tag an effizient arbeiten.|Nach dem Eintritt in das Unternehmen müssen Mitarbeiter nach der ersten Anmeldung darauf warten, dass Anwendungen installiert werden.|Nach dem Eintritt in das Unternehmen melden sich die Mitarbeiter an, und die Anwendungen sind installiert und können sofort verwendet werden.|  
|Mitarbeiter können schnell und einfach zusätzliche Software anfordern, die sie benötigen.|Wenn Mitarbeiter zusätzliche Anwendungen benötigen, reichen sie beim Helpdesk ein Ticket ein. Sie müssen dann in der Regel zwei Tage warten, bis das Ticket bearbeitet wird und die Anwendungen installiert werden.|Wenn Mitarbeiter zusätzliche Anwendungen benötigen, können sie diese auf einer Website anfordern. Die Anwendungen werden unverzüglich installiert, sofern keine Lizenzeinschränkungen vorliegen. Liegen Lizenzeinschränkungen vor, müssen die Benutzer erst eine entsprechende Genehmigung einholen, bevor sie die Anwendung installieren können.<br /><br /> Auf der Website werden den Benutzern nur die Anwendungen angezeigt, die sie installieren dürfen.|  
|Mitarbeiter dürfen ihre eigenen mobilen Geräte bei der Arbeit verwenden, sofern die Geräte den überwachten und erzwungenen Sicherheitsrichtlinien entsprechen.<br /><br /> Diese Richtlinien umfassen das Erzwingen eines sicheren Kennworts, das Sperren eines Geräts nach einem Zeitraum der Inaktivität und die Remotezurücksetzung verlorener oder gestohlener Geräte.|Mitarbeiter stellen für E-Mail-Dienste eine Verbindung ihrer mobilen Geräte mit Exchange-Server her. Aber die Berichterstattungsfunktionen, mit denen überprüft werden kann, ob die Sicherheitsrichtlinien im Rahmen der Standardrichtlinien für Exchange ActiveSync-Postfächer eingehalten werden, sind begrenzt. Die private Nutzung von mobilen Geräten kann untersagt werden, wenn der zuständige IT-Mitarbeiter die Einhaltung der Richtlinien nicht bestätigen kann.|In der IT-Organisation kann mit den erforderlichen Einstellungen gemeldet werden, ob die Sicherheit von mobilen Geräten eingehalten wird. Durch diese Bestätigung können Benutzer ihre mobilen Geräte weiterhin bei der Arbeit verwenden. Bei Verlust oder Diebstahl können Benutzer ihre mobilen Geräte remote zurücksetzen, und Helpdeskmitarbeiter können ein vom Benutzer als verloren gegangen oder gestohlen gemeldetes mobiles Gerät zurücksetzen.<br /><br /> Ermöglichen Sie die Anmeldung mobiler Geräte in einer PKI-Umgebung, um zusätzliche Sicherheit und Kontrolle zu erlangen.|  
|Mitarbeiter können produktiv sein, auch wenn sie nicht an ihrem Platz sind.|Wenn Mitarbeiter nicht an ihrem Platz sind und keine tragbaren Computer besitzen, können sie nicht über die im Unternehmen verfügbaren Kioskcomputer auf ihre Anwendungen zugreifen.|Mitarbeiter können Kioskcomputer zum Zugreifen auf ihre Anwendungen und Daten verwenden.|  
|In der Regel hat Geschäftskontinuität Vorrang vor dem Installieren erforderlicher Anwendungen und Softwareupdates.|Erforderliche Anwendungen und Softwareupdates werden tagsüber installiert, sodass die Benutzer häufig ihre Arbeit unterbrechen müssen, weil bei der Installation die Computerleistung beeinträchtigt wird oder die Computer neu gestartet werden müssen.|Benutzer können ihre Arbeitszeit festlegen, um zu verhindern, dass erforderliche Software installiert wird, während sie den Computer verwenden.|  

 Damit den Anforderungen entsprochen wird, verwendet Adam die folgenden Verwaltungsfunktionen und Konfigurationsoptionen von Configuration Manager:  

-   Anwendungsverwaltung  
-   Verwaltung mobiler Geräte  

Er implementiert diese über die Konfigurationsschritte in der folgenden Tabelle:  

|Konfigurationsschritte|Ergebnis|  
|-------------------------|-------------|  
|Adam stellt sicher, dass neue Benutzer über Benutzerkonten in Active Directory verfügen, und er erstellt in Configuration Manager eine neue abfragebasierte Sammlung für diese Benutzer. Dann definiert er für diese Benutzer die Affinität zwischen Benutzer und Gerät, indem er eine Datei erstellt, in der die Benutzerkonten den verwendeten primären Computern zugeordnet werden. Anschließend importiert er diese Datei in Configuration Manager.<br /><br /> Die von neuen Benutzern benötigten Anwendungen wurden bereits in Configuration Manager erstellt. Er stellt dann die Anwendungen, die den Zweck „Erforderlich“ aufweisen, für die Sammlung mit den neuen Benutzern bereit.|Aufgrund der Informationen zur Affinität zwischen Benutzer und Gerät werden die Anwendungen vor der Benutzeranmeldung auf den einzelnen primären Computern der Benutzer installiert.<br /><br /> Die Anwendungen können sofort nach der Anmeldung des Benutzers verwendet werden.|  
|Adam installiert und konfiguriert die Standortsystemrollen für den Anwendungskatalog, damit die Benutzer nach zu installierenden Anwendungen suchen können. Er erstellt Anwendungsbereitstellungen mit dem Zweck Verfügbar und stellt diese Anwendungen für die Sammlung mit den neuen Benutzern bereit.<br /><br /> Für Anwendungen, für die nur eine begrenzte Anzahl von Lizenzen verfügbar ist, legt Adam fest, dass eine entsprechende Genehmigung erforderlich ist.|Benutzer können nun im Anwendungskatalog nach den Anwendungen suchen, die sie installieren dürfen. Benutzer können die Anwendungen entweder sofort installieren oder eine Genehmigung anfordern und zwecks Anwendungsinstallation zum Anwendungskatalog zurückkehren, nachdem ihre Anforderung vom Helpdesk genehmigt wurde.|  
|Adam erstellt in Configuration Manager einen Exchange Server-Connector, um die mobilen Geräte zu verwalten, die mit dem lokalen Exchange Server-Computer des Unternehmens verbunden werden. Er konfiguriert diesen Connector mit Sicherheitseinstellungen, die die Anforderung zum Festlegen eines sicheren Kennworts und die Sperre des mobilen Geräts nach einer bestimmten Zeit der Inaktivität umfassen.<br /><br /> Zur zusätzlichen Verwaltung von Geräten, auf denen Windows Phone 8, Windows RT und iOS ausgeführt wird, bezieht Adam ein Microsoft Intune-Abonnement. Dann installiert er die Standortsystemrolle „Dienstverbindungspunkt“. Diese Verwaltungslösung für mobile Geräte bietet dem Unternehmen eine größere Unterstützung zur Verwaltung dieser Geräte. Dies umfasst das Zurverfügungstellen von Anwendungen für Benutzer zur Installation auf diesen Geräten sowie eine umfassende Einstellungsverwaltung. Darüber hinaus werden Verbindungen mobiler Geräte mithilfe von PKI-Zertifikaten gesichert, die von Intune automatisch erstellt und bereitgestellt werden.<br /><br /> Nachdem Adam den Dienstverbindungspunkt und das Abonnement für die Verwendung mit Configuration Manager konfiguriert hat, sendet er den Benutzern, denen die betreffenden mobilen Geräte gehören, eine E-Mail mit einem Link, auf den die Benutzer klicken können, um die Registrierung zu starten.<br /><br /> Für die Registrierung der mobilen Geräte über Microsoft Intune verwendet Adam Kompatibilitätseinstellungen, um Sicherheitseinstellungen für die mobilen Geräte zu konfigurieren. Diese Einstellungen umfassen die Anforderung, ein sicheres Kennwort festzulegen und das mobile Gerät nach einer bestimmten Zeit der Inaktivität zu sperren.|Mithilfe dieser zwei Verwaltungslösungen für mobile Geräte kann die IT-Organisation jetzt Berichtsinformationen zu den im Firmennetzwerk verwendeten mobilen Geräten und deren Einhaltung der konfigurierten Sicherheitseinstellungen bereitstellen.<br /><br /> Benutzern wird gezeigt, wie sie ein verloren gegangenes oder gestohlenes mobiles Gerät mithilfe des Anwendungskatalogs oder über das Unternehmensportal remote zurücksetzen können. Zudem erhalten Helpdeskmitarbeiter Anweisungen, wie sie mobile Geräte für Benutzer mithilfe der Configuration Manager-Konsole remote zurücksetzen.<br /><br /> Adam kann jetzt außerdem für die über Microsoft Intune angemeldeten mobilen Geräte mobile Anwendungen für Benutzer zur Installation bereitstellen und mehr Inventurdaten von diesen Geräten sammeln. Darüber hinaus ist eine bessere Verwaltungssteuerung dieser Geräte möglich, weil auf mehr Einstellungen zugegriffen werden kann.|  
|Bei Trey Research stehen mehrere Kioskcomputer zur Verfügung, die von Mitarbeitern verwendet werden, die das Unternehmen besuchen. Die Mitarbeiter möchten, dass ihre Anwendungen auf jedem Gerät, an dem sie sich anmelden, verfügbar sind. Adam möchte jedoch nicht alle Anwendungen lokal auf den einzelnen Computern installieren.<br /><br /> Deshalb erstellt Adam die erforderlichen Anwendungen mit zwei Bereitstellungstypen:<br /><br /> **Erstens:** Eine vollständige, lokale Installation der Anwendung, die jeweils nur auf dem primären Gerät des Benutzers installiert werden darf.<br /><br /> **Zweitens:** Eine virtuelle Version der Anwendung, die nicht auf dem primären Gerät des Benutzers installiert werden darf.|Wenn sich Mitarbeiter, die das Unternehmen besuchen, an einem Kioskcomputer anmelden, werden die von ihnen benötigten Anwendungen auf dem Desktop des Kioskcomputers als Symbole angezeigt. Beim Ausführen der Anwendung wird diese als virtuelle Anwendung gestreamt. Dadurch können die Mitarbeiter genauso produktiv sein, als würden sie an ihrem eigenen Schreibtisch sitzen.|  
|Adam teilt den Benutzern mit, dass sie ihre Arbeitszeit im Softwarecenter konfigurieren und Optionen auswählen können, um zu verhindern, dass Softwarebereitstellungsaktivitäten während der Arbeitszeit sowie zu Zeiten ausgeführt werden, in denen sich der Computer im Präsentationsmodus befindet.|Da Benutzer steuern können, wann von Configuration Manager Software auf ihren Computern bereitgestellt wird, bleiben sie während ihrer gesamten Arbeitszeit produktiv.|  

 Durch diese Konfigurationsschritte und -ergebnisse kann bei Trey Research die Produktivität der Mitarbeiter durch Sicherstellen des Zugriffs auf Anwendungen über jedes Gerät gesteigert werden.  

###  <a name="BKMK_ScenarioUnify"></a> Beispielszenario: Vereinheitlichen der Kompatibilitätsverwaltung für Geräte  
 Bei Trey Research soll eine einheitliche Clientverwaltungslösung eingesetzt werden, mit der sichergestellt wird, dass auf allen Computern eine automatisch aktualisierte Antivirensoftware ausgeführt wird. Das heißt:  

-   Die Windows-Firewall ist aktiviert.  
-   Wichtige Softwareupdates wurden installiert.  
-   Bestimmte Registrierungsschlüssel wurden festgelegt.  
-   Auf verwalteten mobilen Geräten können keine unsignierten Anwendungen installiert oder ausgeführt werden.  

Das Unternehmen möchte diesen Schutz auch für Laptops, deren Verbindungen vom Intranet ins Internet wechseln, auf das Internet erweitern.  

Adam weist diese Unternehmensanforderungen den folgenden Szenarien zu:  

|Anforderungen|Aktueller Zustand der Clientverwaltung|Zukünftiger Zustand der Clientverwaltung|  
|-----------------|-------------------------------------|------------------------------------|  
|Auf allen Computern wird Antischadsoftware ausgeführt, die über die aktuellsten Definitionsdateien verfügt und die Windows Firewall aktiviert.|Verschiedene Computer führen unterschiedliche Antischadsoftwarelösungen aus, die nicht immer auf dem neuesten Stand gehalten werden. Die Windows-Firewall ist zwar standardmäßig aktiviert, aber die Benutzer deaktivieren sie manchmal.<br /><br /> Die Benutzer sind aufgefordert, den Helpdesk zu kontaktieren, wenn sie Schadsoftware auf ihrem Computer entdecken.|Alle Computer führen dieselbe Antischadsoftwarelösung aus, für die automatisch die aktuellsten Definitionsupdatedateien heruntergeladen werden und von der die Windows Firewall automatisch wieder aktiviert wird, wenn sie durch Benutzer deaktiviert wurde.<br /><br /> Der Helpdesk wird automatisch per E-Mail benachrichtigt, wenn Malware erkannt wird.|  
|Für alle Computer werden kritische Softwareupdates im ersten Monat der Veröffentlichung installiert.|Obwohl auf den Computern Softwareupdates installiert sind, werden für viele Computer kritische Softwareupdates nicht automatisch, sondern erst zwei oder drei Monate nach der Veröffentlichung installiert. Dadurch sind die Computer in diesem Zeitraum nicht optimal gegen Angriffe geschützt.<br /><br /> Für Computer, auf denen die kritischen Softwareupdates nicht installiert werden, versendet der Helpdesk zunächst E-Mails mit der Aufforderung an die Benutzer, die Updates zu installieren. Für Computer mit Benutzern, die der Aufforderung weiterhin nicht nachgekommen sind, stellen Techniker eine Remoteverbindung mit diesen Computern her und installieren die fehlenden Softwareupdates manuell.|Die aktuelle Konformitätsrate im angegebenen Monat wird auf über 95 % verbessert, ohne dass E-Mails versendet werden müssen oder der Helpdesk darum bittet, die Updates manuell zu installieren.|  
|Die Sicherheitseinstellungen für bestimmte Anwendungen werden regelmäßig geprüft und ggf. korrigiert.|Für die Computer werden komplexe Startskripts ausgeführt, die für das Zurücksetzen von Registrierungswerten für bestimmte Anwendungen auf der Computergruppenmitgliedschaft basieren.<br /><br /> Da diese Skripts nur beim Start ausgeführt werden und einige Computer tagelang nicht heruntergefahren werden, kann der Helpdesk keine rechtzeitige Überprüfung hinsichtlich einer Konfigurationsverschiebung vornehmen.|Die Registrierungswerte werden überprüft und automatisch korrigiert, ohne Neustart des Computers oder Bezug zur Computergruppenmitgliedschaft.|  
|Auf mobilen Geräten können keine unsicheren Anwendungen installiert oder ausgeführt werden.|Benutzer werden gebeten, keine möglicherweise unsicheren Anwendungen aus dem Internet herunterzuladen und auszuführen. Es gibt aber keine Kontrollen, die dies überwachen bzw. erzwingen.|Auf mobilen Geräten, die mit Microsoft Intune oder Configuration Manager verwaltet werden, wird das Installieren oder Ausführen von nicht signierten Anwendungen automatisch verhindert.|  
|Laptops, die vom Intranet ins Internet wechseln, müssen gesichert werden.|Benutzer, die viel reisen, können sich oft nicht täglich über VPN verbinden. Dadurch entsprechen ihre Laptops nicht mehr den Sicherheitsanforderungen.|Damit den Sicherheitsanforderungen entsprochen werden kann, ist für Laptops lediglich eine Internetverbindung erforderlich. Benutzer müssen sich nicht über VPN anmelden oder VPN verwenden.|  

 Damit den Anforderungen entsprochen wird, verwendet Adam die folgenden Verwaltungsfunktionen und Konfigurationsoptionen von Configuration Manager:  

-   Endpoint Protection  
-   Softwareupdates  
-   Kompatibilitätseinstellungen  
-   Verwaltung mobiler Geräte  
-   Internetbasierte Clientverwaltung  

Er implementiert diese über die Konfigurationsschritte in der folgenden Tabelle:  

|Konfigurationsschritte|Ergebnis|  
|-------------------------|-------------|  
|Adam konfiguriert Endpoint Protection. Er aktiviert die Clienteinstellung, um andere Antischadsoftwarelösungen zu deinstallieren, und aktiviert Windows-Firewall. Er konfiguriert automatische Bereitstellungsregeln, sodass für die Computer regelmäßig die aktuellsten Definitionsupdates gesucht und installiert werden.|Durch die Antischadsoftwarelösung in einem Paket werden alle Computer mit minimalem Verwaltungsaufwand geschützt. Da der Helpdesk automatisch per E-Mail informiert wird, wenn Antischadsoftware erkannt wird, können Probleme schnell behoben werden. So werden Angriffe auf andere Computer verhindert.|  
|Zur Steigerung der Konformitätsrate verwendet Adam automatische Bereitstellungsregeln, definiert Wartungsfenster für Server und untersucht die Vor- und Nachteile bei der Verwendung von Wake-On-LAN für Computer im Ruhezustand.|Die Kompatibilität mit kritischen Softwareupdates wird gesteigert, und die Anforderung an Benutzer oder den Helpdesk, Softwareupdates manuell zu installieren, wird reduziert.|  
|Adam verwendet Kompatibilitätseinstellungen, um nach den angegebenen Anwendungen zu suchen. Wenn die Anwendungen gefunden werden, prüfen Konfigurationselemente die Registrierungswerte und korrigieren diese automatisch, wenn sie nicht konform sind.|Durch die Verwendung von Konfigurationselementen und Konfigurationsbaselines, die auf allen Computern bereitgestellt werden und täglich eine Konformitätsprüfung durchführen, benötigen Sie keine separaten Skripts mehr, die von Computermitgliedschaften und -neustarts abhängig sind.|  
|Adam verwendet Kompatibilitätseinstellungen für angemeldete mobile Geräte und konfiguriert den Exchange Server Connector so, dass das Installieren und Ausführen von nicht signierten Anwendungen auf mobilen Geräten nicht zulässig ist.|Da unsignierte Anwendungen verboten sind, werden mobile Geräte automatisch vor potenziell schädlichen Anwendungen geschützt.|  
|Adam stellt sicher, dass die Standortsystemserver und -computer über die PKI-Zertifikate verfügen, die in Configuration Manager für HTTPS-Verbindungen erforderlich sind. Er installiert dann zusätzliche Standortsystemrollen im Umkreisnetzwerk, von denen Clientverbindungen über das Internet zugelassen werden.|Computer, die vom Intranet ins Internet wechseln, werden automatisch weiterhin von Configuration Manager verwaltet, wenn Sie eine Internetverbindung haben. Diese Computer sind nicht davon abhängig, dass Benutzer sich am Computer anmelden oder eine Verbindung zu VPN herstellen.<br /><br /> Für diese Computer ist die Verwaltung von Antischadsoftware und Windows Firewall, Softwareupdates und Konfigurationselementen sichergestellt. Daher erhöhen sich die Kompatibilitätsstufen automatisch.|  

 Diese Konfigurationsschritte und -ergebnisse führen zur erfolgreichen Vereinheitlichung der Kompatibilitätsverwaltung für Geräte von Trey Research.  

###  <a name="BKMK_ScenarioSimplify"></a> Beispielszenario: Vereinfachen der Clientverwaltung für Geräte  
 Bei Trey Research sollen alle neuen Computer das Basiscomputerimage ihres Unternehmens automatisch installieren, das Windows 7 ausführt. Nachdem das Betriebssystemabbild auf diesen Computern installiert wurde, müssen sie hinsichtlich der von Benutzern zusätzlich installierten Software verwaltet und überwacht werden. Für Computer, auf denen streng vertrauliche Informationen gespeichert werden, sind strengere Verwaltungsrichtlinien als für andere Computer erforderlich. Helpdeskmitarbeiter dürfen beispielsweise keine Remoteverbindung zu diesen Computern herstellen, für einen Neustart muss eine BitLocker PIN eingegeben werden, und nur lokale Administratoren können Software installieren.  

 Adam weist diese Unternehmensanforderungen den folgenden Szenarien zu:  

|Anforderungen|Aktueller Zustand der Clientverwaltung|Zukünftiger Zustand der Clientverwaltung|  
|-----------------|-------------------------------------|------------------------------------|  
|Auf neuen Computern wird Windows 7 installiert.|Der Helpdesk installiert und konfiguriert Windows 7 für die Benutzer und sendet den Computer dann an den entsprechenden Ort.|Neue Computer werden direkt an den Aufstellungsort gesendet und mit dem Netzwerk verbunden. Sie installieren und konfigurieren dann automatisch Windows 7.|  
|Computer müssen verwaltet und überwacht werden. Dies umfasst das Sammeln von Hardware- und Softwareinventurdaten, um Lizenzanforderungen zu ermitteln.|Der Configuration Manager-Client wird über die automatische Clientpushinstallation bereitgestellt. Der Helpdesk untersucht Installationsfehler sowie Clients, für die Inventurdaten nicht erwartungsgemäß versendet wurden.<br /><br /> Es treten häufig Fehler auf, die durch unberücksichtigte Installationsabhängigkeiten und WMI-Beschädigung auf dem Client verursacht werden.|Daten zur Clientinstallation und -inventur, die auf den Computern gesammelt werden, sind verlässlicher und erfordern weniger Unterstützung durch den Helpdesk. In Berichten wird die Softwarenutzung für Lizenzinformationen angezeigt.|  
|Für einige Computer sind strengere Verwaltungsrichtlinien erforderlich.|Aufgrund der strengeren Verwaltungsrichtlinien werden diese Computer zurzeit nicht von Configuration Manager verwaltet.|Diese Computer werden über Configuration Manager verwaltet, um Ausnahmen ohne zusätzlichen Verwaltungsaufwand zu berücksichtigen.|  

 Damit den Anforderungen entsprochen wird, verwendet Adam die folgenden Verwaltungsfunktionen und Konfigurationsoptionen von Configuration Manager:  

-   Betriebssystembereitstellung  
-   Clientbereitstellung und Clientstatus  
-   Kompatibilitätseinstellungen  
-   Clienteinstellungen  
-   Inventurmethoden und Asset Intelligence  
-   Rollenbasierte Verwaltung  

Er implementiert diese über die Konfigurationsschritte in der folgenden Tabelle:  

|Konfigurationsschritte|Ergebnis|  
|-------------------------|-------------|  
|Adam erstellt ein Betriebssystemabbild von einem Computer, auf dem Windows 7 installiert ist und der gemäß den Unternehmensspezifikationen konfiguriert ist. Dann stellt er das Betriebssystem auf den neuen Computern bereit, mithilfe eines unbekannten Computer-Supports und PXE. Außerdem installiert er den Configuration Manager-Client als Teil der Betriebssystembereitstellung.|So sind neue Computer schneller einsatzbereit, ohne Eingreifen des Helpdesk.|  
|Adam konfiguriert eine automatische, standortweite Clientpushinstallation, um den Configuration Manager-Client auf allen gefundenen Computern zu installieren. Dies stellt sicher, dass auf allen Computern, von denen kein Image mit dem Client erstellt wurde, der Client dennoch installiert und der Computer so von Configuration Manager verwaltet wird.<br /><br /> Adam konfiguriert den Clientstatus, um alle ermittelten Clientprobleme automatisch zu beheben. Er konfiguriert außerdem Clienteinstellungen, die das Sammeln erforderlicher Inventurdaten ermöglichen, und konfiguriert Asset Intelligence.|Das Installieren des Clients zusammen mit dem Betriebssystem ist schneller und verlässlicher, als darauf zu warten, dass der Computer von Configuration Manager erkannt wird, und dann zu versuchen, die Clientquelldateien auf dem Computer zu installieren. Wenn Sie jedoch die automatische Clientpushoption aktiviert lassen, stellen Sie eine Sicherungsmethode für einen Computer bereit, auf dem das Betriebssystem bereits installiert ist, um den Client beim Verbinden des Computers mit dem Netzwerk zu installieren.<br /><br /> Clienteinstellungen stellen sicher, dass Inventurinformationen in regelmäßigen Abständen an den Standort gesendet werden. Zusätzlich zu den Clientstatustests stellt dies sicher, dass der Client mit minimaler Beteiligung des Helpdesks ausgeführt werden kann. WMI-Beschädigungen beispielsweise werden erkannt und automatisch korrigiert.<br /><br /> Die Asset Intelligence-Berichte dienen der Überwachung der Softwareverwendung und -lizenzen.|  
|Adam erstellt eine Sammlung für die Computer, für die strengere Richtlinieneinstellungen erforderlich sind. Dann nimmt er eine benutzerdefinierte Clientgeräteeinstellung für diese Sammlung vor, die die Deaktivierung der Remotesteuerung und die Aktivierung der BitLocker-PIN-Eingabe umfasst und nur lokalen Administratoren die Installation von Software gestattet.<br /><br /> Adam konfiguriert die rollenbasierte Verwaltung, sodass Helpdeskmitarbeitern diese Sammlung von Computern nicht angezeigt wird. So wird sichergestellt, dass diese Computer nicht versehentlich als Standardcomputer verwaltet werden.|Diese Computer werden jetzt von Configuration Manager verwaltet – jedoch mit spezifischen Einstellungen, die keinen neuen Standort erfordern.<br /><br /> Die Sammlung für diese Computer ist für die Helpdeskmitarbeiter nicht sichtbar. So wird verhindert, dass diesen Computern versehentlich Bereitstellungen und Skripts für Standardcomputer geschickt werden.|  

 Diese Konfigurationsschritte und -ergebnisse führen dazu, dass Trey Research die Clientverwaltung für Geräte erfolgreich vereinfacht.  

##  <a name="BKMK_NextSteps"></a> Nächste Schritte  
 Machen Sie sich vor der Installation von Configuration Manager mit einigen grundlegenden Konzepten und Begriffen vertraut, die bei Configuration Manager verwendet werden.  

-   Wenn Sie mit System Center 2012 Configuration Manager vertraut sind, können Sie unter [Änderungen in System Center Configuration Manager im Vergleich zu System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) die neuen Funktionen kennenlernen.  
-   Eine allgemeine technische Übersicht von System Center Configuration Manager finden Sie unter [Grundlagen von System Center Configuration Manager](../../core/understand/fundamentals.md).  

Wenn Sie mit den grundlegenden Konzepten vertraut sind, finden Sie in der Dokumentation zu System Center Configuration Manager hilfreiche Informationen zur erfolgreichen Bereitstellung und Verwendung von Configuration Manager.  
