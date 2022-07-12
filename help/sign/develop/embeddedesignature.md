---
title: Erstellen eingebetteter Erlebnisse mit elektronischen Unterschriften und Dokumenten
description: Erfahrt, wie ihr mit Acrobat Sign-APIs Erlebnisse für elektronische Unterschriften und Dokumente in eure Web-Plattformen sowie Content- und Dokumentenmanagementsysteme einbettet.
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7489.jpg
kt: 7489
exl-id: db300cb9-6513-4a64-af60-eadedcd4858e
source-git-commit: 7a27c3ebe52bdb13f99a38abdd6a4881f7fb09c1
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 3%

---

# Integrierte Erlebnisse für elektronische Unterschriften und Dokumente erstellen

Erfahrt, wie ihr mit Acrobat Sign-APIs Erlebnisse für elektronische Unterschriften und Dokumente in eure Web-Plattformen sowie Content- und Dokumentenmanagementsysteme einbettet. Dieses praktische Tutorial besteht aus vier Teilen.

## Teil 1: Was Sie benötigen

Im ersten Teil lernst du, wie du mit allem anfängst, was du für die Teile 2-4 brauchst. Wir beginnen mit dem Abrufen von API-Zugangsberechtigungen.

+++Details zum Abrufen von API-Zugangsberechtigungen anzeigen

