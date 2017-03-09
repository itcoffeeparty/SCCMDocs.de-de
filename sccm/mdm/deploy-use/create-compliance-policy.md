---
title: "Erstellen und Bereitstellen einer Gerätekonformitätsrichtlinie | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Sie eine Gerätekonformitätsrichtlinie in System Center Configuration Manager erstellen und bereitstellen."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
robots: noindex
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 58375a7f23109bbb2e304c17312f3438aa683cb2
ms.lasthandoff: 03/06/2017

---

# <a name="create-and-deploy-a-device-compliance-policy"></a>Erstellen und Bereitstellen einer Gerätekonformitätsrichtlinie

*Gilt für: System Center Configuration Manager (Current Branch)*


## <a name="create-a-compliance-policy"></a>Erstellen einer Konformitätsrichtlinie

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, und klicken Sie auf **Kompatibilitätsrichtlinien**.

3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Kompatibilitätsrichtlinie erstellen**.

4. Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Kompatibilitätsrichtlinien ** **die folgenden Informationen an:

  * **Name:** Geben Sie einen eindeutigen Namen für die Konformitätsrichtlinie ein. Sie können maximal 256 Zeichen verwenden.
  * **Beschreibung:** Geben Sie eine Beschreibung ein, die Ihnen einen Überblick über das VPN-Profil verschafft und dabei behilflich ist, das Profil in der Configuration Manager-Konsole zu ermitteln. Sie können maximal 256 Zeichen verwenden.
  * **Kompatibilitätsrichtlinientyp:** Wählen Sie den Richtlinientyp, den Sie erstellen möchten, auf Grundlage der Tatsache aus, ob Ihr Gerät von Configuration Manager verwaltet wird. **Dies trifft auf Version oder höher zu**.<br /><br /> Wählen Sie für Geräte, die von Intune verwaltet werden, die Option **Compliance rules for devices managed without configuration manager client** (Kompatibilitätsregeln für Geräte, die ohne den Configuration Manager-Client verwaltet werden).  Bei Wahl dieser Option können Sie auch den Typ der Plattform auswählen, dem Sie diese Richtlinie zuweisen möchten.
  * **Schweregrad der Nichtkompatibilität für Berichte:** Geben Sie den Schweregrad an, der gemeldet wird, wenn diese Kompatibilitätsrichtlinie als nicht kompatibel ausgewertet wird. Die folgenden Schweregrade sind verfügbar:<br /><br />
    * **Keine** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.
    *  **Information** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.   
    * **Warnung** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.
    * **Kritisch** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.
    * **Kritisch mit Ereignis** – Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.      

5.  Wählen Sie auf der Seite **Unterstützte Plattformen** die Geräteplattformen, für die diese Kompatibilitätsrichtlinie ausgewertet wird, oder klicken Sie auf **Alle auswählen** , um alle Geräteplattformen auszuwählen.

6.  Auf der Seite **Regeln** definieren Sie eine oder mehrere Regeln, die die Konfiguration bestimmen, die Geräte aufweisen müssen, um als kompatibel eingestuft zu werden. Wenn Sie eine Kompatibilitätsrichtlinie erstellen, sind einige Regeln standardmäßig aktiviert, die Sie aber bearbeiten oder löschen können. Eine vollständige Liste aller Regeln finden Sie unter **Regeln für Kompatibilitätsrichtlinien** weiter unten in diesem Thema.

