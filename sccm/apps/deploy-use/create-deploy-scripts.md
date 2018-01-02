---
title: "Erstellen und Ausführen von Skripts"
titleSuffix: Configuration Manager
description: "Erfahren Sie, wie PowerShell-Skripts erstellt und auf Clientgeräten ausgeführt werden."
ms.custom: na
ms.date: 11/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: BrucePerlerMS
ms.author: bruceper
manager: angrobe
ms.openlocfilehash: 1472f697ae8b82e6268433aa6398fcc10a429994
ms.sourcegitcommit: 5f4a584d4a833b0cc22bd8c47da7dd55aced97fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole

*Gilt für: System Center Configuration Manager (Current Branch)*

>[!TIP]
>Die bei Version 1706 eingeführte Option zum Ausführen von PowerShell-Skripts ist ein Vorabfeature. Informationen zum Aktivieren von Skripts finden Sie unter [Features der Vorabversion in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

Wir haben nun die Möglichkeit zum Ausführen von PowerShell-Skripts besser in System Center Configuration Manager integriert. PowerShell bietet den Vorteil der Erstellung ausgeklügelter, automatisierter Skripts, die von einer größeren Community verstanden und geteilt werden. Die Skripts vereinfachen die Erstellung benutzerdefinierter Tools zur Verwaltung von Software und ermöglichen Ihnen, alltägliche Aufgaben schnell zu erledigen, sodass Sie große Aufträge einfacher und konsistenter bewältigen können.

Durch diese Integration in System Center Configuration Manager können Sie die Funktion *Skripts ausführen* verwenden, um Folgendes zu tun:

- Erstellen und Bearbeiten von Skripts für die Verwendung mit System Center Configuration Manager
- Verwalten der Skriptnutzung mithilfe von Rollen und Sicherheitsbereichen 
- Anwenden von Skripts auf Sammlungen einzelner lokal verwalteter Windows-PCs
- Abrufen schnell aggregierter Skriptergebnisse von Clientgeräten
- Überwachen der Skriptausführung und Anzeigen von Berichtsergebnissen in der Skriptausgabe

>[!WARNING]
>Angesichts der Leistungsfähigkeit von Skripts möchten wir Sie daran erinnern, diese bewusst und sorgfältig einzusetzen. Wir haben zusätzliche Sicherheitsvorkehrungen eingebaut, um Sie zu unterstützen: getrennte Rollen und Bereiche. Stellen Sie die Fehlerfreiheit von Skripts sicher, bevor Sie sie ausführen. Bestätigen Sie außerdem, dass sie aus einer vertrauenswürdigen Quelle stammen, um eine unbeabsichtigte Ausführung von Skripts zu verhindern. Achten Sie auf Sonderzeichen oder sonstige Obfuskation, und informieren Sie sich über die Absicherung von Skripts.

## <a name="prerequisites"></a>Voraussetzungen

- Um PowerShell-Skripts ausführen zu können, muss auf dem Client PowerShell 3.0 installiert sein. Wenn ein Skript jedoch Funktionen aus einer neueren PowerShell-Version enthält, muss diese auch auf dem Client installiert sein, der diese Version von PowerShell ausführt.
- Das Ausführen von Skripts ist nur auf Clients mit Configuration Manager 1706 oder neuer möglich.
- Um Skripts zu verwenden, müssen Sie Mitglied der entsprechenden Configuration Manager-Sicherheitsrolle sein.
- Importieren und Erstellen von Skripts: Ihr Konto benötigt in der Sicherheitsrolle **Hauptadministrator** die Berechtigung **Erstellen** für **SMS-Skripts**.
- Genehmigen und Ablehnen von Skripts: Ihr Konto benötigt in der Sicherheitsrolle **Hauptadministrator** die Berechtigung **Genehmigen** für **SMS-Skripts**.
- Ausführen von Skripts: Ihr Konto benötigt in der Sicherheitsrolle **Hauptadministrator** die Berechtigung **Skript ausführen** für **Sammlungen**.

Weitere Informationen zu Configuration Manager-Sicherheitsrollen finden Sie unter [Grundlagen der rollenbasierten Verwaltung für System Center Configuration Manager](/sccm/core/understand/fundamentals-of-role-based-administration).

## <a name="limitations"></a>Einschränkungen

Von der Funktion „Skripts ausführen“ wird derzeit Folgendes unterstützt:

- Skriptsprachen: PowerShell
- Parametertypen: „integer“, „string“ und „list“

## <a name="run-script-authors-and-approvers"></a>Skript ausführen: Ersteller und Genehmiger

Die Funktion „Skripts ausführen“ arbeitet für die Implementierung und Ausführung eines Skripts mit dem Konzept von *Skriptautoren* und *Skriptgenehmigern* als getrennte Rollen. Die Trennung von Autor- und Genehmigerrolle ermöglicht eine wichtige Prozessüberprüfung für das überaus leistungsstarke Tool „Skripts ausführen“.

### <a name="scripts-roles-control"></a>Steuerung von Skriptrollen

Standardmäßig können Benutzer kein Skript genehmigen, das sie erstellt haben. Da Skripts leistungsstark und vielseitig sind und auf vielen Geräten bereitgestellt werden können, muss ein von einer Person erstelltes Skript von einer anderen Person genehmigt werden. Dies bietet Ihnen zusätzliche Sicherheit vor der unbeaufsichtigten Ausführung eines Skripts. Die sekundäre Genehmigung lässt sich deaktivieren, um das Testen zu vereinfachen.

### <a name="approve-or-deny-a-script"></a>Genehmigen oder Ablehnen eines Skripts

Skripts müssen von der Rolle *Skriptgenehmiger* genehmigt werden, bevor sie ausgeführt werden dürfen. So genehmigen Sie ein Skript

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.
2. Klicken Sie im Arbeitsbereich **Softwarebibliothek** auf **Skripts**.
3. Wählen Sie in der Liste **Skript** das Skript, das Sie genehmigen oder ablehnen möchten. Klicken Sie dann in der Gruppe **Skript** auf der Registerkarte **Start** auf **Genehmigen/Ablehnen**.
4. Wählen Sie im Dialogfeld **Skript genehmigen oder ablehnen** für das Skript entweder **Genehmigen** oder **Ablehnen** aus, und geben Sie optional einen Kommentar zu Ihrer Entscheidung ein.  Wenn Sie ein Skript ablehnen, kann es nicht auf Clientgeräten ausgeführt werden. <br>
![Skript: Genehmigung](./media/run-scripts/RS-approval.png)
5. Schließen Sie den Assistenten ab. In der Liste **Skript** ändert sich die Spalte **Genehmigungsstatus** abhängig von der Aktion, die Sie ausgeführt haben.

### <a name="allow-users-to-approve-their-own-scripts"></a>Benutzern erlauben, eigene Skripts zu genehmigen

Diese Genehmigung erfolgt in erster Linie in der Testphase der Skriptentwicklung.

1. Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.
2. Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.
3. Wählen Sie in der Liste der Standorte Ihren Standort aus, und klicken Sie dann auf der Registerkarte **Start** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.
4. Deaktivieren Sie im Dialogfeld **Eigenschaften von Hierarchieeinstellungen** auf der Registerkarte **Allgemein** das Kontrollkästchen **Skriptautoren nicht das Genehmigen ihrer eigenen Skripts erlauben**.

>[!IMPORTANT]
>Als bewährte Methode sollten Sie nicht zulassen, dass Skriptautoren ihre eigenen Skripts genehmigen können. Dies sollte nur in einer Testumgebung gestattet sein. Bedenken Sie die möglichen Auswirkungen, die eine Änderung dieser Einstellung in einer Produktionsumgebung mit sich bringt.

## <a name="security-scopes"></a>Sicherheitsbereichen
*(Mit Version 1710 eingeführt)*  
Die Funktion „Skripts ausführen“ arbeitet mit Sicherheitsbereichen, einer bereits vorhandenen Configuration Manager-Funktion, um die Erstellung und Ausführung von Skripts zu steuern, indem Kategorien zugewiesen werden, die Benutzergruppen darstellen. Weitere Informationen zu Sicherheitsbereichen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung für System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="create-a-script"></a>Erstellen eines Skripts

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.
2. Klicken Sie im Arbeitsbereich **Softwarebibliothek** auf **Skripts**.
3. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Skript erstellen**.
4. Konfigurieren Sie im Assistenten **Skript erstellen** auf der Seite **Skript** die folgenden Einstellungen:
    - **Skriptname**: Geben Sie einen Namen für das Skript ein. Sie können zwar mehrere Skripts mit dem gleichen Namen erstellen, dies erschwert aber das Auffinden des benötigten Skripts in der Configuration Manager-Konsole.
    - **Skriptsprache**: Derzeit werden nur PowerShell-Skripts unterstützt.
    - **Importieren**: Importieren Sie ein PowerShell-Skript in die Konsole. Das Skript wird im Feld **Skript** angezeigt.
    - **Löschen**: Entfernt das aktuelle Skript aus dem Feld „Skript“
    - **Skript**: Zeigt das gerade importierte Skript. Sie können das Skript in diesem Feld nach Bedarf bearbeiten.
1. Schließen Sie den Assistenten ab. Das neue Skript wird in der Liste **Skript** mit dem Status **Warten auf Genehmigung** angezeigt. Bevor Sie dieses Skript auf Clientgeräten ausführen können, müssen Sie es genehmigen.

## <a name="script-parameters"></a>Skriptparameter
*(Mit Version 1710 eingeführt)*  
Durch Hinzufügen von Parametern zu einem Skript können Sie Ihre Arbeit flexibler gestalten. Im Folgenden wird die aktuelle Fähigkeit der Funktion „Skripts ausführen“ mit Skriptparametern für die Datentypen *String* und *Integer* dargelegt. Listen mit vordefinierten Werten sind ebenfalls verfügbar. Wenn das Skript nicht unterstützte Datentypen aufweist, erhalten Sie eine Warnung.

Klicken Sie im Dialogfeld **Skript erstellen** unter **Skript** auf **Skriptparameter**.

Jeder Parameter Ihres Skripts hat ein eigenes Dialogfeld, in dem Sie weitere Details und eine Validierung hinzufügen können.

### <a name="parameter-validation"></a>Validierung von Parametern

Für jeden Parameter in Ihrem Skript gibt es das Dialogfeld **Skriptparameter – Eigenschaften**, in dem Sie eine Validierung für den jeweiligen Parameter hinzufügen können. Nach dem Hinzufügen der Validierung sollten Sie Fehlermeldungen erhalten, wenn Sie einen Wert für einen Parameter eingeben, der nicht dessen Validierung entspricht.

#### <a name="example-firstname"></a>Beispiel: *FirstName*

In diesem Beispiel können Sie die Eigenschaften des Zeichenfolgenparameters *FirstName* festlegen.

![Skriptparameter: String](./media/run-scripts/RS-parameters-string.png)


Der Abschnitt „Überprüfung“ des Dialogfelds **Skriptparametereigenschaften** enthält die folgenden Felder, die Sie verwenden können:

- **Mindestlänge**: Minimale Anzahl von Zeichen im Feld *FirstName*.
- **Maximale Länge**: Maximale Anzahl von Zeichen im Feld *FirstName*.
- **RegEx**: Kofferwort für *Regular Expression*, d.h. regulärer Ausdruck. Weitere Informationen zur Verwendung von regulären Ausdrücken finden Sie im nächsten Abschnitt *Durchführen der Überprüfung von regulären Ausdrücken*.
- **Benutzerdef. Fehler**: Nützlich zum Hinzufügen einer eigenen benutzerdefinierten Fehlermeldung, die alle Fehlermeldungen im Rahmen der Systemüberprüfung ersetzt.

#### <a name="using-regular-expression-validation"></a>Durchführen der Überprüfung von regulären Ausdrücken

Ein regulärer Ausdruck stellt eine kompakte Programmiermethode dar, um eine Zeichenfolge anhand einer codierten Überprüfung zu überprüfen. Sie können z.B. im Feld *FirstName* nach einem fehlenden Großbuchstaben suchen, indem Sie `[^A-Z]` in das Feld *RegEx* eingeben.

Die Verarbeitung regulärer Ausdrücke für dieses Dialogfeld wird vom .NET Framework unterstützt. Hinweise zur Verwendung von regulären Ausdrücken finden Sie unter [Reguläre Ausdrücke von .NET](https://docs.microsoft.com/dotnet/standard/base-types/regular-expressions). 


## <a name="script-examples"></a>Beispiele für Skripts

Hier finden Sie einige Beispiele, die Skripts veranschaulichen, die sich mit dieser Funktion verwenden lassen.

### <a name="create-a-new-folder-and-file"></a>Erstellen eines neuen Ordners und einer neuen Datei

Dieses Skript erstellt basierend auf Ihrer Namenseingabe einen neuen Ordner und eine Datei in diesem Ordner.

``` powershell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName,
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Abrufen der Betriebssystemversion

Dieses Skript verwendet WMI, um die Betriebssystemversion des Computers abzufragen.

``` powershell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="run-a-script"></a>Ausführen eines Skripts

Nachdem ein Skript genehmigt wurde, kann es für ein einzelnes Gerät oder eine Sammlung ausgeführt werden. Sobald die Ausführung Ihres Skripts beginnt, wird es schnell in einem System mit hoher Priorität gestartet, bei dem binnen einer Stunde ein Timeout auftritt. Die Ergebnisse des Skripts werden dann über ein Zustandsmeldungssystem zurückgegeben.

So wählen Sie eine Sammlung von Zielen für Ihr Skript aus

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.
2. Klicken Sie im Arbeitsbereich Bestand und Kompatibilität auf **Gerätesammlungen**.
3. Klicken Sie in der Liste **Gerätesammlungen** auf die Sammlung von Geräten, auf denen das Skript ausgeführt werden soll.
4. Wählen Sie eine Sammlung Ihrer Wahl aus, und klicken Sie auf **Skript ausführen**.
5. Wählen Sie im Assistenten **Skript ausführen** auf der Seite **Skript** ein Skript in der Liste aus. Es werden nur genehmigte Skripts angezeigt.
6. Klicken Sie auf **Weiter**, und schließen Sie den Assistenten ab.

>[!IMPORTANT]
>Wenn ein Skript nicht ausgeführt wird, weil ein Zielgerät beispielsweise während des einstündigen Zeitraums ausgeschaltet ist, müssen Sie es erneut ausführen.

### <a name="target-machine-execution"></a>Ausführung auf dem Zielcomputer

Das Skript wird mit dem Konto *System* oder *Computer* auf den entsprechenden Zielclients ausgeführt. Dieses Konto hat begrenzten Netzwerkzugriff. Jeder Zugriff auf Remotesysteme und -standorte durch das Skript muss entsprechend eingerichtet werden.

## <a name="script-monitoring"></a>Skriptüberwachung

Nachdem Sie mit der Anwendung eines Skripts auf eine Sammlung von Geräten begonnen haben, gehen Sie wie folgt vor, um den Vorgang zu überwachen. Ab Version 1710 können Sie ein Skript in Echtzeit überwachen, während es ausgeführt wird, und Sie können auch zu einem Bericht für eine bestimmte Ausführung von „Skript ausführen“ zurückkehren. <br>

![Skriptüberwachung: Status der Skriptausführung](./media/run-scripts/RS-monitoring-three-bar.png)

1. Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.
2. Klicken Sie im Arbeitsbereich **Überwachung** auf **Skriptstatus**.
3. In der Liste **Skriptstatus** sehen Sie die Ergebnisse für jedes Skript, das Sie auf Clientgeräten ausgeführt haben. Der Exitcode **0** eines Skripts bedeutet im Allgemeinen, dass das Skript erfolgreich ausgeführt wurde.

## <a name="see-also"></a>Siehe auch

- [Konfigurieren der rollenbasierten Verwaltung für System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Grundlagen der rollenbasierten Verwaltung](/sccm/core/understand/fundamentals-of-role-based-administration)
