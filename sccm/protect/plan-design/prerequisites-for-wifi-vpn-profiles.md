---
title: Voraussetzungen für WLAN- und VPN-Profile
titleSuffix: Configuration Manager
description: Erfahren sie mehr zu den Sicherheitsberechtigungen, die zum Verwalten von Zertifikat-, WLAN- und VPN-Profilen in System Center Configuration Manager erforderlich sind.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 894717df4b5acb7142aa7d171a8b8b63a28f8dc0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Voraussetzungen für WLAN- und VPN-Profile in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

WLAN- und VPN-Profile in System Center Configuration Manager weisen nur Abhängigkeiten innerhalb des Produkts auf.  

 Sie müssen über die folgenden Sicherheitsberechtigungen verfügen, um Einstellungen für den Zugriff auf Unternehmensressourcen wie Zertifikatprofile, WLAN-Profile und VPN-Profile zu verwalten:  

-   Zum Anzeigen und Verwalten von Warnungen und Berichte für WLAN- und VPN-Profile: **Erstellen**, **Löschen**, **Ändern**, **Bericht ändern**, **Lesen** und **Bericht ausführen** für das Objekt **Warnungen**.  

-   So erstellen und verwalten Sie Zertifikatprofile: **Richtlinie erstellen**, **Bericht ändern**, **Lesen**und **Bericht ausführen** für das Objekt **Zertifikatprofil** .  

-   So verwalten Sie Bereitstellungen von WLAN-, Zertifikat- und VPN-Profilen: **Konfigurationsrichtlinien bereitstellen**, **Warnung zu Clientstatus ändern**, **Lesen**und **Ressource lesen** für das Objekt **Sammlung** .  

-   So verwalten Sie alle Konfigurationsrichtlinien: **Erstellen**, **Löschen**, **Ändern**, **Lesen**und **Sicherheitsbereich festlegen** für das Objekt **Konfigurationsrichtlinie** .  

-   Zum Ausführen von Abfragen zu WLAN- und VPN-Profilen: Berechtigung **Lesen** für das Objekt **Abfrage**.  

-   Zum Anzeigen von Informationen zu WLAN- und VPN-Profilen in der System Center Configuration Manager-Konsole: Berechtigung **Lesen** für das Objekt **Standort**.  

-   Zum Anzeigen von Statusmeldungen für WLAN- und VPN-Profile: Berechtigung **Lesen** für das Objekt **Statusmeldungen**.  

-   So erstellen und verwalten Sie das Zertifikatprofil der vertrauenswürdigen Zertifizierungsstelle: **Richtlinie erstellen**, **Bericht ändern**, **Lesen**und **Bericht ausführen** für das Objekt **Zertifikatprofil der vertrauenswürdigen Zertifizierungsstelle** .  

-   So erstellen und verwalten Sie VPN-Profile: **Richtlinie erstellen**, **Bericht ändern**, **Lesen**und **Bericht ausführen** für das Objekt **VPN-Profil** .  

-   So erstellen und verwalten Sie WLAN-Profile: **Richtlinie erstellen**, **Bericht ändern**, **Lesen**und **Bericht ausführen** für das Objekt **WLAN-Profil** .  

 In der Sicherheitsrolle **Zugriffs-Manager für Unternehmensressourcen** sind diese Berechtigungen zum Verwalten der WLAN-Profile in System Center Configuration Manager enthalten. Weitere Informationen finden Sie unter [Configure security in System Center Configuration Manager (Konfigurieren der Sicherheit in System Center Configuration Manager)](../../core/plan-design/security/configure-security.md).
