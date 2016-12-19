---
title: "Ausschließen von Ordnern aus der Softwareinventur | Microsoft Docs"
description: "Schließen Sie Ordner aus der Softwareinventur in System Center Configuration Manager aus."
ms.custom: na
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6d1aabbde576f01de920468fd3ef372bd23be9df
ms.openlocfilehash: 7850b69cdccb0e897ee71b75255004bdc8d0ae97


---
# <a name="how-to-exclude-folders-from-software-inventory-in-system-center-configuration-manager"></a>Ausschließen von Ordnern aus der Softwareinventur in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

 Mithilfe dieses Verfahrens werden die Clientstandardeinstellungen für die Softwareinventur konfiguriert. Sie gilt für alle Computer in der Hierarchie. Wenn Sie diese Einstellungen nur auf manche Computer anwenden möchten, erstellen Sie eine benutzerdefinierte Geräteclienteinstellung und weisen diese einer Sammlung mit den Computern zu, auf denen Sie die Softwareinventur verwenden möchten. Weitere Informationen zum Erstellen benutzerdefinierter Geräteeinstellungen finden Sie unter [Konfigurieren von Geräteclienteinstellungen in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

### <a name="to-configure-software-inventory"></a>So konfigurieren Sie die Softwareinventur  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

5.  Wählen Sie im Dialogfeld **Standardeinstellungen** die Option **Softwareinventur** aus.  

6.  Konfigurieren Sie in der Liste **Geräteeinstellungen** die folgenden Werte:  

    -   **Softwareinventur für Clients aktivieren** – Wählen Sie in der Dropdownliste **Wahr** aus.  

    -   **Zeitplan für die Softwareinventur und Dateisammlung planen** – Konfiguriert das Intervall, in dem der Client Softwareinventur und Dateien sammelt.   

7.  Konfigurieren Sie die erforderlichen Clienteinstellungen. Eine Liste der Clienteinstellungen für Softwareinventur, die Sie konfigurieren können, finden Sie im Abschnitt [Softwareinventur](../../../../core/clients/deploy/about-client-settings.md#software-inventory) des Themas [Clienteinstellungen in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

 Die Clientcomputer werden beim nächsten Clientrichtliniendownload mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Abrufens von Richtlinien für einen einzelnen Client finden Sie unter [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Dec16_HO3-->


