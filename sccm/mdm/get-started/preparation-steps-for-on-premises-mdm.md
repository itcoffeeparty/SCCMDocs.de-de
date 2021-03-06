---
title: 'Vorbereitungsschritte '
titleSuffix: Configuration Manager
description: Bereiten Sie die lokale Verwaltung mobiler Geräte in System Center Configuration Manager vor.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 711af365353d68020a7bbbef8026f452d4203ce3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="preparation-steps-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Vorbereitungsschritte für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Für die lokale Verwaltung mobiler Geräte mit System Center Configuration Manager muss die Configuration Manager-Infrastruktur so eingerichtet sein, dass die erforderlichen Standortsystemrollen (Registrierungsproxypunkt, Registrierungspunkt, Geräteverwaltungspunkt und Verteilungspunkt) über einen vertrauenswürdigen Kanal mit den zu verwaltenden mobilen Geräten kommunizieren können.  

 Die folgenden hochrangigen Aufgaben sind erforderlich, um das Configuration Manager-System für das lokale Mobile Device Management vorzubereiten:  

-   [Einrichten eines Microsoft Intune-Abonnements in System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md)  

     Bei diesem Task registrieren Sie sich für Microsoft Intune und fügen anschließend das Abonnement für Configuration Manager über die Configuration Manager-Konsole hinzu. Dieser Schritt ist nur für Lizenzierungszwecke erforderlich. Intune wird nicht zum Verwalten der Geräte oder zum Speichern von Verwaltungsinformationen verwendet. Die gesamte Koordination und Verwaltung von Geräten erfolgt mithilfe der lokalen Configuration Manager-Infrastruktur in Ihrer Organisation.  

-   [Installieren von Standortsystemrollen für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     Bei diesem Task installieren und konfigurieren Sie die Standortsystemrollen, die zum Verwalten von Geräten mit einer lokalen Configuration Manager-Infrastruktur erforderlich sind. Lokales Mobile Device Management erfordert mindestens die Standortsystemrollen Registrierungsproxypunkt, Registrierungspunkt, Geräteverwaltungspunkt und Verteilungspunkt.  

-   [Einrichten von Zertifikaten für vertrauenswürdige Verbindungen für die lokale Verwaltung von Mobilgeräten in System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

     Bei diesem Task konfigurieren Sie die lokale Configuration Manager-Infrastruktur, um die vertrauenswürdige Übertragung (HTTPS) zwischen verwalteten Geräten und den Servern zu ermöglichen, die die erforderlichen Standortsystemrollen hosten.  

-   [Einrichten der Geräteregistrierung für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

     In diesem Task erteilen Sie den Benutzern die Berechtigung zum Registrieren von Computern und Geräten. Zudem installieren Sie das vertrauenswürdige Stammzertifikat auf Geräten (in der Regel Geräte, die keiner Domäne angehören), um HTTPS-Verbindungen mit den Standortsystemservern zuzulassen.  
