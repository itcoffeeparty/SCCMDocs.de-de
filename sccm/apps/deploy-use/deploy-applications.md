---
title: Bereitstellen von Anwendungen
titleSuffix: Configuration Manager
description: Erstellen oder Simulieren der Bereitstellung einer Anwendung für ein Gerät oder eine Benutzersammlung
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: 10
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0101ba0eade5775577f52920f301a782afd7bbda
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Bereitstellen von Anwendungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Erstellen oder simulieren Sie in Configuration Manager die Bereitstellung einer Anwendung für ein Gerät oder eine Benutzersammlung. Diese Bereitstellung enthält Anweisungen für den Configuration Manager-Client zur Vorgehensweise und zum Zeitpunkt der Installation der Software. 

Bevor Sie eine Anwendung bereitstellen können, müssen Sie mindestens einen Bereitstellungstyp für die Anwendung erstellen. Weitere Informationen finden Sie unter [Erstellen von Anwendungen](/sccm/apps/deploy-use/create-applications).

 Sie können eine Anwendungsbereitstellung auch simulieren. Diese Simulation testet die Anwendbarkeit einer Bereitstellung ohne eine Installation oder Deinstallation der Anwendung. Bei einer simulierten Bereitstellung werden die Erkennungsmethode, Anforderungen und Abhängigkeiten für einen Bereitstellungstyp ausgewertet. Anschließend wird ein Bericht mit den Ergebnissen im Arbeitsbereich **Überwachung** unter dem Knoten **Bereitstellungen** ausgegeben. Weitere Informationen finden Sie unter [Simulate application deployments (Simulieren von Anwendungsbereitstellungen)](/sccm/apps/deploy-use/simulate-application-deployments).

> [!IMPORTANT]
>  Sie können die Bereitstellung erforderlicher Anwendungen simulieren, jedoch nicht die Bereitstellung von Paketen oder Softwareupdates.   
>  MDM-registrierte Geräte unterstützen keine simulierten Bereitstellungen, Einstellungen für Benutzerfreundlichkeit oder Zeitplanung.



## <a name="deploy-an-application"></a>Bereitstellen einer Anwendung

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen**.

2.  Wählen Sie in der Liste **Anwendungen** die Anwendung aus, die Sie bereitstellen möchten. Klicken Sie dann auf die **Home** Registerkarte der **Bereitstellung** auf **Bereitstellen**.

### <a name="specify-general-information-about-the-deployment"></a>Angeben allgemeiner Informationen zur Bereitstellung

Geben Sie im Assistenten zum Bereitstellen von Software auf der Seite **Allgemein** die folgenden Informationen an:

- **Software**: Dieser Wert zeigt die Anwendung an, die bereitgestellt werden soll. Klicken Sie auf **Durchsuchen**, um eine andere Anwendung auszuwählen.
- **Sammlung**: Klicken Sie auf **Durchsuchen**, um die Sammlung auszuwählen, in der Sie die Anwendung bereitstellen möchten.
- **Standard-Verteilungspunktgruppen verwenden, die dieser Sammlung zugeordnet sind**: Speichern Sie den Anwendungsinhalt in der Standard-Verteilungspunktgruppe der Sammlung. Wenn die ausgewählte Sammlung keiner Verteilungspunktgruppe zugeordnet ist, ist diese Option ausgegraut.
- **Inhalt automatisch für Abhängigkeiten bereitstellen**: Wenn Bereitstellungstypen in der Anwendung Abhängigkeiten enthalten, sendet der Standort den Inhalt der abhängigen Anwendung auch an Verteilungspunkte.

    >[!IMPORTANT]
    > Wenn Sie die abhängige Anwendung aktualisieren, nachdem die primäre Anwendung bereitgestellt wurde, verteilt der Standort nicht automatisch neue Inhalte für die Abhängigkeit.

- **Kommentare (optional)**: Geben Sie bei Bedarf eine Beschreibung der Bereitstellung ein.

