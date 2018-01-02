---
title: "Migrieren von Benutzern und Geräten in einer MDM-Hybridlösung zu eigenständigem Intune"
titleSuffix: Configuration Manager
description: "Erfahren Sie, wie Sie Benutzer und Geräte in einer MDM-Hybridlösung zu eigenständigem Intune migrieren."
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: 30474f6dd0216078ab1ac1f4bd9f5044f1b174f0
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/06/2017
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>Migrieren von Benutzern und Geräten in einer MDM-Hybridlösung zu eigenständigem Intune

*Gilt für: System Center Configuration Manager (Current Branch)*    

Wenn Sie sich entschieden haben, dass Sie bereit sind, von einer MDM-Hybridlösung (in Configuration Manager integriertes Intune) zu einer reinen Cloudumgebung mit Intune in Azure zu migrieren, dann ist dieser Artikel genau das Richtige für Sie. Wenn Sie noch unsicher sind, siehe [Wählen zwischen eigenständigem Microsoft Intune und der hybriden Verwaltung mobiler Geräte mit System Center Configuration Manager](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management). 

Sie können mit der Migration zu eigenständigem Intune beginnen, indem Sie einen gestaffelten Ansatz verfolgen. Dieser ermöglicht Ihnen, eine kleine Teilmenge von Benutzern und Geräten zu testen, während die meisten Ihrer Benutzer und Geräte weiterhin mit der MDM-Hybridlösung verwaltet werden. Nachdem Sie die Intune-Funktionalität überprüft haben, können Sie mit der Migration weiterer Benutzer zu Intune beginnen.    

In den folgenden Themen werden die Schritte zur Migration Ihrer Benutzer zu eigenständigem Intune anhand eines gestaffelten Ansatzes beschrieben.    
  
1.  [Importieren von Configuration Manager-Daten in Microsoft Intune](migrate-import-data.md)   
    Das Datenimport-Tool von Intune sammelt Daten zu den Objekten, die Sie in Ihrer Configuration Manager-Hierarchie auswählen. Es liefert Details zu den Objekten, die Sie für den Import auswählen können, und Informationen darüber, warum einige Objekte nicht importiert werden können. Es ermöglicht zudem den Import ausgewählter Objekte in Ihren Microsoft Intune-Mandanten. Auch wenn dieser Schritt optional ist, kann er Ihnen sehr viel Zeit dadurch sparen, dass der Prozess der Neuerstellung von Objekten aus Configuration Manager in Intune automatisiert wird. 
2.  [Vorbereiten von Intune für die Benutzermigration](migrate-prepare-intune.md)    
    Validieren Sie aus Configuration Manager importierte Objekte. Erstellen Sie neue Objekte und AAD-Gruppen. Nehmen Sie Objektzuweisungen zu diesen Gruppen vor. Installieren Sie den Registrierungsdienst für Netzwerkgeräte und Exchange Connectors usw. Nachdem Sie die Schritte abgeschlossen und die Migration zu eigenständigem Intune gestartet haben, sollte diese für Ihre Benutzer unbemerkt erfolgen.  
3.  [Ändern der MDM-Autorität für bestimmte Benutzer (gemischte MDM-Autorität)](migrate-mixed-authority.md)    
    Konfigurieren Sie eine gemischte MDM-Autorität im selben Mandanten, indem Sie einige Benutzer auswählen, die in Intune verwaltet werden sollen, während alle anderen Geräte weiterhin mit einer MDM-Hybridlösung (in Configuration Manager integriertes Intune) verwaltet werden. Sie können testen, ob Intune auf den Geräten einer kleinen Gruppe von Benutzern erwartungsgemäß funktioniert, bevor Sie mit der Migration weiterer Benutzer beginnen. 
4.  [Umstellen der MDM-Autorität auf eigenständiges Intune](change-mdm-authority.md)     
    Stellen Sie die MDM-Autorität auf Mandantenebene von Configuration Manager auf Intune um. Alle übrigen Benutzer und Geräte werden in das eigenständige Intune-System migriert. Sie stellen Ihre MDM-Autorität auf Mandantenebene um, nachdem Sie die Intune-Funktionalität im vorherigen Schritt gründlich getestet und wahrscheinlich die meisten oder alle Ihrer Benutzer bereits migriert haben.