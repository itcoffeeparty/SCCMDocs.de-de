---
title: Pullverteilungspunkt
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Konfigurationen und Einschränkungen zur Verwendung eines Pullverteilungspunkts mit System Center Configuration Manager.
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d6d6f68e913d261a5a23db85707ea0c9ac965cbd
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="use-a-pull-distribution-point-with-system-center-configuration-manager"></a>Verwenden eines Pullverteilungspunkts mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Ein Pullverteilungspunkt für System Center Configuration Manager ist ein Standardverteilungspunkt, der verteilte Inhalte abruft, indem diese aus einem Quellspeicherort wie einem Client heruntergeladen werden, ohne dass eine Pushübertragung der Inhalte vom Standortserver erfolgt.  

 Wenn Sie Inhalt für zahlreiche Verteilungspunkte an einem Standort bereitstellen, können Sie mithilfe von Pullverteilungspunkten nicht nur die Verarbeitungslast auf dem Standortserver verringern, sondern auch die Übertragung des Inhalts an die einzelnen Verteilungspunkte beschleunigen. Hierzu wird der Prozess der Inhaltsübertragung an jeden Verteilungspunkt vom Verteilungs-Manager-Prozess des Standortservers ausgelagert.  

-   Sie können einzelne Verteilungspunkte als Pullverteilungspunkte konfigurieren.  

-   Für jeden Pullverteilungspunkt müssen Sie mindestens einen Quellverteilungspunkt angeben, von dem Bereitstellungen abgerufen werden können (ein Pullverteilungspunkt kann Inhalte nur von einem Verteilungspunkt abrufen, der als Quellverteilungspunkt definiert ist).  

-   Wenn Sie Inhalte an einen Pullverteilungspunkt verteilen, wird der Pullverteilungspunkt vom Standortserver benachrichtigt. Daraufhin wird vom Pullverteilungspunkt das Herunterladen (Übertragen) des Inhalts von einem Quellverteilungspunkt eingeleitet. Die Inhaltsübertragung wird von jedem Pullverteilungspunkt separat verwaltet, und der Inhalt wird von einem Verteilungspunkt heruntergeladen, auf dem eine Kopie des Inhalts bereits verfügbar ist.  

Von Pullverteilungspunkten werden die gleichen Konfigurationen und Funktionen wie von herkömmlichen Configuration Manager-Verteilungspunkten unterstützt. Beispielsweise werden von einem als Pullverteilungspunkt konfigurierten Verteilungspunkt Multicast- und PXE-Konfigurationen, Inhaltsprüfung und bedarfsgesteuerte Inhaltsverteilung unterstützt. Von einem Pullverteilungspunkt werden neben der HTTP- bzw. HTTPS-Kommunikation von Clients die gleichen Zertifikatoptionen wie bei anderen Verteilungspunkten unterstützt. Zudem können Pullverteilungspunkte einzeln oder als Mitglied einer Verteilungspunktgruppe verwaltet werden.  

> [!IMPORTANT]
> Zwar wird von einem Pullverteilungspunkt die Kommunikation über HTTP und HTTPS unterstützt, doch wenn Sie Configuration Manager verwenden, können Sie nur für HTTP konfigurierte Quellverteilungspunkte angeben. Sie können mit dem Configuration Manager SDK einen Quellverteilungspunkt angeben, der für HTTPS konfiguriert ist.  

 **Im Folgenden wird die Abfolge der Ereignisse bei der Verteilung von Inhalten an einen Pullverteilungspunkt dargestellt:**  

-   Sobald Inhalt an einen Pullverteilungspunkt verteilt wird, wird vom Paketübertragungs-Manager auf dem Standortserver die Standortdatenbank überprüft, um zu ermitteln, ob der Inhalt auf einem Quellverteilungspunkt verfügbar ist. Wenn der Inhalt auf keinem Quellverteilungspunkt für den Pullverteilungspunkt verfügbar ist, wird diese Überprüfung alle 20 Minuten wiederholt, bis der Inhalt verfügbar ist.  

