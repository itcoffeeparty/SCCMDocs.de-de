---
title: Technical Preview 1707 | Microsoft-Dokumentation
description: "Erfahren Sie mehr über die Funktionen, die mit der Technical Preview-Version 1707 für System Center Configuration Manager zur Verfügung stehen."
ms.custom: na
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 7ee2fd78c6c502394016ba077d42714041ad01c6
ms.sourcegitcommit: 10f17229c5a359f040cb7f8f5e7bd868a34ac086
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2017
---
# <a name="capabilities-in-technical-preview-1707-for-system-center-configuration-manager"></a>Funktionen in der Technical Preview-Version 1707 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*

In diesem Artikel werden die Funktionen erläutert, die in der Technical Preview-Version 1707 für System Center Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Technical Preview-Version installieren, lesen Sie [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview-Version vertraut zu machen und zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Funktionen in einer Technical Preview-Version geben können.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Bekannte Probleme in dieser Technical Preview:**
-   **Beim Update auf Vorschauversion 1707 tritt ein Fehler auf, wenn Sie einen Standortserver im passiven Modus haben**. Wenn Sie die Vorschauversion 1706 ausführen und einen [primären Standortserver im passiven Modus](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability) haben, müssen Sie den Standortserver im passiven Modus deinstallieren, bevor Sie Ihren Vorschaustandort erfolgreich auf Version 1707 aktualisieren können. Sie können den Standortserver im passiven Modus erneut installieren, wenn an Ihrem Standort Version 1707 ausgeführt wird.

  So deinstallieren Sie den Standortserver im passiven Modus:
  1. Navigieren Sie in der Konsole zu **Administration** > **Übersicht** > **Standortkonfiguration** > **Server und Standortsystemrollen**, und wählen Sie den Standortserver im passiven Modus aus.
  2. Klicken Sie im Bereich **Standortsystemrollen** mit der rechten Maustaste auf die Rolle **Standortserver**, und wählen Sie dann **Rolle entfernen**.
  3. Klicken Sie mit der rechten Maustaste auf den Standortserver im passiven Modus, und wählen Sie dann **Löschen**.
  4. Starten Sie nach dem Deinstallieren des Standortservers auf dem aktiven primären Standortserver den Dienst **CONFIGURATION_MANAGER_UPDATE** neu.



**Im Folgenden werden neue Funktionen aufgelistet, die Sie mit dieser Version ausprobieren können.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Client-Peer-Cache-Unterstützung für Express-Installationsdateien für Windows 10 und Office 365
<!-- 1352486 -->
Ab dieser Version unterstützt Peercache die Verteilung von Express-Installationsdateien mit Inhalt für Windows 10 und von Updatedateien für Office 365. Es sind keine weiteren Konfigurationen erforderlich.

## <a name="surface-device-dashboard"></a>Gerätedashboard Surface
<!--1355788-->
Das Gerätedashboard von Surface enthält Informationen zu den Surface-Geräten in Ihrer Umgebung. Navigieren Sie in der Konsole zu **Überwachung** > **Surface Devices** (Surface-Geräte). Sie können Folgendes anzeigen:
- Prozent von Surfaces
- Prozent von Surface-Modellen
- die fünf besten Betriebssystemversionen

Klicken Sie auf einen Teil des Diagramms der **Surface-Modelle** für eine vollständige Liste der Geräte.  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Konfigurieren und Bereitstellen von Windows Defender Application Guard-Richtlinien
<!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) ist eine neue Windows-Funktion zum Schutz Ihrer Benutzer, indem nicht vertrauenswürdige Websites in einem sicheren isolierten Container geöffnet werden, auf den andere Teile des Betriebssystems keinen Zugriff haben. In dieser Technical Preview haben wir Unterstützung für diese Funktion mithilfe von Configuration Manager-Konformitätseinstellungen hinzugefügt, die Sie konfigurieren und einer Sammlung bereitstellen. Diese Funktion wird als Vorschau für die 64-Bit-Version von Windows 10 Fall Creators Update (Codename: RS3) veröffentlicht. Um diese Funktion jetzt zu testen, müssen Sie eine Preview-Version dieses Updates verwenden.

### <a name="before-you-start"></a>Vorbereitung

