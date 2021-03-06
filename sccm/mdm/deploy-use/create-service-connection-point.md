---
title: Erstellen eines Dienstverbindungspunkts
titleSuffix: Configuration Manager
description: Erstellen eines Dienstverbindungspunkts unter Verwendung von System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 617abb22-d22f-41fb-a76b-1c4259e419d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3dfd02a84cef31c22023b7fc4cb75931dc82160f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-service-connection-point-with-system-center-configuration-manager-and-microsoft-intune"></a>Erstellen eines Dienstverbindungspunkts mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Nachdem Sie Ihr Abonnement erstellt haben, können Sie die Standortsystemrolle „Dienstverbindungspunkt“ installieren, die es Ihnen ermöglicht, eine Verbindung mit dem Intune-Dienst herzustellen. Von dieser Standortsystemrolle werden Einstellungen und Anwendungen mittels Push an den Intune-Dienst übertragen.

 Vom Dienstverbindungspunkt werden Einstellungen und Softwarebereitstellungsinformationen an Configuration Manager gesendet sowie Status- und Inventurmeldungen von mobilen Geräten abgerufen. Der Configuration Manager-Dienst fungiert als Gateway, das mit mobilen Geräten kommuniziert und Einstellungen speichert.

> [!NOTE]
>  Die Standortsystemrolle „Dienstverbindungspunkt“ kann nur an einem Standort der zentralen Verwaltung oder an einem eigenständigen primären Standort installiert werden. Der Dienstverbindungspunkt muss über Internetzugriff verfügen.


## <a name="configure-the-service-connection-point-role"></a>Konfigurieren der Rolle „Dienstverbindungspunkt“

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Server und Standortsystemrollen**.

3.  Fügen Sie einem neuen oder vorhandenen Standortsystemserver die Rolle **Dienstverbindungspunkt** wie folgt hinzu:

    -   Neuer Standortsystemserver: Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Standortsystemserver erstellen** , um den Assistenten zum Erstellen von Standortsystemservern zu starten.

    -   Bestehender Standortsystemserver: Klicken Sie auf den Server, auf dem die Rolle „Dienstverbindungspunkt“ installiert werden soll. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Server** auf **Standortsystemrollen hinzufügen** , um den Assistenten zum Hinzufügen von Standortsystemrollen zu starten.

4.  Wählen Sie auf der Seite **Systemrollenauswahl** die Option **Dienstverbindungspunkt**, und klicken Sie auf **Weiter**.
![Erstellen eines Dienstverbindungspunkts](../media/mdm-service-connection-point.png)

* Schließen Sie den Assistenten ab.

## <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>Wie authentifiziert sich der Dienstverbindungspunkt beim Microsoft Intune-Dienst?
 Der Systemverbindungspunkt erweitert den Configuration Manager, indem er eine Verbindung mit dem cloudbasierten Intune-Dienst herstellt, der mobile Geräte über das Internet verwaltet. Die Authentifizierung des Dienstverbindungspunkts beim Intune-Dienst geschieht auf folgende Weise:

1.  Beim Erstellen eines Intune-Abonnements in der Configuration Manager-Konsole wird der Configuration Manager-Administrator durch Herstellen einer Verbindung mit Azure Active Directory authentifiziert. Dadurch erfolgt eine Umleitung zum jeweiligen AD FS-Server, der zur Eingabe des Benutzernamens und Kennworts auffordert. Anschließend stellt Intune ein Zertifikat für den Mandanten aus.

2.  Das Zertifikat aus Schritt 1 wird in der Standortrolle „Dienstverbindungspunkt“ installiert und zum Authentifizieren und Autorisieren der gesamten weiteren Kommunikation mit dem Microsoft Intune-Dienst verwendet.

> [!div class="button"]
[< Vorheriger Schritt](terms-and-conditions.md) [Nächster Schritt >](enable-platform-enrollment.md)
