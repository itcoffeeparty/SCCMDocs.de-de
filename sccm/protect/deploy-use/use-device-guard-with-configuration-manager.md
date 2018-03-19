---
title: Verwalten von Windows Device Guard
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Windows Device Guard mit System Center Configuration Manager verwalten.
ms.custom: na
ms.date: 10/20/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: 
caps.handback.revision: 
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 8d84d0d65db7668baa7be9bbf0ad1df869b37919
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="device-guard-management-with-configuration-manager"></a>Device Guard-Verwaltung mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

## <a name="introduction"></a>Einführung
Device Guard besteht aus einer Gruppe von Windows 10-Features, die dazu entwickelt wurden, PCs vor Schadsoftware und anderer nicht vertrauenswürdiger Software zu schützen. Device Guard verhindert die Ausführung von Schadcode, indem sichergestellt wird, dass nur genehmigter bekannter Code ausgeführt werden kann.

Device Guard umfasst hardware- und softwarebasierte Sicherheitsfunktionen. Konfigurierbare Codeintegrität ist eine softwarebasierte Sicherheitsstufe, bei der auf einem PC nur die in einer expliziten Liste enthaltene Software ausgeführt werden darf. Für sich genommen weist die konfigurierbare Codeintegrität keine Hardware- oder Firmwareanforderungen auf. Mit Configuration Manager bereitgestellte Windows Defender-Anwendungssteuerungsrichtlinie aktivieren eine konfigurierbare Codeintegritätsrichtlinie auf PCs in gezielten Sammlungen, die die in diesem Thema aufgeführten Mindestanforderungen an die Windows-Version und SKU erfüllen. Optional kann hypervisorbasierter Schutz der durch Configuration Manager bereitgestellten Codeintegritätsrichtlinien über die Gruppenrichtlinie auf unterstützter Hardware aktiviert werden.

