---
title: Windows Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Windows Defender Advanced Threat Protection, einen neuen Dienst, der Unternehmen dabei hilft, auf erweiterte Angriffe zu reagieren, verwalten und überwachen können.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 10d746f88d0e7b869e2b73d389944f3b382d687d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="windows-defender-advanced-threat-protection"></a>Windows Defender Advanced Threat Protection

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab Version 1606 von Configuration Manager (Current Branch) kann Endpoint Protection [Windows Defender Advanced Threat Protection (ATP)](http://aka.ms/technet-wdatp) verwalten und überwachen. Windows Defender ATP unterstützt Unternehmen dabei, erweiterte Angriffe auf ihre Netzwerke zu entdecken, zu untersuchen, und darauf zu reagieren.  Richtlinien von Configuration Manager oder Microsoft Intune können Sie dabei unterstützen, verwaltetes Windows 10, Version 1607, (Build 14328) oder höher zu integrieren und zu verwalten.

Windows Defender ATP ist ein Dienst im [Windows Defender Security Center](https://securitycenter.windows.com). Durch Hinzufügen und Bereitstellen einer Client-Onboardingkonfigurationsdatei kann Configuration Manager den Bereitstellungsstatus und die Windows Defender ATP-Agent-Integrität überwachen. Windows Defender ATP wird von Computern unterstützt, die den Konfigurations-Manager-Client ausführen oder von Microsoft Intune verwaltet werden, aber hybride, MDM-verwaltete Intune-Computer werden nicht unterstützt.

 **Voraussetzungen**  

-   Abonnement für den Windows Defender Advanced Threat Protection-Onlinedienst  
-   Clientcomputer unter Windows 10, Version 1607 und höher  
-   Clientcomputer, auf denen ein Client-Agent der Configuration Manager-Version 1610 oder höher ausgeführt wird oder die von Microsoft Intune verwaltet werden

## <a name="how-to-create-an-onboarding-configuration-file"></a>So erstellen Sie eine Onboardingkonfigurationsdatei  

 1.  Melden Sie sich am [Windows Defender ATP-Onlinedienst](https://securitycenter.windows.com/) an.   

 2.  Klicken Sie auf das Menüelement **Endpoint Management** (Endpunktverwaltung).  

 3.  Wählen Sie **System Center Configuration Manager (Current Branch) Version 1606** aus, und klicken Sie auf **Paket herunterladen**.  

 4.  Laden Sie die komprimierte Archiv-Datei (ZIP-Datei) herunter, und extrahieren Sie die Inhalte.

> [!IMPORTANT]
> Die Windows Defender ATP-Konfigurationsdatei enthält vertrauliche Informationen, die gesichert werden sollten.

## <a name="onboard-devices-for-windows-defender-atp"></a>Integrieren von Geräten für Windows Defender ATP  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität** > **Übersicht** > **Endpoint Protection** > **Windows Defender ATP-Richtlinien**, und klicken Sie auf **Windows Defender ATP-Richtlinie erstellen**. Der Assistent zum Erstellen von Windows Defender ATP-Richtlinien wird geöffnet.  

2.  Geben Sie den **Namen** und die **Beschreibung** für die Windows Defender ATP-Richtlinie ein, und wählen Sie **Onboarding** aus. Klicken Sie auf **Weiter**.  

3.  **Wechseln** Sie zu der Konfigurationsdatei, die Windows Defender ATP-Clouddienstmandanten Ihrer Organisation bereitstellt. Klicken Sie auf **Weiter**.  

4.  Geben Sie die Dateibeispiele an, die von verwalteten Geräten gesammelt und für Analysezwecke freigegeben werden.  

    -   **Keine**   

    -   **Alle Dateitypen**  

     Klicken Sie auf **Weiter**.  

5.  Überprüfen Sie die Zusammenfassung, und schließen Sie den Assistenten ab.  

6.  Sie können nun die Windows Defender ATP-Richtlinie für verwaltete Clientcomputer bereitstellen, indem Sie auf **Bereitstellen** klicken.  

## <a name="monitor-windows-defender-atp"></a>Überwachen von Windows Defender ATP  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Sicherheit**, und klicken Sie dann auf **Windows Defender ATP**.  

2.  Überprüfen Sie das Windows Defender Advanced Threat Protection-Dashboard.  

    -   **Windows Defender Agent Deployment Status** (Windows Defender-Agent-Bereitstellungsstatus) – Anzahl und Prozentsatz der geeigneten verwalteten Clientcomputer mit integrierter aktiver Windows Defender ATP-Richtlinie  

    -   **Integrität von Windows Defender ATP-Agent** – Prozentsatz von Computerclients, die den Status für ihren Windows Defender-ATP-Agent melden  

        -   **Integriert** – Funktioniert ordnungsgemäß  

        -   **Inaktiv** – In dem Zeitraum wurden keine Daten an den Dienst gesendet  

        -   **Agent-Status** – Der Systemdienst für den Agent in Windows wird nicht ausgeführt.  

        -   **Nicht integriert** – Die Richtlinie wurde angewendet, aber der Agent hat die Richtlinienintegration nicht gemeldet.  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>Erstellen und Bereitstellen einer Offboardingkonfigurationsdatei  

1.  Melden Sie sich am [Windows Defender ATP-Onlinedienst](https://securitycenter.windows.com/) an.   

2.  Klicken Sie auf das Menüelement **Endpoint Management** (Endpunktverwaltung).  

3.  Wählen Sie **System Center Configuration Manager (Current Branch) Version 1606** aus, und klicken Sie auf **Endpoint offboarding** (Endpunktoffboarding).  

4.  Laden Sie die komprimierte Archiv-Datei (ZIP-Datei) herunter, und extrahieren Sie die Inhalte. Offboardingdateien sind 30 Tage lang gültig.

5.  Wechseln Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität** > **Übersicht** > **Endpoint Protection** > **Windows Defender ATP-Richtlinien**, und klicken Sie auf **Windows Defender ATP-Richtlinie erstellen**. Der Assistent zum Erstellen von Windows Defender ATP-Richtlinien wird geöffnet.  

6.  Geben Sie den **Namen** und die **Beschreibung** für die Windows Defender ATP-Richtlinie ein, und wählen Sie **Offboarding** aus. Klicken Sie auf **Weiter**.  

7.  **Wechseln** Sie zu der Konfigurationsdatei, die Windows Defender ATP-Clouddienstmandanten Ihrer Organisation bereitstellt. Klicken Sie auf **Weiter**.  

8.  Überprüfen Sie die Zusammenfassung, und schließen Sie den Assistenten ab.  

9.  Sie können nun die Windows Defender ATP-Richtlinie für verwaltete Clientcomputer bereitstellen, indem Sie auf **Bereitstellen** klicken.  

> [!IMPORTANT]
> Die Windows Defender ATP-Konfigurationsdateien enthalten vertrauliche Informationen, die gesichert werden sollten.

[Windows Defender Advanced Threat Protection](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Beheben von Onboardingproblemen mit Windows Defender Advanced Threat Protection](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)
