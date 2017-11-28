---
title: "Aktionen bei Nichtkonformität"
titleSuffix: Configuration Manager
description: "Erfahren Sie, wie Sie Aktionen bei Nichtkonformität mit Configuration Manager einrichten."
ms.custom: na
ms.date: 11/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
caps.latest.revision: "18"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 1dd10d9452fae85f2ecc3d3077fba420454ef337
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="set-up-actions-for-non-compliance"></a>Einrichten von Aktionen bei Nichtkonformität

Die **Aktionen bei Nichtkonformität** erlauben es Ihnen, eine zeitlich geordnete Abfolge von Aktionen zu konfigurieren, die auf Geräte angewendet werden, die nicht konform sind. Beispielsweise können Sie E-Mails an den Endbenutzer von nicht konformen Geräten versenden und/oder diese Geräte als nicht konform kennzeichnen.

## <a name="before-you-begin"></a>Vorbereitung

> [!IMPORTANT]
> Sie müssen mindestens eine Richtlinie für die Gerätekonformität erstellt haben, um Aktionen bei Nichtkonformität einzurichten.

Dies sind die unterstützten Aktionen bei Nichtkonformität:

- E-Mail an Benutzer senden
- Geräte als nicht konform markieren

### <a name="send-e-mail-to-end-user"></a>E-Mail an Benutzer senden

Sie können aus vordefinierten Standard-E-Mail-Vorlagen wählen oder eine vollständig angepasste E-Mail-Benachrichtigung erstellen. Configuration Manager ermöglicht die individuelle Anpassung des Betreffs, des Nachrichtentexts, einschließlich des Firmenlogos, der Kontaktinformationen und weiterer Empfänger.

### <a name="mark-devices-non-compliant"></a>Geräte als nicht konform markieren

Sie können einen Zeitplan mit der Anzahl der Tage festlegen, die das Gerät für den Zugriff auf Unternehmensressourcen gesperrt werden soll. Dies kann sofort geschehen, aber Sie können dem Benutzer auch eine Frist einräumen, die Richtlinien zur Einhaltung der Gerätekonformität einzuhalten.

### <a name="supported-platforms"></a>Unterstützte Plattformen

Unterstützt von [allen über Intune verwalteten Plattformen](https://docs.microsoft.com/intune/supported-devices-browsers).

## <a name="to-add-an-email-template"></a>So fügen Sie eine E-Mail-Vorlage hinzu

Configuration Manager stellt E-Mail-Vorlagen zur Verfügung, Sie können aber auch eigene Vorlagen erstellen. Die E-Mail-Vorlage wird später bei der Erstellung von Aktionen bei Nichtkonformität für die Kommunikation mit den Benutzern verwendet.

1. Wählen Sie in der Configuration Manager-Konsole **Bestand und Kompatibilität** aus.

2. Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Konformitätseinstellungen**, und wählen Sie **Konformitätsbenachrichtigungsvorlagen**.

3. Klicken Sie auf der Registerkarte **Startseite** auf **Konformitätsbenachrichtigungsvorlage erstellen**.

4. Sie müssen die folgenden Informationen eingeben: a. Name: Name der E-Mail-Vorlage.
    b. Von : E-Mail-Adresse, die die E-Mail-Benachrichtigung sendet.
    c. Betreff: Ein Betreff, der die gesendete E-Mail-Benachrichtigung erläutert.
    d. Nachrichtentext: Weiter Details zur E-Mail-Benachrichtigung.

    > [!TIP] 
    > Sie können auch eine **E-Mail-Kopfzeile** mit Ihrem Unternehmenslogo und eine E-Mail-Fußzeile mit dem Unternehmensnamen sowie Kontaktinformationen einfügen. Diese Angaben können Sie auch in den Eigenschaften Ihres Intune-Abonnements ändern.

5. Klicken Sie auf **OK**, um die neue E-Mail-Vorlage zu speichern.

6. Auf der Seite **Aktion hinzufügen** können Sie Ihre neue E-Mail-Vorlage in der Liste auswählen.

7. Nachdem Sie Ihre E-Mail-Vorlage ausgewählt haben, klicken Sie auf **OK**.

## <a name="to-create-actions-for-non-compliance"></a>So erstellen Sie Aktionen bei Nichtkonformität

1. Wählen Sie in der Configuration Manager-Konsole **Bestand und Kompatibilität** aus.

2. Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, und wählen Sie **Kompatibilitätsrichtlinien**.

3. Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** **Kompatibilitätsrichtlinie erstellen**.

4. Wählen Sie den gewünschten Eintrag für **Unterstützte Plattformen**, und klicken Sie zweimal auf **Weiter**. Sie können die Seite **Regeln** überspringen.

5. Auf der Seite **Aktionen bei Nichtkonformität** legen Sie fest, was passiert, wenn ein Gerät nicht konform wird, und klicken Sie **Neu**.
6. Ihnen stehen zwei Optionen zur Wahl: **E-Mail an Benutzer senden** oder **Gerät als nicht konform markieren**.

7. Wenn **E-Mail an Benutzer senden** auswählen, müssen Sie Folgendes eingeben: a. **Karenzzeit (in Tagen):** Sie können 0-365 Tage eingeben.
    b. **Zusätzliche Empfänger (per E-Mail)** c. **E-Mail-Vorlage auswählen:** Sie können die Standard-E-Mail-Vorlagen oder die von Ihnen hinzugefügten benutzerdefinierten Vorlagen auswählen.
    
    > [!TIP] 
    > Sie können auch eine neue E-Mail-Vorlage hinzufügen, wenn Sie die Aktion **E-Mail an Benutzer senden** hinzufügen, indem Sie auf der Seite **Aktion hinzufügen** auf **Neu:** klicken.

8. Wenn Sie **Gerät als nicht konform markieren** auswählen, müssen Sie Folgendes eingeben: a. **Karenzzeit (in Tagen):** Sie können 0-365 Tage eingeben.

9. Sobald Sie die Aktion ausgewählt und die Einstellungen dafür eingegeben haben, klicken Sie zweimal auf **Weiter** und dann auf **Schließen**.


