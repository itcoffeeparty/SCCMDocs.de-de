---
title: Zertifikate und Sicherheit
titleSuffix: Configuration Manager
description: "Verwalten von Zertifikaten und Sicherheit für System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
caps.latest.revision: "1"
author: mestew
ms.author: mstewart
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 9d8812da3588b60f388288cef6f9a093731d873f
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/04/2017
---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>Verwalten von Zertifikaten und Sicherheit für Updates Publisher

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit den folgenden Verfahren können Sie den Zertifikatspeicher auf dem Updateserver sowie ein selbstsigniertes Zertifikat auf dem Clientcomputer konfigurieren und die Gruppenrichtlinie so konfigurieren, dass sie dem Windows Update-Agent das Überprüfen von Computern auf veröffentlichte Updates erlaubt.

## <a name="configure-the-certificate-store-on-the-update-server"></a>Konfigurieren des Zertifikatspeichers auf dem Updateserver
 Updates Publisher verwendet ein digitales Zertifikat zum Signieren der Updates in den Katalogen, die Updates Publisher veröffentlicht. Bevor ein Katalog auf dem Updateserver veröffentlicht werden kann, muss dieses Zertifikat im Zertifikatspeicher des Updateservers vorhanden sein, und im Zertifikatspeicher des Updates Publisher-Computers, wenn dieser Computer nicht mit dem Computer des Updateservers identisch ist.

Das folgende Verfahren ist eine von mehreren möglichen Methoden, um das Zertifikat dem Zertifikatspeicher auf dem Updateserver hinzuzufügen.

### <a name="to-configure-the-certificate-store"></a>So konfigurieren Sie den Zertifikatspeicher
1.  Klicken Sie auf einem Computer, der sowohl auf den Updates Publisher-Computer als auch den Updateserver zugreifen kann, auf **Starten**, **Ausführen**, geben Sie **MMC** in das Textfeld ein, und klicken Sie dann auf **OK**, um die Microsoft Management Console (MMC) zu öffnen.

2.  Klicken Sie auf **Datei**, **Snap-In hinzufügen/entfernen**, **Hinzufügen**, **Zertifikate**, **Hinzufügen**, wählen Sie **Computerkonto**, und klicken Sie dann auf **Weiter**.

3.  Wählen Sie **Ein anderer Computer**, geben Sie den Namen des Updateservers ein, oder klicken Sie auf **Durchsuchen**, um den Updateservercomputer zu suchen, klicken Sie auf **Fertig stellen**, **Schließen** und **OK**.

4.  Erweitern Sie **Zertifikate (*Updateservername*)**, erweitern Sie **WSUS**, und klicken Sie dann auf **Zertifikate**.

5.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf das gewünschte Zertifikat, und klicken Sie auf **Alle Aufgaben** und **Exportieren**.

6.  Verwenden Sie die Standardeinstellungen im Zertifikatexport-Assistenten, um eine Exportdatei mit dem im Assistenten angegebenen Namen und Speicherort zu erstellen. Diese Datei muss für den Updateserver verfügbar sein, bevor Sie mit dem nächsten Schritt fortfahren.

7.  Klicken Sie mit der rechten Maustaste auf **Vertrauenswürdige Herausgeber**, klicken Sie auf **Alle Aufgaben** und dann auf **Importieren**. Schließen Sie den Zertifikatimport-Assistenten mithilfe der exportierten Datei aus Schritt 6 ab.

8.  Wenn ein selbstsigniertes Zertifikat wie z.B. **WSUS Publishers Self-signed** verwendet wird, klicken Sie mit der rechten Maustaste auf **Vertrauenswürdige Stammzertifizierungsstellen**, klicken Sie auf **Alle Aufgaben** und dann auf **Importieren**. Schließen Sie den Zertifikatimport-Assistenten mithilfe der exportierten Datei aus Schritt 6 ab.

9.  Klicken Sie mit der rechten Maustaste auf **Zertifikate (*Updateservername*)**, klicken Sie auf **Verbindung mit anderem Computer herstellen**, geben Sie den Computernamen für den Updates Publisher-Computer ein, und klicken Sie auf **OK**.

10. Wenn Updates Publisher sich auf einem anderen Computer als der Updateserver befindet, wiederholen Sie die Schritte 7 bis 9, um das Zertifikat in den Zertifikatspeicher des Updates Publisher-Computers zu importieren.



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>Konfigurieren eines selbstsignierten Zertifikats auf Clientcomputern
Der Windows Update Agent (WUA) überprüft Clientcomputer auf die Updates aus dem Katalog. Bei diesem Vorgang werden keine Updates installiert, wenn der Agent dieses digitale Zertifikat nicht im Speicher „Vertrauenswürdige Herausgeber“ des lokalen Computers finden kann. Wenn bei der Veröffentlichung des Updateskatalogs ein selbstsigniertes Zertifikat wie **WSUS Publishers Self-signed** verwendet wurde, muss sich das Zertifikat auch im Zertifikatspeicher der vertrauenswürdigen Stammzertifizierungsstellen auf dem lokalen Computer befinden, damit der Agent die Gültigkeit des Zertifikats überprüfen kann.

Sie können eine von mehreren Methoden zum Konfigurieren von Zertifikaten auf Clientcomputern verwenden, z.B. die Gruppenrichtlinie und den **Zertifikatimport-Assistenten** oder die Certutil-Tools und die Softwareverteilung.

