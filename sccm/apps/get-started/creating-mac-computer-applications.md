---
title: "Erstellen von Anwendungen für Macintosh-Computer | System Center Configuration Manager"
description: "Erfahren Sie, was Sie beim Erstellen und Bereitstellen von Anwendungen für Macintosh-Computer berücksichtigen müssen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
caps.latest.revision: 9
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 98b36c58506bcb82fe82f842b8c3ed9dbd2a75d1


---
# <a name="create-mac-computer-applications-with-system-center-configuration-manager"></a>Erstellen von Anwendungen für Macintosh-Computer mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Zusätzlich zu den anderen System Center Configuration Manager-Anforderungen und -Verfahren zum Erstellen einer Anwendung müssen beim Erstellen und Bereitstellen von Anwendungen für Macintosh-Computer auch die folgenden Aspekte berücksichtigt werden.  

> [!IMPORTANT]  
>  Die Verfahren in diesem Thema enthalten Informationen zum Bereitstellen von Anwendungen auf Macintosh-Computern, auf denen Sie den Configuration Manager-Client installiert haben. Macintosh-Computer, die Sie bei Microsoft Intune registriert haben, unterstützen keine Anwendungsbereitstellung.  

## <a name="general-considerations"></a>Allgemeine Aspekte  
 Sie können System Center Configuration Manager nutzen, um Anwendungen auf Macintosh-Computern bereitzustellen, die den Configuration Manager-Client für Macintosh ausführen. Die Schritte zum Bereitstellen von Software auf Macintosh-Computern ähneln den Schritten zum Bereitstellen von Software auf Windows-Computern. Berücksichtigen Sie jedoch folgende Punkte, bevor Sie Anwendungen für Macintosh-Computer, die von Configuration Manager verwaltet werden, erstellen und bereitstellen:  
  
-   Bevor Sie Macintosh-Anwendungspakete auf Macintosh-Computern bereitstellen können, müssen Sie das Tool **CMAppUtil** auf einem Macintosh-Computer verwenden, um diese Anwendungen in ein Format zu konvertieren, das von Configuration Manager gelesen werden kann.  

-   Configuration Manager unterstützt die Bereitstellung von Macintosh-Anwendungen für Benutzer nicht. Diese Bereitstellungen müssen für ein Gerät erfolgen. Genauso gilt für die Bereitstellung von Macintosh-Anwendungen, dass Configuration Manager die Option **Software vorab auf dem primären Gerät des Benutzers bereitstellen** auf der Seite **Bereitstellungseinstellungen** des Assistenten zum Bereitstellen von Software nicht unterstützt.  

-   Simulierte Bereitstellungen werden von Macintosh-Anwendungen unterstützt.  

-   Anwendungen mit dem Zweck **Verfügbar**können auf Macintosh-Computern nicht bereitgestellt werden.  

-   Die Option zum Senden von Aktivierungspaketen beim Bereitstellen von Software wird für Macintosh-Computer nicht unterstützt.  

-   Background Intelligent Transfer Service (BITS) zum Herunterladen von Anwendungsinhalten wird von Macintosh-Computern nicht unterstützt. Treten beim Herunterladen einer Anwendung Fehler auf, wird der Download neu gestartet.  

-   Configuration Manager unterstützt globale Bedingungen nicht, wenn Sie Bereitstellungstypen für Macintosh-Computer erstellen.  

## <a name="steps-to-create-and-deploy-an-application"></a>Schritte zum Erstellen und Bereitstellen einer Anwendung  
 In der folgenden Tabelle finden Sie Schritte, Details und weitere Informationen zum Erstellen von Anwendungen für Macintosh-Computer.  

