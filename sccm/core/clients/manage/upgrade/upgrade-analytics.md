---
title: Upgradebereitschaft
titleSuffix: System Center Configuration Manager
description: Integrieren Sie Upgrade Readiness mit Configuration Manager. Greifen Sie auf Daten zur Upgradekompatibilität in Ihrer Administratorkonsole zu. Führen Sie Upgrades oder Wartungen von Geräten aus.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 96f20c3559ac08cb4c5a16d1d33b74c63a02e4b7
ms.sourcegitcommit: f0bfd9fa0ec5b416f0ea2beee889b94e2ad9c97d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>Integrieren von Upgrade Readiness mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Upgradebereitschaft (früher Upgrade Analytics) ist ein Bestandteil von [Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics), mit dem Sie die Bereitschaft von Geräten in Ihrer Umgebung für ein Upgrade auf Windows 10 ermitteln und analysieren können. Sie können die betreffende Version konfigurieren. Upgradebereitschaft kann in Configuration Manager integriert werden, um auf Daten zur Konformität von Clientupgrades in der Configuration Manager-Verwaltungskonsole zuzugreifen. Mithilfe dynamischer Sammlungen, die auf der Grundlage dieser Daten erstellt wurden, können Sie Geräte für Upgrades oder Abhilfemaßnahmen gezielt auswählen.

Upgradebereitschaft ist eine Lösung in der [Microsoft Operations Management Suite (OMS)](/azure/operations-management-suite/operations-management-suite-overview). Erfahren Sie mehr über Upgradebereitschaft in [Manage Windows upgrades with Upgrade Readiness (Verwalten von Upgrades mit Upgradebereitschaft)](/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness).

<!--
>[!WARNING]
>For Upgrade Readiness to function within Configuration Manager, you must upgrade to Configuration Manager version 1802. The Upgrade Readiness Connector will no longer function in Configuration Manager versions earlier than 1802. 
SMS.507205 Pulled 4/5/18 -->


## <a name="configure-clients"></a>Konfigurieren von Clients

Upgradebereitschaft arbeitet wie alle Windows Analytics-Lösungen mit Windows-Telemetriedaten. Damit Upgradebereitschaft genügend Telemetriedaten empfangen kann, müssen die folgenden Voraussetzungen erfüllt sein:

- Alle Clients müssen mit einem **kommerziellen ID-Schlüssel** konfiguriert werden. 
- Bei Windows 10-Clients muss Telemetrie so konfiguriert sein, dass Telemetriedaten mindestens auf Basisebene gemeldet werden.
-  Auf Clients mit früheren Versionen von Windows müssen spezifische KB-Artikel installiert sein, wie in [Erste Schritte mit Upgradebereitschaft](/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs) beschrieben. Auf ihnen muss auch die Erfassung von Telemetrie in **Clienteinstellungen** aktiviert werden.

Kommerzielle ID-Schlüssel und Windows-Telemetrie können in **Clienteinstellungen** konfiguriert werden. Mehr erfahren Sie unter [Verwenden von Windows Analytics mit Configuration Manager](../monitor-windows-analytics.md).

>[!NOTE]
>Wenn Probleme dahingehend auftreten sollten, dass Upgradebereitschaft nicht wie erwartet Telemetriedaten von Geräten in Ihrer Umgebung empfängt, können einige dieser Probleme durch Verwendung des [Bereitstellungsskripts für Upgradebereitschaft](/windows/deployment/upgrade/upgrade-readiness-deployment-script) behoben werden. In den meisten Umgebungen, in denen die richtigen KB bereitgestellt werden, sollte die Konfiguration des kommerziellen ID-Schlüssels und der Telemetrie unter **Clienteinstellungen** ausreichen.

## <a name="connect-configuration-manager-to-upgrade-readiness"></a>Verbinden von Configuration Manager mit Upgradebereitschaft

