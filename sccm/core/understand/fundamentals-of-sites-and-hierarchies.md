---
title: Grundlagen von Standorten und Hierarchien | System Center Configuration Manager
description: Erhalten Sie grundlegende Informationen zu System Center Configuration Manager-Standorten und Hierarchien.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 07e10ead8d4b147a4a96b1e5189597e1ac4d4f52


---
# <a name="fundamentals-of-sites-and-hierarchies-for-system-center-configuration-manager"></a>Grundlagen von Standorten und Hierarchien für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Eine System Center Configuration Manager-Bereitstellung muss in einer Active Directory-Domäne installiert sein und verfügt über eine Grundlage von einem oder mehreren Configuration Manager-Standorten, die eine Hierarchie von Standorten bilden. Egal ob einzelner Standort oder Hierarchie mit mehreren Standorten – der Typ und der Speicherort der Standorte, die Sie installieren, bieten Ihnen die Möglichkeit, Ihre Bereitstellung bei Bedarf zentral hochzuskalieren, und liefern wichtige Dienste für verwaltete Benutzer und Geräte.

## <a name="hierarchies-of-sites"></a>Hierarchien von Standorten
Wenn Sie System Center Configuration Manager erstmals installieren, bestimmt der erste Configuration Manager-Standort den Umfang Ihrer Hierarchie. Diese bildet die Grundlage für die Verwaltung von Geräten und Benutzern in Ihrem Unternehmen. Dieser erste Standort muss entweder ein Standort der zentralen Verwaltung oder eigenständiger primärer Standort sein.  

 Ein **Standort der zentralen Verwaltung** eignet sich für umfangreiche Bereitstellungen. Er stellt eine Verwaltungszentrale bereit und unterstützt flexibel Geräte, die in einer globalen Netzwerkinfrastruktur verteilt sind. Nach der Installation eines Standorts der zentralen Verwaltung müssen Sie mindestens einen primären Standort als untergeordneten Standort installieren.  Dies ist erforderlich, weil ein Standort der zentralen Verwaltung die Geräteverwaltung nicht direkt unterstützt. Dies ist die Aufgabe eines primären Standorts. Ein Standort der zentralen Verwaltung unterstützt mehrere untergeordnete primäre Standorte zur direkten Verwaltung von Geräten sowie zur Steuerung der Netzwerkbandbreite, falls Ihre verwalteten Geräte sich an unterschiedlichen geografischen Orten befinden.  

 Ein **eigenständiger primärer Standort** eignet sich für kleinere Bereitstellungen und kann zum Verwalten von Geräten verwendet werden, ohne dass zusätzliche Standorte installiert werden müssen. Wenngleich ein eigenständiger primärer Standort die Größe Ihrer Bereitstellung begrenzen kann, unterstützt er ein Szenario zum Erweitern Ihrer Hierarchie zu einem späteren Zeitpunkt, indem ein neuer Standort der zentralen Verwaltung installiert wird. Bei diesem Standorterweiterungsszenario wird Ihr eigenständiger primärer Standort ein untergeordneter primärer Standort. Sie können anschließend zusätzliche untergeordnete primäre Standorte unter Ihrem neuen Standort der zentralen Verwaltung installieren.  Dadurch sind Sie in der Lage, Ihre anfängliche Bereitstellung bei künftigem Wachstum Ihres Unternehmens zu erweitern.  

> [!TIP]  
>  Ein eigenständiger primärer Standort und ein untergeordneter primärer Standort sind eigentlich der gleiche Standorttyp: ein primärer Standort. Der unterschiedliche Name basiert auf der Hierarchiebeziehung, die dann erstellt wird, wenn Sie auch einen Standort der zentralen Verwaltung verwenden.  Durch diese Hierarchiebeziehung kann auch die Installation bestimmter Standortsystemrollen eingeschränkt sein, mit denen die Funktionalität von Configuration Manager erweitert wird. Der Grund dafür ist, dass bestimmte Standortsystemrollen nur am Standort der obersten Ebene der Hierarchie, einem Standort der zentralen Verwaltung oder einem eigenständigen primären Standort, installiert werden können.  

 Nach der Installation Ihres ersten Standorts können Sie weitere Standorte installieren.  Wenn Ihr erster Standort ein Standort der zentralen Verwaltung war, können Sie einen oder mehrere untergeordnete primäre Standorten installieren.  Nach der Installation eines primären Standorts (eigenständig oder untergeordnet primär) können Sie einen oder mehrere sekundäre Standorte installieren.  

 Ein **sekundärer Standort** kann nur als untergeordneter Standort unter einem primären Standort installiert werden. Mit diesem Standorttyp können Sie die Reichweite eines primären Standorts zur Verwaltung von Geräten an Orten erweitern, die eine langsame Netzwerkverbindung mit dem primären Standort haben.   Obwohl ein sekundärer Standort den primären Standort erweitert, werden Clients weiterhin vom primären Standort verwaltet. Der sekundäre Standort unterstützt Geräte am Remotestandort, indem Daten, die Sie (für Bereitstellungen) an Clients senden und die diese Client zurück an den Standort senden, komprimiert werden und ihre Übertragung durch Ihr Netzwerk verwaltet wird.  

 Die folgenden Diagramme enthalten einige Beispiele für Standortentwürfe.  

 ![Beispiele für die Hierarchie](media/Hierarchy_examples.png)  

 Weitere Informationen finden Sie unter den folgenden Themen:  

