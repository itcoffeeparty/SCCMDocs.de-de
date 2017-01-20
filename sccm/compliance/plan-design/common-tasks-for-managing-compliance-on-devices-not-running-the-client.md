---
title: "Allgemeine Aufgaben zur Verwaltung der Konformität auf Geräten, auf denen der System Center Configuration Manager-Client nicht ausgeführt wird | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über System Center Configuration Manager-Kompatibilitätseinstellungen, indem Sie einige Szenarios durcharbeiten."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 116cca2a-0a98-43fd-ac9e-e3daeddefce3
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9e939d871e95a3248d8e5d96cb73063a81fd5cf
ms.openlocfilehash: e24ef149e2a2648c9a7acaedfaa8f0b5bb173ab3


---
# <a name="common-tasks-for-managing-compliance-on-devices-not-running-the-system-center-configuration-manager-client"></a>Allgemeine Aufgaben zur Verwaltung der Kompatibilität auf Geräten, auf denen der System Center Configuration Manager-Client nicht ausgeführt wird

*Gilt für: System Center Configuration Manager (Current Branch)*

Diese Szenarios dienen zur Einführung in das Verwenden von System Center Configuration Manager-Kompatibilitätseinstellungen.  

 Wenn Sie bereits mit Kompatibilitätseinstellungen vertraut sind, finden Sie eine ausführliche Dokumentation zu allen verwendbaren Funktionen im Abschnitt [Configuration items for devices managed without the System Center Configuration Manager client (Konfigurationselemente für Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden)](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md).  

 Bevor Sie beginnen, lesen Sie [Get started with compliance settings in System Center Configuration Manager (Erste Schritte mit Kompatibilitätseinstellungen in System Center Configuration Manager)](../../compliance/get-started/get-started-with-compliance-settings.md), um einige Grundlagen der Kompatibilitätseinstellungen zu erfahren, und lesen Sie zudem [Plan for and configure compliance settings in System Center Configuration Manager (Planen und Konfigurieren von Kompatibilitätseinstellungen in System Center Configuration Manager)](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

## <a name="general-information-for-each-scenario"></a>Allgemeine Informationen für jedes Szenario  
 In jedem Szenario erstellen Sie ein Konfigurationselement, das eine bestimmte Aufgabe ausführt. Öffnen Sie den Assistenten zum Erstellen von Konfigurationselementen, und führen Sie die folgenden Schritte aus:  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationselemente**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  

4.  Geben Sie auf der Registerkarte **Allgemein** des nachstehend gezeigten Assistenten zum Erstellen von Konfigurationselementen einen Namen und eine Beschreibung des Konfigurationselements an. Wählen Sie dann den für jedes Szenario geeigneten Konfigurationselementtyp.  

     ![Zeigt die Seite „Allgemein“ des Assistenten zum Erstellen von Konfigurationselementen](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-81-and-windows-10-devices-managed-without-the-configuration-manager-client"></a>Szenarien für Windows 8.1- und Windows 10-Geräte, die ohne den Configuration Manager-Client verwaltet werden  

### <a name="scenario-restrict-access-to-the-app-store-on-all-windows-pcs"></a>Szenario: Einschränken des Zugriffs auf den App Store auf allen Windows-PCs  
 In diesem Szenario sind Sie der IT-Administrator eines Unternehmens, das mit hochsensiblen Daten arbeitet. Aus diesem Grund schränken Sie die Apps ein, die Benutzer installieren dürfen. Sie möchten, dass Benutzer aller Windows 10-PCs keine Apps mehr aus dem Windows Store herunterladen können. Deshalb führen Sie die folgenden Schritte aus.  

#### <a name="steps"></a>Schritte  

1.  Wählen Sie im Assistenten zum Erstellen von Konfigurationselementen auf der Seite **Allgemein** den Konfigurationselementtyp **Windows 8.1 und Windows 10** aus, und klicken Sie auf **Weiter**.  

2.  Wählen Sie auf der Seite **Unterstützte Plattformen** alle Windows 10-Plattformen aus.  

3.  Wählen Sie auf der Seite **Geräteeinstellungen** die Option **Store**aus, und klicken Sie dann auf **Weiter**.  

4.  Wählen Sie auf der Seite **Store** die Option **Nicht zulässig** als Einstellung für **App Store**aus.  

5.  Wählen Sie **Nicht kompatible Einstellungen wiederherstellen** aus, um sicherzustellen, dass die Änderung auf alle PCs angewendet wird.  

6.  Schließen Sie den Assistenten ab, um das neue Konfigurationselement zu erstellen.  

 Sie können nun die Informationen im Thema [Common tasks for creating and deploying configuration baselines with System Center Configuration Manager (Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines mit System Center Configuration Manager)](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) verwenden, die Ihnen beim Bereitstellen der von Ihnen erstellten Konfiguration auf Geräten helfen.  

## <a name="scenarios-for-windows-phone-devices-managed-without-the-configuration-manager-client"></a>Szenarien für Windows Phone-Geräte, die ohne den Configuration Manager-Client verwaltet werden  

### <a name="scenario-disable-the-use-of-screen-capture-on-a-windows-phone"></a>Szenario: Deaktivieren von Bildschirmaufnahmen auf einem Windows Phone  
 In diesem Szenario werden in Ihrem Unternehmen Windows Phone 8.1-Geräte verwendet. Auf diesen Geräten läuft eine Vertriebs-App, die vertrauliche Informationen enthält. Zum Schutz Ihres Unternehmens möchten Sie Bildschirmaufnahmen auf dem Gerät deaktivieren, die potenziell dazu genutzt werden können, um vertrauliche Informationen aus Ihrem Unternehmen zu schmuggeln.  

1.  Wählen Sie im Assistenten zum Erstellen von Konfigurationselementen auf der Seite **Allgemein** den Konfigurationselementtyp **Windows Phone** aus, und klicken Sie auf **Weiter**.  

2.  Wählen Sie auf der Seite **Unterstützte Plattformen** **Alle Windows 8.1-Plattformen** aus.  

3.  Wählen Sie auf der Seite **Geräteeinstellungen** die Option **Gerät**aus, und klicken Sie dann auf **Weiter**.  

4.  Wählen Sie auf der Seite **Gerät** die Option **Deaktiviert** als Einstellung für **Bildschirmaufnahme**aus.  

5.  Wählen Sie **Nicht kompatible Einstellungen wiederherstellen** aus, um sicherzustellen, dass die Änderung auf alle Windows Phone 8.1-Geräte angewendet wird.  

6.  Schließen Sie den Assistenten ab, um das neue Konfigurationselement zu erstellen.  

 Sie können nun die Informationen im Thema [Common tasks for creating and deploying configuration baselines with System Center Configuration Manager (Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines System Center Configuration Manager)](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) verwenden, die Ihnen beim Bereitstellen der von Ihnen erstellten Konfiguration auf Geräten helfen.  

## <a name="scenarios-for-ios-and-mac-os-x-devices-managed-without-the-configuration-manager-client"></a>Szenarien für iOS- und Mac OS X-Geräte, die ohne den Configuration Manager-Client verwaltet werden  

### <a name="scenario-disable-the-camera-on-ios-devices"></a>Szenario: Deaktivieren der Kamera auf iOS-Geräten  
 In diesem Szenario erzeugt Ihr Unternehmen Pläne für neue Produktentwicklungen mit vertraulichen Informationen, die geheim bleiben müssen. Da Ihr Unternehmen allen Mitarbeitern iPhones oder iPads zur Verfügung stellt, möchten Sie die Kamera auf diesen Geräten deaktivieren, um zu verhindern, dass die Pläne fotografiert werden.  

1.  Wählen Sie im Assistenten zum Erstellen von Konfigurationselementen auf der Seite **Allgemein** den Konfigurationselementtyp **iOS und Mac OS X** aus, und klicken Sie auf **Weiter**.  

2.  Wählen Sie auf der Seite **Unterstützte Plattformen** alle iPhone- und iPad-Geräteplattformen aus.  

3.  Wählen Sie auf der Seite **Geräteeinstellungen** die Option **Sicherheit**aus, und klicken Sie dann auf **Weiter**.  

4.  Wählen Sie auf der Seite **Sicherheit** die Option **Nicht zulässig** als Einstellung für **Kamera**aus.  

5.  Wählen Sie **Nicht kompatible Einstellungen wiederherstellen** aus, um sicherzustellen, dass die Änderung auf alle iOS-Geräte angewendet wird.  

6.  Schließen Sie den Assistenten ab, um das neue Konfigurationselement zu erstellen.  

 Sie können nun die Informationen im Thema [Common tasks for creating and deploying configuration baselines with System Center Configuration Manager (Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines System Center Configuration Manager)](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) verwenden, die Ihnen beim Bereitstellen der von Ihnen erstellten Konfiguration auf Geräten helfen.  

## <a name="scenarios-for-android-and-samsung-knox-standard-devices-managed-without-the-configuration-manager-client"></a>Szenarios für Android- und Samsung KNOX Standard-Geräte, die ohne Configuration Manager-Client verwaltet werden  

### <a name="scenario-require-a-password-on-all-android-5-devices"></a>Szenario: Anfordern eines Kennworts auf allen Android 5-Geräten  
 In diesem Szenario erstellen Sie ein Konfigurationselement nur für Android 5-Geräte, das Benutzern auffordert, auf ihren Geräten ein Kennwort mit mindestens 6 Zeichen zu konfigurieren. Wenn ein Benutzer zudem fünfmal ein falsches Kennwort eingibt, wird das Gerät zurückgesetzt.  

1.  Wählen Sie im Assistenten zum Erstellen von Konfigurationselementen auf der Seite **Allgemein** den Konfigurationselementtyp **Android und Samsung KNOX** aus, und klicken Sie auf **Weiter**.  

2.  Wählen Sie auf der Seite **Unterstützte Plattformen** nur **Android 5** aus (um sicherzustellen, dass die Einstellungen nur für diese Plattform gelten).  

3.  Wählen Sie auf der Seite **Geräteeinstellungen** die Option **Kennwort**aus, und klicken Sie dann auf **Weiter**.  

4.  Konfigurieren Sie auf der Seite **Kennwort** die folgenden Einstellungen:  

    -   **Kennworteinstellungen auf Geräten erforderlich** > **Erforderlich**  

    -   **Minimale Kennwortlänge (Zeichen)** > **6**  

    -   **Anzahl der gescheiterten Anmeldeversuche vor dem Zurücksetzen eines Geräts** > **5**  

5.  Schließen Sie den Assistenten ab, um das neue Konfigurationselement zu erstellen.  

 Sie können nun die Informationen im Thema [Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) verwenden, die Ihnen beim Bereitstellen der von Ihnen erstellten Konfiguration auf Geräten helfen.  



<!--HONumber=Dec16_HO3-->


