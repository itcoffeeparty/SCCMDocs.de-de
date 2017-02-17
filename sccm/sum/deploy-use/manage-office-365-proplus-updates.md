---
title: Verwalten von Office 365 ProPlus-Updates | Microsoft-Dokumentation
description: "Configuration Manager synchronisiert Office 365-Clientupdates aus dem WSUS-Katalog auf den Standortserver, um Updates zur Bereitstellung für den Client zur Verfügung zu stellen."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 01/04/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 6bb2bf0a029bc21e9420ac0ba782e8ea21291896
ms.openlocfilehash: df9ad09c4ce0c2a18ee012cd3ace7b1a850df7b4

---

# <a name="manage-office-365-proplus-updates-with-configuration-manager"></a>Verwalten von Office 365 ProPlus-Updates mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab Configuration Manager-Version 1602 kann Configuration Manager die Office 365-Clientupdates mithilfe des Workflow bei der Softwareupdateverwaltung verwalten. Wenn Microsoft ein neues Update für Office 365-Clients im Office Content Delivery Network (CDN) veröffentlicht, veröffentlicht Microsoft auch ein Updatepaket in Windows Server Update Services (WSUS). Nachdem Configuration Manager das Office 365-Clientupdate aus dem WSUS-Katalog auf den Standortserver übertragen hat, kann das Update für Clients bereitgestellt werden.

## <a name="office-365-client-management-dashboard"></a>Office 365-Clientverwaltungsdashboard  
Ab Version 1610 von Configuration Manager ist das Office 365-Clientverwaltungsdashboard in der Configuration Manager-Konsole verfügbar. Wechseln Sie zu **Softwarebibliothek** > **Übersicht** > **Office 365 Client Management** (Office 365-Clientverwaltung), um das Dashboard anzuzeigen.

<!--- >[!NOTE]
>In the **What's New** workspace in the Configuration Manager console, the new dashboard is incorrectly named **Office 365 Servicing dashboard**. --->

Das Dashboard zeigt Diagramme für Folgendes an:

