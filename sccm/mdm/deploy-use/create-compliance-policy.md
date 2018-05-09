---
title: Erstellen und Bereitstellen einer Gerätekonformitätsrichtlinie
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie eine Gerätekonformitätsrichtlinie in System Center Configuration Manager erstellen und bereitstellen.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex
ms.openlocfilehash: 3dd502e8ba9e03851af6ec58ad63d4aa805fe7b4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-deploy-a-device-compliance-policy"></a>Erstellen und Bereitstellen einer Gerätekonformitätsrichtlinie

*Gilt für: System Center Configuration Manager (Current Branch)*


## <a name="create-a-compliance-policy"></a>Erstellen einer Konformitätsrichtlinie

1.  Wählen Sie in der System Center Configuration Manager-Konsole **Bestand und Kompatibilität** aus.

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, und wählen Sie **Kompatibilitätsrichtlinien**.

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** **Kompatibilitätsrichtlinie erstellen**.

4.  Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Kompatibilitätsrichtlinien die folgenden Informationen an:

  * **Name**: Geben Sie einen eindeutigen Namen für die Konformitätsrichtlinie ein. Sie können bis zu 256 Zeichen verwenden.

  * **Beschreibung**: Geben Sie eine Beschreibung ein, die Ihnen einen Überblick über das VPN-Profil verschafft und dabei behilflich ist, das Profil in der Configuration Manager-Konsole zu ermitteln. Sie können bis zu 256 Zeichen verwenden.

  * **Type of compliance policy** (Typ der Konformitätsrichtlinie): Wählen Sie den Richtlinientyp, den Sie erstellen möchten, auf Grundlage der Tatsache aus, ob Ihr Gerät von Configuration Manager verwaltet wird. <br /><br /> Wählen Sie für Geräte, die von Intune verwaltet werden, die Option **Compliance rules for devices managed without configuration manager client** (Kompatibilitätsregeln für Geräte, die ohne den Configuration Manager-Client verwaltet werden). Bei Wahl dieser Option können Sie auch den Typ der Plattform auswählen, dem Sie diese Richtlinie zuweisen möchten.

  * **Schweregrad der Nichtkonformität für Berichte**: Geben Sie den Schweregrad an, der gemeldet wird, wenn diese Konformitätsrichtlinie als nicht konform ausgewertet wird. Die verfügbaren Schweregrade sind:

     * **Keiner**: Für Geräte, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.
     * **Information**: Für Geräte, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.   
     * **Warnung**: Für Geräte, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.
     * **Kritisch**: Für Geräte, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.
     * **Kritisch mit Ereignis**: Für Geräte, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Der Schweregrad **Kritisch mit Ereignis** wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.      

5.  Wählen Sie auf der Seite **Unterstützte Plattformen** die Geräteplattformen aus, für die diese Konformitätsrichtlinie ausgewertet wird. Sie können auch auf **Alles auswählen** klicken, um alle Geräteplattformen auszuwählen. Folgende Plattformen werden unterstützt: Windows 7, Windows 8.1 und Windows 10; Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 und Windows Server 2016.

6.  Auf der Seite **Regeln** definieren Sie eine oder mehrere Regeln, die die Konfiguration bestimmen, die Geräte aufweisen müssen, um als kompatibel eingestuft zu werden. Wenn Sie eine Konformitätsrichtlinie erstellen, sind einige Regeln standardmäßig aktiviert, die Sie aber bearbeiten oder löschen können. Eine vollständige Liste aller Regeln finden Sie unter „Regeln für Konformitätsrichtlinie“ weiter unten in diesem Artikel.

  > [!NOTE]  
  >  Auf Windows-PCs wird die Windows-Betriebssystemversion 8.1 als Version 6.3 gemeldet (anstelle von 8.1). Wenn die Betriebssystem-Versionsregel für Windows auf die Version Windows 8.1 festgelegt ist, wird das betreffende Gerät als nicht kompatibel gemeldet, selbst wenn auf ihm Windows 8.1 installiert ist. Stellen Sie deshalb sicher, dass Sie in den Regeln für das minimal oder maximal zulässige Betriebssystem die richtige *gemeldete* Version von Windows festlegen. Die Versionsnummer muss derjenigen entsprechen, die durch den **winver**-Befehl zurückgegeben wird. Bei Windows Phones tritt dieses Problem nicht auf. Dort wird als Version wie erwartet 8.1 gemeldet. Für Windows-PCs mit dem Betriebssystem Windows 10 muss die Version auf **10.0** plus OS-Buildnummer festgelegt werden, die vom Befehl **winver** zurückgegeben wird.

