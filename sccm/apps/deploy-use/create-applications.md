---
title: Erstellen von Anwendungen
titleSuffix: Configuration Manager
description: Erstellen Sie Anwendungen mit Bereitstellungstypen, Erkennungsmethoden und Anforderungen für die Installation von Software.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9b90dfcc0916f62905af777e45222ceebf8300f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-applications-with-system-center-configuration-manager"></a>Erstellen von Anwendungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In einer Configuration Manager-Anwendung ist mindestens ein Bereitstellungstyp enthalten. Diese Bereitstellungstypen enthalten die Installationsdateien und Informationen, die für die Installation der Software auf Geräten erforderlich sind. Ein Bereitstellungstyp verfügt zudem über Regeln, wie z.B. Erkennungsmethoden und Anforderungen, die angeben, wann und wie der Client die Software installieren kann.  

 Es gibt die folgenden Möglichkeiten für die Erstellung von Anwendungen:  

-   Erstellen Sie die Anwendungen und Bereitstellungstypen durch Lesen der Installationsdateien der Anwendung automatisch.  

-   Erstellen Sie die Anwendung manuell, und fügen Sie Bereitstellungstypen später hinzu.  

-   Importieren Sie eine Anwendung aus einer Datei.  

> [!NOTE]  
>  Unter [Create applications for mobile devices](../../mdm/deploy-use/create-applications.md) (Erstellen von Anwendungen für mobile Geräte) erhalten Sie ausführliche Informationen zum Erstellen von Anwendungen für iOS, Windows Phone und Android.  



## <a name="start-the-create-application-wizard"></a>Starten des Assistenten zum Erstellen von Anwendungen  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Anwendung erstellen** aus.  



## <a name="specify-whether-you-want-to-automatically-detect-application-information-or-manually-define-the-information"></a>Geben Sie an, ob die Anwendungsinformationen automatisch erkannt oder manuell definiert werden sollen.  

-   Erkennen Sie automatisch Anwendungsinformationen für die Erstellung einer Basisanwendung mit einem einzigen Bereitstellungstyp. Beispiel: eine Windows Installer-Datei ohne Abhängigkeiten oder Anforderungen. Wenn Sie mithilfe dieses Verfahrens eine Anwendung erstellt haben, können Sie diese nach Bedarf bearbeiten, um Bereitstellungstypen hinzuzufügen oder zu ändern und um Erkennungsmethoden, Abhängigkeiten oder Anforderungen hinzuzufügen.  

-   Geben Sie Anwendungsinformationen manuell an, um komplexere Anwendungen mit mehreren Bereitstellungstypen, Abhängigkeiten, Erkennungsmethoden oder Anforderungen zu erstellen.  

### <a name="automatically-detect-application-information"></a>Automatische Erkennung von Anwendungsinformationen  

1.  Wählen Sie auf der Registerkarte **Allgemein** des Assistenten zum Erstellen von Anwendungen die Option **Informationen zu dieser Anwendung automatisch anhand der Installationsdateien erkennen**aus.  

2.  Wählen Sie in der Dropdownliste **Typ** den Installationsdateityp der Anwendung aus, den Sie für die automatische Erkennung verwenden möchten. Informationen zu den verfügbaren Installationstypen finden Sie unter [Von Configuration Manager unterstützte Bereitstellungstypen](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager) in diesem Thema.  

3.  Geben Sie im Feld **Speicherort** den UNC-Pfad im Format *\\\\server\\freigabe\\\dateiname* oder den Store-Link zur Anwendungsinstallationsdatei an, die Sie zur Erkennung von Anwendungsinformationen verwenden möchten. Alternativ dazu können Sie auf **Durchsuchen** klicken, um zur Installationsdatei zu navigieren.  

    > [!IMPORTANT]  
    >  Wenn Sie als Anwendungstyp **Windows Installer (\*MSI-Datei)** auswählen, werden alle Dateien im angegebenen Ordner importiert und an Verteilungspunkte gesendet. Vergewissern Sie sich, dass der angegebene Ordner ausschließlich Dateien enthält, die zur Installation der Anwendung erforderlich sind. Configuration Manager wird getestet, um bis zu 20.000 Anwendungsdateien im Anwendungspaket zu unterstützen. Wenn Ihre Anwendung mehr Dateien enthält, sollten Sie mehrere Anwendungen mit jeweils geringerer Anzahl Dateien erstellen.  

    >  Sie benötigen Zugriff auf den UNC-Pfad mit der Anwendung sowie auf alle Unterordner mit Anwendungsinhalten.  

4.  Überprüfen Sie die importierten Informationen auf der Seite **Informationen importieren** des Assistenten zum Erstellen von Anwendungen, und wählen Sie anschließend **Weiter** aus. Bei Bedarf können Sie **Zurück** auswählen, um Fehler zu korrigieren.  

5.  Geben Sie auf der Seite **Allgemeine Informationen** des Assistenten zum Erstellen von Anwendungen die folgenden Informationen an:  

    > [!NOTE]  
    >  Wenn Configuration Manager diese Informationen aus den Anwendungsinstallationsdateien automatisch erkennt, wird er bereits hier aufgefüllt. Zudem werden je nach erstelltem Anwendungstyp möglicherweise unterschiedliche Optionen angezeigt.  

    -   Allgemeine Informationen zur Anwendung, z.B. Anwendungsname, Kommentare und Version. Geben Sie eine optionale Referenz an, damit Sie die Anwendung in der Configuration Manager-Konsole finden.  

    -   **Installationsprogramm**: Geben Sie das Installationsprogramm und alle zur Installation des Bereitstellungstyps der Anwendung erforderlichen Eigenschaften an.  

        > [!TIP]  
        >  Wenn das Installationsprogramm nicht angezeigt wird, wählen Sie **Durchsuchen** aus, um auf den Speicherort des Installationsprogramms zuzugreifen.  

    -   **Installationsverhalten**: Geben Sie an, ob der Anwendungsbereitstellungstyp nur für den aktuell angemeldeten Benutzer oder für alle Benutzer installiert werden soll. Eine dritte Möglichkeit besteht darin, den Bereitstellungstyp für alle Benutzer zu installieren, wenn er für ein Gerät bereitgestellt wird, oder für einen bestimmten Benutzer, wenn er für einen Benutzer bereitgestellt wird.  

    -   **Automatische VPN-Verbindung verwenden (sofern konfiguriert)**: Wenn ein VPN-Profil auf dem Gerät bereitgestellt wurde, auf dem die App gestartet wird, starten Sie die VPN-Verbindung, wenn die App gestartet wird (nur Windows 8.1 und Windows Phone 8.1).  

         Auf Geräten mit Windows Phone 8.1 werden automatische VPN-Verbindungen nicht unterstützt, wenn mehrere VPN-Profile auf dem Gerät bereitgestellt wurden.  

         Weitere Informationen finden Sie unter [VPN-Profile](../../protect/deploy-use/vpn-profiles.md).  

6.  Wählen Sie **Weiter** aus, überprüfen Sie die Anwendungsinformationen auf der Seite **Zusammenfassung**, und schließen Sie den Assistenten zum Erstellen von Anwendungen ab.  