Das folgende Beispiel zeigt das Konfigurieren des selbstsignierten Zertifikats auf Clientcomputern.

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>So konfigurieren Sie ein selbstsigniertes Zertifikat auf Clientcomputern
1.  Klicken Sie auf einem Computer, der auf den Updateserver zugreifen kann, auf **Starten**, **Ausführen**, geben Sie **MMC** in das Textfeld ein, und klicken Sie dann auf **OK**, um die Microsoft Management Console (MMC) zu öffnen.

2.  Klicken Sie auf **Datei**, **Snap-In hinzufügen/entfernen**, **Hinzufügen**, **Zertifikate**, **Hinzufügen**, wählen Sie **Computerkonto**, und klicken Sie dann auf **Weiter**.

3.  Wählen Sie **Ein anderer Computer**, geben Sie den Namen des Updateservers ein, oder klicken Sie auf **Durchsuchen**, um den Updateservercomputer zu suchen, klicken Sie auf **Fertig stellen**, **Schließen** und **OK**.

4.  Erweitern Sie **Zertifikate (*Updateservername*)**, erweitern Sie **WSUS**, und klicken Sie dann auf **Zertifikate**.

5.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf das Zertifikat, und klicken Sie auf **Alle Aufgaben** und **Exportieren**. Schließen Sie den **Zertifikatexport-Assistenten** unter Verwendung der Standardeinstellungen ab, um eine Exportzertifikatdatei mit dem im Assistenten angegebenen Namen und Speicherort zu erstellen.

6.  Fügen Sie mit einer der folgenden Methoden das Zertifikat hinzu, das auf jedem Clientcomputer, der mit WUA überprüft, ob die Updates im Katalog vorhanden sind, zum Signieren des Updateskatalogs verwendet wird. Fügen Sie das Zertifikat wie folgt auf dem Clientcomputer hinzu:

    -   Für selbstsignierte Zertifikate: Fügen Sie das Zertifikat den Zertifikatspeichern **Vertrauenswürdige Stammzertifizierungsstellen** und **Vertrauenswürdige Herausgeber** hinzu.

    -   Für Zertifikate, die von der Zertifizierungsstelle (ZS) ausgestellt wurden: Fügen Sie das Zertifikat dem Zertifikatspeicher **Vertrauenswürdige Herausgeber** hinzu.

    > [!NOTE]
    > WUA überprüft auch, ob auf dem lokalen Computer die Gruppenrichtlinieneinstellung **Signierten Inhalt von Intranet-Speicherort für Microsoft-Updatedienst zulassen** aktiviert ist. Diese Richtlinieneinstellung muss für WUA aktiviert sein, damit Updates überprüft werden können, die mithilfe von Update Publisher erstellt und veröffentlicht wurden. Weitere Informationen zum Aktivieren dieser Gruppenrichtlinieneinstellung finden Sie unter [Gewusst wie: Konfigurieren der Gruppenrichtlinie auf Clientcomputern] (https://technet.microsoft.com/library/bb530967.aspx(d=robot).



## <a name="configuring-group-policy-to-allow-wua-on-computers-to-scan-for-published-updates"></a>Konfigurieren der Gruppenrichtlinie, um auf Computern die Überprüfung auf veröffentlichte Updates durch WUA zuzulassen
Bevor der Windows Update-Agent (WUA) Computer auf Updates überprüft, die mit Updates Publisher erstellt und veröffentlicht wurden, muss eine Gruppenrichtlinieneinstellung aktiviert werden, um signierten Inhalt von einem Intranetspeicherort für den Microsoft-Updatedienst zuzulassen. Wenn die Richtlinieneinstellung aktiviert ist, akzeptiert WUA Updates von einem Intranetspeicherort, wenn diese im Zertifikatspeicher **Vertrauenswürdige Herausgeber** des lokalen Computers signiert wurden. Es gibt mehrere Methoden zum Konfigurieren der Gruppenrichtlinie auf Computern in der Umgebung.

Für Computer, die sich nicht in der Domäne befinden, kann eine Einstellung des Registrierungsschlüssels konfiguriert werden, die signierten Inhalt von einem Intranetspeicherort für den Microsoft-Updatedienst ermöglicht.

Die folgenden Verfahren umfassen die grundlegenden Schritte zum Konfigurieren der Gruppenrichtlinie für Computer in der Domäne und eines Registrierungsschlüsselwerts auf Computern, die sich nicht in der Domäne befinden.

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>So konfigurieren Sie die Gruppenrichtlinie, um die Überprüfung auf veröffentlichte Updates durch WUA zuzulassen
1.  Öffnen Sie das Gruppenrichtlinienobjekt-Editor-Snap-In Microsoft Management Console (MMC) mit einem Benutzer, der über die entsprechenden Sicherheitsrechte zum Konfigurieren von Gruppenrichtlinien verfügt.

2.  Klicken Sie auf **Durchsuchen**, und wählen Sie die Domäne, OE oder mit der Website verknüpften GPOs, wo die konfigurierte Gruppenrichtlinie an die gewünschten Clientcomputer weitergegeben wird. Klicken Sie auf **OK**, **Fertig stellen**, **Schließen** und **OK**.

3.  Erweitern Sie die ausgewählte Richtlinieneinstellung in der Konsolenstruktur, erweitern Sie **Computerkonfiguration**, **Administrative Vorlagen**, **Windows-Komponenten**, und klicken Sie dann auf **Windows Update**.

4.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf **Signierten Inhalt von Intranet-Speicherort für Microsoft-Updatedienst zulassen**, klicken Sie auf **Eigenschaften**, **Aktiviert** und dann auf **OK**.
