---
title: "Konten für den Zugriff auf Inhalt | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über die Konten, mit denen Clients auf System Center Configuration Manager-Inhalt zugreifen."
ms.custom: na
ms.date: 1/4/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7df9d0f-fbde-47eb-97e7-3d29536424fa
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 4d34a272a93100426cccd2308c5b3b0b0ae94a60
ms.openlocfilehash: ee83aa6fdbd1a82384a4684055ed72620a3f474e

---
# <a name="manage-accounts-to-access-content-in-system-center-configuration-manager"></a>Verwalten von Konten für den Zugriff auf Inhalt in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Nehmen Sie sich vor der Bereitstellung von Inhalt in System Center Configuration Manager Zeit zu überlegen, wie Clients auf Inhalt von Verteilungspunkten zugreifen.  

-   **Netzwerkzugriffskonto** – Wird von Clients verwendet, um die Verbindung zu einem Verteilungspunkt herzustellen und auf Inhalte zuzugreifen. Standardmäßig verwenden Clients zuerst das Computerkonto.  

     Dieses Konto wird auch von Pullverteilungspunkten verwendet, um Inhalte von einem Quellverteilungspunkt in einer Remotegesamtstruktur abzurufen.  

-   **Paketzugriffskonto**: Standardmäßig gewährt Configuration Manager den integrierten Konten **Benutzer** und **Administratoren** Zugriff auf Inhalt auf einem Verteilungspunkt. Sie können weitere Berechtigungen konfigurieren, um den Zugriff zu beschränken.  

-   **Multicastverbindungskonto** – Wird für Betriebssystembereitstellungen verwendet.  

##  <a name="a-namebkmknaaa-network-access-account"></a><a name="bkmk_NAA"></a> Netzwerkzugriffskonto  
 Das Netzwerkzugriffskonto wird von Clientcomputern verwendet, wenn über ihr lokales Computerkonto kein Zugriff auf Inhalte auf Verteilungspunkten möglich ist. Beispielsweise gilt dies für Arbeitsgruppenclients und Computer aus nicht vertrauenswürdigen Domänen. Dieses Konto wird möglicherweise auch bei der Betriebssystembereitstellung verwendet, falls der Computer, von dem das Betriebssystem installiert wird, noch kein Computerkonto in der Domäne hat.  

-   Von Clients wird für den Zugriff auf Ressourcen im Netzwerk nur das Netzwerkzugriffskonto verwendet.  

-   Sie können an jedem primären Standort mehrere Konten als Netzwerkzugriffskonten konfigurieren.  

-   Clients versuchen zunächst, unter Verwendung ihres „ *Computername*$“-Kontos auf Inhalte auf einem Verteilungspunkt zuzugreifen. Wenn der Zugriff mit diesem Konto nicht möglich ist, wird versucht, ein Netzwerkzugriffskonto zu verwenden. Schlägt der Zugriff fehl, erfolgen die weiteren Zugriffsversuche anschließend mit dem Netzwerkzugriffskonto.  

**Berechtigungen**: Weisen Sie diesem Konto die minimal erforderlichen Berechtigungen für den Inhalt zu, der vom Client für den Zugriff auf die Software benötigt wird.  

-   Das Konto muss über die Berechtigung **Auf diesen Computer vom Netzwerk aus zugreifen** für den Verteilungspunkt verfügen.  

-   Erstellen Sie das Konto in einer Domäne, die den erforderlichen Zugriff auf Ressourcen ermöglicht. Das Netzwerkzugriffskonto muss immer einen Domänennamen enthalten. Pass-Through-Sicherheit wird für dieses Konto nicht unterstützt. Wenn es Verteilungspunkte in mehreren Domänen gibt, erstellen Sie das Konto in einer vertrauenswürdigen Domäne.  