Die neue Anwendung wird im Knoten **Anwendungen** der Configuration Manager-Konsole angezeigt. Sie haben den Erstellungsvorgang einer Anwendung abgeschlossen. Wenn Sie der Anwendung weitere Bereitstellungstypen hinzufügen möchten, finden Sie weitere Informationen unter [Bereitstellungstypen für die Anwendung erstellen](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) in diesem Thema.  

### <a name="manually-specify-application-information"></a>Manuelles Angeben von Anwendungsinformationen  

1.  Wählen Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Anwendungen die Option **Anwendungsinformationen manuell angeben** aus, und wählen Sie anschließend **Weiter** aus.  

2.  Geben Sie allgemeine Informationen zur Anwendung an, z.B. Anwendungsname, Kommentare und Version. Geben Sie eine optionale Referenz an, damit Sie die Anwendung in der Configuration Manager-Konsole finden.  

3.  Geben Sie auf der Seite **Anwendungskatalog** des Assistenten zum Erstellen von Anwendungen die folgenden Informationen an:  

    -   **Ausgewählte Sprache**: Wählen Sie in der Dropdownliste die Sprachversion der einzurichtenden Anwendung aus. Wählen Sie **Hinzufügen/Entfernen** aus, um weitere Sprachen für diese Anwendung zu konfigurieren.  

    -   **Lokalisierter Anwendungsname**: Geben Sie den Namen der Anwendung in der Sprache an, die Sie in der Dropdownliste **Ausgewählte Sprache** ausgewählt haben.  

        > [!IMPORTANT]  
        >  Sie müssen für jede Sprachversion, die eingerichtet werden soll, einen lokalisierten Anwendungsnamen angeben.  

    -   **Benutzerkategorien**: Wählen Sie **Bearbeiten** aus, um Anwendungskategorien in der Sprache anzugeben, die Sie in der Dropdownliste **Ausgewählte Sprache** ausgewählt haben. Benutzer des Softwarecenters können diese ausgewählten Kategorien verwenden, um die verfügbaren Anwendungen zu filtern und zu sortieren.  

    -   **Benutzerdokumentation**: Wählen Sie **Durchsuchen** aus, um den Speicherort einer Datei anzugeben, in der Softwarecenter-Benutzer weitere Informationen zu dieser Anwendung erhalten. Bei diesem Speicherort handelt es sich um eine URL oder einen Netzwerkpfad und Dateinamen.

    -   **Linktext**: Geben Sie den Text an, der anstelle der URL für die Anwendung angezeigt wird.  

    -   **URL der Datenschutzrichtlinien für die Anwendung**: Geben Sie eine URL an, unter der die Datenschutzerklärung für die Anwendung verknüpft ist.  

    -   **Lokalisierte Beschreibung**: Geben Sie eine Beschreibung der Anwendung in der Sprache an, die Sie in der Dropdownliste **Ausgewählte Sprache** ausgewählt haben.  

    -   **Schlüsselwörter**: Geben Sie eine Liste mit Schlüsselwörtern in der Sprache an, die Sie in der Dropdownliste **Ausgewählte Sprache** ausgewählt haben. Mithilfe dieser Schlüsselwörter können Softwarecenter-Benutzer nach der Anwendung suchen.  

    -   **Symbol**: Wählen Sie **Durchsuchen** aus, um aus den verfügbaren Symbolen ein Symbol für diese Anwendung auszuwählen. Wenn Sie kein Symbol angeben, wird für die Anwendung ein Standardsymbol verwendet. Sie können nun Symbole mit bis zu 512 x 512 Pixel darstellen.

    -   **Display this as a featured app and highlight it in the company portal** (Als ausgewählte App anzeigen und im Unternehmensportal hervorheben): Mit dieser Option wird die App im Unternehmensportal hervorgehoben angezeigt.  

4.  Wählen Sie auf der Seite **Bereitstellungstypen** des Assistenten zum Erstellen von Anwendungen **Hinzufügen** aus, um einen neuen Bereitstellungstyp zu erstellen.  

 Weitere Informationen finden Sie unter [Bereitstellungstypen für die Anwendung erstellen](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) in diesem Thema.  

5.  Wählen Sie **Weiter** aus, überprüfen Sie die Anwendungsinformationen auf der Seite **Zusammenfassung**, und schließen Sie den Assistenten zum Erstellen von Anwendungen ab.  

Die neue Anwendung wird im Knoten **Anwendungen** der Configuration Manager-Konsole angezeigt.  



##  <a name="create-deployment-types-for-the-application"></a>Bereitstellungstypen für die Anwendung erstellen  
 Wenn Sie Anwendungsinformationen automatisch erkennen, müssen Sie einige der Schritte in diesem Verfahren möglicherweise nicht durchführen.  

### <a name="start-the-create-deployment-type-wizard"></a>Starten des Assistenten zum Erstellen neuer Bereitstellungstypen  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen** aus.  

3.  Wählen Sie eine Anwendung aus, und wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Anwendung** **Bereitstellungstyp erstellen** aus.  

> [!TIP]  
>  Sie können den Assistenten zum Erstellen neuer Bereitstellungstypen auch über den Assistenten zum Erstellen von Anwendungen sowie über die Registerkarte **Bereitstellungstypen** im Dialogfeld *<Anwendungsname\>* **Eigenschaften** starten.  

### <a name="specify-whether-you-want-to-automatically-detect-deployment-type-information-or-manually-set-up-the-information"></a>Angeben, ob die Informationen zum Bereitstellungstyp automatisch erkannt oder manuell eingerichtet werden sollen  
 Wenden Sie eines der folgenden Verfahren an, um Informationen zum Bereitstellungstyp automatisch zu erkennen oder manuell einzurichten.  

#### <a name="automatically-detect-deployment-type-information"></a>Automatisches Erkennen der Informationen zum Bereitstellungstyp  

1.  Wählen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemein** die Option **Informationen zu diesem Bereitstellungstyp automatisch den Installationsdateien entnehmen** aus.  

2.  Wählen Sie im Feld **Typ** den Installationsdateityp der Anwendung aus, den Sie zur Erkennung der Informationen zum Bereitstellungstyp verwenden möchten.  

3.  Geben Sie im Feld **Speicherort** den Netzwerkpfad oder den Store-Link zu den Anwendungsinstallationsdateien an. Configuration Manager erkennt anhand dieser Dateien die Informationen zum Bereitstellungstyp. Sie können auch **Durchsuchen** auswählen, um die Installationsdatei zu suchen.  

    > [!NOTE]  
    >  Sie benötigen Zugriff auf den Netzwerkpfad mit der Anwendung sowie auf alle Unterordner mit Anwendungsinhalten.  

4.  Überprüfen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Informationen importieren** die importierten Informationen, und wählen Sie anschließend **Weiter** aus. Sie können auch **Zurück** auswählen, um zurückzugehen und mögliche Fehler zu beheben.  

