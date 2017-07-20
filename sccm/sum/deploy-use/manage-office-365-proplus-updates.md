---
title: Verwalten von Office 365 ProPlus-Updates | Microsoft-Dokumentation
description: "Configuration Manager synchronisiert Office 365-Clientupdates aus dem WSUS-Katalog auf den Standortserver, um Updates zur Bereitstellung für den Client zur Verfügung zu stellen."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 05/31/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.translationtype: Human Translation
ms.sourcegitcommit: dc221ddf547c43ab1f25ff83c3c9bb603297ece6
ms.openlocfilehash: 744bcb603a02bc7d237ffb3a7f925037b94a23ba
ms.contentlocale: de-de
ms.lasthandoff: 06/01/2017

---

# <a name="manage-office-365-proplus-with-configuration-manager"></a>Verwalten von Office 365 ProPlus mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Configuration Manager synchronisiert Office 365-Clientupdates und stellt sie zur Bereitstellung für Clients mit installiertem Office 365 zur Verfügung. Ab der Configuration Manager-Version 1610 können Sie Office 365-Clientinformationen aus dem Office 365-Clientverwaltungsdashboard überprüfen.

Ab Configuration Manager-Version 1602 kann Configuration Manager die Office 365-Clientupdates mithilfe des Workflow bei der Softwareupdateverwaltung verwalten. Wenn Microsoft ein neues Update für Office 365-Clients im Office Content Delivery Network (CDN) veröffentlicht, veröffentlicht Microsoft auch ein Updatepaket in Windows Server Update Services (WSUS). Nachdem Configuration Manager das Office 365-Clientupdate aus dem WSUS-Katalog auf den Standortserver übertragen hat, kann das Update für Clients bereitgestellt werden.

Ab Version 1702 können Sie den Office 365-Installer aus dem Office 365-Clientverwaltungsdashboard starten, um die erste Office 365-App-Installation einfacher zu machen. Mit dem Assistenten können Sie die Office 365-Installationseinstellungen konfigurieren, Dateien aus Office Content Delivery Networks (CDNs) herunterladen, und eine Skriptanwendung mit dem Inhalt erstellen und bereitstellen.

## <a name="office-365-client-management-dashboard"></a>Office 365-Clientverwaltungsdashboard  
Ab Version 1610 von Configuration Manager ist das Office 365-Clientverwaltungsdashboard in der Configuration Manager-Konsole verfügbar. Wechseln Sie zu **Softwarebibliothek** > **Übersicht** > **Office 365 Client Management** (Office 365-Clientverwaltung), um das Dashboard anzuzeigen.

Das Dashboard zeigt Diagramme für Folgendes an:

