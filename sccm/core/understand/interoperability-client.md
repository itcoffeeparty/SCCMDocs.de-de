---
title: "Verwenden des Configuration Manager-Clients für erweiterte Interoperabilität mit Current Branch | Microsoft-Dokumentation"
description: Hier erfahren Sie, wie Sie den Client aus Long-Term Servicing Branch von Configuration Manager mit einem Current Branch-Standort verwenden.
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 9772224be78eee2777137225a59b53b1fd77a627
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2017
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Verwenden der Configuration Manager-Clientsoftware für erweiterte Interoperabilität mit den zukünftigen Versionen eines Current Branch-Standorts

*Gilt für: System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch)*  

In einigen Fällen erlauben Ihre Unternehmensrichtlinien Ihnen möglicherweise nicht, den Configuration Manager-Client auf einigen PCs regelmäßig zu aktualisieren. Beispielsweise müssen Sie möglicherweise Change-Management-Richtlinien einhalten, oder das Gerät ist unternehmenskritisch.

Während Sie weiterhin nach Möglichkeit automatische Clientupgrades für die meisten Ihrer Clients verwenden sollten, können Sie diesen Anforderungen ab Configuration Manager-Update 1610 durch Installation eines neuen Clients für die langfristige Verwendung entgegenkommen, dem Client für erweiterte Interoperabilität (Extended Interoperability Client, EIC).

Der EIC ist mit Configuration Manager-Standorten mit Version 1610 oder höher kompatibel. Der EIC sollte nur für bestimmte PCs verwendet werden, die nicht häufig aktualisiert werden können, wie Kiosk- oder POS-Geräte. Verwenden Sie für alle anderen PCs den neuesten Configuration Manager-Client.

## <a name="how-this-scenario-works"></a>Funktionsweise dieses Szenarios

Beim Installieren eines neuen konsoleninternen Updates für Current Branch aktualisieren die Clients ihre Clientsoftware typischerweise automatisch, um die neuen Funktionen verwenden zu können.

In diesem Szenario verwenden Sie die Current Branch und erhalten die neuen Features und Updates. Die meisten Clients führen die Clientsoftware von Current Branch aus und können diese Clientsoftware mit jedem von Ihnen installierten Versionsupdate aktualisieren. Wenn Sie jedoch für bestimmte kritische Systeme keine Clientsoftwareupdates erhalten möchten, können Sie den erweiterten Interoperabilitätsclient installieren. Diese Clients werden erst dann neue Clientsoftware installieren, wenn Sie ihnen ausdrücklich eine neue Clientsoftwareversion bereitstellen.

>[!IMPORTANT]
>Am Current Branch-Standort muss Version 1610 oder eine höhere Version ausgeführt werden.

## <a name="how-to-use-the-eic"></a>Verwenden des EIC

1. Rufen Sie den EIC (Clientversion 5.00.8412) aus dem \SMSSETUP\Client-Ordner des Installationsmediums des Configuration Manager 1606-Updates ab. Stellen Sie sicher, dass Sie den gesamten Inhalt des Ordners kopieren.
2. Installieren Sie den EIC manuell auf diesen Geräten. [Lesen Sie weitere Informationen zur manuellen Installation des Clients](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).
3. Schließen Sie diese Sammlung von Clientupgrades aus.

>[!TIP]
>Wenn Sie System Center Configuration Manager Version 1606 im Volume Licensing Service Center (VLSC) suchen möchten, wechseln Sie zur Registerkarte **Downloads and Keys** (Downloads und Schlüssel) des [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), suchen Sie nach „system center config“, und wählen Sie dann **System Center Config Mgr (current branch and LTSB)** aus.

## <a name="the-extended-interoperability-client-software"></a>Die Software des erweiterten Interoperabilitätsclients

Der aktuelle EIC wird weiterhin bis mindestens 18. November 2018 mit aktualisierten Versionen von Configuration Manager (Current Branch) unterstützt. Überprüfen Sie nach diesem Datum, ob diese Seite nähere Informationen zu einem neuen EIC oder einer Erweiterung der Unterstützung für den vorhandenen EIC enthält.

>[!TIP]
>Der EIC wird für mindestens zwei Jahre ab dem Datum des Release unterstützt (siehe [Support for System Center Configuration Manager current branch versions](/sccm/core/servers/manage/current-branch-versions-supported) (Unterstützung für Current Branch-Versionen von System Center Configuration Manager). Die Unterstützung für den aktuellen EIC wird z.B. nach dem Release von 1610 für zwei Jahre gewährt, d.h. bis zum 18. November 2018.

Denken Sie daran, den erweiterten Interoperabilitätsclient auf den mit Current Branch verwalteten Geräten zu aktualisieren, bevor der Client nicht mehr unterstützt wird. Hierfür laden Sie eine neue Clientversion von Microsoft herunter und stellen die aktualisierte Clientsoftware auf Ihren Geräten bereit, die den aktuellen erweiterten Interoperabilitätsclient verwenden.

## <a name="limitations-of-the-extended-interoperability-client"></a>Einschränkungen des Clients für erweiterte Interoperabilität

- Updates für die Software des erweiterten Interoperabilitätsclients sind nicht per konsoleninternes Update verfügbar. Weitere Informationen über die Bereitstellung einer aktualisierten Clientsoftware werden bei Veröffentlichung eines Clientupdates zur Verfügung gestellt.
- Der EIC unterstützt nur Softwareupdates, Inventur sowie Pakete und Programme.

## <a name="next-steps"></a>Nächste Schritte

Verwenden Sie die Informationen in [How to monitor clients](/sccm/core/clients/manage/monitor-clients) (Überwachen von Clients), um sicherzustellen, dass die Clients ordnungsgemäß auf den gewünschten Geräten installiert werden.
