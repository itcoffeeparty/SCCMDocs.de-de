---
title: Mobile Threat Defense
titleSuffix: Configuration Manager
description: "Schränken Sie mit Partnern von Configuration Manager und Intune Mobile Threat Defense den Zugriff auf Unternehmensressourcen nach Geräte-, Netzwerk- und Anwendungsrisiko ein"
ms.custom: na
ms.date: 03/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c0e6824-2dfe-4700-b817-d5631e0eb872
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 83911f35dbe8fc7bc24a4885929fbdf5660e7285
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/12/2017
---
# <a name="intune-mobile-threat-defense-connectors-in-configuration-manager"></a>Intune Mobile Threat Defense-Connectors in Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die [Bereitstellung der hybriden Verwaltung mobiler Geräte (System Center Configuration Manager mit Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) und die Integration zwischen Partnern von Intune und Mobile Threat Defense bietet Ihnen die Möglichkeit, den Zugriff auf Unternehmensressourcen und -daten zu steuern. Dies basiert auf der Risikobewertung.

Intune Mobile Threat Defense-Connectors geben Ihnen die Möglichkeit, einen Mobile Threat Defense-Hersteller Ihrer Wahl als Informationsquelle für Ihre Kompatibilitätsrichtlinien und bedingte Zugriffsregeln zu nutzen. So haben IT-Administratoren die Möglichkeit, eine Schutzschicht um ihre Unternehmensressourcen zu schaffen, wie etwa Exchange oder Sharepoint, besonders für gefährdete mobile Geräte.

## <a name="what-problem-does-this-solve"></a>Welches Problem wird dadurch gelöst?

Unternehmen müssen sensible Daten vor potenziellen Gefahren schützen. Darunter fallen physische, App-basierte und Netzwerk-basierte Bedrohungen, sowie Sicherheitsrisiken beim Betriebssystem.
In der Vergangenheit waren Unternehmen beim Schutz ihrer PCs vor Angriffen proaktiv, während mobile Geräte unüberwacht und ungeschützt blieben. Mobile Plattformen verfügen über einen integrierten Schutz des Betriebssystems durch Techniken wie die Isolierung von Apps oder überprüfte App Stores für Heimanwender, aber diese Plattformen sind trotzdem noch anfällig für komplexe Angriffe. Heute verwenden Angestellte Geräte für die Arbeit und benötigen Zugriff auf vertrauliche Informationen. Deshalb müssen Geräte vor immer komplexeren Angriffen geschützt werden.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>So funktionieren die Intune Threat Defense-Connectors

Der Connector schützt Unternehmensressourcen mithilfe eines Kommunikationskanals zwischen Intune und Ihrem ausgewählten Mobile Threat Defense-Hersteller. Partner von Intune Mobile Threat Defense bieten intuitive, leicht bereitzustellende Anwendungen für mobile Geräte, die aktiv Bedrohungsinformationen scannen und analysieren, um diese in Intune freizugeben, entweder für Berichte oder für Erzwingungen. Wenn beispielsweise eine verbundene Mobile Threat Defense-Anwendung dem Mobile Threat Defense-Hersteller meldet, dass ein Telefon in Ihrem Netzwerk aktuell mit einem Netzwerk verbunden ist, das nicht gegen „Man-in-the-Middle“-Angriffe geschützt ist, werden diese Informationen freigegeben und einer angemessenen Risikostufe zugeordnet (niedrig/mittel/hoch). Dies kann wiederum mit Ihren konfigurierten Einstellungen für berücksichtigte Risikostufen in Intune abgeglichen werden, um festzustellen, ob bestimmte Ressourcen Ihrer Wahl gesperrt werden sollten, während das Gerät gefährdet ist.

## <a name="sample-scenarios"></a>Beispielszenarios

Wenn ein Gerät von der Mobile Threat Defense-Lösung als infiziert eingestuft wird:

![](http://i.imgur.com/Li1WUOU.png)

Der Zugriff wird ermöglicht, wenn das Gerät wiederhergestellt ist:

![](http://i.imgur.com/VCIwpdz.png)

## <a name="mobile-threat-defense-partners"></a>Partner von Mobile Threat Defense

Erfahren Sie, wie Sie den Zugriff auf Unternehmensressourcen basierend auf Gerät, Netzwerk und Anwendungsrisiko schützen können mithilfe von:

- [Lookout](https://docs.microsoft.com/sccm/protect/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)
