---
title: Installieren von Konsolen | Microsoft-Dokumentation
description: "Erfahren Sie mehr zum Installieren von Configuration Manager-Konsolen, um eine Verbindung zu einem Standort der zentralen Verwaltung oder einem primären Standort herzustellen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e3bc8341b384be975098d1b9d7824ef117a47ccb

---
# <a name="install-system-center-configuration-manager-consoles"></a>Installieren von System Center Configuration Manager-Konsolen

*Gilt für: System Center Configuration Manager (Current Branch)*


Administratoren verwenden die System Center Configuration Manager-Konsole zum Verwalten der Configuration Manager-Umgebung. Jede Configuration Manager-Konsole kann eine Verbindung zu einem Standort der zentralen Verwaltung oder einem primären Standort herstellen. Sie können eine Configuration Manager-Konsole jedoch nicht mit einem sekundären Standort verbinden.


> [!NOTE]  
>  Welche Objekte dem Administrator angezeigt werden, der die Konsole ausführt, ist abhängig von den ihm zugewiesenen Berechtigungen. Weitere Informationen zur rollenbasierten Verwaltung finden Sie unter [Grundlagen der rollenbasierten Verwaltung für System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Sie können die Configuration Manager-Konsole während der Installation des Standortservers im Setup-Assistenten installieren oder die eigenständige Anwendung ausführen.  

 Gehen Sie wie folgt vor, um eine Configuration Manager-Konsole mithilfe der eigenständigen Anwendung zu installieren.  

## <a name="to-install-a-configuration-manager-console"></a>So installieren Sie eine Configuration Manager-Konsole  

1.  Vergewissern Sie sich, dass der Administrator, der die Configuration Manager-Konsolenanwendung ausführt, über die folgenden Sicherheitsrechte verfügt:  

    -   **Lokale Administratorrechte** auf dem Computer, auf dem die Konsole ausgeführt wird.  

    -   **Leseberechtigung** für den Speicherort der Installationsdateien der Configuration Manager-Konsole  

2.  Suchen Sie einen der folgenden Speicherorte:  

    -   Navigieren Sie auf dem Configuration Manager-Quellmedium zu **&lt;Configuration Manager-Quelldateien\>\Smssetup\Bin\I386**.  

    -   Navigieren Sie auf dem Standortserver zu **&lt;Installationspfad des Configuration Manager-Standortservers\>\Tools\ConsoleSetup**.  

    > [!TIP]  
    >  Es wird empfohlen, die Installation der Configuration Manager-Konsole statt über das Installationsmedium für System Center Configuration Manager über einen Standortserver zu initiieren. Bei der Installationsmethode für Standortserver werden die Configuration Manager-Konsoleninstallationsdateien sowie die unterstützten Language Packs für den Standort in den Unterordner **Tools\ConsoleSetup** kopiert. Wenn Sie die Configuration Manager-Konsole über das Installationsmedium installieren, wird stets die englische Version installiert, unabhängig von den unterstützten Sprachen auf dem Standortserver oder den Spracheinstellungen für das Betriebssystem auf dem Computer. Optional können Sie den Ordner **ConsoleSetup** an einen anderen Speicherort kopieren, um mit der Installation zu beginnen.  

3.  Doppelklicken Sie auf **consolesetup.exe**. Der Installations-Assistent für die Configuration Manager-Konsole wird geöffnet.  

    > [!IMPORTANT]  
    >  Installieren Sie die Configuration Manager-Konsole immer mithilfe der Datei „consolesetup.exe“. Die Configuration Manager-Konsole kann durch Ausführen von „AdminConsole.msi“ installiert werden. In diesem Fall werden jedoch keine Voraussetzungs- oder Abhängigkeitsprüfungen vorgenommen, sodass die Installation u.U. nicht ordnungsgemäß verläuft.  

4.  Klicken Sie auf der Seite, die geöffnet wird, auf **Weiter**.  

5.  Geben Sie auf der Seite **Standortserver** den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) des Standortservers an, mit dem sich die Configuration Manager-Konsole verbindet.  