Weitere Informationen zu Device Guard finden Sie im [Device Guard-Bereitstellungshandbuch](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

## <a name="using-device-guard-with-configuration-manager"></a>Verwenden von Device Guard mit Configuration Manager

Mit Configuration Manager können Sie eine Windows Defender-Anwendungssteuerungsrichtlinie zum Konfigurieren des Modus bereitstellen, in dem Device Guard auf PCs in einer Sammlung ausgeführt wird. 

Folgende Modi stehen zur Verfügung:

1.  **Erzwingen aktiviert**: Nur vertrauenswürdige ausführbare Dateien dürfen ausgeführt werden.
2.  **Nur überwachen**: Alle Programme können ausgeführt werden, allerdings werden nicht vertrauenswürdige Programme bei ihrer Ausführung im Ereignisprotokoll des lokalen Clients erfasst.

>[!TIP]
>In dieser Version von Configuration Manager ist Device Guard als Vorabfeature enthalten. Informationen zur Aktivierung finden Sie unter [Features der Vorabversion in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>Was kann ausgeführt werden, wenn Sie eine Windows Defender-Anwendungssteuerungsrichtlinie bereitstellen?

Mit Windows Device Guard können Sie streng steuern, was auf von Ihnen verwalteten PCs ausgeführt werden kann. Dieses Feature kann für PCs in Abteilungen mit hohen Sicherheitsanforderungen nützlich sein, in denen es unerlässlich ist, die Ausführung unerwünschter Software zu verhindern.

Wenn Sie eine Richtlinie bereitstellen, wird üblicherweise die Ausführung der folgenden ausführbaren Dateien zugelassen:

- Windows-Betriebssystemkomponenten
- Entwicklungscenter-Hardwaretreiber, die über WHQL-Signaturen (Windows-Hardware Quality Labs) verfügen
- Windows Store-Apps
- Der Configuration Manager-Client 
- Sämtliche, durch Configuration Manager bereitgestellte Software, die PCs nach der Verarbeitung der Windows Defender-Anwendungssteuerungsrichtlinie installieren. 
- Updates zu Windows-Komponenten von:
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager

>[!IMPORTANT]
>Diese Elemente enthalten keine *nicht* in Windows integrierte Software, die automatisch über das Internet bzw. über Softwareupdates von Drittanbietern aktualisiert wird, ganz gleich, ob sie über einen der zuvor genannten Aktualisierungsmechanismen oder über das Internet installiert wird. Nur Softwareänderungen, die über den Configuration Manager-Client bereitgestellt werden, können ausgeführt werden.

## <a name="before-you-start"></a>Vorbereitung

Bevor Sie Windows Defender-Anwendungssteuerungsrichtlinien konfigurieren oder bereitstellen, lesen Sie die folgenden Informationen:

- Die Device Guard-Verwaltung ist ein Vorabfeature für Configuration Manager und unterliegt Änderungen.
- Um Device Guard mit Configuration Manager zu verwenden, muss auf PCs, die Sie verwalten, Windows 10 Enterprise in der Version 1703 oder höher ausgeführt werden.
- Sobald eine Richtlinie auf einem Client-PC erfolgreich verarbeitet wurde, wird Configuration Manager auf diesem Client als verwaltetes Installationsprogramm konfiguriert, und Software, die nach der Verarbeitung der Richtlinie über SCCM bereitgestellt wird, gilt automatisch als vertrauenswürdig. Der Software, die von Configuration Manager vor der Verarbeitung der Windows Defender-Anwendungssteuerungsrichtlinie installiert wurde, wird nicht automatisch vertraut.
- Client-PCs benötigen eine Verbindung mit ihrem Domänencontroller, damit eine Windows Defender-Anwendungssteuerungsrichtlinie erfolgreich verarbeitet werden kann.
- Standardmäßig erfolgt die Konformitätsauswertung für während der Bereitstellung konfigurierbare Windows Defender-Anwendungssteuerungsrichtlinie täglich. Wenn bei der Verarbeitung der Richtlinie Probleme festgestellt werden, kann es sinnvoll sein, den Zeitplan für die Kompatibilitätsauswertung mit einem kürzeren Intervall zu konfigurieren, z.B. jede Stunde. Dieser Zeitplan bestimmt, wie oft Clients im Fall eines Fehlers erneut versuchen, eine Windows Defender-Anwendungssteuerungsrichtlinie zu verarbeiten.
- Wenn Sie eine Windows Defender-Anwendungssteuerungsrichtlinie bereitstellen, können Client-PCs unabhängig vom ausgewählten Erzwingungsmodus keine HTML-Anwendungen mit der Erweiterung „.hta“ ausführen.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Erstellen einer Windows Defender-Anwendungssteuerungsrichtlinie
1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.
2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie anschließend auf **Windows Defender-Anwendungssteuerungsrichtlinien**.
3.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Windows Defender-Anwendungssteuerungsrichtlinie erstellen**.
4.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Windows Defender-Anwendungssteuerungsrichtlinien** die folgenden Einstellungen an:
    - **Name**: Geben Sie einen eindeutigen Namen für diese Windows Defender-Anwendungssteuerungsrichtlinie ein. 
    - **Beschreibung**: Wenn Sie möchten, können Sie eine Beschreibung für die Richtlinie eingeben, anhand derer Sie sie in der Configuration Manager-Konsole erkennen können.
    - **Erzwingungsmodus**: Wählen Sie eine der folgenden Erzwingungsmethoden für Device Guard auf dem Client-PC aus.
        - **Erzwingen aktiviert**: Nur vertrauenswürdige ausführbare Dateien dürfen ausgeführt werden.
        - **Nur überwachen**: Alle Programme können ausgeführt werden, allerdings werden nicht vertrauenswürdige Programme bei ihrer Ausführung im Ereignisprotokoll des lokalen Clients erfasst.
5.  Klicken Sie im **Assistenten zum Erstellen von Windows Defender-Anwendungssteuerungsrichtlinien** auf der Registerkarte **Einschlüsse** auf **Hinzufügen**, wenn Sie optional bestimmten Dateien oder Ordnern auf PCs Vertrauensstellungen hinzufügen möchten. 
6.  Geben Sie im Dialogfeld **Vertrauenswürdige Dateien oder Ordner hinzufügen** Informationen zur Datei bzw. zum Ordner an, der bzw. dem vertraut werden soll. Sie können einen lokalen Datei- oder Ordnerpfad angeben oder eine Verbindung mit einem Remotegerät herstellen, für das Sie über eine entsprechende Berechtigung verfügen, und einen Datei- oder Ordnerpfad auf diesem Gerät angeben.
Wenn Sie einer Windows Defender-Anwendungssteuerungsrichtlinie optional eine Vertrauensstellung für bestimmte Dateien oder Ordner hinzufügen, ermöglicht Ihnen dies Folgendes:
    - Beheben von Problemen mit dem Verhalten verwalteter Installationsprogramme
    - Vertrauen branchenspezifischer Apps, die nicht mit Configuration Manager bereitgestellt werden können
    - Vertrauen von Apps, die in einem Betriebssystemabbild für ein Betriebssystem enthalten sind 
7.  Klicken Sie auf **Weiter**, und schließen Sie den Assistenten ab.

>[!IMPORTANT]
>Die Einbeziehung vertrauenswürdiger Dateien oder Ordner wird nur auf Client-PCs mit Version 1706 oder höher des Configuration Manager-Clients unterstützt. Wenn Einschlussregeln in einer Windows Defender-Anwendungssteuerungsrichtlinie enthalten sind, und die Richtlinie dann für einen Client-PC bereitgestellt wird, auf dem eine frühere Version des Configuration Manager-Clients ausgeführt wird, kann die Richtlinie nicht angewendet werden. Das Aktualisieren dieser älteren Clients behebt dieses Problem. Richtlinien, die keine Einschlussregeln enthalten, können möglicherweise weiterhin auf ältere Versionen des Configuration Manager-Clients angewendet werden.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Bereitstellen einer Windows Defender-Anwendungssteuerungsrichtlinie
1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.
2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie anschließend auf **Windows Defender-Anwendungssteuerungsrichtlinien**.
3.  Wählen Sie aus der Liste der Richtlinien die Richtlinie aus, die Sie bereitstellen möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.
4.  Wählen Sie im Dialogfeld **Windows Defender-Anwendungssteuerungsrichtlinie bereitstellen** die Sammlung aus, der Sie die Richtlinie bereitstellen möchten. Konfigurieren Sie anschließend einen Zeitplan, nach dem die Clients die Richtlinie auswerten sollen. Wählen Sie abschließend aus, ob der Client die Richtlinie außerhalb konfigurierter Wartungsfenster auswerten kann.
5.  Klicken Sie abschließend auf **OK**, um die Richtlinie bereitzustellen. 

### <a name="restarting-the-device-after-deploying-the-policy"></a>Neustarten des Geräts nach der Bereitstellung der Richtlinie

Nachdem die Richtlinie auf einem Client-PC verarbeitet wurde, wird ein Neustart auf dem Client entsprechend der **Clienteinstellungen** für **Computerneustart** geplant. Ein Neustart ist für die Umsetzung von Richtlinien nicht erforderlich, aber die Standardeinstellung. Wenn Sie Neustarts deaktivieren möchten, gehen Sie folgendermaßen vor:

1. Öffnen Sie den **Assistenten zum Erstellen von Windows Defender-Anwendungssteuerungsrichtlinien**.
2. Deaktivieren Sie auf der Seite **Allgemein** das Kontrollkästchen für **Einen Neustart von Geräten erzwingen, damit diese Richtlinie für alle Prozesse durchgesetzt werden kann**.
3. Klicken Sie auf **Weiter**, bis Sie den Assistenten abgeschlossen haben.



## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Überwachen einer Windows Defender-Anwendungssteuerungsrichtlinie

Verwenden Sie die Informationen im Artikel [Überwachen von Konformitätseinstellungen](/sccm/compliance/deploy-use/monitor-compliance-settings), um sicherzustellen, dass die bereitgestellte Richtlinie ordnungsgemäß auf alle PCs angewendet wurde.

Um die Verarbeitung einer Windows Defender-Anwendungssteuerungsrichtlinie zu überwachen, verwenden Sie die folgende Protokolldatei auf Client-PCs:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Informationen dazu, welche Software blockiert oder überwacht wird, finden Sie in den folgenden Ereignisprotokollen des lokalen Clients:

1.  Verwenden Sie zum Sperren und Überwachen von ausführbaren Dateien **Anwendungs- und Dienstprotokolle** > **Microsoft** > **Windows** > **Codeintegrität** > **Betrieb**.
2.  Verwenden Sie zum Sperren und Überwachung von Windows Installer- und Skriptdateien **Anwendungs- und Dienstprotokolle** > **Microsoft** > **Windows** > **AppLocker** > **MSI and Script**.

## <a name="automatically-let-software-run-if-it-is-trusted-by-intelligent-security-graph"></a>Automatisches Ausführen von Software, wenn diese von Intelligent Security Graph als vertrauenswürdig eingestuft wird

Sie können gesperrte Geräte vertrauenswürdige Software ausführen lassen, die laut Microsoft Intelligent Security Graph (ISG) einen guten Ruf hat. ISG umfasst [Windows Defender SmartScreen](https://docs.microsoft.com/windows/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) und andere Microsoft-Dienste. Auf den Geräten muss Windows Defender SmartScreen ausgeführt werden, damit die Software als vertrauenswürdig eingestuft werden kann.

1. Öffnen Sie den **Assistenten zum Erstellen von Windows Defender-Anwendungssteuerungsrichtlinien**.
2. Aktivieren Sie auf der Seite **Einschlüsse** das Kontrollkästchen für **Software autorisieren, die vom Intelligent Security Graph als vertrauenswürdig eingestuft wird**.
3. Fügen Sie im Feld „Trusted files or folder“ (Vertrauenswürdige Dateien oder Ordner) die Dateien und Ordner hinzu, die als vertrauenswürdig gelten sollen.
4. Klicken Sie auf **Weiter**, bis Sie den Assistenten abgeschlossen haben.



## <a name="security-and-privacy-information-for-device-guard"></a>Informationen zu Sicherheit und Datenschutz für Device Guard

- Wenden Sie in dieser Vorabversion keine Windows Defender-Anwendungssteuerungsrichtlinien mit dem Erzwingungsmodus **Nur überwachen** in einer Produktionsumgebung an. Dieser Modus ist nur dazu bestimmt, Ihnen beim Testen der Funktionen in einer Laborumgebung helfen.
- Geräte, auf denen eine Richtlinie im Modus **Nur überwachen** oder **Erzwingen aktiviert**bereitgestellt wurde und die noch nicht neu gestartet wurden, um die Richtlinie zu erzwingen, sind anfällig für die Installation nicht vertrauenswürdiger Software.
In diesem Fall kann die Software möglicherweise weiterhin ausgeführt werden, auch wenn das Gerät neu gestartet wird oder eine Richtlinie im Modus **Erzwingen aktiviert** empfängt.
- Bereiten Sie das Gerät in einer Laborumgebung vor, um sicherzustellen, dass die Windows Defender-Anwendungssteuerungsrichtlinie angewendet wird. Stellen Sie anschließend die Richtlinie **Erzwingung aktiviert** bereit. Starten Sie das Gerät abschließend neu, bevor Sie das Gerät dem Endbenutzer übergeben.
- Stellen Sie keine Richtlinie mit dem aktivierten Modus **Erzwingen aktiviert** und dann später eine Richtlinie mit **Nur überwachen** auf demselben Gerät bereit. Diese Konfiguration kann dazu führen, dass nicht vertrauenswürdige Software ausgeführt werden darf.
- Wenn Sie Configuration Manager verwenden, um konfigurierbare Codeintegrität auf Client-PCs mit Windows Defender-Anwendungssteuerungsrichtlinien zu aktivieren, werden Benutzer mit lokalen Administratorrechten nicht durch die Richtlinie daran gehindert, die Windows Defender-Anwendungssteuerungsrichtlinie zu umgehen oder nicht vertrauenswürdige Software auf anderem Wege auszuführen. 
- Die einzige Möglichkeit, zu verhindern, dass Benutzer mit lokalen Administratorrechten die konfigurierbare Codeintegrität deaktivieren, besteht darin, eine signierte binäre Richtlinie bereitzustellen. Diese Bereitstellung kann prinzipiell über eine Gruppenrichtlinie erfolgen, wird aber aktuell in Configuration Manager nicht unterstützt.
- Beim Einrichten von Configuration Manager als verwaltetes Installationsprogramm auf Client-PCs wird die AppLocker-Richtlinie verwendet. AppLocker wird nur zum Identifizieren verwalteter Installationsprogramme verwendet. Die gesamte Erzwingung erfolgt über konfigurierbare Codeintegrität. 