7.  Überprüfen Sie auf der Seite **Zusammenfassung** des Assistenten die von Ihnen festgelegten Einstellungen, und schließen Sie dann den Assistenten ab.

 Die neue Richtlinie wird im Knoten **Kompatibilitätsrichtlinien** im Arbeitsbereich **Bestand und Kompatibilität** angezeigt.

## <a name="deploy-a-compliance-policy"></a>Bereitstellen einer Konformitätsrichtlinie

1.  Wählen Sie in der Configuration Manager-Konsole **Assets und Konformität** aus.

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, und wählen Sie **Kompatibilitätsrichtlinien**.

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** die Option **Bereitstellen** aus.

4.  Wählen Sie im Dialogfeld **Kompatibilitätsrichtlinien bereitstellen** die Option **Durchsuchen**, um die Benutzersammlung auszuwählen, für die Sie die Richtlinie bereitstellen möchten.

     Darüber hinaus können Sie Optionen auswählen, um Warnungen zu generieren, wenn die Richtlinie nicht konform ist, und Sie können den Zeitplan festlegen, gemäß dem diese Richtlinie auf Konformität ausgewertet wird.

5.  Wählen Sie abschließend **OK** aus.

## <a name="monitor-the-compliance-policy"></a>Überwachen der Konformitätsrichtlinie

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>So zeigen Sie Konformitätsergebnisse in der Configuration Manager-Konsole an

1.  Wählen Sie in der Configuration Manager-Konsole die Option **Überwachung** aus.

2.  Wählen Sie im Arbeitsbereich **Überwachung** die Option **Bereitstellungen**.

3.  Wählen Sie in der Liste **Bereitstellungen** die Kompatibilitätsrichtlinienbereitstellung aus, für die Sie die Kompatibilitätsinformationen prüfen möchten.

4.  Zusammenfassende Informationen zur Kompatibilität der Richtlinienbereitstellung finden Sie auf der Hauptseite. Wählen Sie zum Anzeigen ausführlicherer Informationen die Bereitstellung aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Status anzeigen**, um die Seite **Bereitstellungsstatus** anzuzeigen.

    Die Seite **Bereitstellungsstatus** enthält die folgenden Registerkarten:

    -   **Konform**: Zeigt die Konformität der Richtlinie basierend auf der Anzahl der betroffenen Objekte an. Sie können eine Regel wählen, um unter dem Knoten **Benutzer** oder **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer oder Geräte enthalten sind, die mit dieser Regel kompatibel sind. Im Bereich **Bestandsdetails** werden die Benutzer oder Geräte angezeigt, die mit der Richtlinie kompatibel sind. Um zusätzliche Informationen anzuzeigen, doppelklicken Sie auf einen Benutzer oder ein Gerät in der Liste.

    -   **Fehler**: Zeigt eine Liste aller Fehler für die ausgewählte Richtlinienbereitstellung basierend auf der Anzahl der betroffenen Objekte an. Sie können eine Regel wählen, um unter dem Knoten **Benutzer** oder **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer oder Geräte enthalten sind, durch die mit dieser Regel Fehler generiert wurden. Wenn Sie einen Benutzer oder ein Gerät auswählen, werden im Bereich **Bestandsdetails** die Benutzer oder Geräte angezeigt, die von einem Problem betroffen sind. Um weitere Informationen zum Problem anzuzeigen, doppelklicken Sie auf einen Benutzer oder ein Gerät in der Liste.

    -   **Nicht konform**: Zeigt eine Liste aller nicht konformen Regeln innerhalb der Richtlinie basierend auf der Anzahl der betroffenen Objekte an. Sie können eine Regel wählen, um unter dem Knoten **Benutzer** oder **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer oder Geräte enthalten sind, die mit dieser Regel nicht kompatibel sind. Wenn Sie einen Benutzer oder ein Gerät auswählen, werden im Bereich **Bestandsdetails** die Benutzer oder Geräte angezeigt, die von einem Problem betroffen sind. Um weitere Informationen zu diesem Problem anzuzeigen, doppelklicken Sie auf einen Benutzer oder ein Gerät in der Liste.

    -   **Unbekannt**: Zeigt eine Liste aller Benutzer und Geräte an, für die keine Konformität mit der ausgewählten Richtlinienbereitstellung zusammen mit dem aktuellen Clientstatus von Geräten gemeldet wurde.

