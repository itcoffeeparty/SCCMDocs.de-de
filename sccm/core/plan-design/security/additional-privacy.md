---
title: "System Center Configuration Manager-Datenschutzbestimmungen – Zusatzinformationen | Microsoft-Dokumentation"
description: "Erfahren Sie mehr darüber, wie Microsoft Daten aus einer Bereitstellung von System Center Configuration Manager sammelt und verwendet."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translation.priority.ht:
- cs-cz
- de-de
- en-gb
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 613b7dbf81de84129e113468d554d8430cbc3182

---
# <a name="additional-information-about-privacy-for-system-center-configuration-manager"></a>Weitere Informationen zum Datenschutz für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


## <a name="updates-and-servicing"></a>Updates und Wartung
System Center Configuration Manager führt ein neues Updatemodell ein, das Sie beim Beibehalten des aktuellen Stands Ihrer Configuration Manager-Bereitstellung mit den neuesten Updates und Features unterstützt. Wenn dieses Feature installiert ist, fügt es eine neue Standortsystemrolle auf einem Standortserver hinzu, den der Administrator als Dienstverbindungspunkt ausgewählt hat. Weitere Informationen darüber, welche Informationen gesammelt werden und wie diese verwendet werden, finden Sie im Abschnitt „Nutzungsdaten“ dieser Anweisung.


## <a name="usage-data"></a>Nutzungsdaten
System Center Configuration Manager sammelt Diagnose- und Nutzungsdaten über sich selbst, die von Microsoft zur Verbesserung der Anwendungsinstallation, Qualität und Sicherheit künftiger Releases verwendet werden.
Diagnose- und Nutzungsdaten sind für jede System Center Configuration Manager-Hierarchie aktiviert. Es besteht aus SQL Server-Abfragen, die wöchentlich an jedem primären Standort und am Standort der zentralen Verwaltung ausgeführt werden. Wenn die Hierarchie einen Standort der zentralen Verwaltung verwendet, werden die Daten von primären Standorten dann an diesen Standort repliziert. Am obersten Standort Ihrer Hierarchie sendet der Dienstverbindungspunkt diese Informationen, wenn er prüft, ob Updates vorhanden sind. Wenn sich der Dienstverbindungspunkt im Offlinemodus befindet, werden die Informationen mithilfe des Dienstverbindungstools übertragen.

Configuration Manager erfasst nur Daten von der SQL Server-Datenbank des Standorts und nicht direkt von Clients oder Standortservern.

Administratoren können die Ebene der Datensammlung in der Einstellung „Nutzungsdaten“ der Configuration Manager-Konsole ändern.

