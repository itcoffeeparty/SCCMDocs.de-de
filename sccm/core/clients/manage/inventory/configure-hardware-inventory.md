---
title: Konfigurieren der Hardwareinventur | System Center Configuration Manager
description: "Richten Sie die Hardwareinventur für alle Clients oder für eine Sammlung in System Center Configuration Manager ein."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 41bf42228e41785a05359c08e8dfedae48d50e30


---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Gehen Sie wie nachfolgend beschrieben vor, um die Hardwareinventur in System Center Configuration Manager für Ihren Standort zu konfigurieren.  

 Mithilfe dieses Verfahrens werden die Clientstandardeinstellungen für die Hardwareinventur konfiguriert. Sie gilt für alle Clients in der Hierarchie. Wenn Sie diese Einstellungen nur auf manche Clients anwenden möchten, erstellen Sie eine benutzerdefinierte Geräteclienteinstellung und weisen diese einer Sammlung mit den Geräten zu, auf denen Sie die Hardwareinventur verwenden möchten. Weitere Informationen zum Erstellen benutzerdefinierter Geräteeinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Wenn ein Clientgerät Hardwareinventureinstellungen von mehreren Clienteinstellungssätzen erhält, werden die Hardwareinventurklassen aus jedem Einstellungssatz zusammengeführt, sobald vom Client eine Hardwareinventur gemeldet wird.  

### <a name="to-configure-hardware-inventory"></a>So konfigurieren Sie die Hardwareinventur  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Clienteinstellungen**.  

3.  Klicken Sie auf **Clientstandardeinstellungen**.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie im Dialogfeld **Standardeinstellungen** auf **Hardwareinventur**.  

6.  Konfigurieren Sie in der Liste **Geräteeinstellungen** die folgenden Optionen:  

    -   **Hardwareinventur auf Clients aktivieren** – Wählen Sie in der Dropdownliste **Wahr**aus.  

    -   **Hardwareinventur-Zeitplan** – Geben Sie das Intervall an, in dem von Clients eine Hardwareinventur gesammelt wird. Verwenden Sie den Standardwert (alle **7 Tage** ), oder klicken Sie zum Konfigurieren eines benutzerdefinierten Intervalls auf **Zeitplan** .  

7.  Konfigurieren Sie weitere erforderliche Clienteinstellungen. Eine Liste der Hardwareinventurclient-Einstellungen, die Sie konfigurieren können, finden Sie im Abschnitt [Hardwareinventur](../../../../core/clients/deploy/about-client-settings.md#BKMK_HardwareInventoryDeviceSettings) des Themas [Informationen zu Clienteinstellungen in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

8.  Klicken Sie auf **OK** , um das Dialogfeld **Standardeinstellungen** zu schließen.  

 Die Clientgeräte werden beim nächsten Clientrichtliniendownload mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Abrufens von Richtlinien für einen einzelnen Client finden Sie unter [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Nov16_HO1-->


