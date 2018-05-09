---
title: Konfigurieren von Begrenzungsgruppen
titleSuffix: Configuration Manager
description: Unterstützen Sie Clients bei der Suche nach Standortsystemen, indem Sie Begrenzungsgruppen für die logische Organisation zusammenhängender Netzwerkadressen verwenden, die auch als Grenzen bezeichnet werden
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79c6796c116fbe4d182827e24f41ae4d1e5242fe
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>Begrenzungsgruppen für System Center Configuration Manager


*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie Begrenzungsgruppen in Configuration Manager für die logische Organisation zusammenhängender Netzwerkadressen ([Grenzen](/sccm/core/servers/deploy/configure/boundaries)), um die Verwaltung Ihrer Infrastruktur zu erleichtern. Weisen Sie Begrenzungsgruppen Grenzen zu, bevor Sie die Begrenzungsgruppe verwenden.

Standardmäßig erstellt Configuration Manager eine Standard-Standortbegrenzungsgruppe an jedem Standort.

Ordnen Sie der Begrenzungsgruppe Grenzen (Netzwerkadressen) und Standortsystemrollen wie Verteilungspunkte zu, um Begrenzungsgruppen zu konfigurieren. Durch diese Konfiguration können Clients mit Standortsystemservern wie Verteilungspunkten verknüpft werden, die sich in der Nähe der Clients auf dem Netzwerk befinden.

Wenn Sie die Verfügbarkeit der Standortsystemserver, z.B. Verteilungspunkte, auf einen größeren Bereich von Netzwerkadressen erhöhen möchten, müssen Sie mehreren Begrenzungsgruppen dieselbe Grenze und denselben Server zuweisen.

Client verwenden eine Begrenzungsgruppe für Folgendes:  

