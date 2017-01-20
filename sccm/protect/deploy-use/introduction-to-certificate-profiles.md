---
title: "Einführung in Zertifikatprofile | Microsoft-Dokumentation"
description: Erfahren Sie, wie Zertifikatprofile in System Center Configuration Manager mit den Active Directory-Zertifikatdiensten funktionieren.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: 7
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 25d57d25ca683608bbe9a0695b2463ad5b9a0833


---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Einführung in Zertifikatprofile in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Zertifikatprofile in System Center Configuration Manager werden zusammen mit den Active Directory-Zertifikatdiensten und der Rolle „Registrierungsdienst für Netzwerkgeräte“ verwendet, um für verwaltete Geräte Authentifizierungszertifikate bereitzustellen, sodass Benutzer problemlos auf Unternehmensressourcen zugreifen können. Sie können z. B. Zertifikatprofile erstellen und bereitstellen, um Benutzern die erforderlichen Zertifikate zum Initiieren von VPN- und Drahtlosverbindungen bereitzustellen.  

 Zertifikatprofile in System Center Configuration Manager stellen die folgenden Verwaltungsfunktionen bereit:  

-   Zertifikatregistrierung und -erneuerung von einer Unternehmenszertifizierungsstelle für Geräte unter iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop und Mobile sowie Android. Diese Zertifikate können dann für WLAN- und VPN-Verbindungen verwendet werden.  

-   Bereitstellung von Stammzertifizierungsstellen- und Zwischenzertifizierungsstellen-Zertifikaten zur Konfiguration einer Vertrauenskette auf Geräten für VPN- und WLAN-Verbindungen, wenn die Serverauthentifizierung erforderlich ist.  

-   Überwachen und Melden der installierten Zertifikate.  

 Mit Zertifikatprofilen können Benutzergeräte automatisch so konfiguriert werden, dass auf Unternehmensressourcen wie WLAN-Netzwerke und VPN-Server ohne manuelle Installation von Zertifikaten bzw. ohne Verwendung eines Out-of-Band-Prozesses zugegriffen werden kann. Mit Zertifikatprofilen können auch Unternehmensressourcen geschützt werden, da Sie sicherere Einstellungen verwenden können, die von der Public Key-Infrastruktur (PKI) Ihres Unternehmens unterstützt werden. Sie können z. B. eine Serverauthentifizierung für alle WLAN- und VPN-Verbindungen erforderlich machen, da Sie die erforderlichen Zertifikate auf den verwalteten Geräten bereitgestellt haben.  

 **Beispiel:** Alle Mitarbeiter müssen Verbindungen mit WLAN-Hotspots an verschiedenen Unternehmensstandorten herstellen können. Damit dies möglich ist, können Sie Zertifikate bereitstellen, die zum Herstellen der WLAN-Verbindung erforderlich sind. Sie können außerdem WLAN-Profile im Configuration Manager bereitstellen, die auf das richtige Zertifikat verweisen, damit die WLAN-Verbindung für die Benutzer problemlos hergestellt wird.  

 **Beispiel:** Sie haben eine PKI eingerichtet und möchten Zertifikate auf eine flexiblere, sicherere Art und Weise bereitstellen, die Benutzern ohne Beeinträchtigung der Sicherheit den Zugriff auf Unternehmensressourcen über ihre persönlichen Geräten ermöglicht. Dazu können Sie Zertifikatprofile mit Einstellungen und Protokollen konfigurieren, die von der jeweiligen Geräteplattform unterstützt werden. Die Geräte können diese Zertifikate dann automatisch von einem mit dem Internet verbundenen Registrierungsserver anfordern. Anschließend konfigurieren Sie VPN-Profile, die diese Zertifikate verwenden, damit das Gerät auf Unternehmensressourcen zugreifen kann.  

