---
title: Vorbereiten von Windows 10 für die Co-Verwaltung
titleSuffix: Configuration Manager
description: Erfahren Sie, wie sie Windows 10-Geräte für die Co-Verwaltung vorbereiten.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/28/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 93a991cb3fd78e44f5ae4434a9845a57450e1025
ms.sourcegitcommit: e4ca9fb1fad2caaf61bb46e0a12f4d6b96f15513
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Vorbereiten von Windows 10-Geräten für die Co-Verwaltung
Sie können die Co-Verwaltung auf Windows 10-Geräten aktivieren, die in AD und Azure AD eingebunden, bei Microsoft Intune registriert und ein Client in Configuration Manager sind. Installieren Sie den Configuration Manager-Client auf neuen Windows 10- und bereits in Intune registrierten Geräten jedoch vor der Aktivierung der Co-Verwaltung. Windows 10-Geräte, die Configuration Manager-Clients sind, können Sie bei Intune registrieren und die Co-Verwaltung über die Configuration Manager-Konsole aktivieren.

> [!IMPORTANT]
> Co-Verwaltung wird von Windows 10 Mobile-Geräten nicht unterstützt.


## <a name="prerequisites"></a>Erforderliche Komponenten
Bevor Sie mit der Co-Verwaltung beginnen können, müssen folgende Anforderungen erfüllt sein. Zum einen gelten allgemeine Voraussetzungen und zum anderen unterschiedliche Voraussetzungen für Geräte mit installiertem Configuration Manager-Client und für Geräte, auf denen der Client nicht installiert ist.
### <a name="general-prerequisites"></a>Allgemeine Voraussetzungen
Hier finden Sie die allgemeinen Voraussetzungen für die Aktivierung der Co-Verwaltung:  

- Configuration Manager, Version 1710 oder höher
- Azure AD
- EMS- oder Intune-Lizenzen für alle Benutzer
- [Automatische Registrierung bei Azure AD](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) aktiviert
- Intune-Abonnement &#40;die MDM-Autorität muss in Intune auf **Intune** festgelegt sein&#41;


   > [!Note]  
   > In einer hybriden MDM-Umgebung (Intune integriert in Configuration Manager) ist keine Co-Verwaltung möglich. Sie können jedoch mit der Migration von Benutzern zum eigenständigen Intune beginnen und anschließend die zugehörigen Windows 10-Geräte für die Co-Verwaltung aktivieren. Informationen zur Migration zum eigenständigen Intune finden Sie unter [Beginnen der Migration hybrider MDM-Benutzer und -Geräte zum eigenständigen Intune](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).

### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Zusätzliche Anforderungen an Geräte mit dem Configuration Manager-Client
- Windows 10, Version 1709 oder höher
- [In Azure AD eingebundene Hybridgeräte](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (in AD und Azure AD eingebunden)

### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Zusätzliche Anforderungen an Geräte ohne Configuration Manager-Client
- Windows 10, Version 1709 oder höher
- [Cloud Management Gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) in Configuration Manager (wenn Sie den Configuration Manager-Client mit Intune installieren)

> [!IMPORTANT]
> Co-Verwaltung wird von Windows 10 Mobile-Geräten nicht unterstützt.


## <a name="command-line-to-install-configuration-manager-client"></a>Befehlszeile zum Installieren von Configuration Manager-Clients
Erstellen Sie eine App in Intune für Windows 10-Geräte, die noch keine Configuration Manager-Clients sind. Wenn Sie in den nächsten Abschnitten eine App erstellen, verwenden Sie die folgende Befehlszeile:

`ccmsetup.msi CCMSETUPCMD="/mp:<URL of cloud management gateway mutual auth endpoint> CCMHOSTNAME=<URL of cloud management gateway mutual auth endpoint> SMSSiteCode=<Sitecode> SMSMP=https://<FQDN of MP> AADTENANTID=<AAD tenant ID> AADCLIENTAPPID=<Server AppID for AAD Integration> AADRESOURCEURI=https://<Resource ID>"`

Angenommen, Sie haben die folgenden Werte:

- **URL des Cloudverwaltungsgateway-Endpunkts für die gegenseitige Authentifizierung**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    

   >[!Note]    
   >Verwenden Sie den Wert von **MutualAuthPath** in der SQL-Ansicht **vProxy_Roles** als Wert für die **URL des Cloudverwaltungsgateway-Endpunkts für die gegenseitige Authentifizierung**.

- **FQDN des Verwaltungspunkts (Management Point, MP)**: mp1.contoso.com    
- **Standortcode**: PS1    
- **Azure AD-Mandanten-ID**: 60a413f4-c606-4744-8adb-9476ae3XXXXX    
- **Azure AD-Client-App-ID**: 9fb9315f-4c42-405f-8664-ae63283XXXXX     
- **URI der AAD-Ressourcen-ID**: ConfigMgrServer    

  > [!Note]    
  > Verwenden Sie den Wert von **IdentifierUri** aus der SQL-Ansicht **vSMS_AAD_Application_Ex** als Wert für den **URI der AAD-Ressourcen-ID**.

Daraus ergibt sich die folgende Befehlszeile:

`ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=PS1 SMSMP=https://mp1.contoso.com AADTENANTID=60a413f4-c606-4744-8adb-9476ae3XXXXX AADCLIENTAPPID=9fb9315f-4c42-405f-8664-ae63283XXXXX AADRESOURCEURI=https://ConfigMgrServer"`

> [!Tip]
> Die Befehlszeilenparameter für Ihren Standort finden Sie anhand der folgenden Schritte:     
> 1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-management** (Co-Verwaltung).  
> 2. Klicken Sie auf der Registerkarte „Home“ (Startseite) in der Gruppe „Manage“ (Verwalten) auf  **Configure co-management** (Co-Verwaltung konfigurieren), um den Registrierungs-Assistenten für die Co-Verwaltung zu öffnen.    
> 3. Klicken Sie auf der Seite „Subscriptions“ (Abonnement) auf **Sign In** (Anmelden), melden Sie sich bei Ihrem Intune-Mandanten an, und klicken Sie dann auf **Next** (Weiter).    
> 4. Klicken Sie auf der Seite „Enablement“ (Aktivierung) im Abschnitt **Devices enrolled in Intune** (Bei Intune registrierte Geräte) auf **Copy** (Kopieren), um die Befehlszeile in die Zwischenablage zu kopieren. Speichern Sie sie anschließend, um die Befehlszeile bei der Erstellung einer App zu verwenden.  
> 5. Klicken Sie auf **Cancel** (Schließen), um den Assistenten zu beenden.

> [!Important]    
> Wenn Sie die Befehlszeile anpassen, um den Konfigurations-Manager-Client zu installieren, achten Sie darauf, dass die Befehlszeile nicht mehr als 1024 Zeichen umfasst. Wenn die Befehlszeile aus mehr als 1024 Zeichen besteht, schlägt die Clientinstallation fehl.


## <a name="new-windows-10-devices"></a>Neue Windows 10-Geräte
Auf neuen Windows 10-Geräten können Sie mit dem Dienst „AutoPilot“ den Eindruck beim ersten Ausführen konfigurieren, der die Einbindung des Geräts in AD und Azure AD sowie die Registrierung bei Intune umfasst. Erstellen Sie anschließend eine App in Intune, um den Configuration Manager-Client bereitzustellen.  
1. Aktivieren Sie AutoPilot für die neuen Windows 10-Geräte. Weitere Informationen finden Sie unter [Übersicht über Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).    

   > [!NOTE]   
   > Ab Version 1802 können Sie mit Configuration Manager Geräteinformationen erfassen und melden, die vom Microsoft Store für Unternehmen und Bildungseinrichtungen benötigt werden. Zu diesen Informationen gehört die Seriennummer des Geräts, der Windows-Produktbezeichner und eine Hardwarebezeichner. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** nacheinander die Knoten **Berichterstellung** und **Berichte**, und wählen Sie den Knoten **Hardware – allgemein** aus. Führen Sie den neuen Bericht **Windows AutoPilot-Geräteinformationen** aus, und sehen Sie sich die Ergebnisse an. Klicken Sie in der Berichtsanzeige auf das Symbol **Exportieren**, und aktivieren Sie die Option **CSV (Komma-getrennt)**. Nachdem Sie die Datei gespeichert haben, laden Sie die Daten in den Microsoft Store für Unternehmen und Bildungseinrichtungen hoch. Weitere Informationen finden Sie unter [Hinzufügen von Geräten zum Microsoft Store für Unternehmen und Bildungseinrichtungen](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).

2. Konfigurieren Sie die automatische Registrierung in Azure AD für Ihre Geräte, damit sie automatisch in Intune registriert werden. Weitere Informationen finden Sie unter  [Windows-Geräte registrieren](https://docs.microsoft.com/intune/windows-enroll).
3. Erstellen Sie eine App in Intune mit dem Configuration Manager-Clientpaket, und stellen Sie die App für Windows 10-Geräte bereit, die Sie co-verwalten möchten. Verwenden Sie die [Befehlszeile, um den Configuration Manager-Client zu installieren](#command-line-to-install-configuration-manager-client), während Sie die Schritte zum [Installieren von Clients über das Internet mithilfe von Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure) ausführen.   

## <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Nicht in Intune oder einem Configuration Manager-Client registrierte Windows 10-Geräte
Windows 10-Geräte, die nicht in Intune registriert sind oder den Configuration Manager-Client haben, können Sie automatisch bei Intune registrieren. Erstellen Sie anschließend eine App in Intune, um den Configuration Manager-Client bereitzustellen.
1. Konfigurieren Sie die automatische Registrierung in Azure AD für Ihre Geräte, damit sie automatisch in Intune registriert werden. Weitere Informationen finden Sie unter  [Windows-Geräte registrieren](https://docs.microsoft.com/intune/windows-enroll).  
2. Erstellen Sie eine App in Intune mit dem Configuration Manager-Clientpaket, und stellen Sie die App für Windows 10-Geräte bereit, die Sie co-verwalten möchten. Verwenden Sie die [Befehlszeile, um den Configuration Manager-Client zu installieren](#command-line-to-install-configuration-manager-client), während Sie die Schritte zum [Installieren von Clients über das Internet mithilfe von Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure) ausführen.

## <a name="windows-10-devices-enrolled-in-intune"></a>Bei Intune registrierte Windows 10-Geräte
Erstellen Sie für Windows 10-Geräte, die bereits bei Intune registriert sind, eine App in Intune, um den Configuration Manager-Client bereitzustellen. Verwenden Sie die [Befehlszeile, um den Configuration Manager-Client zu installieren](#command-line-to-install-configuration-manager-client), während Sie die Schritte zum [Installieren von Clients über das Internet mithilfe von Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure) ausführen.  

## <a name="next-steps"></a>Nächste Schritte
[Verschieben von Configuration Manager-Workloads zu Intune](co-management-switch-workloads.md)