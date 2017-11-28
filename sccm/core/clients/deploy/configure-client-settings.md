---
title: Konfigurieren von Clienteinstellungen
titleSuffix: Configuration Manager
description: "Wählen Sie die Clienteinstellungen in System Center Configuration Manager aus."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: "5"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 20a8f91d10d98542f08e440bcfbc1a6f98a51932
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>Konfigurieren von Clienteinstellungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie verwalten alle Clienteinstellungen in System Center Configuration Manager über **Verwaltung** > **Clienteinstellungen**. Ändern Sie die Standardeinstellungen, um Einstellungen für alle Benutzer und Geräte in der Hierarchie zu konfigurieren, auf die keine benutzerdefinierten Einstellungen angewendet wurden. Wenn Sie abweichende Einstellungen nur auf bestimmte Benutzer oder Geräte anwenden möchten, stellen Sie benutzerdefinierte Einstellungen für Sammlungen bereit.  

Informationen zu den einzelnen Clienteinstellungen finden Sie unter [Informationen zu Clienteinstellungen in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).

> [!NOTE]  
>  Sie können außerdem Konfigurationselemente verwenden, um Clients zu verwalten und die Konfigurationskompatibilität von Geräten zu bewerten, nachzuverfolgen und wiederherzustellen. Weitere Informationen finden Sie unter [Sicherstellen der Gerätekompatibilität mit System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="configure-the-default-client-settings"></a>Konfigurieren der Clientstandardeinstellungen    

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** die Option **Eigenschaften** aus.  

4.  Zeigen Sie die Clienteinstellungen für jede Einstellungsgruppe im Navigationsbereich an, und konfigurieren Sie sie.  

 Die Clientcomputer werden beim nächsten Clientrichtliniendownload mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Richtlinienabrufs für einen einzelnen Client finden Sie unter [Initiieren des Richtlinienabrufs für einen Configuration Manager-Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [Verwalten von Clients in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="create-and-deploy-custom-client-settings"></a>Erstellen und Bereitstellen von benutzerdefinierten Clienteinstellungen  
Wenn Sie diese benutzerdefinierten Einstellungen bereitstellen, setzen sie die Clientstandardeinstellungen außer Kraft. Bevor Sie diese Schritte ausführen, vergewissern Sie sich, dass eine Sammlung mit den Benutzern oder Geräten vorhanden ist, für die diese benutzerdefinierten Clienteinstellungen erforderlich sind.  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Clienteinstellungen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Benutzerdefinierte Clienteinstellungen erstellen** und dann eine der folgenden Optionen aus:  

    -   **Benutzerdefinierte Geräteclienteinstellungen erstellen**  

    -   **Benutzerdefinierte Benutzerclienteinstellungen erstellen**  

4.  Geben Sie einen eindeutigen Namen und optional eine Beschreibung an.  

5.  Aktivieren Sie mindestens ein Kontrollkästchen, mit dem eine Gruppe von Einstellungen angezeigt wird.  

6.  Wählen Sie im Navigationsbereich jede Gruppe von Einstellungen aus, und konfigurieren Sie die verfügbaren Einstellungen. Klicken Sie anschließend auf **OK**.   

8.  Wählen Sie die erstellte benutzerdefinierte Clienteinstellung aus. Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Clienteinstellungen** die Option **Bereitstellen** aus.  

9. Wählen Sie im Dialogfeld **Sammlung auswählen** die entsprechende Sammlung aus, und klicken Sie dann auf **OK**. Klicken Sie im Detailbereich auf **Bereitstellungen** , um die ausgewählte Sammlung zu überprüfen.  

10. Zeigen Sie die Reihenfolge der neu erstellten benutzerdefinierten Clienteinstellung an. Wenn mehrere benutzerdefinierte Clienteinstellungen vorhanden sind, werden diese nach der Reihenfolgennummer angewendet. Bei Konflikten setzt die Einstellung mit der niedrigsten Reihenfolgennummer die anderen Einstellungen außer Kraft. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Clienteinstellungen** auf **Priorität erhöhen** oder **Priorität verringern**, um die Reihenfolgennummer zu ändern.  

 Die Clientcomputer werden beim nächsten Clientrichtliniendownload mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Richtlinienabrufs für einen einzelnen Client finden Sie unter [Initiieren des Richtlinienabrufs für einen Configuration Manager-Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [Verwalten von Clients in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

## <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Begrenzen der erweiterten Telemetrie von Windows 10, um nur wichtige Daten an Windows Analytics Device Health zu senden
<!-- 1356148 -->

Ab dem Update 1710 können Sie die Stufe der Windows 10-Telemetriedatensammlung auf **Enhanced (Limited)** (Erweitert [Begrenzt]) festlegen. Mit dieser Einstellung können Sie wertvolle Einblicke zu Geräten in Ihrer Umgebung gewinnen, ohne dass alle Daten in der Telemetriestufe **Enhanced** an Windows 10-Version 1709 oder höher berichtet werden.

Die Telemetriestufe „Enhanced (Limited)“ enthält grundlegende Metriken und eine Teilmenge von Daten, die auf der **erweiterten** Stufe in Windows Analytics gesammelt werden. Weitere Informationen zu Telemetriestufen finden Sie im Artikel zu [Telemetriestufen](https://docs.microsoft.com/windows/configuration/configure-windows-telemetry-in-your-organization#telemetry-levels).

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

2.  Wählen Sie auf der Registerkarte **Startseite** die Option **Eigenschaften** aus.  

3.  Öffnen Sie **Clouddienste**, und legen Sie die Windows 10-Telemetrie auf **Enhanced** (Erweitert) fest.

##  <a name="view-client-settings"></a>Anzeigen der Clienteinstellungen  
 Wenn dem gleichen Gerät oder Benutzer bzw. der gleichen Benutzergruppe Einstellungen für mehrere Clients bereitgestellt wurden, kann sich die Priorisierung und Kombination der Einstellungen zu einer komplexen Angelegenheit auswachsen. So zeigen Sie die Clienteinstellungen an  

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Kompatibilität** > **Geräte** > **Benutzer** oder **Gerätesammlungen** aus.  

3.  Wählen Sie erst ein Gerät, einen Benutzer oder eine Benutzergruppe und dann in der Gruppe **Clienteinstellungen** die Option **Resultierende Clienteinstellungen**aus.  

4.  Bei Auswahl einer Clienteinstellung im linken Fensterbereich werden die Einstellungen angezeigt. In dieser Ansicht sind die Einstellungen schreibgeschützt. 

    > [!NOTE]  
    >  Zum Anzeigen der Clienteinstellungen müssen Sie über Leseberechtigungen für die Clienteinstellungen verfügen.  

    