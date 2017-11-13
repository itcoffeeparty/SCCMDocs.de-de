---
title: "Installieren und Zuweisen des Clients über das Internet"
titleSuffix: Configuration Manager
description: "Führen Sie die Installation und Konfiguration des System Center Configuration Manager-Clients über das Internet durch."
ms.custom: na
ms.date: 8/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: "14"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 2ef7580f94864094e9420eb0f5a5c5b4dc9d6d24
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/12/2017
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Installieren und Zuweisen von Configuration Manager-Windows 10-Clients über das Internet mit Authentifizierung über Azure AD

Für die folgenden Szenarios können Sie die Configuration Manager-Clouddienste mit Azure AD nutzen:

- Manuelles Herunterladen des Configuration Manager-Clients aus dem Internet, Installieren auf Windows 10-Geräten und anschließende Zuweisung zu einem Configuration Manager-Standort. Hierfür wird die Standortsystemrolle „Cloud Management Gateway“ benötigt.
- Verwenden Sie Azure AD, um Clients für den Zugriff auf Ihre Configuration Manager-Standorte zu authentifizieren. Dadurch müssen Sie keine Clientauthentifizierungszertifikate mehr konfigurieren.
- Azure AD-Benutzer an Ihrem Standort ermitteln, um sie in Sammlungen und andere Configuration Manager-Vorgänge einzubeziehen.

Führen Sie dazu die folgenden Schritte aus:

- **Schritt 1: Einrichten der Azure-Dienste-App in Configuration Manager Cloud Services und Konfigurieren der Azure AD-Benutzerermittlung**
- **Schritt 2: Einrichten des Cloud Management Gateways** (optional für lokale Clients)
- **Schritt 3: Konfigurieren von Clienteinstellungen zum Verknüpfen von Windows 10-Geräten mit Azure AD und zum Aktivieren von Clients zur Verwendung des Cloud Management Gateways**
- **Schritt 4: Installieren und registrieren des Configuration Manager-Client mithilfe der Azure Active Directory-Identität**


## <a name="before-you-start"></a>Vorbereitung

- Sie benötigen einen Azure AD-Mandanten.
- Ihre Geräte müssen Windows 10 ausführen, mit Azure AD verknüpft und mit einer Azure AD-Identität angemeldet sein. Clients können zusätzlich zu Azure AD auch einer Domäne beitreten.
- Zusätzlich zum Erfüllen der [geltenden Voraussetzungen](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) für die Standortsystemrolle „Verwaltungspunkt“ müssen Sie außerdem sicherstellen, dass **ASP.NET 4.5** (und alle anderen Optionen, die automatisch ausgewählt werden) auf dem Computer aktiviert sind, der diese Standortsystemrolle hostet.
- So stellen Sie den Client mithilfe von Configuration Manager bereit
    - Konfigurieren Sie mindestens einen Verwaltungspunkt für den HTTPS-Modus, wenn Sie Azure AD anstelle von Clientzertifikaten zum Authentifizieren verwenden möchten.
        Wenn Sie Clientzertifikate anstelle des Cloud Management Gateways verwenden, ist ein HTTPS-Verwaltungspunkt optional, wird jedoch empfohlen. Wenn Sie Azure AD zur Authentifizierung verwenden, ob für lokale oder Internetclients, ist der HTTPS-Verwaltungspunkt erforderlich.
    - Richten Sie ein Cloud Management Gateway ein, wenn Sie Internetclients bereitstellen möchten. Für lokale Clients, die Sie mit Azure AD authentifizieren, müssen Sie das Cloud Management Gateway nicht konfigurieren.


## <a name="step-1-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Schritt 1: Einrichten der Azure-Dienste-App in Configuration Manager Cloud Services

Hiermit wird Ihr Configuration Manager-Standort mit Azure AD verbunden, was eine Voraussetzung für alle anderen Vorgänge in diesem Abschnitt ist. 

Die Benutzerermittlung in Azure AD wird als Teil der *Cloudverwaltung* konfiguriert. Das entsprechende Verfahren hierfür finden Sie in Schritt **6** unter [Erstellen der Azure-Web-App für die Verwendung mit Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) im Thema *Konfigurieren von Azure-Diensten für die Verwendung mit Configuration Manager*.
    
Nach dem Abschluss dieses Verfahrens ist Ihr Configuration Manager-Standort mit Azure AD verbunden. 

## <a name="step-2-set-up-the-cloud-management-gateway"></a>Schritt 2: Einrichten des Cloud Management Gateways

