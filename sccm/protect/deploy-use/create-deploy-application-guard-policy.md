---
title: Erstellen und Bereitstellen einer Windows Defender Application Guard-Richtlinie
titleSuffix: Configuraton Manager
description: Erstellen und Bereitstellen einer Windows Defender Application Guard-Richtlinie.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e7f0a1ccb71abb2fec27e0430bd4195dc85aceae
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Erstellen und Bereitstellen einer Windows Defender Application Guard-Richtlinie 
*Gilt für: System Center Configuration Manager (Current Branch)*
<!-- 1351960 -->
Sie können [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview)-Richtlinien erstellen und bereitstellen, indem Sie den Configuration Manager-Endpunktschutz verwenden. Diese Richtlinien dienen zum Schutz Ihrer Benutzer, indem nicht vertrauenswürdige Websites in einem sicheren isolierten Container geöffnet werden, auf den andere Teile des Betriebssystems keinen Zugriff haben.

## <a name="prerequisites"></a>Erforderliche Komponenten

Wenn Sie eine Windows Defender Application Guard-Richtlinie erstellen möchten, müssen Sie das Windows 10 Fall Creators Update (1709) verwenden. Außerdem müssen die Windows 10-Geräte, auf denen Sie die Richtlinie bereitstellen, mit einer Netzwerkisolationsrichtlinie konfiguriert werden. Weitere Informationen finden Sie in der [Übersicht über Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). 


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Erstellen Sie eine Richtlinie, und durchsuchen Sie die verfügbaren Einstellungen:

1. Wählen Sie in der Configuration Manager-Konsole **Assets und Konformität** aus.
2. Wählen Sie im Arbeitsbereich **Assets und Konformität** nacheinander **Übersicht** > **Endpoint Protection** > **Windows Defender Application Guard** aus.
3. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Windows Defender Application Guard-Richtlinie erstellen**.
4. Sie können die verfügbaren Einstellungen mithilfe des [Referenzartikels](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) durchsuchen und konfigurieren. Mit Configuration Manager können Sie Richtlinieneinstellungen festlegen. Weitere Informationen finden Sie unter [Einstellungen für die Hostinginteraktion](#BKMK_HIS) und [Anwendungsverhalten](#BKMK_AppB).
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

6. Schließen Sie den Assistenten ab, und stellen Sie die Richtlinie auf Windows 10-Geräten bereit, die die Version 1709 verwenden.

### <a name="bkmk_HIS"></a> Einstellungen für die Hostinginteraktion
Mit diesen werden Interaktionen zwischen Hostgeräten und dem Application Guard-Container konfiguriert. Vor Version 1802 von Configuration Manager befanden sich die Einstellungen für das Anwendungsverhalten und die Hostinginteraktion auf der Registerkarte **Einstellungen**.

- **Zwischenablage:** Vor Version 1802 von Configuration Manager befand sich diese Einstellung unter „Einstellungen“.
    - Zulässiger Inhaltstyp:
        - Text
        - Abbilder
- **Druckausgabe läuft:**
    - Drucken in XPS aktivieren
    - Drucken in PDF aktivieren
    - Drucken auf lokalen Netzwerkdruckern aktivieren
    - Enable printing to network printers (Drucken auf Netzwerkdruckern aktivieren)
- **Grafiken:** (ab Configuration Manager Version 1802)
    - Virtual graphics processor access (Zugriff auf virtuellen Grafikprozessor)
- **Dateien:** (ab Configuration Manager Version 1802)
    - Save downloaded files to host (Heruntergeladene Dateien auf Host speichern)

### <a name="bkmk_ABS"></a> Einstellungen für Anwendungsverhalten
Mit diesen wird das Anwendungsverhalten innerhalb der Application Guard-Sitzung konfiguriert. Vor Version 1802 von Configuration Manager befanden sich die Einstellungen für das Anwendungsverhalten und die Hostinginteraktion auf der Registerkarte **Einstellungen**.

- **Inhalt:**
   - Laden unternehmensfremder Inhalte wie z.B. Drittanbieter-Plug-Ins zulassen
- **Andere:**
    - Vom Benutzer generierte Browserdaten beibehalten
    - Sicherheitsereignisse in der isolierten Application Guard-Sitzung überwachen



## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zu Windows Defender Application Guard finden Sie unter [Windows Defender Application Guard Overview (Windows Defender Application Guard – Übersicht)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) und
[Windows Defender Application Guard FAQ (Windows Defender Application Guard – FAQ)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard).
