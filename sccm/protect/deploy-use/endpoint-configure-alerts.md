---
title: Konfigurieren von Endpoint Protection-Warnungen | Microsoft-Dokumentation
description: Konfigurieren von Endpoint Protection-Warnungen in Microsoft System Center 2012 Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 7ade196766d036f5dbca2b39efad380c7895847c


---

#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Konfigurieren von Warnungen für Endpoint Protection in Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

 Sie können Endpoint Protection-Warnungen in Microsoft System Center Configuration Manager konfigurieren, um Administratoren zu benachrichtigen, wenn bestimmte Ereignisse in der Hierarchie auftreten, wie Infektionen mit Schadsoftware. Das Endpoint Protection-Dashboard in der Configuration Manager-Konsole zeigt Benachrichtigungen im Knoten **Warnungen** des Arbeitsbereichs **Überwachung** an, oder kann per E-Mail an angegebene Benutzer versendet werden.

 Führen Sie die folgenden Schritte und zusätzlichen Verfahren aus, die in diesem Thema beschrieben werden, um Warnungen für Endpoint Protection in Configuration Manager zu konfigurieren.

> [!IMPORTANT]
>  Sie benötigen die Berechtigung **Sicherheit erzwingen** für Sammlungen, um Endpoint Protection-Warnungen zu konfigurieren.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Schritte zum Konfigurieren von Warnungen für Endpoint Protection in Configuration Manager

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen**.

3.  Wählen Sie in der Liste **Gerätesammlungen** die Sammlung aus, für die Sie Warnungen konfigurieren möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.

    > [!NOTE]
    >  Es können keine Benachrichtigungen für Benutzersammlungen konfiguriert werden.

4.  Wählen Sie auf der Registerkarte **Warnungen** des Dialogfelds *<Sammlungsname\>***Eigenschaften** die Option **Diese Sammlung im Endpoint Protection-Dashboard anzeigen** aus, wenn Details der Antischadsoftware-Vorgänge für diese Sammlung im Arbeitsbereich **Überwachung** der Configuration Manager-Konsole angezeigt werden sollen.

    > [!NOTE]
    >  Diese Option ist nicht für die Sammlung **Alle Systeme** verfügbar.

5.  Klicken Sie auf der Registerkarte **Warnungen** des Dialogfelds *<Sammlungsname\>***Eigenschaften** auf **Hinzufügen**.

6.  Wählen Sie im Dialogfeld **Neue Sammlungswarnungen hinzufügen** im Bereich **Warnung generieren, wenn die folgenden Bedingungen erfüllt sind** die Warnungen aus, die von Configuration Manager generiert werden sollen, wenn festgelegte Endpoint Protection-Ereignisse eintreten, und klicken Sie dann auf **OK**.

7.  Wählen Sie in der Liste **Bedingungen** auf der Registerkarte **Warnungen** jede Endpoint Protection-Warnung aus, und geben Sie die folgenden Informationen an:

    -   **Warnungsname** ‒ Übernehmen Sie den Standardnamen, oder geben Sie einen neuen Namen für die Warnung ein.

    -   **Warnungsschweregrad** ‒ Wählen Sie aus der Liste den Schweregrad aus, der in der Configuration Manager-Konsole angezeigt werden soll.

8.  Geben Sie je nach ausgewählter Warnung die folgenden zusätzlichen Informationen an:

    -   **Schadsoftwareerkennung** ‒ Diese Warnung wird generiert, wenn auf einem Computer in der überwachten Sammlung Schadsoftware erkannt wird. Der **Schwellenwert für die Schadsoftwareerkennung** gibt den Schwellenwert für die Schadsoftwareerkennung an, bei der diese Warnung generiert wird:

        -   **Hoch – Alle Erkennungen** ‒ Diese Warnung wird generiert, wenn auf mindestens einem Computer der angegebenen Sammlung Schadsoftware erkannt wird, unabhängig davon, welche Aktion vom Endpoint Protection-Client ausgeführt wird.

        -   **Mittel – Erkannt, Aktion steht aus** ‒ Diese Warnung wird generiert, wenn auf mindestens einem Computer der angegebenen Sammlung Schadsoftware erkannt wird, die manuell entfernt werden muss.

        -   **Niedrig – Erkannt, noch aktiv** ‒ Diese Warnung wird generiert, wenn auf mindestens einem Computer der angegebenen Sammlung Schadsoftware erkannt wird, die noch aktiv ist.

    -   **Schadsoftwareausbruch** ‒ Diese Warnung wird generiert, wenn auf einem bestimmten Prozentsatz aller Computer der überwachten Sammlung eine bestimmte Schadsoftware erkannt wird.

        -   **Prozentsatz der von Schadsoftware betroffenen Computer** ‒ Diese Warnung wird generiert, wenn der Prozentsatz der Computer mit Schadsoftware, die in der Sammlung erkannt werden, Ihren angegebenen Prozentsatz übersteigt. Geben Sie einen Prozentsatz von **1** bis **99**an.

            > [!NOTE]
            >  Der Prozentwert basiert auf der Anzahl der Computer in der Sammlung, wobei Computer ausgeschlossen sind, auf denen kein Configuration Manager-Client installiert ist. Eingeschlossen sind Computer, auf denen der Endpoint Protection-Client noch nicht installiert ist.

    -   **Wiederholte Erkennung von Malware** ‒ Diese Warnung wird generiert, wenn bestimmte Schadsoftware häufiger als eine angegebene Anzahl über eine angegebene Anzahl von Stunden auf den Computern in der Sammlung, die Sie überwachen, gefunden wird. Geben Sie die folgenden Informationen ein, um diese Warnung zu konfigurieren:

        -   **Häufigkeit der Erkennung der Schadsoftware:** Die Warnung wird generiert, wenn dieselbe Schadsoftware auf Computern in der Sammlung öfter erkannt wird, als festgelegt wurde. Geben Sie eine Zahl von **2** bis **32**an.

        -   **Erkennungsintervall (Stunden):** Geben Sie das Erkennungsintervall (in Stunden) an, in dem die festgelegte Anzahl von Schadsoftware-Erkennungen erfolgen muss. Geben Sie eine Zahl von **1** bis **168**an.

    -   **Erkennung mehrerer Schadsoftwaretypen** – Diese Warnung wird generiert, wenn mehr als eine angegebene Anzahl von Schadsoftwaretypen über eine angegebene Anzahl von Stunden auf Computern in der Sammlung, die Sie überwachen, erkannt werden. Geben Sie die folgenden Informationen ein, um diese Warnung zu konfigurieren:

        -   **Anzahl der entdeckten Schadsoftwaretypen:** Die Warnung wird generiert, wenn eine angegebene Anzahl unterschiedlicher Schadsoftwaretypen auf Computern in der Sammlung erkannt wird. Geben Sie eine Zahl von **2** bis **32**an.

        -   **Erkennungsintervall (Stunden):** Geben Sie das Erkennungsintervall (in Stunden) an, in dem die festgelegte Anzahl von Schadsoftware-Erkennungen erfolgen muss. Geben Sie eine Zahl von **1** bis **168**an.

9. Klicken Sie auf **OK**, um das Dialogfeld *<Sammlungsname\>***Eigenschaften** zu schließen.  

> [!div class="button"]
[Nächster Schritt >](endpoint-definition-updates.md)

> [!div class="button"]
[Zurück >](endpoint-protection-site-role.md)



<!--HONumber=Dec16_HO3-->


