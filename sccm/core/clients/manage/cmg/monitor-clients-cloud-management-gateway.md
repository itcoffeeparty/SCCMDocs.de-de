---
title: Überwachen des Cloudverwaltungsgateways
titleSuffix: Configuration Manager
description: Überwachen Sie Clients und Netzwerkdatenverkehr mit Cloud Management Gateway.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18a98ae924b985b08aed911797b07ef0a1974420
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Überwachen des Cloudverwaltungsgateways in Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn CMG ausgeführt wird und Clients über diesen Dienst eine Verbindung herstellen, können Sie Clients und den Netzwerkdatenverkehr überwachen, um sich über die Leistung des Diensts zu informieren.



## <a name="monitor-clients"></a>Überwachen von Clients

Clients, die über CMG verbunden sind, werden genauso wie lokale Clients in der Configuration Manager-Konsole angezeigt. Weitere Informationen finden Sie unter [Überwachen von Clients in System Center Configuration Manager](/sccm/core/clients/manage/monitor-clients).



## <a name="monitor-traffic-in-the-console"></a>Überwachen von Datenverkehr in der Konsole

Sie können Datenverkehr über CMG mithilfe der Configuration Manager-Konsole wie folgt überwachen:

1. Gehen Sie zu **Verwaltung > Clouddienste > Cloud Management Gateway** (Cloudverwaltungsgateway).

2. Wählen Sie im Listenbereich Cloud Management Gateway aus.

3. Sehen Sie sich die Informationen zum Datenverkehr im Detailbereich für den CMG-Verbindungspunkt und die Standortsystemrollen an, mit denen eine Verbindung hergestellt wird.



## <a name="set-up-outbound-traffic-alerts"></a>Einrichten von Warnungen für ausgehenden Datenverkehr

Durch Warnungen für ausgehenden Datenverkehr erfahren Sie, wann der für den Zeitraum von 14 Tagen festgelegte Schwellenwert für den Netzwerkdatenverkehr erreicht wird. Wenn Sie Cloud Management Gateway hinzufügen, können Sie Warnungen für den Datenverkehr einrichten. Wenn Sie diesen Teil übersprungen haben, können Sie noch immer die Warnungen einrichten, wenn der Dienst ausgeführt wird. Die Warnungseinstellungen lassen sich jederzeit anpassen.

1. Gehen Sie zu **Verwaltung > Clouddienste > Cloud Management Gateway** (Cloudverwaltungsgateway).

2. Klicken Sie mit der rechten Maustaste im Listenbereich zuerst auf Cloud Management Gateway, und klicken Sie anschließend auf **Eigenschaften**.

3. Klicken Sie auf die Registerkarte **Alerts** (Warnungen). Aktivieren Sie den Schwellenwert und die Warnungen. Geben Sie den Datenschwellenwert in Gigabyte (GB) für den Zeitraum von 14 Tagen an. Legen Sie außerdem für den Schwellenwert eine Prozentzahl fest, mit der die Auslösung unterschiedlicher Warnstufen gesteuert wird.

4. Klicken Sie auf **OK**, wenn Sie fertig sind.



## <a name="monitor-logs"></a>Überwachungsprotokolle

Cloud Management Gateway generiert Einträge in mehreren Protokolldateien. Weitere Informationen finden Sie unter [Protokolldateien in System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).
