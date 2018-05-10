---
title: Konfigurieren der Softwareinventur
titleSuffix: Configuration Manager
description: Konfigurieren Sie die Softwareinventur, und schließen Sie Ordner aus der Softwareinventur in Configuration Manager aus.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 346ff3254f4c1833f49bf256cbf5ad0c489d77e0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Konfigurieren der Softwareinventur in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mithilfe dieses Verfahrens werden die Clientstandardeinstellungen für die Softwareinventur konfiguriert. Sie gilt für alle Computer in der Hierarchie. Wenn diese Einstellungen nur auf manche Clients angewendet werden sollen, erstellen Sie eine benutzerdefinierte Clientgeräteeinstellung, und weisen Sie diese einer Sammlung zu. Weitere Informationen zum Erstellen benutzerdefinierter Geräteeinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).   

## <a name="to-configure-software-inventory"></a>So konfigurieren Sie die Softwareinventur  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

5.  Wählen Sie im Dialogfeld **Standardeinstellungen** die Option **Softwareinventur** aus.  

6.  Konfigurieren Sie in der Liste **Geräteeinstellungen** die folgenden Werte:  

    -   **Softwareinventur für Clients aktivieren** – Wählen Sie in der Dropdownliste **Wahr** aus.  

    -   **Zeitplan für die Softwareinventur und Dateisammlung planen** – Konfiguriert das Intervall, in dem der Client Softwareinventur und Dateien sammelt.   

7.  Konfigurieren Sie die erforderlichen Clienteinstellungen. Im Abschnitt [Softwareinventur](../../../../core/clients/deploy/about-client-settings.md#software-inventory) des Artikels [Informationen zu Clienteinstellungen in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) finden Sie eine Liste der Clienteinstellungen.  

 Die Clientcomputer werden beim nächsten Clientrichtliniendownload mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Abrufens von Richtlinien für einen einzelnen Client finden Sie unter [Verwalten von Clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

 > [!TIP]  
        >   Der Fehlercode 80041006 in der inventoryprovider.log-Datei bedeutet, dass der WMI-Anbieter über nicht genügend Arbeitsspeicher verfügt. Das bedeutet, dass die Beschränkung des Speicherkontingents für den Anbieter erreicht wurde und der Inventuranbieter nicht mehr fortgeführt werden kann.
In diesem Fall erstellt der Inventur-Agent einen leeren Bericht. D.h. keine Inventurelemente werden gemeldet. <br/>
Sie können den Bereich der Softwareinventursammlung reduzieren, um diesen Fehler zu beheben. Wenn der Fehler auftritt, nachdem der Inventurbereich eingeschränkt wurde, können Sie zur Lösung des Problems die in der [_ProviderHostQuotaConfiguration](https://msdn.microsoft.com/library/aa394671)-Klasse definierte [MemoryPerHost](https://blogs.technet.microsoft.com/askperf/2008/09/16/memory-and-handle-quotas-in-the-wmi-provider-service/)-Eigenschaft erhöhen.

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>So schließen Sie Ordner aus der Softwareinventur aus  

1.  Erstellen Sie mit "Notepad.exe" eine leere Datei namens **Skpswi.dat**.  

2.  Klicken Sie mit der rechten Maustaste auf die Datei **Skpswi.dat**, und klicken Sie dann auf **Eigenschaften**. Wählen Sie in den Dateieigenschaften für die Datei "Skpswi.dat" das Attribut **Ausgeblendet** aus.  

3.  Platzieren Sie die Datei **Skpswi.dat** im Stammverzeichnis jeder Clientfestplatte oder Ordnerstruktur, die von der Softwareinventur ausgeschlossen werden soll.  

> [!NOTE]  
>  Die Softwareinventur inventarisiert das Clientlaufwerk nicht noch einmal, außer diese Datei wird vom Laufwerk auf dem Clientcomputer gelöscht.