-   Automatische Standortzuweisung  
-   um einen Standortsystemserver zu finden, der einen Dienst bereitstellen kann, darunter z.B.:
    - Verteilungspunkte für Inhaltsstandorte
    -   Softwareupdatepunkte
    - Zustandsmigrationspunkte
    - Bevorzugte Verwaltungspunkte (wenn Sie bevorzugte Verwaltungspunkte verwenden, müssen Sie diese Option für die Hierarchie und nicht über die Konfiguration der Begrenzungsgruppe aktivieren. Weitere Informationen finden Sie unter [So aktivieren Sie die Verwendung bevorzugter Verwaltungspunkte](#to-enable-use-of-preferred-management-points) in diesem Thema.)

##  <a name="boundary-groups-and-relationships"></a>Begrenzungsgruppen und Beziehungen
Für jede Begrenzungsgruppe in Ihrer Hierarchie können Sie folgende Zuweisungen vornehmen:

-  Eine oder mehrere Grenzen. Bei der **aktuellen** Begrenzungsgruppe eines Clients handelt es sich um eine Netzwerkadresse, die als Grenze definiert ist, die einem bestimmten Begrenzungsgruppe zugewiesen ist. Ein Client kann mehr als eine aktuelle Begrenzungsgruppe aufweisen.
- Eine oder mehrere Standortsystemrollen. Clients können immer Standortsystemrollen verwenden, die mit der aktuellen Begrenzungsgruppe verknüpft sind. Je nach zusätzlichen Konfigurationen haben sie möglicherweise die Möglichkeit, Standortsystemrollen in zusätzlichen Begrenzungsgruppen zu verwenden.  

Für jede von Ihnen erstellte Begrenzungsgruppe können Sie einen unidirektionalen Link zu einer anderen Begrenzungsgruppe konfigurieren. Dieser Link wird als **Beziehung** bezeichnet. Die Begrenzungsgruppen, mit denen Sie verknüpfen, heißen **Nachbarbegrenzungsgruppen**. Eine Begrenzungsgruppe kann mehrere Beziehungen mit unterschiedlichen Nachbarbegrenzungsgruppen haben.

Wenn ein Client in seiner aktuellen Begrenzungsgruppe keinen verfügbaren Standortsystemserver ausfindig machen kann, wird mit der Konfiguration jeder Beziehung festgelegt, wann mit der Suche nach einer verfügbaren benachbarten Begrenzungsgruppe begonnen werden kann. Diese Suche in zusätzlichen Gruppen wird als **Fallback** bezeichnet.

## <a name="fallback"></a>Fallback
Wenn Clients in ihrer aktuellen Begrenzungsgruppe kein verfügbares Standortsystem finden können, sollten Sie zur Vermeidung von Problemen für das Fallbackverhalten die Beziehung zwischen Begrenzungsgruppen definieren. Durch Fallback kann ein Client seine Suche auf zusätzliche Begrenzungsgruppen erweitern, um ein verfügbares Standortsystem zu finden.

Beziehungen werden auf der Registerkarte **Beziehungen** in den Eigenschaften der Begrenzungsgruppe. Wenn Sie eine Beziehung konfigurieren, definieren Sie eine Verknüpfung mit einer Nachbarbegrenzungsgruppe. Konfigurieren Sie für jeden unterstützten Typ von Standortsystemrollen unabhängige Fallbackeinstellungen für die jeweilige benachbarte Begrenzungsgruppe. Wenn Sie beispielsweise eine Beziehung mit einer bestimmten Begrenzungsgruppe konfigurieren, können Sie festlegen, dass das Fallback für Verteilungspunkte schon nach 20 Minuten und nicht erst, wie es der Standard ist, nach 120 Minuten auftritt. Ein ausführlicheres Beispiel finden Sie unter [Beispiel für das Verwenden von Begrenzungsgruppen](#example-of-using-boundary-groups).

Wenn ein Client in seiner aktuellen Begrenzungsgruppe keine verfügbare Standortsystemrolle finden kann, verwendet er die Fallbackzeit in Minuten. Diese Fallbackzeit bestimmt, wann der Client mit der Suche nach einem verfügbaren Standortsystem beginnt, das mit der benachbarten Begrenzungsgruppe verknüpft ist.  

Wenn ein Client kein verfügbares Standortsystem finden kann und beginnt, Speicherorte in benachbarten Begrenzungsgruppen zu durchsuchen, wird der Pool verfügbarer Standortsysteme vergrößert. Die Konfiguration von Begrenzungsgruppen und den zugehörigen Beziehungen definiert die Clientverwendung dieser Pools mit verfügbaren Standortsystemen.

- Eine Begrenzungsgruppe kann mehr als eine Beziehung haben. Mit mehreren Beziehungen können Sie das Fallback für alle Standortsystemtypen für unterschiedliche Nachbarn konfigurieren, der nach unterschiedlich langen Zeitspannen erfolgen soll.    
- Das Ziel des Fallbacks eines Clients kann nur eine Begrenzungsgruppe sein, die ein direkter Nachbar der aktuellen Begrenzungsgruppe ist.
- Wenn ein Client Mitglied mehrerer Begrenzungsgruppen ist, wird die aktuelle Begrenzungsgruppe als die Gesamtheit aller Begrenzungsgruppen dieses Clients definiert. Anschließend erfolgt ein Fallback dieses Clients auf einen Nachbarn einer beliebigen dieser ursprünglichen Begrenzungsgruppen.

### <a name="the-default-site-boundary-group"></a>Die standardmäßige Standortbegrenzungsgruppe
Zusätzlich zu den von Ihnen erstellten Begrenzungsgruppen hat jeder Standort eine Standard-Standortbegrenzungsgruppe, die von Configuration Manager erstellt wird. Diese Gruppe heißt ***Default-Site-Boundary-Group&lt;sitecode>***. Die Gruppe des Standorts ABC hieße z.B. *Default-Site-Boundary-Group&lt;ABC>*.

Für jede von Ihnen erstellte Begrenzungsgruppe erstellt Configuration Manager automatisch einen implizierten Link zu jeder Standard-Standortbegrenzungsgruppe in der Hierarchie.
-   Der implizierte Link ist eine Standardoption für ein Fallback von der aktuellen Begrenzungsgruppe auf die Standardbegrenzungsgruppe der Standorte, die eine Standardfallbackzeit von 120 Minuten hat.
-   Bei Clients, die sich nicht in einer mit einer anderen Begrenzungsgruppe verknüpften Grenze befinden: Verwenden Sie die standardmäßige Standortbegrenzungsgruppe des zugewiesenen Standorts, um gültige Standortsystemrollen zu ermitteln.

So verwalten Sie das Fallback auf die Standard-Standortbegrenzungsgruppe:
- Öffnen Sie die Einstellungen der standardmäßigen Standortbegrenzungsgruppe, und ändern Sie die Werte auf der Registerkarte **Standardverhalten**. Die Änderungen, die Sie hier vornehmen, gelten für *alle* implizierten Links zu dieser Begrenzungsgruppe. Diese Einstellungen können außer Kraft gesetzt werden, indem Sie den expliziten Link zu dieser Standard-Standortbegrenzungsgruppe einer anderen Begrenzungsgruppe konfigurieren.
- Öffnen Sie die Eigenschaften einer benutzerdefinierten Begrenzungsgruppe. Ändern Sie die Werte für den expliziten Link in eine standardmäßige Standortbegrenzungsgruppe. Wenn Sie eine neue Zeit (in Minuten) für das Fallback oder das Blockieren des Fallbacks festlegen, wirkt sich diese Änderung nur auf den von Ihnen konfigurierten Link aus. Durch die Konfiguration des expliziten Links werden die Einstellungen auf der Registerkarte **Standardverhalten** der standardmäßigen Standortbegrenzungsgruppe überschrieben.


## <a name="site-assignment"></a>Standortzuweisung  
 Sie können jede Begrenzungsgruppe mit einem zugewiesenen Standort für Clients konfigurieren.  

-   Ein neu installierter Client, der die automatische Standortzuweisung verwendet, tritt dem zugewiesenen Standort einer Begrenzungsgruppe bei, die die aktuelle Netzwerkadresse des Clients enthält.  
-   Nach Zuweisung zu einem Standort ändert sich die Standortzuweisung eines Clients nicht, wenn sich seine Netzwerkadresse ändert. Beim Wechsel des Clients zu einer neuen Netzwerkadresse, die von einer Grenze in einer Begrenzungsgruppe mit abweichender Standortzuweisung repräsentiert wird, bleibt der dem Client zugewiesene Standort beispielsweise unverändert.  
-   Wenn mithilfe von Active Directory-Systemermittlung eine neue Ressource ermittelt wird, werden die Netzwerkinformationen für diese Ressource anhand der Grenzen in Begrenzungsgruppen bewertet. Dabei wird die neue Ressource einem zugewiesenen Standort zur Verwendung bei einer Clientpushinstallation zugeordnet.  
-   Wenn eine Grenze zu mehreren Begrenzungsgruppen gehört, denen verschiedene Standorte zugewiesen sind, wählen die Clients einen dieser Standorte nach dem Zufallsprinzip aus.  
-   Änderungen an dem zugewiesenen Standort einer Begrenzungsgruppe betreffen nur neue Standortzuweisungsaktionen. Clients, die bereits zuvor einem Standort zugewiesen wurden, bewerten ihre Standortzuweisung nicht basierend auf Änderungen an der Konfiguration einer Begrenzungsgruppe (oder ihrer eigenen Netzwerkadresse) neu.  

Weitere Informationen zur automatischen Standortzuweisung finden Sie unter [Verwenden von automatischen Standortzuweisungen für Computer](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [Zuweisen von Clients zu einem Standort in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

## <a name="distribution-points"></a>Verteilungspunkte

Wenn ein Client den Speicherort eines Verteilungspunkts anfordert, sendet Configuration Manager dem Client eine Liste der Standortsysteme. Diese Standortsysteme weisen den entsprechenden Typ auf, der mit den einzelnen Begrenzungsgruppen verknüpft ist, welche die aktuelle Netzwerkadresse des Clients enthalten:

-   **Während der Softwareverteilung** fordern Clients einen Speicherort für Bereitstellungsinformationen an, die auf einem Verteilungspunkt oder einer anderen gültigen Inhaltsquelle zur Verfügung stehen (wie z.B. ein Client, der für Peer Cache konfiguriert wurde).

-   **Während der Bereitstellung des Betriebssystems** fordern Clients einen Speicherort zum Senden oder Empfangen ihrer Zustandsmigrationsinformationen an.  

Wenn ein Client während der Inhaltsbereitstellung Inhalte anfordert, die aus einer Quelle in seiner aktuellen Begrenzungsgruppe nicht verfügbar sind, fährt der Client mit der Anforderung dieser Inhalte fort. Der Client testet unterschiedliche Inhaltsquellen in seiner aktuellen Begrenzungsgruppe aus, bis der Fallbackzeitraum für eine benachbarte Begrenzungsgruppe oder die standardmäßige Standortbegrenzungsgruppe erreicht ist. Wenn der Client noch keinen Inhalt gefunden hat, erweitert er seine Suche nach Inhaltsquellen auf die Nachbarbegrenzungsgruppen.

Wenn der Inhalt bei Bedarf verteilt wird und an einem Verteilungspunkt nicht verfügbar ist, wenn er von einem Client angefordert wird, beginnt der Prozess zum Übertragen des Inhalts zu diesem Verteilungspunkt. Es besteht die Möglichkeit, dass der Client diesen Server als Inhaltsquelle findet, bevor ein Fallback zur Verwendung einer benachbarten Begrenzungsgruppe durchgeführt wird.

## <a name="software-update-points"></a>Softwareupdatepunkte
Clients verwenden Begrenzungsgruppen zur Auswahl neuer Softwareupdatepunkte. Zur Steuerung, welchen Server ein Client finden kann, können Sie zu verschiedenen Begrenzungsgruppen einzelne Softwareupdatepunkte hinzufügen.

Wenn Sie ein Update von einer früheren Version als Version 1702 durchführen, werden alle vorhandenen Softwareupdatepunkte zur standardmäßigen Standortbegrenzungsgruppe hinzugefügt. Durch dieses Standortupdateverhalten wird das vorherige Clientverhalten bei der Auswahl eines Softwareupdatepunkts aus dem Pool der verfügbaren Server verwaltet. Dieses Verhalten wird so lange beibehalten, bis Sie einzelne Softwareupdatepunkte in unterschiedliche Begrenzungsgruppen einfügen, um ein gesteuertes Auswahl- und Fallbackverhalten zu erzielen.

Wenn Sie einen neuen Standort installieren, werden keine Softwareupdatepunkte zur standardmäßigen Standortbegrenzungsgruppe hinzugefügt. Weisen Sie Softwarepudatepunkte zu einer Begrenzungsgruppe hinzu, damit Clients sie suchen und nutzen können.

### <a name="fallback-for-software-update-points"></a>Fallback für Softwareupdatepunkte
Das Fallback für Softwareupdatepunkte wird genauso wie für andere Standortsystemrollen konfiguriert, hat aber folgende Probleme:
- **Neue Clients verwenden Begrenzungsgruppen zur Auswahl von Softwareupdatepunkten.** Von Ihnen installierte Clients wählen aus den Servern einen Softwareupdatepunkt aus, die mit der von Ihnen konfigurierten Begrenzungsgruppe verknüpft sind. Durch dieses Verhalten wird das vorherige Verhalten ersetzt, bei dem die Clients zufällig einen Softwareupdatepunkt aus der Liste der Server auswählen, die sich die Gesamtstruktur des Clients teilen.

- **Clients verwenden so lange den bisher funktionierenden Softwareupdatepunkt, bis sie ein Fallback ausführen, um einen neuen zu finden.** Clients, die bereits über einen Softwareupdatepunkt verfügen, verwenden diesen so lange weiter, bis er nicht erreicht werden kann. Dieses Verhalten betrifft auch die weitere Verwendung eines Softwareupdatepunkts, der nicht mit der aktuellen Begrenzungsgruppe des Clients verknüpft ist.

  Die weitere Verwendung eines vorhandenen Softwareupdatepunkts ist beabsichtigt, auch wenn sich dieser Server nicht in der aktuellen Begrenzungsgruppe eines Clients befindet. Wenn sich der Softwareupdatepunkt ändert, synchronisiert der Client Daten mit dem neuen Server. Dies verursacht eine erhebliche Netzwerkauslastung. Wenn alle Clients gleichzeitig zu einem neuen Server wechseln, kann durch die Verzögerung beim Übergang eine Komplettauslastung Ihres Netzwerks vermieden werden.

- **Ein Client versucht immer 120 Minuten lang, den bisher funktionierenden Softwareupdatepunkt zu erreichen, bevor ein Fallback initialisiert wird.** Wenn der Client 120 Minuten lang keinen Kontakt herstellen konnte, kommt es zu einem Fallback. Die Einleitung des Fallback führt dazu, dass der Client von seiner aktuellen Begrenzungsgruppe eine Liste der Softwareupdatepunkte erhält. Abhängig von den Fallbackkonfigurationen können auch zusätzliche Softwareupdatepunkte von benachbarten und standardmäßigen Standortbegrenzungsgruppen verfügbar sein.

### <a name="fallback-configurations-for-software-update-points"></a>Fallbackkonfigurationen für Softwareupdatepunkte
#### <a name="beginning-with-version-1706"></a>Ab Version 1706   
Sie können die **Fallbackzeit (in Minuten)** für Softwareupdatepunkte auch auf unter 120 Minuten einstellen. Der Client versucht jedoch weiterhin 120 Minuten lang, seinen ursprünglichen Softwareupdatepunkt zu erreichen. Anschließend erweitert er seine Suche auf zusätzliche Server. Die Fallbackzeiten für Begrenzungsgruppen beginnen, wenn der Client seinen ursprünglichen Server zum ersten Mal nicht erreicht. Wenn der Client seine Suche erweitert, werden am Standort alle Begrenzungsgruppen bereitgestellt, die für weniger als 120 Minuten konfiguriert wurden.

Zum Blockieren des Fallbacks eines Softwareupdatepunkts auf eine benachbarte Begrenzungsgruppe können Sie die Einstellung **Kein Fallback** konfigurieren.

Nachdem er zwei Stunden erfolglos den Kontakt zu seinem ursprünglichen Server gesucht hat, sucht der Client nun mit einer kürzeren Zeitspanne nach einem neuen Softwareupdatepunkt. Durch dieses Verhalten kann der Client die erweiterte Liste potenzieller Softwareupdatepunkte schneller durchgehen.

 -  **Beispiel eines Fallback**  
    Für die aktuelle Begrenzungsgruppe eines Clients ist ein Fallback für Softwareupdatepunkte konfiguriert: *10* Minuten für die Begrenzungsgruppe *A* und *130* Minuten für die Begrenzungsgruppe *B*. Wenn der Client den bisher funktionierenden Softwareupdatepunkt nicht erreichen kann, geschieht Folgendes:
    -   Der Client versucht 120 Minuten lang den ursprünglichen Server zu erreichen. Nach 10 Minuten werden die Softwareupdatepunkte aus der Begrenzungsgruppe A in den Pool der verfügbaren Server aufgenommen. Der Client kann jedoch erst zu ihnen oder einem anderen Server Kontakt aufnehmen, wenn die Zeitspanne (120 Minuten) für den Verbindungsversuch mit dem ursprünglichen Server abgelaufen ist.
    -   Nachdem 120 Minuten lang versucht wurde, den usprünglichen Softwareupdatepunkt zu finden, kann der Client seine Suche ausdehnen. Dazu fügt der Client Server aus seiner aktuellen Begrenzungsgruppe und aus benachbarten Begrenzungsgruppen, die für 120 Minuten oder weniger konfiguriert wurden, zum Pool der verfügbaren Softwareupdatepunkte hinzu. In diesem Pool sind die Server der Begrenzungsgruppe A enthalten, die bereits vorher zum Pool der verfügbaren Server hinzugefügt wurden.
    -       Nach weiteren 10 Minuten (insgesamt 130 Minuten nach der ersten fehlgeschlagenen Kontaktaufnahme zwischen Client und Softwareupdatepunkt) dehnt der Client seine Suche auf die Softwareupdatepunkte der Begrenzungsgruppe B aus.  

#### <a name="prior-to-version-1706"></a>Vor Version 1706
Vor Version 1706 kann bei Fallbackkonfigurationen für Softwareupdatepunkte keine Zeit in Minuten angegeben werden. Stattdessen ist das Fallbackverhalten auf Folgendes beschränkt:

  - **Fallbackzeit (in Minuten)**: Diese Option ist für Softwareupdatepunkte abgeblendet und kann nicht konfiguriert werden. Sie ist auf 120 Minuten festgelegt.
  -     **Kein Fallback:** Mit dieser Konfiguration können Sie das Fallback für einen Softwareupdatepunkt auf eine Nachbarbegrenzungsgruppe blockieren.

Wenn ein Client, der bereits über einen Softwareupdatepunkt verfügt, diesen nicht erreichen kann, führt er ein Fallback aus, um einen anderen Softwareupdatepunkt zu finden. Beim Verwenden von Fallback erhält der Client eine Liste von Softwareupdatepunkten von seiner aktuellen Begrenzungsgruppe. Wenn er 120 Minuten lang keinen verfügbaren Server finden kann, fällt er auf seine benachbarten Begrenzungsgruppen und die standardmäßige Standortbegrenzungsgruppe zurück. Das Fallback auf die beiden Begrenzungsgruppen erfolgt gleichzeitig. Die Fallbackzeit für den Softwareupdatepunkt auf benachbarte Gruppen ist auf 120 Minuten festgelegt. Diese Fallbackzeit kann nicht geändert werden. Das Standardzeitintervall für Fallback auf die Standard-Standortbegrenzungsgruppe ist ebenfalls auf 120 Minuten festgelegt. Wenn ein Client sowohl auf die Nachbar- als auch auf die Standard-Standortbegrenzungsgruppe zurückfällt, versucht er, mit den Softwareupdatepunkten von der Nachbarbegrenzungsgruppe Kontakt aufzunehmen, bevor er einen Punkt aus der Standard-Standortbegrenzungsgruppe verwendet.

### <a name="manually-switch-to-a-new-software-update-point"></a>Manuell auf einen neuen Softwareupdatepunkt wechseln
Zusätzlich zur Verwendung des Fallback, können Sie die Option *Clientbenachrichtigung* nutzen, um ein Gerät manuell zu einem Wechsel auf einen neuen Softwareupdatepunkt zu zwingen.

Beim Wechseln auf einen neuen Server wird das Fallback verwendet, um diesen zu finden. Überprüfen Sie die Konfigurationen für Ihre Begrenzungsgruppen. Stellen Sie vor diesem Wechsel sicher, dass sich Ihre Softwareupdatepunkte in den richtigen Begrenzungsgruppen befinden.

Weitere Informationen finden Sie unter [Manuelles Wechseln von Clients auf einen neuen Softwareupdatepunkt](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).



## <a name="management-points"></a>Verwaltungspunkte
<!-- 1324594 -->
Ab Version 1802 werden Fallbackbeziehungen für Verwaltungspunkte zwischen Begrenzungsgruppen konfiguriert. Dieses Verhalten ermöglicht eine bessere Steuerung der von Clients verwendeten Verwaltungspunkte. Auf der Registerkarte **Beziehungen** der Eigenschaften einer Begrenzungsgruppe gibt es eine Spalte für den Verwaltungspunkt. Wenn Sie eine neue Fallback-Begrenzungsgruppe hinzufügen, ist die Fallbackzeit für den Verwaltungspunkt derzeit immer Null (0). Dieses Verhalten entspricht dem **Standardverhalten** der Standardbegrenzungsgruppe des Standorts.

Bisher tritt ein allgemeines Problem auf, wenn Sie über einen geschützten Verwaltungspunkt in einem sicheren Netzwerk verfügen. Clients im Hauptunternehmensnetzwerk empfangen eine Richtlinie, die diesen geschützten Verwaltungspunkt enthält, auch wenn sie über eine Firewall nicht mit diesem Punkt kommunizieren können. Um dieses Problem zu beheben, verwenden Sie die Option **Nie ein Fallback durchführen**, um sicherzustellen, dass Clients nur ein Fallback auf Verwaltungspunkte durchführen, mit denen sie kommunizieren können.

Beim Upgrade des Standorts auf Version 1802 fügt Configuration Manager alle Verwaltungspunkte ohne Internetzugriff zur standardmäßigen Standortbegrenzungsgruppe hinzu. Dieses Upgradeverhalten stellt sicher, dass ältere Clientversionen weiterhin mit Verwaltungspunkten kommunizieren können. Damit Sie dieses Feature vollständig nutzen können, verschieben Sie Ihre Verwaltungspunkte in die gewünschten Begrenzungsgruppen.

Das Fallback bei Verwaltungspunkten in Begrenzungsgruppen ändert das Verhalten während der Clientinstallation („ccmsetup.exe“) nicht. Wenn der anfängliche Verwaltungspunkt nicht in der Befehlszeile mit dem Parameter „/MP“ angegeben wird, empfängt der neue Client die vollständige Liste aller verfügbaren Verwaltungspunkte. Für den anfänglichen Bootstrapprozess verwendet der Client den ersten Verwaltungspunkt, auf den er zugreifen kann. Sobald der Client beim Standort registriert ist, erhält er die gemäß diesem neuen Verhalten ordnungsgemäß sortierte Verwaltungspunktliste. 

Aktivieren Sie die folgende Einstellung, damit Clients diese Funktion verwenden: **Clients bevorzugen die Verwendung von in Begrenzungsgruppen angegebenen Verwaltungspunkten** unter **Hierarchieeinstellungen**. 

> [!Note]
> Bei Prozessen der Betriebssystembereitstellung haben Begrenzungsgruppen keine Bedeutung.

### <a name="troubleshooting"></a>Problembehandlung
Im **LocationServices.log** werden neue Einträge angezeigt. Das Attribut **Ort** identifiziert einen der folgenden Zustände:
- 0: Unbekannt.
- 1: Der angegebene Verwaltungspunkt befindet sich nur in der standardmäßigen Standortbegrenzungsgruppe für das Fallback.
- 2: Der angegebene Verwaltungspunkt befindet sich in einer Remotebegrenzungsgruppe oder einer benachbarten Begrenzungsgruppe. Wenn sich der Verwaltungspunkt sowohl in einer benachbarten als auch der standardmäßigen Standortbegrenzungsgruppe befindet, lautet der Wert für den Ort „2“.
- 3: Der angegebene Verwaltungspunkt befindet sich in der lokalen oder aktuellen Begrenzungsgruppe. Wenn sich der Verwaltungspunkt sowohl in der aktuellen als auch entweder in einer benachbarten oder der standardmäßigen Standortbegrenzungsgruppe befindet, lautet der Wert für den Ort „3“. Wenn Sie die Einstellung für bevorzugte Verwaltungspunkte in den Hierarchieeinstellungen nicht aktivieren, lautet der Ort immer „3“, unabhängig davon, in welcher Begrenzungsgruppe sich der Verwaltungspunkt befindet.

Clients verwenden zuerst lokale Verwaltungspunkte (Ort 3), danach Remotepunkte (Ort 2), dann Fallbackpunkte (Ort 1). 

Wenn ein Client innerhalb von 10 Minuten fünf Fehler empfängt und mit keinem Verwaltungspunkt in der aktuellen Begrenzungsgruppe kommunizieren kann, versucht er, einen Verwaltungspunkt in einer benachbarten Begrenzungsgruppe oder der standardmäßigen Standortbegrenzungsgruppe zu kontaktieren. Wenn der Verwaltungspunkt in der aktuellen Begrenzungsgruppe zu einem späteren Zeitpunkt wieder online geschaltet wird, kehrt der Client beim nächsten Aktualisierungszyklus zum lokalen Verwaltungspunkt zurück. Der Aktualisierungszyklus beträgt 24 Stunden. Er beginnt ebenfalls von Neuem, wenn der Configuration Manager-Agent-Dienst neu gestartet wird.




## <a name="preferred-management-points"></a>Bevorzugte Verwaltungspunkte

 > [!Note]
 > Das Verhalten dieser Hierarchieeinstellung, **Clients bevorzugen die in Begrenzungsgruppen angegebenen Verwaltungspunkte**, ändert sich ab Version 1802. Wenn Sie diese Einstellung aktivieren, verwendet Configuration Manager die Begrenzungsgruppenfunktion für den zugewiesenen Verwaltungspunkt. Weitere Informationen finden Sie unter [Verwaltungspunkte](#management-points). 

 Bevorzugte Verwaltungspunkte ermöglichen einem Client die Identifikation eines Verwaltungspunkts, der seiner aktuellen Netzwerkadresse (oder Begrenzung) zugeordnet ist.  

-   Ein Client versucht zunächst, einen bevorzugten Verwaltungspunkt seines zugewiesenen Standorts zu verwenden, bevor er einen Verwaltungspunkt seines zugewiesenen Standorts verwendet, der nicht als bevorzugt konfiguriert wurde.  
-   Aktivieren Sie für die Verwendung dieser Option **Clients bevorzugen die Verwendung von in Begrenzungsgruppen angegebenen Verwaltungspunkten** unter **Hierarchieeinstellungen**. Konfigurieren Sie anschließend Begrenzungsgruppen an den einzelnen primären Standorten. Schließen Sie die Verwaltungspunkte ein, die mit den zugehörigen Grenzen dieser Begrenzungsgruppe verknüpft werden sollten.
-   Wenn Sie bevorzugte Verwaltungspunkte konfigurieren und ein Client seine Liste der Verwaltungspunkte organisiert, ordnet er die bevorzugten Verwaltungspunkte am Anfang seiner Liste an. Diese Liste enthält sämtliche Verwaltungspunkte von den zugewiesenen Standorten des Clients.  

> [!NOTE]  
>  Clientroaming bedeutet, dass die Netzwerkadressen geändert werden. Beispiel: Wechsel eines Laptops an einen Remotestandort. Beim Roaming eines Clients kann dieser vor dem Versuch, einen Server des ihm zugewiesenen Standorts zu verwenden, ein Verwaltungspunkt oder ein Proxyverwaltungspunkt des lokalen Standorts als neuen Standort verwenden. Die Liste der Server des ihm zugewiesenen Standorts enthält die bevorzugten Verwaltungspunkte. Weitere Informationen finden Sie unter [Understand how clients find site resources and services (Verstehen, wie Clients Standortressourcen und -dienste suchen)](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="overlapping-boundaries"></a>Überlappende Grenzen  
 Bei der Abfrage von Inhaltsorten werden überlappende Grenzkonfigurationen von Configuration Manager unterstützt. Wenn die Netzwerkadresse des Clients zu mehreren Begrenzungsgruppen gehört:

-   Wenn ein Client Inhalte anfordert, sendet Configuration Manager dem Client eine Liste mit sämtlichen Verteilungspunkten, die über diese Inhalte verfügen.  
-   Wenn von einem Client Zustandsmigrationsinformationen bei einem Server angefordert bzw. an diesen gesendet werden, sendet Configuration Manager dem Client eine Liste mit sämtlichen Zustandsmigrationspunkten, die mit einer Begrenzungsgruppe mit der aktuellen Netzwerkadresse des Clients verknüpft sind.  

So kann von den Clients der am nächsten liegende Server zur Übertragung der Inhalts- oder Zustandsmigrationsinformationen ausgewählt werden.  



## <a name="example-of-using-boundary-groups"></a>Beispiel für das Verwenden von Begrenzungsgruppen
In folgendem Beispiel wird ein Client verwendet, der in einem Verteilungspunkt nach Inhalt sucht. Dieses Beispiel kann auch auf andere Standortsystemrollen angewendet werden, die Begrenzungsgruppen verwenden. Beachten Sie, dass Softwareupdatepunkte die Konfiguration der Fallbackzeit auf eine benachbarte Gruppe nicht unterstützen und immer ein Intervall von 120 Minuten verwenden.

Sie erstellen drei Begrenzungsgruppen, die keine Grenzen oder Standortsystemserver teilen:
-   Gruppe BG_A mit den Verteilungspunkten DP_A1 und DP_A2, die der Gruppe zugeordnet sind
-   Gruppe BG_B mit den Verteilungspunkten DP_B1 und DP_B2, die der Gruppe zugeordnet sind
-   Gruppe BG_C mit den Verteilungspunkten DP_C1 und DP_C2, die der Gruppe zugeordnet sind

Fügen Sie die Netzwerkadressen Ihrer Clients nur in der Begrenzungsgruppe BG_A als Grenzen hinzu. Konfigurieren Sie anschließend Beziehungen aus dieser Begrenzungsgruppe für die anderen zwei Begrenzungsgruppen:
-   Konfigurieren Sie Verteilungspunkte für die erste *benachbarte* Gruppe (BG_B), die nach 10 Minuten verwendet wird. Diese Gruppe enthält die Verteilungspunkte DP_B1 und DP_B2. Beide verfügen über eine gute Verbindung mit den Grenzspeicherorten der ersten Gruppe.
-   Konfigurieren Sie die zweite *benachbarte* Gruppe (BG_C), die nach 20 Minuten verwendet wird. Diese Gruppe enthält die Verteilungspunkte DP_C1 und DP_C2. Beide sind über ein WAN von den anderen Begrenzungsgruppen aus zugänglich.
-   Fügen Sie zudem einen weiteren Verteilungspunkt zur standardmäßigen Standortbegrenzungsgruppe der Standorte hinzu, der sich auf dem Standortserver befindet. Dieser Server ist der am wenigsten bevorzugte Quellspeicherort für Inhalt, der sich jedoch zu all Ihren Begrenzungsgruppen zentral befindet.

    Beispiel für Begrenzungsgruppen und Fallbackzeiten:

     ![Beispiel für Begrenzungsgruppen und Fallbackzeiten](media/BG_Fallback.png)


Mit dieser Konfiguration:
-   Der Client beginnt in seiner *aktuellen* Begrenzungsgruppe (BG_A) mit der Suche nach Inhalten über Verteilungspunkte. Er durchsucht die einzelnen Verteilungspunkte zwei Minuten lang und wechselt anschließend zum nächsten Verteilungspunkt in der Begrenzungsgruppe. Der Pool des Clients mit gültigen Quellspeicherorten für Inhalt umfasst DP_A1 und DP_A2.
-   Wenn der Client 10 Minuten lang keinen Inhalt aus der *aktuellen* Begrenzungsgruppe findet, fügt er die Verteilungspunkte aus der Begrenzungsgruppe BG_B zur Suche hinzu. Anschließend fährt er mit der Suche nach Inhalten über einen Verteilungspunkt in seinem kombinierten Serverpool fort. Dieser Pool enthält nun Server aus den Begrenzungsgruppen BG_A und BG_B. Der Client kontaktiert weiterhin zwei Minuten lang jeden Verteilungspunkt und wechselt anschließend zum nächsten Server in seinem Pool. Der Pool des Clients mit gültigen Quellspeicherorten für Inhalt umfasst DP_A1, DP_A2, DP_B1 und DP_B2.
-   Nach weiteren 10 Minuten (insgesamt 20 Minuten), in denen der Client immer noch keinen Verteilungspunkt mit Inhalt gefunden hat, erweitert er seinen Pool durch verfügbare Server aus der zweiten *benachbarten* Gruppe, der Begrenzungsgruppe BG_C. Der Client verfügt nun über sechs zu durchsuchende Verteilungspunkte (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 und DP_C2). Er wechselt weiterhin alle zwei Minuten zu einem neuen Verteilungspunkt, bis er Inhalt findet.
-   Wenn der Client nach maximal 120 Minuten keinen Inhalt gefunden hat, greift er darauf zurück, die *Standard-Standortbegrenzungsgruppe* als Teil der kontinuierlichen Suche einzuschließen. In den Pool werden nun alle Verteilungspunkte aus den drei konfigurierten Begrenzungsgruppen sowie der letzte Verteilungspunkt eingeschlossen, der sich auf dem Standortserver befindet. Der Client setzt die Suche nach Inhalt anschließend fort und wechselt alle zwei Minuten den Verteilungspunkt, bis er Inhalt gefunden hat.

Sie können steuern, wann bestimmte Verteilungspunkte als Quellspeicherorte für Inhalt hinzugefügt werden, indem Sie die unterschiedlichen benachbarten Gruppen so konfigurieren, dass sie zu unterschiedlichen Zeitpunkten verfügbar sind. Der Client verwendet das Fallback für die standardmäßige Standortbegrenzungsgruppe als Sicherheitsnetz für Inhalte, die an einem anderen Speicherort nicht verfügbar sind.





<!--
### Update existing boundary groups to the new model
When you update to version prior to 1610, the following configurations are automatically made. This behavior ensures your current fallback behavior remains available until you configure new boundary groups and relationships.

-   Each primary site creates a default site boundary group named ***Default-Site-Boundary-Group&lt;sitecode>***.
  - The primary site adds to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group any state migration points and distribution points configured to **Allow fallback source location for content**.
  - The site adds software update points to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group.
-   The site makes a copy of each existing boundary group that includes a site server configured with a slow connection. The name of the new group is ***&lt;original boundary group name>-&lt;original boundary group ID>***:  
    -   Site systems that have a fast connection are left in the original boundary group.
    -   A copy of site systems (distribution points, management points) that have a slow connection are added to the copy of the boundary group. The original site systems configured as slow remain in their original boundary groups for backward compatibility, but are not used from those boundary groups.
    - This boundary group copy does not have boundaries associated with it. However, A fallback link is created between the original group and the new boundary group copy that has the fallback time set to zero.  


- **Specific to secondary sites:**
  - If a secondary site has at least one state migration point or distribution point enabled to **Allow fallback source location for content**, Configuration Manager creates a boundary group named ***Secondary-Site-Neighbor--Tmp&lt;Sitecode>***. 
  - All distribution points enabled to **Allow fallback source location for content** and state migration points are added to this secondary site boundary group.
  - A fallback link is created between the original boundary group and the newly created neighbor boundary group. The fallback time is set to zero.


 The following table identifies the new fallback behavior you can expect from the combination the original deployment settings and distribution point configurations:

Original deployment configuration for “Do not run program” in slow network  |Original distribution point configuration for “Allow client to use a fallback source location for content”  |New fallback behavior  
---------|---------|---------
Selected     |  Selected    |  **No fallback** - Only use the distribution points in current boundary group       
Selected     |  Not selected|  **No fallback** - Only use the distribution points in current boundary group       
Not selected |  Not selected|  **Fallback to neighbor** - Use the distribution points in current boundary group, and then add the distribution points from the neighbor boundary group. Unless an explicit link to the default site boundary group is configured, clients do not fallback to that group.    
Not selected | Selected     |   **Normal fallback** - Use distribution points in current boundary group, then servers from the neighbor and site default boundary groups

 All other deployment configurations result in **Normal fallback**.  
-->



## <a name="changes-from-prior-versions"></a>Änderungen gegenüber früheren Versionen
Im Folgenden handelt es sich um wichtige Änderungen an Begrenzungsgruppen und der Vorgehensweise von Clients bei der Suche nach Inhalten in Configuration Manager (Current Branch). Viele dieser Änderungen und Konzepte arbeiten zusammen.


-   Konfigurationen für „schnell“ oder „langsam“ werden entfernt: Sie konfigurieren einzelne Verteilungspunkte nicht mehr so, dass diese schnell oder langsam sind. Stattdessen wird jedes Standortsystem, das einer Begrenzungsgruppe zugeordnet ist, auf die gleiche Weise behandelt. Aufgrund dieser Änderung unterstützt die Registerkarte **Referenz** der Begrenzungsgruppeneigenschaften die Konfiguration von „schnell“ und „langsam“ nicht mehr.
- Neue standardmäßige Begrenzungsgruppen an jedem Standort: Jeder primäre Standort verfügt über eine neue standardmäßige Begrenzungsgruppe mit dem Namen ***Default-Site-Boundary-Group&lt;sitecode>***. Wenn sich ein Client nicht an einer Netzwerkadresse befindet, die einer Begrenzungsgruppe zugewiesen wurde, verwendet er die Standortsysteme, die mit der Standardgruppe seines zugewiesenen Standorts verknüpft sind. Planen Sie, diese Begrenzungsgruppe als Ersatz für das Konzept der Fallbackinhaltsquelle zu verwenden.   
 -  **Allow fallback source locations for content** (Fallbackquellspeicherorte für Inhalt zulassen) wird entfernt: Sie konfigurieren nicht mehr explizit einen Verteilungspunkt, der für das Fallback verwendet wird. Die Optionen zum Konfigurieren dieser Einstellung werden von der Konsole entfernt.

    Darüber hinaus hat sich das Ergebnis geändert, das auftritt, wenn die Einstellung **Die Verwendung eines Fallbackquellpfads für den Inhalt durch Clients zulassen** auf einem Bereitstellungstyp für Anwendungen festgelegt wird. Diese Einstellung auf einem Bereitstellungstyp ermöglicht es einem Client nun, die Standard-Standortbegrenzungsgruppe als Quellspeicherort für Inhalt zu verwenden.

 -  Begrenzungsgruppenbeziehungen: Jede Begrenzungsgruppe kann mit mindestens einer zusätzlichen Begrenzungsgruppe verknüpft werden. Diese Links bilden Beziehungen, die auf der neuen Registerkarte der Begrenzungsgruppeneigenschaften mit dem Namen **Beziehungen** konfiguriert sind:
    -   Jede Begrenzungsgruppe, der ein Client direkt zugewiesen ist, wird **aktuelle** Begrenzungsgruppe genannt.  
    -   Jede Begrenzungsgruppe, die ein Client aufgrund einer Zuweisung zwischen der *aktuellen* Begrenzungsgruppe des Clients und einer anderen Gruppe verwenden kann, wird als **benachbarte** Begrenzungsgruppe bezeichnet.
    -  Fügen Sie auf der Registerkarte **Beziehungen** Begrenzungsgruppen hinzu, die als *benachbarte* Begrenzungsgruppe verwendet werden sollen. Außerdem sollten Sie eine Zeit in Minuten für das Fallback konfigurieren. Wenn ein Client keine Inhalte von einem Verteilungspunkt in der *aktuellen* Gruppe finden kann, beginnt er dieses Mal damit, Speicherorte für Inhalte von *benachbarten* Begrenzungsgruppen zu durchsuchen.

        Beim Hinzufügen oder Ändern einer Begrenzungsgruppenkonfiguration haben Sie die Möglichkeit, das Fallback auf diese bestimmte Begrenzungsgruppe von der aktuellen Gruppe zu blockieren, die Sie konfigurieren.

    Definieren Sie explizite Verknüpfungen (Links) zwischen den Begrenzungsgruppen, um die neue Konfiguration verwenden zu können. Konfigurieren Sie sämtliche Verteilungspunkte in dieser verknüpften Gruppe mit der gleichen Zeit in Minuten. Wenn ein Client keine Inhaltsquelle von seiner *aktuellen* Begrenzungsgruppe finden kann, bestimmt die von Ihnen konfigurierte Zeit, wann der Client damit beginnt, Inhaltsquellen von dieser benachbarten Begrenzungsgruppe zu suchen.

    Zusätzlich zu Begrenzungsgruppen, die Sie explizit konfigurieren, verfügt jede Begrenzungsgruppe über einen implizierten Link zur Standard-Standortbegrenzungsgruppe. Dieser Link wird nach 120 Minuten aktiv. Dann wird die standardmäßige Standortbegrenzungsgruppe zu einer benachbarten Begrenzungsgruppe. Durch dieses Verhalten können die Clients die Verteilungspunkte, die mit dieser Begrenzungsgruppe verknüpft sind, als Quellspeicherorte für Inhalt verwenden.

    Dieses Verhalten ersetzt, was zuvor als Fallback für den Inhalt bezeichnet wurde. Überschreiben Sie dieses Standardverhalten von 120 Minuten, indem Sie die standardmäßige Begrenzungsgruppe explizit mit einer *aktuellen* Gruppe verknüpfen. Legen Sie eine bestimmte Zeit in Minuten fest oder blockieren Sie das Fallback komplett, um eine Verwendung zu verhindern.


-   Clients versuchen bis zu zwei Minuten lang, Inhalte aus den einzelnen Verteilungspunkten zu erhalten: Wenn ein Client nach einem Quellspeicherort für Inhalt sucht, versucht er zwei Minuten lang auf jeden Verteilungspunkt zuzugreifen, bevor er anschließend einen anderen Verteilungspunkt austestet. Bei diesem Verhalten handelt es sich um eine Änderung gegenüber früheren Versionen, bei denen Clients bis zu zwei Stunden lang versucht haben, eine Verbindung zu einem Verteilungspunkt herzustellen.

    - Clients wählen den ersten Verteilungspunkt zufällig aus dem Pool verfügbarer Server in der *aktuellen* Begrenzungsgruppe (bzw. den aktuellen Begrenzungsgruppen) des Clients aus.

    - Wenn der Client den Inhalt nach zwei Minuten nicht gefunden hat, wechselt er zu einem neuen Verteilungspunkt und versucht, Inhalt von diesem Server zu erhalten. Dieser Vorgang wird alle zwei Minuten wiederholt, bis der Client den Inhalt findet oder den letzten Server im Pool erreicht.

    - Wenn ein Client in seinem *aktuellen* Pool keinen gültigen Quellspeicherort für Inhalt finden kann, bevor der Zeitraum für ein Fallback auf eine *benachbarte* Begrenzungsgruppe erreicht ist, fügt der Client die Verteilungspunkte aus dieser *benachbarten* Begrenzungsgruppe zum Ende seiner aktuellen Liste hinzu. Anschließend durchsucht er die erweiterte Gruppe des Quellpfades, welche die Verteilungspunkte aus beiden Begrenzungsgruppen enthält.

        > [!TIP]  
        > Wenn Sie einen expliziten Link von der aktuellen Begrenzungsgruppe zu der standardmäßigen Standortbegrenzungsgruppe erstellen und eine Fallbackzeit definieren, die kürzer ist als die Fallbackzeit für einen Link zu einer benachbarten Begrenzungsgruppe, beginnen Clients, Quellpfade aus der standardmäßigen Standortbegrenzungsgruppe zu durchsuchen, bevor sie die benachbarte Gruppe einschließen.

    - Wenn der Client vom letzten Server im Pool keinen Inhalt abrufen kann, beginnt er den Prozess erneut.


## <a name="procedures-for-boundary-groups"></a>Prozeduren für Begrenzungsgruppen

### <a name="to-create-a-boundary-group"></a>So erstellen Sie eine Begrenzungsgruppe  
1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Begrenzungsgruppe erstellen**.  

3.  Wählen Sie im Dialogfeld **Begrenzungsgruppe erstellen** die Registerkarte **Allgemein** aus, und geben Sie unter **Name** einen Namen für diese Begrenzungsgruppe an.  

4.  Klicken Sie auf **OK** , um die neue Begrenzungsgruppe zu speichern.  


### <a name="to-configure-a-boundary-group"></a>So konfigurieren Sie eine Begrenzungsgruppe  
 1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

 2.  Wählen Sie die Begrenzungsgruppe aus, die Sie ändern möchten.  

 3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

 4.  Wählen Sie im Dialogfeld **Eigenschaften** für die Begrenzungsgruppe die Registerkarte **Allgemein** aus, um die Grenzen zu ändern, die Mitglieder dieser Begrenzungsgruppe sind.  

     -   Wenn Sie Grenzen hinzufügen möchten, klicken Sie auf **Hinzufügen**, aktivieren Sie das Kontrollkästchen für eine oder mehrere Grenzen, und klicken Sie dann auf **OK**.  

     -   Wenn Sie Grenzen entfernen möchten, wählen Sie die Grenze aus, und klicken Sie auf **Entfernen**.  

 5.  Wählen Sie die Registerkarte **Referenzen** aus, um die Konfiguration für Standortzuweisung und zugeordnete Standortsystemserver zu ändern:  

     -   Wählen Sie zum Aktivieren dieser Begrenzungsgruppe für die Verwendung durch Clients für die Standortzuweisung die Option **Use this boundary group for site assignment** (Diese Begrenzungsgruppe für die Standortzuweisung verwenden) aus. Wählen Sie anschließend aus der Dropdownliste **Zugewiesener Standort** einen Standort aus.  

     -   Um zu konfigurieren, welche verfügbaren Standortsystemserver dieser Begrenzungsgruppe zugeordnet sind, gehen Sie wie folgt vor:  

     1.  Klicken Sie auf **Hinzufügen**, und aktivieren Sie dann das Kontrollkästchen für einen oder mehrere Server. Die Server werden als zugeordnete Standortsystemserver für diese Begrenzungsgruppe hinzugefügt. Nur Server, auf denen die unterstützte Standortsystemrolle installiert ist, sind verfügbar.  

         > [!NOTE]  
         >  Sie können eine beliebige Kombination verfügbarer Standortsysteme von einem beliebigen Standort in der Hierarchie auswählen. Ausgewählte Standortsysteme werden in den Eigenschaften jeder Grenze, die dieser Begrenzungsgruppe angehört, auf der Registerkarte **Standortsysteme** aufgelistet.  

     2.  Wenn Sie einen Server aus dieser Begrenzungsgruppe entfernen möchten, wählen Sie den Server aus, und klicken Sie dann auf **Entfernen**.  

         > [!NOTE]  
         >  Wenn diese Begrenzungsgruppe nicht mehr zum Zuordnen von Standortsystemen verwendet werden soll, müssen Sie alle Server entfernen, die als zugeordnete Standortsystemserver aufgelistet sind.  

 6.  Wählen Sie die Registerkarte **Beziehungen** aus, um das Fallbackverhalten zu konfigurieren:  

     - Klicken Sie auf **Hinzufügen**, und wählen Sie anschließend die Begrenzungsgruppe aus, die Sie konfigurieren möchten.

     - Legen Sie eine Fallbackzeit für Verteilungspunkte fest. Nach dieser Zeitspanne können Clients in der Begrenzungsgruppe, für die Sie die Beziehungen konfigurieren, die Suche nach Inhalten aus den Verteilungspunkten der von Ihnen hinzugefügten Begrenzungsgruppe starten.

     - Wählen Sie zur Verhinderung eines Fallbacks auf eine bestimmte Begrenzungsgruppe die *standardmäßige Standortbegrenzungsgruppe* inbegriffen, die standardmäßig konfiguriert ist, die Begrenzungsgruppe aus, und aktivieren Sie anschließend das Kontrollkästchen **Never Fallback** (Kein Fallback).   

 7.  Klicken Sie auf **OK** , um die Eigenschaften der Begrenzungsgruppe zu schließen und die Konfiguration zu speichern.  

#### <a name="to-associate-a-site-system-server-with-a-boundary-group"></a>So ordnen Sie einer Begrenzungsgruppe Standortsystemserver zu  
 1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

 2.  Wählen Sie die Begrenzungsgruppe aus, die Sie ändern möchten.  

 3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

 4.  Wählen Sie im Dialogfeld **Eigenschaften** für die Begrenzungsgruppe die Registerkarte **Referenzen** aus.  

 5.  Klicken Sie unter **Standortsystemserver auswählen** auf **Hinzufügen**. Wählen Sie die Standortsystemserver aus, die dieser Begrenzungsgruppe zugeordnet werden sollen, und klicken Sie anschließend auf **OK**.  

 6.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen und die Konfiguration der Begrenzungsgruppe zu speichern.  


#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>So konfigurieren Sie einen Fallbackstandort für die automatische Standortzuweisung  

  1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Standortkonfiguration** >  **Standorte**.  

  2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.  

  3.  Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen **Fallbackstandort verwenden**, und wählen Sie dann in der Dropdownliste **Fallbackstandort** einen Standort aus.  

  4.  Klicken Sie auf **OK** , um die Konfiguration zu speichern.  

#### <a name="to-enable-use-of-preferred-management-points"></a>So aktivieren Sie die Verwendung bevorzugter Verwaltungspunkte  

 1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Standortkonfiguration** > **Standorte**, und wählen Sie anschließend **Hierarchieeinstellungen**auf der Registerkarte **Start** aus.  

 2.  Wählen Sie im Dialogfeld „Hierarchieeinstellungen“ auf der Registerkarte **Allgemein** die Option **Clients bevorzugen die in Begrenzungsgruppen angegebenen Verwaltungspunkte**.  

 3.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen und die Konfiguration zu speichern.  
