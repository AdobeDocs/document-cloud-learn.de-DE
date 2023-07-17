---
title: Automatisierung von Dokumenten mit Acrobat Sign für Microsoft Power Platform.
description: Erfahren Sie, wie Sie die Connectors für Acrobat Sign und Adobe PDF Tools für Microsoft Power Apps aktivieren und verwenden. Workflows zur Automatisierung von Genehmigungs- und Unterschriftsprozessen implementieren - schnell und sicher und ohne Programmierung.
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7488.jpg
jira: KT-7488
exl-id: 4113bc3f-293c-44a8-94ab-e1dbac74caed
source-git-commit: aa8fd589d214879f2bfcb6bc54576c707532fd6f
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 1%

---

# Automatisierung von Dokumenten mit Acrobat Sign für Microsoft Power Platform.

Erfahren Sie, wie Sie die Connectors für Acrobat Sign und Adobe PDF Tools für Microsoft Power Apps aktivieren und verwenden. Workflows zur Automatisierung von Genehmigungs- und Unterschriftsprozessen lassen sich schnell und sicher implementieren - ganz ohne Code. Dieses praktische Tutorial besteht aus vier Teilen, die unter den folgenden Links beschrieben werden:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="documentautomation.md#part1">
        <img alt="Teil 1: Signierte Vereinbarungen mit Acrobat Sign in SharePoint speichern" src="assets/documentautomation/AutomationPart1_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part1"><strong>Teil 1: Signierte Vereinbarungen mit Acrobat Sign in SharePoint speichern</strong></a>
    </div>
  </td>
  <td>
    <a href="documentautomation.md#part2">
        <img alt="Teil 2: Automatisierter Genehmigungsprozess für elektronische Unterschriften mit Acrobat Sign" src="assets/documentautomation/AutomationPart2_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part2"><strong>Teil 2: Automatisierter Genehmigungsprozess für elektronische Unterschriften mit Acrobat Sign</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part3">
      <img alt="Teil 3: Automatisierte OCR mit Adobe PDF Tools" src="assets/documentautomation/AutomationPart3_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part3"><strong>Teil 3: Automatisierte OCR mit Adobe PDF Tools</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part4">
      <img alt="Teil 4: Automatisierte Zusammenstellung von Dokumenten mit Adobe PDF Tools" src="assets/documentautomation/AutomationPart4_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part4"><strong>Teil 4: Automatisierte Zusammenstellung von Dokumenten mit Adobe PDF Tools</strong></a>
    </div>
  </td>
</tr>
</table>

## Voraussetzungen

* Vertrautheit mit Microsoft 365 und Power Automate
* Acrobat Sign Knowledge
* Microsoft 365-Konto mit Zugriff auf SharePoint und Power Automate (Basic für Acrobat Sign, Premium für Adobe PDF Tools)
* Entwicklerkonto für Acrobat Sign für Unternehmen oder Acrobat Sign

**Übungen 1 und 2**

* Acrobat Sign-Konto mit Zugriff auf die API. Ein Entwicklerkonto oder ein Unternehmenskonto.
* Auf die SharePoint-Website kann von Power Automate zugegriffen werden, für die Sie Bearbeitungsberechtigungen haben. Vollständiger Administratorzugriff wird empfohlen.
* Beispieldokument für die Signaturgenehmigungsanforderung und -unterzeichnung.

**Übungen 3 und 4**

