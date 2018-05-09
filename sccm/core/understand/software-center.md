---
title: Benutzerleitfaden für Softwarecenter
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zu Features und Funktionen des Softwarecenters.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: 4c45da7b5a4b7f8945b23d03d0fd551276205ee2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="software-center-user-guide"></a>Benutzerleitfaden für Softwarecenter

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit dem Softwarecenter installiert der IT-Administrator Ihrer Organisation Anwendungen und Softwareupdates und führt Upgrades für Windows durch. In diesem Benutzerleitfaden werden die Softwarecenter-Funktionen für Benutzer des Computers beschrieben.

### <a name="general-notes-about-software-center-functionality"></a>Allgemeine Hinweise zu Softwarecenter-Funktionen
- In diesem Artikel werden die neuesten Softwarecenter-Features beschrieben. Wenn Ihre Organisation eine ältere Softwarecenter-Version verwendet, die immer noch unterstützt wird, sind nicht alle Features verfügbar. Weitere Informationen erhalten Sie von Ihrem IT-Administrator.
- Ihr IT-Administrator deaktiviert möglicherweise einige Softwarecenter-Funktionen. Das Anwendungsverhalten kann daher je nach Einstellungen variieren.
<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->



## <a name="how-to-open-software-center"></a>Öffnen des Softwarecenters

Das Softwarecenter können Sie auf einem Windows 10-Computer besonders einfach starten, indem Sie auf **Start** klicken und `Software Center` eingeben. 

Alternativ können Sie auch über das Startmenü in der Menübandgruppe **Microsoft System Center** nach dem **Softwarecenter**-Symbol suchen.



## <a name="applications"></a>Applications

Klicken Sie auf die Registerkarte **Anwendungen** zum Suchen und Installieren von Anwendungen, die Ihr IT-Administrator für Sie oder auf diesem Computer bereitstellt.
- **Alle**: Hierdurch werden alle Anwendungen angezeigt, die Sie installieren können.
- **Erforderlich**: Hierdurch werden alle Anwendungen angezeigt, deren Verwendung vom IT-Administrator erzwungen wird. Wenn Sie eine dieser Anwendungen deinstallieren, installiert das Softwarecenter sie erneut.
- **Filter:** Ihr IT-Administrator kann Kategorien für Anwendungen erstellen. Falls Kategorien verfügbar sind, können Sie durch Klicken auf die Dropdownliste die Ansicht so filtern, dass nur Anwendungen einer bestimmten Kategorie angezeigt werden. Klicken Sie auf **Alle**, um sich alle Anwendungen anzeigen zu lassen.
- **Sortieren nach:** Hierdurch wird die Liste der Anwendungen neu geordnet. Standardmäßig wird als Sortieroption **Zuletzt verwendet** festgelegt.
- **Suchen:** Falls Sie bestimmte Elemente nicht finden, können Sie im Suchfeld Stichwörter eingeben, um nach den Elementen suchen.
-  Switch the view (Ansicht wechseln): Klicken Sie zum Wechseln zwischen Listenansicht und Kachelansicht auf die jeweiligen Symbole. Die Standardansicht für die Anwendungsliste ist die Kachelansicht. 
    - Kachelansicht: Ihr IT-Administrator kann die Symbole anpassen. Unter der Kachel befinden sich der Anwendungsname, der Herausgeber und die Version. 
    - Listenansicht: In dieser Ansicht werden das Anwendungssymbol, der Name, der Herausgeber, die Version und der Status angezeigt. 


### <a name="install-multiple-applications"></a>Mehrere Anwendungen installieren 
<!-- 1357126 -->
Sie können mehrere Anwendungen gleichzeitig installieren und müssen nicht auf den Abschluss einer Installation warten, bevor Sie mit der nächsten fortfahren. Dies ist allerdings nur bei Anwendungen möglich, für die die folgenden Voraussetzungen erfüllt sind:
- Die App wird Ihnen angezeigt.
- Die App wurde noch nicht heruntergeladen und ist noch nicht installiert.
- Ihr IT-Administrator benötigt keine Genehmigung zur Installation der App.

Gehen Sie folgendermaßen vor, um mehrere Anwendungen gleichzeitig zu installieren:
 1. Klicken Sie auf das Mehrfachauswahlsymbol, um den Mehrfachauswahlmodus in der Listenansicht zu nutzen. ![Mehrfachauswahlsymbol im Softwarecenter](media/software-center-multi-select-apps.png) in der oberen rechten Ecke.
 2. Wählen Sie mindestens zwei Apps aus, die installiert werden müssen, indem Sie das Feld links neben den Apps in der Liste aktivieren.
 3. Klicken Sie auf die Schaltfläche **Install Selected** (Auswahl installieren).

Die Apps werden wie gewöhnlich installiert, allerdings nacheinander.




## <a name="updates"></a>Updates

