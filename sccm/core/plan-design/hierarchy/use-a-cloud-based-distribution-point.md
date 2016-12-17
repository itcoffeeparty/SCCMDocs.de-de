---
title: Cloudbasierter Verteilungspunkt | System Center Configuration Manager
description: "Erfahren Sie mehr über Konfigurationen und Einschränkungen zur Verwendung eines cloudbasierten Verteilungspunkts mit System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c1838866241c30598346b84cb36b8bf4967bf7f6


---
# <a name="use-a-cloud-based-distribution-point-with-system-center-configuration-manager"></a>Verwenden eines cloudbasierten Verteilungspunkts mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ein cloudbasierter Verteilungspunkt ist ein in Microsoft Azure gehosteter System Center Configuration Manager-Verteilungspunkt. Die folgende Informationen sollen Ihnen die Konfigurationen und Einschränkungen bei der Verwendung eines cloudbasierten Verteilungspunkts näherbringen.

Wenn Sie einen primären Standort installiert haben und bereit für die Installation eines cloudbasierten Verteilungspunkts sind, lesen Sie den Artikel [Install cloud-based distribution points in Microsoft Azure](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md) (Installieren von cloudbasierten Verteilungspunkten in Microsoft Azure).


## <a name="plan-to-use-a-cloud-based-distribution-point"></a>Planen, einen cloudbasierten Verteilungspunkt zu verwenden
Bei Verwendung eines cloudbasierten Verteilungspunkt auszuführende Aufgaben:  

-   **Konfigurieren von Clienteinstellungen** , um Benutzern und Geräten Zugriff auf die Inhalte zu ermöglichen  

-   **Angeben eines primären Standorts zur Verwaltung der Übertragung von Inhalten** an den Verteilungspunkt  

-   **Angeben von Schwellenwerten** für die Menge an Inhalten, die Sie auf einem Verteilungspunkt speichern möchten, sowie für die Menge an Inhalten, die von Clients vom Verteilungspunkt übertragen werden können  


Auf Basis dieser konfigurierten Schwellenwerte kann Configuration Manager Warnungen ausgeben, wenn die Gesamtmenge an Inhalten, die Sie auf dem Verteilungspunkt gespeichert haben, sich der angegebenen Speichermenge nähert, bzw. wenn von Clients übertragene Daten sich den von Ihnen definierten Schwellenwerten nähern.  

Von cloudbasierten Verteilungspunkten werden die folgenden Funktionen unterstützt, die auch von lokalen Verteilungspunkten unterstützt werden:  

-   Cloudbasierte Verteilungspunkte werden einzeln oder als Mitglieder von Verteilungspunktgruppen verwaltet.  

-   Sie können einen cloudbasierten Verteilungspunkt als Fallbackinhaltsquelle verwenden.  

-   Sowohl intranet- als auch internetbasierte Clients werden unterstützt.  


Aus cloudbasierten Verteilungspunkten ergeben sich die folgenden zusätzlichen Vorteile:  

-   Inhalt, der an den cloudbasierten Verteilungspunkt gesendet wird, wird von Configuration Manager verschlüsselt, bevor er von Configuration Manager an Microsoft Azure übermittelt wird.  

-   In Microsoft Azure können Sie den Clouddienst manuell skalieren, um der schwankenden Nachfrage nach Inhaltsanforderungen von Clients Rechnung zu tragen, ohne zusätzliche Verteilungspunkte installieren und bereitstellen zu müssen.  

-   Der Download von Inhalt durch Clients, die für Windows BranchCache konfiguriert sind, wird von cloudbasierten Verteilungspunkten unterstützt.  


Bei cloudbasierten Verteilungspunkten ergeben sich die folgenden Einschränkungen:  

-   Ein cloudbasierter Verteilungspunkt kann nicht zum Hosten von Softwareupdatepaketen verwendet werden.  

-   Ein cloudbasierter Verteilungspunkt kann nicht für PXE- oder multicastfähige Bereitstellungen verwendet werden.  

-   Clients wird kein cloudbasierter Verteilungspunkt als Inhaltsort für eine Tasksequenz angeboten, die mit der Bereitstellungsoption **Inhalt lokal herunterladen, wenn dies für die Ausführung der Tasksequenz erforderlich ist**bereitgestellt wird. Von Tasksequenzen, die mit der Bereitstellungsoption **Den gesamten Inhalt vor Starten der Tasksequenz lokal herunterladen** bereitgestellt wurden, kann dagegen ein cloudbasierter Verteilungspunkt als gültiger Inhaltsort verwendet werden.  