Weitere Informationen finden Sie im Artikel „Weitere Informationen“ zu Nutzungsdatenebenen und -einstellungen unter [http://go.microsoft.com/fwlink/?LinkID=626566](http://go.microsoft.com/fwlink/?LinkID=626566).


## <a name="customer-experience-improvement-program"></a>Programm zur Verbesserung der Benutzerfreundlichkeit
Das Programm zur Verbesserung der Benutzerfreundlichkeit (Customer Experience Improvement Program, CEIP) sammelt über die Configuration Manager-Konsole Informationen zu Ihrer Hardwarekonfiguration sowie Ihrer Verwendung unserer Software und unserer Dienste, um Trends und Gebrauchsmuster zu identifizieren. Ebenfalls werden vom CEIP Typ und Anzahl der auftretenden Fehler, die Software- und Hardwareleistung sowie die Geschwindigkeit der Dienste protokolliert.  Ihr Name, Ihre Adresse oder andere Kontaktdaten werden nicht erfasst. Es werden keine CEIP-Daten von Client-Computern gesammelt.

Wir verwenden diese Informationen, um die Qualität, Zuverlässigkeit und Leistung von Microsoft-Software und -Diensten zu verbessern.

Weitere Informationen zu den von CEIP erfassten, verarbeiteten und übermittelten Information siehe die CEIP-Datenschutzerklärung unter [http://go.microsoft.com/fwlink/?LinkID=525211](http://go.microsoft.com/fwlink/?LinkID=525211).

## <a name="oms-connector"></a>OMS-Connector
Der Microsoft Operations Management Suite-Connector synchronisiert Daten wie Sammlungen von System Center Configuration Manager in Microsoft Operations Management Suite. Die Microsoft Azure-Abonnement-ID und der geheime Schlüssel werden in der Configuration Manager-Datenbank gespeichert, wenn ein Administrator die Funktion konfiguriert. Sowohl das Azure Active Directory-Clientgeheimnis als auch der gemeinsam genutzte Schlüssel der Microsoft Operations Management Suite werden in der lokalen System Center Configuration Manager-Datenbank gespeichert. Die gesamte Kommunikation zwischen System Center Configuration Manager und Microsoft Operations Management Suite verwendet HTTPS. Es werden keine zusätzlichen Informationen über die Sammlungen an Microsoft außerhalb von zufälligen Telemetriedaten bereitgestellt. Weitere Informationen darüber, welche Informationen von Microsoft Operations Management Suite gesammelt werden, finden Sie unter [http://go.microsoft.com/fwlink/?LinkId=823545](http://go.microsoft.com/fwlink/?LinkId=823545).

## <a name="asset-intelligence"></a>Asset Intelligence
Mit Asset Intelligence können IT-Administratoren die Konformität mit Konfigurationsstandards definieren, nachverfolgen und proaktiv verwalten. Durch Messungen und Berichterstattung zu Bereitstellung und Verwendung sowohl physischer als auch virtueller Anwendungen werden den Organisationen gute Geschäftsentscheidungen zur Softwarelizenzierung und die Einhaltung von Lizenzverträgen erleichtert. Nach dem Sammeln von Nutzungsdaten von Configuration Manager-Clients stehen Administratoren verschiedene Features zur Verfügung, mit denen sie die Daten einschließlich Sammlungen, Abfragen und Berichte anzeigen können.

Bei der Synchronisierung wird jeweils ein Katalog bekannter Software von Microsoft heruntergeladen. Der IT-Administrator kann wahlweise Informationen über nicht kategorisierte Softwaretitel, die in der Organisation gefunden wurden, an Microsoft senden, um entsprechende Recherchen durchzuführen und diese in den Katalog aufzunehmen. Vor dem Hochladen dieser Informationen werden in einem Dialogfeld die Daten angezeigt, die hochgeladen werden sollen. Hochgeladene Daten können nicht zurückgerufen werden. Von Asset Intelligence werden keine Benutzer-, Computer oder Lizenzverwendungsinformationen an Microsoft gesendet.

Nachdem ein Softwaretitel hochgeladen wurde, können die Recherchemitarbeiter bei Microsoft diesen identifizieren und kategorisieren und danach dieses Wissen allen anderen Kunden, die dieses Feature verwenden, sowie anderen Nutzern des Katalogs zur Verfügung stellen. Die Informationen über alle hochgeladenen Softwaretitel werden zu Allgemeingut, da das Wissen um die betreffende Anwendung und ihre Kategorisierung Teil des Katalogs werden und somit von anderen Katalognutzern heruntergeladen werden können. Berücksichtigen Sie beim Konfigurieren der Asset Intelligence-Datensammlung und bei der Entscheidung, ob Informationen an System Center Online übermittelt werden sollen, die Datenschutzanforderungen Ihrer Organisation.

Asset Intelligence ist in System Center Configuration Manager standardmäßig nicht aktiviert. Nicht kategorisierte Titel werden nie automatisch hochgeladen. Im System kann dieser Task auch nicht automatisiert werden. Sie müssen den Upload jedes Softwaretitels manuell auswählen und genehmigen.

## <a name="endpoint-protection"></a>Endpoint Protection
Microsoft Cloud Protection Service (früher Microsoft Active Protection Service oder MAPS) anwendbare Produkte: System Center Endpoint Protection und das Endpoint Protection-Feature von System Center Configuration Manager (für die Verwaltung von System Center Endpoint Protection und Windows Defender für Windows 10). Diese Funktion ist für System Center Endpoint Protection für Linux oder System Center Endpoint Protection für Mac nicht implementiert.

Die Microsoft Cloud Protection Service-Antimalware-Community ist eine freiwillige weltweite Online-Community, die System Center Endpoint Protection-Benutzer umfasst. Nach einem Beitritt zu Microsoft Cloud Protection Service sendet System Center Endpoint Protection automatisch Informationen an Microsoft, anhand derer bestimmt wird, welche Software auf mögliche Bedrohungen hin zu überprüfen ist und wie die Wirksamkeit von System Center Endpoint Protection verbessert werden kann. Diese Community hilft bei der Eindämmung neuer Infektionen mit Schadsoftware. Wenn ein Microsoft Cloud Protection Service-Bericht Details zu Schadsoftware oder potenziell unerwünschter Software enthält, die möglicherweise vom Endpoint Protection-Client entfernt werden kann, wird von Microsoft Cloud Protection Service die jüngste Signatur heruntergeladen, um für Abhilfe zu sorgen. Von Microsoft Cloud Protection Service werden auch „falsch positive Ergebnisse“ ermittelt (ein Element wurde ursprünglich als Schadsoftware identifiziert, obwohl es keine war) und behoben.

Microsoft Cloud Protection Service-Berichte enthalten Informationen potenzielle Malware-Dateien wie Dateinamen, kryptografische Hashwerte, Anbieter, Größe und Datumstempel. Darüber hinaus sammelt Microsoft Cloud Protection Service möglicherweise vollständige URLs, um den Ursprung der Datei anzugeben. Diese URLs können gelegentlich persönliche Informationen wie Suchbegriffe oder in Formularen eingegebene Daten enthalten. Berichte können auch die Aktionen enthalten, die Sie vorgenommen haben, wenn Endpoint Protection Sie über unerwünschte Software informiert hat. Microsoft Cloud Protection Service-Berichte enthalten diese Informationen, damit Microsoft beurteilen kann, wie effektiv Endpoint Protection Malware und potenziell unerwünschte Software erkennen und entfernen kann und versuchen kann, neue Malware zu identifizieren.

Ein Beitritt zu Microsoft Cloud Protection Service ist mit einfacher Mitgliedschaft oder mit Premiummitgliedschaft möglich. In einfachen Mitgliederberichten sind die oben beschriebenen Informationen enthalten. Premiummitgliederberichte sind umfangreicher und können zusätzliche Details über die von Endpoint Protection erkannte Software enthalten, darunter den Speicherort der Software, Dateinamen, Softwarebetrieb sowie Auswirkungen auf den Computer. Diese Berichte und die Berichte anderer Endpoint Protection-Benutzer, die an Microsoft Cloud Protection Service teilnehmen, werden von Microsoft-Mitarbeitern verwendet, um neue Bedrohungen rascher zu erkennen. Anschließend werden Schadsoftwaredefinitionen für Programme erstellt, die den Analysekriterien entsprechen, und als aktualisierte Definitionen allen Benutzern über Microsoft Update zugänglich gemacht.

Zur besseren Erkennung und Behebung bestimmter Infektionen mit Schadsoftware werden vom Produkt regelmäßig Informationen zum Sicherheitszustand des PCs an Microsoft Cloud Protection Service gesendet. Diese Informationen umfassen Details zu den Sicherheitseinstellungen des PCs sowie Protokolldateien, in denen die Treiber und andere Software beschrieben sind, die beim Hochfahren des Computers geladen werden.
Eine Nummer, die Ihren PC eindeutig identifiziert, wird ebenfalls gesendet. Möglicherweise werden von Microsoft Cloud Protection Service die IP-Adressen gesammelt, mit denen die potenziellen Schadsoftwaredateien eine Verbindung herstellen.

Microsoft Cloud Protection Service-Berichte werden zur Verbesserung der Softwareprodukte und Dienste von Microsoft verwendet. Sie können außerdem zu Statistik-, Test- oder Analysezwecken sowie zur Erstellung von Definitionen verwendet werden. Nur Mitarbeiter, Auftragnehmer, Partner und Lieferanten von Microsoft, die diese Berichte für ihre Arbeit benötigen, erhalten Zugriff darauf.

Die Erfassung persönlicher Informationen durch Microsoft Cloud Protection Service erfolgt nicht absichtlich. Die von Microsoft Cloud Protection Service unbeabsichtigt erfassten persönlichen Informationen werden von Microsoft nicht verwendet, um Sie zu identifizieren oder zu kontaktieren.

Weitere Details zu gesammelten Daten finden Sie in der Produktdokumentation unter [http://go.microsoft.com/fwlink/?LinkId=823547](http://go.microsoft.com/fwlink/?LinkId=823547).

## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Standorthierarchie – geografische Ansicht mit Bing Maps
Mit „Standorthierarchie – geografische Ansicht“ kann die physische Configuration Manager-Servertopologie anhand von Karten, die von Microsoft Bing Maps bereitgestellt werden, angezeigt werden. Zum Aktivieren dieses Features werden von Ihnen bereitgestellte Standortinformationen von Ihrem Server an den Webdienst Bing Maps übertragen.

Microsoft verwendet die Informationen, um Microsoft Bing Maps sowie andere Websites und Dienste zu betreiben und zu verbessern. Weitere Informationen finden Sie in der Microsoft-Datenschutzbestimmung unter http://go.microsoft.com/fwlink/?LinkId=823548.
Sie haben die Wahl, die geografische Ansicht der Standorthierarchie nicht zu verwenden. Die Hierarchiediagrammansicht gestattet Ihnen, die Hierarchie anzusehen, ohne den Dienst Bing Maps zu verwenden.

## <a name="microsoft-intune-subscription"></a>Microsoft Intune-Abonnement
Kunden, die ein Abonnement für Microsoft Intune erworben haben, können Configuration Manager zum Verwalten ihrer mobilen Geräte über Microsoft Intune verwenden. [Microsoft Online Services-Datenschutzbestimmung](http://go.microsoft.com/fwlink/?LinkId=262214) gilt für die Microsoft Online-Services, einschließlich Microsoft Intune. Wenn Kunden auch ein Microsoft Intune-Abonnement haben, sollte die [Onlinedatenschutzbestimmungen für Online Dienste von Microsoft ](http://go.microsoft.com/fwlink/?LinkId=262214) in Verbindung mit dieser Datenschutzerklärung gelesen werden.

Für die gesamte Microsoft Intune-Kommunikation wird HTTPS verwendet. Zum Konfigurieren des Microsoft Intune-Abonnements und zum Herunterladen der Zertifikatsignieranforderung (Certificate Signing Request, CSR), die für die Konfiguration der iOS-Unterstützung erforderlich ist, muss sich ein Administrator über das Unternehmenskonto unter Angabe des dazugehörigen Kennworts bei Microsoft Intune anmelden. Die betreffenden Anmeldeinformationen werden nicht in Configuration Manager gespeichert. Die übrige Kommunikation mit Microsoft Intune wird über PKI-Zertifikate authentifiziert, die automatisch von Microsoft Intune generiert werden.

Zur Verwaltung von Geräten, die mit Microsoft Intune verbunden sind, werden bestimmte Informationen mit Microsoft Intune ausgetauscht. Zu diesen Informationen gehören der Benutzerprinzipalname (UPN) aller Benutzer, die dem Dienst zugewiesen wurden, sowie Inventarinformationen der Geräte, die von Microsoft Intune verwaltet werden. Metadaten (z.B. Anwendungsname, Herausgeber und Version) für Inhalte, die Manage.Microsoft.com-Verteilungspunkten zugewiesen wurden, werden an Microsoft Intune gesendet. Die einem Manage.Microsoft.com-Verteilungspunkt zugewiesenen eigentlichen Binärinhalte werden vor dem Hochladen an Microsoft Intune verschlüsselt.

Diese Option wird standardmäßig nicht konfiguriert. Administratoren können steuern, welche Inhalte an Manage.microsoft.com-Verteilungspunkte übertragen und welche Benutzer dem Dienst zugewiesen werden. Das Feature kann jederzeit entfernt werden.



<!--HONumber=Dec16_HO3-->