Ab der Current Branch-Version 1706 kommt der [Assistent für Azure-Dienste](../../../servers/deploy/configure/azure-services-wizard.md) zum Einsatz, um die Konfiguration der von Ihnen verwendeten Azure-Dienste mit Configuration Manager zu vereinfachen. Ehe Sie Configuration Manager mit Upgradebereitschaft verbinden können, muss eine App-Registrierung bei Azure AD des Typs *Web-App/API* im [Azure-Portal](https://portal.azure.com) erstellt werden. Weitere Informationen zum Erstellen einer App-Registrierung finden Sie unter [Registrieren Ihrer Anwendung bei Ihrem Azure Active Directory-Mandanten](/azure/active-directory/active-directory-app-registration). Im **Azure-Portal** müssen Sie außerdem Ihrer neu registrierten Web-App die Berechtigung *Mitwirkender* für die Ressourcengruppe erteilen, die den OMS-Arbeitsbereich enthält, in dem sich Ihre Upgradebereitschaft-Daten befinden. Der **Assistent für Azure-Dienste** verwendet diese App-Registrierung, um Configuration Manager die sichere Kommunikation mit Azure AD zu ermöglichen und Ihre Infrastruktur mit Ihren Upgradebereitschaft-Daten zu verbinden.

>[!IMPORTANT]
>Die Berechtigung *Mitwirkender* muss der App selbst und nicht einer Azure AD-Benutzeridentität erteilt werden. Dies liegt daran, dass es die registrierte App und kein Azure AD-Benutzer ist, die im Auftrag Ihrer Configuration Manager-Infrastruktur auf die Daten zugreift. Beim Zuweisen von Berechtigungen müssen Sie im Bereich **Benutzer hinzufügen** nach dem Namen der App-Registrierung suchen, wenn Sie die Berechtigungen erteilen möchten. Beim [Bereitstellen von Configuration Manager mit Berechtigungen für OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) für Verbindungen mit [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm) gehen Sie genauso vor. Diese Schritte müssen ausgeführt werden, bevor die App-Registrierung mit dem *Assistenten für Azure-Dienste* in Configuration Manager importiert wird.

### <a name="use-the-azure-wizard-to-create-the-connection"></a>Verwenden des Assistenten für Azure-Dienste zum Erstellen der Verbindung

Befolgen Sie die Anweisungen unter [Konfigurieren von Azure-Diensten zur Verwendung mit Configuration Manager](../../../servers/deploy/configure/azure-services-wizard.md), um eine Verbindung mit Upgradebereitschaft herzustellen, indem Sie die zuvor erstellte Web-App-Registrierung importieren. 

Auf der Seite *Konfiguration* werden die folgenden Werte vorab ausgefüllt, wenn der Web-App-Import erfolgreich war und im **Azure-Portal** die richtigen Berechtigungen zugewiesen wurden. 
-  Azure-Abonnements
-  Azure-Ressourcengruppe
-  Windows Analytics-Arbeitsbereich

Mehr als eine Ressourcengruppe oder ein Arbeitsbereich sind nur verfügbar, wenn die registrierte Azure AD-Web-App über die Berechtigung *Mitwirkender* für mehr als eine Ressourcengruppe verfügt oder wenn die ausgewählte Ressourcengruppe mehr als einen OMS-Arbeitsbereich enthält.
 
## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>Anzeigen und Verwenden der Informationen zur Upgradebereitschaft in Configuration Manager

Nachdem Sie Upgradebereitschaft und Configuration Manager integriert haben, können Sie die Analyse der Upgradebereitschaft Ihrer Clients anzeigen.

1. Wählen Sie in der Configuration Manager-Konsole die Optionen **Überwachung** > **Übersicht** > **Upgrade Readiness** aus.
2. Überprüfen Sie die Daten, einschließlich des Status der Upgradebereitschaft und des Prozentsatzes an Windows-Geräten, die Telemetriedaten melden.
3. Sie können das Dashboard zum Anzeigen von Daten für Geräte in bestimmten Sammlungen filtern.
4. Sie können Geräte in einem bestimmten Bereitschaftsstatus anzeigen und eine dynamische Sammlung für sie erstellen. Wenn die Geräte bereit sind, können Sie ein Upgrade dieser Geräte ausführen oder entsprechende Maßnahmen auf Geräten ergreifen, auf denen das Upgrade blockiert wird.

## <a name="using-the-upgrade-readiness-connector-version-1702-and-earlier"></a>Verwenden des Connectors für Upgradebereitschaft (bis Version 1702)

In Configuration Manager-Versionen bis 1702 müssen andere Schrittfolgen ausgeführt und Voraussetzungen erfüllt werden, um eine Verbindung mit Upgradebereitschaft herzustellen.

### <a name="prerequisites"></a>Erforderliche Komponenten

- Um der Configuration Manager-Umgebung eine Verbindung hinzuzufügen, müssen Sie zunächst einen [Dienstverbindungspunkt](/sccm/core/servers/deploy/configure/about-the-service-connection-point) in einem [Onlinemodus](https://azure.microsoft.com/documentation/articles/resource-group-create-service-principal-portal/) konfigurieren. Wenn Sie Ihrer Umgebung eine Verbindung hinzufügen, wird auch der Microsoft Monitoring Agent auf dem Computer installiert, auf dem die Standortsystemrolle ausgeführt wird.
- Registrieren Sie Configuration Manager als „Webanwendung und/oder Web-API”-Verwaltungstool, und rufen Sie die [Client-ID dieser Registrierung](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/) ab.
- Erstellen Sie für das registrierte Verwaltungstool in Azure Active Directory einen Clientschlüssel.
- Geben Sie der registrierten Web-App im Azure-Portal Zugriff auf OMS, wie unter [Bereitstellen von Configuration Manager mit Berechtigungen für OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms) beschrieben.

    > [!IMPORTANT]
    > Achten Sie beim Konfigurieren der OMS-Zugriffsberechtigung darauf, dass Sie die Rolle **Mitwirkender** auswählen, und weisen Sie ihr Berechtigungen für die Ressourcengruppe der registrierten App zu.

### <a name="create-the-connection"></a>Erstellen der Verbindung

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Clouddienste** > **Upgrade Readiness Connector** > **Verbindung mit Upgrade Analytics erstellen** aus, um den **Assistent für das Hinzufügen einer Upgrade Analytics-Verbindung** zu starten.
3.  Geben Sie auf dem Bildschirm **Azure Active Directory** zunächst den **Mandanten**, die **Client-ID** und den **geheimen Clientschlüssel** ein, und wählen Sie anschließend **Weiter** aus.
4.  Geben Sie auf dem Bildschirm **Upgrade Readiness** die Verbindungseinstellungen ein, indem Sie Ihr **Azure-Abonnement**, die **Azure-Ressourcengruppe** und den **Operations Management Suite-Arbeitsbereich** angeben.
5.  Überprüfen Sie die Verbindungseinstellungen auf dem Bildschirm **Zusammenfassung**, und wählen Sie dann **Weiter** aus.

    > [!NOTE]
    > Sie müssen Upgrade Readiness mit dem Standort der obersten Ebene in der Hierarchie verbinden. Wenn Sie Upgrade Readiness mit einem eigenständigen primären Standort verbinden und dann Ihrer Umgebung einen Standort der zentralen Verwaltung hinzufügen, müssen Sie die OMS-Verbindung in der neuen Hierarchie löschen und neu erstellen.