|Schritt|Details|  
|----------|-------------|  
|Schritt 1: Vorbereiten von Macintosh-Anwendungen für Configuration Manager|Bevor Sie Configuration Manager-Anwendungen von Macintosh-Softwarepaketen erstellen können, müssen Sie das Tool **CMAppUtil** auf einem Macintosh-Computer verwenden, um die Macintosh-Software in eine Configuration Manager **CMMAC**-Datei zu konvertieren.|  
|Schritt 2: Erstellen einer Configuration Manager-Anwendung, in der die Macintosh-Software enthalten ist|Verwenden Sie den Assistenten zum Erstellen von Anwendungen, um eine Anwendung für die Macintosh-Software zu erstellen.|  
|Schritt 3: Erstellen eines Bereitstellungstyps für die Macintosh-Anwendung|Dieser Schritt ist nur erforderlich, wenn diese Informationen nicht automatisch aus der Anwendung importiert wurden.|  
|Schritt 4: Bereitstellen der Macintosh-Anwendung|Verwenden Sie den Assistenten zum Bereitstellen von Software, um die Anwendung auf Macintosh-Computern bereitzustellen.|  
|Schritt 5: Überwachen der Bereitstellung von Macintosh-Anwendungen|Überwachen Sie den Erfolg der Bereitstellung von Anwendungen auf Macintosh-Computern.|  

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>Zusätzliche Verfahren zum Erstellen und Bereitstellen von Anwendungen für Macintosh-Computer  
 Gehen Sie wie folgt vor, um Anwendungen für Macintosh-Computer, die von Configuration Manager verwaltet werden, zu erstellen und bereitzustellen.  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>Schritt 1: Vorbereiten von Macintosh-Anwendungen für Configuration Manager  
 Die erforderlichen Schritte zum Erstellen und Bereitstellen von Configuration Manager-Anwendungen auf Macintosh-Computern ähneln dem Bereitstellungsprozess für Windows-Computer. Bevor Sie jedoch Configuration Manager-Anwendungen erstellen, die Macintosh-Bereitstellungstypen enthalten, müssen Sie die Anwendungen mit der Verwendung des Tools **CMAppUtil** vorbereiten. Dieses Tool wird mit den Macintosh-Clientinstallationsdateien heruntergeladen. Mit dem **CMAppUtil** -Tool können Informationen zur Anwendung erfasst werden, darunter Erkennungsdaten von folgenden Macintosh-Paketen:  

-   Apple Disc Image (.dmg)  

-   Meta Package-Datei (.mpkg)  

-   Mac OS X Installer-Paket (.pkg)  

-   Mac OS X-Anwendung (.app)  
  
Nach dem Erfassen von Anwendungsinformationen wird von **CMAppUtil** eine Datei mit der Erweiterung **.cmmac**erstellt. Diese Datei enthält die Installationsdateien für die Macintosh-Software und Informationen über Erkennungsmethoden, mit denen ermittelt werden kann, ob die Anwendung bereits installiert ist. Von**CMAppUtil** können auch **.dmg** -Dateien verarbeitet werden, die mehrere Macintosh-Anwendungen enthalten und mit denen pro Anwendung verschiedene Bereitstellungstypen erstellt werden.  
  
1.  Kopieren Sie das Macintosh-Softwareinstallationspaket in einen Ordner auf dem Macintosh-Computer, auf dem Sie den Inhalt der von der Microsoft Download Center-Website heruntergeladenen Datei **macclient.dmg** extrahiert haben.  

2.  Öffnen Sie auf diesem Macintosh-Computer ein Terminal-Fenster, und navigieren Sie zu dem Ordner, in dem Sie den Inhalt der **macclient.dmg** -Datei extrahiert haben.  