5.  Geben Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemeine Informationen** die folgenden Informationen an:  

    > [!NOTE]  
    >  Einige Informationen zum Bereitstellungstyp können schon vorhanden sein, wenn sie aus den Anwendungsinstallationsdateien gelesen wurden. Zudem werden je nach erstelltem Bereitstellungstyp möglicherweise unterschiedliche Optionen angezeigt.  

    -   Allgemeine Informationen zum Bereitstellungstyp, darunter Name, Administratorkommentare und verfügbare Sprachen.  

    -   **Installationsprogramm**: Geben Sie das Installationsprogramm und alle zur Installation des Bereitstellungstyps erforderlichen Eigenschaften an.  

    -   **Installationsverhalten**: Geben Sie an, ob der Bereitstellungstyp für den gegenwärtig angemeldeten Benutzer oder für alle Benutzer installiert werden soll. Eine dritte Möglichkeit besteht darin, den Bereitstellungstyp für alle Benutzer zu installieren, wenn er für ein Gerät bereitgestellt wird, oder für einen bestimmten Benutzer, wenn er für einen Benutzer bereitgestellt wird.  

    -   **Automatische VPN-Verbindung verwenden (sofern konfiguriert)**: Wenn ein VPN-Profil auf dem Gerät bereitgestellt wurde, auf dem die App gestartet wird, starten Sie die VPN-Verbindung, wenn die App gestartet wird (nur Windows 8.1 und Windows Phone 8.1). Wenn mehrere VPN-Profile auf einem Windows 8.1-Gerät bereitgestellt wurden, wird standardmäßig das erste bereitgestellte VPN-Profil verwendet.  

         Auf Geräten mit Windows Phone 8.1 werden automatische VPN-Verbindungen nicht unterstützt, wenn mehrere VPN-Profile auf dem Gerät bereitgestellt wurden.  

         Weitere Informationen finden Sie unter [VPN-Profile](../../protect/deploy-use/vpn-profiles.md).  

6.  Wählen Sie **Weiter** aus, und fahren Sie mit [Specify content options for the deployment type](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type) (Angeben von Inhaltsoptionen für den Bereitstellungstyp) fort.  

#### <a name="manually-set-up-the-deployment-type-information"></a>Manuelles Einrichten der Informationen zum Bereitstellungstyp  

1.  Wählen Sie auf der Seite **Allgemein** des Assistenten zum Erstellen neuer Bereitstellungstypen in der Dropdownliste **Typ** den Typ der Anwendungsinstallationsdateien für diesen Bereitstellungstyp aus. 

2.  Wählen Sie **Informationen zum Bereitstellungstyp manuell angeben** aus, und klicken Sie anschließend auf **Weiter**.

3.  Geben Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemeine Informationen** einen Namen für den Bereitstellungstyp an. Geben Sie optional eine Beschreibung und die Sprachen für diesen Bereitstellungstyp an, und klicken Sie anschließend auf **Weiter**.  

4.  Fahren Sie mit [Angeben von Inhaltsoptionen für den Bereitstellungstyp](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type) fort.  

###  <a name="specify-content-options-for-the-deployment-type"></a>Angeben von Inhaltsoptionen für den Bereitstellungstyp  

1.  Geben Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Inhalt** die folgenden Informationen an:  

    -   **Inhaltsort**: Geben Sie den Speicherort des Inhalts für diesen Bereitstellungstyp an, oder klicken Sie auf **Durchsuchen**, um den Inhaltsordner für den Bereitstellungstyp auszuwählen.  

        > [!IMPORTANT]  
        >  Das Systemkonto des Standortservercomputers muss zum Zugriff auf den angegebenen Inhaltsort berechtigt sein.  

    -   **Einstellungen für zu deinstallierenden Inhalt**: Geben Sie eine der folgenden Optionen an:
        - **Übereinstimmend mit zu installierendem Inhalt**: Wählen Sie diese Option aus, wenn die Inhalte für die Installation und die Deinstallation identisch sind. Dies ist die Standardoption.
        - **Nicht zu deinstallierender Inhalt**: Wählen Sie diese Option aus, wenn Ihre Anwendung für die Deinstallation keine Inhalte benötigt.
        - **Abweichend von zu installierendem Inhalt**: Wählen Sie diese Option aus, wenn die für die Deinstallation benötigten Inhalten von den Inhalten für die Installation abweichen. Geben Sie anschließend den Speicherort des Anwendungsinhalts an, der für die Deinstallation der Anwendung verwendet wird.
5. Klicken Sie auf **OK**, um das Dialogfeld zu Bereitstellungstyp-Eigenschaften zu schließen.

    -   **Inhalt dauerhaft in Clientcache speichern**: Mit dieser Option geben Sie an, ob der Inhalt im Cache des Clients dauerhaft beibehalten werden soll. Der Client behält den Inhalt selbst dann bei, wenn die App bereits installiert wurde. Diese Option ist bei einigen Bereitstellungen nützlich, z.B. bei Windows Installer-basierter Software. Windows Installer benötigt eine lokale Kopie des Quellinhalts für die Anwendung von Updates. Dies ist der Fall, auch wenn der verfügbare Cachespeicher durch diese Option verringert wird. Wenn Sie diese Option auswählen, kann es bei einer umfangreichen Bereitstellung im späteren Verlauf zu einem Fehler kommen, falls der Cache nicht über ausreichend Speicherplatz verfügt.  

    -   **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen**: Wählen Sie diese Option aus, um die Netzwerkauslastung zu reduzieren. Clients laden Inhalte von anderen lokalen Clients im Netzwerk herunter, von denen die Inhalte bereits heruntergeladen und zwischengespeichert wurden. Diese Option nutzt Windows BranchCache-Technologie.  

    -   **Installationsprogramm**: Geben Sie den Namen des Installationsprogramms und alle erforderlichen Installationsparameter an, oder wählen Sie **Durchsuchen** aus, um den Speicherort der Installationsdatei zu suchen.  

    -   **Installationsstart in**: Geben Sie optional den Ordner an, in dem sich das Installationsprogramm für den Bereitstellungstyp befindet. Dabei kann es sich um einen absoluten Pfad auf dem Client oder um einen Pfad zum Verteilungspunktordner handeln, in dem sich die Installationsdateien befinden.  

    -   **Deinstallationsprogramm**: Geben Sie bei Bedarf den Namen des Deinstallationsprogramms und alle erforderlichen Parameter an, oder klicken Sie auf **Durchsuchen**, um den Speicherort zu suchen.  

    -   **Deinstallationsstart in**: Geben Sie optional den Ordner an, in dem sich das Deinstallationsprogramm für den Bereitstellungstyp befindet. Dieser Ordner kann ein absoluter Pfad auf dem Client sein. Es kann auch ein relativer Pfad auf einem Verteilungspunkt des Ordners mit dem Paket sein.  

    -   **Installationsprogramm ausführen und Programm als 32-Bit-Prozess auf 64-Bit-Clients deinstallieren**: Verwenden Sie die 32-Bit-Dateipfade und 32-Bit-Registrierungspfade auf Windows-Computern zum Ausführen des Installationsprogramms für den Bereitstellungstyp.  

2.  Wählen Sie **Weiter** aus.  

