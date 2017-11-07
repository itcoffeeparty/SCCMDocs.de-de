---
title: "Paketübertragungs-Manager"
titleSuffix: Configuration Manager
description: "Hier finden Sie Informationen dazu, wie mit dem Paketübertragungs-Manager in System Center Configuration Manager Inhalte von einem Standortserver an einen Remoteverteilungspunkt übertragen werden."
ms.custom: na
ms.date: 2/8/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 7cc724404411ff2ef4897e1bb422f523f357f8eb
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/12/2017
---
# <a name="package-transfer-manager-in-system-center-configuration-manager"></a>Paketübertragungs-Manager in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

An einem System Center Configuration Manager-Standort ist der Paketübertragungs-Manager eine Komponente des SMS_Executive-Diensts, mit der die Übertragung von Inhalt von einem Standortservercomputer zu Remoteverteilungspunkten an einem Standort verwaltet wird. (Ein Remoteverteilungspunkt ist ein Verteilungspunkt, der sich nicht auf dem Standortservercomputer befindet.) Vom Paketübertragungs-Manager werden keine Konfigurationen vom Administrator unterstützt. Wenn Sie wissen, wie der Manager funktioniert, hilft Ihnen das jedoch bei der Planung der Content Management-Infrastruktur sowie beim Beheben von Problemen bei der Inhaltsverteilung.


Wenn Sie Inhalte an einen oder mehrere Remoteverteilungspunkte an einem Standort verteilen, erstellt der **Verteilungs-Manager** einen Auftrag für die Inhaltsübertragung. Anschließend benachrichtigt er den Paketübertragungs-Manager auf primären und sekundären Standortservern, damit diese die Inhalte an die Remoteverteilungspunkte übertragen.

 Die Aktionen des Paketübertragungs-Managers werden in der Datei **pkgxfermgr.log** auf dem Standortserver protokolliert. Die Protokolldatei ist der einzige Ort, an dem Sie die Aktivitäten des Paketübertragungs-Managers anzeigen können.  

> [!NOTE]  
>  In früheren Versionen von Configuration Manager wird die Übertragung von Inhalt an einen Remoteverteilungspunkt vom Verteilungs-Manager verwaltet. Ebenso wird die Übertragung von Inhalt zwischen Standorten vom Verteilungs-Manager verwaltet. Bei System Center Configuration Manager ist der Verteilungs-Manager weiterhin für die Verwaltung der Inhaltsübertragung zwischen zwei Standorten zuständig. Der Paketübertragungs-Manager verwaltet jedoch jetzt die Übertragung von Inhalten an eine große Anzahl von Verteilungspunkten. Dies führt zu einer Steigerung der Gesamtleistung bei der Inhaltsbereitstellung sowohl zwischen zwei Standorten als auch zwischen Verteilungspunkten innerhalb desselben Standorts.  

Zur Übertragung von Inhalt an einen Standardverteilungspunkt werden vom Paketübertragungs-Manager die gleichen Vorgänge verwendet wie beim Verteilungs-Manager in früheren Configuration Manager-Versionen. Die Übertragung von Inhalt an den jeweiligen Remoteverteilungspunkt wird aktiv verwaltet. Wenn Sie jedoch Inhalte an einen Pullverteilungspunkt verteilen, wird der Pullverteilungspunkt vom Paketübertragungs-Manager über das Vorhandensein des Inhalts benachrichtigt. Anschließend übernimmt der Pullverteilungspunkt den Übertragungsvorgang.  

Im Folgenden wird beschrieben, wie die Übertragung von Inhalten an Standardverteilungspunkte und als Pullverteilungspunkte konfigurierte Verteilungspunkte vom Paketübertragungs-Manager verwaltet wird:
1.  **Ein Administrator stellt Inhalte an mindestens einem Verteilungspunkt an einem Standort bereit.**  

    -   **Standardverteilungspunkt:** Ein Auftrag für die Übertragung dieses Inhalts wird vom Verteilungs-Manager erstellt.  

    -   **Pullverteilungspunkt:** Ein Auftrag für die Übertragung dieses Inhalts wird vom Verteilungs-Manager erstellt.  

