---
title: "Auswählen von Intune standalone oder der hybriden Verwaltung mobiler Geräte | System Center Configuration Manager"
description: "Wählen Sie aus, ob Sie die hybride Verwaltung mobiler Geräte mit Intune und Configuration Manager bereitstellen oder Intune standalone ausführen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2e6ec1b2b822298d4fa6a17e2d7439167b83080a

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Wählen zwischen Microsoft Intune standalone und der hybriden Verwaltung mobiler Geräte mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Eine der am häufigsten gestellten Fragen bezüglich der Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit Microsoft Intune ist folgende: „Sollte ich die hybride Verwaltung mobiler Geräte mit Intune und Configuration Manager bereitstellen oder Intune standalone in der Konfiguration nur für die Cloud ausführen?“ Dies ist eine wichtige Entscheidung, die nach der Implementierung nicht einfach geändert wird.  

 Eine Bereitstellung von Intune standalone umfasst keine lokale Infrastruktur und wird über eine Webkonsole verwaltet. Sie ist flexibel, einfach und bei Organisationen beliebt, bei denen die Cloud an erster Stelle steht.  

 Eine Bereitstellung der hybriden Verwaltung mobiler Geräte umfasst Intune und Configuration Manager und wird über Tools verwaltet, mit denen erfahrene Administratoren von Configuration Manager vertraut sind. Sie bietet die zentralisierte Verwaltung von MDM- und herkömmlichen Clients sowie die Skalierung in großen Umgebungen.  

##  <a name="what-does-intune-standalone-mean"></a>Was bedeutet Intune standalone?  
 Intune ist im Grunde ein Clouddienst. Intune-Rechenzentren werden in Nordamerika, Europa und Asien gehostet und stellen mobile Geräte mit Sicherheitsrichtlinien, E-Mail- und WLAN-Profilen, Anwendungen, Inventur usw. bereit.  

 Eine Implementierung von Intune standalone erfordert keine lokale Infrastruktur. Die gesamte Konfiguration, Verwaltung, Bereitstellung und Berichterstellung erfolgt über eine webbasierte Konsole, auf die von der ganzen Welt aus zugegriffen werden kann.  

 Für die Arbeit mit lokalen Anwendungen wie z.B. Microsoft Exchange und dem Registrierungsdienst für Netzwerkgeräte stehen lokale Connectors für die Bereitstellung von Konnektivität zum Intune-Dienst zur Verfügung.  

 Intune ist ein Clouddienst und kann daher innerhalb eines kleinen Zeitrahmens erstellt und bereitgestellt werden.  

##  <a name="what-does-hybrid-mdm-mean"></a>Was bedeutet die hybride Verwaltung mobiler Geräte?  
 Für Organisationen, die Ihre Configuration Manager-Investition maximieren möchten, Kunden, die eine differenzierte Kontrolle benötigen, oder Kunden, die die Skalierungseinschränkungen von Intune überschreiten, steht für die Verwaltung mobiler Geräte eine Hybridimplementation zur Verfügung.  

 Hybridbereitstellungen erfordern Microsoft System Center 2012 Configuration Manager SP1 oder höher.  

 Der Intune-Dienst ist mithilfe der Dienstverbindungspunkt-Standortsystemrolle (früher als Microsoft Intune Connector bezeichnet) mit Configuration Manager verbunden, die entweder bei der zentralen Verwaltung oder dem primären Standort einer Configuration Manager-Hierarchie installiert wird. Ein Intune-Mandant kann mit nur einer Configuration Manager-Hierarchie und eine Configuration Manager-Hierarchie kann mit nur einem Intune-Mandanten verbunden werden.  

 In einer Konfiguration der hybriden Verwaltung mobiler Geräte wird ein Teil des Verarbeitungs- und Speicheraufwands von der lokalen Configuration Manager-Infrastruktur ausgeführt. Durch diesen Gewinn an Effizienz kann die hybride Verwaltung mobiler Geräte weiter skaliert werden als Intune standalone.  

 Eine Hybridbereitstellung ermöglicht die Verwendung von Tools, mit denen Configuration Manager-Administratoren bereits vertraut sind. Erweiterte Funktionen wie z.B. die rollenbasierte Zugriffssteuerung (RBAC), SQL Server Reporting Services (SSRS) und die komplexe Geräte- und Benutzergruppierung mithilfe von Sammlungsmitgliedschaftsabfragen stehen zur Verfügung, sobald die hybride Verwaltung mobiler Geräte implementiert wurde.  

