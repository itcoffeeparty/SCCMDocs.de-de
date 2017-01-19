---
title: "Paketübertragungs-Manager | Microsoft-Dokumentation"
description: "Hier finden Sie Informationen dazu, wie mit dem Paketübertragungs-Manager in System Center Configuration Manager Inhalte von einem Standortserver an einen Remoteverteilungspunkt übertragen werden."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 6e61c56b9d1111287bf5a9f22832f6b1ca8146b7

---
# <a name="package-transfer-manager-in-system-center-configuration-manager"></a>Paketübertragungs-Manager in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

An einem System Center Configuration Manager-Standort ist der Paketübertragungs-Manager eine Komponente von SMS_Executive, mit der die Übertragung von Inhalt von einem Standortservercomputer zu Remoteverteilungspunkten an einem Standort verwaltet wird. (Ein Remoteverteilungspunkt ist ein Verteilungspunkt, der sich nicht auf dem Standortservercomputer befindet.) Vom Paketübertragungs-Manager werden keine Konfigurationen vom Adminsitrator unterstützt. Wenn Sie verstehen, wie der Manager funktioniert, hilft Ihnen das jedoch bei der Planung der Content Management-Infrastruktur sowie beim Beheben von Problemen bei der Inhaltsverteilung.


Wenn Sie Inhalte an mindestens einen Remoteverteilungspunkt an einem Standort verteilen, wird vom **Verteilungs-Manager** ein Inhaltsübertragungsauftrag erstellt, und der Paketübertragungs-Manager auf primären und sekundären Standortservern wird benachrichtigt, um den Inhalt an die Remoteverteilungspunkte zu übertragen.

 Die Aktionen des Paketübertragungs-Managers werden in der Datei **pkgxfermgr.log** auf dem Standortserver protokolliert. Die Protokolldatei ist der einzige Ort, an dem Sie die Aktivitäten des Paketübertragungs-Managers anzeigen können.  

> [!NOTE]  
>  In früheren Versionen von Configuration Manager wird die Übertragung von Inhalt an einen Remoteverteilungspunkt vom Verteilungs-Manager verwaltet. Ebenso wird die Übertragung von Inhalt zwischen Standorten vom Verteilungs-Manager verwaltet. Bei System Center Configuration Manager ist der Verteilungs-Manager weiterhin für die Verwaltung der Übertragung von Inhalt zwischen zwei Standorten zuständig. Allerdings wird in Configuration Manager durch den Paketübertragungs-Manager eine Entlastung des Verteilungs-Managers von den Vorgängen ermöglicht, die zur Übertragung von Inhalt an eine große Zahl von Verteilungspunkten erforderlich sind. Verglichen mit früheren Produktversionen wird hierdurch eine Steigerung der Gesamtleistung bei der Inhaltsbereitstellung sowohl zwischen zwei Standorten als auch zwischen Verteilungspunkten innerhalb desselben Standorts unterstützt.  

 Zur Übertragung von Inhalt an einen Standardverteilungspunkt werden vom Paketübertragungs-Manager die gleichen Vorgänge verwendet wie beim Verteilungs-Manager in früheren Configuration Manager-Versionen. Die Übertragung von Inhalt an den jeweiligen Remoteverteilungspunkt wird aktiv verwaltet. Wenn Sie jedoch Inhalt an einen Pullverteilungspunkt verteilen, wird der Pullverteilungspunkt vom Paketübertragungs-Manager über das Vorhandensein des Inhalts benachrichtigt, und der Vorgang der Übertragung dieses Inhalts wird an den Pullverteilungspunkt übergeben.  

