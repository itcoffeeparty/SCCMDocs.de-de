---
title: "Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät | System Center Configuration Manager"
description: "Verknüpfen Sie Benutzer und Geräte mit Affinität zwischen Benutzer und Gerät, und stellen Sie Apps automatisch auf Geräten bereit, die einem Benutzer zugeordnet sind."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bb918eb5f7a69cad47de761a3e95e92926524e3a


---
# <a name="link-users-and-devices-with-user-device-affinity-in-system-center-configuration-manager"></a>Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Durch die Affinität zwischen Benutzer und Gerät in System Center Configuration Manager wird ein Benutzer einem oder mehreren Geräten zugeordnet. Dadurch ist es zum Bereitstellen einer Anwendung für den Benutzer nicht erforderlich, die Namen seiner Geräte zu kennen. Anstatt die Anwendung für jedes einzelne Gerät eines Benutzers bereitzustellen, stellen Sie sie für den Benutzer bereit. Mithilfe der Affinität zwischen Benutzer und Gerät wird dann automatisch sichergestellt, dass die Anwendung auf allen Geräten installiert wird, die dem Benutzer zugeordnet sind.  

 Sie können primäre Geräte definieren, wobei es sich in der Regel um solche Geräte handelt, die Benutzer täglich für die Ausführung ihrer Arbeit verwenden. Durch das Erstellen einer Affinität zwischen einem Benutzer und einem Gerät bieten sich zusätzliche Optionen für die Bereitstellung von Apps. Wenn ein Benutzer beispielsweise Microsoft Office Visio benötigt, können Sie es mithilfe einer Windows Installer-Bereitstellung auf dem primären Gerät des Benutzers installieren. Auf Geräten, bei denen es sich nicht um ein primäres Gerät handelt, können Sie Microsoft Office Visio dagegen als virtuelle Anwendung bereitstellen. Sie können mithilfe der Affinität zwischen Benutzer und Gerät Software auf dem Gerät eines Benutzers auch vorab bereitstellen, während der Benutzer nicht angemeldet ist. Wenn sich der Benutzer dann anmeldet, ist die Anwendung bereits installiert und betriebsbereit.  

 Sie müssen die Informationen zur Affinität zwischen Benutzer und Gerät für Computer verwalten. Affinitäten zwischen Benutzer und Gerät werden von Configuration Manager für die registrierten mobilen Geräte automatisch verwaltet.  

## <a name="manually-configure-user-device-affinity"></a>Manuelles Konfigurieren der Affinität zwischen Benutzer und Gerät  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Geräte**.  

3.  Wählen Sie in der Liste ein Gerät aus. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Gerät** dann auf **Primäre Benutzer bearbeiten**.  

4.  Wählen Sie im Dialogfeld **Primäre Benutzer bearbeiten** die Benutzer aus, die dem ausgewählten Gerät als primäre Benutzer hinzugefügt werden sollen, und klicken Sie dann auf **Hinzufügen**.  

    > [!NOTE]  
    >  In der Liste **Primäre Benutzer** sind Benutzer, die bereits primäre Benutzer dieses Geräts sind, mit der jeweils zum Zuweisen der Beziehung zwischen Benutzer und Gerät verwendeten Methode aufgelistet.  

## <a name="configure-primary-devices-for-a-user"></a>Konfigurieren primärer Geräte für einen Benutzer  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Benutzer**.  

3.  Wählen Sie in der Liste einen Benutzer aus. Klicken Sie auf der Registerkarte **Gerät** dann auf **Primäre Geräte bearbeiten**.  

4.  Wählen Sie im Dialogfeld **Primäre Geräte bearbeiten** die Geräte aus, die dem ausgewählten Benutzer als primäre Geräte hinzugefügt werden sollen, und klicken Sie dann auf **Hinzufügen**.  

    > [!NOTE]  
    >  In der Liste **Primäre Geräte** sind Geräte, die bereits als primäre Geräte für diesen Benutzer konfiguriert sind, mit der jeweils zum Zuweisen der Beziehung zwischen Benutzer und Gerät verwendeten Methode aufgelistet.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Automatisches Erstellen von Affinitäten zwischen Benutzern und Geräten (nur Windows-PCs)  
 Von Configuration Manager werden Daten zu Benutzeranmeldungen aus dem Windows-Ereignisprotokoll ausgelesen. Zum Nutzen der automatischen Erstellung von Affinitäten zwischen Benutzer und Gerät müssen Sie die folgenden beiden Einstellungen aus der lokalen Sicherheitsrichtlinie auf Clientcomputern aktivieren, damit Anmeldeereignisse im Windows-Ereignisprotokoll gespeichert werden.  

-   **Anmeldeversuche überwachen**  