##  <a name="planning-choices-and-intune-deployment-timelines"></a>Planen von Auswahlmöglichkeiten und Zeitplänen für die Intune-Bereitstellung  
 Die Intune-Innovation und -Weiterentwicklung erfolgt schnell mit monatlichen Updates, die neue oder verbesserte Funktionen, eine erweiterte Skalierung, neue Benutzeroberflächenelemente über das Azure-Portal, dynamische Gruppen über Azure Active Directory usw. bereitstellen. Daher sollte bei allen Entwurfsentscheidungen die zukünftige Richtung des Produkts berücksichtigt werden.  

 Viele der eigenen Funktionen, die eine hybride Konfiguration aktuell bereitstellt, werden funktionell in Intune standalone repliziert, da der Dienst kurz-, mittel- und langfristig entwickelt wird.  

 Wenn Sie eine Entscheidung zwischen eigenständig und hybrid treffen, sollten Sie die Bereitstellungszeitpläne berücksichtigen. Kunden durchlaufen üblicherweise mehrere Bereitstellungsiterationen, einschließlich Entwurf, Build, Benutzerakzeptanztests und Pilotphasen, und benötigen dafür oft mehrere Monate, bevor Sie für die Bereitstellung in die Produktion bereit sind. Berücksichtigen Sie aus diesem Grund bei der Auswahl eines Intune-Hierarchieentwurfs die Zeit, zu der die tatsächliche Bereitstellung erfolgt und die kurz-, mittel- und langfristige Richtung des Diensts.  

 Da der Intune-Dienst ständig weiterentwickelt wird, ist unser Ziel die Vereinfachung Ihrer Konfigurationsauswahl. In Zukunft sollte der einzige Grund für die Auswahl einer Umgebung der hybriden Verwaltung mobiler Geräte sein, dass ein Kunde eine einzelne Verwaltungskonsole für sowohl herkömmliche Clients als auch mobile Geräte benötigt.  Wir arbeiten hart daran, die Skalierbarkeit zu verbessern, die rollenbasierte Zugriffssteuerung über das Azure-Portal und dynamische Gruppen durch bessere Azure Active Directory-Integration hinzuzufügen – alles ausgerichtet auf kurz- und mittelfristige Dienstupdates.  

 Abschließend arbeiten wir zudem daran, sicherzustellen, dass Sie einfach und reibungslos zwischen der hybriden und der eigenständigen Konfiguration wechseln können, unabhängig davon, welche Konfiguration Sie heute auswählen. Im Moment erfordert das Wechseln zwischen MDM-Autoritäten einen manuellen Eingriff von Microsoft Support sowie eine erhebliche Anstrengung durch den Mandanten. Um dies zu vereinfachen, ist unser Ziel, die Koexistenz der hybriden Verwaltung mobiler Geräte und Intune standalone zuzulassen, wodurch Sie Benutzer zwischen den beiden Verwaltungstypen hin und her schieben können, ohne dass Sie sich für eine der beiden Konfigurationen entscheiden müssen.  Durch diese Änderung entfallen zudem die heutigen Herausforderungen, dass der Support kontaktiert werden muss, sowie das Aufheben der Registrierung von Geräten und das erneute Registrieren dieser.  

##  <a name="pros-and-cons-of-intune-standalone"></a>Vor- und Nachteile von Intune standalone  

|Vorteile|Nachteile|  
|----------|----------|  
|Schnelle Erstellung und Bereitstellung<br /><br /> Keine lokale Infrastruktur<br /><br /> Häufigere Updates und Funktionsreleases<br /><br /> Niedrige Lernkurve<br /><br /> Extern verfügbare Verwaltungskonsole|Eingeschränkte Berichterstellungsfunktionen<br /><br /> Eingeschränkte Sicherheitsrolleneinschränkung<br /><br /> Keine externen Tools (wie z.B. PowerShell usw.)<br /><br /> Eingeschränkte App-Inventur<br /><br /> Grundlegende Benutzer- und Gerätegruppierungsfunktionen<br /><br /> Silverlight erforderlich|  

