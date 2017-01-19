---
title: Endpoint Protection-Schadsoftwaredefinitionen von der Netzwerkfreigabe | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie Schadsoftwaredefinitionen für Endpoint Protection aus Microsoft Updates für Configuration Manager herunterladen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 344f551a370378620d3d11870993a77e60f9f685


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



<!--HONumber=Dec16_HO3-->


