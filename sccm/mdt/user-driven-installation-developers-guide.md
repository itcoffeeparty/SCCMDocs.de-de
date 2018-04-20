---
title: Benutzergesteuerte Installation
titleSuffix: Microsoft Deployment Toolkit
description: 'Entwicklerleitfaden zur benutzerdefinierten Installation des Microsoft Deployment Toolkits 2013. '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: a2b3a3a0-7b81-4191-b1f9-c618e59347c3
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 434178f100c32a4188ecf5283066f9332035f761
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2018
---
# <a name="user-driven-installation---developers-guide"></a>Entwicklerleitfaden: Benutzergesteuerte Installation
Mithilfe der benutzergesteuerten Installation (User Driven Installation, UDI) wird die Bereitstellung von Windows®-Clientbetriebssystemen wie Windows 8.1 für Computer vereinfacht, die das Feature der Betriebssystembereitstellung in Microsoft System Center® 2012 R2 Configuration Manager verwenden. Die UDI ist Bestandteil des Microsoft Deployment Toolkits (MDT).  

## <a name="introduction"></a>Einführung  
 Wenn Sie mithilfe des Betriebssystembereitstellungsfeatures ein Betriebssystem bereitstellen möchten, müssen Sie in der Regel sämtliche Angaben machen, die für die Bereitstellung benötigt werden. Diese Informationen werden in Konfigurationsdateien oder in Datenbanken konfiguriert (z.B. in der CustomSettings.ini-Datei oder der MDT-Datenbank [MDT DB]). Sie müssen sämtliche Konfigurationseinstellungen bereitstellen, bevor Sie mit der Bereitstellung beginnen können.  

 Die UDI umfasst eine von einem Assistenten gesteuerte Schnittstelle, über die Sie Konfigurationsinformationen zur Verfügung stellen können, bevor Sie die Bereitstellung vornehmen. So können Sie erst generische Tasksequenzen für die Betriebssystembereitstellung erstellen und anschließend im Rahmen der Bereitstellung computerspezifische Informationen zur Verfügung stellen. Dadurch wird der Bereitstellungsprozess flexibler.  

### <a name="target-audience"></a>Zielgruppe  
 Dieser Leitfaden richtet sich an Entwickler, die benutzerdefinierte Seiten für den UDI-Assistenten sowie Editors für benutzerdefinierte Assistentenseiten für den Designer des UDI-Assistenten erstellen. Ein grobes Verständnis der Entwicklung von Windows-Anwendungen mithilfe der folgenden Elemente wird vorausgesetzt:  

-   C++ – wird zum Erstellen der benutzerdefinierten Assistentenseiten verwendet  

-   Microsoft .NET Framework – wird zum Erstellen der Editors für benutzerdefinierte Assistentenseiten verwendet  

-   Windows Presentation Foundation (WPF) – wird zum Erstellen der Editors für benutzerdefinierte Assistentenseiten verwendet  

-   Von WPF unterstützte Sprachen wie C#, C++ oder Microsoft Visual Basic® .NET – werden zum Erstellen der Editors für benutzerdefinierte Assistentenseiten verwendet  

### <a name="about-this-guide"></a>Über diesen Leitfaden  
 Dieser Leitfaden enthält alle nötigen Referenzinformationen, die Ihnen bei der Anpassung der UDI für Ihre Organisation helfen sollen. Es werden keine Informationen zur Verwaltung oder zu Vorgängen gegeben. Das heißt z.B., dass weder die Installation des MDT (das die UDI beinhaltet) noch die Konfiguration der UDI zur Bereitstellung von Betriebssystemen und Anwendungen noch die Bereitstellung mithilfe des UDI-Assistenten erläutert werden. Weitere Informationen zu diesen Themen finden in der UDI-Referenz unter *Verwenden des Microsoft Deployment Toolkits* (im Lieferumfang des Microsoft Deployment Toolkits enthalten).  

## <a name="udi-development-overview"></a>Übersicht: UDI-Entwicklung  
 Mithilfe der UDI-Entwicklung können Sie die Features erweitern, die die UDI mit sich bringt. In der Regel sollten Sie die UDI-Entwicklung verwenden, wenn Sie zusätzliche Informationen sammeln möchten, die während der UDI-Bereitstellung verarbeitet werden. Diese Informationen werden normalerweise als Tasksequenzvariablen gespeichert, die von den einzelnen Tasksequenzschritten in einer UDI-Tasksequenz in Configuration Manager gelesen werden.  

### <a name="udi-architecture"></a>UDI-Architektur  
 Das allgemeine Ziel der UDI-Entwicklung ist das Erstellen von benutzerdefinierten Assistentenseiten, die im UDI-Assistenten angezeigt werden können. Sie können mithilfe der benutzerdefinierten Assistentenseiten die bereits vorhanden UDI-Features erweitern, sodass sie den Anforderungen Ihres Unternehmens und den technischen Standards entsprechen. Auf einer benutzerdefinierten Assistentenseite werden Informationen gesammelt, die die durch die UDI bereitgestellten Assistentenseiten ergänzen bzw. ersetzen.  

 In Abbildung 1 wird die Beziehung zwischen dem Designer des UDI-Assistenten und dem UDI-Assistenten dargestellt.  

 ![UDIDevelopersGuide1](media/UDIDevelopersGuide1.jpg "UDIDevelopersGuide1")  
Abbildung 1: Beziehung zwischen dem UDI-Assistenten und dem Designer des UDI-Assistenten  

 **Abbildung 1: Beziehung zwischen dem UDI-Assistenten und dem Designer des UDI-Assistenten**  

 Auf der Konzeptebene umfasst die UDI-Entwicklung die Erstellung von  

-   **benutzerdefinierten Assistentenseiten.** Die Assistentenseiten werden im UDI-Assistenten angezeigt. Sie enthalten die Informationen, die für den Bereitstellungsprozess erforderlich sind. Die Seiten für den Assistenten werden in Microsoft Visual Studio® mit C++ erstellt. Die benutzerdefinierten Assistentenseiten werden als DLLs implementiert, die der UDI-Assistent liest. Das UDI Software Development Kit (SDK) enthält ein Beispiel zum Erstellen von benutzerdefinierten Assistentenseiten.  

