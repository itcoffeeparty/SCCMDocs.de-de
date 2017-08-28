---
title: TITEL DES ARTIKELS | Microsoft-Dokumentation
description: 
keywords: 
author: GITHUB USERNAME
manager: ALIAS
ms.date: 10/06/2016
ms.topic: article
ms.prod: 
ms.service: 
ms.technology: 
ms.assetid: GET ONE FROM guidgenerator.com
ms.openlocfilehash: a218011ded1ff3acc1dbd24471119b701f2cce23
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="metadata-and-markdown-template"></a>Metadaten- und Markdownvorlage

Diese docs.ms-Vorlage enthält Beispiele für Markdownsyntax sowie Anleitungen zum Festlegen der Metadaten. Sie ist im Stammverzeichnis jedes EM Pilot-Repositorys (z.B. ~/Azure-RMSDocs-pr /template.md) verfügbar und soll als Markdowndatei gelesen werden. Sie können aber in [der veröffentlichten Version](https://stage.docs.microsoft.com/en-us/rights-management/template) sehen,wie die Markdownbeispiele gerendert werden.

Beim Erstellen einer Markdowndatei sollten Sie die Vorlage in eine neue Datei kopieren, die Metadaten wie unten angegeben eintragen, die H1-Überschrift oben als Titel des Artikels festlegen und den Inhalt löschen.


## <a name="metadata"></a>Metadaten

Der vollständige, in erforderliche und optionale Felder unterteilte Metadatenblock ist oben; weitere Details finden Sie im [OPS-Metadatenmerkblatt](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data). Wichtige Hinweise:

- Sie **müssen** ein Leerzeichen zwischen dem Doppelpunkt (:) und dem Wert für ein Metadatenelement einfügen.
- Wenn ein optionales Metadatenelement keinen Wert hat, kommentieren Sie das Element mit einem # aus (lassen Sie es weder leer, noch verwenden Sie „K. A.“). Wenn Sie einen Wert für ein auskommentiertes Element hinzufügen, achten Sie darauf, das # zu entfernen.
- Doppelpunkte in einem Wert (z.B. einem Titel) unterbrechen den Metadatenparser. Verwenden Sie an ihrer Stelle die HTML-Codierung &#58; (z.B. „title: Azure Rights Management&#58; die Grundlagen | Azure RMS“).
- **title**: Dieser Titel wird in Suchmodulergebnissen angezeigt. Der Titel sollte mit einem senkrechten Strich (|) gefolgt vom Namen des Diensts enden (siehe z.B. oben). Der Titel muss nicht (und sollte wahrscheinlich nicht) mit dem Titel in der H1-Überschrift übereinstimmen. Er sollte ungefähr 65 Zeichen lang sein (einbezogener Inhalt | DIENSTNAME).
- **author**, **manager**, **reviewer**: Das author-Feld sollte den **Github-Benutzernamen** des Autors enthalten, nicht seinen Alias.  Andererseits sollten die Felder „manager“ und „reviewer“ Aliase enthalten. „ms.reviewer“ gibt den Namen des PM an, der dem Artikel oder Dienst zugeordnet ist.
- **ms.assetid**: Dies ist die GUID des Artikels aus CAPS. Wenn Sie eine neue Markdowndatei erstellen, rufen Sie eine GUID bei [https://www.guidgenerator.com](https://www.guidgenerator.com) ab.
- **ms.prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic**, **ms.tgt_pltfrm**: Mögliche Werte für diese Elemente finden Sie [hier](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## <a name="basic-markdown-and-gfm"></a>Basis-Markdownversionen und GFM

Alle Basis-Markdownversionen und GFM (Github-flavored Markdown, spezielles Github-Markdown) werden unterstützt. Weitere Informationen hierzu finden Sie unter:

- [Markdown: Syntax](https://daringfireball.net/projects/markdown/syntax)
- [Dokumentation zu Github-Flavored Markdown (GFM)](https://guides.github.com/features/mastering-markdown)

## <a name="headings"></a>Überschriften

Beispiele für Überschriften der ersten und zweiten Ebene siehe oben.

Es **darf** nur eine Überschrift der ersten Ebene in Ihrem Thema geben, die als Titel auf der Seite angezeigt wird.  

Überschriften der zweiten Ebene generieren das Inhaltsverzeichnis auf der Seite, das im Abschnitt „In diesem Artikel“ unterhalb des Titels auf der Seite angezeigt wird.

### <a name="third-level-heading"></a>Überschrift der dritten Ebene
#### <a name="fourth-level-heading"></a>Überschrift der vierten Ebene
##### <a name="fifth-level-heading"></a>Überschrift der fünften Ebene
###### <a name="sixth-level-heading"></a>Überschrift der sechsten Ebene

## <a name="text-styling"></a>Textformat

*Kursiv*

**Fett**

~~Durchgestrichen~~



## <a name="links"></a>Links

Um eine Verknüpfung mit einer Markdowndatei im gleichen Repository herzustellen, verwenden Sie [relative Links](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2).

- Beispiel: [What is Azure Rights Management](./understand-explore/what-is-azure-rights-management.md) (Was ist Azure Rights Management?)

Um eine Verknüpfung mit einer Überschrift in der gleichen Markdowndatei herzustellen, zeigen Sie die Quelle des veröffentlichten Artikels an, und suchen Sie die ID der Überschrift (z.B. `id="blockquote"`, und stellen Sie mit # + ID die Verknüpfung her (z.B. `#blockquote`).

- Beispiel: [Blockzitate](#blockquote)

Um eine Verknüpfung mit einer Überschrift in einer Markdowndatei im gleichen Repository herzustellen, verwenden Sie relative Verknüpfung + Hashtagverknüpfung.

- Beispiel: [technische Übersicht des Anmeldevorgangs](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

Um eine Verknüpfung mit einer externen Datei herzustellen, verwenden Sie die vollständige URL als Link.

- Beispiel: [Github](http://www.github.com)

Wenn eine URL in einer Markdowndatei angezeigt wird, wird sie in einen klickbaren Link umgewandelt.

- Beispiel: http://www.github.com

## <a name="lists"></a>Listen

### <a name="ordered-lists"></a>Sortierte Listen

1. This
1. Is
1. An
1. Ordered
1. List  


#### <a name="ordered-list-with-an-embedded-list"></a>Sortierte Liste mit eingebetteter Liste

1. Here
1. comes
1. an
1. embedded
    1. Miss Scarlett
    1. Professor Plum
1. ordered
1. list


### <a name="unordered-lists"></a>Unsortierte Listen

- This
- is
- a
- bulleted
- list


##### <a name="unordered-list-with-an-embedded-lists"></a>Unsortierte Liste mit einer eingebetteten Liste

- This
- bulleted
- list
    - Mrs. Peacock
    - Mr. Green
- contains  
- other
    1. Colonel Mustard
    1. Mrs. White
- lists


## <a name="horizontal-rule"></a>Horizontale Trennlinie

---

## <a name="tables"></a>Tabellen

| Tabellen        | sind           | cool  |
| ------------- |:-------------:| -----:|
| SP 3 ist      | rechtsbündig | 1.600 $ |
| SP 2 ist      | zntriert      |   12 $ |
| SP 1 ist standardmäßig | linksbündig     |    1 $ |


## <a name="code"></a>Code

### <a name="codeblock"></a>Codeblock

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### <a name="in-line-code"></a>Inlinecode

Dies ist ein Beispiel für `in-line code`.

## <a name="blockquotes"></a>Blockzitate

> Die Trockenheit hatte nun zehn Millionen Jahre lang angehalten, und die Herrschaft der schrecklichen Echsen hatte längst geendet. Hier am Äquator, in dem Kontinent, der eines Tages Afrika heißen sollte, hatte der Existenzkampf einen neuen Gipfel der Grausamkeit erreicht, und der Sieger war noch nicht in Sicht. In diesem trostlosen und verdorrten Land konnte nur der Kleine oder der Schnelle oder der Wilde gedeihen oder auch nur zu überleben hoffen.

## <a name="images"></a>Abbilder

### <a name="static-image"></a>Statisches Bild

![Dies ist der alternative Text.](./media/AzRMS_elements.png)

### <a name="linked-image"></a>Verknüpftes Bild

[![Alternativer Text für verknüpftes Bild](./media/AzRMS_elements.png)](https://azure.microsoft.com)

### <a name="animated-gif"></a>Animierte GIF-Datei

![animierte GIF-Datei](./media/hololens.gif)

## <a name="alerts"></a>Warnungen

### <a name="note"></a>Hinweis

> [!NOTE]
> Dies ist ein HINWEIS

### <a name="warning"></a>Warnung

> [!WARNING]
> Dies ist eine WARNUNG

### <a name="tip"></a>Tipp

> [!TIP]
> Dies ist ein TIPP

### <a name="important"></a>Wichtig

> [!IMPORTANT]
> Dies ist WICHTIG

## <a name="videos"></a>Videos

### <a name="channel-9"></a>Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### <a name="youtube"></a>Youtube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## <a name="docsms-extentions"></a>docs.ms-Erweiterungen

### <a name="button"></a>Schaltfläche

> [!div class="button"]
[Schaltflächenlinks](/rights-management)

### <a name="selector"></a>Selector

> [!div class="op_single_selector"]
- [Foo](/rights-management/template.md)
- [Balken](/rights-management/scratch.md)

### <a name="step-by-step"></a>Schritt für Schritt

>[!div class="step-by-step"]
[Vor](https://www.example.com)
[weiter](https://www.example.com)