### <a name="set-up-detection-methods-to-indicate-the-presence-of-the-deployment-type-windows-pcs-only"></a>Einrichten von Methoden zum Erkennen vorhandener Bereitstellungstypen (nur Windows-PCs)  
 Mit dem folgenden Verfahren richten Sie eine Erkennungsmethode ein, durch die angegeben wird, ob der Bereitstellungstyp bereits installiert ist.  

1.  Wählen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Erkennungsmethode** die Option **Regeln konfigurieren, um zu erkennen, ob dieser Bereitstellungstyp vorhanden ist** aus. Wählen Sie anschließend **Klausel hinzufügen** aus.  

    > [!NOTE]  
    >  Sie können auch **Mithilfe eines benutzerdefinierten Skripts erkennen, ob dieser Bereitstellungstyp vorhanden ist** auswählen. Weitere Informationen finden Sie unter [Use a custom script to check for the presence of a deployment type (So erkennen Sie einen vorhandenen Bereitstellungstyp mithilfe eines benutzerdefinierten Skripts)](/sccm/apps/deploy-use/create-applications#Use-a-custom-script-to-check-for-the-presence-of-a-deployment-type).  

2.  Wählen Sie im Dialogfeld **Erkennungsregel** in der Dropdownliste **Einstellungstyp** die Methode aus, die Sie zum Erkennen des Vorhandenseins des Bereitstellungstyps verwenden möchten. Folgende Methoden stehen zur Auswahl:  

    -   **Dateisystem**: Erkennt, ob eine angegebene Datei oder ein angegebener Ordner auf einem Clientgerät vorhanden ist. Diese Erkennung zeigt an, dass die Anwendung installiert ist.  

        > [!NOTE]  
        >  Die Angabe eines UNC-Pfads zu einer Netzwerkfreigabe im Feld „Pfad“ wird vom Einstellungstyp **Dateisystem** nicht unterstützt. Sie können nur einen lokalen Pfad auf dem Clientgerät angeben.  
        >   
        >  Wählen Sie die Option **Diese Datei/dieser Ordner ist einer 32-Bit-Anwendung auf 64-Bit-Systemen zugeordnet** aus, um die angegebene Datei bzw. den angegebenen Order zuerst an 32-Bit-Speicherorten zu suchen. Wenn die Datei bzw. der Ordner nicht gefunden wird, werden die 64-Bit-Speicherorte durchsucht.  

    -   **Registrierung**: Erkennt, ob ein angegebener Registrierungsschlüssel oder Registrierungswert auf einem Clientgerät vorhanden ist. Diese Erkennung zeigt an, dass die Anwendung installiert ist.  

        > [!NOTE]  
        >  Wählen Sie die Option **Dieser Registrierungsschlüssel ist mit einer 32-Bit-Anwendung auf 64-Bit-Systemen verknüpft** aus, um den angegebenen Registrierungsschlüssel zuerst in 32-Bit-Registrierungspfaden zu suchen. Wenn der Registrierungsschlüssel nicht gefunden wird, werden 64-Bit-Pfade durchsucht.  

    -   **Windows Installer**: Erkennt, ob eine angegebene Windows Installer-Datei auf einem Clientgerät vorhanden ist. Diese Erkennung zeigt an, dass die Anwendung installiert ist.  

3.  Geben Sie Details zu dem Element an, anhand dessen erkannt werden soll, ob dieser Bereitstellungstyp installiert ist. Beispielsweise können Sie eine Datei, einen Ordner, einen Registrierungsschlüssel oder -wert oder einen Windows Installer-Produktcode verwenden.  

4.  Geben Sie an, ob das Element vorhanden sein oder eine Regel erfüllen muss. Wählen Sie beispielsweise bei der Erkennung anhand einer Datei die Option **The file system setting must exist on the target system to indicate presence of this application** (Die Dateisystemeinstellung muss auf dem Zielsystem vorhanden sein, um das Vorhandensein dieser Anwendung anzuzeigen) aus.  

5.  Wählen Sie **Weiter** aus, um das Dialogfeld **Erkennungsregel** zu schließen.  

####  <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a>Verwenden eines benutzerdefinierten Skripts zum Überprüfen eines vorhandenen Bereitstellungstyps  

1.  Aktivieren Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Erkennungsmethode** das Kontrollkästchen **Mithilfe eines benutzerdefinierten Skripts erkennen, ob dieser Bereitstellungstyp vorhanden ist**, und wählen Sie dann**Bearbeiten** aus.  

2.  Wählen Sie im Dialogfeld **Skript-Editor** in der Dropdownliste **Skripttyp** die Skriptsprache aus, die Sie zum Erkennen des Bereitstellungstyps verwenden möchten.  

3.  Geben Sie das gewünschte Skript in das Feld **Skriptinhalte** ein. Sie können auch den Inhalt eines vorhandenen Skripts in dieses Feld einfügen oder **Öffnen** auswählen, um ein vorhandenes gespeichertes Skript zu suchen. Configuration Manager überprüft die Ergebnisse des Skripts. Es liest die Werte, die vom Skript in den Standardausgabestream (STDOUT), den Standardfehlerstream (STDERR) und den Exitcode geschrieben wurden. Wenn das Skript mit einem Wert ungleich 0 (null) beendet wird, schlägt das Skript fehl und der Erkennungszustand der Anwendung ist unbekannt. Wenn der Exitcode gleich null ist und in „STDOUT“-Daten enthalten sind, ist der Erkennungszustand der Anwendung „Installiert“.  

 Überprüfen Sie anhand der folgenden Tabelle, ob eine Anwendung über die Ausgabe eines Skripts installiert wurde:  

|Exitcode des Skripts|Details|
|--------------------------------|-----------------|
|0|**Aus „STDOUT“ gelesene Daten**: Leer<br /><br /> **Aus „STDERR“ gelesene Daten**: Leer<br /><br /> **Skriptergebnis**: Erfolgreich<br /><br /> **Erkennungszustand der Anwendung**: Nicht installiert|  
|0|**Aus „STDOUT“ gelesene Daten**: Leer<br /><br /> **Aus „STDERR“ gelesene Daten**: Nicht leer<br /><br /> **Skriptergebnis**: Fehler<br /><br /> **Erkennungszustand der Anwendung**: Unbekannt|  
|0|**Aus „STDOUT“ gelesene Daten**: Nicht leer<br /><br /> **Aus „STDERR“ gelesene Daten**: Leer<br /><br /> **Skriptergebnis**: Erfolgreich<br /><br /> **Erkennungszustand der Anwendung**: Installiert|  
|0|**Aus „STDOUT“ gelesene Daten**: Nicht leer<br /><br /> **Aus „STDERR“ gelesene Daten**: Nicht leer<br /><br /> **Skriptergebnis**: Erfolgreich<br /><br /> **Erkennungszustand der Anwendung**: Installiert|  
|Wert ungleich null|**Aus „STDOUT“ gelesene Daten**: Leer<br /><br /> **Aus „STDERR“ gelesene Daten**: Leer<br /><br /> **Skriptergebnis**: Fehler<br /><br /> **Erkennungszustand der Anwendung**: Unbekannt|  
|Wert ungleich null|**Aus „STDOUT“ gelesene Daten**: Leer<br /><br /> **Aus „STDERR“ gelesene Daten**: Nicht leer<br /><br /> **Skriptergebnis**: Fehler<br /><br /> **Erkennungszustand der Anwendung**: Unbekannt|  
|Wert ungleich null|**Aus „STDOUT“ gelesene Daten**: Nicht leer<br /><br /> **Aus „STDERR“ gelesene Daten**: Leer<br /><br /> **Skriptergebnis**: Fehler<br /><br /> **Erkennungszustand der Anwendung**: Unbekannt|  
|Wert ungleich null|**Aus „STDOUT“ gelesene Daten**: Nicht leer<br /><br /> **Aus „STDERR“ gelesene Daten**: Nicht leer<br /><br /> **Skriptergebnis**: Fehler<br /><br /> **Erkennungszustand der Anwendung**: Unbekannt|  

In der folgenden Tabelle sind Beispielskripte für Microsoft Visual Basic (VB) aufgeführt, mit deren Hilfe Sie eigene Skripte für die Anwendungserkennung schreiben können.  

|Visual Basic-Beispielskript|Beschreibung|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|Vom Skript wird ein Exitcode ungleich null zurückgegeben, was darauf hindeutet, dass es nicht erfolgreich ausgeführt werden konnte. In diesem Fall ist der Erkennungszustand der Anwendung Unbekannt.|  
|**WScript.StdErr.Write "Script failed"**<br /><br /> **WScript.Quit(0)**|Das Skript gibt einen Exitcode von 0 (null) zurück, aber der Wert für „STDERR“ ist nicht leer. Dieses Ergebnis gibt an, dass das Skript nicht erfolgreich ausgeführt werden konnte. In diesem Fall ist der Erkennungszustand der Anwendung Unbekannt.|  
|**WScript.Quit(0)**|Vom Skript wird ein Exitcode gleich null zurückgegeben, was darauf hindeutet, dass es erfolgreich ausgeführt wurde. Der Wert für „STDOUT“ ist jedoch leer, was darauf hindeutet, dass die Anwendung nicht installiert ist.|  
|**WScript.StdOut.Write "The application is installed"**<br /><br /> **WScript.Quit(0)**|Vom Skript wird ein Exitcode gleich null zurückgegeben, was darauf hindeutet, dass es erfolgreich ausgeführt wurde. Der Wert für „STDOUT“ ist nicht leer, was darauf hindeutet, dass die Anwendung installiert ist.|  
|**WScript.StdOut.Write "The application is installed"**<br /><br /> **WScript.StdErr.Write "Completed"**<br /><br /> **WScript.Quit(0)**|Vom Skript wird ein Exitcode gleich null zurückgegeben, was darauf hindeutet, dass es erfolgreich ausgeführt wurde. Die Werte für „STDOUT“ und „STDERR“ sind nicht leer, was darauf hindeutet, dass die Anwendung installiert ist.|  

 > [!NOTE]  
 >  Die maximal zulässige Größe für ein Skript beträgt 32 KB.  

4.  Wählen Sie **OK** aus, um das Dialogfeld **Skript-Editor** zu schließen.  

### <a name="specify-user-experience-options-for-the-deployment-type"></a>Angeben von Optionen für die Benutzerfreundlichkeit des Bereitstellungstyps  
 Durch diese Einstellungen wird angegeben, wie der Client die Anwendung auf Geräten installiert und was dem Benutzer angezeigt wird.  

1.  Geben Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Benutzerfreundlichkeit** die folgenden Informationen an:  

    -   **Installationsverhalten**: Wählen Sie in der Dropdownliste eine der folgenden Optionen aus:  

        -   **Für Benutzer installieren**: Die Anwendung wird nur für den Benutzer installiert, für den sie bereitgestellt wird.  

        -   **Für System installieren**: Die Anwendung wird nur einmal installiert und ist für alle Benutzer verfügbar.  

        -   **Für System installieren, wenn Ressource ein Gerät ist; andernfalls für Benutzer installieren**: Wenn die Anwendung auf einem Gerät bereitgestellt wird, wird sie für alle Benutzer installiert. Wenn die Anwendung für einen Benutzer bereitgestellt wird, installiert der Client sie nur für diesen Benutzer.  

    -   **Anmeldeanforderung**: Geben Sie die Anmeldeanforderungen für diesen Bereitstellungstyp anhand der folgenden Optionen an:  

        -   **Nur wenn ein Benutzer angemeldet ist**  

        -   **Unabhängig von Benutzeranmeldung**  

        -   **Nur wenn kein Benutzer angemeldet ist**  

        > [!NOTE]  
        >  Diese Option ist standardmäßig auf **Nur wenn ein Benutzer angemeldet ist** festgelegt. Wenn Sie in der Dropdownliste **Installationsverhalten** die Option **Für Benutzer installieren** auswählen, können Sie diese Option nicht ändern.  

    -   **Sichtbarkeit des Installationsprogramms**: Gibt den Modus an, in dem der Bereitstellungstyp auf Clientgeräten ausgeführt wird. Die folgenden Optionen sind verfügbar:  

        -   **Maximiert**: Der Bereitstellungstyp wird auf Clientgeräten im maximierten Modus ausgeführt. Benutzer sehen alle Installationsaktivitäten.  

        -   **Normal**: Der Bereitstellungstyp wird basierend auf den Standardeinstellungen des Systems und Programms im normalen Modus ausgeführt. Dies ist der Standardmodus.  

        -   **Minimiert**: Der Bereitstellungstyp wird auf Clientgeräten im minimierten Modus ausgeführt. Benutzer können die Installationsaktivität möglicherweise im Infobereich oder in der Taskleiste sehen.  

        -   **Ausgeblendet**: Der Bereitstellungstyp wird ausgeblendet auf Clientgeräten ausgeführt. Benutzer sehen keine Installationsaktivitäten.  

    -   **Benutzern gestatten, die Programminstallation anzuzeigen und mit ihr zu interagieren**: Gibt an, ob ein Benutzer bei der Installation des Bereitstellungstyps die Installationsoptionen einrichten darf.  

        > [!NOTE]  
        >  Diese Option ist standardmäßig aktiviert, wenn in der Dropdownliste **Installationsverhalten** die Option **Für Benutzer installieren** ausgewählt wurde.  

        > [!IMPORTANT]
        > Ab Version 1802 ist diese Einstellung optional, wenn Sie das Verhalten **Für System installieren** auswählen. Diese Änderung dient primär dazu, dass einem Benutzer während einer Tasksequenz die Interaktion mit der Installation erlaubt wird. Führen Sie beispielsweise einen Setupvorgang aus, der den Endbenutzer nach verschiedenen Optionen befragt. Einige Anwendungsinstallationsprogramme können Eingabeaufforderungen an Benutzer nicht deaktivieren, oder der Installationsprozess fordert bestimmte Konfigurationswerte an, die nur dem Benutzer bekannt sind. <!--1356976-->
        > 
        > Eine Installation im Systemkontext und das Zulassen einer Benutzerinteraktion mit der Installation stellt keine sichere Konfiguration dar. Weitere Informationen finden Sie unter [Security and privacy for cloud management gateway (Sicherheit und Datenschutz für das Cloudverwaltungsgateway)](/sccm/apps/plan-design/security-and-privacy-for-application-management#bkmk_interact).

    -   **Maximal zulässige Laufzeit (Minuten)**: Hiermit wird die maximal zulässige Zeit für die Ausführung des Programms auf dem Clientcomputer angegeben. Sie können für diese Einstellung eine ganze Zahl größer oder gleich Null angeben. Die Standardeinstellung ist 120 Minuten.  

         Dieser Wert wird verwendet:  

        -   Überwachen Sie die Ergebnisse des Bereitstellungstyps.  

        -   Überprüfen Sie, ob ein Bereitstellungstyp installiert wird, wenn auf Clientgeräten Wartungsfenster definiert wurden. Wenn ein Wartungsfenster vorhanden ist, wird ein Programm nur dann gestartet, wenn die verbleibende Dauer des Wartungsfensters noch mindestens der Einstellung unter **Maximal zulässige Laufzeit** entspricht.  

        > [!IMPORTANT]  
        >  Wenn der Zeitraum für **Maximal zulässige Laufzeit** länger ist als das geplante Wartungsfenster, kann dies zu einem Problem führen. Wird die maximale Laufzeit vom Benutzer auf einen Wert festgelegt, der die Länge der verfügbaren Wartungsfenster überschreitet, wird dieser Bereitstellungstyp nicht ausgeführt.  

    -   **Geschätzte Installationszeit (Minuten)**: Geben Sie an, wie lange die Installation des Bereitstellungstyps voraussichtlich dauert. Benutzern wird diese Zeit im Softwarecenter angezeigt.  

    -   **Angeben des spezifischen Neustartverhaltens**: Geben Sie an, welche Aktion nach der Installation durchgeführt werden soll. Die folgenden Optionen sind verfügbar:  

        -   **Bestimmen des Verhaltens basierend auf Rückgabecodes:** Handhaben von Neustarts basierend auf den Codes, die auf der Registerkarte „Rückgabecodes“ konfiguriert werden. Das Softwarecenter zeigt **Möglicherweise ist ein Neustart notwendig** an. Wenn ein Benutzer während der Installation angemeldet ist, erhält er, je nach den Einstellungen zur Benutzerfreundlichkeit der Bereitstellung, eine Aufforderung.  

        -   **Keine bestimmte Aktion:** Es ist kein Neustart nach der Installation erforderlich. Das Softwarecenter meldet, dass kein Neustart erforderlich ist.  
        -   **Das Installationsprogramm der Software erzwingt möglicherweise einen Neustart des Geräts:** Configuration Manager steuert oder startet keinen Neustart, bei der tatsächlichen Installation geschieht dies jedoch möglicherweise ohne Warnung. Verwenden Sie diese Einstellung, um zu verhindern, dass Configuration Manager Installationsfehler meldet, wenn das Installationsprogramm einen Neustart initiiert. Das Softwarecenter zeigt **Möglicherweise ist ein Neustart notwendig** an.  

        -   **Configuration Manager-Client erzwingt einen verbindlichen Geräteneustart**: Configuration Manager erzwingt nach erfolgreicher Installation einen Neustart des Geräts. Das Softwarecenter meldet, dass ein Neustart erforderlich ist. Wenn ein Benutzer während der Installation angemeldet ist, erhält er, je nach den Einstellungen zur Benutzerfreundlichkeit der Bereitstellung, eine Aufforderung.

### <a name="specify-requirements-for-the-deployment-type"></a>Angeben von Anforderungen für den Bereitstellungstyp  

1.  Wählen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Anforderungen** **Hinzufügen** aus, um das Dialogfeld **Anforderung erstellen** zu öffnen und eine neue Anforderung hinzuzufügen.  

    > [!NOTE]  
    >  Sie können neue Anforderungen auch im Dialogfeld **Eigenschaften** von *<Name des Bereitstellungstyps\>* auf der Registerkarte **Anforderungen** hinzufügen.  

2.  Wählen Sie in der Dropdownliste **Kategorie** aus, ob diese Anforderung für ein Gerät oder einen Benutzer bestimmt ist. Wählen Sie **Benutzerdefiniert** aus, wenn eine zuvor erstellte globale Bedingung verwendet werden soll. Bei Auswahl von **Benutzerdefiniert** können Sie auch **Erstellen** auswählen, um eine neue globale Bedingung zu erstellen. Weitere Informationen über globale Bedingungen finden Sie unter [Erstellen von globalen Bedingungen](../../apps/deploy-use/create-global-conditions.md).  

    > [!IMPORTANT]  
    >  Der Client ignoriert sämtliche Anforderungen der Kategorie **Benutzer** mit der Bedingung **Primäres Gerät**, wenn Sie die Anwendung für eine Gerätesammlung bereitstellen.  
    >   
    >  Wenn Sie System Center 2012 R2 Configuration Manager SP1 für die Erstellung eines Windows-Pakets und -Programms oder einer Tasksequenz mit Windows 10 als Anforderung verwendet haben und anschließend ein Upgrade auf System Center Configuration Manager ausführen, werden die Anforderungen für Windows 10 möglicherweise entfernt. Um dieses Problem zu beheben, geben Sie die Anforderungen erneut an. Die Anforderung wird auf Geräten weiterhin ordnungsgemäß verarbeitet, obwohl sie aus der Anforderungsanzeige entfernt wurde.  

3.  Wählen Sie in der Dropdownliste **Bedingung** die Bedingung aus, anhand derer bewertet werden soll, ob der Benutzer bzw. das Gerät den Installationsanforderungen entspricht. Die Inhalte dieser Liste sind von der ausgewählten Kategorie abhängig.  

4.  Wählen Sie aus der Dropdownliste **Operator** den zu verwendenden Operator aus. Dieser Operator vergleicht die ausgewählte Bedingung mit dem angegebenen Wert. Er bewertet, ob der Benutzer bzw. das Gerät die Installationsanforderungen erfüllt. Welche Operatoren verfügbar sind, ist von der ausgewählten Bedingung abhängig.  

    > [!IMPORTANT]  
    >  Die verfügbaren Anforderungen variieren je nach Gerätetyp, die der Bereitstellungstyp verwendet.  

5.  Geben Sie im Feld **Wert** die zu verwendenden Werte an. Diese Werte werden, zusammen mit der ausgewählten Bedingung und dem Operator, verwendet, um zu bewerten, ob der Benutzer bzw. das Gerät die Installationsanforderungen erfüllt. Welche Werte verfügbar sind, hängt von der ausgewählten Bedingung und dem ausgewählten Operator ab.  

6.  Wählen Sie **OK** aus, um die Anforderung zu speichern und das Dialogfeld **Anforderung erstellen** zu schließen.  

### <a name="specify-dependencies-for-the-deployment-type"></a>Angeben von Abhängigkeiten für den Bereitstellungstyp  
 Mit Abhängigkeiten wird mindestens ein Bereitstellungstyp einer anderen Anwendung definiert, der installiert sein muss, bevor ein Bereitstellungstyp installiert wird. Sie können die abhängigen Bereitstellungstypen einrichten, die vor der Installation eines Bereitstellungstyps automatisch installiert werden.  

> [!IMPORTANT]  
>  In einigen Fällen ist ein Bereitstellungstyp von einem Bereitstellungstyp abhängig, der ebenfalls über Abhängigkeiten verfügt. Die maximale Anzahl unterstützter Abhängigkeiten in der Kette beträgt fünf.  

1.  Wählen Sie auf der Seite **Abhängigkeiten** des Assistenten zum Erstellen neuer Bereitstellungstypen die Option **Hinzufügen** aus.  

    > [!IMPORTANT]  
    >  Sie können neue Abhängigkeiten auch im Dialogfeld *<Name des Bereitstellungstyps\>***Eigenschaften** auf der Registerkarte **Abhängigkeiten** hinzufügen.  

2.  Wählen Sie im Dialogfeld **Abhängigkeit hinzufügen** **Hinzufügen** aus.  

3.  Wählen Sie im Dialogfeld **Erforderliche Anwendung angeben** eine vorhandene Anwendung aus sowie einen der Anwendungsbereitstellungstypen, der als Abhängigkeit verwendet werden soll.  

    > [!TIP]  
    >  Sie können **Anzeigen** auswählen, um die Eigenschaften der ausgewählten Anwendung bzw. des ausgewählten Bereitstellungstyps anzuzeigen.  

4.  Wählen Sie **OK** aus, um das Dialogfeld **Erforderliche Anwendung angeben** zu schließen.  

5.  Wenn eine abhängige Anwendung automatisch installiert werden soll, aktivieren Sie das Kontrollkästchen **Automatisch installieren** neben der abhängigen Anwendung.  

    > [!NOTE]  
    >  Eine abhängige Anwendung muss nicht bereitgestellt werden, damit sie automatisch installiert werden kann.  

6.  Geben Sie im Dialogfeld **Abhängigkeit hinzufügen** unter **Name der Abhängigkeitsgruppe** einen Namen für diese Gruppe von Anwendungsabhängigkeiten ein.  

7.  Verwenden Sie optional die Schaltflächen **Priorität erhöhen** und **Priorität verringern**. Diese Aktionen ändern die Reihenfolge, in welcher der Client die einzelnen Abhängigkeiten bewertet.  

8.  Wählen Sie **OK** aus, um das Dialogfeld **Abhängigkeit hinzufügen** zu schließen.  

### <a name="confirm-the-deployment-type-settings-and-finish-the-wizard"></a>Bestätigen der Bereitstellungstypeinstellungen und Abschließen des Assistenten  

1.  Überprüfen Sie die **Zusammenfassung**. Wählen Sie **Weiter** aus, um den Bereitstellungstyp zu erstellen. Wählen Sie **Zurück** aus, um die Einstellungen für den Bereitstellungstyp zu ändern.  

2.  Nachdem die Seite **Fortschritt** geschlossen wurde, überprüfen Sie die ausgeführten Aktionen. Wählen Sie anschließend **Schließen** aus, um den Assistenten abzuschließen.  

3.  Wenn der Assistent zum Erstellen neuer Bereitstellungstypen aus dem Assistenten zum Erstellen von Anwendungen heraus gestartet wurde, wird nun wieder die Seite **Bereitstellungstypen** des Assistenten zum Erstellen von Anwendungen angezeigt.  



## <a name="set-up-additional-options-for-deployment-types-that-contain-virtual-applications"></a>Einrichten zusätzlicher Optionen für Bereitstellungstypen, die virtuelle Anwendungen enthalten  
 Wenden Sie die folgenden Verfahren an, um zusätzliche Optionen für Bereitstellungstypen einzurichten, die virtuelle Anwendungen enthalten.  

### <a name="set-up-content-options-for-application-virtualization-app-v-deployment-types"></a>Einrichten von Inhaltsoptionen für Application Virtualization-Bereitstellungstypen (App-V)  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungen** aus.  

2.  Wählen Sie in der Liste **Anwendungen** eine Anwendung aus, die über ein App-V-Bereitstellungstyp verfügt. Wählen Sie anschließend auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

3.  Wählen Sie im Dialogfeld Eigenschaften von *<Anwendungsname\>* **Properties** auf der Registerkarte **Bereitstellungstypen** einen App-V-Bereitstellungstyp aus, und wählen Sie dann **Bearbeiten** aus.  

4.  Konfigurieren Sie im Dialogfeld *<Name des Bereitstellungstyps\>* **Eigenschaften** auf der Registerkarte **Inhalt** bei Bedarf die folgenden Optionen:  

    -   **Inhalt dauerhaft in Clientcache speichern:** Wählen Sie diese Option aus, um sicherzustellen, dass die Inhalte für diesen Bereitstellungstyp nicht aus dem Configuration Manager-Clientcache gelöscht werden.  

    -   **Inhalt vor dem Start in den App-V-Cache laden**: Bei Auswahl dieser Option werden alle Inhalte für die virtuelle Anwendung vor dem Starten der Anwendung in den App-V-Cache geladen. Zudem wird mit dieser Option sichergestellt, dass der Anwendungsinhalt nicht im Cache fixiert wird. Der Client löscht den Inhalt nach Bedarf.  

5.  Wählen Sie **OK** aus, um das Dialogfeld *<Name des Bereitstellungstyps\>* **Eigenschaften** zu schließen.  

6.  Wählen Sie **OK** aus, um das Dialogfeld **Eigenschaften von** *<Anwendungsname\>* zu schließen.  

### <a name="set-up-publishing-options-for-app-v-deployment-types"></a>Einrichten von Veröffentlichungsoptionen für App-V-Bereitstellungstypen  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungen** aus.  

3.  Wählen Sie in der Liste **Anwendungen** eine Anwendung aus, die über ein App-V-Bereitstellungstyp verfügt. Wählen Sie anschließend auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

4.  Wählen Sie im Dialogfeld Eigenschaften von *<Anwendungsname\>* **Properties** auf der Registerkarte **Bereitstellungstypen** einen App-V-Bereitstellungstyp aus, und wählen Sie dann **Bearbeiten** aus.  

5.  Wählen Sie im Dialogfeld **Eigenschaften** von *<Name des Bereitstellungstyps\>* auf der Registerkarte **Veröffentlichung** die Elemente in der virtuellen Anwendung aus, die veröffentlicht werden sollen.  

6.  Wählen Sie **OK** aus, um das Dialogfeld *<Name des Bereitstellungstyps\>* **Eigenschaften** zu schließen.  

7.  Wählen Sie **OK** aus, um das Dialogfeld **Eigenschaften von** *<Anwendungsname\>* zu schließen.  



## <a name="import-an-application"></a>Importieren einer Anwendung  
 Gehen Sie wie folgt vor, um eine Anwendung in Configuration Manager zu importieren. Informationen zum Exportieren von Anwendungen finden Sie unter [Management tasks for System Center Configuration Manager applications (Verwaltungsaufgaben für System Center Configuration Manager-Anwendungen)](../../apps/deploy-use/management-tasks-applications.md).  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen** aus.   

3.  Wählen Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** **Anwendung importieren** aus.  

4.  Wählen Sie auf der Seite **Allgemein** des **Assistenten zum Importieren von Anwendungen** die Option **Durchsuchen** aus. Geben Sie anschließend einen Netzwerkpfad zur ZIP-Datei mit der zu importierenden Anwendung an.  

5.  Wählen Sie auf der Seite **Dateiinhalt** die Aktion aus, die ausgeführt werden soll, wenn die zu importierende Anwendung das Duplikat einer vorhandenen Anwendung ist. Sie können eine neue Anwendung erstellen, oder das Duplikat ignorieren, und eine neue Revision zur vorhandenen Anwendung hinzufügen.  

6.  Überprüfen Sie auf der Seite **Zusammenfassung** die durchzuführenden Aktionen, und schließen Sie dann den Assistenten ab.  

 Die neue Anwendung wird im Knoten **Anwendungen** angezeigt.  

> [!TIP]  
>  Das Windows PowerShell-Cmdlet **Import-CMApplication** hat die gleiche Funktion wie dieses Verfahren. Weitere Informationen finden Sie unter [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  



##  <a name="deployment-types-supported-by-configuration-manager"></a>Von Configuration Manager unterstützte Bereitstellungstypen  

|Name des Bereitstellungstyps|Weitere Informationen|  
|--------------------------|----------------------|  
|**Windows Installer (\*msi-Datei)**|Hiermit wird ein Bereitstellungstyp aus einer Windows Installer-Datei erstellt.|  
|**Windows-App-Paket (\*.appx, \*.appxbundle)**|Erstellt einen Bereitstellungstyp für Windows 8 oder höher. Wählen Sie eine Windows-App-Paketdatei oder ein gebündeltes Windows-App-Paket aus.|  
|**Windows-App-Paket (im Windows Store)**|Erstellt einen Bereitstellungstyp für Windows 8 oder höher. Geben Sie einen Link zur App im Windows Store an, oder durchsuchen Sie den Store, um die App auszuwählen.<br /><br /> Konfigurieren Sie die Gruppenrichtlinieneinstellung **Store-Anwendung deaktivieren** auf **Deaktiviert** oder **Nicht konfiguriert**, um die App als Link zum Windows Store bereitzustellen. Wenn diese Einstellung aktiviert ist, können Clients keine Verbindung mit dem Windows Store zum Herunterladen und Installieren von Anwendungen herstellen.<br /><br /> Windows 8-Bereitstellungstypen, bei denen ein Link zu einem Store verwendet wird, werden unabhängig von ihrer Priorität immer vor anderen Bereitstellungstypen ausgewertet.|  
|**Skriptinstallationsprogramm**|Hiermit wird ein Bereitstellungstyp erstellt, in dem ein Skript angegeben wird. Dieses Skript wird auf Clientgeräten ausgeführt und dient zur Installation von Inhalten oder zur Ausführung einer Aktion.|  
|**Microsoft Application Virtualization 4**|Erstellt einen Bereitstellungstyp aus einem Microsoft Application Virtualization 4-Manifest.|  
|**Microsoft Application Virtualization 5**|Hiermit wird ein Bereitstellungstyp aus einer Microsoft Application Virtualization 5-Paketdatei erstellt.|  
|**Windows Phone-App-Paket (\*.xap-Datei)**|Hiermit wird ein Bereitstellungstyp aus einer Windows Phone-App-Paketdatei erstellt.|  
|**Windows Phone-App-Paket (in Windows Phone Store)**|Erstellt einen Bereitstellungstyp, indem ein Link zur App im Windows Phone-Store angegeben wird.|  
|**App-Paket für iOS (\*.ipa-Datei)**|Hiermit wird ein Bereitstellungstyp aus einer iOS-App-Paketdatei erstellt.|  
|**App-Paket für iOS aus App Store**|Hiermit wird ein Bereitstellungstyp erstellt, indem ein Link zur iOS-App im App Store angegeben wird.|  
|**App-Paket für Android (\*.apk-Datei)**|Hiermit wird ein Bereitstellungstyp aus einer Android-App-Paketdatei erstellt.|  
|**App-Paket für Android auf Google Play**|Hiermit wird ein Bereitstellungstyp erstellt, indem ein Link zur App auf Google Play angegeben wird.|  
|**Mac OS X**|Hiermit wird ein Bereitstellungstyp für Macintosh-Computer aus einer CMMAC-Datei erstellt, die Sie mit dem Tool „CMAppUtil“ erstellt haben.<br /><br /> Gilt nur für Mac-Computer, auf denen der Configuration Manager-Client ausgeführt wird.|  
|**Webanwendung**|Hiermit wird ein Bereitstellungstyp erstellt, der einen Link zu einer Webanwendung angibt. Mit dem Bereitstellungstyp wird auf dem Gerät des Benutzers eine Verknüpfung mit der Webanwendung installiert.<br /><br /> Wenn Sie den verwalteten Microsoft Intune-Browser auf iOS- oder Android-Geräten installiert haben, sollten Sie sicherstellen, dass Benutzer den verwalteten Browser nur zum Öffnen der App verwenden können. Geben Sie den Link zur App in einem der folgenden Formate an, und ersetzen Sie dabei **http:** durch **http-intunemam:** oder **https:** durch **https-intunemam:**<br /><br /> - **http-intunemam://<Pfad zur Web-App\>**<br /><br /> - **https-intunemam://<Pfad zur Web-App\>**<br /><br /> Sie können mithilfe der Configuration Manager-Anwendungsanforderungen sicherstellen, dass die Apps, die Sie mit Managed Browser verknüpfen möchten, nur auf iOS- und Android-Geräten installiert werden.<br /><br /> Weitere Informationen zu Intune Managed Browser finden Sie unter [Verwalten des Internetzugriffs mittels Richtlinien für verwaltete Browser mit System Center Configuration Manager](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).|  
|**Windows Installer über die Verwaltung mobiler Geräte (\*.msi)**|Mit diesem Installationstyp können Sie Windows Installer-basierte Apps auf Windows 10-PCs erstellen und bereitstellen.<br /><br /> Folgendes muss berücksichtigt werden, wenn Sie diese Art Installationsprogramm verwenden:<br><br>– Sie können nur eine einzelne Datei mit der Erweiterung „.msi“ hochladen.<br /><br /> – Produktcode und Produktversion der Datei werden zur Erkennung der App verwendet.<br /><br /> – Es wird das standardmäßige Neustartverhalten der App verwendet. Dieser Neustart wird nicht von Configuration Manager gesteuert.<br /><br /> – Pro Benutzer definierte MSI-Pakete werden für einen einzelnen Benutzer installiert.<br /><br /> – Pro Computer definierte MSI-Pakete werden für alle Benutzer des Geräts installiert.<br /><br /> – MSI-Pakete im Dualmodus werden zurzeit nur für alle Benutzer des Geräts installiert.<br /><br /> – App-Updates werden unterstützt, wenn jede Version den gleichen MSI-Produktcode aufweist.|  



## <a name="next-steps"></a>Nächste Schritte

Nach der Erstellung einer Anwendung in Configuration Manager ist der nächste Schritt das [Bereitstellen der Anwendung](/sccm/apps/deploy-use/deploy-applications).