Richten Sie das Cloud Management Gateway ein, um die in diesem Thema beschriebenen Cloudverwaltungsszenarien zu ermöglichen. Hilfe finden Sie in den folgenden Themen: 

- [Planen des Cloud Management Gateways in Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway)
- [Einrichten des Cloud Management Gateways für Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway)
- [Überwachen des Cloud Management Gateways in Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway)

## <a name="step-3-configure-client-settings-to-join-windows-10-devices-with-azure-ad-and-enable-clients-to-use-the-cloud-management-gateway"></a>Schritt 3: Konfigurieren von Clienteinstellungen zum Verknüpfen von Windows 10-Geräten mit Azure AD und zum Aktivieren von Clients zur Verwendung des Cloud Management Gateways

1.  Konfigurieren Sie die folgenden Clienteinstellungen im Abschnitt **Cloud Services** anhand der Informationen in [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](/sccm/core/clients/deploy/configure-client-settings).
    - **Zugriff auf Cloudverteilungspunkt zulassen**: Aktivieren Sie diese Einstellung, um internetbasierte Geräte beim Abrufen des zur Installation des Configuration Manager-Clients erforderlichen Inhalts zu unterstützen. Wenn der Inhalt nicht auf dem Cloudverteilungspunkt verfügbar ist, können Geräte den Inhalt von einem Verwaltungspunkt abrufen, der mit dem Cloud Management Gateway verbunden ist.
    - **Automatische Registrierung neuer einer Windows 10-Domäne beigetretener Geräte mit Azure Active Directory**: Legen Sie diese Option auf **Ja** (Standard) oder **Nein** fest.
    - **Clients die Verwendung eines Cloudverwaltungsgateways ermöglichen**: Legen Sie diese Option auf **Ja** (Standard) oder **Nein** fest.
2.  Stellen Sie die Clienteinstellungen in der gewünschten Sammlung von Geräten bereit. Stellen Sie diese Einstellungen nicht für Benutzersammlungen bereit.

Um zu bestätigen, dass das Gerät Azure AD beigetreten ist, führen Sie in einem Eingabeaufforderungsfenster **dsregcmd.exe /status** aus. Im Feld **AzureAdjoined** in den Ergebnissen wird **YES** angezeigt, wenn das Gerät in Azure AD eingebunden ist.


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>Schritt 4: Installieren und registrieren des Configuration Manager-Client mithilfe der Azure Active Directory-Identität

Folgen Sie anschließend zum Installieren des Clients der Anleitung unter [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually), und verwenden Sie die Befehlszeile für die Installation: 

**ccmsetup.exe /mp&#58; https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=DFD SMSMP=https://SCCMDFPSS.contoso.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011DB47 AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d17026 AADRESOURCEURI=https://contososerver**

- **/MP**: Quelle herunterladen. Kann bei Bootstrap aus dem Internet auf CMG festgelegt werden.
- **CCMHOSTNAME**: Name des Internetverwaltungspunkts Sie finden diese Informationen, indem Sie **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** an einer Eingabeaufforderung auf einem verwalteten Client ausführen.
- **SMSSiteCode**: Standortcode Ihres Configuration Manager-Standorts
- **SMSMP**: Name des anfänglichen Verwaltungspunkts. Dieser kann sich in Ihrem Intranet befinden.
- **AADTENANTID**, **AADTENANTNAME**: ID und Name des Azure AD-Mandanten, den Sie mit Configuration Manager verknüpft haben Diese Informationen können Sie herausfinden, indem Sie auf einem Azure AD beigetretenen Gerät „dsregcmd.exe /status“ an einer Eingabeaufforderung ausführen.
- **AADCLIENTAPPID**: Die Azure AD-Client-App-ID Hilfe zum Ermitteln dieses Werts finden Sie unter [Erstellen einer Azure Active Directory-Anwendung und eines Dienstprinzipals mit Ressourcenzugriff mithilfe des Portals](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri**: Der Bezeichner-URI der eingebundenen Azure AD-Server-App. Weitere Informationen siehe [Konfigurieren von Azure-Diensten zur Verwendung mit dem Configuration Manager](/sccm/core/servers/deploy/configure/azure-services-wizard).




## <a name="next-steps"></a>Nächste Schritte

Lesen Sie nach dem Abschluss dieser Schritte den Artikel [Überwachen von Clients in System Center Configuration Manager](/sccm/core/clients/manage/monitor-clients).