3.  Navigieren Sie zum Ordner **Tools** , und geben Sie die folgende Befehlszeile ein:  

     **./CMAppUtil** *<Eigenschaften\>*  

     Angenommen, Sie möchten den Inhalt einer im Desktop-Ordner des Benutzers gespeicherten Apple-Abbilddatei namens **MySoftware.dmg** in einer **cmmac** -Datei im selben Ordner speichern und **cmmac** -Dateien für alle in der Abbilddatei enthaltenen Anwendungen erstellen. Verwenden Sie dazu die folgende Befehlszeile:  

     **./CMApputil –c /Users/** *Benutzername\>* **/Desktop/MySoftware.dmg -o /Users/** *<Benutzername\>* **/Desktop -a**  

    > [!NOTE]  
    >  Der Anwendungsname darf nicht länger sein als 128 Zeichen.  

     Verwenden Sie zum Konfigurieren der Optionen für **CMAppUtil**die Befehlszeileneigenschaften aus der folgenden Tabelle:  

    |Eigenschaft|Weitere Informationen|  
    |--------------|----------------------|  
    |**-h**|Zeigt die verfügbaren Befehlszeileneigenschaften an.|  
    |**-r**|Gibt die **detection.xml** -Datei der angegebenen **.cmmac** -Datei in **stdout**aus. Die Ausgabe enthält die Erkennungsparameter und die Version von **CMAppUtil** , die zum Erstellen der **.cmmac** -Datei verwendet wurde.|  
    |**-c**|Gibt die zu konvertierende Quelldatei an.|  
    |**-o**|Diese Eigenschaft muss zusammen mit der Eigenschaft -c verwendet werden, um den Pfad für die Ausgabe anzugeben.|  
    |**-a**|Verwenden Sie diese Eigenschaft zusammen mit der Eigenschaft "–c" und der Datenträger-Imagedatei (**.dmg**), damit automatisch CMMAC-Dateien für alle Anwendungen und Pakete erstellt werden, die in der Datenträger-Imagedatei gefunden werden.|  
    |**-s**|Damit wird die Erstellung der **detection.xml** -Datei übersprungen, wenn keine Erkennungsparameter gefunden wurden, und die Erstellung der **.cmmac** -Datei ohne die **detection.xml** -Datei erzwungen.|  
    |**-v**|Zeigt eine ausführlichere Ausgabe aus dem **CMAppUtil** -Tool sowie Diagnoseinformationen an.|  

4.  Stellen Sie sicher, dass die **.cmmac** -Datei in dem angegebenen Ausgabeordner erstellt wurde.  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>Erstellen einer Configuration Manager-Anwendung, in der die Macintosh-Software enthalten ist  

Gehen Sie wie folgt vor, um eine Anwendung für Macintosh-Computer, die von Configuration Manager verwaltet werden, zu erstellen.  
  
1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen**.  
  
3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Anwendung erstellen**.  

4.  Wählen Sie auf der Registerkarte **Allgemein** des Assistenten zum Erstellen von Anwendungen die Option **Informationen zu dieser Anwendung automatisch anhand der Installationsdateien erkennen**aus.  

    > [!NOTE]  
    >  Wählen Sie die Option **Anwendungsinformationen manuell angeben** aus, wenn Sie selbst Informationen über die Anwendung angeben möchten. Weitere Informationen zum manuellen Angeben der Information finden Sie unter [Erstellen von Anwendungen mit System Center Configuration Manager](../../apps/deploy-use/create-applications.md).  

5.  Wählen Sie in der Dropdownliste **Typ** die Option **Mac OS X**aus.  

6.  Geben Sie im Feld **Speicherort** den UNC-Pfad zur Macintosh-Anwendungsinstallationsdatei (**CMMAC-Datei**) an, mit der die Anwendungsinformationen erkannt wird. Verwenden Sie dazu das Format *\\\\<Server\>\\<Freigabe\>\\<Dateiname\>*. Alternativ dazu können Sie auf **Durchsuchen** klicken und den Speicherort der Installationsdatei angeben.  

    > [!NOTE]  
    >  Sie benötigen Zugriff auf den UNC-Pfad mit der Anwendung.  

7.  Klicken Sie auf **Weiter**.  

8.  Überprüfen Sie auf der Seite **Informationen importieren** des Assistenten zum Erstellen von Anwendungen die importierten Informationen. Bei Bedarf können Sie auf **Zurück** klicken, um Fehler zu korrigieren. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  

9. Geben Sie auf der Seite **Allgemeine Informationen** des Assistenten zum Erstellen von Anwendungen Informationen zur Anwendung wie den Anwendungsnamen, Kommentare, die Version und eine optionale Referenz der Anwendung für die Configuration Manager-Konsole an.  

    > [!NOTE]  
    >  Einige Anwendungsinformationen sind auf dieser Seite möglicherweise schon vorhanden, wenn sie bereits aus den Anwendungsinstallationsdateien abgerufen wurden.  