### <a name="specify-content-options-for-the-deployment"></a>Angeben von Inhaltsoptionen für die Bereitstellung

Klicken Sie auf der Seite **Inhalt** auf **Hinzufügen**, um den dieser Bereitstellung zugeordneten Inhalt Verteilungspunkten oder Verteilungspunktgruppen hinzuzufügen. Wenn Sie auf der Seite **Allgemein** die Option **Use default distribution points associated to this collection** (Dieser Sammlung zugeordnete Standardverteilungspunkte verwenden) auswählen, wird diese Option automatisch aufgefüllt. Nur ein Mitglied der Sicherheitsrolle „Anwendungsadministrator“ kann dies ändern.

### <a name="specify-deployment-settings"></a>Angeben von Bereitstellungseinstellungen

Geben Sie im Assistenten zum Bereitstellen von Software auf der Seite **Bereitstellungseinstellungen** die folgenden Informationen an:

- **Aktion**: Wählen Sie in der Dropdownliste aus, ob diese Bereitstellung zum **Installieren** oder **Deinstallieren** der Anwendung dienen soll.

    > [!NOTE]
    >  Wenn eine Anwendung zweimal auf einem Gerät bereitgestellt wird, einmal mit der Aktion **Installieren** und einmal mit der Aktion **Deinstallieren**, hat die Anwendungsbereitstellung mit der Aktion **Installieren** höhere Priorität.

  Sie können die Aktion einer Bereitstellung nicht mehr ändern, nachdem sie erstellt wurde.

- **Zweck**: Wählen Sie in der Dropdownliste eine der folgenden Optionen aus:  
    - **Verfügbar**: Wenn die Anwendung für einen Benutzer bereitgestellt wird, ist sie für den Benutzer im Softwarecenter als veröffentlichte Anwendung sichtbar, und er kann sie bei Bedarf installieren.
    - **Erforderlich**: Die Anwendung wird gemäß dem Zeitplan automatisch bereitgestellt. Wenn der Bereitstellungsstatus nicht ausgeblendet ist, kann jede Person, die die Anwendung verwendet, den Bereitstellungsstatus nachverfolgen, und die Anwendung vor Ablauf der Frist über das Softwarecenter installieren.

    > [!NOTE]   
    >  Wenn als Bereitstellungsaktion **Deinstallieren** ausgewählt wurde, wird als Bereitstellungszweck automatisch **Erforderlich** festgelegt. Dieses Verhalten kann nicht geändert werden.  

- **Deploy automatically according to schedule whether or not a user is logged on** (Automatisch mit oder ohne Benutzeranmeldung bereitstellen): Wählen Sie diese Option aus, wenn die Bereitstellung für einen Benutzer bestimmt ist, um die Anwendung auf den primären Geräten des Benutzers bereitzustellen. Bei dieser Einstellung ist es nicht erforderlich, dass sich der Benutzer vor der Ausführung der Bereitstellung anmeldet. Wählen Sie diese Option nicht aus, wenn der Benutzer mit der Installation interagieren muss. Diese Option ist nur verfügbar, wenn der Bereitstellungszweck auf **Erforderlich**festgelegt ist.

