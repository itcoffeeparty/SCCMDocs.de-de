---
title: "Überwachen von Anwendungen über die System Center Configuration Manager-Konsole | System Center Configuration Manager"
description: "Überwachen Sie die Bereitstellung von Software, einschließlich Updates, Kompatibilitätseinstellungen und Anwendungen, mithilfe des Arbeitsbereichs „Überwachung“ in Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ca82638267d6d9e1bb4eb6855785ac383a2191e9


---
# <a name="monitor-applications-from-the-system-center-configuration-manager-console"></a>Überwachen von Anwendungen in der System Center Configuration Manager-Konsole

*Gilt für: System Center Configuration Manager (Current Branch)*


## <a name="introduction"></a>Einführung

Sie können in System Center Configuration Manager die Bereitstellung der gesamten Software überwachen, z.B. Softwareupdates, Kompatibilitätseinstellungen, Anwendungen, Tasksequenzen sowie Pakete und Programme. Sie können Bereitstellungen über den Arbeitsbereich **Überwachung** in der Configuration Manager-Konsole oder mithilfe von Berichten überwachen.  

 Für Anwendungen in Configuration Manager wird eine zustandsbasierte Überwachung unterstützt, sodass Sie den letzten Anwendungsbereitstellungszustand für Benutzer und Geräte nachverfolgen können. In diesen Zustandsmeldungen werden Informationen über einzelne Geräte angegeben. Wenn beispielsweise eine Anwendung für eine Sammlung von Benutzern bereitgestellt wird, können Sie den Kompatibilitätszustand und den Zweck der Bereitstellung in der Configuration Manager-Konsole anzeigen.  

 Für einen Anwendungsbereitstellungszustand wird einer der folgenden Kompatibilitätszustände angezeigt:  

-   **Erfolg** : Die Anwendung wurde erfolgreich bereitgestellt oder war bereits installiert.  

-   **In Bearbeitung** : Die Anwendungsbereitstellung wird ausgeführt.  

-   **Unbekannt** : Der Zustand der Anwendungsbereitstellung konnte nicht ermittelt werden. Dieser Zustand gilt nicht für Bereitstellungen mit dem Zweck **Verfügbar**. Dieser Zustand wird in der Regel angezeigt, wenn noch keine Zustandsmeldungen vom Client eingegangen sind.  

-   **Anforderungen nicht erfüllt** : Die Anwendung wurde nicht bereitgestellt, weil sie mit einer Abhängigkeit oder einer Anforderungsregel nicht kompatibel war oder weil das Zielbetriebssystem für die Bereitstellung ungültig war.  

-   **Fehler** : Bei der Bereitstellung der Anwendung ist ein Fehler aufgetreten.  
  
Sie können für jeden Kompatibilitätszustand zusätzliche Informationen anzeigen, wie zum Beispiel Unterkategorien im Kompatibilitätszustand oder die Anzahl der Benutzer und Geräte in dieser Kategorie. Der Kompatibilitätszustand **Fehler** enthält beispielsweise die folgenden Unterkategorien:  
  
-   Fehler beim Auswerten von Anforderungen  

-   Inhaltsfehler  

-   Installationsfehler  

 Wenn auf eine Anwendungsbereitstellung mehrere Kompatibilitätszustände zutreffen, wird der aggregierte Zustand mit der geringsten Kompatibilität angezeigt. Beispiel:  

-   Wenn ein Benutzer sich bei zwei Geräten anmeldet und die Anwendung auf einem Gerät erfolgreich ist, auf dem anderen dagegen ein Fehler auftritt, wird für diesen Benutzer der Aggregatzustand **Fehler**für die Anwendungsbereitstellung angezeigt.  

-   Wenn eine Anwendung für alle Benutzer bereitgestellt wird, die sich bei einem Computer anmelden, werden für diesen Computer mehrere Bereitstellungsergebnisse angezeigt. Wenn bei einer Bereitstellung ein Fehler auftritt, wird für den Computer der Aggregatbereitstellungszustand **Fehler**angezeigt.  
  
