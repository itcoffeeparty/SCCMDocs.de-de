---
title: MDT-Beispiele
titleSuffix: Microsoft Deployment Toolkit
description: 'Beispiele zum Microsoft Deployment Toolkit (MDT) '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 2ff0100c-b7ef-4e09-8c96-fc1898390b6d
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: fe61cecea2b2a4f4083933b937af90dfb61ea5bf
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2018
---
# <a name="microsoft-deployment-toolkit-samples-guide"></a>Leitfaden mit Beispielen zum Microsoft Deployment Toolkit (MDT)  
 Dieser Leitfaden ist Teil des Microsoft® Deployment Toolkit 2013 (MDT) und soll Spezialisten durch die Bereitstellung von Windows-Betriebssystemen und Microsoft Office führen. Dieser Leitfaden dient insbesondere mit Beispielen für Konfigurationseinstellungen für spezifische Bereitstellungsszenarios.  

> [!NOTE]
>  In diesem Dokument bezieht sich *Windows* auf die Betriebssysteme Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012, und Windows Server 2008 R2, sofern nichts anderes angegeben ist. Das MDT unterstützt keine Windows-Versionen, die auf ARM-Prozessoren basieren. Ebenso bezieht sich *MDT* auf das MDT 2013, sofern nicht anders angegeben.  

 **Verwenden dieses Leitfadens**  

 Sehen Sie sich die Liste der unterschiedlichen Themen im Inhaltsverzeichnis an.  

1.  Wählen Sie das Szenario aus, das den Bereitstellungszielen Ihrer Organisation am ehesten entspricht.  

2.  Überprüfen Sie die Beispielkonfigurationseinstellungen des ausgewählten Szenarios.  

3.  Verwenden Sie die Beispielkonfigurationseinstellungen als Grundlage für die Konfigurationseinstellungen Ihrer Umgebung.  

4.  Passen Sie die Beispielkonfigurationseinstellungen für Ihre Umgebung an.  

 In vielen Fällen können mehrere Szenarios erforderlich sein, um die Konfigurationseinstellungen für die Umgebung zu vervollständigen.  

 Da dieser Leitfaden nur Beispielkonfigurationseinstellungen enthält, können die in der folgenden Tabelle aufgelisteten Anleitungen Sie weiterhin bei der Anpassung der Konfigurationseinstellungen für die Umgebung unterstützen.  

 |Handbuch|Dieses Handbuch unterstützt Sie bei Folgendem:|  
 |-|-|  
 |*Schnellstarthandbuch für Microsoft System Center 2012 R2 Configuration Manager* |Verwendung von System Center 2012 R2 Configuration Manager zum Installieren von Windows 8.1 in einem Bereitstellungsszenario für einen neuen Computer.|  
 |*Schnellstarthandbuch für die Installation von Lite Touch* |Installieren von Windows 8.1 durch die Lite Touch-Installation (LTI) mithilfe von startbaren Medien in einem Bereitstellungsszenario für einen neuen Computer.|  
 |*Schnellstarthandbuch für benutzergesteuerte Installation* |Installieren von Windows 8.1 mit benutzergesteuerter Installation und System Center 2012 R2 Configuration Manager in einem Bereitstellungsszenario für einen neuen Computer.|  
 |*Verwenden des Microsoft Deployment Toolkits* |Weiteres Anpassen der Konfigurationsdateien, die in Bereitstellungen der Zero Touch-Installation (ZTI) und LTI verwendet werden. Dieser Leitfaden enthält auch allgemeine Konfigurationsrichtlinien und eine technische Referenz für Konfigurationseinstellungen.|


