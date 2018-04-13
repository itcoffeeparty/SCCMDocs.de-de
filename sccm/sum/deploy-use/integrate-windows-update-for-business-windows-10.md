---
title: Integration mit Windows Update für Unternehmen in Windows 10
titleSuffix: Configuration Manager
description: Verwenden Sie Windows Update for Business, um Windows 10-basierte Geräte in Ihrer Organisation, die mit Windows Update verbunden sind, auf dem neuesten Stand zu halten.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: e27e5f043af28b74369f21d19e5b20e19572213a
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Integration mit Windows Update für Unternehmen in Windows 10

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit Windows Update for Business (WUfB) können Sie Windows 10-Geräte in Ihrer Organisation hinsichtlich der neuesten Schutzmaßnahmen und Windows-Features auf dem neuesten Stand halten, wenn diese Geräte eine direkte Verbindung mit dem Windows Update-Dienst herstellen. Configuration Manager kann zwischen Windows 10-Computern unterscheiden, die WUfB und WSUS zum Abrufen von Softwareupdates verwenden.  

 Einige Configuration Manager-Features sind nicht mehr verfügbar, wenn Configuration Manager-Clients so konfiguriert sind, dass sie Updates von Windows Update empfangen, was Windows Update for Business (WUfB) oder Windows Insider einbezieht:  

-   Windows Update-Berichterstellung zur Kompatibilität:  

    -   Configuration Manager wird nicht über die Updates informiert, die auf Windows Update veröffentlicht werden. Die Configuration Manager-Clients, die für den Empfang von Updates von WU konfiguriert sind, zeigen für diese Updates in der Configuration Manager-Konsole **Unbekannt** an.  

    -   Die Problembehandlung für den allgemeinen Konformitätsstatus ist schwierig, da der Status **Unbekannt** nur für Clients verwendet wurde, die den Überprüfungsstatus von WSUS nicht zurückmeldeten. Jetzt werden auch Configuration Manager-Clients einbezogen, die Updates von Windows Update erhalten.  

    -   Der bedingte Zugriff (auf Unternehmensressourcen) auf Basis des Status zur Kompatibilität funktioniert nicht erwartungsgemäß für Clients, die Updates von Windows Update empfangen, da sie nie die Kompatibilität von Configuration Manager erfüllen.  

    -   Die Konformität der Definitionsupdates ist Teil der gesamten Berichterstellung zur Updatekonformität und funktioniert auch nicht wie erwartet.  Die Kompatibilität der Definitionsupdates zählt auch zur bedingten Zugriffsauswertung  

-   Die allgemeine Endpoint Protection-Berichterstellung für Defender, die auf dem Status der Updatekonformität basiert, zeigt aufgrund der fehlenden Überprüfungsdaten keine exakten Ergebnisse an.  

-   Configuration Manager kann keine Microsoft-Updates für Office, Internet Explorer und Visual Studio auf Clients bereitstellen, die zum Abrufen von Updates mit WUfB verbunden sind.  

-   Configuration Manager kann keine auf WSUS veröffentlichten und über Configuration Manager verwalteten Updates von Drittanbietern für Clients bereitstellen, die für den Empfang von Updates mit WUfB verbunden sind.  

-   Die vollständige Clientbereitstellung von Configuration Manager, die die Softwareupdateinfrastruktur verwendet, funktioniert nicht für Clients, die für den Empfang von Updates mit WUfB verbunden sind.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identifizieren von Clients, die WUfB für Windows 10-Updates verwenden  
 Mit den folgenden Schritten ermitteln Sie Clients, die zum Abrufen von Windows 10-Updates und -Upgrades WUfB verwenden. Anschließend konfigurieren Sie diese Clients so, dass sie zum Abrufen von Updates nicht mehr WSUS verwenden, und stellen eine Einstellung für den Client-Agent bereit, um den Softwareupdateworkflow für diese Clients zu deaktivieren.  

 **Voraussetzungen**  

-   Clients, die Windows 10 Desktop Pro oder Windows 10 Enterprise Edition Version 1511 oder höher ausführen  

-   [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) wird bereitgestellt und die Clients verwenden WUfB zum Abrufen von Windows 10-Updates und -Upgrades.  

#### <a name="to-identify-clients-that-use-wufb"></a>So identifizieren Sie Clients, die WUfB verwenden  

