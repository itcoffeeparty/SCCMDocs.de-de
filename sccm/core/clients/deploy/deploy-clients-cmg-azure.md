---
title: Installieren von Clients mit Azure AD
titleSuffix: Configuration Manager
description: Installieren und Zuweisen von Configuration Manager-Clients auf Windows 10-Geräten mithilfe von Azure Active Directory zur Authentifizierung
ms.custom: na
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: 14
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 12fc1b394ae98c2b384630f4a00e4239e4e8d9d6
ms.sourcegitcommit: aed99ba3c5e9482199cb3fc5c92f6f3a160cb181
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Installieren und Zuweisen von Configuration Manager-Windows 10-Clients über das Internet mit Authentifizierung über Azure AD

Wenn Sie Configuration Manager-Clients auf Windows 10-Geräten mit Azure AD zur Authentifizierung installieren möchten, müssen Sie Configuration Manager in Azure Active Directory (Azure AD) integrieren. Clients können im Intranet direkt mit einem HTTPS-fähigen Verwaltungspunkt kommunizieren. Des Weiteren können sie auch internetbasiert sein und über das CMG (cloud management gateway, Cloudverwaltungsgateway) oder mit einem internetbasierten Verwaltungspunkt kommunizieren. Für diesen Prozess wird Azure AD zur Authentifizierung von Clients bei dem Configuration Manager-Standort verwendet. Dadurch müssen Sie keine Clientauthentifizierungszertifikate mehr konfigurieren.



## <a name="before-you-begin"></a>Vorbereitung

- Voraussetzung ist ein Azure AD-Mandant.  

- Geräteanforderungen:  

    - Windows 10  

    - Einbindung in Azure AD (einfache Einbindung in Clouddomäne oder Einbindung in Hybrid-Azure AD)  

