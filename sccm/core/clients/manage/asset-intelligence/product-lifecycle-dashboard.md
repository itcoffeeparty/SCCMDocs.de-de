---
title: "Dashboard für den Produktlebenszyklus"
titleSuffix: Configuration Manager
description: "Informieren Sie sich über das Dashboard für den Produktlebenszyklus in System Center Configuration Manager."
ms.custom: na
ms.date: 02/13/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: cfc54c1beb92d0102897f77ce3c287cc0ef9e0f4
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2018
---
# <a name="use-the-product-lifecycle-dashboard-to-manage-microsoft-lifecycle-policy-in-system-center-configuration-manager"></a>Verwenden des Dashboards für den Produktlebenszyklus zum Verwalten der Microsoft Lifecycle-Richtlinie in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*

Ab der [Technical Preview-Version 1802](/sccm/core/get-started/capabilities-in-technical-preview-1802) können Sie das Configuration Manager-Dashboard für den Produktlebenszyklus verwenden. Das Dashboard zeigt den Status der Microsoft Lifecycle-Richtlinie für Microsoft-Produkte an, die auf mit Configuration Manager verwalteten Geräten installiert sind. Das Dashboard bietet Ihnen Informationen zu Microsoft-Produkten in Ihrer Umgebung, deren Supportfähigkeit und den Daten des Supportendes. Auf diesem Dashboard erfahren Sie, welche Art von Support für die jeweiligen Produkte verfügbar ist. Dieses Feature hilft Ihnen dabei, zu planen, wann Sie die von Ihnen verwendeten Microsoft-Produkte aktualisieren müssen, bevor das Ende des Supports erreicht ist.  