- Anzahl der Office 365-Clients
- Office 365-Clientversionen
- Office 365-Clientsprachen
- Office 365-Clientkanäle     
Weitere Informationen finden Sie unter [Übersicht über die Updatekanäle für Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

Verwenden Sie am oberen Rand des Dashboards die Dropdowneinstellung **Sammlung**, um die Dashboarddaten nach Mitgliedern einer bestimmten Sammlung zu filtern.

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Anzeigen von Daten im Office 365-Clientverwaltungsdashboard
Die im Office 365-Clientverwaltungsdashboard angezeigten Daten kommen aus der Hardwareinventur. Die Hardwareinventur muss aktiviert und die **Office 365 ProPlus Configurations**-Hardwareinventurklasse ausgewählt sein, damit die Daten im Dashboard angezeigt werden können.
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>So zeigen Sie Daten im Office 365-Clientverwaltungsdashboard an
1. Aktivieren Sie die Hardwareinventur, falls diese noch nicht aktiviert ist. Weitere Informationen finden Sie unter [Konfigurieren der Hardwareinventur](\sccm\core\clients\manage\configure-hardware-inventory).
2. Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  
3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  
4. Klicken Sie im Dialogfeld **Clientstandardeinstellungen** auf **Hardwareinventur**.  
5. Klicken Sie in der Liste **Geräteeinstellungen** auf **Klassen festlegen**.  
6. Im Dialogfeld der **Hardwareinventurklassen**wählen Sie **Office 365 ProPlus-Configurations** (Office 365 ProPlus-Konfigurationen) aus.  
7.  Klicken Sie auf **OK** , um die Änderungen zu speichern und das Dialogfeld **Hardwareinventurklassen** zu schließen.  
Das Office 365-Clientverwaltungsdashboard zeigt Daten dann an, während die Hardwareinventur ausgewertet wird.

<!---
 On the upper-right side of the dashboard, click **Office 365 Installer** to start the Office 365 Client Installation Wizard to deploy Office 365 apps to clients. For details, see [Deploy Office 365 apps to clients](#deploy-office-365-apps-to-clients).
- On the middle-right side of the dashboard, click **Create an ADR** to open the Automatic Deployment Rule Wizard to create a new automatic deployment rule (ADR). To create an ADR for Office 365 apps, select **Office 365 Client** when you choose the product. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- On the lower-right side of the dashboard, click **Create Client Agent Settings** to open Client Agent settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings).
--->

## <a name="deploy-office-365-updates-with-configuration-manager"></a>Bereitstellen von Office 365-Updates mit Configuration Manager
Befolgen Sie die folgenden Schritte, um Office 365-Updates mit Configuration Manager bereitzustellen:

1.  [Überprüfen Sie die Anforderungen](https://technet.microsoft.com/library/mt628083.aspx) für die Verwendung von Configuration Manager zum Verwalten von Office 365-Client-Updates im Abschnitt **Anforderungen für die Verwendung von Configuration Manager zum Verwalten von Office 365-Clientupdates** des verlinkten Themas.  

2.  [Konfigurieren Sie Softwareupdatepunkte](../get-started/configure-classifications-and-products.md), um die Office 365-Clientupdates zu synchronisieren. Legen Sie als Klassifizierung **Updates** fest, und wählen Sie **Office 365-Client** als Produkt aus. Möglicherweise müssen Sie Softwareupdates mindestens einmal synchronisieren, bevor das Produkt „Office 365-Client“ Ihnen zur Auswahl steht. Nach dem Konfigurieren von Softwareupdatepunkten müssen Sie Softwareupdates synchronisieren, um die Klassifizierung **Updates** zu verwenden.  

3.  Aktivieren Sie die Office 365-Clients, damit sie Updates von Configuration Manager erhalten können. Sie können dies mithilfe von Configuration Manager-Clienteinstellungen oder Gruppenrichtlinien tun. Verwenden Sie eine der nachfolgenden Methoden, um den Client zu aktivieren:  
    - Methode 1: Ab der Version 1606 von Configuration Manager können Sie die Configuration Manager-Clienteinstellung zum Verwalten des Office 365-Client-Agents nutzen. Nachdem Sie diese Einstellung konfiguriert und Updates für Office 365 bereitgestellt haben, kommuniziert der Configuration Manager-Client-Agent mit dem Office 365-Client-Agent, um Office 365-Updates von einem Verteilungspunkt herunterzuladen und zu installieren. Configuration Manager macht eine Bestandsaufnahme der Office 365 ProPlus-Clienteinstellungen.
      1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Übersicht** > **Clienteinstellungen**.  

      2.  Öffnen Sie die entsprechenden Geräteeinstellungen zum Aktivieren des Client-Agents. Weitere Informationen zu standardmäßigen und benutzerdefinierten Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Klicken Sie auf **Softwareupdates** und wählen Sie **Ja** für die Einstellung **Verwaltung des Office 365-Client-Agents aktivieren** aus.  

    - Methode 2: [Aktivieren Sie die Office 365-Clients, um Updates von Configuration Manager zu erhalten](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient), indem Sie das Office-Bereitstellungstool oder die Gruppenrichtlinie verwenden.  

4. [Stellen Sie für Clients Office 365-Updates bereit](deploy-software-updates.md).  

<!--  ## Add other languages for Office 365 update downloads
Beginning in Configuration Manager version 1610, you can add support for Configuration Manager to download updates for any languages supported by Office 365 regardless of whether they are supported in Configuration Manager.

### To add support to download updates for additional languages
Use the following procedure on the central administration site, or stand-alone primary site, where the software update point site system role is installed.
1. From a command prompt, type *wbemtest* as an administrative user to open the Windows Management Instrumentation Tester.
2. Click **Connect**, and then type *root\sms\site_<siteCode>*.
3. Click **Query**, and then run the following query:
   *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*
4. Double-click the object with the site code for the central administration site or stand-alone primary site.

5. Browse the properties for View Embedded.
3). Find the SMS_EmbeddedProperty instance with the PropertyName of "AdditionalUpdateLanguagesForO365"
4). Set Value2 to be additional languages, e.g.:  pt-pt,af-za,nn-no, and save
5). Right click to download an O365 update, choose languages from UI
6). Verify that the language packs got downloaded including the UI specified ones plus the SDK specified ones. Admin can check the content package share specified to verify this.
-->

<!-- ## Change the update channel after you enable Office 365 clients to receive updates from Configuration Manager
To change the update channel after you enable Office 365 clients to receive updates from Configuration Manager, you must distribute a registry key value change to Office 365 clients using group policy. Change the **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** registry key to use one of the following values:

- Current Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Deferred Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- First Release for Current Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- First Release for Deferred Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf
-->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->



<!--HONumber=Jan17_HO3-->


