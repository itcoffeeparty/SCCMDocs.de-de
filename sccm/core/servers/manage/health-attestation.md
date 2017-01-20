---
title: "Integritätsnachweis | Microsoft-Dokumentation"
description: "Erfahren Sie mehr zum Integritätsnachweis, der in der Configuration Manager-Konsole angezeigt werden kann."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: 17
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 937a168f79168b3e3a3a578513814abb2b368d9f


---
# <a name="health-attestation-for-system-center-configuration-manager"></a>Integritätsnachweis für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab System Center Configuration Manager Current Branch Version 1602 können Administratoren den Status des [Windows 10-Nachweises zur Geräteintegrität](https://technet.microsoft.com/library/mt592023.aspx) in der Configuration Manager-Konsole anzeigen.  Diese Funktion ist für PCs und lokale Ressourcen verfügbar, die von Configuration Manager verwaltet werden sowie für mobile Geräte, die von Microsoft Intune verwaltet werden. Administratoren können angeben, ob die Berichterstellung über die Cloud oder über die lokale Infrastruktur durchgeführt wird. Dadurch können Client-PCs ohne Internetzugriff mithilfe des Integritätsnachweises Geräte aktivieren und verwalten. Mit dem Nachweis der Geräteintegrität kann der Administrator sicherstellen, dass Clientcomputer über die folgenden aktivierten vertrauenswürdigen BIOS-, TPM- und Startsoftwarekonfigurationen verfügen:  

-   Antischadsoftware-Frühstart – Antischadsoftware-Frühstart (Early Launch Anti-Malware, ELAM) schützt Ihren Computer beim Starten und bevor Drittanbietertreiber initialisiert werden. [Informationen zum Aktivieren von ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  

-   BitLocker – Mit der Windows-BitLocker-Laufwerkverschlüsselungs-Software können Sie alle Daten verschlüsseln, die auf dem Windows-Betriebssystemvolume gespeichert sind.  [Informationen zum Aktivieren von Bitlocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  

-   Sicherer Start – Sicherer Start ist ein Sicherheitsstandard, der von Mitgliedern der PC-Industrie entwickelt wurde, um sicherzustellen, dass Ihr PC nur mit Software startet, die der PC-Hersteller als vertrauenswürdig eingestuft hat. [Weitere Informationen zu Sicherer Start](https://technet.microsoft.com/library/hh824987.aspx)  

-   Codeintegrität – Codeintegrität ist ein Feature, das die Sicherheit des Betriebssystems verbessert, indem es die Integrität einer Treiber- oder Systemdatei jedes Mal überprüft, wenn sie in den Arbeitsspeicher geladen wird. [Erfahren Sie mehr über Codeintegrität](https://technet.microsoft.com/library/dd348642.aspx)  



##  <a name="device-health-attestation"></a>Nachweis der Geräteintegrität  
 Der Configuration Manager-Geräteintegritätsnachweis zeigt Folgendes an:  

-   **Integritätsnachweisstatus** – Zeigt die Anteile der Geräte in kompatiblem, nicht kompatiblem, Fehler- und unbekanntem Status an  

-   **Geräte mit Health Attestation-Unterstützung** – Zeigt den Prozentsatz der Geräte an, die den Integritätsnachweisstatus berichten  

-   **Nicht kompatible Geräte nach Clienttyp** – Zeigt den Anteil an mobilen Geräten und Computern an, die nicht kompatibel sind  

-   **Wichtigste fehlende Integritätsnachweiseinstellungen** – Zeigt nach Einstellungen gelistet die Anzahl von Geräte an, für die die Health Attestation-Einstellung fehlt  

 **Anforderungen:**  

-   Clientgeräte, auf denen Win10 ausgeführt wird  

-   Windows Server 2016 Technical Preview 5 mit [Nachweis zur Geräteintegrität aktiviert](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation)

-    TPM 2-aktiviert  

-   Zulassen der Kommunikation zwischen dem Configuration Manager-Client-Agent und dem „has.spserv.microsoft.com“ (Port 443) Health Attestation-Dienst

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Aktivieren der Kommunikation mit dem Integritätsnachweisdienst auf Configuration Manager-Clientcomputern  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Übersicht** > **Clienteinstellungen**aus.  Wählen Sie die Registerkarte für **Computer-Agent** -Einstellungen aus.  

2.  Wählen Sie im Dialogfeld **Standardeinstellungen**  **Computer-Agent** aus, und scrollen Sie nach unten zu **Kommunikation mit Integritätsnachweisdienst aktivieren**.  

3.  Legen Sie **Kommunikation mit Integritätsnachweisdienst aktivieren** auf **Ja**fest, und klicken Sie anschließend auf **OK**.  

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Aktivieren der lokalen Kommunikation mit dem Integritätsnachweisdienst auf Configuration Manager-Clientcomputern


1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Clienteinstellungen**, und legen Sie anschließend **Lokalen Integritätsnachweisdienst verwenden** auf **Ja**fest.


2. Geben Sie die **URL für lokalen Integritätsnachweisdienst**an, und klicken Sie anschließend auf **OK**.

## <a name="how-to-view-health-attestation"></a>Anzeigen des Integritätsnachweises  


1.  Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung** , klicken Sie auf den Knoten **Sicherheit** und anschließend auf **Integritätsnachweis**, um den Nachweis der Geräteintegrität anzuzeigen.  

2.  Der Nachweis der Geräteintegrität wird angezeigt.  

 Der Status des Nachweises der Clientgeräteintegrität kann verwendet werden, um in Kompatibilitätsrichtlinien für Geräte, die von Configuration Manager mit Microsoft Intune verwaltet werden, Regeln für den bedingten Zugriff zu definieren. Weitere Informationen finden Sie unter [Verwalten von Kompatibilitätsrichtlinien für Geräte in System Center Configuration Manager](/sccm/protect/deploy-use/device-compliance-policies).  



<!--HONumber=Dec16_HO3-->