#### <a name="to-monitor-the-compliance-status-of-an-individual-device"></a>So überwachen Sie den Konformitätsstatus eines einzelnen Geräts

1.  Wählen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Bestand und Konformität**.

2.  Wählen Sie **Geräte**.

3. Um mehr Spalten zu aktivieren, klicken Sie mit der rechten Maustaste auf eine der Spalten.

  Sie können die folgenden Spalten hinzufügen:

  - **Azure Active Directory-Geräte-ID**: Der eindeutige Bezeichner für das Gerät in Azure Active Directory.

  - **Konformität: Fehlerdetails**: Details der Fehlermeldung, wenn der Prozess einen Fehler auslöst. Wenn diese Spalte leer ist, bedeutet dies, dass keine Fehler gefunden wurden und der Konformitätsstatus erfolgreich gemeldet wurde.

  - **Konformität: Fehlerort**: Weitere Details dazu, an welcher Stelle der Fehler ausgelöst wurde. Wenn diese Spalte leer ist, bedeutet dies, dass keine Fehler gefunden wurden und der Konformitätsstatus erfolgreich gemeldet wurde. Beispiele, wo ein Fehler im Kompatibilitätsprozess auftreten könnte: 
      - ConfigMgr-Client
      - Verwaltungspunkt
      - Intune
      - Azure Active Directory
<br></br>
  - **Konformität: Zeitpunkt der Auswertung**: Letzte Überprüfung der Konformität.

  - **Konformität: Zeitpunkt der Festlegung**: Letztes Konformitätsupdate mit Azure Active Directory.

  - **Konform mit bedingtem Zugriff**: Gibt an, ob der Computer mit bedingten Zugriffsrichtlinien konform ist.

  > [!IMPORTANT]
  > Diese Spalten werden standardmäßig nicht angezeigt.

#### <a name="to-view-intune-compliance-policies-charts"></a>Anzeigen von Diagrammen zu Konformitätsrichtlinien von Intune
1. Wählen Sie in der Configuration Manager-Konsole die Option **Überwachung** aus.

2. Wechseln Sie im Arbeitsbereich **Überwachung** zu **Übersicht** > **Konformitätseinstellungen** > **Konformitätsrichtlinien**.

   Die folgenden Diagramme werden angezeigt:

    - **Gerätekonformität insgesamt**: Zeigt die Gesamtkonformität von Geräten für alle Konformitätsrichtlinien.
    - **Hauptgründe für Nichtkonformität**: Zeigt die häufigsten Richtlinien an, mit denen Geräte nicht konform sind.

3. Wählen Sie einen Bereich in einem beliebigen Diagramm, um einen Drilldown zu einer Liste der Geräte innerhalb dieser Kategorie auszuführen.

#### <a name="to-view-a-health-attestation-report"></a>So zeigen Sie einen Integritätsnachweisbericht an

1. Wählen Sie in der Configuration Manager-Konsole die Option **Überwachung** aus.

2.  Wählen Sie zum Anzeigen eines Übersichtsberichts mit dem aktuellen Status von Geräten, angeordnet nach Konformitätsstatus, **Sicherheit** und anschließend **Integritätsnachweis**.

3.  Wählen Sie zum Anzeigen eines Berichts, in dem alle Geräte und die Integritätsnachweisattribute aufgeführt sind, **Sicherheit** und anschließend **Integritätsnachweis**.

## <a name="compliance-policy-rules"></a>Regeln für Kompatibilitätsrichtlinien
* **Kennworteinstellungen auf mobilen Geräten erforderlich**: Sie können festlegen, dass Benutzer ein Kennwort eingeben müssen, bevor sie auf ihr Gerät zugreifen können.

  **Unterstützt auf:**
    * Windows Phone 8+
    * iOS 6+
    * Android 4.0+
    * Samsung KNOX Standard 4.0+

