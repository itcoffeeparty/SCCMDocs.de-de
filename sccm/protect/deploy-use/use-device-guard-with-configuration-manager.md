---
title: Verwalten von Windows Device Guard | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Windows Device Guard mit System Center Configuration Manager verwalten.
ms.custom: na
ms.date: 04/14/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: 13
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 49599f529bb409f40caf9057989762e759f1c0ac
ms.openlocfilehash: 113dddb2939fedf24e8d489ff4443bd5e3e72c65
ms.contentlocale: de-de
ms.lasthandoff: 05/17/2017


---


# <a name="device-guard-management-with-configuration-manager"></a>Device Guard-Verwaltung mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

## <a name="introduction"></a>Einführung
Windows Device Guard besteht aus einer Gruppe von Windows 10-Features, die dazu entwickelt wurden, PCs vor Schadsoftware und anderer nicht vertrauenswürdiger Software zu schützen. Device Guard verhindert die Ausführung von Schadcode, indem sichergestellt wird, dass nur genehmigter bekannter Code ausgeführt werden kann.

Device Guard umfasst hardware- und softwarebasierte Sicherheitsfunktionen. Konfigurierbare Codeintegrität ist eine softwarebasierte Sicherheitsstufe, bei der auf einem PC nur die in einer expliziten Liste enthaltene Software ausgeführt werden darf. Für sich genommen weist die konfigurierbare Codeintegrität keine Hardware- oder Firmwareanforderungen auf. Mit Configuration Manager bereitgestellte Device Guard-Richtlinien aktivieren eine konfigurierbare Codeintegritätsrichtlinie auf PCs in gezielten Sammlungen, die die unten aufgeführten Mindestanforderungen an Windows-Version und SKU erfüllen. Optional kann hypervisorbasierter Schutz der durch Configuration Manager bereitgestellten Codeintegritätsrichtlinien über die Gruppenrichtlinie auf unterstützter Hardware aktiviert werden.

