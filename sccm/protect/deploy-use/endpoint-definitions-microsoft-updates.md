---
title: Endpoint Protection-Schadsoftwaredefinitionen von der Netzwerkfreigabe
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Schadsoftwaredefinitionen für Endpoint Protection aus Microsoft Updates für Configuration Manager herunterladen.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0d8037f2258f97e2782d475598ca62d2f605e5cd
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates-for-configuration-manager"></a>Aktivieren der Endpoint Protection-Schadsoftwaredefinitionen zum Herunterladen aus Microsoft Updates für Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 Wenn Sie das Herunterladen von Definitionsupdates von Microsoft Update auswählen, prüfen die Clients die Microsoft Update-Website in dem Intervall, das im Dialogfeld für die Richtlinie für Antischadsoftware im Abschnitt **Definitionsupdates** definiert ist.

 Diese Methode kann nützlich sein, wenn der Client nicht mit dem Configuration Manager-Standort verbunden ist, oder wenn die Benutzer in der Lage sein sollen, Definitionsupdates einzuleiten.

> [!IMPORTANT]
>  Clients müssen auf Microsoft Update im Internet zugreifen können, um diese Methode zum Herunterladen von Definitionsupdates nutzen zu können.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Verwenden des Microsoft Center zum Schutz vor Schadsoftware zum Herunterladen von Definitionen
 Sie können Clients zum Herunterladen von Definitionsupdates aus dem Microsoft Center zum Schutz vor Schadsoftware konfigurieren. Diese Option wird von Endpoint Protection-Clients zum Herunterladen von Definitionsupdates verwendet, wenn das Herunterladen von Updates aus einer anderen Quelle nicht möglich war. Diese Updatemethode ist nützlich, wenn ein Problem mit Ihrer Configuration Manager-Infrastruktur besteht, durch das die Bereitstellung von Updates verhindert wird.

> [!IMPORTANT]
>  Clients müssen auf Microsoft Update im Internet zugreifen können, um diese Methode zum Herunterladen von Definitionsupdates nutzen zu können.


> [!div class="button"]
[Nächster Schritt >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Zurück >](endpoint-configure-alerts.md)