-   **Editors für benutzerdefinierte Assistentenseiten.** Editors für benutzerdefinierte Assistentenseiten werden verwendet, um das Verhalten Ihrer benutzerdefinierten Assistentenseite zu konfigurieren. Die Editors für benutzerdefinierte Assistentenseiten werden als DLLs implementiert, die der Designer des UDI-Assistenten liest. Sie können diese Editors mithilfe der folgenden Elemente erstellen:  

    -   [WPF](http://msdn.microsoft.com/library/ms754130.aspx) Version 4.0  

    -   [Microsoft Prism](http://compositewpf.codeplex.com/) Version 4.0  

    -   [Microsoft Unity-Anwendungsblock](http://unity.codeplex.com/) (Unity) Version 2.1  

     Das MDT umfasst alle Assemblys, die benötigt werden, um einen Editor für benutzerdefinierte Assistentenseiten zu erstellen, die im Designer des UDI-Assistenten verwendet werden können. Das UDI SDK enthält ein Beispiel für die Vorgehensweise beim Erstellen von Editors für benutzerdefinierte Assistentenseiten.  

 Außerdem verarbeitet der Designer des UDI-Assistenten Konfigurationsdateien, die den jeweiligen Editor für benutzerdefinierte Assistentenseiten verwenden. Erstellen Sie die Konfigurationsdateien des Editors für benutzerdefinierte Assistentenseiten im Rahmen des Prozesses, in dem Sie benutzerdefinierte Assistentenseiten und Editors für benutzerdefinierte Assistentenseiten erstellen. Der Designer des UDI-Assistenten erstellt die XML-Informationen, die die Konfigurationsdatei für den UDI-Assistenten benötigt, sowie eine zugehörige APP-Datei.  

### <a name="preparing-the-udi-development-environment"></a>Vorbereiten der UDI-Entwicklungsumgebung  
 Bevor Sie mit dem Erstellen Ihrer eigenen benutzerdefinierten Assistentenseiten und den Editors für diese Seiten beginnen können, müssen Sie die folgenden Schritte ausführen, um die UDI-Entwicklungsumgebung vorzubereiten:  

1.  Überprüfen Sie, ob die unter [Erfüllen der Voraussetzung für die UDI-Entwicklungsumgebung](#PrepareUDIDevelopmentEnvironmentPrerequisites) beschriebenen Voraussetzungen erfüllt sind.  

2.  Konfigurieren Sie die UDI-Entwicklungsumgebung wie unter [Konfigurieren der UDI-Entwicklungsumgebung](#ConfigureUDIDevelopmentEnvironment) beschrieben.  

3.  Überprüfen Sie, ob die UDI-Entwicklungsumgebung wie unter [Überprüfen der UDI-Entwicklungsumgebung](#VerifyUDIDeploymentEnvironment) beschrieben konfiguriert ist.  

####  <a name="PrepareUDIDevelopmentEnvironmentPrerequisites"></a> Erfüllen der Voraussetzungen für die UDI-Entwicklungsumgebung  
 Sie müssen die folgenden Schritte ausführen, um die Voraussetzungen für die UDI-Entwicklungsumgebung zu erfüllen:  

1.  Überprüfen Sie, ob Sie die unter [Erfüllen der Hardwarevoraussetzungen für die UDI-Entwicklungsumgebung](#PrepareUDIDevelopmentEnvironmentHardwarePrerequisites) beschriebenen Hardwarevoraussetzungen erfüllt haben.  

2.  Überprüfen Sie, ob die unter [Erfüllen der Softwarevoraussetzungen für die UDI-Entwicklungsumgebung](#PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites) beschriebenen Softwarevoraussetzungen für die UDI-Entwicklung erfüllt sind.  

#####  <a name="PrepareUDIDevelopmentEnvironmentHardwarePrerequisites"></a> Erfüllen der Hardwarevoraussetzungen für die UDI-Entwicklungsumgebung  
 Für die UDI-Entwicklungsumgebung gelten die gleichen Hardwarevoraussetzungen wie für die Microsoft Visual Studio 2010-Version, die Sie verwenden. Weitere Informationen zu diesen Voraussetzungen finden Sie in den Systemanforderungen der einzelnen Versionen unter [Visual Studio 2010-Produkte](http://www.microsoft.com/visualstudio/products/2010-editions).  

#####  <a name="PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites"></a> Erfüllen der Softwarevoraussetzungen für die UDI-Entwicklungsumgebung  
 Es gelten die folgenden Softwarevoraussetzungen für die UDI-Entwicklungsumgebung:  

-   Sie können alle Windows-Betriebssystemversionen verwenden, die Visual Studio 2010 unterstützt (Windows 7 oder Windows Server® 2008 R2 werden empfohlen).  

     Sie benötigen ein Windows-Betriebssystem, das die Prozessorarchitektur unterstützt, für die Sie entwickeln möchten. Sie können unter Verwendung eines 64-Bit-Betriebssystems sowohl für 32-Bit- als auch für 64-Bit-Betriebssysteme eine UDI-Entwicklung durchführen. Wenn Sie ein 32-Bit-Betriebssystem verwenden, können Sie nur eine UDI-Entwicklung für 32-Bit-Betriebssysteme durchführen. Daher sollten Sie ein 64-Bit-Betriebssystem verwenden.  

    > [!NOTE]
    >  Intel Itanium-Versionen (IA-64) von Windows-Betriebssystemen werden für UDI-Entwicklungsumgebungen nicht unterstützt.  

     Weitere Informationen zu den Betriebssystemen, die Visual Studio 2010 unterstützt, finden Sie in den Systemanforderungen der einzelnen Versionen unter [Visual Studio 2010-Produkte](http://www.microsoft.com/visualstudio/products/2010-editions).  

-   Microsoft .NET Framework-Version 4.0 (von Visual Studio 2010 erfordert)  

-   C++ (die für das Erweitern von UDI-Assistentenseiten verwendete Sprache)  

-   Andere von WPF unterstützte Sprachen wie C#, Visual Basic .NET oder C++ bzw. Common Language Infrastructure, die verwendet werden, um Editors für Assistentenseiten des Designers des UDI-Assistenten zu erweitern.  

    > [!NOTE]
    >  Der Beispielquellcode für die Editors für Assistentenseiten des Designers des UDI-Assistenten ist in C# geschrieben. Installieren Sie C#, wenn Sie den Beispielquellcode verwenden möchten.  

####  <a name="ConfigureUDIDevelopmentEnvironment"></a> Konfigurieren der UDI-Entwicklungsumgebung  
 Wenn die Voraussetzungen für die UDI-Entwicklungsumgebung erfüllt sind, führen Sie die folgenden Schritte aus, um die UDI-Entwicklungsumgebung zu konfigurieren:  

1.  Installieren Sie Visual Studio 2010.  

     Installieren Sie C++ sowie alle anderen Sprachen, die WPF unterstützt.  

    > [!NOTE]
    >  Der Beispielquellcode für die Editorseiten des Designers des UDI-Assistenten ist in C# geschrieben. Installieren Sie C#, wenn Sie den Beispielquellcode verwenden möchten.  

     Weitere Informationen zum Installieren von Visual Studio 2010 finden Sie unter [Installieren von Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx).  

2.  Install Sie das MDT.  

     Weitere Informationen zum Installieren des MDT finden Sie in dem MDT-Dokument *Verwenden des Microsoft Deployment Toolkits* im Abschnitt „Installieren des MDT oder ein Upgrade ausführen“.  

3.  Erstellen Sie im Windows-Explorer einen *local_folder*-Ordner. Dabei kann es sich um einen beliebigen Ordner handeln, der sich auf dem Entwicklungscomputer auf dem lokalen Laufwerk befindet.  

4.  Kopieren Sie den Ordner „*installation_folder*\SDK“ in den Ordner *local_folder*. Dabei ist der Ordner *installation_folder* der Ordner, in dem Sie das MDT installiert haben, und der Ordner *local_folder* ist der Order, der sich auf dem Entwicklungscomputer auf dem lokalen Laufwerk befindet.  

     Sie müssen den SDK-Ordner an einen anderen Ort kopieren, weil das MDT in dem Ordner mit den Programmdateien installiert wird, in den nur Personen mit erweiterten Berechtigungen schreiben können. Wenn Sie den SDK-Ordner an einen anderen Ort kopieren, können Sie die Dateien in dem SDK-Ordner auch ohne erweiterte Berechtigungen ändern.  

5.  Kopieren Sie den Ordner „*installation_folder*\Templates\Distribution\Tools“ in den Ordner *local_folder*. Dabei ist der Ordner *installation_folder* der Ordner, in dem Sie das MDT installiert haben, und *local_folder* der Ordner, den Sie zuvor erstellt haben.  

6.  Benennen Sie den Ordner „*local_folder*\Tools“ in „*local_folder*\OSDSetupWizard“ um. Dabei ist *local_folder* der Ordner, den Sie zuvor erstellt haben.  

     Wenn Sie diese Schritte ausgeführt haben, sollte die Ordnerstruktur der Unterordner von *local_folder* wie in Abbildung 2 dargestellt aussehen. Dabei ist *local_folder* der Ordner, den Sie zuvor erstellt haben und der als *UDIDevelopment* in der Abbildung dargestellt wird.  

     ![UDIDevelopersGuide2](media/UDIDevelopersGuide2.jpg "UDIDevelopersGuide2")  
Abbildung 2: Ordnerstruktur für die UDI-Entwicklung  

     **Abbildung 2: Ordnerstruktur für die UDI-Entwicklung**  

####  <a name="VerifyUDIDeploymentEnvironment"></a> Überprüfen der UDI-Entwicklungsumgebung  
 Nachdem die UDI-Entwicklungsumgebung konfiguriert wurde, überprüfen Sie, ob dabei Probleme entstanden sind, indem Sie sicherstellen, dass die Beispielprojekte einwandfrei in Visual Studio 2010 erstellt werden.  

 Überprüfen Sie Folgendes, um sicherzustellen, dass die UDI-Entwicklungsumgebung richtig erstellt wurde:  

-   Wird das SamplePage-Projekt wie unter [Überprüfen, ob das SamplePage-Projekt richtig erstellt wird](#VerifySamplePageProjectBuildsCorrectly) beschrieben erstellt?  

-   Wird das SampleEditor-Projekt wie unter [Überprüfen, ob das SampleEditor-Projekt richtig erstellt wird](#VerifySampleEditorProjectBuildsCorrectly) beschrieben erstellt?  

#####  <a name="VerifySamplePageProjectBuildsCorrectly"></a> Überprüfen, ob das SamplePage-Projekt richtig erstellt wird  
 Das SamplePage-Projekt ist ein Beispiel für die Vorgehensweise beim Erstellen einer benutzerdefinierten Seite für den UDI-Assistenten. Weitere Informationen zu dem SamplePage-Projekt finden Sie im Abschnitt [Überprüfen der SamplePage-Projektmappe in Visual Studio](#ReviewSamplePageVisualStudioSolution).  

 **So überprüfen Sie, ob das SamplePage-Projekt richtig erstellt wird**  

1.  Starten Sie Visual Studio 2010.  

2.  Öffnen Sie das SamplePage-Projekt.  

     Das SamplePage-Projekt befindet sich in dem Ordner „*local_folder*\SDK\UDI\SamplePage“. Dabei ist *local_folder* der Ordner, den Sie zuvor erstellt haben.  

3.  Klicken Sie in Visual Studio 2010 im Projektmappen-Explorer mit der rechten Maustaste auf das SamplePage-Projekt, und klicken Sie anschließend auf **Eigenschaften**.  

     Dann wird das Dialogfeld **SamplePage Property Pages** (SamplePage-Eigenschaftenseite) angezeigt.  

4.  Gehen Sie in diesem Dialogfeld zu „Konfigurationseigenschaften“ > „Debuggen“.  

5.  Klicken Sie in den Debugeigenschaften unter **Konfiguration** auf **Alle Konfigurationen**.  

6.  Geben Sie in den Debugeigenschaften unter **Befehl** **$(TargetDir)\OSDSetupWizard.exe** ein.  

7.  Geben Sie in den Debugeigenschaften unter **Arbeitsverzeichnis** **$(TargetDir)** ein.  

8.  Gehen Sie im Dialogfeld **SamplePage Property Pages** (SamplePage-Eigenschaftenseite) zu „Konfigurationseigenschaften“ > „Buildereignisse“ > „Postbuildereignis“.  

9. Geben Sie in den Postbuildereigniseigenschaften unter **Befehlszeile** Folgendes ein:  

    ```  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\*.*" "$(TargetDir)"  
    xcopy /y /i "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\en-us" "$(TargetDir)en-us"  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\OSDResults\Images\UDI_Wizard_Banner.bmp" "$(ProjectDir)header.bmp"  
    copy /y "$(ProjectDir)Config.xml" "$(TargetDir)”  
    copy /y "$(ProjectDir)header.bmp" "$(TargetDir)header.bmp"  
    ```  

10. Klicken Sie im Dialogfeld **SamplePage Property Pages** (SamplePage-Eigenschaftenseite) auf **OK**.  

11. Speichern Sie das Projekt.  

12. Klicken Sie im Menü **Debuggen** auf **Debuggen starten**.  

     Dann wird das Dialogfeld **Microsoft Visual Studio** angezeigt, das Sie darüber informiert, dass die Quelle nicht mehr aktuell ist, und Sie fragt, ob Sie das Projekt erstellen möchten.  

13. Klicken Sie im Dialogfeld **Microsoft Visual Studio** auf **Ja**.  

     Dann wird das Dialogfeld **No Debugging Informationen** (Keine Debuginformationen) angezeigt, das Sie darüber informiert, dass für die OSDSetupWizard.exe-Datei keine Debuginformationen verfügbar sind.  

14. Klicken Sie im Dialogfeld **No Debugging Informationen** (Keine Debuginformationen) auf **Ja**.  

     Der UDI-Assistent wird geöffnet, und die benutzerdefinierte Assistentenseite wird angezeigt.  

15. Überprüfen Sie, ob Sie unter **Choose your location** (Ihren Speicherort auswählen) einen Wert auswählen können.  

16. Klicken Sie in dem Formular **Wizard with sample page**(Assistent mit Beispielseite) auf **Abbrechen**.  

     Dann wird das Dialogfeld **Assistenten abbrechen** angezeigt.  

17. Klicken Sie im Dialogfeld **Assistenten abbrechen** auf **Ja**.  

18. Schließen Sie Visual Studio 2010.  

#####  <a name="VerifySampleEditorProjectBuildsCorrectly"></a> Überprüfen, ob das SampleEditor-Projekt richtig erstellt wird  
 Das SampleEditor-Projekt ist ein Beispiel für die Vorgehensweise beim Erstellen eines Editors für benutzerdefinierte Assistentenseiten für den Designer des UDI-Assistenten. Weitere Informationen zu dem SampleEditor-Projekt finden Sie im Abschnitt [Überprüfen der SamplePage-Projektmappe in Visual Studio](#ReviewSamplePageVisualStudioSolution).  

 **So überprüfen Sie, ob das SampleEditor-Projekt richtig erstellt wird**  

1.  Starten Sie Visual Studio 2010.  

2.  Öffnen Sie das SampleEditor-Projekt.  

     Das SampleEditor-Projekt befindet sich in dem Ordner „*local_folder*\SDK\UDI\SampleEditor“. Dabei ist *local_folder* der Ordner, den Sie zuvor erstellt haben.  

3.  Wählen Sie in Visual Studio 2010 im Projektmappen-Explorer das SampleEditor-Projekt aus.  

4.  Klicken Sie im Menü **Projekt** auf **Verweis hinzufügen**.  

     Das Dialogfeld **Verweis hinzufügen** wird geöffnet.  

5.  Klicken Sie im Dialogfeld **Verweis hinzufügen** auf die Registerkarte **Durchsuchen**.  

6.  Gehen Sie in der Registerkarte **Durchsuchen** zu *installation_folder*\Bin. Dabei ist *installation_folder* der Ordner, in dem Sie das MDT installiert haben. Wählen Sie die folgenden Dateien aus, und klicken Sie auf **OK**:  

    -   Microsoft.Enterprise.UDIDesigner.Common.dll  

    -   Microsoft.Enterprise.UDIDesigner.DataService.dll  

    -   Microsoft.Enterprise.UDIDesigner.Infrastructure.dll  

    -   Microsoft.Practices.Prism.dll  

    -   Microsoft.Practices.ServiceLocation.dll  

    -   Microsoft.Practices.Unity.dll  

    -   RibbonControlsLibrary.dll  

    > [!NOTE]
    >  Sie können auf der Registerkarte **Durchsuchen** mehrere Dateien auswählen, indem Sie STRG gedrückt halten und die Dateien anklicken.  

7.  Gehen Sie im Projektmappen-Explorer zu „SampleEditor“ > „Verweise“.  

8.  Stellen Sie sicher, dass für keinen der Verweise Warnungen oder Fehler angezeigt werden.  

9. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das SampleEditor-Projekt, und klicken Sie dann auf **Eigenschaften**.  

     Dann wird das Dialogfeld **SampleEditor Property Pages** (SampleEditor-Eigenschaftenseite) angezeigt.  

10. Klicken Sie im Dialogfeld **SampleEditor Property Pages** (SampleEditor-Eigenschaftenseite) auf die Registerkarte **Debuggen**.  

11. Klicken Sie auf der Registerkarte **Debuggen** auf **Externes Programm starten**.  

12. Geben Sie unter **Externes Programm starten** ***installation_folder\Bin\UDIDesigner.exe*** ein, und klicken Sie auf **OK**. Dabei ist *installation_folder* der Ordner, in dem Sie das MDT installiert haben.  

    > [!TIP]
    >  Klicken Sie auf die Schaltfläche mit den Auslassungspunkten (...), um den Ordner zu durchsuchen, und klicken Sie auf die UDIDesigner.exe-Datei.  

13. Klicken Sie im Menü **Datei** auf **Alles speichern**.  

14. Kopieren Sie die Datei „*local_folder*\SDK\SamplePage\SamplePage.dll.config“ in den Ordner „*installation_folder*\Bin\Config“. Dabei ist *local_folder* der Ordner, den Sie zuvor im Rahmen der Konfiguration auf dem Entwicklungscomputer erstellt haben, und *installation_folder* ist der Ordner, in dem Sie das MDT installiert haben.  

15. Klicken Sie in Visual Studio 2010 im Menü **Debuggen** auf **Debuggen starten**.  

     Dann wird der Designer des UDI-Assistenten gestartet.  

16. Klicken Sie im Designer des UDI-Assistenten auf dem Menüband auf **Öffnen**.  

     Dann wird das Dialogfeld **Öffnen** angezeigt.  

17. Öffnen Sie im Dialogfeld **Öffnen** die Datei unter „*local_folder*\SDK\SamplePage\SamplePage\Config.xml“. Dabei ist *local_folder* der Ordner, den Sie zuvor im Rahmen der Konfiguration auf dem Entwicklungscomputer erstellt haben.  

     Die Config.xml-Datei wird geöffnet, und im Detailbereich wird die benutzerdefinierte Gruppe [StageGroup](#StageGroup) angezeigt.  

18. Klicken Sie im Detailbereich auf die Registerkarte **Konfigurieren**.  

19. Überprüfen Sie die Konfigurationsinformationen für das Feld **Speicherort** einschließlich der folgenden Elemente:  

    -   Die Schaltfläche **Entsperrt**, mit der Sie das Feld **Speicherort** aktivieren bzw. deaktivieren  

    -   Das Feld **Standardwert**, in dem Sie einen Standardwert eingeben, der auf dem Feld **Speicherort** angezeigt werden soll  

    -   Das Feld **Name, der auf der Seite „Zusammenfassung“ angezeigt wird**, in das Sie einen Titel eingeben, der auf der Seite **Zusammenfassung** angezeigt wird.  

    -   Das Listenfeld **Speicherort**, auf dem eine Liste möglicher Speicherorte angezeigt wird  

20. Schließen Sie den Designer des UDI-Assistenten.  

21. Schließen Sie Visual Studio 2010.  

## <a name="reviewing-the-udi-sdk-examples"></a>Überprüfen der UDI SDK-Beispiele  
 Bevor Sie mit der Entwicklung beginnen, sollten Sie die in dem UDI SDK enthaltenen Beispiele überprüfen. Verwenden Sie die in diesem Leitfaden enthaltenen Informationen und den Quellcode in den Beispielen, um Ihre eigenen benutzerdefinierten UDI-Assistentenseiten und Editors für Assistentenseiten zu erstellen.  

 Sehen Sie sich die UDI SDK-Beispiele an, und überprüfen Sie Folgendes:  

-   Die Inhalte des SDK-Ordners, den Sie zuvor wie unter [Überprüfen der Inhalte des SDK-Ordners](#ReviewContentsofSDKFolder) beschrieben bei der Installation kopiert haben.  

-   Das Beispiel für eine benutzerdefinierte UDI-Assistentenseite, das unter [Überprüfen der SamplePage-Projektmappe in Visual Studio](#ReviewSamplePageVisualStudioSolution) beschrieben wird.  

-   Das Beispiel für den Editor einer benutzerdefinierten UDI-Assistentenseite, der unter [Überprüfen der SampleEditor-Projektmappe in Visual Studio](#ReviewSampleEditorVisualStudioSolution) beschrieben wird.  

###  <a name="ReviewContentsofSDKFolder"></a> Überprüfen der Inhalte des SDK-Ordners  
 Sie haben im Rahmen der Konfiguration der UDI-Entwicklungsumgebung den SDK-Ordner aus dem Ordner, in dem Sie das MDT installiert haben, in einen anderen von Ihnen erstellten Ordner kopiert. In Tabelle 1 werden die Unterordner des SDK-Ordners einschließlich einer kurzen Beschreibung aufgeführt.  

### <a name="table-1-folders-in-the-udi-sdk"></a>Tabelle 1. Ordner im UDI SDK  

|**Ordner**|**Dieser Ordner enthält**|  
|-|-|  
|Includes|Die C++-Headerdateien, die für das Erstellen von benutzerdefinierten Seiten für den UDI-Assistenten benötigt werden.|  
|Libs|Die C++-Bibliotheksdateien, die mit Ihrer benutzerdefinierten Seite verknüpft werden. Es gibt sowohl 32-Bit- als auch 64-Bit-Versionen der statischen DLLs. **Hinweis:** Es sind keine Itanium-Versionen der Bibliotheken (IA-64) verfügbar.|  
|SampleEditor|Ein Visual Studio-Projekt zum Erstellen eines benutzerdefinierten Editors, der verwendet wird, um die SamplePage-Seite (in C# verfasst) im Designer des UDI-Assistenten zu bearbeiten.|  
|SamplePage|Ein Visual Studio-Projekt zum Erstellen einer benutzerdefinierten UDI-Assistentenseite, die in Visual C++ geschrieben ist.|  

###  <a name="ReviewSamplePageVisualStudioSolution"></a> Überprüfen der SamplePage-Projektmappe in Visual Studio  
 Bevor Sie mit dem Erstellen Ihrer benutzerdefinierten Assistentenseiten und den Editors für diese Seiten beginnen können, müssen Sie die folgenden Tasks ausführen, um die UDI-Entwicklungsumgebung vorzubereiten:  

-   Überprüfen Sie wie unter [Überprüfen des Lebenszyklus der Assistentenseite](#ReviewWizardPageLifeCycle) die Phasen des Lebenszyklus einer UDI-Assistentenseite.  

-   Überprüfen Sie wie unter [Überprüfen des SamplePage-Beispiels](#ReviewSamplePageExample) beschrieben die Visual Studio-Projektmappe zu der SamplePage-Seite im UDI SDK.  

####  <a name="ReviewWizardPageLifeCycle"></a> Überprüfen des Lebenszyklus der Assistentenseite  
 Eine UDI-Assistentenseite verfügt über Methoden, die mit den einzelnen Phasen des Lebenszyklus der Seite übereinstimmen. Sie müssen zum Erstellen Ihrer benutzerdefinierten Assistentenseite diese Methoden mit Ihrem Code überschreiben. In Tabelle 2 sind die Methoden einschließlich kurzer Beschreibungen aufgeführt, die Sie überschreiben müssen. Außerdem wird angegeben, in welcher Phase des Lebenszyklus der Assistentenseite Sie die Methode verwenden sollen.  

### <a name="table-2-methods-in-a-wizard-page-life-cycle"></a>Tabelle 2: Methoden im Lebenszyklus der Assistentenseite  

|**Methode**|**Beschreibung**|  
|-|-|  
|**OnWindowCreated**|Diese Methode wird nur einmal aufgerufen, nachdem das Fenster der Seite erstellt wurde.<br /><br /> Schreiben Sie für diese Methode Code, der die Seite anfänglich initialisiert und der nur einmal ausgeführt werden soll. Verwenden Sie diese Methode beispielsweise, um Felder zu initialisieren oder Konfigurationsinformationen aus den **Setter**-Elementen in der Konfigurationsdatei des UDI-Assistenten zu lesen.|  
|**OnWindowShown**|Diese Methode wird immer dann aufgerufen, wenn eine Seite im UDI-Assistenten angezeigt wird. Sie wird zum ersten Mal aufgerufen, wenn die Seite angezeigt wird, und anschließend immer dann, wenn Sie zu der Seite navigieren, indem Sie im Assistenten auf **Weiter** oder **Zurück** klicken.<br /><br /> Schreiben Sie für diese Methode Code, der die Seite darauf vorbereitet, angezeigt zu werden – also z.B. zum Lesen von Speicher-, Tasksequenz- oder Umgebungsvariablen und anschließend zum Aktualisieren der Seite basierend auf den Änderungen, die möglicherweise an den Variablen vorgenommen werden.|  
|**OnCommonControlEvent**|Diese Methode kann immer dann aufgerufen werden, wenn die Assistentenseite angezeigt wird und eine WM_NOTIFY-Meldung eines untergeordneten Elements (in der Regel häufig verwendete Steuerelemente) erhält.<br /><br /> Schreiben Sie für diese Methode Code, der WM_NOTIFY-Meldungen anhand der Benachrichtigungsmeldung verarbeitet. Sie sollten z.B. auf von einem häufig verwendeten Steuerelement ausgelöste Ereignisse antworten, indem Sie z.B. auf Ereignisse für ein **TreeView**-Steuerelement klicken bzw. doppelklicken.|  
|**OnUnhandledEvent**|Diese Methode wird immer dann aufgerufen, wenn eine nicht verarbeitete Fenstermeldung für eine Assistentenseite angezeigt wird. Über diese Methode können Sie diese Fenstermeldungen, die ansonsten nicht verarbeitet werden würden, abfangen und verarbeiten.<br /><br /> Schreiben Sie für diese Methode Code, der die Fenstermeldungen verarbeitet, die Ihre Assistentenseite betreffen. In der Regel müssen Sie diese Methode nicht überschreiben.|  
|**OnNextClicked**|Diese Methode wird aufgerufen, wenn Sie im Assistenten auf **Weiter** klicken.<br /><br /> Schreiben Sie für diese Methode Code, der alle notwendigen Schritte ausführt, bevor Sie zur nächsten Assistentenseite wechseln, und der z.B. eine Validierung durchführt, die lange dauern kann. Wenn die Validierung fehlschlägt, können Sie die **Weiter**-Anforderung abbrechen und eine Meldung anzeigen.|  
|**OnWindowHidden**|Diese Methode wird immer dann aufgerufen, wenn die Seite ausgeblendet wird, wenn entweder die letzte oder die nächste Assistentenseite angezeigt wird.<br /><br /> Schreiben Sie für diese Methode Code, der sämtliche Aktionen durchführt, bevor die Seite ausgeblendet und eine andere Seite angezeigt wird. In der Regel müssen Sie diese Methode nicht überschreiben.|  

####  <a name="ReviewSamplePageExample"></a> Überprüfen des SamplePage-Beispiels  
 Überprüfen Sie mithilfe der folgenden Liste das SamplePage-Beispiel. Diese Liste enthält die Sequenz von Ereignissen im Rahmen des Lebenszyklus der Assistentenseite des SamplePage-Beispiels:  

1.  Der UDI-Assistent (OSDSetupWizard.exe) liest wie in [Schritt 1: Der UDI-Assistent (OSDSetupWizard.exe) liest die Config.xml-Datei](#UDIWizardReadstheConfigFile) beschrieben die Konfigurationsinformationen aus der Konfigurationsdatei (Config.xml-Datei) des UDI-Assistenten in dem Beispiel.  

2.  Der UDI-Assistent lädt die DLLs, die für jede Assistentenseite erforderlich sind, die wie in [Schritt 2: Der UDI-Assistent lädt die DLL für die benutzerdefinierte Assistentenseite](#UDIWizardLoadstheDLLforCustomWizardPage) beschrieben in der Konfigurationsdatei des UDI-Assistenten aufgeführt sind.  

3.  Der UDI-Assistent zeigt die benutzerdefinierte Assistentenseite an und ermöglicht die in [Schritt 3: Der UDI-Assistent zeigt die benutzerdefinierte Assistentenseite an](#UDIWizardDisplaysCustomWizardPage) beschriebene gewünschte Interaktion von Steuerelementen.  

4.  Wenn die benutzerdefinierte Assistentenseite die Informationen gesammelt hat, können Sie alle notwendigen Tasks ausführen, bevor Sie auf **Weiter** klicken, um wie in [Schritt 4: Auf der benutzerdefinierten Assistentenseite wird auf die Schaltfläche „Weiter“ geklickt](#TheNextButtonisClickedinCustomWizardPage) mit der nächsten Assistentenseite fortzufahren.  

#####  <a name="UDIWizardReadstheConfigFile"></a> Schritt 1: Der UDI-Assistent (OSDSetupWizard.exe) liest die Config.xml-Datei  
 Wenn der UDI-Assistent (OSDSetupWizard.exe) gestartet wird, liest dieser standardmäßig die primäre Konfigurationsdatei (UDIWizard_Config.xml) des UDI-Assistenten.  

> [!NOTE]
>  Das Beispiel verwendet die Config.xml-Datei als die Konfigurationsdatei. Im MDT lautet die Standardkonfigurationsdatei „UDIWizard_Config.xml“. Diese befindet sich im Ordner „Skripts“ im MDT-Dateipaket für die Konfiguration.  

 Sie können die vom UDI-Assistenten verwendete Standardkonfigurationsdatei überschreiben, indem Sie den Tasksequenzschritt des UDI-Assistenten dahingehend verändern, dass dieser den **/definition**-Parameter verwendet. Weitere Informationen zum Überschreiben der Standardkonfigurationsdatei, die der UDI-Assistent verwendet, finden Sie unter „Überschreiben der Konfigurationsdatei, die der UDI-Assistent verwendet“.  

 Die Elemente auf höchster Ebene in der Config.xml-Datei lauten wie folgt:  

-   [DLLs](#DLLs)-Element  

-   [Style](#Style)-Element  

-   [Pages](#Pages)-Element  

-   [StageGroups](#StageGroups)-Element  

 Weitere Informationen zum Schema der Konfigurationsdatei des UDI-Assistenten und zu den einzelnen Elementen finden Sie unter [Schemareferenz zur Konfigurationsdatei des UDI-Assistenten](#UDIWizardConfigurationFileSchemaReference).  

 Der UDI-Assistent überprüft das **DLLs**-Element, damit die DLL-Dateien geladen werden. In dem Beispiel werden zwei DLL-Dateien aufgeführt: „SamplePage.dll“ und „SharedPages.dll“. Diese Dateien müssen sich in demselben Ordner befinden wie die OSDSetupWizard.exe-Datei, nämlich in dem Tools\\*platform*-Ordner, wobei *platform* „x86“ für die 32-Bit-Version und „x64“ für die 64-Bit-Version ist.  

 Der UDI-Assistent überprüft das **Pages**-Element, indem er nach den Seiten sucht, die definiert sind. In diesem Beispiel werden zwei Seiten definiert: die Seite **Custom** und die Seite **SummaryPage**. Das **Type**-Attribut des **Page**-Elements wird in der PageClassIDs.h-Datei definiert und definiert den Typ Ihrer benutzerdefinierten Seite.  

 In dem Beispiel ist **Microsoft.SamplePage.LocationPage** der definierte Typ. Ersetzen Sie für Ihre benutzerdefinierte Seite folgende Elemente, um mögliche Konflikte mit anderen Seiten zu vermeiden, die Sie möglicherweise in der Zukunft erstellen:  

-   Ihren Organisationsnamen anstelle von **Microsoft**.  

-   Ihren Projektnamen anstelle von **SamplePage**.  

-   Den Namen für Ihre benutzerdefinierte Assistentenseite anstelle von **LocationPage**.  

#####  <a name="UDIWizardLoadstheDLLforCustomWizardPage"></a> Schritt 2: Der UDI-Assistent lädt die DLL für die benutzerdefinierte Assistentenseite  
 Wenn der UDI-Assistent Ihre DLL lädt, ruft er die **RegisterFactories**-Funktion auf, die in Ihre DLL-Datei implementiert werden muss. In dem Beispiel ist diese Funktion in die dllmain.ccp-Datei implementiert. Jede Assistentenseite, die Sie erstellen, muss die **RegisterFactories**-Funktion implementieren.  

 Die **RegisterFactories**-Funktion wird verwendet, um die Factoryklasse Ihrer Assistentenseite mit der Klassenfactory für den UDI-Assistenten zu registrieren. *Klassenfactorys* sind Klassen, die Instanzen von anderen Klassen erstellen können. Die **RegisterFactories**-Funktion erstellt eine neue Instanz einer Factoryklasse und übergibt diese Klasse an die Klassenfactoryregistrierung für den UDI-Assistenten, der diese Factoryklasse dem Assistenten zur Verfügung stellt. Der UDI-Assistent sucht nach einer Factoryklasse, die mit einer ID registriert ist, die mit dem **Type**-Attribut des **Page**-Elements der benutzerdefinierten Assistentenseite übereinstimmt.  

 In dem Beispiel wird die ID als **ID_Location** in der PageClassIds.h-Datei (**Microsoft.SamplePage.LocationPage**) definiert und stimmt mit dem **Type**-Attribut für das **Page**-Element in der Config.xml-Datei überein. **ID_Location** wird in der **RegisterFactories**-Funktion, die in die dllmain.ccp-Datei implementiert wurde, als ein Parameter übergeben.  

 Sie können mithilfe der Funktionsvorlage Register_*name* eine Funktion erstellen, um den Erstellvorgang für eine neue Factoryinstanz zu vereinfachen und die neu erstellte Instanz anschließend registrieren. Der **name**-Wert, der über die Register-Funktionsvorlage zur Verfügung gestellt wird, muss die **iClassFactory**-Schnittstelle implementieren. Die [ClassFactoryImpl](#ClassFactoryImplClass)-Klasse verarbeitet die meisten Details zum Implementieren einer Klassenfactory.  

 Sie können auch die **RegisterFactories**-Funktion verwenden, um Tasktypen und Validierungssteuerelementtypen zu registrieren. Weitere Informationen finden Sie unter:  

-   [Erstellen von benutzerdefinierten UDI-Tasks](#CreatingCustomUDITasks)  

-   [Erstellen von benutzerdefinierten UDI-Validierungssteuerelementen](#CreatingCustomUDIValidators)  

> [!NOTE]
>  Das Beispiel enthält und registriert nur eine benutzerdefinierte Assistentenseite. Es umfasst und registriert daher keine benutzerdefinierten Tasks und Validierungssteuerelemente.  

#####  <a name="UDIWizardDisplaysCustomWizardPage"></a> Schritt 3: Der UDI-Assistent zeigt die benutzerdefinierte Assistentenseite an  
 Die benutzerdefinierte Assistentenseite in dem Beispiel wird in der LocationPage.cpp-Datei definiert. Assistentenseiten werden von Vorlagenklassen abgeleitet, die die meisten Funktionen einer Seiten bereitstellen. Alle Assistentenseiten sollten von der Vorlagenklasse [WizardPageImpl](#WizardPageImplTemplateClass) abgeleitet werden, die die Schnittstelle [IWizardPage](#IWizardPageInterface) implementiert. Jede Assistentenseite kann basierend auf den Anforderungen der Seite unterschiedliche optionale Vorlagenklassen und zugehörige Schnittstellen implementieren.  

 Die Vorlagenklasse [WizardPageImpl](#WizardPageImplTemplateClass) verfügt über einige nützliche Schnittstellen, mit denen Sie benutzerdefinierte Assistentenseiten schreiben können. Implementieren Sie die Vorlagenklasse [WizardPageImpl](#WizardPageImplTemplateClass) als Basisklasse für Ihre benutzerdefinierte Assistentenseite.  

 Eine Liste der verfügbaren  

-   Vorlagenklassen für Assistentenseiten finden Sie unter [Hilfsklassen für die Assistentenseite](#WizardPageHelperClasses).  

-   Schnittstellen für die Vorlagenklassen für Assistentenseiten finden Sie unter [Schnittstellen für die Assistentenseite](#WizardPageInterfaces).  

 Die benutzerdefinierte Assistentenseite in dem Beispiel wurde von der Vorlagenklasse [WizardPageImpl](#WizardPageImplTemplateClass) abgeleitet und implementiert die Schnittstelle [IWizardPage](#IWizardPageInterface). Außerdem implementiert die benutzerdefinierte Assistentenseite die Schnittstelle **IFieldCallback**. Sowohl die Assistentenseite als auch die Schnittstelle werden in die LocationPage.cpp-Datei implementiert.  

 Die benutzerdefinierte Beispielassistentenseite überschreibt die folgenden Methoden:  

-   **OnWindowCreated**. Die **OnWindowCreated**-Methode in der benutzerdefinierten Assistentenseite ruft die folgenden Methoden auf:  

    -   [AddField](#AddField). Diese Methode verknüpft das Steuerelement **IDC_COMBO_LOCATION** in der **IDD_LOCATION_PAGE**-Ressource mit dem [Data](#Data)-Element **Speicherort** in der Config.xml-Datei.  

         Sie können auch anstelle der **AddField**-Methode die Methoden [AddRadioGroup](#AddRadioGroup) und [AddToGroup](#AddToGroup) verwenden, um andere Steuerelemente und Verhalten zu unterstützen.  

        > [!NOTE]
        >  Vergewissern Sie sich, dass Sie die Methoden [AddField](#AddField), [AddRadioGroup](#AddRadioGroup) oder [AddToGroup](#AddToGroup) aufrufen, bevor Sie die [InitFields](#InitFields)-Methode aufrufen.  

    -   [InitFields](#InitFields). Verwenden Sie diese Methode, um die Felder (Steuerelemente) zu initialisieren, die Sie zu dem Formular hinzugefügt haben. Bei dem Zeiger der Seite handelt es sich um einen Parameter. In dem Beispiel wird der **this**-Zeiger übergeben. Dieser verweist auf die aktuelle Seite.  

        > [!NOTE]
        >  Wenn Sie die Verwendung des **this**-Zeigers unterstützen möchten, müssen Sie neben den Schnittstellen, die die Vorlagenklasse [WizardPageImpl](#WizardPageImplTemplateClass) unterstützt, auch die Schnittstelle **IFieldCallback** implementieren.  

         Die Schnittstelle **IFieldCallback** ruft die Methode **SetFieldDefault** auf, die verwendet wird, um die Standardwerte für Steuerelemente (ausschließlich der Werte für Textfelder und Kontrollkästchen) festzulegen. In dem Beispiel legt die Methode **SetFieldDefault** basierend auf dem im **Standardelement** angegebenen Standardwert für das [Field](#Field)-Element in der Config.xml-Datei den ersten Index des Kombinationsfeld-Steuerelements fest.  

     Die **OnWindowCreated**-Methode richtet den Formularcontroller mithilfe der Schnittstelle [IFormController](#IFormController-Interface) ein. Weitere Informationen zum Einrichten des Formularcontrollers finden Sie unter [ Einrichten des Formulars](#SettingUptheForm).  

-   **InitLocations**. Diese Methode füllt das Kombinationsfeld über die Liste der Speicherorte in der Config.xml-Datei auf. Das [Data](#Data)-Element und das untergeordnete [DataItem](#DataItem)-Element in der Confg.xml-Datei stellen die Liste mit möglichen Werten bereit.  

-   **OnNextClicked**. Diese Methode führt die folgenden Tasks aus:  

    -   Die Tasksequenzvariable **TSLocation** mit dem im Kombinationsfeld aktivierten Wert wird mithilfe der **SaveFields**-Methode aktualisiert.  

    -   Informationen, die auf der **Zusammenfassungsseite** angezeigt werden, werden mithilfe der **SaveFields**-Methode angezeigt.  

#####  <a name="TheNextButtonisClickedinCustomWizardPage"></a> Schritt 4: Auf der benutzerdefinierten Assistentenseite wird auf die Schaltfläche „Weiter“ geklickt  
 Wenn der Benutzer die Felder auf der benutzerdefinierten Assistentenseite vervollständigt hat, klickt dieser auf **Weiter**. Dann wird die **OnNextClicked**-Methode aufgerufen. Die **OnNextClicked**-Methode führt sämtliche Tasks aus, die notwendig sind, bevor Sie mit der nächsten Assistentenseite fortfahren können – z.B. zeichnet sie alle Konfigurationsänderungen auf, die auf der benutzerdefinierten Assistentenseite vorgenommen werden.  

 Die Außerkraftsetzung für die **OnNextClicked**-Methode wird für die benutzerdefinierte Assistentenseite in die LocationPage.ccp-Datei implementiert. In der **OnNextClicked**-Methode auf der benutzerdefinierten Beispielseite werden die folgenden Methoden aufgerufen:  

1.  [InitSection](#InitSection). Diese Methode initialisiert den Header (Bezeichnung) für die Zusammenfassungsdaten, die auf der **Zusammenfassungsseite** angezeigt werden. In der Regel können Sie diesen Wert mithilfe der **DisplayName()**-Funktion einrichten. Die dieser Beschriftung zugeordneten Daten werden über die [SaveFields](#SaveFields)-Methode gespeichert.  

2.  [SaveFields](#SaveFields). Diese Methode speichert Feldwerte in Tasksequenzvariablen und den Daten, die auf der **Zusammenfassungsseite** angezeigt werden.  

###  <a name="ReviewSampleEditorVisualStudioSolution"></a> Überprüfen der SampleEditor-Projektmappe in Visual Studio  
 Bevor Sie mit dem Erstellen Ihrer eigenen benutzerdefinierten Assistentenseiten und den Editors für diese Seiten beginnen können, müssen Sie die folgenden Schritte ausführen, um die UDI-Entwicklungsumgebung vorzubereiten:  

-   Überprüfen Sie wie unter [Überprüfen der Architektur des Designers des UDI-Assistenten](#ReviewUDIWizardDesignerArchitecture) beschrieben die Architektur des Designers des UDI-Assistenten.  

-   Überprüfen Sie die Komponenten einer UDI-Assistentenseite, die mithilfe der Konfigurationsdatei des UDI-Assistenten wie unter [Überprüfen der konfigurierbaren Komponenten einer UDI-Assistentenseite](#ReviewConfigurableComponentsofUDIWizardPage) beschrieben angepasst werden können.  

-   Überprüfen Sie wie unter [Überprüfen des EditorPage-Beispiels](#ReviewEditorPageExample) beschrieben das im UDI SDK bereitgestellte EditorPage-Beispiel.  

####  <a name="ReviewUDIWizardDesignerArchitecture"></a> Überprüfen der Architektur des Designers des UDI-Assistenten  
 Der Designer des UDI-Assistenten wurde mithilfe von WPF, Prism und Unity entwickelt. Der UDI-Designer wird verwendet, um die Konfigurationsdatei des UDI-Assistenten (UDIWizard_Config.xml) zu bearbeiten, die der UDI-Assistent (OSDSetupWizard.exe) zur Laufzeit liest. Das [Pages](#Pages)-Element in der Konfigurationsdatei des UDI-Assistenten enthält eine Liste von Seiten, die für jede Assistentenseite über ein eigenes [Page](#Page)-Element verfügt.  

 Wenn Sie die Konfigurationseinstellungen für eine Assistentenseite bearbeiten, lädt der Designer des UDI-Assistenten den Editor für benutzerdefinierte Seiten, der dem Typ der Assistentenseite entspricht. Die Editors für benutzerdefinierte Assistentenseiten werden als WPF-Benutzersteuerelemente entwickelt. Die Seiten des Editors für benutzerdefinierte Assistentenseiten verwenden für WPF das Entwurfsmuster [Model-View-ViewModel](http://msdn.microsoft.com/magazine/dd419663.aspx) (MVVM).  

 Mithilfe des MVVM-Entwurfsmusters kann die Benutzeroberfläche, also die Präsentation, von den dargestellten Daten getrennt werden. Bei den Daten handelt es sich um eine Fassade des [Page](#Page)-Elements in der Konfigurationsdatei des UDI-Assistenten (im Beispiel die Config.xml-Datei), auf die über die Eigenschaft [CurrentPage](#CurrentPage) der [IDataService](#IDataService)-Schnittstelle zugegriffen werden kann.  

 Der Designer des UDI-Assistenten verwendet **DependencyAttribute**, um auf die **DataService**-Klasse zugreifen zu können, die auf dem Dependency Injection-Framework in Unity basiert. Weitere Informationen zum Dependency Injection-Framework in Unity finden Sie unter [Inject Some Life into Your Applications—Getting to Know the Unity Application Block (Grundlegendes zum Unity-Anwendungsblock – Gestalten Sie Ihre Anwendungen lebendig)](http://msdn.microsoft.com/library/ff650806.aspx).  

####  <a name="ReviewConfigurableComponentsofUDIWizardPage"></a> Überprüfen der konfigurierbaren Komponenten einer UDI-Assistentenseite  
 Wenn Sie Ihre benutzerdefinierte Assistentenseite erstellen, sind möglicherweise einige der Konfigurationseinstellungen in Form von Code festgelegt und können nicht mehr geändert werden, nachdem Sie die Seite kompiliert haben. Für andere Konfigurationseinstellungen müssen Sie hingegen zulassen, dass die Konfigurationseinstellungen mithilfe des Designers des UDI-Assistenten geändert werden.  

 In der Regel werden die Konfigurationseinstellungen, die Sie mithilfe des Designers des UDI-Assistenten konfigurieren möchten, in der Konfigurationsdatei des UDI-Assistenten (im Beispiel die Config.xml-Datei) gespeichert. Sie können ggf. jedoch auch Ihre eigene separate Konfigurationsdatei erstellen. In der UDIWizard_Config.xml.app-Datei wird z.B. eine eigene Konfigurationsdatei verwendet. Die UDIWizard_Config.xml.app-Datei wird von dem Task zur **Entwicklung von Anwendungen** und dem Typ **ApplicationPage** für Assistentenseiten verwendet.  

 Im Folgenden werden die typischen Konfigurationseinstellungen aufgeführt, die Sie mithilfe des Designers des UDI-Assistenten verwalten können.  

-   **Field**. Über Felder können Benutzer Eingaben machen. Felder werden als [Field](#Field)-Elemente in der Konfigurationsdatei des UDI-Assistenten (UDIWizard_Config.xml) angezeigt, in der die Konfigurationseinstellungen für die einzelnen Felder enthalten sind. Der zugehörige Editor der Assistentenseite muss eine Methode zum Bearbeiten der Konfigurationseinstellungen für das Feld zur Verfügung stellen, das [FieldElementControl](#FieldElementControl) verwendet.  

-   **Eigenschaften**. Mithilfe von Setters können Sie Eigenschaften für Entitäten auf der Seite erstellen – z.B. Seiten im [Page](#Page)-Element, Felder im [Field](#Field)-Element oder Daten in den Elementen [Data](#Data) oder [DataItem](#DataItem). Konfigurieren Sie die Eigenschaften in den [Setter]()-Elementen. Fügen Sie für jede Eigenschaft, die Sie definieren möchten, ein separates [Setter]()-Element hinzu. Bearbeiten Sie mithilfe von [SetterControl](#SetterControl) die Eigenschaften, und konfigurieren Sie mithilfe von anderen Steuerelementen andere [Setter]()-Elemente.  

-   **Daten**. Daten werden verwendet, um Informationen zu speichern, die von der Assistentenseite und anderen Komponenten verwendet werden können. Sie können Daten für Seiten oder Felder definieren, indem Sie die Element [Data](#Data) oder [DataItem](#DataItem) verwenden. Die Daten können flach oder hierarchisch strukturiert sein, wenn die Elemente [Data](#Data) oder [DataItem](#DataItem) richtig verwendet werden. Die Config.xml-Datei in dem Beispiel im SDK stellt dar, wie flache Datenstrukturen erstellt werden.  

 Der von Ihnen erstellte Editor für benutzerdefinierte Assistentenseiten muss diese Konfigurationseinstellungen verwalten können.  

####  <a name="ReviewEditorPageExample"></a> Überprüfen des EditorPage-Beispiels  
 Das EditorPage-Beispiel wird verwendet, um die Konfigurationseinstellungen für die Assistentenseite **SamplePage** in der Konfigurationsdatei des UDI-Assistenten zu konfigurieren. Das EditorPage-Beispiel verfügt über die folgenden primären Komponenten:  

-   Die Benutzeroberfläche zum Konfigurieren der Einstellungen für das Kombinationsfeld **Speicherort**  

-   Die Benutzeroberfläche zum Hinzufügen oder Bearbeiten eines Speicherorts in der Liste mit möglichen Speicherorten, die im Kombinationsfeld **Speicherort** dargestellt werden.  

-   Konfigurationseinstellungen, die aus der Konfigurationsdatei gelesen bzw. in ihr gespeichert werden  

-   Code, der andere Komponenten unterstützt  

 Führen Sie die folgenden Schritte aus, um das EditorPage-Beispiel in Visual Studio zu überprüfen:  

1.  Überprüfen Sie wie unter [Überprüfen des Lade- und Initialisierungsvorgangs des Editors der Assistentenseite](#ReviewWizardPageEditorLoadingInitialization) beschrieben, wie der Editor der **SampleEditor**-Assistentenseite im Designer des UDI-Assistenten geladen und initialisiert wird.  

2.  Überprüfen Sie wie unter [Überprüfen der Benutzeroberfläche, die zum Konfigurieren des Kombinationsfelds „Speicherort“ verwendet wird](#ReviewUserInterfaceUsedtoConfigureLocationComboBox) beschrieben die Benutzeroberfläche, die zum Bearbeiten des Kombinationsfelds **Speicherort** in den Dateien „LocationPageEditor.xaml“ und „LocationPageEditor.xaml.cs“ verwendet wird.  

3.  Überprüfen Sie wie unter [Überprüfen der Benutzeroberfläche, die zum Bearbeiten der Liste möglicher Speicherorte verwendet wird](#ReviewUserInterfaceUsedtoModifyListofPossibleLocations) beschrieben die Benutzeroberfläche, die verwendet wird, um Speicherorte zu den Listen in den Dateien „AddEditLocationView.xaml“ und „AddEditLocationView.xaml.cs“ hinzuzufügen oder zu bearbeiten.  

4.  Überprüfen Sie wie unter [Überprüfen des Codes, der zum Verwalten von Konfigurationsinformationen verwendet wird](#ReviewCodeUsedtoManageConfigurationInformation) beschrieben den Code, der zum Verwalten von Konfigurationsinformationen verwendet wird, die in der Konfigurationsdatei des UDI-Assistenten gespeichert werden.  

#####  <a name="ReviewWizardPageEditorLoadingInitialization"></a> Überprüfen des Lade- und Initialisierungsvorgangs des Editors der Assistentenseite  
 Editors für benutzerdefinierte Assistentenseiten werden geladen, wie vom Designer des UDI-Assistenten verlangt. Die Konfigurationsdateien des Designers des UDI-Assistenten werden geladen, wenn der dieser gestartet wird. Der Designer des UDI-Assistenten überprüft den Ordner „*install_folder*\Bin\Config“ nach Dateien mit der Endung „.config“. Dabei ist *install_folder* der Ordner, in dem das MDT installiert ist.  

 Bei der Konfiguration der UDI-Entwicklungsumgebung haben Sie die SamplePage.dll.confg-Datei in den Ordner „*install_folder*\Bin\Config“ kopiert. Wenn Sie den Designer des UDI-Assistenten starten, wird die SamplePage.dll.confg-Datei gesucht und geladen.  

 Der Designer des UDI-Assistenten verwendet die folgenden Attribute des [Page](#Page)-Element in der SamplePage.dll.confg-Datei, um das EditorPage-Beispiel zu laden und zu initialisieren:  

-   **DesignerAssembly**. Dieses Attribut bestimmt den Namen der DLL, die geladen werden soll. Die DLL muss in demselben Ordner gespeichert sein wie die UDIDesigner.exe-Datei – also in dem Ordner „*install_folder*\Bin“. Dabei ist *install_folder* der Name des Ordners, in dem das MDT installiert ist.  

-   **DesignerType**. Bei diesem Attribut handelt es sich um den Microsoft .NET-Typnamen der Klasse, die das WPF-Benutzersteuerelement enthält.  

-   **Typ**. Verwenden Sie dieses Attribut, um den Seitentyp der benutzerdefinierten Assistentenseite zu konfigurieren, den der UDI-Assistent lädt. Der Designer des UDI-Assistenten verwendet dieses Attribut, um das passende [Page](#Page)-Element in der Konfigurationsdatei des UDI-Assistenten zu suchen.  

-   **Dll**. Verwenden Sie dieses Attribut, um das [DLL](#DLL)-Element in der Konfigurationsdatei des UDI-Assistenten zu konfigurieren, die der Designer des UDI-Assistenten erstellt.  

-   **Beschreibung**. Verwenden Sie dieses Attribut, um Informationen zum Editor für Assistentenseiten bereitzustellen. Der Wert dieses Attributs wird im Dialogfeld **Neue Seite hinzufügen** im Designer des UDI-Assistenten angezeigt, der verwendet wird, um die Assistentenseite zu der „Seitenbibliothek“ hinzuzufügen.  

-   **DisplayName**. Verwenden Sie dieses Attribut, um den Namen der benutzerdefinierten Assistentenseite anzuzeigen, die im Designer des UDI-Assistenten angezeigt wird. Der Wert dieses Attributs wird im Dialogfeld **Neue Seite hinzufügen** im Designer des UDI-Assistenten angezeigt, der verwendet wird, um die Assistentenseite zu der „Seitenbibliothek“ hinzuzufügen.  

     Im Beispiel lautet der Typ der benutzerdefinierten Assistentenseite **SamplePage**, der in der Config.xml-Datei gespeichert wird, **Microsoft.SamplePage.LocationPage**. Die Config.xml-Datei ist im Ordner „*local_folder*\SDK\SamplePage\SamplePage“ gespeichert. Dabei ist *local_folder* der Ordner, den Sie zuvor im Rahmen der Konfiguration auf dem Entwicklungscomputer erstellt haben.  

#####  <a name="ReviewUserInterfaceUsedtoConfigureLocationComboBox"></a> Überprüfen der Benutzeroberfläche, die zum Konfigurieren des Kombinationsfelds „Speicherort“ verwendet wird  
 Wenn der Editor der Assistentenseite geladen und initialisiert wird, wird der Editor für die SampleEditor-Assistentenseite geladen, wenn eine Seite vom Typ **Microsoft.SamplePage.LocationPage** bearbeitet wird. Die Benutzeroberfläche für den Seiteneditor wird in der LocationPageEditor.xaml-Datei gespeichert.  

 Wenn Sie die Benutzeroberfläche auf der Registerkarte **Entwurf** und den Code auf der Registerkarte **XAML** überprüfen, sehen Sie die Beziehung zwischen der graphischen Benutzeroberfläche und den Elementen und Attributen in Extensible Application Markup Language (XAML).  

 Wenn Sie z.B. das **Controls:FieldElementControl**-Element in XAML überprüfen, können Sie sehen, welche Auswirkungen dies auf das Layout der jeweiligen Benutzeroberfläche hat. Verwenden Sie das **Controls:FieldElementControl**-Element, um das Steuerelement [FieldElementControl](#FieldElementControl) zu definieren.  

 Die **Binding**-Parameter in der XAML-Datei binden die Felder im Editor für die Beispielseite mit den Informationen in der Konfigurationsdatei des UDI-Assistenten. Beispielsweise bindet der folgende Code das Textfeld **Standardwert** and das [Default](#Default)-Element in der Konfigurationsdatei des UDI-Assistenten („Config.xml“ im Beispiel):  

```  
<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
```  

 Weitere Informationen finden Sie unter [How to: Make Data Available for Binding in XAML (Vorgehensweise: Verfügbarmachen von Daten für die Bindung in XAML)](http://msdn.microsoft.com/library/ms748857.aspx).  

 Verwenden Sie das **Views:CollectionTControl.ColumnCollectionView**-Element in XAML, um die Liste mit verfügbaren Speicherorten in der Rasteransicht zu bearbeiten. Verwenden Sie das [CollectionTControl](#CollectionTControl)-Steuerelement, um die Rasteransicht anzuzeigen und diese an das [Data](#Data)-Element mit dem Namen **Speicherort** in der UDI-Konfigurationsdatei zu binden.  

#####  <a name="ReviewUserInterfaceUsedtoModifyListofPossibleLocations"></a> Überprüfen der Benutzeroberfläche, die zum Bearbeiten der Liste möglicher Speicherorte verwendet wird  
 Die Benutzeroberfläche zum Ändern der Liste von möglichen Speicherorten besteht aus den folgenden Elementen:  

-   Ein kontextbezogenes Menü und Schaltflächen auf dem Menüband, mit denen Sie wie unter [Überprüfen eines kontextbezogenen Menüs und von Schaltflächen auf dem Menüband zum Ändern der Liste mit Speicherorten](#ReviewContextSensitiveMenuandRibbonButtons) beschrieben die Reihenfolge von Elementen in der Liste mit Speicherorten hinzufügen, bearbeiten oder ändern können.  

-   Ein Dialogfeld, das angezeigt wird, wenn Sie wie unter [Überprüfen des Dialogfelds zum Hinzufügen oder Bearbeiten von Speicherorten](#ReviewDialogBoxforAddingEditingLocations) beschrieben ein Element der Liste von Speicherorten hinzufügen bzw. bearbeiten möchten.  

######  <a name="ReviewContextSensitiveMenuandRibbonButtons"></a> Überprüfen eines kontextbezogenen Menüs und von Schaltflächen auf dem Menüband zum Ändern der Liste mit Speicherorten  
 Wenn Sie mit der rechten Maustaste auf das Listenfeld klicken, das die Liste der Standorte enthält, wird ein kontextbezogenes Menü angezeigt. Sie können diese Tasks auch über die Schaltflächen auf dem Menüband durchführen. Das Steuerelement **Views:CollectionsTControl** in der LocationPageEditor.xaml-Datei definiert die Methoden, die basierend auf den durchgeführten Aktionen und Eigenschaften aufgerufen werden und die Sie wie folgt festlegen:  

-   **SelectedItem**. Diese an Daten gebundene Eigenschaft wird aktiviert, wenn der Benutzer ein Element aus der Liste auswählt. Diese Eigenschaft ist an die **CurrentLocation**-Eigenschaft im Ansichtsmodell gebunden, die sich in der LocationPageEditorViewModel.cs-Datei befindet und von dem [CollectionTControl](#CollectionTControl)-Steuerelement verwendet wird, um das ausgewählte Element zu übergeben, wenn Sie ein bereits vorhandenes Element bearbeiten oder entfernen.  

-   **AddItemAction**. Diese Aktion wird durchgeführt, wenn der Benutzer im kontextbezogenen Menü oder über die Schaltflächen auf dem Menüband auf die Option **Element hinzufügen** klickt. Dann wird eine Datenbindung an eine Eigenschaft im Ansichtsmodell hergestellt, die das **AddLocationAction**-Objekt zurückgibt. Bei diesem Objekt handelt es sich um die **AddLocationCallback**-Methode, die sich in der LocationPageEditorViewModel.cs-Datei befindet und das Dialogfeld in der AddEditLocationView.xaml-Datei anzeigt.  

-   **EditItemAction**. Diese Aktion wird durchgeführt, wenn der Benutzer im kontextbezogenen Menü auf die Option **Element bearbeiten** klickt. Dann wird eine Datenbindung an eine Eigenschaft im Ansichtsmodell hergestellt, die das **EditLocationAction**-Objekt zurückgibt. Bei diesem Objekt handelt es sich um die **EditLocationCallback**-Methode, die sich in der LocationPageEditorViewModel.cs-Datei befindet und das Dialogfeld in der AddEditLocationView.xaml-Datei anzeigt.  

-   **RemoveAction**. Diese Aktion wird durchgeführt, wenn der Benutzer im kontextbezogenen Menü auf die Option **Element entfernen** klickt. Dann wird eine Datenbindung an eine Eigenschaft im Ansichtsmodell hergestellt, die das **RemoveAction**-Objekt zurückgibt. Bei diesem Objekt handelt es sich um die **EditLocationCallback**-Methode, die sich in der LocationPageEditorViewModel.cs-Datei befindet und eine Meldung anzeigt, über die bestätigt wird, dass der Speicherort gelöscht wurde.  

######  <a name="ReviewDialogBoxforAddingEditingLocations"></a> Überprüfen des Dialogfelds zum Hinzufügen oder Bearbeiten von Speicherorten  
 Wenn Sie zu der Liste mit Speicherorten einen neuen Speicherort hinzufügen oder einen bereits vorhandenen Speicherort bearbeiten, wird eine Meldung angezeigt, die in der AddEditLocationView.xaml-Datei angezeigt wird. Die Meldung wird über die [ShowDialogWindow](#ShowDialogWindow)-Fenstermethode in der LocationPageEditorViewModel.cs-Datei angezeigt.  

 Die Benutzeroberfläche in der AddEditLocationView.xaml-Datei besteht aus den folgenden Elementen:  

-   Ein Dialogfeldrahmen mit dem Namen **DialogFrame**, der die folgenden Elementen enthält:  

    -   Ein Titel, den Sie über das **DialogTitle**-Attribut des Dialogfeldrahmens konfigurieren  

    -   Eine **OK**-Schaltfläche, die den Rückgabestatus wie für die Eigenschaft **Genehmigt** auf **TRUE** festlegt. Der Rückgabestatus wird in der **AddLocationCallback**-Methode der LocationPageEditorViewModel.cs-Datei überprüft, um zu bestimmen, ob der Benutzer auf **OK** geklickt hat.  

    -   Eine **Abbrechen**-Schaltfläche, die den Rückgabestatus wie für die Eigenschaft **Genehmigt** auf **FALSE** festlegt. Der Rückgabestatus wird in der **AddLocationCallback**-Methode der LocationPageEditorViewModel.cs-Datei überprüft, um zu bestimmen, ob der Benutzer auf **Abbrechen** geklickt hat.  

-   Ein WPF-Element, das folgende Elemente enthält:  

    -   Eine Bezeichnung, die Sie über das **Content**-Attribut konfigurieren können  

    -   Ein Textfeld, das an das [Data](#Data)-Element mit dem Namen **Speicherort** in der UDI-Konfigurationsdatei gebunden ist (die Config.xml-Datei in dem Beispiel)  

######  <a name="ReviewCodeUsedtoManageConfigurationInformation"></a> Überprüfen des Codes, der zum Verwalten von Konfigurationsinformationen verwendet wird  
 Die Konfigurationsinformationen zu Ihrer benutzerdefinierten Assistentenseite wird in der Konfigurationsdatei des UDI-Assistenten gespeichert. Dabei handelt es sich  

-   in dem Beispiel, das im Lieferumfang des UDI SDK enthalten ist, um die Config.xml-Datei. Diese Datei enthält nur die Konfigurationseinstellungen zu dem Beispiel.  

-   um die im Lieferumfang des MDT enthaltene UDIWizard_Config.xml-Datei, die im Ordner „*installation_folder*\Templates\Distribution\Scripts“ gespeichert ist. Dabei ist *installation_folder* der Ordner, in dem Sie das MDT installiert haben. Diese Datei enthält die Konfigurationseinstellungen für alle integrierten Assistentenseiten und -phasen.  

 Im SampleEditor-Beispiel können die Konfigurationsinformationen mithilfe der Routine **Speicherorte** verwaltet werden. Sie befinden sich in der LocationPageEditorViewModel.cs-Datei. Die Routine **Speicherorte** gibt über die Konfigurationsdatei des UDI-Assistenten eine Liste zurück. Insbesondere die zurückgegebene Liste enthält für jedes [DataItem](#DataItem)-Element in der Konfigurationsdatei des UDI-Assistenten jeweils ein Element.  

## <a name="creating-custom-udi-wizard-pages"></a>Erstellen von benutzerdefinierten Assistentenseiten  
 In der Regel werden benutzerdefinierte UDI-Assistentenseiten wie folgt erstellt:  

1.  Erstellen Sie eine SamplePage-Projektmappe, die als Startpunkt dienen soll.  

2.  Platzieren Sie die gewünschten Steuerelemente (Felder) auf dem Formular.  

3.  Schreiben Sie Code, um entsprechende Tasks auszuführen, wenn die Assistentenseite geladen wird (Überschreibungen der **OnWindowCreated**-Methode). Dies umfasst die folgenden Schritte:  

    1.  Initialisieren Sie das Formular.  

    2.  Lesen Sie Speicher-, Tasksequenz und Umgebungsvariablen bzw. Informationen wie **Setter**-Eigenschaften aus XML-Dateien.  

4.  Schreiben Sie beliebigen Code, um passende Tasks auszuführen, wenn die Seite angezeigt wird (überschreibt die **OnWindowShown**-Methode). Dies umfasst die folgenden Schritte:  

    1.  Aktivieren oder deaktivieren Sie Steuerelemente basierend auf Informationen, die gelesen werden, wenn die Seite in Schritt 3 geladen wurde.  

    2.  Aktualisieren Sie die Steuerelemente basierend auf den Informationen, die gelesen wurden, als die Seite in Schritt 3 geladen wurde. Steuerelemente werden beispielsweise anhand dieser Informationen aufgefüllt.  

5.  Schreiben Sie beliebigen Code, um die passenden Tasks auszuführen, während der Benutzer mit der Assistentenseite interagiert.  

6.  Schreiben Sie beliebigen Code, um passende Tasks auszuführen, wenn der Benutzer im UDI-Assistenten auf **Weiter** klickt (überschreibt die **OnNextClicked**-Methode). Dies umfasst die folgenden Schritte:  

    1.  Aktualisieren Sie Speicher-, Tasksequenz und Umgebungsvariablen bzw. Informationen aus XML-Dateien.  

    2.  Aktualisieren Sie ggf. die Informationen auf den Zusammenfassungsseiten, falls dies noch nicht durch die Felder auf der Seite durchgeführt wurde.  

7.  Erstellen Sie die Projektmappe.  

     Vergewissern Sie sich, dass es sich bei der Version der DLL, die Sie erstellen, um dieselbe Prozessorplattform handelt wie bei der Installation der MDT, d.h. die Prozessorplattform für Windows Preinstallation Environment (Windows PE). Der UDI-Assistent kann auf den folgenden Betriebssystemen ausgeführt werden:  

    -   **Das bereits auf dem Zielcomputer vorhandene Betriebssystem.** Sie können 32-Bit-Versionen Ihrer Assistentenseite sowohl auf 32-Bit als auch auf 64-Bit-Windows-Betriebssystemen ausführen. Sie können 64-Bit-Versionen Ihrer Assistentenseite nur auf 64-Bit-Windows-Betriebssystemen ausführen.  

    -   **Windows PE auf dem Zielcomputer.** Windows PE unterstützt das Ausführen von 32-Bit-Anwendungen auf 64-Bit-Versionen von Windows PE nicht. Daher müssen Sie für jede Prozessorarchitektur von Windows PE, die Sie verwenden möchten, eine Version Ihrer Assistentenseite erstellt haben.  

8.  Kopieren Sie die DLL zu Ihrer benutzerdefinierten Assistentenseite in den Plattformordner „*installation_folder*\Templates\Distribution\Tools\“. Dabei steht *installation_folder* für den Ordner, in dem Sie das MDT installiert haben, und *platform* für **x86** (32-Bit-Version) oder für **x64** (64-Bit-Version).  

9. Schließen Sie die Schritte zum Erstellen des Editors für benutzerdefinierte Seiten ab.  

## <a name="creating-custom-wizard-page-editors"></a>Erstellen von Editors für benutzerdefinierte Assistentenseiten  
 In der Regel werden Editors für benutzerdefinierte UDI-Assistentenseiten wie folgt erstellt:  

1.  Erstellen Sie eine SampleEditor-Projektmappe, die als Startpunkt dienen soll.  

2.  Erstellen Sie die primäre Benutzeroberfläche des Seiteneditors in einer XAML-Datei.  

3.  Fügen Sie Instanzen des [FieldElementControl](#FieldElementControl)-Steuerelements hinzu, die für die Assistentenseite erforderlich sind, die ggf. konfiguriert werden soll.  

4.  Fügen Sie Instanzen des [SetterControl](#SetterControl)-Steuerelements hinzu, die für die Assistentenseite erforderlich sind, die ggf. konfiguriert werden soll.  

5.  Fügen Sie Instanzen des [CollectionTControl](#CollectionTControl)-Steuerelements hinzu, die für die Assistentenseite erforderlich sind, die ggf. konfiguriert werden soll.  

6.  Fügen Sie die [IDataService](#IDataService)-Schnittstelle hinzu.  

7.  Schreiben Sie passenden Code, um die Konfigurationsdatei des UDI-Assistenten anhand der Konfigurationseinstellungen zu aktualisieren, die über den Editor für benutzerdefinierte Assistentenseiten konfiguriert werden sollen.  

8.  Erstellen Sie untergeordnete Dialogfelder in einer XAML-Datei, und rufen Sie diese über den primären Seiteneditor ab, indem Sie, wie für die zu konfigurierende Assistentenseite erforderlich, die [IMessageBoxService](#IMessageBoxService)-Schnittstelle verwenden.  

9. Fügen Sie basierend auf den Anforderungen der zu konfigurierenden Assistentenseite die passenden Schnittstellen zu dem Menüband des Designers des UDI-Assistenten hinzu.  

10. Erstellen Sie die Projektmappe.  

    > [!NOTE]
    >  Vergewissern Sie sich, dass es sich bei der Version der DLL, die Sie erstellen, um dieselbe Prozessorplattform wie bei der Installation des MDT handelt. Wenn Sie z.B. die 64-Bit-Version des MDT installieren, sollten Sie auch eine 64-Bit-Version des Editors für benutzerdefinierte Seiten erstellen.  

11. Erstellen Sie eine Konfigurationsdatei für den Designer des UDI-Assistenten, um die benötigten DLLs zu laden und den Editor für Assistentenseiten den zugehörigen Assistentenseiten zuzuordnen (die SamplePage.dll.config-Datei in dem Beispiel).  

     Weitere Informationen zu den Elementen, die erforderlich sind, um eine Assistentenseite mit dem Editor zu verknüpfen, finden Sie im Abschnitt [DesignerMappings](#DesignerMappings)-Element. Betrachten Sie außerdem die untergeordneten Elemente und die zugehörigen Attribute.  

12. Kopieren Sie die Konfigurationsdatei des Designers des UDI-Assistenten, den Sie im vorherigen Schritt im Ordner „*installation_folder*\Bin\Config“ erstellt haben. Dabei ist *installation_folder* der Ordner, in dem Sie die MDT-Version erstellt haben.  

13. Kopieren Sie die DLL zum Editor Ihrer benutzerdefinierten Assistentenseite in den Ordner „*installation_folder*\Bin“. Dabei ist *installation_folder* der Ordner, in dem Sie Das MDT erstellt haben.  

##  <a name="CreatingCustomUDITasks"></a> Erstellen von benutzerdefinierten UDI-Tasks  
 *UDI-Tasks* sind DLLs, die in C++ geschrieben sind und die [ITask](#ITaskinterface)-Schnittstelle implementieren. Registrieren Sie die DLL mit der Taskbibliothek des Designers des UDI-Assistenten, indem Sie eine Konfigurationsdatei für diesen Designer erstellen (CONFIG-Datei) und diese in dem Ordner „*installation_folder*\Bin\Config“ speichern. Dabei ist *installation_folder* der Ordner, in dem Sie das MDT erstellt haben.  

> [!NOTE]
>  Sie können eine DLL erstellen, die Assistentenseiten, Tasks und Validierungssteuerelemente in Form einer DLL-Datei enthält. Außerdem können Sie eine einzelne Konfigurationsdatei (.config) für den Designer des UDI-Assistenten erstellen, der die Konfigurationseinstellungen für die Assistentenseiten, Tasks und Validierungssteuerelemente in der DLL enthält.  

 **Gehen Sie wie folgt vor, um benutzerdefinierte UDI-Tasks zu erstellen**  

1.  Schreiben Sie Code, der die Schnittstelle [ITask](#ITaskinterface) sowie die folgenden Methoden implementiert:  

    -   [Init](#Init). Diese Methode wird aufgerufen, um Ihren Task zu initialisieren.  

    -   [Execute](#Execute). Diese Methode wird aufgerufen, um Ihren Task auszuführen.  

2.  Schreiben Sie Code, der die Klassenfactory des benutzerdefinierten Tasks für die Factoryregistrierung registriert.  

3.  Erstellen Sie die Projektmappe für Ihren benutzerdefinierten Task.  

    > [!NOTE]
    >  Vergewissern Sie sich, dass es sich bei der Version der DLL, die Sie erstellen, um dieselbe Prozessorplattform wie bei der Installation des MDT handelt. Wenn Sie z.B. die 64-Bit-Version des MDT installieren, sollten Sie auch eine 64-Bit-Version des benutzerdefinierten UDI-Tasks erstellen.  

4.  Erstellen Sie unterhalb des [TaskLibrary](#TaskLibrary)-Elements ein [Task](#Task)-Element in der Konfigurationsdatei des Designers des UDI-Assistenten, das dem folgenden Auszug ähnelt:  

    ```  
    <Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
       <TaskItem Type="Setter" Name="Status Bitmap">  
          <Param Name="BitmapFilename"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Log File">  
          <Param Name="log"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Write Configuration File">  
          <Param Name="writecfg"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Read Configuration File">  
          <Param Name="readcfg"/>  
       </TaskItem>  
    </Task>  
    ```  

    > [!NOTE]
    >  Sämtliche [Task](#Task)-Elemente sollten den **BitmapFilename**-Parameter enthalten. Geben Sie alle anderen Parameter wie von dem Task verlangt an. Beispielsweise wird im vorherigen Beispiel der **log**-Parameter verwendet, um einen Parameter für den Speicherort der Protokolldatei anzugeben.  

5.  Kopieren Sie die Konfigurationsdatei des Designers des UDI-Assistenten, den Sie im vorherigen Schritt im Ordner „*installation_folder*\Bin\Config“ erstellt haben. Dabei ist *installation_folder* der Ordner, in dem Sie das MDT installiert haben.  

6.  Kopieren Sie die DLL zu Ihrem benutzerdefinierten Task in den Plattformordner „*installation_folder*\Templates\Distribution\Tools\“. Dabei steht *installation_folder* für den Ordner, in dem Sie das MDT installiert haben, und *platform* für **x86** (32-Bit-Version) oder für **x64** (64-Bit-Version).  

##  <a name="CreatingCustomUDIValidators"></a> Erstellen von benutzerdefinierten UDI-Validierungssteuerelementen  
 *UDI-Validierungssteuerelemente* sind DLLs, die in C++ geschrieben sind und die **IValidator**-Schnittstelle implementieren. Registrieren Sie die DLL für das Validierungssteuerelement des Designers des UDI-Assistenten, indem Sie eine Konfigurationsdatei für diesen Designer erstellen (CONFIG-Datei) und diese in dem Ordner „*installation_folder*\Bin\Config“ speichern. Dabei ist *installation_folder* der Ordner, in dem Sie das MDT installiert haben.  

 **Gehen Sie wie folgt vor, um benutzerdefinierte UDI-Validierungssteuerelemente zu erstellen**  

1.  Schreiben Sie Code, der eine Unterklasse der **BaseValidator**-Klasse erstellt und die folgenden Methoden implementiert:  

    -   **Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)**. Der Formularcontroller ruft den **Init**-Member auf, um das Validierungssteuerelement zu initialisieren. Diese Methode muss die **Init**-Methode für die **BaseValidator**-Klasse aufrufen. Sie liest in der Regel alle Eigenschaften, die für das Validierungssteuerelement in der Konfigurationsdatei des UDI-Assistenten festgelegt sind. Das Validierungssteuerelement **InvalidCharactersValidator** ruft beispielsweise über diese Methode den Wert der **InvalidChars**-Eigenschaft ab.  

    -   **IsValid**. Der Formularcontroller ruft diese Methode ab, um zu überprüfen, ob das Steuerelement gültigen Text enthält. Im Folgenden ist ein Beispiel der **IsValid**-Methode für ein Validierungssteuerelement dargestellt, das sicherstellt, dass das Feld nicht leer ist:  

        ```  
        BOOL IsValid(LPBSTR pMessage)  
        {  
            __super::IsValid(pMessage);  

            _bstr_t text;  
            m_pText->GetText(text.GetAddress());  
            return (text.length() > 0);  
        }  
        ```  

    -   **Init(IControl \*pControl, LPCTSTR-Meldung)**. Der Formularcontroller ruft diesen Member für jeden Tastaturanschlag und andere Ereignisse auf, damit das Validierungssteuerelement die Inhalte des Steuerelements und die aktualisierten Meldungen im unteren Bereich der Assistenten überprüfen (oder löschen) kann.  

     In der Regel müssen Sie nur diese Methoden überschreiben. Je nach Validierungssteuerelement müssen Sie jedoch möglicherweise andere Methoden in der Unterklasse der **BaseValidator**-Klasse außer Kraft setzen, die Sie erstellen. Betrachten Sie die **BaseValidator**-Klasse, wenn Sie weitere Informationen zu diesen anderen Methoden benötigen.  

2.  Schreiben Sie Code, der die benutzerdefinierte Taskklasse für die Registrierungsfactory registriert.  

3.  Erstellen Sie die Projektmappe für Ihren benutzerdefinierten Task.  

    > [!NOTE]
    >  Vergewissern Sie sich, dass es sich bei der Version der DLL, die Sie erstellen, um dieselbe Prozessorplattform wie bei der Installation des MDT handelt. Wenn Sie z.B. die 64-Bit-Version des MDT installieren, sollten Sie auch eine 64-Bit-Version des benutzerdefinierten UDI-Tasks erstellen.  

4.  Erstellen Sie unterhalb des **ValidatorLibrary**-Elements ein [Validierungssteuerelement](#Validator) in der Konfigurationsdatei des Designers des UDI-Assistenten, das dem folgenden Auszug ähnelt:  

    ```  
    <Validator   
    <Validator DLL="" Description="Must follow a pre-defined pattern" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern">  
       <Param Description="Enter the message you want displayed when the text in this field doesn't match the pattern:" Name="Message" DisplayName="Message"/>  
       <Param Description="The name of a pre-defined regular expression pattern. Must be Username, ComputerName, or Workgroup" Name="NamedPattern" DisplayName="Named Pattern"/>  
    </Validator>  
    ```  

    > [!WARNING]
    >  Sämtliche [Validierungssteuerelemente](#Validator) sollten den **Message**-Parameter beinhalten. Geben Sie wie vom Validierungssteuerelement verlangt alle anderen Parameter an. Beispielsweise wird im Auszug zuvor der **NamedPattern**-Parameter verwendet, um den Parameter für den Namen eines vordefinierten Musters für einen regulären Ausdruck anzugeben.  

5.  Kopieren Sie die Konfigurationsdatei des Designers des UDI-Assistenten, den Sie im vorherigen Schritt im Ordner „*installation_folder*\Bin\Config“ erstellt haben. Dabei ist *installation_folder* der Ordner, in dem Sie das MDT installiert haben.  

6.  Kopieren Sie die DLL zu Ihrem benutzerdefinierten Task in den Plattformordner „*installation_folder*\Templates\Distribution\Tools\“. Dabei steht *installation_folder* für den Ordner, in dem Sie das MDT installiert haben, und *platform* für **x86** (32-Bit-Version) oder für **x64** (64-Bit-Version).  

## <a name="udi-wizard-reference"></a>Referenz zum UDI-Assistenten  

### <a name="wizard-page-components"></a>Komponenten der Assistentenseite  
 Sie können eine von mehreren zuvor erstellten Komponenten verwenden, um Ihre benutzerdefinierten Seiten zu erstellen.  

#### <a name="creating-component-instances"></a>Erstellen von Komponenteninstanzen  
 Der UDI-Assistent verwendet Klassenfactorys, um neue Instanzen von Objekten für Sie zu erstellen. Diese Factorys sind unter Verwendung einer Zeichenfolge als Schlüssel zu einer Factory für eine Factoryregistrierung registriert. Die **WmiRepository**-Komponente wird von der Zeichenfolge „Microsoft.Wizard.WmiRepository“ ermittelt, die in der IWmiRepository-Headerdatei als **ID_WmiRepository** verfügbar ist.  

 Angenommen, Sie haben Ihre Seite als eine Unterklasse von **WizardPageImpl** geschrieben, können Sie wie folgt eine neue Instanz einer **WmiRepoistory**-Komponente erstellen:  

```  
PWmiRepository pWmi;  
CreateInstance(Container(), ID_WmiRepository, &pWmi);  
```  

 Bei der **CreateInstance**-Funktion handelt es sich um eine typsichere Vorlagenfunktion zum Erstellen einer neuen Instanz von Komponenten. Bei **PWmiRepository** handelt es sich um einen intelligenten Zeiger, der die Verweiszählung für Sie übernimmt.  

#### <a name="creatable-components"></a>Erstellbare Komponenten  
 Es gibt eine Reihe von Komponenten, die Sie für die Registrierung registrieren können. Der erste Satz von Komponenten wird immer registriert, da er von der wichtigsten ausführbaren Datei des UDI-Assistenten zur Verfügung gestellt wird. Die übrigen beiden Sätze von Komponenten werden in optionalen DLLs zur Verfügung gestellt. Damit Sie auf diese Komponenten zugreifen können, muss die DLL im Abschnitt **DLLs** der CONFIG-XML-Datei aufgeführt sein. Für den Code ist nicht relevant, welche ausführbare Datei eine bestimmte Komponente enthält.  

 Die Liste der Komponenten-IDs für Komponenten, die bei der Factoryregistrierung registriert wurden (in OSDSetupWizard definiert), wird in Tabelle 3 dargestellt. Der Komponentenname entspricht dabei der ID, jedoch ohne das Präfix *ID_*.  

### <a name="table-3-component-ids"></a>Tabelle 3: Komponenten-IDs  

|**ID**|**Beschreibung**|  
|-|-|  
|ID_ACPowerTask|(ITask, IWizardComponent) Ein Preflighttask, mit dem sichergestellt wird, dass Ihr Computer sich nicht ausschließlich im Akkubetrieb befindet.|  
|ID_AppDiscoveryTask|(ITask, IWizardComponent) Ein spezieller Task für die Ermittlung von Softwareelementen, die Sie auf Ihrem Computer installiert haben.|  
|**ID_BackgroundTask**|(**IBackgroundTask**, **IWizardComponent**) Kann zur Ausführung eines Tasks in einem anderen Thread verwendet werden.|  
|**ID_CopyFilesTask**|(**ITask**, **IWizardComponent**) Ein Task zum Kopieren von Dateien.|  
|**ID_FormController**|(**IFormController**) Vermutlich müssen Sie selbst keine Instanz erstellen, da für Ihre Seite eine eigene Instanz zur Verfügung gestellt wird.|  
|**ID_InvalidCharactersValidator**|(**IValidator**) Stellt sicher, dass kein Textfeld Zeichen aus einer Liste enthält, die für das Validierungssteuerelement bereitgestellt wurde.|  
|**ID_Logger**|(**ILogger**) Vermutlich müssen Sie selbst keine Instanz erstellen, da für Ihre Seite ein Zeiger auf die freigegebene Instanz bereitgestellt wird.|  
|**ID_NonEmptyValidator**|(**IValidator**) Ein Validierungssteuerelement, das sicherstellt, dass keine leeren Felder vorhanden sind.|  
|**ID_PasswordValidator**|(**IValidator**) Ein Validierungssteuerelement, das sicherstellt, dass der Inhalt eines Textfelds nicht in einem anderen Textfeld vorhanden ist.|  
|**ID_Regex**|(**IRegEx**) Wertet einen regulären Ausdruck aus, wobei nach Übereinstimmungen gesucht wird.|  
|**ID_RegExValidator**|(**IValidator**) Ein Validierungssteuerelement, das einen regulären Ausdruck oder ein bekanntes Muster überprüft.|  
|**ID_SimpleStringProperties**|(**IStringProperties**, **ISimpleStringProperties**) Stellt eine einfache Möglichkeit bereit, ohne XML Eigenschaften an Tasks zu senden.|  
|**ID_ShellExecuteTask**|(**ITask**, **IWizardComponent**) Ausführung eines externen Programms.|  
|**ID_SummaryBag**|(**ISummaryBag**) Indirekt über die Form-Methode auf Ihrer Seite verfügbar.|  
|**ID_TaskManager**|(**ITaskManager**, **IBackgroundCallback**, **IWizardComponent**) Verwaltet die Ausführung mehrerer Tasks und die Benutzeroberfläche.|  
|**ID_WmiRepository**|(**IWmiRepository**, **IWizardComponent**) Ermöglicht die Ausführung von WMI-Abfragen (Windows-Verwaltungsinstrumentation).|  
|**ID_IXmlDocument**|(**IXmlDocument**) Stellt eine Fassade zum Lesen und Schreiben von XML-Dokumenten bereit.|  

 Die festgelegten Datei „OSDRefreshWizard.dll“, die freigegebenen Seiten und andere Steuerelementkomponenten werden in den Tabellen 4 und 5 aufgeführt.  

### <a name="table-4-directory-controls"></a>Tabelle 4: Steuerelemente für Verzeichnisse  

|**ID**|**Beschreibung**|  
|-|-|  
|**ID_Directory**|(**IDirectory**) Eine Fassade zum Abrufen von Verzeichnisinformationen vom Dateisystem.|  

### <a name="table-5-defined-sharedpagesdll"></a>Tabelle 5: Defined SharedPages.dll  

|**ID**|**Beschreibung**|  
|-|-|  
|**ID_ADHelper**|(**IADHelper**) Stellt eine Fassade für bestimmte Features in Active Directory® Domain Services (AD DS) bereit.|  
|**ID_CpuInfo**|(**ICpuInfo**) Ermittelt, ob für Ihre CPU eine 32- oder eine 64-Bit-Architektur verwendet wird.|  
|**ID_DomainJoinValidator**|(**IDomainJoinValidator**) Verfügt über mehrere Methoden, mit denen überprüft wird, ob die Einbindung in eine Domäne mit bestimmten Anmeldeinformationen zulässig ist.|  
|**ID_DriveList**|(**IDriveList**, **IBindableList**, **IWizardComponent**) Verwendet WMI, um eine Liste der auf Ihrem Computer vorhandenen Laufwerke abzurufen.|  
|**ID_WiredNetworkTask**|(**ITask**) Ein Task, der überprüft, ob Sie über einen kabelgebundenen (anstelle eines kabellosen) Netzwerkadapters mit dem Netzwerk verbunden sind.|  

#### <a name="control-components"></a>Steuerelementkomponenten  
 Sie können mit Steuerelementen auf Ihrer Seite kommunizieren, indem Sie die Vorlagenfunktion **GetControlWrapper** verwenden, die Zugriff auf einen der Komponententypen bereitstellt, die in Tabelle 6 aufgeführt sind.  

### <a name="table-6-components"></a>Tabelle 6: Komponenten  

|**Steuerelementtypen für Dialogfelder**|**Beschreibung**|  
|-|-|  
|**CONTROL_CHECK_BOX**|(**ICheckBox**) Eine Fassade zum Verwenden von Kontrollkästchen-Steuerelementen.|  
|**CONTROL_COMBO_BOX**|(**IComboBox**) Eine Fassade zum Verwenden von Kombinationsfeld-Steuerelementen.|  
|**CONTROL_GENERIC**|(**IControl**) Ermöglicht es Ihnen, mit den meisten Arten von Steuerelementen den aktivierten und den sichtbaren Zustand zu steuern|  
|**CONTROL_LIST_VIEW**|(**IListView**) Eine Fassade, die Zugriff auf Features eines Listenansicht-Steuerelements bereitstellt.|  
|**CONTROL_PROGRESS_BAR**|(**IProgressBar**) Eine Fassade zum Festlegen des Fortschritts innerhalb des Statusanzeige-Steuerelements.|  
|**CONTROL_RADIO_BUTTON**|(**IRadioButton**) Eine Fassade zum Verwenden von Optionsfeld-Steuerelementen.|  
|**CONTROL_STATIC_TEXT**|(**IStaticText**) Eine Fassade, die Lese-/Schreibberechtigungen für den Text eines Steuerelements wie einer Bezeichnung oder eines Textfelds bereitstellt.|  
|**CONTROL_TREE_VIEW**|(**ItreeView**) Eine Fassade zum Verwenden von Strukturansicht-Steuerelementen.|  

#### <a name="image-list-component"></a>ImageList-Komponente  
 Diese Komponente ist eine Fassade für ein **ImageList**-Steuerelement auf Ihrer Seite. Sie erstellen eine Bildliste mit der Schnittstelle **IListView** oder **ITreeView**.  

#### <a name="formcontroller-component"></a>FormController-Komponente  
 Diese Komponente wird vom Assistenten für Sie erstellt und Ihrer Seite übergeben. Sie greifen darauf über Ihre Seite mit der **Form**-Methode zu, die von der Basisklasse **WizardPageImpl** implementiert wird.  

#### <a name="invalidcharactervalidator-component"></a>InvalidCharacterValidator-Komponente  
 Hierbei handelt es sich um ein Validierungssteuerelement, das Sie in Ihre Seite integrieren können. Die in „IValidator.h“ definierte ID lautet **ID_InvalidCharactersValidator**. Für diese ist der Textwert „Microsoft.Wizard.Validation.InvalidChars“ festgelegt.  

 Dieses Validierungssteuerelement sucht nach einer Eigenschaft (ein **Setter**-Element in der Konfigurationsdatei) mit dem Namen **InvalidChars**. Dabei handelt es sich um eine Liste mit unzulässigen Zeichen. Das Validierungssteuerelement überprüft Zeichen in einem Textfeld. Wenn der Text Zeichen aus dieser Liste enthält, meldet die Komponente einen Fehler.  

#### <a name="nonemptyvalidator-component"></a>NonEmptyValidator-Komponente  
 Hierbei handelt es sich um ein Validierungssteuerelement, das Sie in Ihre Seite integrieren können. Die in „IValidator.h“ definierte ID lautet **ID_NonEmptyValidator**. Für diese ist der Textwert „Microsoft.Wizard.Validation.NonEmpty“ festgelegt.  

 Dieses Validierungssteuerelement meldet einen Fehler, wenn das Textfeld (oder ein anderes Steuerelement, das **IStaticText** unterstützt) einen leeren Zeichenfolgenwert aufweist.  

#### <a name="passwordvalidator-component"></a>PasswordValidator-Komponente  
 Hierbei handelt es sich um ein Validierungssteuerelement, das Sie in Ihre Seite integrieren können. Die in „IValidator.h“ definierte ID lautet **ID_PasswordValidator**. Für diese ist der Textwert „Microsoft.Wizard.Validation.Password“ festgelegt.  

 Dieses Validierungssteuerelement kann für zwei unterschiedliche Textsteuerelemente (die **IStaticText** unterstützen) verwendet werden. Wenn diese nicht die gleichen Werte aufweisen, wird ein Fehler gemeldet. Wenn also die Textfelder **Kennwort** und **Kennwort bestätigen** unterschiedliche Werte aufweisen, schlägt der Überprüfungsvorgang fehl.  

 Da für dieses Validierungssteuerelement zwei Steuerelemente erforderlich sind, müssen mehr Einstellungen als bei anderen Validierungssteuerelementen vorgenommen werden. Für die Konfiguration kann beispielsweise der folgende Vorgang verwendet werden:  

```  
Form()->AddToGroup(IDC_EDIT_PASSWORD, IDC_EDIT_PASSWORD2);  
PValidator pValidator;  
Form()->AddValidator(IDC_EDIT_PASSWORD, ID_PasswordValidator, pMessage, &pValidator);  
PStaticText pPassword2;  
GetControlWrapper(View(), IDC_EDIT_PASSWORD2, CONTROL_STATIC_TEXT, &pPassword2);  
pValidator->SetProperty(0, pPassword2);  
```  

 Definieren Sie zuerst das Steuerelement **Kennwort bestätigen** als untergeordnetes Steuerelement des Steuerelements **Kennwort**. Wenn nun der Formularcontroller das Steuerelement **Kennwort** deaktiviert, wird auch das Steuerelement **Kennwort bestätigen** deaktiviert. Fügen Sie anschließend ein Kennwort-Validierungssteuerelement zum Formular hinzu. Übergeben Sie abschließend dem Steuerelement **Kennwort bestätigen** das Kennwort-Validierungssteuerelement mit der Schnittstelle.  

 Aufgrund der Anforderungen, die sich durch die beiden Steuerelemente ergeben, müssen Sie zum Einrichten dieses Validierungssteuerelements anstelle einer XML-Konfigurationsdatei Code verwenden.  

#### <a name="regexvalidator-component"></a>RegExValidator-Komponente  
 Hierbei handelt es sich um ein Validierungssteuerelement, das Sie in Ihre Seite integrieren können. Die in „IValidator.h“ definierte ID lautet **ID_RegExValidator**. Für diese ist der Textwert „Microsoft.Wizard.Validation.RegEx“ festgelegt.  

 Dieses Validierungssteuerelement überprüft, ob der Inhalt eines Textsteuerelements (das **IStaticText** unterstützt) mit einem regulären Ausdruck übereinstimmt. Der Vorgang schlägt fehl, wenn dies nicht der Fall ist.  

 Sie können dieses Validierungssteuerelement alternativ auch mit einem vordefinierten benannten Muster verwenden. Wenn Sie einen regulären Ausdruck verwenden möchten, muss der XML-Code eine Settereigenschaft mit dem Namen **Pattern** aufweisen. Wenn Sie stattdessen ein benanntes Muster verwenden möchten, verwenden Sie den Setter **NamedPattern** mit einem der Werte aus Tabelle 7.  

### <a name="table-7-named-pattern-setters"></a>Tabelle 7: Setter für benannte Muster  

|**Muster**|**Beschreibung**|  
|-|-|  
|Benutzername|Überprüft, ob die Syntax „domain\user“ oder user@domain verwendet wird.|  
|ComputerName|Der Name muss zwischen 1 und 15 Zeichen lang sein und darf bestimmte Zeichen wie „:“ und „?“ nicht enthalten.|  
|Arbeitsgruppe|Der Name muss zwischen 1 und 15 Zeichen lang sein und darf bestimmte Zeichen (z.B. „=“, „+“ und „?“) nicht enthalten.|  

#### <a name="factoryregistry-component"></a>FactoryRegistry-Komponente  
 Mit dieser Komponente werden alle Klassenfactorys und Dienste erfasst. Sie Implementiert die **IFactoryRegistry**-Schnittstelle und ist indirekt über die **Container**-Methode Ihrer Seite verfügbar. Darüber hinaus lädt die Registrierung Erweiterungs-DLLs. Nach dem Laden einer DLL sucht die Registrierung nach der exportierten Funktion **RegisterFactories**. Sie müssen diese Funktion implementieren und darin alle relevanten Klassenfactorys wie etwa diejenigen für Ihre Seiten, Tasks und Validierungssteuerelemente registrieren. Das folgende Beispiel stammt aus dem Beispielprojekt:  

```  
extern "C" __declspec(dllexport) void RegisterFactories(IFactoryRegistry *factories)  
{  
Register<LocationPageFactory>(ID_LocationPage, factories);  
}  
```  

#### <a name="logger-component"></a>Logger-Komponente  
 Diese Komponente kann auf Ihrer Seite mit der **Logger**-Methode (die durch **WizardPageImpl** implementiert wird) verwendet werden. Mit dieser Methode schreiben Sie Einträge in die Protokolldatei. Der Inhalt der Protokolldatei eignet sich zur Diagnose von Problemen, die möglicherweise bei Benutzern auftreten, wenn diese den UDI-Assistenten ausführen.  

#### <a name="propertybag-component"></a>PropertyBag-Komponente  
 Der *Eigenschaftenbehälter* (property bag) ist ein Container für Speichervariablen. Der Eigenschaftenbehälter kann auf Ihrer Seite durch **Container()->Properties()** verwendet werden. Speichervariablen sind nützlich, wenn temporäre Daten einer Seite an andere Seiten übergeben werden.  

#### <a name="tsvariablebag-and-tsrepository-components"></a>TSVariableBag- und TSRepository-Komponente  
 Die **TSVariableBag**-Komponente ermöglicht das Lesen und Schreiben von Tasksequenzvariablen. Dazu speichert sie Werte im Arbeitsspeicher, bis der Benutzer üblicherweise auf **Fertig stellen** klickt. Sie können auf den **TSVariable**-Behälter über die Methode **TSVariables** (die durch die **WizardPageImpl**-Basisklasse implementiert wird) auf Ihrer Seite zugreifen. Diese Komponenten protokollieren alle Lese- und Schreibvorgänge für Tasksequenzvariablen.  

#### <a name="wmirepository-component"></a>WmiRepository-Komponente  
 Diese Komponente stellt eine Fassade zum Verwenden von WMI-Abfragen bereit. Durch den Aufruf der **CreateInstance**-Hilfsfunktion mit **ID_WmiRepository** erhalten Sie eine Instanz dieser Komponente, die die Schnittstelle **IWmiRepository** unterstützt. Diese Komponente gibt Ergebnisdatensätze über die **IWmiIterator**-Schnittstelle zurück.  

###  <a name="WizardPageHelperClasses"></a> Hilfsklassen für die Assistentenseite  
 Mit den im UDI SDK bereitgestellten Hilfsklassen können Sie für den UDI-Assistenten benutzerdefinierte Seiten erstellen. In Tabelle 8 werden die Hilfsklassen aufgeführt.  

### <a name="table-8-helper-classes"></a>Tabelle 8: Hilfsklassen  

|**Hilfsklasse**|**Beschreibung**|  
|-|-|  
|[ClassFactoryImpl-Klasse](#ClassFactoryImplClass)|Hierbei handelt es sich um eine nützliche Basisklasse zum Erstellen einer Klassenfactory, die Sie mit der Factoryregistrierung registrieren können.|  
|[Interface-Vorlagenklasse](#InterfaceTemplateClass)|Verwenden Sie diese Vorlagenklasse zum Erstellen einer Komponente, die mehr als eine Schnittstelle implementieren kann.|  
|[Path-Hilfsklasse](#PathHelperClass)|Diese Klasse stellt häufig verwendete Vorgänge für Dateien und Verzeichnisse bereit.|  
|[Pointer-Vorlagenklasse](#PointerTemplateClass)|Diese Klasse stellt eine Verweiszählung bereit, mit der die Lebensdauer von COM-Komponenten verwaltet werden kann. Achten Sie darauf, Schnittstellen freizugeben, wenn Sie diese nicht mehr benötigen. Diese Vorlagenklasse verwaltet die Lebensdauer automatisch.|  
|[PUnknown-Klasse](#PUnkownClass)|Diese Klasse ist ein intelligenter Zeiger für die IUnknown-Schnittstelle. Verwenden Sie für alle anderen Schnittstellen die Pointer-Vorlagenklasse.|  
|[StringUtil-Hilfsklasse](#StringUtilHelperClass)|Diese Klasse enthält Hilfsmethoden, die das Verwenden von Zeichenfolgen vereinfachen.|  
|[SubInterface-Vorlagenklasse](#SubInterfaceTemplateClass)|Diese Basisklasse erleichtert das Implementieren einer Komponente, die eine Schnittstelle unterstützt, die wiederum von einer anderen Schnittstelle erbt.|  
|[UnknownImpl-Vorlagenklasse](#UnknownImplTemplateClass)|Diese Klasse ist für viele Aufgaben zuständig, die beim Erstellen einer COM-Komponente anfallen.|  
|[WizardComponent-Vorlagenklasse](#WizardComponentTemplateClass)|Diese Basisklasse wird zum Erstellen von Komponenten verwendet, die Zugriff auf Assistentendienste wie die Komponentenerstellung und die Protokollierung benötigen.|  
|[WizardPageImpl-Vorlagenklasse](#WizardPageImplTemplateClass)|Diese Basisklasse sollte für alle benutzerdefinierten Assistentenseiten verwendet werden.|  

####  <a name="ClassFactoryImplClass"></a> ClassFactoryImpl-Klasse  
 Hierbei handelt es sich um eine nützliche Basisklasse zum Erstellen einer Klassenfactory, die Sie mit der Factoryregistrierung registrieren können.  

 Der folgende Ausschnitt wurde der Datei „LocationPage.h“ aus dem Beispielprojekt entnommen und dient der Definition der **ClassFactoryImpl**-Klasse.  

```  
#pragma once  

#include "ClassFactoryImpl.h"  

class LocationPageFactory :public ClassFactoryImpl  
{  
protected:  
    IUnknown *CreateNewInstance();  
};  
```  

 Der folgende Ausschnitt wurde der Datei „LocationPage.cpp“ für die Seite des Beispielassistenten entnommen und dient der Definition der Klassenfactory für diese Seite.  

```  
IUnknown *LocationPageFactory::CreateNewInstance()  
{  
    return static_cast<IWizardPage *>(new LocationPage);  
}  
```  

####  <a name="InterfaceTemplateClass"></a> Interface-Vorlagenklasse  
 Verwenden Sie diese Vorlagenklasse zum Erstellen einer Komponente, die mehr als eine Schnittstelle implementieren kann. Dies wird im folgenden Beispiel demonstriert:  

```  
classLocationPage :public Interface<IFieldCallback, WizardPageImpl<IDD_LOCATION_PAGE>>  
```  

 Durch diesen Code wird eine Verkettung von Basisklassen vorgenommen, durch die sowohl **IFieldCalback** als auch die Schnittstellen unterstützt werden, die von **WizardPageImpl** unterstützt werden (nämlich **IWizardPage**).  

####  <a name="PathHelperClass"></a> Path-Hilfsklasse  
 Diese Klasse stellt häufig verwendete Vorgänge für Dateien und Verzeichnisse bereit:  

```  
static inline std::wstring GetModulePath(HINSTANCE hModule)  
```  

 Auch der vollständige Pfad zur EXE- oder DLL-Datei kann mithilfe des Instanzhandles zurückgegeben werden, das Sie dieser Methode übergeben:  

```  
static inline std::wstring GetModuleFilename(HINSTANCE hModule)  
```  

 Des Weiteren kann die Klasse den vollständigen Pfad und Dateinamen der EXE- und DLL-Datei mithilfe des Instanzhandles zurückgeben, das Sie dieser Methode übergeben:  

```  
static inline std::wstring GetDirecotryName(LPCWSTR fullName)  
```  

 . . . oder auch nur den Pfad ohne Dateinamen:  

```  
static inline std::wstring GetFileName(LPCWSTR fullName)  
```  

 Bei einem gegebenen Pfad mit einem Dateinamen gibt die Path-Hilfsklasse nur den Dateinamen zurück:  

```  
static inline std::wstring Combine(LPCWSTR path, LPCWSTR name)  
```  

 Die Klasse kann ebenso eine neue Zeichenfolge zurückgeben, die sich aus dem Pfad und dem Dateinamen (oder einem anderen Pfad) zusammensetzt.  

####  <a name="PointerTemplateClass"></a> Pointer-Vorlagenklasse  
 Diese Klasse wird in der Datei „Pointer.h“ definiert. Da für die Verwaltung der Lebensdauer von COM-Komponenten eine Verweiszählung verwendet wird, ist es wichtig, dass Sie Schnittstellen freigeben, wenn Sie diese nicht mehr benötigen. Microsoft stellt eine Vorlagenklasse bereit, die die Lebensdauer automatisch verwaltet. Wenn Sie z.B. einen intelligenten Zeiger für eine XML-Schnittstelle nutzen möchten, könnten Sie folgenden Code verwenden:  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 In der ersten Zeile wird der intelligente Zeiger definiert. In der zweiten Zeile wird ein intelligenter Zeiger durch einen anderen Aufruf abgerufen. Durch den Operator **&** wird eine vorhandene Schnittstelle freigegeben und die Adresse für den internen Zeiger zurückgegeben. Nachdem Sie einen Zeiger auf diese Weise abgerufen haben, ruft die **Pointer**-Instanz **Release** auf, wenn der Gültigkeitsbereich der Variable endet. Microsoft empfiehlt die Nutzung intelligenter Zeiger anstelle des manuellen Aufrufs von **AddRef** und **Release**.  

 Die Klasse für intelligente Zeiger **Pointer** ruft darüber hinaus auch **QueryInterface** auf, wodurch weitere Schnittstellen abgerufen werden. Wenn z.B. die Factoryregistrierung eine neue Instanz einer Komponente erstellt, wird der folgende Code verwendet:  

```  
PWizardComponent pComp = pUnknown;  
if (pComp != nullptr)  
    pComp->SetContainer(m_pContainer);  
```  

 In der ersten Zeile wird **QueryInterface** im Hintergrund aufgerufen, wodurch die **IWizardComponent**-Schnittstelle angefordert wird. Der resultierende intelligente Zeiger entspricht **nullptr**, wenn die Komponente diese Schnittstelle nicht unterstützt.  

####  <a name="PUnkownClass"></a> PUnknown-Klasse  
 Diese Klasse ist ein intelligenter Zeiger für die **IUnknown**-Schnittstelle. Verwenden Sie für alle anderen Schnittstellen die **Pointer**-Vorlagenklasse.  

####  <a name="StringUtilHelperClass"></a> StringUtil-Hilfsklasse  
 Diese Klasse ist in der Datei „Utilities.h“ definiert und enthält Hilfsmethoden, die das Verwenden von Zeichenfolgen vereinfachen:  

```  
static inline int CompareIgnore(LPCWSTR first, LPCWSTR second)  
```  

 Diese Methode vergleicht zwei Zeichenfolgen und ignoriert dabei die Groß-/Kleinschreibung (siehe Tabelle 9).  

### <a name="table-9-stringutil-helper-class"></a>Tabelle 9: StringUtil-Hilfsklasse  

|**Zurückgegebener Wert**|**Beschreibung**|  
|-|-|  
|**0**|Die Zeichenfolgen stimmen überein. Die Groß-/Kleinschreibung wird nicht berücksichtigt.|  
|**< 0**|Erste Zeichenfolge < zweite Zeichenfolge|  
|**> 0**|Erste Zeichenfolge > zweite Zeichenfolge|  

 Der folgenden Codeausschnitt enthält Beispiele für weitere Methoden:  

```  
static inline std::wstring Format(LPCWSTR input, int index, LPCWSTR value)  
static inline std::wstring Format(LPCWSTR input, int index, DWORD value)  
```  

 Diese Methoden ähneln insofern den **Format**-Methoden von Microsoft .NET, als Parameter in der Form **{0}** geschrieben werden. Dadurch wird allerdings die Eingabe nicht formatiert. Stattdessen findet nur eine Ersetzung statt:  

```  
static inline std::wstring Printf(std::wstring format, I val)  
static inline std::wstring Printf(std::wstring format, I val1, J val2)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3, L val4)  
```  

 Es handelt sich also um Wrapper für **StringCchPrintf**, die einen Wert des Typs **wstring** zurückgeben und dafür sorgen, dass Sie nicht selbst Zeichenfolgen oder Puffern Speicher zuordnen müssen.  

####  <a name="SubInterfaceTemplateClass"></a> SubInterface-Vorlagenklasse  
 Diese Basisklasse erleichtert das Implementieren einer Komponente, die eine Schnittstelle unterstützt, die wiederum von einer anderen Schnittstelle erbt. Beispielsweise erbt die Schnittstelle **ICheckBox** von **IControl**. Im Folgenden Beispiel wird gezeigt, wie diese Klasse zum Definieren von **CheckBoxWrapper** verwendet wird:  

```  
classCheckBoxWrapper :public SubInterface<IControl, UnknownImpl<ICheckBox> >  
```  

 Die Basisschnittstelle ist der erste Parameter, die abgeleitete Schnittstelle der zweite.  

####  <a name="UnknownImplTemplateClass"></a> UnknownImpl-Vorlagenklasse  
 Diese Klasse ist in der Datei „UnknownImpl.h“ definiert und für viele Aufgaben zuständig, die beim Erstellen einer COM-Komponente anfallen. Der folgende Codeausschnitt stellt ein Beispiel für die Verwendungsweise der Basisklasse dar:  

```  
classDirectory :public UnknownImpl<IDirectory>  
```  

 In diesem Code wird eine Klasse definiert, die die **IDirectory**-Schnittstelle unterstützt.  

####  <a name="WizardComponentTemplateClass"></a> WizardComponent-Vorlagenklasse  
 Diese Klasse ist in der Datei „IWizardComponent.h“ definiert und eignet sich zum Erstellen von Komponenten, die Zugriff auf Assistentendienste wie die Komponentenerstellung und die Protokollierung benötigen.  

 Ein Beispiel ist die **CopyFilesTask**-Komponente, die folgendermaßen definiert wird:  

```  
classCopyFilesTask :public WizardComponent<ITask>  
{  
    ...  
```  

 Der Parameter für diese Vorlagenklasse ist die Hauptschnittstelle, die Sie für die Komponente verwenden möchten. Im Fall von Tasks ist dies **ITask**. Durch die Nutzung von **WizardComponent** unterstützt Ihre Komponente sowohl die von Ihnen bereitgestellte Schnittstelle (im vorliegenden Beispiel **ITask**) als auch **IWizardComponent**.  

 Sobald Sie mit der Klassenfactoryregistrierung eine neue Komponente erstellen, ruft die Registrierung die Methode **IWizardComponent->SetContainer** der Komponente auf, damit Ihre Komponenten auf die Assistentendienste zugreifen können.  

####  <a name="WizardPageImplTemplateClass"></a> WizardPageImpl-Vorlagenklasse  
 Verwenden Sie diese Klasse als Basisklasse für Ihre benutzerdefinierten Seiten. Dies wird im folgenden Beispiel demonstriert:  

```  
class LocationPage :public WizardPageImpl<IDD_LOCATION_PAGE>  
```  

 Der Parameter ist die Ressourcen-ID für Ihre Dialogfeldvorlage.  

###  <a name="WizardPageInterfaces"></a> Schnittstellen für die Assistentenseite  
 Der UDI-Assistent verwendet Schnittstellen, um auf unterschiedliche Steuerelemente auf Ihrer Seite zuzugreifen. Mit der **GetControlWrapper**-Funktion rufen Sie auf Ihrer Seite einen Wrapper für ein Steuerelement ab. Der folgenden Codeausschnitt enthält hierfür ein Beispiel:  

```  
PStaticText pFormat;  
GetControlWrapper(View(), IDC_CHECK_PARTITION, CONTROL_STATIC_TEXT, &pFormat);  
```  

 **PStaticText** ist ein intelligenter Zeiger auf die **IStaticText**-Schnittstelle. Intelligente Zeiger rufen automatisch die COM-Methode **Release()** auf, wenn deren Gültigkeitsbereich endet oder wenn Sie einer Methode die Adresse einer Variablen übergeben (beispielsweise durch **&pFormat**).  

#### <a name="iadhelper-interface"></a>IADHelper-Schnittstelle  

```  
__interfaceIADHelper : IUnknown  
{  
    HRESULT Init(ILogger *pLogger);  
    HRESULT ValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain);  
    HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain);  
};  

```  

##### <a name="hresult-initilogger-plogger"></a>HRESULT Init(ILogger \*pLogger)  
 Hierdurch wird die Komponente initialisiert und der Protokollierung übergeben.  

##### <a name="hresultvalidlogonlpctstr-username-lpctstr-password-lpctstr-domain"></a>HRESULTValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain)  
 Diese Methode überprüft, ob bestimmte Anmeldeinformationen gültig sind. Die möglichen Ergebnisse der Überprüfung sind in Tabelle 10 dargestellt.  

### <a name="table-10-hresultvalidlogon"></a>Tabelle 10: HResultValidLogon  

|**HResult**|**Beschreibung**|  
|-|-|  
|S_OK|Die Anmeldeinformationen sind gültig.|  
|S_FALSE|Die Anmeldeinformationen sind ungültig.|  
|E_FAIL|Der Domänencontroller wurde nicht gefunden. Weitere Informationen befinden sich in den Protokollen.|  

##### <a name="hresult-hasaccesslpctstr-username-lpctstr-password-lpctstr-domain-lpctstr-computername-lpctstr-accountdomain"></a>HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain)  
 Diese Methode überprüft, ob mit bestimmten Anmeldeinformationen Lese-/Schreibzugriff auf das Computerobjekt in AD DS besteht. Die möglichen Ergebnisse der Überprüfung sind in Tabelle 11 dargestellt.  

### <a name="table-11-hresult-hasaccess"></a>Tabelle 11: HResult HasAccess  

|**HRESULT**|**Beschreibung**|  
|-|-|  
|S_OK|Der Benutzer hat Zugriff.|  
|E_FAIL|Der Benutzer hat keinen Zugriff. Weitere Informationen befinden sich in der Protokolldatei.|  

#### <a name="ibackgroundtask-interface"></a>IBackgroundTask-Schnittstelle  

```  
__interface IBackgroundTask : IUnknown  
{  
    HRESULT Init(ITask *pTask, int id, IBackgroundCallback *pCallback);  
    void Start(void);  
    BOOL Running(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    HRESULT Terminate(DWORD exitCode);  
    HRESULT GetExitCode(LPDWORD pCode, HRESULT *pHresult);  
    HRESULT Close(void);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Die Seite **Fortschritt** verwendet diese Klasse, um Tasks in einem separaten Thread auszuführen. Sie können diese Klasse verwenden, um Vorgänge für einen eigenen Thread auszuführen. *Tasks* umfassen alle Klassen, die die **ITask**-Schnittstelle unterstützen.  

 Diese Schnittstelle wird von der Komponente **ID_BackgroundTask** („Microsoft.Wizard.BackgroundTask“) implementiert, die in der Schnittstelle der Datei „IBackgroundTask.h“ definiert ist.  

##### <a name="hresult-inititask-ptask-int-id-ibackgroundcallback-pcallback"></a>HRESULT Init(ITask \*pTask, int id, IBackgroundCallback \*pCallback)  
 Diese Schnittstelle initialisiert die Komponente. Details können Tabelle 12 entnommen werden.  

### <a name="table-12-hresult-init"></a>Tabelle 12: HRESULT Init  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**pTask**|Zeiger auf die Klasse, die den Code enthält, der in einem anderen Thread ausgeführt werden soll.|  
|**Id**|Eine Zahl, die mit der Rückrufmethode **Finished** verwendet wird, um festzustellen, welcher Task beendet wurde. Dieser Parameter ist hilfreich, wenn Sie mehrere Tasks mit derselben Rückrufmethode starten.|  
|**pCallback**|Eine Klasse, die die **Finished**-Methode implementiert. Letztere wird aufgerufen, wenn ein Task beendet wird. Der Aufruf der **Finished**-Methode findet nicht im Thread für die Benutzeroberfläche, sondern im Hintergrundthread statt.|  

##### <a name="void-startvoid"></a>void Start(void)  
 Diese Methode startet den Task in einem Hintergrundthread und gibt die in Tabelle 13 aufgeführten Elemente zurück.  

### <a name="table-13-return-background-thread"></a>Tabelle 13: Rückgabe des Hintergrundthreads  

|**Zurückgegebener Wert**|**Beschreibung**|  
|-|-|  
|**E_INVALIDARG**|Der Task wird bereits ausgeführt und kann aktuell nicht gestartet werden.|  
|**E_FAIL**|Beim Starten des Threads ist ein Problem aufgetreten.|  
|**S_OK**|Der Thread wurde gestartet.|  

##### <a name="bool-running"></a>BOOL Running()  
 Wenn der Hintergrundtask aktuell ausgeführt wird, gibt die Methode TRUE zurück, andernfalls FALSE.  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 Diese Methode wartet solange, bis der Thread beendet wird oder die Zeit in Millisekunden abgelaufen ist.  

##### <a name="hresult-terminatedword-exitcode"></a>HRESULT Terminate(DWORD exitCode)  
 Diese Methode beendet den Thread, der aktuell ausgeführt wird (siehe Tabellen 14 und 15). Dieser Prozess nimmt möglicherweise etwas Zeit in Anspruch, nachdem die Methode einen Wert zurückgegeben hat.  

### <a name="table-14-hresult-terminate-exit-code"></a>Tabelle 14: HRESULT Terminate – Exitcode  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**exitCode**|Der Exitcode, der an die Finished-Rückrufmethode gesendet wird. Dieser kann auch mit der **GetExitCode**-Methode abgerufen werden.|  

### <a name="table-15-termination-codes"></a>Tabelle 15: Beendigungscodes  

|**Zurückgegebener Wert**|**Beschreibung**|  
|-|-|  
|**E_FAIL**|Der Beendigungsaufruf ist fehlgeschlagen.|  
|**S_OK**|Der Beendigungsaufruf war erfolgreich.|  

##### <a name="hresult-getexitcodelpdword-pcode-hresult-phresult"></a>HRESULT GetExitCode(LPDWORD pCode, HRESULT \*pHresult)  
 Verwenden Sie diese Methode, um den Ergebniscode eines ausgeführten Tasks im Hintergrundthread abzurufen (siehe Tabelle 16).  

### <a name="table-16-result-codes"></a>Tabelle 16: Ergebniscodes  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**pCode**|Zeiger auf einen **DWORD**-Typ, der bei der Rückgabe festgelegt oder auf **nullptr** festgelegt wird, wenn Sie den Rückgabewert nicht benötigen. Bei Beendigung wird dieser Parameter auf **STILL_ACTIVE** festgelegt, wenn der Thread ausgeführt, der Code von der **Execute**-Methode des Tasks zurückgegeben oder der Wert der **Terminate**-Methode (falls ausgeführt) übergeben wird.|  
|**pHresult**|Zeiger auf einen **HRESULT**-Typ, der bei der Rückgabe festgelegt oder auf **nullptr** festgelegt wird, wenn Sie den **HRESULT**-Wert nicht benötigen.|  

##### <a name="hresult-closevoid"></a>HRESULT Close(void)  
 Diese Methode gibt den Hintergrundthread frei. Sie gibt **E_INVALIDARG** zurück, wenn der Thread gerade ausgeführt wird, andernfalls **S_OK**.  

#### <a name="icheckbox-interface"></a>ICheckBox-Schnittstelle  

```  
__interface ICheckBox : IControl  
{  
    void Check(BOOL check);  
    BOOL IsButtonChecked();  
};  
```  

##### <a name="void-checkbool-check"></a>void Check(BOOL check)  
 Legt den Aktivierungszustand des Steuerelements fest. Wenn für die Methode TRUE angegeben wird, wird das Kontrollkästchen aktiviert. Bei FALSE wird es deaktiviert.  

##### <a name="bool-isbuttonchecked"></a>BOOL IsButtonChecked()  
 Diese Methode gibt den aktuellen Aktivierungszustand eines Kontrollkästchens zurück.  

#### <a name="icombobox-interface"></a>IComboBox-Schnittstelle  

```  
__interface IComboBox : IControl  
{  
    HRESULT Bind([in] IBindableList *pList);  
    HRESULT Select(int index);  
    int Selected(void);  
    void Add([in] LPCTSTR caption);  
    HRESULT GetText([out, retval] LPBSTR pText);  
    void Clear();  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle wird durch die **CheckBoxWrapper**-Komponente implementiert. Mit der Hilfsfunktion **GetControlWrapper** und dem Typ **CONTROL_COMBO_BOX** rufen Sie eine Instanz dieser Komponente ab.  

##### <a name="hresult-bindin-ibindablelist-plist"></a>HRESULT Bind([in] IBindableList \*pList)  
 Verwenden Sie diese Methode, wenn Sie über eine Datenquelle verfügen, die die **IBindableList**-Schnittstelle implementiert. Das Listenfeld initialisiert den Inhalt mit den Beschriftungen aus dieser Liste.  

##### <a name="hresult-selectint-index"></a>HRESULT Select(int index)  
 Im Kombinationsfeld wird das Element am angegebenen Index ausgewählt.  

##### <a name="int-selectedvoid"></a>int Selected(void)  
 Diese Methode gibt den Index des ausgewählten Elements oder **-1** zurück, wenn kein Element ausgewählt wurde.  

##### <a name="void-addin-lpctstr-caption"></a>void Add([in] LPCTSTR caption)  
 Dem Kombinationsfeld wird manuell ein Element hinzugefügt.  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 Die Zeichenfolge des aktuell ausgewählten Elements im Kombinationsfeld wird abgerufen.  

##### <a name="void-clear"></a>void Clear()  
 Aus dem Kombinationsfeld werden alle Elemente entfernt.  

#### <a name="icontrol-interface"></a>IControl-Schnittstelle  

```  
__interface IControl : IUnknown  
{  
    HRESULT SetEnable(BOOL enable);  
    BOOL IsEnabled(void);  
    HRESULT SetVisible(BOOL visible);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle wird durch die **ControlWrapper**-Komponente implementiert. Mit der Hilfsfunktion **GetControlWrapper** und dem Typ **CONTROL_GENERIC** rufen Sie eine Instanz dieser Komponente ab.  

##### <a name="hresult-setenablebool-enable"></a>HRESULT SetEnable(BOOL enable)  
 Das Steuerelement wird aktiviert oder deaktiviert.  

##### <a name="bool-isenabledvoid"></a>BOOL IsEnabled(void)  
 Wenn das Steuerelement aktiviert wurde, wird TRUE zurückgegeben, andernfalls FALSE.  

##### <a name="hresult-setvisiblebool-visible"></a>HRESULT SetVisible(BOOL visible)  
 Das Steuerelement wird ausgeblendet oder angezeigt.  

#### <a name="icpuinfo-interface"></a>ICpuInfo-Schnittstelle  

```  
__interface ICpuInfo : IUnknown  
{  
    BOOL Is64Bit(void);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle rufen Sie durch das Erstellen einer neuen **ID_CpuInfo**-Komponente ab. Die Schnittstelle enthält genau eine Methode, mit der sich ermitteln lässt, ob für die CPU eine 32- oder eine 64-Bit-Architektur verwendet wird. Beachten Sie, dass diese Methode TRUE zurückgibt, wenn Sie ein 32-Bit-Betriebssystem auf einem 64-Bit-Computer ausführen, da nur die Wortbreite der CPU (nicht des Betriebssystems) berücksichtigt wird.  

##### <a name="idirectory-interface"></a>IDirectory-Schnittstelle  

```  
__interface IDirectory : IUnknown  
{  
    BOOL FileExists(LPCWSTR name);  
    BOOL FindFirst([in] LPCWSTR name);  
    HRESULT FoundName([out, retval] LPBSTR name);  
    DWORD FoundAttributes(void);  
    BOOL FindNext(void);  
    void FinishFind(void);  
};  
```  

###### <a name="overview"></a>Übersicht  
 Die **Directory**-Komponente, die Sie mit **ID_Directory** erstellen, stellt eine Fassade zum Verwenden von Verzeichnissen auf dem Dateisystem bereit.  

###### <a name="bool-fileexistslpcwstr-name"></a>BOOL FileExists(LPCWSTR name)  
 Diese Methode gibt TRUE zurück, wenn eine Datei mit dem von Ihnen angegebenen Namen vorhanden ist.  

###### <a name="bool-findfirstin-lpcwstr-name"></a>BOOL FindFirst([in] LPCWSTR name)  
 Diese Methode such nach der ersten Übereinstimmung mit dem von Ihnen angegebenen Namen. Sie unterstützt Platzhalterzeichen und gibt sowohl den Datei- als auch den Verzeichnisnamen zurück. Die Methode gibt TRUE zurück, wenn eine Übereinstimmung gefunden wurde, andernfalls FALSE.  

###### <a name="hresult-foundnameout-retval-lpbstr-name"></a>HRESULT FoundName([out, retval] LPBSTR name)  
 Diese Methode ruft den Namen der gefundenen Datei mit einem Aufruf von **FindFirst** oder **FindNext** ab.  

###### <a name="dword-foundattributesvoid"></a>DWORD FoundAttributes(void)  
 Diese Methode gibt das Attribut für die letzte gefundene Datei oder das letzte gefundene Verzeichnis zurück. Mit dem folgenden Code können Sie überprüfen, ob es sich bei dem Element um ein Verzeichnis handelt:  

```  
pDirectory->FoundAttributes() & FILE_ATTRIBUTE_DIRECTORY  
```  

###### <a name="bool-findnextvoid"></a>BOOL FindNext(void)  
 Die nächste Übereinstimmung wird gesucht. Diese Methode gibt TRUE zurück, wenn eine weitere Übereinstimmung gefunden wurde, andernfalls FALSE.  

###### <a name="void-finishfindvoid"></a>void FinishFind(void)  
 Diese Methode gibt für den Suchvorgang verwendete Ressourcen frei.  

#### <a name="idomainjoinvalidator-interface"></a>IDomainJoinValidator-Schnittstelle  

```  
__interface IDomainJoinValidator : IUnknown  
{  
    HRESULT Init(ILogger *pLogger, IWizardPageContainer *pContainer, IStaticText *pUsername, IStaticText *pPassword, IStaticText *pComputerName);  
    HRESULT IsUsernameValid(LPCWSTR domainName);  
    BOOL CanModifyComputerAdEntry(LPCWSTR domainName);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Eine Instanz dieser Schnittstelle erhalten Sie durch den Aufruf der **CreateInstance**-Vorlagenfunktion mit dem **ID_DomainJoinValidator**-Wert.  

##### <a name="hresult-initilogger-plogger-iwizardpagecontainer-pcontainer-istatictext-pusername-istatictext-ppassword-istatictext-pcomputername"></a>HRESULT Init(ILogger \*pLogger, IWizardPageContainer \*pContainer, IStaticText \*pUsername, IStaticText \*pPassword, IStaticText \*pComputerName)  
 Die Instanz wird mit den in Tabelle 17 aufgeführten Parametern initialisiert.  

### <a name="table-17-hresult-init---instance-initialization"></a>Tabelle 17: HRESULT Init – Instanzinitialisierung  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**pLogger**|Die Protokollierungsinstanz, die auf Ihrer Seite mit der **Logger**-Methode verwendet werden kann.|  
|**pContainer**|Die Ergebnisse, die mit der **Container**-Methode Ihrer Seite übergeben werden.|  
|**pUsername**|Das Textfeld mit dem Benutzernamen, der überprüft werden soll.|  
|**pPassword**|Das Textfeld mit dem Kennwort, das überprüft werden soll.|  
|**PComputerName**|Das Textfeld mit dem Namen des Computers, der der Domäne hinzugefügt werden soll.|  

##### <a name="hresult-isusernamevalidlpcwstr-domainname"></a>HRESULT IsUsernameValid(LPCWSTR domainName)  
 Diese Methode verwendet zur Durchführung ihrer Aufgaben die Methode **IADHelper->ValidLogon**. Weitere Informationen finden Sie im Abschnitt zur letztgenannten Methode.  

##### <a name="bool-canmodifycomputeradentrylpcwstr-domainname"></a>BOOL CanModifyComputerAdEntry(LPCWSTR domainName)  
 Mit dieser Methode wird überprüft, ob der Benutzer berechtigt ist, den Computereintrag zu ändern. Die meisten Aufgaben werden von **IADHelper->HasAccess** durchgeführt. Wenn diese Methode FALSE zurückgibt, finden Sie in der Protokolldatei weitere Informationen.  

#### <a name="idrivelist-interface"></a>IDriveList-Schnittstelle  

```  
__interface IDriveList : IUnknown  
{  
    HRESULT Init(IWmiRepository *pWmi);  
    HRESULT SetWhereClause(LPCTSTR whereClause);  
    HRESULT SetMinimumDriveSize(__int64 size);  
    HRESULT Update(void);  
    HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned);  

    size_t Count(void);  
    HRESULT GetProperty(size_t index, LPCTSTR propName,  LPVARIANT value);  
    HRESULT GetCaption(size_t index,  LPBSTR pCaption);  
}  
```  

##### <a name="hresult-initiwmirepository-pwmi"></a>HRESULT Init(IWmiRepository \*pWmi)  
 Rufen Sie diese Methode vor dem Aufruf aller anderen Komponenten auf. Sie müssen vor dem Aufruf dieser Methode ein neues **WMI-Repository** erstellen.  

##### <a name="hresult-setwhereclauselpctstr-whereclause"></a>HRESULT SetWhereClause(LPCTSTR whereClause)  
 Mit dieser Methode können Sie Text hinzufügen, der als WHERE-Klausel in der Abfrage angezeigt wird. Mit der folgenden Codezeile werden beispielsweise nur USB-Laufwerke zurückgegeben:  

```  
pDrives->SetWhereClause(L"WHERE InterfaceType='USB'");  
```  

##### <a name="hresult-setminimumdrivesizeint64-size"></a>HRESULT SetMinimumDriveSize(\__int64 size)  
 Legen Sie in Byte die Mindestgröße für Laufwerke fest, die von der Abfrage zurückgegeben werden.  

##### <a name="hresult-updatevoid"></a>HRESULT Update(void)  
 Mit dieser Methode wird die Abfrage ausgeführt. Die Liste der Laufwerke, die nach dem Aufrufen dieser Methode zur Verfügung steht, wird nach dem Laufwerkbuchstaben sortiert.  

##### <a name="hresult-addpropertyenumdiskquerysection-section-lpctstr-propname-lpctstr-propnamereturned"></a>HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned)  
 Diese Methode fügt die Namen zusätzlicher Eigenschaften hinzu, die Sie in den Abfrageergebnissen verfügbar machen möchten. Rufen Sie diese Methode vor dem Aufruf von **Update** auf. In Tabelle 18 werden drei nützliche Eigenschaften aufgeführt.  

### <a name="table-18-hresult-addproperty-useful-properties"></a>Tabelle 18: HRESULT AddProperty – nützliche Eigenschaften  

|**Abschnitt**|**Eigenschaft**|**Beschreibung**|  
|-|-|-|  
|**DISKQUERY_LOGICALDISK**|**Size**|Die Größe in Byte; als Zeichenfolge dargestellt.|  
|**DISKQUERY_DISKPARTITION**|**DiskIndex**|Die Laufwerknummer als ganze Zahl; beginnt mit 0.|  
|**DISKQUERY_LOGICALDISK**|**VolumeName**|Die Volumebezeichnung.|  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 Die Anzahl der Datensätze, die von der Abfrage zurückgegeben werden. Rufen Sie vor dem Aufruf dieser Methode **Update** auf.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propname--lpvariant-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propName, LPVARIANT value)  
 Diese Methode ruft den Wert einer Eigenschaft aus den Abfrageergebnissen ab, wie in Tabelle 19 wird.  

### <a name="table-19-hresult-getproperty"></a>Tabelle 19: HRESULT GetProperty  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**Index**|Nullbasierter Index für den Ergebnisdatensatz.|  
|**propName**|Name der Eigenschaft, beispielsweise „Size“.|  
|**Wert**|Dieser Parameter enthält bei der Rückgabe einen Variant-Wert der Eigenschaft.|  

##### <a name="hresult-getcaptionsizet-index--lpbstr-pcaption"></a>HRESULT GetCaption(size_t index, LPBSTR pCaption)  
 Diese Methode ruft den Beschriftungstext eines Datensatzes ab. Dieser Text entspricht der **Caption**-Eigenschaft.  

#### <a name="iimagelist-interface"></a>IImageList-Schnittstelle  

```  
__interface IImageList  
{  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    HImageList GetImageList(void);  
    int AddImage(HInstance hInstance, int resourceId);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle wird durch die **ImageList**-Komponente implementiert. Über die Schnittstelle **IListView** rufen Sie eine Instanz dieser Komponente ab.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Mit dieser Methode wird eine neue Bildliste erstellt, die von der Komponente verwaltet wird. Rufen Sie diese Methode nur einmal auf.  

##### <a name="himagelist-getimagelistvoid"></a>HImageList GetImageList(void)  
 Diese Methode gibt das Handle für die Bildliste zurück, falls Sie andere Vorgänge für die Bildliste ausführen müssen.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HInstance hInstance, int resourceId)  
 Mit dieser Methode wird der Bildliste ein neues Bild aus einer Ressource hinzugefügt. Details können Tabelle 20 entnommen werden.  

### <a name="table-20-hresult-iimagelist-interface"></a>Tabelle 20: HRESULT – IImageList-Schnittstelle  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**hInstance**|Instanzhandle des Moduls, das die Bitmapressource enthält.|  
|**resourceId**|ID der Ressource, aus der das Bild der Bildliste hinzugefügt wird.|  

#### <a name="ilistview-interface"></a>IListView-Schnittstelle  

```  
__interface IListView : IControl  
{  
    int AddItem([in] LPCTSTR text);  
    int AddColumn(int width, [in] LPCTSTR text);  
    HRESULT SetSubItem(int index, int column, [in] LPCTSTR text);  
    int GetWidth(void);  
    void SetExtendedStyle(DWORD style);  
    int GetSelectedItem(void);  
    HRESULT SelectItem(int index);  
    BOOL IsItemChecked(int index);  
    int GetItemCount(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  
    HRESULT SetImage(int index, int imageIndex);  
    HRESULT Clear(void);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle wird durch die **ControlWrapper**-Komponente implementiert. Mit der Hilfsfunktion **GetControlWrapper** und dem Typ **CONTROL_LIST_VIEW** rufen Sie eine Instanz dieser Komponente ab.  

##### <a name="int-additemin-lpctstr-text"></a>int AddItem([in] LPCTSTR text)  
 Mit dieser Methode wird dem Listenfeld eine neue Zeile hinzugefügt. Die Methode gibt den Index des hinzugefügten Elements zurück.  

##### <a name="int-addcolumnint-width-in-lpctstr-text"></a>int AddColumn(int width, [in] LPCTSTR text)  
 Mit dieser Methode wird der Listenansicht eine neue Spalte hinzugefügt.  

##### <a name="hresult-setsubitemint-index-int-column-in-lpctstr-text"></a>HRESULT SetSubItem(int index, int column, [in] LPCTSTR text)  
 Mit dieser Methode wird der Text einer Spalte festgelegt, die nicht der ersten Spalte des Listenfelds entspricht. Details können Tabelle 21 entnommen werden.  

### <a name="table-21-hresult-setsubitem"></a>Tabelle 21: HRESULT – SetSubItem  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**index**|Der Index des Listenelements, das geändert werden soll.|  
|**column**|Der Index der Spalte, die aktualisiert werden soll. Die erste Spalte wird durch **AddItem** festgelegt. Alle folgenden Spalten werden mit dieser Methode festgelegt.|  
|**text**|Die Zeichenfolge, die in der Spalte angezeigt werden soll.|  

##### <a name="int-getwidthvoid"></a>int GetWidth(void)  
 Diese Methode gibt die Breite des Textfelds zurück.  

##### <a name="void-setextendedstyledword-style"></a>void SetExtendedStyle(DWORD style)  
 Mit dieser Methode können erweiterte Stile für das Listenfeld festgelegt werden. Dies wird im folgenden Beispiel demonstriert:  

```  
m_pList->SetExtendedStyle(LVS_EX_FULLROWSELECT);  
```  

##### <a name="int-getselecteditemvoid"></a>int GetSelectedItem(void)  
 Diese Methode gibt den Index des Elements zurück, das aktuell in der Listenansicht ausgewählt ist.  

##### <a name="hresult-selectitemint-index"></a>HRESULT SelectItem(int index)  
 Mit dieser Methode wird das Listenelement am angegebenen Index ausgewählt.  

##### <a name="bool-isitemcheckedint-index"></a>BOOL IsItemChecked(int index)  
 Diese Methode gibt TRUE zurück, wenn ein Element in der Liste ausgewählt ist. Voraussetzung zum Aufruf dieser Methode ist, dass **SetExtendedStyle** zum Festlegen des Kontrollkästchenstils aufgerufen wurde.  

##### <a name="int-getitemcountvoid"></a>int GetItemCount(void)  
 Diese Methode gibt die Anzahl der Elemente in der Listenansicht zurück.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Mit dieser Methode wird eine neue Bildliste erstellt, die der Listenansicht angefügt wird.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 Mit dieser Methode wird der Bildliste der Bildansicht ein Bild hinzugefügt. Sie müssen vor dem Aufruf dieser Methode zuerst **CreateImageList** aufrufen.  

##### <a name="hresult-setimageint-index-int-imageindex"></a>HRESULT SetImage(int index, int imageIndex)  
 Mit dieser Methode wird das Bild festgelegt, das links neben einem bestimmten Element der Listenansicht angezeigt wird.  

##### <a name="hresult-clearvoid"></a>HRESULT Clear(void)  
 Mit dieser Methode werden alle Elemente aus der Listenansicht entfernt.  

#### <a name="iprogressbar-interface"></a>IProgressBar-Schnittstelle  

```  
__interface IProgressBar : IControl  
{  
    HRESULT SetPercentage(int position);  
    int GetPercentage(void);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle wird durch die **ProgressBarWrapper**-Komponente implementiert. Mit der Hilfsfunktion **GetControlWrapper** und dem Typ **CONTROL_PROGRESS_BAR** rufen Sie eine Instanz dieser Komponente ab.  

##### <a name="hresult-setpercentageint-position"></a>HRESULT SetPercentage(int position)  
 Mit dieser Methode wird der Fortschritt innerhalb der Statusanzeige mit einer Zahl zwischen 0 und 100 festgelegt. In Win32®-Statusanzeigen wird ein Standardbereich der Größe 100 verwendet.  

##### <a name="int-getpercentagevoid"></a>int GetPercentage(void)  
 Diese Methode gibt den aktuellen Fortschritt der Statusanzeige zurück.  

#### <a name="iradiobutton-interface"></a>IRadioButton-Schnittstelle  

```  
__interface IRadioButton : IControl  
{  
public:  
    void SetGroup(int firstId, int lastId);  
    void CheckRadio(int id);  
    BOOL IsButtonChecked(int id);  
    void EnableRadio(int id, BOOL enable);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle wird durch die **RadioButtonWrapper**-Komponente implementiert. Mit der Hilfsfunktion **GetControlWrapper** und dem Typ **CONTROL_RADIO_BUTTON** rufen Sie eine Instanz dieser Komponente ab.  

##### <a name="void-setgroupint-firstid-int-lastid"></a>void SetGroup(int firstId, int lastId)  
 Mit dieser Methode wird der Wrapper mit dem Bereich der Optionsfelder festgelegt, der als Gruppe behandelt werden soll. Rufen Sie diese Methode auf, bevor Sie **CheckRadio** aufrufen.  

##### <a name="void-checkradioint-id"></a>void CheckRadio(int id)  
 Mit dieser Methode wird ausschließlich das angegebene Optionsfeld innerhalb der ausgewählten Gruppe der Optionsfelder aktiviert. Rufen Sie **SetGroup** auf, bevor Sie diese Methode aufrufen.  

##### <a name="bool-isbuttoncheckedint-id"></a>BOOL IsButtonChecked(int id)  
 Diese Methode gibt TRUE zurück, wenn das Optionsfeld aktuell aktiviert ist, andernfalls FALSE.  

##### <a name="void-enableradioint-id-bool-enable"></a>void EnableRadio(int id, BOOL enable)  
 Diese Methode aktiviert oder deaktiviert ein Optionsfeld.  

#### <a name="istatictext-interface"></a>IStaticText-Schnittstelle  

```  
__interface IStaticText : IControl  
{  
    HRESULT SetText([in] LPCTSTR pText);  
    HRESULT GetText([out, retval] LPBSTR pText);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle wird durch die **StaticTextWrapper**-Komponente implementiert. Mit der Hilfsfunktion **GetControlWrapper** und dem Typ **CONTROL_STATIC_TEXT** rufen Sie eine Instanz dieser Komponente ab.  

##### <a name="hresult-settextin-lpctstr-ptext"></a>HRESULT SetText([in] LPCTSTR pText)  
 Mit dieser Methode wird der Text für das Steuerelement festgelegt.  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 Diese Methode gibt den aktuellen Textwert des Steuerelements zurück.  

####  <a name="ITaskinterface"></a> ITask-Schnittstelle  

```  
__interface IControl : IUnknown  
{  
    HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings);  
    HRESULT Execute(LPDWORD pReturnCode);  
};  
```  

 Diese Schnittstelle können Sie implementieren, wenn Ihre Komponente als Task auf der Preflightseite verfügbar sein soll oder wenn Sie die **BackgroundTask**-Komponente verwenden möchten, um Aufgaben in einem Hintergrundthread auszuführen.  

 Die folgenden Komponenten implementieren die **ITask**-Schnittstelle:  

-   ID_ShellExecuteTask, L"Microsoft.Wizard.ShellExecuteTask"  

-   ID_CopyFilesTask, L"Microsoft.Wizard.CopyFilesTask"  

-   ID_ACPowerTask, L"Microsoft.OSDRefresh.ACPowerTask"  

-   ID_WiredNetworkTask, L"Microsoft.SharedPages.WiredNetworkTask"  

##### <a name="init"></a>Anfangsstatus  

```  
HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings)  
```  

 Wenn Sie einen Task für die Preflightseite schreiben, rufen Sie diese Methode zur Initialisierung des Tasks auf. Die Konfigurationsdatei kann beispielsweise folgenden XML-Code enthalten:  

```  
<Task DisplayName="Check Windows Scripting Host" Type="Microsoft.Wizard.ShellExecuteTask">  
  <Setter Property="filename">%windir%\system32\cscript.exe</Setter>  
  <Setter Property="parameters">Preflight\OSDCheckWSH.vbs</Setter>  
  <Setter Property="BitmapFilename">images\WinScriptHost.bmp</Setter>  
  <ExitCodes>  
    <ExitCode State="Success" Type="0" Value="0" Text="" />  
    <ExitCode State="Error" Type="-1" Value="*" Text="Windows Scripting Host not installed." />  
  </ExitCodes>  
</Task>  
```  

 Durch den **pProperties**-Parameter kann auf die drei Setter-Werte zugegriffen werden, und der **pTaskSettings**-Parameter ermöglicht den Zugriff auf das **Task**-Element und die untergeordneten Elemente. Die meisten Tasks müssen Daten des **pProperties**-Parameters nur lesen.  

#####  <a name="Execute"></a> Execute  

```  
HRESULT Execute(LPDWORD pReturnCode)  
```  

 Hier schreiben Sie den Code zur Ausführung des Tasks. Diese Methode gibt **S_OK** zurück, wenn keine Fehler auftreten. Ein anderer **HRESULT**-Wert kann zurückgegeben werden, wenn während der Ausführung des Tasks ein Fehler auftritt. Andere Werte als **S_OK**, die diese Methode zurückgibt, werden <Error\>-Elementen im Abschnitt <ExitCodes\> zugeordnet, wenn Sie die Preflightseite verwenden.  

 Der **pReturnCode**-Parameter muss mit einer Zahl aktualisiert werden, die den Zustand des Tasks angibt. Diese Werte werden von der Preflightseite den < ExitCode\>-Elementen zugeordnet.  

#### <a name="itreeview-interface"></a>ITreeView-Schnittstelle  

```  
__interface ITreeView : IControl  
{  
    void EnableCheckboxes(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  

    HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL);  
    void SetImage(HTREEITEM item, int image, int expandImage);  

    void Clear(void);  
    BOOL SetFirstVisible(HTREEITEM item);  
    BOOL SelectItem(HTREEITEM item);  
    void CheckItem(HTREEITEM item, UINT checkState);  
    HTREEITEM SelectedItem(void);  
    int SetItemHeight(SHORT height);  
    HRESULT EnableItem(HTREEITEM item, BOOL enable);  
    void Expand(HTREEITEM hItem, BOOL expand);  

    HTREEITEM GetChild(HTREEITEM hParent);  
    HTREEITEM GetParent(HTREEITEM hNode);  
    HTREEITEM GetNextItem(HTREEITEM hPrevious);  

    UINT IsChecked(HTREEITEM item);  
    BOOL IsEnabled(HTREEITEM item);  

    INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL *pCancel);  
    HRESULT SetEventHandler(ITreeViewEvent *pEventHandler);  

    void SetSelectedBackColor(COLORREF color);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle wird durch die **TreeViewWrapper**-Komponente implementiert. Mit der Hilfsfunktion **GetControlWrapper** und dem Typ **CONTROL_TREE_VIEW** rufen Sie eine Instanz dieser Komponente ab.  

##### <a name="void-enablecheckboxesvoid"></a>void EnableCheckboxes(void)  
 Diese Methode aktiviert Kontrollkästchen im Strukturansicht-Steuerelement durch Festlegen des **TVS_CHECKBOXES**-Stils.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Mit dieser Methode wird dem Strukturansicht-Steuerelement eine neue Bildliste hinzugefügt. Der **flags**-Parameter wird der aufgerufenen **ImageList_Create**-Win32-Funktion übergeben.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 Mit dieser Methode wird der Bildliste ein Bild aus einer Ressource (**resourceId**) im Modul mit dem Instanzhandle **hInstance** hinzugefügt.  

##### <a name="htreeitem-additemlpctstr-text-htreeitem-hparent--null"></a>HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL)  
 Mit dieser Methode wird der Strukturansicht ein Knoten hinzugefügt. Der neue Knoten wird auf der obersten Ebene hinzugefügt, wenn **hParent** NULL ist. Andernfalls muss das Handle dem übergeordneten Element übergeben werden, an das das neue Element angefügt werden soll. Diese Methode gibt das Handle für das neue Element zurück.  

##### <a name="void-setimagehtreeitem-item-int-image-int-expandimage"></a>void SetImage(HTREEITEM item, int image, int expandImage)  
 Mit dieser Methode wird ein Bild festgelegt, das für ein Strukturansichtselement verwendet werden soll. Sie können sowohl das normale als auch das erweiterte Bild festlegen.  

##### <a name="void-clearvoid"></a>void Clear(void)  
 Mit dieser Methode werden alle Elemente aus der Strukturansicht entfernt.  

##### <a name="bool-setfirstvisiblehtreeitem-item"></a>BOOL SetFirstVisible(HTREEITEM item)  
 Mit dieser Methode wird sichergestellt, dass das Strukturansichtselement angezeigt wird. In der Strukturansicht wird ggf. automatisch nach unten gescrollt, damit dieses Element angezeigt wird.  

##### <a name="bool-selectitemhtreeitem-item"></a>BOOL SelectItem(HTREEITEM item)  
 Mit dieser Methode wird die Auswahl des aktuell ausgewählten Elements aufgehoben, und das bereitgestellte Element wird ausgewählt. Sie können anschließend **SetFirstVisible** aufrufen, um sicherzustellen, dass das neu ausgewählte Element angezeigt wird.  

##### <a name="void-checkitemhtreeitem-item-uint-checkstate"></a>void CheckItem(HTREEITEM item, UINT checkState)  
 Mit dieser Methode wird das Bild festgelegt, das für das Kontrollkästchen in der Strukturansicht angezeigt werden soll. Das Bild befindet sich in einem eigenen **ImageList**-Steuerelement, das von der Strukturansicht verwaltet wird. Standardmäßig enthält diese Bildliste drei Bilder. Details können Tabelle 22 entnommen werden.  

### <a name="table-22void-checkitem-image-list-default"></a>Tabelle 22: void CheckItem – Standardbildliste  

|**checkState**|**Beschreibung**|  
|-|-|  
|**0**|Leer|  
|**1**|Deaktiviert|  
|**2**|Ausgewählt|  

##### <a name="htreeitem-selecteditemvoid"></a>HTREEITEM SelectedItem(void)  
 Diese Methode gibt das Handle des Strukturansichtselements zurück, das aktuell in der Strukturansicht ausgewählt ist.  

##### <a name="int-setitemheightshort-height"></a>int SetItemHeight(SHORT height)  
 Diese Methode legt die Höhe aller Elemente im Strukturansicht-Steuerelement in Pixeln fest. Die vorherige Höhe wird in Pixeln zurückgegeben.  

##### <a name="hresult-enableitemhtreeitem-item-bool-enable"></a>HRESULT EnableItem(HTREEITEM item, BOOL enable)  
 Diese Methode aktiviert oder deaktiviert ein einzelnes Element in der Struktur. Wenn ein Element mit untergeordneten Elementen deaktiviert wird, werden die untergeordneten Elemente nicht deaktiviert.  

##### <a name="void-expandhtreeitem-hitem-bool-expand"></a>void Expand(HTREEITEM hItem, BOOL expand)  
 Diese Methode erweitert oder reduziert einen Knoten in der Struktur.  

##### <a name="htreeitem-getchildhtreeitem-hparent"></a>HTREEITEM GetChild(HTREEITEM hParent)  
 Diese Methode gibt das erste untergeordnete Element eines Strukturansichtselements oder NULL zurück, wenn keine untergeordneten Elemente vorhanden sind.  

##### <a name="htreeitem-getparenthtreeitem-hnode"></a>HTREEITEM GetParent(HTREEITEM hNode)  
 Diese Methode gibt das Handle des übergeordneten Elements für einen Knoten in der Strukturansicht oder NULL zurück, wenn sich der Knoten auf der obersten Ebene befindet.  

##### <a name="htreeitem-getnextitemhtreeitem-hprevious"></a>HTREEITEM GetNextItem(HTREEITEM hPrevious)  
 Sie können diese Methode mit einem von **GetChild** zurückgegebenen Handle aufrufen, um alle untergeordneten Elemente eines Knotens zu durchlaufen. Diese Methode gibt das nächste gleichgeordnete Strukturelement zurück, das über dasselbe übergeordnete Element verfügt.  

##### <a name="uint-ischeckedhtreeitem-item"></a>UINT IsChecked(HTREEITEM item)  
 Diese Methode gibt **0** zurück, wenn der Strukturansichtsknoten aktiviert wurde, andernfalls **1**.  

##### <a name="bool-isenabledhtreeitem-item"></a>BOOL IsEnabled(HTREEITEM item)  
 Diese Methode gibt TRUE zurück, wenn der Strukturansichtsknoten aktiviert ist, andernfalls FALSE.  

##### <a name="intptr-commoncontroleventword-controlid-void-pinfo-bool-pcancel"></a>INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL \*pCancel)  
 Diese Methode ist nur zur internen Verwendung.  

##### <a name="hresult-seteventhandleritreeviewevent-peventhandler"></a>HRESULT SetEventHandler(ITreeViewEvent \*pEventHandler)  
 Rufen Sie diese Methode auf, wenn Sie Benachrichtigungen erhalten möchten, wenn das ausgewählte Element geändert wird oder der Benutzer den Aktivierungszustand eines Strukturansichtselements ändert. Sie müssen **ITreeViewEvent** in Ihre Komponente implementieren, um diese Rückrufe zu erhalten.  

##### <a name="void-setselectedbackcolorcolorref-color"></a>void SetSelectedBackColor(COLORREF color)  
 Festlegen der Hintergrundfarbe für das ausgewählte Element.  

#### <a name="iwmiiteration-interface"></a>IWmiIteration-Schnittstelle  

```  
__interface IWmiIterator : IUnknown  
{  
    HRESULT Next(void);  
    HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue);  
};  
```  

##### <a name="overview"></a>Übersicht  
 In der Regel wird diese Schnittstelle gemeinsam mit **IWmiRepository** verwendet, wenn mit WMI-Aufrufen gearbeitet wird. Die Schnittstelle **IWmiIteration** ermöglicht Ihnen das Durchlaufen der Werte, die von einer Abfrage zurückgegeben werden.  

##### <a name="hresult-nextvoid"></a>HRESULT Next(void)  
 Navigiert zum nächsten Element in den Abfrageergebnissen. Details können Tabelle 23 entnommen werden.  

### <a name="table-23-hresult-nextvoid-query-returns"></a>Tabelle 23: Rückgabe der Abfrage HRESULT Next(void)  

|**HRRESULT**|**Beschreibung**|  
|-|-|  
|**S_OK**|Auf das nächste Ergebnis verschoben. Sie können **GetProperty** verwenden, um Eigenschaften dieses Ergebnisses abzurufen.|  
|**S_FALSE**|In der Liste sind keine Elemente mehr vorhanden.|  
|**E_NOT_SET**|Es sind keine Abfrageergebnisse vorhanden.|  

##### <a name="hresult-getpropertylpctstr-propertyname-out-lpvariant-pvalue"></a>HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue)  
 Diese Methode ruft den Wert einer Eigenschaft aus dem aktuellen Ergebnisdatensatz ab, wie in Tabelle 24 und Tabelle 25 gezeigt wird.  

### <a name="table-24-hresult-getproperty"></a>Tabelle 24: HRESULT GetProperty  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**propertyName**|Name der Eigenschaft, die Sie abrufen möchten.|  
|**pValue**|Verweist auf eine VARIANT-Struktur, die bei der Ausgabe den Eigenschaftswert enthält.|  

### <a name="table-25-hresult-getproperty-result"></a>Tabelle 25: Ergebnis von HRESULT GetProperty  

|**HRESULT**|**Beschreibung**|  
|-|-|  
|**S_OK**|Der Eigenschaftswert wurde abgerufen.|  
|**WBEM_E_NOT_FOUND**|Es gibt keine Eigenschaft mit diesem Namen.|  
|**E_NOT_VALID_STATE**|Es ist kein aktueller Datensatz vorhanden.|  

> [!NOTE]
>  Die Methode **GetProperty** kann andere WMI-Fehlercodes zurückgeben, die nicht in der Tabelle 25 aufgelistet sind. Die aufgeführten Werte sind häufig zurückgegebene Ergebnisse.  

#### <a name="iwmirepository-interface"></a>IWmiRepository-Schnittstelle  

```  
__interface IWmiRepository : IUnknown  
{  
    HRESULT SetNamespace(LPCWSTR namespaceName);  
    HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle wird durch die Komponente **WmiRepository** (**ID_WmiRepository**) zurückgegeben.  

##### <a name="hresult-setnamespacelpcwstr-namespacename"></a>HRESULT SetNamespace(LPCWSTR namespaceName)  
 Diese Methode legt den WMI-Namespace fest, der für die Abfrage verwendet wird. Rufen Sie diese Methode auf, bevor Sie **ExecQuery** aufrufen. Wenn Sie diese Methode nicht aufrufen, ist der Namespace „root\cimv2“. Diese Methode gibt immer **S_OK** zurück.  

##### <a name="hresult-execquerylpcwstr-query-out-iwmiiterator-ppiterator"></a>HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator)  
 Führen Sie eine Abfrage für den WMI-Namespace mit einem Aufruf von **SetNamespace** aus, wie in Tabelle 26 und Tabelle 27 dargestellt wird.  

### <a name="table-26-hresult-execquery"></a>Tabelle 26: HRESULT ExecQuery  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**Query**|Die Zeichenfolge für die WMI-Abfrage, die Sie ausführen möchten.|  
|**ppIterator**|Übergibt einen Zeiger an einen Schnittstellenzeiger, der bei der Rückgabe mit einer Schnittstelle gefüllt wird, wodurch Ihnen Zugriff auf die Abfrageergebnisse gewährt wird.|  

### <a name="table-27-hresult-query-result"></a>Tabelle 27: HRESULT-Abfrageergebnis  

|**HRESULT**|**Beschreibung**|  
|-|-|  
|**S_OK**|Die Abfrage war erfolgreich.|  
|**Other**|Wenn die Abfrage nicht erfolgreich war, wird WMI **HRESULT** zurückgegeben.|  

#### <a name="iformcontroller-interface"></a>IFormController-Schnittstelle  

```  
__interface IFormController : IUnknown  
{  
    Init(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    SetPageInfo(ISettingsProperties *pPageInfo);  

    Validate(void);  

    AddToGroup(int groupControlId, int controlId);  
    UpdateCheckGroup(int groupControlId);  
    AddValidator(int controlId, IValidator *pValidator, IControl *pCOntrol = 0);  

    AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr);  
    DisableValidation(int controlId, BOOL disable);  

    AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type);  
    AddRadioGroup(LPCWSTR groupName, int radioControlId);  
    EnableRadioGroup(LPCWSTR groupName, BOOL enable);  
    InitFields(IFieldCallback *pFieldCallback = nullptr);  
    SaveFields(IFieldCallback *pFieldCallback = nullptr);  
    BOOL IsFieldDisabled(int controlId);  

    InitSection(LPCWSTR key, LPCWSTR sectionCaption);  
    AddSummaryItem(LPCWSTR first, LPCWSTR second);  
    SuppressLogValue(LPCWSTR tsVariableName);  
    SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption);  
    LoadText(int controlId, LPCWSTR tsVariableName);  

    void ControlEvent(WORD eventId, WORD controlId);  
    BOOL IsValid(void);  
 };  
```  

##### <a name="overview"></a>Übersicht  
 Jede Seite im UDI-Assistenten verfügt über einen eigenen Formularcontroller, der diese Schnittstelle implementiert. Verwenden Sie diesen Controller zum Herstellen einer Verbindung zwischen den Felddaten in der XML-Konfigurationsdatei und den Steuerelementen auf Ihrer Seite. Der Formularcontroller übernimmt dann viele Details für Sie.  

#####  <a name="SettingUptheForm"></a> Einrichten des Formulars  
 Den Formularcontroller können Sie im Allgemeinen in der **OnWindowCreated**-Methode Ihrer Seite einrichten. Dazu müssen Sie in der Regel die in Tabelle 28 aufgeführten Methoden aufrufen.  

### <a name="table-28-onwindowcreated-method"></a>Tabelle 28: OnWindowCreated-Methode  

|**Methode**|**Beschreibung**|  
|-|-|  
|**Init**|Initialisiert den Formularcontroller.|  
|**AddField**|Stellt eine Verbindung zwischen einem Feld in der XML-Konfigurationsdatei, das ein Zeichenfolgename ist, und einem Steuerelement im Dialogfeld Ihrer Seite her, das eine ID ist.|  
|**AddRadioGroup**|Wird zum Verbinden eines Optionsfelds mit sowohl einer Gruppe als auch einem Steuerelement in Ihrem Dialogfeld verwendet.|  
|**AddToGroup**|Ermöglicht „untergeordnete“ Steuerelemente, die zusammen mit den übergeordneten Elementen oder basierend auf dem ausgewählten Optionsfeld aktiviert oder deaktiviert werden.|  
|**InitFields**|Rufen Sie diese Methode auf, wenn Sie die **Add**-Methoden zum Einrichten des Formulars aufgerufen haben.|  
|**Validate**|Führt die ursprüngliche Überprüfung durch.|  

##### <a name="processing-form-events"></a>Verarbeiten von Formularereignissen  
 Fügen Sie den folgenden Aufruf Ihrer **OnControlEvent**-Methode hinzu:  

```  
Form()->ControlEvent(eventId, controlId);  
```  

 Dieser Aufruf übergibt Ereignisse an den Formularcontroller, damit er formularbezogene Ereignisse verarbeiten kann.  

##### <a name="save-form-data"></a>Speichern von Formulardaten  
 Rufen Sie in der Methode **OnNextClicked** die in Tabelle 29 gezeigten Formularmethoden auf.  

### <a name="table-29-onnextclicked-method"></a>Tabelle 29: OnNextClicked-Methode  

|**Methode**|**Beschreibung**|  
|-|-|  
|**InitSection**|Stellt den Namen des Abschnitts bereit, der auf der Seite **Zusammenfassung** für diese Seite angezeigt wird.|  
|**SaveFields**|Speichern von Feldwerten auf Tasksequenzvariablen und der Seite **Zusammenfassung**.|  

#####  <a name="Init"></a> Init  

```  
HRESULT Init(IWizardPageView *pView, IWizardPageContainer *pContainer)  
```  

 Diese Methode wird in der Regel zu Beginn der Methode **OnWindowCreated** der Seite aufgerufen. Der Befehl sollte etwa wie folgt aussehen:  

```  
Form()->Init(View(), Container());  
```  

##### <a name="setpageinfo"></a>SetPageInfo  

```  
HRESULT SetPageInfo(ISettingsProperties *pPageInfo)  
```  

 Diese Methode wird intern aufgerufen, und Sie sollten Sie nicht selbst aufrufen. Sie stellt dem Formularcontroller den XML-Code der Seite bereit.  

##### <a name="validate"></a>Validate  

```  
HRESULT Validate(void)  
```  

 Diese Methode führt alle Validierungssteuerelemente aus, die an Steuerelemente angefügt sind. Wenn ein Validierungssteuerelement nicht besteht, zeigt der Formularcontroller eine Warnmeldung an, deaktiviert die Schaltfläche **Weiter** und beendet dann die Verarbeitung der Validierungssteuerelemente. In der Regel müssen Sie diese Methode nur am Ende Ihrer **OnWindowCreated**-Methode aufrufen. Sie gibt immer **S_OK** zurück.  

##### <a name="addtogroup"></a>AddToGroup  

```  
AddToGroup(int groupControlId, int controlId)  
```  

 Diese Methode fügt, wie in Tabelle 30 dargestellt wird, ein Steuerelement als „untergeordnetes“ Element eines Kontrollkästchens oder Optionsfelds hinzu. Alle diese untergeordneten Steuerelemente werden deaktiviert, wenn das übergeordnete Steuerelement nicht ausgewählt ist. Diese Methode gibt immer **S_OK** zurück.  

### <a name="table-30-addtogroup"></a>Tabelle 30: AddToGroup  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**groupControlId**|Die ID des Kontrollkästchens oder Optionsfelds, das den Aktivierungszustand des untergeordneten Elements steuert.|  
|**Controlld**|Die ID des Steuerelements, dass Sie als untergeordnetes Element hinzufügen möchten.|  

##### <a name="updatecheckgroup"></a>UpdateCheckGroup  

```  
HRESULT UpdateCheckGroup(int groupControlId)  
```  

 Diese Methode aktualisiert den Aktivierungs- und Deaktivierungszustand der untergeordneten Steuerelemente einer Gruppe basierend auf dem Zustand des übergeordneten Steuerelements. In der Regel müssen Sie diese Methode nicht selbst aufrufen, da der Formularcontroller sie für Sie aufruft.  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, IValidator *pValidator, IControl *pControl = 0)  
```  

 Rufen Sie diese Methode nur auf, wenn Sie ein Validierungssteuerelement in Code statt mit XML-Code erstellen möchten. Diese Methode gibt immer **S_OK** zurück.  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr)  
```  

 Rufen Sie diese Methode nur auf, wenn Sie ein Validierungssteuerelement in Code statt mit XML-Code erstellen möchten.  

##### <a name="disablevalidation"></a>DisableValidation  

```  
HRESULT DisableValidation(int controlId, BOOL disable)  
```  

 Rufen Sie diese Methode auf, um entweder ein Validierungssteuerelement für ein Steuerelement zu deaktivieren oder um, wie in Tabelle 31 gezeigt wird, die normale Validierung wiederherzustellen. Diese Methode ist beispielsweise nützlich, wenn Sie über Regeln zum Aktivieren oder Deaktivieren von Steuerelementen verfügen, die nicht von der Formularvalidierung abgedeckt werden und Sie die Validierung eines Steuerelements deaktivieren müssen. Das heißt, dass Sie diese Methode normalerweise nicht aufrufen. Diese Methode gibt immer **S_OK** zurück.  

### <a name="table-31-hresult-disablevalidation"></a>Tabelle 31: HRESULT DisableValidation  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**controlId**|Das Steuerelement, für das Sie die Validierung aktivieren oder deaktivieren möchten.|  
|**Deaktivieren**|Legen Sie diesen Parameter auf TRUE fest, um die Validierung zu deaktivieren, oder legen Sie ihn auf FALSE fest, um die normale Validierung wiederherzustellen.|  

#####  <a name="AddField"></a> AddField  

```  
HRESULT AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type)  
```  

 Fügen Sie wie in Tabelle 32 gezeigt eine Steuerelementzuordnung zwischen dem Namen in einem **Feldelement** der XML-Konfigurationsdatei und der Steuerelement-ID im Dialogfeld Ihrer Seite hinzu. Sie müssen diese Methode vor dem Aufruf von **InitFields** aufrufen, da **InitFields** diese Information verwendet. Diese Methode gibt immer **S_OK** zurück.  

### <a name="table-32-hresult-addfield"></a>Tabelle 32: HRESULT AddField  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**Fieldname**|Der Name des Felds, wie er im XML-Code Ihrer Seite angezeigt wird.|  
|**controlId**|Die ID des Steuerelements in der Dialogfeldvorlage Ihrer Seite.|  
|**suppressLog**|Legen Sie diesen Parameter auf TRUE fest, wenn Sie nicht möchten, dass Werte aus diesem Feld in die Protokolldatei geschrieben werden. Legen Sie diesen Parameter für Kennwort- oder PIN-Felder immer auf TRUE fest.|  
|**Typ**|Der Typ des Steuerelements, der einem der folgenden Typen entspricht:<br /><br /> -   **CONTROL_STATIC_TEXT**<br />-   **CONTROL_COMBO_BOX**<br />-   **CONTROL_LIST_VIEW**<br />-   **CONTROL_PROGRESS_BAR**<br />-   **CONTROL_GENERIC**<br />-   **CONTROL_RADIO_BUTTON**<br />-   **CONTROL_CHECK_BOX**<br />-   **CONTROL_TREE_VIEW**|  

#####  <a name="AddRadioGroup"></a> AddRadioGroup  

```  
HRESULT AddRadioGroup(LPCWSTR groupName, int radioControlId)  
```  

 Diese Methode fügt, wie in Tabelle 33 gezeigt wird, einer benannten Optionsfeldgruppe ein Steuerelement hinzu. Sie müssen diese Methode vor der Methode **InitFields** aufrufen, da diese Methode Attribute des Elements **RadioGroup** verwendet, um die Einstellungen aller Optionsfeld-Steuerelemente in der Gruppe zu steuern. Optionsfeldgruppen können gesperrt sein, z.B. damit alle Optionsfelder deaktiviert sind, aber untergeordnete Steuerelemente ausschließlich basierend auf dem ausgewählten Optionsfeld aktiviert oder deaktiviert werden. Diese Methode gibt immer **S_OK** zurück.  

### <a name="table-33-hresult-addradiogroup"></a>Tabelle 33: HRESULT AddRadioGroup  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**groupName**|Eine Zeichenfolge, die eine Gruppe von Optionsfeldern auf dieser Seite definiert.|  
|**radioControlId**|Die ID eines einzelnen Optionsfelds, das dieser Gruppe hinzugefügt werden soll.|  

##### <a name="enableradiogroup"></a>EnableRadioGroup  

```  
HRESULT EnableRadioGroup(LPCWSTR groupName, BOOL enable)  
```  

 Diese Methode ermöglicht Ihnen das Aktivieren oder Deaktivieren einer gesamten Optionsfeldgruppe. Durch das Deaktivieren einer Optionsfeldgruppe werden alle Optionsfeld-Steuerelemente in der Gruppe und alle untergeordneten Elemente dieser Optionsfelder deaktiviert, die mit **AddToGroup** hinzugefügt wurden. Siehe Tabelle 34 und Tabelle 35.  

### <a name="table-34-enableradiogroup"></a>Tabelle 34: EnableRadioGroup  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**groupName**|Name einer Optionsfeldgruppe, den Sie bereit mit einem Aufruf von **AddRadioGroup** definiert haben.|  
|**Aktivieren**|Legen Sie diesen Parameter auf TRUE fest, um die Optionsfeldgruppe zu aktivieren, oder legen Sie ihn auf FALSE fest, um die Gruppe zu deaktivieren.|  

### <a name="table-35-hresult-enableradiogroup"></a>Tabelle 35: HRESULT EnableRadioGroup  

|**HRESULT**|**Beschreibung**|  
|-|-|  
|**S_OK**|Gruppe aktiviert oder deaktiviert|  
|**E_INVALIDARG**|Es ist keine Optionsfeldgruppe mit dem von Ihnen angegebenen Namen vorhanden.|  

#####  <a name="InitFields"></a> InitFields  

```  
HRESULT InitFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 Rufen Sie für jedes Feld **AddField** auf, das von XML-Code gesteuert werden kann, bevor Sie diese Methode aufrufen. Diese Methode gibt immer **S_OK** zurück.  

 Der Parameter **pFieldCallback** ist optional. Wenn Sie ihn angeben, ruft der Formularcontroller **SetFieldDefault** für Steuerelemente auf, die nicht **CONTROL_STATIC_TEXT** oder **CONTROL_CHECK_BOX** sind. Dieses Verhalten ermöglicht Ihnen, einen Standardwert aus dem XML-Code abzurufen und ihn selbst in dem Steuerelement festzulegen.  

#####  <a name="SaveFields"></a> SaveFields  

```  
HRESULT SaveFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 Diese Methode speichert Feldwerte in Tasksequenzvariablen und Zusammenfassungsdaten, die auf der Seite **Zusammenfassung** angezeigt werden. Das Angeben eines Zeigers in **pFieldCallback** ermöglicht Ihnen, das Speichern von Werten für Steuerelemente selbst zu behandeln, die **CONTROL_STATIC_TEXT** nicht unterstützen.  

##### <a name="isfielddisabled"></a>IsFieldDisabled  

```  
BOOL IsFieldDisabled(int controlId)  
```  

 Mit dieser Methode können Sie überprüfen, ob ein Feld im XML-Code deaktiviert wurde.  

#####  <a name="InitSection"></a> InitSection  

```  
HRESULT InitSection(LPCWSTR key, LPCWSTR sectionCaption)  
```  

 Diese Methode initialisiert die Zusammenfassungsdaten, die auf der Seite **Zusammenfassung** angezeigt werden, wie in Tabelle 36 gezeigt wird. Rufen Sie diese Methode in Ihrer **OnNextClicked**-Methode auf, bevor Sie **SaveFields** aufrufen. Diese Methode gibt immer **S_OK** zurück.  

### <a name="table-36-hresult-initsection"></a>Tabelle 36: HRESULT InitSection  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**Key**|Dieser Parameter sollte für Ihre Seite eindeutig sein. Er wird verwendet, um sicherzustellen, dass jede Seite ihre eigenen Zusammenfassungsinformationen besitzt.|  
|**sectionCaption**|Die Kopfzeile, die auf der Seite **Zusammenfassung** angezeigt wird. In der Regel wird **DisplayName()** als Wert für diesen Parameter verwendet.|  

##### <a name="addsummaryitem"></a>AddSummaryItem  

```  
HRESULT AddSummaryItem(LPCWSTR first, LPCWSTR second)  
```  

 Mit dieser Methode können Sie der Seite **Zusammenfassung** zusätzlich zu den mit XML festgelegten Elementen Zusammenfassungselemente hinzufügen. Siehe Tabelle 37.  

### <a name="table-37-hresult-addsummaryitem"></a>Tabelle 37: HRESULT AddSummaryItem  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**First**|Die Beschriftung des Zusammenfassungselements, die auf der linken Seite angezeigt wird.|  
|**Second**|Der Wert, der auf der rechten Seite angezeigt wird.|  

##### <a name="suppresslogvalue"></a>SuppressLogValue  

```  
HRESULT SuppressLogValue(LPCWSTR tsVariableName)  
```  

 Rufen Sie diese Methode für Tasksequenzvariablen auf, für die keine Werte in die Protokolldatei geschrieben werden sollen. Rufen Sie diese Methode für Tasksequenzvariablen auf, die Kennwörter, PINs oder andere sensible Werte speichern, die ein Benutzer möglicherweise eingibt.  

##### <a name="savetext"></a>SaveText  

```  
HRESULT SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption)  
```  

 Diese Methode speichert den Wert eines Textsteuerelements in einer Tasksequenzvariable und dem Bereich „Zusammenfassung“. In der Regel müssen Sie diese Methode nicht selbst aufrufen, da der Formularcontroller sie für alle Felder aufruft. Siehe Tabelle 38.  

### <a name="table-38-hresult-savetext"></a>Tabelle 38: HRESULT SaveText  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**controlId**|Die ID des Textfelds, das den Wert enthält, den Sie speichern möchten (oder ein beliebiges anderes Steuerelement, das Text zurückgeben kann).|  
|**tsVariableName**|Name der Tasksequenzvariable, die Sie ändern möchten.|  
|**summaryCaption**|Die Beschriftung für diesen Wert auf der Seite **Zusammenfassung**.|  

##### <a name="loadtext"></a>LoadText  

```  
HRESULT LoadText(int controlId, LPCWSTR tsVariableName)  
```  

 Diese Methode liest den Wert einer Tasksequenzvariable und legt das Textfeld auf diesen Wert fest.  

##### <a name="controlevent"></a>ControlEvent  

```  
void ControlEvent(WORD eventId, WORD controlId)  
```  

 Rufen Sie diese Methode in Ihrer **OnControlEvent**-Methode auf, um sicherzustellen, dass der Formularcontroller Steuerelementereignisse verarbeiten kann und somit ordnungsgemäß funktioniert. Die Werte, die Sie an diese Methode übergeben, sind dieselben Werte, die an die Methode **OnControlEvent** übergeben werden.  

##### <a name="isvalid"></a>IsValid  

```  
BOOL IsValid(void)  
```  

 Diese Methode gibt den Status der letzten Validierung des Formulars zurück. Wenn eines der Validierungssteuerelemente einen Fehler meldet, gibt diese Methode FALSE zurück. Das heißt, dass TRUE nur zurückgegeben wird, wenn alle Steuerelemente auf der Seite gültig sind.  

#### <a name="ivalidator-interface"></a>IValidator-Schnittstelle  

```  
__interface IValidator : IUnknown  
{  
    HRESULT Init(IControl *pControl, LPCTSTR message);  
    HRESULT Init(IControl *pControl, IWizardPageContainer *pContainer, IStringProperties *pProperties);  
    BOOL, IsValid(LPBSTR pMessage);  
    HRESULT SetProperty(int propertyId, LPVARIANT pValue);  
    HRESULT SetProperty(int propertyId, IUnknown *pUnknown);  
    HRESULT SetProperty)(int propertyId, LPCTSTR pValue);  
};  
```  

##### <a name="overview"></a>Übersicht  
 *Validierungssteuerelemente* sind Komponenten, die ein einzelnes Steuerelement auf Ihrer Seite überprüfen können. Die einfachste Möglichkeit, ein Validierungssteuerelement zu implementieren, ist, es als eine Unterklasse der **BaseValidator**-Klasse zu verwenden, die in der Headerdatei „BaseValidator.h“ definiert wird.  

##### <a name="hresult-initicontrol-pcontrol-lpctstr-message"></a>HRESULT Init(IControl \*pControl, LPCTSTR message)  
 Wenn Sie ein Validierungssteuerelement in Ihrem Code erstellen, können Sie diese Methode aufrufen, um das Validierungssteuerelement zu initialisieren. Siehe Tabelle 39.  

### <a name="table-39-hresult-init"></a>Tabelle 39: HRESULT Init  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**pControl**|Das Steuerelement, das Ihr Validierungssteuerelement überprüfen muss.|  
|**Message**|Die Nachricht, die auf der Seite angezeigt werden soll, wenn das Steuerelement ungültig ist.|  

##### <a name="hresult-initicontrol-pcontrol-iwizardpagecontainer-pcontainer-istringproperties-pproperties"></a>HRESULT Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)  
 Der Formularcontroller ruft diese Methode auf, um Validierungssteuerelemente zu initialisieren, die er basierend auf dem XML-Code der Seite erstellt. Siehe Tabelle 40.  

### <a name="table-40-hresult-init-method"></a>Tabelle 40: HRESULT Init-Methode  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**pControl**|Das Steuerelement, das Ihr Validierungssteuerelement überprüfen muss.|  
|**pContainer**|Wenn Ihr Validierungssteuerelement Zugriff auf die Protokollierung erfordert oder andere Komponenten erstellen muss.|  
|**pProperties**|Stellt Ihrem Validierungssteuerelement den Zugriff auf die Eigenschaften (Setter-Elemente) bereit.|  

##### <a name="bool-isvalidlpbstr-pmessage"></a>BOOL, IsValid(LPBSTR pMessage)  
 Diese Methode gibt TRUE oder FALSE zurück, je nachdem, ob das Steuerelement gültig oder ungültig ist. Bei der Rückgabe sollte **pMessage** mit einem neuen **BSTR** gefüllt sein, der die Nachricht enthält, die angezeigt wird, wenn das Steuerelement ungültig ist.  

##### <a name="hresult-setpropertyint-propertyid-lpvariant-pvalue"></a>HRESULT SetProperty(int propertyId, LPVARIANT pValue)  
 Sie können diese Methode implementieren, wenn Sie zusätzliche Werte benötigen, die nicht im XML-Code bereitgestellt werden.  

##### <a name="hresult-setpropertyint-propertyid-iunknown-punknown"></a>HRESULT SetProperty(int propertyId, IUnknown \*pUnknown)  
 Sie können diese Methode implementieren, wenn Sie zusätzliche Werte benötigen, die nicht im XML-Code bereitgestellt werden.  

##### <a name="hresult-setpropertyint-propertyid-lpctstr-pvalue"></a>HRESULT SetProperty)(int propertyId, LPCTSTR pValue)  
 Sie können diese Methode implementieren, wenn Sie zusätzliche Werte benötigen, die nicht im XML-Code bereitgestellt werden.  

#### <a name="iregex-interface"></a>IRegEx-Schnittstelle  

```  
__interface IRegEx : IUnknown  
{  
    BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex);  
    HRESULT GetMatch(size_t index, LPBSTR pValue);  
};  
```  

 Diese Methode wird mithilfe der Komponente **ID_Regex** (IRegex.h) implementiert und bietet Unterstützung für die Verarbeitung von regulären Ausdrücken.  

##### <a name="bool-matchesregexlpctstr-input-lpctstr-regex"></a>BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex)  
 Diese Methode führt den regulären Ausdruck für den Eingabetext aus. Sie verwendet die Funktion **regex_match** der C++-Standardbibliothek, um die eigentliche Arbeit zu übernehmen. Die Methode gibt TRUE zurück, wenn Übereinstimmungen gefunden wurden, andernfalls FALSE.  

##### <a name="hresult-getmatchsizet-index-lpbstr-pvalue"></a>HRESULT GetMatch(size_t index, LPBSTR pValue)  
 Diese Methode ermöglicht Ihnen das Abrufen der Übereinstimmungen aus dem letzten Aufruf von **MatchesRegex**. Beachten Sie, dass diese Methode keine Fehler verarbeitet und entweder **S_OK** zurückgibt oder eine Ausnahme auslöst.  

#### <a name="isummaryinfo-interface"></a>ISummaryInfo-Schnittstelle  

```  
__interface ISummaryInfo : IUnknown  
{  
    size_t Count(void);  
    HRESULT Clear(void);  
    HRESULT AddInfo(LPCTSTR pFirst, LPCTSTR pSecond);  
    HRESULT GetInfo(size_t index, LPBSTR pFirst, LPBSTR pSecond);  
    HRESULT GetCaption(LPBSTR pCaption);  
    HRESULT SetCaption(LPCTSTR caption);  
};  
```  

 Sie sollten diese Schnittstelle nicht direkt verwenden müssen. Verwenden Sie stattdessen **IFormController**.  

#### <a name="isummarybag"></a>ISummaryBag  

```  
__interface ISummaryBag : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetInfoByIndex(size_t index, [out] ISummaryInfo **ppSummary);  
    HRESULT GetInfoByKey(LPCTSTR key, [out] ISummaryInfo **ppSummary);  
};  
```  

 Sie sollten diese Schnittstelle nicht direkt verwenden müssen. Verwenden Sie stattdessen **IFormController**.  

#### <a name="itsvariablebag-interface"></a>ITSVariableBag-Schnittstelle  

```  
__interface ITSVariableBag : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue);  
    void Clear(void);  
    HRESULT Remove([in] LPCTSTR variableName);  
    HRESULT SuppressLogValue([in] LPCTSTR variableName);  
    void Save(void);  
};  
```  

 Diese Schnittstelle stellt den Zugriff auf Tasksequenzvariablen zur Verfügung. Sie können mithilfe der Methode **TSVariables()** Ihrer Seite auf diese Schnittstelle zugreifen.  

##### <a name="void-getvaluein-lpctstr-variablename-out-lpbstr-pvalue"></a>void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue)  
 Diese Methode liest den Wert einer Tasksequenzvariable.  

> [!NOTE]
>  Nach dem ersten Lesevorgang werden Werte zwischengespeichert.  

##### <a name="void-setvaluein-lpctstr-variablename-in-lpctstr-pvalue"></a>void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue)  
 Diese Methode legt den Wert einer Tasksequenzvariable fest. Dieser Wert wird im Arbeitsspeicher gespeichert. Tasksequenzwerte werden geschrieben, wenn Sie im UDI-Assistenten auf **Fertig stellen** klicken.  

##### <a name="void-clearvoid"></a>void Clear(void)  
 Diese Methode entfernt alle Tasksequenzwerte, die im Arbeitsspeicher gespeichert wurden.  

##### <a name="hresult-removein-lpctstr-variablename"></a>HRESULT Remove([in] LPCTSTR variableName)  
 Diese Methode entfernt einen bestimmten Tasksequenzwert aus dem Arbeitsspeicher. Wenn Sie das nächste Mal **GetValue** mit dem gleichen Tasksequenznamen aufrufen, versucht die Methode den Wert aus der Tasksequenz abzurufen.  

##### <a name="hresult-suppresslogvaluein-lpctstr-variablename"></a>HRESULT SuppressLogValue([in] LPCTSTR variableName)  
 Jedes Mal, wenn Tasksequenzvariablen geschrieben werden, wenn Sie z.B. im UDI-Assistenten auf **Fertig stellen** klicken, werden die Namen und Werte in die Protokolldatei geschrieben. Rufen Sie diese Methode auf, um die Protokollierung von vertraulichen Werten zu unterdrücken, z.B. Kennwörter oder PINs für eine spezifische Tasksequenzvariable.  

##### <a name="void-savevoid"></a>void Save(void)  
 Diese Methode speichert alle Tasksequenzwerte, die mit Aufrufen von **SetValue** festgelegt wurden.  

#### <a name="itsvariablerepository-interface"></a>ITSVariableRepository-Schnittstelle  

```  
__interface ITSVariableRepository : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, BOOL logValue, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, BOOL logValue, [in] LPCTSTR value);  
};  
```  

 Diese Schnittstelle ist für die interne Verwendung durch **TSVariableBag** zum Lesen und Schreiben von Tasksequenzvariablen.  

#### <a name="iwizardfinish-interface"></a>IWizardFinish-Schnittstelle  

```  
__interface IWizardFinish : IUnknown  
{  
    HRESULT Canceled(void);  
    HRESULT Finished(void);  
};  
```  

 Diese Schnittstelle ist in erweiterten Szenarios hilfreich, in denen Sie zusätzliche Verarbeitungsvorgänge ausführen möchten, wenn Sie im UDI-Assistenten auf **Fertig stellen** oder **Abbrechen** klicken. Der UDI-Assistent enthält einen Task für **Fertig stellen**, der Tasksequenzvariablen speichert, wenn Sie auf **Fertig stellen** klicken. Wenn Sie den Assistenten abbrechen, legt der Task nur die Tasksequenzvariable **OSDSetupWizCancelled** auf TRUE fest und speichert keine Änderungen in anderen Tasksequenzvariablen.  

 Wenn Sie Ihre eigene Komponente zum Fertigstellen erstellen, müssen Sie Ihren Code wie folgt registrieren:  

```  
Register<MyFinishTaskFactory>(ID_MyFinishTask, pRegistry);  

PWizardFinish pFinish;  
CreateInstance(pRegistry, ID_MyFinishTask, &pFinish);  

PWizardFinishService pService;  
GetService<IWizardFinishService>(pRegistry, &pService);  

pService->Register(pFinish);  
```  

#### <a name="ibindablelist-interface"></a>IBindableList-Schnittstelle  

```  
__interface IBindableList : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetCaption(size_t index, LPBSTR pCaption);  
};  
```  

 Implementieren Sie diese Schnittstelle, wenn Sie über eine Datenquellenkomponente verfügen, die Sie mithilfe der Methode **Bind** an ein Kombinationsfeld binden möchten.  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 Diese Methode gibt die Anzahl der Elemente in der Liste zurück.  

##### <a name="hresult-getcaptionsizet-index-lpbstr-pcaption"></a>HRESULT GetCaption(size_t index, LPBSTR pCaption)  
 Diese Methode gibt die Beschriftung des Elements bei einem angegebenen Index zurück.  

#### <a name="idatanodes-interface"></a>IDataNodes-Schnittstelle  

```  
__interface IDataNodes : IUnknown  
{  
    size_t Count();  
    HRESULT SetCaptionProperty(LPCTSTR captionProperty);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue);  
    HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode);  
};  
```  

 Diese Schnittstelle bietet Zugriff auf hierarchische Daten, die auf einer Seite gespeichert werden können. Sie können diese Schnittstelle mithilfe der Methoden der Schnittstelle **ISettingsProperties** abrufen, die über die Methode **Settings** für Ihre Seite verfügbar ist.  

 Daten im XML-Code einer Seite können etwa wie folgt aussehen:  

```  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  
```  

 Das Aufrufen von **Settings()->GetDataNode(L"Network", &pData)** stellt Ihnen die Schnittstelle **IDataNodes** mit zwei Datenelementen zur Verfügung (beide verfügen über jeweils zwei Eigenschaften).  

##### <a name="sizet-count"></a>size_t Count()  
 Diese Methode gibt die Anzahl der **DataItem**-Elemente zurück.  

##### <a name="hresult-setcaptionpropertylpctstr-captionproperty"></a>HRESULT SetCaptionProperty(LPCTSTR captionProperty)  
 Die Komponente, die diese Schnittstelle unterstützt, unterstützt auch **IBindableList**, was das Auffüllen eines Kombinationsfelds mit Daten aus dem XML-Code der Seite vereinfacht. Diese Methode steuert, welche Eigenschaft (Setter) in den einzelnen **DataItem**-Elementen für diese Bindung verwendet wird. Sie können diese Methode z.B. mit **DisplayName** aufrufen, und sie würde diese Settereigenschaft für die Datenbindung verwenden. Das Kombinationsfeld würde dann **Public** und **Dev Team** als Elemente enthalten.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-out-lpbstr-propertyvalue"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue)  
 Diese Methode ruft eine Eigenschaft aus einem der **DataItem**-Elemente ab. Siehe Tabelle 41 und Tabelle 42.  

### <a name="table-41-dataitem-getproperty"></a>Tabelle 41: DataItem GetProperty  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**Index**|Der Indexwert (beginnend mit 0 (null)) des Elements **DataItem**, für das Sie einen Eigenschaftswert abrufen möchten.|  
|**propertyName**|Name der Settereigenschaft, für die Sie einen Wert abrufen.|  
|**propertyValue**|Enthält bei der Rückgabe den Zeichenfolgenwert einer Eigenschaft.|  

### <a name="table-42-hresult-getproperty"></a>Tabelle 42: HRESULT GetProperty  

|||  
|-|-|  
|**HRESULT**|**Beschreibung**|  
|**S_OK**|Die Eigenschaft wurde abgerufen.|  
|**E_INVALIDARG**|Der Index liegt hinter dem Ende des Arrays.|  

##### <a name="hresult-getnodesizet-index-out-isettingsproperties-ppnode"></a>HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode)  
 Diese Methode ähnelt **GetProperty**. Statt jedoch einen Wert aus einem **DataItem**-Element zurückzugeben, wird **DataItem** als Ganzes in eine **ISettingsProperties**-Schnittstelle eingebunden und zurückgegeben. Siehe Tabelle 43 und Tabelle 44.  

### <a name="table-43-hresult-getnode"></a>Tabelle 43: HRESULT GetNode  

|**Parameter**|**Beschreibung**|  
|-|-|  
|Index|Der Indexwert (beginnend mit 0 (null)) des Elements **DataItem**, für das Sie einen Eigenschaftswert abrufen möchten.|  
|**ppNode**|Die Schnittstelle **ISettingsProperties**, die den **DataItem**-Knoten beim Beenden umschließt.|  

### <a name="table-44-hresult-getnode-results"></a>Tabelle 44: Ergebnisse von HRESULT GetNode  

|**HRESULT**|**Beschreibung**|  
|-|-|  
|**S_OK**|Der Knoten wurde abgerufen.|  
|**E_INVALIDARG**|Der Index liegt hinter dem Ende des Arrays.|  

#### <a name="ifactoryregistry-interface"></a>IFactoryRegistry-Schnittstelle  

```  
__interface IFactoryRegistry : IUnknown  
{  
    void Register(LPCTSTR type,  IClassFactory *pFactory);  
    HRESULT LoadAndRegister(LPCTSTR dllName, ILogger *pLogger);  
    BOOL Contains(LPCTSTR type);  
    HRESULT GetFactory(LPCTSTR type,  IClassFactory **ppFactory);  
    HRESULT CreateInstance(LPCTSTR type,  IUnknown **ppInstance);  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
    HRESULT RegisterService(REFGUID iid, IUnknown *pService);  
    HRESULT GetService(REFGUID iid,  IUnknown **ppService);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Wenn Sie eine neue benutzerdefinierte Seite erstellen, müssen Sie mindestens eine *Seitenfactory* erstellen, eine Klasse die **IClassFactory** implementiert. (Sie können **ClassFactoryImpl** als Basisklasse Ihrer Factory verwenden.)  

##### <a name="void-registerlpctstr-type--iclassfactory-pfactory"></a>void Register(LPCTSTR type, IClassFactory \*pFactory)  
 Diese Methode registriert eine Klassenfactory mit der Registrierung. Siehe Tabelle 45.  

### <a name="table-45-iclassfactory-void-register"></a>Tabelle 45: IClassFactory void Register  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**Typ**|Eine Zeichenfolge, die die Factory identifiziert, die Sie registrieren. In der Regel sollte dieser Parameter den Namen Ihres Unternehmens in der Zeichenfolge enthalten, um sicherzustellen, dass er eindeutig ist.|  
|**pFactory**|Ein Zeiger auf die Instanz Ihrer Klassenfactory|  

##### <a name="hresult-loadandregisterlpctstr-dllname-ilogger-plogger"></a>HRESULT LoadAndRegister(LPCTSTR dllName, ILogger \*pLogger)  
 Diese Methode ist nur zur internen Verwendung.  

##### <a name="bool-containslpctstr-type"></a>BOOL Contains(LPCTSTR type)  
 Diese Methode ist im Allgemeinen zur internen Verwendung. Sie überprüft, ob eine Klassenfactory für einen Typ registriert wurde.  

##### <a name="hresult-getfactorylpctstr-type--iclassfactory-ppfactory"></a>HRESULT GetFactory(LPCTSTR type, IClassFactory **ppFactory)  
 Mit dieser Methode können Sie die Klassenfactory abrufen. In der Regel würden Sie **CreateInstance** aufrufen. Wenn Sie jedoch vorhaben, eine große Anzahl der gleichen Komponente zu erstellen, ist es effizienter, die Factory abzurufen, und sie hinterher aufzufordern, Instanzen für Sie zu erstellen.  

##### <a name="hresult-createinstancelpctstr-type--iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type, IUnknown **ppInstance)  
 Diese Methode erstellt entsprechend ihrem Typ eine neue Instanz einer Komponente. Verwenden Sie stattdessen die Methodenvorlage **CreateInstance**, die typsichere Objekterstellung ermöglicht.  

##### <a name="hresult-setcontaineriwizardpagecontainer-pcontainer"></a>HRESULT SetContainer(IWizardPageContainer \*pContainer)  
 Diese Methode ist nur zur internen Verwendung.  

##### <a name="hresult-registerservicerefguid-iid-iunknown-pservice"></a>HRESULT RegisterService(REFGUID iid, IUnknown \*pService)  
 *Dienste* sind einzelne Instanzen einer Komponente, die an mehreren Stellen verwendet werden können. Sie können diese Methode verwenden, um einen Dienst auf einer Seite zu registrieren und dieselbe Instanz von einer anderen Seite aus abzurufen.  

##### <a name="hresult-getservicerefguid-iid--iunknown-ppservice"></a>HRESULT GetService(REFGUID iid, IUnknown **ppService)  
 Diese Methode ruft einen Dienst ab, der zuvor durch einen Aufruf von RegisterService registriert wurde.  

##### <a name="hresult-setlanguagelangid-languageid"></a>HRESULT SetLanguage(LANGID languageId)  
 Diese Methode legt die Sprache des UDI-Assistenten auf den von Ihnen im Parameter **languageId** angegebenen Sprachbezeichner fest.  

##### <a name="langid-getlanguage"></a>LANGID GetLanguage()  
 Diese Methode gibt den Wert des Sprachbezeichners zurück, den Sie mit dem Befehlszeilenparameter **/locale** für den UDI-Assistenten angegeben haben. Diese Methode gibt einen der folgenden Werte zurück:  

-   Den Wert des Sprachbezeichners, den Sie mit dem Befehlszeilenparameter **/locale** angegeben haben.  

-   0 (null), wenn Sie den Befehlszeilenparameter **/locale** angegeben haben.  

#### <a name="ilogger-interface"></a>ILogger-Schnittstelle  

```  
__interface ILogger : IUnknown  
{  
    HRESULT Init(LPCWSTR logFilename);  
    HRESULT MoveLog(LPCWSTR logFilename);  
    HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message);  
    HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message);  
    HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message);  
    HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Normal(LPCTSTR component, LPCTSTR message);      
    HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Verbose(LPCTSTR component, LPCTSTR message);  
    HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Debug(LPCWSTR component, LPCWSTR message);  
    HRESULT EnableDebug(BOOL debug);  
    HRESULT Close(void);  
    HRESULT GetLogFilename(LPBSTR pFilename);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Der UDI-Assistent protokolliert Informationen in einer Protokolldatei, die bei der Problembehandlung von Problemen in dem Feld helfen. Es wird empfohlen, dass Ihre Seiten Informationen protokollieren. Sie können einen Zeiger auf diese Schnittstelle mithilfe der Methode **Logger()** über Ihre Seite abrufen. Zeilen in der Protokolldatei enthalten eine Zahl für die „Ebene“, die Fehlermeldungen, normale Meldungen, ausführliche Meldungen oder Debugmeldungen darstellt.  

> [!NOTE]
>  Debugmeldungen werden nicht in der Protokolldatei gespeichert, es sei denn, die Unterstützung für das Debuggen ist eingeschaltet. Sie können die Debugunterstützung einschalten, indem Sie die folgende Zeile dem Element **Style** in der Konfigurationsdatei hinzufügen:  

```  
<Setter Property="debug">true</Setter>  
```  

##### <a name="init"></a>Anfangsstatus  

```  
HRESULT Init(LPCWSTR logFilename)  
```  

 Diese Methode ist nur zur internen Verwendung.  

##### <a name="movelog"></a>MoveLog  

```  
HRESULT MoveLog(LPCWSTR logFilename)  
```  

 Diese Methode ist nur zur internen Verwendung.  

##### <a name="logbase"></a>LogBase  

```  
HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message)  
```  

 Diese Methode ist nur zur internen Verwendung.  

##### <a name="log"></a>Protokoll  

```  
HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message)  
```  

 Diese Methode ist nur zur internen Verwendung.  

##### <a name="error"></a>Fehler  

```  
HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message)  
```  

 Rufen Sie diese Information auf, um Informationen zu einem Fehler zu protokollieren. Siehe Tabelle 46.  

### <a name="table-46-hresult-error"></a>Tabelle 46: HRESULT-Fehler  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**Fehler**|Der Fehlercode, der von einem Aufruf zurückgegeben wird (Dieser Code wird im Protokolleintrag als Zahl dargestellt).|  
|**Komponente**|Eine Zeichenfolge, die die Ursache des Fehlers identifiziert, die in der Regel Ihre Seite oder die Komponente ist, die Sie geschrieben haben.|  
|**Message**|Die Nachricht, die erklärt, was den Fehler verursacht hat.|  

#####  <a name="Error2"></a> Error2  

```  
HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Diese Methode entspricht der Methode **Error**, ermöglicht Ihnen jedoch, eine zweiteilige Meldung bereitzustellen. Die endgültige Nachricht verfügt in der Ausgabedatei dann über „Message“ gefolgt von „Message2“. Diese Methode dient ausschließlich der Bequemlichkeit.  

##### <a name="normal"></a>Normal  

```  
HRESULT Normal(LPCTSTR component, LPCTSTR message)  
```  

 Diese Methode protokolliert eine normale Meldung. Weitere Informationen finden Sie in der Beschreibung der Methode [Error](#Error) für Parameter.  

##### <a name="normal2"></a>Normal2  

```  
HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Diese Methode protokolliert eine normale Meldung. Weitere Informationen finden Sie in der Beschreibung der Methode [Error2](#Error2) für Parameter.  

##### <a name="verbose"></a>Ausführlich  

```  
HRESULT Verbose(LPCTSTR component, LPCTSTR message)  
```  

 Diese Methode protokolliert eine ausführliche Meldung. Weitere Informationen finden Sie in der Beschreibung der Methode [Error](#Error) für Parameter.  

##### <a name="verbose2"></a>Verbose2  

```  
HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Diese Methode protokolliert eine ausführliche Meldung. Weitere Informationen finden Sie in der Beschreibung der Methode [Error2](#Error2) für Parameter.  

##### <a name="debug"></a>Debug  

```  
HRESULT Debug(LPCWSTR component, LPCWSTR message)  
```  

 Diese Methode protokolliert eine Debugmeldung. Weitere Informationen finden Sie in der Beschreibung der Methode [Error](#Error) für Parameter. Debugmeldungen werden nicht in der Datei gespeichert, es sei denn, sie sind aktiviert. Weitere Informationen finden Sie im Abschnitt „Übersicht“.  

##### <a name="enabledebug"></a>EnableDebug  

```  
HRESULT EnableDebug(BOOL debug)  
```  

 Diese Methode ist nur zur internen Verwendung.  

##### <a name="close"></a>Schließen  

```  
HRESULT Close(void)  
```  

 Diese Methode ist nur zur internen Verwendung.  

##### <a name="getlogfilename"></a>GetLogFilename  

```  
HRESULT GetLogFilename(LPBSTR pFilename)  
```  

 Diese Methode ruft den Namen der Protokolldatei ab.  

#### <a name="iorientation-interface"></a>IOrientation-Schnittstelle  

```  
__interface IOrientation : IUnknown  
{  
    void SetController(IWizardDialogController *pController);  
    int AddPage(LPCTSTR name);  
    void SelectPage(int index);  
};  
```  

 Diese Schnittstelle ist nur zur internen Verwendung.  

#### <a name="isettings-interface"></a>ISettings-Schnittstelle  

```  
__interface ISettings : IUnknown  
{  
    int NumDlls();  
    int NumPages();  

    HRESULT SetStage(LPCWSTR stageName);  
    HRESULT GetDllName(long index, __out LPBSTR pDllName);  
    HRESULT GetPageInfo(long index, __out ISettingsProperties **ppPageInfo);  
    HRESULT GetStyle(__out ISettingsProperties **ppStyleInfo);  
};  
```  

 Diese Schnittstelle ist nur zur internen Verwendung.  

#### <a name="isettingsproperties-interface"></a>ISettingsProperties-Schnittstelle  

```  
__interface ISettingsProperties : IUnknown  
{  
    HRESULT GetAttribute(LPCTSTR attributeName, __out LPBSTR attributeValue);  
    IStringProperties * Properties();  
   RESULT SelectNodes(LPCTSTR xPath, __out IXMLDOMNodeList **ppList);  
    HRESULT SelectSingleNode(LPCTSTR xPath, __out IXMLDOMNode **ppNode);  
    HRESULT GetDataNode(LPCTSTR name, __out ISettingsProperties **ppNode);  
    HRESULT GetDataNodes(__out IDataNodes **ppNodes);  
    HRESULT GetChildDataNodes(LPCTSTR childeName, __out IDataNodes **ppNodes);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle stellt den Zugriff auf Seitendaten zur Verfügung. Verwenden Sie die Methode **Settings()** der Seite, um allgemeine Seitendaten abzurufen.  

##### <a name="hresult-getattributelpctstr-attributename--lpbstr-attributevalue"></a>HRESULT GetAttribute(LPCTSTR attributeName, LPBSTR attributeValue)  
 Diese Methode ermöglicht Ihnen, Werte der Attribute auf dem Hauptknoten abzurufen. Wenn Sie die Methode **Settings()** der Seite verwenden, ist der Knoten **Seite** der Hauptknoten.  

##### <a name="istringproperties--properties"></a>IStringProperties * Properties()  
 Diese Methode ermöglicht den Zugriff auf die Werte der Settereigenschaft des Hauptknotens. Bei einer Seite sind dies die allgemeinen Eigenschaften.  

##### <a name="hresult-selectnodeslpctstr-xpath--ixmldomnodelist-pplist"></a>HRESULT SelectNodes(LPCTSTR xPath, IXMLDOMNodeList **ppList)  
 Rufen Sie diese Methode auf, wenn Sie eine Liste von XML-Knoten mithilfe eines XPath-Ausdrucks direkt aufrufen möchten. Wenn möglich, ist es besser, eine der anderen Methoden zu verwenden. Verwenden Sie diese Methode nur, wenn Sie keine andere Möglichkeit haben, Knoten abzurufen.  

##### <a name="hresult-selectsinglenodelpctstr-xpath--ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xPath, IXMLDOMNode **ppNode)  
 Rufen Sie diese Methode auf, wenn Sie einen einzelnen XML-Knoten mithilfe eines XPath-Ausdrucks direkt aufrufen möchten. Wenn möglich, ist es besser, eine der anderen Methoden zu verwenden. Verwenden Sie diese Methode nur, wenn Sie keine andere Möglichkeit haben, einen Knoten abzurufen.  

##### <a name="hresult-getdatanodelpctstr-name--isettingsproperties-ppnode"></a>HRESULT GetDataNode(LPCTSTR name, ISettingsProperties **ppNode)  
 Ruft ein **Datenelement** basierend auf dem Attribut **Name** des Elements ab.  

##### <a name="hresult-getdatanodesidatanodes-ppnodes"></a>HRESULT GetDataNodes(IDataNodes **ppNodes)  
 Diese Methode ruft eine Liste der **DataItem**-Elemente im aktuellen Knoten ab. Rufen Sie auf der Seitenebene **GetDataNode** auf, um eine **ISettingsProperty**-Schnittstelle für die Daten abzurufen. Rufen Sie auf dieser Instanz **GetDataNodes** auf, um die Liste von Datensätzen abzurufen. Ein Beispiel finden Sie in diesem XML-Codeausschnitt:  

```  
    <Page …>  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  

PSettingsProperties pData;  
Settings()->GetDataNode(L"Network", &pData);  
PDataNodes pNodes;  
pData->GetDataNodes(&pNodes);  
```  

##### <a name="hresult-getchilddatanodeslpctstr-childename--idatanodes-ppnodes"></a>HRESULT GetChildDataNodes(LPCTSTR childeName, IDataNodes **ppNodes)  
 Diese Methode bietet eine schnelle Möglichkeit, um die **DataItem**-Knoten von einem spezifischen **Datenknoten** abzurufen. Mithilfe des XML-Codes aus dem Beispiel zu **GetDataNodes** führt der folgende Code dasselbe aus, wie die vier Zeilen im Beispiel unter **GetDataNodes**, jedoch zuzüglich der Überprüfung von Fehlern:  

```  
ISimpleStringProperties Interface  
```  

#### <a name="isimplestringproperties-interface"></a>ISimpleStringProperties-Schnittstelle  

```  
__interface ISimpleStringProperties : IStringProperties  
{  
void Add(LPCTSTR propertyName, LPCTSTR value);  
};  
```  

 Diese Schnittstelle allein ist nicht sonderlich nützlich. Allerdings wird sie von der Komponente **ID_SimpleStringProperties** implementiert, die ebenfalls die Schnittstelle **IStringProperties** implementiert. Sie können diese Komponente in Fällen verwenden, in denen Sie mehrere Eigenschaften an eine andere Komponente wie einen Task übergeben müssen, die Werte jedoch programmgesteuert hinzugefügt werden sollen, anstatt XML-Werte zu verwenden. Der folgende Codeausschnitt stellt ein Beispiel für die Verwendung der Schnittstelle dar:  

```  
PSimpleStringProperties *pProperties;  
CreateInstance(Container(), ID_SimpleStringProperties, &pProperties);  
pProperties->Add(L"filename", L"%windir%\\system32\\cscript.exe");  
pTask->Init(pProperties, nullptr);  
IStringProperties  
__interface IStringProperties : IUnknown  
{  
    HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue);  
};  
```  

 Diese Schnittstelle bietet einfachen Zugriff auf eine Gruppe von Setter-Elementen, die aus XML-Code stammen. Diese Schnittstelle ist für die Eigenschaften einer Seite verfügbar, die **Settings()->Properties()** verwendet.  

##### <a name="hresult-getlpctstr-propertyname-out-lpbstr-ppropvalue"></a>HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue)  
 Diese Methode ruft einen einzelnen Eigenschaftswert ab. Siehe Tabelle 47 und Tabelle 48.  

### <a name="table-47-ihresult-get-property-value"></a>Tabelle 47: Wert von HRESULT Get Property  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**propertyName**|Name der Eigenschaft, die Sie lesen möchten.|  
|**pPropValue**|Enthält beim Beenden den Eigenschaftswert als Zeichenfolge (Dieser Wert ist **nullptr**, wenn keine solche Eigenschaft vorhanden ist).|  

### <a name="table-48-ihresult-get-property-value-results"></a>Tabelle 48: Ergebnisse von IHRESULT Get Property Value  

|||  
|-|-|  
|**HRESULT**|**Beschreibung**|  
|**S_OK**|Der Eigenschaftswert wird abgerufen.|  
|**E_INVALIDARG**|Es gibt keine Eigenschaft mit dem angegebenen Namen.|  

#### <a name="itaskmanager-interface"></a>ITaskManager-Schnittstelle  

```  
__interface ITaskManager : IUnknown  
{  
    HRESULT Init(IWizardPageView *pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties *pPageInfo, ITaskManagerCallback *pCallback);  
    HRESULT SetFailMessage(LPCWSTR message);  

    HRESULT Start(void);  

    HRESULT GetTaskMessage(size_t index, LPBSTR message);  
    HRESULT GetResultType)(size_t index, LPBSTR type);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value);  
    int GetSelectedIndex(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    size_t FailedCount(void);  
    size_t WarningCount(void);  
    size_t SucceedCount(void);  
    size_t RunningCount(void);  

    void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo);  
    void OnControlEvent(WORD eventId, WORD controlId);  
    void EnableButtons(BOOL enable);  
}  
```  

 Diese Schnittstelle wird von der Komponente **TaskManager** (**ID_TaskManager** in ITaskManager.h) implementiert. Das ist die Komponente, die Tasks auf der Preflightseite ausführt. Sie können die Preflightseite entweder direkt verwenden, was Sie in den meisten Fällen tun, oder Sie erstellen Ihre eigene Seite und lassen diese Komponente die meiste Arbeit übernehmen.  

##### <a name="hresult-initiwizardpageview-ppageview-int-idlistview-int-idmessage-int-idretrybutton-isettingsproperties-ppageinfo-itaskmanagercallback-pcallback"></a>HRESULT Init(IWizardPageView \*pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties \*pPageInfo, ITaskManagerCallback \*pCallback)  
 Sie müssen zunächst diese Methode aufrufen, bevor Sie eine andere Methode aufrufen können. Sie initialisiert die Komponente **TaskManager**. Siehe Tabelle 49.  

### <a name="table-49-hresult-init"></a>Tabelle 49: HRESULT Init  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**pPageView**|Ermöglicht den Zugriff auf die Seite, die die Tasks ausführt (diese Seite muss über einen bestimmten Satz von Steuerelementen verfügen, die in den folgenden Parametern beschrieben werden).|  
|**idListView**|Die Steuerelement-ID eines **ListView**-Steuerelements, das die Liste der Tasks und den Status der jeweiligen Tasks anzeigt.|  
|**idMessage**|Die Steuerelement-ID eines Textfelds, die zum Anzeigen einer Nachricht für den Task verwendet wird, den Sie auswählen.|  
|**idRetryButton**|Die Steuerelement-ID einer Schaltfläche, auf die Sie klicken können, um Tasks erneut auszuführen.|  
|**pPageInfo**|Ein Wrapper um den XML-Code der Seite (**TaskManager** lädt eine Reihe von Tasks zum Ausführen aus diesem XML-Code).|  
|**pCallback**|Kann NULL sein (wenn dieser Parameter nicht NULL ist, ruft **TaskManager** die Methode **Started** auf, wenn ein Task gestartet wird, und die Methode **Finished** für jeden Task, der beendet wird.)|  

##### <a name="hresult-setfailmessagelpcwstr-message"></a>HRESULT SetFailMessage(LPCWSTR message)  
 Diese Methode legt die Meldung fest, die angezeigt wird, wenn mindestens ein Task fehlschlägt.  

##### <a name="hresult-startvoid"></a>HRESULT Start(void)  
 Diese Methode startet alle Tasks. Jeder Task wird auf einem separaten Thread gestartet.  

##### <a name="hresult-gettaskmessagesizet-index-lpbstr-message"></a>HRESULT GetTaskMessage(size_t index, LPBSTR message)  
 Diese Methode ist nur zur internen Verwendung. Sie ruft die aktuelle Meldung für einen Task basierend auf seinem Index in der Liste der Tasks ab.  

##### <a name="hresult-getresulttypesizet-index-lpbstr-type"></a>HRESULT GetResultType)(size_t index, LPBSTR type)  
 Diese Methode ruft den aktuellen „Typ“ eines Tasks ab. In Tabelle 50 werden die verfügbaren Typen gezeigt.  

### <a name="table-50-hresult-getresulttype"></a>Tabelle 50: HRESULT GetResultType  

|**Typ**|**Beschreibung**|  
|-|-|  
|**0**|Stellt einen Task dar, der erfolgreich war.|  
|**1**|Stellt einen Task dar, der eine Warnung zurückgegeben hat.|  
|**-1**|Stellt einen Task dar, der fehlgeschlagen ist.|  

 Der Typ wird anhand des Beendigungs- und Fehlercodes und Übereinstimmungen des XML-Elements <ExitCodes\> des Tasks abgerufen.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-lpbstr-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value)  
 Diese Methode wird von den Fortschritts- und Preflightseiten verwendet, um die Settereigenschaft **BitmapFilename** abzurufen, damit neben der Meldung für den von Ihnen hervorgehobenen Task ein Bild angezeigt werden kann. Das heißt, Sie können dem XML-Code des Tasks einen benutzerdefinierten Setter hinzufügen und diesen dann mit dieser Methode abrufen.  

##### <a name="int-getselectedindexvoid"></a>int GetSelectedIndex(void)  
 Diese Methode ruft den Index des aktuell ausgewählten Tasks ab, was nützlich ist, wenn Sie zusätzliche Informationen über diesen Task abrufen möchten (siehe **GetProperty**-Methode), um diese für den ausgewählten Task anzuzeigen. Die Fortschritt- und Preflightseiten verwenden diese Methode, um ein Bild für den ausgewählten Task anzuzeigen.  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 Diese Methode hilft hauptsächlich bei Komponententests, damit der Test sicherstellen kann, dass Tasks vor dem Komponententest beendet werden. Sie würden diese Methode normalerweise nicht aufrufen. Die Rückgabe findet dann statt, wenn entweder das Ausführen aller Tasks abgeschlossen oder die Wartezeit abgelaufen ist.  

##### <a name="sizet-failedcountvoid"></a>size_t FailedCount(void)  
 Diese Methode gibt die Anzahl der momentan als fehlgeschlagen markierten Tasks zurück.  

##### <a name="sizet-warningcountvoid"></a>size_t WarningCount(void)  
 Diese Methode gibt die Anzahl der momentan mit Warnungen markierten Tasks zurück.  

##### <a name="sizet-succeedcountvoid"></a>size_t SucceedCount(void)  
 Diese Methode gibt die Anzahl der momentan als erfolgreich markierten Tasks zurück.  

##### <a name="sizet-runningcountvoid"></a>size_t RunningCount(void)  
 Diese Methode gibt die Anzahl der momentan ausgeführten Tasks zurück.  

##### <a name="void-oncommoncontroleventword-controlid-lpnmhdr-pinfo"></a>void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo)  
 Rufen Sie diese Methode über das **OnCommonControlEvent** Ihrer Seite auf, damit die Komponente **TaskManager** die erforderlichen Ereignisse verarbeiten kann.  

##### <a name="void-oncontroleventword-eventid-word-controlid"></a>void OnControlEvent(WORD eventId, WORD controlId)  
 Rufen Sie diese Methode über das **OnControlEvent** Ihrer Seite auf, damit die Komponente **TaskManager** die erforderlichen Ereignisse verarbeiten kann.  

##### <a name="void-enablebuttonsbool-enable"></a>void EnableButtons(BOOL enable)  
 Diese Methode ist nur zur internen Verwendung.  

#### <a name="iwizardcomponent-interface"></a>IWizardComponent-Schnittstelle  

```  
__interface IWizardComponent : IUnknown  
{  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
};  
```  

##### <a name="overview"></a>Übersicht  
 In der Regel wird diese Schnittstelle nicht direkt implementiert, sondern über die Vorlagenklasse **WizardComponent**. Wenn Ihre Komponente diese Schnittstelle implementiert und Sie eine Klassenfactory mit der Registrierung registriert haben, erhält Ihre Komponente bei der Erstellung einen Zeiger auf die Instanz **IWizardPageContainer**. Das hilft Ihnen beispielsweise beim Zugreifen auf die Protokollierung oder die Registrierung, um andere Komponenten zu erstellen, die Ihre Komponente möglicherweise benötigt.  

#### <a name="iwizarddialogcontroller-interface"></a>IWizardDialogController-Schnittstelle  

```  
__interface IWizardDialogController : IUnknown  
{  
    void Initialize(ISettings *pSettings);  
    void InitPages(void);  
    void Start();  
    void Next();  
    void Finish();  
    void Previous();  
    int NumPages();  
    void Cancel();  

    HRESULT Focus(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage();  

    void ChangePage(size_t newIndex);  
    IUnknown *CurrentPage(void);  
    HRESULT GetCurrentTitle([out, retval] LPBSTR pDisplayName);  
};  
```  

 Diese Schnittstelle ist nur zur internen Verwendung.  

#### <a name="iwizarddialogview-interface"></a>IWizardDialogView-Schnittstelle  

```  
__interface IWizardDialogView : IUnknown  
{  
    HRESULT LoadBannerImage(LPCTSTR bannerFilename);  
    HRESULT LoadPage(LPCTSTR pageType, ISettingsProperties *pPageSettings, IWizardPageView **view);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    HRESULT Focus(WizardButtons button);  
    void EnableFinish(BOOL isFinish);  
    void Exit(int exitCode);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
    void SetTitle(LPCTSTR title);  
    void SetPageTitle(LPCTSTR title);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    HWND GetHwnd(void);  
    void UpdateFocus(void);  
};  
```  

 Diese Schnittstelle ist nur zur internen Verwendung.  

####  <a name="IWizardPageInterface"></a> IWizardPage-Schnittstelle  

```  
__interface IWizardPage : IUnknown  
{  
    HRESULT SetPageSettings(ISettingsProperties *pPageSettings);  
    HINSTANCE GetInstanceHandle(void);  
    int GetDialogResourceId(void);  
    void WindowCreated(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    void WindowShown(void);  
    void WindowHidden(void);  

    HRESULT NextClicked(void);  
    void ControlEvent(WORD eventId, WORD controlId);  
    void CommonControlEvent(WORD controlId, LPNMHDR pInfo, LPBOOL pCancel);  
    void UnhandledEvent(HWND hwnd, UINT message, WPARAM wParam, LPARAM lParam);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle wird durch **WizardPageImpl** implementiert, also müssen Sie sie in der Regel nicht selbst implementieren. Der Assistent ruft alle diese Methoden für Sie auf, wenn er mit Ihren benutzerdefinierten Seiten interagiert.  

#### <a name="iwizardpagecontainer-interface"></a>IWizardPageContainer-Schnittstelle  

```  
__interface IWizardPageContainer : IUnknown  
{  
    ILogger * Logger(void);  
    IPropertyBag * Properties(void);  
    HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance);  
    HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance);  
    HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest);  
    HRESULT GotoPage(LPCTSTR pageName);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    BOOL InPreview(void);  
    HWND GetHwnd(void);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle ist für Ihre Seite über die Methode **Container** verfügbar (durch **WizardPageImpl** implementiert) und gewährt Ihnen Zugriff auf verschiedene Dienste des Assistenten.  

##### <a name="ilogger--loggervoid"></a>ILogger * Logger(void)  
 Verwenden Sie diese Methode, um Nachrichten in die Protokolldatei zu schreiben, zum Beispiel:  

```  
Logger()->Verbose(s_component, L"Message for log file");  
```  

##### <a name="ipropertybag--propertiesvoid"></a>IPropertyBag * Properties(void)  
 Diese Methode gewährt Zugriff auf „Speichervariablen“, die Eigenschaften sind und sich nur im Arbeitsspeicher befinden, während der UDI-Assistent ausgeführt wird. Diese Eigenschaften stehen anderen Seiten zur Verfügung, entweder in Code oder XML mit der Syntax **$memoryVarName$**.  

##### <a name="hresult-createinstancelpctstr-type-out-iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance)  
 Diese Methode ermöglicht Ihnen, eine neue Instanz jeder registrierten Komponente zu erstellen. Allerdings ist es besser, die Vorlagenfunktion **CreateInstance** zu verwenden, da sie stark typisiert ist.  

##### <a name="hresult-getservicerefiid-iid-out-iunknown-ppinstance"></a>HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance)  
 Diese Methode ermöglicht Ihnen, einen Dienst abzurufen, der registriert wurde. Allerdings ist es besser, die Vorlagenfunktion **GetService** aufzurufen, die stark typisiert ist (anstelle **IUnknown** zu verwenden).  

##### <a name="hresult-replacevariableslpctstr-source-out-lpbstr-pdest"></a>HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest)  
 Diese Methode behandelt die Arbeit mit Variablen in Zeichenfolgenwerten. Sie unterstützt die Formate, die in Tabelle 51 und Tabelle 52 gezeigt werden.  

### <a name="table-51-hresult-replacevariables"></a>Tabelle 51: HRESULT ReplaceVariables  

|**Format**|**Beschreibung**|  
|-|-|  
|**$Name$**|Ersetzt den Wert einer Speichervariable mit diesem Namen (wenn keine Speichervariable mit diesem Namen vorhanden ist, wird das „Token“ entfernt).|  
|**%Name%**|Entweder eine Tasksequenzvariable oder eine Umgebungsvariable. Die Reihenfolge ist wie folgt:<br /><br /> 1.  Verwenden Sie den Wert einer Tasksequenzvariable, wenn vorhanden.<br />2.  Verwenden Sie den Wert einer Umgebungsvariable, wenn vorhanden.<br />3.  Entfernen Sie andernfalls den Text aus der Zeichenfolge.|  

### <a name="table-52-hresult-parameter"></a>Tabelle 52: HRESULT-Parameter  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**Quelle**|Die Eingabezeichenfolge, die eine beliebige Kombination der Variablen **$** und **%** oder keine enthalten kann.|  
|**pDest**|Enthält bei der Rückgabe eine neue Zeichenfolge, die alle Token gemäß Tabelle 51 ersetzt.|  

##### <a name="hresult-gotopagelpctstr-pagename"></a>HRESULT GotoPage(LPCTSTR pageName)  
 Diese Methode wurde nicht vollständig getestet. Dahinter steckt die Idee, dass Sie basierend auf dem in der XML-Konfigurationsdatei festgelegten Namen der Seite direkt zu einer bestimmten Seite navigieren können. Das Aufrufen dieser Methode umgeht **OnNextClicked** auf der Seite. Außerdem kann sich das Verhalten dieser Methode noch ändern, verwenden Sie sie also auf eigene Verantwortung.  

##### <a name="int-showmessageboxlpctstr-message-lpctstr-lpcaption-uint-utype"></a>int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType)  
 Diese Methode zeigt ein Meldungsfeld an, dessen Text und Beschriftung Sie angeben. Der Parameter **uType** ist ein beliebiger Wert, den Sie der Win32-Funktion **MessageBox** bereitstellen.  

##### <a name="bool-inpreviewvoid"></a>BOOL InPreview(void)  
 Diese Methode gibt TRUE zurück, wenn Sie den Assistenten im Vorschaumodus gestartet haben, indem Sie den Parameter **/preview** angeben. In der Seitenansicht ist die Schaltfläche **Weiter** nie deaktiviert. Mit dieser Methode können Sie Code in der Seitenansicht umgehen, z.B. Code der Probleme verursachen könnte, wenn Sie über keine gültigen Daten auf der Seite verfügen.  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 Diese Methode gibt das **HWND** des Hauptdialogfelds zurück. Verwenden Sie diese Methode mit Bedacht. Im Allgemeinen ist die Anwendungsprogrammierschnittstelle des UDI-Assistenten so entworfen, dass Sie nie direkt mit Fensterhandles arbeiten.  

#### <a name="iwizardpageview-interface"></a>IWizardPageView-Schnittstelle  

```  
__interface IWizardPageView : IUnknown  
{  
    HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown **ppControl);  
    HWND GetHwnd(void);  
    HWND GetControl(int itemId);  
    HRESULT Show (void);  
    HRESULT Hide(void);  
    HRESULT Focus(int itemId);  
    IWizardPage * Page(void);  
    IFormController * Form(void);  

    HRESULT FocusWizardButton(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
};  
```  

 Diese Schnittstelle ist für den Code Ihrer Seite über die Methode **View** verfügbar (wird von **WizardPageImpl** implementiert).  

##### <a name="hresult-getcontrolwrapperint-itemid-dialogcontroltypes-controltype-iunknown-ppcontrol"></a>HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown \*ppControl)  
 Der UDI-Assistent verwendet *Wrapper*, die eigentlich Fassaden für die Interaktion mit den Steuerelementen auf Ihrer Seite sind. Durch Verwendung dieser Fassaden anstelle der tatsächlichen Steuerelemente wird das Schreiben von Tests für Ihre Seite deutlich erleichtert, da Sie Modellfassaden aus Ihren Tests bereitstellen können.  

 Statt einer direkten Verwendung dieser Methode wird die Verwendung der Vorlagenmethode **GetControlWrapper** empfohlen, die eine starke Typisierung aufweist. Beispiel:  

```  
PComboBox m_pLanguagePackCombo;  
GetControlWrapper(View(), IDC_MY_COMBO, CONTROL_COMBO_BOX, &m_pCombo);  
```  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 Diese Methode gibt das Fensterhandle für Ihre Seite zurück. Im Allgemeinen sollten Sie keinen Zugriff auf dieses Fensterhandle benötigen.  

##### <a name="hwnd-getcontrolint-itemid"></a>HWND GetControl(int itemId)  
 Falls erforderlich, können Sie diese Methode aufrufen, um das Fensterhandle für ein Steuerelement auf Ihrer Seite abzurufen. (Es wird jedoch empfohlen, die Vorlagenfunktion **GetControlWrapper** aufzurufen.)  

##### <a name="hresult-show-void"></a>HRESULT Show (void)  
 Diese Methode ist nur zur internen Verwendung.  

##### <a name="hresult-hidevoid"></a>HRESULT Hide(void)  
 Diese Methode ist nur zur internen Verwendung.  

##### <a name="hresult-focusint-itemid"></a>HRESULT Focus(int itemId)  
 Legt den Eingabefokus auf ein bestimmtes Steuerelement fest.  

##### <a name="iwizardpage--pagevoid"></a>IWizardPage * Page(void)  
 Diese Methode ist nur zur internen Verwendung.  

##### <a name="iformcontroller--formvoid"></a>IFormController * Form(void)  
 Diese Methode ist nur zur internen Verwendung.  

##### <a name="hresult-focuswizardbuttonwizardbuttons-button"></a>HRESULT FocusWizardButton(WizardButtons button)  
 Legt den Fokus auf eine der Schaltflächen des Assistenten fest. **WizardButtons** weist zwei Werte auf: **BackButton** und **NextButton**.  

##### <a name="hresult-setenablewizardbuttons-button-bool-enable"></a>HRESULT SetEnable(WizardButtons button, BOOL enable)  
 Fordert an, dass eine der Schaltflächen des Assistenten aktiviert oder deaktiviert wird. Die Schaltfläche stimmt möglicherweise nicht mit dem von Ihnen angeforderten Status überein. Wenn Sie beispielsweise den UDI-Assistenten mit dem Switch **/preview** ausführen, werden die Schaltflächen immer aktiviert. **WizardButtons** weist zwei Werte auf: **BackButton** und **NextButton**.  

##### <a name="void-showwarningmessagelpctstr-message"></a>void ShowWarningMessage(LPCTSTR message)  
 Diese Methode zeigt unten im Seiteninhaltsbereich eine Warnmeldung an. Diese Meldung kann beliebigen Text enthalten.  

##### <a name="void-hidewarningmessagevoid"></a>void HideWarningMessage(void)  
 Blendet eine Warnmeldung aus, die Sie mit dem Aufruf von **ShowWarningMessage** angezeigt haben.  

#### <a name="ixmldocument-interface"></a>IXmlDocument-Schnittstelle  

```  
__interface IXmlDocument : IUnknown  
    HRESULT Load(LPCTSTR filename);  
    HRESULT LoadXml(LPCTSTR xml);  
    HRESULT Save(LPCWSTR filename);  
    HRESULT GetParseErrorMessage(LPBSTR pMessage);  
    HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList **ppNodes);  
    HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode **ppNode);  
    HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns);  
    HRESULT AddAttribute(IXMLDOMNode *pNode, LPCWSTR name, LPCWSTR value);  
    HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode **ppNode);  
};  
```  

##### <a name="overview"></a>Übersicht  
 Diese Schnittstelle wird von der Komponente **ID_IXmlDocument** implementiert, bei der es sich um eine Fassade handelt, die zur Vereinfachung der Arbeit mit XML-Dokumenten in C++ entwickelt wurde.  

##### <a name="hresult-loadlpctstr-filename"></a>HRESULT Load(LPCTSTR filename)  
 Diese Methode lädt ein XML-Dokument aus einer externen Datei. Sie gibt **S_OK** zurück, wenn die Datei ohne Fehler geladen wurde, oder **S_FALSE**, wenn ein Fehler aufgetreten ist. Wenn ein Fehler aufgetreten ist, können Sie die Fehlermeldung durch Aufrufen von **GetParseErrorMessage** abrufen.  

##### <a name="hresult-loadxmllpctstr-xml"></a>HRESULT LoadXml(LPCTSTR xml)  
 Diese Methode lädt ein XML-Dokument aus einer Zeichenfolge und nicht aus einer externen Datei. Außer bei der Quelle zum Lesen des XML-Dokuments ist das Verhalten mit der Methode **Load** identisch.  

##### <a name="hresult-savelpcwstr-filename"></a>HRESULT Save(LPCWSTR filename)  
 Diese Methode speichert das XML-Dokument, das im Arbeitsspeicher einer externen Datei enthalten ist.  

##### <a name="hresult-getparseerrormessagelpbstr-pmessage"></a>HRESULT GetParseErrorMessage(LPBSTR pMessage)  
 Diese Methode gibt ggf. eine neue Zeichenfolge mit der Fehlermeldung zum Laden des XML-Dokuments zurück. Die Methode gibt immer **S_OK** zurück.  

##### <a name="hresult-selectnodeslpctstr-xpath-ixmldomnodelist-ppnodes"></a>HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList \**ppNodes)  
 Mit dieser Methode können Sie einen XPath-Ausdruck zum Abrufen einer Sammlung von Knoten aus dem Dokument verwenden. Die Methode gibt immer **S_OK** zurück.  

##### <a name="hresult-selectsinglenodelpctstr-xpath-ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode \**ppNode)  
 Mit dieser Methode können Sie einen XPath-Ausdruck zum Abrufen eines Knotens aus dem Dokument verwenden. Die Methode gibt immer **S_OK** zurück.  

##### <a name="hresult-addschemalpctstr-filename-lpctstr-ns"></a>HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns)  
 Diese Methode fügt den Namen einer externen Schemadatei hinzu, die für die Überprüfung des Schemas Ihres XML-Dokuments verwendet wird, wenn dieses geladen wird. Bei dem von Ihnen angegebenen Namespace handelt es sich um die Zeichenfolge, die Sie in XPath-Abfragen verwenden können, auch wenn dies nicht getestet wurde.  

##### <a name="hresult-addattributeixmldomnode-pnode-lpcwstr-name-lpcwstr-value"></a>HRESULT AddAttribute(IXMLDOMNode \*pNode, LPCWSTR name, LPCWSTR value)  
 Diese Methode fügt ein neues Attribut zu einem vorhandenen Knoten im XML-Dokument hinzu. Siehe Tabelle 53.  

### <a name="table-53-hresult-addattribute"></a>Tabelle 53. HRESULT AddAttribute  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**pNode**|Der Knoten, zu dem ein Attribut hinzugefügt werden soll|  
|**Name**|Der Name des neuen Attributs|  
|**Wert**|Der Wert für das neue Attribut|  

##### <a name="hresult-createnodedomnodetype-type-lpcwstr-name-lpcwstr-ns-ixmldomnode-ppnode"></a>HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode \**ppNode)  
 Rufen Sie diese Methode auf, um einen neuen Knoten zu erstellen:  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 Nachdem Sie einen neuen Knoten erstellt haben, können Sie ihn als untergeordnetes Element zu einem anderen Knoten hinzufügen, indem Sie die Methode **AppendChild** des übergeordneten Elements aufrufen.  

### <a name="helper-functions"></a>Hilfsfunktionen  

#### <a name="createinstance-template-function"></a>CreateInstance-Vorlagenfunktion  

```  
HRESULT CreateInstance(IWizardPageContainer *pContainer, LPCTSTR type, I **ppObject)  
```  

 Diese Funktion ist in IWizardPageContainer.h definiert und stellt über die Methode **IWizardPageContainer->CreateInstance** einen typsicheren Wrapper zur Verfügung. Beispiel:  

```  
CreateInstance<IDirectory>(Container(), ID_Directory, &pDirectory);  
```  

 Dieser Code erstellt eine neue Komponente vom Typ **ID_Directory** zum Abrufen der **IDirectory**-Schnittstelle dieser Komponente.  

#### <a name="getservice-template-function"></a>GetService-Vorlagenfunktion  

```  
void GetService(IWizardPageContainer *pContainer, I **ppService)  
```  

 Diese Funktion ist in IWizardPageContainer.h definiert und stellt über die Methode **IWizardPageContainer->GetService** einen typsicheren Wrapper zur Verfügung. Beispiel:  

```  
GetService<ITSVariableBag>(Container(), &pTsBag);  
```  

 Diese Funktion ruft die Komponente der Tasksequenz ab, welche die **ITSVariableBag**-Schnittstelle unterstützt. (Bei **ITSVariableBag** können Sie stattdessen die Methode „TSVariables“ der **WizardPageImpl**-Klasse verwenden.)  

### <a name="udi-wizard-designer-configuration-file-schema-reference"></a>Verweis auf Konfigurationsdateischema des Designers des UDI-Assistenten  
 Diese Datei wird vom Designer des UDI-Assistenten verwendet. Für jede benutzerdefinierte DLL-Datei wird eine separate Datei erstellt, die benutzerdefinierte Editoren für Assistentenseiten, benutzerdefinierte Tasks oder benutzerdefinierte Validierungssteuerelemente enthalten kann. Die Datei muss mit *.config* enden und im Ordner „*installation_folder*\Bin\Config“ enthalten sein (dabei steht *installation_folder* für den Ordner, in dem Sie MDT installiert haben).  

  In Tabelle 54 werden die Elemente in der Konfigurationsdatei des Designers des UDI-Assistenten mit den zugehörigen Beschreibungen aufgelistet. Das **DesignerConfig**-Element ist der Stammknoten für diesen Verweis.  

### <a name="table-54-elements-in-the-udi-wizard-designer-configuration-file-and-their-descriptions"></a>Tabelle 54. Elemente in der Konfigurationsdatei des Designers des UDI-Assistenten mit zugehörigen Beschreibungen  

|**Elementname**|**Beschreibung**|  
|-|-|  
|[DesignerConfig](#DesignerConfig)|Gibt den Stamm für alle anderen Elemente an|  
|[DesignerMappings](#DesignerMappings)|Gruppiert eine Reihe von [Page](#Page)-Elementen|  
|[Page](#Page)|Gibt den Editor für Assistentenseiten an, der in den Designer des UDI-Assistenten geladen werden soll und für die Bearbeitung der Konfigurationseinstellungen für eine Assistentenseite verwendet wird|  
|[Param](#Param)|Gibt einen Parameter an, der an das übergeordnete [Task](#Task)- oder [Validator](#Validator)-Element übergeben wird und einem [Setter]()-Element in der Konfigurationsdatei des UDI Wizard entspricht. **Hinweis:** Die Attribute für dieses Element unterscheiden sich, wenn das [Task](#Task)- oder [Validator](#Validator)-Element das übergeordnete Element ist.|  
|[Task](#Task)|Gibt einen Task innerhalb der Taskbibliothek an|  
|[TaskItem](#TaskItem)|Gibt eine Gruppe von Parametern an, die an den Task übergeben werden sollen|  
|[TaskLibrary](#TaskLibrary)|Gruppiert eine Reihe von [Task](#Task)-Elementen|  
|[Validator](#Validator)|Gibt ein Validierungssteuerelement innerhalb der Bibliothek für Validierungssteuerelemente an|  
|[ValidatorLibrary](#ValidatorLibrary)|Gruppiert eine Reihe von [Validator](#Validator)-Elementen|  

####  <a name="DesignerConfig"></a> DesignerConfig  
 Dieses Element gibt den Stamm für alle anderen Elemente an.  

##### <a name="element-information"></a>Elementinformationen  
  In Tabelle 55 finden Sie weitere Informationen zum [DesignerConfig](#DesignerConfig)-Element.  

### <a name="table-55-designerconfig-element-information"></a>Tabelle 55. Informationen zum DesignerConfig-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Eins: Dieses Element ist erforderlich.|  
|Übergeordnete Elemente|Keine|  
|Inhalt|**DesignerMappings**, **TaskLibrary**, **ValidatorLibrary**|  

##### <a name="element-attributes"></a>Elementattribute  
 Dieses Element besitzt keine Attribute.  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="DesignerMappings"></a> DesignerMappings  
 Dieses Element gruppiert eine Reihe von [Seitenelementen](#Page).  

##### <a name="element-information"></a>Elementinformationen  
  In Tabelle 56 finden Sie weitere Informationen zum [DesignerMappings](#DesignerMappings)-Element.  

### <a name="table-56-designermappings-element-information"></a>Tabelle 56. Informationen zum DesignerMappings-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|0 (null) oder eins innerhalb des [DesignerConfig](#DesignerConfig)-Elements (Dieses Element ist optional, wenn die DLL keine benutzerdefinierte Assistentenseite enthält, die dieser Konfigurationsdatei des Designers des UDI-Assistenten entspricht.)|  
|Übergeordnete Elemente|**DesignerConfig**|  
|Inhalt|**Page**|  

##### <a name="element-attributes"></a>Elementattribute  
 Dieses Element besitzt keine Attribute.  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   - <DesignerMappings>  
        <Page DLL="SharedPages.dll"  
           Description="Used to display text that describes the current stagegroup"  
           Type="Microsoft.SharedPages.WelcomePage"  
           DisplayName="Welcome"   
           Image="Welcome_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.WelcomePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Captures or restores user state data"  
           Type="Microsoft.OSDRefresh.UserStatePage"  
           DisplayName="User Data"  
           Image="UserState_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.UserStatePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Allows selecting the image to install, target drive, and whether to format"  
           Type="Microsoft.OSDRefresh.VolumePage"  
           DisplayName="Volume"  
           Image="Volume_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.VolumePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
     </DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Page"></a> Page  
 Dieses Element gibt den Editor für Assistentenseiten an, der in den Designer des UDI-Assistenten geladen werden soll, der wiederum für die Bearbeitung der Konfigurationseinstellungen für eine Assistentenseite verwendet wird.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 57 finden Sie weitere Informationen zum [Page](#Page)-Element.  

### <a name="table-57-page-element-information"></a>Tabelle 57. Informationen zum Page-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Mindestens ein Vorkommen für jede im [DesignerMappings](#DesignerMappings)-Element definierte Assistentenseite|  
|Übergeordnete Elemente|**DesignerMappings**|  
|Inhalt|Wohlgeformte XML-Inhalte|  

##### <a name="element-attributes"></a>Elementattribute  
In Tabelle 58 werden die Attribute des [Page](#Page)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-58-attributes-and-corresponding-values-for-the-page-element"></a>Tabelle 58. Attribute und zugehörige Werte des Page-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**Beschreibung**|Gibt Text an, der Informationen zu dem im Designer des UDI-Assistenten angezeigten Parameter enthält|  
|**DesignerAssembly**|Gibt den Namen der DLL-Datei an, die dem Editor für Assistentenseiten zugeordnet ist (Die DLL-Datei muss im Ordner „*installation_folder*\Bin“ enthalten sein (dabei steht *installation_folder* für den Ordner, in dem Sie MDT installiert haben).|  
|**DesignerType**|Gibt den Namen des Editors für Assistentenseite innerhalb der DLL-Datei im Attribut **DesignerAssembly** an (Dies ist der Microsoft .NET-Typ des Editors für Assistentenseiten mit dem vollständig qualifizierten Microsoft .NET-Namespace.)|  
|**DisplayName**|Gibt den benutzerfreundlichen Namen des Seiteneditors an, der im Designer des UDI-Assistenten angezeigt wird|  
|**DLL**|Gibt den Namen der DLL-Datei an, die der Assistentenseite zugeordnet ist (Die DLL-Datei muss im Ordner „*installation_folder*\Templates\Distribution\Tools\\*platform*“ enthalten sein (dabei steht *installation_folder* für den Ordner, in dem Sie MDT installiert haben, während *platform* für **x86** der 32-Bit-Version oder für **x64** der 64-Bit-Version stehen kann.) **Hinweis:** Stellen Sie sicher, dass die DLL-Prozessorarchitektur der installierten MDT-Prozessorarchitektur entspricht. Wenn Sie beispielsweise eine 32-Bit-Version von MDT installiert haben, sollten Sie sicherstellen, dass Sie eine 32-Bit-DLL für die Assistentenseite verwenden.|  
|**Image**|Gibt den Namen eines Images der Seite im PNG-Format (PNG = Portable Network Graphics) an (Die PNG-Datei muss im Ordner „*installation_folder*\Bin\Images“ enthalten sein (dabei steht *installation_folder* für den Ordner, in dem Sie MDT installiert haben).|  
|**Typ**|Gibt den Editor für Assistentenseiten an und muss mit dem Namen übereinstimmen, der bei der Registrierung der benutzerdefinierten Seite verwendet wurde|  

##### <a name="remarks"></a>Hinweise  
 Der Designer des UDI-Assistenten verwendet das [Page](#Page)-Element wie eine Vorlage zur Erstellung des ursprünglichen XML-Codes für einen neuen Assistenten. Der Designer des UDI-Assistenten führt eine Schemaüberprüfung durch, um sicherzustellen, dass das [Page](#Page)-Element und die untergeordneten Elemente ein gültiges Format aufweisen. Dieses Element gibt eine Zuordnung zwischen dem Seitentyp des UDI-Assistenten und den Informationen an, die der Designer des UDI-Assistenten für die Bearbeitung und Erstellung von Seiten dieses Typs mithilfe eines benutzerdefinierten Seiteneditors benötigt.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="Param"></a> Param  
 Dieses Element gibt einen Parameter an, der an das übergeordnete [Task](#Task)- oder [Validator](#Validator)-Element übergeben wird und einem [Setter]()-Element in der Konfigurationsdatei des UDI-Assistenten entspricht.  

> [!NOTE]
>  Dies Attribute für dieses Element unterscheiden sich, wenn das [Task](#Task)- oder [Validator](#Validator)-Element das übergeordnete Element ist.  

##### <a name="element-information"></a>Elementinformationen  
 In Tabelle 59 finden Sie weitere Informationen zum [Param](#Param)-Element.  

### <a name="table-59-param-element-information"></a>Tabelle 59. Informationen zum Param-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Mindestens ein Vorkommen bei jedem übergeordneten [TaskItem](#TaskItem)- oder [Validator](#Validator)-Element|  
|Übergeordnete Elemente|**TaskItem**, **Validator**|  
|Inhalt|Wohlgeformte XML-Inhalte|  

##### <a name="element-attributes"></a>Elementattribute  
  In Tabelle 60 werden die Attribute des [Param](#Param)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-60-attributes-and-corresponding-values-for-the-param-element"></a>Tabelle 60. Attribute und zugehörige Werte des Param-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**Beschreibung**|Gibt Text an, der Informationen zu dem im Designer des UDI-Assistenten angezeigten Parameter enthält. **Hinweis:** Dieses Attribut ist nur für das [Validator](#Validator)-Element gültig.|  
|**DisplayName**|Gibt den benutzerfreundlichen Namen des Parameters für Validierungssteuerelemente an, der für die entsprechende Seite des UDI-Assistenten im Designer des UDI-Assistenten angezeigt wird (Dieser Name ist in der Regel beschreibender als das Attribut **Name**.) **Hinweis:** Dieses Attribut gilt nur für das [Validator](#Validator)-Element.|  
|**Name**|Gibt den Namen des Parameters an, der je nach übergeordnetem Element an den Task oder das Validierungssteuerelement übergeben wird (Dieses Attribut wird in der Konfigurationsdatei des UDI-Assistenten das Attribut **Property** in einem [Setter]()-Element.) **Hinweis:** Dieser Parameter wird für die übergeordneten [TaskItem](#TaskItem)- und [Validator](#Validator)-Elemente verwendet.|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="Task"></a> Task  
 Dieses Element gibt einen Task innerhalb der Taskbibliothek an.  

##### <a name="element-information"></a>Elementinformationen  
 In Tabelle 61 finden Sie weitere Informationen zum [Task](#Task)-Element.  

### <a name="table-61-task-element-information"></a>Tabelle 61. Informationen zum Task-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Mindestens ein Vorkommen im [TaskLibrary](#TaskLibrary)-Element (Dieses Element ist nicht optional, wenn das **TaskLibrary**-Element angegeben ist.)|  
|Übergeordnete Elemente|**TaskLibrary**|  
|Inhalt|**TaskItem**|  

##### <a name="element-attributes"></a>Elementattribute  
  In Tabelle 62 werden die Attribute des [Task](#Task)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-62-attributes-and-corresponding-values-for-the-task-element"></a>Tabelle 62. Attribute und zugehörige Werte des Task-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**Beschreibung**|Gibt Text an, der Informationen zu dem im Designer des UDI-Assistenten angezeigten Task enthält|  
|**DLL**|Gibt den Namen der DLL-Datei an, die dem Task zugeordnet ist (Die DLL-Datei muss im Ordner „*installation_folder*\Templates\Distribution\Tools\\*platform*“ enthalten sein (dabei steht *installation_folder* für den Ordner, in dem Sie MDT installiert haben, während *platform* für **x86** der 32-Bit-Version oder für **x64** der 64-Bit-Version stehen kann.)|  
|**Name**|Gibt den Namen des auf der entsprechenden Seite des UDI-Assistenten und im Designer des UDI-Assistenten angezeigten Tasks an|  
|**Typ**|Gibt den Tasktyp an, der bei der Registrierung von Zuordnungsinstanzen registriert wird und zum Aufrufen eines bestimmten Tasks in einer DLL-Datei verwendet wird|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="TaskItem"></a> TaskItem  
 Dieses Element gibt eine Gruppe von Parametern an, die an den Task übergeben werden sollen.  

##### <a name="element-information"></a>Elementinformationen  
  In Tabelle 63 finden Sie weitere Informationen zum [TaskItem](#TaskItem)-Element.  

### <a name="table-63-taskitem-element-information"></a>Tabelle 63. Informationen zum TaskItem-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Mindestens ein Vorkommen in jedem **Task**-Element|  
|Übergeordnete Elemente|**Task**|  
|Inhalt|**Param**|  

##### <a name="element-attributes"></a>Elementattribute  
 In Tabelle 64 werden die Attribute des [TaskItem](#TaskItem)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-64-attribute-and-corresponding-values-for-the-taskitem-element"></a>Tabelle 64. Attribute und zugehörige Werte des TaskItem-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**Typ**|Gibt den Elementtyp an, der in der Konfigurationsdatei des UDI-Assistenten erstellt wird. Es wird ein XML-Element erstellt, das dem Wert dieses Attributs entspricht. Wenn der Wert dieses Attributs beispielsweise [File](#File) lautet, wird in der Konfigurationsdatei des UDI-Assistenten ein **File**-Element erstellt.<br /><br /> Derzeit werden nur folgende Werte unterstützt:<br /><br /> Der Wert -   **File**, für den zwei untergeordnete [Param](#Param)-Elemente erforderlich sind (ein untergeordnetes **Param**-Element mit dem auf **Source** festgelegten Attribut **Name** und ein weiteres untergeordnetes **Param**-Element mit dem auf **Dest** festgelegten Attribut **Name**)<br />Der Wert -   [Setter](), für den ein untergeordnetes **Param**-Element erforderlich ist|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="TaskLibrary"></a> TaskLibrary  
 Dieses Element gruppiert eine Reihe von [Task](#Task)-Elementen.  

##### <a name="element-information"></a>Elementinformationen  
 In Tabelle 65 finden Sie weitere Informationen zum [TaskLibrary](#TaskLibrary)-Element.  

### <a name="table-65-tasklibrary-element-information"></a>Tabelle 65. Informationen zum TaskLibrary-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|0 (null) oder eins innerhalb des [DesignerConfig](#DesignerConfig)-Elements (Dieses Element ist optional, wenn keine benutzerdefinierten Tasks in der DLL enthalten sind, die dieser Konfigurationsdatei des Designers des UDI-Assistenten entsprechen.)|  
|Übergeordnete Elemente|**DesignerConfig**|  
|Inhalt|**Task**|  

##### <a name="element-attributes"></a>Elementattribute  
 Dieses Element besitzt keine Attribute.  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  

```  
<DesignerConfig>  
   - <TaskLibrary>  
        +<Task DLL="" Description="Executes a process with the given command line." Type="Microsoft.Wizard.ShellExecuteTask" Name="Shell Execute Task">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
        +<Task DLL="SharedPages.dll" Description="Check to ensure a wired network connection is available." Type="Microsoft.SharedPages.WiredNetworkTask" Name="Wired Network Check">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.OSDRefresh.ACPowerTask" Name="AC Power Check">  
        +<Task DLL="" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.Wizard.CopyFilesTask" Name="Copy Files Task">  
     </TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Validator"></a> Validator  
 Dieses Element gibt ein Validierungssteuerelement innerhalb der Bibliothek für Validierungssteuerelemente an.  

##### <a name="element-information"></a>Elementinformationen  
 In Tabelle 66 finden Sie weitere Informationen zum [Validator](#Validator)-Element.  

### <a name="table-66-validator-element-information"></a>Tabelle 66. Informationen zum Validator-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|0 (null) oder mehr Vorkommen innerhalb des [ValidatorLibrary](#ValidatorLibrary)-Elements (Dieses Element ist optional.)|  
|Übergeordnete Elemente|**ValidatorLibrary**|  
|Inhalt|**Param**|  

##### <a name="element-attributes"></a>Elementattribute  
In Tabelle 67 werden die Attribute des [Validator](#Validator)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-67-attributes-and-corresponding-values-for-the-validator-element"></a>Tabelle 67. Attribute und zugehörige Werte des Validator-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**Beschreibung**|Gibt den Text an, der Informationen zu dem im Designer des UDI-Assistenten angezeigten Validierungssteuerelements enthält|  
|**DisplayName**|Gibt den benutzerfreundlichen Namen des im Designer des UDI-Assistenten angezeigten Validierungssteuerelements an (Dieser Name ist in der Regel beschreibender als das Attribut **Name**.)|  
|**DLL**|Gibt den Namen der DLL-Datei an, die dem Validierungssteuerelement zugeordnet ist (die DLL-Datei muss im Ordner „*installation_folder*\Templates\Distribution\Tools\\*platform*“ enthalten sein (dabei steht *installation_folder* für den Ordner, in dem Sie MDT installiert haben, während *platform* für **x86** der 32-Bit-Version oder für **x64** der 64-Bit-Version steht).|  
|**Name**|Gibt den Namen des auf der entsprechenden Seite des UDI-Assistenten und im Designer des UDI-Assistenten angezeigten Validierungssteuerelements an|  
|**Typ**|Gibt den Validierungssteuerelementtyp an, der bei der Registrierung von Zuordnungsinstanzen registriert und zum Aufrufen eines bestimmten Validierungssteuerelements in einer DLL-Datei verwendet wird|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="ValidatorLibrary"></a> ValidatorLibrary  
 Dieses Element gruppiert eine Reihe von [Validator](#Validator)-Elementen.  

##### <a name="element-information"></a>Elementinformationen  
 In Tabelle 68 finden Sie weitere Informationen zum [ValidatorLibrary](#ValidatorLibrary)-Element.  

### <a name="table-68-validatorlibrary-element-information"></a>Tabelle 68. Informationen zum ValidatorLibrary-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|0 (null) oder ein Vorkommen innerhalb des [DesignerConfig](#DesignerConfig)-Elements (dieses Element ist optional, wenn keine benutzerdefinierten Validierungssteuerelemente in der DLL enthalten sind, die dieser Konfigurationsdatei des Designers des UDI-Assistenten entsprechen).|  
|Übergeordnete Elemente|**DesignerConfig**|  
|Inhalt|**Validator**|  

##### <a name="element-attributes"></a>Elementattribute  
 Dieses Element besitzt keine Attribute.  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 <DesignerConfig\>   + <TaskLibrary\>   - <ValidatorLibrary\>        +<Validator DLL="" Description="Erfordert Text in einem Feld" Type="Microsoft.Wizard.Validation.NonEmpty" Name="NonEmpty"\>        +<Validator DLL="" Description="Erlaubt bestimmte Zeichen nicht in einem Feld" Type="Microsoft.Wizard.Validation.InvalidChars" Name="InvalidChars"\>        +<Validator DLL="" Description="Muss einem vordefinierten Muster entsprechen" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern"\>        +<Validator DLL="" Description="Die Inhalt müssen einem regulären Ausdruck entsprechen" Type="Microsoft.Wizard.Validation.RegEx" Name="RegEx"\>     </ValidatorLibrary\>   + <DesignerMappings\></DesignerConfig\>  

## <a name="udi-wizard-designer-reference"></a>Verweis auf den Designer des UDI-Assistenten  

### <a name="controls"></a>Steuerelemente  
 Bei den Steuerelementen, mit denen benutzerdefinierte Editoren für Assistentenseiten für die Verwendung im Designer des UDI-Assistenten erstellt werden, handelt es sich um WPF-Instanzen vom Typ **UserControl**. In Tabelle 69 werden die Steuerelemente aufgelistet, mit denen Sie benutzerdefinierte Editoren für Assistentenseiten erstellen können.  

### <a name="table-69-controls-that-can-be-used-to-create-custom-wizard-page-editors"></a>Tabelle 69. Steuerelemente für die Erstellung von benutzerdefinierten Editoren für Assistentenseiten  

|Steuerelement|Beschreibung|  
|-|-|  
|[CollectionTControl](#CollectionTControl)|Mit diesem Steuerelement werden Daten bearbeitet, die im [Data](#Data)-Element innerhalb eines [Page](#Page)-Elements gespeichert sind.|  
|[FieldElementControl](#FieldElementControl)|Mit diesem Steuerelement wird ein Feld bearbeitet, das in der Regel mit einem TextBox-Steuerelement auf der XAML-Seite verknüpft ist.|  
|[SetterControl](#SetterControl)|Mit diesem Steuerelement wird der Wert eines [Setter]()-Elements in der Konfigurationsdatei des UDI-Assistenten geändert.|  

####  <a name="CollectionTControl"></a> CollectionTControl  
 Dieses Steuerelement stellt viele Funktionen für die Bearbeitung von Daten bereit. Wie bei der Verwendung dieses Steuerelements vorzugehen ist, lernen Sie am besten, wenn Sie sich das Beispiel ansehen, das zeigt, wie Daten unter dem **Data**-Element einer Seite bearbeitet werden. Das Beispiel zeigt insbesondere, wie Elemente in diesem Steuerelement hinzugefügt, entfernt und bearbeitet werden.  

####  <a name="FieldElementControl"></a> FieldElementControl  
 Mit diesem Steuerelement wird ein Feld bearbeitet, das in der Regel mit einem **TextBox**-Steuerelement auf der XAML-Seite verknüpft ist.  

##### <a name="example"></a>Beispiel  
 Der folgende Auszug aus einer XAML-Datei veranschaulicht die Verwendung von **FieldElementControl** für die Konfiguration des Standardwerts eines Felds auf einer Assistentenseite mithilfe eines untergeordneten **TextBox**-Steuerelements:  

```  
<Controls:FieldElementControl  
Width="450"  
Margin="0,5"  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
HeaderText="Location Combo Box"  
InstructionText="Here you can configure the behavior of the location combo box."  
HideValidationTab="True">  

<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
</Controls:FieldElementControl>  
```  

##### <a name="properties"></a>Eigenschaften  

###### <a name="fielddata"></a>FieldData  
 Diese Zeichenfolgeneigenschaft enthält Informationen zum Verbinden von **FieldElementControl** mit der zugrunde liegenden XML für das Feld. Die Verbindung wird mit einer Eigenschaft der Seiteneditorschnittstelle hergestellt. Der folgende Auszug aus einer XAML-Datei veranschaulicht die Verwendung der Eigenschaft **FieldData**:  

```  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
```  

 In diesem Auszug lautet der Name der Seiteneditorschnittstelle **ControlRoot** und wird im Parameter **ElementName** angegeben. Die Bindung erfolgt mit der Eigenschaft **DataContext.Location** der **ControlRoot**-Seiteneditorschnittstelle. **DataContext** ist ein Ansichtsmodell, das auf das [Page](#Page)-Element in der Konfigurationsdatei des UDI-Assistenten verweist. **Location** ist eine Eigenschaft der Ansicht, die eine Liste der möglichen Speicherorte zurückgibt und von einem [Data](#Data)-Element in der Konfigurationsdatei des UDI-Assistenten definiert wird. Jeder Speicherort wird von einem [DataItem](#DataItem)-Element in der Konfigurationsdatei des UDI-Assistenten definiert.  

###### <a name="headertext"></a>HeaderText  
 Mit dieser Zeichenfolge können Sie einen Header für das Steuerelement [FieldElementControl](#FieldElementControl) angeben. Der Header fungiert als Titel des Steuerelements und ist als fetter, orangefarbener Text formatiert, der direkt über dem Steuerelement angezeigt wird.  

###### <a name="instructiontext"></a>InstructionText  
 Mit dieser Zeichenfolge können Sie Informationen für das Steuerelement [FieldElementControl](#FieldElementControl) angeben. Der Text enthält in der Regel eine Kurzbeschreibung des Felds sowie eine Erläuterung dessen, welche Auswirkungen das Feld auf die entsprechende Assistentenseite hat.  

###### <a name="hideenablebutton"></a>HideEnableButton  
 Mit dieser booleschen Eigenschaft können Sie die Sichtbarkeit der Schaltfläche steuern, mit welcher der Status zwischen **Entsperrt** und **Gesperrt** (aktiviert oder deaktiviert) geändert werden kann. Bei Festlegung auf:  

-   **TRUE** ist die Schaltfläche nicht sichtbar  

-   **FALSE** ist die Schaltfläche sichtbar (Dies ist der Standardwert.)  

###### <a name="hidedefaulttab"></a>HideDefaultTab  
 Mit dieser booleschen Eigenschaft können Sie die Sichtbarkeit des Abschnitts steuern, der das für die Festlegung des Standardwerts verwendete Steuerelement enthält. Obwohl sich die Eigenschaft auf eine Registerkarte bezieht, kann bei dem Steuerelement [FieldElementControl](#FieldElementControl) statt einer Registerkarte ein Abschnitt ausgeblendet werden. Bei Festlegung auf:  

-   **TRUE** ist der Abschnitt nicht sichtbar  

-   **FALSE** ist der Abschnitt sichtbar (Dies ist der Standardwert.)  

###### <a name="hideborder"></a>HideBorder  
 Mit dieser booleschen Eigenschaft können Sie die Sichtbarkeit des Rahmens um das Feldsteuerelement steuern. Bei Festlegung auf:  

-   **TRUE** ist der Rahmen nicht sichtbar  

-   **FALSE** ist der Rahmen sichtbar (Dies ist der Standardwert.)  

###### <a name="hideimage"></a>HideImage  
 Mit dieser booleschen Eigenschaft können Sie die Sichtbarkeit des Images steuern, das von der Eigenschaft **FieldImageSource** konfiguriert wird. Bei Festlegung auf:  

-   **TRUE** ist das Image nicht sichtbar  

-   **FALSE** ist das Image sichtbar (Dies ist der Standardwert.)  

###### <a name="hidevalidationtab"></a>HideValidationTab  
 Mit dieser booleschen Eigenschaft können Sie die Sichtbarkeit des Abschnitts steuern, in dem die Liste der Validierungssteuerelemente verwaltet wird. Obwohl sich die Eigenschaft auf eine Registerkarte bezieht, kann bei dem Steuerelement [FieldElementControl](#FieldElementControl) statt einer Registerkarte ein Abschnitt ausgeblendet werden. Bei Festlegung auf:  

-   **TRUE** ist der Abschnitt nicht sichtbar  

-   **FALSE** ist der Abschnitt sichtbar (Dies ist der Standardwert.)  

###### <a name="hidesummarytab"></a>HideSummaryTab  
 Mit dieser booleschen Eigenschaft können Sie die Sichtbarkeit des Abschnitts steuern, in dem Sie die Beschriftung für das Feld mit der Zusammenfassung konfigurieren. Die Beschriftung und der entsprechende Wert des Felds werden in einem **SummaryPage**-Assistentenseitentyp in einem Stage Flow angezeigt. Obwohl sich die Eigenschaft auf eine Registerkarte bezieht, kann bei dem Steuerelement [FieldElementControl](#FieldElementControl) statt einer Registerkarte ein Abschnitt ausgeblendet werden. Bei Festlegung auf:  

-   **TRUE** ist der Abschnitt nicht sichtbar  

-   **FALSE** ist der Abschnitt sichtbar (Dies ist der Standardwert.)  

###### <a name="hidetasksequencetab"></a>HideTaskSequenceTab  
 Mit dieser booleschen Eigenschaft können Sie die Sichtbarkeit des Abschnitts steuern, in dem Sie die Variable der Tasksequenz konfigurieren, die dem Feld entspricht. Obwohl sich die Eigenschaft auf eine Registerkarte bezieht, kann bei dem Steuerelement [FieldElementControl](#FieldElementControl) statt einer Registerkarte ein Abschnitt ausgeblendet werden. Bei Festlegung auf:  

-   **TRUE** ist der Abschnitt nicht sichtbar  

-   **FALSE** ist der Abschnitt sichtbar (Dies ist der Standardwert.)  


####  <a name="SetterControl"></a> SetterControl  
 Mit diesem Steuerelement wird der Wert eines [Setter]()-Elements in der Konfigurationsdatei des UDI-Assistenten geändert. Dieses Steuerelement enthält ein untergeordnetes Steuerelement, mit dem der Wert des **setter**-Elements geändert werden kann.  

##### <a name="example"></a>Beispiel  
 Der folgende Auszug aus einer XAML-Datei veranschaulicht die Verwendung des Steuerelements **SetterControl** für die Änderung eines [Setter]()-Elements mit dem Namen **KeyLocationSetter** mithilfe eines untergeordneten **TextBox**-Steuerelements.  

```  
<Controls:SetterControl Margin="5"  
        Width="450"  
        HeaderText="Title text"  
        SetterData="{Binding KeyLocationSetter}"   
        InstructionText="What this means…"  
        HorizontalAlignment="Left">  

    <TextBox  
                   Margin="0,3"  
                   Text="{Binding SetterData.SetterValue, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"  
    />  

</Controls:SetterControl>  
```  

##### <a name="properties"></a>Eigenschaften  

###### <a name="setterdata"></a>SetterData  
 Sie müssen diese Eigenschaft an eine Eigenschaft in Ihrer Ansicht oder Ihrem Ansichtsmodell verbinden, die mit dem Setter verbunden ist. Die Vorgehensweise ist vergleichbar mit dem Binden an ein Feld, wie für das Steuerelement **FieldElementControl** beschrieben wurde.  

###### <a name="headertext"></a>HeaderText  
 Mit dieser Eigenschaft können Sie den Text festlegen, der im Header des Steuerelements angezeigt werden soll. Betrachten Sie diese Eigenschaft als einen Titel für das Steuerelement. Standardmäßig wird sie fett und in Orange angezeigt.  

###### <a name="instructiontext"></a>InstructionText  
 Legen Sie diese Eigenschaft für den Text fest, der unterhalb des Headers erscheinen soll. In der Regel handelt es sich dabei um eine Anweisung, über die der Benutzer Ihres benutzerdefinierten Editors erfährt, wann und weshalb er bzw. sie das Verhalten des Felds ändern sollte.  

### <a name="interfaces"></a>Schnittstellen  
In Tabelle 70 werden die Schnittstellen aufgelistet, mit denen Sie benutzerdefinierte Editoren für Assistentenseiten erstellen können.  

### <a name="table-70-interfaces-that-can-be-used-to-create-custom-wizard-page-editors"></a>Tabelle 70. Schnittstellen für die Erstellung von benutzerdefinierten Editoren für Assistentenseiten  

|**Schnittstelle**|**Beschreibung**|  
|-|-|  
|[IDataService](#IDataService)|Über diese Schnittstelle können Sie Felder mit den **Data**-Elementen in der Konfigurationsdatei des UDI-Assistenten verbinden.|  
|[IMessageBoxService](#IMessageBoxService)|Diese Schnittstelle bietet Zugriff auf Methoden, mit denen Sie Meldungsfelder anzeigen können.|  

####  <a name="IDataService"></a> IDataService  
 Diese Schnittstelle enthält verschiedene Eigenschaften und Methoden, von denen Sie jedoch voraussichtlich nur eine Eigenschaft benötigen. Bei dieser Eigenschaft handelt es sich um die einzige hier dokumentierte Eigenschaft.  

 Sie können die Abhängigkeitsinjektion verwenden, um mit Code wie dem folgenden in Ihrer Klasse einen Zeiger für diese Schnittstelle abzurufen:  

```  
[Dependency]  
public IDataService DataService { get; set; }  
```  

##### <a name="properties"></a>Eigenschaften  
 In Tabelle 71 werden die Eigenschaften für die **IDataService**-Schnittstelle aufgelistet.  

### <a name="table-71-properties-for-the-idataservice-interface"></a>Tabelle 71. Eigenschaften für die IDataService-Schnittstelle  

|**Schnittstelle**|**Beschreibung**|  
|-|-|  
|[CurrentPage](#CurrentPage)|Diese Eigenschaft bietet Zugriff auf die XML-Elemente, Attribute und Werte unterhalb des Kontexts der aktuellen Seite, die in der Konfigurationsdatei des UDI-Assistenten bearbeitet werden|  

######  <a name="CurrentPage"></a> CurrentPage  

```  
XElement CurrentPage { get; set; }  
```  

 Diese Eigenschaft bietet Zugriff auf den XML-Code für die aktuelle Seite. Sie sollten diese Eigenschaft niemals festlegen. Es steht Ihnen jedoch frei, den XML-Code für Ihre Seite zu ändern. Der beispielhafte Seiteneditor zeigt Beispiele für die Änderung des XML-Codes an. Sie verwenden diese Eigenschaft hauptsächlich, wenn Sie über benutzerdefinierte Daten verfügen. Bei Feldern und Eigenschaften (Setter) können Sie vorgefertigte Steuerelemente verwenden, die sich um sämtliche Details kümmern.  

####  <a name="IMessageBoxService"></a> IMessageBoxService  
 Diese Schnittstelle bietet Zugriff auf Methoden, mit denen Sie Meldungsfelder anzeigen können. Möglicherweise fragen Sie sich, wofür Sie eine Schnittstelle zum Anzeigen eines Meldungsfelds benötigen. Tatsächlich benötigen Sie sie nicht: Microsoft verwendet diese Schnittstelle verschlüsselt, da dies für das Schreiben automatisierter Tests für Designerseiten hilfreich ist.  

 Die Verwendung dieser Methoden bietet jedoch einen Vorteil: Bei den Dialogfeldern ist als „Besitzer“ immer der UDI-Assistent festgelegt. Dadurch wird sichergestellt, dass das Dialogfeld ordnungsgemäß mit dem verknüpft ist.  

 Sie können die Abhängigkeitsinjektion verwenden, um mit Code wie dem folgenden in Ihrer Klasse einen Zeiger für diese Schnittstelle abzurufen:  

```  
[Dependency]  
public IMessageBoxService MessageBoxes { get; set; }  
```  

##### <a name="methods"></a>Methoden  
 In Tabelle 72 werden die Methoden für die **IMessageBoxService**-Schnittstelle aufgelistet.  

### <a name="table-72-methods-for-the-imessageboxservice-interface"></a>Tabelle 72. Methoden für die IMessageBoxService-Schnittstelle  

|**Methode**|**Beschreibung**|  
|-|-|  
|[ShowMessageBox](#ShowMessageBox)|Diese überladene Methode wird verwendet, um ein Meldungsfeld mit folgenden Mitgliedern anzuzeigen:<br /><br /> -   [ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)<br />-   [ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)<br />-   [ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|  
|[ShowDialogWindow](#ShowDialogWindow)|Mit dieser Methode können Sie ein neues Dialogfeld erstellen.|  
|[ShowWizardWindow](#ShowWizardWindow)|Mit dieser Methode können Sie einen benutzerdefinierten Editor innerhalb eines Dialogfelds anzeigen, das die Navigationsschaltflächen **Weiter** und **Zurück** enthält.|  

######  <a name="ShowMessageBox"></a> ShowMessageBox  
 Diese Methode zeigt ein Meldungsfeld an, bei dem es sich um ein untergeordnetes Element des benutzerdefinierten Editors für Assistentenseiten handelt. Dieses Mitglied ist überladen: Tabelle 73 enthält eine Liste der Mitglieder mitsamt einer Kurzbeschreibung für jedes Mitglied. Vollständige Informationen zu den einzelnen Mitgliedern (einschließlich Syntax, Nutzung und Beispiele) finden Sie im Abschnitt zu den einzelnen Mitgliedern.  

### <a name="table-73-overloaded-members-for-the-showmessagbox-method"></a>Tabelle 73. Überladene Mitglieder der Methode „ShowMessagBox“  

|Mitglied|Beschreibung|  
|-|-|  
|[ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)|Zeigt ein Meldungsfeld mit einem Symbol und der Schaltfläche **OK** an|  
|[ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)|Zeigt ein Meldungsfeld mit einem Symbol und verschiedene mögliche Kombinationen aus Schaltflächen an|  
|[ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|Zeigt ein Meldungsfeld an, das Informationen zu einer Ausnahme und die Schaltfläche **OK** enthält|  

######  <a name="ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon"></a> ShowMessageBox(String message, String caption, MessageBoxImage icon)  

```  
void ShowMessageBox(String message, String caption, MessageBoxImage icon);  
```  

 Diese Methode zeigt ein Meldungsfeld mit der Schaltfläche **OK** an. Siehe Tabelle 74.  

### <a name="table-74-parameters-for-the-showmessageboxstring-message-string-caption-messageboximage-icon-method"></a>Tabelle 74. Parameter für die Methode „ShowMessageBox(String message, String caption, MessageBoxImage icon)“  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**message**|Die im Inhaltsbereich des Meldungsfelds anzuzeigende Meldung|  
|**caption**|Der in der Titelleiste des Dialogfelds anzuzeigende Text|  
|**icon**|Die Art des im Meldungsfeld anzuzeigenden Symbols|  

######  <a name="ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon"></a> ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)  

```  
MessageBoxResult ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon);  
```  

 Diese Methode zeigt ein Meldungsfeld mit den anzuzeigenden Schaltflächen und den Berichten an, bei denen Sie auf die Schaltfläche geklickt haben. Siehe Tabelle 75.  

### <a name="table-75-parameters-for-the-showmessageboxstring-message-string-caption-messageboxbutton-button-messageboximage-icon-method"></a>Tabelle 75. Parameter für die Methode „ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)“  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**message**|Die im Inhaltsbereich des Meldungsfelds anzuzeigende Meldung|  
|**caption**|Der in der Titelleiste des Dialogfelds anzuzeigende Text|  
|**button**|Die anzuzeigenden Schaltflächen|  
|**icon**|Die Art des im Meldungsfeld anzuzeigenden Symbols|  

######  <a name="ShowMessageBox_Exception_exception"></a> ShowMessageBox(Exception exception)  

```  
void ShowMessageBox(Exception exception);  
```  

 Diese Methode zeigt ein Meldungsfeld an, das Informationen zu einer Ausnahme angibt. Dieses Meldungsfeld verfügt über eine einzige Schaltfläche: die Schaltfläche **OK**. Siehe Tabelle 76.  

### <a name="table-76-parameters-for-the-showmessageboxexception-exception-method"></a>Tabelle 76. Parameter für die Methode „ShowMessageBox(Exception exception)“  

|**Parameter**|**Beschreibung**|  
|-|-|  
|**exception**|Die Ausnahme, die Sie melden möchten (Im Dialogfeld wird **exception.Message** als Inhalt verwendet.)|  

######  <a name="ShowDialogWindow"></a> ShowDialogWindow  

```  
void ShowDialogWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 Diese Methode erstellt ein neues Dialogfeld, das den von Ihnen im Parameter **ViewType** angegebenen Text enthält. Der Designer des UDI-Assistenten erstellt eine neue Instanz dieses Typs und umschließt diese in einem Dialogfeld, das die Schaltflächen **OK** und **Abbrechen** enthält.  

 Sie übergeben über den Parameter „DialogPayload“ Daten an Ihr Steuerelement. Die **SampleEditor**-Lösung im SDK-Verzeichnis enthält ein Beispiel zur Verwendung dieser Funktion.  

######  <a name="ShowWizardWindow"></a> ShowWizardWindow  

```  
void ShowWizardWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 Mit dieser Methode können Sie einen benutzerdefinierten Editor innerhalb eines Dialogfelds anzeigen, das die Navigationsschaltflächen **Weiter** und **Zurück** enthält. Microsoft hat für die Verwendung dieser Methode kein Beispiel bereitgestellt.  

###  <a name="UDIWizardConfigurationFileSchemaReference"></a> Verweis auf Konfigurationsdateischema des UDI-Assistenten  
 Diese Datei wird vom UDI-Assistenten verwendet und vom Designer des UDI-Assistenten konfiguriert. Diese Datei dient zum Konfigurieren von:  

-   Im UDI-Assistenten angezeigten Assistentenseiten  

-   Der Sequenz der Assistentenseiten im UDI-Assistenten  

-   Einstellungen für die Felder auf den einzelnen Assistentenseiten  

-   Verfügbaren StageGroups im Designer des UDI-Assistenten  

-   Verfügbaren Stufen in den einzelnen Bereitstellungs-Assistenten im Designer des UDI-Assistenten  

  In Tabelle 77 werden die Elemente in der Konfigurationsdatei des UDI-Assistenten mitsamt einer Beschreibung für jedes Element aufgelistet. Das **Wizard**-Element ist der Stammknoten für diesen Verweis.  

### <a name="table-77-elements-in-the-udi-wizard-configuration-file-and-their-descriptions"></a>Tabelle 77. Elemente in der Konfigurationsdatei des UDI-Assistenten mit zugehörigen Beschreibungen  

|**Elementname**|**Beschreibung**|  
|-|-|  
|[Data](#Data)|Gruppiert die einzelnen [DataItem](#DataItem)-Elemente in einem [Page](#Page)-Element und wird vom Attribut **Name** benannt.|  
|[DataItem](#DataItem)|Gruppiert die einzelnen [Setter]()-Elemente in einem [Page](#Page)-Element. Sie können hierarchische Daten erstellen, indem Sie mindestens ein [Data](#Data)-Element in einem [DataItem](#DataItem)-Element einschließen. Jedes **DataItem**-Element stellt ein einzelnes Element dar. So kann eine Liste der verfügbaren Laufwerke beispielsweise ein **DataItem**-Element für den Anzeigenamen und anderes **DataItem**-Element für den entsprechenden Laufwerkbuchstaben enthalten.|  
|[Standard](#Default)|Gibt einen Standardwert für das im übergeordneten [Feld](#Field)- oder [RadioGroup](#RadioGroup)-Element angegebene Feld an. Die Standardeinstellung ist auf den Wert festgelegt, der von diesem Element in Klammern gesetzt wird.|  
|[DLL](#DLL)|Gibt eine DLL an, die vom UDI-Assistenten und dem Designer des UDI-Assistenten geladen und auf die vom UDI-Assistenten und dem Designer des UDI-Assistenten verwiesen werden soll.|  
|[DLLs](#DLLs)|Gruppiert die einzelnen [DLL](#DLL)-Elemente.|  
|[Fehler](#Error)|Gibt einen möglichen Fehlercode an, den ein Task zurückgeben kann. Der Wert des Fehlercodes wird von dem **HRESULT** des Tasks zurückgegeben und von diesem Element eingeschlossen, damit genauere Informationen zum Fehler bereitgestellt werden können.|  
|[ExitCode](#ExitCode)|Gibt einen möglichen Exitcode für einen Task an. Bei Exitcodes handelt es sich um Rückgabecodes, die von dem Task erwartet werden. Erstellen Sie für jeden möglichen Exitcode ein **ExitCode**-Element. Andernfalls können Sie ein Sternchen (\*) im Attribut **Value** angeben, um Rückgabecodes zu verarbeiten, die nicht in anderen **ExitCode**-Elementen aufgeführt sind.|  
|[ExitCodes](#ExitCodes)|Gruppiert mehrere [ExitCode](#ExitCode)- und [Error](#Error)-Elemente für ein [Task](#Task)- oder **Error**-Element.|  
|[Field](#Field)|Gibt eine Instanz eines Steuerelements in einem [Page](#Page)-Element an, das zum Bereitstellen von Anpassungen mit XML verwendet wird. Nicht alle Steuerelemente ermöglichen Anpassungen mit XML. Dies ist nur bei Steuerelementen möglich, die das [Field](#Field)-Element verwenden.|  
|[Fields](#Fields)|Gruppiert die einzelnen [Field](#Field)-Elemente in einem [Page](#Page)-Element.|  
|[File](#File)|Gibt die Quelle und das Ziel für den Kopiervorgang einer Datei mithilfe des Tasktyps **Microsoft.Wizard.CopyFilesTask** an. Sie können einzelne **File**-Elemente einschließen, um mehrere Dateien in einen einzelnen Task zu kopieren.|  
|[Page](#Page)|Gibt eine Instanz einer Seite an und enthält sämtliche Konfigurationseinstellungen für diese Seite.|  
|[PageRef](#PageRef)|Gibt einen Verweis auf eine Instanz einer Seite an, die sich in einem [Stage](#Stage)-Element innerhalb eines [StageGroup](#StageGroup)-Elements befindet.|  
|[Pages](#Pages)|Gruppiert die einzelnen [Page](#Page)-Elemente.|  
|[RadioGroup](#RadioGroup)|Gibt eine Gruppe von Optionsfeldern in einem [Feld](#Field)-Element an.|  
|[StageGroup](#StageGroup)|Gibt eine Gruppe von mindestens einer Phase an.|  
|[StageGroups](#StageGroups)|Gruppiert mehrere Phasen innerhalb einer Konfigurationsdatei des UDI-Assistenten.|  
|[Setter]()|Gibt eine Eigenschafteneinstellung für den Wert einer Eigenschaft an, die in der Eigenschaft **Property** benannt wird.|  
|[Stage](#Stage)|Gibt eine Phase in einer [StageGroup](#StageGroup)an und enthält mindestens ein [PageRef](#PageRef)-Element.|  
|[Style](#Style)|Gruppiert die einzelnen [Setter]()-Elemente, die das Aussehen und Verhalten des UDI-Assistenten konfigurieren. Dazu zählt auch der Titel, der im oberen Bereich des Assistenten angezeigt wird, sowie das Bannerbild, das im UDI-Assistent angezeigt wird.|  
|[Task](#Task)|Gibt einen Task an, der auf der im übergeordneten [Page](#Page)-Element angegeben Seite ausgeführt werden soll.|  
|[Aufgaben](#Tasks)|Gruppiert mehrere Tasks für ein [Page](#Page)-Element.|  
|[Validator](#Validator)|Gibt ein Validierungssteuerelement für das Feldsteuerelement an, das im übergeordneten [Field](#Field)-Element angegeben wird.|  
|[Wizard](#Wizard)|Gibt den Stamm für alle anderen Elemente an.|  

####  <a name="Data"></a> Data  
 Dieses Element gruppiert die einzelnen [DataItem](#DataItem)-Elemente in einem [Page](#Page)-Element und wird vom Attribut **Name** benannt.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 78 finden Sie weitere Informationen zum [Data](#Data)-Element.  

### <a name="table-78-data-element-information"></a>Tabelle 78. Informationen zum Data-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|0 (null) oder mehrere Vorkommen innerhalb der einzelnen [Page](#Page)-Elemente (Dieses Element ist optional.)|  
|Übergeordnete Elemente|**Page**, **DataItem**|  
|Inhalt|**DataItem**, **Setter**|  

##### <a name="element-attributes"></a>Elementattribute  
 In Tabelle 79 werden die Attribute des [Data](#Data)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-79-attributes-and-corresponding-values-for-the-data-element"></a>Tabelle 79. Attribute und zugehörige Werte des Data-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**Name**|Gibt den Namen des [Data](#Data)-Elements an|  

##### <a name="remarks"></a>Hinweise  
 Das Attribut **Name** lässt Code zum Abrufen eines bestimmten Datensatzes zu.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="DataItem"></a> DataItem  
 Dieses Element gruppiert die einzelnen [Setter]()-Elemente innerhalb eines [Page](#Page)-Elements. Sie können hierarchische Daten erstellen, indem Sie mindestens ein [Data](#Data)-Element in einem [DataItem](#DataItem)-Element einschließen. Jedes **DataItem**-Element stellt ein einzelnes Element dar. So kann eine Liste der verfügbaren Laufwerke beispielsweise ein **DataItem**-Element für den Anzeigenamen und anderes **DataItem**-Element für den entsprechenden Laufwerkbuchstaben enthalten.  

##### <a name="element-information"></a>Elementinformationen  
 In Tabelle 80 finden Sie weitere Informationen zum [DataItem](#DataItem)-Element.  

### <a name="table-80-dataitem-element-information"></a>Tabelle 80. Informationen zum DataItem-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|0 (null) oder mehrere Vorkommen innerhalb der einzelnen [Data](#Data)-Elemente (Dieses Element ist optional.)|  
|Übergeordnete Elemente|**Data**|  
|Inhalt|**Data**, **Setter**|  

##### <a name="element-attributes"></a>Elementattribute  
 Dieses Element besitzt keine Attribute.  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

#### <a name="default"></a>Standard  
 Dieses Element gibt einen Standardwert für das im übergeordneten [Field](#Field)- oder [RadioGroup](#RadioGroup)-Element angegebene Feld an. Die Standardeinstellung ist auf den Wert festgelegt, der von diesem Element in Klammern gesetzt wird.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 81 finden Sie weitere Informationen zum [Default](#Default)-Element.  

### <a name="table-81-default-element-information"></a>Tabelle 81. Informationen zum Default-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse |0 (null) oder mehrere Vorkommen innerhalb eines [Field](#Field)- oder [RadioGroup](#RadioGroup)-Elements (Dieses Element ist optional.)|  
|Übergeordnete Elemente|**Field**, **RadioGroup**|  
|Inhalt|Kann beliebiger wohlgeformter XML-Inhalt sein, ist jedoch in der Regel Standardtext|  

##### <a name="element-attributes"></a>Elementattribute  
 Dieses Element besitzt keine Attribute.  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird der Standardwert für das Feld **TimeZone** auf „Pacific Normalzeit“ festgelegt:  

```  
<Field Name="TimeZone" Enabled="true" VarName="OSDTimeZone" Summary="Time Zone:">  
  <Default>Pacific Standard Time</Default>  
```  

####  <a name="DLL"></a> DLL  
 Dieses Element gibt eine DLL an, die vom UDI-Assistenten und vom Designer des UDI-Assistenten geladen und auf die vom UDI-Assistenten und vom Designer des UDI-Assistenten verwiesen werden soll.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 82 finden Sie weitere Informationen zum [DLL](#DLL)-Element.  

### <a name="table-82-dll-element-information"></a>Tabelle 82. Informationen zum DLL-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Mindestens ein Vorkommen im [DLLs](#DLLs)-Element|  
|Übergeordnetes Element|**DLLs**|  
|Inhalt|Für dieses Element ist kein Inhalt zulässig|  

##### <a name="element-attributes"></a>Elementattribute  
 In Tabelle 83 werden die Attribute des [DLL](#DLL)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-83-attributes-and-corresponding-values-for-the-dll-element"></a>Tabelle 83. Attribute und zugehörige Werte des DLL-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|Name|Gibt den Namen der DLL an, auf die vom UDI-Assistenten und vom Designer des UDI-Assistenten verwiesen werden soll|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  

```  
<DLLs>  
  <DLL Name="OSDRefreshWizard.dll" />   
  <DLL Name="SharedPages.dll" />  
</DLLs>  
```  

####  <a name="DLLs"></a> DLLs  
 Dieses Element gruppiert die einzelnen [DLL](#DLL)-Elemente.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 84 finden Sie weitere Informationen zum [DLLs](#DLLs)-Element.  

### <a name="table-84-dlls-element-information"></a>Tabelle 84. Informationen zum DLLs-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Einem|  
|Übergeordnete Elemente|**Wizard**|  
|Inhalt|**DLL**|  

##### <a name="element-attributes"></a>Elementattribute  
 Dieses Element besitzt keine Attribute.  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  

```  
<DLLs>  
   <DLL Name="OSDRefreshWizard.dll" />  
   <DLL Name="SharedPages.dll" />   
</DLLs>  
```  

####  <a name="Error"></a> Fehler  
 Dieses Element gibt einen möglichen Fehlercode an, der von einem Task zurückgegeben werden kann. Der Wert des Fehlercodes wird vom **HRESULT** des Tasks zurückgegeben und eingeschlossen, damit genauere Informationen zum Fehler bereitgestellt werden können.  

##### <a name="element-information"></a>Elementinformationen  
 In Tabelle 85 finden Sie weitere Informationen zum [Error](#Error)-Element.  

### <a name="table-85-error-element-information"></a>Tabelle 85. Informationen zum Error-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|0 (null) oder mehrere Vorkommen innerhalb der einzelnen [ExitCode](#ExitCode)-Elemente (Dieses Element ist optional.)|  
|Übergeordnete Elemente|**ExitCodes**|  
|Inhalt|Wohlgeformte XML-Inhalte|  

##### <a name="element-attributes"></a>Elementattribute  
 In Tabelle 86 werden die Attribute des [Error](#Error)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

###  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**Status**|Gibt den Rückgabestatus eines Tasks an, in dem ein Fehler aufgetreten ist. Der Wert für dieses Attribut ist in der Regel auf „Fehler“ festgelegt. Dieser Wert wird auf der Assistentenseite des UDI-Assistenten in der Spalte **Status** angezeigt.|  
|**Text**|Gibt die Beschreibung zur Fehlerbedingung an, die in dem Task aufgetreten ist.|  
|**Typ**|Gibt an, ob dieses Element einen Fehler, eine Warnung oder einen Erfolg darstellt. Der in **Type** angegebene Wert muss innerhalb eines [ExitCode](#ExitCodes)-Elements eindeutig sein. Folgende Werte sind für dieses Element gültig:<br /><br /> -   **0:** Das Element stellt einen Erfolg dar.<br />-   **1:** Das Element stellt eine Warnung dar.<br />-   **–1:** Das Element stellt einen Fehler dar.|  
|**Wert**|Gibt den Wert des Codes an, den der Task als numerischen Wert zurückgegeben hat. Das Angeben des Werts für ein Sternchen (*) gibt den Standardwert für Rückgabecodes an, die nicht in anderen [Error](#Error)-Elementen aufgeführt sind.|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="ExitCode"></a> ExitCode  
 Dieses Element gibt einen möglichen Exitcode für einen Task an. Bei Exitcodes handelt es sich um Rückgabecodes, die der Task erwartet. Erstellen Sie für jeden möglichen Exitcode ein **ExitCode**-Element. Andernfalls können Sie ein Sternchen (\*) im Attribut **Value** angeben, um Rückgabecodes zu verarbeiten, die nicht in anderen **ExitCode**-Elementen aufgeführt sind.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 87 finden Sie weitere Informationen zum [ExitCode](#ExitCode)-Element.  

### <a name="table-87-exitcode-element-information"></a>Tabelle 87: Informationen zum ExitCode-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Nullmal (0) oder öfter innerhalb jedes [ExitCodes](#ExitCodes)-Elements (Dieses Element ist optional.)|  
|Übergeordnete Elemente|**ExitCodes**|  
|Inhalt|Mindestens ein [ExitCode](#ExitCode)-Element und null (0) oder mehr [Error](#Error)-Elemente|  

##### <a name="element-attributes"></a>Elementattribute  
In Tabelle 88 werden die Attribute des [ExitCode](#ExitCode)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-88-attributes-and-corresponding-values-for-the-exitcode-element"></a>Tabelle 88: Attribute und zugehörige Werte des ExitCode-Elements  

|**Attribut**|Beschreibung|  
|-|-|  
|**Status**|Gibt den Rückgabestatus eines Tasks an. Der Wert dieses Attributs wird in der **Status**-Spalte der entsprechenden Seite des Assistenten im UDI-Assistent angezeigt. Sie können jeden Wert für dieses Attribut verwenden, der für Ihren Task aussagekräftig ist. Folgende Werte werden üblicherweise für dieses Attribut verwendet:<br /><br /> – Erfolg<br />– Warnung<br />– Fehler|  
|**Text**|Gibt den beschreibenden Text für den Exitcode des Tasks an.|  
|**Typ**|Gibt an, ob dieses Element einen Fehler, eine Warnung oder einen Erfolg darstellt. Der in „type“ angegebene Wert muss innerhalb eines [ExitCode](#ExitCodes)-Elements eindeutig sein. Folgende Werte sind für dieses Element gültig:<br /><br /> -   **0:** Das Element stellt einen Erfolg dar.<br />-   **1:** Das Element stellt eine Warnung dar.<br />-   **–1:** Das Element stellt einen Fehler dar.|  
|**Wert**|Gibt den Wert des Codes an, den der Task als numerischen Wert zurückgegeben hat. Das Angeben des Werts für ein Sternchen (*) gibt den Standardwert für Rückgabecodes an, die nicht in anderen [ExitCode](#ExitCode)-Elementen aufgeführt sind.|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="ExitCodes"></a> ExitCodes  
 Dieses Element gruppiert mehrere [ExitCode](#ExitCode)- und [Error](#Error)-Elemente für ein [Task](#Task)- oder **Error**-Element.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 89 finden Sie weitere Informationen zum [ExitCodes](#ExitCodes)-Element.  

### <a name="table-89-exitcodes-element-information"></a>Tabelle 89: Informationen zum ExitCodes-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Einmal innerhalb jedes [Task](#Task)-Elements|  
|Übergeordnete Elemente|**Task**|  
|Inhalt|**Error**, **ExitCode**|  

##### <a name="element-attributes"></a>Elementattribute  
 Dieses Element besitzt keine Attribute.  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="Field"></a> Field  
 Dieses Element gibt eine Instanz eines Steuerelements in einem [Page](#Page)-Element an, das zum Bereitstellen von Anpassungen mit XML verwendet wird. Nicht alle Steuerelemente ermöglichen Anpassungen mit XML. Dies ist nur bei Steuerelementen möglich, die das [Field](#Field)-Element verwenden.  

##### <a name="element-information"></a>Elementinformationen  
 In Tabelle 90 finden Sie weitere Informationen zum [Field](#Field)-Element.  

### <a name="table-90-field-element-information"></a>Tabelle 90: Informationen zum Field-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Nullmal (0) oder öfter innerhalb jedes [Field](#Field)-Elements (Dieses Element ist optional.)|  
|Übergeordnete Elemente|**Fields**|  
|Inhalt|**Default**, **Validator**|  

##### <a name="element-attributes"></a>Elementattribute  
In Tabelle 91 werden die Attribute des [Field](#Field)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-91-attributes-and-corresponding-values-for-the-field-element"></a>Tabelle 91: Attribute und zugehörige Werte des Field-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**Enabled**|Gibt an, ob das Feld für Benutzereingaben aktiviert ist (Das Element kann auf TRUE oder FALSE festgelegt ist.)|  
|**Name**|Gibt den Namen des Felds an|  
|**Zusammenfassung**|Gibt den beschreibenden Text an, der auf der Seite **Zusammenfassung** des Assistenten für den Wert angezeigt wird, den dieses Feld festlegt|  
|**VarName**|Gibt den Namen der Tasksequenzvariablen an, der mithilfe dieses Felds im übergeordneten Element [Field](#Field) gelesen oder konfiguriert wird|  

##### <a name="remarks"></a>Hinweise  
 Dieses Element kann null (0) oder mehr [Default](#Default)-Elemente und null (0) oder mehr [Validator](#Validator)-Elemente enthalten.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="Fields"></a> Fields  
 Dieses Element gruppiert die einzelnen [Field](#Field)-Elemente innerhalb eines [Page](#Page)-Elements.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 92 finden Sie weitere Informationen zum [Fields](#Fields)-Element.  

### <a name="table-92-fields-element-information"></a>Tabelle 92: Informationen zum Fields-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|0 (null) oder mehrere Vorkommen innerhalb der einzelnen [Page](#Page)-Elemente (Dieses Element ist optional.)|  
|Übergeordnete Elemente|**Page**|  
|Inhalt|**Field**, **RadioGroup**|  

##### <a name="element-attributes"></a>Elementattribute  
 Dieses Element besitzt keine Attribute.  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="File"></a> File  
 Dieses Element gibt die Quelle und das Ziel für den Kopiervorgang einer Datei mithilfe des Tasktyps **Microsoft.Wizard.CopyFilesTask** an. Sie können einzelne [File](#File)-Elemente einschließen, um mehrere Dateien in einen einzelnen Task zu kopieren.  

##### <a name="element-information"></a>Elementinformationen  
 In Tabelle 93 finden Sie weitere Informationen zum [File](#File)-Element.  

### <a name="table-93-file-element-information"></a>Tabelle 93: Informationen zum File-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Mindestens einmal für jeden Task, der den Tasktyp **Microsoft.Wizard.CopyFilesTask** aufweist|  
|Übergeordnete Elemente|**Task**|  
|Inhalt|Keine|  

##### <a name="element-attributes"></a>Elementattribute  
 In Tabelle 94 werden die Attribute des [File](#File)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-94-attributes-and-corresponding-values-for-the-file-element"></a>Tabelle 94: Attribute und zugehörige Werte des File-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**Dest**|Gibt den vollqualifizierten oder relativen Pfad zum Zielordner der Datei an, der im **Source**-Attribut angegeben ist. Umgebungsvariablen sind als Teil des Pfads zulässig.|  
|**Quelle**|Gibt den vollqualifizierten oder relativen Pfad zur Quelldatei an, die der Tasktyp **Microsoft.Wizard.CopyFilesTask** kopiert. Dieses Attribut unterstützt Platzhalterzeichen, sodass mehrere Dateien mithilfe eines einzelnen [File](#File)-Elements kopiert werden können. Umgebungsvariablen sind als Teil des Pfads zulässig.|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="PageElement"></a> Page  
 Dieses Element enthält eine Instanz einer Seite sowie alle Konfigurationseinstellungen für diese Seite.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 95 finden Sie weitere Informationen zum [Page](#Page)-Element.  

### <a name="table-95-page-element-information"></a>Tabelle 95: Informationen zum Page-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Mindestens einmal in jedem [Pages](#Pages)-Element|  
|Übergeordnete Elemente|**Pages**|  
|Inhalt|**Data**, **Fields**, **Setter**, **Tasks**|  

##### <a name="element-attributes"></a>Elementattribute  
In Tabelle 96 werden die Attribute des [Page](#Page)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-96-attributes-and-corresponding-values-for-the-page-element"></a>Tabelle 96: Attribute und zugehörige Werte des Page-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**DisplayName**|Gibt den benutzerfreundlichen Namen der Seite des Assistenten an, der im Designer des UDI-Assistenten angezeigt wird. Dieser Name ist in der Regel beschreibender als das **Name**-Attribut.|  
|**Name**|Gibt den Namen der Seite des Assistenten an, der im Designer des UDI-Assistenten angezeigt wird.|  
|**Typ**|Gibt den Typ der Seite des Assistenten an, die direkt mit einer bestimmten Seite des Assistenten innerhalb einer DLL verknüpft ist.|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="PageRef"></a> PageRef  
 Dieses Element gibt einen Verweis auf eine Instanz eine Seite an, die sich innerhalb eines [Stage](#Stage)-Elements innerhalb eines [StageGroup](#StageGroup)-Elements befindet.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 97 finden Sie weitere Informationen zum [PageRef](#PageRef)-Element.  

### <a name="table-97-pageref-element-information"></a>Tabelle 97: Informationen zum PageRef-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Mindestens einmal innerhalb eines [Stage](#Stage)-Elements|  
|Übergeordnete Elemente|**Stage**|  
|Inhalt|Keine|  

##### <a name="element-attributes"></a>Elementattribute  
In Tabelle 98 werden die Attribute des [PageRef](#PageRef)-Elements mitsamt einer Beschreibung dafür aufgelistet.  

### <a name="table-98-attributes-and-corresponding-values-for-the-pageref-element"></a>Tabelle 98: Attribute und zugehörige Werte des PageRef-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**Page**|Gibt die Instanz einer Seite an, die sich innerhalb eines [Stage](#Stage)-Elements innerhalb eines [StageGroup](#StageGroup)-Elements befindet. Legen Sie diesen Wert für das Name-Attribut eines [Page](#Page)-Elements fest.|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="Pages"></a> Pages  
 Dieses Element gruppiert die einzelnen [Page](#Page)-Elemente.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 99 finden Sie weitere Informationen zum [Pages](#Pages)-Element.  

### <a name="table-99-pages-element-information"></a>Tabelle 99: Informationen zum Pages-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Einem|  
|Übergeordnete Elemente|**Wizard**|  
|Inhalt|**Page**|  

##### <a name="element-attributes"></a>Elementattribute  
 Dieses Element besitzt keine Attribute.  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  

```  
<Pages>  
   + <Page Name="WelcomePage" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="ConfigScanPage" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="ConfigScanBareMetal" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="RebootPage" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
   + <Page Name="WelcomePageReplace" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="VolumePage" DisplayName="Volume" Type="Microsoft.OSDRefresh.VolumePage">  
   + <Page Name="UserRestorePage" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ComputerPage" DisplayName="New Computer Details" Type="Microsoft.OSDRefresh.ComputerPage">  
   + <Page Name="AdminAccounts" DisplayName="Administrator Password" Type="Microsoft.SharedPages.AdminAccountsPage">  
   + <Page Name="UDAPage" DisplayName="User Device Affinity" Type="Microsoft.OSDRefresh.UDAPage">  
   + <Page Name="LanguagePage" DisplayName="Language" Type="Microsoft.OSDRefresh.LanguagePage">  
   + <Page Name="ApplicationPage" DisplayName="Install Programs" Type="Microsoft.OSDRefresh.ApplicationPage">  
     <Page Name="SummaryPage" DisplayName="Summary" Type="Microsoft.Shared.SummaryPage" />   
   + <Page Name="UserCapturePageOldPC" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ProgressPage" DisplayName="Capture Data" Type="Microsoft.OSDRefresh.ProgressPage">  
   + <Page Name="RebootAfterCapture" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
</Pages>  
```  

####  <a name="RadioGroup"></a> RadioGroup  
 Dieses Element gibt die Optionsfelder innerhalb eines [Field](#Field)-Elements an.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 100 finden Sie weitere Informationen zum [RadioGroup](#RadioGroup)-Element.  

### <a name="table-100-radiogroup-element-information"></a>Tabelle 100: Informationen zum RadioGroup-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Nullmal (0) oder öfter innerhalb eines [Field](#Fields)-Elements (Dieses Element ist optional.)|  
|Übergeordnete Elemente|**Fields**|  
|Inhalt|**Standard**|  

##### <a name="element-attributes"></a>Elementattribute  
 In Tabelle 101 werden die Attribute des [RadioGroup](#RadioGroup)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-101-attributes-and-corresponding-values-for-the-radiogroup-element"></a>Tabelle 101: Attribute und zugehörige Werte des RadioGroup-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**Locked**|Gibt an, ob die Optionsfelder für Benutzereingaben aktiviert sind. Das Attribut kann auf Folgendes festgelegt werden:<br /><br /> -   **TRUE:** Gibt an, dass die Optionsfelder deaktiviert sind und Benutzer diese in der Gruppe nicht auswählen können.<br />-   **FALSE:** Gibt an, dass die Optionsfelder aktiviert sind und Benutzer diese in der Gruppe auswählen können.|  
|**Name**|Gibt den Namen der Gruppe für Optionsfelder an.|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="StageGroup"></a> StageGroup  
 Dieses Element gibt eine Gruppe für die Bereitstellungsphase an.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 102 finden Sie weitere Informationen zum [StageGroup](#StageGroup)-Element.  

### <a name="table-102-stagegroup-element-information"></a>Tabelle 102: Informationen zum StageGroup-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Mindestens einmal innerhalb eines [StageGroups](#StageGroups)-Elements|  
|Übergeordnete Elemente|**StageGroups**|  
|Inhalt|**Stage**|  

##### <a name="element-attributes"></a>Elementattribute  
 In Tabelle 103 werden die Attribute des [StageGroup](#StageGroup)-Elements mitsamt einer Beschreibung der Attribute aufgelistet.  

### <a name="table-103-attributes-and-corresponding-values-for-the-stagegroup-element"></a>Tabelle 103: Attribute und zugehörige Werte des StageGroup-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**DisplayName**|Gibt den benutzerfreundlichen Namen des StageGroup-Elements an, der im Designer des UDI-Assistenten angezeigt wird. Dieser Name ist in der Regel beschreibender als das **Name**-Attribut.|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="StageGroups"></a> StageGroups  
 Dieses Element gruppiert mehrere StageGroup-Elemente innerhalb einer Konfigurationsdatei des UDI-Assistenten.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 104 finden Sie weitere Informationen zum [StageGroups](#StageGroups)-Element.  

### <a name="table-104-stagegroups-element-information"></a>Tabelle 104: Informationen zum StageGroups-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Null (0) oder mehr innerhalb eines [Wizard](#Wizard)-Elements|  
|Übergeordnete Elemente|**Wizard**|  
|Inhalt|**StageGroup**|  

##### <a name="element-attributes"></a>Elementattribute  
 Dieses Element besitzt keine Attribute.  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="Setter"></a> Setter  
 Dieses Element gibt eine Einstellung für den Wert einer Eigenschaft an, die in der **Property**-Eigenschaft benannt wird.  

##### <a name="element-information"></a>Elementinformationen  
 In Tabelle 105 finden Sie weitere Informationen zum [Setter]()-Element.  

### <a name="table-105-setter-element-information"></a>Tabelle 105: Informationen zum Setter-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Nullmal (0) oder öfter innerhalb jedes übergeordneten Elements (Dieses Element ist optional.)|  
|Übergeordnete Elemente|**Data**, **DataItem**, **Page**, **Style**, **Task**, **Validator**|  
|Inhalt|Enthält einen Zeichenfolgenwert im **Property**-Attribut|  

##### <a name="element-attributes"></a>Elementattribute  
In Tabelle 106 werden die Attribute des [Setter]()-Elements mitsamt einer Beschreibung dafür aufgelistet.  

### <a name="table-106-attributes-and-corresponding-values-for-the-setter-element"></a>Tabelle 106: Attribute und zugehörige Werte des Setter-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**Eigenschaft**|Gibt den Eigenschaftsname an, der festgelegt wird. Der Eigenschaftsname wird auf den Wert festgelegt, der in Klammern hinter dem Attribut steht.|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

#### <a name="stage"></a>Stadium  
 Dieses Element gibt ein [Stage](#Stage)-Element innerhalb eines [StageGroup](#StageGroup)-Elements an und enthält mindestens ein [PageRef](#PageRef)-Element.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 107 finden Sie weitere Informationen zum [Stage](#Stage)-Element.  

### <a name="table-107-stage-element-information"></a>Tabelle 107: Informationen zum Stage-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Mindestens einmal innerhalb eines [StageGroup](#StageGroup)-Elements|  
|Übergeordnete Elemente|**StageGroup**|  
|Inhalt|**PageRef**|  

##### <a name="element-attributes"></a>Elementattribute  
In Tabelle 108 werden die Attribute des [Stage](#Stage)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-108-attributes-and-corresponding-values-for-the-stage-element"></a>Table 108: Attribute und zugehörige Werte des Stage-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**DisplayName**|Gibt den benutzerfreundlichen Namen der Seite des Assistenten an, der im Designer des UDI-Assistenten angezeigt wird. Dieser Name ist in der Regel beschreibender als das **Name**-Attribut.|  
|**Name**|Gibt den Namen des Stage-Elements an. Der Wert dieses Element wird verwendet, wenn der UDI-Assistent mit dem Befehlszeilenparameter **/stage: name** gestartet wird.|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="Style"></a> Style  
 Dieses Element gruppiert die einzelnen [Setter]()-Elemente, die das Aussehen und Verhalten des UDI-Assistenten konfigurieren. Dazu zählt auch der Titel, der im oberen Bereich des Assistenten angezeigt wird sowie das Bannerbild, das im UDI-Assistent angezeigt wird.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 109 finden Sie weitere Informationen zum Style-Element.  

### <a name="table-109-style-element-information"></a>Tabelle 109: Informationen zum Style-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Einem|  
|Übergeordnete Elemente|**Wizard**|  
|Inhalt|**Setter**|  

##### <a name="element-attributes"></a>Elementattribute  
 Dieses Element besitzt keine Attribute.  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  

```  
<Style>  
  <Setter Property="bannerFilename">UDI_Wizard_Banner.bmp</Setter>   
  <Setter Property="title">Operating System Deployment (OSD) Refresh Wizard</Setter>   
</Style>  
```  

####  <a name="TaskElement"></a> Task  
 Dieses Element gibt einen Task an, der auf der Seite ausgeführt werden soll, die im übergeordneten [Page](#Page)-Element angegeben wird.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 110 finden Sie weitere Informationen zum [Task](#Task)-Element.  

### <a name="table-110-task-element-information"></a>Tabelle 110: Informationen zum Task-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Mindestens einmal innerhalb eines [Tasks](#Tasks)-Elements|  
|Übergeordnete Elemente|**Aufgaben**|  
|Inhalt|**ExitCodes**, **File**, **Setter**|  

##### <a name="element-attributes"></a>Elementattribute  
In Tabelle 111 werden die Attribute des [Task](#Task)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-111-attributes-and-corresponding-values-for-the-task-element"></a>Tabelle 111: Attribute und zugehörige Werte des Task-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**DependsOn**|Gibt an, ob ein Task von einem anderen Task abhängig ist. Der Wert dieses Attributs wird auf das **Name**-Attribut eines anderen [Task](#Task)-Elements festgelegt. **Hinweis:** Dieses Attribut kann nicht mithilfe des Designers für den UDI-Assistenten konfiguriert werden. Sie können dieses Attribut jedoch manuell zu einem [Task](#Task)-Element hinzufügen, indem Sie die XML-Datei direkt bearbeiten.|  
|**DisplayName**|Gibt den benutzerfreundlichen Namen des Tasks an, der im Designer des UDI-Assistenten angezeigt wird. Dieser Name ist in der Regel beschreibender als das **Name**-Attribut.|  
|**Name**|Gibt den Namen des Tasks an. Dieser Name muss eindeutig sein.|  
|Geben Sie|Gibt den Tasktyp des Tasks an, der ausgeführt werden soll. Dieser wird in der DLL definiert, die den Task enthält.|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="Tasks"></a> Tasks  
 Dieses Element gruppiert mehrere Tasks für ein [Page](#Page)-Element.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 112 finden Sie weitere Informationen zum [Tasks](#Tasks)-Element.  

### <a name="table-112-tasks-element-information"></a>Tabelle 112: Informationen zum Tasks-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Nullmal (0) oder einmal innerhalb jedes [Page](#Page)-Elements (Dieses Element ist optional.)|  
|Übergeordnete Elemente|**Page**|  
|Inhalt|**Task**|  

##### <a name="element-attributes"></a>Elementattribute  
In Tabelle 113 werden die Attribute des [Tasks](#Tasks)-Elements mitsamt einer Beschreibung für jedes Element aufgelistet.  

### <a name="table-113-attributes-and-corresponding-values-for-the-tasks-element"></a>Tabelle 113: Attribute und zugehörige Werte des Tasks-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|**NameTitle**|Gibt die Beschriftung an, die im oberen Bereich der Spalte angezeigt wird, die den Namen des Tasks auf der entsprechenden Seite des Assistenten enthält.|  
|**StatusTitle**|Gibt die Beschriftung an, die im oberen Bereich der Spalte angezeigt wird, die den Status des Tasks auf der entsprechenden Seite des Assistenten enthält.|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="ValidatorElement"></a> Validator  
 Dieses Element gibt ein Validierungssteuerelement für das Feldsteuerelement an, das im übergeordneten [Field](#Field)-Element angegeben wird.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 114 finden Sie weitere Informationen zum [Validator](#Validator)-Element.  

### <a name="table-114-validator-element-information"></a>Tabelle 114: Informationen zum Validator-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Null (0) oder mehr innerhalb eines [Field](#Field)-Elements|  
|Übergeordnete Elemente|**Field**|  
|Inhalt|**Setter**|  

##### <a name="element-attributes"></a>Elementattribute  
In Tabelle 115 werden die Attribute des [Validator](#Validator)-Elements mitsamt einer Beschreibung dafür aufgelistet.  

### <a name="table-115-attributes-and-corresponding-values-for-the-validator-element"></a>Tabelle 115: Attribute und zugehörige Werte des Validator-Elements  

|**Attribut**|**Beschreibung**|  
|-|-|  
|Geben Sie|Gibt den Typ des Validierungssteuerelements an. Dieser wird in der DLL definiert, die das Validierungssteuerelement enthält|  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  
 Keine.  

####  <a name="Wizard"></a> Wizard  
 Dieses Element gibt den Stamm für alle anderen Elemente an.  

##### <a name="element-information"></a>Elementinformationen  
In Tabelle 116 finden Sie weitere Informationen zum [Wizard](#Wizard)-Element.  

### <a name="table-116-wizard-element-information"></a>Tabelle 116: Informationen zum Wizard-Element  

|**Attribut**|**Wert**|  
|-|-|  
|Anzahl der Vorkommnisse|Einem|  
|Übergeordnete Elemente|Keine|  
|Inhalt|**DLLs**, **Pages**, **StageGroups**, **Style**|  

##### <a name="element-attributes"></a>Elementattribute  
 Dieses Element besitzt keine Attribute.  

##### <a name="remarks"></a>Hinweise  
 Keine.  

##### <a name="example"></a>Beispiel  

```  
<Wizard>  
   + <DLLs>  
   + <Style>  
   + <Pages>  
   + <StageGroups>  
</Wizard>  
```