1.  Deaktivieren Sie den Windows Update-Agent, damit er nicht WSUS abfragt, wenn er zuvor aktiviert war. Der folgende Registrierungsschlüssel kann festgelegt werden, um anzugeben, ob der Computer WSUS oder Windows Update abfragt.  Wenn als Wert „2“ festgelegt wird, wird WSUS nicht überprüft.  
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**

2.  Im Ressourcen-Explorer von Configuration Manager befindet sich unter dem Knoten **Windows Update** das neue Attribut **UseWUServer**.  

3.  Erstellen Sie eine Sammlung auf Basis des **UseWUServer** -Attributs für alle Computer, die für Updates und Upgrades über WUfB verbunden sind.  

4.  Erstellen Sie eine Client-Agent-Einstellung zur Deaktivierung des Workflows für das Softwareupdate. Stellen Sie die Einstellung für die Sammlung von Computern bereit, die direkt mit WUfB verbunden sind.  

5.  Die Computer, die über WUfB verwaltet werden, zeigen als Kompatibilitätsstatus **Unbekannt** an und werden im Gesamtprozentsatz der Kompatibilität nicht berücksichtigt.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Konfigurieren von Windows Update for Business-Zurückstellungsrichtlinien
<!-- 1290890 -->
Ab Version 1706 des Configuration Manager können Sie Zurückstellungsrichtlinien für Funktions- oder Qualitätsupdates für Windows 10-Geräte konfigurieren, die von Windows Update for Business direkt verwaltet werden. Sie können die Zurückstellungsrichtlinien im neuen Knoten **Windows Update for Business-Richtlinien** unter **Softwarebibliothek** > **Windows 10-Wartung** verwalten.

>[!NOTE] 
>Ab Configuration Manager Version 1802 können Sie Rückstellungsrichtlinien für Windows-Insider festlegen. <!--507201-->Weitere Informationen zum Windows-Insider-Programm finden Sie unter [Erste Schritte mit dem Windows-Insider-Programm für Unternehmen](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business).

### <a name="prerequisites"></a>Erforderliche Komponenten
Windows 10-Geräte, die von Windows Update for Business verwaltet werden, benötigen Internetzugriff.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Sie erstellen Sie eine Windows Update for Business-Zurückstellungsrichtlinie
1. In **Softwarebibliothek** > **Windows 10-Wartung** > **Windows Update for Business-Richtlinien**
2. Wählen Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** die Option **Windows Update for Business-Richtlinie erstellen** aus, um den Assistenten für das Erstellen von Windows Update for Business-Richtlinien zu öffnen.
3. Geben Sie auf der Seite **Allgemein** einen Namen und eine Beschreibung für die Richtlinie ein.
4. Konfigurieren Sie auf der Seite **Zurückstellungsrichtlinien**, ob Sie Funktionsupdates zurückstellen oder anhalten möchten. Funktionsupdates bieten in der Regel neue Funktionen für Windows. Nach dem Konfigurieren der Einstellung **Branchbereitschaftsniveau** können Sie dann festlegen, ob und wie lange Sie das Empfangen von Funktionsupdates zurückstellen möchten, sobald diese verfügbar sind.
    - **Branchbereitschaftsniveau**: Legen Sie den Branch fest, für den das Gerät Windows-Updates erhält (Current Branch oder Current Branch for Business).
    - **Zurückstellungszeitraum (Tage)**: Geben Sie die Anzahl der Tage an, die Funktionsupdates verzögert werden. Sie können den Empfang dieser Funktionsupdates für einen Zeitraum von 180 Tagen nach ihrer Veröffentlichung verzögern.
    - **Anhalten von Funktionsupdates ab**: Wählen Sie aus, ob Sie das Empfangen von Funktionsupdates für einen Zeitraum von bis zu 60 Tagen ab dem Zeitpunkt des Anhaltens der Updates anhalten möchten. Nach Ablauf der maximalen Anzahl von Tagen läuft die Anhaltefunktion automatisch ab, sodass das Gerät in Windows Update nach in Frage kommenden Updates sucht. Nach diesem Suchvorgang können Sie die Updates erneut anhalten. Sie können das Anhalten von Funktionsupdates beenden, indem Sie das Kontrollkästchen deaktivieren.   
