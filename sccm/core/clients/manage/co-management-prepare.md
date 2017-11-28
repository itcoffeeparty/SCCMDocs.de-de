---
title: "Vorbereiten von Windows 10-Geräten für die Co-Verwaltung"
description: "Erfahren Sie, wie sie Windows 10-Geräte für die Co-Verwaltung vorbereiten."
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: b336b56cc34119a4acec8e798b8c59970f5c7dbf
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Vorbereiten von Windows 10-Geräten für die Co-Verwaltung
Sie können die Co-Verwaltung auf Windows 10-Geräten aktivieren, die in AD und Azure AD eingebunden, bei Intune registriert und ein Client in Configuration Manager sind. Installieren Sie den Configuration Manager-Client auf neuen Windows 10- und bereits in Intune registrierten Geräten jedoch vor der Aktivierung der Co-Verwaltung. Windows 10-Geräte, die Configuration Manager-Clients sind, können Sie bei Intune registrieren und die Co-Verwaltung über die Configuration Manager-Konsole aktivieren.

## <a name="command-line-to-install-configuration-manager-client"></a>Befehlszeile zum Installieren von Configuration Manager-Clients
Sie müssen in Intune eine App für Windows 10-Geräte erstellen, die noch keine Configuration Manager-Clients sind. Wenn Sie in den nächsten Abschnitten eine App erstellen, verwenden Sie die folgende Befehlszeile:

```ccmsetup.msi CCMSETUPCMD="/mp:&#60;*URL of cloud management gateway mutual auth endpoint*&#62;/ CCMHOSTNAME=&#60;*URL of cloud management gateway mutual auth endpoint*&#62; SMSSiteCode=&#60;*Sitecode*&#62; SMSMP=https:&#47;/&#60;*FQDN of MP*&#62; AADTENANTID=&#60;*AAD tenant ID*&#62; AADTENANTNAME=&#60;*Tenant name*&#62; AADCLIENTAPPID=&#60;*Server AppID for AAD Integration*&#62; AADRESOURCEURI=https:&#47;/&#60;*Resource ID*&#62;”```

Angenommen, Sie haben die folgenden Werte:

- **URL des Cloudverwaltungsgateway-Endpunkts für die gegenseitige Authentifizierung**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Verwenden Sie den Wert von **MutualAuthPath** in der SQL-Ansicht **vProxy_Roles** als Wert für die **URL des Cloudverwaltungsgateway-Endpunkts für die gegenseitige Authentifizierung**.

- **FQDN des Verwaltungspunkts (Management Point, MP)**: sccmmp.corp.contoso.com    
- **Standortcode**: PS1    
- **Azure AD-Mandanten-ID**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Name des Azure AD-Mandanten**: contoso    
- **ID der Azure AD-Client-App**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **URI der AAD-Ressourcen-ID**: ConfigMgrServer    

  > [!Note]    
  > Verwenden Sie den Wert von **IdentifierUri** aus der SQL-Ansicht **vSMS_AAD_Application_Ex** als Wert für den **URI der AAD-Ressourcen-ID**.

Daraus ergibt sich die folgende Befehlszeile:

```ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer”```

> [!Tip]
>Die Befehlszeilenparameter für Ihren Standort finden Sie anhand der folgenden Schritte:     
> 1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-management** (Co-Verwaltung).  
> 2. Klicken Sie auf der Registerkarte „Home“ (Startseite) in der Gruppe „Manage“ (Verwalten) auf  **Configure co-management** (Co-Verwaltung konfigurieren), um den Registrierungs-Assistenten für die Co-Verwaltung zu öffnen.    
> 3. Klicken Sie auf der Seite „Subscriptions“ (Abonnement) auf **Sign In** (Anmelden), melden Sie sich bei Ihrem Intune-Mandanten an, und klicken Sie dann auf **Next** (Weiter).    
> 4. Klicken Sie auf der Seite „Enablement“ (Aktivierung) im Abschnitt **Devices enrolled in Intune** (Bei Intune registrierte Geräte) auf **Copy** (Kopieren), um die Befehlszeile in die Zwischenablage zu kopieren. Speichern Sie sie anschließend, um die Befehlszeile bei der Erstellung einer App zu verwenden.  
> 5. Klicken Sie auf **Cancel** (Schließen), um den Assistenten zu beenden.

## <a name="new-windows-10-devices"></a>Neue Windows 10-Geräte
Auf neuen Windows 10-Geräten können Sie mit dem Dienst „AutoPilot“ den Eindruck beim ersten Ausführen konfigurieren, der die Einbindung des Geräts in AD und Azure AD sowie die Registrierung bei Intune umfasst. Erstellen Sie anschließend eine App in Intune, um den Configuration Manager-Client bereitzustellen.  
1. Aktivieren Sie AutoPilot für die neuen Windows 10-Geräte. Weitere Informationen finden Sie unter [Übersicht über Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
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