10. Klicken Sie auf **Weiter**, überprüfen Sie auf der Seite **Zusammenfassung** die Anwendungsinformationen, und schließen Sie den Assistenten zum Erstellen von Anwendungen ab.  

11. Die neue Anwendung wird im Knoten **Anwendungen** der Configuration Manager-Konsole angezeigt.  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>Schritt 3: Erstellen eines Bereitstellungstyps für die Macintosh-Anwendung  
 Gehen Sie wie folgt vor, um einen Bereitstellungstyp für Macintosh-Computer, die von Configuration Manager verwaltet werden, zu erstellen.  

> [!NOTE]  
>  Wenn Sie mit dem Assistenten zum Erstellen von Anwendungen automatisch Informationen zur Anwendung importiert haben, wurde möglicherweise bereits ein Bereitstellungstyp für die Anwendung erstellt.  
  
1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen**.  
  
3.  Wählen Sie eine Anwendung aus, und klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Anwendung** auf **Bereitstellungstyp erstellen** , um einen neuen Bereitstellungstyp für diese Anwendung zu erstellen.  

    > [!NOTE]  
    >  Sie können den Assistenten zum Erstellen neuer Bereitstellungstypen auch über den Assistenten zum Erstellen von Anwendungen sowie über die Registerkarte **Bereitstellungstypen** im Dialogfeld **Eigenschaften** von *<Anwendungsname\>* starten.  

4.  Wählen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemein** in der Dropdownliste **Typ** den Eintrag **Mac OS X**aus.  

5.  Geben Sie im Feld **Speicherort** den UNC-Pfad zur Anwendungsinstallationsdatei (**CMMAC-Datei**) an. Verwenden Sie dazu das Format \\\\<Server\>\\<Freigabe\>\\<Dateiname\>. Alternativ dazu können Sie auf **Durchsuchen** klicken und den Speicherort der Installationsdatei angeben.  

    > [!NOTE]  
    >  Sie benötigen Zugriff auf den UNC-Pfad mit der Anwendung.  

6.  Klicken Sie auf **Weiter**.  

7.  Überprüfen Sie auf der Seite **Informationen importieren** des ** **Assistenten zum Erstellen neuer Bereitstellungstypen die importierten Informationen. Bei Bedarf können Sie auf **Zurück** klicken, um Fehler zu korrigieren. Klicken Sie zum Fortfahren auf Weiter.  

8.  Geben Sie auf der Seite **Allgemeine Informationen** des ** **Assistenten zum Erstellen neuer Bereitstellungstypen Informationen zur Anwendung an, beispielsweise Anwendungsname, Kommentare und die Sprachen, in denen dieser Bereitstellungstyp verfügbar sein soll.  

    > [!NOTE]  
    >  Einige Informationen zum Bereitstellungstyp sind auf dieser Seite möglicherweise schon vorhanden, wenn sie bereits aus den Anwendungsinstallationsdateien abgerufen wurden.  

9. Klicken Sie auf **Weiter**.  

10. Auf der Seite **Anforderungen** des Assistenten zum Erstellen neuer Bereitstellungstypen können Sie die Bedingungen angegeben, die erfüllt sein müssen, damit ein Bereitstellungstyp auf einem Macintosh-Computer installiert werden kann.  

11. Klicken Sie auf **Hinzufügen** , um das Dialogfeld **Anforderung erstellen** zu öffnen und eine neue Anforderung hinzuzufügen.  

    > [!NOTE]  
    >  Sie können neue Anforderungen auch im Dialogfeld **Eigenschaften** von *<Name des Bereitstellungstyps>\>* auf der Registerkarte **Anforderungen** hinzufügen.  

12. Wählen Sie in der Dropdownliste **Kategorie** aus, dass diese Anforderung für ein Gerät bestimmt ist.  