5. Wählen Sie aus, ob Qualitätsupdates zurückgestellt oder angehalten werden sollen. Qualitätsupdates sind meist Korrekturen und Verbesserungen an vorhandener Windows-Funktionalität und werden in der Regel am ersten Dienstag jedes Monats veröffentlicht, wenngleich sie jederzeit von Microsoft veröffentlicht werden können. Sie können festlegen, ob und wie lange Sie Qualitätsupdates nach deren Verfügbarkeit zurückstellen möchten.
    - **Zurückstellungszeitraum (Tage)**: Geben Sie die Anzahl der Tage an, die Funktionsupdates verzögert werden. Sie können den Empfang dieser Funktionsupdates für einen Zeitraum von 180 Tagen nach ihrer Veröffentlichung verzögern.
    - **Anhalten von Qualitätsupdates ab**: Wählen Sie aus, ob Sie das Empfangen von Qualitätsupdates für einen Zeitraum von bis zu 35 Tagen ab dem Zeitpunkt des Anhaltens der Updates anhalten möchten. Nach Ablauf der maximalen Anzahl von Tagen läuft die Anhaltefunktion automatisch ab, sodass das Gerät in Windows Update nach in Frage kommenden Updates sucht. Nach diesem Suchvorgang können Sie die Updates erneut anhalten. Sie können das Anhalten von Qualitätsupdates beenden, indem Sie das Kontrollkästchen deaktivieren.
6. Wählen Sie **Updates aus anderen Microsoft-Produkten installieren** aus, um die Gruppenrichtlinieneinstellung zu aktivieren, mit deren Hilfe Zurückstellungseinstellungen auf Microsoft Update sowie auf Windows-Updates angewendet werden können.
7. Wählen Sie **Treiber in Windows-Updates einschließen** aus, um Treiber automatisch über Windows-Updates zu aktualisieren. Wenn Sie diese Einstellung deaktivieren, werden Treiberupdates nicht von Windows-Updates heruntergeladen.
8. Schließen Sie den Assistenten ab, um die neue Zurückstellungsrichtlinie zu erstellen.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>So stellen Sie eine Windows Update for Business-Zurückstellungsrichtlinie bereit
1. In **Softwarebibliothek** > **Windows 10-Wartung** > **Windows Update for Business-Richtlinien**
2. Aktivieren Sie auf der Registerkarte **Start** in der Gruppe **Bereitstellung** die Option **Windows Update for Business-Richtlinie bereitstellen**.
3. Konfigurieren Sie die folgenden Einstellungen:
    - **Bereitzustellende Konfigurationsrichtlinie**: Wählen Sie die Windows Update for Business-Richtlinie aus, die Sie bereitstellen möchten.
    - **Sammlung**: Klicken Sie auf **Durchsuchen**, um die Sammlung auszuwählen, in der Sie die Richtlinie bereitstellen möchten.
    - **Nicht konforme Regeln wiederherstellen, falls dies unterstützt wird**: Wählen Sie diese Option aus, um Regeln automatisch wiederherzustellen, die nicht mit der Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI), der Registrierung, Skripts und sämtlichen Einstellungen für die von Configuration Manager registrierten mobilen Geräte konform sind.
    - **Wiederherstellung außerhalb des Wartungsfensters zulassen:** Wenn ein Wartungsfenster für die Sammlung konfiguriert wurde, für die Sie die Richtlinie bereitstellen, aktivieren Sie diese Option, um Konformitätseinstellungen zum Wiederherstellen des Werts außerhalb des Wartungsfensters zuzulassen. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Warnung generieren:** Konfiguriert eine Warnung, die generiert wird, sobald die Konformität einer Konfigurationsbaseline zu einem bestimmten Datum und einer bestimmten Uhrzeit unterhalb eines angegebenen Prozentsatzes liegt. Sie können außerdem angeben, ob eine Warnung an System Center Operations Manager gesendet werden soll.
    - **Zufällige Verzögerung (Stunden)**: Gibt ein Verzögerungsfenster an, um eine übermäßige Verarbeitung im Registrierungsdienst für Netzwerkgeräte zu vermeiden. Der Standardwert ist 64 Stunden.
    - **Zeitplan**: Geben Sie den Zeitplan für die Auswertung der Konformität an, gemäß dem das bereitgestellte Profil auf Clientcomputern ausgewertet wird. Dabei kann es sich um einen einfachen oder benutzerdefinierten Zeitplan handeln. Das Profil wird von Clientcomputern ausgewertet, wenn sich der Benutzer anmeldet.
4.  Schließen Sie den Assistenten ab, um das Profil bereitzustellen.
