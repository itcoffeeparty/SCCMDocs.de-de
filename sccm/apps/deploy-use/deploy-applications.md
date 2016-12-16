---
title: Bereitstellen von Anwendungen | System Center Configuration Manager
description: "Erstellen Sie einen Bereitstellungstyp, oder simulieren Sie die Bereitstellung für eine Anwendung mithilfe von System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e608bcbadc82487018bb29c5e05660275d8fa275


---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Bereitstellen von Anwendungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*



 Bevor Sie eine System Center Configuration Manager-Anwendung bereitstellen können, müssen Sie mindestens einen Bereitstellungstyp für die Anwendung erstellen. Weitere Informationen zum Erstellen von Anwendungen und Bereitstellungstypen finden Sie unter [Create applications (Erstellen von Anwendungen)](../../apps/deploy-use/create-applications.md).  

> [!IMPORTANT]  
>  Sie können erforderliche Anwendungen bereitstellen (installieren/deinstallieren), jedoch keine Pakete oder Softwareupdates. Auch simulierte Bereitstellungen werden für mobile Geräte nicht unterstützt.  
>   
>  Einstellungen für Benutzerfreundlichkeit und Zeitplanung im Assistenten zum Bereitstellen von Software werden für mobile Geräte ebenfalls nicht unterstützt.  

 Sie können eine Anwendungsbereitstellung auch simulieren. Bei dieser Art der Bereitstellung wird die Anwendbarkeit einer Anwendungsbereitstellung auf Computern getestet, ohne die Anwendung zu installieren oder zu deinstallieren. Bei einer simulierten Bereitstellung werden Erkennungsmethode, Anforderungen und Abhängigkeiten für einen Bereitstellungstyp ausgewertet. Anschließend wird ein Bericht mit den Ergebnissen im Arbeitsbereich **Überwachung** unter dem Knoten **Bereitstellungen** ausgegeben. Weitere Informationen finden Sie unter [Simulieren von Anwendungsbereitstellungen](../../apps/deploy-use/simulate-application-deployments.md).  

## <a name="deploy-an-application"></a>Bereitstellen einer Anwendung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen**.  

3.  Wählen Sie in der Liste **Anwendungen** die Anwendung aus, die Sie bereitstellen möchten. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

4.  Geben Sie im Assistenten zum Bereitstellen von Software auf der Seite **Allgemein** die folgenden Informationen an:  

    -   **Software** : Hier wird die Anwendung angezeigt, die bereitgestellt werden soll. Sie können auf **Durchsuchen** klicken, um eine andere Anwendung auszuwählen.  

    -   **Sammlung** : Klicken Sie auf **Durchsuchen** , um die Sammlung auszuwählen, in der Sie die Anwendung bereitstellen möchten.  

    -   **Standard-Verteilungspunktgruppen verwenden, die dieser Sammlung zugeordnet sind** : Wählen Sie diese Option aus, wenn der Anwendungsinhalt in der Standard-Verteilungspunktgruppe der Sammlung gespeichert werden soll. Wenn die ausgewählte Sammlung keiner Verteilungspunktgruppe zugeordnet ist, ist diese Option nicht verfügbar.  

    -   **Inhalt automatisch für Abhängigkeiten bereitstellen** : Wenn diese Option aktiviert ist und Bereitstellungstypen in der Anwendung Abhängigkeiten enthalten, wird der Inhalt der abhängigen Anwendung ebenfalls an Verteilungspunkte gesendet.  

        > [!IMPORTANT]  
        >  Wenn Sie ein Update der abhängigen Anwendung ausführen, nachdem die primäre Anwendung bereitgestellt wurde, wird neuer Inhalt für die Abhängigkeit nicht automatisch verteilt.  

    -   **Kommentare (optional)** : Geben Sie bei Bedarf eine Beschreibung der Bereitstellung ein.  

5.  Klicken Sie auf der Seite **Inhalt** auf **Hinzufügen**, um den dieser Bereitstellung zugeordneten Inhalt Verteilungspunkten oder Verteilungspunktgruppen hinzuzufügen. Wenn Sie auf der Seite **Allgemein** die Option „Standard-Verteilungspunktgruppen verwenden, die dieser Sammlung zugeordnet sind“ aktiviert haben, wird diese Option automatisch aufgefüllt und kann nur von einem Mitglied der Sicherheitsrolle **Anwendungsadministrator** geändert werden.  

6.  Klicken Sie auf **Weiter**.  

