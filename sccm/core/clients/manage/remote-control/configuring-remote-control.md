---
title: Konfigurieren der Remotesteuerung
titleSuffix: Configuration Manager
description: Richten Sie die Remotesteuerung in System Center Configuration Manager ein.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
caps.latest.revision: 4
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: b5183f64a4793d2d24fec71a29ceaf0148446a36
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/12/2017
---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Konfigurieren der Remotesteuerung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

 In diesem Verfahren wird die Konfiguration der Clientstandardeinstellungen für die Remotesteuerung beschrieben. Diese Einstellungen gelten für alle Computer in der Hierarchie. Wenn diese Einstellungen nur auf manche Computer angewendet werden sollen, weisen Sie eine benutzerdefinierte Geräteclienteinstellung einer Sammlung mit diesen Computern zu. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md). 

Für die Verwendung der Remoteunterstützung oder des Remotedesktops müssen sie auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, installiert und konfiguriert sein. Weitere Informationen zum Installieren und Konfigurieren der Remoteunterstützung oder des Remotedesktops finden Sie in der Windows-Dokumentation.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>So aktivieren Sie die Remotesteuerung und konfigurieren die Clienteinstellungen  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

5.  Wählen Sie im Dialogfeld **Standard** die Option **Remotetools** aus.  

6.  Konfigurieren Sie die Remotesteuerungs-, Remoteunterstützungs- und Remotedesktop-Clienteinstellungen. Eine Liste der Remotetools-Clienteinstellungen, die Sie konfigurieren können, finden Sie unter [Remotetools](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

    Sie können den Firmennamen ändern, der im Dialogfeld **ConfigMgr-Remotesteuerung** angezeigt wird, indem Sie in den Clienteinstellungen **Computer-Agent** einen Wert für **Im Softwarecenter angezeigter Organisationsname** konfigurieren.  

 Die Clientcomputer werden beim nächsten Download der Clientrichtlinien mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Abrufens von Richtlinien für einen einzelnen Client finden Sie unter [Verwalten von Clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

#### <a name="enable-keyboard-translation"></a>Aktivieren der Tastaturübersetzung

Standardmäßig überträgt Configuration Manager die Schlüsselposition vom Standort des anzeigenden Benutzers an den Standort des freigebenden Benutzers. Dies kann zu Problemen führen, wenn die Tastaturkonfiguration des anzeigenden Benutzers von der des freigebenden Benutzers abweicht. Beispielsweise würde ein anzeigender Benutzer mit einer englischen Tastatur ein „A“ eingeben, die französische Tastatur des freigebenden Benutzers würde jedoch ein „Q“ bereitstellen. Sie haben jetzt die Möglichkeit, die Remotesteuerung so zu konfigurieren, dass das Zeichen selbst von der Tastatur des anzeigenden Benutzers an den freigebenden Benutzer übertragen wird. Beim freigebenden Benutzer kommt das an, was der anzeigende Benutzer beabsichtigt einzugeben.

Wählen Sie zum Aktivieren der Tastaturübersetzung in **Configuration Manager-Remotesteuerung** **Aktion** und **Enable keyboard translation** (Tastaturübersetzung aktivieren) aus, um die Schlüsselposition zu übertragen.

> [!NOTE]
>
> Spezielle Schlüssel wie z.B. ~!#@$% werden nicht richtig übersetzt.


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>Tastenkombinationen für den Remotesteuerungsviewer

|Tastenkombination|Beschreibung|  
|-----------------------|-----------------|  
|ALT+BILD-AUF|Wechselt zwischen gerade ausgeführten Programmen von links nach rechts.|  
|ALT+BILD-AB|Wechselt zwischen gerade ausgeführten Programmen von rechts nach links.|  
|ALT+EINFG|Wechselt zwischen gerade ausgeführten Programmen in der Reihenfolge, in der sie geöffnet wurden.|  
|ALT+POS1|Zeigt das Menü **Start** an.|  
|STRG+ALT+ENDE|Zeigt das Dialogfeld "Windows-Sicherheit" an (STRG+ALT+ENTF).|  
|ALT+ENTF|Zeigt das Windows-Menü an.|  
|STRG+ALT+Minuszeichen (auf der Zehnertastatur)|Kopiert das aktive Fenster des lokalen Computers in die Zwischenablage des Remotecomputers.|  
|STRG+ALT+Pluszeichen (auf der Zehnertastatur)|Kopiert den gesamten Fensterbereich des lokalen Computers in die Zwischenablage des Remotecomputers.|  