Weitere Informationen zur Microsoft Lifecycle-Richtlinie für Produkte finden Sie unter [Microsoft Lifecycle-Richtlinie](https://support.microsoft.com/en-us/lifecycle).

## <a name="prerequisites"></a>Erforderliche Komponenten 

 Damit Sie Daten auf dem Dashboard für den Produktlebenszyklus anzeigen können, müssen folgende Voraussetzungen erfüllt sein: 
- Auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, muss Internet Explorer 9 oder höher installiert sein. 
- Für die Hyperlinkfunktion auf dem Dashboard ist ein Reporting Services-Punkt erforderlich, da die Hyperlinks mit SSRS-Berichten (SQL Server Reporting Services) verknüpft sind. Weitere Informationen finden Sie unter [Berichterstellung in System Center Configuration Manager](/sccm/core/servers/manage/reporting). 
- Der Asset Intelligence-Synchronisierungspunkt muss konfiguriert und synchronisiert sein. Weitere Informationen finden Sie unter [Konfigurieren von Asset Intelligence in System Center Configuration Manager](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).

Welche Daten auf dem Dashboard angezeigt werden, richtet sich danach, ob der Asset Intelligence-Synchronisierungspunkt installiert ist. Das Dashboard verwendet den Asset Intelligence-Katalog als Metadaten für Produkttitel. Die Metadaten werden mit Inventurdaten in Ihrer Hierarchie verglichen. 

>[!NOTE]
>Wenn Sie den Asset Intelligence-Dienstpunkt zum ersten Mal konfigurieren, stellen Sie sicher, dass Sie die [Asset Intelligence-Hardwareinventurklassen aktivieren](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence#BKMK_EnableAssetIntelligence). Das Dashboard für den Lebenszyklus benötigt diese Asset Intelligence-Hardwareinventurklassen und zeigt erst dann Daten an, wenn Clients nach Hardwareinventurdaten gesucht und diese zurückgegeben haben.  

## <a name="use-the-microsoft-product-lifecycle-dashboard"></a>Verwenden des Microsoft-Dashboard für den Produktlebenszyklus

Das Dashboard zeigt basierend auf den Inventurdaten, die von verwalteten Geräten erfasst werden, Informationen zu allen aktuellen Produkten an. Die für Betriebssysteme und SQL Server angezeigten Informationen beschränken sich jedoch auf folgende Versionen:

- Windows Server 2008 und höher
- Windows XP und höher
- SQL Server 2008 und höher

Um auf das Dashboard für den Lebenszyklus zuzugreifen, wechseln Sie in der Configuration Manager-Konsole zu **Assets und Konformität** > **Asset Intelligence** > **Produktlebenszyklus**.

>[!NOTE]
>Die Daten auf dem Dashboard basieren auf dem Standort, mit dem die Configuration Manager-Konsole verbunden ist. Wenn die Konsole eine Verbindung zu Ihrem Standort der obersten Ebene herstellt, sehen Sie die Daten für die gesamte Hierarchie. Bei einer Verbindung mit einem untergeordneten primären Standort werden nur die Daten aus diesem Standort angezeigt.

### <a name="product-lifecycle-dashboard"></a>Dashboard für den Produktlebenszyklus

![Dashboard für den Produktlebenszyklus](/sccm/core/clients/manage/asset-intelligence/media/product-lifecycle-dashboard.png)

Das Dashboard verfügt über die folgenden Kacheln: 
- **Top 5-Produkte, die das Ende des Lebenszyklus erreicht haben**: Diese Kachel zeigt eine konsolidierte Datenansicht der Produkte in Ihrer Umgebung, deren Lebenszyklus abgelaufen ist. Das Diagramm zeigt installierte Software, deren Lebenszyklus abgelaufen ist, basierend auf dem Supportlebenszyklus für Betriebssysteme und SQL Server-Produkte.  
- **Top 5-Produkte, deren Lebenszyklus in den nächsten sechs Monaten endet**: Diese Kachel zeigt eine konsolidierte Datenansicht der Produkte in Ihrer Umgebung, deren Lebenszyklus innerhalb der nächsten sechs Monate abläuft. Das Diagramm zeigt installierte Software, deren Lebenszyklus innerhalb von sechs Monaten ablaufen wird, basierend auf dem Supportlebenszyklus für Betriebssysteme und SQL Server-Produkte.
- **Lebenszyklusdaten für die installierten Produkte**: Diese Kachel bietet einen allgemeinen Überblick darüber, wann ein Produkt keinen Supportstatus mehr haben wird. Das Diagramm zeigt eine Aufschlüsselung der Anzahl von Clients, auf denen das Produkt installiert ist, den Status der Supportverfügbarkeit sowie einen Link zu weiteren Informationen zu den nächsten Schritten. Das Diagramm enthält die folgenden Informationen:     
    - Verbleibende Supportdauer
    - Anzahl in der Umgebung 
    - Enddatum des grundlegenden Supports
    - Enddatum des erweiterten Supports
    - Nächste Schritte 

>[!IMPORTANT]
>Die Daten auf diesem Dashboard dienen nur zu Ihrer Information und zur internen Verwendung innerhalb Ihres Unternehmens. Sie sollten sich im Hinblick auf die Konformität nicht ausschließlich auf diese Informationen verlassen. Überprüfen Sie die Genauigkeit der bereitgestellten Informationen sowie die Verfügbarkeit von Supportinformationen auf dieser Website: https://support.microsoft.com/de-de/lifecycle.

## <a name="reporting"></a>Berichterstellung
Unter der Kategorie **Produktlebenszyklus** wurden die folgenden neuen Berichte hinzugefügt:
- **Allgemeine Übersicht über den Produktlebenszyklus**: Zeigt eine Liste der Produktlebenszyklen an. Die Liste kann nach Produktname und vom Benutzer angegebener Anzahl von Tagen bis zum Ablauf gefiltert werden. 
- **Computer mit einem bestimmten Softwareprodukt**: Zeigt eine Liste mit Computern an, auf denen ein bestimmtes Produkt erkannt wurde.
- **In der Organisation vorgefundene Liste abgelaufener Produkte**: Zeigt Details zu Produkten in Ihrer Umgebung, deren Lebenszyklus abgelaufen ist. 
- **Liste von Computern mit abgelaufenen Produkten in der Organisation**: Zeigt Computer an, auf denen abgelaufene Produkte installiert sind. Sie können diesen Bericht nach dem Produktnamen filtern.

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Installation oder dem Update der Technical Preview finden Sie unter [Technical Preview für System Center Configuration Manager](/sccm/core/get-started/technical-preview).  

