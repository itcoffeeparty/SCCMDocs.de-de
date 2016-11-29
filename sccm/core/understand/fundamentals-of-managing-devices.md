---
title: "Grundlagen der Verwaltung von Geräten | System Center Configuration Manager"
description: "Erfahren Sie, wie Sie Geräte mit System Center Configuration Manager verwalten."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f4d39f31723711a7f5ec2b1aa39e81d3a3188029


---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>Grundlagen der Verwaltung von Geräten mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager kann zwei große Gerätegruppen verwalten.

Bei der ersten Gruppe, den **Clients**, handelt es sich um Geräte wie Arbeitsstationen, Laptops, Server und mobile Geräte, auf denen die Configuration Manager-Clientsoftware zu Ihrer Verwaltung installiert ist.   

Die zweite Gruppe, **verwaltete Geräte**, kann Clients umfassen, bezeichnet aber in der Regel mobile Geräte, auf denen keine Configuration Manager-Clientsoftware installiert ist, und die Sie mit Microsoft Intune oder mithilfe der integrierten lokalen Verwaltung mobiler Geräte von Configuration Manager verwalten.

Zusätzlich zur Verwaltung von Geräten, mit dem oder ohne den Configuration Manager-Client, können Sie die benutzerorientierte Verwaltung dazu nutzen, die von Ihnen verwalteten Geräte zu gruppieren und zu identifizieren.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Verwalten von Geräten mit dem Configuration Manager-Client

 Die Verwaltung von Clients umfasst Vorgänge wie das Erfassen des Bestands von Hardware und Software von Geräten, das Installieren neuer Software auf einem Gerät oder das Festlegen von Einstellungen, die Kompatibilität mit einer bestimmten Konfiguration melden oder erzwingen. Für einige Verwaltungsfunktionen, wie z. B. Hardwareinventur, muss auf dem Gerät die Configuration Manager-Clientsoftware ausgeführt werden. Andere Vorgänge, z. B. das Installieren (Bereitstellen) von Software auf einem Gerät, werden für alle verwalteten Geräten unterstützt.  

 Sie müssen ein Gerät in Ihrem Netzwerk ermitteln und anschließend die Configuration Manager-Clientsoftware darauf bereitstellen (installieren), um das Gerät mithilfe der Clientsoftware zu verwalten. Sie können die Clientsoftware alternativ manuell auf einem neuen Computer installieren und anschließend veranlassen, dass der Computer Ihrem Standort beitritt, wenn er Ihrem Netzwerk beitritt. Um Geräte zu ermitteln, auf denen die Clientsoftware noch nicht installiert ist, führen Sie eine oder mehrere der integrierten Ermittlungsmethoden durch. Nachdem ein Gerät erkannt wurde, können Sie die Clientsoftware mithilfe einer von mehreren Methoden installieren lassen. Informationen zur Ermittlung finden Sie unter [Ausführen der Ermittlung für System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

 Nach der Ermittlung von Geräten, die die Ausführung der Configuration Manager-Clientsoftware unterstützen, können Sie die Software mithilfe einer von mehreren Methoden installieren. Nachdem die Software installiert und der Client einem primären Standort zugewiesen wurde, können Sie mit dem Verwalten des Geräts beginnen.  Zu den gängigen Installationsmethoden zählen die „Clientpushinstallation“, die auf Softwareupdates basierende Installation mithilfe von Gruppenrichtlinien, die manuelle Installation auf einem Computer oder das Hinzufügen des Clients zu einem Betriebssystemabbild, das Sie bereitstellen.  

 Nachdem der Client installiert wurde, können Sie die Aufgaben bei der Verwaltung von Geräten mithilfe von Sammlungen vereinfachen. Sammlungen sind logische Gruppen von Geräten oder Benutzern, die Sie erstellen, damit Sie Verwaltungstasks auf mehreren Geräten mit den gleichen Kriterien ausführen können. Beispielsweise kann es vorkommen, dass Sie eine mobile Geräteanwendung auf allen mobilen Geräten installieren möchten, die von Configuration Manager angemeldet wurden. In diesem Fall können Sie die Sammlung **Alle mobilen Geräte** verwenden, bei der Computer automatisch ausgeschlossen sind. Sie können eigene Sammlungen erstellen, um die von Ihnen verwalteten Geräte Ihren Geschäftsanforderungen entsprechend logisch zu gruppieren.  

 Weitere Informationen finden Sie unter den folgenden Themen:  

-   [Wählen einer Geräteverwaltungslösung für System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  

-   [Clientinstallationsmethoden in System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [Einführung in Sammlungen in System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Clienteinstellungen  
 Bei der Erstinstallation von Configuration Manager werden alle Clients in der Hierarchie mit den Clientstandardeinstellungen konfiguriert. Diese Einstellungen können Sie ändern. Diese Clienteinstellungen umfassen eine Reihe von Konfigurationsoptionen, z.B. wie häufig die Gerätekommunikation mit dem Standort stattfindet, ob der Client für Softwareupdates und andere Verwaltungsvorgänge aktiviert ist und ob Benutzer ihre mobilen Geräte für die Verwaltung durch Configuration Manager registrieren können.  

 Falls Sie für bestimmte Benutzer- oder Gerätegruppen unterschiedliche Clienteinstellungen benötigen, können Sie benutzerdefinierte Clienteinstellungen erstellen und diese den Sammlungen zuweisen.  Mitglieder der Sammlung sind so konfiguriert, dass sie die benutzerdefinierten Einstellungen haben. Sie können auch mehrere benutzerdefinierte Clienteinstellungen erstellen, die in der angegebenen (numerischen) Reihenfolge angewendet werden.  Bei Konflikten setzt die Einstellung mit der niedrigsten Reihenfolgennummer die anderen Einstellungen außer Kraft.  

 Die folgende Abbildung enthält ein Beispiel für die Erstellung und Anwendung von benutzerdefinierten Clienteinstellungen.  

 ![Clienteinstellungen](media/ClientSettings.gif)  

 Weitere Informationen zu Clienteinstellungen finden Sie unter  
                [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) und [Informationen zu Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>Verwalten von Geräten ohne Configuration Manager-Client  
 Configuration Manager unterstützt die Verwaltung einiger Geräte, auf denen die Clientsoftware nicht installiert ist, und die nicht über die Zusammenarbeit mit Microsoft Intune verwaltet werden. Weitere Informationen finden Sie unter [Verwalten mobiler Geräte mithilfe lokaler Infrastruktur in System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) und [Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-centric-management"></a>Benutzerzentrierte Verwaltung  
 Zusätzlich zu den Sammlungen für Geräte gibt es auch Benutzersammlungen, die Benutzer aus den Active Directory-Domänendiensten enthalten. Wenn Sie eine Benutzersammlung verwenden, können Sie die Software auf allen Computern installieren, an denen sich Mitglieder der Sammlung anmelden. Sie können außerdem die **Affinität zwischen Benutzer und Gerät** so konfigurieren, dass die Software, die Sie bereitstellen, nur auf den Geräten installiert wird, die als Hauptgerät eines Benutzers angegeben sind. Diese Hauptgeräte werden als primäre Geräte bezeichnet. Ein Benutzer kann über ein oder mehrere primäre Geräte verfügen.  

 Eine der Möglichkeiten, mit denen Benutzer die Softwarebereitstellung auf ihren Geräten steuern können, ist die Verwendung der Computerclientschnittstelle **Softwarecenter**. Softwarecenter wird automatisch auf Clientcomputern installiert und kann von den Benutzern über das Startmenü aufgerufen werden. Mithilfe des Softwarecenters können Benutzer ihre eigene Software verwalten und Folgendes ausführen:  

-   Installieren von Software  

-   Planen der automatischen Installation der Software außerhalb der Arbeitszeit  

-   Konfigurieren, wann die Installation von Software auf ihrem Gerät durch Configuration Manager zulässig ist  

-   Konfigurieren der Zugriffseinstellungen für die Remotesteuerung, wenn die Remotesteuerung in Configuration Manager aktiviert ist  

-   Konfigurieren der Optionen für die Energieverwaltung, wenn dies von einem Administrator gestattet wurde  

 Über einen Link im Softwarecenter können Benutzer den **Anwendungskatalog**aufrufen und dort Software durchsuchen, installieren und anfordern. Darüber hinaus ermöglicht der Anwendungskatalog Benutzern das Konfigurieren einiger Voreinstellungen, das Zurücksetzen ihrer Mobilgeräte und (sofern diese Konfiguration zulässig ist) das Angeben ihrer eigenen primären Geräte für die Affinität zwischen Benutzer und Gerät. (Die Informationen zur Affinität zwischen Benutzer und Gerät können auch auf andere Weise konfiguriert werden, beispielsweise durch Importieren der Informationen aus einer Datei und durch automatisches Generieren anhand von Nutzungsdaten.)  

 Da es sich beim Anwendungskatalog um eine in IIS gehostete Website handelt, können Benutzer im Intranet oder Internet den Anwendungskatalog direkt mithilfe eines Browsers aufrufen.  



<!--HONumber=Nov16_HO1-->


