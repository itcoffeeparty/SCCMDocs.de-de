---
title: 'Verwalten von Startabbildern (Startimages) '
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie in Configuration Manager die Windows PE-Startimages verwalten, die Sie während der Bereitstellung von Betriebssystemen verwenden.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
caps.latest.revision: 23
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8fd5510ec00cdcf6829778b264b759588a2323cb
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>Verwalten von Startimages mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ein Startimage in Configuration Manager ist ein [Windows PE-Image](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (WinPE), das während einer Betriebssystembereitstellung verwendet wird. Mithilfe von Startimages wird ein Computer in WinPE gestartet. Dieses minimale Betriebssystem enthält begrenzte Komponenten und Dienste. Configuration Manager verwendet WinPE zur Vorbereitung des Zielcomputers für die Windows-Installation. Gehen Sie wie in den folgenden Abschnitten beschrieben vor, um Startimages zu verwalten:

## <a name="BKMK_BootImageDefault"></a> Standardstartimages
Configuration Manager stellt zwei Standardstartimages bereit: ein Startimage zur Unterstützung von x86-Plattformen und eines zur Unterstützung von x64-Plattformen. Diese Images sind hier gespeichert: \\\\*Servername*>\SMS_<*Standortcode*>\osd\boot\\<*x64*> oder <*i386*>. Die Standardstartimages werden je nach der von Ihnen ausgeführten Aktion aktualisiert oder neu generiert.

Betrachten Sie die folgenden Verhaltensweisen für die Aktionen, die für die standardmäßigen Startimages beschrieben werden:
- Die Quellentreiberobjekte müssen gültig sein. Diese Objekte enthalten die Treiberquellendateien. Wenn die Objekte nicht gültig sind, fügt der Standort die Treiber nicht zu den Startimages hinzu.
- Startimages, die nicht auf den standardmäßigen Startimages basieren, werden nicht geändert, selbst wenn sie die gleiche Version von Windows PE verwenden.
- Verteilen Sie die geänderten Startimages neu auf Verteilungspunkte.
- Erstellen Sie alle Medien neu, die die geänderten Startimages verwenden.
- Wenn die benutzerdefinierten oder Standardstartimages nicht automatisch aktualisiert werden sollen, speichern Sie sie nicht am Standardspeicherort.

> [!NOTE]
> Das Ablaufprotokolltool von Configuration Manager (CMTrace) wird zu allen Startimages in der **Softwarebibliothek** hinzugefügt. Wenn Sie Windows PE aufgerufen haben, starten Sie das Tool, indem Sie über die Eingabeaufforderung **CMTrace** eingeben. Ab Version 1802 werden Sie beim Starten der Datei „cmtrace.exe“ in Windows PE nicht mehr aufgefordert, zu entscheiden, ob dieses Programm die Standardanzeige für Protokolldateien sein soll.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Verwenden Sie Updates und Wartungen, um die neueste Version des Configuration Manager zu installieren.
Wenn Sie die Windows ADK-Version (Assessment and Deployment Kit) ab Version 1702 upgraden und anschließend Updates und Wartung zum Installieren der neuesten Version von Configuration Manager verwenden, generiert der Standort die standardmäßigen Startimages neu. Dieses Update schließt die neue WinPE-Version des aktualisierten Windows ADK, die neue Version des Configuration Manager-Clients, Treiber, Anpassungen ein. Der Standort ändern keine benutzerdefinierte Startimages.

Vor Version 1702 aktualisiert Configuration Manager das vorhandene Startimage mit den Clientkomponenten, Treibern, Anpassungen. Es wird jedoch nicht die neueste WinPE-Version von Windows ADK verwendet. Ändern Sie das Startimage manuell, um die aktuelle Version des Windows ADK zu verwenden.

### <a name="upgrade-from-configuration-manager-2012-to-configuration-manager-current-branch-cb"></a>Aktualisieren von Configuration Manager 2012 auf Configuration Manager Current Branch (CB)
Wenn Sie mithilfe des Setupvorgangs für Configuration Manager 2012 ein Upgrade auf Configuration Manager CB durchführen, generiert der Standort die standardmäßigen Startimages neu. Dieses Update schließt die neue WinPE-Version des aktualisierten Windows ADK und die neue Version des Configuration Manager-Clients ein. Alle Anpassungen des Startimages bleiben unverändert. Der Standort ändern keine benutzerdefinierte Startimages.

### <a name="update-distribution-points-with-the-boot-image"></a>Aktualisieren von Verteilungspunkten mithilfe des Startabbilds
Wenn Sie die Aktion **Verteilungspunkte aktualisieren** aus dem Knoten **Startimages** in der Konsole verwenden, aktualisiert der Standort das Startimage des Ziels mit den Clientkomponenten, Treibern und Anpassungen.    

Ab Configuration Manager Version 1706 können Sie das Startimage mit der aktuellen Version von WinPE aus dem Installationsverzeichnis des Windows ADK neu laden. Auf der Seite **Allgemein** des Assistenten für das Update von Verteilungspunkten werden folgende Informationen bereitgestellt: 
 - Die auf dem Standortserver installierte Windows ADK
 - Die Windows ADK-Version von WinPE im Startimage
 - Die Version des Configuration Manager-Clients. Mithilfe dieser Informationen können Sie entscheiden, ob das Startimage erneut geladen werden soll. Der Knoten **Startimages** enthält auch eine neue Spalte für (**Clientversion**). In dieser Spalte können Sie die Configuration Manager-Clientversion in den einzelnen Startimages schnell anzeigen.    


##  <a name="BKMK_BootImageCustom"></a> Anpassen eines Startimages  
 Wenn ein Startimage auf der WinPE-Version der unterstützten Version des Windows ADK basiert, können Sie es über die Konsole anpassen oder [ändern](#BKMK_ModifyBootImages). Wenn ein Standort mit einer neuen Version aktualisiert wird und eine neue Version des Windows ADK installiert wird, werden benutzerdefinierte Startimages (die sich nicht im Standardspeicherort für Startimages befinden) nicht mit der neuen Version des Windows ADK aktualisiert. In diesem Fall können Sie die Startimages in der Configuration Manager-Konsole nicht anpassen. Diese funktionieren jedoch weiterhin wie vor dem Upgrade.  

 Wenn ein Startimage auf einer anderen Version des an einem Standort installierten Windows ADK basiert, müssen Sie die Startimages anpassen. Passen Sie diese Startimages mit einer anderen Methode an, wie z.B. mit dem Befehlszeilenprogramm DISM (Deployment Image Servicing and Management). DISM ist Bestandteil des Windows ADK. Weitere Informationen zu Startimages finden Sie unter [Anpassen von Startimages](customize-boot-images.md).  

##  <a name="BKMK_AddBootImages"></a> Hinzufügen eines Startimages  

 Bei einer Standortinstallation fügt Configuration Manager automatisch Startimages hinzu, die auf einer WinPE-Version aus der unterstützten Version von Windows ADK basieren. Abhängig von der Configuration Manager-Version können Sie möglicherweise Startimages hinzufügen, die auf einer anderen WinPE-Version aus der unterstützten Version von Windows ADK basieren. Es tritt ein Fehler auf, wenn Sie versuchen, ein Startimage hinzuzufügen, das eine nicht unterstützte Version von WinPE enthält. Die folgende Liste enthält die derzeit unterstützten Windows ADK- und Windows PE-Versionen: 

-   **Windows ADK-Version**  

     Windows ADK für Windows 10  

-   **Windows PE-Versionen für Startimages, die über die Configuration Manager-Konsole angepasst werden können**  

     Windows PE 10  

-   **Unterstützte Windows PE-Versionen für Startimages, die nicht über die Configuration Manager-Konsole angepasst werden können**  

     Windows PE 3.1<sup>1</sup> und Windows PE 5  

     <sup>1</sup> Sie können zu Configuration Manager nur dann ein Startimage hinzufügen, wenn es auf Windows PE 3.1 basiert. Führen Sie ein Upgrade von Windows AIK für Windows 7 (basierend auf Windows PE 3.0) mit der Ergänzung zu Windows AIK für Windows 7 SP1 (basierend auf Windows PE 3.1) durch. Laden Sie die Ergänzung zu Windows AIK für Windows 7 SP1 aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188)herunter.  

     Verwenden Sie beispielsweise die Configuration Manager-Konsole, um Startimages, die auf Windows PE 10 basieren, aus dem Windows ADK für Windows 10 anzupassen. Passen Sie ein Startimage, das auf Windows PE 5 basiert, mithilfe der Version von DISM von einem anderen Computer aus dem Windows ADK für Windows 8 an. Fügen Sie anschließend das benutzerdefinierte Startimage zur Configuration Manager-Konsole hinzu. Weitere Informationen zu Startimages finden Sie unter [Anpassen von Startimages](customize-boot-images.md).

 Gehen Sie wie folgt vor, um ein Startabbild manuell hinzuzufügen.  

#### <a name="to-add-a-boot-image"></a>So fügen Sie ein Startabbild hinzu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Startabbilder**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Startabbild hinzufügen** , um den Assistenten zum Hinzufügen von Startabbildern zu starten.  

4.  Geben Sie auf der Seite **Datenquelle** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

    -   Geben Sie im Feld **Pfad** den Pfad der Startabbilddatei (WIM-Datei) an.  

         Der angegebene Pfad muss ein gültiger Netzwerkpfad im UNC-Format sein. Zum Beispiel: \\\\<*Servername*\\<*Freigabename*>\\<*Startimagename*>.wim.  

    -   Wählen Sie das Startabbild in der Dropdownliste **Startabbild** aus. Wenn die WIM-Datei mehrere Startabbilder enthält, wählen Sie das gewünschte Abbild aus.  

5.  Geben Sie auf der Seite **Allgemein**  die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

    -   Geben Sie im Feld **Name** einen eindeutigen Namen für das Startabbild an.  

    -   Geben Sie im Feld **Version** eine Versionsnummer für das Startabbild an.  

    -   Geben Sie im Feld **Kommentar** anhand einer kurzen Beschreibung an, wie das Startabbild verwendet werden soll.  

6.  Schließen Sie den Assistenten ab.  

 Das Startimage wird jetzt im Knoten **Startimage** der Configuration Manager-Konsole aufgeführt. Bevor das Startimage für die Bereitstellung eines Betriebssystems verwendet werden kann, müssen Sie dieses an Verteilungspunkte verteilen. 

> [!NOTE]  
>  Im Knoten **Startimage** der Konsole, wird in der Spalte **Größe (KB)** die dekomprimierte Größe der einzelnen Startimages angezeigt. Wenn der Standort über das Netzwerk ein Startimage sendet, sendet er eine komprimierte Kopie. Diese Kopie ist in der Regel kleiner als die in der Spalte **Größe (KB)** aufgeführte Größer.  

##  <a name="BKMK_DistributeBootImages"></a> Verteilen von Startimages an einen Verteilungspunkt  
 Startabbilder werden genau wie anderer Inhalt an Verteilungspunkte verteilt. In den meisten Fällen müssen Sie das Startabbild an mindestens einen Verteilungspunkt verteilen, bevor Sie ein Betriebssystem bereitstellen und bevor Sie Medien erstellen.   

> [!NOTE]  
> Wenn Sie PXE verwenden möchten, um ein Betriebssystem bereitzustellen, sollten Sie folgende Punkte beachten, bevor Sie das Startimage verteilen:  
> - Konfigurieren Sie mindestens einen Verteilungspunkt zum Akzeptieren von PXE-Anforderungen.  
> - Verteilen Sie sowohl ein x86- als auch ein x64-PXE-fähiges Startimage an mindestens einen PXE-fähigen Verteilungspunkt.  
> - Configuration Manager verteilt die Startimages an den Ordner **RemoteInstall** auf dem PXE-fähigen Verteilungspunkt.  
>   
> Weitere Informationen zur Verwendung von PXE zum Bereitstellen von Betriebssystemen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Die Schritte zum Verteilen eines Startabbilds finden Sie unter [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  

##  <a name="BKMK_ModifyBootImages"></a> Ändern eines Startimages  
 Sie können dem Abbild Gerätetreiber hinzufügen, Gerätetreiber aus dem Abbild entfernen oder die Eigenschaften des Startabbilds bearbeiten. Die Gerätetreiber, die Sie hinzufügen oder entfernen, können Treiber für Netzwerkkarten oder Massenspeichergeräte umfassen. Berücksichtigen Sie beim Ändern von Startabbildern die folgenden Faktoren:  

-   Importieren Sie die Gerätetreiber in den Gerätetreiberkatalog und aktivieren Sie diese dort, bevor Sie sie dem Startimage hinzufügen.  

-   Wenn Sie ein Startabbild ändern, wird keines der zugewiesenen Pakete geändert, auf die das Startabbild verweist.  

-   Nachdem Sie Änderungen an einem Startimage vorgenommen haben, müssen Sie dieses an den Verteilungspunkten **aktualisieren**, die bereits darüber verfügen. Durch diesen Prozess wird Clients die aktuelle Version des Startimages zur Verfügung gestellt. Weitere Informationen finden Sie unter [Manage content you have distributed](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage).  

 Gehen Sie wie folgt vor, um ein Startabbild zu ändern.  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>So ändern Sie die Eigenschaften eines Startabbilds  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Startabbilder**.  

3.  Wählen Sie das Startabbild aus, das Sie ändern möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften** , um das Dialogfeld **Eigenschaften** für das Startabbild zu öffnen.  

5.  Legen Sie die folgenden Einstellungen fest, um das Verhalten des Startabbilds zu ändern:  

    -   Klicken Sie auf der Registerkarte **Abbilder** auf **Neu laden**, wenn Sie die Eigenschaften des Startabbilds mithilfe eines externen Tools geändert haben.  

    -   Fügen Sie auf der Registerkarte **Treiber** die Windows-Gerätetreiber hinzu, die zum Starten von WinPE erforderlich sind. Beachten Sie beim Hinzufügen von Gerätetreibern die folgenden Punkte:  

        -   Wählen Sie **Hide drivers that do not match the architecture of the boot image** (Treiber ausblenden, die nicht mit der Architektur des Startimages übereinstimmen) aus, damit nur Treiber für die Architektur des Startimages angezeigt werden. Die Architektur basiert auf der Architektur, die in der INF-Datei vom Hersteller angegeben ist.  

        -   Wählen Sie **Hide drivers that are not in a storage or network class (for boot images)** (Treiber ausblenden, die in keiner Speicher- oder Netzwerkklasse enthalten sind (für Startimages)) aus, damit nur Speicher- und Netzwerktreiber angezeigt werden. Diese Option blendet auch andere Treiber aus, die in der Regel nicht für Startimages benötigt werden, z.B. Video- oder Modemtreiber.  

        -   Wählen Sie **Hide drivers that are not digitally signed** (Treiber ausblenden, die nicht digital signiert sind) aus, um Treiber auszublenden, die keine digitale Signatur aufweisen.  

        -   Es wird empfohlen, nur Netzwerk- und Massenspeichertreiber zum Startimage hinzuzufügen, es sei denn, für WinPE sind andere Treiber erforderlich.  

        -   Da in WinPE bereits zahlreiche Treiber integriert sind, fügen Sie nur die Netzwerk- und Massenspeichertreiber hinzu, die nicht mit WinPE bereitgestellt werden.  

        -   Stellen Sie sicher, dass die zum Startimage hinzugefügten Treiber der Architektur des Startimages entsprechen.  

        > [!NOTE]  
        >  Sie müssen Gerätetreiber in den Treiberkatalog importieren, bevor Sie sie einem Startabbild hinzufügen. Informationen zum Importieren von Gerätetreibern finden Sie unter [Verwalten von Treibern](manage-drivers.md).  

    -   Wählen Sie auf der Registerkarte **Anpassung** die folgenden Einstellungen aus:  

        -   Aktivieren Sie das Kontrollkästchen **Prestart-Befehl aktivieren** , um einen Befehl anzugeben, der vor der Tasksequenz ausgeführt werden soll. Wenn Sie diese Option aktivieren, geben Sie auch die auszuführende Befehlszeile und alle unterstützenden Dateien an, die für den Befehl erforderlich sind.  

            > [!WARNING]  
            >  Fügen Sie **cmd /c** am Anfang der Befehlszeile hinzu. Wenn Sie **cmd /c** nicht angeben, wird der Befehl nach der Ausführung nicht geschlossen. Die Bereitstellung wartet weiterhin auf den Abschluss des Befehls und startet keine weiteren konfigurierten Befehle oder Aktionen.  

            > [!TIP]  
            >  Während der Erstellung der Tasksequenzmedien werden die Paket-ID und die Prestart-Befehlszeile einschließlich des Wertes vorhandener Tasksequenzvariablen in die Protokolldatei „CreateTSMedia.log“ geschrieben. Dieses Protokoll befindet sich auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird. Anhand dieser Protokolldatei können Sie den Wert für die Tasksequenzvariablen überprüfen.  

        -   Geben Sie unter **Windows PE-Hintergrund** an, ob Sie den WinPE-Standardhintergrund oder einen benutzerdefinierten Hintergrund verwenden möchten.  

        -   Wählen Sie **Befehlsunterstützung aktivieren (nur Test)** aus, um während der Bereitstellung des Startabbilds über die Taste **F8** eine Eingabeaufforderung zu öffnen. Diese Option kann sich bei der Behandlung von Problemen, die beim Testen der Bereitstellung auftreten, als nützlich erweisen. Es wird davon abgeraten, diese Einstellung in einer Produktionsbereitstellung zu verwenden.  

        -   Konfigurieren Sie den temporären Speicherbereich für Windows PE. Dies ist temporärer Speicher (RAM), der von WinPE verwendet wird. Wenn eine Anwendung z. B. in WinPE ausgeführt wird und temporäre Dateien geschrieben werden müssen, werden die Dateien von WinPE an den temporären Speicherbereich im Arbeitsspeicher umgeleitet, um das Vorhandensein einer Festplatte zu simulieren. Standardmäßig werden von WinPE 32 MB beschreibbarer Arbeitsspeicher zugeordnet.  

    -   Führen Sie auf der Registerkarte **Datenquelle** für die folgenden Einstellungen ein Update aus:  

        -   Legen Sie **Imagepfad** und **Imageindex** fest, um die Quelldatei des Startimages zu ändern.  

        -   Wählen Sie **Verteilungspunkte entsprechend einem Zeitplan aktualisieren** aus, um einen Zeitplan dafür zu erstellen, wann der Standort das Startimage aktualisiert.  

        -   Wählen Sie **Inhalt in Clientcache belassen** aus, wenn Sie nicht möchten, dass der Inhalt dieses Pakets veraltet und aus dem Clientcache gelöscht wird, um Platz für anderen Inhalt zu schaffen.  

        -   Wählen Sie **Binäre differenzielle Replikation aktivieren** aus, um anzugeben, dass beim Update des Startimagepakets am Verteilungspunkt nur geänderte Dateien verteilt werden sollen. Durch diese Einstellung wird der Netzwerkdatenverkehr zwischen den Standorten minimiert. BDR ist besonders nützlich, wenn das Startimagepaket groß ist und die Änderungen relativ gering sind.  

        -   Wählen Sie **Dieses Startimage über den PXE-fähigen Verteilungspunkt bereitstellen** aus, wenn Sie das Startimage in einer PXE-fähigen Bereitstellung verwenden.  

            > [!NOTE]  
            >  Weitere Informationen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   Wählen Sie auf der Registerkarte **Datenzugriff** die folgenden Einstellungen aus:  

        -   Legen Sie **Einstellungen für die Paketfreigabe** fest, wenn der Inhalt dieses Pakets von Clients vom Netzwerk installiert werden soll.  

        -   Geben Sie unter **Einstellungen für die Paketaktualisierung** an, auf welche Weise Benutzer durch Configuration Manager vom Verteilungspunkt getrennt werden sollen. Über Configuration Manager kann möglicherweise kein Update ausgeführt werden, wenn Benutzer mit dem Verteilungspunkt verbunden sind.  

    -   Wählen Sie auf der Registerkarte **Verteilungseinstellungen** die folgenden Einstellungen aus:  

        -   Geben Sie in der Liste **Verteilungspriorität** die Prioritätsstufe an. Configuration Manager verwendet diese Prioritätsliste, wenn der Standort mehrere Pakete an denselben Verteilungspunkt verteilt.  

        -   Wählen Sie **Den Inhalt für dieses Paket an bevorzugte Verteilungspunkte verteilen** aus, wenn Sie eine bedarfsgesteuerte Inhaltsverteilung an bevorzugte Verteilungspunkte aktivieren möchten. Wenn Sie diese Einstellung aktivieren und der von einem Client angeforderte Inhalt für das Paket auf keinem der bevorzugten Verteilungspunkte verfügbar ist, wird der Inhalt vom Verwaltungspunkt an alle bevorzugten Verteilungspunkte verteilt.  

        -   Geben Sie unter **Einstellungen für vorab bereitgestellten Verteilungspunkt** an, wie das Startimage an Verteilungspunkte verteilt werden soll, die für vorab bereitgestellten Inhalt aktiviert sind.  

            > [!NOTE]  
            >  Weitere Informationen zu vorab bereitgestelltem Inhalt finden Sie unter [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  

    -   Wählen Sie auf der Registerkarte **Inhaltsorte** den Verteilungspunkt bzw. die Verteilungspunktgruppe aus, und führen Sie die folgenden Aktionen aus:  

        -   Klicken Sie auf **Neu verteilen** , um das Startabbild erneut an den ausgewählten Verteilungspunkt oder an die ausgewählte Verteilungspunktgruppe zu verteilen.  

        -   Klicken Sie auf **Überprüfen** , um die Integrität des Startabbildpakets am ausgewählten Verteilungspunkt bzw. in der ausgewählten Verteilungspunktgruppe zu überprüfen.  

    -   Geben Sie auf der Registerkarte **Optionale Komponenten** die Komponenten an, die Windows PE zur Verwendung mit Configuration Manager hinzugefügt werden. Weitere Informationen zu verfügbaren optionalen Komponenten finden Sie unter [WinPE: Hinzufügen von Paketen (Referenz zu optionalen Komponenten)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

    -   Wählen Sie auf der Registerkarte **Sicherheit** einen Administrator aus, und ändern Sie die Vorgänge, die dieser Administrator ausführen kann.  

6.  Nachdem Sie die Eigenschaften konfiguriert haben, klicken Sie auf **OK**.  

##  <a name="BKMK_BootImagePXE"></a> Konfigurieren eines Startimages, das über einen PXE-fähigen Verteilungspunkt bereitgestellt werden soll  
 Bevor Sie ein Startimage für eine PXE-Betriebssystembereitstellung verwenden können, müssen Sie das Startimage für die Bereitstellung über einen PXE-fähigen Verteilungspunkt konfigurieren.  

#### <a name="to-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a>So konfigurieren Sie ein Startimage, das über einen PXE-fähigen Verteilungspunkt bereitgestellt werden soll  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Startabbilder**.  

3.  Wählen Sie das Startabbild aus, das Sie ändern möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften** , um das Dialogfeld **Eigenschaften** für das Startabbild zu öffnen.  

5.  Wählen Sie auf der Registerkarte **Datenquelle** die Option **Dieses Startimage über den PXE-fähigen Verteilungspunkt bereitstellen**aus.  

    > [!NOTE]  
    >  Weitere Informationen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

6.  Nachdem Sie die Eigenschaften konfiguriert haben, klicken Sie auf **OK**.  

##  <a name="BKMK_BootImageLanguage"></a> Konfigurieren von mehreren Sprachen für die Startimagebereitstellung  
 Startabbilder sind sprachneutral. Mit dieser Funktion können Sie ein Startimage verwenden, um den Text der Tasksequenz in WinPE in mehreren Sprachen anzuzeigen. Schließen Sie die entsprechende Sprachunterstützung von der Registerkarte **Optionale Komponenten** des Startimages ein. Legen Sie anschließend die entsprechende Tasksequenzvariable fest, um die anzuzeigende Sprache anzugeben. Die Sprache des bereitgestellten Betriebssystems hängt von der Sprache in WinPE ab. Die Sprache, die dem Benutzer in WinPE angezeigt wird, wird wie folgt bestimmt:  

-   Wenn ein Benutzer die Tasksequenz unter einem vorhandenen Betriebssystem ausführt, wird von Configuration Manager automatisch die für den Benutzer konfigurierte Sprache verwendet. Wird die Tasksequenz automatisch als Folge eines obligatorischen Bereitstellungsstichtags ausgeführt, wird von Configuration Manager die Sprache des Betriebssystems verwendet.  

-   Für Betriebssystembereitstellungen, für die PXE oder Medien verwendet werden, können Sie den Wert für die Sprach-ID in der Variablen **SMSTSLanguageFolder** als Teil eines Prestart-Befehls festlegen. Wenn der Computer mit WinPE gestartet wird, werden Meldungen in der Sprache angezeigt, die Sie in der Variablen angegeben haben. Falls beim Zugreifen auf die Sprachressourcendatei im angegebenen Ordner ein Fehler auftritt oder Sie die Variable nicht festlegen, werden in WinPE Meldungen in der Standardsprache angezeigt.  

    > [!NOTE]  
    >  Wenn das Medium mit einem Kennwort geschützt ist, wird der Text, mit dem Benutzer zur Eingabe des Kennworts aufgefordert werden, immer in der WindPE-Sprache angezeigt.  

 Verwenden Sie das folgende Verfahren zum Festlegen der WinPE-Sprache für Betriebssystembereitstellungen, die per PXE oder Startmedium initiiert werden.  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>So legen Sie die Windows PE-Sprache für Betriebssystembereitstellungen fest, die per PXE oder Startmedium initiiert werden  

1.  Überprüfen Sie vor dem Aktualisieren des Startimages, ob sich die richtige Tasksequenz-Ressourcendatei („tsres.dll“) im entsprechenden Sprachordner auf dem Standortserver befindet. Die Ressourcendatei für Englisch befindet sich beispielsweise an folgendem Speicherort: <*ConfigMgrInstallationFolder*>\OSD\bin\x64\00000409\tsres.dll.  

2.  Legen Sie als Teil des Prestart-Befehls die Umgebungsvariable SMSTSLanguageFolder auf die gewünschte Sprach-ID fest. Die Sprach-ID muss im Dezimalformat angegeben werden (nicht hexadezimal). Wenn Sie die Sprach-ID auf Englisch festlegen möchten, geben Sie z.B. den Dezimalwert 1033 an, und nicht den Hexadezimalwert 00000409 für den Ordnernamen.  
