---
title: "Sicherheit und Datenschutz für Abfragen"
titleSuffix: Configuration Manager
description: "Verstehen Sie die bewährten Methoden für Sicherheit und Datenschutz beim Abfragen von Informationen aus der Standortdatenbank."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 6ab8498a2153dd272e9451aa58b68b4f804cd93a
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/12/2017
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Sicherheit und Datenschutz für Abfragen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager können Sie Informationen von der Standortdatenbank auf Basis der von Ihnen angegebenen Kriterien abrufen. Die Informationen zur Standortdatenbank werden von Configuration Manager während des Standardbetriebs gesammelt. Mithilfe von Informationen, die bei einer Ermittlung oder Inventur gesammelt wurden, können Sie beispielsweise eine Abfrage so konfigurieren, dass Geräte identifiziert werden, die die angegebenen Kriterien erfüllen.  

 Weitere Informationen zu Abfragen finden Sie unter [Introduction to Queries in Configuration Manager (Einführung in Abfragen in System Center Configuration Manager)](../../../core/servers/manage/introduction-to-queries.md). Weitere Informationen zu bewährten Sicherheitsmethoden und Datenschutzinformationen zu Configuration Manager-Vorgängen, bei denen Informationen gesammelt werden, die Sie mithilfe von Abfragen abrufen können, finden Sie unter [Sicherheit und Datenschutz für System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Bewährte Sicherheitsmethoden für Abfragen  
 Verwenden Sie die folgende bewährte Sicherheitsmethode für Abfragen:  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Wenn Sie eine Abfrage exportieren oder importieren, die an einem Netzwerkspeicherort gespeichert ist, schützen Sie den Speicherort und den Netzwerkkanal.|Schränken Sie die Anzahl der Personen ein, die auf den Netzwerkordner zugreifen können.<br /><br /> Verwenden Sie SMB-Signaturen (Server Message Block) bzw. Internetprotokollsicherheit (IPsec) zwischen dem Netzwerkspeicherort und dem Standortserver, um potenzielle Angreifer an der Manipulation der Abfragedaten vor dem Import zu hindern.|  

## <a name="see-also"></a>Weitere Informationen:  
 [Abfragen – Technische Referenz für System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
