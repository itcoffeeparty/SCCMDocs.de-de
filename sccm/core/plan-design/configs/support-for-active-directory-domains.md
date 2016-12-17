---
title: "Unterstützung für AD-Domänen| System Center Configuration Manager"
description: "Rufen Sie die Anforderungen für die Mitgliedschaft eines System Center Configuration Manager-Standortsystems in einer Active Directory-Domäne ab."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fdcd1b3b59dbe2b5bd82499e8d29230b3d8ca5cd


---
# <a name="support-for-active-directory-domains-for-system-center-configuration-manager"></a>Unterstützung für Active Directory-Domänen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Alle System Center Configuration Manager-Standortsysteme müssen Mitglieder einer unterstützten Windows Active Directory-Domäne sein. Configuration Manager-Clientcomputer können Mitglieder der Domäne oder der Arbeitsgruppe sein.  

 **Anforderungen und Einschränkungen:**  

-   Die Domänenmitgliedschaft schließt Standortsysteme ein, die eine internetbasierte Clientverwaltung in einem Umkreisnetzwerk (auch als überwachtes Subnetz oder DMZ bezeichnet) unterstützen.  

-   Änderungen an den folgenden Einstellungen eines Computers, der eine Standortsystemrolle hostet, werden nicht unterstützt:  

    -   Domänenmitgliedschaft  

    -   Domänenname  

    -   Computername  

Sie müssen die Standortsystemrolle (einschließlich des Standorts bei einem Standortserver) deinstallieren, bevor Sie diese Änderungen vornehmen.  

**Domänen mit den folgenden Domänenfunktionsebenen werden unterstützt:**  

-   Windows Server 2008  

-   Windows Server 2008 R2  

-   Windows Server 2012  

-   Windows Server 2012 R2  

##  <a name="a-namebkmkdisjointa-disjoint-namespace"></a><a name="bkmk_Disjoint"></a> Zusammenhanglose Namespaces  
Configuration Manager unterstützt die Installation von Standortsystemen und Clients in einer Domäne mit einem zusammenhanglosen Namespace.  

Ein zusammenhangloser Namespace liegt vor, wenn das primäre DNS-Suffix (Domain Name System) eines Computers nicht mit dem Active Directory DNS-Domänennamen an dem Ort, an dem der Computer sich befindet, übereinstimmt. Der Computer mit dem abweichenden primären DNS-Suffix wird als zusammenhanglos betrachtet. Ein zusammenhangloser Namespace liegt auch vor, wenn der NetBIOS-Domänenname eines Domänencontrollers nicht mit dem Active Directory DNS-Domänennamen übereinstimmt.  

In der folgenden Tabelle werden die bei zusammenhanglosen Namespaces unterstützten Szenarien aufgeführt.  

|Szenario|Weitere Informationen|  
|--------------|----------------------|  
|**Szenario 1:**<br /><br /> Das primäre DNS-Suffix des Domänencontrollers unterscheidet sich vom Active Directory DNS-Domänennamen. Computer, die Mitglieder der Domäne sind, können zusammenhanglos oder nicht zusammenhanglos sein.|Das primäre DNS-Suffix des Domänencontrollers unterscheidet sich in diesem Szenario vom Active Directory DNS-Domänennamen. Der Domänencontroller ist in diesem Szenario zusammenhanglos. Computer, die Mitglieder der Domäne sind, einschließlich der Standortserver und Computer, können ein primäres DNS-Suffix aufweisen, das entweder mit dem primären DNS-Suffix des Domänencontrollers oder mit dem Active Directory DNS-Domänennamen übereinstimmt.|  
|**Szenario 2:**<br /><br /> Ein Mitgliedscomputer in einer Active Directory DNS-Domäne ist zusammenhanglos, obwohl der Domänencontroller nicht zusammenhanglos ist.|In diesem Szenario unterscheidet sich das primäre DNS-Suffix eines Mitgliedscomputers, auf dem ein Standortsystem installiert ist, vom Active Directory DNS-Domänennamen, obwohl das primäre DNS-Suffix des Domänencontrollers mit dem Active Directory DNS-Domänennamen übereinstimmt. In diesem Fall ist ein Domänencontroller nicht zusammenhanglos, und ein Mitgliedscomputer ist zusammenhanglos. Mitgliedscomputer, auf denen der Configuration Manager-Client ausgeführt wird, können ein primäres DNS-Suffix aufweisen, das entweder mit dem primären DNS-Suffix des separaten Standortsystemservers oder mit dem Active Directory DNS-Domänennamen übereinstimmt.|  

 Damit ein Computer auf zusammenhanglose Domänencontroller zugreifen kann, müssen Sie das Active Directory-Attribut **msDS-AllowedDNSSuffixes** für den Domänenobjektcontainer ändern. Sie müssen dem Attribut beide DNS-Suffixe hinzufügen.  

 Darüber hinaus müssen Sie die Suchliste für jeden zusammenhanglosen Computer in der Domäne konfigurieren und so sicherstellen, dass in der Suchliste für die DNS-Suffixe alle im Unternehmen bereitgestellten DNS-Namespaces enthalten sind. Fügen Sie der Liste der Namespaces das primäre DNS-Suffix des Domänencontrollers, den DNS-Domänennamen und alle zusätzlichen Namespaces für andere Server mit Interoperabilität mit Configuration Manager hinzu. Sie können die Gruppenrichtlinien-Verwaltungskonsole verwenden, um die Suchliste für DNS-Suffixe **** zu konfigurieren.  

> [!IMPORTANT]  
>  Wenn Sie in Configuration Manager auf einen Computer verweisen, geben Sie das primäre DNS-Suffix des Computers an. Das Suffix muss mit dem FQDN, der als Attribut **dnsHostName** in der Active Directory-Domäne registriert ist, und mit dem Dienstprinzipalnamen (SPN) des Systems übereinstimmen.  

##  <a name="a-namebkmkslda-single-label-domains"></a><a name="bkmk_SLD"></a> Einteilige Domänen  
 Configuration Manager unterstützt Standortsysteme und Clients in einer einteiligen Domäne, wenn die folgenden Kriterien erfüllt sind:  

-   Die einteilige Domäne muss in Active Directory Domain Services mit einem zusammenhanglosen DNS-Namespace konfiguriert sein, der über eine gültige Domäne der obersten Ebene verfügt.  

     **Beispiel:** Die einteilige Domäne „Contoso“ ist so konfiguriert, dass sie im DNS von „contoso.com“ einen zusammenhanglosen Namespace aufweist. Wenn Sie das DNS-Suffix in Configuration Manager also für einen Computer in der Domäne „Contoso“ festlegen, geben Sie „Contoso.com“ und nicht „Contoso“ an.  

-   DCOM-Verbindungen zwischen Standortservern im Systemkontext müssen erfolgreich sein, was durch die Kerberos-Authentifizierung sichergestellt wird.  



<!--HONumber=Nov16_HO1-->