-   **Anmeldeereignisse überwachen**  

 Sie können diese Einstellungen mithilfe von Windows-Gruppenrichtlinien konfigurieren.  

> [!IMPORTANT]  
>  Wenn ein Fehler bewirkt, dass im Windows-Ereignisprotokoll eine große Zahl von Einträgen generiert wird, kann dies dazu führen, dass ein neues Ereignisprotokoll erstellt wird. In diesem Fall sind vorhandene Anmeldeereignisse für Configuration Manager möglicherweise nicht mehr verfügbar.  
>   
>  Gehen Sie beim Implementieren der Überwachung von ** ** Anmeldeversuchen und Anmeldeereignissen ** ** in Windows XP vorsichtig vor. Standardmäßig ist die Beibehaltungsrichtlinie auf sieben Tage festgelegt, und es ist äußerst wahrscheinlich, dass die betreffenden Ereignisse das Sicherheitsereignisprotokoll innerhalb dieses Zeitraums füllen. Standardbenutzer können sich nicht mehr anmelden, wenn das Ereignisprotokoll voll ist. Um dieses Problem zu verhindern, sollten Sie auch die Richtlinie **Aufbewahrungsmethode** für das Sicherheitsprotokoll auf **Ereignisse bei Bedarf überschreiben**festlegen. Sollen ausreichend Daten für die Affinität zwischen Benutzer und Gerät zur Verfügung stehen, legen Sie die Richtlinie „Maximale Größe des Sicherheitsprotokolls“ auf einen Wert wie 5 bis 20 MB fest.  

### <a name="configure-the-site-to-automatically-create-user-device-affinities"></a>Konfigurieren des Standorts für das automatische Erstellen von Affinitäten zwischen Benutzer und Gerät  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Clienteinstellungen**.  

3.  Zum Ändern der Clientstandardeinstellungen wählen Sie **Clientstandardeinstellungen**, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**. Zum Erstellen von benutzerdefinierten Client-Agent-Einstellungen wählen Sie den Knoten **Clienteinstellungen** aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Benutzerdefinierte Geräteclienteinstellungen erstellen**.  

    > [!NOTE]  
    >  Wenn Sie die Clientstandardeinstellungen ändern, werden sie auf allen Computern in der Hierarchie bereitgestellt. Weitere Informationen zum Konfigurieren von Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

4.  Konfigurieren Sie Folgendes für die Clienteinstellung **Affinität zwischen Benutzer und Gerät**:  

    -   **Nutzungsschwellenwert (Minuten) für Affinität zwischen Benutzer und Gerät** : Geben Sie die Nutzungsdauer in Minuten an, nach der eine Affinität zwischen Benutzer und Gerät erstellt wird.  

    -   **Nutzungsschwellenwert (Tage) für Affinität zwischen Benutzer und Gerät** : Geben Sie die Anzahl von Tagen an, über die der Nutzungsschwellenwert für die Affinität zwischen Benutzer und Gerät gemessen wird.  

    -   **Affinität zwischen Benutzer und Gerät automatisch aus Verwendungsdaten konfigurieren** : Wählen Sie in der Dropdownliste den Wert **Wahr** aus, um das automatische Erstellen von Affinitäten zwischen Benutzern und Geräten für den Standort zu aktivieren. Wenn Sie **Falsch**auswählen, müssen Sie alle Zuweisungen der Affinität zwischen Benutzer und Gerät genehmigen.  

    > [!TIP]  
    >  **Beispiel** : Wenn für **Nutzungsschwellenwert (Minuten) für Affinität zwischen Benutzer und Gerät** ein Wert von **60** Minuten und für **Nutzungsschwellenwert (Tage) für Affinität zwischen Benutzer und Gerät** ein Wert von **5** Tagen angegeben ist, muss der Benutzer das Gerät über einen Zeitraum von fünf Tagen insgesamt mindestens 60 Minuten lang nutzen, damit eine Affinität zwischen Benutzer und Gerät automatisch erstellt wird.  
   
Nachdem eine Affinität zwischen Benutzer und Gerät automatisch erstellt wurde, werden die Schwellenwerte für die Affinität zwischen Benutzer und Gerät weiterhin von Configuration Manager überwacht. Wenn die Aktivität des Benutzers auf dem Gerät die konfigurierten Schwellenwerte unterschreitet, wird die Affinität zwischen Benutzer und Gerät entfernt. Konfigurieren Sie für **Nutzungsschwellenwert (Tage) für Affinität zwischen Benutzer und Gerät** einen Wert von mindestens **7** Tagen, um zu verhindern, dass eine automatisch konfigurierte Affinität zwischen Benutzer und Gerät verlorengeht, wenn der Benutzer sich über einen längeren Zeitraum (z. B. während des Wochenendes) nicht anmeldet.  