- **Aktivierungspakete senden**: Wenn der Bereitstellungszweck auf **Erforderlich** festgelegt ist, wird ein Aktivierungspaket an Computer gesendet, bevor der Client die Bereitstellung ausführt. Dieses Paket aktiviert den Computer zum Installationsstichtag. Bevor Sie diese Option verwenden, müssen Computer und Netzwerke für Wake-On-LAN konfiguriert sein.
- **Allow clients on a metered Internet connection to download content after the installation deadline, which might incur additional costs** (Clients mit einer getakteten Internetverbindung dürfen den Inhalt nach dem Installationsstichtag herunterladen (Zusatzkosten können anfallen)): Diese Option ist nur für Bereitstellungen mit dem Zweck **Erforderlich** verfügbar.
- **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box** (Ausgeführte ausführbare Dateien automatisch schließen, die im Eigenschaftendialogfeld des Bereitstellungstyps auf der Registerkarte „Installationsverhalten“ angegeben wurden): Weitere Informationen finden Sie unter [check for running executable files before installing an application (Prüfen auf ausgeführte ausführbare Dateien vor der Installation einer Anwendung)](#how-to-check-for-running-executable-files-before-installing-an-application).

- **Require administrator approval if users request this application** (Genehmigung durch Administrator erforderlich, wenn Benutzer diese Anwendung anfordern): Bei Version 1710 und früheren Versionen genehmigt der Administrator alle Benutzeranforderungen für die Anwendung, bevor der Benutzer diese installieren kann. Diese Option ist abgeblendet, wenn der Zweck der Bereitstellung **Erforderlich** lautet, oder wenn die Anwendung für eine Gerätesammlung bereitgestellt wird.  

    > [!NOTE]
    >  Genehmigungsanforderungen für Anwendungen werden im Arbeitsbereich **Softwarebibliothek** unter **Anwendungsverwaltung** im Knoten **Genehmigungsanforderungen** angezeigt. Wenn eine Anforderung nicht innerhalb von 45 Tagen genehmigt wird, wird sie entfernt. Ausstehende Genehmigungsanforderungen können durch eine Neuinstallation abgebrochen werden.  
    >  Nachdem Sie eine Anwendung für die Installation genehmigt haben, können Sie die Anforderung in der Configuration Manager-Konsole **verweigern**. Diese Aktion führt nicht dazu, dass der Client die Anwendung auf allen Geräten deinstalliert, sondern hindert Benutzer daran, neue Kopien der Anwendung aus dem Softwarecenter herunterzuladen.

- **An administrator must approve a request for this application on the device** (Ein Administrator muss eine Anforderung für diese Anwendung auf dem Gerät genehmigen): Ab Version 1802 genehmigt der Administrator jede Benutzeranforderung für die Anwendung, bevor der Benutzer diese auf dem angeforderten Gerät installieren kann. Wenn ein Administrator die Anforderung genehmigt, kann der Benutzer die Anwendung nur auf diesem spezifischen Gerät installieren. Der Benutzer muss eine weitere Anforderung senden, um die Anwendung auf einem anderen Gerät installieren zu können. Diese Option ist abgeblendet, wenn der Zweck der Bereitstellung **Erforderlich** lautet, oder wenn die Anwendung für eine Gerätesammlung bereitgestellt wird. <!--1357015-->  

    Dies ist ein optionales Feature. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options). Wenn dieses Feature nicht aktiviert ist, sehen Sie die Vorerfahrung.  

    > [!Important]  
    > Der Configuration Manager-Client muss ebenfalls Version 1802 aufweisen. Sie müssen ebenfalls das neue Softwarecenter verwenden.  

    > [!Note]  
    > Sehen Sie sich in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** unter **Anwendungsverwaltung** die **Genehmigungsanforderungen** an. Sie finden jetzt in Liste eine Spalte **Gerät** für jede Anforderung. Wenn Sie eine Aktion zur Anforderung ausführen, enthält das Dialogfeld „Anwendungsanforderung“ auch den Namen des Geräts, von dem aus der Benutzer die Anforderung übermittelt hat.  
    >  Wenn eine Anforderung nicht innerhalb von 45 Tagen genehmigt wird, wird sie entfernt. Ausstehende Genehmigungsanforderungen können durch eine Neuinstallation abgebrochen werden.  
    >  Nachdem Sie eine Anwendung für die Installation genehmigt haben, können Sie die Anforderung in der Configuration Manager-Konsole **verweigern**. Diese Aktion führt nicht dazu, dass der Client die Anwendung auf allen Geräten deinstalliert, sondern hindert Benutzer daran, neue Kopien der Anwendung aus dem Softwarecenter herunterzuladen.