* **Kennwort zum Entsperren eines inaktiven Geräts anfordern**: Sie können festlegen, dass Benutzer für den Zugriff auf ein gesperrtes Gerät ein Kennwort benötigen.

  **Unterstützt auf:**
  * Windows Phone 8+
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Minuten Inaktivität vor Anforderung des Kennworts**: Gibt die Leerlaufzeit an, bevor der Benutzer sein Kennwort erneut eingeben muss. Legen Sie den Wert auf eine der verfügbaren Optionen fest: **1 Minute**, **5 Minuten**, **15 Minuten**, **30 Minuten**, **1 Stunde**.

  Diese Regel muss mit der Option **Kennwort zum Entsperren eines inaktiven Geräts anfordern** verwendet werden. Der hier festgelegte Wert bestimmt, wann das Gerät als inaktiv betrachtet und gesperrt wird. Wenn **Kennwort zum Entsperren eines inaktiven Geräts anfordern** auf **True** gesetzt ist, muss der Benutzer ein Kennwort für den Zugriff auf das gesperrte Gerät eingeben.

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows RT/8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Automatische Updates erforderlich**: Sie können angeben, dass Updates auf Geräten mit Windows 8.1 oder höher automatisch installiert werden sollen, und Sie können die Update-Klasse angeben.

  Der Wert sollte auf **Keine** festgelegt werden, um die automatische Installation zu verhindern. Bei **Empfohlen** werden alle empfohlenen Updates automatisch installiert. Um nur Updates zu installieren, die als wichtig eingestuft werden, legen Sie den Wert auf **Wichtig** fest.

  **Unterstützt auf:**
  * Windows Phone 8+

* **Einfache Kennwörter zulassen**: Sie können zulassen, dass Benutzer einfache Kennwörter wie „1234“ oder „1111“ verwenden. Diese Einstellung ist standardmäßig deaktiviert.

  **Unterstützt auf:**
  * Windows Phone 8+
  * iOS 6+

* **Minimale Kennwortlänge**: Sie können die Mindestanzahl an Ziffern oder Zeichen angeben, die das Benutzerkennwort enthalten muss (standardmäßig 6).

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

  >[!NOTE]
  >Für Geräte, die Windows ausführen und mit einem Microsoft-Konto gesichert sind, ist keine korrekte Auswertung mit der Konformitätsrichtlinie möglich, wenn **Minimale Kennwortlänge** größer als 8 Zeichen oder die **Minimale Anzahl von Zeichensätzen:** größer als 2 ist.

* **Dateiverschlüsselung auf mobilem Gerät**: Sie können festlegen, dass das Gerät verschlüsselt sein muss, um eine Verbindung mit Ressourcen herstellen zu können. Geräte unter Windows Phone 8 werden automatisch verschlüsselt. Geräte unter iOS werden verschlüsselt, wenn Sie die Einstellung **Kennworteinstellungen auf mobilen Geräte erforderlich**konfigurieren. Diese Einstellung ist standardmäßig aktiviert.

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Device must not be jailbroken or rooted** (Gerät darf nicht per Jailbreak oder Rooting manipuliert worden sein): Wenn Sie diese Einstellung aktivieren, sind Geräte mit Jailbreak oder gerootete Geräte (iOS bzw. Android) nicht konform. Diese Einstellung ist standardmäßig deaktiviert.

  **Unterstützt auf:**
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **E-Mail-Profil muss von Intune verwaltet sein**: Wenn diese Option auf **Ja** festgelegt ist, muss das Gerät das E-Mail-Profil verwenden, das auf dem Gerät bereitgestellt wurde. Das Gerät gilt als nicht kompatibel, wenn das E-Mail-Profil nicht für dieselbe Benutzergruppe bereitgestellt wird, für die die Kompatibilitätsrichtlinie gilt.

  Es wird ebenso als nicht kompatibel gemeldet, wenn der Benutzer bereits ein E-Mail-Konto auf dem Gerät eingerichtet hat, das mit dem Intune-E-Mail-Profil übereinstimmt, das auf dem Gerät bereitgestellt wurde. Intune kann das vom Benutzer bereitgestellte Profil in diesem Fall nicht überschreiben und daher nicht verwalten. Der Benutzer kann die Konformität seines Geräts herstellen, indem er die vorhandene E-Mail-Einstellung entfernt, sodass Intune das verwaltete E-Mail-Profil installieren kann.

  Weitere Informationen zu E-Mail-Profilen finden Sie unter [Aktivieren des Zugriffs auf Unternehmens-E-Mail mithilfe von E-Mail-Profilen in Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx). Diese Einstellung ist standardmäßig deaktiviert.

  **Unterstützt auf:**
  * iOS 6+