> [!NOTE]  
>  Auf Windows-PCs wird die Windows-Betriebssystemversion 8.1 als Version 6.3 gemeldet (anstelle von 8.1).    Wenn die Betriebssystem-Versionsregel für Windows auf die Version Windows 8.1 festgelegt ist, wird das betreffende Gerät als nicht kompatibel gemeldet, selbst wenn auf ihm Windows 8.1 installiert ist. Stellen Sie deshalb sicher, dass Sie in den Regeln für das minimal oder maximal zulässige Betriebssystem die richtige **gemeldete** Version von Windows festlegen. Die Versionsnummer muss derjenigen entsprechen, die durch den winver-Befehl zurückgegeben wird. Bei Windows Phones tritt dieses Problem nicht auf. Dort wird als Version wie erwartet 8.1 gemeldet.  
>   
>  Bei Windows-PCs mit dem Betriebssystem Windows 10 muss die Version auf „10.0“ plus OS-Buildnummer festgelegt werden, die vom Befehl „winver“ zurückgegeben wird. Beispiel: 10.0.10586.  
> Bei Windows 10 Mobile gibt es dieses Problem nicht.  
>   
>  ![CA&#95;Win10OSversion](media/CA_Win10OSversion.png)  

7.  Überprüfen Sie auf der Seite **Zusammenfassung** des Assistenten die von Ihnen festgelegten Einstellungen, und schließen Sie dann den Assistenten ab.

 Die neue Richtlinie wird im Knoten **Kompatibilitätsrichtlinien** im Arbeitsbereich **Bestand und Kompatibilität** angezeigt.

## <a name="deploy-a-compliance-policy"></a>Bereitstellen einer Konformitätsrichtlinie

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, und klicken Sie auf **Kompatibilitätsrichtlinien**.

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.

4.  Klicken Sie im Dialogfeld **Kompatibilitätsrichtlinien bereitstellen** auf **Durchsuchen** , um die Benutzersammlung auszuwählen, für die Sie die Richtlinie bereitstellen möchten.

     Darüber hinaus können Sie Optionen auswählen, um Warnungen zu generieren, wenn die Richtlinie nicht befolgt wird. Sie können auch den Zeitplan konfigurieren, gemäß dem diese Richtlinie auf Kompatibilität ausgewertet wird.

5.  Klicken Sie abschließend auf **OK**.

## <a name="monitor-the-compliance-policy"></a>Überwachen der Konformitätsrichtlinie

### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>So zeigen Sie Kompatibilitätsergebnisse in der Configuration Manager-Konsole an

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.

2.  Klicken Sie im Arbeitsbereich **Überwachung** auf **Bereitstellungen**.

3.  Wählen Sie in der Liste **Bereitstellungen** die Kompatibilitätsrichtlinienbereitstellung aus, für die Sie die Kompatibilitätsinformationen prüfen möchten.

4.  Zusammenfassende Informationen zur Kompatibilität der Richtlinienbereitstellung finden Sie auf der Hauptseite. Wählen Sie zum Anzeigen ausführlicherer Informationen die Bereitstellung aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Status anzeigen** , um die Seite **Bereitstellungsstatus** anzuzeigen.

     Auf der Seite **Bereitstellungsstatus** sind die folgenden Registerkarten enthalten:

    -   **Kompatibel**: Zeigt die Kompatibilität mit der Richtlinie basierend auf der Anzahl der betroffenen Bestände an. Sie können auf eine Regel klicken, um unter dem Knoten **Benutzer** oder **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer oder Geräte enthalten sind, die mit dieser Regel kompatibel sind. Im Bereich **Bestandsdetails** werden die Benutzer oder Geräte angezeigt, die mit der Richtlinie kompatibel sind. Doppelklicken Sie auf einen Benutzer oder ein Gerät in der Liste, um weitere Informationen anzuzeigen.

    -   **Fehler**: Zeigt eine Liste aller Fehler für die ausgewählte Bereitstellung der Richtlinie basierend auf der Anzahl der betroffenen Bestände an. Sie können auf eine Regel klicken, um unter dem Knoten **Benutzer** oder **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer oder Geräte enthalten sind, durch die mit dieser Regel Fehler generiert wurden. Wenn Sie einen Benutzer oder ein Gerät auswählen, werden im Bereich **Bestandsdetails** die Benutzer oder Geräte angezeigt, die vom ausgewählten Problem betroffen sind. Doppelklicken Sie auf einen Benutzer oder ein Gerät in der Liste, um weitere Informationen zum Problem anzuzeigen.

    -   **Nicht kompatibel**: Zeigt eine Liste aller nicht kompatiblen Regeln innerhalb der Richtlinie basierend auf der Anzahl der betroffenen Bestände an. Sie können auf eine Regel klicken, um unter dem Knoten **Benutzer** oder **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer oder Geräte enthalten sind, die nicht mit dieser Regel kompatibel sind. Wenn Sie einen Benutzer oder ein Gerät auswählen, werden im Bereich **Bestandsdetails** die Benutzer oder Geräte angezeigt, die vom ausgewählten Problem betroffen sind. Doppelklicken Sie auf einen Benutzer oder ein Gerät in der Liste, um weitere Informationen zu diesem Problem anzuzeigen.

    -   **Unbekannt**: Zeigt eine Liste aller Benutzer und Geräte an, für die keine Kompatibilität mit der ausgewählten Richtlinienbereitstellung zusammen mit dem aktuellen Clientstatus von Geräten gemeldet wurde.

### <a name="to-view-intune-compliance-policies-charts"></a>Anzeigen von Diagrammen zu Konformitätsrichtlinien von Intune
1. Klicken Sie ab Version 1610 von Configuration Manager in der Configuration Manager-Konsole auf **Überwachung**.
2. Wechseln Sie im Arbeitsbereich **Überwachung** zu **Übersicht** > **Konformitätseinstellungen** >  **Konformitätsrichtlinien**.
3. Die folgenden Diagramme werden angezeigt:
    - **Overall Device Compliance**: (Allgemeine Gerätekonformität) Zeigt die Gesamtkonformität von Geräten für alle Konformitätsrichtlinien.
    - **Top Non-Compliance Reasons**: (Häufigste Gründe für Nichtkonformität) Zeigt die häufigsten Richtlinien an, mit denen Geräte nicht konform sind.
4. Klicken Sie einen Bereich im Diagramm an, um einen Drilldown zu einer Liste der Geräte innerhalb dieser Kategorie auszuführen.

### <a name="to-view-a-health-attestation-report"></a>So zeigen Sie einen Integritätsnachweisbericht an

1.  Klicken Sie ab **Version 1602 von Configuration Manager** in der Configuration Manager-Konsole auf **Überwachung**.

2.  Klicken Sie zum Anzeigen eines Übersichtsberichts mit dem aktuellen Status von Geräten, angeordnet nach Kompatibilitätsstatus, auf **Sicherheit** und anschließend auf **Integritätsnachweis**.

3.  Klicken Sie zum Anzeigen eines Berichts, in dem alle Geräte und die Integritätsnachweisattribute aufgeführt sind, auf **Sicherheit** und anschließend auf **Integritätsnachweis**.

## <a name="compliance-policy-rules"></a>Regeln für Kompatibilitätsrichtlinien
* **Kennworteinstellungen auf mobilen Geräten erforderlich:** Legen Sie fest, dass Benutzer ein Kennwort eingeben müssen, bevor sie auf ihr Gerät zugreifen können.

  **Unterstützt auf:**
    * Windows Phone 8+
    * iOS 6+
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
* **Kennwort zum Entsperren eines inaktiven Geräts anfordern (Update&1602;):** Legen Sie fest, dass Benutzer für den Zugriff auf ein gesperrtes Gerät ein Kennwort benötigen.

  **Unterstützt auf:**
  * Windows Phone 8+
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Minuten Inaktivität vor Anforderung des Kennworts (Update&1602;):** Gibt die Leerlaufzeit an, bevor der Benutzer sein Kennwort erneut eingeben muss. Legen Sie den Wert auf eine der verfügbaren Optionen fest: **1 Minute**, **5 Minuten**, **15 Minuten**, **30 Minuten**, **1 Stunde**.

  Diese Regel muss mit der Option **Kennwort zum Entsperren eines inaktiven Geräts anfordern**verwendet werden. Der hier festgelegte Wert bestimmt, wann das Gerät als inaktiv betrachtet und gesperrt wird. Wenn  **Kennwort zum Entsperren eines inaktiven Geräts anfordern** auf **TRUE**festgelegt ist, muss der Benutzer ein Kennwort eingeben, um auf das gesperrte Geräte zuzugreifen.

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows RT/8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Automatische Updates erforderlich (Update 1602):** Sie können angeben, dass Geräte mit Windows 8.1 oder höher Updates automatisch installieren sollen, und Sie können die Update-Klasse angeben.

  Der Wert sollte auf **Kein** festgelegt werden, um eine automatische Installation zu verhindern, auf **Empfohlen** , um alle empfohlenen Updates automatisch zu installieren oder auf **Wichtig** , um nur Updates zu installieren, die als wichtig eingestuft wurden.

  **Unterstützt auf:**
  * Windows Phone 8+

* **Einfache Kennwörter zulassen:** Erlauben Sie, dass Benutzer einfache Kennwörter wie „1234“ oder „1111“ verwenden können. Diese Einstellung ist **standardmäßig deaktiviert**.

  **Unterstützt auf:**
  * Windows Phone 8+
  * iOS 6+

* **Minimale Kennwortlänge:** Gibt die Mindestanzahl an Ziffern oder Zeichen an, die das Benutzerkennwort enthalten muss (standardmäßig **6**).

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  >[!NOTE]
  >Für Geräte, die Windows ausführen und mit einem Microsoft-Konto gesichert sind, ist keine korrekte Auswertung mit der Konformitätsrichtlinie möglich, wenn **Minimale Kennwortlänge** größer als 8 Zeichen oder die **Minimale Anzahl von Zeichensätzen:** größer als 2 ist.

* **Dateiverschlüsselung auf mobilem Gerät:** Verlangt für eine Verbindungsherstellung mit Ressourcen, dass das Gerät verschlüsselt ist. Geräte unter **Windows Phone 8** werden **automatisch verschlüsselte**. Geräte unter **iOS** werden verschlüsselt, wenn Sie die Einstellung **Kennworteinstellungen auf mobilen Geräten erforderlich** (standardmäßig aktiviert) konfigurieren.

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Gerät darf keinen Jailbreak oder Rootzugriff verwenden:** Geräte, die mit Jailbreak (iOS) oder Rooting (Android) manipuliert wurden, sind nicht kompatibel (standardmäßig deaktiviert).

  **Unterstützt auf:**
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **E-Mail-Profil muss von Intune verwaltet sein:** Wenn diese Option auf „Ja“ festgelegt ist, muss das Gerät das E-Mail-Profil verwenden, das auf demselben Gerät bereitgestellt wurde. Das Gerät gilt als nicht kompatibel, wenn das E-Mail-Profil nicht für dieselbe Benutzergruppe bereitgestellt wird, für die die Kompatibilitätsrichtlinie gilt.

  Es wird ebenso als nicht kompatibel gemeldet, wenn der Benutzer bereits ein E-Mail-Konto auf dem Gerät eingerichtet hat, das mit dem Intune-E-Mail-Profil übereinstimmt, das auf dem Gerät bereitgestellt wurde. Intune kann das vom Benutzer bereitgestellte Profil in diesem Fall nicht überschreiben und daher nicht verwalten. Der Benutzer kann die Kompatibilität seines Geräts herstellen, indem er die vorhandenen E-Mail-Einstellungen entfernt, wodurch es Intune gestattet wird, das verwaltete E-Mail-Profil zu installieren.

  Weitere Informationen zu E-Mail-Profilen finden Sie unter [Aktivieren des Zugriffs auf Unternehmens-E-Mail mithilfe von E-Mail-Profilen in Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx). Diese Einstellung ist standardmäßig deaktiviert.

  **Unterstützt auf:**
  * iOS 6+

* **E-Mail-Profil:** Wenn **E-Mail-Profil muss von Intune verwaltet sein** aktiviert ist, klicken Sie auf **Auswählen**, um das E-Mail-Profil auszuwählen, von dem Geräte verwaltet werden müssen. Das E-Mail-Profil muss auf dem Gerät vorhanden sein.

  **Unterstützt auf:**
  * iOS 6+

* **Minimum OS required** (Minimales Betriebssystem erforderlich): Wenn ein Gerät die minimalen Anforderungen an die erforderliche Betriebssystemversion nicht erfüllt, wird es als nicht kompatibel gemeldet. Es wird ein Link zur Vorgehensweise beim Upgraden angezeigt. Die Endbenutzer können ein Upgrade des Gerätes durchführen und anschließend auf die Unternehmensressourcen zugreifen.

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Maximum OS version allowed** (Maximale erlaubte Betriebssystemversion): Wenn ein Gerät eine neuere Betriebssystemversion verwendet als die in der Richtlinie angegebene, wird der Zugriff auf Unternehmensressourcen gesperrt, und der Benutzer wird gebeten, sich an den IT-Administrator zu wenden. Mit diesem Gerät kann solange nicht auf Unternehmensressourcen zugegriffen werden, bis die Regel geändert und die betreffende Betriebssystemversion zugelassen wird.

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Geräte müssen als fehlerfrei gemeldet werden (Update 1602):** Sie können eine Regel festlegen, die anfordert, dass Windows 10-Geräte in neuen oder vorhandenen Kompatibilitätsrichtlinien als fehlerfrei gemeldet werden müssen. Wenn diese Einstellung aktiviert ist, werden Windows 10-Geräte vom Integritätsnachweisdienst auf die folgenden Kriterien untersucht:
 - **BitLocker is enabled** (BitLocker aktiviert): Wenn Bitlocker aktiviert ist, kann das Gerät Daten, die auf dem Laufwerk gespeichert sind, vor unbefugtem Zugriff schützen, wenn das Gerät ausgeschaltet wird oder in den Ruhezustand wechselt.

   Die Windows BitLocker-Laufwerkverschlüsselung verschlüsselt alle Daten, die auf dem Windows-Betriebssystemvolume gespeichert sind. BitLocker nutzt das TPM, um das Windows-Betriebssystem und Benutzerdaten zu schützen, und hilft sicherzustellen, dass ein Computer nicht manipuliert wird, selbst wenn er unbeaufsichtigt ist, verlorenen gegangen ist oder gestohlen wird.<br />Wenn der Computer mit einem kompatiblen TPM ausgestattet ist, verwendet BitLocker das TPM zum Sperren der Verschlüsselungsschlüssel, die die Daten schützen. Daher kann erst auf die Schlüssel zugegriffen werden, nachdem das TPM den Zustand des Computers überprüft hat.
  - **Code integrity is enabled** (Codeintegrität aktiviert): Die Codeintegrität ist ein Feature zum Überprüfen der Integrität von Treibern oder Systemdateien, sobald diese in den Arbeitsspeicher geladen werden. Codeintegrität erkennt, ob nicht signierte Treiber oder Systemdateien in den Kernel geladen werden oder ob eine Systemdatei durch böswillige Software geändert wurde, die von einem Benutzerkonto mit Administratorrechten ausgeführt wurde.
  - **Secure boot is enabled** (Sicherer Start aktiviert): Wenn der sichere Start aktiviert ist, wird das System gezwungen, in einem vom Hersteller als vertrauenswürdig eingestuften Zustand zu starten. Bei aktiviertem sicheren Start müssen auch die Kernkomponenten, die zum Starten des Computers verwendet werden, über ordnungsgemäße kryptografische Signaturen verfügen, denen das Unternehmen vertraut, das das Gerät hergestellt hat. Die UEFI-Firmware überprüft dies, bevor sie den Computer starten lässt. Wenn Dateien so manipuliert wurden, das ihre Signatur nicht mehr stimmt, startet das System nicht.
  - **Early-launch antimalware is enabled** (Antischadsoftware-Frühstartfeature aktiviert) (diese Einstellung gilt nur für PCs): Dieses Feature bietet Schutz für Computer in Ihrem Netzwerk, sobald diese gestartet und bevor Treiber von Drittanbietern initialisiert werden.<br />Diese Regel ist standardmäßig deaktiviert.

  Informationen zur Funktionsweise des Integritätsnachweisdiensts finden Sie unter [HealthAttestation CSP](https://msdn.microsoft.com/library/dn934876.aspx)(HealthAttestation-Kryptografiedienstanbieter).
  **Unterstützt auf:**
  * Windows 10 und Windows 10 Mobile

