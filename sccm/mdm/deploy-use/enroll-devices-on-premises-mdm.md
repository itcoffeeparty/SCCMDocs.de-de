---

title: "Registrieren von Geräten | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über Geräteregistrierungsmethoden für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 8f9667388c3557a84fc84c742e25f0c3bd2e2a5f
ms.lasthandoff: 03/06/2017


---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Registrieren von Geräten für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Zum Verwalten von Computern und Geräten mit der lokalen Verwaltung mobiler Geräte in System Center Configuration Manager müssen die Geräte registriert werden, damit Configuration Manager für Verwaltungstasks mit den Geräten kommunizieren kann. Configuration Manager bietet zwei Methoden zum Registrieren von Geräten:  

-   **Benutzerregistrierung** : Bei dieser Methode initiieren Benutzer den Registrierungsvorgang auf ihren Geräten. Damit die Benutzerregistrierung erfolgreich ist, muss auf dem Gerät ein vertrauenswürdiges Stammzertifikat installiert sein, und der Benutzer muss für die Registrierung von Configuration Manager bereitgestellt sein.  Zum Registrieren eines Geräts braucht der Benutzer lediglich seine Unternehmensanmeldeinformationen anzugeben, und das Gerät wird für die Verwaltung registriert.  

     Weitere Informationen finden Sie unter [Informationen zur Registrierung von Geräten mit der lokalen Verwaltung mobiler Geräte in System Center Configuration Manager](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

-   **Massenregistrierung** : Bei dieser Methode braucht der Benutzer des Geräts die Registrierung nicht zu initiieren. Stattdessen wird ein Massenregistrierungspaket in Configuration Manager erstellt, auf dem Gerät abgelegt und geöffnet. Das Paket stellt nach dem Öffnen die erforderlichen Informationen zum Registrieren des Geräts bereit.  

     Weitere Informationen finden Sie unter [Massenregistrierung von Geräten mit der lokalen Verwaltung von Geräten in System Center Configuration Manager](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md).  

 > [!NOTE]  
>  Configuration Manager Current Branch unterstützt die Registrierung bei der lokalen Verwaltung mobiler Geräte für Geräte, auf denen folgende Betriebssysteme ausgeführt werden:  
>   
>  -   Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Microsoft 10 Team \(ab Configuration Manager Version 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise   

