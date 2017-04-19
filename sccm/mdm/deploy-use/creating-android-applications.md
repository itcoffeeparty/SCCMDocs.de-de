---
title: Erstellen von Android-Anwendungen | Microsoft Docs
description: "Was Sie beim Erstellen und Bereitstellen von Apps für Android-Geräte berücksichtigen müssen."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 27a92dc1c3710ff55f0b145386319dda371533d9
ms.openlocfilehash: d3b20a59a9147e09e58f04f83f97fd72ebfef5a1
ms.lasthandoff: 04/07/2017

---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>Erstellen von Android-Apps mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In einer System Center Configuration Manager-Anwendung ist mindestens ein Bereitstellungstyp enthalten, der die Installationsdateien und Informationen enthält, die zur Bereitstellung der Software für ein Gerät erforderlich sind. Bereitstellungstypen verfügen auch über Regeln, aus denen hervorgeht, wann und wie die Software bereitgestellt wird.  

 Es gibt die folgenden Möglichkeiten zum Erstellen von Anwendungen:  

-   Erstellen Sie die Anwendungen und Bereitstellungstypen durch Lesen der Installationsdateien der Anwendung automatisch.  
-   Erstellen Sie die Anwendung manuell, und fügen Sie Bereitstellungstypen später hinzu.  
-   Importieren Sie eine Anwendung aus einer Datei.  

Unter [Starten des Assistenten zum Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) finden Sie weitere Informationen zu erforderlichen Schritten zum Erstellen von Configuration Manager-Anwendungen und Bereitstellungstypen. Berücksichtigen Sie beim Erstellen und Bereitstellen von Apps für Android-Geräte auch Folgendes.  

## <a name="general-considerations-for-android-apps"></a>Allgemeine Aspekte für Android-Apps

Configuration Manager unterstützt die Bereitstellung folgender App-Typen für Android:

|Gerätetyp|Unterstützte Dateien|
|-|-|
|Android|.apk|

Die folgenden Bereitstellungsaktionen werden unterstützt:

|Gerätetyp|Unterstützte Aktionen|
|-|-|
|Android|**Verfügbar**, **Erforderlich** Der Benutzer muss der Installation und Deinstallation zustimmen.

## <a name="approve-and-deploy-android-for-work-apps"></a>Genehmigen und Bereitstellen von Android for Work Apps
Als ein Configuration Manager-Administrator können Sie Apps auch auf der [Play for Work-Website](https://play.google.com/work) genehmigen und bereitstellen und diese Apps auf verwalteten Android for Work-Geräten bereitstellen.

Gehen Sie wie folgt vor, um Apps im Play for Work-Store zu genehmigen, diese mit der Configuration Manager-Konsole zu synchronisieren und sie anschließend in verwalteten Android for Work-Geräten bereitzustellen. Um Apps in die Arbeitsprofile von Benutzern bereitzustellen, müssen Sie die Apps zunächst in Play for Work genehmigen und anschließend mit der Configuration Manager-Konsole synchronisieren.

1. Öffnen Sie einen Browser und navigieren Sie zu https://play.google.com/work.
2. Melden Sie sich mit dem Google-Administratorkonto an, das Sie an Ihren Intune-Mandanten gebunden haben.
3. Suchen Sie nach Apps, die Sie in Ihrer Umgebung bereitstellen möchten, und wählen Sie jeweils **Approve** (Genehmigen), um die App für Android for Work zur Verfügung zu stellen.
4. Gehen Sie in der Configuration Manager-Konsole zu **Administrator** > **Übersicht** > **Cloud Services** > **Android for Work**, und klicken Sie dann auf **Synchronisierung**.
5. Es kann bis zu zehn Minuten dauern, bis Apps synchronisiert sind; navigieren Sie anschließend zu **Softwarebibliothek** > **Übersicht** > **Anwendungsverwaltung** > **Lizenzinformationen für Store-Apps**.
6. Wählen Sie eine App, die mit Play for Work synchronisiert wurde, und klicken Sie dann auf **Anwendung erstellen**.
7. Stellen Sie den Assistenten fertig, und wählen Sie anschließend **Schließen**.
8. Navigieren Sie zu **Softwarebibliothek** > **Übersicht** > **Anwendungsverwaltung** > **Anwendungen**, wählen Sie eine Android for Work-App aus, und stellen Sie diese wie gewohnt bereit.

Um Play for Work-Apps mit Configuration Manager zu synchronisieren müssen Sie zunächst mindestens eine App auf der Play for Work-Website genehmigen.

