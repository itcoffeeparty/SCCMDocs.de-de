---
title: Synchronisieren von Daten | Microsoft Operations Management Suite | System Center Configuration Manager
description: Synchronisieren Sie Daten aus System Center Configuration Manager mit Microsoft Operations Management Suite.
ms.custom: na
ms.date: 10/13/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fbce476b8a9b91a88354fb4abfadfd2526ca5e8
ms.openlocfilehash: 5786f0734ce186601f5173003b9b133ed6ae8b11

---
# <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Synchronisieren von Daten von System Center Configuration Manager mit der Microsoft Operations Management Suite

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können nun mit dem Microsoft Operations Management Suite-Connector (OMS) Daten, z.B. Ihre Sammlungen, von System Center Configuration Manager mit OMS synchronisieren. Dadurch werden Daten aus der Configuration Manager-Bereitstellung in OMS sichtbar dargestellt.

## <a name="add-an-oms-connection-to-configuration-manager"></a>Hinzufügen einer OMS-Verbindung zu Configuration Manager

Um eine OMS-Verbindung zur Configuration Manager-Umgebung hinzuzufügen, müssen Sie zuerst einen [Dienstverbindungspunkt](../../../core/servers/deploy/configure/about-the-service-connection-point.md) in einem [Onlinemodus](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/) konfigurieren. Wenn Sie Ihrer Umgebung eine OMS-Verbindung hinzufügen, wird auch der Microsoft Monitoring Agent auf dem Computer installiert, auf dem die Standortsystemrolle ausgeführt wird.
1.  Wählen Sie im Arbeitsbereich **Verwaltung** **OMS-Connector** aus. Klicken Sie im Menüband auf „Verbindung mit Operations Management Suite erstellen“. Daraufhin wird der **Assistent für die Verbindung mit der Operations Management Suite** geöffnet. Wählen Sie **Weiter** aus.
2.  Vergewissern Sie sich auf dem Bildschirm **Allgemein**, dass Sie folgende Informationen besitzen, und wählen Sie **Weiter** aus.

    * Configuration Manager wurde als „Webanwendung und/oder Web-API”-Verwaltungstool registriert, und Sie haben die [Client-ID dieser Registrierung](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
    * Für das registrierte Verwaltungstool in Azure Active Directory wurde ein Clientschlüssel erstellt.
    * Im Azure Management Portal wurde die registrierte Web-App mit der Berechtigung bereitgestellt, auf OMS zuzugreifen, wie in [Provide Configuration Manager with permissions to OMS (Bereitstellen von Configuration Manager mit Berechtigungen für OMS)](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms) beschrieben.

3.  Konfigurieren Sie auf dem Bildschirm **Azure Active Directory** Ihre Verbindungseinstellungen zu OMS, indem Sie **Mandant**, **Client-ID** und **Geheimer Schlüssel** angeben und dann **Weiter** auswählen.
4.  Auf dem Bildschirm **OMS-Verbindungskonfiguration** geben Sie die Verbindungseinstellungen ein, indem Sie **Azure-Abonnement**, **Azure-Ressourcengruppe** und **Operations Management Suite-Arbeitsbereich** angeben.
5.  Überprüfen Sie die Verbindungseinstellungen auf dem Bildschirm **Zusammenfassung**, und wählen Sie dann **Weiter** aus. Auf dem Bildschirm **Status** wird der Verbindungsstatus angezeigt. Anschließend sollte **Abgeschlossen** angezeigt werden.

> [!NOTE]
> Sie müssen OMS mit dem Standort der obersten Ebene in der Hierarchie verbinden. Wenn Sie OMS mit einem eigenständigen primären Standort verbinden und dann Ihrer Umgebung einen Standort der zentralen Verwaltung hinzufügen, müssen Sie die OMS-Verbindung in der neuen Hierarchie löschen und neu erstellen.

Nachdem Sie Configuration Manager mit OMS verbunden haben, können Sie Sammlungen hinzufügen oder entfernen und die Eigenschaften der OMS-Verbindung anzeigen.

## <a name="viewing-microsoft-operations-management-suite-connection-properties-in-configuration-manager"></a>Anzeigen der Verbindungseigenschaften von Microsoft Operations Management Suite in Configuration Manager

1.  Navigieren Sie zu **Clouddienste**, und wählen Sie dann **OMS-Connector** aus, um die Seite **OMS-Verbindungseigenschaften** zu öffnen.
2.  Auf dieser Seite befinden sich zwei Registerkarten:
  * Die Registerkarte **Azure Active Directory** zeigt **Mandant**, **Client-ID**, **Client secret key expiration** (Ablauf des geheimen Clientschlüssels) an und ermöglicht Ihnen zu **Überprüfen**, ob **Geheimer Clientschlüssel** abgelaufen ist.
  * Die Registerkarte **OMS-Verbindungseigenschaften** zeigt **Azure-Abonnement**, **Azure-Ressourcengruppe**, **Operations Management Suite-Arbeitsbereich** und eine Liste der **Gerätesammlungen, für die die Operations Management Suite Daten abrufen kann**. Geben Sie mithilfe der Schaltfläche **Hinzufügen** und **Entfernen** an, welche Sammlungen zulässig sind.



<!--HONumber=Nov16_HO1-->


