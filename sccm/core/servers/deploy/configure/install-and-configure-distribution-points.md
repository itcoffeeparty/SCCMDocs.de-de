---
title: Verwalten von Verteilungspunkten
titleSuffix: Configuration Manager
description: Den Inhalt, den Sie für Geräte und Benutzer bereitstellen, mithilfe von Verteilungspunkten hosten
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
caps.latest.revision: 5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1010e339c586922f818e1af1e193abba95dace7b
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="install-and-configure-distribution-points-for-system-center-configuration-manager"></a>Installieren und Konfigurieren von Verteilungspunkten für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Um die Inhaltsdateien die Inhaltsdateien zu hosten, die Sie für Geräte und Benutzer bereitstellen, können Sie Configuration Manager-Verteilungspunkte installieren. Die Erstellung von Verteilungspunktgruppen erleichtert die Verwaltung von Verteilungspunkten und die Verteilung von Inhalt an die Verteilungspunkte.  

 Wenn Sie *einen neuen Verteilungspunkt installieren* (mithilfe des Installations-Assistenten) oder *die Eigenschaften eines vorhandenen Verteilungspunkts verwalten* (durch Bearbeiten der Verteilungspunkteigenschaften), können Sie einen Großteil der Einstellungen des Verteilungspunkts konfigurieren. Es gibt jedoch einige Einstellungen, die entweder bei der Installation oder bei der Bearbeitung, aber nicht gleichzeitig verfügbar sind:  

-   Einstellungen, die nur bei der Installation eines Verteilungspunkts verfügbar sind:  

    -   **Zulassen, dass Configuration Manager IIS auf dem Verteilungspunktcomputer installiert**

    -   **Konfigurieren der Laufwerksspeicherplatzeinstellungen für den Verteilungspunkt**  

-   Einstellungen, die nur bei der Bearbeitung der Eigenschaften eines Verteilungspunkts verfügbar sind:  

    -   **Verwalten der Beziehungen zwischen Verteilungspunktgruppen**  

    -   **Anzeigen von auf dem Verteilungspunkt bereitgestelltem Inhalt**  

    -   **Konfigurieren der Begrenzung der Datenübertragungsrate für Datenübertragungen an Verteilungspunkte**  

    -   **Konfigurieren der Zeitpläne für Datenübertragungen an Verteilungspunkte**  

