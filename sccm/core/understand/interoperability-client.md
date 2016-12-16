---
title: "Verwenden des Interoperabilitätsclients mit Current Branch | System Center Configuration Manager"
description: Hier erfahren Sie, wie Sie den Client aus Long-Term Servicing Branch von Configuration Manager mit einem Current Branch-Standort verwenden.
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
Robots: NOINDEX,NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: 45ef4be7bf0b1c2e99f25ac398265bb71489c17e
ms.openlocfilehash: a97eb7a637611ba269cf8f16635b8165c19283f1

---
# <a name="use-the-client-software-from-the-version-1606-baseline-media-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Verwenden der Clientsoftware aus Version 1606 der Baselinemedien für erweiterte Interoperabilität mit den zukünftigen Versionen eines Current Branch-Standorts

*Gilt für: System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch)*  

Sie können die Configuration Manager-Clientsoftware für Windows-Computer (client.msi) von Version 1606 der bei System Center 2016 oder einem System Center Configuration Manager-Release (Current Branch und Long-Term Servicing Branch 1606) mitgelieferten Baselinemedien-DVD verwenden, um Geräte zu verwalten, die zu einem Current Branch-Standort gehören. Dieser Client wird als „erweiterter Interoperabilitätsclient“ bezeichnet.

## <a name="how-this-scenario-works"></a>Vorgehensweise bei diesem Szenario:
Beim Installieren eines neuen konsoleninternen Updates für Current Branch aktualisieren die Clients ihre Clientsoftware typischerweise automatisch, um die neuen Funktionen verwenden zu können.

In diesem Szenario verwenden Sie die Current Branch und erhalten die neuen Features und Updates. Die meisten Clients führen die Clientsoftware von Current Branch aus und können diese Clientsoftware mit jedem von Ihnen installierten Versionsupdate aktualisieren. Wenn Sie jedoch für bestimmte kritische Systeme keine Clientsoftwareupdates erhalten möchten, können Sie den erweiterten Interoperabilitätsclient installieren. Diese Clients werden erst dann neue Clientsoftware installieren, wenn Sie ihnen ausdrücklich eine neue Clientsoftwareversion bereitstellen.

Weitere Informationen darüber, wie Sie verhindern können, dass Client Branch-Clients bei der Installation einer neuen Configuration Manager-Version automatische Updates durchführen, werden mit Version 1610 von Current Branch verfügbar sein.

Am Current Branch-Standort muss Version 1606 oder eine höhere Version ausgeführt werden.

## <a name="the-extended-interoperability-client-software"></a>Die Software des erweiterten Interoperabilitätsclients
Wenn Sie den erweiterten Interoperabilitätsclient aus dem System Center 2016- der dem System Center Configuration Manager-Release (Current Branch und Long-Term Servicing Branch 1606) mit einem Current Branch-Standort verwenden, wird der Client bis zwei Jahre nach der allgemeinen Verfügbarkeit des Releases unterstützt, in diesem Fall ab dem 12. Oktober 2016.

Denken Sie daran, den erweiterten Interoperabilitätsclient auf den mit Current Branch verwalteten Geräten zu aktualisieren, bevor der Client nicht mehr unterstützt wird. Hierfür laden Sie eine neue Clientversion von Microsoft herunter, und stellen die aktualisierte Clientsoftware auf Ihren Geräten bereit, die den aktuellen erweiterten Interoperabilitätsclient verwenden.

**Einschränkungen des erweiterten Interoperabilitätsclients:**
-   Updates für die Software des erweiterten Interoperabilitätsclients sind nicht per konsoleninternes Update verfügbar. Weitere Informationen über die Bereitstellung einer aktualisierten Clientsoftware werden bei Veröffentlichung eines Clientupdates zur Verfügung gestellt.

## <a name="identify-the-client-version-you-use"></a>Ermitteln der von Ihnen verwendeten Clientversion
Nachstehend finden Sie die wichtigsten verfügbaren Clientversionen für Current Branch und LTSB:

|Clientversion|Branch und Version |  
|----------------|---------------------|
|5.00.8325.xxxx |   - Current Branch 1511|
|5.00.8355.xxxx |- Current Branch 1602|
|5.00.8412.1307 |- Current Branch 1606 </br> - Current Branch 1606 mit 1606 Hotfixrollup (KB3186654)</br>- erweiterter Interoperabilitätsclient der Baselinemedien der Version 1606|  

Im Client können Sie die Clientversion auf der Registerkarte **Allgemein** im Control Panel Applet des Configuration Manager sehen.

In der Registerkarte **Komponenten** des Applets werden für manche Komponenten verschiedene Werte angezeigt. Beispiel: Für eine Clientversion 8412.1307 können manche Komponenten als 5.00.8412.**1000** oder 5.00.8412.**1006** aufgelistet sein.  Diese bei manchen Komponenten bestehende Abweichung der letzten vier Ziffern ist normal und bedeutet nicht, dass die Komponente nicht korrekt auf die aktuelle Clientversion aktualisiert werden konnte.



<!--HONumber=Nov16_HO1-->


