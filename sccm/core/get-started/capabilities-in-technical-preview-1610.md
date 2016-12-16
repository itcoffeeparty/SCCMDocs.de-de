---
title: "Funktionen in Technical Preview 1610 für System Center Configuration Manager"
description: "Erfahren Sie mehr zu den Features, die in Technical Preview für System Center Configuration Manager 1610 zur Verfügung stehen."
ms.custom: na
ms.date: 10/21/2016
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: article
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
caps.latest.revision: 2
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c9fe6961a63495d08a3e58e3ddf46c5d316e2613
ms.openlocfilehash: 865b5078282bf240aa6a2aef5cb2662f2471fb71

---
# <a name="capabilities-in-technical-preview-1610-for-system-center-configuration-manager"></a>Funktionen in Technical Preview 1610 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*



In diesem Artikel werden die Features erläutert, die in der Technical Preview für System Center Configuration Manager 1610 verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen.      Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen, und zu erfahren, wie Sie Updates zwischen Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.    


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtern nach Inhaltsgröße in automatischen Bereitstellungsregeln
Sie können jetzt nach Inhaltsgrößen für Softwareupdates in automatischen Bereitstellungsregeln filtern. Sie können z.B. den Filter **Inhaltsgröße (KB)** auf **< 2048** festlegen, um nur die Softwareupdates herunterzuladen, die kleiner als 2 MB sind. Mit diesem Filter wird verhindert, dass große Softwareupdates automatisch heruntergeladen werden, um die vereinfachte Windows-Wartung vorheriger Versionen zu unterstützen, wenn die Bandbreite eingeschränkt ist. Details finden Sie unter [Configuration Manager und vereinfachte Windows-Wartung auf vorherigen Betriebssystemebene](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

#### <a name="to-configure-the-content-size-field"></a>So konfigurieren Sie das Feld für die Inhaltsgröße
Navigieren Sie zur Seite **Softwareupdates** im Assistenten zum Erstellen automatischer Bereitstellungsregeln, wenn Sie einen ADR erstellen, oder zur Registerkarte **Softwareupdates** in den Eigenschaften für einen vorhandenen ADR, um das Feld **Inhaltsgröße (KB)** zu konfigurieren.

![Feld für Inhaltsgröße](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Verbesserte Funktionalität für erforderliche Softwaredialoge
Wenn ein Benutzer erforderliche Software von der Einstellung **Warten und erinnern:** erhält, kann er sie aus der folgenden Dropdownliste von Werten auswählen:
- Später: Gibt an, dass Benachrichtigungen basierend auf den in den Client-Agenteinstellungen konfigurierten Benachrichtigungseinstellungen geplant sind
- Feste Zeit: Gibt an, dass die Benachrichtigung nach der ausgewählten Zeit erneut angezeigt wird. Wenn ein Benutzer z.B. 30 Minuten auswählt, wird die Benachrichtigung in 30 Minuten erneut angezeigt.

![Computer-Agentseite in den Client-Agenteinstellungen](media/computeragentsettings.png)

Die maximale Wartezeit basiert immer auf den Benachrichtigungswerten, die in den Einstellungen des Client-Agents zu jedem Zeitpunkt der Bereitstellung konfiguriert sind. Wenn zum Beispiel die Einstellung **Bereitstellungsstichtag in mehr als 24 Stunden, Benutzer erinnern alle (Stunden)** auf der Seite des Computer-Agents auf 10 Stunden festgelegt ist und das Dialogfeld mehr als 24 Stunden vor Ablauf der Frist gestartet wird, erhält der Benutzer einen Satz an Warteoptionen von bis zu, aber nie mehr als 10 Stunden. Wenn sich der Stichtag nähert, wird das Dialogfeld weniger Optionen anzeigen. Dies stimmt mit den entsprechenden Client-Agenteinstellungen für jede Komponente der Bereitstellungszeit überein.

Darüber hinaus fällt bei Bereitstellungen mit hohem Risiko, z.B. einer Tasksequenz, die ein Betriebssystem bereitstellen, die Benachrichtigung des Endbenutzers deutlicher aus. Immer wenn der Benutzer benachrichtigt wird, dass eine kritische Softwarewartung erforderlich ist, wird anstatt einer vorübergehenden Benachrichtigung in der Taskleiste ein Dialogfeld wie das folgende auf dem Computer des Benutzers angezeigt:

![Erforderlicher Softwaredialog](media/requiredsoftwaredialog.png)


Weitere Informationen:
- [Einstellungen zum Verwalten von Bereitstellungen mit hohem Risiko](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Konfigurieren von Clienteinstellungen](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Zuvor genehmigte Anwendungsanforderungen verweigern

Als Administrator können Sie jetzt eine zuvor genehmigte Anwendungsanforderung verweigern. Einmal verweigert, müssen spätere Benutzer eine erneute Anfrage zur Installation dieser Anwendung stellen. Die Anwendung wird durch die Verweigerung nicht deinstalliert. Stattdessen wird eine erneute Genehmigung für jede neue Anforderung für diese Anwendung von diesem Benutzer erzwungen. Bisher war die Verweigerung einer Anwendungsanforderung nur für Anwendungsanforderungen verfügbar, die nicht genehmigt wurden.

#### <a name="try-it-out"></a>Probieren Sie es aus
So verweigern Sie eine genehmigte Anwendungsanforderung:

1.  [Erstellen Sie eine Anwendung](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/create-applications) in der Configuration Manager-Konsole, die eine Genehmigung benötigt, und stellen Sie sie bereit.
2.  Öffnen Sie das Softwarecenter auf einem Clientcomputer, und reichen Sie eine Anwendungsanforderung ein.
3.  Genehmigen Sie die Anwendungsanforderung in der Configuration Manager-Konsole.
4.  Genehmigte Anwendungsanforderung verweigern: Navigieren Sie In der Configuration Manager-Konsole zu **Softwarebibliothek** > **Übersicht** > **Anwendungsverwaltung** > **Genehmigungsanforderungen**, und wählen Sie die Anwendungsanforderung aus, die Sie verweigern möchten.  Klicken Sie im Menüband auf **Verweigern**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Ausschließen von Clients von automatischen Upgrades
Technical Preview 1610 führt eine neue Einstellung ein, die Sie verwenden können, um eine Clientsammlung von der automatischen Installation aktualisierter Clientversionen auszuschließen.  Dies gilt sowohl für automatische Upgrades und als auch für andere Methoden, wie Upgrades auf der Basis von Softwareupdates, Registrierungsskripts und Gruppenrichtlinien. Dies kann für eine Computersammlung genutzt werden, die bei einem Upgrade des Clients größere Sorgfalt benötigt. Ein Client, der sich in einer ausgeschlossenen Sammlung befindet, ignoriert Anforderungen zur Installation von aktualisierter Clientsoftware.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Ausschluss vom automatischen Upgrade konfigurieren
So konfigurieren Sie Ausschlüsse aus automatischen Upgrades:
1.  Öffnen Sie in der Configuration Manager-Konsole die **Hierarchieeinstellungen** unter **Verwaltung > Standortkonfiguration > Standorte**, und wählen Sie dann die Registerkarte **Clientupgrade** aus.
2.  Aktivieren Sie die Kontrollkästchen **Exclude specified clients from upgrade** (Angegebene Clients aus Upgrades ausschließen) und **Exclusion collection** (Ausschlusssammlung), und wählen Sie die Sammlung aus, die Sie ausschließen möchten. Sie können nur eine einzelne Sammlung für den Ausschluss auswählen.
3.  Klicken Sie auf **OK**, um die Konfiguration zu schließen und zu speichern. Nachdem die Clients Richtlinien aktualisiert haben, können Clients in der ausgeschlossenen Sammlung nicht mehr automatisch Updates der Clientsoftware installieren.

  ![Einstellungen für automatische Ausschlüsse aus Upgrades](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Obwohl die Benutzeroberfläche angibt, dass Upgrades für Clients nicht mit einer beliebigen Methode durchgeführt werden können, gibt es zwei Methoden, die Sie verwenden können, um diese Einstellungen außer Kraft zu setzen. Die Clientpushinstallation und eine manuelle Clientinstallation können verwendet werden, um diese Konfiguration außer Kraft zu setzen. Weitere Details erfahren Sie im nächsten Abschnitt.


### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>So führen Sie für einen Client in einer ausgeschlossenen Sammlung ein Upgrade durch
Solange eine Sammlung für den Ausschluss konfiguriert ist, können Mitglieder dieser Sammlung ihre Clientsoftware nur mit einer der beiden Methoden, die den Ausschluss außer Kraft setzen, upgegradet werden:
 - **Clientpushinstallation** – Sie können die Clientpushinstallation verwenden, um einen Client in einer ausgeschlossen Sammlung upzugraden. Dies ist zulässig, da es als Absicht des Administrators betrachtet wird und Ihnen ermöglicht, Clients upzugraden, ohne die gesamte Sammlung aus der Ausschlussliste zu entfernen.       
 - **Manuelle Clientinstallation** – Sie können Clients in einer ausgeschlossenen Sammlung unter Verwendung des Befehlszeilenschalters ***/ignoreskipupgrade*** mit ccmsetup manuell upgraden.

  Wenn Sie versuchen, einen Client, der Mitglied der ausgeschlossenen Sammlung ist, manuell upzugraden, und diesen Schalter nicht verwenden, wird der Client die neue Clientsoftware nicht installieren. Weitere Informationen finden Sie unter [Manuelles Installieren von Configuration Manager-Clients](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually).

Weitere Informationen zu Clientinstallationsmethoden finden Sie unter [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).


## <a name="see-also"></a>Siehe auch
[Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md)



<!--HONumber=Nov16_HO1-->


