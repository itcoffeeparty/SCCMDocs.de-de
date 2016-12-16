---
title: "Einrichten einer hybriden Geräteverwaltung für Android mit System Center Configuration Manager und Microsoft Intune"
description: "Bereiten Sie die Verwaltung mobiler Android-Geräte mit Configuration Manager und Intune vor."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fa189e812a2e3104cb337ccf40c693621745ee53


---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Einrichten einer hybriden Geräteverwaltung für Android mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Benutzer können für System Center Configuration Manager die Unternehmensportal-App für Android aus Google Play herunterladen, mit der sie Android-Geräte (einschließlich Samsung KNOX) registrieren können. Mit der Android-Unternehmensportal-App können Sie Kompatibilitätseinstellungen verwalten, Android-Geräte zurücksetzen oder löschen, Apps bereitstellen und die Software- und Hardwareinventur erfassen. Wenn die Android-Unternehmensportal-App auf Android-Geräten nicht installiert ist, stehen Ihnen nicht alle Verwaltungsfunktionen zur Verfügung (z. B. Inventur- und Kompatibilitätseinstellungen), aber Sie können trotzdem Apps auf Android-Geräten bereitstellen.  

## <a name="prepare-to-manage-android-mobile-devices-with-configuration-manager-and-intune"></a>Vorbereiten der Verwaltung mobiler Android-Geräte mit Configuration Manager und Intune  
 Mit den folgenden Schritten kann Configuration Manager Android-Geräte verwalten.  

#### <a name="to-enable-android-enrollment"></a>So aktivieren Sie die Android-Registrierung  

1.  **Voraussetzungen** ‒ Bevor Sie die Registrierung einer Plattform einrichten können, müssen Sie die Voraussetzungen und Schritte in [Einrichten der hybriden Verwaltung mobiler Geräte](setup-hybrid-mdm.md) erfüllen und ausführen.  

2.  Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Clouddienste** > **Microsoft Intune-Abonnement**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Abonnement** auf **Plattformen konfigurieren** > **Android**.  

4.  Wählen Sie im Dialogfeld **Eigenschaften von Microsoft Intune-Abonnement** die Registerkarte **Android** aus, und klicken Sie, um das Kontrollkästchen **Android-Registrierung aktivieren** zu aktivieren.  

 Nachdem Sie die Einrichtung abgeschlossen haben, müssen Sie Ihre Benutzer informieren, wie sie ihre Geräte registrieren sollen. Informationen hierzu finden Sie unter [Informieren der Benutzer über den Einsatz von Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Diese Informationen gelten für mobile Geräte, die mit Microsoft Intune und Configuration Manager verwaltet werden.



<!--HONumber=Nov16_HO1-->