> [!TIP]  
>  Zur Vermeidung von Kontosperrungen sollten Sie das Kennwort für ein vorhandenes Netzwerkzugriffskonto nicht ändern. Erstellen Sie stattdessen ein neues Konto, und konfigurieren Sie das neue Konto in Configuration Manager. Wenn genügend Zeit verstrichen ist, sodass alle Clients die neuen Kontodetails empfangen haben, entfernen Sie das alte Konto aus den freigegebenen Netzwerkordnern, und löschen Sie es.  

> [!IMPORTANT]  
>  Erteilen Sie diesem Konto keine Rechte zur interaktiven Anmeldung.  
>   
>  Gewähren Sie diesem Konto nicht das Recht, der Domäne Computer hinzuzufügen. Wenn während einer Tasksequenz Computer der Domäne beitreten müssen, verwenden Sie dafür das Tasksequenz-Editor-Domänenbeitrittskonto.  

### <a name="to-configure-the-network-access-account"></a>So konfigurieren Sie das Netzwerkzugriffskonto  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Administration** >   **Standortkonfiguration** >  **Standorte**, und wählen Sie anschließend den Standort aus.  

2.  Klicken Sie in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren** > **Softwareverteilung**.  

3.  Klicken Sie auf die Registerkarte **Netzwerkzugriffskonto** . Konfigurieren Sie ein oder mehrere Konten, und klicken Sie dann auf **OK**.  

##  <a name="a-namebkmkpaaa-package-access-accounts"></a><a name="bkmk_Paa"></a> Paketzugriffskonten  
 Mit Paketzugriffskonten können Sie durch Festlegen von NTFS-Dateisystemberechtigungen angeben, welche Benutzer und Benutzergruppen auf Paketinhalt an Verteilungspunkten zugreifen können. Standardmäßig wird von Configuration Manager nur den allgemeinen Zugriffskonten **Benutzer** und **Administratoren** Zugriff gewährt. Sie können den Zugriff für Clientcomputer jedoch durch den Einsatz zusätzlicher Windows-Konten oder -Gruppen steuern. Paketinhalte werden von mobilen Geräten immer anonym abgerufen. Die Paketzugriffskonten werden daher nicht von mobilen Geräten verwendet.  

 Wenn die Inhaltsdateien in einem Paket von Configuration Manager auf einen Verteilungspunkt kopiert werden, werden standardmäßig die folgenden Berechtigungen erteilt: **Lesen** für die lokale Gruppe **Benutzer** und **Vollzugriff** für die lokale Gruppe **Administratoren**. Die tatsächlich erforderlichen Berechtigungen sind vom jeweiligen Paket abhängig. Von Clients in Arbeitsgruppen oder nicht vertrauenswürdigen Gesamtstrukturen wird das Netzwerkzugriffskonto zum Zugriff auf den Paketinhalt verwendet. Stellen Sie anhand der definierten Paketzugriffskonten sicher, dass das Netzwerkzugriffskonto über Berechtigungen für das Paket verfügt.  

 Verwenden Sie Konten in einer Domäne mit Zugriff auf die Verteilungspunkte. Wenn Sie das Konto nach der Paketerstellung erstellen oder ändern, müssen Sie das Paket erneut verteilen. Wenn ein Paketupdate ausgeführt wird, werden die NTFS-Dateisystemberechtigungen für das Paket nicht geändert.  

 Das Netzwerkzugriffskonto braucht nicht als Paketzugriffskonto hinzugefügt werden, da es Mitglied der Gruppe **Benutzer** ist und somit standardmäßig hinzugefügt wird. Der Zugriff von Clients auf das Paket kann nicht dadurch verhindert werden, dass das Paketzugriffskonto auf das Netzwerkzugriffskonto beschränkt wird.  