Klicken Sie auf die Registerkarte **Updates**, um sich Softwareupdates anzeigen zu lassen, die Ihr IT-Administrator auf diesem Computer bereitgestellt hat.  
- **Alle**: Hierdurch werden alle Updates angezeigt, die Sie installieren können.
- **Erforderlich**: Hierdurch werden alle Updates angezeigt, deren Installation vom IT-Administrator erzwungen wird.
- **Sortieren nach:** Hierdurch wird die Liste der Updates neu geordnet. Die Standardsortieroption für diese Liste ist **Anwendungsname: A bis Z**.

Klicken Sie zum Installieren von Updates auf **Install All** (Alle installieren).

Wenn Sie nur bestimmte Updates installieren möchten, klicken Sie auf das Symbol, um den Mehrfachauswahlmodus zu nutzen. Überprüfen Sie die Updates, die installiert werden sollen, und klicken Sie anschließend auf **Auswahl installieren**.



## <a name="operating-systems"></a>Betriebssysteme

Klicken Sie auf die Registerkarte **Betriebssysteme**, um sich Windows-Versionen anzeigen zu lassen, die Ihr IT-Administrator auf diesem Computer bereitgestellt hat.  
- **Alle**: Hierdurch werden alle Windows-Versionen angezeigt, die Sie installieren können.
- **Erforderlich**: Hierdurch werden alle Upgrades angezeigt, deren Installation vom IT-Administrator erzwungen wird.
- **Sortieren nach:** Hierdurch wird die Liste der Updates neu geordnet. Die Standardsortieroption für diese Liste ist **Anwendungsname: A bis Z**.



## <a name="installation-status"></a>Installationsstatus

Klicken Sie auf die Registerkarte **Installationsstatus**, um sich den Status von Anwendungen anzeigen zu lassen. Folgende Status können angezeigt werden:
- **Installiert:** Diese Anwendung wurde bereits von Softwarecenter auf diesem Computer installiert.
- **Downloadvorgang läuft:** Die Software, die auf diesem Computer installiert werden soll, wird derzeit von Softwarecenter heruntergeladen.
- **Failed** (Fehler): Bei der Softwareinstallation wurde von Softwarecenter ein Fehler erkannt.



## <a name="device-compliance"></a>Gerätekonformität

Klicken Sie auf die Registerkarte **Gerätekonformität**, um sich den Konformitätsstatus dieses Computers anzeigen zu lassen.

Klicken Sie auf **Konformität überprüfen**, um die Einstellungen dieses Geräts mit den Sicherheitsrichtlinien abzugleichen, die von Ihrem IT-Administrator definiert wurden.



## <a name="options"></a>Optionen

Klicken Sie auf die Registerkarte **Optionen**, um sich zusätzliche Einstellungen für diesen Computer anzeigen zu lassen.

### <a name="work-information"></a>Arbeitsinformationen

Geben Sie Ihre üblichen Arbeitszeiten an. Ihr IT-Administrator kann Softwareinstallationen so planen, dass diese außerhalb der Geschäftszeiten durchgeführt werden. Legen Sie die Zeiten so fest, dass für Systemwartungsaufgaben mindestens vier Stunden täglich zur Verfügung stehen. Ihr IT-Administrator kann allerdings wichtige Anwendungen und Softwareupdates auch während der Geschäftszeiten installieren.

- Wählen Sie aus den jeweiligen Dropdownlisten die früheste und späteste Uhrzeit aus, zu der Sie diesen Computer verwenden. Die Standardwerte sind **5:00** und **22:00**.

- Aktivieren Sie die Kontrollkästchen neben den Wochentagen, um festzulegen, wann Sie diesen Computer üblicherweise verwenden. Standardmäßig werden von Softwarecenter nur die Kontrollkästchen für Werktage aktiviert.  


### <a name="power-management"></a>Energieverwaltung

Ihr IT-Administrator kann Richtlinien zur Energieverwaltung festlegen. Diese unterstützen Ihre Organisation dabei, Strom zu sparen, wenn dieser Computer nicht verwendet wird. 

Aktivieren Sie das Kontrollkästchen neben **Do not apply power settings from my IT department to this computer** (Energieeinstellungen meiner IT-Abteilung nicht auf diesen Computer anwenden), wenn dieser Computer von der Richtlinie ausgenommen werden soll. Diese Einstellung ist standardmäßig deaktiviert, und vom Computer werden die Energieeinstellungen verwendet. 


### <a name="computer-maintenance"></a>Computerwartung

Geben Sie an, wie Änderungen an der Software vor Ablauf der Frist vom Softwarecenter übernommen werden sollen.
- **Erforderliche Software automatisch außerhalb der Geschäftszeiten installieren oder deinstallieren und Computer neu starten:** Diese Einstellung ist standardmäßig deaktiviert.
- **Softwarecenter-Aktivitäten anhalten, wenn sich der Computer im Präsentationsmodus befindet:** Diese Einstellung ist standardmäßig aktiviert.
- **Sync Policy** (Synchronisierungsrichtlinie): Klicken Sie nur auf diese Schaltfläche, wenn Sie von Ihrem IT-Administrator dazu aufgefordert werden. Dieser Computer überprüft mit einer Serverabfrage, ob neue Anwendungen, Softwareupdates oder Betriebssysteme verfügbar sind.

