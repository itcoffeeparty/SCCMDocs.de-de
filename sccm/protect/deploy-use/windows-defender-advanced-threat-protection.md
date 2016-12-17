---
title: Windows Defender Advanced Threat Protection | System Center Configuration Manager
description: "Erfahren Sie, wie Sie Windows Defender Advanced Threat Protection, einen neuen Dienst, der Unternehmen dabei hilft, auf erweiterte Angriffe zu reagieren, verwalten und überwachen können."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: a4ad2d93ecd994fff00dab33084a734252cac651

---
# <a name="windows-defender-advanced-threat-protection"></a>Windows Defender Advanced Threat Protection

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab Version 1606 von Configuration Manager (Current Branch) kann Endpoint Protection Windows Defender Advanced Threat Protection (ATP) verwalten und überwachen. Windows Defender ATP ist ein neuer Dienst, der Unternehmen dabei unterstützt, erweiterte Angriffe auf ihre Netzwerke zu entdecken, zu untersuchen, und darauf zu reagieren.  Weitere Informationen finden Sie unter [Windows Defender ATP](http://aka.ms/technet-wdatp). Richtlinien von Configuration Manager können Sie dabei unterstützen, verwaltetes Windows 10, Version 1607, (Build 14328) oder höher zu integrieren und zu verwalten.

Windows Defender ATP ist ein Dienst im [Windows-Sicherheitscenter](https://securitycenter.windows.com). Durch Hinzufügen und Bereitstellen einer Client-Onboardingkonfigurationsdatei kann Configuration Manager den Bereitstellungsstatus und die Windows Defender ATP-Agent-Integrität überwachen. Windows Defender ATP wird nur auf PCs mit Configuration Manager-Client unterstützt. Die lokale Verwaltung von Mobilgeräten und Computer, die mithilfe der hybriden Verwaltung mobiler Geräte verwaltet werden, werden nicht unterstützt.

 **Voraussetzungen**  

-   Abonnement für den Onlinedienst Windows Defender Advanced Threat Protection  

-   Clients unter Windows 10, Version 1607 und höher  

## <a name="how-to-create-an-onboarding-configuration-file"></a>So erstellen Sie eine Onboardingkonfigurationsdatei  

 1.  Melden Sie sich am [Windows Defender ATP-Onlinedienst](https://securitycenter.windows.com/) an.   

 2.  Klicken Sie auf das Menüelement **Client On-boarding** (Clientonboarding).  

 3.  Wählen Sie **System Center Configuration Manager** aus, und klicken Sie auf **Paket herunterladen**.  

 4.  Laden Sie die komprimierte Archivdatei (.zip-Datei) herunter, und extrahieren Sie den Inhalt.

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



<!--HONumber=Nov16_HO1-->

