---
title: Einrichten eines Intune-Abonnements | Lokal | System Center Configuration Manager
description: "Richten Sie ein Intune-Abonnement ein, um die Lizenzierung für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager zu verfolgen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
caps.latest.revision: 8
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4daf5d6ea30aa1fb4aa189ef6da9b364fe197805


---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Einrichten eines Microsoft Intune-Abonnements in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die lokale Verwaltung mobiler Geräte in System Center Configuration Manager setzt ein Microsoft Intune-Abonnement voraus, damit die Lizenzierung verfolgt werden kann. Der Intune-Dienst wird nicht zum Verwalten von Geräten oder zum Speichern von Verwaltungsinformationen verwendet. Für die lokale Verwaltung mobiler Geräte erfolgt die gesamte Geräteverwaltung über die Configuration Manager-Infrastruktur.  

> [!IMPORTANT]  
>  Configuration Manager unterstützt die gleichzeitige Verwendung von Microsoft Intune und der lokalen Configuration Management-Infrastruktur als Verwaltungsstellen nicht. Somit deaktivieren Sie beim Einrichten des Intune-Abonnements für die lokale Verwaltung tatsächlich die Intune-Verwaltung.  

 Die Einrichtung des Intune-Diensts, sodass dieser mit der lokalen Verwaltung mobiler Geräte arbeitet, umfasst die folgenden allgemeinen Schritte:  

-   [Registrieren für Microsoft Intune](#bkmk_signup)  

-   [Hinzufügen des Intune-Abonnements zu Configuration Manager](#bkmk_addSub)  

-   [Konfigurieren des Intune-Abonnements zur lokalen Verwaltung mobiler Geräte](#bkmk_configure)  

> [!TIP]  
>  Es wird empfohlen, dass Sie das Intune-Abonnement für die lokale Verwaltung mobiler Geräte einrichten, bevor Sie die erforderlichen Standortsystemrollen installieren, um die erforderliche Zeit zu minimieren, bis die neu installierten Standortsystemrollen funktionsfähig sind.  

##  <a name="a-namebkmksignupa-sign-up-for-microsoft-intune"></a><a name="bkmk_signup"></a> Registrieren für Microsoft Intune  
 Intune ist erforderlich, damit die lokale Verwaltung mobiler Geräte funktionsfähig ist. [Registrieren](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/) Sie sich einfach für ein Test- oder ein kostenpflichtiges Abonnement, und wechseln Sie dann zum nächsten Schritt, um das Abonnement Configuration Manager hinzuzufügen.  

##  <a name="a-namebkmkaddsuba-add-the-intune-subscription-to-configuration-manager"></a><a name="bkmk_addSub"></a> Hinzufügen des Intune-Abonnements zu Configuration Manager  
 Damit das Abonnement Configuration Manager hinzugefügt wird, befolgen Sie einfach die gleichen grundlegenden Schritte wie beim Hinzufügen des Abonnements für die Verwaltung mobiler Geräte mit Intune. Informationen über die Unterschiede finden Sie in den Hinweisen unten. Verwenden Sie dann die Anweisungen aus [So erstellen Sie das Microsoft Intune-Abonnement](../../mdm/plan-design/hybrid-mobile-device-management.md#bkmk_subscription) in [Hybride Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune](../../mdm/plan-design/hybrid-mobile-device-management.md).  

> [!NOTE]  
>  Bedenken Sie beim Hinzufügen des Intune-Abonnements Folgendes:  
>   
>  -   Die im Assistenten zum Hinzufügen eines Microsoft Intune\-Abonnements angegebene Sammlung wird nicht für die Benutzerrechtdelegierung der lokalen Verwaltung mobiler Geräte verwendet. Sie dient lediglich der Verwaltung mobiler Geräte mit Intune. Allerdings müssen Sie an eine Sammlung angeben, damit der Assistent fortgesetzt werden kann.  
> -   Die im Assistenten angegebene Standortcodeeinstellung wird für die lokale Verwaltung mobiler Geräte ignoriert. Der verwendete Standortcode ist der Code, den Sie im Registrierungsprofil angeben, das den Benutzern die Berechtigung zum Registrieren von Geräten erteilt.  
> -   Aktivieren Sie nicht die Multi-Factor Authentication. Sie wird in der lokalen Verwaltung mobiler Geräte nicht unterstützt.  

##  <a name="a-namebkmkconfigurea-configure-the-intune-subscription-for-on-premises-mobile-device-management"></a><a name="bkmk_configure"></a> Konfigurieren des Intune-Abonnements zur lokalen Verwaltung mobiler Geräte  

1.  Klicken Sie in der Configuration Manager-Konsole mit der rechten Maustaste auf **Microsoft Intune-Abonnement**, und klicken Sie dann auf **Eigenschaften**.  

2.  Aktivieren Sie im Feld für die lokale Verwaltung mobiler Geräte das Kontrollkästchen neben **Geräte nur lokal verwalten**, und klicken Sie dann auf **OK**.  

    > [!NOTE]  
    >  Durch Aktivieren dieses Kontrollkästchens konfigurieren Sie das Intune-Abonnement so, dass alle Verwaltungsinformationen lokal vorgehalten und Daten nicht in der Cloud repliziert werden.  

3.  Wenn Sie beabsichtigen, Geräte mit Windows 10 Mobile zu verwalten, klicken Sie mit der rechten Maustaste auf **Microsoft Intune-Abonnement**, klicken Sie dann auf **Plattformen konfigurieren**, und klicken Sie anschließend auf  **Windows Phone**.  

4.  Aktivieren Sie das Kontrollkästchen neben **Windows Phone 8.1 und Windows 10 Mobile**, und klicken Sie dann auf **OK**.  

5.  Wenn Sie beabsichtigen, Desktopcomputer mit Windows 10 zu verwalten, klicken Sie mit der rechten Maustaste auf **Microsoft Intune-Abonnement**, klicken Sie dann auf **Plattformen konfigurieren**, und klicken Sie anschließend auf **Windows-Registrierung aktivieren**.  

6.  Aktivieren Sie das Kontrollkästchen neben **Windows-Registrierung aktivieren**, und klicken Sie dann auf **OK**.  



<!--HONumber=Nov16_HO1-->