Materialien herunterladen [hier](https://github.com/benvanderberg/adobe-sign-pdftools-powerautomate-tutorial)

## Teil 1: Signierte Vereinbarungen mit Acrobat Sign in SharePoint speichern {#part1}

Im ersten Teil verwendest du eine Power Automate Flow-Vorlage, um einen automatisierten Workflow einzurichten, der alle signierten Verträge auf deiner SharePoint-Website speichert.

1. Navigieren Sie zu Power Automate.
1. Suchen Sie nach Acrobat Sign.

   ![Screenshot der Navigation zu Power Automate](assets/documentautomation/automation_1.png)

1. Auswählen **Eine abgeschlossene Acrobat Sign-Vereinbarung in der SharePoint-Bibliothek speichern**.

   ![Screenshot des abgeschlossenen Vertrags zum Speichern einer Acrobat Sign in der SharePoint-Bibliotheksaktion](assets/documentautomation/automation_2.png)

1. Überprüfen Sie den Bildschirm und konfigurieren Sie alle erforderlichen Verbindungen. Aktivieren Sie die Acrobat Sign-Verbindung.
1. Klicken Sie auf das blaue `+` Symbol.

   ![Screenshot der Flussverbindung zwischen Acrobat Sign und SharePoint](assets/documentautomation/automation_3.png)

1. Geben Sie Ihre E-Mail-Adresse für das Acrobat Sign-Konto ein und klicken Sie im neuen Fenster auf das Kennwortfeld.

   ![Screenshot des Anmeldebildschirms von Acrobat Sign](assets/documentautomation/automation_4.png)

   Warten Sie einen Moment, bis Adobe Ihr Konto überprüft hat.

   >[!NOTE]
   >
   >Bei dieser Prüfung werden Sie an den entsprechenden Anmeldenamen weitergeleitet, wenn Sie eine Adobe ID oder unser Unternehmens-SSO verwenden.

1. Vollständige Anmeldung.
1. Klicken **Weiter** , um zum Bearbeitungsbildschirm von Flow zu gelangen.
1. Benennen Sie den Trigger.

   ![Screenshot des Auslösers](assets/documentautomation/automation_5.png)

1. SharePoint-Einstellungen konfigurieren.

   ![Screenshot der Konfiguration Ihrer SharePoint-Einstellungen](assets/documentautomation/automation_6.png)

   **Site-Adresse:** Ihre SharePoint-Site
   **Ordnerpfad:** Pfad zu den freigegebenen Dokumenten, die Sie verwenden möchten
   **Dateiname:** Übernehmen Sie die Standardeinstellung
   **Dateiinhalt:** Übernehmen Sie die Standardeinstellung

1. Ablauf speichern.

   ![Screenshot des Symbols &quot;Speichern&quot;](assets/documentautomation/automation_7.png)

1. Navigieren Sie mit dem blauen Zurück-Pfeil zum Übersichtsbildschirm des Textflusses. Du wirst diesen Flow im zweiten Teil testen.

   ![Screenshot des Übersichtsbildschirms für den Textfluss](assets/documentautomation/automation_8.png)

Sie werden diesen Flow im nächsten Teil testen.

## Teil 2: Automatisierter Genehmigungsprozess für elektronische Unterschriften mit Acrobat Sign {#part2}

Im zweiten Teil bauen wir den ersten Teil mit einem robusteren Flow auf und testen beide Flows, um sie in Aktion zu sehen.

1. Auswählen **Vorlagen** auf der linken Seite der Power Automate-Oberfläche.

   ![Screenshot der Vorlagenauswahl](assets/documentautomation/automation_9.png)

1. Suchen Sie nach &quot;Genehmigung durch Manager&quot;.
1. Auswählen **Genehmigung einer ausgewählten Datei durch den Anforderungs-Manager**.

   ![Screenshot der Auswahl der Genehmigung für Request Manager für eine ausgewählte Datei](assets/documentautomation/automation_10.png)

   Überprüfen Sie die Verbindungen und fügen Sie fehlende Verbindungen hinzu.

   >[!NOTE]
   >
   >Wenn dies der erste Flow ist, der mit Genehmigungen ausgeführt wird, werden diese vollständig konfiguriert, sobald der Flow ausgeführt wird.

1. Klicken **Weiter** , um zum Flussbearbeitungsbildschirm zu wechseln.

   Dieser Textfluss enthält viele vorkonfigurierte Schritte, einschließlich Fehlerüberprüfung und verschachtelte bedingte Schritte.

1. Konfigurieren **Für eine ausgewählte Datei** wie folgt:
   **Site-Adresse:** Ihre SharePoint-Site
   **Bibliotheksname:** Ihr Dokumentenrepository
1. Fügen Sie wie folgt eine Eingabe hinzu:
   **Typ**: Email
   **Name**: E-Mail des Unterzeichners

   ![Screenshot der Konfiguration des Ablaufs](assets/documentautomation/automation_11.png)

1. Konfigurieren **Dateieigenschaften abrufen:** wie folgt:
   **Site-Adresse:** Ihre SharePoint-Site
   **Bibliotheksname:** Ihr Dokumentenrepository

1. Scrollen Sie nach unten und suchen Sie nach **Wenn ja**.

   ![Screenshot der Konfiguration &quot;Wenn ja&quot;](assets/documentautomation/automation_12.png)

1. Klicken **Aktion hinzufügen** in der **Wenn ja** , um die Schritte hinzuzufügen, die zum Signieren gesendet werden sollen.

   ![Screenshot des Hinzufügens einer Aktion im Feld &quot;Wenn ja&quot;](assets/documentautomation/automation_13.png)

1. Suchen nach **SharePoint Dateiinhalt abrufen** und wählen Sie **Dateiinhalt abrufen**.

   ![Screenshot des Suchfelds](assets/documentautomation/automation_14.png)

1. Konfigurieren Sie die **Dateiinhalt abrufen** wie folgt:

   ![Screenshot der Konfiguration des Dateiinhalts abrufen](assets/documentautomation/automation_15.png)

   **Site-Adresse:** Deine SharePoint-Website.
   **Dateikennung:** Suchen Sie nach &quot;identifier&quot; und wählen Sie Identifier aus der Liste **Dateieigenschaften abrufen** -Schritt.
1. Suchen Sie nach &quot;Adobe&quot; und wählen Sie **Acrobat Sign** , um eine weitere Aktion hinzuzufügen.

   ![Screenshot des Suchmenüs](assets/documentautomation/automation_16.png)

1. Geben Sie &quot;upload&quot; in das Suchfeld für Acrobat Sign ein und wählen Sie **Dokument hochladen und Dokument-ID abrufen**.
1. Suchen nach der dynamischen Variable **Name** , um den Namen des im Trigger ausgewählten Elements/Dokuments unter **Dateiname**.
1. Klicken **Expression** im variablen Assistenten unter **Dateiinhalt**.

   ![Screenshot des Bildschirms Dokument hochladen und Dokument-ID abrufen](assets/documentautomation/automation_17.png)

1. Einen einzelnen Apostroph hinzufügen und zurück klicken, um **Dynamischer Inhalt**, löschen Sie Ihren Apostroph, wählen Sie **Dateiinhalt** und dann auf **OK**.

   Stellen Sie sicher, dass keine zusätzlichen Apostrophe vorhanden sind und es wie in der folgenden Beispieldatei aussieht.

   ![Screenshot des Bildschirms &quot;Dynamischer Inhalt&quot;](assets/documentautomation/automation_18.png)

1. Gib im Suchbereich von Acrobat Sign &quot;create&quot; ein, um eine weitere Acrobat Sign-Aktion hinzuzufügen.
1. Auswählen **Dokumente aus hochgeladenem Dokument erstellen und zur Unterzeichnung versenden**.

   ![Screenshot der Suche nach create](assets/documentautomation/automation_19.png)

1. Konfigurieren Sie die erforderlichen Informationen: Auswählen **Name** aus dem Assistenten für dynamische Variablen in **Vereinbarungsname**.
Auswählen **Dokument-ID** aus dem Assistenten für dynamische Variablen in **Dokument-ID**.
Auswählen **E-Mail des Unterzeichners** aus dem Assistenten für dynamische Variablen in **E-Mail des Teilnehmers**.
Geben Sie &quot;1&quot; in **Reihenfolge der Teilnehmer**.
Auswählen **Unterzeichner** aus der Dropdown-Liste in **Rolle des Teilnehmers**.

   ![Screenshot der erforderlichen Informationen](assets/documentautomation/automation_20.png)

1. **Speichern** den Flow fest.

### Testen des Textflusses

Rufe das Dokument-Repository deiner SharePoint-Website auf, um es zu testen.

1. Wählen Sie das Dokument aus und wählen Sie **Automatisieren** und die **Fluss** erstellt hast.

   ![Screenshot der Auswahl des Menüs &quot;Automatisieren&quot; und des Textflusses](assets/documentautomation/automation_21.png)

1. Starten Sie den Flow, um die Verbindungen zu validieren (nur beim ersten Flow).
1. Geben Sie eine nette Nachricht an den Genehmiger in **Nachricht**.
1. E-Mail für das Dokument eingeben Unterzeichner in **E-Mail des Unterzeichners**.
1. Klicken **Textfluss ausführen**.

Der konfigurierte Genehmiger für den Benutzer, der den Flow startet, erhält eine Genehmigungsanforderung. Sie können die Genehmigung per E-Mail oder über das Menü &quot;Power Automate-Aktionselemente&quot; erteilen.
Nach der Genehmigung unterschreiben Sie Ihr Dokument. Abhängig von Ihrem Benutzer und wenn er bei Sign angemeldet ist, müssen Sie die Signaturfenster möglicherweise in einem privaten Browserfenster öffnen.

![Screenshot des Öffnens in einem privaten Browserfenster](assets/documentautomation/automation_22.png)

Schließen Sie die Signatur ab und sehen Sie dann in Ihrem SharePoint-Ordner nach.

![Screenshot des Ordners &quot;SharePoint&quot;](assets/documentautomation/automation_23.png)

## Teil 3: Automatisierte OCR mit Adobe PDF Tools {#part3}

Im dritten Teil lernen Sie, wie Sie OCR in PDF automatisieren, wenn diese in Microsoft SharePoint importiert werden. Damit wird ein Problem behoben, das bei gescannten PDF-Dokumenten auftritt, die in SharePoint nicht durchsucht werden können.

![Screenshot eines PDF-Dokuments im Browser](assets/documentautomation/automation_24.png)

### Einrichten eines Ordners in SharePoint

Wechseln Sie zu Microsoft SharePoint, wo Sie Dokumente speichern möchten.

1. Klicken **+ Neu** , um einen neuen Ordner mit dem Namen &quot;Verarbeitete Verträge&quot; zu erstellen.
1. Klicken **+ Neu** , um einen neuen Ordner mit dem Namen &quot;Alte Verträge&quot; zu erstellen.

   ![Screenshot neuer Ordner](assets/documentautomation/automation_25.png)

Diese Ordner werden jetzt als Teil Ihres Power Automate -Ablaufs referenziert.

### Textfluss aus Vorlage erstellen

1. Melden Sie sich bei https://flow.microsoft.com an.
1. Klicken **Vorlagen** in der Seitenleiste.

   ![Screenshot der Vorlagenauswahl](assets/documentautomation/automation_26.png)

1. Auswählen **Konvertieren neu hinzugefügter Dateien in durchsuchbare PDF mit Text in SharePoint**.
1. Klicken Sie auf **+** neben Adobe PDF Tools.

   ![Screenshot der Auswahl des Symbols &quot;+&quot;](assets/documentautomation/automation_27.png)

1. Navigieren Sie auf einer neuen Registerkarte zu https://www.adobe.com/go/powerautomate_getstarted .
1. Klicken Sie auf **Erste Schritte**.

   ![Screenshot der Schaltfläche &quot;Erste Schritte&quot;](assets/documentautomation/automation_28.png)

1. Mit der Adobe ID anmelden

   ![Screenshot des Anmeldebildschirms](assets/documentautomation/automation_29.png)

1. Geben Sie den Namen der Anmeldeinformationen und die Beschreibung der Anmeldeinformationen ein und klicken Sie auf **Anmeldeinformationen erstellen**.

   ![Screenshot des Bildschirms &quot;Zugangsdaten erstellen&quot;](assets/documentautomation/automation_30.png)

   Lassen Sie das Fenster mit den Anmeldeinformationen geöffnet. Sie müssen sie in Microsoft Power Automate eingeben.

   ![Screenshot der Browser-Registerkarte zum Öffnen](assets/documentautomation/automation_31.png)

1. Geben Sie die Anmeldeinformationen ein und klicken Sie auf **In Microsoft Power Automate erstellen**.

   ![Screenshot der Eingabe der Anmeldeinformationen für PDF Tools](assets/documentautomation/automation_32.png)

1. Klicken Sie auf **Fortfahren**.

   ![Screenshot des Klicks auf &quot;Weiter&quot;](assets/documentautomation/automation_33.png)

   Jetzt können Sie eine Ansicht des Workflows anzeigen und müssen ihn für Ihre Umgebung konfigurieren.

1. Wählen Sie das Feld Site-Adresse aus, und wählen Sie unter dem Trigger namens die SharePoint-Site aus, die Sie verwenden. **Wenn eine Datei in einem Ordner erstellt wird**.

   ![Screenshot der Auswahl Wenn eine Datei in einem Ordner erstellt wird Auslöser](assets/documentautomation/automation_34.png)

1. Klicken Sie auf das Ordnersymbol, um zum Ordner Alte Verträge unter Ordner-ID zu navigieren.

   ![Screenshot der Auswahl des Ordners &quot;Alte Verträge&quot;](assets/documentautomation/automation_35.png)

1. Bearbeiten Sie die **Datei erstellen** Aktion am Ende des Textflusses:

   Ändern **Site-Adresse** zu Ihrer Site-Adresse.
Geben Sie den Speicherort des Ordners &quot;Verarbeitete Verträge&quot; im Ordnerpfad an.

1. Klicken **Speichern** in der rechten oberen Ecke.
1. Klicken **Test**.
1. Auswählen **Manuell**.
1. Klicken **Test**.

   ![Screenshot des Testflusses](assets/documentautomation/automation_36.png)

### Neuen Flow testen

1. Navigieren Sie zum Ordner Alte Verträge in SharePoint.
1. Navigieren Sie in den Übungsdateien, die Sie heruntergeladen haben, zu &quot;E03/Old Contracts&quot;.
1. Kopieren Sie die Dateien ReleaseFormXX.pdf in den Ordner Alte Verträge in SharePoint.

   ![Screenshot des Kopierens der Dateien](assets/documentautomation/automation_37.png)

Wenn Sie jetzt zum Ordner &quot;Verarbeitete Verträge&quot; navigieren, werden Ihre PDF angezeigt, nachdem der Flow einige Sekunden lang ausgeführt wurde. Wenn Sie die PDF öffnen, können Sie sehen, dass der Text ausgewählt werden kann.
Darüber hinaus indiziert SharePoint das Dokument, sodass Sie den Inhalt Ihrer Dokumente über die Suchleiste in SharePoint durchsuchen können.

## Teil 4: Automatisierte Zusammenstellung von Dokumenten mit Adobe PDF Tools {#part4}

Im vierten Teil dieses Tutorials lernen Sie, wie Sie anhand der Informationen, die Sie bei der Auswahl und beim Starten eines Flows in Microsoft SharePoint erhalten, eine Vielzahl von Dokumenten zusammenführen. In diesem Szenario hat der Textfluss folgende Auswirkungen:

* Fragen Sie nach Informationen, um auszuwählen, was in einem Paket für einen Kunden enthalten sein soll.
* Auf der Grundlage der bereitgestellten Informationen werden zahlreiche Dokumente zusammengeführt. Diese Dokumente enthalten ein Deckblatt und optionale Whitepaper.
* Das zusammengeführte Dokument wird in SharePoint gespeichert.

### Importieren von Übungsdateien in SharePoint

1. Öffnen Sie den Ordner E04 in den Übungsdateien.
1. Importieren Sie die Ordner &quot;Angebot&quot;, &quot;Vorlagen&quot; und &quot;Generierte Dokumente&quot; in SharePoint.

   ![Screenshot des Importordners](assets/documentautomation/automation_38.png)

Diese Ordner werden als Referenz verwendet. Insbesondere verwenden Sie die Datei proposal.docx für Ihr Angebot.

Der Ordner &quot;Vorlagen&quot; enthält die Titelseiten-Designs für verschiedene Städte. Es gibt auch einen Whitepaper-Ordner, der optionale zusätzliche Whitepaper enthält, die bei Auswahl an das Ende angehängt werden.

### Textfluss in Microsoft Power Automate importieren

1. Melden Sie sich bei Microsoft Power Automate an (https://flow.microsoft.com).
1. Klicken **Meine Flows**.

   ![Screenshot der Auswahl von &quot;Meine Flows&quot;](assets/documentautomation/automation_39.png)

1. Klicken Sie auf **Importieren**.

   ![Screenshot des Importbildschirms](assets/documentautomation/automation_40.png)

1. Klicken **Hochladen** und wählen Sie den Ordner Generateproposal_20210311231623.zip in E04/Flows/.

   ![Screenshot der Ordnerauswahl](assets/documentautomation/automation_41.png)

1. Klicken Sie auf **Importieren**.

1. Klicken Sie auf das Schraubenschlüsselsymbol unter Aktion neben **Angebot an Kunden senden**.

   ![Screenshot des Schraubenschlüsselsymbols](assets/documentautomation/automation_42.png)

1. Auswählen **Neu erstellen** unter Setup.
1. Legen Sie den Namen des Textflusses unter &quot;Ressourcenname&quot; fest.
1. Klicken Sie auf **Speichern**.

   Wiederholen Sie diesen Vorgang für die anderen Ressourcen des Typs &quot;Verwandte Themen&quot;, und wählen Sie die Verbindung aus.

   ![Screenshot der Dateispeicherung](assets/documentautomation/automation_43.png)

1. Klicken **Importieren** nachdem Sie alle Ihre Verbindungen hergestellt haben.

### Festlegen für eine ausgewählte Datei

Nachdem der Textfluss erstellt wurde, gehen Sie wie folgt vor:

1. Klicken Sie auf **Bearbeiten**.

   ![Screenshot der Stelle, an der die Bearbeitung ausgewählt werden soll](assets/documentautomation/automation_44.png)

1. Auslöser auswählen **Für eine ausgewählte Datei**.

   Fügen Sie Ihre SharePoint-Site der Site-Adresse hinzu.
Fügen Sie Ihre Bibliothek der Bibliothek hinzu.

   ![Screenshot des fertigen Auslösers](assets/documentautomation/automation_45.png)

### VorlageOrdnerpfad festlegen

1. Klicken Sie auf die Variable &quot;templateFolderPath&quot;.
1. Legen Sie den Pfad fest, zu dem sich der Vorlagenordner innerhalb der von Ihnen importierten SharePoint-Site befindet.

### Cover festlegen Dateiinhalt abrufen

1. Klicken **Abdeckung** , wodurch der Bereich erweitert wird.
1. Erweitern **Deckblatt: Dateiinhalt abrufen**.

   Legen Sie die Site-Adresse auf Ihre SharePoint-Site fest.

   ![Screenshot des erweiterten Covers](assets/documentautomation/automation_46.png)



### Ausgewählte Datei festlegen

1. Erweitern Sie die **Ausgewählte Datei** Bereichsaktion.

   Ändern Sie die Site-Adresse und den Bibliotheksnamen in Ihre SharePoint-Site bzw. Bibliothek unter **Dateieigenschaften abrufen**.
Ändern Sie die Site-Adresse in Ihre SharePoint-Site unter **Dateiinhalt abrufen**.

   ![Screenshot der erweiterten Aktion &quot;Ausgewählte Datei&quot;](assets/documentautomation/automation_47.png)

### Festlegen von Whitepapern

1. Klicken **Whitepaper** Aktion.
1. Erweitern **Bedingung: Whitepaper hinzufügen**.

   ![Screenshot der erweiterten Bedingung &quot;Whitepaper hinzufügen&quot;](assets/documentautomation/automation_48.png)

1. Erweitern **Whitepaper 1: Dateiinhalte über den Pfad abrufen**.
Bearbeiten Sie die Site-Adresse für die angegebene SharePoint-Site.

Wiederholen Sie dieselben Schritte für **Bedingung: Whitepaper 2 hinzufügen**.

### Erstellungsdatei festlegen

1. Erweitern **Datei erstellen**.

   Bearbeiten Sie Site-Adresse und Ordnerpfad zur SharePoint-Site und zum Pfad, in dem sich der Ordner &quot;Generated Docs&quot; befindet.

1. Klicken Sie auf **Speichern**.

### Den Flow testen

1. Navigieren Sie in SharePoint zum Angebotsordner.
1. Wählen Sie den Ordner Angebot.docx .

   ![Screenshot der Auswahl des Angebotsordners](assets/documentautomation/automation_49.png)

1. Wählen Sie Ihren Textfluss unter dem **Automatisieren** Menü.

   ![Screenshot der Auswahl des Automatisierungsmenüs](assets/documentautomation/automation_50.png)

1. Klicken **Weiter** , um den Textfluss zu beginnen.

   ![Screenshot der Schaltfläche &quot;Weiter&quot;](assets/documentautomation/automation_51.png)

1. Wählen Sie Ihr Cover und die Whitepaper, die Sie anhängen möchten.
1. Klicken **Textfluss ausführen**.

   ![Screenshot der Schaltfläche &quot;Textfluss ausführen&quot;](assets/documentautomation/automation_52.png)

Navigieren Sie zum Ordner &quot;Dokumente generieren&quot;. Sie sollten jetzt Ihre generierte PDF-Datei sehen.

![Screenshot des SharePoint-Verzeichnisses mit neuer PDF-Datei](assets/documentautomation/automation_53.png)

### Hinzufügen von Protect und anderen Aktionen zum Flow

Nachdem Sie einen Textfluss erstellt haben, bearbeiten Sie diesen, um das PDF-Dokument mit einem Kennwort zu verschlüsseln. Dies zeigt auch, wie Sie andere Aktionen verwenden können.

1. Navigieren Sie zurück zum Ende des Flows.
1. Klicken Sie auf **+** Zeichen zwischen **PDF zusammenführen** und **Datei erstellen**.

   ![Screenshot der Stelle, an der das Pluszeichen ausgewählt werden soll](assets/documentautomation/automation_54.png)

1. Auswählen **Aktion hinzufügen**.
1. Suchen Sie nach &quot;Adobe PDF Tools&quot;.

   ![Screenshot der Suche nach Adobe PDF](assets/documentautomation/automation_55.png)

1. Auswählen **Protect PDF von der Anzeige**.
1. Setzen Sie das Feld Dateiname mithilfe von dynamischem Inhalt auf **PDF-Dateiname von Merge-PDF**.

   ![Screenshot mit dynamischem Inhalt](assets/documentautomation/automation_56.png)

   Im Trigger befindet sich das Feld Kennwort, das Teil des Initiierungsformulars ist. Wir können das hier verwenden.

1. Suchen nach **Kennwortfeld** Dynamischen Inhalt verwenden und ihn in das Feld &quot;Kennwort&quot; platzieren.

   ![Screenshot der Kennwortsuche](assets/documentautomation/automation_57.png)

1. Dynamischen Inhalt verwenden, um ihn auf **PDF von Dateiinhalten aus Merge-PDF** im Feld Dateiinhalt .
1. Ändern Sie die **Datei erstellen** , um den Dateiinhalt von Protect PDF anstatt von Merge-PDF zu erhalten.
1. Erweitern **Datei erstellen**.
1. Löschen Sie das Feld Dateiinhalt.
1. Platzieren von dynamischem Inhalt **PDF von Dateiinhalten** von **Protect PDF von der Anzeige**.

### Den Flow testen

1. Navigieren Sie in SharePoint zum Angebotsordner.
1. Wählen Sie Angebot.docx.

   ![Screenshot der Auswahl des Angebotsordners](assets/documentautomation/automation_58.png)

1. Auswählen **Automatisieren** , um Ihren Flow auszuwählen.

   ![Screenshot der Auswahl von &quot;Automatisieren&quot; im Menü](assets/documentautomation/automation_59.png)

1. Klicken **Weiter** , um den Textfluss zu beginnen.

   ![Screenshot der Auswahl von Weiter](assets/documentautomation/automation_60.png)

1. Wählen Sie das Cover und die Whitepaper aus, die Sie anhängen möchten.
1. Legen Sie im Feld Kennwort das Kennwort fest, das Sie festlegen möchten.
1. Klicken **Textfluss ausführen**.

   ![Screenshot der ausgewählten Dateien und Schaltfläche &quot;Textfluss ausführen&quot;](assets/documentautomation/automation_61.png)

1. Navigieren Sie zum Ordner &quot;Dokumente generieren&quot;.
Sie sollten Ihre generierte PDF-Datei sehen. Öffnen Sie die PDF-Datei und Sie werden aufgefordert, Ihr PDF-Kennwort einzugeben.

   ![Screenshot der generierten PDF im SharePoint-Ordner](assets/documentautomation/automation_62.png)