-   Wenn vom Paketübertragungs-Manager die Verfügbarkeit des Inhalts bestätigt wird, wird der Pullverteilungspunkt benachrichtigt, damit der Inhalt heruntergeladen wird. Wenn bei dieser Benachrichtigung ein Fehler auftritt, wird sie auf Grundlage der **Wiederholungseinstellungen** der Softwareverteilungskomponenten für Pullverteilungspunkte wiederholt. Nach Eingang dieser Benachrichtigung auf dem Pullverteilungspunkt wird versucht, den Inhalt von den Quellverteilungspunkten herunterzuladen.  

-   Während der Pullverteilungspunkt den Inhalt herunterlädt, ruft der Paketübertragungs-Manager den Status basierend auf dem **Status der Abrufeinstellungen** der Softwareverteilungskomponente für Pullverteilungspunkte ab.  Sobald das Herunterladen auf den Pullverteilungspunkt abgeschlossen ist, wird dieser Status an den Verwaltungspunkt übermittelt.

**Ein Pullverteilungspunkt kann bei der Installation des Verteilungspunkts bzw. danach konfiguriert werden** , indem Sie die Eigenschaften der Standortsystemrolle „Verteilungspunkt“ bearbeiten.  

**Die Konfiguration als Pullverteilungspunkt kann durch Bearbeiten der Eigenschaften des Verteilungspunkts entfernt werden**. Wenn Sie die Konfiguration als Pullverteilungspunkt entfernen, wird der normale Betrieb vom Verteilungspunkt wiederaufgenommen. Nachfolgende Inhaltsübertragungen an den Verteilungspunkt werden vom Standortserver verwaltet.  

## <a name="to-configure-software-distribution-component-for-pull-distribution-points"></a>So konfigurieren Sie Softwareverteilungskomponente für Pullverteilungspunkte

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Standorte** aus.  

2.  Wählen Sie die gewünschte Website aus, und wählen Sie **Standortkomponenten konfigurieren** > **Softwareverteilung** aus.

3. Wählen Sie die Registerkarte **Pullverteilungspunkt** aus.  

4.  Konfigurieren Sie in der Liste **Wiederholungseinstellungen** die folgenden Werte:  

    -   **Anzahl der Wiederholungen**: Die Anzahl der Versuche des Paketübertragungs-Managers, den Pullverteilungspunkt zum Herunterladen des Inhalts zu benachrichtigen.  Wenn diese Anzahl überschritten wird, bricht der Paketübertragungs-Manager die Übertragung ab.

    -   **Verzögerung vor Neuversuchen (Minuten)**: Die Anzahl der Minuten, die zwischen den Versuchen des Paketübertragungs-Managers verstreichen. 

5.  Konfigurieren Sie in der Liste **Status der Abrufeinstellungen** die folgenden Werte:  

    -   **Anzahl der Abrufe**: Die Anzahl der Kontakte zwischen dem Paketübertragungs-Manager und dem Pullverteilungspunkt zum Abrufen des Auftragsstatus.  Wenn diese Anzahl vor dem Auftragsabschluss überschritten wird, bricht der Paketübertragungs-Manager die Übertragung ab.

    -   **Verzögerung vor Neuversuchen (Minuten)**: Die Anzahl der Minuten, die zwischen den Versuchen des Paketübertragungs-Managers verstreichen. 
    
    > [!NOTE]  
    >  Wenn der Paketübertragungs-Manager einen Auftrag abbricht, weil die Anzahl der Statusabfragen überschritten wurde, wird der Pullverteilungspunkt den Inhalt weiterhin herunterladen.  Nach dem Abschluss wird die entsprechende Statusmeldung an den Paketübertragungs-Manager gesendet, und die Konsole spiegelt den neuen Status wider.
    
## <a name="limitations-for-pull-distribution-points"></a>Einschränkungen für Pullverteilungspunkte  

-   Ein cloudbasierter Verteilungspunkt kann nicht als Pullverteilungspunkt konfiguriert werden.  