- Anzahl der Office 365-Clients
- Office 365-Clientversionen
- Office 365-Clientsprachen
- Office 365-Clientkanäle     
Weitere Informationen finden Sie unter [Übersicht über die Updatekanäle für Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

Verwenden Sie am oberen Rand des Dashboards die Dropdowneinstellung **Sammlung**, um die Dashboarddaten nach Mitgliedern einer bestimmten Sammlung zu filtern.

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Anzeigen von Daten im Office 365-Clientverwaltungsdashboard
Die im Office 365-Clientverwaltungsdashboard angezeigten Daten kommen aus der Hardwareinventur. Die Hardwareinventur muss aktiviert und die **Office 365 ProPlus Configurations**-Hardwareinventurklasse ausgewählt sein, damit die Daten im Dashboard angezeigt werden können.
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>So zeigen Sie Daten im Office 365-Clientverwaltungsdashboard an
1. Aktivieren Sie die Hardwareinventur, falls diese noch nicht aktiviert ist. Weitere Informationen finden Sie unter [Konfigurieren der Hardwareinventur](\sccm\core\clients\manage\configure-hardware-inventory).
2. Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  
3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  
4. Klicken Sie im Dialogfeld **Clientstandardeinstellungen** auf **Hardwareinventur**.  
5. Klicken Sie in der Liste **Geräteeinstellungen** auf **Klassen festlegen**.  
6. Im Dialogfeld der **Hardwareinventurklassen**wählen Sie **Office 365 ProPlus-Configurations** (Office 365 ProPlus-Konfigurationen) aus.  
7.  Klicken Sie auf **OK** , um die Änderungen zu speichern und das Dialogfeld **Hardwareinventurklassen** zu schließen.  
Das Office 365-Clientverwaltungsdashboard zeigt Daten dann an, während die Hardwareinventur ausgewertet wird.

## <a name="deploy-office-365-updates-with-configuration-manager"></a>Bereitstellen von Office 365-Updates mit Configuration Manager
Befolgen Sie die folgenden Schritte, um Office 365-Updates mit Configuration Manager bereitzustellen:

1.  [Überprüfen Sie die Anforderungen](https://technet.microsoft.com/library/mt628083.aspx) für die Verwendung von Configuration Manager zum Verwalten von Office 365-Client-Updates im Abschnitt **Anforderungen für die Verwendung von Configuration Manager zum Verwalten von Office 365-Clientupdates** des verlinkten Themas.  

2.  [Konfigurieren Sie Softwareupdatepunkte](../get-started/configure-classifications-and-products.md), um die Office 365-Clientupdates zu synchronisieren. Legen Sie als Klassifizierung **Updates** fest, und wählen Sie **Office 365-Client** als Produkt aus. Möglicherweise müssen Sie Softwareupdates mindestens einmal synchronisieren, bevor das Produkt „Office 365-Client“ Ihnen zur Auswahl steht. Nach dem Konfigurieren von Softwareupdatepunkten müssen Sie Softwareupdates synchronisieren, um die Klassifizierung **Updates** zu verwenden.
3.  Aktivieren Sie die Office 365-Clients, damit sie Updates von Configuration Manager erhalten können. Sie können dies mithilfe von Configuration Manager-Clienteinstellungen oder Gruppenrichtlinien tun. Verwenden Sie eine der nachfolgenden Methoden, um den Client zu aktivieren:  
    - Methode 1: Ab der Version 1606 von Configuration Manager können Sie die Configuration Manager-Clienteinstellung zum Verwalten des Office 365-Client-Agents nutzen. Nachdem Sie diese Einstellung konfiguriert und Updates für Office 365 bereitgestellt haben, kommuniziert der Configuration Manager-Client-Agent mit dem Office 365-Client-Agent, um Office 365-Updates von einem Verteilungspunkt herunterzuladen und zu installieren. Configuration Manager macht eine Bestandsaufnahme der Office 365 ProPlus-Clienteinstellungen.
      1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Übersicht** > **Clienteinstellungen**.  

      2.  Öffnen Sie die entsprechenden Geräteeinstellungen zum Aktivieren des Client-Agents. Weitere Informationen zu standardmäßigen und benutzerdefinierten Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Klicken Sie auf **Softwareupdates** und wählen Sie **Ja** für die Einstellung **Verwaltung des Office 365-Client-Agents aktivieren** aus.  

    - Methode 2: [Aktivieren Sie die Office 365-Clients, um Updates von Configuration Manager zu erhalten](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient), indem Sie das Office-Bereitstellungstool oder die Gruppenrichtlinie verwenden.  

4. [Stellen Sie für Clients Office 365-Updates bereit](deploy-software-updates.md).   

> [!Important]
> Wenn Sie über einen Office 365-Client mit mehreren Sprachen verfügen und Updates für weniger Sprachen herunterladen, werden die Updates nicht installiert. Nehmen wir z.B. an, Sie haben einen Office 365-Client mit en-US und de-DE. Auf dem Standortserver laden Sie nur den en-US-Inhalt für ein zutreffendes Office 365-Update herunter und stellen ihn bereit. Wenn der Benutzer die Installation für dieses Updates aus dem Softwarecenter startet, hängt das Update beim Herunterladen des Inhalts. Sie müssen Updates in der gleichen Sprache wie die Office 365-Clients herunterladen und bereitstellen.  


## <a name="add-other-languages-for-office-365-update-downloads"></a>Hinzufügen weiterer Sprachen für Downloads des Office 365-Updates
Ab Configuration Manager-Version 1610 können Sie Unterstützung für das Herunterladen von Updates für alle Sprachen hinzufügen, die von Office 365 unterstützt werden – unabhängig davon, ob sie in Configuration Manager unterstützt werden.
> [!IMPORTANT]  
> Das Konfigurieren zusätzlicher Sprachen für das Office 365-Update ist eine standortweite Einstellung. Nachdem Sie die Sprachen mithilfe des folgenden Verfahrens hinzugefügt haben, werden alle Office 365-Updates in diesen Sprachen sowie in den Sprachen heruntergeladen, die Sie auf der Seite „Sprachauswahl“ in den Assistenten „Softwareupdates herunterladen“ oder „Softwareupdates bereitstellen“ auswählen.

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>So fügen Sie Unterstützung für das Herunterladen von Updates für weitere Sprachen hinzu
Gehen Sie am Standort der zentralen Verwaltung oder an einem eigenständigen primären Standort, an dem die Standortsystemrolle „Softwareupdatepunkt“ installiert ist, folgendermaßen vor.
1. Geben Sie an der Eingabeaufforderung als Administrator den Befehl *wbemtest* ein, um das Testprogramm für die Windows-Verwaltungsinstrumentation zu öffnen.
2. Klicken Sie auf **Verbinden**, und geben Sie dann *root\sms\site_&lt;siteCode&gt;* ein.
3. Klicken Sie auf **Abfrage**, und führen Sie dann die folgende Abfrage aus: *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![WMI-Abfrage](..\media\1-wmiquery.png)
4. Doppelklicken Sie im Ergebnisbereich auf das Objekt mit dem Standortcode für den Standort der zentralen Verwaltung oder für den eigenständigen primären Standort.
5. Wählen Sie die **Props**-Eigenschaft, klicken Sie auf **Eigenschaft bearbeiten**, und klicken Sie dann auf **Eingebettet**.
![Eigenschaften-Editor](..\media\2-propeditor.png)
6. Beginnen Sie beim ersten Abfrageergebnis, und öffnen Sie jedes Objekt, bis Sie das Objekt finden, dessen **PropertyName**-Eigenschaft **AdditionalUpdateLanguagesForO365** lautet.
7. Wählen Sie **Value2**, und klicken Sie auf **Eigenschaft bearbeiten**.  
![Value2-Eigenschaft bearbeiten](..\media\3-queryresult.png)
8. Fügen Sie **Value2**-Eigenschaft zusätzliche Sprachen hinzu, und klicken Sie auf **Eigenschaft speichern**.  
Beispiel: pt-pt (Portugiesisch – Portugal) af-za (für Afrikaans – Südafrika), nn-no (für Norwegisch [Nynorsk] – Norwegen) usw.  
![Sprachen im Eigenschaften-Editor hinzufügen](..\media\4-props.png)  
9. Klicken Sie auf **Schließen**, klicken Sie auf **Schließen**, klicken Sie auf **Eigenschaft speichern**, klicken Sie auf **Objekt speichern** (wenn Sie hier auf **Schließen** klicken, werden die Werte verworfen), klicken Sie auf **Schließen**, und klicken Sie dann auf **Beenden**, um das Testprogramm für die Windows-Verwaltungsinstrumentation zu beenden.
10. Wechseln Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Übersicht** > **Office 365-Clientverwaltung** > **Office 365-Updates**.
11. Beim Herunterladen von Updates für Office 365 werden die Updates jetzt in der Sprache heruntergeladen, die Sie im Assistenten auswählen, und in den Sprachen, die Sie in diesem Verfahren konfiguriert haben. Um zu überprüfen, ob die Updates in diesen Sprachen heruntergeladen wurden, wechseln Sie zur Paketquelle für das Update, und suchen Sie nach Dateien mit dem Sprachcode im Dateinamen.  
![Dateinamen mit zusätzlichen Sprachen](..\media\5-verification.png)


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Ändern des Updatekanals nach dem Aktivieren des Erhalts von Updates für Office 365-Clients über Configuration Manager
Um den Updatekanal zu ändern, nachdem Sie Office 365-Clients den Erhalt von Updates von Configuration Manager ermöglicht haben, können Sie mithilfe von Gruppenrichtlinien die Änderung eines Registrierungsschlüsselwerts an Office 365-Clients verteilen. Ändern Sie den Registrierungsschlüssel **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** auf einen der folgenden Werte:

- Aktueller Kanal:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Verzögerter Kanal:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- Erstes Release für den aktuellen Kanal:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- Erstes Release für den verzögerten Kanal:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf

## <a name="deploy-office-365-apps"></a>Bereitstellen von Office 365-Apps  
Ab Version 1702 können Sie den Office 365-Installer aus dem Office 365-Clientverwaltungsdashboard starten, um die erste Office 365-App-Installation einfacher zu machen. Mit dem Assistenten können Sie die Office 365-Installationseinstellungen konfigurieren, Dateien aus Office Content Delivery Networks (CDNs) herunterladen, und eine Skriptanwendung für die Dateien erstellen und bereitstellen.

Dies ist besonders hilfreich, da Office 365-Updates für Clients ohne installiertes Office 365 nicht anwendbar sind. Vor der Version 1702 mussten Sie zum erstmaligen Installieren von Office 365-Apps auf Clients das Office 365-Bereitstellungstool (ODT) und die Office 365-Installationsquelldateien manuell herunterladen, einschließlich aller benötigten Sprachpakete, und Configuration.xml generieren, das die korrekte Office-Version und den korrekten Office-Kanal angibt. Anschließend müssen Sie entweder ein Legacypaket oder eine Skriptanwendung für Clients zur Installation der Office 365-Apps erstellen und bereitstellen.

> [!NOTE]
> - Der Computer, der den Office 365-Installer ausführt, muss über Internetzugriff verfügen.  
> - Der Benutzer, der den Office 365-Installer ausführt, muss über die Zugriffe **Lesen** und **Schreiben** auf der Freigabe für die im Assistenten bereitgestellten Inhaltsorte verfügen.
> - Wenn Sie einen 404-Downloadfehler erhalten, kopieren Sie die folgenden Dateien in den Benutzerorder %temp%:
>    - [releasehistory.xml](http://officecdn.microsoft.com.edgesuite.net/wsus/releasehistory.cab)
>    - [o365client_32bit.xml](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  
> - Nachdem Sie Office 365-Anwendungen mithilfe des Office 365-Installer erstellt und bereitgestellt haben, werden die Office-Updates von Configuration Manager nicht standardmäßig verwaltet. Damit Office 365-Clients Updates von Configuration Manager erhalten können, lesen Sie [Bereitstellen von Office 365-Updates mit Configuration Manager](#deploy-office-365-updates-with-configuration-manager).

### <a name="to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard"></a>Bereitstellen von Office 365-Apps für Clients aus dem Office 365-Clientverwaltungsdashboard
1. Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Übersicht** > **Office 365-Clientverwaltung**.
2. Klicken Sie im oberen rechten Bereich auf **Office 365-Installer**. Der Office 365-Installations-Assistent wird geöffnet.
3. Geben Sie auf der Seite **Anwendungseinstellungen** einen Namen und eine Beschreibung für die App an, geben Sie den Downloadpfad für die Dateien ein, und klicken Sie anschließend auf **Weiter**. Beachten Sie, dass der Pfad im folgenden Format angegeben sein muss: &#92;&#92;*Server*&#92;*Freigabe*.
4. Wählen Sie auf der Seite **Import Client Settings** (Clienteinstellungen importieren) aus, ob Sie die Office 365-Clienteinstellungen von einer vorhandenen XML-Konfigurationsdatei importieren oder die Einstellungen manuell angeben möchten, und klicken Sie anschließend auf **Weiter**.  

    Wenn Sie über eine vorhandene Konfigurationsdatei verfügen, geben Sie den Speicherort für die Datei an, und fahren Sie mit Schritt 7 fort. Beachten Sie, dass der Speicherort im folgenden Format angegeben werden muss: &#92;&#92;*Server*&#92;*Freigabe*&#92;*Dateiname*.XML.
    > [!IMPORTANT]    
    > Die XML-Konfigurationsdatei darf nur [vom Office 365 ProPlus-Client unterstützte Sprachen](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) enthalten.

5. Wählen Sie auf der Seite **Client Products** (Clientprodukte) die Office 365-Suite aus, die Sie verwenden, wählen Sie die Anwendungen aus, die Sie einschließen möchten, wählen Sie etwaige zusätzliche Office-Produkte aus, die enthalten sein sollen, und klicken Sie anschließend auf **Weiter**.
6. Wählen Sie auf der Seite **Clienteinstellungen** die einzuschließenden Einstellungen aus, und klicken Sie anschließend auf **Weiter**.
7. Wählen Sie auf der Seite **Bereitstellung** aus, ob die Anwendung bereitgestellt werden soll, und klicken Sie anschließend auf **Weiter**.  
Wenn Sie auswählen, das Paket nicht im Assistenten bereitzustellen, fahren Sie mit Schritt 9 fort.
8. Konfigurieren Sie die restlichen Seiten des Assistenten, wie Sie dies bei einer normalen Anwendungsbereitstellung tun würden. Weitere Informationen finden Sie unter [Erstellen und Bereitstellen einer Anwendung](/sccm/apps/get-started/create-and-deploy-an-application).
9. Schließen Sie den Assistenten ab.
10. Sie können die Anwendung über **Softwarebibliothek** > **Übersicht** > **Anwendungsverwaltung** > **Anwendungen** genauso bereitstellen und ändern, wie Sie dies bei jeder anderen Anwendung in Configuration Manager tun würden.   

> [!IMPORTANT]
> Die Office 365-App, die Sie mithilfe des Assistenten für Office 365-Anwendungen in Configuration Manager erstellen und bereitstellen, wird nicht automatisch von Configuration Manager verwaltet. Dies geschieht erst nach Aktivierung der Client-Agent-Einstellung für Softwareupdates **Verwaltung des Office 365-Client-Agents aktivieren**. Weitere Informationen finden Sie unter [Informationen zu Clienteinstellungen](/sccm/core/clients/deploy/about-client-settings).

>[!NOTE]
>Nach der Bereitstellung von Office 365-Apps können Sie Regeln zur automatischen Bereitstellung erstellen, um die Apps zu verwalten. Um eine Regel zur automatischen Bereitstellung für Office 365-Apps zu erstellen, klicken Sie auf **ADR erstellen** im Office 365-Clientverwaltungsdashboard, und wählen Sie **Office 365-Client** bei der Auswahl des Produkts aus. Weitere Informationen finden Sie unter [Automatically deploy software updates (Automatisches Bereitstellen von Softwareupdates)](/sccm/sum/deploy-use/automatically-deploy-software-updates).

<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->