2.  **Der Verteilungs-Manager führt vorläufige Prüfungen aus.**  

    -   **Standardverteilungspunkt:** Durch den Verteilungs-Manager wird eine einfache Prüfung ausgeführt, ob alle Verteilungspunkte für den Empfang des Inhalts bereit sind. Nach dieser Prüfung wird der Paketübertragungs-Manager vom Verteilungs-Manager benachrichtigt, damit die Übertragung von Inhalt an den Verteilungspunkt gestartet wird.  

    -   **Pullverteilungspunkt:** Der Verteilungs-Manager startet den Paketübertragungs-Manager, der daraufhin den Pullverteilungspunkt darüber informiert, dass ein neuer Auftrag für die Inhaltsübertragung vorhanden ist. Der Status der Remoteverteilungspunkte, bei denen es sich um Pullverteilungspunkte handelt, wird vom Verteilungs-Manager nicht überprüft, weil die Inhaltsübertragungen von den Pullverteilungspunkten jeweils autark verwaltet werden.  

3.  **Der Paketübertragungs-Manager bereitet die Inhaltsübertragung vor.**  

    -   **Standardverteilungspunkt:** Die Single Instance Content Stores aller angegebenen Remoteverteilungspunkte werden vom Paketübertragungs-Manager untersucht, um Dateien zu ermitteln, die sich bereits auf dem jeweiligen Verteilungspunkt befinden. Danach werden nur diejenigen Dateien in die Warteschlange für die Übertragung eingereiht, die nicht bereits vorhanden sind.  

        > [!NOTE]  
        >  Um alle Dateien in der Verteilung auch dann auf den Verteilungspunkt zu kopieren, wenn die Dateien im Single Instance Store des Verteilungspunkts bereits vorhanden sind, verwenden Sie die Aktion **Neu verteilen** für Inhalte.  

    -   **Pullverteilungspunkt:** Für jeden Pullverteilungspunkt in der Verteilung werden die Quellverteilungspunkte durch den Paketübertragungs-Manager darauf überprüft, ob Inhalt vorhanden ist.  

        -   Wenn der Inhalt auf mindestens einem Quellverteilungspunkt zur Verfügung steht, sendet der Paketübertragungs-Manager eine Benachrichtigung an den betreffenden Pullverteilungspunkt. Die Benachrichtigung weist den Verteilungspunkt an, mit der Inhaltsübertragung zu beginnen. Die Benachrichtigung umfasst Dateinamen und -größen, Attribute und Hashwerte.  

        -   Solange der Inhalt noch nicht zur Verfügung steht, wird vom Paketübertragungs-Manager keine Benachrichtigung an den Verteilungspunkt gesendet. Stattdessen wird die Überprüfung alle 20 Minuten wiederholt, bis der Inhalt verfügbar ist. Wenn der Inhalt dann zur Verfügung steht, wird die Benachrichtigung vom Paketübertragungs-Manager an den betreffenden Pullverteilungspunkt gesendet.  

        > [!NOTE]  
        >  Damit der Pullverteilungspunkt auch dann alle Dateien in der Verteilung auf den Verteilungspunkt kopiert, wenn die Dateien im Single Instance Store des Verteilungspunkts bereits vorhanden sind, verwenden Sie die Aktion **Neu verteilen** für Inhalte.  

