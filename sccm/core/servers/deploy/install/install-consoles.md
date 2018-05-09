---
title: Installieren der Konsole
titleSuffix: Configuration Manager
description: Installieren Sie die Configuration Manager-Konsole, um eine Verbindung zu einem Standort der zentralen Verwaltung oder einem primären Standort herzustellen.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f17e479ef6b285cdb70960471dced73e83af520c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="install-the-system-center-configuration-manager-console"></a>Installieren der System Center Configuration Manager-Konsole

*Gilt für: System Center Configuration Manager (Current Branch)*

Administratoren verwenden die Configuration Manager-Konsole zum Verwalten der Configuration Manager-Umgebung. Jede Configuration Manager-Konsole kann eine Verbindung zu einem Standort der zentralen Verwaltung oder zu einem primären Standort herstellen. Sie können eine Configuration Manager-Konsole jedoch nicht mit einem sekundären Standort verbinden.

> [!NOTE]  
>  Administratoren werden Objekte in der Konsole entsprechend den Berechtigungen angezeigt, die ihren Benutzerkonten zugewiesen sind. Weitere Informationen zur rollenbasierten Verwaltung finden Sie unter [Grundlagen der rollenbasierten Verwaltung](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Beim Installieren des Standortservers können Sie auch die Configuration Manager-Konsole installieren. Wenn Sie die Konsole und den Standortserver getrennt voneinander installieren möchten, müssen Sie den eigenständigen Installer verwenden.  

 In den folgenden Anleitungen wird beschrieben, wie Sie die Configuration Manager-Konsole mit dem eigenständigen Installer installieren.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>So installieren Sie die Configuration Manager-Konsole mithilfe des Setup-Assistenten  

1.  Stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:  

    -  Sie verfügen über **lokale Administratorrechte** auf dem Zielcomputer für die Konsole.  

    -   Sie haben eine **Leseberechtigung** für den Speicherort der Installationsdateien der Configuration Manager-Konsole.  

2.  Wechseln Sie zu einem der folgenden Speicherorte:  

    -   Navigieren Sie auf dem Standortserver zu `<Configuration Manager site server installation path>\Tools\ConsoleSetup`.  

    -   Navigieren Sie über das Quellmedium in Configuration Manager zu `<Configuration Manager source files>\Smssetup\Bin\I386`.  

    > [!TIP]  
    >  Es wird empfohlen, den Installer für die Configuration Manager-Konsole nicht über das Installationsmedium für System Center Configuration Manager, sondern über einen Standortserver zu starten. Bei der Installation eines Standortservers werden die Installationsdateien für die Configuration Manager-Konsole und die unterstützten Sprachpakete für den Standort in den Unterordner **Tools\ConsoleSetup** kopiert. Bei der Installation der Configuration Manager-Konsole über das Installationsmedium wird immer die englische Version installiert. Dieses Verhalten tritt auch dann auf, wenn der Standortserver verschiedene Sprachen unterstützt oder für das Betriebssystem des Zielcomputers eine andere Sprache festgelegt wird. Optional können Sie den Ordner **ConsoleSetup** an einen anderen Speicherort kopieren, um mit der Installation zu beginnen.

3.  Um den Setup-Assistenten für die Configuration Manager-Konsole zu öffnen, doppelklicken Sie auf **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Installieren Sie die Configuration Manager-Konsole immer mithilfe der Datei **consolesetup.exe**. Sie können die Configuration Manager-Konsole zwar auch mit „adminconsole.msi“ installieren, jedoch finden dabei keine Überprüfungen auf erforderliche Komponenten oder Abhängigkeiten statt. Das Installationsprogramm wird in diesem Fall möglicherweise nicht korrekt ausgeführt.  

4.  Wählen Sie im Assistenten **Weiter** aus.  

5.  Geben Sie auf der Seite **Standortserver** den vollqualifizierten Domänennamen (FQDN) des Standortservers an, mit dem sich die Configuration Manager-Konsole verbindet.  

6.  Geben Sie auf der Seite **Installationsordner** den Installationsordner für die Configuration Manager-Konsole ein. Der Ordnerpfad darf nicht auf Leerzeichen enden und darf keine Unicode-Zeichen enthalten.  

7.  Wählen Sie auf der Seite **Programm zur Verbesserung der Benutzerfreundlichkeit** (CEIP) aus, ob Sie an diesem Programm teilnehmen möchten.  
    > [!Note]  
    > Ab Configuration Manager Version 1802 ist das CEIP-Feature nicht mehr im Produkt enthalten.

8.  Wählen Sie auf der Seite **Installationsbereit** die Option **Installieren** aus, um die Configuration Manager-Konsole zu installieren.  



## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>So installieren Sie die Configuration Manager-Konsole mithilfe einer Eingabeaufforderung  

1.  Öffnen Sie auf dem Server, über den Sie die Configuration Manager-Konsole installieren möchten, ein Eingabeaufforderungsfenster, und navigieren Sie zu einem der folgenden Speicherorte:  

    -   `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    > [!TIP]  
    >  Bei der Installation der Configuration Manager-Konsole über eine Befehlszeile wird immer die englische Version installiert. Dieses Verhalten tritt auch dann auf, wenn für das Betriebssystem des Zielcomputers eine andere Sprache festgelegt wird. Um die Configuration Manager-Konsole in einer anderen Sprache als Englisch zu installieren, müssen Sie die [Configuration Manager-Konsole mithilfe des Setup-Assistenten installieren](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  Geben Sie an der Eingabeaufforderung den Befehl **consolesetup.exe** ein. Verwenden Sie eine der folgenden Befehlszeilenoptionen:  

|  .     | Beschreibung     |
  |-------------|-------------|
  |/q|Installiert die Configuration Manager-Konsole unbeaufsichtigt Wenn Sie diese Option verwenden, sind die Optionen **EnableSQM**, **TargetDir**und **DefaultSiteServerName** erforderlich.|  
  |/uninstall|Deinstalliert die Configuration Manager-Konsole Sie müssen diese Option zuerst angeben, wenn Sie sie mit der Option **/q** verwenden.|  
  |LangPackDir|Gibt den Pfad zu dem Ordner an, der die Sprachdateien enthält. Sie können die Sprachdateien mit dem **Setup-Downloadprogramm** herunterladen. Wenn Sie diese Option nicht verwenden, wird von Setup im aktuellen Ordner nach dem Sprachordner gesucht. Wenn der Sprachordner nicht gefunden wird, wird nur die Sprache Englisch installiert. Weitere Informationen finden Sie unter [Setup-Downloadprogramm](setup-downloader.md).|  
  |TargetDir|Gibt den Installationsordner zur Installation der Configuration Manager-Konsole an. Diese Option ist erforderlich, wenn Sie die Option **/q** verwenden.|  
  |EnableSQM|Hiermit wird angegeben, ob Sie am Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP) teilnehmen möchten. Verwenden Sie den Wert **1**, um die CEIP-Funktion zu verknüpfen, und den Wert **0**, um nicht am Programm teilzunehmen. Diese Option ist erforderlich, wenn Sie die Option **/q** verwenden.</br></br>Hinweis: Ab Configuration Manager Version 1802 ist das CEIP-Feature nicht mehr im Produkt enthalten.|  
  |DefaultSiteServerName|Damit wird der FQDN des Standortservers angegeben, mit dem beim Start der Konsole eine Verbindung hergestellt wird. Diese Option ist erforderlich, wenn Sie die Option **/q** verwenden.|  


  ### <a name="examples"></a>Beispiele

  -  `consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com`  

  -  `consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr Console" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com`  

  -  `consolesetup.exe /uninstall /q`  