## <a name="deploying-windows-8-applications-using-mdt"></a>Bereitstellen von Windows 8-Anwendungen unter Verwendung des MDT  
 Das MDT kann Windows 8-Anwendungspakete bereitstellen, die über die APPX-Dateierweiterung verfügen. Diese Anwendungspakete sind neu in Windows 8. Weitere Informationen zu diesen Anwendungen finden Sie unter [Entwickeln von Windows Store-Apps](http://msdn.microsoft.com/windows/apps).  

 Stellen Sie Windows 8-Anwendungen mit dem MDT bereit, indem Sie die folgenden Schritte ausführen:  

-   Stellen Sie Windows 8-Anwendungen, wie unter [Bereitstellen von Windows 8-Anwendungen mithilfe von LTI](#DeployWin8LTI) beschrieben, mit LTI bereit.  

-   Stellen Sie Windows 8-Anwendungen, wie unter [Bereitstellen von Windows 8-Anwendungen mithilfe von UDI](#DeployWin8UDI) beschrieben, mit der benutzergesteuerten Installation (User-Driven Installation, UDI) bereit.  

###  <a name="DeployWin8LTI"></a> Bereitstellen von Windows 8-Anwendungen mit LTI  
 Sie können Windows 8-Anwendungen erstellen, indem Sie LTI wie jede andere Anwendung verwenden, die den Installationsvorgang über eine Befehlszeile starten. Sie können LTI-Bereitstellungen Windows 8-Anwendungen im Anwendungsknoten in der Deployment Workbench hinzufügen.  

 **Bereitstellen einer Windows 8-Anwendung mit LTI**  

1.  Erstellen Sie einen freigegebenen Netzwerkordner, in dem die Anwendung gespeichert wird.  

2.  Kopieren Sie die Windows 8-Anwendung in den freigegebenen Netzwerkordner, den Sie im vorherigen Schritt erstellt haben.  

     Stellen Sie sicher, dass Sie die APPX-Datei der Windows 8-Anwendung und alle anderen erforderlichen Dateien kopieren, z.B. eine CER-Datei, die das Anwendungszertifikat enthält.  

3.  Erstellen Sie ein LTI-Anwendungselement für die Windows 8-Anwendung im Anwendungsknoten in der Deployment Workbench mithilfe des Assistenten für neue Anwendungen.  

     Geben Sie **app_file_name** auf der Assistentenseite **Befehlsdetails** in der **Befehlszeile** ein, wenn Sie den Assistenten für neue Anwendungen abschließen (*app_file_name* entspricht dabei dem Namen der Windows 8-Anwendung).  

     Weitere Informationen zum Abschließen des Assistenten für neue Anwendungen in der Deployment Workbench finden Sie in den folgenden Abschnitten der MDT-Dokumentation *Verwenden des Microsoft Deployment Toolkits*:  

    -   „Create a New Application That Is Deployed from the Deployment Share (Erstellen einer neuen Anwendung, die über die Bereitstellungsfreigabe bereitgestellt wird)“  

    -   „Create a New Application That Is Deployed from Another Network Shared Folder (Erstellen einer neuen Anwendung, die über einen anderen freigegebenen Netzwerkordner bereitgestellt wird)“  

4.  Wählen Sie das zuvor erstellte LTI-Anwendungselement in einer LTI-Tasksequenz aus.  

###  <a name="DeployWin8UDI"></a> Bereitstellen von Windows 8-Anwendungen mit UDI  
 Sie können Windows 8-Anwendungen erstellen, indem Sie UDI wie jede andere Anwendung verwenden, die den Installationsvorgang über eine Befehlszeile starten. Sie können UDI-Bereitstellungen Windows 8-Anwendungen in der Assistentenseite **ApplicationPage** im Designer des UDI-Assistenten hinzufügen.  

> [!NOTE]
>  Die Bereitstellung von Windows 8 und Windows 8-Anwendungen mit UDI erfordert System Center 2012 R2 Configuration Manager.  

 **Bereitstellen einer Windows 8-Anwendung mit UDI**  

1.  Erstellen Sie einen freigegebenen Netzwerkordner, in dem die Anwendung gespeichert wird.  

     Dieser Ordner wird der Quellordner für die Configuration Manager-Anwendung sein, die Sie im späteren Verlauf erstellen.  

2.  Kopieren Sie die Windows 8-Anwendung in den freigegebenen Netzwerkordner, den Sie im vorherigen Schritt erstellt haben.  

     Stellen Sie sicher, dass Sie die APPX-Datei der Windows 8-Anwendung und alle anderen erforderlichen Dateien kopieren, z.B. eine CER-Datei, die das Anwendungszertifikat enthält.  

3.  Fügen Sie die Windows 8-Anwendung als eine Configuration Manager-Anwendung hinzu.  

4.  Erstellen Sie ein Configuration Manager-Anwendungselement für die Windows 8-Anwendung mithilfe des Assistenten zum Erstellen von Anwendungen in der Configuration Manager-Konsole.  

     Erstellen Sie einen Bereitstellungstyp zum Bereitstellen der Windows 8-Anwendung mithilfe des Assistenten zum Erstellen neuer Bereitstellungstypen, während Sie den Assistenten zum Erstellen von Anwendungen abschließen. Geben Sie auf der Seite **Inhalt** des Assistenten zum Erstellen neuer Bereitstellungstypen **app_file_name** in das **Installationsprogramm** ein (*app_file_name* entspricht dem Namen der Windows 8-Anwendung).  

     Weitere Informationen zum Abschließen des Assistenten zum Erstellen einer Anwendung in der Configuration Manager-Konsole finden Sie in den folgenden Abschnitten der Dokumentationsbibliothek für System Center 2012 Configuration Manager, die in Configuration Manager enthalten ist:  

    -   [Erstellen von Anwendungen in Configuration Manager](http://technet.microsoft.com/library/gg682159.aspx)  

    -   [Erstellen von Bereitstellungstypen in Configuration Manager](http://technet.microsoft.com/library/gg682174.aspx#BKMK_Step3)  

    -   [Verwalten von Anwendungen und Bereitstellungstypen in Configuration Manager](http://technet.microsoft.com/library/gg682031)  

5.  Stellen Sie sicher, dass das Feature „Affinität zwischen Benutzer und Gerät (UDA)“ in Configuration Manager ordnungsgemäß konfiguriert ist, um die Affinität zwischen Benutzer und Gerät für die Bereitstellung der Configuration Manager-Anwendung zu unterstützen.  

     Weitere Informationen zum Konfigurieren der Affinität zwischen Benutzer und Gerät zum Unterstützen der Configuration Manager-Anwendungsbereitstellung finden Sie unter [Verwalten der Affinität zwischen Benutzer und Gerät in Configuration Manager](http://technet.microsoft.com/library/gg699365).  

6.  Stellen Sie die in Schritt 4 erstellte Anwendung für die Zielbenutzer bereit.  

     Weitere Informationen zum Bereitstellen einer Anwendung für Benutzer finden Sie unter [Bereitstellen von Anwendungen in Configuration Manager](http://technet.microsoft.com/library/gg682082).  

7.  Konfigurieren Sie die Assistentenseite **ApplicationPage**, um die in Schritt 4 erstellte Configuration Manager-Anwendung mithilfe des Designers für den UDI-Assistenten zu enthalten.  

     Weitere Informationen zum Konfigurieren der Assistentenseite **ApplicationPage** mithilfe des Designers für den UDI-Assistenten finden Sie im Abschnitt „Step 5-11: Customize the UDI Wizard Configuration File for the Target Computer (Schritt 5-11: Anpassen der Konfigurationsdatei des UDI-Assistenten für den Zielcomputer)“ in der MDT-Dokumentation *Quick start Guide for User-Driven Installation (Schnellstarthandbuch für die benutzergesteuerte Installation)*.  

8.  Wählen Sie das zuvor erstellte UDI-Anwendungselement in einer UDI-Tasksequenz aus.  

    > [!NOTE]
    >  Die Windows 8-Anwendung wird nicht durch die Tasksequenz installiert, sondern über das Feature „benutzerzentrierter App-Installer“ (AppInstall.exe) in UDI, wenn der Benutzer sich zum ersten Mal am Zielcomputer anmeldet (gemäß der UDA-Einstellung, die Sie in Schritt 5 konfiguriert haben).  

     Weitere Informationen zum Feature „benutzerzentrierter App-Installer“ in UDI finden Sie im Abschnitt „User-Centric App Installer Reference (Referenz für den benutzerzentrierten App-Installer)“ in der MDT-Dokumentation *Toolkit Reference (Toolkit-Referenz)*.  

## <a name="managing-mdt-using-windows-powershell"></a>Verwalten des MDT mithilfe von Windows PowerShell  
 Sie können MDT-Bereitstellungsfreigaben mithilfe der Deployment Workbench und Windows PowerShell verwalten. Das MDT enthält ein Windows PowerShell™-Snap-In (Microsoft.BDD.SnapIn), das geladen werden muss, bevor MDT-spezifische Features in Windows PowerShell verwendet werden. Folgendes ist im Windows PowerShell-Snap-In des MDT enthalten:  

-   Ein Windows PowerShell-Anbieter (MDTProvider), der den Zugriff auf die Inhalte einer Bereitstellungsfreigabe bietet.  

-   Cmdlets, die die Fähigkeit zum Verwalten von Bereitstellungsfreigaben gewähren.  

 Verwalten Sie MDT-Bereitstellungsfreigaben mithilfe von Windows PowerShell, indem Sie folgende Schritte ausführen:  

-   Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

-   Erstellen Sie, wie unter [Creating a Deployment Share Using Windows PowerShell (Erstellen einer Bereitstellungsfreigabe mithilfe von Windows PowerShell)](#CreateDeployShare) beschrieben, eine Bereitstellungsfreigabe mithilfe von Windows PowerShell.  

-   Zeigen Sie, wie unter [Viewing Deployment Share Properties Using Windows PowerShell (Anzeigen der Eigenschaften einer Bereitstellungsfreigabe mithilfe von Windows PowerShell)](#ViewDeployShareProp) beschrieben, Eigenschaften einer Bereitstellungsfreigabe mithilfe von Windows PowerShell an.  

-   Zeigen Sie die Liste der Bereitstellungsfreigaben, wie unter [Viewing the List of Deployment Shares Using Windows PowerShell (Anzeigen der Liste von Bereitstellungsfreigaben mithilfe von Windows PowerShell)](#ViewListDeployShare) beschrieben, mithilfe von Windows PowerShell an.  

-   Aktualisieren Sie eine Bereitstellungsfreigabe, die Startimages von Windows Preinstallation Environment (Windows PE) neu generiert, wie unter [Updating a Deployment Share Using Windows PowerShell (Aktualisieren einer Bereitstellungsfreigabe mithilfe von Windows PowerShell)](#UpdateDeployShare) beschrieben.  

-   Aktualisieren Sie eine verknüpfte Bereitstellungsfreigabe, die Inhalte aus einer Bereitstellungsfreigabe in die verknüpfte Bereitstellungsfreigabe repliziert, wie unter [Updating a Linked Deployment Share Using Windows PowerShell (Aktualisieren einer verknüpften Bereitstellungsfreigabe mithilfe von Windows PowerShell)](#UpdateLinkedDeployShare) beschrieben.  

-   Aktualisieren Sie Bereitstellungsmedien, die Inhalte von einer Bereitstellungsfreigabe in das Bereitstellungsmedium replizieren und dann neue startbare Images generieren, wie unter [Updating Deployment Media Using Windows PowerShell (Aktualisieren von Bereitstellungsmedien mithilfe von Windows PowerShell)](#UpdateDeployMedia) beschrieben.  

-   Verwalten Sie Elemente in einer Bereitstellungsfreigabe (z.B. Betriebssysteme, Betriebssystempakete, Anwendungen und Gerätetreiber) wie unter [Managing Items in a Deployment Share Using Windows PowerShell (Verwalten von Elementen in einer Bereitstellungsfreigabe mithilfe von Windows PowerShell)](#ManageItemDeployShare) beschrieben.  

-   Automatisieren Sie die Auffüllung von Elementen in einer Bereitstellungsfreigabe (z.B. Betriebssysteme, Betriebssystempakete, Anwendungen und Gerätetreiber) wie unter [Automating Population of a Deployment Share (Automatisieren der Auffüllung einer Bereitstellungsfreigabe)](#AutomatePopulateDeployShare) beschrieben.  

-   Verwalten Sie die Ordner in einer Bereitstellungsfreigabe mithilfe von Windows PowerShell wie unter [Managing Deployment Share Folders Using Windows PowerShell (Verwalten von Bereitstellungsfreigabe-Ordnern mithilfe von Windows PowerShell)](#ManageDeployShareFolder) beschrieben.  

###  <a name="LoadMDTSnapIn"></a> Laden des Windows PowerShell-Snap-Ins des MDT  
 Die MDT-Cmdlets werden in dem Windows PowerShell-Snap-In **Microsoft.BDD.SnapIn** zur Verfügung gestellt, das vor der Verwendung der MDT-Cmdlets geladen werden muss. Sie können das Windows PowerShell-Snap-In des MDT mithilfe einer der folgenden Methoden laden:  

-   Laden Sie das Windows PowerShell-Snap-In des MDT mithilfe der Konsole für Windows PowerShell-Module wie unter [Load the MDT Windows PowerShell Snap-In Using the Import System Modules Task (Laden des Windows PowerShell-Snap-Ins des MDT mithilfe des Tasks „Systemmodule importieren“)](#LoadMDTSnapInImport) beschrieben.  

-   Laden Sie das Windows PowerShell-Snap-In des MDT, wie unter [Load the MDT Windows PowerShell Snap-In Using the Add-PSSnapIn Cmdlet (Laden des Windows PowerShell-Snap-Ins des MDT mithilfe des Cmdlets „Add-PSSnapIn“)](#LoadMDTSnapInCmdlet) beschrieben, mithilfe des Cmdlets **Add-PSSnapIn**.  

####  <a name="LoadMDTSnapInImport"></a> Laden des Windows PowerShell-Snap-Ins des MDT mithilfe des Tasks „Systemmodule importieren“  
 Der Task „Systemmodule importieren“ enthält automatisch alle Windows PowerShell-Module und Snap-Ins, die sich in den Modulen im Verzeichnis %Windir%\System32\WindowsPowerShell\1.0\Modules befinden. Während dem Installationsvorgang des MDT wird das Windows PowerShell-Snap-In **Microsoft.BDD.SnapIn** des MDT automatisch in diesem Ordner installiert.  

> [!NOTE]
>  Der Task „Systemmodule importieren“ ist nur in Windows 7 und Windows Server 2008 R2 verfügbar, wenn Windows PowerShell 3.0 nicht auf dem Computer installiert ist. Ab Windows PowerShell 3.0 werden Module automatisch importiert, wenn Sie zum ersten Mal ein Cmdlet in dem Modul verwenden.  

 Sie können eine Windows PowerShell-Konsole mit dem Task „Systemmodule importieren“ starten, indem Sie eine der folgenden Methoden ausführen:  

-   Führen Sie in der Taskleiste einen Rechtsklick auf das **Windows PowerShell**-Symbol aus, und klicken Sie dann auf **Systemmodule importieren**.  

-   Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Windows PowerShell-Module**.  

 Weitere Informationen zum Starten einer Windows PowerShell-Konsole mit „Systemmodule importieren“ finden Sie unter [Starting Windows PowerShell with Import System Modules (Starten von Windows PowerShell mit „Systemmodule importieren“)](http://msdn.microsoft.com/library/windows/desktop/hh847866.aspx).  

####  <a name="LoadMDTSnapInCmdlet"></a> Laden des Windows PowerShell-Snap-Ins des MDT mithilfe des Cmdlets „Add-PSSnapIn“  
 Sie können das Windows PowerShell-Snap-In **Microsoft.BDD.PSSnapIn** des MDT aus einer beliebigen Windows PowerShell-Umgebung mithilfe des Cmdlets [Add-PSSnapIn](http://technet.microsoft.com/library/hh849705.aspx) laden, wie im folgenden Beispiel gezeigt wird:  

```  
Add-PSSnapin -Name Microsoft.BDD.PSSnapIn  
```  

###  <a name="CreateDeployShare"></a> Erstellen einer Bereitstellungsfreigabe mithilfe von Windows PowerShell  
 Sie können Bereitstellungsfreigaben mithilfe von Windows PowerShell-Cmdlets des MDT erstellen. Der Stammordner für die Bereitstellungsfreigabe wird mithilfe von standardmäßigen Windows PowerShell-Cmdlets und Aufrufen von Klassenbefehlen der Windows-Verwaltungsinstrumentation (WMI) erstellt und freigegeben. Die Bereitstellungsfreigabe wird durch den Windows PowerShell-Anbieter „MDTProvider“ und das Cmdlet [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) aufgefüllt. Das Windows PowerShell-Laufwerk „MDTProvider“ wird mithilfe des Cmdlets **Add-MDTPersistentDrive** beibehalten.  

 **So bereiten Sie eine Bereitstellungsfreigabe mithilfe der Windows PowerShell-Cmdlets des MDT vor**  

1.  Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

2.  Erstellen Sie den Ordner, der der Stammordner der neuen Bereitstellungsfreigabe wird, mithilfe des Cmdlets **New-Item**, wie im folgenden Beispiel gezeigt und unter [Verwenden des Cmdlets „New-Item“](http://technet.microsoft.com/library/ee176914.aspx) beschrieben wird:  

    ```  
    New-Item "C:\MDTDeploymentShare$" -Type directory  
    ```  

     Das Cmdlet zeigt an, dass der Ordner erfolgreich erstellt wurde.  

3.  Geben Sie den im vorherigen Schritt erstellten Ordner mit der Klasse **WMI win32_share** frei, wie im folgenden Beispiel gezeigt wird:  

    ```  
    ([wmiclass]"win32_share").Create("C:\MDTDeploymentShare$", "MDTDeploymentShare$",0)  
    ```  

     Der Aufruf der Klasse **win32_share** gibt die Ergebnisse des Aufrufs zurück. Wenn der Wert von **ReturnValue** 0 (null) ist, war der Aufruf erfolgreich.  

4.  Geben Sie den neuen freigegebenen Ordner mithilfe des Cmdlets [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) als Bereitstellungsfreigabe an, wie im folgenden Beispiel gezeigt wird:  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose  
    ```  

     Das Cmdlet beginnt automatisch mit dem Erstellen der Bereitstellungsfreigabe und dem Kopieren der Vorlageinformationen in die neue Bereitstellungsfreigabe. Sobald dieser Kopiervorgang abgeschlossen ist, zeigt das Cmdlet die Informationen für die neue Bereitstellungsfreigabe an.  

    > [!NOTE]
    >  Der Wert im Parameter *Name* (DS002) muss eindeutig sein und darf nicht dem Namen einer vorhandenen Bereitstellungsfreigabe im Windows PowerShell-Laufwerk entsprechen.  

5.  Stellen Sie sicher, dass die entsprechenden Bereitstellungsfreigabeordner mithilfe des Befehls **Dir** erstellt wurden, wie im folgenden Beispiel gezeigt wird:  

    ```  
    dir ds002:  
    ```  

     Die Liste der Standardordner im Stamm der Breitstellungsfreigabe wird angezeigt.  

6.  Fügen Sie die neue Bereitstellungsfreigabe der Liste beständiger Bereitstellungsfreigaben des MDT mithilfe des Cmdlets **Add-MDTPersistentDrive** hinzu, wie im folgenden Beispiel gezeigt wird:  

    ```  
    $NewDS=Get-PSDrive "DS002"  
    Add-MDTPersistentDrive  -Name "DS002" -InputObject $NewDS Verbose  
    ```  

     In diesem Beispiel wird die Variable *$NewDS* verwendet, um das Objekt des Windows PowerShell-Laufwerks für die neue Bereitstellungsfreigabe an das Cmdlet zu übergeben.  

     Alternativ können Sie die Cmdlets [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) und **Add-MDTPersistentDrive** kombinieren, wie im folgenden Beispiel gezeigt wird:  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose | Add-MDTPersistentDrive -Verbose  
    ```  

     Im vorherigen Beispiel stellt die Windows PowerShell-Pipeline die Parameter *Name* und *InputObject* bereit.  

###  <a name="ViewDeployShareProp"></a> Anzeigen der Eigenschaften einer Bereitstellungsfreigabe mithilfe von Windows PowerShell  
 Sie können die Eigenschaften von Bereitstellungsfreigaben des MDT mithilfe des Cmdlets [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) und dem Windows PowerShell-Anbieter „MDTProvider“ anzeigen. Dieselben Eigenschaften können auch in der Deployment Workbench angezeigt werden.  

 **So zeigen Sie Eigenschaften einer Bereitstellungsfreigabe mithilfe der Windows PowerShell-Cmdlets des MDT an**  

1.  Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

2.  Stellen Sie sicher, dass die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, mithilfe des Cmdlets **Restore-MDTPersistentDrive** wie im folgenden Beispiel gezeigt wiederhergestellt werden:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Wenn die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, bereits wiederhergestellt wurden, wird eine Warnmeldung angezeigt, dass das Cmdlet das Laufwerk nicht wiederherstellen kann.  

3.  Überprüfen Sie, ob MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, ordnungsgemäß wiederhergestellt werden. Verwenden Sie hierzu das Cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) wie im Folgenden gezeigt:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Die Liste der Windows PowerShell-Laufwerke, die mithilfe von MDTProvider bereitgestellt werden, wird angezeigt.  

4.  Zeigen Sie die Eigenschaften der Bereitstellungsfreigabe mithilfe des Cmdlets [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) an, wie im folgenden Beispiel gezeigt wird:  

    ```  
    Get-ItemProperty "DS002:"  
    ```  

     In diesem Beispiel lautet der Name eines Windows PowerShell-Laufwerks, das in Schritt 3 zurückgegeben wurde, *DS002:*. Das Cmdlet gibt die Eigenschaften der Bereitstellungsfreigabe zurück.  

###  <a name="ViewListDeployShare"></a> Anzeigen der Liste von Bereitstellungsfreigaben mithilfe von Windows PowerShell  
 Sie können die Liste der Bereitstellungsfreigaben des MDT mithilfe des Cmdlets [Get-PSDrive](http://technet.microsoft.com/library/hh849796) und dem Windows PowerShell-Anbieter „MDTProvider“ anzeigen. Die gleiche Liste von Bereitstellungsfreigaben kann auch in der Deployment Workbench angezeigt werden.  

 **So zeigen Sie eine Liste von Bereitstellungsfreigaben mithilfe der Windows PowerShell-Cmdlets des MDT an**  

1.  Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

2.  Stellen Sie sicher, dass die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, mithilfe des Cmdlets **Restore-MDTPersistentDrive** wie im folgenden Beispiel gezeigt wiederhergestellt werden:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Wenn die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, bereits wiederhergestellt wurden, wird eine Warnmeldung angezeigt, dass das Cmdlet das Laufwerk nicht wiederherstellen kann.  

3.  Zeigen Sie für jede Bereitstellungsfreigabe eine Liste der MDT-Bereitstellungen an, die Windows PowerShell-Laufwerke freigeben. Verwenden Sie hierzu das Cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) wie im Folgenden gezeigt:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Die Liste mit bereitgestellten Windows PowerShell-Laufwerken, die „MDTProvider“ verwenden, wird für jede Bereitstellungsfreigabe einzeln angezeigt.  

###  <a name="UpdateDeployShare"></a> Aktualisieren einer Bereitstellungsfreigabe mithilfe von Windows PowerShell  
 Sie können die Bereitstellungsfreigaben des MDT mithilfe des Cmdlets **Update-MDTDeploymentShare** und dem Windows PowerShell-Anbieter „MDTProvider“ aktualisieren. Das Aktualisieren einer Bereitstellungsfreigabe erstellt die Windows PE-Startimages (WIM- und ISO-Dateien), die für das Starten der LTI-Bereitstellung erforderlich sind. Mithilfe der Deployment Workbench können Sie denselben Prozess ausführen, der unter „Update a Deployment Share in the Deployment Workbench (Aktualisieren einer Bereitstellungsfreigabe in der Deployment Workbench)“ beschrieben wird.  

 **So aktualisieren Sie eine Bereitstellungsfreigabe mithilfe von Windows PowerShell**  

1.  Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

2.  Stellen Sie sicher, dass die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, mithilfe des Cmdlets **Restore-MDTPersistentDrive** wie im folgenden Beispiel gezeigt wiederhergestellt werden:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Wenn die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, bereits wiederhergestellt wurden, wird eine Warnmeldung angezeigt, dass das Cmdlet das Laufwerk nicht wiederherstellen kann.  

3.  Überprüfen Sie, ob MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, ordnungsgemäß wiederhergestellt werden. Verwenden Sie hierzu das Cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) wie im Folgenden gezeigt:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Die Liste der Windows PowerShell-Laufwerke, die mithilfe von MDTProvider bereitgestellt werden, wird angezeigt.  

4.  Aktualisieren Sie die Bereitstellungsfreigabe mithilfe des Cmdlets **Update-MDTDeploymentShare**, wie im folgenden Beispiel gezeigt wird:  

    ```  
    Update-MDTDeploymentShare -Path "DS002:" -Force  
    ```  

     In diesem Beispiel lautet der Name eines Windows PowerShell-Laufwerks, das in Schritt 3 zurückgegeben wurde, *DS002:*.  

    > [!NOTE]
    >  Das Aktualisieren der Bereitstellungsfreigabe kann einige Zeit in Anspruch nehmen. Der Fortschritt des Cmdlets wird am oberen Rand der Windows PowerShell-Konsole angezeigt.  

     Das Cmdlet gibt keine Ausgabe zurück, wenn das Update erfolgreich ausgeführt wurde.  

###  <a name="UpdateLinkedDeployShare"></a> Aktualisieren einer verknüpften Bereitstellungsfreigabe mithilfe von Windows PowerShell  
 Sie können verknüpfte Bereitstellungsfreigaben des MDT mithilfe des Cmdlets **Update-MDTLinkedDS** und dem Windows PowerShell-Anbieter „MDTProvider“ aktualisieren (bzw. replizieren). Das Aktualisieren einer verknüpften Bereitstellungsfreigabe repliziert den Inhalt aus der ursprünglichen Bereitstellungsfreigabe in die verknüpfte Bereitstellungsfreigabe. Mithilfe der Deployment Workbench können Sie denselben Prozess ausführen, der unter „Replicate Linked Deployment Shares in the Deployment Workbench (Replizieren von verknüpften Bereitstellungsfreigaben in der Deployment Workbench)“ beschrieben wird.  

 **So aktualisieren Sie eine verknüpfte Bereitstellungsfreigabe mithilfe von Windows PowerShell**  

1.  Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

2.  Stellen Sie sicher, dass die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, mithilfe des Cmdlets **Restore-MDTPersistentDrive** wie im folgenden Beispiel gezeigt wiederhergestellt werden:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Wenn die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, bereits wiederhergestellt wurden, wird eine Warnmeldung angezeigt, dass das Cmdlet das Laufwerk nicht wiederherstellen kann.  

3.  Überprüfen Sie, ob MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, ordnungsgemäß wiederhergestellt werden. Verwenden Sie hierzu das Cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) wie im Folgenden gezeigt:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Die Liste der Windows PowerShell-Laufwerke, die mithilfe von MDTProvider bereitgestellt werden, wird angezeigt.  

4.  Aktualisieren Sie die Bereitstellungsfreigabe mithilfe des Cmdlets **Update-MDTDeploymentShare**, wie im folgenden Beispiel gezeigt wird:  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     In diesem Beispiel lautet der Name eines Windows PowerShell-Laufwerks, das in Schritt 3 zurückgegeben wurde, *DS002:*.  

    > [!NOTE]
    >  Das Aktualisieren der verknüpften Bereitstellungsfreigabe kann einige Zeit in Anspruch nehmen. Der Fortschritt des Cmdlets wird am oberen Rand der Windows PowerShell-Konsole angezeigt.  

     Das Cmdlet gibt keine Ausgabe zurück, wenn das Update erfolgreich ausgeführt wurde.  

###  <a name="UpdateDeployMedia"></a> Aktualisieren von Bereitstellungsmedien mithilfe von Windows PowerShell  
 Sie können die Bereitstellungsmedien des MDT mithilfe des Cmdlets **Update-MDTMedia** und dem Windows PowerShell-Anbieter „MDTProvider“ aktualisieren (bzw. generieren). Das Aktualisieren von Bereitstellungsmedien repliziert den Inhalt aus der ursprünglichen Bereitstellungsfreigabe in die verknüpfte Bereitstellungsfreigabe und generiert dann ISO- und WIM-Dateien. Mithilfe der Deployment Workbench können Sie denselben Prozess ausführen, der unter „Generate Media Images in the Deployment Workbench (Generieren von Medienimages in der Deployment Workbench)“ beschrieben wird.  

 Nachdem das Cmdlet **Update-MDTMedia** ausgeführt wurde, werden folgende Dateien erstellt:  

-   Eine ISO-Datei im Ordner *media_folder* (*media_folder* entspricht dem von Ihnen angegeben Ordner für die Medien).  

     Das Generieren der ISO-Datei ist eine Option, die Sie wie folgt konfigurieren können:  

    -   Klicken Sie auf das Kontrollkästchen **Generate a Lite Touch bootable ISO image** (Mit Lite Touch startbares ISO-Image generieren) in der Registerkarte **Allgemein** des Dialogfelds **Medieneigenschaften** (Deaktivieren Sie dieses Kontrollkästchen, um die erforderliche Zeit für das Generieren der Medien zu verringern, sofern Sie keine startbaren DVDs erstellen oder virtuelle Computer (VMs) starten müssen).  

    -   Festlegen der gleichen Eigenschaft mithilfe des Cmdlets [Set-ItemProperty](http://technet.microsoft.com/library/hh849844)  

-   WIM-Dateien im Ordner *media_folder*\Content\Deploy\Boot (*media_folder* entspricht dem von Ihnen angegeben Ordner für die Medien).  

 **So aktualisieren Sie eine verknüpfte Bereitstellungsfreigabe mithilfe von Windows PowerShell**  

1.  Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

2.  Stellen Sie sicher, dass die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, mithilfe des Cmdlets **Restore-MDTPersistentDrive** wie im folgenden Beispiel gezeigt wiederhergestellt werden:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Wenn die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, bereits wiederhergestellt wurden, wird eine Warnmeldung angezeigt, dass das Cmdlet das Laufwerk nicht wiederherstellen kann.  

3.  Überprüfen Sie, ob MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, ordnungsgemäß wiederhergestellt werden. Verwenden Sie hierzu das Cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) wie im Folgenden gezeigt:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Die Liste der Windows PowerShell-Laufwerke, die mithilfe von MDTProvider bereitgestellt werden, wird angezeigt.  

4.  Aktualisieren Sie die Bereitstellungsfreigabe mithilfe des Cmdlets **Update-MDTDeploymentShare**, wie im folgenden Beispiel gezeigt wird:  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     In diesem Beispiel lautet der Name eines Windows PowerShell-Laufwerks, das in Schritt 3 zurückgegeben wurde, *DS002:*.  

    > [!NOTE]
    >  Das Aktualisieren der verknüpften Bereitstellungsfreigabe kann einige Zeit in Anspruch nehmen. Der Fortschritt des Cmdlets wird am oberen Rand der Windows PowerShell-Konsole angezeigt.  

     Das Cmdlet gibt keine Ausgabe zurück, wenn das Update erfolgreich ausgeführt wurde.  

###  <a name="ManageItemDeployShare"></a> Verwalten von Elementen in einer Bereitstellungsfreigabe mithilfe von Windows PowerShell  
 Eine Bereitstellungsfreigabe enthält Elemente, die zum Ausführen von Bereitstellungen verwendet werden, z.B. Betriebssysteme, Anwendungen, Gerätetreiber, Betriebssystempakete und Tasksequenzen. Diese Elemente können mithilfe von Windows PowerShell-Cmdlets und mit dem MDT bereitgestellten Cmdlets verwaltet werden.  

 Weitere Informationen zum direkten Verarbeiten von Elementen mithilfe von Windows PowerShell-Cmdlets finden Sie unter [Direktes Verarbeiten von Elementen](http://technet.microsoft.com/library/dd315266.aspx). Die Ordnerstruktur für eine Bereitstellungsfreigabe kann auch mithilfe von Windows PowerShell verwaltet werden. Weitere Informationen finden Sie unter [Managing Deployment Share Folders Using Windows PowerShell (Verwalten von Bereitstellungsfreigabeordnern mithilfe von Windows PowerShell)](#ManageDeployShareFolder).  

####  <a name="ImportItemDeployShare"></a> Importieren eines Elements in eine Bereitstellungsfreigabe  
 Sie können jeden Typ von Element mithilfe von MDT-Cmdlets importieren, z.B. Betriebssysteme, Anwendungen oder Gerätetreiber. Für jeden Elementtyp gibt es ein spezifisches MDT-Cmdlet. Wenn Sie mehrere Elemente mithilfe von Windows PowerShell in eine Bereitstellungsfreigabe importieren möchten, finden Sie Informationen dazu unter [Automating Population of a Deployment Share (Automatisieren der Auffüllung einer Bereitstellungsfreigabe)](#AutomatePopulateDeployShare).  

 In der folgenden Tabelle werden die Windows PowerShell-Cmdlets des MDT aufgelistet, die zum Importieren von Elementen in eine Bereitstellungsfreigabe verwendet werden, und eine kurze Beschreibung von jedem Cmdlet zur Verfügung gestellt. Beispiele zur Verwendung eines jeden Cmdlets finden Sie in den entsprechenden Abschnitten.  

 |**Cmdlet** | **Beschreibung** |  
 |-|-|  
 |**Import-MDTApplication** |Importiert eine Anwendung in eine Bereitstellungsfreigabe|  
 |**Import-MDTDriver** |Importiert mindestens einen Gerätetreiber in eine Bereitstellungsfreigabe|  
 |**Import-MDTOperatingSystem** |Importiert mindestens ein Betriebssystem in eine Bereitstellungsfreigabe|  
 |**Import-MDTPackage** |Importiert mindestens ein Betriebssystempaket in eine Bereitstellungsfreigabe|  
 |**Import-MDTTaskSequence** |Importiert eine Tasksequenz in eine Bereitstellungsfreigabe|  

####  <a name="ViewPropertyDeployShare"></a> Anzeigen der Eigenschaften eines Elements in eine Bereitstellungsfreigabe  
 Jedes Element in einer Bereitstellungsfreigabe verfügt über andere Eigenschaften. Sie können die Eigenschaften eines Elements in einer Bereitstellungsfreigabe mithilfe des Cmdlets [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) anzeigen. Das Cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) verwendet MDTProvider zum Anzeigen der Eigenschaften eines bestimmten Elements, genau wie Sie die Eigenschaften in der Deployment Workbench anzeigen können.  

 Wenn Sie die Eigenschaften von mehreren Elementen in einer Bereitstellungsfreigabe mithilfe von Windows PowerShell anzeigen möchten, finden Sie Informationen dazu unter [Automating Population of a Deployment Share (Automatisieren der Auffüllung einer Bereitstellungsfreigabe)](#AutomatePopulateDeployShare).  

 **So zeigen Sie die Eigenschaften eines Elements in einer Bereitstellungsfreigabe mithilfe von Windows PowerShell an**  

1.  Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

2.  Stellen Sie sicher, dass die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, mithilfe des Cmdlets **Restore-MDTPersistentDrive** wie im folgenden Beispiel gezeigt wiederhergestellt werden:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Wenn die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, bereits wiederhergestellt wurden, wird eine Warnmeldung angezeigt, dass das Cmdlet das Laufwerk nicht wiederherstellen kann.  

3.  Überprüfen Sie, ob MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, ordnungsgemäß wiederhergestellt werden. Verwenden Sie hierzu das Cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) wie im folgenden Beispiel gezeigt:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Die Liste der Windows PowerShell-Laufwerke, die mithilfe von MDTProvider bereitgestellt werden, wird angezeigt.  

4.  Geben Sie eine Liste der Elemente für den Elementtyp zurück, dessen Eigenschaften Sie mithilfe des Cmdlets [Get-Item](http://technet.microsoft.com/library/hh849788) anzeigen möchten, wie im folgenden Beispiel gezeigt wird:  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     Im vorherigen Beispiel wird eine Liste aller Betriebssysteme in der Bereitstellungsfreigabe angezeigt. Die Ausgabe wird an das Cmdlet **Format-List** weitergeleitet, sodass die langen Namen der Betriebssysteme angezeigt werden können. Weitere Informationen zur Verwendung des Cmdlets **Format-List** finden Sie unter [Verwenden des Cmdlet „Format-List“](http://technet.microsoft.com/library/ee176830.aspx). Das gleiche Verfahren kann verwendet werden, um die Liste anderer Elementtypen zurückzugeben, z.B. Gerätetreiber oder Anwendungen.  

    > [!TIP]
    >  Sie können anstelle des Cmdlets [Get-Item](http://technet.microsoft.com/library/hh849788) auch den Befehl **Dir** verwenden, um die Liste der Betriebssysteme anzuzeigen.  

5.  Zeigen Sie die Eigenschaften von einem der im vorherigen Schritt aufgelisteten Elemente mithilfe des Cmdlets [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) an, wie im folgenden Beispiel gezeigt wird:  

    ```  
    Get-ItemProperty -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     In diesem Beispiel entspricht der Wert des Parameters *Path* dem vollqualifizierten Windows PowerShell-Pfad zum Element, einschließlich des Dateinamens, der im vorherigen Schritt zurückgegeben wurde. Sie können das gleiche Verfahren verwenden, um die Eigenschaften anderer Elementtypen anzuzeigen, z.B. Gerätetreiber oder Anwendungen.  

####  <a name="RemoveItemDeployShare"></a> Entfernen eines Elements aus einer Bereitstellungsfreigabe  
 Sie können ein Element mithilfe des Cmdlets [Remove-Item](http://technet.microsoft.com/library/hh849765) aus einer Bereitstellungsfreigabe entfernen. Das Cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765) entfernt mit MDTProvider ein bestimmtes Element, so wie Sie ein Element aus der Deployment Workbench entfernen können. Wenn Sie mehrere Elemente aus einer Bereitstellungsfreigabe mithilfe von Windows PowerShell entfernen möchten, finden Sie Informationen dazu unter [Automating Population of a Deployment Share (Automatisieren der Auffüllung einer Bereitstellungsfreigabe)](#AutomatePopulateDeployShare).  

> [!NOTE]
>  Wenn ein Element entfernt wird, das von einer Tasksequenz verwendet wird, schlägt die Tasksequenz fehl. Stellen Sie sicher, dass ein Element nicht von anderen Elementen in der Bereitstellungsfreigabe referenziert wird, bevor Sie das Element entfernen. Wenn ein Element entfernt wird, kann es nicht wiederhergestellt werden.  

 **So entfernen Sie ein Element aus einer Bereitstellungsfreigabe mithilfe von Windows PowerShell**  

1.  Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

2.  Stellen Sie sicher, dass die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, mithilfe des Cmdlets **Restore-MDTPersistentDrive** wie im folgenden Beispiel gezeigt wiederhergestellt werden:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Wenn die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, bereits wiederhergestellt wurden, wird eine Warnmeldung angezeigt, dass das Cmdlet das Laufwerk nicht wiederherstellen kann.  

3.  Überprüfen Sie, ob MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, ordnungsgemäß wiederhergestellt werden. Verwenden Sie hierzu das Cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) wie im folgenden Beispiel gezeigt:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Die Liste der Windows PowerShell-Laufwerke, die mithilfe von MDTProvider bereitgestellt werden, wird angezeigt.  

4.  Geben Sie eine Liste der Elemente für den Elementtyp zurück, dessen Eigenschaften Sie mithilfe des Cmdlets [Get-Item](http://technet.microsoft.com/library/hh849788) anzeigen möchten, wie im folgenden Beispiel gezeigt wird:  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     Im vorherigen Beispiel wird eine Liste aller Betriebssysteme in der Bereitstellungsfreigabe angezeigt. Die Ausgabe wird an das Cmdlet **Format-List** weitergeleitet, sodass die langen Namen der Betriebssysteme angezeigt werden können. Weitere Informationen zur Verwendung des Cmdlets **Format-List** finden Sie unter [Verwenden des Cmdlet „Format-List“](http://technet.microsoft.com/library/ee176830.aspx). Sie können das gleiche Verfahren verwenden, um die Liste anderer Elementtypen zurückzugeben, z.B. Gerätetreiber oder Anwendungen.  

    > [!TIP]
    >  Sie können anstelle des Cmdlets [Get-Item](http://technet.microsoft.com/library/hh849788) auch den Befehl **Dir** verwenden, um die Liste der Betriebssysteme anzuzeigen.  

5.  Entfernen Sie eines der im vorherigen Schritt aufgelisteten Elemente mithilfe des Cmdlets [Remove-Item](http://technet.microsoft.com/library/hh849765), wie im folgenden Beispiel gezeigt wird:  

    ```  
    Remove-Item -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     In diesem Beispiel entspricht der Wert des Parameters *Path* dem vollqualifizierten Windows PowerShell-Pfad zum Element, einschließlich des Dateinamens, der im vorherigen Schritt zurückgegeben wurde.  

     Sie können das gleiche Verfahren verwenden, um andere Elementtypen zu entfernen, z.B. Gerätetreiber oder Anwendungen.  

    > [!NOTE]
    >  Wenn ein Element entfernt wird, das von einer Tasksequenz verwendet wird, schlägt die Tasksequenz fehl. Stellen Sie sicher, dass ein Element nicht von anderen Elementen in der Bereitstellungsfreigabe referenziert wird, bevor Sie das Element entfernen.  

###  <a name="AutomatePopulateDeployShare"></a> Automatisieren der Auffüllung einer Bereitstellungsfreigabe  
 Die Windows PowerShell-Cmdlets des MDT ermöglichen das Verwalten von einzelnen Elementen. Allerdings können die Cmdlets mithilfe einiger Features für die Skripterstellung von Windows PowerShell verwendet werden, um die Auffüllung einer Bereitstellungsfreigabe zu automatisieren.  

 Eine Organisation muss möglicherweise mehrere Bereitstellungsfreigaben für verschiedene Geschäftseinheiten bereitstellen, oder eine Organisation stellt anderen Organisationen Bereitstellungsdienste für Betriebssysteme bereit. In beiden dieser Beispiele benötigen die Organisationen die Möglichkeit, konsistent konfigurierte Bereitstellungsfreigaben zu erstellen und aufzufüllen.  

 Eine Methode für die Verwaltung mehrerer Elemente ist eine CSV-Datei (durch Trennzeichen getrennte Werte), die eine Liste aller Elemente enthält, die Sie mit dem Cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) in einer Bereitstellungsfreigabe verwalten möchten.  

 Im Folgenden finden Sie einen Auszug aus einem Windows PowerShell-Skript zum Importieren einer Liste von Anwendungen basierend auf Informationen in einer CSV-Datei, das die Cmdlets [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), [ForEach-Object](http://technet.microsoft.com/library/hh849731) und **Import-MDTApplication** verwendet:  

```  
$List=Import-CSV "C:\MDT\Import-MDT-Apps.csv"  
ForEach-Object ($App in $List) {  
Import-MDTApplication –path $App.ApplicationFolder -enable "True" –Name $App.DescriptiveName –ShortName $App.Shortname –Version $App.Version –Publisher $App.Publisher –Language $App.Language –CommandLine $App.CommandLine –WorkingDirectory $App.WorkingDirectory –ApplicationSourcePath $App.SourceFolder –DestinationFolder $App.DestinationFolder –Verbose  
}  
```  

 In diesem Beispiel enthält die Datei unter C:\MDT\Import-MDT-Apps.csv ein Feld für jede zum Importieren einer Anwendung erforderliche Variable. Weitere Informationen zum Erstellen einer CSV-Datei zur Verwendung mit dem Cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) finden Sie unter [Verwenden des Cmdlets „Import-Csv“](http://technet.microsoft.com/library/ee176874.aspx).  

 Sie können die gleiche Methode zum Importieren von Betriebssystemen, Gerätetreibern und anderen Elementen in einer Bereitstellungsfreigabe verwenden, indem Sie die folgenden Schritte ausführen:  

1.  Erstellen Sie eine CSV-Datei für jeden Elementtyp einer Bereitstellungsfreigabe, die aufgefüllt werden soll.  

2.  Weitere Informationen zum Erstellen einer CSV-Datei zur Verwendung mit dem Cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) finden Sie unter [Verwenden des Cmdlets „Import-Csv“](http://technet.microsoft.com/library/ee176874.aspx).  

3.  Erstellen Sie eine Windows PowerShell-Skriptdatei, die zum Automatisieren der Auffüllung der Bereitstellungsfreigabe verwendet wird.  

     Weitere Informationen zum Erstellen eines Windows PowerShell-Skripts finden Sie unter [Skripterstellung mit Windows PowerShell](http://technet.microsoft.com/scriptcenter/powershell.aspx).  

4.  Erstellen Sie alle erforderlichen Ordnerstrukturen, die vor dem Importieren der Elemente der Bereitstellungsfreigabe in der Bereitstellungsfreigabe enthalten sein müssen.  

     Weitere Informationen finden Sie unter [Managing Deployment Share Folders Using Windows PowerShell (Verwalten von Bereitstellungsfreigabeordnern mithilfe von Windows PowerShell)](#ManageDeployShareFolder).  

5.  Fügen Sie einer der in Schritt 1 erstellten CSV-Dateien die Zeile für das Cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) hinzu.  

     Weitere Informationen zum Cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) finden Sie unter [Verwenden des Cmdlets „Import-CSV“](http://technet.microsoft.com/library/ee176874.aspx).  

6.  Erstellen Sie eine [ForEach-Object](http://technet.microsoft.com/library/hh849731)-Cmdlet-Schleife, die jedes Element der CSV-Datei verarbeitet, die im Cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) vom vorherigen Schritt referenziert werden.  

     Weitere Informationen zum Cmdlet [ForEach-Object](http://technet.microsoft.com/library/hh849731) finden Sie unter [Verwenden des Cmdlets „ForEach-Object“](http://technet.microsoft.com/library/ee176828).  

7.  Fügen Sie das entsprechende MDT-Cmdlet zum Importieren der Elemente der Bereitstellungsfreigabe in der Cmdlet-Schleife [ForEach-Object](http://technet.microsoft.com/library/hh849731) hinzu, die Sie im vorherigen Schritt erstellt haben.  

     Weitere Informationen zu den MDT-Cmdlets für das Importieren von Elementen in eine Bereitstellungsfreigabe finden Sie unter [Import an Item into a Deployment Share (Importieren eines Elements in eine Bereitstellungsfreigabe)](#ImportItemDeployShare).  

###  <a name="ManageDeployShareFolder"></a> Verwalten von Bereitstellungsfreigabeordnern mithilfe von Windows PowerShell  
 Sie können Ordner in einer Bereitstellungsfreigabe mithilfe von Befehlszeilentools verwalten, z.B. der Befehl **mkdir**, oder indem Sie Windows PowerShell-Cmdlets und den Windows PowerShell-Anbieter „MDTProvider“ verwenden, z.B. das Cmdlet [New-Item](http://technet.microsoft.com/library/hh849795). Dieselbe Ordnerstruktur für Bereitstellungsfreigaben kann auch in der Deployment Workbench angezeigt und verwaltet werden. Weitere Informationen zum direkten Verarbeiten von Elementen mithilfe von Windows PowerShell-Cmdlets finden Sie unter [Direktes Verarbeiten von Elementen](http://technet.microsoft.com/library/dd315266.aspx).  

#### <a name="create-a-folder-in-a-deployment-share-using-windows-powershell"></a>Erstellen eines Ordners in einer Bereitstellungsfreigabe mithilfe von Windows PowerShell  
 **So erstellen Sie einen Ordner in einer Bereitstellungsfreigabe mithilfe von Windows PowerShell**  

1.  Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

2.  Stellen Sie sicher, dass die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, mithilfe des Cmdlets **Restore-MDTPersistentDrive** wie im folgenden Beispiel gezeigt wiederhergestellt werden:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Wenn die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, bereits wiederhergestellt wurden, wird eine Warnmeldung angezeigt, dass das Cmdlet das Laufwerk nicht wiederherstellen kann.  

3.  Zeigen Sie für jede Bereitstellungsfreigabe eine Liste der MDT-Bereitstellungen an, die Windows PowerShell-Laufwerke freigeben. Verwenden Sie hierzu das Cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) wie im Folgenden gezeigt:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Die Liste mit bereitgestellten Windows PowerShell-Laufwerken, die den MDTProvider verwenden, wird für jede Bereitstellungsfreigabe einzeln angezeigt.  

4.  Erstellen Sie in einer Bereitstellungsfreigabe im Ordner „Betriebssysteme“ einen Ordner namens *Windows_8*. Verwenden Sie hierzu wie im folgenden Beispiel gezeigt den Befehl **mkdir**:  

    ```  
    mkdir "DS002:\Operating Systems\Windows_8"  
    ```  

     In diesem Beispiel lautet der Name eines Windows PowerShell-Laufwerks, das in Schritt 3 zurückgegeben wurde, *DS002:*.  

5.  Stellen Sie sicher, dass der Ordner ordnungsgemäß erstellt wird, indem Sie den folgenden Befehl eingeben:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Der Ordner „Windows_8“ und alle anderen im Ordner „Betriebssysteme“ vorhandenen Ordner werden angezeigt.  

6.  Erstellen Sie im Ordner „Betriebssysteme“ einen Ordner mit dem Namen *Windows_7* in einer Bereitstellungsfreigabe. Verwenden Sie hierzu das Cmdlet [New-Item](http://technet.microsoft.com/library/hh849795) wie im folgenden Beispiel oder unter [Verwenden des Cmdlets „New-Item“](http://technet.microsoft.com/library/ee176914.aspx) dargestellt:  

    ```  
    New-Item "DS002:\Operating Systems\Windows_7" -Type directory  
    ```  

     Das Cmdlet zeigt an, dass der Ordner erfolgreich erstellt wurde.  

7.  Stellen Sie sicher, dass der Ordner ordnungsgemäß erstellt wird, indem Sie den folgenden Befehl eingeben:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Der Ordner „Windows_7“ und alle anderen im Ordner „Betriebssysteme“ vorhandenen Ordner werden angezeigt.  

#### <a name="delete-a-folder-in-a-deployment-share-using-windows-powershell"></a>Löschen eines Ordners in einer Bereitstellungsfreigabe mithilfe von Windows PowerShell  
 **So löschen Sie einen Ordner in einer Bereitstellungsfreigabe mithilfe von Windows PowerShell:**  

1.  Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

2.  Stellen Sie sicher, dass die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, mithilfe des Cmdlets **Restore-MDTPersistentDrive** wie im folgenden Beispiel gezeigt wiederhergestellt werden:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Wenn die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, bereits wiederhergestellt wurden, wird eine Warnmeldung angezeigt, dass das Cmdlet das Laufwerk nicht wiederherstellen kann.  

3.  Zeigen Sie für jede Bereitstellungsfreigabe eine Liste der MDT-Bereitstellungen an, die Windows PowerShell-Laufwerke freigeben. Verwenden Sie hierzu das Cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) wie im Folgenden gezeigt:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Die Liste mit bereitgestellten Windows PowerShell-Laufwerken, die „MDTProvider“ verwenden, wird für jede Bereitstellungsfreigabe einzeln angezeigt.  

4.  Löschen (entfernen) Sie im Ordner „Betriebssysteme“ in einer Bereitstellungsfreigabe den Ordner mit dem Namen *Windows_8*. Verwenden Sie hierzu wie im folgenden Beispiel gezeigt den Befehl **mkdir**:  

    ```  
    rmdir "DS002:\Operating Systems\Windows_8"  
    ```  

     In diesem Beispiel lautet der Name eines Windows PowerShell-Laufwerks, das in Schritt 3 zurückgegeben wurde, *DS002:*.  

5.  Stellen Sie sicher, dass der Ordner ordnungsgemäß entfernt wird, indem Sie den folgenden Befehl eingeben:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Der Ordner „Windows_8“ wird nicht mehr in der Ordnerliste im Ordner „Betriebssysteme“ angezeigt.  

6.  Löschen (entfernen) Sie im Ordner „Betriebssysteme“ in einer Bereitstellungsfreigabe den Ordner mit dem Namen *Windows_7*. Verwenden Sie hierzu wie im folgenden Beispiel gezeigt das Cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765):  

    ```  
    Remove-Item "DS002:\Operating Systems\Windows_7"  
    ```  

     Das Cmdlet zeigt an, dass der Ordner erfolgreich entfernt wurde.  

7.  Stellen Sie sicher, dass der Ordner ordnungsgemäß erstellt wird, indem Sie den folgenden Befehl eingeben:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Der Ordner „Windows_7“ wird nicht mehr in der Ordnerliste im Ordner „Betriebssysteme“ angezeigt.  

#### <a name="rename-a-folder-in-a-deployment-share-using-windows-powershell"></a>Umbenennen eines Ordners in einer Bereitstellungsfreigabe mithilfe von Windows PowerShell  
 **So benennen Sie einen Ordner in einer Bereitstellungsfreigabe mithilfe von Windows PowerShell um:**  

1.  Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

2.  Stellen Sie sicher, dass die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, mithilfe des Cmdlets **Restore-MDTPersistentDrive** wie im folgenden Beispiel gezeigt wiederhergestellt werden:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Wenn die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, bereits wiederhergestellt wurden, wird eine Warnmeldung angezeigt, dass das Cmdlet das Laufwerk nicht wiederherstellen kann.  

3.  Zeigen Sie für jede Bereitstellungsfreigabe eine Liste der MDT-Bereitstellungen an, die Windows PowerShell-Laufwerke freigeben. Verwenden Sie hierzu das Cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) wie im Folgenden gezeigt:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Die Liste mit bereitgestellten Windows PowerShell-Laufwerken, die „MDTProvider“ verwenden, wird für jede Bereitstellungsfreigabe einzeln angezeigt.  

4.  Benennen Sie im Ordner „Betriebssysteme“ in einer Bereitstellungsfreigabe den Ordner mit dem Namen *Windows_8* in *Win_8* um. Verwenden Sie hierzu wie im folgenden Beispiel gezeigt den Befehl **ren**:  

    ```  
    ren "DS002:\Operating Systems\Windows_8" "Win_8"  
    ```  

     In diesem Beispiel lautet der Name eines Windows PowerShell-Laufwerks, das in Schritt 3 zurückgegeben wurde, *DS002:*.  

5.  Stellen Sie sicher, dass der Ordner ordnungsgemäß entfernt wird, indem Sie den folgenden Befehl eingeben:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Der Ordner „Windows_8“ wird umbenannt in *Win_8*.  

6.  Benennen Sie im Ordner „Betriebssysteme“ in einer Bereitstellungsfreigabe den Ordner mit dem Namen *Windows_7* in *Win_7* um. Verwenden Sie hierzu wie im folgenden Beispiel gezeigt das Cmdlet [Rename-Item](http://technet.microsoft.com/library/hh849763):  

    ```  
    Rename-Item "DS002:\Operating Systems\Windows_7" "Win_7"  
    ```  

     Das Cmdlet zeigt an, dass der Ordner erfolgreich umbenannt wurde.  

7.  Stellen Sie sicher, dass der Ordner ordnungsgemäß erstellt wird, indem Sie den folgenden Befehl eingeben:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Der Ordner „Windows_7“ wird umbenannt in *Win_7*.  

## <a name="automating-the-application-of-operating-system-service-packs-in-deployment-shares"></a>Automatisieren der Anwendung von Betriebssystem-Service Packs in Bereitstellungsfreigaben  
 Betriebssystem-Service Packs sind ein normaler Bestandteil des Lebenszyklus einer Software. Die vorhandenen Betriebssysteme in Bereitstellungsfreigaben müssen mit diesen Service Packs aktualisiert werden. Auf diese Weise wird sichergestellt, dass neu bereitgestellte oder aktualisierte Computer über die neuesten Sicherheitsempfehlungen und Konfigurationseinstellungen verfügen.  

 Dies kann sehr zeitaufwändig sein, wenn eine Organisation über viele Bereitstellungsfreigaben mit mehreren Betriebssystemen in jeder Bereitstellungsfreigabe verfügt und die Betriebssysteme in jeder Bereitstellungsfreigabe manuell mit den Service Packs aktualisiert werden. Die Methoden für die Automatisierung der Anwendung von Betriebssystem-Service Packs in Bereitstellungsfreigaben umfassen:  

-   Das Kopieren von aktualisiertem Quellinhalt, der das Service Pack (z.B. Windows 7 mit dem SP1-Medium) bereits enthält, in den Ordner der Bereitstellungsfreigabe, in der sich das vorhandene Betriebssystem befindet. Dieser Vorgang wird unter [Automating the Application of Operating System Service Packs from Updated Source Media (Automatisieren der Anwendung von Betriebssystem-Service Packs aus aktualisierten Quellmedien)](#AutomateAppFromUSM) beschrieben.  

-   Das Anwenden des Service Packs auf einen Referenzcomputer und das anschließende Erfassen eines aktualisierten Images von einem Referenzcomputer. Dieser Vorgang wird unter [Automating the Application of Operating System Service Packs Using a Reference Computer and Windows PowerShell (Automatisieren der Anwendung von Betriebssystem-Service Packs mithilfe eines Referenzcomputers und Windows PowerShell)](#AutomateAppUsingRef) beschrieben.  

###  <a name="AutomateAppFromUSM"></a> Automatisieren der Anwendung von Betriebssystem-Service Packs aus aktualisierten Quellmedien  
 Sie können den Prozess der Aktualisierung von Betriebssystem-Service Packs, die Windows PowerShell verwenden, automatisieren, wenn Sie über Quellmedien verfügen, die das Service Pack enthalten, wie etwa eine DVD mit bereits integriertem Windows 7 mit SP1.  

 Dazu werden die vorhandenen Betriebssystemdateien ohne Service Pack in der Bereitstellungsfreigabe mit Windows PowerShell durch die Quellmedien des Betriebssystems mit dem Service Pack überschrieben.  

 **So automatisieren Sie die Anwendung von Betriebssystem-Service Packs aus aktualisierten Quellmedien mithilfe von Windows PowerShell:**  

1.  Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

2.  Stellen Sie sicher, dass die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, mithilfe des Cmdlets **Restore-MDTPersistentDrive** wie im folgenden Beispiel gezeigt wiederhergestellt werden:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Wenn die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, bereits wiederhergestellt wurden, wird eine Warnmeldung angezeigt, dass das Cmdlet das Laufwerk nicht wiederherstellen kann.  

3.  Zeigen Sie für jede Bereitstellungsfreigabe eine Liste der MDT-Bereitstellungen an, die Windows PowerShell-Laufwerke freigeben. Verwenden Sie hierzu das Cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) wie im folgenden Beispiel gezeigt:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Die Liste mit bereitgestellten Windows PowerShell-Laufwerken, die „MDTProvider“ verwenden, wird für jede Bereitstellungsfreigabe einzeln angezeigt.  

4.  Entfernen Sie den Ordner für das vorhandene Betriebssystem aus der Bereitstellungsfreigabe. Verwenden Sie hierzu wie im folgenden Beispiel gezeigt die Cmdlets [Get-ChildItem](http://technet.microsoft.com/library/hh849800) und [Remove-Item](http://technet.microsoft.com/library/hh849765):  

    ```  
    Get-ChildItem “DS002:\Operating Systems\Windows 7” –recurse | Remove-Item –recurse –force  
    ```  

     In diesem Beispiel lautet der Name eines Windows PowerShell-Laufwerks, das in Schritt 3 zurückgegeben wurde, *DS002:*.  

5.  Kopieren Sie wie im folgenden Beispiel gezeigt den Inhalt der Quelldateien des Betriebssystems mit integriertem Service Pack mithilfe des Cmdlets [Copy-Item](http://technet.microsoft.com/library/hh849793):  

    ```  
    Copy-Item "E:\*" -Destination "DS002:\Operating Systems\Windows 7"-Recurse -Force  
    ```  

     In diesem Beispiel befinden sich die Quelldateien des Betriebssystems auf Laufwerk E, und der Name des Windows PowerShell-Laufwerks, das in Schritt 3 zurückgegeben wurde, lautet *DS002:*.  

6.  Aktualisieren Sie alle MDT-Bereitstellungsmedien basierend auf der Bereitstellungsfreigabe mithilfe des Cmdlets **Update-MDTMedia**.  

 Weitere Informationen zum Aktualisieren von MDT-Bereitstellungsmedien basierend auf der Bereitstellungsfreigabe mithilfe des Cmdlets **Update-MDTMedia** finden Sie unter [Updating Deployment Media Using Windows PowerShell (Aktualisieren von Bereitstellungsmedien mithilfe von Windows PowerShell)](#UpdateDeployMedia).  

###  <a name="AutomateAppUsingRef"></a> Automatisieren der Anwendung von Betriebssystem-Service Packs mithilfe eines Referenzcomputers und Windows PowerShell  
 Sie können den Prozess des Aktualisierens von Betriebssystem-Service Packs, die Windows PowerShell verwenden, automatisieren, wenn Sie nur über das noch nicht in das Betriebssystem integrierte Service Pack verfügen, wie etwa SP1 für Windows 7, das noch nicht in ein Windows 7-Image integriert ist.  

 Stellen Sie hierzu das Betriebssystem ohne das Service Pack auf einem Referenzcomputer bereit. Wenden Sie nun das Service Pack auf den Referenzcomputer an. Erfassen Sie anschließend ein Betriebssystemimage des Referenzcomputers. Überschreiben Sie zuletzt die Datei „Install.wim“ im Betriebssystem der Bereitstellungsfreigabe mithilfe von Windows PowerShell durch die erfasste WIM-Datei.  

 **So automatisieren Sie die Anwendung von Betriebssystem-Service Packs aus aktualisierten Quellmedien mithilfe von Windows PowerShell:**  

1.  Stellen Sie das Zielbetriebssystem auf einem Referenzcomputer bereit.  

     Weitere Informationen zum Bereitstellen eines Referenzcomputers finden Sie unter den folgenden Ressourcen des MDT-Artikels *Verwenden des Microsoft Deployment Toolkits*:  

    -   „Preparing for LTI Deployment to the Reference Computer (Vorbereitungen für die LTI-Bereitstellung auf dem Referenzcomputer)“  

    -   „Deploying To and Capturing an Image of the Reference Computer in LTI (Bereitstellen auf dem Referenzcomputer und Erfassen eines Images des Referenzcomputers in LTI)“  

2.  Installieren Sie das gewünschte Service Pack auf dem Referenzcomputer.  

     Weitere Informationen zum Installieren des Service Packs finden Sie in der Dokumentation des Service Packs.  

3.  Erfassen Sie ein Image des Referenzcomputers, indem Sie eine Tasksequenz basierend auf der Tasksequenzvorlage **Sysprep and Capture** erstellen und bereitstellen.  

     Weitere Informationen zum Erstellen einer Tasksequenz basierend auf der Tasksequenzvorlage **Sysprep and Capture** finden Sie unter „Create a New Task Sequence in the Deployment Workbench (Erstellen einer neuen Tasksequenz in der Deployment Workbench)“.  

4.  Laden Sie das Windows PowerShell-Snap-In des MDT wie unter [Loading the MDT Windows PowerShell Snap-In (Laden des Windows PowerShell-Snap-Ins des MDT)](#LoadMDTSnapIn) beschrieben.  

5.  Stellen Sie sicher, dass die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, mithilfe des Cmdlets **Restore-MDTPersistentDrive** wie im folgenden Beispiel gezeigt wiederhergestellt werden:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Wenn die MDT-Bereitstellungen, die Windows PowerShell-Laufwerke freigeben, bereits wiederhergestellt wurden, wird eine Warnmeldung angezeigt, dass das Cmdlet das Laufwerk nicht wiederherstellen kann.  

6.  Zeigen Sie für jede Bereitstellungsfreigabe eine Liste der MDT-Bereitstellungen an, die Windows PowerShell-Laufwerke freigeben. Verwenden Sie hierzu das Cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) wie im folgenden Beispiel gezeigt:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Die Liste mit bereitgestellten Windows PowerShell-Laufwerken, die „MDTProvider“ verwenden, wird für jede Bereitstellungsfreigabe einzeln angezeigt.  

7.  Überschreiben Sie wie im folgenden Beispiel gezeigt mithilfe des Cmdlets [Copy-Item](http://technet.microsoft.com/library/hh849793) die Datei „Install.wim“ im Betriebssystem der Bereitstellungsfreigabe durch die in Schritt 3 erfasste WIM-Datei:  

    ```  
    Copy-Item "DS002:\Captures\Win7SP1.wim" -Destination "DS002:\Operating Systems\Windows 7\sources\Install.wim" Force  
    ```  

     In diesem Beispiel entspricht die erfasste Datei des Betriebssystemimages (Win7SP1.wim) im Ordner „Aufnahmen“ in der Freigabe „DS002:“ dem Namen eines Windows PowerShell-Laufwerks, das in Schritt 6 zurückgegeben wurde. Das vorhandene Windows 7-Betriebssystem wird im Ordner *Windows 7* gespeichert.  

8.  Aktualisieren Sie alle MDT-Bereitstellungsmedien basierend auf der Bereitstellungsfreigabe mithilfe des Cmdlets **Update-MDTMedia**.  

     Weitere Informationen zum Aktualisieren von MDT-Bereitstellungsmedien basierend auf der Bereitstellungsfreigabe mithilfe des Cmdlets **Update-MDTMedia** finden Sie unter [Updating Deployment Media Using Windows PowerShell (Aktualisieren von Bereitstellungsmedien mithilfe von Windows PowerShell)](#UpdateDeployMedia).  

## <a name="customizing-deployment-based-on-chassis-type"></a>Anpassen der Bereitstellung basierend auf dem Chassistyp  
 Sie können die Bereitstellung basierend auf dem Chassistyp des Computers anpassen. Die Skripts erstellen lokale Variablen, die in der Datei „CustomSettings.ini“ verarbeitet werden können. Die lokalen Variablen `IsLaptop`, `IsDesktop` und `IsServer` geben an, ob es sich bei dem Computer um einen Laptop, Desktopcomputer oder Server handelt.  

> [!NOTE]
>  In früheren Versionen der Deployment Workbench wurde mit dem `IsServer`-Flag angegeben, dass es sich bei dem vorhandenen Betriebssystem um ein Serverbetriebssystem handelt (z.B. Windows Server 2003 Enterprise Edition). Dieses Flag wurde in `IsServerOS` umbenannt.  

 **So implementieren Sie lokale Variablen in der Datei „CustomSettings.ini“:**  

1.  Fügen Sie im `[Settings]`-Bereich in der `Priority`-Zeile einen benutzerdefinierten Abschnitt hinzu, um die Bereitstellung basierend auf dem Chassistyp anzupassen (`ByChassisType` im folgenden Beispiel, wobei *Chassis* den Computertyp darstellt).  

2.  Erstellen Sie den benutzerdefinierten Abschnitt, der dem in Schritt 1 definierten benutzerdefinierten Abschnitt entspricht (`ByChassisType` im folgenden Beispiel, wobei *Chassis* den Computertyp darstellt).  

3.  Definieren Sie für jeden Chassistyp, der erkannt werden soll, einen Unterabschnitt (`Subsection=Laptop-%IsLaptop%, Subsection=Desktop-%IsDesktop%, Subsection=Server-%IsServer%` im folgenden Beispiel).  

4.  Erstellen Sie für jeden `True`- und `False`-Status aller in Schritt 3 definierten Unterabschnitte einen Unterabschnitt (z.B. `[Laptop-True], [Laptop-False], [Desktop-True], [Desktop-False]` im folgenden Beispiel).  

5.  Fügen Sie unter jedem `True`- und `False`-Unterabschnitt die entsprechenden Einstellungen basierend auf dem Chassistyp hinzu.  

 **Auflistung 1: Beispiel für das Anpassen der Bereitstellung basierend auf dem Chassistyp in der Datei „CustomSettings.ini“**  

```  
[Settings]  

Priority=...,ByLaptopType,ByDesktopType,ByServerType  

[ByLaptopType]  
Subsection=Laptop-%IsLaptop%  

[ByDesktopType]  
Subsection=Desktop-%IsDesktop%  

[ByServerType]  
Subsection=Server-%IsServer%  
.  
.  
.  

[Laptop-True]  
.  
.  
.  

[Laptop-False]  
.  
.  
.  

[Desktop-True]  
.  
.  
.  

[Desktop-False]  
.  
.  
.  

[Server-True]  
.  
.  
.  

[Server-False]  
.  
.  
.  
```  

## <a name="deploying-applications-based-on-earlier-application-versions"></a>Bereitstellen von Anwendungen basierend auf früheren Anwendungsversionen  
 Häufig werden bei der Installation eines Betriebssystems auf einem vorhandenen Computer die gleichen Anwendungen installiert, die bereits zuvor auf dem Computer installiert wurden. Verwenden Sie hierfür MDT-Skripts (insbesondere „ZTIGather.wsf“), um zwei verschiedene Informationsquellen abzurufen:  

-   **Configuration Manager-Softwareinventur-Feature:** Enthält einen Datensatz für jedes Anwendungspaket (in diesem Fall Auflistungen in „Programme und Funktionen“ in Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2), die bei der letzten Inventarisierung des Computers durch Configuration Manager installiert wurden.  

-   **Eine Zuordnungstabelle:** Beschreibt, welches Paket und welches Programm für jeden Datensatz installiert werden müssen (da in den Datensätzen „Programme und Funktionen“ oder „Software“ nicht angegeben wird, mit welchem Paket die Anwendung installiert wurde, wodurch das Paket nicht automatisch nur auf Grundlage der Inventur ausgewählt werden kann).  

 **So führen Sie eine dynamische computerspezifische Anwendungsinstallation aus:**  

1.  Verwenden Sie die Tabelle in der MDT-Datenbank, um bestimmte Pakete mit Anwendungen zu verbinden, die im Zielbetriebssystem aufgeführt werden.  

2.  Füllen Sie die Tabelle mit Daten auf, die das entsprechende Paket der Anwendung zuordnen, die in „Programm und Funktionen“ oder „Software“ aufgeführt ist.

     **SQL-Abfrage zum Auffüllen der Tabelle**  

    ```  
    use [MDTDB]  
    go  
    INSERT INTO [PackageMapping] (ARPName, Packages) VALUES('Office12.0', 'XXX0000F:Install Office 2010 Professional Plus')  
    go  
    ```  

     Die eingefügte Zeile stellt eine Verbindung zwischen einem beliebigen Computer mit dem Eintrag `Office12.0` und dem Paket „Microsoft Office 2010 Professional Plus“ her.  

     Das bedeutet, dass Microsoft Office 2010 Professional Plus auf einem beliebigen Computer installiert wird, auf dem derzeit Microsoft Office 2007 (Office 12.0) ausgeführt wird. Fügen Sie für beliebige andere Pakete ähnliche Einträge hinzu. Elemente, für die kein Eintrag vorhanden ist, werden ignoriert (es wird kein Paket installiert).  

3.  Erstellen Sie eine gespeicherte Prozedur, um die Verknüpfung der Informationen in der neuen Tabelle mit den Inventurdaten zu vereinfachen.  

    ```  
    use [MDTDB]  
    go  

    if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[RetrievePackages]') and OBJECTPROPERTY(id, N'IsProcedure') = 1)  
    drop procedure [dbo].[RetrievePackages]  
    go  

    CREATE PROCEDURE [dbo].[RetrievePackages]  
    @MacAddress CHAR(17)  
    AS  

    SET NOCOUNT ON  

    /* Select and return all the appropriate records based on current inventory */  
    SELECT * FROM PackageMapping  
    WHERE ARPName IN  
    (  
      SELECT ProdID0 FROM CM_DB.dbo.v_GS_ADD_REMOVE_PROGRAMS a, CM_DB.dbo.v_GS_NETWORK_ADAPTER n  
      WHERE a.ResourceID = n.ResourceID AND  
      MACAddress0 = @MacAddress  
    )  
    go  
    ```  

     In der gespeicherten Prozedur im vorhergehenden Beispiel wird davon ausgegangen, dass sich die Configuration Manager-Datenbank für den zentralen primären Standort auf dem Computer befindet, auf dem SQL Server als MDT-Datenbank ausgeführt wird. Befindet sich die Datenbank für den zentralen primären Standort auf einem anderen Computer, muss die gespeicherte Prozedur entsprechend geändert werden. Zudem muss der Name der Datenbank (`CM_DB`) aktualisiert werden. Außerdem sollten Sie in Betracht ziehen, weiteren Konten Lesezugriff auf die Ansicht **V_GS_ADD_REMOVE_PROGRAMS** in der Configuration Manager-Datenbank zu gewähren.  

4.  Konfigurieren Sie die Datei „CustomSettings.ini“ so, dass diese Datenbanktabelle abgefragt wird. Geben Sie hierzu den Namen eines Abschnitts an (`[DynamicPackages]` in der **Prioritäten**-Liste), der auf die Datenbankinformationen verweist.  

    ```  
    [Settings]  
    …  
    Priority=MacAddress, DefaultGateway, DynamicPackages, Default  
    …  
    ```  

5.  Erstellen Sie einen `[DynamicPackages]`-Abschnitt, um den Namen eines Datenbankabschnitts anzugeben.  

    ```  
    [DynamicPackages]  
    SQLDefault=DB_DynamicPackages  
    ```  

6.  Erstellen Sie einen Datenbankabschnitt, um die Datenbankinformationen und Abfragedetails anzugeben.  

    ```  
    [DB_DynamicPackages]  
    SQLServer=SERVER1  
    Database=MDTDB  
    StoredProcedure=RetrievePackages  
    Parameters=MacAddress  
    SQLShare=Logs  
    Instance=SQLEnterprise2005  
    Port=1433  
    Netlib=DBNMPNTW  
    ```  

     Im vorhergehenden Beispiel wird die MDT-Datenbank mit dem Namen *MDTDB* auf dem Computer abgefragt, auf dem die SQL Server-Instanz mit dem Namen *SERVER1* ausgeführt wird. Die Datenbank enthält eine gespeicherte Prozedur mit dem Namen `RetrievePackages` (die in Schritt 3 erstellt wurde).  

 Sobald „ZTIGather.wsf“ ausgeführt wird, wird automatisch eine `SELECT`-SQL-Anweisung (Structured Query Language) generiert, und der Wert des benutzerdefinierten Schlüssels **MakeModelQuery** wird als Parameter an die Abfrage übergeben:  

 ```  
 EXECUTE RetrievePackages ?  
 ```  

 Das entsprechende „?“ wird durch den tatsächlichen Wert des benutzerdefinierten Schlüssels **MACAddress** ersetzt.  Diese Abfrage gibt eine Datensatzgruppe mit den in Schritt 2 eingegebenen Zeilen zurück.  

 Eine variable Anzahl von Argumenten kann nicht an eine gespeicherte Prozedur übergeben werden. Besitzt ein Computer mehr als eine MAC-Adresse, können daher nicht alle MAC-Adressen an die gespeicherte Prozedur übergeben werden. Alternativ dazu können Sie die gespeicherte Prozedur durch eine Ansicht ersetzen, mit der die Ansicht mit einer `SELECT`-Anweisung mit einer `IN`-Klausel abgefragt werden kann, um alle MAC-Adresswerte zu übergeben.  

 Auf Grundlage des hier dargestellten Szenarios wird eine Zeile zurückgegeben (`XXX0000F:Install Office 2010 Professional Plus`), wenn der aktuelle Computer über den Wert `Office12.0` in der Tabelle verfügt (Schritt 2). Dies bedeutet, dass durch den ZTI-Prozess während der Zustandswiederherstellungsphase das Paket „XXX0000F:Install Office 2001 Professional Plus“ installiert wird.  

## <a name="fully-automated-lti-deployment-scenario"></a>Vollständig automatisiertes LTI-Bereitstellungsszenario  
 Der Hauptzweck von LTI besteht darin, den Bereitstellungsprozess so weit wie möglich zu automatisieren. Obwohl ZTI mithilfe von MDT-Skripts und Windows-Bereitstellungsdiensten eine vollständige Automatisierung der Bereitstellung ermöglicht, sind die Anforderungen an die Infrastruktur mit LTI geringer.  

 Sie können den im LTI-Bereitstellungsprozess verwendeten Windows-Bereitstellungs-Assistenten so automatisieren, dass die angezeigten Assistentenseiten verringert (oder entfernt) werden. Sie können den Windows-Bereitstellungs-Assistenten komplett überspringen, indem Sie in „CustomSettings.ini“ die Eigenschaft **SkipWizard** angeben. Verwenden Sie zum Überspringen von einzelnen Assistentenseiten die folgenden Eigenschaften:  

-   **SkipAdminPassword**  

-   **SkipApplications**  

-   **SkipBDDWelcome**  

-   **SkipBitLocker**  

-   **SkipBitLockerDetails**  

-   **SkipTaskSequence**  

-   **SkipCapture**  

-   **SkipComputerBackup**  

-   **SkipComputerName**  

-   **SkipDomainMembership**  

-   **SkipFinalSummary**  

-   **SkipLocaleSelection**  

-   **SkipPackageDisplay**  

-   **SkipProductKey**  

-   **SkipSummary**  

-   **SkipTimeZone**  

-   **SkipUserData**  

Weitere Informationen zu den einzelnen Eigenschaften finden Sie unter der entsprechenden Eigenschaft im MDT-Artikel *Toolkit-Referenz*.  

Geben Sie für jede übersprungene Assistentenseite die Werte für die entsprechenden Eigenschaften an, die in der Regel über die Assistentenseite in den Dateien „CustomSettings.ini“ und „BootStrap.ini“ gesammelt werden. Weitere Informationen zu den Eigenschaften, die in diesen Dateien konfiguriert werden müssen, finden Sie im Abschnitt „Providing Properties for Skipped Deployment Wizard Pages (Bereitstellen von Eigenschaften für übersprungene Seiten des Bereitstellungs-Assistenten)“ im MDT-Artikel *Toolkit-Referenz*.  

## <a name="fully-automated-lti-deployment-for-a-refresh-computer-scenario"></a>Vollständig automatisierte LTI-Bereitstellung für das Szenario „Computer aktualisieren“  
 Die folgende Abbildung zeigt eine „CustomSettings.ini“-Datei, die für das Szenario „Computer aktualisieren“ verwendet wird, um alle Seiten des Windows-Bereitstellungs-Assistenten zu überspringen. In diesem Beispiel stehen die Eigenschaften, die beim Überspringen der Assistentenseite angegeben werden müssen, direkt unterhalb der Eigenschaft, die die Assistentenseite überspringt.  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  
SkipCapture=YES  
SkipAdminPassword=YES  
SkipProductKey=YES  

DeploymentType=REFRESH  

SkipDomainMembership=YES  
JoinDomain=DomainName  
DomainAdmin=Administrator  
DomainAdminDomain=DomainName  
DomainAdminPassword=a_secure_password  

SkipUserData=yes  
UserDataLocation=AUTO  
UDShare=\\Servername\Sharename\Directory  
UDDir=%ComputerName%  

SkipComputerBackup=YES  
ComputerBackuplocation=AUTO  
BackupShare=\\Servername\Backupsharename  
BackupDir=%ComputerName%  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%ComputerName%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  
UserID=Administrator  
UserDomain=DomainName  
UserPassword=P@ssw0rd  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=DomainName\Username  
```  

## <a name="fully-automated-lti-deployment-for-a-new-computer-scenario"></a>Vollständig automatisierte LTI-Bereitstellung für das Szenario „Neuer Computer“  
 Das folgende Beispiel zeigt eine „CustomSettings.ini“-Datei, die für das Szenario „Neuer Computer“ verwendet wird, um alle Seiten des Windows-Bereitstellungs-Assistenten zu überspringen. In diesem Beispiel stehen die Eigenschaften, die beim Überspringen der Assistentenseite angegeben werden müssen, direkt unterhalb der Eigenschaft, die die Assistentenseite überspringt.  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  

SkipCapture=YES  
ComputerBackupLocation=\\WDG-MDT-01\Backup$\  
BackupFile=MyCustomImage.wim  

SkipAdminPassword=YES  
SkipProductKey=YES  

SkipDomainMembership=YES  
JoinDomain=WOODGROVEBANK  
DomainAdmin=Administrator  
DomainAdminDomain=WOODGROVEBANK  
DomainAdminPassword=P@ssw0rd  

SkipUserData=Yes  
UserDataLocation=\\WDG-MDT-01\UserData$\Directory\usmtdata  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%SerialNumber%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=WOODGROVEBANK\PilarA  
CaptureGroups=YES  
SLShare=\\WDG-MDT-01\UserData$\Logs  
Home_page=http://www.microsoft.com/NewComputer  
```  

## <a name="calling-web-services-in-mdt"></a>Aufrufen von Webdiensten in MDT  
 In früheren MDT-Versionen wurde die Verarbeitung von Regeln durch „CustomSettings.ini“ und Datenbanken unterstützt, von denen Werte vom lokalen Computer abgerufen werden konnten (in der Regel mit WMI), um zu entscheiden, welche Aktionen auf jedem Computer während der Bereitstellung ausgeführt werden sollten. Zudem konnten SQL-Abfragen und Aufrufe für gespeicherte Prozeduren ausgeführt werden, um zusätzliche Informationen von externen Datenbanken abzurufen. Doch bei dieser Herangehensweise gab es auch Herausforderungen, insbesondere bei der Herstellung von sicheren SQL-Verbindungen.  

 Zur Lösung dieses Problems besitzt MDT nun die Möglichkeit, Webdienstaufrufe basierend auf einfachen Regeln auszuführen, die in „CustomSettings.ini“ definiert werden. Diese Webdienstanforderungen erfordern keinen besonderen Sicherheitskontext und können jeden beliebigen TCP/IP-Port verwenden, um Firewallkonfigurationen zu vereinfachen.  

 Das folgende Beispiel zeigt die Konfiguration von „CustomSettings.ini“, um einen bestimmten Webdienst aufzurufen. In diesem Szenario wird der Webdienst zufällig über eine Internetsuche ausgewählt. Als Eingabe wird eine Postleitzahl verwendet. Zurückgegeben werden Stadt, Land, Ortskennzahl und Zeitzone (als Buchstabe) für die angegebene Postleitzahl.  

```  
[Settings]  
Priority=Default, USZipService  
Properties=USZip, City, State, Zip, Area_Code, Time_Zones   
[Default]  
USZip=98052   
[USZipService]  
WebService=http://www.webservicex.net/uszip.asmx/GetInfoByZIP  
Parameters=USZip  
```  

 Wenn Sie diesen Code ausführen, wird eine Ausgabe ähnlich der folgenden erzeugt:
```  
Added new custom property USZIP  
Added new custom property CITY  
Added new custom property STATE  
Added new custom property ZIP  
Added new custom property AREA_CODE  
Added new custom property TIME_ZONES  
Using from [Settings]: Rule Priority = DEFAULT, USZIPSERVICE  
------ Processing the [DEFAULT] section ------  
Property USZIP is now = 98052  
Using from [DEFAULT]: USZIP = 98052  
------ Processing the [USZIPSERVICE] section ------  
Using COMMAND LINE ARG: Ini file = CustomSettings.ini  
CHECKING the [USZIPSERVICE] section  
About to execute web service call to http://www.webservicex.net/uszip.asmx/GetInfoByZIP: USZip=98052  
Response from web service: 200 OK  
Successfully executed the web service.  
Property CITY is now = Redmond  
Obtained CITY value from web service:  CITY = Redmond  
Property STATE is now = WA  
Obtained STATE value from web service:  STATE = WA  
Property ZIP is now = 98052  
Obtained ZIP value from web service:  ZIP = 98052  
Property AREA_CODE is now = 425  
Obtained AREA_CODE value from web service:  AREA_CODE = 425  
------ Done processing CustomSettings.ini ------  
```  

 Beim Ausführen eines Webdiensts sollten Sie einige Dinge überwachen, die kleinere Probleme verursachen könnten:  

-   Führen Sie keine besonderen Aktionen mit Proxyservern aus. Sie können anonyme Proxys, sofern vorhanden, verwenden. Die Authentifizierung bei einem Proxyserver kann jedoch Probleme verursachen. In den meisten Fällen wird kein Webdienst aufgerufen.  

-   „CustomSettings.ini“ oder „ZTIGather.xml“ suchen nach Eigenschaften, die im XML-Markup definiert sind, das als Ergebnis des Webdienstaufrufs zurückgegeben wurde (wie bei einer Datenbankabfrage oder einer anderen Regel). Die XML-Suche unterscheidet jedoch zwischen Groß- und Kleinschreibung. Der hier beschriebene Webdienst gibt jedoch alle Eigenschaftsnamen in Großbuchstaben zurück. Dies wird von „ZTIGather.xml“ erwartet. Einträge in Kleinbuchstaben oder mit gemischter Groß- und Kleinschreibung können zur Umgehung des Problems neu zugeordnet werden.  

-   Eine `POST`-Anforderung an den Webdienst wird empfohlen. Daher muss der Webdienstaufruf `POST` unterstützen können.  

## <a name="connecting-to-network-resources"></a>Herstellen einer Verbindung mit Netzwerkressourcen  
 Während der LTI- und ZTI-Bereitstellungsprozesse müssen Sie möglicherweise auf eine Netzwerkressource auf einem Server zugreifen, der nicht der Hostserver der Bereitstellungsfreigabe ist. Sie müssen sich bei dem anderen Server authentifizieren, um dort auf freigegebene Ordner oder Dienste zugreifen zu können. Sie können beispielsweise eine Anwendung aus einem freigegebenen Ordner installieren, der sich auf einem anderen Server als dem Hostserver der Bereitstellungsfreigabe befindet, die die MDT-Skripts verwenden.  

> [!NOTE]
>  Weitere Informationen zum Abfragen von SQL Server-Datenbanken auf einem anderen Server als dem Hostserver der Bereitstellungsfreigabe finden Sie unter den Eigenschaften **Database**, **DBID**, **DBPwd**, **Instance**, **NetLib**, **Order**, **Parameters**, **ParameterCondition**, **SQLServer**, **SQLShare** und **Table** im MDT-Artikel *Toolkit-Referenz*.  

 Mithilfe des Skripts „ZTIConnect.wsf“ können Sie eine Verbindung mit anderen Servern herstellen und auf deren Ressourcen zugreifen. Die Syntax für das Skript „ZTIConnect.wsf“ lautet wie folgt (wobei *unc_path* ein UNC-Pfad (Universal Naming Convention) zur Herstellung einer Verbindung mit dem Server ist):  

```  
Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:unc_path  
```  

 In den meisten Fällen wird das ZTIConnect.wsf-Skript als Task-Sequencer-Aufgabe ausgeführt. Führen Sie das ZTIConnect.wsf-Skript vor Aufgaben aus, die Zugriff auf einen anderen Server als den Hostserver der Bereitstellungsfreigabe benötigen.  

 **So fügen Sie das Skript „ZTIConnect.wsf“ der Tasksequenz eines Builds als Aufgabe hinzu:**  

1.  Klicken Sie auf **Start**, und zeigen Sie auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe* > Tasksequenzen. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Detailbereich auf ***Tasksequenz***. Hierbei entspricht *Tasksequenz* der zu ändernden Tasksequenz.  

4.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

5.  Klicken Sie auf die Registerkarte „Tasksequenz“, navigieren Sie zu **Gruppe** (wobei *Gruppe* der Gruppe entspricht, in der das Skript „ZTIConnect.wsf“ ausgeführt werden soll), und klicken Sie auf **Hinzufügen**. Klicken Sie auf **Allgemein** und anschließend auf **Befehlszeile ausführen**.  

    > [!NOTE]
    >  Fügen Sie die Aufgabe vor anderen Aufgaben hinzu, die Zugriff auf Ressourcen auf dem Zielserver benötigen.  

6.  Füllen Sie die Registerkarte **Eigenschaften** der neuen Aufgabe mit den folgenden Informationen aus:

    |**Feld** |**Vorgehensweise** |  
    |-|-|  
    |**Name** |Geben Sie **Mit Server verbinden** ein (wobei „Server“ dem Name des Servers entspricht, mit dem die Verbindung hergestellt werden soll).|  
    |**Beschreibung** |Geben Sie erklärenden Text ein, warum die Verbindung hergestellt werden soll.|  
    |**Befehl** |Geben Sie **Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:unc_path** ein (wobei *unc_path* dem UNC-Pfad zu einem freigegebenen Ordner auf dem Server entspricht).|  

7.  Füllen Sie die Registerkarte **Optionen** der neuen Aufgabe mit den folgenden Informationen aus: Sofern nicht anders angegeben, belassen Sie die Standardwerte, und klicken Sie auf **OK**.  

    |**Feld** |**Vorgehensweise** |  
    |-|-|  
    |**Erfolgscodes** |Geben Sie **0 3010** ein. (Das Skript „ZTIConnect.wsf“ gibt nach erfolgreichem Abschluss diese Codes zurück.)|  
    |**Listenfeld „Bedingungen“** |Fügen Sie alle Bedingungen hinzu, die möglicherweise erforderlich sind. (In den meisten Fällen sind für diese Aufgabe keine Bedingungen erforderlich.)|  

 Nachdem die Aufgabe hinzugefügt wurde, die das Skript „ZTIConnect.wsf“ ausführt, können nachfolgende Aufgaben auf Netzwerkressourcen auf dem in der **/uncpath**-Option des Skripts „ZTIConnect.wsf“ angegebenen Server zugreifen.  

## <a name="deploying-the-correct-device-drivers-to-computers-with-the-same-hardware-devices-but-different-make-and-model"></a>Bereitstellen der korrekten Gerätetreiber auf Computern mit identischen Hardwaregeräten aber unterschiedlichem Typ und Modell  
 Selbst bei einem nahezu identischen Treibersatz gibt es viele unterschiedliche Modellnummern und Bezeichnungen. Wegen dieser unterschiedlichen Modellnummern und Bezeichnungen verbringen Sie möglicherweise unnötig viel Zeit mit der Eingabe von mehreren Datenbankeinträgen für ein bestimmtes Modell. Mit der folgenden Vorgehensweise können Sie eine neue Eigenschaft mithilfe des Funktionsaufrufs „Benutzerabbruch“ definieren, der eine Teilzeichenfolge der Modellnummer zurückgibt:  

 **So erstellen Sie Modell-Aliase:**  

1.  Klicken Sie auf **Start**, und zeigen Sie auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

4.  Klicken Sie im Dialogfeld **Eigenschaften** auf die Registerkarte **Regeln**.  

5.  Erstellen Sie Aliase für Hardwaretypen in den Abschnitten zu Typ und Modell der MDT-Datenbank. Kürzen Sie den Modelltyp an der geöffneten Klammer „(“ in der Modellbezeichnung. So wird beispielsweise *HP DL360 (G112)* zu *HP DL360* verkürzt.  

6.  Fügen Sie jedem Abschnitt die benutzerdefinierte Variable **ModelAlias** hinzu.  

7.  Erstellen Sie einen neuen `[SetModel]`-Abschnitt.  

8.  Fügen Sie den **Priorität**-Einstellungen im `[Settings]`-Abschnitt den `[SetModel]`-Abschnitt hinzu.  

9. Fügen Sie dem `ModelAlias`-Abschnitt eine Zeile hinzu, um auf ein Benutzerabbruchskript zu verweisen, das die Modellbezeichnung bei „(“ kürzt.  

10. Erstellen Sie eine **MMApplications**-Datenbanksuche, in der **ModelAlias** und **Model** identisch sind.  

11. Erstellen Sie ein Benutzerabbruchskript, und platzieren Sie es zur Verkürzung der Modellbezeichnung im selben Verzeichnis wie die Datei „CustomSettings.ini“.  

    Die folgenden beiden Beispiele zeigen jeweils eine CustomSettings.ini-Datei und ein Benutzerabbruchskript.  

     **CustomSettings.ini:**  

    ```  
    [Settings]   
    Priority=SetModel, MMApplications, Default   
    Properties= ModelAlias   
    [SetModel]   
    ModelAlias=#SetModelAlias()#   
    Userexit=Userexit.vbs   
    [MMApplications]   
    SQLServer=Server1  
    Database=MDTDB   
    Netlib=DBNMPNTW   
    SQLShare=logs   
    Table= MakeModelSettings    
    Parameters=Make, ModelAlias   
    ModelAlias=Model   
    Order=Sequence  
    ```  

     **Benutzerabbruchskript:**  

    ```  
    Function UserExit(sType, sWhen, sDetail, bSkip)   
      UserExit = Success   
    End Function   

    Function SetModelAlias()   
      If Instr(oEnvironment.Item("Model"), "(") <> 0 Then   
        SetModelAlias = Left(oEnvironment.Item("Model"), _  
                          Instr(oEnvironment.Item("Model"), _  
                            "(") - 1)   
        oLogging.CreateEntry "USEREXIT – " & _  
          "ModelAlias has been set to " & SetModelAlias, _  
          LogTypeInfo  
      Else   
        SetModelAlias = oEnvironment.Item("Model")   
        oLogging.CreateEntry " USEREXIT - " & _  
          "ModelAlias has not been changed.", LogTypeInfo   
      End if   
    End Function  
    ```  

## <a name="configuring-conditional-task-sequence-steps"></a>Konfigurieren von bedingten Tasksequenzschritten  
 In einigen Szenarios sollten Sie einen Tasksequenzschritt entsprechend definierter Kriterien bedingt ausführen. Beliebige Kombinationen aus diesen Bedingungen können hinzugefügt werden, um zu bestimmen, ob der Tasksequenzschritt ausgeführt werden soll. So können Sie beispielsweise mit dem Wert einer Tasksequenzvariable und dem Wert einer Registrierungseinstellung bestimmen, ob ein Tasksequenzschritt ausgeführt werden soll.  

 Verwenden Sie die folgenden Bedingungen, um eine Tasksequenz mithilfe von MDT bedingt auszuführen:  

-   eine oder mehrere **IF**-Anweisungen  

-   eine Tasksequenzvariable  

-   die Version des Zielbetriebssystems  

-   die booleschen Ergebnisse einer WMI-Abfrage  

-   eine Registrierungseinstellung  

-   die auf dem Zielcomputer installierte Software  

-   die Eigenschaften eines Ordners  

-   die Eigenschaften einer Datei  

### <a name="configuring-a-conditional-task-sequence-step"></a>Konfigurieren eines bedingten Tasksequenzschritts  
 Bedingte Tasksequenzschritte werden in der Deployment Workbench auf der Registerkarte **Optionen** eines Tasksequenzschritts konfiguriert. Sie können dem Tasksequenzschritt eine oder mehrere Bedingungen hinzufügen, um die passende Bedingung für die Ausführung oder Nichtausführung des Schritts zu erstellen.  

> [!NOTE]
>  Für jeden bedingten Tasksequenzschritt ist mindestens eine **IF**-Anweisung erforderlich.  

 **So zeigen Sie die Registerkarte „Optionen“ eines Tasksequenzschritts an:**  

1.  Klicken Sie auf **Start**, und zeigen Sie auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe* > Tasksequenzen. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Detailbereich auf **Tasksequenz**. Hierbei entspricht *Tasksequenz* der Bezeichnung der zu konfigurierenden Tasksequenz.  

4.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

5.  Klicken Sie im Dialogfeld **Eigenschaften** für ***Tasksequenz*** auf der Registerkarte **Tasksequenz** auf ***Schritt*** (wobei *Schritt* der Bezeichnung der zu konfigurierenden Tasksequenz entspricht). Klicken Sie anschließend auf die Registerkarte **Optionen**.  

 Führen Sie auf der Registerkarte **Optionen** des Tasksequenzschritts die folgenden Aktionen aus:  

-   **Hinzufügen**: Klicken Sie auf diese Schaltfläche, um dem Tasksequenzschritt eine Bedingung hinzuzufügen.  

-   **Entfernen**: Klicken Sie auf diese Schaltfläche, um aus dem Tasksequenzschritt eine vorhandene Bedingung zu entfernen.  

-   **Bearbeiten**: Klicken Sie auf diese Schaltfläche, um eine vorhandene Bedingung in einem Tasksequenzschritt zu ändern.  

### <a name="if-statements-in-conditions"></a>IF-Anweisungen in Bedingungen  
 Alle Tasksequenzbedingungen enthalten mindestens eine **IF**-Anweisung. **IF**-Anweisungen bilden die Grundlage für die Erstellung bedingter Tasksequenzschritte. Eine Bedingung für einen Tasksequenzschritt kann nur eine **IF**-Anweisung enthalten. Unterhalb der obersten **IF**-Anweisung können jedoch mehrere **IF**-Anweisungen geschachtelt werden, um komplexere Bedingungen zu erstellen.  

 Eine **IF**-Anweisung kann auf den folgenden Bedingungen basieren, die im Dialogfeld **Eigenschaften der IF-Anweisung** konfiguriert werden.  

 |**Bedingung** |**Wählen Sie diese Option zum Ausführen der Tasksequenz in folgenden Fällen aus:** |  
 |-|-|  
 |**Alle Bedingungen** |Alle Bedingungen unterhalb dieser **IF**-Anweisung müssen erfüllt sein.|  
 |**Mindestens eine Bedingung** |Mindestens eine Bedingung unterhalb dieser **IF**-Anweisung muss erfüllt sein.|  
 |**Keine** |Keine der Bedingungen unterhalb dieser **IF**-Anweisung muss erfüllt sein.|  

 Fügen Sie weitere Kriterien zu den Bedingungen hinzu (wie z.B. Tasksequenzvariablen oder Werte in einer Registrierungseinstellung), um die Bedingung für das Ausführen des Tasksequenzschritts zu vervollständigen.  

 **So fügen Sie einem Tasksequenzschritt eine Bedingung für die IF-Anweisung hinzu:**  

1.  Gehen Sie zur Registerkarte **Optionen** unter ***Schritt*** (wobei *Schritt* der Bezeichnung des zu konfigurierenden Tasksequenzschritts entspricht). Klicken Sie auf **Hinzufügen** und anschließend auf **IF-Anweisung**.  

2.  Klicken Sie im Dialogfeld **Eigenschaften der IF-Anweisung** auf **Bedingung** (wobei *Bedingung* einer der Bedingungen in der vorherigen Tabelle entspricht), und klicken Sie dann auf **OK**.  

### <a name="task-sequence-variables-in-conditions"></a>Tasksequenzvariablen in Bedingungen  
 Verwenden Sie die Bedingung **Tasksequenzvariable**, um eine beliebige Tasksequenzvariable auszuwerten, die durch die Aufgabe **Tasksequenzvariable festlegen** oder eine andere Aufgabe in der Tasksequenz erstellt wurde. Stellen Sie sich beispielsweise ein Netzwerk mit Windows XP-Clientcomputern vor, von denen einige einer Domäne angehören und einige sich in einer Arbeitsgruppe befinden. Da aufgrund der aktuellen Domänenrichtlinie alle Benutzereinstellungen im Netzwerk gespeichert werden müssen, müssen die Benutzereinstellungen möglicherweise nur für Computer gespeichert werden, die nicht der Domäne angehören, d.h. sich in der Arbeitsgruppe befinden. Fügen Sie in diesem Fall der Aufgabe **Benutzerdateien und Einstellungen erfassen** eine Bedingung hinzu, die sich an die Computer in der Arbeitsgruppe richtet.  

 **So fügen Sie eine Bedingung basierend auf einer Tasksequenzvariable hinzu:**  

1.  Gehen Sie zur Registerkarte **Optionen** unter ***Schritt*** (wobei *Schritt* der Bezeichnung des zu konfigurierenden Tasksequenzschritts entspricht). Klicken Sie auf **Bedingung hinzufügen** und anschließend auf **Tasksequenzvariable**.  

2.  Geben Sie im Dialogfeld **Tasksequenzvariable** der Bedingung im Feld **Variable** Folgendes ein: **OSDJoinType**.  

    > [!NOTE]
    >  Diese Variable wird für Computer, die einer Domäne angehören, auf **0** festgelegt und für Computer in einer Arbeitsgruppe auf **1**.  

3.  Klicken Sie im Feld **Bedingung** auf **Gleich**.  

4.  Geben Sie in das Feld **Wert** den Wert **1** ein, und klicken Sie auf **OK**.  

### <a name="operating-system-version-in-conditions"></a>Betriebssystemversionen in Bedingungen  
 Verwenden Sie zur Überprüfung der vorhandenen Betriebssystemversion des Zielcomputers oder des vorhandenen Clients (beim Erfassen eines Images) die Bedingung **Betriebssystemversion**. Stellen Sie sich beispielsweise ein Netzwerk mit mehreren Servern vor, die von Windows Server 2003 auf Windows Server 2008 aktualisiert werden sollen. Die Netzwerkeinstellungen sollten nur auf Server kopiert und angewendet werden, auf denen Windows Server 2003 ausgeführt wird. Alle anderen Servern verfügen über die Standardnetzwerkeinstellungen, die von Windows Server 2008 verwendet werden.  

 **So fügen Sie eine Bedingung basierend auf der Betriebssystemversion hinzu:**  

1.  Klicken Sie im Tasksequenz-Editor auf die Aufgabe **Netzwerkeinstellungen erfassen**.  

2.  Klicken Sie auf **Bedingung hinzufügen** und anschließend auf **Betriebssystemversion**.  

3.  Klicken Sie im Feld **Architektur** auf den entsprechenden Server. Klicken Sie in diesem Beispiel auf **x86**.  

4.  Klicken Sie im Feld **Betriebssystem** auf das Betriebssystem und die Version, für die eine Bedingung festgelegt werden soll. Klicken Sie in diesem Beispiel auf **x86 Windows 2003**.  

5.  Klicken Sie im Feld **Bedingung** auf die entsprechende Bedingung und anschließend auf **OK**.  

### <a name="file-properties-in-conditions"></a>Dateieigenschaften in Bedingungen  
 Verwenden Sie zur Überprüfung der Version und/oder des Zeitstempels einer bestimmten Datei die Bedingung **Dateieigenschaften**, um zu entscheiden, ob eine Aufgabe oder eine Gruppe von Aufgaben ausgeführt werden soll. In diesem Beispiel enthält die Produktionsumgebung ein Image von Windows Server 2003, das ständig aktualisiert und für jeden neuen Server, der dem Netzwerk hinzugefügt wird, verwendet wird. Auf allen Servercomputern in der Umgebung wird eine benutzerdefinierte Anwendung ausgeführt, die die Version 3.60.6815 der DAO-Anwendungsprogrammierschnittstelle (Digital Access Object) erfordert.  

 Alle vorhandenen Server funktionieren ordnungsgemäß. Jeder neuer Server, der dem Netzwerk mit dem Image hinzugefügt wird, kann die Anwendung jedoch nicht ausführen. Da die Verwaltung und Aktualisierung von Images zur Zuständigkeit einer anderen Gruppe gehört, sollte hier die Bereitstellungstasksequenz dahingehend geändert werden, dass die entsprechende DAO-Version installiert wird, wenn die vorhandene mit dem Image bereitgestellte DAO-Version nicht korrekt ist.  

 **So fügen Sie einem Tasksequenzschritt in Configuration Manager 2007 R3 die Bedingung „Dateieigenschaften“ hinzu:**  

1.  Erstellen Sie in Configuration Manager 2007 R3 ein Paket zum Installieren von DAO 3.60.6815. Geben Sie diesem Paket den Namen *DAO* mit einem Programm namens *InstallDAO*. Weitere Informationen zum Erstellen von Paketen finden Sie unter [Erstellen eines Pakets](http://technet.microsoft.com/library/bb693627.aspx).  

2.  Erstellen Sie den Schritt **Software installieren**, um das DAO-Paket bereitzustellen.  

3.  Klicken Sie auf den in Schritt 2 erstellten Tasksequenzschritt **Software installieren**, und klicken Sie dann auf die Registerkarte **Optionen**.  

4.  Klicken Sie auf **Bedingung hinzufügen** und dann auf **Dateieigenschaften**.  

5.  Geben Sie im Feld **Pfad** Folgendes ein: **C:\Program Files\Microsoft Shared\DAO\dao360.dll**.  

6.  Aktivieren Sie das Kontrollkästchen **Version überprüfen**, und klicken Sie dann für die Bedingung auf **Ungleich**.  

7.  Geben Sie im Feld **Version** Folgendes ein: **3.60.6815**.  

8.  Deaktivieren Sie in diesem Fall das Kontrollkästchen **Zeitstempel überprüfen**, und klicken Sie dann auf **OK**.  

### <a name="folder-properties-in-conditions"></a>Ordnereigenschaften in Bedingungen  
 Verwenden Sie zur Überprüfung des Zeitstempels eines bestimmten Ordners die Bedingung **Ordnereigenschaften**, um zu bestimmen, ob eine Aufgabe oder eine Gruppe von Aufgaben ausgeführt werden soll. Stellen Sie sich beispielsweise vor, dass eine intern entwickelte Anwendung für die Zusammenarbeit mit Windows 8 aktualisiert wurde. Allerdings wurde nicht auf allen Computern im Netzwerk die neueste Version der Anwendung installiert. Daher muss vor einem Upgrade der Anwendung ein Datenkonvertierungsprozess ausgeführt werden.  

 Lautet der Zeitstempel des Ordners, in dem die Anwendung installiert wurde, 31.12.2007 oder früher, wird auf dem Zielcomputer eine inkompatible Version der Anwendung ausgeführt. In diesem Fall sollten Sie einen Datenkonvertierungsprozess auf dem Zielcomputer ausführen. Führen Sie entsprechend der Bedingung einen Tasksequenzschritt zur Ausführung des Datenkonvertierungsprozesses auf Computern aus, die über eine frühere Version der Anwendung verfügen.  

 **So fügen Sie einem Tasksequenzschritt die Bedingung „Ordnereigenschaften“ hinzu:**  

1.  Gehen Sie in der Configuration Manager-Konsole oder in der Deployment Workbench zum Tasksequenz-Editor, und bearbeiten Sie ***Tasksequenz*** (wobei *Tasksequenz* der zu bearbeitenden Tasksequenz entspricht).  

2.  Erstellen Sie die Aufgabe **Befehlszeile**, um den Datenkonvertierungsprozess auszuführen.  

3.  Klicken Sie auf die Aufgabe, die Sie in Schritt 1 erstellt haben.  

4.  Klicken Sie auf **Bedingung hinzufügen** und dann auf **Ordnereigenschaften**.  

5.  Geben Sie im Feld **Pfad** den Pfad des Ordners ein, der die Anwendung enthält.  

6.  Aktivieren Sie das Kontrollkästchen **Zeitstempel überprüfen**.  

7.  Klicken Sie für die Bedingung auf **Kleiner als oder gleich**.  

8.  Klicken Sie im Feld **Datum** auf **31.12.2007**.  

9. Klicken Sie im Feld **Uhrzeit** auf **12:00:00 Uhr**, und klicken Sie dann auf **OK**.  

### <a name="registry-settings-in-conditions"></a>Registrierungseinstellungen in Bedingungen  
 Verwenden Sie die Bedingung **Registrierungseinstellung**, um zu überprüfen, ob in der Registrierung Schlüssel und Werte sowie die entsprechenden in den Registrierungswerten gespeicherten Daten vorhanden sind. Stellen Sie sich beispielsweise vor, dass eine derzeit auf eine kleine Gruppe von Computern angewendete Anwendung nicht unter Windows 8 ausgeführt werden kann. Eine Windows 8-Bereitstellung soll hier für ein Upgrade bei Computern sorgen, auf denen derzeit Windows XP ausgeführt wird. Erstellen Sie eine Bedingung für die erste Aufgabe einer Sequenz, um in der Registrierung nach einem Eintrag für die inkompatible Anwendung zu suchen und bei erfolgreicher Suche den Bereitstellungsprozess für diesen Computer zu unterbrechen.  

 **So fügen Sie einem Tasksequenzschritt eine Bedingung für die Registrierungseinstellung hinzu:**  

1.  Gehen Sie in der Configuration Manager-Konsole oder in der Deployment Workbench zum Tasksequenz-Editor, und bearbeiten Sie ***Tasksequenz*** (wobei *Tasksequenz* der Tasksequenz entspricht, die Windows 8 bereitstellt).  

2.  Klicken Sie auf die erste Aufgabe der Sequenz, und klicken Sie dann auf die Registerkarte **Optionen**.  

3.  Klicken Sie auf **Bedingung hinzufügen** und dann auf **Registrierungseinstellung**.  

4.  Klicken Sie in der Liste **Stammschlüssel** auf **HKEY_LOCAL_MACHINE**.  

5.  Geben Sie in das Feld **Schlüssel** Folgendes ein: **SOFTWARE\WOODGROVE**.  

6.  Klicken Sie für die Bedingung auf **Nicht vorhanden**. In diesem Fall wird die Aufgabe nur ausgeführt und die Sequenz nur fortgesetzt, wenn der Schlüssel nicht vorhanden ist.  

7.  Wenn Sie den Wertnamen in das Feld **Wertname** eingeben, kann die Bedingung optional überprüfen, ob ein Wert nicht vorhanden ist.  

8.  Wenn eine andere Bedingung als **Vorhanden/Nicht vorhanden** verwendet wurde, geben Sie einen Wert und Werttyp an.  

9. Klicken Sie auf **OK**.  

### <a name="wmi-queries-in-conditions"></a>WMI-Abfragen in Bedingungen  
 Verwenden Sie zum Ausführen einer beliebigen WMI-Abfrage die Bedingung **WMI-Abfrage**. Die Bedingung wird mit TRUE bewertet, wenn die Abfrage mindestens ein Ergebnis zurückgibt. Stellen Sie sich beispielsweise vor, dass ein Bereitstellungsteam für das Betriebssystem aller Server eines bestimmten Modells (z.B. Dell 1950) ein Upgrade durchführen muss. Mit einer WMI-Abfrage kann das Modell jedes Computers überprüft und die Bereitstellung nur dann fortgesetzt werden, wenn das richtige Modell gefunden wird.  

 **So fügen Sie einem Tasksequenzschritt eine Bedingung für die WMI-Abfrage hinzu:**  

1.  Gehen Sie in der Configuration Manager-Konsole oder in der Deployment Workbench zum Tasksequenz-Editor, und bearbeiten Sie ***Tasksequenz*** (wobei *Tasksequenz* der Tasksequenz entspricht, mit der ein Upgrade der Server durchgeführt wird).  

2.  Klicken Sie auf die erste Aufgabe der Sequenz, und klicken Sie dann auf die Registerkarte **Optionen**.  

3.  Klicken Sie auf **Bedingung hinzufügen** und dann auf **WMI abfragen**.  

4.  Geben Sie im Feld **WMI-Namespace** Folgendes ein: **root\cimv2**.  

5.  Geben Sie im Feld **WQL-Abfrage** Folgendes ein: **SELECT \* FROM Win32_ComputerSystem WHERE Model LIKE "%Dell%%1950%"**. Klicken Sie auf **OK**.  

### <a name="installed-software-in-conditions"></a>Installierte Software in Bedingungen  
 Verwenden Sie die Bedingung **Installierte Software**, um zu überprüfen, ob eine bestimmte Software derzeit auf einem Zielcomputer installiert ist. Mit dieser Bedingung kann nur Software bewertet werden, die mit MSI-Dateien (Microsoft Installer) installiert wurde. Stellen Sie sich beispielsweise vor, dass Sie für das Betriebssystem aller Server ein Upgrade durchführen möchten, mit Ausnahme derjenigen, auf denen Microsoft SQL Server 2012 ausgeführt wird.  

 **So fügen Sie einem Tasksequenzschritt eine Bedingung für installierte Software hinzu:**  

1.  Gehen Sie in der Configuration Manager-Konsole oder in der Deployment Workbench zum Tasksequenz-Editor, und bearbeiten Sie ***Tasksequenz*** (wobei *Tasksequenz* der Tasksequenz entspricht, mit der ein Upgrade der Server durchgeführt wird).  

2.  Klicken Sie auf die erste Aufgabe der Sequenz, und klicken Sie dann auf die Registerkarte **Optionen**.  

3.  Klicken Sie auf **Bedingung hinzufügen** und dann auf **Installierte Software**.  

4.  Klicken Sie auf **Durchsuchen** und anschließend auf die MSI-Datei für SQL Server 2012.  

5.  Aktivieren Sie das Kontrollkästchen **Auf dieses bestimmte Produkt anwenden**, um nur Computer mit SQL Server 2012 und keiner anderen Version als Zielcomputer dieser Abfrage anzugeben.  

6.  Klicken Sie auf **OK**.  

### <a name="complex-conditions"></a>Komplexe Bedingungen  
 Mehrere Bedingungen können mithilfe von **IF**-Anweisungen zu komplexen Bedingungen gruppiert werden. Stellen Sie sich beispielsweise vor, dass ein bestimmter Schritt nur für Contoso 1950-Computer ausgeführt werden soll, auf denen Windows Server 2003 oder Windows Server 2008 ausgeführt wird. Als programmgesteuerte **IF**-Anweisung würde dies etwa folgendermaßen aussehen:  

```  
IF ((Computer Model IS “Contoso 1950”) AND (operating system=2003 OR operating system=2008))  
```  

 **So fügen Sie eine komplexe Bedingung hinzu:**  

1.  Gehen Sie in der Configuration Manager-Konsole oder in der Deployment Workbench zum Tasksequenz-Editor, und bearbeiten Sie ***Tasksequenz*** (wobei *Tasksequenz* der Tasksequenz entspricht, mit der ein Upgrade der Server durchgeführt wird).  

2.  Klicken Sie auf den Tasksequenzschritt, dem die Bedingung hinzugefügt werden soll, und klicken Sie dann auf die Registerkarte **Optionen**.  

3.  Klicken Sie auf **Bedingung hinzufügen**, auf **IF-Anweisung** und anschließend auf **Alle Bedingungen**. Klicken Sie auf **OK**.  

4.  Klicken Sie auf die Bedingungsanweisung, auf **Bedingung hinzufügen** und anschließend auf **WMI-Abfrage**.  

5.  Vergewissern Sie sich, dass **root\cimv2** als WMI-Namespace angegeben ist. Geben Sie in das Feld **WQL-Abfrage** Folgendes ein: **SELECT \* FROM Win32_ComputerSystem WHERE ComputerModel LIKE “%Contoso%1950%”**. Klicken Sie auf **OK**.  

6.  Klicken Sie auf die **IF**-Anweisung und anschließend auf **Bedingung hinzufügen**. Klicken Sie auf **IF-Anweisung** und anschließend auf **Beliebige Bedingung**. Klicken Sie auf **OK**.  

7.  Klicken Sie auf die zweite **IF**-Anweisung. Klicken Sie auf **Bedingung hinzufügen** und anschließend auf **Betriebssystemversion**.  

8.  Klicken Sie im Feld **Architektur** auf die Serverarchitektur. Klicken Sie in diesem Beispiel auf **x86**.  

9. Klicken Sie im Feld **Betriebssystem** auf das Betriebssystem und die Version. Klicken Sie in diesem Beispiel auf **x86 Windows 2003 original release** (x86 Windows 2003, Originalrelease). Klicken Sie auf **OK**.  

10. Klicken Sie auf die zweite **IF**-Anweisung. Klicken Sie auf **Bedingung hinzufügen** und anschließend auf **Betriebssystemversion**.  

11. Klicken Sie im Feld **Architektur** auf die Serverarchitektur. Klicken Sie in diesem Beispiel auf **x86**.  

12. Klicken Sie im Feld **Betriebssystem** auf das Betriebssystem und die Version. Klicken Sie in diesem Beispiel auf **x86 Windows 2008 original release** (x86 Windows 2003, Originalrelease). Klicken Sie auf **OK**.  

## <a name="creating-a-highly-scalable-lti-deployment-infrastructure"></a>Erstellen einer hochgradig skalierbaren LTI-Bereitstellungsinfrastruktur  
 In diesem Szenario ist für die Bereitstellungsinfrastruktur keine elektronische Softwareverteilung verfügbar. Sie erstellen daher mit dem MDT eine Infrastruktur für eine vollständig automatisierte LTI-Bereitstellung. Für die skalierbare LTI-Infrastruktur werden SQL Server, Windows-Bereitstellungsdienste und DFS-Replikationstechnologien für Windows Server 2003 verwendet.  

 Für die Skalierung der LTI-Infrastruktur sind folgende Schritte erforderlich:  

-   [Stellen Sie sicher, dass eine entsprechende Infrastruktur vorhanden ist.](#EnsureInfrastructure)  

-   [Fügen Sie Inhalte zum MDT hinzu.](#AddContent)  

-   [Bereiten Sie Windows-Bereitstellungsdienste vor.](#PrepareDeployment)  

-   [Konfigurieren Sie die DFS-Replikation.](#ConfigureFileReplication)  

-   [Bereiten Sie die SQL Server-Replikation vor.](#PrepareSQLReplication)  

-   [Konfigurieren Sie die SQL Server-Replikation](#ConfigureSQLReplication)  

 In diesem Szenario wird davon ausgegangen, dass wie zu Beginn dieses Artikels erläutert wurde das MDT auf einem Masterbereitstellungsserver konfiguriert ist und die Konfiguration der MDT-Datenbank bereits abgeschlossen wurde.  

###  <a name="EnsureInfrastructure"></a> Sicherstellen, dass eine entsprechende Infrastruktur vorhanden ist  
 Für die hochgradig skalierbare LTI-Bereitstellungsinfrastruktur wird eine Hub-and-Spoke-Topologie (engl. Nabe und Speiche) für die Replikation von Inhalten verwendet. Sie müssen daher zuerst in der Produktionsumgebung einen Bereitstellungsserver festlegen, der die Rolle des Masterbereitstellungsservers übernimmt.  Im Folgenden werden die erforderlichen Komponenten für den Masterbereitstellungsserver aufgeführt:  

 |**Erforderliche Komponente** |**Zweck/Kommentar** |  
 |-|-|  
 |Windows Server 2003 R2|Für DFS-Replikation erforderlich|  
 |MDT |Enthält die Masterkopie der Bereitstellungsfreigabe|  
 |SQL Server 2005|Muss eine Vollversion sein, damit die Replikation einer MDT-Datenbank zulässig ist|  
 |DFS-Replikation |Für die Replikation der Bereitstellungsfreigabe erforderlich|  
 |Windows-Bereitstellungsdienste |Erforderlich für das Zulassen netzwerkbasierter PXE-Installationen|  

 Nach der Auswahl des Masterbereitstellungsservers ist es erforderlich, dass Sie zusätzliche Server an allen Standorten bereitstellen, damit LTI-Bereitstellungen unterstützt werden.  Im Folgenden werden die erforderlichen Komponenten für den untergeordneten Bereitstellungsserver aufgeführt:  

 |**Erforderliche Komponente** |**Zweck/Kommentar** |  
 |-|-|  
 |Windows Server 2003 R2|Für DFS-Replikation erforderlich|  
 |Microsoft SQL Server 2005 Express Edition |Empfängt replizierte Kopien der MDT-Datenbank|  
 |DFS-Replikation |Für die Replikation der Bereitstellungsfreigabe erforderlich|  
 |Windows-Bereitstellungsdienste |Erforderlich für das Zulassen netzwerkbasierter PXE-Installationen|  

> [!NOTE]
>  Windows-Bereitstellungsdienste müssen auf jedem untergeordneten Server eingerichtet und konfiguriert werden. Es ist jedoch nicht notwendig, Start- oder Installationsimages hinzuzufügen.  

###  <a name="AddContent"></a> Hinzufügen von Inhalt zum MDT  
 Füllen Sie den Masterbereitstellungsserver mithilfe der Deployment Workbench mit Inhalten auf. Anschließend erstellen Sie die MDT-Datenbank und füllen diese auf. Diese Aktionen werden in den folgenden Abschnitten beschrieben. Informationen zum Auffüllen der Datenbank mit  

-   Anwendungen finden Sie im MDT-Artikel *Using the Microsoft Deployment Toolkit (Verwenden des Microsoft Deployment Toolkit)* im Abschnitt „Configuring Applications in the Deployment Workbench (Konfigurieren von Anwendungen in der Deployment Workbench)“.  

-   Betriebssystemen finden Sie im MDT-Artikel *Using the Microsoft Deployment Toolkit (Verwenden des Microsoft Deployment Toolkit)* im Abschnitt „Configuring Operating Systems in the Deployment Workbench (Konfigurieren von Betriebssystemen in der Deployment Workbench)“.  

-   Betriebssystempaketen finden Sie im MDT-Artikel *Using the Microsoft Deployment Toolkit (Verwenden des Microsoft Deployment Toolkit)* im Abschnitt „Configuring Packages in the Deployment Workbench (Konfigurieren von Paketen in der Deployment Workbench)“.  

-   Gerätetreibern finden Sie im MDT-Artikel *Using the Microsoft Deployment Toolkit (Verwenden des Microsoft Deployment Toolkit)* im Abschnitt „Configuring Device Drivers in the Deployment Workbench (Konfigurieren von Gerätetreibern in der Deployment Workbench)“.  

-   Tasksequenzen finden Sie im MDT-Artikel *Using the Microsoft Deployment Toolkit (Verwenden des Microsoft Deployment Toolkit)* im Abschnitt „Configuring Task Sequences in the Deployment Workbench (Konfigurieren von Tasksequenzen in der Deployment Workbench)“.  

> [!NOTE]
>  Stellen Sie sicher, dass die Datei „LiteTouchPE_x86.wim“, die bei der Aktualisierung der Bereitstellungsfreigabe erstellt wird, Windows-Bereitstellungsdienste hinzugefügt wurde.  

###  <a name="PrepareDeployment"></a> Vorbereiten von Windows-Bereitstellungsdienste  
 Da die Datei „LiteTouchPE_x86.wim“ in regelmäßigen Abständen über die Replikationsgruppe der DFS-Replikation repliziert wird, muss der Startkonfigurations-Datenspeicher in regelmäßigen Abständen aktualisiert werden, damit er der neu replizierten Windows PE-Umgebung angepasst wird. Führen Sie die folgenden Schritte auf allen Bereitstellungsservern aus.  

 **So bereiten Sie Windows-Bereitstellungsdienste vor**  

1.  Öffnen Sie ein Eingabeaufforderungsfenster.  

2.  Geben Sie **WDSUtil/set-server/BCDRefreshPolicy/Enabled:yes/RefreshPeriod:60** ein, und drücken Sie anschließend die EINGABETASTE.  

> [!NOTE]
>  Im hier dargestellten Beispiel wird der Aktualisierungszeitraum auf 60 Minuten festgelegt. Sie können diesen Wert jedoch auch so konfigurieren, dass eine Replikation in demselben Zeitraum wie dem der DFS-Replikation vorgenommen wird.  

###  <a name="ConfigureFileReplication"></a> Konfigurieren der DFS-Replikation  
 Beim Skalieren der LTI-Bereitstellungsarchitektur verwenden Sie die DFS-Replikation als Grundlage für die Replikation von Inhalten der MDT-Bereitstellungsfreigabe und der Lite Touch-Startumgebung von Windows PE sowie für die Replikation von Inhalten des Masterbereitstellungsservers auf den untergeordneten Bereitstellungsservern.  

> [!NOTE]
>  Stellen Sie sicher, dass die DFS-Replikation installiert ist, bevor Sie die folgenden Schritte ausführen.  

 **So konfigurieren Sie die DFS-Replikation, um den Bereitstellungsinhalt zu replizieren:**  

1.  Öffnen Sie die DFS-Verwaltungskonsole.  

2.  Erweitern Sie den Knoten „DFS-Verwaltung“.  

3.  Klicken Sie mit der rechten Maustaste auf **Replikation**, und klicken Sie anschließend auf **Neue Replikationsgruppe**.  

4.  Klicken Sie im Assistenten für neue Replikationsgruppen auf der Seite **Replikationsgruppentyp** auf **New Multipurpose Replication Group** (Neue Mehrzweckreplikationsgruppe).  

5.  Klicken Sie auf **Weiter**.  

6.  Geben Sie auf der Seite **Name und Domäne** die folgenden Informationen ein:  

    -   Geben Sie im Feld **Name for replication group** (Name der Replikationsgruppe) einen Namen für die Replikationsgruppe ein, beispielsweise **MDT 2010-Replikationsgruppe**.  

    -   Geben Sie im Feld **Optional description of replication group** (Optionale Beschreibung der Replikationsgruppe) eine Beschreibung der Replikationsgruppe ein, beispielsweise **Gruppe für Replikation von MDT 2010-Daten**.  

    -   Achten Sie darauf, dass das Feld **Domäne** den richtigen Domänennamen enthält.  

7.  Klicken Sie auf **Weiter**.  

8.  Führen Sie auf der Seite **Replikationsgruppenmitglieder** die folgenden Schritte aus:  

    1.  Klicken Sie auf **Hinzufügen**.  

    2.  Geben Sie die Namen aller Server ein, die Mitglieder dieser Replikationsgruppe sein sollen. Beispiele sind alle untergeordneten Bereitstellungsserver und der Masterbereitstellungsserver.  

    3.  Klicken Sie auf **OK**.  

9. Klicken Sie auf **Weiter**.  

10. Klicken Sie auf der Seite **Topologieauswahl** zuerst auf **Hub-and-Spoke** und anschließend auf **Weiter**.  

11. Klicken Sie auf der Seite **Hub Members** (Hubmitglieder) zuerst auf den Masterbereitstellungsserver und anschließend auf **Hinzufügen**.  

12. Klicken Sie auf **Weiter**.  

13. Stellen Sie auf der Seite**Hub and Spoke Connections** (Hub-and-Spoke-Verbindungen) sicher, dass für jeden untergeordneten Bereitstellungsserver der Masterbereitstellungsserver als **Required Hub Member** (Erforderliches Hubmitglied) aufgeführt ist.  

14. Klicken Sie auf **Weiter**.  

15. Geben Sie auf der Seite **Replikationsgruppenzeitplan und Bandbreite** einen Zeitplan an, nach dem Inhalte zwischen Servern repliziert werden.  

16. Klicken Sie auf **Weiter**.  

17. Klicken Sie auf der Seite **Primäres Mitglied** im Feld **Primäres Mitglied** auf den Masterbereitstellungsserver.  

18. Klicken Sie auf **Weiter**.  

19. Geben Sie auf der Seite **Zu replizierende Ordner** auf **Hinzufügen**, und führen Sie anschließend die folgenden Schritte aus:  

    1.  Klicken Sie im Feld **Local Path of the folder to replicate** (Lokaler Pfad des zu replizierenden Ordners) auf **Durchsuchen**, um den Ordner *X\\*Deployment aufzurufen, wobei *X* der Laufwerkbuchstabe auf dem Bereitstellungsserver ist.  

    2.  Klicken Sie auf **Use name based on path** (Pfadbasierten Namen verwenden).  

    3.  Klicken Sie auf **OK**.  

    4.  Klicken Sie auf **Hinzufügen**.  

    5.  Klicken Sie im Dialogfeld **Zu replizierenden Ordner hinzufügen** auf **Durchsuchen**, um den Ordner *X:*\RemoteInstall\Boot aufzurufen.  

    6.  Klicken Sie auf **Use name based on path** (Pfadbasierten Namen verwenden).  

20. Klicken Sie auf **Weiter**.  

21. Führen Sie auf der Seite **Local Path of Distribution on Other Members** (Lokaler Verteilungspfad für andere Mitglieder) die folgenden Schritte aus:  

    1.  Wählen Sie alle Mitglieder der Verteilergruppe aus, und klicken Sie anschließend auf **Bearbeiten**.  

    2.  Klicken Sie im Dialogfeld **Edit Local Path** (Lokalen Pfad bearbeiten) auf **Aktiviert**.  

    3.  Geben Sie für den Bereitstellungsfreigabeordner den Speicherpfad, beispielsweise ***X:\Deployment***, auf dem untergeordneten Bereitstellungsserver ein, wobei *X* der Laufwerkbuchstabe auf dem Bereitstellungsserver ist.  

    4.  Klicken Sie auf **OK**.  

22. Klicken Sie auf **Weiter**.  

23. Führen Sie auf der Seite **Local Path of Distribution on Other Members** (Lokaler Startpfad für andere Mitglieder) die folgenden Schritte aus:  

    1.  Wählen Sie alle Mitglieder der Verteilergruppe aus, und klicken Sie anschließend auf **Bearbeiten**.  

    2.  Klicken Sie im Dialogfeld **Edit Local Path** (Lokalen Pfad bearbeiten) auf **Aktiviert**.  

    3.  Geben Sie für den Startfreigabeordner den Speicherpfad, beispielsweise ***X:\RemoteInstall\Boot***, auf dem untergeordneten Bereitstellungsserver ein, wobei *X* der Laufwerkbuchstabe auf dem Bereitstellungsserver ist.  

    4.  Klicken Sie auf **OK**.  

24. Klicken Sie auf **Weiter**.  

25. Klicken Sie auf der Seite **Remote Settings and Create Replication Group** (Remoteeinstellungen und Replikationsgruppe erstellen) auf **Erstellen**, um den Assistenten für neue Replikationsgruppen abzuschließen.  

26. Klicken Sie auf der Seite **Bestätigung** auf **Schließen**, um den Assistenten zu schließen.  

> [!NOTE]
>  Stellen Sie sicher, dass die neue Replikationsgruppe unter dem Knoten „Replikation“ aufgeführt ist.  

###  <a name="PrepareSQLReplication"></a> Vorbereiten der SQL Server-Replikation  
 Vor dem Konfigurieren der SQL Server-Replikation müssen Sie mehrere vorbereitende Schritte ausführen, um sicherzustellen, dass die Bereitstellungsserver ordnungsgemäß konfiguriert sind.  

 **So bereiten Sie die SQL Server-Replikation auf dem Masterbereitstellungsserver vor:**  

1.  Erstellen Sie einen Ordner zum Speichern der Datenbankmomentaufnahmen, und konfigurieren Sie anschließend den Ordner als Freigabe.  

    > [!NOTE]
    >  Weitere Informationen zum Sichern des Momentaufnahmeordners finden Sie unter [Securing the Snapshot Folder (Sichern des Momentaufnahmeordners)](http://msdn2.microsoft.com/library/ms151151.aspx).  

2.  Stellen Sie sicher, dass der SQL Server-Browser-Dienst aktiviert ist und für diesen die Einstellung „Automatisch“ festgelegt ist.  

3.  Klicken Sie im Feld **SQL Server Surface Area Configuration** (SQL Server-Oberflächenkonfiguration) auf **Lokale Verbindungen und Remoteverbindungen**.  

 **So bereiten Sie die SQL Server-Replikation auf dem untergeordneten Bereitstellungsserver vor:**  

1.  Klicken Sie im Feld **SQL Server Surface Area Configuration** (SQL Server-Oberflächenkonfiguration) auf **Lokale Verbindungen und Remoteverbindungen**.  

2.  Erstellen Sie optional eine leere Datenbank zum Hosten der replizierten MDT-Datenbank.  

> [!NOTE]
>  Für diese Datenbank muss derselbe Name wie für die MDT-Datenbank auf dem Masterbereitstellungsserver festgelegt werden. Wenn beispielsweise für die MDT-Datenbank auf dem Masterbereitstellungsserver der Name *MDTDB* festgelegt wurde, ist es erforderlich, dass Sie eine leere Datenbank mit dem Namen *MDTDB* auf dem untergeordneten Bereitstellungsserver erstellen.  

###  <a name="ConfigureSQLReplication"></a> Konfigurieren der SQL Server-Replikation  
 Nach dem Konfigurieren der Datei- und Ordnerreplikation, die zur Erstellung der Bereitstellungsinfrastruktur erforderlich ist, müssen Sie SQL Server konfigurieren, um die MDT-Datenbank replizieren zu können.  

> [!NOTE]
>  Obwohl Sie die Möglichkeit haben, nur eine einzelne, zentrale MDT-Datenbank zu verwalten, erhalten Sie durch die Verwaltung einer replizierten Version der MDT-Datenbank mehr Kontrolle über die Datenübertragung in einem WAN.  

 Von SQL Server 2005 wird ein Replikationsmodell verwendet, das einem Magazinverteilungsmodell ähnelt:  

1.  Ein *Magazin* wird von einem *Verleger* zur Verfügung gestellt (veröffentlicht).  

2.  Durch *Verteiler* wird die Veröffentlichung verteilt.  

3.  *Leser* können die Veröffentlichung abonnieren, sodass diese in regelmäßigen Abständen dem Abonnenten übermittelt wird (dies entspricht einem *Pushabonnement*).  

 Diese Terminologie wird während der gesamten SQL Server-Replikationseinrichtung und in den Konfigurationsassistenten verwendet.  

#### <a name="configure-a-sql-server-publisher"></a>Konfigurieren eines SQL Server-Verlegers  
 Führen Sie die folgenden Schritte aus, um den Masterbereitstellungsserver als SQL Server-Verleger zu konfigurieren:  

1.  Öffnen Sie SQL Server Management Studio.  

2.  Klicken Sie mit der rechten Maustaste auf den Knoten **Replikation** und anschließend mit der linken auf **Verteilung konfigurieren**.  

3.  Klicken Sie im Verteilungskonfigurations-Assistenten auf **Weiter**.  

4.  Klicken Sie auf der Seite **Verteiler** auf **als seinen eigenen Verteiler verwenden. SQL Server erstellt eine Verteilungsdatenbank und ein Protokoll**. Klicken Sie anschließend auf **Weiter**.  

5.  Geben Sie auf der Seite **Momentaufnahmeordner** im Abschnitt **Preparing for SQL Server Replication** (SQL Server-Replikation vorbereiten) den UNC-Pfad zum erstellten Momentaufnahmeordners ein.  

6.  Klicken Sie auf der Seite **Verteilungsdatenbank** auf **Weiter**.  

7.  Klicken Sie auf der Seite **Verleger** zuerst auf den Masterbereitstellungsserver, um diesen als Verteiler festzulegen, und anschließend auf **Weiter**.  

8.  Klicken Sie auf der Seite **Aktionen des Assistenten** zuerst auf **Verteilung konfigurieren** und anschließend auf **Weiter**.  

9. Klicken Sie nach Abschluss des Assistenten zuerst auf **Fertig stellen** und anschließend auf **Schließen**.  

#### <a name="enable-the-mdt-db-for-replication"></a>Aktivieren der MDT-Datenbank für die Replikation  
 Führen Sie die folgenden Schritte aus, um die MDT-Datenbank für die Replikation auf dem Masterbereitstellungsserver zu aktivieren:  

1.  Klicken Sie in SQL Server Management Studio mit der rechten Maustaste auf den Knoten **Replikation** und anschließend mit der linken auf **Verlegereigenschaften**.  

2.  Führen Sie auf der Seite **Verlegereigenschaften** die folgende Schritte aus:  

    1.  Klicken Sie auf **Publisher Databases** (Verlegerdatenbanken).  

    2.  Klicken Sie zuerst auf die MDT-Datenbank und anschließend auf **Transaktionsreplikation**.  

    3.  Klicken Sie auf **OK**.  

 Die MDT-Datenbank ist nun für die Transaktions-und Momentaufnahmereplikation konfiguriert.  

#### <a name="create-a-publication-of-the-mdt-db"></a>Erstellen einer Veröffentlichung der MDT-Datenbank  
 Führen Sie die folgenden Schritte aus, um eine Veröffentlichung der MDT-Datenbank zu erstellen, die die untergeordneten Bereitstellungsserver abonnieren können:  

1.  Erweitern Sie in SQL Server Management Studio den Knoten „Replikation“, und klicken Sie mit der rechten Maustaste auf **Lokale Veröffentlichungen**. Klicken Sie anschließend auf **New Publication** (Neue Veröffentlichung).  

2.  Klicken Sie im Assistenten für neue Veröffentlichungen auf **Weiter**.  

3.  Klicken Sie auf der Seite **Veröffentlichungsdatenbank** zuerst auf die MDT-Datenbank und anschließend auf **Weiter**.  

4.  Klicken Sie auf der Seite **Veröffentlichungstyp** zuerst auf **Momentaufnahmeveröffentlichung** und anschließend auf **Weiter**.  

5.  Wählen Sie auf der Seite **Artikel** alle Elemente für **Tables, Stored Procedures** (Tabellen, gespeicherte Prozeduren) und **Sichten** aus. Klicken Sie anschließend auf **Weiter**.  

6.  Klicken Sie auf der Seite **Articles Issues** (Artikelprobleme) auf **Weiter**.  

7.  Klicken Sie auf der Seite **Tabellenzeilen filtern** auf **Weiter**.  

8.  Führen Sie auf der Seite **Momentaufnahme-Agent** die folgenden Schritte aus:  

    1.  Aktivieren Sie das Kontrollkästchen neben **Momentaufnahme sofort erstellen und zum Initialisieren von Abonnements verfügbar halten**.  

    2.  Aktivieren Sie das Kontrollkästchen neben **Ausführung des Momentaufnahme-Agents zu folgenden Zeitpunkten planen**.  

    3.  Klicken Sie auf **Ändern**.  

    > [!NOTE]
    >  Geben Sie einen Zeitplan an, der eine Stunde vor dem Replizieren der Datenbank in Kraft tritt.  

9. Klicken Sie auf **Weiter**.  

10. Klicken Sie auf der Seite **Agentsicherheit** zuerst auf das Konto, mit dem der Momentaufnahme-Agent ausgeführt werden soll, und anschließend auf **Weiter**.  

11. Klicken Sie auf der Seite **Aktionen des Assistenten** zuerst auf **Veröffentlichung erstellen** und anschließend auf **Weiter**.  

12. Geben Sie auf der Seite **Assistenten abschließen** einen beschreibenden Veröffentlichungsnamen in das Feld **Veröffentlichungsname** ein.  

13. Klicken Sie nach der Erstellung der Veröffentlichung durch den Assistenten zuerst auf **Fertig stellen**, um den Assistenten abzuschließen, und anschließend auf **Schließen**.  

    > [!NOTE]
    >  Die Veröffentlichung wird jetzt unter dem Knoten „Lokale Veröffentlichungen“ in SQL Server Management Studio angezeigt.  

#### <a name="subscribe-child-deployment-servers-to-the-published-mdt-db"></a>Hinzufügen von Bereitstellungsservern als Abonnenten der veröffentlichten MDT-Datenbank  
 Nach der Veröffentlichung der MDT-Datenbank können Sie dieser Veröffentlichung die untergeordneten Bereitstellungsserver als Abonnenten hinzufügen. Die Bereitstellungsserver erhalten dadurch unter Berücksichtigung eines Zeitplans eine Kopie der Datenbank, damit die Clientcomputer während einer Bereitstellung eine Datenbank abfragen können, die sich nicht in einem WAN, sondern lokal im Netzwerk befindet.  

 **So fügen Sie der Veröffentlichung der MDT-Datenbank untergeordnete Bereitstellungsserver als Abonnenten hinzu:**  

1.  Navigieren Sie in SQL Server Management Studio zu „Replikation“ > „Lokale Veröffentlichungen“.  

2.  Klicken Sie zuerst mit der rechten Maustaste auf die Veröffentlichung, die Sie im vorherigen Abschnitt erstellt haben, und anschließend mit der linken auf **New Subscriptions** (Neue Abonnements).  

3.  Klicken Sie im Assistenten für neue Abonnements auf **Weiter**.  

4.  Klicken Sie auf der Seite **Veröffentlichung** auf die Veröffentlichung, die Sie im vorherigen Abschnitt erstellt haben.  

5.  Klicken Sie auf der Seite **Speicherort des Verteilungs-Agents** zuerst auf **Alle Agents auf dem Verteiler SERVERNAME ausführen (Pushabonnements)** und anschließend auf **Weiter**.  

6.  Fügen Sie auf der Seite **Abonnenten** alle untergeordneten Bereitstellungsserver hinzu, indem Sie die folgenden Schritte ausführen:  

    1.  Klicken Sie zuerst auf **Abonnent hinzufügen** und anschließend auf **SQL Server-Abonnenten hinzufügen**.  

    2.  Fügen Sie alle untergeordneten Bereitstellungsserver hinzu.  

    3.  Klicken Sie für alle hinzugefügten untergeordneten Bereitstellungsserver im Feld **Abonnementdatenbank** auf die jeweilige leere MDT-Datenbank auf dem untergeordneten Bereitstellungsserver.  

    > [!NOTE]
    >  Wenn die leere MDT-Datenbank noch nicht erstellt wurde, müssen Sie im Feld **Abonnementdatenbank** die Option zum Erstellen einer neuen Datenbank auswählen.  

    > [!NOTE]
    >  Für diese Datenbank muss derselbe Name wie für die MDT-Datenbank auf dem Masterbereitstellungsserver festgelegt werden. Wenn beispielsweise für die MDT-Datenbank auf dem Masterbereitstellungsserver der Name *MDTDB* festgelegt wurde, ist es erforderlich, dass Sie eine leere Datenbank mit dem Namen *MDTDB* auf dem untergeordneten Bereitstellungsserver erstellen.  

7.  Klicken Sie auf **Weiter**.  

8.  Klicken Sie auf der Seite **Sicherheit für den Verteilungs-Agent** auf **...**, um das Dialogfeld **Sicherheit für den Verteilungs-Agent** zu öffnen.  

9. Geben Sie die Daten für das Konto an, das für den Verteilungs-Agent verwendet werden soll, und klicken Sie anschließend auf **Weiter**.  

10. Führen Sie auf der Seite **Synchronisierungszeitplan** die folgenden Schritte aus:  

    1.  Klicken Sie im Feld **Agentzeitplan** auf **<Zeitplan definieren\>**.  

    2.  Geben Sie den Zeitplan an, der zur Replikation der Datenbank zwischen dem Masterbereitstellungsserver und den untergeordneten Bereitstellungsservern verwendet werden soll, und klicken Sie anschließend auf **Weiter**.  

11. Klicken Sie auf der Seite **Initialize Subscription** (Abonnement initialisieren) auf **Weiter**.  

12. Klicken Sie auf der Seite **Aktionen des Assistenten** zuerst auf **Abonnements erstellen** und anschließend auf **Weiter**.  

13. Klicken Sie nach dem erfolgreichen Abschluss des Assistenten zuerst auf **Fertig stellen** und anschließend auf **Schließen**.  

 Die SQL Server-Replikation ist jetzt konfiguriert, und die MDT-Datenbank wird in regelmäßigen Abständen zwischen dem Masterbereitstellungsserver und allen untergeordneten Bereitstellungsservern repliziert, die als Abonnenten der Datenbank hinzugefügt wurden.  

#### <a name="configure-customsettingsini"></a>Konfigurieren der Datei „CustomSettings.ini“  
 Nach der erfolgreichen Erstellung der LTI-Bereitstellungsinfrastruktur enthält jeder Standort einen LTI-Bereitstellungsserver mit einer replizierten Kopie  

-   der Bereitstellungsfreigabe,  

-   der MDT-Datenbank  

-   und der Windows PE-Umgebung LiteTouchPE_x86, die Windows-Bereitstellungsdienste hinzugefügt wurde.  

 Nun können Sie die Datei „CustomSettings.ini“ für die Bereitstellungsfreigabe konfigurieren, um Bereitstellungsinhalte (Bereitstellungsfreigabe und Datenbank) des lokalen Bereitstellungsservers zu verwenden. Dabei handelt es sich um den Server, der die Umgebung mit der Datei „LiteTouchPE_x86.wim“ über Windows-Bereitstellungsdienste zur Verfügung stellt.  

 Wenn die Datei „LiteTouchPE_x86.wim“ durch Windows-Bereitstellungsdienste übermittelt wird, wird ein Registrierungsschlüssel mit dem Namen des verwendeten Windows-Bereitstellungsdienste-Servers konfiguriert. Das MDT erfasst diesen Servernamen in einer Variablen (%WDSServer%), die Sie zum Konfigurieren von „CustomSettings.ini“ nutzen können.  

 **So verwenden Sie stets den lokalen LTI-Bereitstellungsserver:**  

> [!NOTE]
>  Voraussetzung für die folgenden Schritte ist, dass die Bereitstellungsfreigabe erstellt und mit „Deployment$“ als Freigabe festgelegt wurde.  

1.  Klicken Sie auf **Start**, und zeigen Sie auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

4.  Klicken Sie auf die Registerkarte **Regeln**, und ändern Sie in der Datei „CustomSettings.ini“ die folgenden Eigenschaften:  

    -   Konfigurieren Sie für jeden hinzugefügten SQL Server-Abschnitt **SQLServer** so, dass der Servername **%WDSServer%** verwendet wird. Ein Beispiel ist **SQLServer=%WDSServer%**.  

    -   Falls Sie **DeployRoot** konfigurieren, müssen Sie **DeployRoot** so konfigurieren, dass die Variable **%WDSServer%** verwendet wird. Ein Beispiel ist **DeployRoot=\\\\%WDSServer%\Deployment$**.  

5.  Klicken Sie auf **Edit BootStrap.ini** (BootStrap.ini bearbeiten).  

6.  Konfigurieren Sie „BootStrap.ini“ für die Verwendung der Eigenschaft **%WDSServer%**, indem Sie den Wert **DeployRoot** zu **DeployRoot=\\\\%WDSServer%\Deployment$** hinzufügen oder ihn ändern.  

7.  Klicken Sie zuerst auf **Datei** und anschließend auf **Speichern**, um die Änderungen an der Datei „BootStrap.ini“ zu speichern.  

8.  Klicken Sie auf **OK**.  

     Die Bereitstellungsfreigabe und die Windows PE-Umgebung „LiteTouchPE_x86.wim“ müssen aktualisiert werden.  

9. Klicken Sie im Aktionsbereich auf **Update Deployment Share** (Bereitstellungsfreigabe aktualisieren).  

     Der Assistent für das Update der Bereitstellungsfreigabe wird gestartet.  

10. Wählen Sie auf der Seite **Optionen** die gewünschten Optionen für das Update der Bereitstellungsfreigabe aus, und klicken Sie auf **Weiter**.  

11. Überprüfen Sie auf der Seite **Zusammenfassung**, ob die Details korrekt sind, und klicken Sie anschließend auf **Weiter**.  

12. Klicken Sie auf der Seite **Bestätigung** auf **Fertig stellen**.  

 Im folgenden Beispiel wird dargestellt, welche Informationen die Datei „CustomSettings.ini“ nach dem Ausführen der in diesem Abschnitt beschriebenen Schritte enthält.  

 **Beispielhafte „CustomSettings.ini“-Datei, die für eine skalierbare LTI-Bereitstellungsinfrastruktur konfiguriert wurde**  

```  
[Settings]  
Priority=CSettings,CPackages, CApps, CAdmins, CRoles, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac  

[CSettings]  
SQLServer=%WDSServer%  
Instance=  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerSettings  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CPackages]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerPackages  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CApps]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerApplications  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CAdmins]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerAdministrators  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CRoles]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerRoles  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
```  

## <a name="selecting-a-local-mdt-server-when-multiple-servers-exist"></a>Auswählen eines lokalen MDT-Servers bei Vorhandensein mehrerer Server  
 In diesem Szenario werden mehrere MDT-Server dazu verwendet, eine große Anzahl gleichzeitiger Bereitstellungen und Bereitstellungen für mehrere Standorte zu unterstützen. Bei der Initialisierung einer LTI-Bereitstellung besteht das Standardverhalten darin, einen Verbindungspfad zum MDT-Server anzufordern und auf die erforderlichen Dateien zuzugreifen, um den Bereitstellungsprozess zu starten.  

 Der Windows-Bereitstellungs-Assistent kann mit der Datei „LocalServer.xml“ ausgewählte bekannte Bereitstellungsserver für jeden Standort anzeigen.  

 Zur Verwendung der Datei „LocationServer.xml“ sind folgende Schritte erforderlich:  

-   Machen Sie sich mithilfe des Abschnitts [Grundlegendes zur Datei „LocationServer.xml“](#UnderstandingLocationServer) mit dem Zweck der Datei vertraut.  

-   Erstellen Sie mithilfe des Abschnitts [Erstellen der Datei „LocationServer.xml“](#CreateLocationServer) die Datei.  

-   Fügen Sie mithilfe des Abschnitts „Hinzufügen der Datei „LocationServer.xml“ zum Verzeichnis „Extra Files“ die Datei zum entsprechenden Verzeichnis hinzu.  

-   Aktualisieren Sie die Datei „BootStrap.ini“ mithilfe des Abschnitts [Aktualisieren der Datei „BootStrap.ini“](#UpdateBootstrap).  

-   Aktualisieren Sie die Bereitstellungsfreigabe mithilfe des Abschnitts [Aktualisieren der Bereitstellungsfreigabe](#UpdateDeploymentShare).  

 In diesen Szenario wird davon ausgegangen, dass das MDT auf einem Bereitstellungsserver konfiguriert ist.  

###  <a name="UnderstandingLocationServer"></a> Grundlegendes zur Datei „LocationServer.xml“  
 Zunächst müssen Sie verstehen, wie das MDT „LocationServer.xml“ verwendet. Während der LTI wird die Datei „BootStrap.ini“ von MDT-Skripts gelesen und verarbeitet, damit zusätzliche Informationen zur Bereitstellung erfasst werden. Dieser Vorgang findet statt, bevor eine Verbindung mit dem Bereitstellungsserver hergestellt wird. Aus diesem Grund wird die Eigenschaft **DeployRoot** häufig dazu verwendet, in der Datei „BootStrap.ini“ den Bereitstellungsserver anzugeben, mit dem eine Verbindung hergestellt werden soll.  

 Wenn die Datei „BootStrap.ini“ nicht die Eigenschaft **DeployRoot** enthält, laden MDT-Skripts eine Assistentenseite, auf der der Benutzer aufgefordert wird, einen Pfad zum Bereitstellungsserver anzugeben. Beim Initialisieren der Assistentenseite für eine **HTA-Anwendung (HTML Application)** wird von den MDT-Skripts überprüft, ob die Datei „LocationServer.xml“ vorhanden ist. Falls dies der Fall ist, werden mit dieser verfügbare Bereitstellungsserver angezeigt.  

#### <a name="understand-when-to-use-locationserverxml"></a>Verwendung von „LocationServer.xml“  
 Das MDT bietet mehrere Möglichkeiten zur Ermittlung des Servers, mit dem während einer LTI-Bereitstellung eine Verbindung hergestellt werden soll. Bei der Suche nach dem Bereitstellungsserver eignen sich je nach Szenario unterschiedliche Methoden. Es ist daher wichtig, den Einsatzbereich von „LocationServer.xml“ zu kennen.  

 Das MDT stellt mehrere Methoden bereit, um den am besten geeigneten Bereitstellungsserver automatisch zu ermitteln und zu verwenden. Diese Methoden werden in der folgenden Tabelle aufgeführt.

 |**Methode** |**Details** |  
 |-|-|  
 |**%WDSServer%** |Diese Methode wird verwendet, wenn der MDT-Server auf dem Server von Windows-Bereitstellungsdienste gehostet wird.<br /><br /> Bei der Initialisierung der LTI-Bereitstellung über Windows-Bereitstellungsdienste wird Umgebungsvariable %WDSServer% erstellt und mit dem Namen des Windows-Bereitstellungsdienste-Servers aufgefüllt.<br /><br /> Die **DeployRoot**-Variable kann mithilfe dieser Variablen automatisch eine Verbindung mit der Bereitstellungsfreigabe auf dem Windows-Bereitstellungsdienste-Server herstellen. Ein Beispiel ist:<br /><br /> **DeployRoot=\\\\%WDSServer%\Deployment$** |  
 |**Standortbasierte Automatisierung** |Das MDT kann über die Datei „BootStrap.ini“ die standortbasierte Automatisierung verwenden, um den Server zu ermitteln, auf dem die Bereitstellung erfolgen soll.<br /><br /> Mit der Eigenschaft **Standardgateway** können Sie zwischen verschiedenen Standorten unterscheiden. Für jede **Standardgateway**-Eigenschaft wird ein anderer MDT-Server festgelegt.<br /><br /> Weitere Informationen zur Verwendung der standortbasierten Automatisierung finden Sie unter „Selecting the Methods for Applying Configuration Settings (Auswählen der Methoden für das Anwenden von Konfigurationseinstellungen)“.|  

 Jeder der in der obigen Tabelle aufgeführten Ansätze stellt eine Möglichkeit bereit, die Auswahl des Bereitstellungsservers an einem festgelegten Standort für bestimmte Szenarios zu automatisieren. Diese Ansätze gelten für bestimmte Szenarios, z.B. wenn der MDT-Server auf demselben Server gehostet wird wie Windows-Bereitstellungsdienste.  

 Es gibt jedoch auch Szenarios, für die diese Ansätze nicht geeignet sind. Dies ist beispielsweise der Fall, wenn mehrere Bereitstellungsserver an einem bestimmten Standort vorhanden sind oder die Automatisierungslogik nicht angewendet werden kann (etwa dann, wenn die Granularität der Netzwerksegmentierung zur Ermittlung des Standorts zu grob ist oder der MDT-Server von Windows-Bereitstellungsdienste getrennt wird).  

 In diesen Szenarios bietet die Datei „LocationServer.xml“ eine flexible Möglichkeit zur Darstellung dieser Informationen zum Zeitpunkt der Bereitstellung, ohne dass die Servernamen und die Namen der Bereitstellungsfreigaben bekannt sein müssen.  

###  <a name="CreateLocationServer"></a> Erstellen der Datei „LocationServer.xml“  
 Wenn Sie sich während der LTI-Bereitstellung eine Liste der verfügbaren Bereitstellungsserver anzeigen lassen möchten, können Sie die Datei „LocationServer.xml“ erstellen, die Details für jeden Server enthält. Im MDT ist „LocationServer.xml“ nicht als Standarddatei vorhanden. Sie müssen diese daher mit der folgenden Anleitung erstellen.  

#### <a name="create-a-locationserverxml-file-to-support-multiple-locations"></a>Erstellen der Datei „LocationServer.xml“ zur Unterstützung mehrerer Standorte  
 Die einfachste Methode zum Erstellen und Verwenden von „LocationServer.xml“ besteht darin, die entsprechende Datei zu erstellen und dieser Einträge für jeden Bereitstellungsserver in der Umgebung hinzuzufügen (entweder an demselben Standort oder an unterschiedlichen Standorten).  

 Erstellen Sie die Datei „LocationServer.xml“, indem Sie für jeden Server einen neuen Abschnitt erstellen, und fügen Sie dann die folgenden Informationen hinzu:  

-   einen eindeutigen Bezeichner  

-   einen Namen, über den sich der Standort leicht ermitteln lässt  

-   einen UNC-Pfad zum MDT-Server für diesen Standort  

 Im Folgenden wird veranschaulicht, wie eine Beispieldatei „LocationServer.xml“ mit den oben genannten Eigenschaften zur Unterstützung mehrerer Standorte erstellt wird.  

 **Beispieldatei „LocationServer.xml“ zur Unterstützung mehrerer Standorte**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 Geben Sie unter Verwendung dieses Formats unterschiedliche Servereinträge für jeden Standort oder für Situationen an, in denen mehrere Server an einem einzigen Standort vorhanden sind, indem Sie für jeden Server an diesem Standort einen Servereintrag stellen. Dies wird im folgenden Beispiel demonstriert:   

 **Beispieldatei „LocationServer.xml“ zur Unterstützung mehrerer Server an mehreren Standorten**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ DS1, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso HQ DS2, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS02\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

#### <a name="create-a-locationserverxml-file-to-load-balance-multiple-servers-at-different-locations"></a>Erstellen der Datei „LocationServer.xml“ zum Vornehmen eines Lastenausgleichs für mehrere Server an verschiedenen Standorten  
 Geben Sie mithilfe von „LocationServer.xml“ mehrere Server pro Standorteintrag an, und nehmen Sie dann einen grundlegenden Lastenausgleich vor, damit das MDT bei der Auswahl eines Standorts automatisch einen Bereitstellungsserver aus der Liste der verfügbaren Server auswählt. Zur Bereitstellung dieser Funktion kann in der Datei „LocationServer.xml“ eine Gewichtungsmetrik angegeben werden.  

 Die folgende Beispieldatei „LocationServer.xml“ ist für mehrere Server an verschiedenen Standorten konfiguriert.  

 **Beispieldatei „LocationServer.xml“ für unterschiedliche Speicherorte**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <Server1>\\STLDS01\Deployment$</Server1>  
        <Server2>\\STLDS02\Deployment$</Server2>  
        <Server3>\\STLDS03\Deployment$</Server3>  
        <Server weight=”1”>\\STLDS01\Deployment$</Server>  
        <Server weight=”2”>\\STLDS02\Deployment$</Server>  
        <Server weight=”4”>\\STLDS03\Deployment$</Server>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 Die Gewichtungsmetrik geben Sie mit dem Tag <server weight\> an, das vom MDT bei der Auswahl des Servers verwendet wird. Die Wahrscheinlichkeit für die Auswahl eines bestimmten Servers wird wie folgt berechnet:  

 **Servergewichtung/Summe aller Servergewichtungen**  

 Im obigen Beispiel werden für die drei Server am Standort „Contoso HQ“ 1, 2 und 4 als Servergewichtungen festgelegt. Die Wahrscheinlichkeit für die Auswahl eines Servers mit der Gewichtung 2 beträgt also 2/7. Wenn Sie daher das Gewichtungssystem verwenden möchten, müssen Sie die Kapazität der verfügbaren Server an jedem Standort festlegen, und jedem Server je nach Serverkapazität in Bezug auf alle anderen Server eine Gewichtung zuordnen.  

### <a name="adding-the-locationserverxml-file-to-the-extra-files-directory"></a>Hinzufügen der Datei „LocationServer.xml“ zum Verzeichnis „Extra Files“ (Zusätzliche Dateien)  
 Nachdem Sie die Datei „LocationServer.xml“ erstellt haben, fügen Sie sie den Windows PE-Startimages „LiteTouch_x86“ und „LiteTouch_x64“ im Ordner ***X:\\Deploy\Control*** hinzu. Fügen Sie diesen Windows PE-Images mithilfe der Bereitstellungsworkbench weitere Dateien und Ordner hinzu, indem Sie ein weiteres Verzeichnis angeben, in dem die Eigenschaften der Bereitstellungsfreigabe hinzugefügt werden.  

 **So fügen Sie der Bereitstellungsfreigabe die Datei „LocationServer.xml“ hinzu**  

1.  Erstellen Sie im Stammordner der Bereitstellungsfreigabe einen Ordner namens *Extra Files* (Zusätzliche Dateien), z.B. „D:\Production Deployment Share\Extra Files“.  

2.  Erstellen Sie eine Ordnerstruktur im Ordner „Extra Files“ (Zusätzliche Dateien), die den Windows PE-Standort abbildet, an dem sich die zusätzliche Datei befinden sollte.  

     Die Datei „LocationServer.xml“ muss sich in Windows PE beispielsweise im Ordner „\Deploy\Control“ befinden. Daher müssen Sie dieselbe Ordnerstruktur unter „Extra Files“ (zusätzliche Dateien) erstellen, z.B. „D:\Production Deployment Share\Extra Files\Deploy\Control“.  

3.  Kopieren Sie „LocationServer.xml“ in den Ordner „*Bereitstellungsfreigabe*\Extra Files\Deploy\Control“, wobei *Bereitstellungsfreigabe* dem vollqualifizierten Pfad zum Stammordner der Bereitstellungsfreigabe entspricht.  

4.  Klicken Sie auf **Start**, und zeigen Sie auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

5.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

6.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

7.  Führen Sie im Dialogfeld ***BereitstellungsfreigabeProperties*** (wobei „Bereitstellungsfreigabe“ dem Namen der Bereitstellungsfreigabe entspricht) die folgenden Schritte aus:  

    1.  Klicken Sie auf die Registerkarte **Windows PE platform Settings** (Einstellungen der Windows PE-Plattform), wobei *platform* (Plattform) der Architektur des Windows PE-Images entspricht, das konfiguriert werden soll.  

    2.  Geben Sie im Bereich **Windows PE Customizations** (Anpassungen für Windows PE) im Feld **Extra directory to add** (Zusätzliches Verzeichnis, das hinzugefügt werden soll) den vollqualifizierten ***Pfad*** zum Ordner „Extra Files“ ein, z.B. „D:\Production Deployment Share\Extra Files“, und klicken Sie dann auf **OK**.  

###  <a name="UpdateBootstrap"></a> Aktualisieren der Datei „ BootStrap.ini“  
 Bei der Erstellung einer Bereitstellungsfreigabe mithilfe der Bereitstellungsworkbench, wird automatisch eine **DeployRoot**-Eigenschaft erstellt und in der Datei „Bootstrap.ini“ aufgefüllt. Da die **DeployRoot**-Eigenschaft mit der Datei „LocationServer.xml“ aufgefüllt wird, müssen Sie diesen Wert aus der Datei „Bootstrap.ini“ entfernen.  

 **So entfernen Sie die Eigenschaft „DeployRoot“ aus der Datei „Bootstrap.ini“**  

1.  Klicken Sie auf **Start**, und zeigen Sie auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

4.  Klicken Sie im Dialogfeld ***BereitstellungsfreigabeProperties*** auf die Registerkarte **Regeln** und dann auf **Edit BootStrap.ini** („BootStrap.ini“ bearbeiten). *Bereitstellungsfreigabe* entspricht dabei dem Namen der Bereitstellungsfreigabe.  

5.  Entfernen Sie den Wert **DeployRoot**, z.B. **DeployRoot=\\\Server\Deployment$**.  

6.  Klicken Sie zuerst auf **Datei** und anschließend auf **Speichern**, um die Änderungen an der Datei „BootStrap.ini“ zu speichern.  

7.  Klicken Sie auf **OK**, um die Änderungen zu übernehmen.  

###  <a name="UpdateDeploymentShare"></a> Aktualisieren der Bereitstellungsfreigabe  
 Die Bereitstellungsfreigabe muss anschließend aktualisiert werden, um eine neue LiteTouch_x86- und LiteTouch_x64-Startumgebung zu generieren, die „LocationServer.xml“ und die aktualisierte Datei „Bootstrap.ini“ enthält.  

 **So aktualisieren die Bereitstellungsfreigabe**  

1.  Klicken Sie auf **Start**, und zeigen Sie auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Aktionsbereich auf **Update Deployment Share** (Bereitstellungsfreigabe aktualisieren).  

     Der Assistent für das Update der Bereitstellungsfreigabe wird gestartet.  

4.  Wählen Sie auf der Seite **Optionen** die gewünschten Optionen für das Update der Bereitstellungsfreigabe aus, und klicken Sie auf **Weiter**.  

5.  Überprüfen Sie auf der Seite **Zusammenfassung**, ob die Details korrekt sind, und klicken Sie anschließend auf **Weiter**.  

6.  Klicken Sie auf der Seite **Bestätigung** auf **Fertig stellen**.  

> [!NOTE]
>  Wenn der Updatevorgang abgeschlossen ist, können Sie die neuen Windows PE-Umgebungen LiteTouch_x86 und LiteTouch_x64 wieder zu den Windows-Bereitstellungsdiensten hinzufügen oder diese auf Bootmedien brennen, um sie während der Bereitstellung zu verwenden.  

## <a name="replacing-an-existing-computer-with-a-new-computer-using-lite-touch-installation"></a>Ersetzen eines vorhandenen Computers durch einen neuen Computer mithilfe der Lite-Touch-Installation  
 Sie können MDT für die Bereitstellung eines Images auf einem neuen Computer verwenden, der als Ersatz für einen vorhandenen Computer in der Unternehmensarchitektur dient. Dieser Fall kann auftreten, wenn für ein Betriebssystem ein Upgrade auf ein anderes Betriebssystem ausgeführt wird (für ein neues Betriebssystem könnte neue Hardware erforderlich sein), oder wenn die Organisation neuere, schnellere Computer für vorhandene Anwendungen benötigt.  

 Beim Ersetzen eines vorhandenen Computers durch einen neuen Computer empfiehlt Microsoft, sämtliche Einstellungen zu berücksichtigen, die von einem Computer zum anderen migriert werden, wie z.B. Benutzerkonten und Benutzerstatusdaten. Darüber hinaus ist es wichtig, für den Fall einer fehlgeschlagenen Migration eine Wiederherstellungslösung zu erstellen.  

 In dieser Beispielbereitstellung wird der vorhandene Computer (WDG-EXIST-01) in der Domäne CORP durch einen neuen Computer (WDG-NEW-02) ersetzt, indem Benutzerstatusdaten des Computers WDG-EXIST-01 erfasst und in einer Netzwerkfreigabe gespeichert werden. Anschließend wird ein vorhandenes Image für WDG-NEW-02 bereitgestellt. Zum Schluss werden die erfassten Benutzerstatusdaten auf dem Computer WDG-NEW-02 wiederhergestellt. Die Bereitstellung erfolgt über einen Bereitstellungsserver (WDG-MDT-01).  

 Verwenden Sie in MDT die Vorlage „Tasksequenz zum Ersetzen des Standardclients“, um eine Tasksequenz für alle erforderlichen Bereitstellungstasks zu erstellen.  

 In dieser Demonstration wird Folgendes vorausgesetzt:  

-   MDT wurde auf dem Bereitstellungsserver (WDG-MDG-01) installiert.  

-   Die Bereitstellungsfreigabe wurde bereits erstellt und aufgefüllt, einschließlich Betriebssystemimages, Anwendungen und Gerätetreiber.  

-   Ein Image eines Referenzcomputers wurde bereits erfasst und wird auf dem neuen Computer (WDG-NEW-02) bereitgestellt.  

-   Ein freigegebener Netzwerkordner (UserStateCapture$) wurde erstellt und auf dem Bereitstellungsserver (WDG-MDT-01) mit den entsprechenden Freigabeberechtigungen freigegeben.  

 Vor Beginn dieses Beispiels sollte eine Bereitstellungsfreigabe vorhanden sein. Weitere Informationen zur Erstellung einer Bereitstellungsfreigabe finden Sie im Abschnitt „Verwalten von Bereitstellungsfreigaben in der Deployment Workbench“ des MDT-Artikels *Verwenden des Microsoft Deployment Toolkits*.  

### <a name="step-1-create-a-task-sequence-to-capture-the-user-state"></a>Schritt 1: Erstellen einer Tasksequenz zur Erfassung des Benutzerstatus  
 Erstellen Sie mit dem Assistenten für neue Tasksequenzen im Knoten „Tasksequenzen“ der Deployment Workbench MDT-Tasksequenzen. Wählen Sie für die Durchführung des ersten Teils des Bereitstellungsszenarios zum Ersetzen eines Computers (in dem der Benutzerstatus auf dem vorhandenen Computer erfasst wird) im Assistenten für neue Tasksequenzen die Vorlage „Tasksequenz zum Ersetzen des Standardclients“ aus.  

 **So erstellen Sie in dem Bereitstellungsszenario zum Ersetzen eines Computers eine Tasksequenz zum Erfassen des Benutzerstatus**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe* > Tasksequenzen. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Bereich „Aktionen“ auf **Neue Tasksequenz**.  

     Der Assistent für neue Tasksequenzen wird gestartet.  

4.  Führen Sie die Assistenten für neue Tasksequenzen mit den folgenden Informationen aus. Übernehmen Sie die Standardwerte, sofern dies nicht anders angegeben ist.  

    |**Auf dieser Assistentenseite** |**Vorgehensweise** |  
    |-|-|  
    |**Allgemeine Einstellungen** |1.  Geben Sie unter **Tasksequenz-ID** Folgendes ein: **VISTA_EXIST**.<br />2.  Geben Sie unter **Tasksequenzname** Folgendes ein: **Szenario zum Ersetzen eines Computers auf vorhandenem Computer ausführen**.<br />3.  Klicken Sie auf **Weiter**.|  
    |**Vorlage auswählen** |Unter **Folgende Vorlagen für Tasksequenzen sind verfügbar**. **Wählen Sie die Vorlage aus, die Sie als Ausgangspunkt verwenden möchten**. Wählen Sie **Tasksequenz zum Ersetzen eines Standardclients** aus, und klicken Sie anschließend auf **Weiter**.|  
    |**Zusammenfassung** |Überprüfen Sie, ob die Konfigurationsdetails korrekt sind, und klicken Sie anschließend auf **Weiter**.|  
    |**Bestätigung** |Klicken Sie auf **Fertig stellen**.|  

 Der Assistent für neue Tasksequenzen wird beendet, und die Tasksequenz **VISTA_EXIST** wird zur Liste der Tasksequenzen hinzugefügt.  

### <a name="step-2-create-a-task-sequence-to-deploy-operating-system-and-restore-the-user-state"></a>Schritt 2: Erstellen einer Tasksequenz für die Bereitstellung eines Betriebssystems und zur Wiederherstellung des Benutzerstatus  
 Erstellen Sie mit dem Assistenten für neue Tasksequenzen im Knoten „Tasksequenzen“ der Deployment Workbench MDT-Tasksequenzen. Wählen Sie für die Durchführung des zweiten Teils des Bereitstellungsszenarios zum Ersetzen eines Computers (in dem das Betriebssystem bereitgestellt und anschließend der Benutzerstatus auf dem vorhandenen Computer wiederhergestellt wird) im Assistenten für neue Tasksequenzen die Vorlage „Tasksequenz für Standardclient“ aus.  

 **So erstellen Sie in dem Bereitstellungsszenario zum Ersetzen eines Computers eine Tasksequenz für die Bereitstellung des Benutzerstatus**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe* > Tasksequenzen. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Bereich „Aktionen“ auf **Neue Tasksequenz**.  

     Der Assistent für neue Tasksequenzen wird gestartet.  

4.  Führen Sie die Assistenten für neue Tasksequenzen mit den folgenden Informationen aus. Übernehmen Sie die Standardwerte, sofern dies nicht anders angegeben ist.  

    |**Auf dieser Assistentenseite**|**Vorgehensweise**|  
    |-|-|  
    |**Allgemeine Einstellungen**|1.  Geben Sie unter **Tasksequenz-ID** Folgendes ein: **VISTA_NEW**.<br />2.  Geben Sie unter **Tasksequenzname** Folgendes ein: **Szenario zum Ersetzen eines Computers auf neuem Computer ausführen**.<br />3.  Klicken Sie auf **Weiter**.|  
    |**Vorlage auswählen**|Unter **Folgende Vorlagen für Tasksequenzen sind verfügbar**. **Wählen Sie die Vorlage aus, die Sie als Ausgangspunkt verwenden möchten**. Wählen Sie **Tasksequenz für Standardclient** aus, und klicken Sie anschließend auf **Weiter**.|  
    |**Betriebssystem auswählen**|Unter **Folgende Betriebssystemimages können mit dieser Tasksequenz bereitgestellt werden**. Wählen Sie ein Betriebssystem aus, das verwendet werden soll. Wählen Sie ***captured_vista_image*** aus (hierbei steht *captured_vista_image* für das erfasste Image des Referenzcomputers, das zum Knoten „Betriebssystem“ in der Deployment Workbench hinzugefügt wird), und klicken Sie auf *Weiter*.|  
    |**Produktschlüssel angeben**|Wählen Sie **Zu diesem Zeitpunkt keinen Produktschlüssel angeben** aus, und klicken Sie anschließend auf **Weiter**.|  
    |Betriebssystemeinstellungen|1.  Geben Sie unter **Vollständiger Name** Folgendes ein: **Woodgrove-Mitarbeiter**.<br />2.  Geben Sie unter **Organisation** Folgendes ein: **Woodgrove-Bank**.<br />3.  Geben Sie unter **Internet Explorer-Homepage**  Folgendes ein :**http://www.woodgrovebank.com**.<br />4.  Klicken Sie auf **Weiter**.|  
    |**Administratorkennwort**|Geben Sie unter **Administratorkennwort** und **Administratorkennwort bestätigen** **P@ssw0rd** ein, und klicken Sie anschließend auf **Fertig stellen**.|  
    |**Bestätigung**|Klicken Sie auf **Fertig stellen**.|  

 Der Assistent für neue Tasksequenzen wird beendet, und die Tasksequenz **VISTA_NEW** wird zur Liste der Tasksequenzen hinzugefügt.  

### <a name="step-3-customize-the-mdt-configuration-files"></a>Schritt 3: Anpassen der MDT-Konfigurationsdateien  
 Wenn die MDT-Tasksequenz erstellt wurde, können Sie die MDT-Konfigurationsdateien anpassen, die die Konfigurationseinstellungen für die Erfassung von Informationen zum Benutzerstatus bereitstellen. Passen Sie insbesondere die Datei „CustomSettings.ini“ an, indem Sie die Datei in den Eigenschaften der Bereitstellungsfreigabe ändern, die zuvor im Bereitstellungsprozess erstellt wurde. In einem späteren Schritt wird die Bereitstellungsfreigabe aktualisiert, um sicherzustellen, dass die Konfigurationsdatei in der Bereitstellungsfreigabe aktualisiert wird.  

 **So passen Sie die MDT-Konfigurationsdateien für die Erfassung von Informationen zum Benutzerstatus an**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

     Das Dialogfeld **Eigenschaften** wird angezeigt.  

4.  Klicken Sie im Dialogfeld **Eigenschaften** auf die Registerkarte **Regeln**.  

5.  Ändern Sie auf der Registerkarte **Regeln** die Datei „CustomSettings.ini“ so, dass die erforderlichen Änderungen wie im Beispiel dargestellt berücksichtigt werden. Nehmen Sie alle weiteren für die Umgebung erforderlichen Änderungen vor.  

     **Benutzerdefinierte Datei „CustomSettings.ini“**  

    ```  
    [Settings]  
    Priority=Default  
    Properties=MyCustomProperty  

    [Default]  
    OSInstall=Y  

    UDShare=\\WDG-MDT-01\UserStateCapture$  
    UDDir=%OSDCOMPUTERNAME%  
    UserDataLocation=NETWORK  
    SkipCapture=NO  
    SkipAdminPassword=YES  
    SkipProductKey=YES  

    ```  

6.  Klicken Sie im Dialogfeld **Eigenschaften** auf **OK**.  

7.  Schließen Sie alle geöffneten Fenster und Dialogfelder.  

### <a name="step-4-configure-the-windows-pe-options-for-the-deployment-share"></a>Schritt 4: Konfigurieren der Windows PE-Optionen für die Bereitstellungsfreigabe  
 Konfigurieren Sie im Knoten „Bereitstellungsfreigaben“ in der Deployment Workbench die Windows PE-Optionen für die Bereitstellungsfreigabe.  

> [!NOTE]
>  Wenn die Gerätetreiber für den vorhandenen Computer (WDG-EXIST-01) und den neuen Computer (WDG-NEW-01) in Windows Vista enthalten sind, können Sie diesen Schritt überspringen und mit dem folgenden Schritt fortfahren.  

 **So konfigurieren Sie die Windows PE-Optionen für die Bereitstellungsfreigabe**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

     Das Dialogfeld **Eigenschaften** wird angezeigt.  

4.  Wählen Sie im Dialogfeld **Eigenschaften** auf der Registerkarte **Komponenten der *Windows PE*-Plattform** (wobei *Plattform* für die Architektur des zu konfigurierenden Windows PE-Images steht) im **Auswahlprofil** die Option ***Gerätetreiber*** aus (dabei steht *Gerätetreiber* für den Namen des Auswahlprofils für den Gerätetreiber), und klicken Sie anschließend auf **OK**.  

### <a name="step-5-update-the-deployment-share"></a>Schritt 5: Aktualisieren der Bereitstellungsfreigabe  
 Nach dem Konfigurieren der Windows PE-Optionen für die Bereitstellungsfreigabe können Sie die Bereitstellungsfreigabe aktualisieren. Durch ein Update der Bereitstellungsfreigabe werden sämtliche MDT-Konfigurationsdateien aktualisiert. Darüber hinaus wird eine benutzerdefinierte Version von Windows PE generiert. Mit der benutzerdefinierten Version von Windows PE wird der Referenzcomputer gestartet und der LTI-Bereitstellungsprozess initiiert.  

 **So aktualisieren Sie die Bereitstellungsfreigabe in der Deployment Workbench**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Bereich „Aktionen“ auf **Bereitstellungsfreigabe aktualisieren**.  

     Der Assistent für das Update der Bereitstellungsfreigabe wird gestartet.  

4.  Wählen Sie auf der Seite **Optionen** die gewünschten Optionen für das Update der Bereitstellungsfreigabe aus, und klicken Sie auf **Weiter**.  

5.  Überprüfen Sie auf der Seite **Zusammenfassung**, ob die Details korrekt sind, und klicken Sie anschließend auf **Weiter**.  

6.  Klicken Sie auf der Seite **Bestätigung** auf **Fertig stellen**.  

 Die Deployment Workbench beginnt mit das Update der Bereitstellungsfreigabe. Die Deployment Workbench erstellt die Dateien „LiteTouchPE_x86.iso“ und „LiteTouchPE_x86.wim“ (für 32-Bit-Zielcomputer) oder die Dateien „LiteTouchPE_x64.iso“ und „LiteTouchPE_x64.wim“ (für 64-Bit-Zielcomputer) in dem Ordner „*Bereitstellungsfreigabe*\Boot“ (dabei steht *Bereitstellungsfreigabe* für den freigegebenen Ordner, der als Bereitstellungsfreigabe verwendet wird).  

### <a name="step-6-create-the-lti-bootable-media"></a>Schritt 6: Erstellen der über LTI startbaren Medien  
 Geben Sie eine Methode an, mit der der Computer mit der benutzerdefinierten Version von Windows PE gestartet werden soll, die beim Update der Bereitstellungsfreigabe erstellt wurde. Die Deployment Workbench erstellt die Dateien „LiteTouchPE_x86.iso“ und „LiteTouchPE_x86.wim“ (für 32-Bit-Zielcomputer) oder die Dateien „LiteTouchPE_x64.iso“ und „LiteTouchPE_x64.wim“ (für 64-Bit-Zielcomputer) in dem Ordner „*Bereitstellungsfreigabe*\Boot“ (dabei steht *Bereitstellungsfreigabe* für den freigegebenen Ordner, der als Bereitstellungsfreigabe verwendet wird). Erstellen Sie die entsprechenden über LTI startbaren Medien aus einem dieser Images.  

 **So erstellen Sie über LTI startbare Medien**  

1.  Navigieren Sie in Windows Explorer zum Ordner „*Bereitstellungsfreigabe*\Boot“ (dabei steht *Bereitstellungsfreigabe* für den freigegebenen Ordner, der als Bereitstellungsfreigabe verwendet wird).  

2.  Führen Sie basierend auf dem Computertyp des vorhandenen Computers (WDG-EXIST-01) und des neuen Computers (WDG-NEW-02) einen der folgenden Tasks aus:  

    -   Wenn es sich bei dem Referenzcomputer um einen physischen Computer handelt, erstellen Sie eine CD oder eine DVD der ISO-Datei.  

    -   Wenn es sich bei dem Referenzcomputer um einen virtuellen Computer handelt, starten Sie den virtuellen Computer direkt von der ISO-Datei oder von einer CD oder DVD der ISO-Datei.  

### <a name="step-7-start-the-existing-computer-with-the-lti-bootable-media"></a>Schritt 7: Starten des vorhandenen Computers mit den über LTI startbaren Medien  
 Starten Sie den vorhandenen Computer (WDG-EXIST-01) mit den über LTI startbaren Medien, die zuvor im Prozess erstellt wurden. Mit dieser CD wird Windows PE auf dem vorhandenen Computer gestartet und der MDT-Bereitstellungsprozess initiiert. Am Ende des MDT-Bereitstellungsprozesses werden die Informationen zur Migration des Benutzerstatus in dem freigegebenen Ordner „UserStateCapture$“ gespeichert.  

> [!NOTE]
>  Sie können den MDT-Prozess auch initiieren, indem Sie den Zielcomputer über die Windows-Bereitstellungsdienste starten. Weitere Informationen finden Sie im Abschnitt „Vorbereiten der Windows-Bereitstellungsdienste“ des MDT-Artikels *Verwenden des Microsoft Deployment Toolkits*.  

 **So starten Sie den vorhandenen Computer mit den über LTI startbaren Medien**  

1.  Starten Sie WDG-EXIST-01 mit den über LTI startbaren Medien, die zuvor im Prozess erstellt wurden.  

     Zunächst wird Windows PE und anschließend der Windows-Bereitstellungs-Assistent gestartet.  

2.  Führen Sie den Windows-Bereitstellungs-Assistenten mit den folgenden Informationen aus. Übernehmen Sie die Standardwerte, sofern dies nicht anders angegeben ist.  

    |**Auf dieser Assistentenseite**|**Vorgehensweise**|  
    |-|-|  
    |**Willkommen bei der Bereitstellung**|Klicken Sie auf **Bereitstellungs-Assistent ausführen**, um ein neues Betriebssystem zu installieren, und klicken Sie anschließend auf **Weiter**.|  
    |**Geben Sie Anmeldeinformationen für die Verbindung mit Netzwerkfreigaben an.**|1.  Geben Sie unter **Benutzername** Folgendes ein: **Administrator**.<br />2.  Geben Sie unter **Kennwort** Folgendes ein: **P@ssw0rd**.<br />3.  Geben Sie unter **Domäne** Folgendes ein: **CORP**.<br />4.  Klicken Sie auf **OK**.|  
    |**Wählen Sie eine Tasksequenz aus, die auf diesem Computer ausgeführt werden soll.**|Klicken Sie auf *Szenario zum Ersetzen eines Computers auf vorhandenem ausführen* und anschließend auf **Weiter**.|  
    |**Geben Sie den Speicherort für Ihre Daten und Einstellungen an.**|Klicken Sie auf **Weiter**.|  
    |**Geben Sie den Speicherort für eine vollständige Computersicherung an.**|Klicken Sie auf **Vorhandenen Computer nicht sichern**, und anschließend auf **Weiter**.|  
    |**Bereit zum Starten**|Klicken Sie auf **Starten**.|  

     Sollten Fehler oder Warnungen auftreten, finden Sie im MDT-Dokument *Referenz zur Fehlerbehebung* weitere Informationen.  

3.  Klicken Sie im Dialogfeld **Bereitstellungszusammenfassung** auf **Details**.  

     Sollten Fehler oder Warnungen auftreten, überprüfen Sie diese und zeichnen Sie sämtliche Diagnoseinformationen auf.  

4.  Klicken Sie im Dialogfeld **Bereitstellungszusammenfassung** auf **Fertig stellen**.  

 Die Informationen zur Migration des Benutzerstatus werden erfasst und im freigegebenen Netzwerkordner (UserStateCapture$) gespeichert, der zuvor im Prozess erstellt wurde.  

### <a name="step-8-start-the-new-computer-with-the-lti-bootable-media"></a>Schritt 8: Starten des neuen Computers mit den über LTI startbaren Medien  
 Starten Sie den neuen Computer (WDG-NEW-02) mit den über LTI startbaren Medien, die zuvor im Prozess erstellt wurden. Mit dieser CD wird Windows PE auf dem Referenzcomputer gestartet und der MDT-Bereitstellungsprozess initiiert. Am Ende des MDT-Bereitstellungsprozesses wird Windows Vista auf dem neuen Computer bereitgestellt, und die Informationen zur Migration des Benutzerstatus werden auf dem neuen Computer wiederhergestellt.  

> [!NOTE]
>  Sie können den MDT-Prozess auch initiieren, indem Sie den Zielcomputer über die Windows-Bereitstellungsdienste starten. Weitere Informationen finden Sie im Abschnitt „Vorbereiten der Windows-Bereitstellungsdienste“ des MDT-Artikels *Verwenden des Microsoft Deployment Toolkits*.  

 **So starten Sie den neuen Computer mit den über LTI startbaren Medien**  

1.  Starten Sie WDG-NEW-02 mit den über LTI startbaren Medien, die zuvor im Prozess erstellt wurden.  

     Zunächst wird Windows PE und anschließend der Windows-Bereitstellungs-Assistent gestartet.  

2.  Führen Sie den Windows-Bereitstellungs-Assistenten mit den folgenden Informationen aus. Übernehmen Sie die Standardwerte, sofern dies nicht anders angegeben ist.  

    |**Auf dieser Assistentenseite**|**Vorgehensweise**|  
    |--|--|
    |**Willkommen bei der Bereitstellung**|Klicken Sie auf **Bereitstellungs-Assistent ausführen, um ein neues Betriebssystem zu installieren**, und klicken Sie anschließend auf **Weiter**.|  
    |**Geben Sie Anmeldeinformationen für die Verbindung mit Netzwerkfreigaben an.**|1.  Geben Sie unter **Benutzername** Folgendes ein: **Administrator**.<br />2.  Geben Sie unter **Kennwort** Folgendes ein: **P@ssw0rd**.<br />3.  Geben Sie unter **Domäne** Folgendes ein: **CORP**.<br />4.  Klicken Sie auf **OK**.|  
    |**Wählen Sie eine Tasksequenz aus, die auf diesem Computer ausgeführt werden soll.**|Klicken Sie auf **Szenario zum Ersetzen eines Computers auf neuem Computer ausführen** und anschließend auf **Weiter**.|  
    |**Konfigurieren Sie den Computernamen**|Geben Sie unter **Computername** **WDG-NEW-02** ein, und klicken Sie anschließend auf **Weiter**.|  
    |**Fügen Sie den Computer einer Domäne oder Arbeitsgruppe hinzu**|Klicken Sie auf **Weiter**.|  
    |**Geben Sie an, ob Benutzerdaten wiederhergestellt werden sollen**|1.  Klicken Sie auf **Speicherort angeben**.<br />2.  Geben Sie unter **Speicherort** Folgendes ein: **\\\WDG-MDT-01\UserStateCapture$\WDG-EXIST-01**.<br />3.  Klicken Sie auf **Weiter**.|  
    |**Gebietsschemaauswahl**|Klicken Sie auf **Weiter**.|  
    |**Legen Sie die Zeitzone fest**|Klicken Sie auf **Weiter**.|  
    |**Geben Sie an, ob ein Image erfasst werden soll**|Klicken Sie auf **Kein Image dieses Computers erfassen** und anschließend auf **Weiter**.|  
    |**Geben Sie die BitLocker-Konfiguration an**|Klicken Sie auf **BitLocker für diesen Computer nicht aktivieren** und anschließend auf **Weiter**.|  
    |**Bereit zum Starten**|Klicken Sie auf **Starten**.|  

     Sollten Fehler oder Warnungen auftreten, finden Sie im MDT-Artikel *Referenz zur Fehlerbehebung* weitere Informationen.  

3.  Klicken Sie im Dialogfeld **Bereitstellungszusammenfassung** auf **Details**.  

     Sollten Fehler oder Warnungen auftreten, überprüfen Sie diese und zeichnen Sie sämtliche Diagnoseinformationen auf.  

4.  Klicken Sie im Dialogfeld **Bereitstellungszusammenfassung** auf **Fertig stellen**.  

 Windows Vista ist jetzt auf dem neuen Computer installiert, und die Informationen zur Migration der erfassten Benutzerstatus wurden ebenfalls wiederhergestellt.  

## <a name="integrating-custom-deployment-code-into-mdt"></a>Integrieren des benutzerdefinierten Bereitstellungscodes in MDT  
 Für ein Bereitstellungsteam ist es normal, dass es über komplexe, für die Zielumgebung spezifische Anforderungen verfügt, die von den vordefinierten Tasksequenzaktionen der Deployment Workbench oder standardmäßig von MDT-Konfigurationsdateien nicht erfüllt werden. In diesem Fall müssen Sie zur Erfüllung der Anforderungen benutzerdefinierten Code implementieren.  

 So integrieren Sie benutzerdefinierten Bereitstellungscode in MDT:  

-   Durch Auswahl einer Skriptsprache, wie im Abschnitt [Auswahl der entsprechenden Skriptsprache](#ChooseAppropLanguage) beschrieben  

-   Durch Nutzen von „ZTIUtility.vbs“, wie im Abschnitt [Grundlegendes zur Nutzung von ZTIUtility](#UnderstandLeverageZTI) beschrieben  

-   Durch die Integration eines benutzerdefinierten Bereitstellungscodes, wie im Abschnitt [Integrieren eines benutzerdefinierten Bereitstellungscodes](#IntegrateCustomDeploy) beschrieben  

 In den folgenden Abschnitten wird davon ausgegangen, dass MDT auf einem Bereitstellungsserver konfiguriert ist.  

###  <a name="ChooseAppropLanguage"></a> Auswahl der entsprechenden Skriptsprache  
 Obwohl sämtlicher Code, der unter Windows oder Windows PE ausgeführt werden kann, als Anwendungsinstallation oder über einen MDT-Tasksequenzschritt aufgerufen werden kann, empfiehlt Microsoft die Verwendung von Skripts im Format von VBS- oder WSF-Dateien.  

 Die Verwendung von WSF-Dateien bietet den Vorteil der integrierten Protokollierung sowie einige andere vordefinierte Funktionen, die bereits von den ZTI- und LTI-Prozessen verwendet werden. Diese Funktionen sind im ZTIUtility-Skript verfügbar, das mit dem MDT verteilt wird.  

 Bei einem Verweis aus einem benutzerdefinierten Skript initialisiert das ZTIUtility-Skript die MDT-Umgebung und die Setupklassen. Folgende Klassen sind verfügbar:  

-   **Protokollierung**: Diese Klasse stellt die Protokollierungsfunktion bereit, die alle MDT-Skripts verwenden. Darüber hinaus erstellt sie für jedes Skript, das während der Bereitstellung ausgeführt wird, eine einzelne Protokolldatei sowie eine konsolidierte Protokolldatei mit allen Skripts. Diese Protokolldateien werden in einem Format erstellt, das von TRACE32 gelesen werden kann. Dieses Tool ist im [System Center Configuration Manager 2007 Toolkit V2](https://www.microsoft.com/download/en/details.aspx?id=9257) verfügbar.  

-   **Umgebung**: Diese Klasse konfiguriert Umgebungsvariablen, die über die WMI- und MDT-Regelverarbeitung gesammelt werden, und lässt zu, dass direkt im Skript darauf verwiesen wird. Dadurch können Bereitstellungseigenschaften gelesen werden. Zudem kann Zugriff auf sämtliche Konfigurationsinformationen erteilt werden, die in den ZTI- und LTI-Prozessen verwendet werden.  

-   **Dienstprogramm**: Diese Klasse stellt allgemeine Dienstprogramme bereit, die in ZTI- und LTI-Skripts verwendet werden. Microsoft empfiehlt, diese Klasse bei jeder Entwicklung von benutzerdefiniertem Code zu untersuchen, um zu sehen, ob Code einfach wiederverwendet werden kann. Weitere Informationen zu einigen der in dieser Klasse bereitgestellten Funktionen finden Sie weiter unten in diesem Abschnitt.  

-   **Datenbank**: Diese Klasse führt Funktionen wie das Verbinden mit Datenbanken und das Lesen von Informationen aus Datenbanken aus. Generell wird von einem direkten Zugriff auf die Datenbankklasse abgeraten. Stattdessen sollte die Regelverarbeitung zur Durchführung einer Datenbanksuche verwendet werden.  

-   **Zeichenfolgen**. Diese Klasse führt allgemeine Verarbeitungsroutinen für Zeichenfolgen durch. Diese umfassen z.B. das Erstellen einer durch Trennzeichen getrennten Liste von Elementen, das Anzeigen eines Hexadezimalwerts, das Kürzen von Leerräumen aus einer Zeichenfolge, das rechtsbündige sowie das linksbündige Ausrichten einer Zeichenfolge, das Erzwingen eines Werts in das Zeichenfolgenformat sowie in das Arrayformat, das Generieren einer zufälligen GUID (Globally Unique Identifier) und Base64-Konvertierungen.  

-   **FileHandling**: Diese Klasse führt Funktionen wie das Normalisieren von Pfaden sowie das Kopieren, Verschieben und Löschen von Dateien und Ordnern aus.  

-   **clsRegEx**: Diese Klasse führt Funktionen mit regulären Ausdrücken aus.  

 In MDT wurde eine Reihe von Änderungen in der Skriptarchitektur implementiert, um die Microsoft Visual Basic® Scripting Edition (VBScript) des Clients stabiler und zuverlässiger zu machen. Zu diesen Änderungen zählen die folgenden:  

-   Umfangreiche Änderungen an „ZTIUtility.vbs“ (die Hauptskript-Bibliothek), einschließlich neuer APIs und verbesserter Fehlerbehandlung  

-   Ein neues Aussehen für die Gesamtstruktur der Skripts vom Typ „ZTI_*xxx*.wsf“  

 Die Gesamtstruktur der MDT-Skripts wurde ebenfalls geändert. Die meisten MDT-Skripts werden jetzt in VBScript-**Klassenobjekten** gekapselt. Die Klasse wird mit der Funktion **RunNewInstance** initialisiert und aufgerufen.  

> [!NOTE]
>  Der Großteil der vorhandenen MDT 2008 Update 1-Skripts funktioniert unverändert in MDT (selbst bei den umfangreichen Änderungen, die an „ZTIUtility.vbs“ vorgenommen wurden), da die meisten MDT-Skripts „ZTIUtility.vbs“ enthalten.  

###  <a name="UnderstandLeverageZTI"></a> Grundlegendes zur Nutzung von ZTIUtility  
 Die Datei „ZTIUtility.vbs“ enthält Objektklassen, die in Ihrem benutzerdefinierten Code genutzt werden können. Integrieren Sie benutzerdefinierten Code in MDT unter Verwendung von:  

-   Der in „ZTIUtility.vbs“ definierten Protokollierungsklasse, wie im Abschnitt [Verwenden der ZTIUtility-Protokollierungsklasse](#UseZTILogging) beschrieben  

-   Der in „ZTIUtility.vbs“ definierten Umgebungsklasse, wie im Abschnitt [Verwenden der ZTIUtility-Umgebungsklasse](#UseZTIEnvironment) beschrieben  

-   Der in „ZTIUtility.vbs“ definierten Hilfsprogrammklasse, wie im Abschnitt [Verwenden der ZTIUtility-Hilfsprogrammklasse](#UseZTIUtility) beschrieben  

####  <a name="UseZTILogging"></a> Verwenden der ZTIUtility-Protokollierungsklasse  
 Die Protokollierungsklasse in „ZTIUtiliy.vbs“ stellt einen einfachen Mechanismus bereit, mit dem benutzerdefinierter Code Statusinformationen, Warnungen und Fehler auf die gleiche Weise wie andere Skripts während einer ZTI- oder LTI-Bereitstellung protokolliert. Durch diese Standardisierung wird auch sichergestellt, dass das Dialogfeld **LTI Deployment Summary** (LTI-Bereitstellungsübersicht) den Status eines benutzerdefinierten Codes, der ausgeführt wird, ordnungsgemäß meldet.  

 Im Folgenden wird ein Beispielskript mit benutzerdefiniertem Code dargestellt, in dem die Funktionen **oLogging.CreateEntry** und **TestAndFail** für die Protokollierung unterschiedlicher Arten von Meldungen verwendet werden, und zwar abhängig von den Ergebnissen der verschiedenen Skriptaktionen.  

 **Beispielskript mit ZTIUtility-Protokollierung: „ZTI_Example.wsf“**  

```  
<job id="ZTI_Example">  
<script language="VBScript" src="ZTIUtility.vbs"/>  
<script language="VBScript">  

' //*******************************************************  
' //  
' // Copyright (c) Microsoft Corporation.  All rights reserved  
' // Microsoft Deployment Toolkit Solution Accelerator  
' // File: ZTI_Example.wsf  
' //  
' // Purpose: Example of scripting with the  
' //          Microsoft Deployment Toolkit.  
' //  
' // Usage: cscript ZTI_Example.wsf [/debug:true]  
' //  
' //*******************************************************  

Option Explicit  
RunNewInstance  

'//--------------------------------------------------------  
'// Main Class  
'//--------------------------------------------------------  
Class ZTI_Example  

'//--------------------------------------------------------  
'// Main routine  
'//--------------------------------------------------------  

Function Main()  

  Dim iRetVal  
  Dim sScriptPath  

  iRetVal = SUCCESS  

  oLogging.CreateEntry "Begin example script…", _  
    LogTypeInfo  

  ' %ServerA% is a generic variable available within  
  ' every CustomSettings.ini file.  

  sScriptPath = "\\" & oEnvironment.Item("ServerA") & _  
    "\public\products\Applications\User\Technet\USEnglish"  

  ' Validate a connection to server, net connect with  
  ' credentials if necessary.  
  iRetVal = oUtility.ValidateConnection( sScriptPath )  
  TestAndFail iRetVal, 9991, "Validate Connection to [" & _  
    sScriptPath & "]"  

  'Run Setup Program  

  iRetVal = oUtility.RunWithHeartbeat( """" & _  
    sScriptPath & "\setup.exe"" /?" )  
  TestAndFail iRetVal, 9991, "RunWithHeartbeat [" & _  
    sScriptPath & "]"  

  'Perform any cleanup from installation process  

  oShell.RegWrite "HKLM\Software\Microsoft\SomeValue", _  
    "Done with Execution of XXX.", "REG_SZ"  

  Main = iRetVal  

End Function  

End Class  

</script>  
</job>  
```  

> [!NOTE]
>  Sie können auch weiterhin Skripts verwenden, die **ZTIProcess()** mit **ProcessResults()** aufrufen. Bestimmte erweiterte Features zur Fehlerbehandlung werden dann jedoch nicht aktiviert.  

####  <a name="UseZTIEnvironment"></a> Verwenden der ZTIUtility-Umgebungsklasse  
 Die Umgebungsklasse in „ZTIUtiliy.vbs“ bietet Zugriff auf MDT-Eigenschaften sowie die Möglichkeit zum Updaten dieser Eigenschaften. Im vorangegangenen Beispiel wird das Element **oEnvironment.Item("Memory")** zum Abrufen des verfügbaren Arbeitsspeichers (RAM) verwendet; es kann auch zum Abrufen des Werts einer der im MDT-Artikel *Toolkit-Referenz* beschriebenen Eigenschaften verwendet werden.  

####  <a name="UseZTIUtility"></a> Verwenden der ZTIUtility-Hilfsprogrammklasse  
 Das Skript „ZTIUtility.vbs“ enthält eine Reihe von häufig verwendeten Hilfsprogrammen, die von jedem benutzerdefinierten Bereitstellungsskript verwendet werden können. Sie können diese Hilfsprogramme auf die gleiche Weise zu einem Skript hinzufügen wie die Klassen **oLogging** und **oEnvironment**.  

In der folgenden Tabelle sind einige nützliche Funktionen mitsamt ihrer Ausgabe enthalten. Eine vollständige Liste der Funktionen finden Sie in der Datei „ZTIUtility.vbs“.  

|**Funktion**|**Ausgabe**|  
|-|-|
|**oUtility.LocalRootPath**|Gibt den Pfad des Stammordners zurück, der im Bereitstellungsprozess auf dem Zielcomputer verwendet wird. Beispiel: C:\MININT|  
|**oUtility.BootDevice**|Gibt das Startgerät des Systems zurück. Beispiel: MULTI(0)DISK(0)RDISK(0)PARTITION(1)|  
|**oUtility.LogPath**|Gibt den Pfad zum Ordner „Protokolle“ zurück, der während der Bereitstellung verwendet wird. Beispiel: C:\MININT\SMSOSD\OSDLOGS|  
|**oUtility.StatePath**|Gibt den Pfad der aktuell konfigurierten Zustandsspeichers zurück. Beispiel: C:\MININT\StateStore|  
|**oUtility.ScriptName**|Gibt den Namen des Skripts zurück, das die Funktion aufruft. Beispiel: Z-RAMTest|  
|**oUtility.ScriptDir**|Gibt den Pfad zu dem Skript zurück, das die Funktion aufruft. Beispiel: \\\server_name\Deployment$\Scripts|  
|**oUtility.ComputerName**|Bestimmt den Computernamen, der während des Buildprozesses verwendet wird. Beispiel: computer_name|  
|**oUtility.ReadIni(file, section, item)**|Lässt zu, dass das angegebene Element aus einer INI-Datei gelesen wird|  
|**oUtility.WriteIni(file, section, item, value)**|Lässt zu, dass das angegebene Element in eine INI-Datei geschrieben wird|  
|**oUtility.Sections(file)**|Liest die Abschnitte einer INI-Datei und speichert diese zu Referenzzwecken in einem Objekt|  
|**oUtility.SectionContents(file, section)**|Liest den Inhalt der angegebenen INI-Datei und speichert diesen in einem Objekt|  
|**oUtility.RunWithHeartbeat(sCmd)**|Wenn der Befehl ausgeführt wird, werden alle 0,5 Sekunden Informationen zur Frequenzermittlung in die Protokolle geschrieben.|  
|**oUtility.FindFile**<br /><br /> **(sFilename,sFoundPath)**|Sucht im Ordner „DeployRoot“ und untergeordneten Standardordnern (einschließlich „Servicing“, „Tools“, „USMT“, „Templates“, „Scripts“ und „Control“) (Wartung, Tools, USMT, Vorlagen, Skripts, Steuerlement) nach der angegebenen Datei|  
|**oUtility.findMappedDrive(sServerUNC)**|Überprüft, ob dem angegebenen UNC-Pfad ein Laufwerk zugeordnet ist, und gibt den Laufwerkbuchstaben zurück|  
|**oUtility.ValidateConnection(sServerUNC)**|Überprüft, ob eine Verbindung mit dem angegebenen Server vorhanden ist, und versucht andernfalls, eine Verbindung zu erstellen|  
|**MapNetworkDrive**<br /><br /> **(sShare, SDomID, sDomPwd)**|Ordnet dem als Freigabe angegebenen UNC-Pfad einen Laufwerkbuchstaben zu und gibt den verwendeten Laufwerkbuchstaben zurück; gibt einen Fehler zurück, wenn der Vorgang fehlschlägt|  
|**VerifyPathExists(strPath)**|Überprüft, ob der angegebene Pfad vorhanden ist|  
|**oEnvironment.Substitute(sVal)**|Erweitert sämtliche Variablen oder Funktionen innerhalb einer Zeichenfolge|  
|**oEnvironment.Item**<br /><br /> **(sName)**|Liest oder schreibt eine Variable in einen beständigen Speicher|  
|**oEnvironment.Exists**<br /><br /> **(sName)**|Überprüft, ob die Variable vorhanden ist|  
|**oEnvironment.ListItem**<br /><br /> **(sName)**|Liest oder schreibt eine Variable vom Typ **Array** in einen beständigen Speicher|  
|**oLogging.ReportFailure**<br /><br /> **(sMessage, iError)**|Wird für die Ausführung einer strukturierten Beendigung verwendet, wenn ein nicht behebbarer Fehler auftritt|  
|**oLogging.CreateEvent**<br /><br /> **(iEventID, iType, sMessage, arrParms)**|Schreibt eine Meldung in die Protokolldatei und sendet das Ereignis an einen definierten Server|  
|**oLogging.CreateEntry**<br /><br /> **(sLogMsg, iType)**|Schreibt eine Meldung in die Protokolldatei|  
|**TestAndFail(iRc, iError, sMessage)**|Beendet das Skript mit **iError**, wenn **iRc** fehlschlägt oder auf FALSE festgelegt ist|  
|**TestAndLog(iRc , sMessage)**|Protokolliert nur dann eine Warnung, wenn **iRc** fehlschlägt oder auf FALSE festgelegt ist|  

###  <a name="IntegrateCustomDeploy"></a> Integrieren des benutzerdefinierten Bereitstellungscodes  
 Der benutzerdefinierte Bereitstellungscode kann im MDT-Prozess auf verschiedene Weise integriert werden. Unabhängig von der verwendeten Methode sollten jedoch die folgenden zwei Regeln eingehalten werden:  

-   Der Skriptname des benutzerdefinierten Bereitstellungscodes sollte immer mit dem Buchstaben Z beginnen.  

-   Der benutzerdefinierte Bereitstellungscode sollte im Ordner „Scripts“ (Skripts) in der Bereitstellungsfreigabe gespeichert werden. Beispiel: D:\Production Deployment Share\Scripts.  

 Zu den am häufigsten verwendeten Methoden für die Integration von benutzerdefiniertem Code, durch die zudem eine konsistente Protokollierung sichergestellt wird, zählen die folgenden:  

-   Bereitstellung des Codes als MDT-Anwendung  

-   Starten des Codes als Befehl der MDT-Tasksequenz  

-   Starten des Codes als Benutzerexitskript  

#### <a name="deploy-custom-code-as-an-mdt-application"></a>Bereitstellen des benutzerdefinierten Codes als MDT-Anwendung  
 Benutzerdefinierter Bereitstellungscode kann in die Deployment Workbench importiert und wie jede andere Anwendung verwaltet werden.  

 **So erstellen Sie eine neue Anwendung zum Ausführen von benutzerdefiniertem Code**  

1.  Kopieren Sie den benutzerdefinierten Bereitstellungscode in den Ordner „*Bereitstellungsfreigabe*\Scripts“ (dabei steht *Bereitstellungsfreigabe* für den vollständig qualifizierten Pfad zur Bereitstellungsfreigabe).  

2.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

3.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu „Deployment Shares/*Bereitstellungsfreigabe*/Applications“ (dabei steht *Bereitstellungsfreigabe* für den Namen der zu konfigurierenden Bereitstellungsfreigabe).  

4.  Klicken Sie im Bereich „Aktionen“ auf **Neue Anwendung**.  

     Der Assistent für neue Anwendungen wird gestartet.  

5.  Führen Sie den Assistenten für neue Anwendungen mit den folgenden Informationen aus. Übernehmen Sie die Standardwerte, sofern dies nicht anders angegeben ist.  

    |**Auf dieser Assistentenseite**|**Vorgehensweise**|  
    |-|-|  
    |**Anwendungstyp**|Klicken Sie auf **Application without source files or elsewhere on the network** (Anwendung ohne Quelldateien oder an anderer Stelle im Netzwerk) und anschließend auf **Weiter**.|  
    |**Details**|Füllen Sie diese Seite basierend auf den Informationen aus der Anwendung aus, und klicken Sie anschließend auf **Weiter**.|  
    |**Befehlsdetails**|1.  Geben Sie **cscript.exe %SCRIPTROOT%\Benutzerdefinierter_Code** in das Feld **Befehlszeile** ein (dabei steht *Benutzerdefinierter_Code* für den Namen des entwickelten benutzerdefinierten Codes).<br />2.  Geben Sie **working_directory** in das Feld ***Arbeitsverzeichnis*** ein (dabei steht „working_directory“ für den Namen des Arbeitsverzeichnisses des benutzerdefinierten Codes. Dies ist in der Regel der gleiche Ordner, der auch im Feld **Befehlszeile** angegeben ist).<br />3.  Klicken Sie auf **Weiter**.|  
    |**Zusammenfassung**|Überprüfen Sie, ob die Konfigurationseinstellungen korrekt sind, und klicken Sie anschließend auf **Weiter**.|  
    |**Bestätigung**|Klicken Sie auf **Fertig stellen**.|  

 Die Anwendung wird in der Deployment Workbench im Knoten „Anwendungen“ angezeigt.  

#### <a name="add-the-custom-code-as-a-task-sequence-step"></a>Hinzufügen des benutzerdefinierten Codes als Tasksequenzschritt  
 Benutzerdefinierter Bereitstellungscode kann direkt von einem Punkt in einer Tasksequenz aufgerufen werden. So erhalten Sie Zugriff auf die üblichen Tasksequenzregeln und -optionen.  

 **So fügen Sie den benutzerdefinierten Bereitstellungscode zu einer vorhandenen Tasksequenz hinzu**  

1.  Kopieren Sie den benutzerdefinierten Bereitstellungscode in den Ordner „*Bereitstellungsfreigabe*\Scripts“ (dabei steht *Bereitstellungsfreigabe* für den vollständig qualifizierten Pfad zur Bereitstellungsfreigabe).  

2.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

3.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu „Deployment Workbench > Deployment Shares > *Bereitstellungsfreigabe/Task Sequences*“ (dabei steht *Bereitstellungsfreigabe* für den Namen der zu konfigurierenden Bereitstellungsfreigabe).  

4.  Klicken Sie im Bereich „Details“ auf ***Tasksequenz*** (dabei steht *Tasksequenz* für den Namen der Tasksequenz, die den benutzerdefinierten Code ausführt).  

5.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

6.  Klicken Sie im Dialogfeld ***Tasksequenzeigenschaften*** auf die Registerkarte **Tasksequenz**.  

7.  Navigieren Sie in der Konsolenstruktur zu *Gruppe* (dabei steht *Gruppe* für die Gruppe, die zum Tasksequenzschritt hinzugefügt werden soll).  

8.  Klicken Sie auf **Hinzufügen**, **Allgemein** und anschließend auf **Befehlszeile ausführen**.  

9. Klicken Sie in der Konsolenstruktur auf **Befehlszeile ausführen** und anschließend auf die Registerkarte **Eigenschaften**.  

10. Geben Sie **name** in das Feld ***Name*** ein (dabei steht *name* für einen beschreibenden Namen des benutzerdefinierten Codes).  

11. Geben Sie auf der Registerkarte **Eigenschaften** **command_line** in das Feld ***Befehlszeile*** ein (dabei steht *command_line* für den Befehl zur Ausführung des benutzerdefinierten Codes; Beispiel: **cscript.exe %SCRIPTROOT%\CustomCode.vbs**).  

12. Geben Sie in das Feld **Starten in** ***Pfad*** ein (dabei steht *Pfad* für den vollständig qualifizierten Pfad zu dem Arbeitsverzeichnis des benutzerdefinierten Codes; dieser Pfad ist in der Regel mit dem im Feld **Befehlszeile** angegebenen Pfad identisch), und klicken Sie anschließend auf **OK**.  

 Der neu erstellte Tasksequenzschritt wird in der Liste der Tasksequenzschritte angezeigt.  

#### <a name="run-custom-code-as-a-user-exit-script"></a>Ausführen des benutzerdefinierten Codes als Benutzerexitskript  
 Der benutzerdefinierte Code kann auch als Benutzerexitskript aus „CustomSettings.ini“ unter Verwendung der Anweisung **UserExit** ausgeführt werden. Dadurch wird ein Mechanismus bereitgestellt, mit dem Informationen in den Prozess zur Regelüberprüfung in „CustomSettings.ini“ übergeben werden. Darüber hinaus wird ein dynamisches Update für MDT-Eigenschaften zur Verfügung gestellt.  

 Weitere Informationen zu Benutzerexitskripts und der Anweisung **UserExit** finden Sie im Abschnitt „Benutzerexitskripts in der Datei „CustomSettings.ini“ des MDT-Artikels *Verwenden des Microsoft Deployment Toolkits*.  

## <a name="installing-device-drivers-using-various-installation-methods"></a>Installieren von Gerätetreibern mithilfe verschiedener Installationsmethoden  
 In diesem Szenario stellen Sie mithilfe von MDT ein Betriebssystem für verschiedene Hardwaretypen bereit. Im Rahmen des Bereitstellungsprozesses identifizieren und installieren Sie Gerätetreiber, damit die einzelnen Hardwaretypen ordnungsgemäß funktionieren. Es gibt zwei Haupttypen von Gerätetreibern. Diese beiden Typen müssen während des Bereitstellungsprozesses unterschiedlich behandelt werden:  

-   Gerätetreiber mit einer INF-Datei, die für den Import des Gerätetreibers in die Deployment Workbench verwendet werden können  

-   Gerätetreiber, die als Anwendung verpackt sind und als Anwendung installiert werden müssen  

 Mit dem MDT können Sie für die Betriebssystembereitstellung beide Treibertypen verwenden.  

 Installieren der Gerätetreiber durch:  

-   Bestimmung der Methoden für die Installation der einzelnen Gerätetreiber, wie im Abschnitt [Bestimmen der Methode für die Installation eines Gerätetreibers](#WhichMethodtoInstallDriver) beschrieben  

-   Verwendung der Methode für Standardtreiber, wie im Abschnitt [Installieren von Gerätetreibern mit der Methode für Standardtreiber](#InstallOutofBoxDrivers) beschrieben  

-   Installation der Gerätetreiber als Anwendungen, wie im Abschnitt [Installieren von Gerätetreibern als Anwendungen](#InstallDriversasApplications) beschrieben  

 In diesem Szenario wird davon ausgegangen, dass das MDT auf einem Bereitstellungsserver ausgeführt wird.  

###  <a name="WhichMethodtoInstallDriver"></a> Bestimmen der Methode für die Installation eines Gerätetreibers  
 Hardwarehersteller veröffentlichen Gerätetreiber in einer von zwei Formen:  

-   Als Paket, das Sie extrahieren können und das INF-Dateien enthält, die für den Import des Treibers in die Deployment Workbench verwendet werden  

-   Als Anwendung, die Sie unter Verwendung herkömmlicher Prozesse für die Anwendungsinstallation installieren müssen  

 Gerätetreiberpakete, die für den Zugriff auf INF-Dateien extrahiert werden können, können die automatische MDT-Treibererkennung und den -Installationsprozess verwenden, indem sie zunächst den Treiber in den Knoten „Standardtreiber“ der Deployment Workbench importieren.  

 Gerätetreiberpakete, die nicht für die Isolation von INF-Dateien oder solcher Dateien extrahiert werden können, die nicht ordnungsgemäß funktionieren, wenn sie nicht vorher mit einem Anwendungsinstallationsprogramm wie einer MSI-Datei oder der Datei „Setup.exe“ installiert worden sind, können das Feature „MDT-Anwendung installieren“ verwenden und den Gerätetreiber wie eine normale Anwendung während des Bereitstellungsprozesses installieren.  

###  <a name="InstallOutofBoxDrivers"></a> Installieren von Gerätetreibern mit der Methode für Standardtreiber  
 Sie können Gerätetreiberpakete, die eine INF-Datei enthalten, in die Deployment Workbench importieren und diese automatisch im Rahmen des Bereitstellungsprozesses installieren. Zur Implementierung dieser Bereitstellungsart für Gerätetreiber müssen Sie zunächst den Gerätetreiber zur Deployment Workbench hinzufügen.  

 **So fügen Sie den Gerätetreiber zur Deployment Workbench hinzu**  

1.  Laden Sie den Gerätetreiber herunter, der für die bereitzustellenden Hardwaretypen erforderlich ist, und extrahieren Sie das Gerätetreiberpaket in ein temporäres Verzeichnis.  

2.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

3.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu „Deployment Workbench > Deployment Shares > *Bereitstellungsfreigabe* > Out-of-Box Drivers“ (dabei steht *Bereitstellungsfreigabe* für den Namen der zu u konfigurierenden Bereitstellungsfreigabe).  

4.  Klicken Sie im Bereich „Aktionen“ auf **Treiber importieren**.  

     Der Assistent zum Importieren von Gerätetreibern wird gestartet.  

5.  Klicken Sie auf der Seite **Verzeichnis angeben** im Abschnitt **Treiberquellverzeichnis** auf **Durchsuchen**, um zu dem Ordner mit den neuen Gerätetreibern zu wechseln, und klicken Sie anschließend auf **Weiter**.  

    > [!NOTE]
    >  Der Assistent für neue Gerätetreiber durchsucht alle Unterverzeichnisse des Treiberquellverzeichnisses. Wenn mehrere Treiber installiert werden müssen, sollten Sie diese daher in Ordnern in demselben Stammverzeichnis extrahieren und das Treiberquellverzeichnis anschließend als Stammverzeichnis festlegen, das alle Treiberquellordner enthält.  

6.  Überprüfen Sie auf der Seite **Zusammenfassung**, ob die Einstellungen richtig sind, und klicken Sie anschließend auf **Weiter**, um die Treiber in die Deployment Workbench zu importieren.  

7.  Klicken Sie auf der Seite **Bestätigung** auf **Fertig stellen**.  

 Wenn die Gerätetreiber erforderliche Starttreiber enthalten, wie z.B. Massenspeicher- oder Netzwerkklassentreiber, muss die Bereitstellungsfreigabe anschließend aktualisiert werden, um eine neue LiteTouc_x86- und LiteTouc_x64-Startumgebung zu generieren, welche die neuen Treiber enthält.  

 **So fügen Sie Gerätetreiber zu den Lite Touch Windows PE-Images hinzu**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Aktionsbereich auf **Update Deployment Share** (Bereitstellungsfreigabe aktualisieren).  

     Der Assistent für das Update der Bereitstellungsfreigabe wird gestartet.  

4.  Wählen Sie auf der Seite **Optionen** die gewünschten Optionen für das Update der Bereitstellungsfreigabe aus, und klicken Sie auf **Weiter**.  

5.  Überprüfen Sie auf der Seite **Zusammenfassung**, ob die Details korrekt sind, und klicken Sie anschließend auf **Weiter**.  

6.  Klicken Sie auf der Seite **Bestätigung** auf **Fertig stellen**.  

###  <a name="InstallDriversasApplications"></a> Installieren von Gerätetreibern als Anwendungen  
 Gerätetreiber, die als Anwendungen gepackt werden und nicht in einen Ordner mit einer INF-Datei (zusätzlich zu Treiberdateien) extrahiert werden können, sollten während des Bereitstellungsprozesses als Anwendung für die Installation zur Deployment Workbench hinzugefügt werden.  

 Anwendungen können als Tasksequenzschritt oder in der Datei „CustomSettings.ini“ angegeben werden. Gerätetreiberanwendungen sollten jedoch nur installiert werden, wenn die Tasksequenz auf einem Computer mit den Treibern ausgeführt wird. Um dies sicherzustellen, sollten Sie den Tasksequenzschritt für die Bereitstellung relevanter Gerätetreiberanwendungen als abhängigen Tasksequenzschritt ausführen. Die Bedingungskriterien für die Ausführung des Tasksequenzschritts können mithilfe von WMI-Abfragen für das Gerät auf dem Zielcomputer angegeben werden.  

#### <a name="add-the-device-driver-application-to-the-deployment-workbench"></a>Hinzufügen der Gerätetreiberanwendung zur Deployment Workbench  
 Die einzelnen Gerätetreiberanwendungen müssen zunächst in der Deployment Workbench importiert werden.  

> [!NOTE]
>  Konfigurieren Sie im Dialogfeld **Eigenschaften** einer Anwendung, ob die Anwendung während der Bereitstellung sichtbar sein soll, indem Sie das Kontrollkästchen **Hide this application in the Deployment Wizard** (Diese Anwendung im Bereitstellungs-Assistenten ausblenden) aktivieren oder deaktivieren. Wiederholen Sie diesen Vorgang für jede Gerätetreiberanwendung, die während der Bereitstellung verwendet wird.  

 **So fügen Sie die Gerätetreiberanwendung zur Deployment Workbench hinzu**  

1.  Laden Sie die Gerätetreiberanwendung herunter, und speichern Sie sie an einem temporären Speicherort.  

2.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

3.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu „Deployment Workbench > Deployment Shares > *Bereitstellungsfreigabe* > Applications“ (dabei steht *Bereitstellungsfreigabe* für den Namen der zu konfigurierenden Bereitstellungsfreigabe).  

4.  Klicken Sie im Bereich „Aktionen“ auf **Neue Anwendung**.  

     Der Assistent für neue Anwendungen wird gestartet.  

5.  Klicken Sie auf der Seite **Anwendungstyp** auf **Anwendung mit Quelldateien** und anschließend auf **Weiter**.  

6.  Geben Sie auf der Seite **Details** relevante Informationen über die Anwendung ein, und klicken Sie dann auf **Weiter**.  

7.  Klicken Sie auf der Seite **Quelle** im Abschnitt **Quellverzeichnis** auf **Durchsuchen**, und klicken Sie dann auf das Verzeichnis, das die Quelldateien der Anwendung für Gerätetreiber enthält. Klicken Sie auf **OK**.  

8.  Klicken Sie auf **Weiter**.  

9. Geben Sie auf der Seite **Ziel** einen Namen für das Zielverzeichnis ein, und klicken Sie dann auf **Weiter**.  

10. Geben Sie auf der Seite **Command Details** (Befehlsdetails) im Abschnitt **Befehlszeile** den Befehl ein, der die automatische Installation der Anwendung für Gerätetreiber ermöglicht.  

11. Überprüfen Sie auf der Seite **Zusammenfassung**, dass die Einstellungen richtig sind, und klicken Sie dann auf **Weiter**, um die Anwendung für Gerätetreiber in die Deployment Workbench zu importieren.  

12. Klicken Sie auf der Seite **Bestätigung** auf **Fertig stellen**.  

 Nachdem die Anwendungen in die Deployment Workbench importiert wurden, fügen Sie diese mithilfe der entsprechenden Logik zum Bereitstellungsprozess hinzu, um sicherzustellen, dass die Anwendung nur installiert wird, wenn diese auf der richtigen Hardware ausgeführt wird. Hierfür gibt es verschiedene Möglichkeiten:  

-   Angeben der Anwendung für Gerätetreiber als Teil einer Bereitstellungstasksequenz.  

-   Angeben der Anwendung für Gerätetreiber in „CustomSettings.ini“.  

-   Angeben der Anwendung für Gerätetreiber in der MDT-Datenbank.  

 In den folgenden Abschnitten wird jeder dieser Ansätze ausführlicher beschrieben.  

####  <a name="SpecifyDeviceAppTask"></a> Angeben der Anwendung für Gerätetreiber als Teil einer Tasksequenz  
 Die erste Methode zum Hinzufügen einer Anwendung für Gerätetreiber zum Bereitstellungsprozess besteht im Verwenden einer Tasksequenz, um Schritte für jede Anwendung für Gerätetreiber hinzuzufügen.  

 Es gibt zwei Hauptansätze für das Verwalten von Anwendungen für Gerätetreiber in der Tasksequenz:  

-   Erstellen Sie eine neue Tasksequenzgruppe für jedes Hardwaremodell. Fügen Sie dann eine Abfrage hinzu, um diese Aktionen auszuführen, wenn der Computer einem bestimmten Hardwaretyp entspricht.  

-   Erstellen Sie eine Tasksequenzgruppe für hardwarespezifische Anwendungen. Fügen Sie dann Abfragen für jede Tasksequenzaktion hinzu, sodass jeder Tasksequenzschritt mit dem Hardwaretyp verglichen und nur dann ausgeführt wird, wenn eine Übereinstimmung festgestellt wird.  

 **Erstellen einer neuen Tasksequenzgruppe für jeden Hardwaretyp**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe* > Tasksequenzen. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Detailbereich auf ***Tasksequenz***. Hierbei entspricht *Tasksequenz* der Bereitstellungstasksequenz, die zum Installieren der Anwendung für Gerätetreiber erforderlich ist.  

4.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

5.  Navigieren Sie vor der Installation der Anwendung im Dialogfeld ***Tasksequenzeigenschaften*** auf der Registerkarte **Tasksequenz** im Detailbereich zu Zustandswiederherstellung > Windows Update.  

6.  Klicken Sie auf der Registerkarte **Tasksequenz** auf **Hinzufügen** und dann auf **Neue Gruppe**.  

     Dadurch wird eine neue Tasksequenzgruppe in der Tasksequenz erstellt. Verwenden Sie diese neue Tasksequenzgruppe, um die Schritte für die Installation der hardwarespezifischen Anwendungen für Gerätetreiber zu erstellen.  

7.  Klicken Sie im Detailbereich auf **Neue Gruppe**.  

8.  Geben Sie auf der Registerkarte **Eigenschaften** im Feld **Name** einen Wert für ***Gruppenname*** ein. Hierbei entspricht *Gruppenname* dem Namen der Gruppe, z.B. *Hardwarespezifische Anwendungen: Dell Computer Corporation*.  

9. Klicken Sie auf der Registerkarte **Optionen** auf **Hinzufügen** und dann auf **WMI abfragen**.  

10. Geben Sie im Dialogfeld **Task Sequence WMI Condition** (WMI-Bedingung der Tasksequenz) folgende Informationen ein:  

    -   Geben Sie im Feld **WMI-Namespace** den Wert **root\cimv2** ein.  

    -   Geben Sie im Suchfeld **WQL-Abfrage** eine WQL-Abfrage (WMI Query Language) mithilfe der Klasse **Win32_ComputerSystem** ein, um sicherzustellen, dass die Anwendung nur für einen bestimmten Anwendungstyp installiert wird, z.B.:  

         **SELECT \* FROM Win32_ComputerSystem WHERE Model LIKE *%Hardwaremodell%* AND Manufacturer LIKE *%Hardwarehersteller%***  

         In diesem Beispiel entspricht *Hardwaremodell* dem Namen des Computermodells (z.B. Latitude D620) und *Hardwarehersteller* entspricht dem Namen des Computertyps (z.B. Dell Corporation).  

         Beim Symbol **%** handelt es sich um ein Platzhalterzeichen, das in die Namen eingefügt wird, um es Administratoren zu ermöglichen, alle Computermodelle oder -hersteller zurückzugeben, die den für ***Hardwaremodell*** oder ***Hardwarehersteller*** festgelegten Wert enthalten.  

     Weitere Informationen zu WMI- und WQL-Abfragen finden Sie im Abschnitt „Hinzufügen von WMI-Abfragen zu Bedingungen für Tasksequenzschritte“ im MDT-Artikel *Using the Microsoft Deployment Toolkit (Verwenden des Microsoft Deployment Toolkits)* sowie unter [Querying with WQL (WQL-Abfragen)](http://msdn.microsoft.com/library/aa392902.aspx).  

11. Klicken Sie auf **OK**, um die Abfrage zu übermitteln, und klicken Sie dann erneut auf **OK**, um Änderungen an der Tasksequenz zu übermitteln.  

> [!NOTE]
>  Dieser Vorgang muss für jeden Hardwaretyp jeder Anwendung für Gerätetreiber, die installiert werden soll, wiederholt werden.  

 Nachdem die hardwarespezifischen Tasksequenzgruppen erstellt wurden, können Anwendungen für Gerätetreiber zu jeder Gruppe hinzugefügt werden.  

 **Hinzufügen von Anwendungen für Gerätetreiber zu hardwarespezifischen Tasksequenzgruppen**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe* > Tasksequenzen. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Detailbereich auf ***Tasksequenz***. Hierbei entspricht *Tasksequenz* der Bereitstellungstasksequenz, die zum Installieren der Anwendung für Gerätetreiber erforderlich ist.  

4.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

5.  Klicken Sie im Dialogfeld ***Tasksequenzeigenschaften*** auf die Registerkarte **Tasksequenz**.  

6.  Navigieren Sie im Detailbereich zu Zustandswiederherstellung > *Hardwarespezifische_Gruppe*. Hierbei entspricht *Hardwarespezifische_Gruppe* dem Namen der hardwarespezifischen Gruppen, der der Tasksequenzschritt hinzugefügt wird, um die Anwendung für Gerätetreiber zu installieren.  

7.  Klicken Sie auf der Registerkarte **Tasksequenz** auf **Hinzufügen** > **Allgemein** > **Anwendung installieren**.  

     Der Tasksequenzschritt **Anwendung installieren** wird im Detailbereich angezeigt.  

8.  Klicken Sie im Detailbereich auf **Anwendung installieren**.  

9. Klicken Sie auf der Registerkarte **Eigenschaften** auf **Install a single application** (Eine einzelne Anwendung installieren), und klicken Sie in der Liste **Application to install** (Zu installierende Anwendung) auf ***Hardwareanwendung***. Hierbei entspricht *Hardwareanwendung* der Anwendung zum Installieren der hardwarespezifischen Anwendung.  

> [!NOTE]
>  Dieser Vorgang muss für jede Anwendung für Gerätetreiber, die während einer Bereitstellung verwendet werden muss, wiederholt werden.  

#### <a name="specify-the-device-driver-application-in-customsettingsini"></a>Angeben der Anwendung für Gerätetreiber in „CustomSettings.ini“  
 Wenn eine LTI- oder ZTI-Bereitstellung beginnt, muss zunächst die Verarbeitung der Steuerelementdateien „BootStrap.ini“ und „CustomSettings.ini“ abgeschlossen werden. Beide Dateien enthalten Regeln, die verwendet werden können, um die Bereitstellung dynamisch anzupassen.  

 Aufgrund der Art, wie MDT die Datei „CustomSettings.ini“ verarbeitet, können Sie diese verwenden, um Anwendungen auf Grundlage bestimmter Bedingungen hinzuzufügen. Diese Logik wird verwendet, um für Gerätetreiber spezifische Anwendungen basierend auf bestimmten Hardwaretypen während der Bereitstellung hinzuzufügen. Mithilfe der GUID der Anwendung, die sich in der Datei „Applications.xml“ in der Bereitstellungsfreigabe befindet, wird in „CustomSettings.ini“ auf diese verwiesen.  

 **Suchen einer importierten GUID einer Anwendung**  

1.  Öffnen Sie in der Bereitstellungsfreigabe des Bereitstellungsserver den Ordner „Control“, der sich beispielsweise im Pfad D:\Production Deployment Share\Control befindet.  

2.  Suchen und öffnen Sie die Datei „Application.xml“.  

3.  Suchen Sie die erforderliche Anwendung.  

4.  Suchen Sie die GUID der Anwendung, indem Sie die Zeile suchen, die in den `<guid>`-Tags der Anwendung eingeschlossen ist, z.B. `<application guid={c303fa6e-3a4d-425e-8102-77db9310e4d0}>`.  

 Als Teil des Initialisierungsvorgangs sammeln der LTI- und der ZTI-Prozess Informationen über den Computer, auf dem diese ausgeführt werden. Im Rahmen dieses Prozesses werden WMI-Abfragen durchgeführt, und die Werte der Klasse **Win32_ComputerSystem** für „Typ“ und „Modell“ werden als die Variablen **%Typ%** bzw. **%Modell%** aufgefüllt.  

 Diese Werte können während der Verarbeitung der Datei „CustomSettings.ini“ verwendet werden, um Abschnitte der Datei abhängig vom erkannten Typ oder Modell dynamisch zu lesen.  Im Folgenden finden Sie ein Beispiel für die Datei „CustomSettings.ini“.  

 **Beispieldatei „CustomSettings.ini“, die für die Installation einer hardwarespezifischen Anwendung konfiguriert wurde**  

```  
[Settings]  
Priority=Make, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  

[Dell Computer Corporation]  
Subsection=Dell-%Model%  

[Dell-Latitude D620]  
MandatoryApplications001={1D7DF331-47B7-472C-87B3-442597EC2F7D}  

[Dell-Latitude D610]  
MandatoryApplications001={c303fa6e-3a4d-425e-8102-77db9310e4d0}  
```  

 Verwenden Sie folgende Eigenschaften, um Anwendungen in „CustomSettings.ini“ anzugeben:  

-   **Applications:** Diese Eigenschaft kann verwendet werden, wenn Bereitstellungsadministratoren keinen Anwendungs-Assistenten als Teil des Bereitstellungsprozesses zur Verfügung stellen möchten. Hierfür wird in „CustomSettings.ini“ **SkipApplications=YES** festgelegt.  

-   **MandatoryApplications:** Diese Eigenschaft kann verwendet werden, wenn Bereitstellungsadministratoren den Anwendungs-Assistenten während der Bereitstellung zur Verfügung stellen möchten, damit Bereitstellungstechniker zusätzliche Anwendungen auswählen können, die während der Bereitstellung installiert werden sollen.  

     Wenn der Anwendungs-Assistent ohne die Eigenschaft **MandatoryApplications** (z.B. **SkipApplications=NO**) verwendet wird, werden Anwendungen überschrieben, die von der Eigenschaft **Applications** angegeben werden.  

     Im folgenden Beispiel wird veranschaulicht, wie die Variablenwerte für **%Typ%** und **%Modell%** verwendet werden, um die Erstellung der Anwendungsliste dynamisch zu bearbeiten. Die Werte für „Typ“ und „Modell“ für jeden Hardwaretyp können gesucht werden, indem Sie eine der folgenden Methoden verwenden:  

-   **Das Tool für Systeminformationen:** Verwenden Sie den Knoten „Systemzusammenfassung“ in diesem Tool, um den **Systemhersteller** (Typ) und das **Systemmodell** (Modell) zu identifizieren.  

-   **Windows PowerShell:** Verwenden Sie das Cmdlet **Get-WMIObject –class Win32_ComputerSystem**, um den Typ und das Modell des Computers zu bestimmen.  

-   **Die Befehlszeile der Windows-Verwaltungsinstrumentation:** Verwenden Sie **CSProduct Get Name, Vendor**, um den Namen (Modell) und den Hersteller (Typ) des Computers zurückzugeben.  

 **Bearbeiten von „CustomSettings.ini“ für das Hinzufügen von hardwarespezifischer Logik**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

4.  Klicken sie auf die Registerkarte **Regeln**.  

5.  Die Informationen, die in dieser Registerkarte eingegeben werden, werden in der Datei „CustomSettings.ini“ gespeichert. Bearbeiten Sie die Einträge der Datei „CustomSettings.ini“, um eine Logik für jedes Hardwaremodell hinzuzufügen, das eine für einen Gerätetreiber spezifische Anwendung besitzt. Dies wird unter [Angeben der Anwendung für Gerätetreiber als Teil einer Tasksequenz](#SpecifyDeviceAppTask) beschrieben.  

6.  Klicken Sie auf **OK**, um die Änderungen zu übernehmen.  

7.  Klicken Sie im Detailbereich auf *Bereitstellungsfreigabe*. Hierbei entspricht *Bereitstellungsfreigabe* dem Namen der zu konfigurierenden Bereitstellungsfreigabe.  

8.  Klicken Sie im Aktionsbereich auf **Update Deployment Share** (Bereitstellungsfreigabe aktualisieren).  

     Der Assistent für das Update der Bereitstellungsfreigabe wird gestartet.  

9. Wählen Sie auf der Seite **Optionen** die gewünschten Optionen für das Update der Bereitstellungsfreigabe aus, und klicken Sie auf **Weiter**.  

10. Überprüfen Sie auf der Seite **Zusammenfassung**, ob die Details korrekt sind, und klicken Sie anschließend auf **Weiter**.  

11. Klicken Sie auf der Seite **Bestätigung** auf **Fertig stellen**.  

 Standardmäßig werden während einer LTI-Bereitstellung alle verfügbaren Anwendungen im Windows-Bereitstellungs-Assistent angezeigt. Da für Gerätetreiber spezifische Anwendungen nur für bestimmte Hardwaretypen verfügbar sind, sollten diese nicht ständig angezeigt werden. Indem Sie das für Gerätetreiber spezifische Anwendungspaket in „CustomSettings.ini“ angeben, kann die Anwendung mithilfe der Option **Hide the application in the Deployment Wizard** (Anwendung im Bereitstellungs-Assistent ausblenden) in der Anwendungskonfiguration ausgeblendet werden.  

 **Ausblenden einer Anwendung im Bereitstellungs-Assistent**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu „Deployment Workbench > Deployment Shares > *Bereitstellungsfreigabe* > Applications“ (dabei steht *Bereitstellungsfreigabe* für den Namen der zu konfigurierenden Bereitstellungsfreigabe).  

3.  Klicken Sie im Detailbereich auf ***Anwendung_für_Gerätetreiber***. Hierbei entspricht *Anwendung_für_Gerätetreiber* der Anwendung, die aus dem Bereitstellungs-Assistent ausgeblendet werden soll.  

4.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

5.  Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen **Hide the application in the Deployment Wizard** (Anwendung im Bereitstellungs-Assistent ausblenden).  

6.  Klicken Sie auf **Übernehmen**, und schließen Sie das Dialogfeld **Eigenschaften**.  

#### <a name="specify-the-device-driver-application-in-the-mdt-db"></a>Angeben der Anwendung für Gerätetreiber in der MDT-Datenbank  
 Bei der MDT-Datenbank handelt es sich um eine Datenbankversion der Datei „CustomSettings.ini“. Diese kann zur Bereitstellungszeit nach Informationen abgefragt werden, die während der Bereitstellung verwendet werden sollen. Weitere Informationen zur Verwendung der MDT-Datenbank finden Sie unter „Selecting the Methods for Applying Configuration Settings“ (Auswählen der Methoden für das Anwenden von Konfigurationseinstellungen).  

 Wenn Sie die MDT-Datenbank zur Bereitstellungszeit abfragen, sind drei Methoden verfügbar, um den Zielcomputer zu identifizieren:  

-   Die Suche nach dem einzelnen Computer (z.B. mithilfe der MAC-Adresse oder dem Bestandskennzeichen).  

-   Die Suche nach dem Standort des Computers (mithilfe des Standardgateways).  

-   Die Suche nach dem Typ und Modell des Computers (mithilfe von WMI-Abfragen zu Hersteller, Typ und Modell).  

 Für jeden von Ihnen erstellten Datenbankeintrag können Sie Bereitstellungseigenschaften, Anwendungen und Administratoren festlegen und ob Configuration Manager-Pakete verwendet werden sollen. Indem Sie Einträge zu Typ und Modell in der Datenbank erstellen, können Sie die erforderlichen hardwarespezifischen Anwendungen für Gerätetreiber hinzufügen.  

 **Erstellen von Einträgen in der MDT-Datenbank für das Ermöglichen der Installation von Anwendungen für Gerätetreiber**  

> [!NOTE]
>  Wiederholen Sie diesen Vorgang für jeden Hardwaretyp und jedes Hardwaremodell, der bzw. das eine Anwendung für Gerätetreiber erfordert.  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > **Bereitstellungsfreigabe** > Erweiterte Konfiguration > Datenbank > Typ und Modell. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Aktionsbereich auf **Neu**.  

4.  Geben Sie im Dialogfeld **Eigenschaften** auf der Registerkarte **Identität** im Feld **Typ** ***Typname*** ein. Hierbei entspricht *Typname* einem leicht identifizierbaren Namen, der dem Hersteller des Zielcomputers zugeordnet werden soll.  

5.  Geben Sie im Feld **Modell** ***Modellname*** ein. Hierbei entspricht *Modellname* einem leicht identifizierbaren Namen, der dem Modell des Zielcomputers zugeordnet werden soll.  

6.  Fügen Sie auf der Registerkarte **Anwendungen** alle Anwendungen für Gerätetreiber hinzu, die für dieses Hardwaremodell erforderlich sind.  

## <a name="initiating-mdt-using-windows-deployment-services"></a>Initiieren von MDT mithilfe von Windows-Bereitstellungsdiensten  
 Windows Server 2008 verwendet Windows-Bereitstellungsdienste als aktualisierte und neu gestaltete Version von „Remoteinstallationsdienste“, dem Standardtool für die Bereitstellung in Windows Server 2003 SP2. Mithilfe von Windows-Bereitstellungsdiensten können Sie Windows-Betriebssysteme (insbesondere Windows 7, Windows Server 2008 oder höhere Betriebssysteme) auf einem Netzwerk bereitstellen, indem Sie den PXE-fähigen Netzwerkadapter eines Computers oder ein Startmedium verwenden.  

 Bevor Sie mit Windows-Bereitstellungsdiensten Bereitstellungen durchführen, bestimmen Sie, welche der folgenden Integrationsoptionen am besten zu Ihrer Umgebung passt:  

-   Option 1: Starten von Computern in PXE, um den LTI-Prozess zu initiieren.  

-   Option 2: Bereitstellen eines Betriebssystemimages vom Imagespeicher der Windows-Bereitstellungsdienste.  

-   Option 3: Verwenden von Multicasting mit MDT und der Rolle „Windows Server 2008“ des Windows-Bereitstellungsdiensteservers.  

### <a name="option-1-boot-computers-in-pxe-to-initiate-the-lti-process"></a>Option 1: Starten von Computern in PXE, um den LTI-Prozess zu initiieren  
 Minimieren Sie die Kosten der Verwaltung von Betriebssystembereitstellungen, indem Sie den MDT-Bereitstellungsprozess mithilfe der Windows-Bereitstellungsdienste und dem Dynamic Host Configuration-Protokoll starten. Dadurch müssen Sie kein startbares Medium für jeden Zielcomputer erstellen und bereitstellen.  

#### <a name="create-and-import-the-deployment-workbench-windows-pe-image-into-windows-deployment-services"></a>Erstellen und Importieren des Windows PE-Images der Deployment Workbench in die Windows-Bereitstellungsdienste  
 Wenn Sie eine neue MDT-Bereitstellungsfreigabe erstellen oder eine vorhandene bearbeiten, können Sie ein benutzerdefiniertes Windows PE-Startimage erstellen. Wenn die Bereitstellungsfreigabe aktualisiert wird, wird das Windows PE-Startimage automatisch mit Informationen über diese generiert und aktualisiert. Außerdem werden zusätzliche Treiber oder Komponenten eingefügt, die während der Konfiguration der Bereitstellungsfreigabe angegeben werden.  

 Das Windows PE-Startimage wird als ISO-Imagedatei generiert, die Sie auf eine CD oder DVD schreiben können, und als startbare WIM-Datei. Sie können die WIM-Datei in Windows-Bereitstellungsdienste importieren, sodass Computer, die in PXE starten können, das Windows PE-LTI-Startimage herunterladen und auf einem Netzwerk ausführen können, das zum Initialisieren einer Installation verwendet wird.  

 **Erstellen eines startbaren Windows PE-Images in der Deployment Workbench**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie anschließend auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

     Klicken Sie im Dialogfeld ***BereitstellungsfreigabeProperties*** auf die Registerkarte **Windows PE *platform* Settings** (platform-Einstellungen für Windows PE). Hierbei entspricht „platform“ der Architektur des Windows PE-Images, das konfiguriert werden soll.  

4.  Aktivieren Sie im Bereich **Lite Touch Boot Image Settings** (Einstellungen für das Lite Touch-Startimage) das Kontrollkästchen **Generate a Lite Touch bootable RAM disk ISO image** (Ein startbares Lite Touch-ISO-Image für RAM-Datenträger generieren).  

5.  Klicken Sie auf die Registerkarte **Windows PE *platform* Components** (platform-Komponenten für Windows PE). Hierbei entspricht *platform* der Architektur des Windows PE-Images, das konfiguriert werden soll.  

6.  Klicken Sie im Abschnitt **Treiberinjektion** auf die entsprechenden Treibertypen, die eingefügt werden sollen.  

    > [!NOTE]
    >  Dieser Schritt ist nicht erforderlich, wenn Windows PE die erforderlichen Gerätetreiber bereits enthält.  

7.  Wählen Sie im Abschnitt **Treiberinjektion** aus der Liste **Selection profile** (Auswahlprofil) das entsprechende Treiberauswahlprofil aus.  

8.  Klicken Sie im Dialogfeld **Eigenschaften** auf **OK**.  

    > [!NOTE]
    >  Dieser Schritt ist nicht erforderlich, wenn Windows PE die erforderlichen Gerätetreiber bereits enthält.  

9. Klicken Sie im Detailbereich auf ***Bereitstellungsfreigabe***. Hierbei entspricht *Bereitstellungsfreigabe* dem Namen der zu konfigurierenden Bereitstellungsfreigabe.  

10. Klicken Sie im Aktionsbereich auf **Update Deployment Share** (Bereitstellungsfreigabe aktualisieren).  

     Der Assistent für das Update der Bereitstellungsfreigabe wird gestartet.  

11. Wählen Sie auf der Seite **Optionen** die gewünschten Optionen für das Update der Bereitstellungsfreigabe aus, und klicken Sie auf **Weiter**.  

12. Überprüfen Sie auf der Seite **Zusammenfassung**, ob die Details korrekt sind, und klicken Sie anschließend auf **Weiter**.  

13. Klicken Sie auf der Seite **Bestätigung** auf **Fertig stellen**.  

     Wenn dieser Vorgang abgeschlossen, enthält der Ordner „Boot“ in der Bereitstellungsfreigabe eine bestimmte Anzahl von Startimages, z.B.:  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.wim  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim  

 Sie können die generierten ISO-Dateien direkt auf eine CD oder DVD schreiben oder diese verwenden, um den LTI-Prozess auf neuer Hardware zu initialisieren. Sie können die WIM-Startdateien ebenfalls in die Windows-Bereitstellungsdienste importieren, sodass neue Computer den LTI-Bereitstellungsprozess ohne physische Medien initiieren können.  

 **Importieren des Windows PE-Images in die Windows-Bereitstellungsdienste**  

1.  Starten Sie die Konsole der Windows-Bereitstellungsdienste, und stellen Sie eine Verbindung zu diesen her.  

2.  Klicken Sie in der Konsolenstruktur mit der rechten Maustaste auf **Boot Images** (Startimages), und klicken Sie dann auf **Add Boot Image** (Startimage hinzufügen).  

3.  Navigieren Sie zu dem WIM-Image, das importiert werden soll, z.B. D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim.  

4.  Der Importvorgang liest automatisch die Metadaten des Startimages, die Werte **Imagename** und **Imagebeschreibung** können jedoch bearbeitet werden. **Imagename** wirkt sich auf die Informationen zu den Startoptionen aus, die vom Windows-Start-Manager angezeigt werden, wenn der Client in PXE startet.  

5.  Wenn das Startimage importiert wurde, kann jeder Computer, der in PXE startet und eine Antwort von den Windows-Bereitstellungsdiensten erhält, das LTI-Startimage herunterfahren und eine LTI-Installation initiieren.  

 Die Installation und Konfiguration der Windows-Bereitstellungsdienste sind in diesem Leitfaden nicht enthalten. Weitere Informationen zu Windows-Bereitstellungsdiensten finden Sie im [Handbuch zu den Windows-Bereitstellungsdiensten](http://technet.microsoft.com/library/cc265612.aspx).  

#### <a name="use-windows-deployment-services-to-automatically-detect-the-deployment-server"></a>Verwenden von Windows-Bereitstellungsdiensten zum automatischen Erkennen des Bereitstellungsservers  
 Eine zusätzliche Option ist verfügbar, wenn Sie Windows-Bereitstellungsdienste dafür verwenden, MDT-Startimages zu hosten, wenn die MDT-Bereitstellungsfreigabe auf dem gleichen Server wie die Windows-Bereitstellungsdienste gehostet wird.  

 Wenn ein PXE-Client das MDT-Startimage lädt, wird der Name des Windows-Bereitstellungsdiensteservers aufgezeichnet, der das Startimage hostet, und in der MDT-Eigenschaft **WDSServer** gespeichert. Sie können auf diese Eigenschaft in der Datei „BootStrap.ini“ des Startimages und in der Datei „CustomSettings.ini“ der Bereitstellungsfreigabe über die Eigenschaft **DeployRoot** verweisen. Dies führt dazu, dass ein Client, der über die Windows-Bereitstellungsdienste startet, automatisch die Bereitstellungsfreigabe verwendet, die auf dem Windows-Bereitstellungsdiensteserver gehostet wird. Dadurch muss kein Servername in den Konfigurationsdateien angegeben werden.  

 **Festlegen des lokalen Windows-Bereitstellungsdiensteservers als Bereitstellungsserver**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe* > Erweiterte Konfiguration > Datenbank. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

4.  Klicken sie auf die Registerkarte **Regeln**.  

     Die Informationen, die in dieser Registerkarte eingegeben werden, werden in der Datei „CustomSettings.ini“ gespeichert.  

5.  Konfigurieren Sie die Eigenschaft **DeployRoot** für die Verwendung der Variable **%WDSServer%**, z.B. **DeployRoot=\\\\%WDSServer%\Deployment$**.  

6.  Klicken Sie auf **Edit BootStrap.ini** (BootStrap.ini bearbeiten).  

7.  Konfigurieren Sie „BootStrap.ini“ für die Verwendung der Eigenschaft **%WDSServer%**, indem Sie den Wert **DeployRoot** zu **DeployRoot=\\\\%WDSServer%\Deployment$** hinzufügen oder ihn ändern.  

8.  Klicken Sie im Menü **Datei** auf **Speichern**, um die Änderungen an der Datei „BootStrap.ini“ zu speichern.  

9. Klicken Sie auf **OK**.  

     Die Bereitstellungsfreigabe muss aktualisiert werden.  

10. Klicken Sie im Detailbereich auf **Bereitstellungsfreigabe**. Hierbei entspricht *Bereitstellungsfreigabe* dem Namen der zu konfigurierenden Bereitstellungsfreigabe.  

11. Klicken Sie im Aktionsbereich auf **Update Deployment Share** (Bereitstellungsfreigabe aktualisieren).  

     Der Assistent für das Update der Bereitstellungsfreigabe wird gestartet.  

12. Wählen Sie auf der Seite **Optionen** die gewünschten Optionen für das Update der Bereitstellungsfreigabe aus, und klicken Sie auf **Weiter**.  

13. Überprüfen Sie auf der Seite **Zusammenfassung**, ob die Details korrekt sind, und klicken Sie anschließend auf **Weiter**.  

14. Klicken Sie auf der Seite **Bestätigung** auf **Fertig stellen**.  

15. Importieren Sie die aktualisierte WIM-Startdatei in die Windows-Bereitstellungsdienste.  

### <a name="option-2-deploy-an-operating-system-image-from-the-windows-deployment-services-store"></a>Option 2: Bereitstellen eines Betriebssystemimages vom Speicher der Windows-Bereitstellungsdienste  
 Wenn Sie bereits Windows-Bereitstellungsdienste für die Bereitstellung von Betriebssystemen verwenden, erweitern Sie die Funktionalität von MDT, indem Sie diese dafür konfigurieren, auf die Betriebssystemimages von Windows-Bereitstellungsdiensten zu verweisen, die bereits verwendet werden, statt eigenen Speicher zu verwenden. Konfigurieren Sie sie ebenfalls dafür, Bereitstellungen über Windows-Bereitstellungsdienste durch Treiberverwaltung, Anwendungsbereitstellung, Updateinstallation, Regelverarbeitung und andere MDT-Funktionalitäten zu ergänzen. Nachdem MDT einen Verweis auf ein Betriebssystemimage von Windows-Bereitstellungsdiensten enthält, können Sie dieses wie ein Betriebssystem behandeln, das für eine MDT-Bereitstellungsfreigabe bereitgestellt wurde.  

 **Verweisen auf ein Betriebssystemimage von Windows-Bereitstellungsdiensten**  

> [!NOTE]
>  Die folgenden Schritte erfordern, dass mindestens ein Betriebssystemimage zuvor in den Windows-Bereitstellungsdiensteserver importiert wurde.  

1.  Aktualisieren Sie MDT, um auf die Images der Windows-Bereitstellungsdienste zugreifen zu können, indem Sie folgende Dateien aus dem Ordner „Sources“ des Windows-Mediums in den Ordner C:\Programme\Microsoft Deployment Toolkit\bin des Windows-Bereitstellungsdiensteservers kopieren.  

    -   Wdsclientapi.dll  

    -   Wdscsl.dll  

    -   Wdsimage.dll  

    -   Wdstptc.dll (Diese Datei ist nur anwendbar, wenn Sie diese aus den Quellverzeichnissen von Windows Server 2008 kopiert wird.)  

    > [!NOTE]
    >  Das verwendete Windows-Quellverzeichnis muss mit der Plattform des Betriebssystems übereinstimmen, das auf dem Computer ausgeführt wird, auf dem MDT installiert ist.  

2.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie auf **Deployment Workbench**.  

3.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe* > Betriebssysteme. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

4.  Klicken Sie im Bereich „Aktionen“ auf **Betriebssystem importieren**.  

     Der Assistent für das neue Betriebssystem wird gestartet.  

5.  Klicken Sie auf der Seite **Betriebssystemtyp** auf **Windows Deployment Services images** (Windows-Bereitstellungsdiensteimages), und klicken Sie dann auf **Weiter**.  

6.  Geben Sie auf der Seite **WDS-Server** den Namen des Windows-Bereitstellungsdiensteservers ein, auf den verwiesen werden soll (z.B. **WDSSvr001**), und klicken Sie dann auf **Weiter**.  

7.  Überprüfen Sie auf der Seite **Zusammenfassung**, dass die Einstellungen richtig sind, und klicken Sie dann auf **Weiter**.  

8.  Klicken Sie auf der Seite **Bestätigung** auf **Fertig stellen**.  

     Alle Images, die auf dem Windows-Bereitstellungsdiensteserver verfügbar sind, sind nun für MDT-Tasksequenzen verfügbar.  

> [!NOTE]
>  Das Importieren von Images von Windows-Bereitstellungsdiensten kopiert die Quelldateien nicht vom Windows-Bereitstellungsdiensteserver in die Bereitstellungsfreigabe. MDT verwendet weiterhin die Quelldateien vom ursprünglichen Speicherort aus.  

### <a name="option-3-use-multicasting-with-mdt-and-the-windows-server-2008-windows-deployment-services-role"></a>Option 3: Verwenden von Multicasting mit MDT und der Rolle „Windows Server 2008“ der Windows-Bereitstellungsdienste  
 Mit dem Release von Windows Server 2008 wurden die Windows-Bereitstellungsdienste verbessert, um die Bereitstellung von Images mithilfe von Multicastübertragungen zu unterstützen. MDT enthält ebenfalls Updates, um MDT in das Multicasting der Windows-Bereitstellungsdienste zu integrieren.  

 Darüber hinaus enthält Version 1.1 eines aktualisierten Windows Automated Installation Kit (Windows AIK) die Datei „Wdsmcast.exe“. Dadurch können Multicastsitzungen manuell verknüpft werden, wodurch der Client „Wdsmcast.exe“ starten kann, um Dateien aus einer aktiven Multicastsitzung zu kopieren.  

 Das Script „LTIApply.wsf“ verwendet „Wdsmcast.exe“, wenn es über die Bereitstellungsfreigabe auf Quelldateien für Betriebssysteme zugreift. „LTIApply.wsf“ sucht auf der Bereitstellungsfreigabe entweder im Ordner *Bereitstellungsfreigabe*\Tools\x86 oder *Bereitstellungsfreigabe*\Tools\x64 nach „Wdsmcast.exe“, je nach der ausgeführten Version von Windows PE. Hierbei entspricht *Bereitstellungsfreigabe* dem Namen des Systemordners, der die Bereitstellungsfreigabe enthält.  

 Wenn „LTIApply.wsf“ ausgeführt wird, wird immer versucht, auf WIM-Images von einem vorhandenen Multicaststream zuzugreifen und diese herunterzuladen. Wenn jedoch kein Multicaststream vorhanden ist, wird auf eine Kopie der Standarddatei zurückgegriffen.  

> [!NOTE]
>  Dieser Vorgang gilt nur für WIM-Imagedateien.  

 Folgende Voraussetzungen sind für die Vorbereitung des MDT-Multicastings durch den Bereitstellungsserver erforderlich:  

-   Auf dem Bereitstellungsserver muss Windows Server 2008 oder höher ausgeführt werden.  

-   Die Rolle „Windows-Bereitstellungsdienste“ muss über die Serververwaltungskonsole installiert worden sein.  

-   Windows AIK 1.1 für Windows Server 2008 muss installiert sein.  

-   MDT muss installiert sein.  

-   Wie bei jeder Bereitstellung, die MDT verwendet, muss mindestens ein WIM-Image für ein Betriebssystem importiert worden sein. Dieses muss entweder alle Quelldateien oder ein benutzerdefiniertes Image mit Setupdateien enthalten.  

> [!NOTE]
>  Es ist wichtig, die aktuelle Version von Windows AIK für das Multicasting zu verwenden. Die Kopie von Windows PE, die in früheren Versionen von Windows AIK enthalten ist (z.B. Windows AIK 1.0), unterstützt das Herunterladen von einem Multicastserver nicht.  

 **Konfigurieren von MDT für das Multicasting über eine vorhandene Bereitstellungsfreigabe**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe.  

3.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

4.  Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen **Enable multicast for this deployment share (requires Windows Server 2008 Windows Deployment Services)** (Multicast für diese Bereitstellungsfreigabe aktivieren (erfordert Windows Server 2008 und Windows-Bereitstellungsdienste)).  

5.  Klicken Sie auf **OK**.  

6.  Klicken Sie im Aktionsbereich auf **Update Deployment Share** (Bereitstellungsfreigabe aktualisieren).  

     Der Assistent für das Update der Bereitstellungsfreigabe wird gestartet.  

7.  Wählen Sie auf der Seite **Optionen** die gewünschten Optionen für das Update der Bereitstellungsfreigabe aus, und klicken Sie auf **Weiter**.  

8.  Überprüfen Sie auf der Seite **Zusammenfassung**, ob die Details korrekt sind, und klicken Sie anschließend auf **Weiter**.  

9. Klicken Sie auf der Seite **Bestätigung** auf **Fertig stellen**.  

 Die Bereitstellungsfreigabe wird nun für Multicastübertragungen von Windows-Bereitstellungsdiensten konfiguriert.  

 Dieser Vorgang erstellt eine automatische Umwandlung der Multicastübertragungen von Windows-Bereitstellungsdiensten, die die vorhandene MDT-Bereitstellungsfreigabe direkt verwendet. MDT erstellt keine Übertragungen mit geplanter Umwandlung. Beachten Sie außerdem, dass keine zusätzlichen Images in Windows-Bereitstellungsdienste importiert werden und dass es nicht möglich ist, Multicast für Startimages zu verwenden, da der Multicastclient nicht geladen werden kann, bevor Windows PE ausgeführt wird.  

 **Überprüfen, dass die Multicastübertragung in den Windows-Bereitstellungsdiensten generiert wurde**  

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Windows-Bereitstellungsdienste**.  

2.  Klicken Sie in der Konsolenstruktur der Windows-Bereitstellungsdienste mit der rechten Maustaste auf **Server** und dann auf **Server hinzufügen**.  

3.  Klicken Sie im Dialogfeld **Server hinzufügen** auf **Lokaler Computer**, und klicken Sie dann auf **OK**.  

4.  Klicken Sie in der Konsolenstruktur der Windows-Bereitstellungsdienste auf **Server**, und klicken Sie dann auf ***Servername***. Hierbei entspricht *Servername* dem Namen des Computers, auf dem die Windows-Bereitstellungsdienste ausgeführt werden. Klicken Sie auf **Multicastübertragungen**.  

5.  Im Detailbereich wird eine neue Übertragung mit automatischer Umwandlung für die Bereitstellungsfreigabe aufgeführt, z.B. **BDD Share Deployment$**.  

6.  Überprüfen Sie, dass der Status von **BDD Share Deployment$** auf **Aktiv** festgelegt ist.  

 Nachdem ein Computer bereitgestellt wurde, überprüfen Sie, dass das Betriebssystem durch eine Multicastübertragung heruntergeladen wurde, indem Sie die Datei „BDD.log“ im Ordner \Windows\Temp\DeploymentLogs prüfen.  

 Es gibt zwei Einträge im Protokollordner, die mit **Multicast transfer** (Multicastübertragung) beginnen. Überprüfen Sie diese, um sicherzustellen, dass die Übertragung erfolgreich war. Weitere Informationen zu Multicastübertragungen mit MDT und Windows-Bereitstellungsdiensten finden Sie im Abschnitt „Aktivieren der Multicastbereitstellung über Windows-Bereitstellungsdienste für LTI-Bereitstellungen“ im MDT-Artikel *Verwenden des Microsoft Deployment Toolkits*.  

## <a name="performing-staged-deployments-using-mdt-oem-preload"></a>Durchführen von Stagingbereitstellung mithilfe von MDT (OEM-Vorabladen)  
 In vielen Organisationen werden Computer mit dem Betriebssystemimage vor der Bereitstellung für das Produktionsnetzwerk geladen. In einigen Fällen wird das Laden des Betriebssystemimages von einem Team innerhalb der Organisation durchgeführt, das für die Erstellung des Computers in einer Stagingumgebung zuständig ist. In anderen Fällen wir das Laden des Betriebssystemimages vom Hersteller der Computerhardware durchgeführt. Dieser wird auch als *Originalgerätehersteller* (Original Equipment Manufacturer, OEM) bezeichnet.  

> [!NOTE]
>  Der OEM-Vorabladevorgang wird in MDT nur für Bereitstellungen unterstützt, die mithilfe von LTI durchgeführt werden. Verwenden Sie das vorab bereitgestellte Medienfeature in Configuration Manager.  

### <a name="overview-of-the-oem-preload-process-in-mdt"></a>Übersicht über den OEM-Vorabladevorgang in MDT  
 Der OEM-Vorabladevorgang ist in drei Phasen unterteilt:  

-   **Phase 1:** Erstellen eines medienbasierten Images des Referenzcomputers, das in der Stagingumgebung angewendet werden soll.  

-   **Phase 2:** Anwenden des Referenzcomputerimages auf den Zielcomputer in einer Stagingumgebung.  

-   **Phase 3:** Abschließen der Bereitstellung des Zielcomputers in der Produktionsumgebung.  

 Phase 1 und 3 werden üblicherweise von den Verantwortlichen für die Bereitstellung durchgeführt. Je nach Verwendung des OEM-Vorabladevorgangs in der Organisation kann Phase 2 von der Organisation oder vom Hersteller der Computerhardware, der die Computer bereitstellt, durchgeführt werden. Wenn Phase 2 durch die Organisation durchgeführt wird, befindet sich die Stagingumgebung innerhalb der Organisation. Wenn Phase 2 durch einen OEM durchgeführt wird, befindet sich die Stagingumgebung in dessen Umgebung.  

#### <a name="overview-of-mdt-configuration-files-in-the-oem-preload-process"></a>Übersicht über die MDT-Konfigurationsdateien im OEM-Vorabladevorgang  
 Während Phase 1 und 3 des OEM-Vorabladevorgangs werden separate MDT-Konfigurationsdateien („CustomSettings.ini“ und „BootStrap.ini“) von den ausgeführten Tasksequenzen verwendet. Beide Konfigurationsdateien sind jedoch gleichzeitig in verschiedenen Ordnerstrukturen vorhanden.  

 In Phase 1 werden die Konfigurationsdateien während der Erstellung des Referenzcomputers verwendet und in dem Ordner gespeichert, der für die Tasksequenz spezifisch ist, die in dieser Phase verwendet wird. Die Konfigurationsdateien, die in Phase 3 des OEM-Vorabladevorgangs verwendet werden, werden in dem Ordner gespeichert, der für die Tasksequenz spezifisch ist, die in dieser Phase verwendet wird.  

 Wenn Sie Änderungen an den Konfigurationsdateien vornehmen, stellen Sie sicher, dass diese den richtigen Tasksequenzen in jeder Phase des OEM-Vorabladevorgangs entsprechen.  

#### <a name="overview-of-mdt-log-files-in-the-oem-preload-process"></a>Übersicht über die MDT-Protokolldateien im OEM-Vorabladevorgang  
 Während Phase 1 und 3 des OEM-Vorabladevorgangs werden separate MDT-Protokolldateien generiert:  

-   Die MDT-Protokolldateien für Phase 1 werden in den Ordnern C:\MININT und C:\SMSTSLog gespeichert.  

-   Die MDT-Protokolldateien für Phase 3 werden für x86-basierte Bereitstellungen im Ordner %WINDIR%\System32\CCM\Logs oder für x64-basierte Bereitstellungen im Ordner %WINDIR%\SysWow64\CCM\Logs gespeichert.  

 Verwenden Sie den entsprechenden Ordner, wenn Sie Probleme bei der MDT-Bereitstellung diagnostizieren oder behandeln.  

### <a name="staged-deployments-using-lti"></a>Stagingbereitstellung mithilfe von LTI  
 Führen Sie den OEM-Vorabladevorgang für LTI-Bereitstellungen mithilfe des Bereitstellungsfreigabetyps *Wechselmedien (Medium)* durch. Andere Bereitstellungsfreigabetypen werden für den OEM-Vorabladevorgang nicht unterstützt.  

 Erstellen Sie zum Durchführen des OEM-Vorabladevorgangs zusätzlich zu jeder Tasksequenz, die für die Bereitstellung des Zielbetriebssystems verwendet wird, eine Tasksequenz, die auf der Lite Touch-OEM-Tasksequenzvorlage basiert. Erstellen Sie dann eine Bereitstellungsfreigabe vom Typ *Wechselmedien (Medium)*, die schließlich eine ISO-Datei der Inhalte der Bereitstellungsfreigabe erstellt, z.B. die Datei „LiteTouchPE_x86.iso“ oder „LiteTouchPE_x64.iso“ (je nach Prozessorplattform des Zielcomputers). Der Updatevorgang der Bereitstellungsfreigabe erstellt ebenfalls eine Ordnerstruktur, die verwendet werden kann, um UDF-Medien (Universal Disk Format ) zu erstellen.  

#### <a name="lti-oem-preload-processphase-1-create-a-media-based-image"></a>LTI-OEM-Vorabladevorgang, Phase 1: Erstellen eines medienbasierten Images  
 Die Organisation, in der die Bereitstellung stattfindet, führt Phase 1 des OEM-Vorabladevorgangs durch. Das Ergebnis dieser Phase ist ein startbares Image (z.B. eine ISO-Datei) oder ein startbares Medium (z.B. eine DVD), die an den OEM oder an die Stagingumgebung innerhalb der Organisation gesendet wird, in der die Bereitstellung stattfindet. Diese Schritte werden überwiegend in der Deployment Workbench durchgeführt.  

 **Erstellen eines medienbasierten Images für die Übermittlung an den OEM oder an die Stagingumgebung innerhalb der Organisation, in der die Bereitstellung stattfindet**  

1.  Füllen Sie folgende Knoten für die Bereitstellungsfreigabe in der Deployment Workbench auf:  

    -   Betriebssysteme  

    -   Applications  

    -   Pakete  

    -   Standardtreiber  

     Weitere Informationen zum Durchführen dieses Schritts finden Sie im MDT-Artikel *Verwenden des Microsoft Deployment Toolkits* im Abschnitt „Managing Deployment Shares in the Deployment Workbench (Verwalten von Bereitstellungsfreigaben in Deployment Workbench)“.  

2.  Erstellen Sie eine neue Tasksequenz, die auf der Lite Touch-OEM-Tasksequenzvorlage basiert, in der Deployment Workbench.  

     Weitere Informationen zum Durchführen dieses Schritts finden Sie im MDT-Artikel *Verwenden des Microsoft Deployment Toolkits* im Abschnitt „Configuring Task Sequences in the Deployment Workbench (Konfigurieren von Tasksequenzen in Deployment Workbench)“.  

3.  Erstellen Sie eine weitere Tasksequenz, die verwendet wird, um das Zielbetriebssystem nach der Bereitstellung in der Produktionsumgebung auf dem Zielcomputer bereitzustellen.  

     Weitere Informationen zum Durchführen dieses Schritts finden Sie im MDT-Artikel *Verwenden des Microsoft Deployment Toolkits* im Abschnitt „Configuring Task Sequences in the Deployment Workbench (Konfigurieren von Tasksequenzen in Deployment Workbench)“.  

4.  Erstellen Sie ein Auswahlprofil, das die Anwendungen, Betriebssysteme, Treiber, Pakete und Tasksequenzen enthält, die für die OEM-Bereitstellung erforderlich sind.  

     Weitere Informationen zum Durchführen dieses Schritts finden Sie im MDT-Artikel *Verwenden des Microsoft Deployment Toolkits* im Abschnitt „Manage Selection Profiles (Verwalten von Auswahlprofilen)“.  

5.  Erstellen Sie Bereitstellungsmedien.  

     Weitere Informationen zum Durchführen dieses Schritts finden Sie im MDT-Artikel *Verwenden des Microsoft Deployment Toolkits* im Abschnitt „Manage LTI Deployment Media (Verwalten von LTI-Bereitstellungsmedien)“.  

6.  Aktualisieren Sie die Bereitstellungsmedien, die im vorherigen Schritt in der Deployment Workbench erstellt wurden.  

     Wenn Sie diese aktualisieren, erstellt die Deployment Workbench die Datei „LiteTouchMedia.iso“. Weitere Informationen zum Durchführen dieses Schritts finden Sie im MDT-Artikel *Verwenden des Microsoft Deployment Toolkits* im Abschnitt „Manage LTI Deployment Media (Verwalten von LTI-Bereitstellungsmedien)“.  

7.  Brennen Sie die Datei „LiteTouchMedia.iso“, die im vorherigen Schritt erstellt wurde, auf eine DVD.  

    > [!NOTE]
    >  Wenn Sie die ISO-Datei für den OEM oder die Stagingumgebung der Organisation bereitstellen, ist dieser Schritt nicht erforderlich.  

8.  Stellen Sie die ISO-Datei oder die DVD für den OEM oder die Stagingumgebung der Organisation bereit.  

#### <a name="lti-oem-preload-processphase-2-apply-the-image-to-the-target-computer"></a>LTI-OEM-Vorabladevorgang, Phase 2: Anwenden des Images auf den Zielcomputer  
 Phase 2 des Vorabladevorgangs wird vom OEM oder dem Bereitstellungsteam in der Stagingumgebung oder der Organisation durchgeführt, in der die Bereitstellung stattfindet. Während dieser Phase des Vorgangs wird die ISO-Datei oder die DVD, die in Phase 1 erstellt wurde, auf die Zielcomputer angewendet. Das Ergebnis dieser Phase ist, dass das Image auf den Zielcomputern bereitgestellt wird, sodass diese für die Bereitstellung in der Produktionsumgebung bereit sind.  

 **Anwenden des Images auf die Zielcomputer**  

1.  Starten Sie einen Zielcomputer mit dem Medium, das Sie in Phase 1 erstellt haben.  

     Zunächst wird Windows PE und anschließend der Windows-Bereitstellungs-Assistent gestartet.  

2.  Klicken Sie im Windows-Bereitstellungs-Assistent auf die Tasksequenz **OEM Preinstallation Task Sequence for Staging Environment** (Tasksequenz für die OEM-Vorinstallation für Stagingumgebungen).  

     Die Tasksequenz startet und die Inhalte der startbaren Medien werden auf die lokale Festplatte des Zielcomputers kopiert.  

3.  Wenn der Windows-Bereitstellungs-Assistent für die Tasksequenz **OEM Preinstallation Task Sequence for Staging Environment** (Tasksequenz für die OEM-Vorinstallation für Stagingumgebungen) abgeschlossen ist, kann die Festplatte zum Initiieren des restlichen Bereitstellungsprozesses verwendet werden, indem der Windows-Bereitstellungs-Assistent für die anderen Tasksequenzen ausgeführt wird, die für die Bereitstellung des Betriebssystems verwendet werden.  

     Die Tasksequenz **OEM Preinstallation Task Sequence for Staging Environment** (Tasksequenz für die OEM-Vorinstallation für Stagingumgebungen) ist für das Bereitstellen des Images auf dem Zielcomputer und für das Initiieren des LTI-Prozesses verantwortlich. Der Windows-Bereitstellungs-Assistent wird erneut gestartet, um die Tasksequenzen auszuführen, die für die Bereitstellung des Betriebssystems auf dem Zielcomputer verwendet werden.  

4.  Klonen Sie die Inhalte der ersten Festplatte auf alle erforderlichen Zielcomputer in der Stagingumgebung.  

5.  Die Zielcomputer werden für die Bereitstellung für die Produktionsumgebung bereitgestellt.  

#### <a name="lti-oem-preload-processphase-3-complete-target-computer-deployment"></a>LTI-OEM-Vorabladevorgang, Phase 3: Abschließen der Bereitstellung von Zielcomputern  
 Phase 3 ist die letzte Phase des OEM-Vorabladevorgangs und wird in der Produktionsumgebung der Organisation durchgeführt, in der die Bereitstellung stattfindet. Während dieser Phase des Vorgangs werden die Zielcomputer und das startbare Medienimage, das während der vorherigen Phase auf die Festplatte der Stagingumgebung kopiert wurde, gestartet.  

 **Abschließen der Bereitstellung des Zielcomputers in der Produktionsumgebung**  

1.  Starten Sie den Zielcomputer.  

     Zunächst wird Windows PE und anschließend der Windows-Bereitstellungs-Assistent gestartet.  

2.  Schließen Sie den Windows-Bereitstellungs-Assistenten mithilfe der spezifischen Konfigurationsinformationen für jeden Zielcomputer ab.  

     Weitere Informationen zum Abschließen dieses Schritts finden Sie im MDT-Artikel *Verwenden des Microsoft Deployment Toolkits* im Abschnitt „Running the Deployment Wizard (Ausführen des Bereitstellungs-Assistenten)“.  

 Wenn diese Phase abgeschlossen ist, kann der Zielcomputer in der Produktionsumgebung verwendet werden.  

## <a name="using-windows-powershell-to-perform-common-tasks"></a>Verwenden von Windows PowerShell zum Ausführen allgemeiner Aufgaben  
 Die administrativen MDT-Aufgaben in der Deployment Workbench werden von den zugrunde liegenden Windows PowerShell-Cmdlets durchgeführt. Diese können Sie verwenden, um administrative Aufgaben wie die, die in den folgenden Schritten erläutert werden, zu automatisieren.  

 Sie können die Verwaltung von MDT automatisieren, indem Sie folgende Schritte durchführen:  

-   Erstellen Sie wie unter [Erstellen einer neuen Bereitstellungsfreigabe](#CreateNewDeployShare) beschrieben eine neue Bereitstellungsfreigabe.  

-   Erstellen Sie wie unter [Erstellen eines Ordners](#CreateFolder) beschrieben einen Ordner in einer Bereitstellungsfreigabe.  

-   Löschen Sie wie unter [Löschen eines Ordners](#DeleteFolder) beschrieben einen Ordner aus einer Bereitstellungsfreigabe.  

-   Importieren Sie wie unter [Importieren eines Gerätetreibers](#ImportDeviceDriver) beschrieben einen Gerätetreiber in eine Bereitstellungsfreigabe.  

-   Löschen Sie wie unter [Löschen eines Gerätetreibers](#DeleteDeviceDriver) beschrieben einen Gerätetreiber aus einer Bereitstellungsfreigabe.  

-   Importieren Sie wie unter [Importieren eines Betriebssystempakets](#ImportOpSysPackage) beschrieben ein Betriebssystempaket in eine Bereitstellungsfreigabe.  

-   Löschen Sie wie unter [Löschen eines Betriebssystempakets](#DeleteOpSysPackage) beschrieben ein Betriebssystempaket aus einer Bereitstellungsfreigabe.  

-   Importieren Sie wie unter [Importieren eines Betriebssystems](#ImportOpSys) beschrieben ein Betriebssystem in eine Bereitstellungsfreigabe.  

-   Löschen Sie wie unter [Löschen eines Betriebssystems](#DeleteOpSys) beschrieben ein Betriebssystem aus einer Bereitstellungsfreigabe.  

-   Erstellen Sie wie unter [Erstellen einer Anwendung](#CreateApplication) beschrieben eine Anwendung in einer Bereitstellungsfreigabe.  

-   Löschen Sie wie unter [Löschen einer Anwendung](#DeleteApplication) beschrieben eine Anwendung aus einer Bereitstellungsfreigabe.  

-   Erstellen Sie wie unter [Erstellen einer Tasksequenz](#CreateTaskSequence) beschrieben eine Tasksequenz in einer Bereitstellungsfreigabe.  

-   Löschen Sie wie unter [Löschen einer Tasksequenz](#DeleteTaskSequence) beschrieben eine Tasksequenz aus einer Bereitstellungsfreigabe.  

-   Erstellen Sie wie unter [Erstellen einer MDT-Datenbank](#CreateMDTDB) beschrieben eine MDT-Datenbank.  

-   Erstellen Sie wie unter [Erstellen eines Auswahlprofils](#CreateSelectProfile) beschrieben ein Auswahlprofil.  

-   Aktualisieren Sie wie unter [Aktualisieren einer Bereitstellungsfreigabe](#UpdatingDeployShare) beschrieben eine Bereitstellungsfreigabe.  

-   Erstellen Sie wie unter [Erstellen einer verknüpften Bereitstellungsfreigabe](#CreateLinkedDeployShare) beschrieben eine verknüpfte Bereitstellungsfreigabe.  

-   Aktualisieren Sie wie unter [Aktualisieren einer verknüpften Bereitstellungsfreigabe](#UpdatingLinkedDeployShare) beschrieben eine verknüpfte Bereitstellungsfreigabe.  

-   Löschen Sie wie unter [Löschen einer verknüpften Bereitstellungsfreigabe](#DeleteLinkedDeployShare) beschrieben eine verknüpfte Bereitstellungsfreigabe.  

-   Erstellen Sie wie unter [Erstellen von Medien](#CreateMedia) beschrieben ein Bereitstellungsmedium.  

-   Generieren Sie wie unter [Generieren von Medien](#GenerateMedia) beschrieben ein Bereitstellungsmedium.  

-   Löschen Sie wie unter [Löschen von Medien](#DeleteMedia) beschrieben ein Bereitstellungsmedium.  

###  <a name="CreateNewDeployShare"></a> Erstellen einer neuen Bereitstellungsfreigabe  
 Folgende Windows PowerShell-Befehle erstellen eine neue Bereitstellungsfreigabe namens *Production$* unter D:\Production Deployment Share. Die neue Bereitstellungsfreigabe wird in der Deployment Workbench als „Production“ angezeigt.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "D:\Production Deployment Share" -Description "Production" -NetworkPath "\\Deployment_Server\Production$" -Verbose | add-MDTPersistentDrive -Verbose  
    ```  

###  <a name="CreateFolder"></a> Erstellen eines Ordners  
 Folgende Windows PowerShell-Befehle erstellen einen Adobe-Ordner in der Konsolenstruktur der Deployment Workbench unter Deployment Workbench\/Deployment Shares\/Production\/Applications.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Applications" -enable "True" -Name "Adobe" -Comments "This folder contains Adobe software" -ItemType "folder" -Verbose remove-psdrive DS001 -Verbose  
    ```  

    > [!NOTE]
    >  Wenn Sie „`remove-psdrive`“ zum Skript hinzufügen, wird sichergestellt, dass der Hintergrundprozess abgeschlossen wird, bevor der Vorgang fortgesetzt wird.  

###  <a name="DeleteFolder"></a> Löschen eines Ordners  
 Folgende Windows PowerShell-Befehle löschen den Ordner „Deployment Workbench\/Deployment Shares\/Production\/Applications\/Adobe“.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Remove-item -path "DS002:\Applications\Adobe" -Verbose  
    ```  

> [!NOTE]
>  Das Skript schlägt fehl, wenn der Ordner nicht leer ist.  

###  <a name="ImportDeviceDriver"></a> Importieren eines Gerätetreibers  
 Folgende Windows PowerShell-Befehle importieren den Gerätetreiber „Dell 2407 WFP“ für einen Monitor in die Bereitstellungsfreigabe „Production“.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtdriver -path "DS002:\Out-of-Box Drivers\Monitor" -SourcePath "D:\Drivers\Dell\2407 WFP" -Verbose  
    ```  

###  <a name="DeleteDeviceDriver"></a> Löschen eines Gerätetreibers  
 Folgende Windows PowerShell-Befehle löschen den Treiber „Dell 2407 WFP“ für einen Monitor aus der Bereitstellungsfreigabe „Production“.  

```  
Remove-item -path "DS002:\Out-of-Box Drivers\Dell Inc. Monitor 2407WFP.INF 1.0" -Verbose  
```  

###  <a name="ImportOpSysPackage"></a> Importieren eines Betriebssystempakets  
 Folgende Windows PowerShell-Befehle importieren alle Betriebssystempakete, die sich unter D:\\Updates\\Microsoft\\Vista befinden. Diese Betriebssystempakete werden in der Bereitstellungsfreigabe „Production“ gespeichert, die sich unter D:\\Production Deployment Share befindet.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtpackage -path "DS002:\Packages" -SourcePath "D:\Updates\Microsoft\Vista" -Verbose  
    ```  

###  <a name="DeleteOpSysPackage"></a> Löschen eines Betriebssystempakets  
 Folgende Windows PowerShell-Befehle löschen das angegebene Betriebssystempaket aus der Bereitstellungsfreigabe „Production“.  

```  
Remove-item -path "DS002:\Packages\Package_1_for_KB940105 neutral x86 6.0.1.0 KB940105" -Verbose  
```  

###  <a name="ImportOpSys"></a> Importieren eines Betriebssystems  
 Folgende Windows PowerShell-Befehle importieren das Betriebssystem „Windows Vista“, das sich unter D:\\Operating Systems\\Windows Vista x86 befindet. Das Betriebssystem wird in der Bereitstellungsfreigabe „Production“ gespeichert, die sich unter D:\\Production Deployment Share befindet.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtoperatingsystem -path "DS002:\Operating Systems" -SourcePath "D:\Operating Systems\Windows Vista x86" -DestinationFolder "Windows Vista x86" -Verbose  
    ```  

###  <a name="DeleteOpSys"></a> Löschen eines Betriebssystems  
 Folgende Windows PowerShell-Befehle löschen das Betriebssystem „Windows Vista Home Basic“ aus der Bereitstellungsfreigabe „Production“.  

```  
Remove-item -path "DS002:\Operating Systems\Windows Vista HOMEBASIC in Windows Vista x86 install.wim" -Verbose  
```  

###  <a name="CreateApplication"></a> Erstellen einer Anwendung  
 Folgende Windows PowerShell-Befehle erstellen die Anwendung „Adobe Reader 9“ mithilfe der Quelldateien, die sich unter D:\\Software\\Adobe\\Reader 9 befinden. Diese Anwendung wird in der Bereitstellungsfreigabe „Production“ gespeichert, die sich unter D:\\Production Deployment Share befindet.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-MDTApplication -path "DS002:\Applications" -enable "True" -Name "Adobe Reader 9" -ShortName "Reader" -Version "9" -Publisher "Adobe" -Language "" -CommandLine "setup.exe" -WorkingDirectory ".\Applications\Adobe Reader 9" -ApplicationSourcePath "D:\Software\Adobe\Reader 9" -DestinationFolder "Adobe Reader 9" -Source ".\Applications\Adobe Reader 9" -Verbose  
    ```  

###  <a name="DeleteApplication"></a> Löschen einer Anwendung  
 Folgende Windows PowerShell-Befehle löschen die Anwendung „Adobe Reader 9“ aus der Bereitstellungsfreigabe „Production“.  

```  
Remove-item -path "DS002:\Applications\Adobe Reader 9" -Verbose  
```  

###  <a name="CreateTaskSequence"></a> Erstellen einer Tasksequenz  
 Folgende Windows PowerShell-Befehle erstellen die Tasksequenz **Windows Vista Production Build** (Windows Vista-Produktionsbuild) in der Bereitstellungsfreigabe „Production“, die sich unter D:\\Production Deployment Share befindet.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdttasksequence -path "DS002:\Task Sequences" -Name "Windows Vista Business Production Build" -Template "Client.xml" -Comments "Approved for use in the production environment.  This task sequence uses the Standard Client task sequence template" -ID "Vista_Ref" -Version "1.0" -OperatingSystemPath "DS002:\Operating Systems\Windows Vista BUSINESS in Windows Vista x86 install.wim" -FullName "Fabrikam User" -OrgName "Fabrikam" -HomePage "http://www.Fabrikam.com" -AdminPassword "secure_password" -Verbose  
    ```  

###  <a name="DeleteTaskSequence"></a> Löschen einer Tasksequenz  
 Folgende Windows PowerShell-Befehle löschen die Tasksequenz **Windows Vista Production Build** (Windows Vista-Produktionsbuild) aus der Bereitstellungsfreigabe „Production“.  

```  
Remove-item -path "DS002:\Task Sequences\Windows Vista Business Production Build" -force -Verbose  
```  

###  <a name="CreateMDTDB"></a> Erstellen einer MDT-Datenbank  
 Folgende Windows PowerShell-Befehle erstellen eine neue MDT-Datenbank auf dem Server *\_Bereitstellungsserver* für die Bereitstellungsfreigabe „Production“. Die Datenbankverbindung wird über TCP\/IP hergestellt.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-MDTDatabase -path "DS002:" -SQLServer "DeploymentServer" -Netlib "DBMSSOCN" -Database "MDT2010" -SQLShare "DB_Connect" -Force -Verbose  
    ```  

###  <a name="CreateSelectProfile"></a> Erstellen eines Auswahlprofils  
 Folgende Windows PowerShell-Befehle erstellen ein neues Auswahlprofil für eine Anwendung.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Selection Profiles" -enable "True" -Name "Applications" -Comments "" -Definition "<SelectionProfile><Include path="Applications" /></SelectionProfile>" -ReadOnly "False" -Verbose  
    ```  

###  <a name="UpdatingDeployShare"></a> Aktualisieren einer Bereitstellungsfreigabe  
 Folgende Windows PowerShell-Befehle führen ein Update für die Bereitstellungsfreigabe „Production“ durch, die sich unter D:\\Production Deployment Share befindet.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   Update\-MDTDeploymentShare \-path "DS002:" \-Verbose  

###  <a name="CreateLinkedDeployShare"></a> Erstellen einer verknüpften Bereitstellungsfreigabe  
 Folgende Windows PowerShell-Befehle erstellen eine Bereitstellungsfreigabe, die mit der Bereitstellungsfreigabe „Production“ verknüpft ist und sich unter der Freigabe \\\\*Name\_des\_Remoteservers*\\Deployment$ befindet. Das Auswahlprofil „Everything“ wird verwendet, um zu bestimmen, welche Inhalte in die verknüpfte Bereitstellungsfreigabe repliziert werden. Der Inhalt der Bereitstellungsfreigabe „Production“ wird mit dem Inhalt zusammengeführt, der bereits in der Freigabe \\\\*Name\_des\_Remoteservers*\\Deployment$ vorhanden ist.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Linked Deployment Shares" -enable "True" -Name "LINKED001" -Comments "" -Root "\\RemoteServerName\Deployment$" -SelectionProfile "Everything" -Replace "False" -Verbose  
    ```  

###  <a name="UpdatingLinkedDeployShare"></a> Aktualisieren einer verknüpften Bereitstellungsfreigabe  
 Folgende Windows PowerShell-Befehle aktualisieren die Bereitstellungsfreigabe „LINKED001“.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Replicate-MDTContent -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="DeleteLinkedDeployShare"></a> Löschen einer verknüpften Bereitstellungsfreigabe  
 Folgende Windows PowerShell-Befehle löschen die Bereitstellungsfreigabe „LINKED001“.  

-   Add\-PSSnapIn Microsoft.BDD.PSSnapIn  

-   ```  
    Remove-item -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="CreateMedia"></a> Erstellen von Medien  
 Folgende Windows PowerShell-Befehle erstellen einen Quellordner, der die Inhalte enthält, die zum Erstellen von startbaren Medien verwendet werden. Die Bereitstellungsfreigabe „Production“ wird als Quelle verwendet. Das Auswahlprofil „Everything“ bestimmt, welche Inhalte im Inhaltsordner des Mediums platziert werden sollen. Die Datei „LiteTouchMedia.iso“ wird erstellt, wenn das Medium generiert wird. Das Medium unterstützt x86- und x64-Plattformen.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Media" -enable "True" -Name "MEDIA001" -Comments "some comment here" -Root "D:\Media" -SelectionProfile "Everything" -SupportX86 "True" -SupportX64 "True" -GenerateISO "True" -ISOName "LiteTouchMedia.iso" -Verbose  
    ```  

-   ```  
    New-PSDrive -Name "MEDIA001" -PSProvider "MDTProvider" -Root "D:\Media\Content" -Description "Embedded media deployment share" -Force -Verbose  
    ```  

###  <a name="GenerateMedia"></a> Generieren von Medien  
 Folgender Windows PowerShell-Befehl erstellt die Datei „LiteTouchMedia.iso“ unter D:\\Media. Diese verwendet die Inhalte des Quellordners des Mediums „MEDIA001“.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Generate-MDTMedia -path "DS002:\Media\MEDIA001" -Verbose  
    ```  

###  <a name="DeleteMedia"></a> Löschen von Medien  
 Folgende Windows PowerShell-Befehle löschen das Medium „MEDIA001“ aus der Bereitstellungsfreigabe „Production“.  

```  
Remove-item -path "DS002:\Media\MEDIA001" -Verbos  
```  

## <a name="delaying-domain-join-to-avoid-application-of-group-policy-objects"></a>Verzögern des Domänenbeitritts zum Verhindern der Anwendung von Gruppenrichtlinienobjekten  
 Bei Gruppenrichtlinien handelt es sich um eine umfangreiche und flexible Technologie, die die Möglichkeit bietet, eine große Anzahl von AD DS-Computern (Active Directory Domain Services) und -Benutzerobjekten über ein zentrales 1:n-Modell effizient zu verwalten. Die Einstellungen für Gruppenrichtlinien sind in einem Gruppenrichtlinienobjekt (Group Policy Object, GPO) enthalten und mit mindestens einem AD DS-Dienstcontainer verknüpft, z.B. mit einer Website, Domäne oder Organisationseinheit (OE).  

 Einige Organisationen verfügen über restriktive Einstellungen für Gruppenrichtlinien, die während der Bereitstellung von Betriebssystemen Probleme verursachen können. Folgende Einstellungen für Gruppenrichtlinien können beispielsweise einen automatisierten Anmeldevorgang unterbrechen:  

-   Einschränkungen für die automatische Anmeldung  

-   Umbenennung des Administratorkontos  

-   Rechtliche Banner und Beschriftungen  

-   Restriktive Sicherheitsrichtlinien (z.B. die SSLF-Richtlinie (Specialized Security – Limited Functionality))  

 Eine Option zur Umgebung der Probleme, die ein GPO während der Bereitstellung verursachen kann, besteht darin, dass die Computer der Domäne im Bereitstellungsprozess so spät wie möglich beitreten. Dieser Beitritt kann mithilfe eines benutzerdefinierten Tasksequenzschritts durchgeführt werden, der das Skript „ZTIDomainJoin.wsf“ ausführt.  

 Das Skript „ZTIDomainJoin.wsf“ verwendet die Eigenschaften **DomainAdmin**, **DomainAdminDomain**, **DomainAdminPassword**, **JoinDomain** und **MachineObjectOU**, um den Domänenbeitritt des Zielcomputers durchzuführen Sie können diese Eigenschaften deklarieren, indem Sie den Windows-Bereitstellungs-Assistenten, die Regeln für Bereitstellungsfreigaben, die MDT-Datenbank und die Regeln für Configuration Manager-Computer und -Sammlungen verwenden. Das verwendete Konto muss über die erforderlichen Rechte zum Erstellen und Löschen von Computerobjekten in der Domäne verfügen.  

 In der Regel aktualisiert das Skript „ZTIConfigure.wsf“ die Datei „Unattend.xml“ oder „Unattend.txt“ mit den Werten, die diese Eigenschaften angeben. Diese Einstellungen werden dann vom Programm „Windows Setup“ analysiert, und das System versucht, einen Domänenbeitritt frühzeitig im Bereitstellungsprozess vorzunehmen. Dadurch unterliegt der Zielcomputer den Einstellungen, die in den GPOs der Domäne angegeben sind, und der Bereitstellungsprozess kann fehlschlagen.  

 Sie können bestimmte Elemente aus der Datei „Unattend.xml“ entfernen, um den Domänenbeitritt des Zielcomputers während des Bereitstellungsprozesses absichtlich zu verzögern. Das Skript „ZTIConfigure.wsf“ wird das Schreiben von Eigenschaften in die Datei „Unattend.xml“ überspringen, wenn das zugeordnete Eigenschaftselement in der Datei nicht vorhanden ist.  

> [!NOTE]
>  Dieses Beispiel für eine Problemumgebung ist nur gültig, wenn Sie eine Bereitstellung für die Betriebssysteme „Windows 7“, „Windows Server 2008“ oder „Windows Server 2008 R2“ durchführen.  

 **Vorbereiten der Datei „Unattend.xml“, damit der Zielcomputer während der Ausführung von Windows Setup nicht versucht, der Domäne beizutreten**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe* > Tasksequenzen > *Tasksequenz*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe und *Tasksequenz* dem Namen der Tasksequenz, die konfiguriert werden soll.  

3.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

4.  Klicken Sie auf der Registerkarte **Betriebssysteminformationen** auf **Edit Unattend.xml** (Unattend.xml bearbeiten).  

     Windows System Image Manager (Windows SIM) wird gestartet.  

5.  Navigieren Sie im Bereich **Antwortdatei** zu **Angeben > Identifizierung > Anmeldeinformationen**. Klicken Sie mit der rechten Maustaste auf **Anmeldeinformationen**, und klicken Sie auf **Löschen**.  

6.  Klicken Sie auf **Ja**.  

7.  Speichern Sie die Antwortdatei, und beenden Sie Windows SIM.  

8.  Klicken Sie im Dialogfeld **Eigenschaften** der Tasksequenz auf **OK**.  

 Wenn das `Credentials`-Element in der Datei „Unattend.xml“ nicht vorhanden ist, kann das Skript „ZTIConfigure.wsf“ die Informationen für den Domänenbeitritt in „Unattend.xml“ nicht auffüllen. Dadurch wird Windows Setup daran gehindert, einen Domänenbeitritt durchzuführen.  

 **Hinzufügen einer Tasksequenz, die den Domänenbeitritt des Zielcomputers durchführt**  

1.  Klicken Sie auf **Start**, und zeigen Sie anschließend auf **Alle Programme**. Zeigen Sie auf **Microsoft Development Toolkit**, und klicken Sie auf **Deployment Workbench**.  

2.  Navigieren Sie in der Konsolenstruktur der Deployment Workbench zu Deployment Workbench > Bereitstellungsfreigaben > *Bereitstellungsfreigabe* > Tasksequenzen > *Tasksequenz*. Hierbei entspricht *Bereitstellungsfreigabe* der zu konfigurierenden Bereitstellungsfreigabe und *Tasksequenz* dem Namen der Tasksequenz, die konfiguriert werden soll.  

3.  Klicken Sie im Aktionsbereich auf **Eigenschaften**.  

4.  Navigieren Sie auf der Registerkarte **Tasksequenz** zum Knoten „Zustandswiederherstellung“, und erweitern Sie diesen.  

5.  Überprüfen Sie, dass der Tasksequenzschritt **Recover From Domain** (Aus Domäne wiederherstellen) vorhanden ist. Wenn dies der Fall ist, fahren Sie mit Schritt 9 fort.  

6.  Klicken Sie im Dialogfeld **Eigenschaften** der Tasksequenz auf **Hinzufügen**, navigieren Sie zu **Eigenschaften**, und klicken Sie auf **Recover From Domain** (Aus Domäne wiederherstellen).  

7.  Fügen Sie den Tasksequenzschritt **Recover From Domain** (Aus Domäne wiederherstellen) zum Tasksequenz-Editor hinzu. Überprüfen Sie, dass der Schritt sich in der Tasksequenz an der gewünschten Position befindet.  

8.  Überprüfen Sie, dass die Einstellungen für den Tasksequenzschritt **Recover From Domain** (Aus Domäne wiederherstellen) Ihren Anforderungen entsprechend konfiguriert sind.  

9. Klicken Sie im Dialogfeld **Eigenschaften** der Tasksequenz auf **OK**, um die Tasksequenz zu speichern.
