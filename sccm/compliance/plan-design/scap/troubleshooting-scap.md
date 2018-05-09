---
title: Problembehandlung der SCAP-Erweiterungen
titleSuffix: Configuraton Manager
description: Importieren Sie die SCAP-Kompatibilitätseinstellungen als Konfigurationsbaselines, und exportieren Sie die Ergebnisse
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 05010d73916ac4c012c157a470ed98dce47fc747
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="troubleshoot-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Problembehandlung der SCAP-Erweiterungen für Microsoft System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> Dieses Feature wurde erstmals in Technical Preview Version 1803 als [Vorabfeature](/sccm/core/servers/manage/pre-release-features) eingeführt. Diese Vorabversion der SCAP-Erweiterungen kann unter allen derzeit unterstützten Versionen von Configuration Manager Current Branch und LTSB 1606 installiert werden. Die Installationsdatei befindet sich unter cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi ab Technical Preview Version 1803. 

Die SCAP Extensions für Microsoft System Center Configuration Manager sind auf das Arbeiten mit den SCAP-Datenströmen ausgelegt, die für das für SCAP überprüfte Tool mit ACS-Funktionalität zur Unterstützung von USGCB vorgesehen sind. In der Regel treten bei diesen USGCB-SCAP-Datenströmen, die von der NIST-Website heruntergeladen werden, keine Probleme auf.

Sollten jedoch Probleme auftreten, können Sie diese mithilfe der folgenden Methoden untersuchen und beheben:

- Stellen Sie sicher, dass die SCAP Extensions-Clientkomponenten (scmdcm.msi) auf allen Zielcomputern installiert sind.
- Überprüfen Sie die Protokolldateiausgabe des „Microsoft.Sces.ScapToDcm.exe“-Tools.
- Überprüfen Sie allgemeine Probleme und Lösungen bei Verwendung von SCAP Extensions.
- Wenden Sie sich bei Fragen oder Feedback zu SCAP Extensions an Microsoft.



## <a name="review-microsoftscesscaptodcmexe-tool-log"></a>Überprüfen des „Microsoft.Sces.ScapToDcm.exe“-Toolprotokolls

Das Tool „Microsoft.Sces.ScapToDcm.exe“ erstellt eine benutzerdefinierte benannte Protokolldatei, wenn der Parameter „–log“ angegeben wurde. Die Protokolldatei enthält Informationen zu den Ergebnissen der Ausführung des Tools „Microsoft.Sces.ScapToDcm.exe“. Die Protokolldatei enthält z.B. die Anzahl der Elemente in der XCCDF/DataStream-Eingabedatei, die beim Ausführen des Tools „Microsoft.Sces.ScapToDcm.exe“ ausgelassen oder übersprungen wurden.

Die folgende Tabelle listet einige der Informationen in der Protokolldatei und eine Beschreibung der einzelnen Typen von Informationen auf.

### <a name="description-of-information-found-in-microsoftscesscaptodcmexe-log-files"></a>Beschreibung der Informationen in „Microsoft.Sces.ScapToDcm.exe“-Protokolldateien

| Informationen zu | Beschreibung |
| --- | --- |
| Auslassen | Ein Element kann ausgelassen werden, wenn der Testtyp nicht unterstützt wird. |
| Überspringen |Die ID der OVAL-Definition gehört zu einer ungültigen Plattform. </br> </br> Auf die ID der OVAL-Definition wird nicht durch die XCCDF/DataStream-Eingabedatei verwiesen.</br> </br> Auf die ID des OVAL-Tests wird nicht durch die XCCDF/DataStream-Eingabedatei verwiesen. </br> </br> Die ID des XCCDF-Profils enthält keine @select-Anweisungen, die gleich 1 sind. </br> </br> Die ID des XCCDF-Profils enthält ein abstraktes Attribut, das auf "true" festgelegt ist. </br> </br> Die ID des XCCDF-Profils enthält keine qualifizierende Regel.|

## <a name="common-problems-and-solutions"></a>Allgemeine Probleme und Lösungen

