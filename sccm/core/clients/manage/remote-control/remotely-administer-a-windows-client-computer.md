---
title: Remoteverwaltung eines Windows-Computers | System Center Configuration Manager
description: "Mit System Center Configuration Manager können Windows-Remoteclientcomputer verwaltet werden."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 02c11420d3b05ad4eaae31d9413b66459751da70
ms.openlocfilehash: 51a9b7269993bfa133382b88792ac94032824eed


---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-system-center-configuration-manager"></a>Remoteverwaltung eines Windows-Clientcomputers mithilfe von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Gehen Sie wie folgt vor, um einen Computer in System Center Configuration Manager remote zu verwalten.  

 Bevor Sie die Remotesteuerung einsetzen, sollten Sie die folgenden Themen durchgehen:  

-   [Voraussetzungen für die Remotesteuerung in System Center Configuration Manager](../../../../core/clients/manage/remote-control/prerequisites-for-remote-control.md)  

-   [Configuring remote control in System Center Configuration Manager (Konfigurieren der Remotesteuerung in System Center Configuration Manager)](../../../../core/clients/manage/remote-control/configuring-remote-control.md)  

 Sie können den Configuration Manager-Remotesteuerungsviewer auf drei Arten starten:  

-   Mithilfe der Configuration Manager-Konsole  

-   Über die Windows-Eingabeaufforderung.  

-   Mithilfe des Windows-Menüs **Start** eines Computers, auf dem die Configuration Manager-Konsole aus der Programmgruppe **Microsoft System Center 2012** ausgeführt wird  

### <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>So verwalten Sie einen Clientcomputer remote mit der Configuration Manager-Konsole  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Geräte** oder **Gerätesammlungen**.  

3.  Wählen Sie den Computer aus, der remote verwaltet werden soll. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Geräte** auf **Starten**und dann auf **Remotesteuerung**.  

    > [!IMPORTANT]  
    >  Wenn die Clienteinstellung **Benutzer zur Vergabe der Berechtigung für Remotesteuerung auffordern** auf **Wahr**festgelegt ist, wird eine Verbindung erst dann hergestellt, wenn der Benutzer am Remotecomputer der Remotesteuerungsaufforderung zustimmt. Weitere Informationen finden Sie unter [Configuring remote control in System Center Configuration Manager (Konfigurieren der Remotesteuerung in System Center Configuration Manager)](../../../../core/clients/manage/remote-control/configuring-remote-control.md).  

4.  Wenn das Fenster **Configuration Manager-Remotesteuerung** geöffnet ist, können Sie den Clientcomputer remote verwalten. Verwenden Sie die folgenden Optionen zum Konfigurieren der Verbindung.  

    > [!NOTE]  
    >  Wenn der Computer, mit dem eine Verbindung hergestellt wird, über mehrere Monitore verfügt, wird der Inhalt all dieser Monitore im Remotesteuerungsfenster angezeigt.  

    -   **Datei – Verbinden**: Verbinden mit einem anderen Computer. Diese Option ist nicht verfügbar, wenn eine Remotesteuerungssitzung aktiv ist.  

    -   **Datei – Verbindung trennen**: Beenden der aktiven Remotesteuerungssitzung. Das Fenster **Configuration Manager-Remotesteuerung** wird nicht geschlossen.  

    -   **Datei – Beenden**: Beenden der aktiven Remotesteuerungssitzung. Das Fenster **Configuration Manager-Remotesteuerung** wird geschlossen.  

        > [!NOTE]  
        >  Wenn eine Remotesteuerungssitzung beendet wird, werden die Inhalte der Zwischenablage von Windows auf dem Computer gelöscht, der angezeigt wird.  

    -   **Anzeigen – Vollbild**: Maximieren des Fensters **Configuration Manager-Remotesteuerung**, um den verfügbaren Anzeigebereich zu nutzen.  

        > [!NOTE]  
        >  Drücken Sie STRG+ALT+UNTBR, um den Vollbildmodus zu beenden.  

    -   **Anzeige – Skalierung anpassen**: Skalieren der Anzeige des Remotecomputers auf die Größe des Fensters **Configuration Manager-Remotesteuerung**.  

    -   **Anzeige – Statusleiste**: Ein-/Ausschalten der Anzeige der Fensterstatusleiste des Fensters **Configuration Manager-Remotesteuerung**.  

    -   **Aktion – STRG+ALT+ENTF senden**: Senden der Tastenkombination STRG+ALT+ENTF an den Remotecomputer.  

    -   **Aktion – Freigabe der Zwischenablage aktivieren**: Zulassen des Kopierens und Einfügens von Elementen vom/auf dem Remotecomputer. Wenn dieser Wert geändert wird, muss die Remotesteuerungssitzung neu gestartet werden, damit die Änderung wirksam wird.  

        > [!NOTE]  
        >  Wenn die Freigabe der Zwischenablage in der Configuration Manager-Konsole nicht aktiviert sein soll, legen Sie auf dem Computer, auf dem die Konsole ausgeführt wird, den Wert des Registrierungsschlüssels **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** auf **0**fest.  

    -   **Aktion – Remotetastatur und Maus sperren**: Sperren von Remotetastatur und Remotemaus, um den Benutzer an der Bedienung des Remotecomputers zu hindern.  

    -   **Hilfe – Info**: Anzeigen von Informationen über die aktuelle Version des Remotesteuerungsviewers.  

5.  Benutzer am Remotecomputer können mehr Informationen über die Remotesteuerungssitzung anzeigen, indem sie in Configuration Manager auf das Symbol **Remotesteuerung** im Infobereich von Windows oder auf das Symbol auf der Leiste der Remotesteuerungssitzung klicken.  

6.  Wenn die Remotesteuerungssitzung nicht mehr benötigt wird, verwenden Sie eine der zuvor beschriebenen Methoden, um die Remotesteuerungssitzung zu beenden.  

### <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>So starten Sie den Remotesteuerungsviewer von der Windows-Befehlszeile aus  

-   Geben Sie an der Windows-Eingabeaufforderung *<Configuration Manager-Installationsordner\>***\AdminConsole\Bin\x64\CmRcViewer.exe** ein.  

    > [!NOTE]  
    >  Folgende Befehlszeilenoptionen werden von CmRcViewer.exe unterstützt:  
    >   
    >  -   *<Adresse\>*: Gibt den NetBIOS-Namen, den vollqualifizierten Domänennamen (FQDN) oder die IP-Adresse des Clientcomputers an, mit dem eine Verbindung hergestellt werden soll.  
    > -   *<Standortservername\>*: Gibt den Namen des System Center 2012 Configuration Manager-Standortservers an, an den Statusmeldungen im Zusammenhang mit der Remotesteuerungssitzung gesendet werden sollen.  
    > -   **/?** : Zeigt die Befehlszeilenoptionen für den Remotesteuerungsviewer an.  
    >   
    >  **Beispiel: CmRcViewer.exe** *<Adresse\>* *<\\\Name des Standortservers>*  



<!--HONumber=Nov16_HO1-->