Im Folgenden wird beschrieben, wie die Übertragung von Inhalt an Standardverteilungspunkte und als Pullverteilungspunkte konfigurierte Verteilungspunkte vom Paketübertragungs-Manager verwaltet wird:
1.  **Ein Administrator stellt Inhalt an mindestens einem Verteilungspunkt an einem Standort bereit.**  

    -   **Standardverteilungspunkt:** Ein Auftrag für die Übertragung dieses Inhalts wird vom Verteilungs-Manager erstellt.  

    -   **Pullverteilungspunkt:** Ein Auftrag für die Übertragung dieses Inhalts wird vom Verteilungs-Manager erstellt.  

2.  **Vorläufige Prüfungen werden durch den Verteilungs-Manager ausgeführt.**  

    -   **Standardverteilungspunkt:** Durch den Verteilungs-Manager wird eine einfache Prüfung ausgeführt, ob alle Verteilungspunkte für den Empfang des Inhalts bereit sind. Nach dieser Prüfung wird der Paketübertragungs-Manager vom Verteilungs-Manager benachrichtigt, damit die Übertragung von Inhalt an den Verteilungspunkt gestartet wird.  

    -   **Pullverteilungspunkt:** Der Paketübertragungs-Manager wird vom Verteilungs-Manager gestartet. Daraufhin wird der Pullverteilungspunkt vom Paketübertragungs-Manager darüber informiert, dass ein neuer Auftrag für die Übertragung von Inhalt für den Verteilungspunkt vorhanden ist. Der Status der Remoteverteilungspunkte, bei denen es sich um Pullverteilungspunkte handelt, wird vom Verteilungs-Manager nicht überprüft, weil die Inhaltsübertragungen von den Pullverteilungspunkten jeweils autark verwaltet werden.  

3.  **Vorbereiten des Paketübertragungs-Managers auf die Übertragung von Inhalt**  

    -   **Standardverteilungspunkt:** Die Einzelinstanz-Inhaltsspeicher (Single Instance Content Stores) aller angegebenen Remoteverteilungspunkte werden nun vom Paketübertragungs-Manager untersucht, um Dateien zu ermitteln, die sich bereits auf dem jeweiligen Verteilungspunkt befinden. Danach werden nur diejenigen Dateien in die Warteschlange für die Übertragung eingereiht, die nicht bereits vorhanden sind.  

        > [!NOTE]  
        >  Wenn Sie die Aktion **Neu verteilen** für Inhalt anwenden, werden alle Dateien in der Verteilung auch dann auf den Verteilungspunkt kopiert, wenn die Dateien im Single Instance Store des Verteilungspunkts bereits vorhanden sind.  

    -   **Pullverteilungspunkt:** Für jeden Pullverteilungspunkt in der Verteilung werden die Quellverteilungspunkte durch den Paketübertragungs-Manager darauf überprüft, ob Inhalt vorhanden ist:  

        -   Ist Inhalt an mindestens einem Quellverteilungspunkt vorhanden, dann wird vom Paketübertragungs-Manager eine Benachrichtigung an den betreffenden Pullverteilungspunkt gesendet, mit der dieser angewiesen wird, den Inhaltsübertragungsvorgang zu starten. Die Benachrichtigung umfasst Dateinamen und -größen, Attribute und Hashwerte.  

        -   Solange der Inhalt noch nicht zur Verfügung steht, wird vom Paketübertragungs-Manager keine Benachrichtigung an den Verteilungspunkt gesendet. Stattdessen wird die Überprüfung alle 20 Minuten wiederholt, bis der Inhalt verfügbar ist. Wenn der Inhalt dann zur Verfügung steht, wird die Benachrichtigung vom Paketübertragungs-Manager an den betreffenden Pullverteilungspunkt gesendet.  

        > [!NOTE]  
        >  Wenn Sie die Aktion **Neu verteilen** für Inhalt anwenden, werden vom Pullverteilungspunkt auch dann alle Dateien in der Verteilung auf den Verteilungspunkt kopiert, wenn die Dateien im Single Instance Store des Pullverteilungspunkts bereits vorhanden sind.  

