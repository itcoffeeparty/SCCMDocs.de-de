---
title: Anforderungen an den Domänennamen
titleSuffix: Configuration Manager
description: Anforderungen an den Domänennamen unter Verwendung von System Center Configuration Manager.
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 522c2e82-20eb-4f38-859b-d55640b24e32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f82f8e782446035ffdf3910cb591e07f61fbfb47
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="confirm-domain-name-requirements-with-system-center-configuration-manager-and-microsoft-intune"></a>Anforderungen an den Domänennamen mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Führen Sie gegebenenfalls folgende Schritte durch, um Abhängigkeiten außerhalb von Configuration Manager zu erfüllen:

1. Jedem Benutzer muss eine Intune-Lizenz zugewiesen werden, um Geräte zu registrieren. Um Intune-Lizenzen mit Benutzern zu verknüpfen, benötigt jeder Benutzer einen Benutzerprinzipalnamen (user principal name, UPN), der öffentlich aufgelöst werden kann (z.B. johndoe@contoso.com) oder eine alternative Anmelde-ID, die in Azure Active Directory konfiguriert wurde. Das Konfigurieren einer alternativen ID ermöglicht Benutzern z.B. die Anmeldung mit einer E-Mail-Adresse, auch wenn ihr UPN in einem NetBIOS-Format (z.B. CONTOSO\johndoe) vorliegt.

  - Wenn Ihr Unternehmen öffentlich auflösbare UPNs verwendet (d.h. johndoe@contoso.com), ist keine weitere Konfiguration erforderlich.
  - Wenn Ihr Unternehmen einen nicht auflösbaren UPN verwendet (d.h. CONTOSO\johndoe), müssen Sie [eine alternative ID in Azure Active Directory konfigurieren](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2.  Stellen Sie Active Directory-Verbunddienste (AD FS) bereit, und konfigurieren Sie diese. (Optional)

     Wenn Sie das einmalige Anmelden einrichten, können sich die Benutzer mit ihren normalen Unternehmensanmeldeinformationen anmelden, um auf die Dienste in Intune zuzugreifen.

     Weitere Informationen finden Sie unter den folgenden Themen:
    -   [Vorbereiten des einmaligen Anmeldens](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [Planen und Bereitstellen von AD FS 2.0 für die Verwendung mit dem einmaligen Anmelden](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  Stellen Sie die Verzeichnissynchronisierung bereit, und konfigurieren Sie sie.

     Mithilfe der Verzeichnissynchronisierung können Sie Intune mit synchronisierten Benutzerkonten auffüllen. Die synchronisierten Benutzerkonten und Sicherheitsgruppen werden Intune hinzugefügt. Ein Fehler beim Aktivieren der Verzeichnissynchronisierung ist eine häufige Ursache dafür, dass Geräte beim Einrichten von Configuration Manager-MDM mit Microsoft Intune nicht registriert werden können.

     Weitere Informationen finden Sie unter [Verzeichnisintegration](http://go.microsoft.com/fwlink/?LinkID=271120) in der Active Directory-Dokumentationsbibliothek.

4.  Optional, jedoch nicht empfohlen: Setzen Sie die Microsoft Online-Kennwörter von Benutzern zurück, wenn AD FS nicht verwendet wird.

     Wenn Sie AD FS nicht verwenden, müssen Sie für jeden Benutzer ein Microsoft Online-Kennwort festlegen.

> [!div class="button"]
[< Vorheriger Schritt](create-mdm-collection.md) [Nächster Schritt >](configure-intune-subscription.md)
