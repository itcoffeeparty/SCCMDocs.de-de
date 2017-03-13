---
title: "Aktivieren einer Geräteschutzregel in einer Konformitätsrichtlinie | System Center Configuration Manager"
description: "Aktivieren einer Regel in der Gerätekonformitätsrichtlinie zum Schutz von Mobilgeräten vor Bedrohungen."
ms.custom: na
ms.date: 12/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 020f43e8-738e-4a82-91be-27b10cda9665
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 498b8c02dbf1391e6331c8b9ad7b6ef0fdef22d0
ms.openlocfilehash: 319289c9b211935ba10cb6d3da386ffed3c0153e
ms.lasthandoff: 02/23/2017


---
# <a name="create-a-lookout-device-threat-protection-rule"></a>Einrichten einer Regel zum Schutz vor Gerätebedrohungen mit Lookout

*Gilt für: System Center Configuration Manager (Current Branch)*

## <a name="before-you-begin"></a>Vorbereitung

Intune mit Lookout Mobile Threat Protection (MTP) ermöglicht Ihnen, Bedrohungen für Mobilgeräte zu erkennen und eine Risikobewertung für das Gerät vorzunehmen. Sie können eine Konformitätsrichtlinienregel in Configuration Manager erstellen, die die Risikoanalyse einschließt, um festzustellen, ob das Gerät als konform eingestuft wird. Anschließend können Sie den Zugriff auf Exchange, SharePoint und andere Dienste mit der Richtlinie für den bedingten Zugriff basierend auf der Gerätekonformität zulassen oder blockieren.

So können Sie die Konformitätsrichtlinie für das Gerät von der Lookout-Bedrohungserkennung abhängig machen

-   Die Regel **Schutz vor Gerätebedrohungen** muss in der Konformitätsrichtlinie aktiviert werden.

-   Auf der Seite **Lookout-Status** in der **Intune-Administratorkonsole** muss **Aktiv** angezeigt werden. Weitere Informationen und Anweisungen zum Aktivieren der Lookout-Integration finden Sie im Thema [Aktivieren der Lookout-MTP-Verbindung in Intune](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune).

Vor dem Erstellen der Regel zum Schutz vor Gerätebedrohungen in der Konformitätsrichtlinie empfehlen wir folgende Schritte:

1.  [Einrichten Ihres Lookout-Abonnements zum Schutz vor Gerätebedrohungen](https://docs.microsoft.com/sccm/protect/deploy-use/set-up-your-subscription-with-lookout)

2.  [Aktivieren der Lookout-Verbindung in Intune](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune)

3.  [Konfigurieren der Lookout for Work-App](https://docs.microsoft.com/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps)

>[!NOTE]
>Die Konformitätsregel wird erst nach Abschluss des Setups erzwungen.

## <a name="to-create-a-device-threat-protection-rule"></a>Einrichten einer Regel zum Schutz vor Gerätebedrohungen

Im Rahmen des Setups des Lookout-Schutzes vor Gerätebedrohungen in der [Lookout-Konsole](https://aad.lookout.com) haben Sie eine Richtlinie erstellen, die verschiedene Bedrohungen in die Stufen „Hoch“, „Mittel“ und „Niedrig“ klassifiziert. In der Intune-Konformitätsrichtlinie können Sie die maximal zulässige Bedrohungsstufe festlegen.

So richten Sie mit Lookout eine Regel zum Schutz vor Gerätebedrohungen ein:

1.  Klicken Sie in der Configuration Manager-Konsole auf den Arbeitsbereich **Bestand und Konformität**.

2.  Erweitern Sie unter **Bestand und Konformität** die **Konformitätsrichtlinien**.

3.  Klicken Sie mit der rechten Maustaste auf **Konformitätsrichtlinien**, und wählen Sie dann **Konformitätsrichtlinie erstellen** aus.

4.  Geben Sie den Namen der Konformitätsrichtlinie ein, und wählen Sie dann **Konformitätsregeln für Geräte, die ohne den Configuration Manager-Client verwaltet werden** aus.

5.  Wählen Sie die Betriebssystemplattformen aus, die mit der Konformitätsrichtlinie bereitgestellt werden (Android 4.1 und höher und/oder iOS 8 und höher).

6.  Klicken Sie auf der Seite **Regeln** auf **Neu**, um die Regeln für ein konformes Gerät anzugeben.

7.  Definieren Sie auf der Seite **Regel hinzufügen** eine neue Regel mit den folgenden Informationen:
    1.  Bedingung: Schutz vor Gerätebedrohungen – maximale Risikostufe.
    
    2.  Wert: Folgende Werte sind möglich:
        1.  **Keine (Geschützt)**: Dies ist die sicherste Option. Das bedeutet, dass auf dem Gerät keinerlei Bedrohungen zulässig sind. Bei jeglichem Fund einer Bedrohung (egal welcher Stufe) wird das Gerät als nicht konform ausgewertet.
        2.  **Niedrig**: Das Gerät wird als konform ausgewertet, wenn nur Bedrohungen der Stufe „Niedrig“ vorhanden sind. Jegliche Bedrohung einer höheren Stufe bewirkt, dass das Gerät in den Status „Nicht konform“ eingestuft wird.
        3.  **Mittel**: Das Gerät wird als konform ausgewertet, wenn die auf dem Gerät gefundenen Bedrohungen zur Stufe „Niedrig“ oder „Mittel“ gehören. Wenn Bedrohungen der Stufe „Hoch“ erkannt werden, wird das Gerät als „Nicht konform“ eingestuft.
        4.  **Hoch**: Dies ist die am wenigsten sichere Option. Im Prinzip lässt diese Option alle Bedrohungsstufen zu. Sie ist somit eigentlich nur zu Berichtszwecken nützlich.

>[!IMPORTANT]
>Wenn Sie Richtlinien für bedingten Zugriff für Office 365 und andere Dienste erstellen, wird die oben beschriebene Konformitätsbewertung berücksichtigt. Nicht konforme Geräte werden blockiert und dürfen auf Unternehmensressourcen erst wieder zugreifen, wenn die Bedrohung entfernt wurde.