-   Pakete, die vom Verteilungspunkt ausgeführt werden, werden von einem cloudbasierten Verteilungspunkt nicht unterstützt. Alle Inhalte müssen vom Client heruntergeladen und dann lokal ausgeführt werden.  

-   Das Streaming von Anwendungen mithilfe von Anwendungsvirtualisierung oder ähnlichen Programmen wird von einem cloudbasierten Verteilungspunkt nicht unterstützt.  

-   Vorab bereitgestellter Inhalt wird von einem cloudbasierten Verteilungspunkt nicht unterstützt. Sämtlicher Inhalt wird vom Verteilungs-Manager des primären Standorts, von dem der Verteilungspunkt verwaltet wird, an den Verteilungspunkt übertragen.  

-   Ein cloudbasierter Verteilungspunkt kann nicht als Pullverteilungspunkt konfiguriert werden.  

##  <a name="a-namebkmkprereqsclouddpa-prerequisites-for-cloud-based-distribution-points"></a><a name="BKMK_PrereqsCloudDP"></a> Voraussetzungen für cloudbasierte Verteilungspunkte  
 Die Verwendung eines cloudbasierten Verteilungspunkts setzt Folgendes voraus:  

-   Ein Microsoft Azure-Abonnement  (Informationen hierzu finden Sie unter [Informationen zu Abonnements und Zertifikaten](#BKMK_CloudDPCerts) in diesem Thema)

-   Ein selbstsigniertes oder PKI-Verwaltungszertifikat für die Kommunikation zwischen einem primären Configuration Manager-Standortserver und dem Clouddienst in Microsoft Azure  (Informationen hierzu finden Sie unter [Informationen zu Abonnements und Zertifikaten](#BKMK_CloudDPCerts) in diesem Thema)

-   Ein Dienstzertifikat (PKI), über das von Configuration Manager-Clients eine Verbindung mit cloudbasierten Verteilungspunkten hergestellt und mithilfe von HTTPS Inhalt heruntergeladen wird  

-   Für ein Gerät oder einen Benutzer muss die Clienteinstellung **Zugriff auf Cloudverteilungspunkt zulassen** unter **Clouddienste** auf **Ja**festgelegt werden. Andernfalls ist der Zugriff auf Inhalte auf einem cloudbasierten Verteilungspunkt nicht möglich. Dieser Wert ist standardmäßig auf **Nein**eingestellt.  

-   Der DNS-Namespace muss einen DNS-Alias (CNAME-Eintrag) enthalten, damit der Name des Clouddiensts von Clients aufgelöst werden kann.  

-   Ein Client muss Zugriff auf das Internet haben, damit der cloudbasierte Verteilungspunkt verwendet werden kann.  

##  <a name="a-namebkmkclouddpcosta-cost-of-using-cloud-based-distribution"></a><a name="BKMK_CloudDPCost"></a> Kosten einer cloudbasierten Verteilung  
 Planen Sie beim Verwenden eines cloudbasierten Verteilungspunkts die Kosten der Datenspeicherung und der von Configuration Manager-Clients durchgeführten Downloadübertragungen ein.  

 Configuration Manager bietet Optionen zum Kontrollieren der Kosten und Überwachen des Datenzugriffs:  

-   Sie können die Menge von Inhalten steuern und überwachen, die Sie in einem Clouddienst speichern.  

-   Sie können Configuration Manager so konfigurieren, dass Sie gewarnt werden, wenn **Schwellenwerte** für Clientdownloads monatliche Limits erreichen oder überschreiten.  

-   Zusätzlich können Sie mit dem Peercaching (BranchCache) arbeiten, um die Anzahl von Datenübertragungen von cloudbasierten Verteilungspunkten durch Clients zu reduzieren. Für Windows BranchCache konfigurierte Configuration Manager-Clients können Inhalt über cloudbasierte Verteilungspunkte übertragen.  


**Optionen:**  

-   **Clienteinstellungen für die Cloud:**Sie steuern den Zugriff auf alle cloudbasierten Verteilungspunkte in einer Hierarchie über die **Clienteinstellungen**.  

     In **Clienteinstellungen**wird die Einstellung **Zugriff auf Cloudverteilungspunkte zulassen** von der Kategorie **Cloudeinstellungen**unterstützt. Standardmäßig ist die Priorität auf den Wert **Nein**eingestellt. Sie können diese Einstellung für Benutzer und Geräte aktivieren.  

-   **Schwellenwerte für Datenübertragungen:**Sie können Schwellenwerte für die Menge an Daten konfigurieren, die Sie auf einem Verteilungspunkt speichern möchten, sowie für die Menge an Daten, die Clients von einem Verteilungspunkt herunterladen.  

     Schwellenwerte für cloudbasierte Verteilungspunkte umfassen Folgendes:  

    -   **Schwellenwert für die Speicherwarnung**: Durch einen Schwellenwert für die Speicherwarnung wird eine Obergrenze für die Menge an Daten oder Inhalt festgelegt, die Sie auf dem cloudbasierten Verteilungspunkt speichern möchten. Sie können veranlassen, dass durch Configuration Manager eine Warnung generiert wird, wenn der verbleibende freie Speicherplatz Ihres Speicherwarnschwellenwerts den von Ihnen festgelegten Stand erreicht.  

    -   **Schwellenwert für die Übertragungswarnung**: Ein Schwellenwert für die Übertragungswarnung hilft Ihnen bei der Überwachung der Menge an Inhalt, die innerhalb von 30 Tagen vom Verteilungspunkt an Clients übertragen wird. Mithilfe des Schwellenwerts für die Übertragungswarnung wird die Übertragung von Daten für einen Zeitraum von 30 Tagen überwacht, und es kann eine Warnung sowie eine kritische Warnung ausgegeben werden, wenn die Übertragungen den von Ihnen definierten Wert erreichen.  

        > [!IMPORTANT]  
        >  Configuration Manager überwacht die Übertragung von Daten, beendet die Datenübertragung jedoch nicht, wenn sie den angegebenen Übertragungswarnschwellenwert überschreitet.  

 Sie können Schwellenwerte für jeden cloudbasierten Verteilungspunkt während der Installation des Verteilungspunkts festlegen, oder Sie können die Eigenschaften jedes cloudbasierten Verteilungspunkts bearbeiten, nachdem dieser installiert wurde.  

-   **Warnungen**: Sie können Configuration Manager so konfigurieren, dass Warnungen zu Datenübertragungen von und zu jedem cloudbasierten Verteilungspunkt auf Basis der von Ihnen angegebenen Schwellenwerte für Datenübertragungen ausgegeben werden. Diese Warnungen helfen Ihnen bei der Überwachung der Datenübertragungen sowie bei der Entscheidung, wann Sie den Clouddienst beenden sollten, um die weitere Verwendung zu verhindern. Außerdem helfen sie beim Anpassen des Inhalts, den Sie auf dem Verteilungspunkt speichern, oder der Einstellung, welche Clients die cloudbasierten Verteilungspunkte verwenden dürfen.  

     Der primäre Standort, der den cloudbasierten Verteilungspunkt überwacht, lädt stündlich Transaktionsdaten von Microsoft Azure herunter und speichert sie in der Datei „CloudDP-&lt;Dienstname\>.log“ auf dem Standortserver. Configuration Manager wertet dann diese Informationen anhand der Speicher- und Übertragungskontingente für die einzelnen cloudbasierten Verteilungspunkte aus. Wenn die Datenübertragung das für Warnungen oder kritische Warnungen angegebene Volumen erreicht oder überschreitet, generiert Configuration Manager die entsprechende Warnung.  

    > [!WARNING]  
    >  Da die Informationen zu Datenübertragungen stündlich von Windows Azure heruntergeladen werden, kann die Datennutzung eine Warnung oder einen kritischen Schwellenwert überschreiten, bevor Configuration Manager auf die Daten zugreifen und eine Warnung ausgeben kann.  

    > [!NOTE]  
    >  Warnungen für einen cloudbasierten Verteilungspunkt hängen von den Nutzungsstatistiken aus Windows Azure ab. Es kann bis zu 24 Stunden dauern, bis sie verfügbar sind. Weitere Informationen zu Speicheranalysen für Windows Azure, auch wie häufig Nutzungsstatistiken von Windows Azure aktualisiert werden, finden Sie unter [Speicheranalyse](http://go.microsoft.com/fwlink/p/?LinkID=275111) in der MSDN-Bibliothek.  


-   **Den Clouddienst nach Bedarf starten oder beenden:**Mit dieser Option können Sie einen Clouddienst jederzeit beenden, um zu verhindern, dass der Dienst ununterbrochen von Clients verwendet wird. Wenn Sie den Clouddienst beenden, werden Clients mit sofortiger Wirkung daran gehindert, zusätzliche Inhalte vom Dienst herunterzuladen. Sie können den Clouddienst erneut starten, um den Zugriff für Clients wiederherzustellen. Beispiel: Sie möchten einen Clouddienst möglicherweise beenden, wenn Datenschwellenwerte erreicht sind.  

     Wenn Sie einen Clouddienst beenden, dann wird der Inhalt vom Verteilungspunkt von diesem Clouddienst nicht gelöscht, und es wird auch nicht verhindert, dass vom Standortserver zusätzliche Inhalte an den cloudbasierten Verteilungspunkt übertragen werden.  

     Wählen Sie zum Beenden eines Clouddiensts in der Configuration Manager-Konsole den Verteilungspunkt im Arbeitsbereich **Verwaltung** im Knoten **Cloudverteilungspunkte** unter **Clouddienste** aus. Klicken Sie als Nächstes auf **Dienst beenden** , um den Clouddienst zu beenden, der in Windows Azure ausgeführt wird.  

##  <a name="a-namebkmkclouddpcertsa-about-subscriptions-and-certificates-for-cloud-based-distribution-points"></a><a name="BKMK_CloudDPCerts"></a> Informationen zu Abonnements und Zertifikaten für cloudbasierte Verteilungspunkte  
 Für cloudbasierte Verteilungspunkte sind Zertifikate erforderlich, damit Configuration Manager den Clouddienst verwalten kann, von dem der Verteilungspunkt gehostet wird, und Clients auf Inhalte vom Verteilungspunkt zugreifen können. Im Folgenden finden Sie einen Überblick über diese Zertifikate. Ausführlichere Informationen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Zertifikate**  

-   **Verwaltungszertifikat für die Kommunikation zwischen Standortserver und Verteilungspunkt**: Das Verwaltungszertifikat richtet die Vertrauensstellung zwischen der Verwaltungs-API von Microsoft Azure und Configuration Manager ein. Mithilfe dieser Authentifizierung kann Configuration Manager die Microsoft Azure-API aufrufen, beispielsweise wenn Sie Inhalt bereitstellen oder den Clouddienst starten und beenden. Mit Microsoft Azure können Kunden eigene Verwaltungszertifikate erstellen. Dabei kann es sich um ein selbstsigniertes Zertifikat oder um ein von einer Zertifizierungsstelle ausgegebenes Zertifikat handeln:  

    -   Stellen Sie die CER-Datei des Verwaltungszertifikats für Microsoft Azure bereit, wenn Sie Microsoft Azure für Configuration Manager konfigurieren. Die CER-Datei enthält den öffentlichen Schlüssel für das Verwaltungszertifikat. Sie müssen das Zertifikat in Microsoft Azure hochladen, bevor Sie einen cloudbasierten Verteilungspunkt installieren. Mit diesem Zertifikat wird Configuration Manager der Zugriff auf die Microsoft Azure-API ermöglicht.  

    -   Stellen Sie die PFX-Datei des Verwaltungszertifikats für Configuration Manager bereit, wenn Sie den cloudbasierten Verteilungspunkt installieren. Die PFX-Datei enthält den privaten Schlüssel für das Verwaltungszertifikat. Configuration Manager speichert dieses Zertifikat in der Standortdatenbank. Da in der PFX-Datei der private Schlüssel enthalten ist, müssen Sie das Kennwort angeben, um diese Zertifikatdatei in die Configuration Manager-Datenbank zu importieren.  

    Wenn Sie ein selbstsigniertes Zertifikat erstellen, müssen Sie das Zertifikat zuerst als CER-Datei exportieren und dann als PFX-Datei erneut exportieren.  

    Optional können Sie eine **PUBLISHSETTINGS** -Datei "Version 1" aus dem Microsoft Azure SDK 1.7 angeben. Informationen zu PUBLISHSETTINGS-Dateien finden Sie in der Microsoft Azure-Dokumentation.  

    Weitere Informationen finden Sie unter [Erstellen eines Verwaltungszertifikats](http://go.microsoft.com/fwlink/p/?LinkId=220281) und [Gewusst wie: Hinzufügen eines Verwaltungszertifikats zu einem Windows Azure-Abonnement](http://go.microsoft.com/fwlink/p/?LinkId=241722) im Abschnitt zur Microsoft Azure-Plattform in der MSDN Library.  

-   **Dienstzertifikat für die Clientkommunikation mit dem Verteilungspunkt**: Mithilfe des cloudbasierten Verteilungspunkt-Dienstzertifikats von Configuration Manager wird eine Vertrauensstellung zwischen den Configuration Manager-Clients und dem cloudbasierten Verteilungspunkt hergestellt. Außerdem werden die Daten, die von Clients von diesem Punkt heruntergeladen werden, per Secure Socket Layer (SSL) über HTTPS geschützt.  

    > [!IMPORTANT]  
    >  Der allgemeine Name im Feld für den Zertifikatantragsteller des Dienstzertifikats muss in der Domäne eindeutig sein und darf nicht mit einem Gerät der Domäne übereinstimmen.  

   Eine Beispielbereitstellung dieses Zertifikats finden Sie im Abschnitt *Bereitstellen des Dienstzertifikats für cloudbasierte Verteilungspunkte* des Themas [Beispiel für die schrittweise Bereitstellung der PKI-Zertifikate für System Center Configuration Manager: Windows Server 2008-Zertifizierungsstelle](/sccm/core/plan-design/network/example-deployment-of-pki-certificates) .  

##  <a name="a-namebkmktasksa-common-management-tasks-for-cloud-based-distribution-points"></a><a name="bkmk_Tasks"></a> Allgemeine Verwaltungsaufgaben für cloudbasierte Verteilungspunkte  

-   **Kommunikation zwischen Standortserver und cloudbasiertem Verteilungspunkt:**Beim Installieren eines cloudbasierten Verteilungspunkts müssen Sie einen primären Standort zuweisen, um die Übertragung von Inhalt an den Clouddienst zu verwalten. Diese Aktion entspricht der Installation der Standortsystemrolle „Verteilungspunkt“ an einem bestimmten Standort.  

-   **Kommunikation zwischen Client und cloudbasiertem Verteilungspunkt:**Wenn für ein Gerät oder einen Benutzer eines Geräts die Clienteinstellung für die Verwendung eines cloudbasierten Verteilungspunkts konfiguriert ist, kann das Gerät den cloudbasierten Verteilungspunkt als gültigen Inhaltsspeicherort erhalten:  

    -   Ein cloudbasierter Verteilungspunkt wird als Remoteverteilungspunkt eingestuft, wenn ein Client die verfügbaren Inhaltsspeicherorte auswertet.  

    -   Clients im Intranet nutzen cloudbasierte Verteilungspunkte nur als Fallbackoption, falls keine lokalen Verteilungspunkte verfügbar sind.  

    Zwar können Sie cloudbasierte Verteilungspunkte in bestimmten Regionen von Microsoft Azure installieren, doch bleiben Clients, die cloudbasierte Verteilungspunkte verwenden, die Microsoft Azure-Regionen unbekannt. Von solchen Clients wird ein cloudbasierter Verteilungspunkt nichtdeterministisch ausgewählt. Dies bedeutet Folgendes: Wenn Sie cloudbasierte Verteilungspunkte in mehreren Regionen installieren und ein Client mehrere cloudbasierte Verteilungspunkte als Inhaltsorte empfängt, verwendet der Client u. U. keinen cloudbasierten Verteilungspunkt aus derselben Microsoft Azure-Region wie der Client.  

    Von Clients, die cloudbasierter Verteilungspunkte nutzen können, befolgen bei Inhaltsspeicherortanforderungen die folgende Sequenz:  

    1.  Von einem Client, für den die Nutzung von cloudbasierten Verteilungspunkten konfiguriert wurde, wird immer zuerst versucht, Inhalt von einem bevorzugten Verteilungspunkt abzurufen.  

    2.  Wenn kein bevorzugter Verteilungspunkt verfügbar ist, wird vom Client ein Remoteverteilungspunkt verwendet, sofern diese Option von der Bereitstellung unterstützt wird und ein Remoteverteilungspunkt verfügbar ist.  

    3.  Falls kein bevorzugter Verteilungspunkt oder Remoteverteilungspunkt verfügbar ist, kann der Inhalt vom Client als Fallbackoption von einem cloudbasierten Verteilungspunkt abgerufen werden.  

        > [!NOTE]  
        >  Von Clients im Internet, die als Inhaltsspeicherorte für eine Bereitstellung sowohl einen internetbasierten Verteilungspunkt als auch einen cloudbasierten Verteilungspunkt erhalten, wird nur versucht, Inhalt vom internetbasierten Verteilungspunkt abzurufen. Falls vom Client im Internet kein Inhalt vom internetbasierten Verteilungspunkt abgerufen werden kann, wird vom Client nicht der Versuch unternommen, auf den cloudbasierten Verteilungspunkt zuzugreifen.  


  Wenn von einem Client ein cloudbasierter Verteilungspunkt als Inhaltsspeicherort verwendet wird, wird die Authentifizierung des Clients beim cloudbasierten Verteilungspunkt mithilfe eines Configuration Manager-Zugriffstokens durchgeführt. Falls das Zertifikat des cloudbasierten Verteilungspunkts von Configuration Manager für den Client vertrauenswürdig ist, kann der angeforderte Inhalt vom Client heruntergeladen werden.  

-   **Überwachen cloudbasierter Verteilungspunkte:**Sie können den Inhalt überwachen, den Sie auf jedem Verteilungspunkt bereitstellen, und Sie können den Clouddienst überwachen, der als Host des Verteilungspunkts dient.  

    -   **Inhalt**: Sie überwachen Inhalte, die Sie für einen cloudbasierten Verteilungspunkt bereitstellen, auf dieselbe Weise, wie Sie Inhalte für lokale Verteilungspunkte bereitstellen würden.  

    -   **Clouddienst**: Der Azure-Dienst wird von Configuration Manager regelmäßig überprüft, und es erfolgt eine Warnung, wenn der Dienst nicht aktiv ist oder Abonnement- oder Zertifikatsprobleme auftreten. Sie können auch Details zum Verteilungspunkt im Arbeitsbereich **Verwaltung** im Knoten **Cloudverteilungspunkte** unter **Clouddienste** auf der Configuration Manager-Konsole einsehen. Von diesem Ort aus können Sie sich Informationen zum Verteilungspunkt auf hoher Ebene anzeigen lassen oder einen Verteilungspunkt auswählen und anschließend dessen **Eigenschaften**bearbeiten.  

    Beim Bearbeiten der Eigenschaften eines cloudbasierten Verteilungspunkts können Sie Folgendes:  

    -   Die Datenschwellenwerte für Speicherung und Warnungen anpassen  

    -   Inhalte wie bei einem lokalen Verteilungspunkt verwalten  

    Schließlich können Sie für jeden cloudbasierten Verteilungspunkt die Abonnement-ID, den Dienstnamen sowie andere damit verbundene Details anzeigen, die beim Installieren der cloudbasierten Verteilung angegeben werden, diese jedoch nicht bearbeiten.  

-   **Sicherung und Wiederherstellung von cloudbasierten Verteilungspunkten:**Wenn Sie einen cloudbasierten Verteilungspunkt in der Hierarchie verwenden, dann nutzen Sie folgende Informationen, die bei der Planung einer Sicherung oder Wiederherstellung des Verteilungspunktes hilfreich sind:  

    -   Wenn Sie den vordefinierten Wartungstask **Standortserver sichern** verwenden, dann werden die Konfigurationen für den cloudbasierten Verteilungspunkt automatisch von Configuration Manager berücksichtigt.  

    -   Eine bewährte Methode ist es, sowohl das Verwaltungszertifikat als auch das Dienstzertifikat, das mit einem cloudbasierten Verteilungspunkt verwendet wird, als Kopie zu sichern. Falls Sie den primären Standort von Configuration Manager, von dem der cloudbasierte Verteilungspunkt verwaltet wird, auf einem anderen Computer wiederherstellen, dann müssen Sie die Zertifikate neu importieren, bevor Sie sie weiter verwenden können.  

-   **Deinstallieren eines cloudbasierten Verteilungspunkts**: Zur Deinstallation eines cloudbasierten Verteilungspunkts wählen Sie diesen in der Configuration Manager-Konsole und anschließend **Löschen** aus.  

    Wenn Sie einen cloudbasierten Verteilungspunkt aus einer Hierarchie löschen, dann entfernt Configuration Manager den Inhalt aus dem Clouddienst in Windows Azure.  



<!--HONumber=Nov16_HO1-->