7.  Geben Sie im Assistenten zum Bereitstellen von Software auf der Seite **Bereitstellungseinstellungen** die folgenden Informationen an:  

    -   **Aktion** : Wählen Sie in der Dropdownliste aus, ob diese Bereitstellung zum **Installieren** oder **Deinstallieren** der Anwendung dienen soll.  

        > [!NOTE]  
        >  Wenn eine Anwendung zweimal auf einem Gerät bereitgestellt wird, einmal mit der Aktion **Installieren** und einmal mit der Aktion **Deinstallieren**, hat die Anwendungsbereitstellung mit der Aktion **Installieren** höhere Priorität.  
        >   
        >  Sie können die Aktion einer Bereitstellung nicht mehr ändern, nachdem sie erstellt wurde.  

    -   **Zweck** : Wählen Sie in der Dropdownliste eine der folgenden Optionen aus:  

        -   **Verfügbar** : Wenn die Anwendung für einen Benutzer bereitgestellt wird, ist sie für den Benutzer im Softwarecenter als veröffentlichte Anwendung sichtbar, und er kann sie bei Bedarf installieren.  

        -   **Erforderlich** : Die Anwendung wird gemäß dem konfigurierten Zeitplan automatisch bereitgestellt. Allerdings kann ein Benutzer den Bereitstellungsstatus der Anwendung (sofern dieser nicht ausgeblendet ist) nachverfolgen und die Anwendung vor Ablauf der Frist über das Softwarecenter installieren.  

            > [!NOTE]  
            >  Wenn als Bereitstellungsaktion **Deinstallieren**ausgewählt wurde, wird als Bereitstellungszweck automatisch **Erforderlich** festgelegt, und die Einstellung kann nicht geändert werden.  

    -   **Automatisch mit oder ohne Benutzeranmeldung bereitstellen** : Aktivieren Sie diese Option, wenn die Bereitstellung für einen Benutzer bestimmt ist, um die Anwendung auf den primären Geräten des Benutzers bereitzustellen. Bei dieser Einstellung ist es nicht erforderlich, dass sich der Benutzer vor der Ausführung der Bereitstellung anmeldet. Wählen Sie diese Option nicht, wenn Benutzereingaben erforderlich sind, um die Installation abzuschließen. Diese Option ist nur verfügbar, wenn der Bereitstellungszweck auf **Erforderlich**festgelegt ist.  

    -   **Aktivierungspakete senden** : Wenn der Bereitstellungszweck auf **Erforderlich** festgelegt und diese Option ausgewählt wird, wird vor der Installation der Bereitstellung ein Aktivierungspaket an den Computer gesendet, um ihn zum Zeitpunkt der Installation aus dem Standbymodus zu aktivieren. Sie können diese Option nur verwenden, wenn Computer und Netzwerke für Wake-On-LAN konfiguriert sind.  

    -   **Clients mit einer getakteten Internetverbindung dürfen den Inhalt nach dem Installationsstichtag herunterladen (Zusatzkosten können anfallen)** : Diese Option ist nur für Bereitstellungen mit dem Zweck **Erforderlich**verfügbar.  

    -   **Genehmigung durch Administrator erforderlich, wenn Benutzer diese Anwendung anfordern** : Wenn diese Option ausgewählt ist, muss der Administrator jede Benutzeranforderung für die Anwendung zunächst genehmigen, bevor sie installiert werden kann. Diese Option ist nicht verfügbar, wenn der Zweck der Bereitstellung **Erforderlich** lautet oder wenn die Anwendung für eine Gerätesammlung bereitgestellt wird.  

        > [!NOTE]  
        >  Genehmigungsanforderungen für Anwendungen werden im Arbeitsbereich **Softwarebibliothek** unter **Anwendungsverwaltung** im Knoten **Genehmigungsanforderungen** angezeigt. Wenn eine Genehmigungsanforderung nicht innerhalb von 45 Tagen genehmigt wird, wird sie entfernt. Außerdem können ausstehende Genehmigungsanforderungen durch eine Neuinstallation des Configuration Manager-Client abgebrochen werden.  

    -   **Automatisch ein Upgrade aller abgelösten Versionen dieser Anwendung ausführen** : Wenn diese Option ausgewählt ist, wird für alle abgelösten Versionen der Anwendung ein Upgrade auf die neuere Version ausgeführt.  