- **Automatically upgrade any superseded version of this application** (Automatisch ein Upgrade aller abgelösten Versionen dieser Anwendung ausführen): Der Client führt mit der abgelösten Anwendung ein Upgrade aller abgelösten Versionen dieser Anwendung aus.    

    > [!NOTE]  
    > Ab Version 1802 können Sie diese Option aktivieren oder deaktivieren, wenn der Installationszweck **Verfügbar** oder **Erforderlich** lautet. <!--1351266--> 


### <a name="specify-scheduling-settings-for-the-deployment"></a>Angeben von Einstellungen zur Zeitplanung der Bereitstellung

Stellen Sie im Assistenten zum Bereitstellen von Software auf der Seite **Zeitplanung** die Zeit ein, wann diese Anwendung für Clientgeräte bereitgestellt oder verfügbar gemacht wird.
Welche Optionen auf dieser Seite verfügbar sind, ist davon abhängig, ob die Bereitstellungsaktion auf **Verfügbar** oder **Erforderlich**gesetzt ist.

In einigen Fällen empfiehlt es sich, Benutzern über die von Ihnen angegebenen Fristen hinaus mehr Zeit zum Installieren von erforderlichen Anwendungsbereitstellungen oder Softwareupdates zu geben. Dieses Verhalten ist in der Regel erforderlich, wenn ein Computer für lange Zeit ausgeschaltet wurde und viele Anwendungen installiert werden müssen. Wenn z.B. ein Benutzer aus dem Urlaub zurückgekehrt ist, muss er möglicherweise sehr lange warten, bis überfällige Anwendungsbereitstellungen installiert werden. Sie können jetzt eine zwingende Toleranzperiode definieren, um dieses Problem zu lösen. Dafür müssen Sie die Configuration Manager-Clienteinstellungen für eine Sammlung bereitstellen.

Führen Sie folgende Aktionen aus, um die Karenzzeit zu konfigurieren:

- Auf der Seite **Computer-Agent** der Clienteinstellungen müssen Sie die neue Eigenschaft **Karenzzeit für Erzwingung nach Bereitstellungsfrist (Stunden)** mit einem Wert zwischen **1** und **120** Stunden konfigurieren.
- Wählen Sie auf der Seite **Zeitplanung** in einer neuen erforderlichen Anwendungsbereitstellung die Option **Delay enforcement of this deployment according to user preferences, up to the grace period defined in client settings** (Erzwingen dieser Bereitstellung entsprechend den Benutzervoreinstellungen bis zur Karenzzeit verzögern, die in den Clienteinstellungen definiert ist) aus. Die Karenzzeit für die Erzwingung gilt für alle Bereitstellungen, für die diese Option aktiviert wird, und die für Geräte vorgesehen sind, für die Sie ebenfalls die Clienteinstellungen bereitgestellt haben.

Nach Ablauf der Installationsfrist installiert der Client die Anwendung im ersten nicht geschäftlichen Fenster, das der Benutzer in der Karenzzeit konfiguriert hat. Der Benutzer kann jedoch weiterhin das Software Center öffnen und die Anwendung zu einem beliebigen Zeitpunkt installieren. Nach Ablauf der Toleranzperiode wird die Erzwingung auf normales Verhalten für überfällige Bereitstellungen zurückgesetzt.

Wenn die bereitgestellte Anwendung eine andere Anwendung ablöst, können Sie den Installationsstichtag festlegen, an dem bei Benutzern die neue Anwendung installiert wird. Legen Sie den **Installationsstichtag** fest, um für Benutzer mit der abgelösten Anwendung ein Upgrade auszuführen.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Angeben von Einstellungen für die Benutzerfreundlichkeit der Bereitstellung

Geben Sie im Assistenten zum Bereitstellen von Software auf der Seite **Benutzerfreundlichkeit** an, wie Benutzer mit der Anwendungsinstallation interagieren können.