## <a name="types-of-certificate-profile"></a>Arten von Zertifikatprofilen  
 Sie können drei Typen von Zertifikatprofilen in System Center Configuration Manager erstellen:  

-   **Vertrauenswürdiges Zertifikat der Zertifizierungsstelle** : Ermöglicht die Bereitstellung eines Zertifikats einer vertrauenswürdigen Stammzertifizierungsstelle oder einer Zwischenzertifizierungsstelle, um eine Vertrauenskette zu bilden, wenn das Gerät einen Server authentifizieren muss.  

-   **Simple Certificate Enrollment Protocol (SCEP)** – Ermöglicht das Anfordern eines Zertifikats für ein Gerät oder einen Benutzer mithilfe des SCEP-Protokolls und des Registrierungsdiensts für Netzwerkgeräte auf einem Server mit Windows Server 2012 R2.
-   -   **Privater Informationsaustausch (.pfx)** – Ermöglicht das Anfordern eines Zertifikats für ein Gerät oder einen Benutzer mithilfe des SCEP-Protokolls und des Registrierungsdiensts für Netzwerkgeräte auf einem Server mit Windows Server 2012 R2.

    > [!NOTE]  
    >  Sie müssen ein Zertifikatprofil vom Typ **Vertrauenswürdiges Zertifizierungsstellenzertifikat** erstellen, bevor Sie ein Zertifikatprofil vom Typ **Einstellungen für Simple Certificate Enrollment-Protokoll (SCEP)**erstellen können.  

