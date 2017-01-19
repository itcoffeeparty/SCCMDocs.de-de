---
title: "Ausführen der Ermittlung | Microsoft-Dokumentation"
description: "Lesen Sie eine Übersicht über den Ermittlungsprozess und die Ermittlung von Datensätzen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
caps.latest.revision: 20
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 1d225b9f904215280feef5efd4283cbd51f84577


---
# <a name="run-discovery-for-system-center-configuration-manager"></a>Ausführen der Ermittlung für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können mindestens eine Ermittlungsmethode in    
      System Center Configuration Manager verwenden, um Geräte- und Benutzerressourcen zu finden, die Sie verwalten können. Sie können mithilfe der Ermittlung auch die Netzwerkinfrastruktur in Ihrer Umgebung bestimmen.  Es gibt verschiedene Ermittlungsmethoden, mit denen Sie unterschiedliche Dinge ermitteln können, wobei jede Methode ihre eigenen Konfigurationen und Einschränkungen hat.  

## <a name="overview-of-discovery"></a>Übersicht über die Ermittlung  
 Die Ermittlung ist der Prozess, über den Configuration Manager erfährt, welche Ressourcen Sie verwalten können. Es folgen die verfügbaren Ermittlungsmethoden:  

-   Active Directory-Gesamtstrukturermittlung  

-   Active Directory-Gruppenermittlung  

-   Active Directory-Systemermittlung  

-   Active Directory-Benutzerermittlung  

-   Frequenzermittlung  

-   Netzwerkermittlung  

-   Serverermittlung  

> [!TIP]  
>  Informationen zu den einzelnen Ermittlungsmethoden finden Sie unter [About discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md) (Informationen zu Ermittlungsmethoden in System Center Configuration Manager).  
>   
>  Entscheidungshilfen hinsichtlich der Methoden und den Standorten in Ihrer Hierarchie finden Sie unter [Select discovery methods to use for System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md) (Auswählen von Ermittlungsmethoden zur Verwendung in System Center Configuration Manager).  

 Für die meisten Ermittlungsmethoden müssen Sie die jeweilige Methode am Standort aktivieren und so konfigurieren, dass bestimmte Netzwerk- oder Active Directory-Standorte durchsucht werden. Während der Ausführung wird der angegebene Speicherort auf Informationen zu Geräten oder Benutzern abgefragt, die Configuration Manager verwalten kann.  Wenn eine Ermittlungsmethode Informationen zu einer Ressource findet, werden diese in einer Datei abgelegt, die als DDR (Discovery Data Record) bezeichnet und von einem primären Standort oder Standort der zentralen Verwaltung verarbeitet wird. Bei der Verarbeitung eines DDR wird ein neuer Datensatz in der Standortdatenbank für neu ermittelte Ressourcen erstellt, oder vorhandene Datensätze werden mit neuen Informationen aktualisiert.  

 Bei einigen Ermittlungsmethoden kann hoher Netzwerkdatenverkehr entstehen, und bei der Verarbeitung der resultierenden DDRs werden gegebenenfalls erhebliche CPU-Ressourcen in Anspruch genommen. Sie sollten sich daher auf die Ermittlungsmethoden beschränken, die zur Erreichung Ihrer Ziele erforderlich sind. Möglicherweise genügen ein oder zwei Ermittlungsmethoden für Ihre Zwecke. Später können Sie weitere Methoden Schritt für Schritt hinzufügen, um die Ermittlung in Ihrer Umgebung auszuweiten.  

 Die der Standortdatenbank hinzugefügten Ermittlungsinformationen werden anschließend an jeden Standort in der Hierarchie unabhängig davon repliziert, an welchen Standort sie ermittelt oder verarbeitet wurden. Daher können Sie an verschiedenen Standorten unterschiedliche Zeitpläne und Einstellungen für Ermittlungsmethoden konfigurieren. Es empfiehlt sich, eine bestimmte Ermittlungsmethode nur an einem einzelnen Standort ausführen, um die Belegung von Netzwerkbandbreite aufgrund der Duplizierung von Ermittlungsaktionen und die Verarbeitung redundanter Ermittlungsdaten an mehreren Standorten zu reduzieren.  

 Sie können Ermittlungsdaten verwenden, um benutzerdefinierte Sammlungen und Abfragen zu erstellen, um Ressourcen für die folgenden Verwaltungsaufgaben logisch zu gruppieren:  

-   Pushübertragung von Clientinstallationen oder Upgrades  

-   Bereitstellen von Inhalten für Benutzer oder Geräte  

-   Bereitstellen von Clienteinstellungen und zugehörigen Konfigurationen  

##  <a name="a-namebkmkddrsa-about-discovery-data-records"></a><a name="BKMK_DDRs"></a> Informationen zu Discovery Data Records  
 Discovery Data Records (DDRs) sind Dateien, die durch eine Ermittlungsmethode erstellt wurden. Sie enthalten Informationen zu einer Ressource, die Sie in Configuration Manager verwalten können. DDRs enthalten Informationen über Computer, Benutzer und in einigen Fällen über die Netzwerkinfrastruktur. Sie werden auf primären Standorten oder auf Standorten der zentralen Verwaltung verarbeitet. Nachdem die im DDR enthaltenen Ressourceninformationen in die Datenbank eingetragen wurden, wird der DDR gelöscht, und die Informationen werden als globale Daten auf alle Standorte in der Hierarchie repliziert.  

 Auf welchem Standort ein DDR verarbeitet wird, ist abhängig von den enthaltenen Informationen:  

-   DDRs für neu ermittelte und noch nicht in der Datenbank enthaltene Ressourcen werden auf dem Standort auf der obersten Ebene der Hierarchie verarbeitet. Vom Standort auf der obersten Ebene der Hierarchie wird ein neuer Ressourcendatensatz in der Datenbank erstellt und diesem eine eindeutige ID zugeordnet. DDRs werden mithilfe von dateibasierter Replikation bis auf den Standort auf der obersten Ebene übertragen.  

-   DDRs für bereits ermittelte Objekte werden auf primären Standorten verarbeitet. Von untergeordneten Standorten werden DDRs nicht an den Standort der zentralen Verwaltung übertragen, wenn der DDR Informationen über eine Ressource enthält, die sich bereits in der Datenbank befindet.  

-   Discovery Data Records werden von sekundären Standorten nicht verarbeitet, sondern von diesen immer mithilfe von dateibasierter Replikation an den übergeordneten primären Standort übertragen.  

DDR-Dateien verfügen über die Erweiterung DDR und über eine Größe von in der Regel ca. 1 KB.  

## <a name="get-started-with-discovery"></a>Erste Schritte mit der Ermittlung:  
 Vor Verwendung der Configuration Manager-Konsole zum Konfigurieren der Ermittlung sollten sich mit den Unterschieden zwischen den Methoden, ihren Möglichkeiten und (bei einigen) ihren Einschränkungen vertraut machen.  
Die folgenden Themen bieten grundlegende Informationen zur erfolgreichen Nutzung von Ermittlungsmethoden:  

-   [About discovery methods for System Center Configuration Manager (Informationen zu Ermittlungsmethoden in System Center Configuration Manager)](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Select discovery methods to use for System Center Configuration Manager (Auswählen von Ermittlungsmethoden zur Verwendung in System Center Configuration Manager)](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Wenn Sie die Methoden verstehen, die Sie verwenden möchten, finden Sie einen Leitfaden zum Konfigurieren jeder einzelnen Methode in [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md) (Konfigurieren von Ermittlungsmethoden für System Center Configuration Manager).  



<!--HONumber=Dec16_HO3-->