Weitere Informationen zu Device Guard finden Sie im [Device Guard-Bereitstellungshandbuch](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

Mit Configuration Manager können Sie eine Device Guard-Richtlinie zum Konfigurieren des Modus bereitstellen, in dem Device Guard auf PCs in einer Sammlung ausgeführt wird. 

Folgende Modi stehen zur Verfügung:

1.    **Erzwingen aktiviert**: Nur vertrauenswürdige ausführbare Dateien dürfen ausgeführt werden.
2.    **Nur überwachen**: Alle Programme können ausgeführt werden, allerdings werden nicht vertrauenswürdige Programme bei ihrer Ausführung im Ereignisprotokoll des lokalen Clients erfasst.

>[!TIP]
>In dieser Version von Configuration Manager ist Device Guard als Vorabfeature enthalten. Informationen zur Aktivierung finden Sie unter [Features der Vorabversion in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

### <a name="what-can-run-when-you-deploy-a-device-guard-policy"></a>Welche Software kann ausgeführt werden, wenn Sie eine Device Guard-Richtlinie bereitstellen?

Mit Windows Device Guard können Sie streng steuern, was auf von Ihnen verwalteten PCs ausgeführt werden kann. Dies ist insbesondere für PCs in Abteilungen mit hohen Sicherheitsanforderungen nützlich, in denen es unerlässlich ist, die Ausführung unerwünschter Software zu verhindern.

Wenn Sie eine Richtlinie bereitstellen, wird üblicherweise die Ausführung der folgenden Programme zugelassen:

- Windows-Betriebssystemkomponenten
- Entwicklungscenter-Hardwaretreiber, die über WHQL-Signaturen (Windows-Hardware Quality Labs) verfügen
- Windows Store-Apps
- Der Configuration Manager-Client 
- Sämtliche, durch Configuration Manager bereitgestellte Software, die PCs nach der Verarbeitung der Device Guard-Richtlinie installieren. 
- Updates zu Windows-Komponenten von:
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager

>[!IMPORTANT]
>Dies umfasst keine **nicht** in Windows integrierte Software, die automatisch über das Internet bzw. über Softwareupdates von Drittanbietern aktualisiert wird, ganz gleich, ob sie über einen der oben genannten Aktualisierungsmechanismen oder über das Internet installiert wird. Nur Softwareänderungen, die über den Configuration Manager-Client bereitgestellt werden, dürfen ausgeführt werden.

## <a name="before-you-start"></a>Vorbereitung

Bevor Sie Device Guard-Richtlinien konfigurieren oder bereitstellen, lesen Sie die folgenden Informationen:

- Die Device Guard-Verwaltung ist ein Vorabfeature für Configuration Manager und unterliegt Änderungen.
- Um Device Guard zu verwenden, muss auf PCs, die Sie verwalten, Windows 10 Enterprise mit dem Creators Update oder höher ausgeführt werden.
- Sobald eine Richtlinie auf einem Client-PC erfolgreich verarbeitet wurde, wird Configuration Manager auf diesem Client als verwaltetes Installationsprogramm konfiguriert, und Software, die nach der Verarbeitung der Richtlinie über SCCM bereitgestellt wird, gilt automatisch als vertrauenswürdig. Der Software, die von Configuration Manager vor der Verarbeitung der Device Guard-Richtlinie installiert wurde, wird nicht automatisch vertraut.
- Sobald ein Client-PCs in dieser Vorabversion eine Bereitstellung einer Device Guard-Richtlinie erhält, wird die Verarbeitungszeit dieser Richtlinie über einen Zeitraum von zwei Stunden zufällig festgelegt. 
- Client-PCs benötigen eine Verbindung mit ihrem Domänencontroller, damit eine Device Guard-Richtlinie erfolgreich verarbeitet werden kann.
- Der standardmäßig erfolgt die Kompatibilitätsauswertung für während der Bereitstellung konfigurierbare Device Guard-Richtlinien jeden Tag. Wenn bei der Verarbeitung der Richtlinie Probleme festgestellt werden, kann es sinnvoll sein, den Zeitplan für die Kompatibilitätsauswertung mit einem kürzeren Intervall zu konfigurieren, z.B. jede Stunde. Dieser Zeitplan bestimmt, wie oft Clients im Fall eines Fehlers erneut versuchen, eine Device Guard-Richtlinie zu verarbeiten.
- Wenn Sie eine Device Guard-Richtlinie bereitstellen, können Client-PCs unabhängig vom ausgewählten Erzwingungsmodus keine HTML-Anwendungen mit der Erweiterung „.hta“ ausführen.

## <a name="how-to-create-a-device-guard-policy"></a>Erstellen einer Device Guard-Richtlinie
1.    Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.
2.    Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie dann auf **Device Guard-Richtlinien**.
3.    Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Device Guard-Richtlinie erstellen**.
4.    Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Device Guard-Richtlinien**** die folgenden Informationen an:
    - **Name**: Geben Sie einen eindeutigen Namen für die Device Guard-Richtlinie ein. 
    - **Beschreibung**: Wenn Sie möchten, können Sie eine Beschreibung für die Richtlinie eingeben, anhand derer Sie sie in der Configuration Manager-Konsole erkennen können.
    - **Erzwingungsmodus**: Wählen Sie eine der folgenden Erzwingungsmethoden für Device Guard auf dem Client-PC aus.
        - **Erzwingen aktiviert**: Nur vertrauenswürdige ausführbare Dateien dürfen ausgeführt werden.
        - **Nur überwachen**: Alle Programme können ausgeführt werden, allerdings werden nicht vertrauenswürdige Programme bei ihrer Ausführung im Ereignisprotokoll des lokalen Clients erfasst.
5.    Klicken Sie auf **Weiter**, und schließen Sie den Assistenten ab.

## <a name="how-to-deploy-a-device-guard-policy"></a>Bereitstellen einer Device Guard-Richtlinie
1.    Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.
2.    Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie dann auf **Device Guard-Richtlinien**.
3.    Wählen Sie aus der Liste der Richtlinien die Richtlinie aus, die Sie bereitstellen möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.
4.    Wählen Sie im Dialogfeld  **Device Guard-Richtlinie bereitstellen** die Sammlung aus, der Sie die Richtlinie bereitstellen möchten, konfigurieren Sie einen Zeitplan, nach dem die Clients die Richtlinie auswerten sollen, und wählen Sie schließlich, ob der Client die Richtlinie außerhalb konfigurierter Wartungsfenster auswerten kann.
5.    Klicken Sie abschließend auf **OK**, um die Richtlinie bereitzustellen. 

Sobald die Richtlinie auf einem Client-PC verarbeitet wurde, wird ein Neustart auf dem Client entsprechend der **Clienteinstellungen** für **Computerneustart** geplant.
**Die Richtlinie wird erst wirksam, wenn Sie den Client-PC neu starten.**

## <a name="how-to-monitor-a-device-guard-policy"></a>Überwachen einer Device Guard-Richtlinie

Verwenden Sie die Informationen im Thema [Überwachen von Kompatibilitätseinstellungen](/sccm/compliance/deploy-use/monitor-compliance-settings), um die bereitgestellten Richtlinie zu überwachen und sicherzustellen, dass sie ordnungsgemäß auf alle PCs angewendet wurde.

Verwenden Sie die folgende Protokolldatei auf Client-PCs, um die Verarbeitung einer Device Guard-Richtlinie zu überwachen:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Informationen dazu, welche Software blockiert oder überwacht wird, finden Sie in den folgenden Ereignisprotokollen des lokalen Clients. In der Ereignisanzeige sind folgende Protokolle relevant:

1.    Verwenden Sie zum Sperren und Überwachen von ausführbaren Dateien **Anwendungs- und Dienstprotokolle** > **Microsoft** > **Windows** > **Codeintegrität** > **Betrieb**.
2.    Verwenden Sie zum Sperren und Überwachung von Windows Installer- und Skriptdateien **Anwendungs- und Dienstprotokolle** > **Microsoft** > **Windows** > **AppLocker** > **MSI and Script**.

## <a name="security-and-privacy-information-for-device-guard"></a>Informationen zu Sicherheit und Datenschutz für Device Guard

- Wenden Sie in dieser Vorabversion keine Device Guard-Richtlinien mit dem Erzwingungsmodus **Nur überwachen** in einer Produktionsumgebung an. Dieser Modus ist nur dazu bestimmt, Ihnen beim Testen der Funktionen in einer Laborumgebung helfen.
- Geräte, auf denen eine Richtlinie im Modus **Nur überwachen** bereitgestellt wurde, oder Geräte, auf denen eine Richtlinie im Modus **Erzwingen aktiviert** bereitgestellt wurde, die aber noch nicht neu gestartet wurden, um die Richtlinie zu erzwingen, sind anfällig für die Installation nicht vertrauenswürdiger Software.
In diesem Fall kann die Software möglicherweise weiterhin ausgeführt werden, auch wenn das Gerät neu gestartet wird oder eine Richtlinie im Modus **Erzwingen aktiviert** empfängt.
- Um sicherzustellen, dass die Device Guard-Richtlinie wirksam ist, bereiten Sie das Gerät in einer Laborumgebung vor, stellen die **Erzwingen aktiviert**-Richtlinie bereit und starten Sie das Gerät anschließend neu, bevor Sie es an Endbenutzer weitergeben.
- Stellen Sie keine Richtlinie mit dem aktivierten Modus **Erzwingen aktiviert** und dann später eine Richtlinie mit **Nur überwachen** auf demselben Gerät bereit. Dies kann dazu führen, dass nicht vertrauenswürdige Software ausgeführt werden darf.
- Wenn Sie Configuration Manager verwenden, um konfigurierbare Codeintegrität auf Client-PCs mit Device Guard-Richtlinien zu aktivieren, beachten Sie, dass die Richtlinie Benutzer mit lokalen Administratorrechten **nicht** daran hindert, die Device Guard-Richtlinie zu umgehen oder nicht vertrauenswürdige Software auf anderem Wege auszuführen. 
- Die einzige Möglichkeit, zu verhindern, dass Benutzer mit lokalen Administratorrechten die konfigurierbare Codeintegrität deaktivieren, besteht darin, eine signierte binäre Richtlinie bereitzustellen. Dies ist über Gruppenrichtlinien möglich, wird in Configuration Manager derzeit jedoch nicht unterstützt.
- Beim Einrichten von Configuration Manager als verwaltetes Installationsprogramm auf Client-PCs wird die AppLocker-Richtlinie verwendet. AppLocker wird nur zum Identifizieren verwalteter Installationsprogramme verwendet. Die gesamte Erzwingung erfolgt über konfigurierbare Codeintegrität. 