-   Ein Verteilungspunkt auf einem Standortserver kann nicht als Pullverteilungspunkt konfiguriert werden.  

-   **Mit der Konfiguration für vorab bereitgestellte Inhalte wird die Konfiguration des Pullverteilungspunkts überschrieben**. Von einem für vorab bereitgestellten Inhalt konfigurierten Verteilungspunkt wird auf den Inhalt gewartet. Der Inhalt wird nicht vom Quellverteilungspunkt mithilfe von Pull übertragen, und gleichermaßen wird auf einem Standardverteilungspunkt mit der Konfiguration für vorab bereitgestellten Inhalt kein Inhalt vom Standortserver empfangen.  

-   **Bei der Inhaltsübertragung werden von einem Pullverteilungspunkt keine Konfigurationen für die Planung oder Begrenzung der Datenübertragungsrate verwendet** . Wenn Sie einen bereits installierten Verteilungspunkt als Pullverteilungspunkt konfigurieren, werden Konfigurationen für die Planung und Begrenzung der Datenübertragungsrate zwar gespeichert, aber nicht verwendet. Wenn Sie die Konfiguration des Pullverteilungspunkts zu einem späteren Zeitpunkt entfernen, werden die Konfigurationen für die Planung und Begrenzung der Datenübertragungsrate wie vorgesehen implementiert.  

    > [!NOTE]  
    >  Wenn ein Verteilungspunkt als Pullverteilungspunkt konfiguriert ist, werden die Registerkarten **Zeitplan** und **Begrenzung der Datenübertragungsrate** nicht in den Eigenschaften des Verteilungspunkts angezeigt.  

-   Pullverteilungspunkte verwenden die Einstellungen in der Registerkarte **Allgemein** der **Eigenschaften der Softwareverteilungskomponente** nicht für jeden Standort.  Dies schließt die Einstellungen **Gleichzeitige Verteilung** und **Multicast-Wiederholung** ein.  Verwenden Sie die Registerkarte **Pullverteilungspunkt**, um die Einstellungen für Pullverteilungspunkte zu konfigurieren.

-   Zur Übertragung von Inhalt von einem Quellverteilungspunkt in einer Remotegesamtstruktur muss auf dem Computer, auf dem der Pullverteilungspunkt gehostet wird, ein Configuration Manager-Client installiert sein. Außerdem muss ein Netzwerkzugriffskonto konfiguriert sein, über das der Zugriff auf den Quellverteilungspunkt möglich ist.  

-   Auf einem als Pullverteilungspunkt konfigurierten Computer mit einem Configuration Manager-Client muss die Version des Clients mit der des Configuration Manager-Standorts übereinstimmen, von dem der Pullverteilungspunkt installiert wird. Diese Anforderung gilt für den Pullverteilungspunkt, damit die Komponente „CCMFramework“ verwendet werden kann, die vom Pullverteilungspunkt und dem Configuration Manager-Client genutzt wird.  

## <a name="about-source-distribution-points"></a>Informationen zu Quellverteilungspunkten  
 Beim Konfigurieren des Pullverteilungspunkts müssen Sie mindestens einen Quellverteilungspunkt angeben.  

-   Es werden nur Verteilungspunkte angezeigt, die als Quellverteilungspunkte infrage kommen.  

-   Ein Pullverteilungspunkt kann als Quellverteilungspunkt für einen anderen Pullverteilungspunkt angegeben werden.  

-   Nur Verteilungspunkte, von denen HTTP unterstützt wird, können als Quellverteilungspunkte angegeben werden, wenn Sie Configuration Manager verwenden.  

-   Sie können mit dem Configuration Manager SDK einen Quellverteilungspunkt angeben, der für HTTPS konfiguriert ist. Damit Sie einen für HTTPS konfigurierten Quellverteilungspunkt verwenden können, muss sich der Pullverteilungspunkt auch auf einem Computer mit dem Configuration Manager-Client befinden.  

Jedem Verteilungspunkt in einer Punktliste mit Pull- und Quellverteilungspunkten kann eine Priorität zugewiesen werden:  

