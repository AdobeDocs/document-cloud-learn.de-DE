---
title: Erlebnisse für eingebettete e-Signaturen und Dokumente erstellen
description: Erfahren Sie, wie Sie mithilfe von Adobe Sign APIs E-Signatur- und Dokumenterlebnisse in Ihre Webplattformen und Content- und Dokumentenmanagementsysteme einbetten
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7489.jpg
kt: 7489
exl-id: db300cb9-6513-4a64-af60-eadedcd4858e
source-git-commit: f015bd7ea1a25772a12cd0852d452d120f205a5c
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# Erlebnisse für eingebettete E-Signaturen und Dokumente erstellen

Erfahren Sie, wie Sie mit Adobe Sign APIs die e-Signatur- und Dokumenterlebnisse in Ihre Webplattformen und Content- und Dokumentenmanagementsysteme einbetten. Dieses Tutorial enthält vier Teile, die in den folgenden Links beschrieben werden:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="embeddedesignature.md#part1">
        <img alt="Was Sie brauchen" src="assets/embeddedesignature/EmbedPart1_thumb.png" />
    </a>
    <div>
    <a href="embeddedesignature.md#part1"><strong>Teil 1: Was Sie brauchen</strong></a>
    </div>
  </td>
  <td>
    <a href="embeddedesignature.md#part2">
        <img alt="Teil 2: Code Niedrig/Nein — die Leistungsfähigkeit von Webformularen" src="assets/embeddedesignature/EmbedPart2_thumb.png" />
    </a>
    <div>
    <a href="embeddedesignature.md#part2"><strong>Teil 2: Code Niedrig/Nein — die Leistungsfähigkeit von Webformularen</strong></a>
    </div>
  </td>
  <td>
   <a href="embeddedesignature.md#part3">
      <img alt="Teil 3: Vereinbarung mit einem Formular senden, Daten zusammenführen" src="assets/embeddedesignature/EmbedPart3_thumb.png" />
   </a>
    <div>
    <a href="embeddedesignature.md#part3"><strong>Teil 3: Vertrag mit einem Formular senden und Daten zusammenführen</strong></a>
    </div>
  </td>
  <td>
   <a href="embeddedesignature.md#part4">
      <img alt="Teil 4: Signiererlebnis, Umleitungen und mehr einbetten" src="assets/embeddedesignature/EmbedPart4_thumb.png" />
   </a>
    <div>
    <a href="embeddedesignature.md#part4"><strong>Teil 4: Signiererlebnis, Umleitungen und mehr einbetten</strong></a>
    </div>
  </td>
</tr>
</table>

## Teil 1: Was Sie brauchen {#part1}

Im ersten Teil lernen Sie, wie Sie mit allem beginnen, was Sie für die Teile 2-4 benötigen. Beginnen wir mit API-Anmeldedaten.