4.  **Die Inhaltsübertragung beginnt.**  

    -   **Standardverteilungspunkt:** Durch den Paketübertragungs-Manager werden Dateien an den jeweiligen Remoteverteilungspunkt übertragen. Bei der Übertragung an einen Standardverteilungspunkt:  

        -   Standardmäßig können vom Paketübertragungs-Manager gleichzeitig drei eindeutige Pakete verarbeitet und parallel an fünf Verteilungspunkte verteilt werden. Diese werden zusammen als **Einstellungen für gleichzeitige Verteilung** bezeichnet. Um die gleichzeitige Verteilung einzurichten, wechseln Sie in den **Eigenschaften der Softwareverteilungskomponente** für die einzelnen Standorte auf die Registerkarte **Allgemein**.  

        -   Die Konfigurationen von Zeitplanung und Netzwerkbandbreite der einzelnen Verteilungspunkte werden vom Paketübertragungs-Manager bei der Übertragung von Inhalt an den jeweiligen Verteilungspunkt verwendet. Sie konfigurieren diese Einstellungen in den **Eigenschaften** des jeweiligen Remoteverteilungspunkts. Wechseln Sie zu den Registerkarten **Zeitplan** und **Begrenzung der Datenübertragungsrate**. Weitere Informationen finden Sie unter [Manage content and content infrastructure for System Center Configuration Manager (Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager)](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    -   **Pullverteilungspunkt:** Wenn ein Verteilungspunkt eine Benachrichtigungsdatei empfängt, wird der Vorgang zur Übertragung von Inhalt gestartet. Der Übertragungsvorgang läuft auf jedem Pullverteilungspunkt unabhängig:  

        1.   Die noch nicht im Single Instance Store vorhandenen Dateien in der Inhaltsverteilung werden durch den Pullverteilungspunkt ermittelt, und das Herunterladen des betreffenden Inhalts von einem Quellverteilungspunkt wird vorbereitet.  

        2.   Danach werden vom Pullverteilungspunkt alle Quellverteilungspunkte überprüft, bis ein Quellverteilungspunkt gefunden wird, auf dem der Inhalt verfügbar ist. Wird ein solcher Quellverteilungspunkt mit dem Inhalt erkannt, dann wird mit dem Herunterladen des Inhalts begonnen.  

        > [!NOTE]  
        >  Der Vorgang beim Herunterladen des Inhalts durch den Pullverteilungspunkt ist mit dem von Configuration Manager-Clients verwendeten identisch. Für die Inhaltsübertragung durch den Pullverteilungspunkt werden die Einstellungen für die gleichzeitige Übertragung nicht verwendet. Planungs- und Drosselungsoptionen, die Sie für Standardverteilungspunkte konfigurieren, werden ebenfalls nicht verwendet.  

5.  **Die Inhaltsübertragung wird abgeschlossen.**  

    -   **Standardverteilungspunkt:** Nachdem der Paketübertragungs-Manager die Übertragung von Dateien an die angegebenen Remoteverteilungspunkte abgeschlossen hat, überprüft er den Hash des Inhalts auf dem Verteilungspunkt. Anschließend wird der Verteilungs-Manager darüber informiert, dass die Verteilung abgeschlossen ist.  

    -   **Pullverteilungspunkt:** Sobald das Herunterladen des Inhalts auf den Pullverteilungspunkt abgeschlossen ist, wird der Hash des Inhalts überprüft. Anschließend wird eine Statusmeldung an den Standortverwaltungspunkt übermittelt, um den Erfolg mitzuteilen. Ist dieser Status nach 60 Minuten noch nicht eingegangen, wird der Paketübertragungs-Manager wieder aktiviert. Er überprüft den Pullverteilungspunkt, um zu bestätigen, dass der Inhalt auf den Pullverteilungspunkt heruntergeladen wurde. Ist das Herunterladen des Inhalts noch nicht abgeschlossen, wird der Paketübertragungs-Manager für weitere 60 Minuten in den Ruhemodus versetzt, bis der Pullverteilungspunkt erneut überprüft wird. Dieser Zyklus wird bis zum Abschluss der Inhaltsübertragung an den Pullverteilungspunkt fortgesetzt.  
