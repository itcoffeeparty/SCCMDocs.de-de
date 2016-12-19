---
title: Erstellen von Windows Phone-Anwendungen | Microsoft Docs
description: "Erfahren Sie, was Sie beim Erstellen und Bereitstellen von Anwendungen für Windows Phone-Geräte berücksichtigen müssen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 866113ff-efd0-40d2-ac3a-2edd49732a24
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 557888d1f1f899e3198c430bbe5ccdd44178f824
ms.openlocfilehash: 5cd1ba42afd13e98565d24d1ec8a3ee209e8532c


---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>Erstellen von Windows Phone-Anwendungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Zusätzlich zu den anderen System Center Configuration Manager-Anforderungen und -Verfahren zum Erstellen einer Anwendung müssen beim Erstellen und Bereitstellen von Anwendungen für Windows Phone-Geräte auch die folgenden Aspekte berücksichtigt werden.  

## <a name="general-considerations"></a>Allgemeine Aspekte  
 Configuration Manager unterstützt die Bereitstellung folgender App-Dateitypen:  

|Gerätetyp|Unterstützte Dateitypen|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap, .appx, .appxbundle|  

 Die folgenden Bereitstellungsaktionen werden unterstützt:  

|Gerätetyp|Unterstützte Aktionen|  
|-----------------|-----------------------|  
|Windows Phone 8 und Windows Phone 8.1|Verfügbar, Erforderlich, Deinstallieren|  

## <a name="steps-to-deploy-the-latest-windows-phone-company-portal-app-with-supersedence"></a>Schritte zur Bereitstellung der neuesten Windows Phone-Unternehmensportal-App mit Ablösung  
 In der folgenden Tabelle finden Sie Schritte, Details und weitere Informationen zum Erstellen und Bereitstellen der aktuellen Windows Phone 8-Unternehmensportal-App.  

|Schritt|Weitere Informationen|  
|----------|----------------------|  
|**Schritt 1:** Beschaffen Sie sich die aktuelle Unternehmensportal-App.|Laden Sie die [Unternehmensportal-App von Windows Phone 8](http://go.microsoft.com/fwlink/?LinkId=268440)herunter.|  
|**Schritt 2:** Signieren Sie die Unternehmensportal-App mit Ihrem Symantec-Zertifikat.|Weitere Informationen zum Signieren der Unternehmensportal-App finden Sie unter [Set up Windows Phone and Windows 10 Mobile hybrid device management with System Center Configuration Manager and Microsoft Intune (Einrichten einer hybriden Geräteverwaltung für Windows Phone und Windows 10 Mobile mit System Center Configuration Manager und Microsoft Intune)](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Schritt 3:** Erstellen Sie eine neue Anwendung mit der aktuellen Version der Unternehmensportal-App, und geben Sie eine Ablösungsbeziehung an.|Weitere Informationen finden Sie unter [Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md) und [Überarbeiten und Ablösen von Anwendungen](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Schritt 4:** Fügen Sie die Anwendung dem Assistenten für Microsoft Intune-Abonnements hinzu.|Weitere Informationen finden Sie unter [Set up Windows Phone and Windows 10 Mobile hybrid device management with System Center Configuration Manager and Microsoft Intune (Einrichten einer hybriden Geräteverwaltung für Windows Phone und Windows 10 Mobile mit System Center Configuration Manager und Microsoft Intune)](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Schritt 5:** Löschen Sie die beim Hinzufügen der Unternehmensportal-App zum Assistenten für Microsoft Intune-Abonnements automatisch erstellte Bereitstellung.|Eine automatische Bereitstellung dieser App wurde durch das Microsoft Intune-Abonnement erstellt, da eine Ablösung von dieser Bereitstellung nicht unterstützt wird.|  
|**Schritt 6:** Erstellen Sie eine neue Bereitstellung der Anwendung. Aktivieren Sie im **Assistenten zum Bereitstellen von Software** auf der Seite **Bereitstellungseinstellungen** die Option **Automatically upgrade any superceded versions of this application** (Abgelöste Versionen dieser Anwendung automatisch upgraden).|Erstellen Sie mithilfe der Anwendung, die Sie mit der Ablösungsbeziehung erstellt haben, eine neue Bereitstellung mit Ablösung.|  
|**Schritt 7 (optional):** Die ablösenden Apps würden standardmäßig nach 7 Tagen auf den Geräten installiert werden. Wenn Sie die Unternehmensportal-App auf zuvor bereits angemeldeten Geräten schneller bereitstellen möchten, können Sie für die Einstellung **Erneute Auswertung für Bereitstellungen planen** einen niedrigeren Wert festlegen.<br /><br /> Wenn Sie einen Wert festlegen, der niedriger als die Standardeinstellung ist, kann dies jedoch die Leistung von Netzwerk und Clientcomputern beeinträchtigen.|keine zusätzlichen Informationen|  



<!--HONumber=Dec16_HO3-->


