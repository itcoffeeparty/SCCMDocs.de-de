---
title: 'Registrieren von Geräten '
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Geräteregistrierungsmethoden für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e3254fdad766260e3e162378894526e9b4a7249
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
> -   Windows 10 Team 
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise   
