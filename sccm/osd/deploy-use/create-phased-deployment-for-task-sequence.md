---
title: Erstellen einer Bereitstellung in Phasen für eine Tasksequenz
titleSuffix: Configuration Manager
description: Erstellen von Bereitstellungen in Phasen für eine Tasksequenz
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2bda41cfd01e5ef90771350e650f68a27c3af6ed
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-phased-deployments-for-a-task-sequence-with-system-center-configuration-manager"></a>Bereitstellungen in Phasen für eine Tasksequenz mit System Center Configuration Manager erstellen

*Gilt für: System Center Configuration Manager (Current Branch)*

Bereitstellungen in Phasen automatisieren ein koordiniertes Rollout einer Tasksequenz in einer bestimmten Reihenfolge über mehrere Sammlungen hinweg. Sie können Bereitstellungen in Phasen mit einer von zwei Standardphasen erstellen oder mehrere Phasen manuell konfigurieren. Die Bereitstellung in Phasen von Tasksequenzen unterstützt keine PXE- oder Medieninstallation. 

>[!NOTE]
> Bereitstellungen in Phasen sind ein Vorabfeature, das in Configuration Manager 1802 eingeführt wurde. <!--1356837-->

## <a name="security-scope-and-log-file-information"></a>Sicherheitsbereich und Protokolldateiinformationen

**Sicherheitsbereich:**</br>
Von Bereitstellungen in Phasen erstellte Bereitstellungen können von niemandem angezeigt werden, für den nicht der Sicherheitsbereich **Alles** festgelegt ist.

**Protokolldateien:** </br>
SMS_PhasedDeployment.log

## <a name="create-a-default-two-phased-deployment-for-a-task-sequence"></a>Erstellen einer Bereitstellung in zwei Phasen für eine Tasksequenz

Gehen Sie folgendermaßen vor, um eine Bereitstellung in Phasen zu erstellen. 

1. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.

2. Klicken Sie mit der rechten Maustaste auf eine bereits vorhandene Tasksequenz, und klicken Sie auf **Create Phased Deployment** (Bereitstellung in Phasen). 

3. Vergeben Sie auf der Registerkarte **Allgemein** einen Namen für die Bereitstellung in Phasen, fügen Sie (optional)eine Beschreibung hinzu, und klicken Sie auf **Standardmäßige Bereitstellung in zwei Phasen automatisch erstellen**. 

4. Füllen Sie die Felder **Erste Sammlung** und **Zweite Sammlung** auf. Wählen Sie **Weiter** aus.

5. Wählen Sie in der Registerkarte **Einstellungen** für jede Einstellung des Zeitplans eine Option aus, und klicken Sie anschließend auf **Weiter**. 
    - **Criteria for success of the first phase** (Kriterien für den Erfolg der ersten Phase) 
        - **Deployment success percentage** (Erfolgsprozentsatz der Bereitstellung): Geben Sie den Prozentsatz der Geräte an, für die die Bereitstellung der ersten Phase erfolgreich abgeschlossen wurde. 
    - **Conditions for beginning second phase of deployment after success of the first phase** (Bedingungen für den Beginn der zweiten Phase nach erfolgreicher erster Phase) (eine Option auswählen):
        - **Automatically begin this phase after a deferral period (in days)** (Diese Phase nach einem Rückstellungszeitraum (in Tagen) automatisch starten): Legen Sie fest, wie viele Tage nach dem erfolgreichen Abschluss der ersten Phase die zweite beginnen soll. 
        - **Manually begin the second phase of deployment** (Die zweite Phase der Bereitstellung manuell starten): Die zweite Phase beginnt nicht automatisch nach dem erfolgreichen Abschluss der ersten. Legen Sie fest, dass es manuell gestartet wird. 
    - **Once a device is targeted, install the software** (Nachdem ein Gerät bestimmt wurde, installieren Sie die Software) (eine Option auswählen):
        - **As soon as possible** (So bald wie möglich): Hiermit wird festgelegt, dass die Software installiert wird, sobald ein Gerät bestimmt wird.
        - **Deadline time (relative to the time device is targeted)** (Fristzeitraum (von der Bestimmung des Geräts abhängig)): Legt den Zeitpunkt der Installation auf eine bestimmte Anzahl von Tagen nach der Bestimmung des Geräts fest. 