-   [Einführung in System Center Configuration Manager](../../core/understand/introduction.md)  

-   [Entwerfen einer Hierarchie von Standorten für System Center Configuration Manager](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Installieren von System Center Configuration Manager-Standorten](/sccm/core/servers/deploy/install/installing-sites)  

## <a name="site-system-servers-and-site-system-roles"></a>Standortsystemserver und Standortsystemrollen  
 An jedem Configuration Manager-Standort werden **Standortsystemrollen** installiert, die Verwaltungsvorgänge unterstützen.  Einige Rollen werden standardmäßig installiert, wenn Sie einen Standort installieren, z.B. die Rolle **Standortserver** (die dem Computer zugewiesen wird, auf dem Sie den Standort installieren), und die Rolle „Standortdatenbankserver“ (die dem SQL-Server zugewiesen wird, der die Standortdatenbank hostet). Andere Standortsystemrollen sind optional und werden nur verwendet, wenn Sie die Funktionalität verwenden möchten, die eine Standortsystemrolle bietet.  Jeder Computer, der eine Standortsystemrolle hostet, wird als Standortsystemserver bezeichnet.  

 Für eine kleinere Bereitstellung von Configuration Manager können Sie anfänglich ggf. alle Ihre Standortsystemrollen direkt auf dem Standortservercomputer ausführen. Sobald Ihre verwaltete Umgebung wächst und Anforderungen zunehmen, können Sie zusätzliche Standortsystemserver installieren, um weitere Standortsystemrollen zu hosten. Dadurch können die Standorte weiteren Geräten Dienste effizienter bieten.  

 Informationen zu den verschiedenen Standortsystemrollen finden Sie im Abschnitt [Site system roles](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) (Standortsystemrollen) unter [Plan for site system servers and site system roles for System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md) (Planen von Standortsystemservern und Standortsystemrollen für System Center Configuration Manager).  

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Veröffentlichen von Standortinformationen in Active Directory-Domänendiensten  
 Zur Vereinfachung der Verwaltung von Configuration Manager können Sie das Active Directory-Schema zur Unterstützung von Details erweitern, die von Configuration Manager verwendet werden. Sie können anschließend Standorte ihre wichtigsten Informationen in Active Directory Domain Services (AD DS) veröffentlichen lassen. Dadurch können Computer, die Sie verwalten möchten, Standortinformationen aus der vertrauenswürdigen AD DS-Quelle geschützt abrufen. Die Informationen, die Clients abrufen können, bestimmen verfügbare Standorte, Standortsystemserver und die Dienste, die diese Standortsystemserver bereitstellen.  

 **Die Erweiterung des Active Directory-Schemas** erfolgt nur einmal pro Gesamtstruktur und kann vor oder nach der Installation von Configuration Manager stattfinden.   Wenn Sie das Schema erweitern, müssen Sie einen neuen Active Directory-Container namens **Systemverwaltung** in allen Domänen erstellen, die einen Configuration Manager-Standort enthalten, der Daten für Clients veröffentlicht. Weitere Informationen finden Sie unter [Extend the Active Directory schema for System Center Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md) (Erweitern des Active Directory-Schemas für den Configuration Manager).  

 Die **Veröffentlichung von Standortdaten** erhöht die Sicherheit Ihrer Configuration Manager-Hierarchie und reduziert den Verwaltungsaufwand, ist aber für grundlegende Configuration Manager-Funktionalität nicht erforderlich.  



<!--HONumber=Nov16_HO1-->