Wenn Sie Anwendungen für Windows Embedded-Geräte mit Schreibfilteraktivierung bereitstellen, können Sie angeben, dass die Anwendung im temporären Overlay gespeichert und die Änderungen später übernommen werden sollen. Sie können die Änderungen auch am Installationsstichtag oder während eines Wartungsfensters bereitstellen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden, ist ein Neustart des Geräts erforderlich. Die Änderungen werden auf dem Gerät beibehalten.

>[!NOTE]
    >  Stellen Sie bei der Bereitstellung einer Anwendung auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung mit einem Wartungsfenster ist. Weitere Informationen zu Wartungsfenstern und Windows Embedded-Geräten finden Sie unter [Create Windows Embedded applications (Erstellen von Windows Embedded-Geräten)](../../apps/get-started/creating-windows-embedded-applications.md).
    > Die Optionen **Softwareinstallation** und **Systemneustart (falls dieser zum Abschluss der Installation erforderlich ist)** werden nicht verwendet, wenn der Bereitstellungszweck auf **Verfügbar**gesetzt ist. Sie können auch die Ebene für die Benutzerbenachrichtigung bei der Anwendungsinstallation konfigurieren.

### <a name="specify-alert-options-for-the-deployment"></a>Angeben von Optionen zu Warnungen für die Bereitstellung

Stellen Sie im Assistenten zum Bereitstellen von Software auf der Seite **Warnungen** ein, wie Warnungen von Configuration Manager und System Center Operations Manager für diese Bereitstellung generiert werden. Sie können Schwellenwerte für Berichtswarnungen konfigurieren und die Berichterstattung für die Dauer der Bereitstellung deaktivieren.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Zuordnen der Bereitstellung zu einer iOS-App-Konfigurationsrichtlinie

Klicken Sie auf der Seite **App Configuration Policies** (App-Konfigurationsrichtlinien) auf **Neu**, um diese Bereitstellung einer iOS-App-Konfigurationsrichtlinie zuzuordnen (sofern Sie eine solche erstellt haben). Weitere Informationen zu diesen Richtlinientypen finden Sie unter [Konfigurieren von Apps mit Konfigurationsrichtlinien für Apps](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).

### <a name="deployment-properties"></a>Bereitstellungseigenschaften

Suchen Sie die neue Bereitstellung über den Knoten **Bereitstellungen** des Arbeitsbereichs **Überwachung**. Sie können die Eigenschaften dieser Bereitstellung bearbeiten oder die Bereitstellung auf der Registerkarte **Bereitstellungen** des Anwendungsdetailbereichs löschen.



## <a name="delete-an-application-deployment"></a>Löschen einer Anwendungsbereitstellung

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen**.
3.  Wählen Sie in der Liste **Anwendungen** die Anwendung aus, die die Bereitstellung enthält, die Sie löschen möchten.
4.  Wählen Sie auf der Registerkarte **Bereitstellungen** in der Liste *<Anwendungsname\>* die zu löschende Anwendungsbereitstellung aus. Klicken Sie auf der Registerkarte **Bereitstellung** in der Gruppe **Bereitstellung** dann auf **Löschen**.

Wenn Sie eine Anwendungsbereitstellung löschen, werden bereits installierte Instanzen der Anwendung nicht entfernt. Sie müssen diese Anwendungen mit **Deinstallieren** auf Computern bereitstellen, um sie zu entfernen. Wenn Sie eine Anwendungsbereitstellung löschen oder eine Ressource aus der Sammlung entfernen, in der Sie die Bereitstellung vornehmen, wird diese im Softwarecenter nicht mehr angezeigt.



## <a name="user-notifications-for-required-deployments"></a>Benutzerbenachrichtigungen für erforderliche Bereitstellungen
Wenn Sie erforderliche Software von der Einstellung **Warten und erinnern** erhalten, Können Sie aus der folgenden Dropdownliste von Werten auswählen:
- **Später**: Gibt an, dass Benachrichtigungen basierend auf den in den Clienteinstellungen konfigurierten Benachrichtigungseinstellungen geplant sind.
- **Feste Zeit**: Gibt an, dass die Benachrichtigung nach der ausgewählten Zeit erneut angezeigt wird. Wenn Sie z.B. 30 Minuten auswählen, wird die Benachrichtigung in 30 Minuten erneut angezeigt.

