---
title: Informationen zur PowerShell-Skriptsicherheit
titleSuffix: Configuraton Manager
description: Ressourcen zur PowerShell-Skriptsicherheit
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7799ac9737ac3a6a73d2d7241dd8b56325d4e340
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="learn-more-about-powershell-script-security"></a>Informationen zur PowerShell-Skriptsicherheit

*Gilt für: System Center Configuration Manager (Current Branch)*

Es ist die Aufgabe des Administrators, die vorgeschlagene Verwendung von PowerShell und dessen Parametern in ihrer Umgebung zu prüfen. In diesem Artikel finden Sie einige hilfreiche Ressourcen für Administratoren, die über die Leistungsfähigkeit von PowerShell und potenzielle Risikooberflächen informieren. So lassen sich potenzielle Risikooberflächen verringern und sichere Skripts verwenden.

## <a name="powershell-script-security"></a>PowerShell-Skriptsicherheit
In „Run Scripts“ (Skripts ausführen) ist ein Feature integriert, mit dem Skripts, die in der Umgebung ausgeführt werden sollen, visuell überprüft und genehmigt werden können. Administratoren sollten wissen, dass PowerShell-Skripts verschleiert sein können: Diese Skripts sind schädlich und bei der visuellen Überprüfung während der Skriptgenehmigung nur schwer zu erkennen. Eine bewährte Methode ist die Verwendung von bestimmten Überprüfungstools zusätzlich zur visuellen Überprüfung der PowerShell-Skripts. So lassen sich Probleme mit verdächtigen Skripts ermitteln. Diese Tools sind nicht immer in der Lage, die Absicht des PowerShell-Autors zu bestimmen, und können auf diese Weise auf verdächtige Skripts aufmerksam machen. Anschließend muss der Administrator bestimmen, ob es sich um schädliche oder sichere Skriptsyntax handelt.

## <a name="recommendations"></a>Empfehlungen
- Öffnen Sie die nachfolgenden Links, und machen Sie sich mit den bewährten PowerShell-Methoden zum Thema Sicherheit vertraut.
- **Skripts signieren:** Eine weitere Möglichkeit, die Sicherheit von Skripts zu erhöhen, ist sie überprüfen und signieren zu lassen, bevor sie für die Verwendung importiert werden.
- Speichern Sie keine Geheimnisse (z.B. Kennwörter) in PowerShell-Skripts, und informieren Sie sich über den besten Umgang damit.


## <a name="general-information-about-powershell-security-best-practices"></a>Allgemeine Informationen zu bewährten PowerShell-Methoden zum Thema Sicherheit

Unter diesen Links finden Configuration Manager-Administratoren erste Informationen zu den Best Practices zur PowerShell-Skriptsicherheit.  

[PowerShell Security Best Practices (Bewährte PowerShell-Methoden zum Thema Sicherheit)](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[PowerShell Security Best Practices PowerPoint (PowerPoint-Präsentation zu den bewährten PowerShell-Methoden zum Thema Sicherheit)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[Defending Against PowerShell Attacks (Schutz vor PowerShell-Angriffen)](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[Twitternachricht „Defending Against PowerShell Attacks“ (Schutz vor PowerShell-Angriffen) von Lee Holmes, einem Verfechter von Microsoft PowerShell und des Themas Sicherheit](https://twitter.com/Lee_Holmes/status/922462821081694208)

[Protecting Against Malicious Code Injection (Schutz vor der Einschleusung von schädlichem Code)](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[PowerShell Gallery – New Security Scan (PowerShell-Katalog – Neuer Sicherheitsscan)](https://blogs.msdn.microsoft.com/powershell/2015/08/06/powershell-gallery-new-security-scan/)

[Das PowerShell Blue Team erläutert die detaillierte Skriptblockprotokollierung, die geschützte Ereignisprotokollierung, Antimalware Scan Interface (AMSI) und APIs zum sicheren Generieren von Code.](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[Windows 10 to offer application developers new malware defenses (Windows 10 stellt neue Schutzmaßnahmen gegen Malware für Entwickler bereit)](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>PowerShell-Parametersicherheit
Das Übergeben von Parametern ist eine Möglichkeit, Skripts flexibel zu gestalten und Entscheidungen bis zur Laufzeit zu verzögern. Der Vorgang stellt jedoch auch eine weitere Risikooberfläche dar. Bewährte Methoden zum Verhindern böswilliger Parameter oder zur Einschleusung von Skripts sind folgende:

- Nur vordefinierte Parameter zulassen
- Verwenden Sie das Feature für reguläre Ausdrücke, um zulässige Parameter zu überprüfen.
    - Beispiel: Wenn nur ein bestimmter Wertebereich zulässig ist, nutzen Sie einen regulären Ausdruck, um die Zeichen oder Werte zu überprüfen, aus denen der Bereich bestehen kann.
    - Durch das Überprüfen von Parametern kann verhindert werden, dass Benutzer bestimmte Zeichen verwenden, die auskommentiert werden können, z.B. Anführungszeichen. Beachten Sie, dass es mehrere Arten von Anführungszeichen geben kann. Die Überprüfung zulässiger Zeichen mithilfe regulärer Ausdrücke ist häufig einfacher, als alle nicht zulässigen Eingaben einzeln zu definieren.
- Nutzen Sie das PowerShell-Modul [„Injection Hunter“](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) im PowerShell-Katalog.
    - Es kann auch falsch-positive Ergebnisse geben. Wenn etwas als verdächtig gekennzeichnet ist, sollten Sie daher nach Anzeichen für absichtliches Handeln suchen, um festzustellen, ob es sich um ein echtes Problem handelt. 
- Microsoft Visual Studio verfügt über ein Skriptanalysetool, das PowerShell-Syntax überprüfen kann.
- Im folgenden Video erhalten Sie einen Überblick über die Problemtypen, gegen die Sie sich schützen können (insbesondere Minute 12:20 bis 17:50):     <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>Empfehlungen zur Umgebung
Allgemeine Empfehlungen für PowerShell-Administratoren:
1. Stellen Sie die neueste Version von PowerShell bereit, z.B. Version 5 oder höher, die in Windows 10 integriert ist. Alternativ können Sie das [Windows Management Framework](https://www.microsoft.com/en-us/download/details.aspx?id=54616) bereitstellen, das für alle Windows-Versionen ab einschließlich Windows 7 und Windows Server 2008 R2 verfügbar ist. 
2. Aktivieren und erfassen Sie PowerShell-Protokolle, optional einschließlich der geschützten Ereignisprotokollierung. Integrieren Sie diese Protokolle in Ihre Signaturen und Workflows für die Jagd auf Bedrohungen und die Reaktion auf Sicherheitsvorfälle.
3. Implementieren Sie Just Enough Administration auf sehr wichtigen Systemen, um uneingeschränkten administrativen Zugriff auf diese Systemen zu verhindern oder zu reduzieren.
4. Stellen Sie Device Guard-/Anwendungssteuerungsrichtlinen bereit, damit vorab genehmigte administrative Aufgaben die vollständige Funktionalität von PowerShell verwenden können. Beschränken Sie gleichzeitig die interaktive und nicht genehmigte Verwendung auf einen kleinen Teil der PowerShell-Sprache.
5. Stellen Sie Windows 10 bereit, damit Ihr Antivirus-Anbieter vollständigen Zugriff auf alle Inhalte hat (einschließlich der Inhalte, die zur Laufzeit generiert oder entschleiert werden), die von Windows-Skriptinghosts einschließlich PowerShell verarbeitet werden.