##  <a name="bkmk_install"></a> Installieren eines Verteilungspunkts  
Legen Sie einen Standortsystemserver als Verteilungspunkt fest, bevor Inhalt für Clientcomputer verfügbar gemacht werden kann. Weisen Sie auch mindestens einer [Begrenzungsgruppe](/sccm/core/servers/deploy/configure/boundary-groups#distribution-points) einen Verteilungspunkt zu, bevor lokale Clientcomputer diesen Verteilungspunkt als Quellspeicherort für Inhalt verwenden können. Fügen Sie die Standortrolle für Verteilungspunkte einem neuen oder einem vorhandenen Standortsystemserver hinzu.


 Wenn Sie einen neuen Verteilungspunkt installieren, verwenden Sie einen Installations-Assistenten, der mit Ihnen die verfügbaren Einstellungen durchgeht. Bevor Sie beginnen, beachten Sie die folgenden Voraussetzungen:  

-   Sie benötigen die folgenden Sicherheitsberechtigungen, um einen Verteilungspunkt zu erstellen und zu konfigurieren:  

    -   **Lesen** für das Objekt **Verteilungspunkt**  

    -   **Kopieren an Verteilungspunkt** für das Objekt **Verteilungspunkt**  

    -   **Ändern** für das Objekt **Standort**  

    -   **Zertifikate für Betriebssystembereitstellung verwalten** für das Objekt **Standort**  

-   Installieren Sie Internetinformationsdienste (IIS) auf dem Server, der den Verteilungspunkt hostet. Bei der Installation der Standortsystemrolle kann Configuration Manager IIS für Sie installieren und konfigurieren.  

Verwenden Sie die folgenden grundlegenden Verfahren zum Installieren oder Ändern eines Verteilungspunkts. Weitere Informationen zu den verfügbaren Konfigurationsoptionen finden Sie unter dem Abschnitt [Konfigurieren eines Verteilungspunkts](#bkmk_configs) dieses Themas.  

#### <a name="to-install-a-distribution-point"></a>So installieren Sie einen Verteilungspunkt  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** >  **Standortkonfiguration** > **Server und Standortsystemrollen** aus.  

2.  Fügen Sie die Standortsystemrolle „Verteilungspunkt“ einem neuen oder vorhandenen Standortsystemserver hinzu:  

    -   **Neuer Standortsystemserver**: Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Standortsystemserver erstellen** aus. Der Assistent zum Erstellen von Standortsystemservern wird geöffnet.  

    -   **Bestehender Standortsystemserver**: Wählen Sie den Server aus, auf dem die Standortsystemrolle „Verteilungspunkt“ installiert werden soll. Wenn Sie einen Server auswählen, wird im Ergebnisbereich eine Liste der Standortsystemrollen angezeigt, die bereits auf dem Server installiert sind.  

         Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Server** die Option **Standortsystemrolle hinzufügen** aus. Der Assistent zum Hinzufügen von Standortsystemrollen wird geöffnet.  

3.  Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für den Standortsystemserver an. Wenn Sie den Verteilungspunkt einem vorhandenen Standortsystemserver hinzufügen, überprüfen Sie die Werte, die zuvor konfiguriert wurden.  

4.  Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen **Verteilungspunkt** aus. Anschließend wählen Sie **Weiter** aus.  

5.  Informationen zu den nachfolgenden Seiten des Assistenten finden Sie im Abschnitt [Konfigurieren eines Verteilungspunkts](#bkmk_configs).  

     Wenn Sie den Verteilungspunkt z. B. als Pullverteilungspunkt installieren möchten, wählen Sie die Option **Inhaltspulling von anderen Verteilungspunkten für diesen Verteilungspunkt aktivieren** aus, und nehmen Sie dann die für die Pullverteilungspunkte erforderlichen weiteren Konfigurationen vor.  

6.  Wenn Sie den Assistenten abschließen, wird die Standortrolle „Verteilungspunkt“ dem Standortserver hinzugefügt.  

#### <a name="to-change-a-distribution-point"></a>So ändern Sie einen Verteilungspunkt  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** >  **Verteilungspunkte** und dann den Verteilungspunkt aus, den Sie konfigurieren möchten.  

2.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

3.  Verwenden Sie beim Bearbeiten der Eigenschaften des Verteilungspunkts die Informationen im Abschnitt [Konfigurieren von Verteilungspunkten](#bkmk_configs).  

4.  Nachdem Sie die gewünschten Änderungen vorgenommen haben, speichern Sie Ihre Einstellungen, und schließen Sie die Verteilungspunkteigenschaften.  

##  <a name="bkmk_manage"></a> Verwalten von Verteilungspunktgruppen  
 Verteilungspunktgruppen stellen eine logische Gruppierung von Verteilungspunkten für die Inhaltsverteilung dar. Mithilfe dieser Gruppen können Sie Inhalte von einem zentralen Speicherort für Verteilungspunkte, die mehrere Standorte umfassen, verwalten und überwachen. Beachten Sie Folgendes:

-   Sie können der Verteilungspunktgruppe von beliebigen Standorten innerhalb einer Hierarchie Verteilungspunkte hinzufügen.  

-   Sie können einen Verteilungspunkt zu mehreren Verteilungspunktgruppen hinzufügen.  

-   Wenn Sie Inhalt an eine Verteilungspunktgruppe verteilen, wird der Inhalt von Configuration Manager an alle Verteilungspunkte verteilt, die dieser Verteilungspunktgruppe angehören.  

-   Wenn Sie einer Verteilungspunktgruppe nach der ersten Inhaltsverteilung einen Verteilungspunkt hinzufügen, wird der Inhalt von Configuration Manager automatisch an das neue Mitglied der Verteilungspunktgruppe verteilt.  

-   Sie können einer Verteilungspunktgruppe eine Sammlung zuordnen. Wenn Sie Inhalte an diese Sammlung verteilen, bestimmt Configuration Manager, welche Verteilungspunktgruppen der Sammlung zugeordnet werden. Dann wird der Inhalt an alle Verteilungspunkte verteilt, die Mitglieder dieser Verteilungspunktgruppen sind.  

    > [!NOTE]  
    >  Wenn Sie eine Sammlung einer neuen Verteilungspunktgruppe zuordnen, nachdem bereits Inhalte an die Sammlung verteilt wurden, müssen Sie die Inhalte erneut an die Sammlung verteilen, damit sie auch an die neue Verteilungspunktgruppe verteilt werden.  

#### <a name="to-create-and-configure-a-new-distribution-point-group"></a>So erstellen und konfigurieren Sie eine neue Verteilungspunktgruppe  

1.  Wählen Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Verteilungspunktgruppen** aus.  

2.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Gruppe erstellen** aus.  

3.  Geben Sie den Namen und die Beschreibung für die Verteilungspunktgruppe ein.  

4.  Wählen Sie auf der Registerkarte **Sammlungen** die Option **Hinzufügen** und dann die Sammlungen aus, die der Verteilungspunktgruppe zugeordnet werden sollen, und klicken Sie dann auf **OK**.  

5.  Wählen Sie auf der Registerkarte **Mitglieder** die Option **Hinzufügen** und dann die Verteilungspunkte aus, die der Verteilungspunktgruppe als Mitglieder hinzugefügt werden sollen, und wählen Sie dann **OK** aus.  

6.  Wählen Sie **OK** aus, um die Verteilungspunktgruppe zu erstellen.  

#### <a name="to-add-distribution-points-and-associate-collections-with-an-existing-distribution-point-group"></a>So fügen Sie einer vorhandenen Verteilungspunktgruppe Verteilungspunkte hinzu und ordnen ihr Sammlungen zu  

1.  Wählen Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Verteilungspunktgruppen** aus.  

2.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

3.  Wählen Sie auf der Registerkarte **Sammlungen** die Option **Hinzufügen** aus, um die Sammlungen auszuwählen, die Sie der Verteilungspunktgruppe zuordnen möchten, und wählen Sie dann **OK** aus.  

4.  Wählen Sie auf der Registerkarte **Mitglieder** die Option **Hinzufügen** und dann die Verteilungspunkte aus, die der Verteilungspunktgruppe als Mitglieder hinzugefügt werden sollen, und klicken Sie dann auf **OK**.  

5.  Wählen Sie **OK** aus, um die Änderungen der Verteilungspunktgruppe zu speichern.  

#### <a name="to-add-selected-distribution-points-to-a-new-distribution-point-group"></a>So fügen Sie ausgewählte Verteilungspunkte einer neuen Verteilungspunktgruppe hinzu  

1.  Wählen Sie in der Configuration Manager-Konsole die Option **Verwaltung** > **Verteilungspunkte** und dann die Verteilungspunkte aus, die Sie der neuen Verteilungspunktgruppe hinzufügen möchten.  

2.  Erweitern Sie auf der Registerkarte **Startseite** in der Gruppe **Verteilungspunkte** den Knoten **Ausgewählte Elemente hinzufügen**, und wählen Sie dann **Ausgewählte Elemente neuer Verteilungspunktgruppe hinzufügen** aus.  

3.  Geben Sie den Namen und die Beschreibung für die Verteilungspunktgruppe ein.  

4.  Wählen Sie auf der Registerkarte **Sammlungen** die Option **Hinzufügen** aus, um die Sammlungen auszuwählen, die Sie der Verteilungspunktgruppe zuordnen möchten, und wählen Sie dann **OK** aus.  

5.  Überprüfen Sie auf der Registerkarte **Mitglieder**, ob Configuration Manager die aufgelisteten Verteilungspunkte der Verteilungspunktgruppe als Mitglieder hinzufügen soll. Wählen Sie **Hinzufügen** aus, um die Verteilungspunkte hinzuzufügen, und wählen Sie dann **OK** aus.  

6.  Wählen Sie **OK** aus, um die Verteilungspunktgruppe zu erstellen.  

#### <a name="to-add-selected-distribution-points-to-existing-distribution-point-groups"></a>So fügen Sie ausgewählte Verteilungspunkte vorhandenen Verteilungspunktgruppen hinzu  

1.  Wählen Sie in der Configuration Manager-Konsole die Option **Verwaltung** > **Verteilungspunkte** und dann die Verteilungspunkte aus, die Sie der neuen Verteilungspunktgruppe hinzufügen möchten.  

2.  Erweitern Sie auf der Registerkarte **Startseite** in der Gruppe **Verteilungspunkte** den Knoten **Ausgewählte Elemente hinzufügen**, und wählen Sie dann **Ausgewählte Elemente vorhandenen Verteilungspunktgruppen hinzufügen** aus.  

3.  Wählen Sie unter **Verfügbare Verteilungspunktgruppen**die Verteilungspunktgruppen aus, denen die ausgewählten Verteilungspunkte als Mitglieder hinzugefügt werden sollen, und wählen Sie dann **OK** aus.  



## <a name="reassign-a-distribution-point"></a>Neuzuweisen eines Verteilungspunkts
<!-- 1306937 -->
Viele Kunden verfügen über eine ausgeprägte Configuration Manager-Infrastruktur und verringern die Anzahl von primären und sekundären Standorten, um ihre Umgebung einfacher zu gestalten. Sie benötigen allerdings weiterhin Verteilungspunkte für die Standorte ihrer Zweigstellen, um Inhalte für verwaltete Clients bereitzustellen. Diese Verteilungspunkte enthalten häufig mehrere Terabytes an Inhalt. Dieser Inhalt nimmt viel Zeit in Anspruch, und es wird eine hohe Netzwerk-Bandbreite benötigt, um die Daten an die Remoteserver zu übermitteln. 

Ab Version 1802 können Sie mithilfe dieses Features einen Verteilungspunkt einem anderen primären Standort neu zuweisen, ohne dabei den Inhalt neu verteilen zu müssen. Über diese Aktion wird ein Update für die Standortsystemzuweisung ausgeführt. Gleichzeitig wird der gesamte Inhalt dauerhaft auf dem Server gespeichert. Wenn Sie mehrere Verteilungspunkte neu zuweisen müssen, führen Sie zunächst diese Aktion auf einem einzelnen Verteilungspunkt aus, und fügen Sie anschließend einen Server nach dem anderen hinzu.

> [!IMPORTANT]
> Der Zielserver kann nur die Rolle für den Verteilungspunkt hosten. Wenn der Standortsystemserver eine andere Serverrolle von Configuration Manager hostet (z.B. den Zustandsmigrationspunkt), können Sie den Verteilungspunkt nicht neu zuweisen. Außerdem können Sie keinen Verteilunspunkt für die Cloud neu zuweisen. 

Fügen Sie das Computerkonto des Zielstandortservers vor dem Neuzuweisen eines Verteilungspunkts der lokalen Administratorgruppe auf dem Zielserver mit dem Verteilungspunkt hinzu. 

Führen Sie diese Schritte aus, um einen Verteilungspunkt neu zuzuweisen:
1. Stellen Sie in der Configuration Manager-Konsole eine Verbindung zum Standort der zentralen Verwaltung her. 
2. Gehen Sie zum Arbeitsbereich **Verwaltung**, und klicken Sie dann auf den Knoten **Verteilungspunkte**.
3. Klicken Sie mit der rechten Maustaste auf den Zielverteilungspunkt, und klicken Sie anschließend auf **Verteilungspunkt neu zuweisen**. 
4. Wählen Sie den Zielstandortserver und den Standortcode aus, denen Sie diesen Verteilungspunkt neu zuweisen möchten. 

Überwachen Sie die Neuzuweisung so wie beim Hinzufügen einer neuen Rolle. Die einfachste Methode dafür ist das Aktualisieren der Konsolenansicht nach einigen Minuten. Fügen Sie der Ansicht die Standortcodespalte hinzu. Dieser Wert ändert sich, wenn Configuration Manager den Server neu zuweist. Wenn Sie versuchen, eine andere Aktion auf dem Zielserver auszuführen, bevor Sie die Konsolenansicht aktualisieren, tritt der Fehler „Objekt nicht gefunden“ auf. Stellen Sie sicher, dass der Prozess abgeschlossen ist, und aktualisieren Sie die Konsolenansicht, bevor Sie eine andere Aktion auf dem Server ausführen.

Aktualisieren Sie das Serverzertifikat nach dem Neuzuweisen eines Verteilungspunkts. Der neue Standortserver muss dieses Zertifikat mit dem öffentlichen Schlüssel neu verschlüsseln und es in der Standortdatenbank speichern. Weitere Informationen finden Sie auf der Registerkarte [Allgemein](#general) der Eigenschaften des Verteilungspunkts in der Einstellung **Create a self-signed certificate or import a public key infrastructure (PKI) client certificate for the distribution point** (Selbstsigniertes Zertifikat erstellen oder ein PKI-Clientzertifikat für den Verteilungspunkt importieren). 
- Für PKI-Zertifikate müssen Sie kein neues Zertifikat erstellen. Importieren Sie dieselbe PFX-Datei, und geben Sie das Kennwort ein.
- Passen Sie für selbstsignierte Zertifikate das Ablaufdatum oder den Updatezeitpunkt an.
Wenn Sie das Zertifikat nicht aktualisieren, liefert der Verteilungspunkt weiterhin Inhalt, jedoch schlagen die folgenden Funktionen fehl:
    - Nachrichten zur Inhaltsprüfung (die Datei „distmgr.log“ zeigt an, dass das Zertifikat nicht entschlüsselt werden kann)
    - PXE-Unterstützung für Clients 

### <a name="tips"></a>Tipps
- Führen Sie diese Aktion am Standort der zentralen Verwaltung aus. Dieses Vorgehen hilft bei der Replikation an den primären Standort.
- Verteilen Sie den Inhalt nicht an den Zielserver, um anschließend zu versuchen, ihn neu zuzuweisen. Verteilte Inhaltstasks, die ausgeführt werden, können bei der Neuzuweisung fehlschlagen, werden jedoch wie normal erneut ausgeführt.
- Wenn der Server auch ein Configuration Manager-Client ist, achten Sie darauf, auch den Client dem neuen primären Standort neu zuzuweisen. Dieser Schritt ist besonders wichtig für Pullverteilungspunkte, die Inhalt mithilfe von Clientkomponenten herunterladen.
- Dieser Prozess entfernt den Verteilungspunkt aus der alten Standardbegrenzungsgruppe des Standorts. Falls erforderlich, müssen Sie ihn manuell zur Standardbegrenzungsgruppe des neuen Standorts hinzufügen. Alle anderen Begrenzungsgruppenzuweisungen bleiben unverändert.



##  <a name="bkmk_configs"></a> Konfigurieren eines Verteilungspunkts  
 Einzelne Verteilungspunkte unterstützen viele verschiedene Konfigurationen. Allerdings unterstützen nicht alle Verteilungspunkttypen alle Konfigurationen. Cloudbasierte Verteilungspunkte unterstützen beispielsweise keine Inhaltsbereitstellungen, die für PXE oder Multicast aktiviert sind. Informationen zu den spezifischen Einschränkungen finden in den folgenden Themen:  

-   [Verwenden eines cloudbasierten Verteilungspunkts mit System Center Configuration Manager](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

-   [Verwenden eines Pullverteilungspunkts mit System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

In den folgenden Abschnitten sind die Konfigurationen beschrieben, die Sie beim Installieren eines neuen Verteilungspunkts oder beim Bearbeiten der Eigenschaften eines vorhandenen Verteilungspunkts auswählen können.  

### <a name="general"></a>Allgemein  
 Konfigurieren Sie die allgemeinen Einstellungen des Verteilungspunkts.  

-   **IIS installieren und konfigurieren, sofern dies für Configuration Manager erforderlich ist:** Wählen Sie diese Einstellung, damit Configuration Manager die Internetinformationsdienste (IIS) auf dem Server installiert und konfiguriert, sofern noch nicht erfolgt. IIS müssen auf allen Verteilungspunkten installiert werden. Wenn IIS nicht auf dem Server installiert sind und Sie diese Einstellung nicht auswählen, müssen Sie IIS installieren, damit der Verteilungspunkt erfolgreich installiert werden kann.  

    > [!NOTE]  
    >  Diese Option ist nur bei der Installation eines neuen Verteilungspunkts verfügbar.  

- **BranchCache für diesen Verteilungspunkt aktivieren und konfigurieren:** Wählen Sie diese Einstellung aus, damit Configuration Manager Windows BranchCache auf dem Verteilungspunktserver installiert. Weitere Informationen zur Verwendung von Windows BranchCache mit System Center Configuration Manager finden Sie unter [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#a-namebkmkbranchcachea-branchcache) in *Unterstützung für Windows-Features und -Netzwerke in System Center Configuration Manager*.

-   **Konfigurieren, wie der Clientgeräte mit dem Verteilungspunkt kommunizieren:** Die Verwendung von HTTP und HTTPS hat Vor- und Nachteile. Weitere Informationen finden Sie unter „Bewährte Sicherheitsmethoden für die Inhaltsverwaltung“ im Thema [Sicherheit und Datenschutz für die Inhaltsverwaltung in Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   **Allow clients to connect anonymously** (Zulassen, dass Clients eine anonyme Verbindung herstellen): Mit dieser Einstellung geben Sie an, ob vom Verteilungspunkt anonyme Verbindungen von Configuration Manager-Clients mit der Inhaltsbibliothek zugelassen werden.  

    > [!IMPORTANT]  
    >  Wenn Sie diese Einstellung nicht verwenden, kann die Reparatur einer Windows Installer-Anwendung auf einem Client fehlschlagen.  
    >   
    >  Bei der Bereitstellung einer Windows Installer-Anwendung auf einem Configuration Manager-Client wird die Datei von Configuration Manager in den lokalen Cache des Clients heruntergeladen. Die Dateien werden nach Abschluss der Installation schließlich entfernt.
    >  
    >  Bei der Windows Installer-Quellliste der installierten Windows Installer-Anwendungen wird vom Configuration Manager-Client ein Update mit dem Inhaltspfad der Inhaltsbibliothek auf zugeordneten Verteilungspunkten ausgeführt. Wenn Sie später mit der Systemsteuerungsoption „Software“ für einen Configuration Manager-Client eine Reparaturaktion starten, wird von MSIExec versucht, über einen anonymen Benutzer auf den Inhaltspfad zuzugreifen.  
    >   
    >  Allerdings können Sie das im Microsoft Knowledge Base-Artikel [2619572](http://go.microsoft.com/fwlink/?LinkId=279699) beschriebene Update installieren und anschließend einen Registrierungsschlüssel ändern, um dieses Verhalten zu ändern.  
    >   
    >  Nachdem das Update auf den Clients installiert wurde, wird von MSIExec mithilfe des angemeldeten Benutzerkontos auf den Inhaltspfad zugegriffen, wenn Sie die Einstellung **Clients gestatten, eine anonyme Verbindung herzustellen** nicht aktivieren.  

-   **Für den Verteilungspunkt ein selbstsigniertes Zertifikat erstellen oder ein PKI-Clientzertifikat (Public Key-Infrastruktur) importieren:** Das Zertifikat erfüllt die folgenden Zwecke:  

    -   Durch das Zertifikat wird der Verteilungspunkt gegenüber einem Verwaltungspunkt authentifiziert, bevor vom Verteilungspunkt Statusmeldungen gesendet werden.  

    -   Wenn Sie auf der Seite **PXE-Einstellungen** das Kontrollkästchen **PXE-Unterstützung für Clients aktivieren** aktivieren, wird das Zertifikat an Computer gesendet, von denen ein PXE-Start ausgeführt wird. Bei der Bereitstellung des Betriebssystems kann dann von diesen Computern eine Verbindung mit dem Verwaltungspunkt hergestellt werden.  

    Wenn alle Verwaltungspunkte am Standort für HTTP konfiguriert sind, erstellen Sie ein selbstsigniertes Zertifikat. Wenn die Verwaltungspunkte für HTTPS konfiguriert sind, importieren Sie ein PKI-Clientzertifikat.  

    Um das Zertifikat zu importieren, wechseln Sie zu einer PKCS #12-Datei (Public Key Cryptography Standard), die ein PKI-Zertifikat mit den folgenden Anforderungen für Configuration Manager enthält:  

    -   Die Clientauthentifizierung muss zur Verwendung vorgesehen sein.  

    -   Lassen Sie zu, dass der private Schlüssel exportiert werden kann.  

    > [!TIP]  
    >  Es gibt keine speziellen Anforderungen für den Zertifikatantragsteller oder den alternativen Antragstellernamen (SAN). Sie können ein Zertifikat für mehrere Verteilungspunkte verwenden.  

     Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

     Eine Beispielbereitstellung dieses Zertifikats finden Sie im Abschnitt „Bereitstellen des Clientzertifikats für Verteilungspunkte“ des Themas [Beispiel für die schrittweise Bereitstellung der PKI-Zertifikate für System Center Configuration Manager: Windows Server 2008-Zertifizierungsstelle](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

-   **Diesen Verteilungspunkt für vorab bereitgestellten Inhalt aktivieren:** Mit dieser Einstellung können Sie den Verteilungspunkt für vorab bereitgestellten Inhalt aktivieren. Ist diese Einstellung ausgewählt, können Sie das Verteilungsverhalten bei der Inhaltsverteilung konfigurieren. Sie können immer eine der folgenden Aktionen ausführen:

 - Inhalt wird vorab auf dem Verteilungspunkt bereitgestellt.
 - Der Anfangsinhalt des Pakets wird vorab bereitgestellt, Inhaltsaktualisierungen erfolgen mithilfe des regulären Inhaltsverteilungsvorgangs.
 - Für Inhalt des Pakets wird der reguläre Inhaltsverteilungsvorgang verwendet.  

### <a name="drive-settings"></a>Laufwerkseinstellungen  

> [!NOTE]  
>  Diese Optionen sind nur bei der Installation eines neuen Verteilungspunkts verfügbar.  

Geben Sie die Laufwerkseinstellungen für den Verteilungspunkt an. Sie können bis zu zwei Laufwerke für die Inhaltsbibliothek und zwei Laufwerke für die Paketfreigabe konfigurieren. Configuration Manager kann zusätzliche Laufwerke verwenden, wenn die ersten beiden die konfigurierte Laufwerksspeicherreserve erreichen. Auf der Seite **Laufwerkseinstellungen** werden die Priorität der Laufwerke und der freie Speicherplatz, der auf jedem Laufwerk verbleiben muss, festgelegt.  

-   **Laufwerksspeicherreserve (MB):** Hiermit geben Sie an, wie viel freier Speicher auf einem Laufwerk verbleiben muss. Wird der Wert erreicht, wählt Configuration Manager ein anderes Laufwerk aus, auf dem der Kopiervorgang fortgesetzt wird. Inhaltsdateien können sich über mehrere Laufwerke erstrecken.  

-   **Inhaltsorte**: Geben Sie die Inhaltsorte für die Inhaltsbibliothek und die Paketfreigabe an. Configuration Manager kopiert solange Inhalte zum primären Inhaltsort, bis die Menge des freien Speicherplatzes den unter **Laufwerksspeicherreserve (MB)** angegebenen Wert erreicht. Die Inhaltsorte sind standardmäßig auf **Automatisch**festgelegt. Das Laufwerk, bei dem zum Zeitpunkt der Installation der meiste freie Speicherplatz verfügbar ist, wird als primärer Inhaltsort festgelegt, und das Laufwerk mit dem nächstmeisten freien Speicherplatz als sekundärer Inhaltsort. Wenn vom primären und sekundären Laufwerk die Laufwerksspeicherreserve erreicht wird, wählt Configuration Manager ein anderes verfügbares Laufwerk mit dem meisten freien Speicherplatz aus und setzt den Kopiervorgang dort fort.  

> [!NOTE]  
>  Wenn die Installation durch Configuration Manager nicht auf einem bestimmten Laufwerk erfolgen soll, erstellen Sie eine leere Datei namens **no_sms_on_drive.sms**, und legen Sie sie im Stammordner des Laufwerks ab, bevor Sie den Verteilungspunkt installieren.  

### <a name="pull-distribution-point"></a>Pullverteilungspunkt  
Wenn Sie die Option **Inhaltspulling von anderen Verteilungspunkten für diesen Verteilungspunkt aktivieren** auswählen, ändern Sie die Art und Weise, wie der Computer den Inhalt abruft, den Sie an den Verteilungspunkt verteilen. Der Verteilungspunkt wird zu einem Pullverteilungspunkt.  

Für jeden Pullverteilungspunkt, den Sie konfigurieren, müssen Sie mindestens einen Quellverteilungspunkt angeben, von dem der Inhalt vom Pullverteilungspunkt abgerufen wird:  

-   Wählen Sie **Hinzufügen** und dann mindestens einen verfügbaren Verteilungspunkt als Quellverteilungspunkt aus.  

-   Wählen Sie **Entfernen** aus, um den ausgewählten Verteilungspunkt als Quellverteilungspunkt zu entfernen.  

-   Mit den Pfeiltasten können Sie die Reihenfolge anpassen, in der die Quellverteilungspunkte vom Pullverteilungspunkt kontaktiert werden, wenn vom Pullverteilungspunkt Inhalt übertragen werden soll. Verteilungspunkte mit dem niedrigsten Wert werden zuerst angesprochen.  

### <a name="pxe"></a>PXE  
Geben Sie an, ob PXE auf dem Verteilungspunkt aktiviert werden soll. Wenn Sie PXE aktivieren, installiert Configuration Manager bei Bedarf die Windows-Bereitstellungsdienste (Windows Deployment Services, WDS) auf dem Server. WDS ist der Dienst, der den PXE-Start zur Installation von Betriebssystemen ausgeführt. Wenn Sie den Assistenten zum Erstellen des Verteilungspunkts abgeschlossen haben, installiert Configuration Manager einen Anbieter in den Windows-Bereitstellungsdiensten, der die PXE-Startfunktionen verwendet. 

Wenn Sie die Option **PXE-Unterstützung für Clients aktivieren** auswählen, konfigurieren Sie die folgenden Einstellungen:  

 > [!Note]  
 > Aktivieren Sie unter **Für PXE erforderliche Ports überprüfen** das Kontrollkästchen **Ja**, um zu bestätigen, dass Sie PXE aktivieren möchten. Configuration Manager konfiguriert automatisch die Standardports der Windows-Firewall. Sie müssen die Ports manuell konfigurieren, wenn Sie eine andere Firewall verwenden.  
 >   
 > Wenn WDS und DHCP auf demselben Server installiert sind, müssen Sie WDS für das Lauschen an einem anderen Port konfigurieren. DHCP lauscht standardmäßig auf demselben Port. Weitere Informationen finden Sie unter [Aspekte, wenn sich der Windows-Bereitstellungsdienst und DHCP auf demselben Server befinden](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#BKMK_WDSandDHCP).  

-   **Allow this distribution point to respond to incoming PXE requests** (Antwort auf eingehende PXE-Anforderungen durch diesen Verteilungspunkt zulassen): Gibt an, ob WDS aktiviert werden soll, sodass eingehende PXE-Dienstanforderungen beantwortet werden. Mithilfe dieses Kontrollkästchens können Sie den Dienst aktivieren oder deaktivieren, ohne die PXE-Funktionalität vom Verteilungspunkt zu entfernen.  

-   **Unterstützung für unbekannte Computer aktivieren:** Hiermit wird angegeben, ob die Unterstützung für Computer aktiviert werden soll, die nicht von Configuration Manager verwaltet werden. 

-   **Kennwort erforderlich, wenn PXE von Computern verwendet wird**: Geben Sie ein sicheres Kennwort an, um die Sicherheit für Ihre PXE-Bereitstellungen zusätzlich zu erhöhen.  

-   **Affinität zwischen Benutzer und Gerät**: Geben Sie an, wie bei PXE-Bereitstellungen die Zuordnung von Benutzern und Zielcomputer durch den Verteilungspunkt erfolgen soll. Wählen Sie eine der folgenden Optionen aus:  

    -   **Affinität zwischen Benutzer und Gerät mit automatischer Genehmigung zulassen**: Wählen Sie diese Einstellung aus, wenn Benutzer dem Zielcomputer automatisch zugeordnet werden sollen, ohne dass auf die Genehmigung gewartet wird.  

    -   **Affinität zwischen Benutzer und Gerät mit ausstehender Genehmigung durch den Administrator zulassen**: Wählen Sie diese Einstellung aus, wenn auf die Genehmigung eines Administrators gewartet werden soll, bevor Benutzer dem Zielcomputer zugeordnet werden.  

    -   **Affinität zwischen Benutzer und Gerät nicht zulassen**: Wählen Sie diese Einstellung aus, um anzugeben, dass Benutzer dem Zielcomputer nicht zugeordnet werden sollen.  

     Weitere Informationen zur Affinität zwischen Benutzer und Gerät finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät in System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   **Netzwerkschnittstellen**: Geben Sie an, ob vom Verteilungspunkt auf PXE-Anforderungen von allen oder nur von bestimmten Netzwerkschnittstellen geantwortet werden soll. Wenn nur auf PXE-Anforderungen von bestimmten Netzwerkschnittstellen geantwortet werden soll, müssen Sie die MAC-Adressen dieser Schnittstellen bereitstellen.  

-   **Reaktionsverzögerung für den PXE-Server (in Sekunden) angeben**: Gibt die Länge der Verzögerung (in Sekunden) an, bevor vom PXE-Verteilungspunkt auf Computeranforderungen reagiert wird, wenn mehrere für PXE aktivierte Verteilungspunkte verwendet werden. Standardmäßig reagiert der Configuration Manager-PXE-Dienstpunkt zunächst auf Netzwerk-PXE-Anforderungen.  

> [!NOTE]  
>  Sie können das PXE-Protokoll zum Starten von Betriebssystembereitstellungen für Configuration Manager-Clientcomputer verwenden. Configuration Manager verwendet die für PXE aktivierte Bereitstellungspunkt-Standortrolle zum Initiieren der Betriebssystembereitstellung. Der PXE-aktivierte Verteilungspunkt muss für Folgendes konfiguriert sein:
>
> 1. Antworten auf PXE-Boot-Anfragen, die von Configuration Manager-Clients im Netzwerk gestellt werden.
> 2. Interagieren mit der Configuration Manager-Infrastruktur zur Ermittlung der geeigneten Bereitstellungsaktionen.  

### <a name="multicast"></a>Multicast  
Geben Sie an, ob Multicast auf dem Verteilungspunkt aktiviert werden soll. Wenn Sie Multicast aktivieren, installiert Configuration Manager bei Bedarf die Windows-Bereitstellungsdienste (Windows Deployment Services, WDS) auf dem Server.  

Wenn Sie die Einstellung **Enable multicast to simultaneously send data to multiple clients** (Multicast aktivieren, um gleichzeitig Daten an mehrere Clients zu senden) aktivieren, konfigurieren Sie die folgenden Einstellungen:  

-   **Multicastverbindungskonto:** Geben Sie das Konto an, das verwendet werden soll, wenn Sie Configuration Manager-Datenbankverbindungen für Multicast konfigurieren.  

-   **Multicastadresseinstellungen**: Geben Sie die IP-Adressen an, die zum Senden von Daten an die Zielcomputer verwendet werden sollen. Standardmäßig wird die IP-Adresse von einem DHCP-Server vergeben, der für die Verteilung von Multicastadressen aktiviert ist. Je nach Netzwerkumgebung können Sie IP-Adressen im Bereich von 239.0.0.0 bis 239.255.255.255 angeben.  

    > [!IMPORTANT]  
    >  Die IP-Adressen, die Sie konfigurieren, müssen für die Zielcomputer, von denen das Betriebssystemabbild angefordert wird, zugänglich sein. Vergewissern Sie sich, dass Multicastdatenverkehr von Routern und Firewalls zwischen Zielcomputer und Standortserver zugelassen wird.  

-   **UDP-Portbereich für Multicasts**: Geben Sie den Bereich von UDP-Ports (User Datagram-Protokoll) zum Senden von Daten an die Zielcomputer an.  

    > [!IMPORTANT]  
    >  Die UDP-Ports müssen für die Zielcomputer, von denen das Betriebssystemabbild angefordert wird, zugänglich sein. Vergewissern Sie sich, dass Multicastdatenverkehr von Routern und Firewalls zwischen Zielcomputer und Standortserver zugelassen wird.  

-   **Clientübertragungsrate**: Wählen Sie die Clientübertragungsrate, die zum Herunterladen von Daten auf die Zielcomputer verwendet wird, aus.  

-   **Max. Anzahl von Clients**: Geben Sie die maximale Anzahl von Zielcomputern, von denen das Betriebssystem von diesem Verteilungspunkt heruntergeladen werden kann, an.  

-   **Geplanten Multicast aktivieren:** Geben Sie an, wie Configuration Manager die Startzeit der Bereitstellung des Betriebssystems für Zielcomputer steuert. Konfigurieren Sie die folgenden Optionen:  

    -   **Sitzungsstartverzögerung (Minuten):** Geben Sie an, wie viele Minuten Configuration Manager warten soll, bis auf die erste Bereitstellungsanfrage reagiert wird.  

    -   **Minimale Sitzungsgröße (Clients):** Geben Sie an, wie viele Anforderungen empfangen werden müssen, bevor Configuration Manager das Betriebssystem bereitstellt.  

> [!NOTE]  
>  Bei Multicastbereitstellungen wird die Netzwerkbandbreite beibehalten, indem gleichzeitig Daten an mehrere Configuration Manager-Clients gesendet werden, anstatt dass eine Kopie der Daten über eine separate Verbindung an jeden Client einzeln gesendet wird. Weitere Informationen zur Verwendung von Multicast zum Bereitstellen von Betriebssystemen finden Sie unter [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  



### <a name="group-relationships"></a>Gruppenbeziehungen  

> [!NOTE]  
>  Diese Optionen sind nur bei der Bearbeitung der Eigenschaften eines zuvor installierten Verteilungspunkts verfügbar.  

Verwalten Sie die Verteilungspunktgruppen, in denen dieser Verteilungspunkt Mitglied ist.  

Wählen Sie **Hinzufügen** aus, um diesen Verteilungspunkt einer vorhandenen Verteilungspunktgruppe als Mitglied hinzuzufügen. Wählen Sie eine vorhandene Verteilungspunktgruppe in der Liste des Dialogfelds **Zu Verteilungspunktgruppen hinzufügen** und dann **OK** aus.  

Wählen Sie eine Verteilungspunktgruppe in der Liste und dann **Entfernen** aus, um den Verteilungspunkt aus dieser Verteilungspunktgruppe zu entfernen.  

### <a name="content"></a>Content  

> [!NOTE]  
>  Diese Optionen sind nur bei der Bearbeitung der Eigenschaften eines zuvor installierten Verteilungspunkts verfügbar.  

Verwalten Sie den Inhalt, der an den Verteilungspunkt verteilt wurde. Im Abschnitt **Bereitstellungspakete** finden Sie eine Liste der Pakete, die an diesen Verteilungspunkt verteilt wurden. Sie können ein Paket aus der Liste auswählen und die folgenden Aktionen ausführen:  

-   **Überprüfen**: Hiermit starten Sie den Vorgang zum Überprüfen der Integrität der Inhaltsdateien im Paket. Zum Anzeigen der Ergebnisse der Inhaltsprüfung erweitern Sie im Arbeitsbereich **Überwachung** den Bereich **Verteilungsstatus** und wählen Sie den Knoten **Inhaltsstatus** aus.  

-   **Neu verteilen**: Hiermit kopieren Sie alle Inhaltsdateien im Paket an den Verteilungspunkt und überschreiben vorhandene Dateien. Normalerweise verwenden Sie diese Aktion, um Inhaltsdateien im Paket zu reparieren.  

-   **Entfernen**: Hiermit entfernen Sie die Inhaltsdateien für das Paket vom Verteilungspunkt.  

### <a name="content-validation"></a>Inhaltsprüfung  
Geben Sie an, ob ein Zeitplan für die Überprüfung der Integrität von Inhaltsdateien am Verteilungspunkt festgelegt werden soll. Wenn Sie die Inhaltsprüfung nach einem Zeitplan aktivieren, initiiert Configuration Manager den Vorgang zum festgesetzten Zeitpunkt, und am Verteilungspunkt werden alle Inhalte geprüft. Sie können auch die Priorität der Inhaltsprüfung konfigurieren. Standardmäßig ist die Priorität auf den Wert **Niedrigste (Standard)**festgelegt.  

Zum Anzeigen der Ergebnisse der Inhaltsprüfung erweitern Sie im Arbeitsbereich **Überwachung** den Bereich **Verteilungsstatus** und wählen Sie den Knoten **Inhaltsstatus** aus. Der Inhalt jedes Pakettyps (z. B. Anwendung, Softwareupdatepaket und Startabbild) wird angezeigt.  

> [!WARNING]  
>  Sie geben den Zeitplan für die Inhaltsprüfung zwar anhand der lokalen Zeit des Computers an, der Zeitplan wird in der Configuration Manager-Konsole jedoch anhand der UTC (Coordinated Universal Time, koordinierte Weltzeit) angezeigt.  

### <a name="boundary-group"></a>Begrenzungsgruppe  
Verwalten Sie die Begrenzungsgruppen, denen dieser Verteilungspunkt zugeordnet ist. Planen Sie, den Verteilungspunkt mindestens einer Begrenzungsgruppe hinzuzufügen. Bei der Inhaltsbereitstellung müssen sich die Clients in einer Begrenzungsgruppe befinden, die einem Verteilungspunkt zugeordnet ist, damit dieser Verteilungspunkt als Quellspeicherort für Inhalt verwendet werden kann.

Konfigurieren Sie *Beziehungen* für Begrenzungsgruppen, die definieren, wann und auf welche Begrenzungsgruppen ein Client ausweichen kann, um nach Inhalten zu suchen. Weitere Informationen finden Sie unter [Begrenzungsgruppen](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


### <a name="schedule"></a>Zeitplan  

> [!NOTE]  
>  Diese Optionen sind nur bei der Bearbeitung der Eigenschaften eines zuvor installierten Verteilungspunkts verfügbar.  

> [!TIP]  
>  Diese Registerkarte ist nur verfügbar, wenn Sie die Eigenschaften für einen Verteilungspunkt bearbeiten, der sich an einem vom Standortservercomputer entfernten Ort befindet.  

 Geben Sie an, ob ein Zeitplan konfiguriert werden soll, von dem die Datenübertragungszeiten von Configuration Manager an den Verteilungspunkt eingeschränkt werden.  

> [!IMPORTANT]  
>  Der Zeitplan basiert auf der Zeitzone des sendenden Standorts, nicht auf der des Verteilungspunkts.  

Wählen Sie das Zeitfenster und dann eine der folgenden Einschränkungen für **Verfügbarkeit** aus, um die Datenübertragungszeiten einzuschränken:  

-   **Offen für alle Prioritäten:** Gibt an, dass die Datenübertragung von Configuration Manager an den Verteilungspunkt uneingeschränkt erfolgt  

-   **Mittlere und hohe Priorität zulassen:** Gibt an, dass Configuration Manager nur Daten mit mittlerer und hoher Priorität an den Verteilungspunkt sendet.  

-   **Nur hohe Priorität zulassen:** Gibt an, dass Configuration Manager nur Daten mit hoher Priorität an den Verteilungspunkt sendet.  

-   **Geschlossen:** Gibt an, dass Configuration Manager keine Daten an den Verteilungspunkt sendet  

Sie können Daten nach Priorität einschränken oder die Verbindung für ausgewählte Zeiträume schließen.  

### <a name="rate-limits"></a>Begrenzung der Datenübertragungsrate  

> [!NOTE]  
>  Diese Optionen sind nur bei der Bearbeitung der Eigenschaften eines zuvor installierten Verteilungspunkts verfügbar.  

> [!TIP]  
>  Diese Registerkarte ist nur verfügbar, wenn Sie die Eigenschaften für einen Verteilungspunkt bearbeiten, der sich an einem vom Standortservercomputer entfernten Ort befindet.  

Geben Sie an, ob eine Begrenzung der Datenübertragungsrate konfiguriert werden soll, um die Netzwerkauslastung bei der Inhaltsübertragung durch Configuration Manager auf den Verteilungspunkt zu steuern. Sie können unter folgenden Optionen wählen:  

-   **Unbegrenzt beim Senden an dieses Ziel:** Gibt an, dass die Inhaltsübertragung von Configuration Manager an den Verteilungspunkt ohne Begrenzung der Datenübertragungsrate erfolgt.  

-   **Pulsmodus**: Gibt die Größe der Datenblöcke beim Senden an den Verteilungspunkt an. Sie können auch eine zeitliche Verzögerung zwischen dem Senden der einzelnen Datenblöcke angeben. Verwenden Sie diese Option, wenn Sie Daten über Netzwerke mit sehr niedriger Bandbreite an den Verteilungspunkt senden müssen. Dies kann beispielsweise der Fall sein, wenn eine Beschränkung vorliegt, dass unabhängig von der Geschwindigkeit der Verknüpfung oder deren Auslastung zu einem bestimmten Zeitpunkt nur alle fünf Sekunden 1 KB Daten gesendet werden dürfen.  

-   **Begrenzt auf angegebene maximale Übertragungsraten pro Stunde**: Geben Sie diese Einstellung an, damit die Datenübertragung auf einen Verteilungspunkt nur im konfigurierten Zeitanteil erfolgt. Wenn Sie diese Option verwenden, ermittelt Configuration Manager nicht die verfügbare Netzwerkbandbreite. Stattdessen wird die Zeit, innerhalb derer Daten gesendet werden können, aufgeteilt. Die Daten werden dann innerhalb eines kurzen Zeitblocks gesendet. In den darauffolgenden Zeitblöcken werden keine Daten gesendet. Wenn die Höchstrate beispielsweise auf **50 %**festgelegt ist, überträgt Configuration Manager die Daten für eine bestimmte Dauer, und für eine ebenso lange Dauer werden anschließend keine Daten übertragen. Die tatsächliche Datenmenge bzw. die Größe der Datenblöcke wird nicht verwaltet. Stattdessen wird nur die Dauer der Datenübertragung verwaltet.  
