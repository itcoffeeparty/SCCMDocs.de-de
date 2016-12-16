---
title: "Suchen eines Paketfamiliennamens (PFN) für Pro-App-VPN | System Center Configuration Manager"
description: "Erfahren Sie mehr über die zwei Methoden, einen Paketfamiliennamen zu suchen, sodass Sie ein Pro-App-VPN konfigurieren können."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
caps.latest.revision: 3
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bad09d52a962ea5dccf55e4e2e485a17d934055a

---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>Suchen eines Paketfamiliennamens (PFN) für Pro-App-VPN

*Gilt für: System Center Configuration Manager (Current Branch)*


Es gibt zwei Methoden, einen PFN zu suchen, sodass Sie ein Pro-App-VPN konfigurieren können.

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>Suchen eines PFN für eine App, die auf einem Windows-10-Computer installiert ist

Wenn die App, mit der Sie arbeiten, bereits auf einem Windows-10-Computer installiert ist, können Sie das PowerShell-Cmdlet [Get-AppxPackage](https://technet.microsoft.com/library/hh856044.aspx) zum Abrufen des PFN verwenden.

Die Syntax für Get-AppxPackage lautet:

` Parameter Set: __AllParameterSets`
` Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]`

> [!NOTE]
> Möglicherweise müssen Sie PowerShell als Administrator ausführen, um den PFN abrufen zu können

Verwenden Sie beispielsweise `Get-AppxPackage` zum Abrufen von Informationen zu allen universellen Apps, die auf dem Computer installiert sind.

Verwenden Sie `Get-AppxPackage *<app_name>` zum Abrufen von Informationen über eine App, deren Namen Sie kennen oder teilweise kennen. Beachten Sie die Verwendung des Platzhalterzeichens, das vor allem dann nützlich ist, wenn Sie nicht den vollständigen Namen der App kennen. Verwenden Sie beispielsweise beim Abrufen von Informationen für OneNote `Get-AppxPackage *OneNote`.


Hier sind die abgerufenen Informationen für OneNote:

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>Suchen einer PFN, wenn die App nicht auf einem Computer installiert ist

1.  Wechseln Sie zu https://www.microsoft.com/en-us/store/apps
2.  Geben Sie den Namen der App in der Suchleiste ein. Suchen Sie in unserem Beispiel nach OneNote.
3.  Klicken Sie auf den Link zur App. Beachten Sie, dass die URL, auf die Sie zugreifen, eine Reihe von Buchstaben am Ende hat. In unserem Beispiel sieht die URL folgendermaßen aus: `https://www.microsoft.com/en-us/store/apps/onenote/9wzdncrfhvjl`
4.  Fügen Sie in einer anderen Registerkarte die folgende URL ein, `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata`, und ersetzen Sie dabei `<app id>` mit der App-ID, die Sie von https://www.microsoft.com/en-us/store/apps erhalten haben - Reihe von Buchstaben am Ende der URL aus Schritt 3. In unserem Beispiel, das Beispiel OneNote, fügen Sie ein: `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`.

Die gewünschten Informationen werden in Edge angezeigt. Klicken Sie in Internet Explorer auf **Öffnen**, um die Informationen zu sehen. Der PFN-Wert erscheint in der ersten Zeile. Hier ist das Ergebnis in unserem Beispiel:


`{`
`  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",`
`  "packageIdentityName": "Microsoft.Office.OneNote",`
`  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",`
`  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"`
`}`



<!--HONumber=Nov16_HO1-->


