---
title: VPN-Profile
titleSuffix: Configuration Manager
description: So verwenden Sie VPN-Profile in System Center Configuration Manager, um Benutzern in Ihrer Organisation Einstellungen für VPN bereitzustellen.
ms.custom: na
ms.date: 04/10/2018
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
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d30e7cc834f1693f2cbcf2db840d650421062a19
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>VPN-Profile in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

<!--1283610-->
Verwenden Sie VPN-Profile in Configuration Manager, um Benutzern in Ihrer Organisation Einstellungen für VPN bereitzustellen. Durch Bereitstellen dieser Einstellungen erleichtern Sie dem Endbenutzer das Verbinden mit Ressourcen im Unternehmensnetzwerk.  

 Möglicherweise möchten Sie z.B. alle Windows 10-Geräte mit den Einstellungen konfigurieren, die zum Verbinden mit einer Dateifreigabe im Unternehmensnetzwerk erforderlich sind. Sie können ein VPN-Profil mit den Einstellungen erstellen, die zum Herstellen einer Verbindung mit dem Unternehmensnetzwerk erforderlich sind. Stellen Sie dieses Profil anschließend für alle Benutzer bereit, die über Windows 10-Geräte verfügen. Diese Benutzer sehen die VPN-Verbindung in der Liste der verfügbaren Netzwerke und können mit geringem Aufwand eine Verbindung herstellen.  

 Wenn Sie ein VPN-Profil erstellen, können Sie eine Vielzahl von Sicherheitseinstellungen einrichten. Zu diesen Einstellungen gehören Zertifikate für die Serverüberprüfung und die Clientauthentifizierung, die mithilfe von Configuration Manager-Zertifikatprofilen bereitgestellt wurden. Weitere Informationen finden Sie unter [Zertifikatprofile](introduction-to-certificate-profiles.md).  

> [!Note]  
> Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden können. Weitere Informationen finden Sie unter [Aktivieren optionaler Features von Updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


 Unter [VPN profiles on mobile devices (VPN-Profile auf mobilen Geräten)](/sccm/mdm/deploy-use/create-vpn-profiles) finden Sie Informationen dazu, wie Sie Geräte überprüfen, die Sie unter Verwendung von Configuration Manager mit Microsoft Intune konfigurieren können.  

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

### <a name="next-steps"></a>Nächste Schritte  
 Die folgenden Themen helfen Ihnen beim Planen, Konfigurieren, Betreiben und Warten von VPN-Profilen in Configuration Manager.  

-   [Prerequisites for VPN profiles in System Center Configuration Manager (Voraussetzungen für VPN-Profile in System Center Configuration Manager)](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Security and privacy for VPN profiles in System Center Configuration Manager (Sicherheit und Datenschutz für VPN-Profile in System Center Configuration Manager)](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
