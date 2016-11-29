---
title: "Voraussetzungen für Zertifikatprofile | System Center Configuration Manager"
description: "Erfahren Sie mehr zu Zertifikatprofilen in System Center Configuration Manager sowie zu den entsprechenden externen Abhängigkeiten und Abhängigkeiten innerhalb des Produkts."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0317fd02-3721-4634-b18b-7c976a4e92bf
caps.latest.revision: 9
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ba42385eb31fffd9f74b35108e71a1ae5a9c71f7


---
# <a name="prerequisites-for-certificate-profiles-in-system-center-configuration-manager"></a>Voraussetzungen für Zertifikatprofile in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Zertifikatprofile in System Center Configuration Manager weisen externe Abhängigkeiten sowie Abhängigkeiten innerhalb des Produkts auf.  

## <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Eine ausstellende Zertifizierungsstelle, unter der Active Directory-Zertifikatdienste (AD CS) ausgeführt werden.<br /><br /> Zum Widerrufen von Zertifikaten benötigt das Computerkonto des Standortservers am Anfang der Hierarchie die Berechtigung *Zertifikate ausstellen und verwalten* für jede Zertifikatvorlage, die von einem Zertifikatprofil in Configuration Manager verwendet wird. Erteilen Sie alternativ Zertifikat-Manager-Berechtigungen, um für alle von dieser Zertifizierungsstelle verwendeten Zertifikatvorlagen Berechtigungen zu erteilen.<br /><br /> Die Genehmigung der Verwaltung für Zertifikatsanforderungen wird unterstützt. Die zum Ausstellen von Zertifikaten verwendeten Zertifikatvorlagen müssen für **Informationen werden in der Anforderung angegeben** für den Zertifikatantragsteller so konfiguriert werden, dass dieser Wert von System Center Configuration Manager automatisch bereitgestellt werden kann.|Weitere Informationen zu Active Directory-Zertifikatdiensten finden Sie in der Dokumentation zu Windows Server.<br /><br /> Für Windows Server 2012: [Übersicht über Active Directory-Zertifikatdienste](http://go.microsoft.com/fwlink/p/?LinkId=286744)<br /><br /> Für Windows Server 2008: [Active Directory-Zertifikatdienste in Windows Server 2008](http://go.microsoft.com/fwlink/p/?LinkId=115018)|  
|Der Rollendienst „Registrierungsdienst für Netzwerkgeräte“ für Active Directory-Zertifikatdienste, der unter Windows Server 2012 R2 ausgeführt wird.<br /><br /> Beachten Sie auch Folgendes:<br /><br /> Bei der Kommunikation zwischen dem Client und dem Registrierungsdienst für Netzwerkgeräte werden nur die Portnummern TCP 443 (für HTTPS) bzw. TCP 80 (für HTTP) unterstützt.<br /><br /> Der Server, auf dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird, muss sich auf einem anderen Server befinden als die ausstellende Zertifizierungsstelle.|System Center Configuration Manager kommuniziert mit dem Registrierungsdienst für Netzwerkgeräte in Windows Server 2012 R2, um SCEP-Anforderungen (Simple Certificate Enrollment-Protokoll) zu generieren und zu überprüfen.<br /><br /> Wenn Sie für Benutzer oder Geräte Zertifikate ausstellen, von denen eine Verbindung mit dem Internet hergestellt wird (z.B. für mobile Geräte, die mit Microsoft Intune verwaltet werden), muss der Server, auf dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird, für diese Geräte über das Internet verfügbar sein. Installieren Sie den Server beispielsweise in einem Umkreisnetzwerk (auch als überwachtes Subnetz bezeichnet).<br /><br /> Wenn sich zwischen dem Server, auf dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird, und der ausstellenden Zertifizierungsstelle eine Firewall befindet, müssen Sie diese so konfigurieren, dass der Datenverkehr (DCOM) zwischen den Servern zugelassen wird. Diese Anforderung zur Firewall gilt auch für den Server, auf dem der System Center Configuration Manager-Standortserver und die ausstellende Zertifizierungsstelle ausgeführt werden, damit Zertifikate von System Center Configuration Manager gesperrt werden können.<br /><br /> Wenn der Registrierungsdienst für Netzwerkgeräte so konfiguriert wurde, dass die bewährte Sicherheitsmethode SSL verwendet werden muss, stellen Sie sicher, dass Geräte, mit denen eine Verbindung hergestellt wird, zum Überprüfen des Serverzertifikats Zugriff auf die Zertifikatsperrliste (Certificate Revocation List, CRL) haben.<br /><br /> Weitere Informationen zum Registrierungsdienst für Netzwerkgeräte in Windows Server 2012 R2 finden Sie unter [Using a Policy Module with the Network Device Enrollment Service (Verwenden eines Richtlinienmoduls mit dem Registrierungsdienst für Netzwerkgeräte)](http://go.microsoft.com/fwlink/p/?LinkId=328657).|  
|Wenn die ausstellende Zertifizierungsstelle unter Windows Server 2008 R2 ausgeführt wird, ist für diesen Server ein Hotfix für SCEP-Erneuerungsanforderungen erforderlich.|Installieren Sie den Hotfix, sofern Sie dies nicht bereits getan haben. Weitere Informationen finden Sie im Artikel [2483564: Erneuerungsanforderung für ein SCEP-Zertifikat in Windows Server 2008 R2 schlägt fehl, wenn das Zertifikat mithilfe der NDES verwaltet wird](http://go.microsoft.com/fwlink/?LinkId=311945) in der Microsoft Knowledge Base.|  
|Ein PKI-Clientauthentifizierungszertifikat und ein exportiertes Zertifikat der Stammzertifizierungsstelle.|Mit diesem Zertifikat wird der Server, auf dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird, für System Center Configuration Manager authentifiziert.<br /><br /> Weitere Informationen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).|  
|Unterstützte Gerätebetriebssysteme.|Zertifikatprofile können für Geräte unter den Betriebssystemen iOS, Windows 8.1, Windows RT 8.1, Windows 10 und Android bereitgestellt werden.|  

## <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Standortsystemrolle für Zertifikatregistrierungspunkt|Zertifikatprofile können erst nach der Installation der Standortsystemrolle für den Zertifikatregistrierungspunkt verwendet werden. Diese Rolle kommuniziert mit der System Center Configuration Manager-Datenbank, dem System Center Configuration Manager-Standortserver und dem System Center Configuration Manager-Richtlinienmodul.<br /><br /> Weitere Informationen zu den Systemanforderungen für diese Standortsystemrolle sowie zur Installation in der Hierarchie finden Sie im Abschnitt **Anforderungen an das Standortsystem** im Thema [Unterstützte Konfigurationen für System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md).<br /><br /> Beachten Sie: Der Zertifikatregistrierungspunkt darf nicht auf dem Server installiert sein, auf dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird.|  
|System Center Configuration Manager-Richtlinienmodul, das auf dem Server installiert ist, auf dem der Rollendienst „Registrierungsdienst für Netzwerkgeräte“ für Active Directory-Zertifikatdienste ausgeführt wird|Zum Bereitstellen von Zertifikatprofilen muss das System Center Configuration Manager-Richtlinienmodul installiert werden. Sie finden dieses Richtlinienmodul auf dem System Center Configuration Manager-Installationsmedium.|  
|Ermittlungsdaten|Die Werte für den Zertifikatantragsteller und den alternativen Antragstellernamen werden von System Center Configuration Manager bereitgestellt und aus den von der Ermittlung gesammelten Informationen abgerufen:<br /><br /> Für Benutzerzertifikate: Active Directory-Benutzerermittlung<br /><br /> Für Computerzertifikate: Active Directory-Systemermittlung und Netzwerkermittlung|  
|Spezielle Sicherheitsberechtigungen für die Verwaltung von Zertifikatprofilen|Sie müssen über die folgenden Sicherheitsberechtigungen verfügen, um Einstellungen für den Zugriff auf Unternehmensressourcen wie Zertifikatprofile, WLAN-Profile und VPN-Profile zu verwalten:<br /><br /> So zeigen Sie Warnungen und Berichte für Zertifikatprofile an und verwalten sie: **Erstellen**, **Löschen**, **Ändern**, **Bericht ändern**, **Lesen**und **Bericht ausführen** für das Objekt **Warnungen** .<br /><br /> So erstellen und verwalten Sie Zertifikatprofile: **Richtlinie erstellen**, **Bericht ändern**, **Lesen** und **Bericht ausführen** für das Objekt **Zertifikatprofil** .<br /><br /> So verwalten Sie Bereitstellungen von WLAN-, Zertifikat- und VPN-Profilen: **Konfigurationsrichtlinien bereitstellen**, **Warnung zu Clientstatus ändern**, **Lesen**und **Ressource lesen** für das Objekt **Sammlung** .<br /><br /> So verwalten Sie alle Konfigurationsrichtlinien: **Erstellen**, **Löschen**, **Ändern**, **Lesen** und **Sicherheitsbereich festlegen** für das Objekt **Konfigurationsrichtlinie** .<br /><br /> So führen Sie mit Zertifikatprofilen verknüpfte Abfragen aus: Berechtigung **Lesen** für das Objekt **Abfrage** .<br /><br /> So zeigen Sie Zertifikatprofilinformationen in der System Center Configuration Manager-Konsole an: Berechtigung **Lesen** für das Objekt **Standort**.<br /><br /> So zeigen Sie Statusmeldungen für Zertifikatprofile an: Berechtigung **Lesen** für das Objekt **Statusmeldungen** .<br /><br /> So erstellen und verwalten Sie das Zertifikatprofil der vertrauenswürdigen Zertifizierungsstelle: **Richtlinie erstellen**, **Bericht ändern**, **Lesen** und **Bericht ausführen** für das Objekt **Zertifikatprofil der vertrauenswürdigen Zertifizierungsstelle** .<br /><br /> So erstellen und verwalten Sie VPN-Profile: **Richtlinie erstellen**, **Bericht ändern**, **Lesen** und **Bericht ausführen** für das Objekt **VPN-Profil** .<br /><br /> So erstellen und verwalten Sie WLAN-Profile: **Richtlinie erstellen**, **Bericht ändern**, **Lesen** und **Bericht ausführen** für das Objekt **WLAN-Profil** .<br /><br /> In der Sicherheitsrolle **Zugriffs-Manager für Unternehmensressourcen** sind diese Berechtigungen zum Verwalten der Zertifikatprofile in System Center Configuration Manager enthalten. Weitere Informationen finden Sie im Abschnitt **Configure role-based administration** des Themas [Configure security in System Center Configuration Manager](../../core/plan-design/security/configure-security.md) .|  



<!--HONumber=Nov16_HO1-->

