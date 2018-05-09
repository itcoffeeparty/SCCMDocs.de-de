---
title: Einführung in Zertifikatprofile
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Zertifikatprofile in System Center Configuration Manager mit den Active Directory-Zertifikatdiensten funktionieren.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c4230b935b7fabc44743d57fcb2315348edb4274
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Einführung in Zertifikatprofile in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Zertifikatprofile arbeiten mit Active Directory-Zertifikatdiensten und der Rolle des Registrierungsdiensts für Netzwerkgeräte (NDES, Network Device Enrollment Service). Erstellen Sie Authentifizierungszertifikate für verwaltete Geräte, bzw. stellen Sie sie bereit, damit Benutzer einfach auf Unternehmensressourcen zugreifen können. Sie können z.B. Zertifikatprofile erstellen und bereitstellen, um Benutzern die erforderlichen Zertifikate zum Herstellen einer Verbindung mit VPN- und Drahtlosverbindungen bereitzustellen.

Zertifikatprofile können Benutzergeräte automatisch konfigurieren. Benutzer greifen auf Unternehmensressourcen wie WLAN-Netzwerke und VPN-Server zu, ohne manuell Zertifikate erstellen zu müssen oder einen Out-of-Band-Vorgang zu verwenden. Mit Zertifikatprofilen werden Unternehmensressourcen geschützt, da Sie sicherere Einstellungen verwenden können, die von der Public Key-Infrastruktur (PKI) Ihres Unternehmens unterstützt werden. Sie können z.B. eine Serverauthentifizierung für alle WLAN- und VPN-Verbindungen erforderlich machen, da Sie die erforderlichen Zertifikate auf den verwalteten Geräten bereitgestellt haben.   

Zertifikatprofile bieten die folgenden Verwaltungsfunktionen:  

-   Zertifikatregistrierung und -erneuerung von einer Unternehmenszertifizierungsstelle für Geräte unter iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop und Mobile sowie Android. Diese Zertifikate können dann für WLAN- und VPN-Verbindungen verwendet werden.  

-   Bereitstellen vertrauenswürdiger Zertifikate der Stamm- oder Zwischenzertifizierungsstelle Diese Zertifikate konfigurieren eine Vertrauenskette auf Geräten für VPN- und WLAN-Verbindungen, wenn die Serverauthentifizierung erforderlich ist.  

-   Überwachen und Melden der installierten Zertifikate.  

**Beispiel:** Alle Mitarbeiter müssen Verbindungen mit WLAN-Hotspots an verschiedenen Unternehmensstandorten herstellen können. Um die einfache Benutzerverbindung zu ermöglichen, stellen Sie zunächst die Zertifikate bereit, die für die WLAN-Verbindung erforderlich sind. Stellen Sie anschließend die WLAN-Profile bereit, die auf das Zertifikat verweisen.  

**Beispiel:** Sie verfügen über eine PKI. Sie möchten zu einer flexibleren und sichereren Methode für die Bereitstellung von Zertifikaten wechseln. Benutzer müssen auf Unternehmensressourcen von ihren persönlichen Geräten aus zugreifen können, ohne dass sie die Sicherheit beeinträchtigen. Konfigurieren Sie Zertifikatprofile mit Einstellungen und Protokollen, die von der jeweiligen Geräteplattform unterstützt werden. Die Geräte können diese Zertifikate dann automatisch von einem mit dem Internet verbundenen Registrierungsserver anfordern. Anschließend konfigurieren Sie VPN-Profile, die diese Zertifikate verwenden, damit das Gerät auf Unternehmensressourcen zugreifen kann.  



## <a name="types-of-certificate-profiles"></a>Arten von Zertifikatprofilen  
 Es gibt drei Arten von Zertifikatprofilen:  

-   **Vertrauenswürdiges ZS-Zertifikat**: Stellen Sie ein vertrauenswürdiges Zertifikat der Stamm- oder Zwischenzertifizierungsstelle bereit. Diese Zertifikate bilden eine Vertrauenskette, wenn das Gerät einen Server authentifizieren muss.  

-   **Registrierungsdienst für Netzwerkgeräte**: Fordern Sie mithilfe des SCEP-Protokolls ein Zertifikat für ein Gerät oder einen Benutzer an. Dieser Typ erfordert eine NDES-Rolle (Registrierungsdienst für Netzwerkgeräte) auf einem Server unter Windows Server 2012 R2 oder höher.

    Sie müssen ein **vertrauenswürdiges Zertifikat der Zertifizierungsstelle** erstellen, um ein Zertifikatprofil des Typs **Simple Certificate Enrollment Protocol (SCEP)** erstellen zu können.