Zum Erstellen und Bereitstellen von Windows Defender Application Guard-Richtlinien müssen die Windows 10-Geräte, auf denen Sie die Richtlinie bereitstellen, mit einer Netzwerkisolationsrichtlinie konfiguriert werden. Weitere Informationen finden Sie in [diesem Blogbeitrag](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Diese Funktion funktioniert nur mit aktuellen Windows 10 Insider-Builds. Um sie zu testen, muss auf Ihren Clients ein aktueller Windows 10 Insider-Build ausgeführt werden.

### <a name="try-it-out"></a>Probieren Sie es aus!

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>So erstellen Sie eine Richtlinie und durchsuchen die verfügbaren Einstellungen

1. Wählen Sie in der Configuration Manager-Konsole **Assets und Konformität** aus.
2. Wählen Sie im Arbeitsbereich **Assets und Konformität** nacheinander **Übersicht** > **Endpoint Protection** > **Windows Defender Application Guard** aus.
3. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Windows Defender Application Guard-Richtlinie erstellen**.
4. Unter Verwendung des Blogbeitrags als Referenz können Sie die verfügbaren Einstellungen zum Testen der Funktion durchsuchen und konfigurieren.
5. In dieser Version haben wir die neue Seite **Netzwerkdefinition** zum Assistenten hinzugefügt. Geben Sie auf dieser Seite die Unternehmensidentität an, und definieren Sie die Grenze Ihres Unternehmensnetzwerks.<br>PCs unter Windows 10 speichern nur eine Netzwerkisolationsliste auf dem Client. In dieser Version können Sie zwei unterschiedliche Arten von Netzwerkisolationslisten erstellen (eine von Windows Information Protection und eine von Windows Defender Application Guard) und diese dem Client bereitstellen. Wenn Sie beide Richtlinien bereitstellen, müssen diese Netzwerkisolationlisten übereinstimmen. Wenn Sie Listen bereitstellen, die nicht mit dem gleichen Client übereinstimmen, schlägt die Bereitstellung fehl.
Weitere Informationen über das Angeben von Netzwerkdefinition finden Sie in der [Dokumentation zu Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
6. Wenn Sie fertig sind, schließen Sie den Assistenten ab, und stellen Sie die Richtlinie auf einem oder mehreren Windows 10-Geräten bereit.

### <a name="further-reading"></a>Weitere Informationen
Weitere Informationen zu Windows Defender Application Guard finden Sie in [diesem Blogbeitrag](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Darüber hinaus finden Sie in [diesem Blogbeitrag](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903) weitere Informationen zum eigenständigen Modus von Windows Defender Application Guard.

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Hinzufügen von Parametern während der Bereitstellung von PowerShell-Skripts aus Configuration Manager

<!-- 1236459 --->

In der letzten Technical Preview haben wir eine neue Funktion eingeführt, mit der Sie folgende Aktionen durchführen können: [Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole](/sccm/core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console).
In dieser Technical Preview haben wir diese Funktion erweitert. Configuration Manager liest nun das PowerShell-Skript, und zeigt alle Parameter im Assistenten zum Erstellen von Skripts an. Sie können einen Wert für den Parameter im Assistenten angeben, der bei der Ausführung des Skripts verwendet wird. Alternativ können Sie den Parameter leer lassen. Wenn Sie so vorgehen, müssen Sie einen Wert für den Parameter angeben, wenn Sie das Skript ausführen.
In dieser technischen Vorschau müssen Sie alle Parameter angeben, die ein Skript benötigt. In einem zukünftigen Release soll die Angabe von Skriptparametern optional sein.

### <a name="try-it-out"></a>Probieren Sie es aus!

1. Folgen Sie zum [Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole](/sccm/core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console) diesen Anweisungen.
2. Wählen Sie auf der neuen Seite **Skriptparameter** des **Create Script Wizard** (Assistenten zum Erstellen von Skripts) einen Parameter aus, und klicken Sie anschließend auf **Bearbeiten**.
3. Geben Sie einen Parameterwert für den ausgewählten Parameter an, und klicken Sie anschließend auf **OK**.
4. Schließen Sie den Assistenten ab.

Wenn das Skript ausgeführt wird, werden alle Parameterwerte verwendet, die Sie konfiguriert haben.