![Gruppe „Computer-Agent“ in Clientstandardeinstellungen](media/ComputerAgentSettings.png)

Die maximale Erinnerungszeit basiert immer auf den Benachrichtigungswerten, die in den Clienteinstellungen zu jedem Zeitpunkt der Bereitstellung konfiguriert sind. Zum Beispiel:
- Sie konfigurieren die Einstellung **Deployment deadline greater than 24 hours, remind users every (hours)** (Bereitstellungsstichtag größer als 24 Stunden, Benutzer alle (Stunden) erinnern) auf der Seite **Computer-Agent** für 10 Stunden.
- Der Client zeigt das Benachrichtigungsdialogfeld mehr als 24 Stunden vor dem Bereitstellungsstichtag an.
- Im Dialogfeld werden Erinnerungsoptionen von bis zu maximal 10 Stunden angezeigt. 
- Wenn der Bereitstellungsstichtag näher rückt, werden im Dialogfeld weniger Optionen angezeigt. Diese Optionen stimmen mit den entsprechenden Clienteinstellungen für jede Komponente der Bereitstellungszeit überein.

Bei Bereitstellungen mit hohem Risiko, z.B. einer Tasksequenz, die ein Betriebssystem bereitstellen, fällt die Benachrichtigung des Benutzers deutlicher aus. Immer wenn Sie benachrichtigt werden, dass eine wichtige Softwarewartung erforderlich ist, wird anstatt einer vorübergehenden Benachrichtigung in der Taskleiste ein Dialogfeld wie das folgende angezeigt:

![Erforderlicher Softwaredialog, der Sie über wichtige Softwarewartung benachrichtigt](media/client-toast-notification.png)



## <a name="how-to-check-for-running-executable-files-before-installing-an-application"></a>So prüfen Sie auf ausgeführte ausführbare Dateien, bevor Sie eine Anwendung installieren

Geben Sie im Dialogfeld **Eigenschaften** eines Bereitstellungstyps auf der Registerkarte **Installationsverhalten** mindestens eine ausführbare Datei an. Wenn eine dieser ausführbaren Dateien auf dem Client ausgeführt wird, blockiert diese die Installation des Bereitstellungstyps. Der Benutzer muss die ausgeführte ausführbare Datei schließen, bevor der Client den Bereitstellungstyp installieren kann. Für Bereitstellungen mit dem Zweck „Erforderlich“ kann der Client die ausgeführte ausführbare Datei automatisch schließen.

1. Öffnen Sie das Dialogfeld **Eigenschaften** für jeden Bereitstellungstyp.
2. Klicken Sie auf der Registerkarte **Installationsverhalten** des Dialogfelds *<deployment type name>* **Eigenschaften** auf **Hinzufügen**.
3. Geben Sie im Dialogfeld **Ausführbare Datei hinzufügen oder bearbeiten** den Namen der ausführbaren Datei an, die bei der Ausführung die Installation der Anwendung blockiert. Optional können Sie auch einen Anzeigenamen für die Anwendung eingeben, damit Sie sie leichter identifizieren können.
4. Klicken Sie auf **OK** und schließen Sie das Dialogfeld *<deployment type name>* **Eigenschaften**.
5. Wenn Sie die Anwendung auf der Seite **Bereitstellungseinstellungen** des Assistenten zum Bereitstellen von Software bereitstellen, wählen Sie **Ausgeführte ausführbare Dateien automatisch schließen, die im Eigenschaftendialogfeld des Bereitstellungstyps auf der Registerkarte „Installationsverhalten“ angegeben wurden** aus.

Nachdem Clients die Bereitstellung empfangen haben, wird folgendes Verhalten angewendet:

