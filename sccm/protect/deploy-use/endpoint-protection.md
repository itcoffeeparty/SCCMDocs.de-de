---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Richtlinien für Antischadsoftware und die Sicherheit der Windows-Firewall für Clientcomputer in der Configuration Manager-Hierarchie verwalten.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2da4b91411822b6274da3e165ff3e43e8752dc45
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="endpoint-protection"></a>Endpoint Protection

*Gilt für: System Center Configuration Manager (Current Branch)*

Endpoint Protection verwaltet Richtlinien für Antischadsoftware und die Sicherheit der Windows-Firewall für Clientcomputer in der Configuration Manager-Hierarchie.  

> [!IMPORTANT]  
>  Sie benötigen eine Lizenz für die Verwendung von Endpoint Protection, damit Sie Clients in der Configuration Manager-Hierarchie verwalten können.  

 Bei der Verwendung von Endpoint Protection mit Configuration Manager ergeben sich für Sie die folgenden Vorteile:  

-   Sie können Antischadsoftware-Richtlinien und Windows-Firewall-Einstellungen erstellen und Windows Defender Advanced Threat Protection für ausgewählte Computergruppen verwalten.  
-   Sie können mit Configuration Manager-Softwareupdates die neuesten Definitionsdateien für Antischadsoftware herunterladen, um Clientcomputer auf dem neuesten Stand zu halten.  
-   Senden Sie E-Mail-Benachrichtigungen, verwenden Sie Funktionen für eine konsoleninterne Überwachung, und zeigen Sie Berichte an. Administratoren werden durch diese Aktionen informiert, sobald Schadsoftware auf Clientcomputern erkannt wird.  

Ab Windows 10 und Windows Server 2016 ist Windows Defender bereits auf den Computern installiert. Bei diesen Betriebssystemen wird bei der Installation des Configuration Manager-Clients ein Verwaltungsclient für Windows Defender installiert. Auf Computern unter Windows 8.1 und früher wird mit dem Configuration Manager-Client auch der Endpoint Protection-Client installiert. Windows Defender und der Endpoint Protection-Client verfügt über folgende Funktionen:  

-   Erkennung von Schadsoftware und Spyware sowie Wiederherstellung  
-   Erkennung von Rootkits und Wiederherstellung  
-   Bewertung kritischer Sicherheitsrisikos und automatische Definitions- und Modulupdates  
-   Erkennung von Sicherheitslücken im Netzwerk über das Netzwerkinspektionssystem  
-   Integration mit Cloud Protection Service, um Microsoft Schadsoftware zu melden. Wenn Sie diesem Dienst beitreten, werden vom Endpoint Protection-Client oder Windows Defender die neuesten Definitionen aus dem Microsoft Center zum Schutz vor Schadsoftware heruntergeladen, sobald nicht identifizierte Schadsoftware auf einem Computer erkannt wird.  

> [!NOTE]  
>  Der Endpoint Protection-Client kann auf einem Server, auf dem Hyper-V ausgeführt wird, sowie auf virtuellen Gastcomputern mit unterstützten Betriebssystemen installiert werden. Endpoint Protection-Aktionen weisen eine integrierte, zufällige Verzögerung auf, damit Schutzdienste nicht gleichzeitig ausgeführt werden und somit eine übermäßige CPU-Auslastung verhindert wird.  

 Darüber hinaus nutzen Sie Endpoint Protection zum Verwalten von Windows-Firewalleinstellungen in der Configuration Manager-Konsole.  

 [Beispielszenario: Verwenden von System Center Endpoint Protection zum Schutz von Computern vor Schadsoftware in System Center Configuration Manager](scenarios-endpoint-protection.md) Endpoint Protection und Windows-Firewall  


## <a name="managing-malware-with-endpoint-protection"></a>Verwalten von Schadsoftware mit Endpoint Protection  
 Mit Endpoint Protection in Configuration Manager können Sie Antischadsoftware-Richtlinien erstellen, in denen Einstellungen für Endpoint Protection-Clientkonfigurationen enthalten sind. Stellen Sie diese Richtlinien für Antischadsoftware auf Clientcomputern bereit. Überwachen Sie dann die Einhaltung über den Knoten **Endpoint Protection-Status** unter **Sicherheit** im Arbeitsbereich **Überwachung**. Nutzen Sie zudem die Endpoint Protection-Berichte im Knoten **Berichterstellung**.  

 Weitere Informationen:  

-   [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md) ‒ Erstellen, Bereitstellen und Überwachen von Richtlinien für Antischadsoftware mit einer Liste der Einstellungen, die Sie konfigurieren können  

-   [Überwachen von Endpoint Protection in System Center Configuration Manager](monitor-endpoint-protection.md) ‒ Überwachen von Aktivitätsberichten, infizierten Clientcomputern und mehr  