4.  **Beginn der Inhaltsübertragung**  

    -   **Standardverteilungspunkt:** Durch den Paketübertragungs-Manager werden Dateien an den jeweiligen Remoteverteilungspunkt übertragen. Bei der Übertragung an einen Standardverteilungspunkt:  

        -   Standardmäßig können vom Paketübertragungs-Manager gleichzeitig drei eindeutige Pakete verarbeitet und parallel an fünf Verteilungspunkte verteilt werden. Diese heißen **Einstellungen für gleichzeitige Verteilung** und werden auf der Registerkarte **Allgemein** der **Eigenschaften der Softwareverteilungskomponente** für jeden Standort konfiguriert.  

        -   Die Konfigurationen von Zeitplanung und Netzwerkbandbreite der einzelnen Verteilungspunkte werden vom Paketübertragungs-Manager bei der Übertragung von Inhalt an den jeweiligen Verteilungspunkt verwendet. Sie konfigurieren diese Einstellungen auf den Registerkarten **Zeitplan** und **Begrenzung der Datenübertragungsrate** in den **Eigenschaften** des jeweiligen Remoteverteilungspunkts. Weitere Informationen finden Sie unter [Manage content and content infrastructure for System Center Configuration Manager (Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager)](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    -   **Pullverteilungspunkt:** Wenn ein Verteilungspunkt eine Benachrichtigungsdatei empfängt, wird der Vorgang zur Übertragung von Inhalt gestartet. Der Übertragungsvorgang läuft auf jedem Pullverteilungspunkt unabhängig:  

        -   Die noch nicht im Single Instance Store vorhandenen Dateien in der Inhaltsverteilung werden durch den Pullverteilungspunkt ermittelt, und das Herunterladen des betreffenden Inhalts von einem Quellverteilungspunkt wird vorbereitet.  

        -   Danach werden vom Pullverteilungspunkt alle Quellverteilungspunkte überprüft, bis ein Quellverteilungspunkt gefunden wird, auf dem der Inhalt verfügbar ist. Wird ein solcher Quellverteilungspunkt mit dem Inhalt erkannt, dann wird mit dem Herunterladen des Inhalts begonnen.  

        > [!NOTE]  
        >  Der Vorgang beim Herunterladen des Inhalts durch den Pullverteilungspunkt ist mit dem von Configuration Manager-Clients verwendeten identisch. Zur Übertragung des Inhalts durch den Pullverteilungspunkt werden weder die Einstellungen zur gleichzeitigen Übertragung noch die Zeitplan- und Einschränkungsoptionen verwendet, die Sie für Standardverteilungspunkte konfiguriert haben.  

5.  **Die Übertragung von Inhalt wird abgeschlossen.**  

    -   **Standardverteilungspunkt:** Nachdem die Übertragung der Dateien an die angegebenen Remoteverteilungspunkte abgeschlossen ist, wird der Hash des Inhalts auf dem Verteilungspunkt durch den Paketübertragungs-Manager überprüft, und der Verteilungs-Manager wird darüber informiert, dass die Verteilung abgeschlossen ist.  

    -   **Pullverteilungspunkt:** Sobald das Herunterladen des Inhalts auf den Pullverteilungspunkt abgeschlossen ist, wird der Hash des Inhalts überprüft, und eine Statusmeldung wird an den Standortverwaltungspunkt übermittelt, um den Erfolg mitzuteilen. Wenn dieser Status allerdings nach 60 Minuten nicht empfangen wird, wird der Paketübertragungs-Manager aktiviert, um auf dem Pullverteilungspunkt zu überprüfen, ob der Inhalt heruntergeladen wurde. Ist das Herunterladen des Inhalts noch nicht abgeschlossen, wird der Paketübertragungs-Manager für 60 Minuten deaktiviert, bevor der Pullverteilungspunkt erneut überprüft wird. Dieser Zyklus wird bis zum Abschluss der Inhaltsübertragung an den Pullverteilungspunkt fortgesetzt.  



<!--HONumber=Dec16_HO3-->