13. Wählen Sie in der Dropdownliste **Bedingung** die Bedingung aus, anhand derer bewertet werden soll, ob der Windows- bzw. der Macintosh-Computer den Installationsanforderungen entspricht. Der Inhalt dieser Liste ist von der ausgewählten Kategorie abhängig.  

14. Wählen Sie in der Dropdownliste **Operator** den Operator aus, der zum Vergleichen der ausgewählten Bedingung mit dem angegebenen Wert verwendet werden soll, um zu bewerten, ob der Benutzer bzw. das Gerät den Installationsanforderungen entspricht. Welche Operatoren verfügbar sind, ist von der ausgewählten Bedingung abhängig.  

15. Geben Sie im Feld **Wert** die Werte ein, die in Kombination mit der ausgewählten Bedingung und dem Operator verwendet werden sollen, um zu bewerten, ob der Benutzer bzw. das Gerät den Installationsanforderungen entspricht.  Welche Werte verfügbar sind, ist von der ausgewählten Bedingung und dem ausgewählten Operator abhängig.  

16. Klicken Sie auf **OK** , um die Anforderungsregel zu speichern und das Dialogfeld **Anforderung erstellen** zu schließen.  

17. Klicken Sie im ** ** Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Anforderungen**auf **Weiter**.  

18. Überprüfen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Zusammenfassung** die Aktionen, die von diesem Assistenten ** **ausgeführt werden sollen.  Bei Bedarf können Sie auf **Zurück** klicken, um die Einstellungen für den Bereitstellungstyp zu ändern. Klicken Sie auf **Weiter** , um den Bereitstellungstyp zu erstellen.  

19. Nachdem die Seite **Status** abgeschlossen ist, überprüfen Sie die ausgeführten Aktionen, und klicken Sie dann auf **Schließen**, um den **Assistenten zum Erstellen von Bereitstellungstypen** abzuschließen.  

20. Wenn dieser Assistent mit **Anwendungsassistent erstellen** gestartet wurde, wird jetzt die Seite **Bereitstellungstypen** angezeigt.  

###  <a name="deploy-the-mac-application"></a>Bereitstellen der Macintosh-Anwendung  
 Die Schritte zum Bereitstellen von Anwendungen auf Macintosh-Computern ähneln den Schritten zum Bereitstellen von Anwendungen auf Windows-Computern mit folgenden Ausnahmen:  

-   Die Bereitstellung von Anwendungen für Benutzer wird nicht unterstützt.  

-   Bereitstellungen mit dem Zweck **Verfügbar** werden nicht unterstützt.  

-   Die Option **Software vorab auf dem primären Gerät des Benutzers bereitstellen** auf der Seite **Bereitstellungseinstellungen** des Assistenten zum Bereitstellen von Software wird nicht unterstützt.  

-   Da das Softwarecenter von Macintosh-Computern nicht unterstützt wird, wird die Einstellung **Benutzerbenachrichtigungen** auf der Seite **Benutzerfreundlichkeit** des Assistenten zum Bereitstellen von Software ignoriert.  

-   Die Option zum Senden von Aktivierungspaketen beim Bereitstellen von Software wird für Macintosh-Computer nicht unterstützt.  

> [!NOTE]  
>  Sie können eine Sammlung erstellen, die ausschließlich Macintosh-Computer enthält. Erstellen Sie dazu eine Sammlung, von der eine Abfrageregel verwendet wird, und nutzen Sie eine beispielhafte WQL-Abfrage im Thema [Erstellen von Abfragen](../../core/servers/manage/create-queries.md).  
  
 Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](../../apps/deploy-use/deploy-applications.md).  
  
###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>Schritt 5: Überwachen der Bereitstellung von Macintosh-Anwendungen  
 Die Überwachung von Anwendungsbereitstellungen auf Macintosh-Computern kann auf dieselbe Weise erfolgen wie auf Windows-Computern.  

 Weitere Informationen finden Sie unter [Überprüfen von Anwendungen](/sccm/apps/deploy-use/monitor-applications-from-the-console).  



<!--HONumber=Nov16_HO1-->