Die folgende Tabelle enthält einige allgemeine Probleme und Lösungen, die Ihnen bei der Problembehandlung helfen.

Tabelle 1.6 Allgemeine Probleme und Lösungen

| Problem | Mögliche Lösung |
| --- | --- |
| Wenn für eine Baseline der Status **Fehler** oder **Unbekannt** angezeigt wird und IE den Bericht nicht anzeigen kann. Die IE-Meldung lautet &quot;Der Bericht ist entweder leer oder ungültig&quot; | Wählen Sie die Baseline aus, und klicken Sie auf **Auswerten**, um die Baseline erneut auszuführen. Warten Sie dann, um **Status „Kompatibel“**/**Aktualisierung „Letzte Auswertung“** zu überwachen. Nach der Aktualisierung des Datums der letzten Auswertung auf das aktuelle Datum samt Uhrzeit (was bedeutet, dass die Auswertung abgeschlossen wurde), wählen Sie die Baseline aus und zeigen den Bericht erneut an. Wenn Internet Explorer den Bericht weiterhin nicht anzeigen kann, kann dies bedeuten, dass die Baseline zu groß ist. Generieren Sie den Inhalt erneut unter Verwendung einer kleineren Batchgröße, um kleinere untergeordnete Baselines zu erstellen. Wenn dieses Problem für die übergeordneten Baselines geschieht, versuchen Sie stattdessen, die untergeordneten Baselines bereitzustellen. |
| Ich habe Gruppenrichtlinienobjekte (GPOs) erstellt, die die vorgeschriebenen USGCB-Einstellungen enthalten, und diese mit den Organisationseinheiten (OUs) verknüpft, die Computer mit Windows 7 enthalten. Dennoch wird in Kompatibilitätsberichten angegeben, dass einige der Einstellungen nicht richtig konfiguriert sind. | Es ist möglich, dass die Gruppenrichtlinienberechtigungen falsch sind oder nicht mit der richtigen Organisationseinheit verknüpft wurden. Es ist jedoch wahrscheinlicher, dass die neuen Einstellungen noch nicht wirksam geworden sind. Standardmäßig suchen Gruppenrichtlinien auf Clientcomputern, die zu einer Active Directory-Domäne gehören, alle 90 Minuten nach Aktualisierungen. Dies ist möglicherweise ein Grund, warum die Einstellungen scheinbar nicht angewendet wurden, auch wenn Sie die Richtlinien ordnungsgemäß konfiguriert haben. Ein weiterer zu beachtender Aspekt ist, dass viele Computereinstellungen einen Neustart erfordern, damit sie wirksam werden. Z.B. die Einstellung namens „**Systemkryptografie: FIPS-konformen Algorithmus für Verschlüsselung, Hashing und Signatur verwenden“ erfordert den Neustart des Computers, bevor Windows die angegebenen Verschlüsselungsalgorithmen verwenden kann. Sie können das Aktualisierungsintervall für Gruppenrichtlinien umgehen, indem Sie den folgenden Befehl in einer Eingabeaufforderung mit Administratorrechten eingeben: gpupdate/force Nach dem Abschluss der Aktualisierung der Gruppenrichtlinie starten Sie den Computer neu, um sicherzustellen, dass alle Einstellungen wirksam werden. Weitere Informationen finden Sie im Knowledge Base-Artikel 298444: [A Description of the Group Policy Update Utility (Eine Beschreibung des Updatehilfsprogramms der Gruppenrichtlinie)](http://support.microsoft.com/kb/298444). |
| Ich habe Probleme bei der Angabe der Datenbankverbindung mit den Informationen zu meiner Organisation. | Informationen zur Vorgehensweise zum Konfigurieren Ihrer Datenbankverbindungsinformationen finden Sie im Artikel [Installieren und Konfigurieren der SCAP-Erweiterungen](/sccm/compliance/plan-design/scap/install-configure-scap). 

## <a name="next-step"></a>Nächste Schritte
> [!div class="nextstepaction"]
> [Installieren und Konfigurieren der SCAP-Erweiterungen](/sccm/compliance/plan-design/scap/install-configure-scap)