## <a name="requirements-and-supported-platforms"></a>Anforderungen und unterstützte Plattformen  
 Zum Bereitstellen von Zertifikatprofilen, für die das Simple Certificate Enrollment-Protokoll verwendet wird, müssen Sie den Zertifikatregistrierungspunkt auf einem Standortsystemserver am Standort der zentralen Verwaltung oder an einem primären Standort registrieren. Zudem müssen Sie ein Richtlinienmodul für den Registrierungsdienst für Netzwerkgeräte – das Configuration Manager-Richtlinienmodul – auf einem Server unter Windows Server 2012 R2 mit der Rolle „Active Directory-Zertifikatdienste“ und einem funktionsfähigen Registrierungsdienst für Netzwerkgeräte installieren, der für die Geräte verfügbar ist, die die Zertifikate benötigen. Bei Geräten, die von Microsoft Intune registriert werden, muss der Registrierungsdienst für Netzwerkgeräte über das Internet verfügbar sein, z.B. in einem Umkreisnetzwerk (auch als DMZ bezeichnet).  

 Weitere Informationen zur Unterstützung eines Richtlinienmoduls durch den Registrierungsdienst für Netzwerkgeräte, damit System Center Configuration Manager Zertifikate bereitstellen kann, finden Sie unter [Verwenden eines Richtlinienmoduls mit dem Registrierungsdienst für Netzwerkgeräte](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

 System Center Configuration Manager unterstützt die anforderungs-, gerätetyp- und betriebssystemabhängige Bereitstellung von Zertifikaten an unterschiedliche Zertifikatspeicher. Folgende Geräte und Betriebssysteme werden unterstützt:  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop und Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Um Profile für Android-, iOS-, Windows Phone- und registrierte Windows 8.1-Geräte (und höher) bereitzustellen, müssen diese Geräte bei Microsoft Intune registriert werden. Informationen zum Registrieren von Geräten finden Sie unter [Verwalten mobiler Geräte mit Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 In einem typischen Szenario für System Center Configuration Manager werden vertrauenswürdige Stammzertifizierungsstellenzertifikate zum Authentifizieren von WLAN- und VPN-Servern installiert, wenn für die Kommunikation die Authentifizierungsprotokolle EAP-TLS, EAP-TTLS und PEAP sowie die VPN-Tunnelprotokolle IKEv2, L2TP/IPsec und Cisco IPsec verwendet werden.  

 Sie müssen sicherstellen, dass auf dem Gerät ein Stammzertifizierungsstellen-Zertifikat des Unternehmens installiert ist. Nur dann können vom Gerät mithilfe eines SCEP-Zertifikatprofils Zertifikate angefordert werden.  

 Sie können eine Reihe von Einstellungen in einem SCEP-Zertifikatprofil angeben, um benutzerdefinierte Zertifikate für unterschiedliche Umgebungen oder Verbindungsanforderungen anzufordern. Der **Assistent zum Erstellen von Zertifikatprofilen** enthält zwei Seiten für Parameter für die Anmeldung. Die erste Seite **SCEP-Anmeldung**enthält Einstellungen für die Anmeldeanforderung sowie zum Installationsort des Zertifikats. Auf der zweiten Seite **Zertifikateigenschaften**wird das angeforderte Zertifikat beschrieben.  

## <a name="deploying-certificate-profiles"></a>Bereitstellen von Zertifikatvorlagen  
 Beim Bereitstellen eines Zertifikatprofils werden die Zertifikatdateien im Profil auf Clientgeräten installiert. Zudem werden SCEP-Parameter bereitgestellt, und die SCEP-Anforderungen werden auf dem Clientgerät verarbeitet. Sie können Zertifikatprofile für Benutzer- oder Gerätesammlungen bereitstellen und den Zielspeicher für die einzelnen Zertifikate angeben. Durch Anwendbarkeitsregeln wird bestimmt, ob die Zertifikate auf dem Gerät installiert werden können. Beim Bereitstellen von Zertifikatprofilen für Benutzersammlungen wird durch die Affinität zwischen Benutzer und Gerät bestimmt, auf welchen Geräten der Benutzer die Zertifikate installiert werden. Wenn Zertifikatprofile, die Benutzerzertifikate enthalten, für Gerätesammlungen bereitgestellt werden, werden die Zertifikate standardmäßig auf allen primären Geräten der Benutzer installiert. Sie können dieses Verhalten, das Zertifikate auf allen Geräten der Benutzer bereitstellt, auf der Seite **SCEP-Anmeldung** des **Assistent zum Erstellen von Zertifikatprofilen** ändern. Zudem werden Benutzerzertifikate auf Geräten, bei denen es sich um Arbeitsgruppencomputer handelt, nicht installiert.  

## <a name="monitoring-certificate-profiles"></a>Überwachen von Zertifikatprofilen  
 Sie können die Bereitstellungen von Zertifikatprofilen in der System Center Configuration Manager-Konsole im Knoten **Bereitstellungen** des Arbeitsbereichs **Überwachung** überwachen.  

 Zudem können Sie Zertifikatprofile mit einem der folgenden System Center Configuration Manager-Berichte überwachen:  

-   **Verlauf von Zertifikaten, die vom Zertifikatregistrierungspunkt ausgestellt wurden**  

-   **Nach dem Ausstellungsstatus sortierte Liste von Beständen für Zertifikate, die vom Zertifikatregistrierungspunkt angemeldet wurden**  

-   **Liste von Beständen mit Zertifikaten, die bald ablaufen**  

## <a name="automatic-revocation-of-certificates"></a>Automatisches Sperren von Zertifikaten  
 System Center Configuration Manager widerruft automatisch Benutzer- und Computerzertifikate, die unter den folgenden Umständen mithilfe von Zertifikatprofilen erstellt wurden:  

-   Die Verwaltung in System Center Configuration Manager wurde für dieses Gerät außer Kraft gesetzt.  

-   Das Gerät wird selektiv zurückgesetzt.  

-   Das Gerät wurde in der System Center Configuration Manager-Hierarchie gesperrt.  

 Zum Sperren der Zertifikate wird vom Standortserver ein Sperrbefehl an die ausstellende Zertifizierungsstelle gesendet. Der Grund für die Sperre ist **Vorgangsende**.  



<!--HONumber=Dec16_HO3-->


