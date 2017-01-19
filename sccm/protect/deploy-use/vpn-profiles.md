---
title: VPN-Profile in System Center Configuration Manager | Microsoft-Dokumentation
description: "So verwenden Sie VPN-Profile in System Center Configuration Manager, um Benutzern in Ihrer Organisation Einstellungen für VPN bereitzustellen."
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: 6
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 593fbd0587d54490246f48ae54f666bac6b7830d
ms.openlocfilehash: 0ff83aed4d5e19806a8c69f4b45e39a6156dee7e


---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>VPN-Profile in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Verwenden Sie VPN-Profile in System Center Configuration Manager (auch als ConfigMgr oder SCCM bekannt), um Benutzern in Ihrer Organisation Einstellungen für VPN bereitzustellen. Durch Bereitstellen dieser Einstellungen erleichtern Sie dem Endbenutzer das Verbinden mit Ressourcen im Unternehmensnetzwerk.  

 Sie möchten z. B. allen Geräten, auf denen das iOS-Betriebssystem ausgeführt wird, die Einstellungen zur Verfügung stellen, die zum Verbinden mit einer Dateifreigabe im Unternehmensnetzwerk erforderlich sind. Sie können ein VPN-Profil mit den zum Verbinden mit dem Unternehmensnetzwerk erforderlichen Einstellungen erstellen und dieses Profil dann für alle Benutzer mit Geräten unter iOS in der Hierarchie bereitstellen. Benutzer von iOS-Geräten sehen die VPN-Verbindung in der Liste der verfügbaren Netzwerke und können sich mühelos mit diesem Netzwerk verbinden.  

 Wenn Sie ein VPN-Profil erstellen, können Sie eine Vielzahl von Sicherheitseinstellungen aufnehmen, darunter auch Zertifikate für die Serverüberprüfung und Clientauthentifizierung, die mit System Center Configuration Manager-Zertifikatprofilen bereitgestellt wurden. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

 In diesem Abschnitt wird erklärt, welche Geräte Sie mit VPN-Profilen konfigurieren können, wenn Sie Configuration Manager oder Configuration Manager mit Microsoft Intune verwenden.  

## <a name="vpn-profiles-when-using-configuration-manager"></a>VPN-Profile bei der Verwendung von Configuration Manager  
 Die folgende Tabelle beschreibt die VPN-Profile, die Sie für verschiedene Geräteplattformen konfigurieren können.  

|Verbindungstyp|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|Nein|Nein|Nein|Nein|  
|**Pulse Secure**|Ja|Nein|Ja|Ja|  
|**F5 Edge Client**|Ja|Nein|Ja|Ja|  
|**Dell SonicWALL Mobile Connect**|Ja|Nein|Ja|Ja|  
|**Prüfpunkt für mobiles VPN**|Ja|Nein|Ja|Ja|  
|**Microsoft SSL (SSTP)**|Ja|Ja|Ja|Nein|  
|**Microsoft Automatic**|Ja|Ja|Ja|Nein|  
|**IKEv2**|Ja|Ja|Ja|Nein|  
|**PPTP**|Ja|Ja|Ja|Nein|  
|**L2TP**|Ja|Ja|Ja|Nein|  

## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>VPN-Profile bei der Verwendung von Configuration Manager mit Intune  
 Um Profile für Android-, iOS-, Windows Phone- und Windows 8.1-Geräte bereitzustellen, müssen diese Geräte bei Microsoft Intune registriert werden. Geräte auf anderen Plattformen können ebenfalls bei Intune registriert werden. Informationen zum Registrieren finden Sie unter [Verwalten von Geräten für die Verwaltung in Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx). Diese Tabelle zeigt, welcher Verbindungstyp für jede Geräteplattform unterstützt wird:  

|Verbindungstyp|iOS und Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop und Mobile|  
|---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
|Cisco AnyConnect|Ja|Ja|Nein|Nein|Nein|Nein|Ja (OMA-URI)|  
|Pulse Secure|Ja|Ja|Ja|Nein|Ja|Ja|Ja|  
|F5 Edge Client|Ja|Ja|Ja|Nein|Ja|Ja|Ja|  
|Dell SonicWALL Mobile Connect|Ja|Ja|Ja|Nein|Ja|Ja|Ja|  
|Prüfpunkt für mobiles VPN|Ja|Ja|Ja|Nein|Ja|Ja|Ja|  
|Microsoft SSL (SSTP)|Nein|Nein|Ja|Ja|Ja|Nein|Nein|  
|Microsoft Automatic|Nein|Nein|Ja|Ja|Ja|Nein|Ja (OMA-URI)|  
|IKEv2|Ja (Benutzerdefinierte Richtlinie)|Nein|Ja|Ja|Ja|Ja|Ja (OMA-URI)|  
|PPTP|Ja|Nein|Ja|Ja|Ja|Nein|Ja (OMA-URI)|  
|L2TP|Ja|Nein|Ja|Ja|Ja|Nein|Ja (OMA-URI)|  

### <a name="next-steps"></a>Nächste Schritte  
 Die folgenden Themen helfen Ihnen beim Planen, Konfigurieren, Betreiben und Warten von VPN-Profilen in Configuration Manager.  

-   [Prerequisites for VPN profiles in System Center Configuration Manager (Voraussetzungen für VPN-Profile in System Center Configuration Manager)](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Security and privacy for VPN profiles in System Center Configuration Manager (Sicherheit und Datenschutz für VPN-Profile in System Center Configuration Manager)](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)



<!--HONumber=Dec16_HO3-->


