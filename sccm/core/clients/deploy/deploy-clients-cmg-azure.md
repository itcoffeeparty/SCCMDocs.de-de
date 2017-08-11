---
title: "Installieren und Zuweisen des Clients über das Internet | Microsoft-Dokumentation"
description: "Führen Sie die Installation und Konfiguration des System Center Configuration Manager-Clients über das Internet durch."
ms.custom: na
ms.date: 7/31/2017
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
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: f604557d208b2dda9dc1c6b4c4d27d896d47695e
ms.contentlocale: de-de
ms.lasthandoff: 07/29/2017

---

# <a name="install-and-assign-configuration-manager-clients-from-the-internet-using-azure-ad-for-authentication"></a>Installieren und Zuweisen von Configuration Manager-Clients über das Internet mit Authentifizierung über Azure AD

Für die folgenden Szenarios können Sie die Configuration Manager-Clouddienste mit Azure AD nutzen:

- Manuelles Herunterladen und Installieren des Configuration Manager-Client aus dem Internet und anschließende Zuweisung zu einem Configuration Manager-Standort. Hierfür wird die Standortsystemrolle „Cloud Management Gateway“ benötigt.
- Azure AD verwenden, um Clients über das Internet für den Zugriff auf Ihre Configuration Manager-Standorte zu authentifizieren. Dadurch müssen Sie keine Clientauthentifizierungszertifikate mehr konfigurieren.
- Azure AD-Benutzer an Ihrem Standort ermitteln, um sie in Sammlungen und andere Configuration Manager-Vorgänge einzubeziehen.

Führen Sie dazu die folgenden Schritte aus:

- **Schritt 1: Einrichten von Cloud Management Gateway**
- **Schritt 2: Einrichten der Azure-Dienste-App in Configuration Manager-Clouddiensten**
- **Schritt 3: Konfigurieren der Clienteinstellungen, um Windows 10-Geräte mit Azure AD zu registrieren**
- **Schritt 4: Installieren und registrieren des Configuration Manager-Client mithilfe der Azure Active Directory-Identität**


## <a name="before-you-start"></a>Vorbereitung

- Sie benötigen einen Azure AD-Mandanten.
- Auf Ihren Geräten, die in Azure AD eingebunden sein müssen, muss Windows 10 ausgeführt werden. Clients können zusätzlich zu Azure AD auch einer Domäne beitreten.
- Zusätzlich zum Erfüllen der [geltenden Voraussetzungen](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) für die Standortsystemrolle „Verwaltungspunkt“ müssen Sie außerdem sicherstellen, dass **ASP.NET 4.5** (und alle anderen Optionen, die automatisch ausgewählt werden) auf dem Computer aktiviert sind, der diese Standortsystemrolle hostet.
- So stellen Sie den Client mithilfe von Configuration Manager bereit
    - Konfigurieren Sie mindestens einen Verwaltungspunkt für den HTTPS-Modus.
    - Richten Sie Cloud Management Gateway ein.

## <a name="step-1-set-up-the-cloud-management-gateway"></a>Schritt 1: Einrichten von Cloud Management Gateway

Richten Sie das Cloud Management Gateway ein, damit Clients ohne Zertifikate im Internet auf Ihren Configuration Manager-Standort zugreifen können. Hilfe finden Sie in den folgenden Themen: 

- [Planen des Cloud Management Gateways in Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway)
- [Einrichten des Cloud Management Gateways für Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway)
- [Überwachen des Cloud Management Gateways in Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway)

## <a name="step-2-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Schritt 2: Einrichten der Azure-Dienste-App in Configuration Manager Cloud Services

Hiermit wird Ihr Configuration Manager-Standort mit Azure AD verbunden, was eine Voraussetzung für alle anderen Vorgänge in diesem Abschnitt ist. 

Die Benutzerermittlung in Azure AD wird als Teil der *Cloudverwaltung* konfiguriert. Das entsprechende Verfahren hierfür finden Sie in Schritt **6** unter [Erstellen der Azure-Web-App für die Verwendung mit Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) im Thema *Konfigurieren von Azure-Diensten für die Verwendung mit Configuration Manager*.
    
Nach dem Abschluss dieses Verfahrens ist Ihr Configuration Manager-Standort mit Azure AD verbunden. 

## <a name="step-3-configure-client-settings-to-register-windows-10-devices-with-azure-ad"></a>Schritt 3: Konfigurieren der Clienteinstellungen, um Windows 10-Geräte mit Azure AD zu registrieren

1.  Konfigurieren Sie die folgenden Clienteinstellungen im Abschnitt „Clouddienste“ anhand der Informationen in [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](/sccm/core/clients/deploy/configure-client-settings).
    - **Automatische Registrierung neuer einer Windows 10-Domäne beigetretener Geräte mit Azure Active Directory**: Legen Sie diese Option auf **Ja** (Standard) oder **Nein** fest.
    - **Clients die Verwendung eines Cloudverwaltungsgateways ermöglichen**: Legen Sie diese Option auf **Ja** (Standard) oder **Nein** fest.
2.  Stellen Sie die Clienteinstellungen in der gewünschten Sammlung von Geräten bereit.

Um zu bestätigen, dass das Gerät Azure AD beigetreten ist, führen Sie in einem Eingabeaufforderungsfenster **dsregcmd.exe /status** aus. Im Feld **AzureAdjoined** in den Ergebnissen wird **YES** angezeigt, wenn das Gerät in Azure AD eingebunden ist.


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>Schritt 4: Installieren und registrieren des Configuration Manager-Client mithilfe der Azure Active Directory-Identität

Bevor Sie beginnen, stellen Sie sicher, dass die Quelldateien für die Clientinstallation lokal auf dem Gerät gespeichert sind, auf dem der Client installiert werden soll. Folgen Sie anschließend der Anleitung unter [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) und verwenden Sie die Befehlszeile für die Installation: 

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso AADCLIENTAPPID= AADRESOURCEURI=https://contososerver**

- **/NoCrlCheck:**: Wenn Ihr Verwaltungspunkt oder Cloud Management Gateway ein nicht öffentliches Serverzertifikat verwendet, kann der Client ggf. nicht auf den Speicherort der Zertifikatsperrliste zugreifen.
- **/Source**: Lokaler Ordner: Speicherort der Clientinstallationsdateien
- **CCMHOSTNAME**: Name des Internetverwaltungspunkts Sie finden diese Informationen, indem Sie **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** an einer Eingabeaufforderung auf einem verwalteten Client ausführen.
- **SMSMP**: Name des anfänglichen Verwaltungspunkts. Dieser kann sich in Ihrem Intranet befinden.
- **SMSSiteCode**: Standortcode Ihres Configuration Manager-Standorts
- **AADTENANTID**, **AADTENANTNAME**: ID und Name des Azure AD-Mandanten, den Sie mit Configuration Manager verknüpft haben Diese Informationen können Sie herausfinden, indem Sie auf einem Azure AD beigetretenen Gerät „dsregcmd.exe /status“ an einer Eingabeaufforderung ausführen.
- **AADCLIENTAPPID**: Die Azure AD-Client-App-ID Hilfe zum Ermitteln dieses Werts finden Sie unter [Erstellen einer Azure Active Directory-Anwendung und eines Dienstprinzipals mit Ressourcenzugriff mithilfe des Portals](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri**: Der Bezeichner-URI der eingebundenen Azure AD-Server-App.


## <a name="next-steps"></a>Nächste Schritte

Lesen Sie nach dem Abschluss dieser Schritte den Artikel [Überwachen von Clients in System Center Configuration Manager](/sccm/core/clients/manage/monitor-clients).