- Wenn Sie die Anwendung als **Verfügbar** bereitgestellt haben und ein Benutzer versucht, sie zu installieren, fordert der Client ihn dazu auf, die ausgeführten ausführbaren Dateien zu schließen, bevor er mit der Installation fortfahren kann.

- Wenn Sie die Anwendung als **Erforderlich** bereitgestellt haben, und die Option **Ausgeführte ausführbare Dateien automatisch schließen, die im Eigenschaftendialogfeld des Bereitstellungstyps auf der Registerkarte „Installationsverhalten“ angegeben wurden** ausgewählt ist, wird dem Benutzer ein Dialogfeld angezeigt, das ihn darüber informiert, dass die angegebenen ausführbaren Dateien automatisch geschlossen werden, wenn die Frist für die Installation der Anwendung abgelaufen ist. Sie können diese Dialogfelder unter **Clienteinstellungen** > **Computer-Agent** zeitlich festlegen. Wenn Sie nicht möchten, dass der Endbenutzer diese Meldungen sieht, wählen Sie auf der Registerkarte **User Experience** (Benutzererfahrung) der Bereitstellungseigenschaften **In Softwarecenter und allen Benachrichtigungen ausblenden** aus.

- Wenn Sie die Anwendung als **Erforderlich** bereitgestellt haben, und die Option **Ausgeführte ausführbare Dateien automatisch schließen, die im Eigenschaftendialogfeld des Bereitstellungstyps auf der Registerkarte „Installationsverhalten“ angegeben wurden** nicht ausgewählt ist, schlägt die Installation der App fehl, wenn mindestens eine der angegebenen Anwendungen ausgeführt wird.



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Bereitstellen von für Benutzer verfügbare Anwendungen auf in Azure AD eingebundenen Geräten
<!-- 1322613 -->
Wenn Sie Anwendungen als für Benutzer verfügbar bereitstellen, können diese ab Version 1802 die Anwendungen über das Softwarecenter auf Azure AD-Geräten (Azure Active Directory) durchsuchen und installieren.  

#### <a name="prerequisites"></a>Erforderliche Komponenten

- Aktivieren Sie HTTPS auf dem Verwaltungspunkt.  

- Integrieren Sie den Standort in [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) für die **Cloudverwaltung**.  

    - Konfigurieren Sie die [Azure AD-Benutzerermittlung](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).  

- Stellen Sie über Azure AD eine Anwendung als für eine Benutzersammlung verfügbar bereit.  

- Verteilen Sie Anwendungsinhalte an einen [Cloudverteilungspunkt](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point).  

- Aktivieren Sie die Clienteinstellung **Neues Softwarecenter verwenden** in der Gruppe [Computer-Agent](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

- Als Clientbetriebssystem muss Windows 10 verwendet werden, und es muss in Azure AD eingebunden sein. Eine einfache Einbindung in die Clouddomäne oder eine Einbindung in Hybrid-Azure AD  

- Zur Unterstützung internetbasierter Clients:  

    - [Cloudverwaltungsgateway](/sccm/core/clients/manage/plan-cloud-management-gateway)  

    - Aktivieren Sie die Clienteinstellung **Benutzerrichtlinienanforderungen von Internetclients aktivieren** in der Gruppe [Clientrichtlinie](/sccm/core/clients/deploy/about-client-settings#client-policy).  

- So unterstützen Sie Clients im Intranet:  

    - Fügen Sie den Cloudverteilungspunkt zu einer Begrenzungsgruppe hinzu, die von den Clients verwendet wird.  

    - Clients müssen den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) des HTTPS-fähigen Verwaltungspunkts auflösen können.  



## <a name="next-steps"></a>Nächste Schritte

   -  [Einstellungen zum Verwalten von Bereitstellungen mit hohem Risiko](../../protect/understand/settings-to-manage-high-risk-deployments.md)  
   -  [Konfigurieren von Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md)
   -  [Benutzerleitfaden des Softwarecenters](/sccm/core/understand/software-center)