6. Klicken Sie auf der Registerkarte **Phasen** auf die ersten Phase und dann auf **Bearbeiten**.  Geben Sie für **Benutzerfreundlichkeit** z.B. **Benutzerbenachrichtigungen** und **Schreibfilterverarbeitung für Windows Embedded-Geräte** an. Klicken Sie auf **Übernehmen**.

7. Konfigurieren Sie die Einstellungen von **Verteilungspunkte** für die Phase auf der Registerkarte **Verteilungspunkte**. Klicken Sie auf **Übernehmen** und dann auf **OK**.        

8. Bearbeiten Sie auf der Registerkarte **Phasen** die zweite Phase für **Benutzerfreundlichkeit** und **Verteilungspunkte**. Klicken Sie auf **Übernehmen** und dann auf **OK**.

9. Bestätigen Sie Ihre Auswahl auf der Registerkarte **Übersicht**, und klicken Sie auf **Weiter**, um im Assistenten fortzufahren.

>[!WARNING]
>Bei Bereitstellungen in Phasen werden Sie nicht benachrichtigt, wenn die Bereitstellung einer Tasksequenz [mit einem hohem Risiko](/sccm/protect/understand/settings-to-manage-high-risk-deployments.md) verbunden ist. 


## <a name="suspend-and-resume-phases-or-move-to-the-next-phase"></a>Halten Sie Phasen an, und setzen Sie sie fort, oder gehen Sie zur nächsten Phase über.
In manchen Fällen müssen Sie manuell eine Bereitstellung in Phasen manuell anhalten oder fortsetzen oder manuell die nächste Phase einleiten. 

### <a name="move-to-the-next-phase"></a>Einleiten der nächsten Phase
Wenn Sie die Einstellung **Manually begin the second phase of deployment** (Zweite Phase der Bereitstellung manuell einleiten) auswählen, müssen Sie die zweite Phase auslösen. Mithilfe der folgenden Anleitung können Sie die nächste Phase einleiten: 

1. Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** aus, erweitern Sie **Betriebssysteme**, und klicken Sie anschließend auf **Tasksequenzen**.
2. Markieren Sie die Tasksequenz.
3. Klicken Sie unten in der Verwaltungskonsole auf die Registerkarte **Phased Deployment** (Bereitstellung in Phasen). 
4. Klicken Sie mit der rechten Maustaste auf die Bereitstellung in Phasen, und wählen Sie **Move to next phase** (Zur nächsten Phase übergehen) aus.
![Anhalten, fortsetzen oder einleiten einer Phase](media/Suspend-phased-deployment.PNG)

### <a name="suspend-or-resume-a-phased-deployment"></a>Anhalten oder fortsetzen einer Bereitstellung in Phasen
1. Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** aus, erweitern Sie **Betriebssysteme**, und klicken Sie anschließend auf **Tasksequenzen**.
2. Markieren Sie die Tasksequenz, und klicken Sie unten in der Verwaltungskonsole auf die Registerkarte **Phased Deployment** (Bereitstellung in Phasen). 
3. Wählen Sie die Bereitstellung in Phasen aus, und klicken Sie im Menüband auf **Anhalten** oder **Fortsetzen**.

## <a name="next-steps"></a>Nächste Schritte
[Erstellen einer benutzerdefinierten Tasksequenz](create-a-custom-task-sequence.md) </br>
[Erstellen einer Tasksequenz für Nicht-Betriebssystembereitstellungen mit System Center Configuration Manager](create-a-task-sequence-for-non-operating-system-deployments.md) 