## <a name="import-user-device-affinities-from-a-file"></a>Importieren von Affinitäten zwischen Benutzer und Gerät aus einer Datei  
 Sie können eine Datei importieren, die Affinitäten zwischen Benutzern und Geräten enthält, um viele Beziehungen gleichzeitig zu erstellen. Für dieses Verfahren müssen die entsprechenden Geräte bereits ermittelt worden und in der Configuration Manager-Datenbank als Ressourcen vorhanden sein, da andernfalls ein Fehler auftritt.  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Benutzer** oder **Geräte**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Affinität zwischen Benutzer und Gerät importieren**.  

4.  Geben Sie im ** ** Assistenten zum Importieren von Affinität zwischen Benutzer und Gerät auf der Seite **Zuordnung wählen**die folgenden Informationen an:  

    -   **Dateiname** : Geben Sie eine CSV-Datei (kommagetrennte Werte) an, die eine Liste mit Benutzern und Geräten enthält, zwischen denen eine Affinität erstellt werden soll. In der Datei muss jedes Paar aus Benutzer und Gerät in einer separaten Zeile stehen und durch ein Komma getrennt sein. Verwenden Sie folgendes Format: *<Domäne\>\\<Benutzername\>*, *<NetBIOS-Name des Geräts>\>*.  

    -   **Diese Datei enthält zu Referenzzwecken Spaltenüberschriften** : Wenn die CSV-Datei (kommagetrennte Werte) eine Zeile mit einer Überschrift enthält, wählen Sie diese Option aus, damit die Kopfzeile beim Importieren ignoriert wird.  

5.  Wenn die zu importierende Datei mehr als zwei Elemente pro Zeile enthält, können Sie mithilfe der Optionen **Spalte** und **Zuweisen** angeben, welche Spalten Benutzer und Geräte enthalten und welche Spalten beim Importieren ignoriert werden sollen.  

6.  Klicken Sie auf **Weiter** , und schließen Sie dann den ** **Assistenten zum Importieren von Affinität zwischen Benutzer und Gerät ab.  

## <a name="let-end-users-create-a-user-device-affinity"></a>Benutzern gestatten, eine Affinität zwischen Benutzer und Gerät zu erstellen  
 Verwenden Sie diese Verfahren, um Benutzern das Erstellen eigener Affinitäten zwischen Benutzer und Gerät über das Softwarecenter zu ermöglichen.  

### <a name="configure-the-site-to-allow-user-created-user-device-affinity-requests"></a>Konfigurieren des Standorts, um von Benutzern erstellte Affinitätsanforderungen zwischen Benutzer und Gerät zu gestatten  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Clienteinstellungen**.  

3.  Zum Ändern der Clientstandardeinstellungen wählen Sie **Clientstandardeinstellungen**, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**. Zum Erstellen von benutzerdefinierten Client-Agent-Einstellungen wählen Sie den Knoten **Clienteinstellungen** aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Benutzerdefinierte Benutzerclienteinstellungen erstellen**.  

    > [!NOTE]  
    >  Wenn Sie die Clientstandardeinstellungen ändern, werden sie auf allen Computern in der Hierarchie bereitgestellt. Informationen zum Konfigurieren der Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

4.  Wählen Sie die Clienteinstellung **Affinität zwischen Benutzer und Gerät** und dann aus der Dropdownliste **Benutzer das Festlegen primärer Geräte gestatten** den Wert **True**aus.  

### <a name="configure-a-user-device-affinity"></a>Konfigurieren einer Affinität zwischen Benutzer und Gerät  

1.  Klicken Sie im Anwendungskatalog auf **Eigene Systeme**.  

2.  Aktivieren Sie die Option **Ich nutze diesen Computer regelmäßig für meine Arbeit**.  

## <a name="manage-user-device-affinity-requests-from-users"></a>Verwalten von Affinitätsanforderungen zwischen Benutzer und Gerät  
 Wenn die Clienteinstellung **Affinität zwischen Benutzer und Gerät automatisch aus Verwendungsdaten konfigurieren** auf den Wert **Falsch**festgelegt ist, müssen Sie alle Affinitätszuweisungen zwischen Benutzern und Geräten genehmigen.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Genehmigen oder Ablehnen einer Affinitätsanforderung zwischen Benutzer und Gerät  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Wählen Sie im Arbeitsbereich **Bestand und Kompatibilität** die Benutzer- oder Gerätesammlung aus, für die Sie Affinitätsanforderungen verwalten möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Sammlung** auf **Affinitätsanforderungen verwalten**.  

4.  Wählen Sie im Dialogfeld **Affinitätsanforderungen zwischen Benutzer und Gerät verwalten** eine Affinitätsanforderungen aus, und klicken Sie dann auf **Genehmigen** oder **Ablehnen**.  



<!--HONumber=Nov16_HO1-->


