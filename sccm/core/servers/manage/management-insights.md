---
titleSuffix: Configuration Manager
description: Informationen zum Feature „Einblicke für die Verwaltung“, das in der Configuration Manager-Konsole verfügbar ist
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d2d6a58bd5aba873ea35c5bcf511a3cc22514b51
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="management-insights-in-system-center-configuration-manager"></a>Einblicke für die Verwaltung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Das Feature „Einblicke für die Verwaltung“ in System Center Configuration Manager stellt Informationen zum aktuellen Zustand Ihrer Umgebung bereit. Die Informationen basieren auf der Analyse von Daten aus der Standortdatenbank. Diese Einblicke vermitteln Ihnen ein genaueres Verständnis Ihrer Umgebung, sodass Sie entsprechende Maßnahmen ergreifen können. Dieses Feature wurde in Configuration Manager Version 1802 veröffentlicht. <!--1353967-->

## <a name="review-management-insights-in-the-configuration-manager-console"></a>Aufrufen der Einblicke für die Verwaltung in der Configuration Manager-Konsole 
Um die Regeln anzuzeigen, ist die **Leseberechtigung** erforderlich.

1. Öffnen Sie die Configuration Manager-Konsole. 
2. Wechseln Sie zum Knoten **Verwaltung**, und klicken Sie auf **Verwaltungseinblicke**.
3. Klicken Sie auf **Alle Einblicke**.
4. Doppelklicken Sie auf den **Gruppennamen des Verwaltungseinblicks**, den Sie anzeigen möchten. Alternativ können Sie sie auch markieren, und im Menüband auf **Einblicke anzeigen** klicken. 
5. In der Ansicht finden Sie vier Registerkarten zusammen mit den Anforderungen für das Ausführen der Regel. 
    - **Alle Regeln**: Bietet eine vollständige Liste der Regeln für die ausgewählte Gruppe der Einblicke für die Verwaltung.
    - **Abgeschlossen**: Listet die Regeln auf, die keine Aktion erfordern. 
    - **In Bearbeitung**: Zeigt Regeln an, für die einige, aber nicht alle Voraussetzungen erfüllt sind.
    - **Action Needed** (Aktion erforderlich): Führt die Regeln auf, die Aktionen erfordern. Klicken Sie mit der rechten Maustaste, und wählen Sie **Weitere Details** aus, um die Elemente abzurufen, für die eine Aktion erforderlich ist. 
    - **Erforderliche Komponenten**: Wenn eine Regel erfordert, dass bestimmte Elemente abgeschlossen werden müssen, bevor sie ausgeführt werden können, werden die erforderlichen Elemente hier angezeigt.   
    
    **Alle Regeln und Voraussetzungen für die Clouddienstgruppe** ![Verwaltungseinblicke – Alle Regeln und Voraussetzungen für die Clouddienstgruppe](./media/Management-insights-all-cloud-rules.png)

## <a name="management-insights-reevaluation-and-logging"></a>Erneute Auswertung und Protokollierung des Features „Verwaltungseinblicke“
Die Anwendbarkeit der Regeln für Verwaltungseinblicke werden wöchentlich neu ausgewertet. Sie können eine Regel manuell erneut auswerten, indem mit der rechten Maustaste auf die Regel und dann auf **Re-evaluate** (Erneut auswerten) klicken.

**Protokolldatei für Regeln für Verwaltungseinblicke:** SMS_DataEngine.log
## <a name="management-insights-groups-and-rules"></a>Gruppen und Regeln für Verwaltungseinblicke
Regeln werden in verschiedenen Gruppen von Verwaltungseinblicken organisiert. Wenn Gruppen und Regeln hinzugefügt werden, werden sie der folgenden Liste hinzugefügt:

**Anwendungen**: Einblicke für die Anwendungsverwaltung

- **Anwendungen ohne Bereitstellungen**: Listet diejenigen Anwendungen in Ihrer Umgebung auf, für die keine aktiven Bereitstellungen vorhanden sind. Mit dieser Regel können Sie nicht verwendete Anwendungen finden und löschen, um die in der Konsole angezeigte Anwendungsliste zu vereinfachen. 

