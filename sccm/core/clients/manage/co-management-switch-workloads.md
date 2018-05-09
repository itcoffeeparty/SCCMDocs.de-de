---
title: Verschieben von Configuration Manager-Workloads zu Intune
titleSuffix: Configuraton Manager
description: Erfahren Sie, wie Sie Workloads, die derzeit von Configuration Manager verwaltet werden, zu Microsoft Intune verschieben.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 439e4e26c08b5a2710da0978ed2407d715bc86bd
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Verschieben von Configuration Manager-Workloads zu Intune
In [Vorbereiten von Windows 10-Geräten für die Co-Verwaltung](co-management-prepare.md) haben Sie Windows 10-Geräte für die Co-Verwaltung vorbereitet. Diese Geräte sind in AD und Azure AD eingebunden, bei Intune registriert und verwenden den Configuration Manager-Client. Wahrscheinlich sind aber noch nicht alle Ihrer Windows 10-Geräte, die in AD eingebunden und mit dem Configuration Manager-Client versehen sind, auch in Azure AD eingebunden oder bei Intune registriert. Das folgende Verfahren enthält eine Anleitung für die Aktivierung der Co-Verwaltung und die Vorbereitung Ihrer restlichen Windows 10-Geräte (Configuration Manager-Clients ohne Intune-Registrierung) für die Co-Verwaltung. Außerdem können Sie damit beginnen, bestimmte Configuration Manager-Workloads zu Intune zu verschieben.

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-management** (Co-Verwaltung).    
2. Klicken Sie auf der Registerkarte „Startseite“ in der Gruppe „Verwalten“ auf  **Co-Verwaltung konfigurieren**, um den Konfigurations-Assistenten für die Co-Verwaltung zu öffnen.    
3. Klicken Sie auf der Seite „Subscriptions“ (Abonnement) auf **Sign In** (Anmelden), melden Sie sich bei Ihrem Intune-Mandanten an, und klicken Sie dann auf **Next** (Weiter).   
4. Wählen Sie auf der Seite „Enablement“ (Aktivierung) **Pilot** oder **All** (Alle), um die automatische Registrierung bei Intune zu aktivieren, und klicken Sie dann auf **Next** (Weiter). Wenn Sie **Pilot** auswählen, werden nur die Configuration Manager-Clients aus der Gruppe „Pilotprojekt“ automatisch bei Intune registriert. Mit dieser Option können Sie für einen Teil der Clients die Co-Verwaltung aktivieren, um diese zu testen und einen Rollout in Phasen vorzunehmen. Die Befehlszeile kann verwendet werden, um den Configuration Manager-Client als App in Intune für Geräte bereitzustellen, die bereits bei Intune registriert sind. Weitere Informationen finden Sie unter [Bei Intune registrierte Windows 10-Geräte](co-management-prepare.md#windows-10-devices-enrolled-in-intune).
5. Wählen Sie auf der Seite „Workloads“ aus, ob Configuration Manager-Workloads von „Pilot Intune“ oder „Intune“ verwaltet werden sollen, und klicken Sie dann auf **Next** (Weiter). Die Einstellung **Pilot Intune** schaltet die zugehörige Workload nur für die Geräte in der Pilotgruppe um. Die Einstellung **Intune** schaltet die zugehörige Workload für alle Windows 10-Geräte mit Co-Verwaltung um. 
        
   > [!Important]    
   > Bevor Sie Workloads umschalten, vergewissern Sie sich, dass der entsprechende Workload in Intune ordnungsgemäß konfiguriert und bereitgestellt wurde. Auf diese Weise wird sichergestellt, dass Workloads immer von einem der Verwaltungstools für Ihre Geräte verwaltet werden.   
1. Konfigurieren Sie auf der Seite „Staging“ (Bereitstellung) die folgenden Einstellungen, und klicken Sie dann auf **Next** (Weiter):
    - **Pilot**: Die Pilotgruppe enthält eine oder mehrere Sammlungen, die Sie auswählen. Verwenden Sie diese Gruppe im Rahmen des Rollouts der Co-Verwaltung in mehreren Phasen. Sie können mit einer kleinen Testsammlung beginnen und der Pilotgruppe nach und nach weitere Sammlungen hinzufügen, während Sie die Co-Verwaltung für weitere Benutzer und Geräte ausrollen. Die Sammlungen in der Pilotgruppe lassen sich jederzeit in den Einstellungen der Co-Verwaltung ändern.
    - **Produktion**: Konfigurieren Sie die **Ausschlussgruppe** mit mindestens einer Sammlung. Geräte, die einer der Sammlungen in dieser Gruppe angehören, werden von der Co-Verwaltung ausgeschlossen. 
2. Schließen Sie den Assistenten, um die Co-Verwaltung zu aktivieren.  

## <a name="modify-your-co-management-settings"></a>Ändern der Co-Verwaltungseinstellungen
Nachdem Sie die Co-Verwaltung mithilfe des Assistenten aktiviert haben, können Sie die Einstellungen in den Eigenschaften der Co-Verwaltung ändern.  
- Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-management** (Co-Verwaltung).  
Wählen Sie das entsprechende Co-Verwaltungsobjekt aus, und klicken Sie dann auf der Registerkarte „Home“ (Startseite) auf **Properties** (Eigenschaften). 

## <a name="workloads-able-to-be-transitioned-to-intune"></a>Auf Intune umstellbare Workloads
Bestimmte Workloads können auf Intune umgestellt werden. Die folgende Liste wird kontinuierlich um die neuesten Workloads ergänzt, die auf Intune umgestellt werden können:
1. Konformitätsrichtlinien für Geräte
2. Ressourcenzugriffsrichtlinien: Mit Ressourcenzugriffsrichtlinien werden VPN-, WLAN, E-Mail- und Zertifikateinstellungen auf Geräten konfiguriert. Weitere Informationen finden Sie unter [Bereitstellen von Ressourcenzugriffsprofilen](https://docs.microsoft.com/intune/device-profiles).
      - E-Mail-Profil
      - WLAN-Profil
      - VPN-Profil
      - Zertifikatprofil
3. Windows Update-Richtlinien
4. Endpoint Protection (ab Configuration Manager Version 1802)
      - Windows Defender Application Guard
      - Windows Defender Firewall
      - Windows Defender-SmartScreen
      - Windows-Verschlüsselung
      - Windows Defender Exploit Guard
      - Windows Defender Application Control
      - Windows Defender Security Center
      - Windows Defender Advanced Threat Protection



## <a name="monitor-co-management"></a>Überwachen der Co-Verwaltung
Nachdem Sie die Co-Verwaltung aktiviert haben, können Sie der Co-Verwaltung unterliegende Geräte mithilfe der folgenden Methoden überwachen:

- [Das Dashboard für die Co-Verwaltung](/sccm/core/clients/manage/co-management-dashboard)
- **SQL-Sicht und WMI-Klasse**: Sie können die SQL-Sicht **v&#95;ClientCoManagementState** in der Configuration Manager-Standortdatenbank oder die WMI-Klasse **SMS&#95;Client&#95;ComanagementState** abfragen. Anhand der Informationen in der WMI-Klasse können Sie in Configuration Manager benutzerdefinierte Sammlungen erstellen, um den Bereitstellungsstatus Ihrer Co-Verwaltung zu ermitteln. Weitere Informationen finden Sie unter [Erstellen von Sammlungen in System Center Configuration Manager](/sccm/core/clients/manage/collections/create-collections). Die folgenden Felder sind in der SQL-Sicht und WMI-Klasse verfügbar: 
    - **MachineId**: Gibt eine eindeutige Geräte-ID für den Configuration Manager-Client an.
    - **MDMEnrolled**: Gibt an, ob das Gerät bei MDM registriert ist. 
    - **Autorität**: Gibt die Autorität an, für die das Gerät registriert ist.
    - **ComgmtPolicyPresent**: Gibt an, ob die Configuration Manager-Co-Verwaltungsrichtlinie auf dem Client vorhanden ist. Wenn **MDMEnrolled** den Wert **0** hat, erfolgt für das Gerät keine Co-Verwaltung, und zwar unabhängig davon, ob die Co-Verwaltungsrichtlinie auf dem Client vorhanden ist.

   > [!Note]    
   > Ein Gerät unterliegt der Co-Verwaltung, wenn die Felder **MDMEnrolled** und **ComgmtPolicyPresent** den Wert **1** haben.

- **Bereitstellungsrichtlinien:** Es gibt zwei Richtlinien, die unter **Überwachung** > **Bereitstellungen** erstellt werden: eine Richtlinie für die Pilotgruppe und eine für die Produktion. Diese Richtlinien melden nur die Anzahl der Geräte, auf die Configuration Manager die Richtlinie angewendet hat. Dabei wird nicht berücksichtigt, wie viele Geräte bei Intune registriert sind, was eine Voraussetzung dafür ist, dass eine Co-Verwaltung von Geräten möglich ist.  

## <a name="check-compliance-for-co-managed-devices"></a>Überprüfen der Konformität von Geräten unter Co-Verwaltung
Benutzer können die Konformität ihrer Windows 10-Geräte mit Co-Verwaltung im Softwarecenter sogar dann überprüfen, wenn der bedingte Zugriff von Configuration Manager oder Intune verwaltet wird. Benutzer können auch die Konformität überprüfen, indem sie die Unternehmensportal-App verwenden, wenn der bedingte Zugriff von Intune verwaltet wird.

## <a name="next-steps"></a>Nächste Schritte
Verwenden Sie die folgenden Ressourcen, um die Workloads zu verwalten, die Sie auf Intune umstellen:
- [Kompatibilitätsrichtlinie für Geräte](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Ressourcenzugriffsrichtlinien](https://docs.microsoft.com/intune/device-profiles)
- [Windows Update for Business-Richtlinien](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Endpoint Protection für Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)
