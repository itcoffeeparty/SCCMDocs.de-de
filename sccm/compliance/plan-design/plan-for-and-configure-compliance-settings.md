---
title: Planen und Konfigurieren von Konformitätseinstellungen
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu den Voraussetzungen und Konfigurationsaufgaben für die Arbeit mit Konformitätseinstellungen in System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 84643f38b5dd0c42a611ca50aaae6ab6d9f52405
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="plan-for-and-configure-compliance-settings-in-system-center-configuration-manager"></a>Planen und Konfigurieren von Konformitätseinstellungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bevor Sie beginnen, mit System Center Configuration Manager-Kompatibilitätseinstellungen zu arbeiten, gibt es einige Voraussetzungen, die Sie kennen sollten, und einige Konfigurationsaufgaben, die Sie ausführen müssen.  

## <a name="prerequisites-for-compliance-settings"></a>Voraussetzungen für Konformitätseinstellungen  

|Voraussetzung|Weitere Informationen|  
|------------------|----------------------|  
|Windows Configuration Manager-Clients müssen für die Kompatibilitätsauswertung aktiviert und konfiguriert werden.|Informationen hierzu finden Sie weiter unten.|  
|Wenn Sie Berichte ausführen möchten, müssen Sie die Berichterstellung für Ihren Standort konfigurieren.|[Berichterstellung in System Center Configuration Manager](../../core/servers/manage/reporting.md)|  
|Erforderliche Sicherheitsberechtigungen|Die Sicherheitsrolle **Kompatibilitätseinstellungs-Manager** beinhaltet die erforderlichen Berechtigungen, um Kompatibilitätseinstellungen, Konfigurationselemente für Benutzerdaten und -profile sowie Remoteverbindungsprofile verwalten zu können.<br /><br /> [Configure role-based administration (Konfigurieren der rollenbasierten Verwaltung)](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Aktivieren und Konfigurieren von Kompatibilitätseinstellungen (nur für Windows-PCs)  

In dieser Vorgehensweise werden die Standardclienteinstellungen für Konformitätseinstellungen konfiguriert und auf alle Computer in Ihrer Hierarchie angewendet. Wenn Sie diese Einstellungen nur auf manche Computer anwenden möchten, erstellen Sie eine benutzerdefinierte Geräteclienteinstellung, und weisen Sie diese einer Sammlung zu, die die Computer enthält, für die Sie die Kompatibilitätseinstellungen anwenden möchten. Weitere Informationen zum Erstellen von benutzerdefinierten Geräteeinstellungen finden Sie unter [How to configure client settings (Konfigurieren von Clienteinstellungen)](../../core/clients/deploy/configure-client-settings.md).  

> [!TIP]  
>  Andere Gerätetypen erfordern keine besondere Konfiguration für die Auswertung von Kompatibilitätseinstellungen.  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Clienteinstellungen** > **Standardeinstellungen**.  
2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  
3.  Klicken Sie im Dialogfeld **Standardeinstellungen** auf **Kompatibilitätseinstellungen**.  
4.  Konfigurieren Sie die folgenden Clienteinstellungen für Kompatibilitätseinstellungen:
    - **Kompatibilitätsauswertung auf Clients aktivieren:** Legen Sie diese Einstellung auf **TRUE** fest, wenn Sie die Kompatibilität auf Clientgeräten auswerten möchten.
    - **Kompatibilitätsauswertung planen:** Klicken Sie auf **Zeitplan**, wenn Sie den Standardzeitplan der Kompatibilitätsauswertung auf Clientgeräten ändern möchten.
    - **Benutzerdaten und -profile aktivieren:** Aktivieren Sie diese Option, wenn Sie Konfigurationselemente für Benutzerdaten und -profile auf Windows-Computern erstellen und bereitstellen möchten. Ausführlichere Informationen finden Sie unter [Erstellen von Konfigurationselementen für Benutzerdaten und -profile](/sccm/compliance/deploy-use/create-remote-connection-profiles).
5. Klicken Sie auf **OK** , um das Dialogfeld **Standardeinstellungen** zu schließen.  

Die Clientcomputer werden beim nächsten Download der Clientrichtlinien mit diesen Einstellungen konfiguriert.  
