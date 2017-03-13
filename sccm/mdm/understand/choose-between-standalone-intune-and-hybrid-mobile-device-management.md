---
title: "Auswählen von Intune Standalone oder der hybriden Verwaltung mobiler Geräte (MDM) | Microsoft-Dokumentation"
description: "Wählen Sie aus, ob Sie die hybride Verwaltung mobiler Geräte mit Intune und Configuration Manager bereitstellen oder Intune standalone ausführen."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 84e3896dd05a8c157f4e94625b0eca60aacc11d3
ms.openlocfilehash: 8f2625aadfd0aed92d9922c7e3c0d3d166a78cdd
ms.lasthandoff: 02/25/2017

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Wählen zwischen Microsoft Intune standalone und der hybriden Verwaltung mobiler Geräte mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Eine der am häufigsten gestellten Fragen bezüglich der Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit Microsoft Intune ist folgende: „Sollte ich die hybride Verwaltung mobiler Geräte mit Intune und Configuration Manager bereitstellen oder Intune standalone in der Konfiguration nur für die Cloud ausführen?“ Um diese Frage zu beantworten, sollten Sie die beiden Optionen gut vergleichen, und die Updates erwägen, die Anfang 2017 für Intune standalone verfügbar sein werden.

## <a name="what-is-intune-standalone"></a>Was ist Intune standalone?

Intune standalone ist eine rein cloudbasierte MDM-Lösung, die keine lokalen Ressourcen umfasst und mithilfe einer Webkonsole verwaltet wird, auf die von überall in der Welt aus zugegriffen werden kann. Intune Rechenzentren werden in Nordamerika, Europa und Asien gehostet. Da Intune ein Clouddienst ist, können Sie die Intune-Verwaltung auf Ihren Geräten in einem relativ kleinen Zeitrahmen bereitstellen. Sie können möglicherweise auch Intune standalone auswählen, wenn sich Ihre Organisation in die Cloud verlagert.

## <a name="what-is-hybrid-mdm-with-configuration-manager"></a>Was ist die hybride Verwaltung mobiler Geräte (Hybrid-MDM) mit Configuration Manager?

Die hybride Verwaltung mobiler Geräte ist eine Lösung, die Intune als Übermittlungskanal für Richtlinien, Profile und Anwendungen für Geräte nutzt, jedoch die lokale Infrastruktur von Configuration Manager verwendet, um Inhalt zu speichern und zu verwalten und die Geräte zu verwalten. Sie können die hybride Verwaltung mobiler Geräte auswählen, wenn Sie bereits viel in Configuration Manager investiert haben und dieses Produkt erweitern möchten, um mobile Geräte zu verwalten. Mit einer hybriden Implementierung erhalten Sie zentralisierten Zugriff, d.h., dass Sie dieselbe lokale Infrastruktur und Administratorkonsole zum Verwalten mobiler Geräte sowohl mit Intune als auch mit PCs und Servern mit dem herkömmlichen Configuration Manager-Client verwenden können.

## <a name="whats-coming-to-intune-standalone-in-early-2017"></a>Was gibt es Anfang 2017 Neues für Intune standalone?

Wenn Sie zwischen standalone und hybrid auswählen, sollten Sie über Features nachdenken, die Anfang 2017 für Intune standalone erhältlich sein werden. Heute verfügt die hybride Verwaltung mobiler Geräte über mehrere fortgeschrittene Features, denen zu verdanken ist, dass einige Kunden heute ihre Geräte mit Hybrid-MDM anstatt mit Intune standalone verwalten:

-   Programmgesteuerter Zugriff (API): SDK- und PowerShell-Verwaltungsoptionen

-   Benutzerdefinierte Berichterstellung: Erstellen angepasster Berichte

-   Rollenbasierte Zugriffssteuerung: Einschränken des Zugriffs auf Verwaltungsfunktionen auf Grundlage zugewiesener Rollen

-   Skalieren: Bereitstellen und Verwalten von über 100.000 mobilen Geräten.

-   Zentralisiert: Verwalten sowohl von herkömmlichen PC-Clients als auch von mit Intune verwalteten Geräten mit derselben Konsole

Wenn Sie noch heute Ihre Intune-Bereitstellung planen und einige Monate für Pilottests, Akzeptanztests und für die Bereitstellung erübrigen können, denken Sie vielleicht darüber nach, nun Intune standalone auszuwählen, da Sie wissen, dass die Updates für den Clouddienst über mehr Funktionalität verfügen. In der ersten Hälfte des Kalenderjahres 2017, erhält Intune standalone Updates, die den Großteil der erweiterten Funktionalität einer hybriden Bereitstellung mit Configuration Manager erhalten werden. Intune standalone wird schon bald in die Microsoft Azure-Cloudplattform verschoben und erhält so verbesserte Skalierbarkeit, rollenbasierten Zugriff über das Azure-Portal, benutzerdefinierte Berichterstellung sowie programmgesteuerten Zugriff über die Azure Graph-API.

Sie können von Hybrid-MDM zu Intune standalone wechseln und auch wieder zurück. Sie benötigen für diesen Vorgang jedoch die Hilfe des Microsoft-Supports sowie vom Microsoft Operations Support. Dazu muss die Registrierung aller Geräte aufgehoben und wieder erneuert werden, nachdem die Verwaltungsstelle geändert wurde.  Microsoft arbeitet daran, die Erfahrung zum Umschalten von Konfigurationen in einem zukünftigen Dienstupdate zu verbessern.

