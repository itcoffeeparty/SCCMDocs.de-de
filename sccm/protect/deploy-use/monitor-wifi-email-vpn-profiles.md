---
title: "Überwachen von E-Mail-, WLAN- und VPN-Profilen | System Center Configuration Manager"
description: "Erfahren Sie mehr über das Überwachen des Kompatibilitätsstatus von E-Mail-, WLAN- und VPN-Profilen in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
caps.latest.revision: 4
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9ae359deaacb88804379622fa96e5fdb0e03b6bf


---

# <a name="monitor-email-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Überwachen von E-Mail-, WLAN- und VPN-Profilen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Nachdem Sie System Center Configuration Manager E-Mail-, WLAN- oder VPN-Profile für Benutzer in Ihrer Hierarchie bereitgestellt haben, können Sie mit den folgenden Verfahren den Kompatibilitätsstatus des Profils überwachen:  

-   [Anzeigen von Kompatibilitätsergebnissen in der Configuration Manager-Konsole](#BKMK_console)  

-   [Anzeigen von Kompatibilitätsergebnissen mithilfe von Berichten](#BKMK_Reports)  

##  <a name="a-namebkmkconsolea-how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a> Anzeigen von Kompatibilitätsergebnissen in der Configuration Manager-Konsole  
 Mit diesem Verfahren können Sie Details zur Kompatibilität der bereitgestellten Profile in der System Center Configuration Manager-Konsole anzeigen.  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>So zeigen Sie Kompatibilitätsergebnisse in der Configuration Manager-Konsole an  

1.  Klicken Sie in der System Center Configuration Manager-Konsole auf **Überwachung**.  

2.  Klicken Sie im Arbeitsbereich **Überwachung** auf **Bereitstellungen**.  

3.  Wählen Sie in der Liste **Bereitstellungen** die Bereitstellung der Profile aus, für die Sie die Kompatibilitätsinformationen prüfen möchten.  

4.  Zusammenfassende Informationen zur Kompatibilität der Bereitstellung der Profile finden Sie auf der Hauptseite. Wählen Sie zum Anzeigen ausführlicherer Informationen die Bereitstellung der Profile aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Status anzeigen**, um die Seite **Bereitstellungsstatus** anzuzeigen.  

     Auf der Seite **Bereitstellungsstatus** sind die folgenden Registerkarten enthalten:  

    -   **Kompatibel:** Zeigt die Kompatibilität des Profils basierend auf der Anzahl der betroffenen Bestände an. Sie können auf eine Regel doppelklicken, um unter dem Knoten **Benutzer** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer enthalten sind, die mit diesem Profil kompatibel sind. Im Bereich **Bestandsdetails** werden die Benutzer angezeigt, die mit dem Profil kompatibel sind. Doppelklicken Sie auf einen Benutzer in der Liste, um weitere Informationen anzuzeigen.  

        > [!IMPORTANT]  
        >  Ein Profil wird nicht ausgewertet, wenn es für ein Clientgerät nicht gilt. Es wird jedoch als kompatibel zurückgegeben.  

    -   **Fehler:** Zeigt eine Liste aller Fehler für die ausgewählte Bereitstellung des Profils basierend auf der Anzahl der betroffenen Bestände an. Sie können auf eine Regel doppelklicken, um unter dem Knoten **Benutzer** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer enthalten sind, durch die mit diesem Profil Fehler generiert wurden. Wenn Sie einen Benutzer auswählen, werden im Bereich **Bestandsdetails** die Benutzer angezeigt, die vom ausgewählten Problem betroffen sind. Doppelklicken Sie auf einen Benutzer in der Liste, um weitere Informationen über das Problem anzuzeigen.  

    -   **Nicht kompatibel** : Zeigt eine Liste aller nicht kompatiblen Regeln im Profil basierend auf der Anzahl der betroffenen Bestände an. Sie können auf eine Regel doppelklicken, um unter dem Knoten **Benutzer** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer enthalten sind, die mit diesem Profil nicht kompatibel sind. Wenn Sie einen Benutzer auswählen, werden im Bereich **Bestandsdetails** die Benutzer angezeigt, die vom ausgewählten Problem betroffen sind. Doppelklicken Sie auf einen Benutzer in der Liste, um weitere Informationen über das Problem anzuzeigen.  

    -   **Unbekannt:** Zeigt eine Liste aller Benutzer an, von denen keine Kompatibilität der ausgewählten Bereitstellung des Profils zusammen mit dem aktuellen Clientstatus von Geräten gemeldet wurde.  

5.  Auf der Seite **Bereitstellungsstatus** finden Sie ausführliche Informationen zur Kompatibilität des bereitgestellten Profils. Unter dem Knoten **Bereitstellungen** wird ein temporärer Knoten erstellt, mit dessen Hilfe Sie die Informationen schnell wiederfinden können.  

##  <a name="a-namebkmkreportsa-how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a> Anzeigen von Kompatibilitätsergebnissen mithilfe von Berichten  
 Zu den Kompatibilitätseinstellungen, in die auch die Profile in System Center Configuration Manager eingeschlossen sind, gehören verschiedene integrierte Berichte, mit denen Sie Informationen zu Profilen überwachen können. Diese Berichte verfügen über die Berichtskategorie **Kompatibilitäts- und Einstellungsverwaltung**.  

> [!IMPORTANT]  
>  Sie müssen ein Platzhalterzeichen (%) verwenden, wenn Sie in Berichten zu Kompatibilitätseinstellungen die Parameter **Gerätefilter** und **Benutzerfilter** eingestellt haben.  

 Weitere Informationen zum Konfigurieren der Berichterstellung in System Center Configuration Manager finden Sie unter [Berichterstellung in System Center Configuration Manager](../../core/servers/manage/reporting.md).  



<!--HONumber=Nov16_HO1-->