* [Acrobat Sign-Entwicklerkonto](https://acrobat.adobe.com/de/de/sign/developer-form.html)
* [Startcode](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [VS-Code (oder Editor Ihrer Wahl)](https://code.visualstudio.com)
* Python 3.x
   * Mac - Homebrew
   * Linux - Integriertes Installationsprogramm
   * Windows - Chocolatey
   * Alle — https://www.python.org/downloads/

+++

## Teil 2: Wenig oder kein Code - die Leistungsfähigkeit von Webformularen

Im zweiten Teil des Tutorials lernst du die Optionen kennen, mit denen du Web-Formulare mit wenig oder ohne Code ausfüllen kannst. Es ist immer ratsam, zu sehen, ob du es zunächst vermeiden kannst, Code zu schreiben.

+++Anzeigen von Details zum Erstellen eines Webformulars

1. Über das Entwicklerkonto auf Acrobat Sign zugreifen

1. Auswählen **Webformular veröffentlichen** auf der Startseite.

   ![Screenshot Acrobat Sign Homepage](assets/embeddedesignature/embed_1.png)

1. Vereinbarung erstellen

   ![Screenshot der Erstellung eines Webformulars](assets/embeddedesignature/embed_2.png)

1. Betten Sie den Vertrag in eine einfache HTML-Seite ein.

1. Experimentieren Sie mit dynamischem Hinzufügen von Abfrageparametern.

   ![Screenshot des Hinzufügens von Abfrageparametern](assets/embeddedesignature/embed_3.png)

+++

## Teil 3: Vereinbarung mit einem Formular senden und Daten zusammenführen

Im dritten Teil werden Vereinbarungen dynamisch erstellt.

+++Details zur dynamischen Erstellung von Vereinbarungen anzeigen

Zuerst müssen Sie den Zugriff einrichten. Mit Acrobat Sign gibt es zwei Möglichkeiten, eine Verbindung über API herzustellen. OAuth-Token und Integrationsschlüssel. Sofern Sie nicht einen ganz bestimmten Grund haben, OAuth mit Ihrer Anwendung zu verwenden, sollten Sie zuerst die Integrationsschlüssel überprüfen.

1. Auswählen **Integrationsschlüssel** im Fenster &quot; **API-Informationen** unter dem Menü **Konto** in Acrobat Sign.

   ![Screenshot des Speicherorts für den Integrationsschlüssel](assets/embeddedesignature/embed_4.png)

Nachdem Sie nun Zugriff haben und mit der API interagieren können, sehen Sie, was mit der API möglich ist.

1. Navigieren Sie zur Registerkarte [Acrobat Sign REST-API Version 6 - Methoden](http://adobesign.com/public/docs/restapi/v6).

   ![Screenshot der Navigation mit den Methoden der Acrobat Sign REST-API Version 6](assets/embeddedesignature/embed_5.png)

1. Verwenden Sie das Token als &quot;Bearer&quot;-Wert.

   ![Screenshot des Inhaberwerts](assets/embeddedesignature/embed_6.png)

Um Ihre erste Vereinbarung zu senden, sollten Sie wissen, wie Sie die API verwenden.

1. Erstellen Sie ein temporäres Dokument und senden Sie es.

>[!NOTE]
>
>JSON-basierte Anforderungsaufrufe verfügen über die Optionen &quot;Model&quot; und &quot;Minimal Model Schema&quot;. Dadurch erhalten Sie Spezifikationen und einen minimalen Nutzlastsatz.

![Screenshot der Erstellung eines temporären Dokuments](assets/embeddedesignature/embed_7.png)

Nachdem Sie eine Vereinbarung zum ersten Mal gesendet haben, können Sie die Logik hinzufügen. Es empfiehlt sich immer, Helfer einzusetzen, um Wiederholungen zu minimieren. Nachstehend sind einige Beispiele aufgeführt:

**Überprüfung**

![Screenshot der Validierungslogik](assets/embeddedesignature/embed_8.png)

**Kopfzeilen/Authentifizierung**

![Screenshot der Kopfzeilen/Authentifizierungslogik](assets/embeddedesignature/embed_9.png)

**Basis-URI**

![Screenshot der Basis-URI-Logik](assets/embeddedesignature/embed_10.png)

Achten Sie darauf, wo temporäre Dokumente innerhalb des Gesamtplans des Sign-Ökosystems landen.
Transient -> Vereinbarungsverzögerung -> Vorlage -> Vereinbarungsverzögerung -> Widget -> Vereinbarung

In diesem Beispiel wird eine Vorlage als Dokumentquelle verwendet. Dies ist in der Regel der beste Weg, es sei denn, Sie haben einen guten Grund, Dokumente dynamisch zum Signieren zu generieren (z. B. älterer Code oder Dokumentgenerierung).

Der Code ist recht einfach. Es verwendet ein Bibliotheksdokument (Vorlage) als Dokumentquelle. Der erste und der zweite Unterzeichner werden dynamisch zugewiesen. Die `IN_PROCESS` Status bedeutet, dass das Dokument sofort gesendet wird. Außerdem `mergeFieldInfo` wird zum dynamischen Ausfüllen von Feldern verwendet.

![Screenshot des Codes zum dynamischen Hinzufügen von Signaturen](assets/embeddedesignature/embed_11.png)

+++

## Teil 4: Einbetten von Signaturerlebnissen, Umleitungen und mehr

In vielen Fällen möchten Sie möglicherweise zulassen, dass der auslösende Teilnehmer eine Vereinbarung sofort unterzeichnet. Dies ist nützlich für kundenorientierte Anwendungen und Terminals.

+++Details zur Einbettung des Signiererlebnisses anzeigen

Wenn Sie nicht möchten, dass die erste sendende E-Mail ausgelöst wird, können Sie das Verhalten einfach verwalten, indem Sie den API-Aufruf ändern.

![Screenshot des Codes, um das Senden von E-Mails nicht auszulösen](assets/embeddedesignature/embed_12.png)

So steuern Sie die Umleitung nach Signatur:

![Screenshot des Codes zur Steuerung der Umleitung nach Signatur](assets/embeddedesignature/embed_13.png)

Nach dem Aktualisieren des Vereinbarungserstellungsprozesses wird im letzten Schritt die Signatur-URL generiert. Dieser Aufruf ist ebenfalls ziemlich einfach und generiert eine URL, die ein Unterzeichner verwenden kann, um auf seinen Teil des Signiervorgangs zuzugreifen.

![Screenshot des Codes zum Generieren einer Unterzeichner-URL](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>Beachten Sie, dass der Aufruf zur Vereinbarungserstellung technisch asynchron ist. Dies bedeutet, dass eine POST-Vereinbarungsaufforderung erfolgen kann, die Vereinbarung jedoch noch nicht fertig ist. Es empfiehlt sich, einen Wiederholungskreis einzurichten. Verwenden Sie einen Wiederholungsversuch oder eine andere Best Practice für Ihre Umgebung.

![Screenshot, der besagt, dass es Best Practice ist, eine Wiederholungsschleife einzurichten](assets/embeddedesignature/embed_15.png)

Wenn alles zusammengestellt ist, ist die Lösung ziemlich einfach. Sie treffen eine Vereinbarung und generieren dann eine Signatur-URL, auf die der Unterzeichner klicken und das Signaturritual beginnen kann.

+++

## Weitere Themen

* [JS Events](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Webhook-Ereignisse
   * [REST-API](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
   * [Webhooks in Acrobat Sign v6](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [Anforderungs-E-Mails (mit Ereignissen) erneut aktivieren](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [Zeitüberschreitung durch Wiederholung ersetzen](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)
* Benutzerdefinierte Erinnerungen
   * Mit der ersten Erstellung

      ![Screenshot der Navigation zu Power Automate](assets/embeddedesignature/embed_16.png)

   * Oder fügen Sie eine [während des Fluges](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant)
