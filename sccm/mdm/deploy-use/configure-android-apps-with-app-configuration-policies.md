---
title: Konfigurieren von Android for Work-Apps mit Konfigurationsrichtlinien für Apps
titleSuffix: Configuration Manager
description: Vermeiden Sie Konfigurationsprobleme auf Geräten, die Android for Work ausführen, indem Sie Benutzern Richtlinien zur Konfiguration von Apps bereitstellen, bevor die Benutzer Apps ausführen.
ms.custom: na
ms.date: 09/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9126d188-7780-45a4-b21d-7fcf4fad7da2
caps.latest.revision: 0
caps.handback.revision: 0
author: NathBarn
ms.author: NathBarn
manager: angrobe
ms.openlocfilehash: 0b1d4993e6ddb2301121a1e32b1672425e919dea
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="apply-settings-to-android-for-work-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Anwenden von Einstellungen für Android for Work-Apps mit App-Konfigurationsrichtlinien in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können Konfigurationsrichtlinien für Apps in System Center Configuration Manager verwenden, um Einstellungen bereitzustellen, die beim Ausführen einer App durch den Benutzer erforderlich sein können. Beispielsweise kann eine App vom Benutzer Folgendes anfordern:
- Eine benutzerdefinierte Portnummer
- Spracheinstellungen
- Sicherheitseinstellungen
- Brandingeinstellungen wie z.B. ein Unternehmenslogo

Wenn der Benutzer die Einstellungen falsch eingibt, liegt die Last, sie zu beheben, auf Ihrem Help Desk, und die App-Bereitstellung ist langsam. Zur Vermeidung dieser Probleme können Sie App-Konfigurationsrichtlinien verwenden, um erforderliche Einstellungen für Benutzer bereitzustellen, bevor sie die App ausführen. Die Einstellungen werden automatisch einem Benutzer zugeordnet. Der Benutzer muss keine Maßnahmen ergreifen.
Anstatt Konfigurationsrichtlinien direkt für Benutzer und Geräte bereitzustellen, verknüpfen Sie eine Richtlinie mit einem Bereitstellungstyp, wenn Sie die App bereitstellen. Die Richtlinieneinstellungen werden immer dann angewendet wenn die App danach sucht – in der Regel beim ersten Ausführen der App.

Konfigurationsrichtlinien für Android-Apps stehen nur auf Geräten zur Verfügung, die Android for Work ausführen. App-Konfigurationsrichtlinien gelten für genehmigte Apps aus dem Play for Work-Store. Informationen zu Android-Apps, die per Volumenlizenz erworben wurden, finden Sie unter [Bereitstellen von Apps für Android for Work-Geräte](https://docs.microsoft.com/intune/deploy-use/android-for-work-apps).

Weitere Informationen zu App-Installationstypen finden Sie unter [Einführung in die Anwendungsverwaltung](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Erstellen einer Konfigurationsrichtlinie für Apps

1. Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **App-Konfigurationsrichtlinien** aus.
2. Wählen Sie auf der Registerkarte **Start** in der Gruppe **App-Konfigurationsrichtlinien** die Option **App-Konfigurationsrichtlinie erstellen** aus.
3. Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen einer App-Konfigurationsrichtlinie die folgenden Richtlinieninformationen an:
  - **Name**. Geben Sie einen eindeutigen Namen für die Richtlinie ein.
  - **Beschreibung**. Zur leichteren Identifizierung der Richtlinie können Sie optional eine Beschreibung hinzufügen.
  -  **Wählen Sie einen Konfigurationsrichtlinientyp aus**. Geben Sie die Plattform an, für die die App-Konfigurationsrichtlinie bestimmt ist: **Konfigurationsrichtlinie für Android for Work-Apps**.
  -  **Zugewiesene Kategorien zum leichteren Suchen und Filtern**. Wählen Sie optional zum Erstellen und Zuweisen von Kategorien für die Richtlinie **Kategorien** aus. Kategorien machen es einfacher für Sie, Elemente in der Configuration Manager-Konsole zu sortieren und zu finden.
4. Wählen Sie auf der Seite **Android for Work-Richtlinie** aus, wie Sie die Informationen zur Konfigurationsrichtlinie angeben möchten:
  - **Name und Wert-Paare angeben**. Sie können diese Option für Daten der Eigenschaftsliste verwenden, die keine Schachtelung verwenden. Angeben eines Name/Wert-Paars:
        1. Wählen Sie **Neu** aus, um ein neues JSON-Paar hinzuzufügen.
        2. Geben Sie im Dialogfeld **Name/Wert-Paar hinzufügen** Folgendes an:
            - **Typ**. Wählen Sie aus der Liste den Typ des Werts aus, den Sie angeben möchten.
            - **Name**. Geben Sie den Namen des Eigenschaftslistenschlüssels an, für den Sie einen Wert angeben möchten.
            - **Wert**. Geben Sie den Wert an, der für den eingegebenen Schlüssel festgelegt wird.

  - **Wechseln Sie zu einer JSON-Datei mit einer Eigenschaftsliste**. Verwenden Sie diese Option, wenn Sie bereits über eine JSON-Datei zum Konfigurieren einer App verfügen, oder für komplexere Dateien, die Schachtelung verwenden. Geben Sie im Feld **App-Konfigurationsrichtlinie** die Informationen zur Eigenschaftsliste im richtigen JSON-Format an.
5. Zum Importieren einer zuvor erstellten JSON-Datei wählen Sie **Datei auswählen** aus.
6. Wählen Sie **Weiter** aus. Falls Sie Fehler im JSON-Code feststellen, korrigieren Sie diese, bevor Sie fortfahren.
7. Schließen Sie die im Assistenten gezeigten Schritte ab.

Die neue App-Konfigurationsrichtlinie wird im Knoten **App-Konfigurationsrichtlinien** des Arbeitsbereichs **Softwarebibliothek** angezeigt.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Zuordnen einer Konfigurationsrichtlinie für Apps zu einer Configuration Manager-Anwendung

Um eine App-Konfigurationsrichtlinie mit der Bereitstellung einer Android for Work-App zuzuordnen, stellen Sie die Anwendung wie gewohnt bereit, indem Sie die Vorgehensweise im Thema [Bereitstellen von Anwendungen](/sccm/apps/deploy-use/deploy-applications) durchführen.

Wählen Sie im Assistenten zum Bereitstellen von Software auf der Seite **App-Konfigurationsrichtlinien** **Neu**. Wählen Sie anschließend im Dialogfeld **App-Konfigurationsrichtlinie auswählen** einen Bereitstellungstyp und die App-Konfigurationsrichtlinie aus, die Sie zuordnen möchten.
Bei der Installation des Bereitstellungstyps werden die Einstellungen der App-Konfigurationsrichtlinie automatisch angewendet.