6.  Geben Sie auf der Seite **Installationsordner** den Installationsordner für die Configuration Manager-Konsole an. Der Ordnerpfad darf nicht auf Leerzeichen enden und darf keine Unicode-Zeichen enthalten.  

7.  Geben Sie auf der Seite **Programm zur Verbesserung der Benutzerfreundlichkeit** an, ob Sie am Programm zur Verbesserung der Benutzerfreundlichkeit teilnehmen möchten.  

8.  Klicken Sie auf der Seite **Installationsbereit** auf **Installieren**, um die Configuration Manager-Konsole zu installieren.  

## <a name="to-install-a-configuration-manager-console-from-a-command-prompt"></a>So installieren Sie eine Configuration Manager-Konsole mithilfe einer Eingabeaufforderung  

1.  Öffnen Sie auf dem Server, von dem aus Sie die Configuration Manager-Konsole installieren möchten, ein Eingabeaufforderungsfenster, und wechseln Sie zu einem der folgenden Speicherorte:  

    -   **&lt;Installationspfad des Configuration Manager-Standortservers\>\Tools\ConsoleSetup**  

    -   **&lt;Configuration Manager-Installationsmedium\>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  Wenn Sie eine Configuration Manager-Konsole über eine Eingabeaufforderung installieren, wird stets die englische Version installiert, unabhängig von den Spracheinstellungen für das auf dem Computer ausgeführte Betriebssystem. Wenn Sie die Configuration Manager-Konsole in einer anderen Sprache installieren möchten, müssen Sie sie mithilfe der vorhergehenden Prozedur installieren.  

2.  Geben Sie **consolesetup.exe** ein, und wählen Sie aus den folgenden Befehlszeilenoptionen aus:  

|  .     | Beschreibung     |
  | :------------- | :------------- |
  |/q|Installiert die Configuration Manager-Konsole unbeaufsichtigt Wenn Sie diese Option verwenden, sind die Optionen **EnableSQM**, **TargetDir**und **DefaultSiteServerName** erforderlich.|  
  |/uninstall|Deinstalliert die Configuration Manager-Konsole Sie müssen diese Option zuerst angeben, wenn Sie sie mit der Option **/q** verwenden.|  
  |LangPackDir|Gibt den Pfad zu dem Ordner an, der die Sprachdateien enthält. Sie können die Sprachdateien mit dem **Setup-Downloadprogramm** herunterladen. Wenn Sie diese Option nicht verwenden, wird von Setup im aktuellen Ordner nach dem Sprachordner gesucht. Wenn der Sprachordner nicht gefunden wird, wird nur die Sprache Englisch installiert. Weitere Informationen finden Sie unter [Setup-Downloadprogramm](/sccm/core/servers/deploy/install/setup-downloader).|  
  |TargetDir|Gibt den Installationsordner zur Installation der Configuration Manager-Konsole an. Diese Option ist erforderlich, wenn Sie die Option **/q** verwenden.|  
  |EnableSQM|Hiermit wird angegeben, ob Sie am Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP) teilnehmen möchten. Geben Sie den Wert 1 an, wenn Sie am Programm teilnehmen möchten. Geben Sie den Wert 0 an, wenn Sie nicht teilnehmen möchten. Diese Option ist erforderlich, wenn Sie die Option **/q** verwenden.|  
  |DefaultSiteServerName|Damit wird der FQDN des Standortservers angegeben, mit dem beim Start der Konsole eine Verbindung hergestellt wird. Diese Option ist erforderlich, wenn Sie die Option **/q** verwenden.|  


  **Anwendungsbeispiele:**  
  -  **consolesetup.exe /q TargetDir="D:\Programme\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Programme\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  



<!--HONumber=Dec16_HO3-->