* **E-Mail-Profil**: Wenn **E-Mail-Konto muss von Intune verwaltet sein.** aktiviert ist, klicken Sie auf **Auswählen**, um das E-Mail-Profil auszuwählen, von dem Geräte verwaltet werden müssen. Das E-Mail-Profil muss auf dem Gerät vorhanden sein.

  **Unterstützt auf:**
  * iOS 6+

* **Minimum OS required** (Erforderliche Mindestversion des Betriebssystems): Wenn ein Gerät die von Ihnen festgelegten Minimalanforderungen an die Betriebssystemversion nicht erfüllt, wird es als nicht konform gemeldet. Ein Link mit Informationen zur Vorgehensweise beim Upgraden wird angezeigt. Die Benutzer können ein Upgrade des Geräts durchführen und anschließend auf die Unternehmensressourcen zugreifen.

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Maximum OS version allowed** (Höchste zulässige Version des Betriebssystems): Wenn ein Gerät eine neuere Betriebssystemversion verwendet, als Sie in der Regel festlegen, wird der Zugriff auf Unternehmensressourcen gesperrt, und der Benutzer wird gebeten, sich an den IT-Administrator zu wenden. Solange Sie die Regel nicht ändern und die betreffende Betriebssystemversion zulassen, kann das Gerät nicht auf Unternehmensressourcen zugreifen.

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Geräte müssen als fehlerfrei gemeldet werden**: Sie können eine Regel festlegen, die anfordert, dass Windows 10-Geräte in neuen oder vorhandenen Konformitätsrichtlinien als fehlerfrei gemeldet werden müssen. Wenn Sie diese Einstellung aktivieren, werden Windows 10-Geräte vom Integritätsnachweisdienst (Health Attestation Service, HAS) auf die folgenden Kriterien untersucht:

  - **BitLocker is enabled** (BitLocker aktiviert): Wenn Bitlocker aktiviert ist, kann das Gerät Daten, die auf dem Laufwerk gespeichert sind, vor unbefugtem Zugriff schützen, wenn das Gerät ausgeschaltet wird oder in den Ruhezustand wechselt.

   Die Windows BitLocker-Laufwerkverschlüsselung verschlüsselt alle Daten, die auf dem Windows-Betriebssystemvolume gespeichert sind. BitLocker verwendet das TPM, um Windows-Betriebssystem und Benutzerdaten zu schützen. TPM stellt sicher, dass ein Computer auch dann nicht manipuliert wird, wenn er unbeaufsichtigt gelassen, verloren oder gestohlen wird.
   
   Wenn der Computer mit einem kompatiblen TPM ausgestattet ist, verwendet BitLocker das TPM zum Sperren der Verschlüsselungsschlüssel, die die Daten schützen. Daher kann erst auf die Schlüssel zugegriffen werden, nachdem das TPM den Zustand des Computers überprüft hat.

  - **Code integrity is enabled** (Codeintegrität aktiviert): Die Codeintegrität ist ein Feature zum Überprüfen der Integrität von Treibern oder Systemdateien, sobald diese in den Speicher geladen werden. Codeintegrität erkennt, ob ein nicht signierter Treiber oder eine nicht signierte Systemdatei in den Kernel geladen wird. Außerdem wird erkannt, ob eine Systemdatei durch böswillige, von einem Benutzerkonto mit Administratorrechten ausgeführte Software geändert wurde.

  - **Secure boot is enabled** (Sicherer Start aktiviert): Wenn der sichere Start aktiviert ist, wird das System gezwungen, in einem vom Hersteller als vertrauenswürdig eingestuften Zustand zu starten. Bei aktiviertem sicheren Start müssen auch die Kernkomponenten, die zum Starten des Computers verwendet werden, über ordnungsgemäße kryptografische Signaturen verfügen, denen das Unternehmen vertraut, das das Gerät hergestellt hat. Die UEFI-Firmware überprüft dies, bevor sie den Computer starten lässt. Wenn Dateien so manipuliert wurden, dass ihre Signatur nicht mehr stimmt, startet das System nicht.

  - **Early-launch antimalware is enabled** (Frühstart von Antischadsoftware aktiviert): Diese Einstellung gilt nur für PCs. Dieses Feature bietet Schutz für Computer in Ihrem Netzwerk, sobald diese gestartet und bevor Treiber von Drittanbietern initialisiert werden.
  
   Diese Regel ist standardmäßig deaktiviert.

  Informationen zur Funktionsweise des Integritätsnachweisdiensts finden Sie unter [HealthAttestation CSP](https://msdn.microsoft.com/library/dn934876.aspx)(HealthAttestation-Kryptografiedienstanbieter).

  **Unterstützt auf:**
  * Windows 10 und Windows 10 Mobile

> [!NOTE]
> Ab Configuration Manager 1802 wird im Softwarecenter das Element „Integritätsnachweis“ angezeigt, mit dem das Gerät nicht konform ist. <!--1235616--> 
![Gerätekonformität „Geräteintegritätsnachweis“ im Softwarecenter](./media/Software-Center-noncompliant.PNG)


- **Apps that cannot be installed on the device** (Apps, die auf dem Gerät nicht installiert werden können): Wenn Benutzer Apps installieren, die sich auf der Administratorliste der nicht konformen Apps befinden, werden diese blockiert, wenn versucht wird, auf geschäftliche E-Mails oder auf andere Geschäftsressourcen zuzugreifen, die den bedingten Zugriff unterstützen. Für diese Regel wird der Name der App benötigt; wenn Sie eine App auf diese Administratorliste der nicht kompatiblen Apps setzen möchten, benötigen Sie dafür zusätzlich die App-ID. Ebenso kann der App-Herausgeber hinzugefügt werden; dies ist jedoch nicht zwingend notwendig.

    **Unterstützt auf:**
      * iOS 6+
      * Android 4.0+
      * Samsung KNOX Standard 4.0+
<br></br>
* **Erforderlicher Kennworttyp**:Legen Sie fest, ob Benutzer ein alphanumerisches oder numerisches Kennwort erstellen müssen. Bei alphanumerischen Kennwörtern legen Sie außerdem die erforderliche Mindestzahl an Zeichen fest. Die vier Zeichengruppen sind Kleinbuchstaben, Großbuchstaben, Symbole und Zahlen.

    **Unterstützt auf:**
    * Windows Phone 8+
    * Windows 8.1+
    * iOS 6+
<br></br>
* **USB-Debugging auf Gerät blockieren**: Sie müssen diese Einstellungen nicht konfigurieren, da USB-Debuggen auf Android for Work-Geräten bereits deaktiviert ist.

    **Unterstützt auf:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Apps von unbekannten Quellen blockieren**: Legen Sie fest, dass Geräte die Installation von Apps aus unbekannten Quellen verhindern müssen. Sie müssen diese Einstellung nicht konfigurieren, da Android for Work-Geräte die Installation aus unbekannten Quellen stets einschränken.

    **Unterstützt auf:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Bedrohungsüberprüfung für Apps erzwingen**: Diese Einstellung gibt an, dass das Feature zum Überprüfen von Apps auf dem Gerät aktiviert ist. 

    **Unterstützt auf:**
    * Android 4.2 bis 4.4
    * Samsung KNOX Standard 4.0+

### <a name="find-an-app-id"></a>Finden einer App-ID

Eine App-ID ist ein Bezeichner, der die App in den Anwendungsdiensten Apple und Google eindeutig identifiziert. Ein Beispiel ist „com.contoso.myapp“. So finden Sie eine:

- **Android**
    - Die App-ID finden Sie in der URL des Google Play Stores, die für die Erstellung der App verwendet wurde. Eine Beispiel-App-ID ist: *…?id=com.companyname.appname&hl=en*.

- **iOS**
    1. In der URL des iTunes-Stores finden Sie die ID-Nummer, Beispiel: */id875948587?mt=8*.

    2. Wechseln Sie in einem Webbrowser zur folgenden URL, und ersetzen Sie die Nummer durch die ID-Nummer, die Sie gerade gefunden haben (in diesem Fall im vorherigen Beispiel): https://itunes.apple.com/lookup?id=875948587.

    3. Laden Sie die Textdatei herunter und öffnen Sie sie.
  
    4. Suchen Sie nach dem Text **bundleId**.

    Eine Beispiel-App-ID ist: „*bundleId*“:„*com.companyname.appname*“. 