8.  Konfigurieren Sie im Assistenten zum Bereitstellen von Software auf der Seite **Zeitplanung** , wann diese Anwendung für Clientgeräte bereitgestellt oder verfügbar gemacht wird.  
    Welche Optionen auf dieser Seite verfügbar sind, ist davon abhängig, ob die Bereitstellungsaktion auf **Verfügbar** oder **Erforderlich**gesetzt ist.  

9. Wenn die bereitgestellte Anwendung eine andere Anwendung ablöst, können Sie den Stichtag festlegen, an dem bei Benutzern die neue Anwendung installiert wird. Verwenden Sie dafür die Einstellung **Installationsstichtag** , um für Benutzer mit abgelösten Anwendungen ein Upgrade auszuführen.  

10. Geben Sie im Assistenten zum Bereitstellen von Software auf der Seite **Benutzerfreundlichkeit** an, wie Benutzer mit der Anwendungsinstallation interagieren können.
    Beim Bereitstellen von Anwendungen für Windows Embedded-Geräte mit Schreibfilteraktivierung können Sie angeben, dass die Anwendung im temporären Overlay gespeichert und die Änderungen später übernommen werden sollen. Sie können auch angeben, dass die Änderungen am Installationsstichtag oder während eines Wartungsfensters übernommen werden sollen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden, ist ein Neustart erforderlich, und die Änderungen werden auf dem Gerät beibehalten.  
   > [!NOTE]  
   >  Stellen Sie beim Bereitstellen einer Anwendung auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist. Weitere Informationen zur Verwendung von Wartungsfenstern beim Bereitstellen von Anwendungen auf Windows Embedded-Geräten finden Sie unter [Erstellen von Windows Embedded-Anwendungen](../../apps/get-started/creating-windows-embedded-applications.md).  
   >  Die Optionen **Softwareinstallation** und **Systemneustart (falls dieser zum Abschluss der Installation erforderlich ist)** werden nicht verwendet, wenn der Bereitstellungszweck auf **Verfügbar**gesetzt ist. Sie können auch die Ebene für die Benutzerbenachrichtigung bei der Anwendungsinstallation konfigurieren.  
11. Konfigurieren Sie im Assistenten zum Bereitstellen von Software auf der Seite **Warnungen**, wie Warnungen von Configuration Manager und System Center Operations Manager für diese Bereitstellung generiert werden. Sie können Schwellenwerte für Berichtswarnungen konfigurieren und die Berichterstattung für die Dauer der Bereitstellung deaktivieren.  

12. (Nur für iOS-Apps) – Klicken Sie auf der Seite **App-Konfigurationsrichtlinien** auf **Neu**, um diese Bereitstellung einer iOS-App-Konfigurationsrichtlinie zuzuordnen (sofern Sie eine solche erstellt haben). Weitere Informationen zu diesen Richtlinientypen finden Sie unter [Konfigurieren von Apps mit Konfigurationsrichtlinien für Apps](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).  

13. Überprüfen Sie im Assistenten zum Bereitstellen von Software auf der Seite **Zusammenfassung** die Aktionen, die für die Bereitstellung ausgeführt werden. Klicken Sie auf **Weiter** , um den Assistenten abzuschließen.  

 Die neue Bereitstellung wird anschließend im Arbeitsbereich **Überwachung** im Knoten **Bereitstellungen** in der Liste **Bereitstellungen** angezeigt. Sie können die Eigenschaften dieser Bereitstellung bearbeiten oder die Bereitstellung auf der Registerkarte **Bereitstellungen** des Anwendungsdetailbereichs löschen.  

## <a name="delete-an-application-deployment"></a>Löschen einer Anwendungsbereitstellung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen**.  

3.  Wählen Sie in der Liste **Anwendungen** die Anwendung aus, deren Bereitstellung Sie löschen möchten.  

4.  Wählen Sie auf der Registerkarte **Bereitstellungen** in der Liste *<Anwendungsname\>* die zu löschende Anwendungsbereitstellung aus. Klicken Sie auf der Registerkarte **Bereitstellung** in der Gruppe **Bereitstellung** dann auf **Löschen**.  

 Wenn Sie eine Anwendungsbereitstellung löschen, werden bereits installierte Instanzen der Anwendung nicht entfernt. Sie müssen diese Anwendungen mit der Aktion **Deinstallieren**auf Computern bereitstellen, um sie zu entfernen. Wenn Sie eine Anwendungsbereitstellung löschen oder eine Ressource aus der Sammlung entfernen, in der Sie die Bereitstellung vornehmen, wird diese im Softwarecenter nicht mehr angezeigt.  



<!--HONumber=Nov16_HO1-->


