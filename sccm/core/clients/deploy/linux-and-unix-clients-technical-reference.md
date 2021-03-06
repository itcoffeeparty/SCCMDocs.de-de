---
title: UNIX- und Linux-Clientkomponentendienste und -befehle
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Komponentendienste und -befehle auf Linux- und UNIX-Clients in System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3e66708471b22346901e8ee16e63dd962b699a16
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-system-center-configuration-manager"></a>UNIX- und Linux-Clientkomponentendienste und -befehle für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 In der folgenden Tabelle sind die Clientkomponentendienste des Configuration Manager-Clients für Linux und UNIX enthalten.  

|Dateiname|Weitere Informationen|  
|---------------|----------------------|  
|ccmexec.bin|Dieser Dienst ist gleichbedeutend mit dem ccmexc-Dienst auf einem Windows-basierten Client. Er ist verantwortlich für die gesamte Kommunikation mit Configuration Manager-Standortsystemrollen. Zudem kommuniziert er mit dem omiserver.bin-Dienst, um eine Hardwareinventur auf dem lokalen Computer zu ermitteln.<br /><br /> Führen Sie **ccmexec -h**aus, um eine Liste der unterstützten Befehlszeilenargumente zu erhalten.|  
|omiserver.bin|Dieser Dienst ist der CIM-Server. Der CIM-Server stellt ein Framework für austauschbare Softwaremodule bereit, die als Anbieter bezeichnet werden. Anbieter interagieren mit Linux- und UNIX-Computerressourcen und erfassen die Hardwareinventurdaten. Zum Beispiel die **Anbieter** für eine Linux-Computer sammelt Daten, die das Linux-Betriebssystem-Prozessen zugeordnet.|  

 Die folgenden Tabellen List-Befehle, die Sie verwenden können, um zu starten, beenden oder Neustarten der Dienste für Clients (ccmexec.bin und omiserver.bin) unter jeder Version von Linux oder UNIX. Beim Starten oder Beenden des ccmexec-Diensts wird der Dienst „omiserver“ ebenfalls gestartet oder beendet.  

|Betriebssystem|Befehle|  
|----------------------|--------------|  
|Universal Agent<br /><br /> RHEL 4 und SLES 9|Starten: **/etc/init d/ccmexecd start**<br /><br /> Beenden: **/etc/init d/ccmexecd stop**<br /><br /> Neu starten: **/etc/init d/ccmexecd restart**|  
|Solaris 9|Starten: **/etc/init d/ccmexecd start**<br /><br /> Beenden: **/etc/init d/ccmexecd stop**<br /><br /> Neu starten: **/etc/init d/ccmexecd restart**|  
|Solaris 10|Starten:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> Beenden:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|Solaris 11|Starten:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> Beenden:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|AIX|Starten:<br /><br /> **startsrc -s omiserver**<br /><br /> **startsrc -s ccmexec**<br /><br /> Beenden:<br /><br /> **stopsrc -s ccmexec**<br /><br /> **stopsrc -s omiserver**|  
|HP-UX|Starten: **/sbin/init.d/ccmexecd start**<br /><br /> Beenden: **/sbin/init.d/ccmexecd stop**<br /><br /> Neu starten: **/sbin/init.d/ccmexecd restart**|  