##  <a name="pros-and-cons-of-hybrid-mdm"></a>Vor- und Nachteile der hybriden Verwaltung mobiler Geräte  

|Vorteile|Nachteile|  
|----------|----------|  
|Skalierungsfunktion<br /><br /> Erweiterte Tools (wie z.B. Configuration Manager-Konsole, PowerShell, Protokollierung usw.)<br /><br /> Rollenbasierte Zugriffssteuerung (role-based access control, RBAC)<br /><br /> Erweiterte Berichterstellung<br /><br /> Zentralisierte Verwaltung von MDM + herkömmlichen Clients<br /><br /> Erweiterte App-Inventur<br /><br /> Fortgeschrittene Benutzer- und Gerätegruppierung<br /><br /> Unterstützt mehrere Connectors für lokales Exchange und Exchange Online<br /><br /> Unterstützt mehrere NDES/CRP-Rollen<br /><br /> Funktion zum Kennzeichnen von Geräten als „unternehmenseigen“<br /><br /> Bessere Funktionen für die Problembehandlung<br /><br /> Configuration Manager-Nutzer-CALs, die im Abonnement enthalten sind|Lokale Komplexität (Konfiguration und Verwaltung)<br /><br /> Steile Lernkurve<br /><br /> Wartung für Updates und Funktionsreleases erforderlich<br /><br /> Zusätzliche Lizenzanforderungen (wie z.B. Windows, SQL Server usw.)|  