Der Bereitstellungszustand für Paket- und Programmbereitstellungen wird nicht aggregiert.  
  
 Mithilfe dieser Unterkategorien können Sie Probleme bei der Anwendungsbereitstellung schnell identifizieren. Sie können außerdem zusätzliche Informationen zu den Geräten anzeigen, die zu einer bestimmten Unterkategorie eines Kompatibilitätszustands gehören.  

 Die Anwendungsverwaltung in Configuration Manager umfasst mehrere integrierte Berichte, mit deren Hilfe Daten zu Anwendungen und Bereitstellungen überwacht werden können. Die Berichte gehören zur Berichtkategorie **Softwareverteilung – Anwendungsüberwachung**.  

 Weitere Informationen zum Konfigurieren der Berichterstellung in Configuration Manager finden Sie unter [Berichterstellung in System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Überwachen des Zustands einer Anwendung in der Configuration Manager-Konsole  
  
1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung** > **Bereitstellungen**.  
  
3.  Wenn Sie die Bereitstellungsdetails für jeden Kompatibilitätszustand und die Geräte in diesem Zustand überprüfen möchten, wählen Sie eine Bereitstellung aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Status anzeigen** , um den Bereich **Bereitstellungsstatus** anzuzeigen. In diesem Bereich können Sie für alle Kompatibilitätszustände anzeigen, welche Bestände den jeweiligen Zustand aufweisen. Klicken Sie auf einen Bestand, um detaillierte Informationen zu dessen Bereitstellungsstatus anzuzeigen.  

    > [!NOTE]  
    >  Im Bereich **Bereitstellungsstatus** können maximal 20.000 Elemente angezeigt werden. Verwenden Sie Configuration Manager-Berichte, um Anwendungsstatusdaten zu einer größeren Anzahl von Elementen anzuzeigen.  
    >   
    >  Der Status von Bereitstellungstypen wird im Bereich **Bereitstellungsstatus** aggregiert. Verwenden Sie den Bericht **Fehler in der Anwendungsinfrastruktur** in der Berichtskategorie **Softwareverteilung – Anwendungsüberwachung**, um ausführlichere Informationen zu Bereitstellungstypen anzuzeigen.  

4.  Wählen Sie eine Bereitstellung aus, und klicken Sie dann im Fenster **Ausgewählte Bereitstellungseigenschaften** auf die Registerkarte **Zusammenfassung** , um allgemeine Statusinformationen zu einer Anwendungsbereitstellung anzuzeigen.  

5.  Wählen Sie eine Bereitstellung aus, und klicken Sie dann im Fenster **Ausgewählte Bereitstellungseigenschaften** auf die Registerkarte **Bereitstellungstypen** , um Informationen zum Anwendungsbereitstellungstyp zu überprüfen.  

Bei den Informationen, die nach dem Klicken auf **Status anzeigen** im Bereich **Bereitstellungsstatus** angezeigt werden, handelt es sich um Livedaten aus der Configuration Manager-Datenbank. Bei den Informationen, die auf den Registerkarten **Zusammenfassung** und **Bereitstellungstypen** angezeigt wird, handelt es sich um zusammengefasste Daten. Klicken Sie auf **Zusammenfassung ausführen** , wenn die auf den Registerkarten **Zusammenfassung** und **Bereitstellungstypen** angezeigten Daten nicht mit den Daten im Bereich **Bereitstellungsstatus** übereinstimmen, um die Daten auf diesen Registerkarten zu aktualisieren. Gehen Sie folgendermaßen vor, um das Standardintervall für die Zusammenfassung von Anwendungsbereitstellungsdaten zu konfigurieren:  
1. Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Standortkonfiguration** > **Standorte**.
2. Wählen Sie in der Liste **Standorte** den Standort aus, für den Sie das Zusammenfassungsintervall konfigurieren möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Statuszusammenfassungen**.
3. Klicken Sie im Dialogfeld **Statuszusammenfassungen** auf **Anwendungsbereitstellung – Zusammenfassung**, und klicken Sie dann auf **Bearbeiten**.  
4. Konfigurieren Sie im Dialogfeld **Anwendungsbereitstellung – Zusammenfassung** die erforderlichen Zusammenfassungsintervalle, und klicken Sie dann auf **OK**.  



<!--HONumber=Nov16_HO1-->


