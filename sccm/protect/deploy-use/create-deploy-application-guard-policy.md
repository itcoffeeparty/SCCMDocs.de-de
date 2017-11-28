---
title: Erstellen und Bereitstellen einer Windows Defender Application Guard-Richtlinie
titleSuffix: Configuration Manager
description: Erstellen und Bereitstellen einer Windows Defender Application Guard-Richtlinie.
ms.custom: na
ms.date: 11/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 
caps.latest.revision: "5"
author: ErikjeMS
ms.author: erikje
manager: angrobe
ms.openlocfilehash: db2508e5bbd1435fce432b6ef98d7968e68ea5ab
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="create-and-deploy-windows-defender-application-guard-policy----1351960---"></a>Erstellen und Bereitstellen einer Windows Defender Application Guard-Richtlinie <!-- 1351960 -->

Sie können [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview)-Richtlinien erstellen und bereitstellen, indem Sie den Configuration Manager-Endpunktschutz verwenden. Diese Richtlinien dienen zum Schutz Ihrer Benutzer, indem nicht vertrauenswürdige Websites in einem sicheren isolierten Container geöffnet werden, auf den andere Teile des Betriebssystems keinen Zugriff haben.

## <a name="prerequisites"></a>Voraussetzungen

Damit Sie eine Windows Defender Application-Richtlinie erstellen können, müssen Sie das Windows 10 Fall Creator’s Update nutzen. Außerdem müssen die Windows 10-Geräte, auf denen Sie die Richtlinie bereitstellen, mit einer Netzwerkisolationsrichtlinie konfiguriert werden. Weitere Informationen finden Sie in der [Übersicht über Windows Defender Application Guard](https://docs.microsoft.com/en-us/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). Diese Funktion funktioniert nur mit aktuellen Windows 10 Insider-Builds. Um sie zu testen, muss auf Ihren Clients ein aktueller Windows 10 Insider-Build ausgeführt werden.


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Erstellen Sie eine Richtlinie, und durchsuchen Sie die verfügbaren Einstellungen:

1. Wählen Sie in der Configuration Manager-Konsole **Bestand und Kompatibilität** aus.
2. Wählen Sie im Arbeitsbereich **Assets und Konformität** nacheinander **Übersicht** > **Endpoint Protection** > **Windows Defender Application Guard** aus.
3. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Windows Defender Application Guard-Richtlinie erstellen**.
4. Unter Verwendung des [Blogbeitrags](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97) als Referenz können Sie die verfügbaren Einstellungen durchsuchen und konfigurieren.
5. Geben Sie auf der Seite **Netzwerkdefinition** die Unternehmensidentität an, und definieren Sie die Grenze Ihres Unternehmensnetzwerks.

    > [!NOTE]
    > PCs unter Windows 10 speichern nur eine Netzwerkisolationsliste auf dem Client. Sie können zwei verschiedene Arten von Netzwerkisolationslisten erstellen und diese auf dem Client bereitstellen:
    >
    >  - eine aus Windows Information Protection
    >  - eine aus Windows Defender Application Guard
    >
    > Wenn Sie beide Richtlinien bereitstellen, müssen diese Netzwerkisolationlisten übereinstimmen. Wenn Sie Listen bereitstellen, die nicht mit dem gleichen Client übereinstimmen, schlägt die Bereitstellung fehl. Weitere Informationen finden Sie in der [Dokumentation zu Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
    > 
    > 

6. Wenn Sie fertig sind, schließen Sie den Assistenten ab, und stellen Sie die Richtlinie auf einem oder mehreren Windows 10-Geräten bereit.

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zu Windows Defender Application Guard finden Sie in [diesem Blogbeitrag](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Darüber hinaus finden Sie in [diesem Blogbeitrag](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903) weitere Informationen zum eigenständigen Modus von Windows Defender Application Guard.
