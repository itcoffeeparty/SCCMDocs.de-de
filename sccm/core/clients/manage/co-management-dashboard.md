---
title: Dashboard für die Co-Verwaltung
titleSuffix: Configuraton Manager
description: Abrufen von Informationen zur Co-Verwaltung mit dem Dashboard
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cdf073aa3e9ca3be6062ea0e5e0528bb97937989
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="co-management-dashboard-in-system-center-configuration-manager"></a>Dashboard für die Co-Verwaltung in System Center Configuration Manager
*Gilt für: System Center Configuration Manager (Current Branch)*

Ab Version 1802 können Sie ein Dashboard mit Informationen zur Co-Verwaltung aufrufen. Mithilfe des Dashboards können Sie die Computer überprüfen, die in Ihrer Umgebung gemeinsam verwaltet werden. Mit den Diagrammen lassen sich Geräte identifizieren, bei denen möglicherweise ein Eingriff erforderlich ist.<!--1356648-->

## <a name="open-the-co-management-dashboard"></a>Öffnen des Dashboards für die Co-Verwaltung
Gehen Sie folgendermaßen vor, um das Dashboard für die Co-Verwaltung zu öffnen: 

1. Öffnen Sie die Configuration Manager-Konsole. 
2. Klicken Sie auf den Knoten **Überwachung**. 
3. Klicken Sie auf **Co-Verwaltung**, um das Dashboard zu laden.

## <a name="reviewing-information-in-the-co-management-dashboard"></a>Abrufen von Informationen im Dashboard für die Co-Verwaltung

Im Dashboard für die Co-Verwaltung werden vier Diagramme für Ihre Umgebung angezeigt: 

- **Gemeinsam verwaltete Geräte:** Prozentsatz der gemeinsam verwalteten Geräte in Ihrer gesamten Umgebung

    ![Diagramm „Gemeinsam verwaltete Geräte“](media\co-management-dashboard\Percent-Co-managed-graph.PNG)

- **Clientbetriebssystemverteilung:** Anzahl der Clientgeräte pro Betriebssystem nach Version Die folgenden Gruppierungen werden verwendet: </br>
    - Windows 7 und 8.x
    - Windows 10 niedriger als 1709
    - Windows 10 1709 und höher

         > [!NOTE] 
         > Voraussetzung für die Co-Verwaltung ist die Version 1709 oder höher von Windows 10.

     Wenn Sie mit dem Mauszeiger auf einen Diagrammabschnitt zeigen, wird die Prozentzahl der Geräte angezeigt, die zur ausgewählten Betriebssystemgruppierung gehören.

     ![Diagramm „Clientbetriebssystemverteilung“](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)

- **Co-Verwaltungsstatus:** Aufschlüsselung nach erfolgreichen und fehlgeschlagenen Gerätevorgängen für die folgenden Kategorien:
    - Erfolgreich, in Hybrid-Azure AD eingebunden
    - Erfolgreich, in Azure AD eingebunden
    - Fehler: automatische Registrierung fehlgeschlagen
    
     Wenn Sie mit dem Mauszeiger auf einen Diagrammabschnitt zeigen, wird die Prozentzahl der Geräte angezeigt, die zur jeweiligen Kategorie gehören. 

     ![Diagramm „Co-Verwaltungsstatus“](media\co-management-dashboard\Co-management-status-graph.PNG)

     Wenn Sie auf einen Diagrammabschnitt klicken, wird die Geräteliste für die Kategorie aufgerufen.
 
     ![Liste für Geräte, bei denen die Registrierung fehlgeschlagen ist](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


- **Workloadübergang:** Balkendiagramm mit der Anzahl der Geräte, die Sie für die folgenden vier verfügbaren Workloads zu Microsoft Intune übertragen haben:
    - Kompatibilitätsrichtlinien
    - Ressourcenzugriff
    - Windows Update for Business
    - Endpoint Protection

     Wenn Sie mit dem Mauszeiger auf einen Diagrammabschnitt zeigen, wird die Anzahl der übertragenen Geräte für die Workload angezeigt. 
     ![Balkendiagramm „Workloadübergang“](media\co-management-dashboard\Workload-Transition.PNG)


## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Co-Verwaltung finden Sie unter:
 - [Co-Verwaltung für Windows 10-Geräte](/sccm/core/clients/manage/co-management-overview.md)
 - [Vorbereiten von Windows 10-Geräten für die Co-Verwaltung](/sccm/core/clients/manage/co-management-prepare.md)

    