- Benutzeranforderungen:  

    - Der angemeldete Benutzer muss eine Azure AD-Identität sein.   

    - Wenn der Benutzer eine Verbundsidentität oder synchronisierte Identität ist, müssen Sie in Configuration Manager die [Active Directory-Benutzerermittlung](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) und die [Azure AD-Benutzerermittlung](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc) verwenden. Weitere Informationen zu Hybrididentitäten finden Sie unter [Define a hybrid identity adoption strategy (Festlegen einer Strategie zur Einführung von Hybrididentitäten)](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- Zusätzlich zu den [erforderlichen Komponenten](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq) für die Standortsystemrolle des Verwaltungspunkts müssen Sie auch **ASP.NET 4.5** auf diesem Server installieren. Bei der Aktivierung von ASP.NET 4.5 werden weitere Optionen automatisch ausgewählt, die Sie ebenfalls verwenden müssen.  

- Konfigurieren Sie alle Verwaltungspunkte für den HTTPS-Modus. Weitere Informationen finden Sie unter [PKI-Zertifikatanforderungen](/sccm/core/plan-design/network/pki-certificate-requirements) und [Deploy the web server certificate for site systems that run IIS (Bereitstellen des Webserverzertifikats für Standortsysteme, auf denen IIS ausgeführt wird)](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  
    - Wenn Sie das CMG verwenden, müssen Sie nur HTTPS für Verwaltungspunkte konfigurieren, die Sie für das CMG aktivieren.
    - Wenn Sie Clients mithilfe von tokenbasierter Authentifizierung von Azure AD im Intranet bereitstellen, müssen alle Verwaltungspunkte, die diese Clients möglicherweise kontaktieren, für HTTPS aktiviert sein. 

- Richten Sie optional ein [CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) ein, um internetbasierte Clients bereitzustellen. Für lokale Clients, die sich bei Azure AD authentifizieren, ist kein CMG erforderlich.  


## <a name="configure-azure-services-for-cloud-management"></a>Konfigurieren von Azure-Diensten für die Cloudverwaltung

Verbinden Sie zuerst Ihren Configuration Manager-Standort mit Azure AD. Weiter Informationen hierzu finden Sie unter [Konfigurieren von Azure-Diensten](/sccm/core/servers/deploy/configure/azure-services-wizard). Stellen Sie eine Verbindung mit dem **Cloudverwaltungsdienst** her.

Aktivieren Sie die [Azure AD-Benutzerermittlung](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc) während des Onboardings für die **Cloudverwaltung**. 

Nachdem Sie diese Aktionen ausgeführt haben, wird Ihr Configuration Manager-Standort mit Azure AD verbunden. 



## <a name="configure-client-settings"></a>Konfigurieren von Clienteinstellungen

Die folgenden Clienteinstellungen unterstützen das Einbinden von Windows 10-Geräten in Azure AD. Außerdem können damit internetbasierte Clients das CMG und den Cloudverteilungspunkt verwenden.

1.  Konfigurieren Sie die folgenden Clienteinstellungen im Abschnitt **Clouddienste** anhand der Informationen in [Konfigurieren von Clienteinstellungen](/sccm/core/clients/deploy/configure-client-settings).  

    - **Zugriff auf Cloudverteilungspunkt zulassen**: Aktivieren Sie diese Einstellung, um internetbasierte Geräte beim Abrufen des zur Installation des Configuration Manager-Clients erforderlichen Inhalts zu unterstützen. Wenn am Cloudverteilungspunkt der Inhalt nicht verfügbar ist, können Geräte diesen über das CMG abrufen. Der Bootstrap für die Clientinstallation sendet vier Stunden lang wiederholt Anforderungen an den Cloudverteilungspunkt, bevor das CMG als Ausweichlösung verwendet wird.<!--495533-->  

    - **Registrieren Sie neue, in die Domäne eingebundene Windows 10-Geräte automatisch bei Azure Active Directory**: Legen Sie diese Option auf **Ja** oder **Nein** fest. Der Standardwert für diese Einstellung ist **Ja**. Dieses Verhalten ist auch die Standardeinstellung in Version 1709 von Windows 10.

    - **Clients die Verwendung eines Cloudverwaltungsgateways ermöglichen**: Legen Sie diese Option auf **Ja** (Standard) oder **Nein** fest.  

2.  Stellen Sie die Clienteinstellungen in der gewünschten Sammlung von Geräten bereit. Stellen Sie diese Einstellungen nicht für Benutzersammlungen bereit.

Um zu bestätigen, dass das Gerät in Azure AD eingebunden wurde, müssen Sie `dsregcmd.exe /status` mit der Eingabeaufforderung ausführen. Im Feld **AzureAdjoined** wird in den Ergebnissen **JA** angezeigt, wenn das Gerät in Azure AD eingebunden ist.



## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Installieren und Registrieren des Clients mithilfe einer Azure AD-Identität

Wenn Sie den Client mithilfe einer Azure AD-Identität manuell installieren möchten, ist es zuerst erforderlich, dass Sie sich mit der allgemeinen Vorgehensweise unter [Manuelles Installieren von Clients](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual) vertraut machen. 

 > [!Note]  
 > Das Gerät benötigt zwar Zugriff auf das Internet, um Azure AD kontaktieren zu können, muss aber nicht internetbasiert sein. 

Im folgenden Beispiel wird die allgemeine Syntax für den Befehl demonstriert, der mit der Befehlszeile ausgeführt wird: `ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften](/sccm/core/clients/deploy/about-client-installation-properties).

Die Eigenschaften „/mp“ und „CCMHOSTNAME“ legen je nach Szenario die Eigenschaften eines der folgenden Punkte fest:
- Lokaler Verwaltungspunkt: Geben Sie nur die Eigenschaft „/mp“ an. Die Angabe von „CCMHOSTNAME“ ist nicht erforderlich.
- Cloudverwaltungsgateway
- Internetbasierter Verwaltungspunkt: Die Eigenschaft „SMSMP“ legt entweder den lokalen oder internetbasierten Verwaltungspunkt fest.

Im folgenden Beispiel wird ein Cloudverwaltungsgateway verwendet. Darin werden die Beispielwerte für jede Eigenschaft ersetzt: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Wenn Sie die Clientinstallation mithilfe einer Azure AD-Identität über Microsoft Intune automatisieren möchten, finden Sie unter [Vorbereiten von Windows 10-Geräten für die Co-Verwaltung](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client) weitere Informationen.



## <a name="next-steps"></a>Nächste Schritte

Lesen Sie nach dem Abschluss dieser Schritte den Artikel [Überwachen von Clients in System Center Configuration Manager](/sccm/core/clients/manage/monitor-clients).