* [Adobe Sign-Entwicklerkonto](https://acrobat.adobe.com/de/de/sign/developer-form.html)
* [Starter-Code](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [VS-Code (oder Editor Ihrer Wahl)](https://code.visualstudio.com)
* Python 3.x
   * Mac - Homebrew
   * Linux — Integriertes Installationsprogramm
   * Windows — Schokolade
   * Alle — https://www.python.org/downloads/

## Teil 2: Code Niedrig/Nein — die Leistungsfähigkeit von Webformularen {#part2}

Im zweiten Teil lernen Sie die Option &quot;Niedrig/Kein-Code&quot;, wenn Sie Webformulare verwenden. Es empfiehlt sich immer zu prüfen, ob Sie es vermeiden können, zuerst Code zu schreiben.

1. Greifen Sie mit Ihrem Entwicklerkonto auf Adobe Sign zu.
1. Klicken Sie auf der Startseite auf **Webformular veröffentlichen**.

   ![Screenshot Adobe Sign-Startseite](assets/embeddedesignature/embed_1.png)

1. Vereinbarung erstellen.

   ![Screenshot zum Erstellen eines Webformulars](assets/embeddedesignature/embed_2.png)

1. Betten Sie Ihre Vereinbarung auf einer einfachen HTML-Seite ein.
1. Experimentieren Sie mit dem dynamischen Hinzufügen von Abfrageparametern.

   ![Screenshot zum Hinzufügen von Abfrageparametern](assets/embeddedesignature/embed_3.png)

## Teil 3: Vertrag mit einem Formular senden und Daten zusammenführen {#part3}

In Teil 3 erstellen Sie Vereinbarungen dynamisch.

Zuerst müssen Sie den Zugriff festlegen. Mit Adobe Sign gibt es zwei Möglichkeiten, eine Verbindung über API herzustellen. OAuth Tokens &amp; Integrationsschlüssel. Wenn Sie keinen speziellen Grund haben, OAuth mit Ihrer Anwendung zu verwenden, sollten Sie zuerst die Integrationsschlüssel durchsuchen.

1. Wählen Sie **Integrationsschlüssel** im Menü **API-Informationen** unter der Registerkarte **Konto** in Adobe Sign aus.

   ![Screenshot der Suche nach dem Integrationsschlüssel](assets/embeddedesignature/embed_4.png)

Nachdem Sie nun Zugriff auf die API haben und mit ihr interagieren können, erfahren Sie, was Sie mit der API machen können.

1. Navigieren Sie zu [Adobe Sign REST API Version 6 Methods](http://adobesign.com/public/docs/restapi/v6).

   ![Screenshot der Navigation durch Adobe Sign REST API Version 6-Methoden](assets/embeddedesignature/embed_5.png)

1. Verwenden Sie das Token als &quot;Inhaberwert&quot;.

   ![Screenshot des Trägerwerts](assets/embeddedesignature/embed_6.png)

Um Ihre erste Vereinbarung zu senden, sollten Sie sich mit der Verwendung der API vertraut machen.

1. Erstellen Sie ein temporäres Dokument und senden Sie es.

>[!NOTE]
>
>JSON-basierte Anforderungsaufrufe haben die Option &quot;Modell&quot;und &quot;Minimales Modellschema&quot;. Dadurch erhalten Sie Spezifikationen und einen minimalen Nutzlastsatz.

![Screenshot zum Erstellen eines temporären Dokuments](assets/embeddedesignature/embed_7.png)

Nachdem Sie eine Vereinbarung zum ersten Mal gesendet haben, können Sie die Logik hinzufügen. Es empfiehlt sich immer, einige Helfer einzurichten, um Wiederholungen zu minimieren. Nachstehend sind einige Beispiele aufgeführt:

**Überprüfung**

![Screenshot der Validierungslogik](assets/embeddedesignature/embed_8.png)

**Kopfzeilen/Auth**

![Screenshot der Header/auth-Logik](assets/embeddedesignature/embed_9.png)

**Basis-URI**

![Screenshot der Basis-URI-Logik](assets/embeddedesignature/embed_10.png)

Achten Sie darauf, wo Transiente Dokumente innerhalb des großen Schemas des Sign-Ökosystems landen.
Transient -> Vereinbarung
Transient -> Vorlage -> Vereinbarung
Transient -> Widget -> Vereinbarung

In diesem Beispiel wird eine Vorlage als Dokumentquelle verwendet. Dies ist in der Regel die beste Methode, es sei denn, Sie haben einen soliden Grund, Dokumente dynamisch zum Unterschreiben zu generieren (z. B. alten Code oder Dokumentengenerierung).

Der Code ist recht einfach. Es verwendet ein Bibliotheksdokument (Vorlage) für die Dokumentquelle. Der erste und der zweite Unterzeichner werden dynamisch zugewiesen. Der Status `IN_PROCESS` bedeutet, dass das Dokument sofort gesendet wird. Außerdem wird `mergeFieldInfo` verwendet, um Felder dynamisch auszufüllen.

![Screenshot des Codes zum dynamischen Hinzufügen von Signaturen](assets/embeddedesignature/embed_11.png)

## Teil 4: Signiererlebnis, Umleitungen und mehr einbetten {#part4}

In vielen Fällen möchten Sie dem auslösenden Teilnehmer möglicherweise erlauben, eine Vereinbarung sofort zu signieren. Dies ist nützlich für kundenorientierte Anwendungen und Kiosks.

Wenn Sie nicht möchten, dass die erste gesendete E-Mail ausgelöst wird, können Sie das Verhalten einfach verwalten, indem Sie den API-Aufruf ändern.

![Screenshot des Codes, um das Senden von E-Mails nicht auszulösen](assets/embeddedesignature/embed_12.png)

So steuern Sie die Umleitung nach der Signatur:

![Screenshot des Codes zur Steuerung der Umleitung nach der Signatur](assets/embeddedesignature/embed_13.png)

Nach der Aktualisierung des Vereinbarungsvorgangs wird im letzten Schritt die Signatur-URL generiert. Dieser Aufruf ist ebenfalls recht einfach und generiert eine URL, über die ein Unterzeichner auf seinen Teil des Signiervorgangs zugreifen kann.

![Screenshot des Codes zum Generieren einer Unterzeichner-URL](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>Beachten Sie, dass der Vereinbarungserstellungsaufruf technisch asynchron ist. Dies bedeutet, dass eine Vereinbarungsaufforderung &quot;POST&quot;durchgeführt werden kann, die Vereinbarung jedoch noch nicht fertig ist. Die beste Methode ist, eine Wiederholungsschleife zu erstellen. Verwenden Sie eine Wiederholung oder eine andere Methode, die für Ihre Umgebung am besten geeignet ist.

![Screenshot zeigt, dass es am besten ist, eine Wiederholungsschleife zu erstellen](assets/embeddedesignature/embed_15.png)

Wenn alles zusammengesetzt ist, ist die Lösung ziemlich einfach. Sie erstellen eine Vereinbarung und generieren dann eine Signatur-URL, auf die der Unterzeichner klicken und das Signaturritual starten kann.

### Zusätzliche Themen

* [JS-Ereignisse](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Webhook-Ereignisse
   * [REST API](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
   * [Webhooks in Adobe Sign v6](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [Anforderungs-E-Mails erneut aktivieren (mit Ereignissen)](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [Zeitüberschreitung durch Wiederholung ersetzen](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)

   <br> 
* Benutzerdefinierte Erinnerungen
   * Mit der ersten Erstellung

      ![Screenshot der Navigation zu Power Automate](assets/embeddedesignature/embed_16.png)

   * Oder fügen Sie einen [In-flight](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant) hinzu

## Weitere Ressourcen

http://bit.ly/Summit21-T126

Enthält:
* Adobe Sign-Entwicklerkonto
* Adobe Sign API-Dokumente
* Beispielcode
* Visual Studio-Code
* Python