-   **Privater Informationsaustausch (.pfx)**: Erfordert für ein Gerät oder einen Benutzer ein PFX-Zertifikat (auch als PKCS #12-Zertifikat bezeichnet).<!--1321368-->  

    Sie können PFX-Zertifikatprofile erstellen, indem Sie entweder aus bestehenden Zertifikaten [Anmeldeinformationen importieren](/sccm/mdm/deploy-use/import-pfx-certificate-profiles) oder für die Bearbeitung von Anfragen [eine Zertifizierungsstelle definieren](/sccm/mdm/deploy-use/create-pfx-certificate-profiles).

    > [!Note]  
    > Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

    Ab Version 1706 können Sie Microsoft oder Entrust als Zertifizierungsstelle für **PFX-Zertifikate (Personal information exchange)** nutzen.


## <a name="requirements-and-supported-platforms"></a>Anforderungen und unterstützte Plattformen  
Um Zertifikatprofile bereitzustellen, die SCEP verwenden, installieren Sie den Zertifikatregistrierungspunkt auf einem Standortsystemserver. Installieren Sie ebenso ein Richtlinienmodul für den Registrierungsdienst für Netzwerkgeräte, das Configuration Manager-Richtlinienmodul, auf einem Server, der Windows Server 2012 R2 oder höher ausführt. Dieser Server erfordert die Rolle „Active Directory-Zertifikatdienste“ sowie einen funktionierenden Registrierungsdienst für Netzwerkgeräte, der für Geräte, die die Zertifikate erfordern, zugänglich ist. Benutzer müssen über das Internet auf den Registrierungsdienst für Netzwerkgeräte auf Geräten, die mit Microsoft Intune registriert sind, zugreifen können, beispielsweise in einem Umkreisnetzwerk, auch als DMZ bekannt.  

PFX-Zertifikate erfordern auch einen Zertifikatregistrierungspunkt. Geben Sie auch die Zertifizierungsstelle (Certificate Authority – CA) für das Zertifikat und die notwendigen Anmeldeinformationen an. Ab Version 1706 können Sie entweder Microsoft oder Entrust als Zertifizierungsstelle angeben.  

Weitere Informationen zur Unterstützung eines Richtlinienmoduls durch den Registrierungsdienst für Netzwerkgeräte, damit Configuration Manager Zertifikate bereitstellen kann, finden Sie unter [Verwenden eines Richtlinienmoduls mit dem Registrierungsdienst für Netzwerkgeräte](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

Configuration Manager unterstützt die anforderungs-, gerätetyp- und betriebssystemabhängige Bereitstellung von Zertifikaten für unterschiedliche Zertifikatspeicher. Folgende Geräte und Betriebssysteme werden unterstützt:  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop und Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Um Profile für Android-, iOS-, Windows Phone- und registrierte Windows 8.1-Geräte (und höher) bereitzustellen, müssen diese Geräte [bei Microsoft Intune registriert](/intune/device-enrollment) werden.   

In einem typischen Szenario für Configuration Manager werden vertrauenswürdige Zertifikate von Stammzertifizierungsstellen zum Authentifizieren von WLAN- und VPN-Servern installiert, wenn für die Kommunikation die Authentifizierungsprotokolle EAP-TLS, EAP-TTLS und PEAP sowie die VPN-Tunnelprotokolle IKEv2, L2TP/IPsec und Cisco IPsec verwendet werden.  

Ein Zertifikat einer Stammzertifizierungsstelle des Unternehmens muss auf dem Gerät installiert sein. Nur dann können vom Gerät mithilfe eines SCEP-Zertifikatprofils Zertifikate angefordert werden.  

Sie können Einstellungen in einem SCEP-Zertifikatprofil angeben, um benutzerdefinierte Zertifikate für unterschiedliche Umgebungen oder Verbindungsanforderungen anzufordern. Der **Assistent zum Erstellen von Zertifikatprofilen** verfügt über zwei Seiten für Parameter für die Anmeldung. Die erste Seite **SCEP-Anmeldung** enthält Einstellungen für die Anmeldeanforderung sowie zum Installationsort des Zertifikats. Auf der zweiten Seite **Zertifikateigenschaften**wird das angeforderte Zertifikat beschrieben.  

## <a name="deploying-certificate-profiles"></a>Bereitstellen von Zertifikatprofilen  
 Beim Bereitstellen eines Zertifikatprofils werden die Zertifikatdateien im Profil auf Clientgeräten installiert. Zudem werden SCEP-Parameter bereitgestellt, und die SCEP-Anforderungen werden auf dem Clientgerät verarbeitet. Sie können Zertifikatprofile für Benutzer- oder Gerätesammlungen bereitstellen und den Zielspeicher für die einzelnen Zertifikate angeben. Durch Anwendbarkeitsregeln wird bestimmt, ob die Zertifikate auf dem Gerät installiert werden können. Beim Bereitstellen von Zertifikatprofilen für Benutzersammlungen wird durch die Affinität zwischen Benutzer und Gerät bestimmt, auf welchen Geräten der Benutzer die Zertifikate installiert werden. Wenn Zertifikatprofile, die Benutzerzertifikate enthalten, für Gerätesammlungen bereitgestellt werden, werden die Zertifikate standardmäßig auf allen primären Geräten der Benutzer installiert. Das Verhalten, dass das Zertifikat auf allen Geräten der Benutzer bereitgestellt wird, können Sie auf der Seite **SCEP-Anmeldung** des **Assistenten zum Erstellen von Zertifikatprofilen** ändern. Wenn die Geräte Arbeitsgruppencomputer sind, werden Benutzerzertifikate nicht bereitgestellt.  

## <a name="monitoring-certificate-profiles"></a>Überwachen von Zertifikatprofilen  

Sie können Zertifikatprofilbereitstellungen überwachen, indem Sie Konformitätsergebnisse oder -berichte anzeigen. Diese Ansätze werden unter [Überwachen von Zertifikatprofilen in System Center Configuration Manager](/sccm/protect/deploy-use/monitor-certificate-profiles) beschrieben.


## <a name="automatic-revocation-of-certificates"></a>Automatisches Sperren von Zertifikaten  
 System Center Configuration Manager widerruft automatisch Benutzer- und Computerzertifikate, die unter den folgenden Umständen mithilfe von Zertifikatprofilen erstellt wurden:  

-   Die Verwaltung in System Center Configuration Manager wurde für dieses Gerät außer Kraft gesetzt.  

-   Das Gerät wird selektiv zurückgesetzt.  

-   Das Gerät wurde in der System Center Configuration Manager-Hierarchie gesperrt.  

 Zum Sperren der Zertifikate wird vom Standortserver ein Sperrbefehl an die ausstellende Zertifizierungsstelle gesendet. Der Grund für die Sperre ist **Vorgangsende**.  