-   [Verwalten von Richtlinien für Antischadsoftware und Firewalleinstellungen für Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-firewall.md) ‒ Auf Clientcomputern gefundene Antischadsoftware korrigieren  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Verwalten der Windows-Firewall mit Endpoint Protection  
 Durch Endpoint Protection in Configuration Manager verfügen Sie über eine grundlegende Verwaltung der Windows-Firewall auf Clientcomputern. Für jedes Netzwerkprofil können Sie die folgenden Einstellungen konfigurieren:  

-   Aktivieren oder Deaktivieren der Windows-Firewall  

-   Blockieren eingehender Verbindungen, einschließlich der in der Liste der zugelassenen Programme aufgeführten Verbindungen  

-   Benachrichtigen des Benutzers, wenn ein neues Programm von der Windows-Firewall blockiert wird  

> [!NOTE]  
>  Von Endpoint Protection wird nur die Verwaltung der Windows-Firewall unterstützt.  


 Weitere Informationen finden Sie unter [Erstellen und Bereitstellen von Windows-Firewallrichtlinien für Endpoint Protection](create-windows-firewall-policies.md).  


## <a name="windows-defender-advanced-threat-protection"></a>Windows Defender Advanced Threat Protection

Endpoint Protection verwaltet und überwacht Windows Defender Advanced Threat Protection (ATP). Der Windows Defender ATP-Dienst unterstützt Unternehmen dabei, erweiterte Angriffe auf Unternehmensnetzwerke zu entdecken, zu untersuchen, und darauf zu reagieren. Weitere Informationen finden Sie unter [Windows Defender Advanced Threat Protection](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Endpoint Protection-Workflow  
 Das folgende Diagramm bringt Ihnen den Workflow zur Implementierung von Endpoint Protection in Ihrer Configuration Manager-Hierarchie näher.  

 ![Endpoint Protection-Workflow](../media/Endpoint-Protection-Workflow.gif)  

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Endpoint Protection-Client für Macintosh-Computer und Linux-Server  
 System Center Endpoint Protection umfasst einen Endpoint Protection-Client für Linux- und Macintosh-Computer. Diese Clients sind nicht im Lieferumfang von Configuration Manager enthalten. Stattdessen müssen Sie die folgenden Produkte aus dem [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx) herunterladen.  

-   System Center Endpoint Protection für den Mac  

-   System Center Endpoint Protection für Linux  


> [!IMPORTANT]  
>  Sie müssen ein Microsoft-Volumenlizenz-Kunde sein, damit Sie die Endpoint Protection-Installationsdateien für Linux und den Macintosh herunterladen können.  

 Diese Produkte können nicht über die Configuration Manager-Konsole verwaltet werden. Allerdings wird mit den Installationsdateien ein System Center Operations Manager-Management Pack bereitgestellt, das es Ihnen ermöglicht, den Client für Linux mit Operations Manager zu verwalten.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Abrufen des Endpoint Protection-Clients für Macintosh-Computer und Linux-Server

Gehen Sie folgendermaßen vor, um die Imagedatei mit der Endpoint Protection-Clientsoftware und Dokumentation für Macintosh-Computer und Linux-Server herunterzuladen.
1. Melden Sie sich beim [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx) an.
2. Wählen Sie die Registerkarte **Downloads and Keys** (Downloads und Schlüssel) oben auf der Website aus.
3. Filtern Sie nach dem Produkt **System Center Endpoint Protection (Current Branch)**.
4. Klicken Sie auf den Link **Herunterladen**.
5. Klicken Sie auf **Continue**(Weiter). Es sollten mehrere Dateien angezeigt werden, einschließlich eine mit der Bezeichnung **System Center Endpoint Protection (current branch - version 1606) for Linux OS and Macintosh OS Multilanguage   32/64 bit   1878 MB ISO** (System Center Endpoint Protection (Current Branch –Version 1606) für Linux- und Mac-Betriebssysteme, mehrsprachig, 32/64 Bit, 1878 MB ISO).
6. Klicken Sie zum Herunterladen der Datei auf das Pfeilsymbol. Der Dateiname lautet **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050.ISO**.

Dieses Update von Januar 2018 (X21-67050) schließt folgende Versionen ein:

- System Center Endpoint Protection für Macintosh 4.5.32.0 (Unterstützung für macOS 10.13 High Sierra)
- System Center Endpoint Protection für Linux 4.5.20.0 

 Weitere Informationen zum Installieren und Verwalten von Endpoint Protection-Clients für Linux- und Macintosh-Computer finden Sie in der begleitenden Dokumentation dieses Produkts. Diese Produktdokumentation ist im Ordner **Dokumentation** der ISO-Datei zu finden.