##  <a name="planning-decisions"></a>Planungsentscheidungen  
 ![hybride&#45;Entscheidungen](../../mdm/understand/media/hybrid-decisions.png)  

|Schritt|Entscheidung|
|-|-|  
|<img src="media/hybrid-1.png" style="min-width:32px">|**Wie viele Geräte planen Sie zu verwalten?**<br /><br /> Intune standalone unterstützt bis zu 50.000 Geräte. Die hybride Verwaltung mobiler Geräte unterstützt bis zu 300.000 Geräte.<br /><br /> Für jede Bereitstellung von signifikanter Größe – ob eigenständige oder hybride Verwaltung mobiler Geräte – empfehlen wir, dass Sie Ihr Microsoft-Konto-Team kontaktieren. Ihr Microsoft-Konto-Team kann für Sie den Kontakt zu Intune-Experten herstellen, die die Skalierung und die Einschränkungen weiter ausführen können.|  
|![hybrid&#45;2](../../mdm/understand/media/hybrid-2.png)|**Ist eine differenzierte Zugriffssteuerung erforderlich? (RBAC)**<br /><br /> System Center 2012 Configuration Manager wurde die rollenbasierte Zugriffssteuerung (RBAC) hinzugefügt. RBAC ermöglicht Configuration Manager-Administratoren das Entwerfen und Bereitstellen von komplexen Berechtigungssätzen, um den Administratorzugriff auf Configuration Manager-Objekte und -Funktionen einzuschränken.<br /><br /> Intune standalone bietet nur zwei Administratorrollen: Vollzugriff und Schreibgeschützter Zugriff.<br /><br /> Wenn Ihre Organisation bestimmte Administratoren für bestimmte Benutzer, Geräte, Funktionen oder Objekte beschränken muss, wird Configuration Manager mit RBAC benötigt.<br /><br /> Wenn Ihre Organisation über ein kleines Verwaltungsteam verfügt und die Komplexität der differenzierten Zugriffssteuerung nicht erforderlich ist, ist Intune mit integrierten Sicherheitsrollen am besten geeignet.|  
|![hybrid&#45;3](../../mdm/understand/media/hybrid-3.png)|**Werden erweiterte Berichterstellungsfunktionen benötigt?**<br /><br /> Die hybride Verwaltung mobiler Geräte mit Configuration Manager enthält erweiterte Berichterstellungsfunktionen, die SQL Server Reporting Services (SSRS) verwenden. Configuration Manager verfügt über 34 integrierte MDM-Berichte und mehr als 400 Configuration Manager-Standardberichte. SSRS ermöglicht Administratoren und Wirtschaftsanalytikern das Schreiben ihrer eigenen benutzerdefinierten Berichte. Darüber hinaus kann die Configuration Manager-Datenbank von externen Tools, wie z.B. Orchestrierungstools, abgefragt werden, um bestimmte Funktionen, wie z.B. benutzerdefinierte Warnungen, bereitzustellen. Da die Berichte von Configuration Manager ausgeführt werden, können alle Berichte auch Daten enthalten, die nicht von MDM stammen, wie z.B. herkömmliche PC-Inventur parallel zur Inventur mobiler Geräte.<br /><br /> Intune standalone stellt 9 Berichte bereit. Diese Berichte können nicht angepasst werden und bieten begrenzte Eingabevariablen an. Berichte können ausgedruckt oder in CSV oder HTML exportiert werden.<br /><br /> Wenn Ihre Organisation erweiterte Berichterstellungsfunktionen erfordert, und über die Bandbreite und das Wissen zum Verwalten von SSRS verfügt, ist die hybride Verwaltung mobiler Geräte am besten geeignet.<br /><br /> Wenn Ihre Organisation ein einfach zu verwendendes Berichterstellungsmodul und vordefinierte Berichte verwenden möchte, sollte die Berichterstellungsfunktion von Intune standalone ausreichen.|  
|![hybrid&#45;4](../../mdm/understand/media/hybrid-4.png)|**Verwalten Sie Windows 10-Geräte ohne Internetzugriff?**<br /><br /> In Configuration Manager (Current Branch) können Windows 10-Geräte über den MDM-Kanal verwaltet werden, wobei nur eine lokale Infrastruktur verwendet wird.<br /><br /> Die Funktion zur lokalen Verwaltung mobiler Geräte wurde entworfen, um die MDM-Verwaltung für Clients zu ermöglichen, die über keinen Internetzugriff verfügen, und ist primär auf Geräte für die einmalige Verwendung (wie z.B. Kiosk-Geräte) und IoT-Geräte ausgerichtet.<br /><br /> Aufgrund des Nur-Cloud-Ansatzes von Intune standalone müssen alle verwalteten Geräte über einen Internetzugriff verfügen. Wenn Ihre Organisation Windows 10-Geräte über die lokale Verwaltung mobiler Geräte verwalten möchte, ist eine hybride MDM-Konfiguration erforderlich. Beachten Sie, dass die lokale Verwaltung mobiler Geräte die gleichzeitige Verwaltung von sowohl mobilen Internet- als auch Intranet-Geräten nicht unterstützt.|  
|![hybrid&#45;5](../../mdm/understand/media/hybrid-5.png)|**Benötigen Sie eine vollständige App-Inventur?**<br /><br /> Intune standalone sammelt standardmäßig nur die App-Inventur für Apps, die von Intune verwaltet und bereitgestellt werden. Dies bedeutet, dass Inventurberichte keine Informationen zu quergeladenen Apps enthalten, die von Benutzern außerhalb des Intune-Unternehmensportals installiert wurden.<br /><br /> Die hybride Verwaltung mobiler Geräte mit Configuration Manager ermöglicht Administratoren das Festlegen bestimmter Geräte als „unternehmenseigen“. Wenn ein Gerät als unternehmenseigen festgelegt ist, wird erweiterte App-Inventur gesammelt und Zugriff auf die vollständige App-Liste eines Geräts gewährt.<br /><br /> Wenn Ihre Organisation Informationen zu persönlich installierten Apps von verwalteten Geräten benötigt, ist die hybride Verwaltung mobiler Geräte erforderlich. Berücksichtigen Sie vor einer Entscheidung basierend auf dieser Auswahl die Auswirkung auf die Privatsphäre Ihres Endbenutzers.|  
|![hybrid&#45;6](../../mdm/understand/media/hybrid-6.png)|**Möchten Sie PCs auf herkömmliche „dicker Client“-Weise verwalten?**<br /><br /> Ein Vorteil der hybriden Verwaltung mobiler Geräte gegenüber einer eigenständigen Konfiguration ist die zentralisierte Verwaltung. Dies bedeutet, dass eine Organisation all ihre Desktopcomputer, Server und mobilen Geräte von einem Verwaltungstool aus, der Configuration Manager-Konsole, verwalten kann. Auch beim Configuration Manager-Client stehen erweiterte Verwaltungsfunktionen wie Hardware- und Softwareinventur, Softwareupdateverwaltung, Softwarebereitstellung und Betriebssystembereitstellung für nicht mobile Geräte zur Verfügung.<br /><br /> Wenn Ihre Organisation herkömmliche Windows-, Linux/UNIX- und MAC-Clients verwalten möchte, stellt Configuration Manager die primäre Verwaltungsplattform dar.<br /><br /> Intune standalone bietet außerdem die herkömmliche PC-Verwaltung (Windows 7, 8.1 und 10) mithilfe des Intune-PC-Verwaltungsclients. Es bietet die grundlegende PC-Verwaltung, einschließlich Hardwareinventur, Windows-Updates, Endpoint Protection und einfacher Softwarebereitstellung. Der Client arbeitet nicht mit Configuration Manager und kann daher sowohl bei der Intune standalone-Bereitstellung als auch der Bereitstellung der hybriden Verwaltung mobiler Geräte verwendet werden.|  
|![hybrid&#45;7](../../mdm/understand/media/hybrid-7.png)|**Möchten Sie die lokale Infrastruktur verwalten?**<br /><br /> Jede lokale Infrastruktur ist mit einem gewissen Maß an Verwaltungsaufwand und Komplexität verbunden. Configuration Manager ist ein Produkt, das signifikantes Wissen, Erfahrung und Investition erfordert, um seine Infrastruktur zu verwalten und zu warten.<br /><br /> Die hybride Verwaltung mobiler Geräte erfordert mindestens einen primären Configuration Manager-Standort mit der Datenbankrolle, der Reporting Services-Rolle und der Dienstverbindungspunkt-Rolle. Wenn die herkömmliche PC-Verwaltung erforderlich ist, werden der Verwaltungspunkt, der Verteilungspunkt, der Softwareupdatepunkt und die Anwendungskatalogrollen möglicherweise ebenfalls benötigt. Erweiterte Funktionen wie die Zertifikatbereitstellung, die Mac-Verwaltung und Endpoint Protection fügen sogar noch mehr Rollen und Komplexität hinzu.<br /><br /> Die Configuration Manager-Hierarchie erfordert eine erhebliche Verwaltung und Wartung, um sicherzustellen, dass sie fehlerfrei ist und wie gewünscht funktioniert.<br /><br /> Wenn der Aufwand für eine Configuration Manager-Hierarchie nicht gewünscht ist, ist eine Intune standalone-Bereitstellung Ihre beste Option.|  
|![hybrid&#45;8](../../mdm/understand/media/hybrid-8.png)|**Benötigen Sie externe Tools?**<br /><br /> Configuration Manager ist ein ausgereiftes Unternehmensprodukt und enthält viele Methoden, um mit dem Dienst zu interagieren, ohne die Konsole zu verwenden. Eine Bereitstellung der hybriden Verwaltung mobiler Geräte ermöglicht Administratoren die Verwendung des Configuration Manager SDK oder die Verwendung von PowerShell, um mobile Geräte programmgesteuert zu verwalten. Sie ermöglicht Administratoren außerdem die Verwendung von Tools wie System Center Orchestrator, PowerBI und verschiedene Drittanbieter-Add-Ins.<br /><br /> Bei einer Intune standalone-Bereitstellung muss die gesamte Verwaltung über die Silverlight-Konsole ausgeführt werden, und es stehen keine externen Tools zur Verfügung.|  
|![hybrid&#45;9](../../mdm/understand/media/hybrid-9.png)|**Möchten Sie schnelle MDM-Funktionsupdates?**<br /><br /> Obwohl Configuration Manager (Current Branch) eine schnelle Wartung von Updates und Funktionen bietet, eignet sich die Bereitstellung von Clouddiensten wie z.B. Intune für eine noch schnellere Produktionsbereitstellung.<br /><br /> Intune standalone erhält neue Funktionen wahrscheinlich vor einer Bereitstellung der hybriden Verwaltung mobiler Geräte.<br /><br /> Wenn Ihre Organisation gern innovativ ist, bietet Intune standalone die neuesten MDM-Funktionen rechtzeitig an.|



<!--HONumber=Nov16_HO1-->