**Clouddienste**: Hiermit können Sie mit vielen Clouddiensten integrieren und Ihre Geräte modern verwalten. 
 - **Assess co-management readiness** (Bereitschaft für die Co-Verwaltung bewerten): Damit können Sie nachvollziehen, welche Schritte zum Aktivieren der Co-Verwaltung erforderlich sind. Für diese Regel gibt es Voraussetzungen. 
 - **Enable your devices to be hybrid Azure Active Directory-joined** (Geräte für die hybride Verknüpfung mit Azure Active Directory aktivieren): Mit Azure AD verknüpfte Geräte ermöglichen es Benutzern, sich mit ihren Domänenanmeldeinformationen anzumelden, und gleichzeitig sicherzustellen, dass die Geräte die Sicherheits- und Konformitätsstandards der Organisation erfüllen. 
 - **Modernize your identity and access infrastructure** (Identitäts- und Zugriffsinfrastruktur modernisieren): Der Clouddienst Azure AD und die integrierte Multi-Factor Authentication schützen vertrauliche Daten und Anwendungen sowohl lokal als auch in der Cloud. 
 - **Upgrade your clients to Windows 10, version 1709 or above** (Clients auf Windows 10 Version 1709 oder höher upgraden): Windows 10 Version 1709 oder höher verbessert und modernisiert die Benutzererfahrung. 


**Sammlungen**: Einblicke, die die Verwaltung vereinfachen, indem sie Sammlungen bereinigen und neu konfigurieren.
   - **Leere Sammlungen**: Führt Sammlungen in Ihrer Umgebung auf, die keine Elemente enthalten. 

**Simplified Management** (Vereinfachte Verwaltung): Einblicke, die Ihnen helfen, die tägliche Verwaltung Ihrer Umgebung zu vereinfachen. 
   - **Outdated client versions** (Veraltete Clientversionen): Führt alle Clients auf, deren Versionen älter als zwei Jahre sind. 

**Softwarecenter**: Einblicke für die Verwaltung des Softwarecenters. 
   - **Direct users to Software Center instead of Application Catalog** (Benutzer zum Softwarecenter statt zum Anwendungskatalog weiterleiten): Überprüft, ob Benutzer in den letzten 14 Tagen Anwendungen aus dem Anwendungskatalog installiert oder angefordert haben. Die primäre Funktionalität des Anwendungskatalogs ist jetzt im Softwarecenter verfügbar. Die Unterstützung für die Website des Anwendungskatalogs endet mit dem ersten Update, das nach dem 1. Juni 2018 veröffentlicht wird.
   - **Use the new version of Software Center** (Neue Version des Softwarecenters verwenden): Die frühere Version des Softwarecenters wird nicht mehr unterstützt. Legen Sie fest, dass Clients das neue Softwarecenter verwenden, indem Sie die Clienteinstellung **Computer-Agent** >**Neues Softwarecenter verwenden** aktivieren.

**Windows 10:** Einblicke in die Bereitstellung und Wartung von Windows 10. Die Windows 10-Gruppe zu Einblicken in die Verwaltung ist verfügbar, wenn mehr als die Hälfte des Clients unter Windows 7, Windows 8 oder Windows 8.1 ausgeführt werden.
   - **Configure Windows telemetry and commercial ID key** (Windows-Telemetrie und kommerzielle ID-Schlüssel konfigurieren): Um Daten aus Upgradebereitschaft zu verwenden, müssen Geräte mit einem kommerziellen ID-Schlüssel konfiguriert werden und über aktivierte Telemetrie verfügen. Windows 10-Geräten müssen die Telemetrieebene „Enhanced (Limited)“ (Erweitert (Begrenzt)) oder höher haben.
   - **Connect Configuration Manager to Upgrade Readiness** (Configuration Manager mit Upgradebereitschaft verknüpfen): Nutzen Sie Upgradebereitschaft, um Ihre Windows 10-Bereitstellungen zu beschleunigen, bevor der Support für Windows 7 ausläuft. **Configure Windows telemetry and commercial ID key** ist eine Voraussetzung.

     **Regeln für Windows 10-Einblicke für die Verwaltung**
    ![Einblicke für die Verwaltung – Regeln für Windows 10](./media/Windows-10-insights-group.png)
    