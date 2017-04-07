---
title: 'Synchronisieren von Daten | Microsoft-Dokumentation | Microsoft Operations Management Suite '
description: Synchronisieren Sie Daten aus System Center Configuration Manager mit Microsoft Operations Management Suite.
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 3acfaa2cf8c64ece5cef65b80372067336d6a815
ms.lasthandoff: 03/27/2017

---


# <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Synchronisieren von Daten von System Center Configuration Manager mit der Microsoft Operations Management Suite


*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können nun mit dem Microsoft Operations Management Suite-Connector (OMS) Daten, z.B. Ihre Sammlungen, von System Center Configuration Manager mit den OMS-Protokollanalyseressourcen in Microsoft Azure synchronisieren. Dadurch werden Daten aus der Configuration Manager-Bereitstellung in OMS sichtbar dargestellt.
> [!TIP]
> Der OMS-Connector ist ein vorab veröffentlichtes Feature. Weitere Informationen erhalten Sie unter [Use pre-release features from updates (Verwenden von vorab veröffentlichten Features von Updates)](/sccm/core/servers/manage/pre-release-features).

Ab Version 1702 können Sie den OMS-Connector für die Verbindung mit einem OMS-Arbeitsbereich verwenden, der sich in der Microsoft Azure Government-Cloud befindet. Dazu müssen Sie eine Konfigurationsdatei ändern, bevor Sie den OMS-Connector installieren. Weitere Informationen finden Sie unter [Verwenden des OMS-Connectors mit der Azure Government-Cloud](#fairfaxconfig) in diesem Thema.

## <a name="prerequisites"></a>Voraussetzungen
- Bevor Sie den OMS-Connector in Configuration Manager installieren, müssen Sie Configuration Manager mit Berechtigungen für OMS bereitstellen. Sie müssen insbesondere den *Zugriff als Mitwirkender* in der Azure-*Ressourcengruppe* gewähren, die den OMS-Protokollanalyse-Arbeitsbereich enthält. Die Vorgehensweisen dazu werden im Protokollanalysen-Inhalt dokumentiert. Informationen finden Sie in der OMS-Dokumentation unter [Bereitstellen von Configuration Manager mit Berechtigungen für OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms).

- Der OMS-Connector muss auf dem Computer installiert werden, der einen [Dienstverbindungspunkt](/sccm/core/servers/deploy/configure/about-the-service-connection-point) hostet, der sich in [Onlinemodus](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation) befindet.

  Wenn Sie OMS mit einem eigenständigen primären Standort verbunden haben und planen, Ihrer Umgebung einen Standort der zentralen Verwaltung hinzuzufügen, müssen Sie die aktuelle Verbindung löschen und anschließend den Connector am neuen Standort der zentralen Verwaltung erneut konfigurieren.

- Sie müssen Microsoft Monitoring Agent für OMS auf den Dienstverbindungspunk zusammen mit den OMS-Connector installieren.  Der Agent und der OMS-Connector müssen so konfiguriert werden, dass sie den gleichen **OMS-Arbeitsbereich** nutzen. In der OMS-Dokumentation unter [Herunterladen und Installieren des Agents](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) finden Sie Informationen zur Installation des Agents.

- Nachdem Sie den Connector und den Agent installiert haben, müssen Sie OMS für die Verwendung von Configuration Manager-Daten konfigurieren.  Dazu gehen Sie im OMS-Portal unter [Importieren von Sammlungen](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).



## <a name="install-the-oms-connector"></a>Installieren des OMS-Connectors  
1. Konfigurieren Sie in der Configuration Manager-Konsole Ihre [Hierarchie zur Verwendung von Features der Vorabversion](/sccm/core/servers/manage/pre-release-features), und aktivieren Sie die Verwendung des OMS-Connectors.  

2. Navigieren Sie als nächstes zu **Verwaltung** > **Clouddienste** > **OMS-Connector**. Klicken Sie im Menüband auf „Verbindung mit Operations Management Suite erstellen“. Daraufhin wird der **Assistent für die Verbindung mit der Operations Management Suite** geöffnet. Wählen Sie **Weiter** aus.  


3.    Vergewissern Sie sich auf der Seite **Allgemein**, dass Sie folgende Informationen besitzen, und wählen Sie **Weiter** aus.  
  - Configuration Manager wurde als „Webanwendung und/oder Web-API”-Verwaltungstool registriert, und Sie haben die [Client-ID dieser Registrierung](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).  
  - Für das registrierte Verwaltungstool in Azure Active Directory wurde ein Clientschlüssel erstellt.  

  - Im Azure Management Portal wurde die registrierte Web-App mit der Berechtigung bereitgestellt, auf OMS zuzugreifen, wie in [Provide Configuration Manager with permissions to OMS (Bereitstellen von Configuration Manager mit Berechtigungen für OMS)](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) beschrieben.  

4.    Konfigurieren Sie auf der Seite **Azure Active Directory** Ihre Verbindungseinstellungen zu OMS, indem Sie **Mandant**, **Client-ID** und **Geheimer Schlüssel** angeben und dann **Weiter** auswählen.  

5.    Auf der Seite **OMS-Verbindungskonfiguration** geben Sie die Verbindungseinstellungen ein, indem Sie **Azure-Abonnement**, **Azure-Ressourcengruppe** und **Operations Management Suite-Arbeitsbereich** angeben.  Der Arbeitsbereich muss mit dem Arbeitsbereich übereinstimmen, der für den Microsoft-Verwaltungs-Agent konfiguriert ist, der auf dem Dienstverbindungspunkt installiert ist.  

6.    Überprüfen Sie die Verbindungseinstellungen auf der Seite **Zusammenfassung**, und wählen Sie dann **Weiter** aus. Auf der Seite **Status** wird der Verbindungsstatus angezeigt. Anschließend sollte **Abgeschlossen** angezeigt werden.

Nachdem Sie Configuration Manager mit OMS verbunden haben, können Sie Sammlungen hinzufügen oder entfernen und die Eigenschaften der OMS-Verbindung anzeigen.

## <a name="verify-the-oms-connector-properties"></a>Überprüfen der Eigenschaften des OMS-Connectors
1.    Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clouddienste**, wählen Sie dann **OMS-Connector** aus, um die Seite **OMS-Verbindung**** zu öffnen.
2.    Auf dieser Seite befinden sich zwei Registerkarten:
  - **Azure Active Directory:**   
    Diese Registerkarte zeigt **Mandant**, **Client-ID**, **Client secret key expiration** (Ablauf des geheimen Clientschlüssels) an und ermöglicht Ihnen zu Überprüfen, ob Ihr geheimer Clientschlüssel abgelaufen ist.

  - **OMS-Verbindungseigenschaften:**  
    Diese Registerkarte zeigt **Azure-Abonnement**, **Azure-Ressourcengruppe**, **Operations Management Suite-Arbeitsbereich** und eine Liste der **Gerätesammlungen, für die die Operations Management Suite Daten abrufen kann**. Geben Sie mithilfe der Schaltfläche **Hinzufügen** und **Entfernen** an, welche Sammlungen zulässig sind.

## <a name="fairfaxconfig"> </a> Verwenden des OMS-Connectors mit der Azure Government-Cloud


1.  Bearbeiten Sie auf jedem Computer, auf dem die Configuration Manager-Konsole installiert ist, die folgende Konfigurationsdatei, damit sie auf die Government-Cloud zeigt: ***&lt;Installationspfad_von_Configuration_Manager>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Bearbeitungen:**

    Ändern Sie den Wert für die Einstellung *FairFaxArmResourceID* in „https://management.usgovcloudapi.net/“.

   - **Original:**
      &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **Bearbeitet:**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  Ändern Sie den Wert für die Einstellung *FairFaxAuthorityResource* in „https://login.microsoftonline.com/“.

  - **Original:**
    &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

    - **Bearbeitet:**
    &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.com/&lt;/value>

2.    Nachdem Sie die Datei mit den zwei Änderungen gespeichert haben, starten Sie die Configuration Manager-Konsole auf demselben Computer neu, und installieren Sie anschließend den OMS-Connector über die Konsole. Verwenden Sie für die Installation des Connectors die Informationen in [Synchronisieren von Daten von System Center Configuration Manager mit der Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite), und wählen Sie den **Operations Management Suite-Arbeitsbereich** aus, der sich in der Microsoft Azure Government-Cloud befindet.

3.    Nach der erfolgreichen Installation des OMS-Connectors steht Ihnen die Verbindung zur Government-Cloud von jeder Konsole aus zur Verfügung, die sich mit dem Standort verbindet.

