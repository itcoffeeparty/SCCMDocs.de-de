---
title: Erstellen von Android-Anwendungen | Microsoft Docs
description: "Was Sie beim Erstellen und Bereitstellen von Apps für Android-Geräte berücksichtigen müssen."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 3d90b2cb1e255b9e8827a991779024ccecde9646
ms.lasthandoff: 03/06/2017

---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>Erstellen von Android-Apps mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In einer System Center Configuration Manager-Anwendung ist mindestens ein Bereitstellungstyp enthalten, der die Installationsdateien und Informationen enthält, die zur Bereitstellung der Software für ein Gerät erforderlich sind. Bereitstellungstypen verfügen auch über Regeln, aus denen hervorgeht, wann und wie die Software bereitgestellt wird.  

 Es gibt die folgenden Möglichkeiten zum Erstellen von Anwendungen:  

-   Erstellen Sie die Anwendungen und Bereitstellungstypen durch Lesen der Installationsdateien der Anwendung automatisch.  

-   Erstellen Sie die Anwendung manuell, und fügen Sie Bereitstellungstypen später hinzu.  

-   Importieren Sie eine Anwendung aus einer Datei.  

Unter [Starten des Assistenten zum Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) finden Sie weitere Informationen zu erforderlichen Schritten zum Erstellen von Configuration Manager-Anwendungen und Bereitstellungstypen. Berücksichtigen Sie beim Erstellen und Bereitstellen von Apps für Android-Geräte auch Folgendes.  

## <a name="general-considerations"></a>Allgemeine Aspekte

Configuration Manager unterstützt die Bereitstellung folgender App-Typen für Android:

|Gerätetyp|Unterstützte Dateien|
|-|-|
|Android|.apk|

Die folgenden Bereitstellungsaktionen werden unterstützt:

|Gerätetyp|Unterstützte Aktionen|
|-|-|
|Android|**Verfügbar**, **Erforderlich** Der Benutzer muss der Installation und Deinstallation zustimmen.