### <a name="to-manage-access-accounts"></a>So verwalten Sie Zugriffskonten  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Wählen Sie im Arbeitsbereich **Softwarebibliothek** je nach Inhaltstyp, für den Sie Zugriffskonten verwalten möchten, einen der folgenden Schritte aus:  

    -   **Anwendungen**: Erweitern Sie **Anwendungsverwaltung**, klicken Sie auf **Anwendungen**, und wählen Sie dann die Anwendungen aus, für die Sie Zugriffskonten verwalten möchten.  

    -   **Pakete**: Erweitern Sie **Anwendungsverwaltung**, klicken Sie auf **Pakete**, und wählen Sie dann die Pakete aus, für die Sie Zugriffskonten verwalten möchten.  

    -   **Bereitstellungspakete**: Erweitern Sie **Anwendungsverwaltung**, klicken Sie auf **Bereitstellungspakete**, und wählen Sie dann die Bereitstellungspakete aus, für die Sie Zugriffskonten verwalten möchten.  

    -   **Treiberpakete**: Erweitern Sie **Anwendungsverwaltung**, klicken Sie auf **Treiberpakete**, und wählen Sie dann die Treiberpakete aus, für die Sie Zugriffskonten verwalten möchten.  

    -   **Betriebssystemabbilder**: Erweitern Sie **Betriebssysteme**, klicken Sie auf **Betriebssystemabbilder**, und wählen Sie dann die Betriebssystemabbilder aus, für die Sie Zugriffskonten verwalten möchten.  

    -   **Betriebssysteminstallationspakete**: Erweitern Sie **Betriebssysteme**, klicken Sie auf **Betriebssysteminstallationspakete**, und wählen Sie dann die Betriebssysteminstallationspakete aus, für die Sie Zugriffskonten verwalten möchten.  

    -   **Startabbilder**: Erweitern Sie **Betriebssysteme**, klicken Sie auf **Startabbilder**, und wählen Sie dann die Startabbilder aus, für die Sie Zugriffskonten verwalten möchten.  

3.  Klicken Sie mit der rechten Maustaste auf das ausgewählte Objekt, und klicken Sie dann auf **Zugriffskonten verwalten**.  

4.  Geben Sie im Dialogfeld **Konto hinzufügen** den Kontotyp an, dem Zugriff auf den Inhalt gewährt werden soll, und geben Sie dann die Zugriffsrechte an, die dem Konto zugeordnet sind.  

    > [!NOTE]  
    >  Wenn Sie einen Benutzernamen für das Konto hinzufügen und von Configuration Manager ein lokales Benutzerkonto und ein Domänenbenutzerkonto mit diesem Namen gefunden wird, werden von Configuration Manager Zugriffsrechte für das Domänenbenutzerkonto festgelegt.  

##  <a name="a-namebkmkmultia-multicast-connection-account"></a><a name="bkmk_multi"></a> Multicastverbindungskonto  
 Über das Multicastverbindungskonto können von den Verteilungspunkten, die für Multicast konfiguriert sind, Informationen aus der Standortdatenbank gelesen werden.  

-   Sie geben ein Konto an, das verwendet werden soll, wenn Sie Configuration Manager-Datenbankverbindungen für Multicast konfigurieren.  

-   Zwar wird standardmäßig das Computerkonto des Verteilungspunkts verwendet, aber Sie können stattdessen auch ein Benutzerkonto konfigurieren.  

-   Sie müssen stets ein Benutzerkonto angeben, wenn die Standortdatenbank sich in einer nicht vertrauenswürdigen Gesamtstruktur befindet.  

-   Die Konten benötigen die Berechtigung **Lesen** für die Standortdatenbank  

Wenn Ihr Rechenzentrum beispielsweise über ein Umkreisnetzwerk in einer anderen Gesamtstruktur als der des Standortservers und der Standortdatenbank verfügt, können Sie mit diesem Konto die Multicast-Informationen aus der Standortdatenbank lesen.  
Erstellen Sie dieses Konto ggf. als lokales Konto mit geringen Rechten auf dem Computer, auf dem Microsoft SQL Server ausgeführt wird.  

> [!IMPORTANT]  
>  Erteilen Sie diesem Konto keine Rechte zur interaktiven Anmeldung.  



<!--HONumber=Jan17_HO1-->