-   Sie können jedem Quellverteilungspunkt eine gesonderte Priorität zuweisen, Sie können aber auch mehreren Quellverteilungspunkten die gleiche Priorität zuweisen.  

-   Über die Priorität wird bestimmt, in welcher Reihenfolge vom Pullverteilungspunkt Inhalt von dessen Quellverteilungspunkten angefordert wird.  

-   Zuerst wird vom Pullverteilungspunkt eine Verbindung mit einem Quellverteilungspunkt mit dem niedrigsten Wert für die Priorität hergestellt.  Wenn es mehrere Quellverteilungspunkte mit der gleichen Priorität gibt, wird vom Pullverteilungspunkt auf nicht deterministische Weise einer der Quellverteilungspunkte mit dieser Priorität ausgewählt.  

-   Ist der Inhalt in der ausgewählten Quelle nicht verfügbar, wird vom Pullverteilungspunkt versucht, den Inhalt von einem anderen Verteilungspunkt mit der gleichen Priorität herunterzuladen.  

-   Wenn der Inhalt auf keinem der Verteilungspunkte mit einer bestimmten Priorität vorhanden ist, wird vom Pullverteilungspunkt versucht, den Inhalt von einem Verteilungspunkt herunterzuladen, dem eine Priorität mit dem nächstgrößeren Wert zugewiesen wurde. Dieser Prozess wird wiederholt, bis der Inhalt gefunden wurde, oder der Pullverteilungspunkt wird für 30 Minuten deaktiviert, bevor der Prozess erneut beginnt.  

Wenn von einem Pullverteilungspunkt Inhalt von einem Quellverteilungspunkt heruntergeladen wird, wird dieser Pullverteilungspunkt im Bericht **Verwendungsdatenzusammenfassung für Verteilungspunkt** in der Spalte **Clients mit Zugriff (eindeutig)** als Client gezählt.  

 Die Inhaltsübertragung von einem Quellverteilungspunkt erfolgt standardmäßig über das **Computerkonto** des Pullverteilungspunkts. Wenn aber Inhalt von einem Quellverteilungspunkt übertragen wird, der sich in einer Gesamtstruktur befindet, wird vom Pullverteilungspunkt immer das Netzwerkzugriffskonto verwendet. Dieser Vorgang setzt voraus, dass der Configuration Manager-Client auf dem Computer installiert ist. Außerdem muss ein Netzwerkzugriffskonto konfiguriert sein, über das der Zugriff auf den Quellverteilungspunkt möglich ist.  

## <a name="about-content-transfers"></a>Informationen zur Übertragung von Inhalten  
 Die Inhaltsübertragung wird von den Pullverteilungspunkten über die Komponente **CCMFramework** der Configuration Manager-Clientsoftware verwaltet.  

-   Dieses Framework wird von **Pulldp.msi** installiert, wenn Sie den Verteilungspunkt als Pullverteilungspunkt konfigurieren. Der Configuration Manager-Client ist für das Framework nicht erforderlich.  

-   Nach der Installation des Pullverteilungspunkts muss der Dienst „CCMExec“ auf dem Verteilungspunktcomputer funktionstüchtig sein, damit der Pullverteilungspunkt eingesetzt werden kann.  
<!--sms.503672 -Clarified BITS use-->
-   Wenn der Pullverteilungspunkt Inhalte überträgt, erfolgt die Übertragung mithilfe des in das Windows-Betriebssystem integrierten **Background Intelligent Transfer Service** (BITS). Für einen Pullverteilungspunkt muss nicht das optionale BITS-IIS-Servererweiterungsfeature installiert werden.

-  Der Pullverteilungspunkt protokolliert den Vorgang in den Dateien **datatransferservice.log** und **pulldp.log** auf dem Verteilungspunktcomputer.

## <a name="see-also"></a>Weitere Informationen:  
 [Grundlegende Konzepte für die Inhaltsverwaltung in System Center Configuration Manager](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   
