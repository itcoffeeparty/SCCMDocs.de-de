---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Verwenden von System Center Updates Publisher zum Verwalten benutzerdefinierter Updates
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 3a9c7758e394118041700192a393aff98f0d9087
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Gilt für: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) ist ein eigenständiges Tool, mit dem unabhängige Softwarehersteller oder Entwickler branchenspezifischer Anwendungen benutzerdefinierte Updates verwalten können. Dies schließt Updates mit Abhängigkeiten ein, z.B. Treiber und Updatepakete.

Mit Updates Publisher können Sie Folgendes ausführen:

-   Importieren von Updates aus externen Katalogen (nicht von Microsoft stammenden Updatekatalogen).
-   Ändern von Updatedefinitionen einschließlich Anwendbarkeit und Bereitstellungsmetadaten.
-   Exportieren von Updates in externe Kataloge.
-   Veröffentlichen von Updates auf einem Updateserver.

Nach der Veröffentlichung von Updates auf einem Updateserver können Sie mit dem System Center Configuration Manager Updates erkennen und auf Ihren verwalteten Geräten bereitstellen.

> [!TIP]  
> Die vorherige Version, [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/?LinkId=848111), wird weiterhin unterstützt. Diese aktualisierte Version behält die gleiche Funktionalität bei, unterstützt aber zusätzliche Betriebssysteme, neue Features zur Vereinfachung mancher Aufgaben und eine aktualisierte Benutzeroberfläche.

## <a name="workspaces"></a>Arbeitsbereiche
Wenn Sie Updates Publisher öffnen, wird standardmäßig der Knoten „Übersicht“ des *Arbeitsbereichs „Updates“* angezeigt.

![Updates Publisher-Konsole](media/console1.png)   


Updates Publisher ist in vier Arbeitsbereiche unterteilt.


**Arbeitsbereich „Updates“**: Verwenden Sie diesen Arbeitsbereich, um Softwareupdates und Updatepakete zu [erstellen](/sccm/sum/tools/create-updates-with-updates-publisher) und zu [verwalten](/sccm/sum/tools/manage-updates-with-updates-publisher). Dies umfasst das Zuweisen von Updates und Paketen zu einer Veröffentlichung, das Veröffentlichen und das Exportieren in ein anderes Update Publisher-Repository.

**Arbeitsbereich „Veröffentlichungen“**: Hier [verwalten Sie Veröffentlichungen](/sccm/sum/tools/updates-publisher-publications). Eine Veröffentlichung ist eine Gruppe von Updates, die Sie erstellen, um das Exportieren und Veröffentlichen von Updates zu vereinfachen.

Das Verwalten von Veröffentlichungen umfasst das Veröffentlichen von Updates auf einem Server, damit Ihre Clients sie finden und installieren können, das Exportieren von Updates und Paketen für die Verwendung durch andere Updates Publisher-Installationen, oder das Ändern des Inhalts oder von Details einer Veröffentlichung.



**Arbeitsbereich „Regeln“**: Hier [verwalten Sie Anwendbarkeitsregeln](/sccm/sum/tools/updates-publisher-applicability-rules), die gespeichert und dann mit Updates, die Sie bereitstellen, verwendet werden können. Es gibt zwei Typen von Regeln:

-   „Installierbar“-Regeln – diese Regeln helfen zu bestimmen, ob ein Client ein Update installieren sollte.
-   „Installiert“-Regeln – diese Regeln überprüfen, ob ein Update bereits installiert ist.

**Arbeitsbereich „Kataloge“**: Nutzen Sie diesen Arbeitsbereich zum Hinzufügen und [Verwalten von Softwareupdatekatalogen](/sccm/sum/tools/updates-publisher-catalogs). Dies schließt den Import von Softwareupdates aus diesen Katalogen in das Updates Publisher-Repository ein.
## <a name="first-steps"></a>Erste Schritte
[Installieren](/sccm/sum/tools/install-updates-publisher) Sie zuerst Updates Publisher, und [konfigurieren](/sccm/sum/tools/updates-publisher-options) Sie dann die Optionen.
