---
title: Automatisierung von Dokumenten mit Acrobat Sign für Microsoft Power Platform.
description: Erfahren Sie, wie Sie die Connectors für Acrobat Sign und Adobe PDF Tools für Microsoft Power Apps aktivieren und verwenden. Workflows zur Automatisierung von Genehmigungs- und Unterschriftsprozessen implementieren - schnell und sicher und ohne Programmierung.
feature: Integrations, Workflow
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7488.jpg
jira: KT-7488
exl-id: 4113bc3f-293c-44a8-94ab-e1dbac74caed
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '2448'
ht-degree: 0%

---

# Automatisierung von Dokumenten mit Acrobat Sign für Microsoft Power Platform.

Erfahren Sie, wie Sie die Connectors für Acrobat Sign und Adobe PDF Tools für Microsoft Power Apps aktivieren und verwenden. Workflows zur Automatisierung von Genehmigungs- und Unterschriftsprozessen lassen sich schnell und sicher implementieren - ganz ohne Code. Dieses praktische Tutorial besteht aus vier Teilen, die unter den folgenden Links beschrieben werden:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="documentautomation.md#part1">
        <img alt="Teil 1: Signierte Vereinbarungen in SharePoint mit Acrobat Sign speichern" src="assets/documentautomation/AutomationPart1_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part1"><strong>Teil 1: Signierte Vereinbarung in SharePoint mit Acrobat Sign speichern</strong></a>
    </div>
  </td>
  <td>
    <a href="documentautomation.md#part2">
        <img alt="Teil 2: Automatisierter Genehmigungsprozess für elektronische Unterschriften mit Acrobat Sign" src="assets/documentautomation/AutomationPart2_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part2"><strong>Teil 2: Automatisierter Genehmigungsprozess für E-Signaturen mit Acrobat Sign</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part3">
      <img alt="Teil 3: Automatisierte OCR mit Adobe PDF Tools" src="assets/documentautomation/AutomationPart3_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part3"><strong>Teil 3: Automatisierte OCR für Dokumente mit Adobe PDF Tools</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part4">
      <img alt="Teil 4: Automatisierte Zusammenstellung von Dokumenten mit Adobe PDF Tools." src="assets/documentautomation/AutomationPart4_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part4"><strong>Teil 4: Automatisierte Dokumentzusammenstellung mit Adobe PDF Tools</strong></a>
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
* Beispieldokument für die Signaturgenehmigungsanforderung und -unterschrift.

**Übungen 3 und 4**

Materialien [hier herunterladen](https://github.com/benvanderberg/adobe-sign-pdftools-powerautomate-tutorial)

## Teil 1: Signierte Vereinbarungen in SharePoint mit Acrobat Sign speichern {#part1}

Im ersten Teil verwendest du eine Power Automate Flow-Vorlage, um einen automatisierten Workflow einzurichten, der alle signierten Verträge auf deiner SharePoint-Website speichert.

1. Navigieren Sie zu Power Automate.
1. Suchen Sie nach Acrobat Sign.

   ![Screenshot der Navigation zu Power Automate](assets/documentautomation/automation_1.png)

1. Wählen Sie **Eine abgeschlossene Acrobat Sign-Vereinbarung in der SharePoint-Bibliothek speichern**.

   ![Screenshot des Abschlusses der Vereinbarung zum Speichern einer Acrobat Sign in der SharePoint-Bibliotheksaktion](assets/documentautomation/automation_2.png)

1. Überprüfen Sie den Bildschirm und konfigurieren Sie alle erforderlichen Verbindungen. Aktivieren Sie die Acrobat Sign-Verbindung.
1. Klicken Sie auf das blaue `+`-Symbol.

   ![Screenshot der Flussverbindung zwischen Acrobat Sign und SharePoint](assets/documentautomation/automation_3.png)

1. Geben Sie Ihre E-Mail-Adresse für das Acrobat Sign-Konto ein und klicken Sie im neuen Fenster auf das Kennwortfeld.

   ![Screenshot der Acrobat Sign-Anmeldung auf dem Bildschirm](assets/documentautomation/automation_4.png)

   Warten Sie einen Moment, bis Adobe Ihr Konto überprüft.

   >[!NOTE]
   >
   >Bei dieser Prüfung werden Sie an den entsprechenden Anmeldenamen weitergeleitet, wenn Sie eine Adobe ID oder unser Unternehmens-SSO verwenden.

1. Vollständige Anmeldung.
1. Klicken Sie auf **Weiter**, um zum Bearbeitungsbildschirm für den Flow zu wechseln.
1. Benennen Sie den Auslöser.

   ![Screenshot der Benennung des Triggers](assets/documentautomation/automation_5.png)

1. SharePoint-Einstellungen konfigurieren.

   ![Screenshot der Konfiguration Ihrer SharePoint-Einstellungen](assets/documentautomation/automation_6.png)

   **Site-Adresse:** Ihre SharePoint-Site
   **Ordnerpfad:** Pfad zu den freigegebenen Dokumenten, die Sie verwenden möchten
   **Dateiname:** Akzeptieren Sie den Standardwert.
   **Dateiinhalt:** Akzeptieren Sie den Standard

1. Spare den Fluss.

   ![Screenshot des Speichersymbols](assets/documentautomation/automation_7.png)

1. Navigieren Sie mit dem blauen Zurück-Pfeil zum Übersichtsbildschirm des Textflusses. Du wirst diesen Flow im zweiten Teil testen.

   ![Screenshot des Flussübersichtsbildschirms](assets/documentautomation/automation_8.png)

Sie werden diesen Flow im nächsten Teil testen.

## Teil 2: Automatisierter Genehmigungsprozess für elektronische Unterschriften mit Acrobat Sign {#part2}

Im zweiten Teil bauen wir den ersten Teil mit einem robusteren Flow auf und testen beide Flows, um sie in Aktion zu sehen.

1. Wählen Sie auf der linken Seite der Power Automate-Schnittstelle **Vorlagen** aus.

   ![Screenshot der Auswahl von Vorlagen](assets/documentautomation/automation_9.png)

1. Suchen Sie nach &quot;Genehmigung durch Manager&quot;.
1. Wählen Sie **Genehmigung des Anforderungs-Managers für eine ausgewählte Datei** aus.

   ![Screenshot der Auswahl der Genehmigung des Anforderungs-Managers für eine ausgewählte Datei](assets/documentautomation/automation_10.png)

   Überprüfen Sie die Verbindungen und fügen Sie fehlende Verbindungen hinzu.

   >[!NOTE]
   >
   >Wenn dies der erste Flow ist, der mit Genehmigungen ausgeführt wird, werden diese vollständig konfiguriert, sobald der Flow ausgeführt wird.

1. Klicken Sie auf **Weiter**, um zum Textflussbearbeitungsbildschirm zu wechseln.

   Dieser Textfluss enthält viele vorkonfigurierte Schritte, einschließlich Fehlerüberprüfung und verschachtelte bedingte Schritte.

1. Konfigurieren Sie **Für eine ausgewählte Datei** wie folgt:
   **Site-Adresse:** Ihre SharePoint-Site
   **Bibliotheksname:** Ihr Dokumentenrepository
1. Fügen Sie wie folgt eine Eingabe hinzu:
   **Typ**: E-Mail
   **Name**: E-Mail des Unterzeichners

   ![Screenshot der Konfiguration des Flows](assets/documentautomation/automation_11.png)

1. Konfigurieren Sie **Dateieigenschaften abrufen:** wie folgt:
   **Site-Adresse:** Ihre SharePoint-Site
   **Bibliotheksname:** Ihr Dokumentenrepository

1. Scrollen Sie nach unten und suchen Sie nach **Wenn ja**.

   ![Screenshot der Konfiguration &quot;Wenn ja&quot;](assets/documentautomation/automation_12.png)

1. Klicken Sie auf **Aktion hinzufügen** im Feld **Wenn ja** (nicht der unterste), um die Schritte zum Senden zur Signatur hinzuzufügen.

   ![Screenshot des Hinzufügens einer Aktion im Feld &quot;Wenn ja&quot;](assets/documentautomation/automation_13.png)

1. Suchen Sie nach **SharePoint get file content** und wählen Sie **Get file content**.

   ![Screenshot des Suchfelds](assets/documentautomation/automation_14.png)

1. Konfigurieren Sie **Dateiinhalt abrufen** wie folgt:

   ![Screenshot der Konfiguration von Dateiinhalt abrufen](assets/documentautomation/automation_15.png)

   **Site-Adresse:** Ihre SharePoint-Site.
   **Dateibezeichner:** Suchen Sie nach &quot;Bezeichner&quot; und wählen Sie &quot;Bezeichner&quot; aus dem Schritt **Dateieigenschaften abrufen**.
1. Suchen Sie nach &quot;Adobe&quot; und wählen Sie **Acrobat Sign** aus, um eine weitere Aktion hinzuzufügen.

   ![Screenshot des Suchmenüs](assets/documentautomation/automation_16.png)

1. Geben Sie &quot;upload&quot; in das Suchfeld für Acrobat Sign ein und wählen Sie **Dokument hochladen und Dokument-ID abrufen**.
1. Suchen Sie nach der dynamischen Variable &quot;**Name**&quot;, um den Namen des im Trigger ausgewählten Elements/Dokuments unter &quot;**Dateiname**&quot; abzurufen.
1. Klicken Sie im Variablenassistenten unter **Dateiinhalt** auf **Ausdruck**.

   ![Screenshot des Bildschirms Dokument hochladen und Dokument-ID abrufen](assets/documentautomation/automation_17.png)

1. Fügen Sie einen einzelnen Apostroph hinzu, klicken Sie dann auf &quot;**Dynamischer Inhalt**&quot; zurück, löschen Sie den Apostroph, wählen Sie &quot;**Dateiinhalt**&quot; aus und klicken Sie dann auf &quot;**OK**&quot;.

   Stellen Sie sicher, dass keine zusätzlichen Apostrophe vorhanden sind und es wie in der folgenden Beispieldatei aussieht.

   ![Screenshot, wie der Bildschirm &quot;Dynamischer Inhalt&quot; aussehen soll](assets/documentautomation/automation_18.png)

1. Gib im Suchbereich von Acrobat Sign &quot;create&quot; ein, um eine weitere Acrobat Sign-Aktion hinzuzufügen.
1. Wählen Sie **Vereinbarung aus hochgeladenem Dokument erstellen und zum Unterschreiben senden**.

   ![Screenshot der Suche nach create](assets/documentautomation/automation_19.png)

1. Konfigurieren Sie die erforderlichen Informationen:
Wählen Sie **Name** aus dem Assistenten für dynamische Variablen in **Vereinbarungsname**.
Wählen Sie **Dokument-ID** aus dem Assistenten für dynamische Variablen in **Dokument-ID**.
Wählen Sie **E-Mail des Unterzeichners** aus dem Assistenten für dynamische Variablen in **E-Mail des Teilnehmers** aus.
Geben Sie in **Teilnehmerreihenfolge** &quot;1&quot; ein.
Wählen Sie im Dropdown-Menü **Teilnehmerrolle** die Option **Unterzeichner** aus.

   ![Screenshot der erforderlichen Informationen](assets/documentautomation/automation_20.png)

1. **Speichern** Sie den Flow.

### Testen des Flows

Rufe das Dokument-Repository deiner SharePoint-Website auf, um es zu testen.

1. Wählen Sie das Dokument aus, und wählen Sie **Automate** und den **Flow** aus, den Sie gerade erstellt haben.

   ![Screenshot der Auswahl des Automatisierungsmenüs und des Textflusses](assets/documentautomation/automation_21.png)

1. Starten Sie den Flow, um die Verbindungen zu validieren (nur beim ersten Flow).
1. Geben Sie eine nette Nachricht an den Genehmiger in **Nachricht** ein.
1. Geben Sie die E-Mail-Adresse für den Unterzeichner des Dokuments in **E-Mail des Unterzeichners** ein.
1. Klicken Sie auf **Textfluss ausführen**.

Der konfigurierte Genehmiger für den Benutzer, der den Flow startet, erhält eine Genehmigungsanforderung. Sie können die Genehmigung per E-Mail oder über das Menü &quot;Power Automate-Aktionselemente&quot; erteilen.
Nach der Genehmigung unterschreiben Sie Ihr Dokument. Abhängig von Ihrem Benutzer und wenn er bei Sign angemeldet ist, müssen Sie die Signaturfenster möglicherweise in einem privaten Browserfenster öffnen.

![Screenshot des Öffnens im privaten Browserfenster](assets/documentautomation/automation_22.png)

Schließen Sie die Signatur ab und sehen Sie dann in Ihrem SharePoint-Ordner nach.

![Screenshot des SharePoint-Ordners](assets/documentautomation/automation_23.png)

## Teil 3: Automatisierte OCR mit Adobe PDF Tools {#part3}

Im dritten Teil lernen Sie, wie Sie OCR in PDF automatisieren, wenn diese in Microsoft SharePoint importiert werden. Damit wird ein Problem behoben, das bei gescannten PDF-Dokumenten auftritt, die in SharePoint nicht durchsucht werden können.

![Screenshot des PDF-Dokuments im Browser](assets/documentautomation/automation_24.png)

### Einrichten eines Ordners in SharePoint

Wechseln Sie zu Microsoft SharePoint, wo Sie Dokumente speichern möchten.

1. Klicken Sie auf **+ Neu**, um einen neuen Ordner mit dem Namen &quot;Verarbeitete Verträge&quot; zu erstellen.
1. Klicken Sie auf **+ Neu**, um einen neuen Ordner mit dem Namen &quot;Alte Verträge&quot; zu erstellen.

   ![Screenshot der neuen Ordner](assets/documentautomation/automation_25.png)

Diese Ordner werden jetzt als Teil Ihres Power Automate -Ablaufs referenziert.

### Erstellen von Textflüssen aus Vorlagen

1. Melden Sie sich bei https://flow.microsoft.com an.
1. Klicken Sie auf der Seitenleiste auf **Vorlagen**.

   ![Screenshot der Auswahl von Vorlagen](assets/documentautomation/automation_26.png)

1. Wählen Sie **Neu hinzugefügte Dateien in durchsuchbaren PDF in SharePoint umwandeln**.
1. Klicken Sie auf das Symbol **+** neben Adobe PDF Tools.

   ![Screenshot der Auswahl des Plus-Symbols &#x200B;](assets/documentautomation/automation_27.png)

1. Navigieren Sie auf einer neuen Registerkarte zu https://www.adobe.com/go/powerautomate_getstarted_de .
1. Klicken Sie auf **Erste Schritte**.

   ![Screenshot der Schaltfläche &quot;Erste Schritte&quot;](assets/documentautomation/automation_28.png)

1. Mit der Adobe ID anmelden

   ![Screenshot des Anmeldebildschirms](assets/documentautomation/automation_29.png)

1. Geben Sie den Namen der Anmeldeinformationen und die Beschreibung der Anmeldeinformationen ein und klicken Sie auf **Anmeldeinformationen erstellen**.

   ![Screenshot des Bildschirms &quot;Anmeldeinformationen erstellen&quot;](assets/documentautomation/automation_30.png)

   Lassen Sie das Fenster mit den Anmeldeinformationen geöffnet. Sie müssen sie in Microsoft Power Automate eingeben.

   ![Screenshot der Browserregisterkarte, die geöffnet bleiben soll](assets/documentautomation/automation_31.png)

1. Geben Sie die Anmeldeinformationen ein und klicken Sie auf **In Microsoft Power Automate erstellen**.

   ![Screenshot der Eingabe der Anmeldeinformationen für die PDF-Tools](assets/documentautomation/automation_32.png)

1. Klicken Sie auf **Fortfahren**.

   ![Screenshot des Klicks auf &quot;Weiter&quot;](assets/documentautomation/automation_33.png)

   Jetzt können Sie eine Ansicht des Workflows anzeigen und müssen ihn für Ihre Umgebung konfigurieren.

1. Wählen Sie das Feld &quot;Site-Adresse&quot; und wählen Sie unter dem Trigger &quot;**Wenn eine Datei in einem Ordner erstellt wird&quot; die SharePoint-Site aus, die Sie verwenden.**

   ![Screenshot der Auswahl Wenn eine Datei in einem Ordnerauslöser erstellt wird](assets/documentautomation/automation_34.png)

1. Klicken Sie auf das Ordnersymbol, um zum Ordner Alte Verträge unter Ordner-ID zu navigieren.

   ![Screenshot der Auswahl des Ordners &quot;Alte Verträge&quot;](assets/documentautomation/automation_35.png)

1. Bearbeiten Sie die Aktion &quot;**Datei erstellen**&quot; am unteren Rand des Flusses:

   Ändern Sie **Site-Adresse** in Ihre Site-Adresse.
Geben Sie den Speicherort des Ordners &quot;Verarbeitete Verträge&quot; im Ordnerpfad an.

1. Klicken Sie in der rechten oberen Ecke auf **Speichern**.
1. Klicken Sie auf **Test**.
1. Wählen Sie **Manuell** aus.
1. Klicken Sie auf **Test**.

   ![Screenshot des Testflusses](assets/documentautomation/automation_36.png)

### Neuen Flow testen

1. Navigieren Sie zum Ordner Alte Verträge in SharePoint.
1. Navigieren Sie in den Übungsdateien, die Sie heruntergeladen haben, zu &quot;E03/Old Contracts&quot;.
1. Kopieren Sie die Dateien ReleaseFormXX.pdf in den Ordner Alte Verträge in SharePoint.

   ![Screenshot des Kopierens der Dateien](assets/documentautomation/automation_37.png)

Wenn Sie jetzt zum Ordner &quot;Verarbeitete Verträge&quot; navigieren, werden Ihre PDF angezeigt, nachdem der Flow einige Sekunden lang ausgeführt wurde. Wenn Sie die PDF öffnen, können Sie sehen, dass der Text ausgewählt werden kann.
Darüber hinaus indiziert SharePoint das Dokument, sodass Sie den Inhalt Ihrer Dokumente über die Suchleiste in SharePoint durchsuchen können.

## Teil 4: Automatisierte Zusammenstellung von Dokumenten mit Adobe PDF Tools. {#part4}

Im vierten Teil dieses Tutorials lernen Sie, wie Sie anhand der Informationen, die Sie bei der Auswahl eines Textflusses aus Microsoft SharePoint und beim Starten dieses Textflusses angegeben haben, eine Vielzahl von Dokumenten zusammenführen. In diesem Szenario hat der Textfluss folgende Auswirkungen:

* Fragen Sie nach Informationen, um auszuwählen, was in einem Paket für einen Kunden enthalten sein soll.
* Auf der Grundlage der bereitgestellten Informationen werden zahlreiche Dokumente zusammengeführt. Diese Dokumente enthalten ein Deckblatt und optionale Whitepaper.
* Das zusammengeführte Dokument wird in SharePoint gespeichert.

### Übungsdateien in SharePoint importieren

1. Öffnen Sie den Ordner E04 in den Übungsdateien.
1. Importieren Sie die Ordner &quot;Angebot&quot;, &quot;Vorlagen&quot; und &quot;Generierte Dokumente&quot; in SharePoint.

   ![Screenshot des Imports von Ordnern](assets/documentautomation/automation_38.png)

Diese Ordner werden als Referenz verwendet. Insbesondere verwenden Sie die Datei proposal.docx für Ihr Angebot.

Im Ordner &quot;Vorlagen&quot; befindet sich der Ordner &quot;Covers&quot;, der Titelseiten-Designs für verschiedene Städte enthält. Es gibt auch einen Whitepaper-Ordner, der optionale zusätzliche Whitepaper enthält, die bei Auswahl an das Ende angehängt werden.

### Textfluss in Microsoft Power Automate importieren

1. Melden Sie sich bei Microsoft Power Automate an (https://flow.microsoft.com).
1. Klicken Sie auf **Meine Flows**.

   ![Screenshot des Ortes, an dem meine Flows ausgewählt werden](assets/documentautomation/automation_39.png)

1. Klicken Sie auf **Importieren**.

   ![Screenshot des Importbildschirms](assets/documentautomation/automation_40.png)

1. Klicken Sie auf **Hochladen** und wählen Sie den Ordner Generateproposal_20210311231623.zip in E04/Flows/.

   ![Screenshot der Auswahl von Ordner](assets/documentautomation/automation_41.png)

1. Klicken Sie auf **Importieren**.

1. Klicken Sie auf das Schraubenschlüsselsymbol unter &quot;Aktion&quot; neben **Angebot an Kunden senden**.

   ![Screenshot des Schraubenschlüsselsymbols](assets/documentautomation/automation_42.png)

1. Wählen Sie unter &quot;Setup&quot; &quot;**Als neu erstellen&quot;** aus.
1. Legen Sie den Namen des Textflusses unter &quot;Ressourcenname&quot; fest.
1. Klicke auf **Speichern**.

   Wiederholen Sie diesen Vorgang für die anderen Ressourcen des Typs &quot;Verwandte Themen&quot;, und wählen Sie die Verbindung aus.

   ![Screenshot des Speicherns der Datei](assets/documentautomation/automation_43.png)

1. Klicken Sie auf **Importieren**, nachdem Sie alle Verbindungen hergestellt haben.

### Festlegen für eine ausgewählte Datei

Nachdem der Textfluss erstellt wurde, gehen Sie wie folgt vor:

1. Klicken Sie auf **Bearbeiten**.

   ![Screenshot des Ortes, an dem die Bearbeitung ausgewählt werden soll](assets/documentautomation/automation_44.png)

1. Wählen Sie den Trigger **Für eine ausgewählte Datei**.

   Fügen Sie Ihre SharePoint-Site der Site-Adresse hinzu.
Fügen Sie Ihre Bibliothek der Bibliothek hinzu.

   ![Screenshot des abgeschlossenen Triggers](assets/documentautomation/automation_45.png)

### templateFolderPath festlegen

1. Klicken Sie auf die Variable &quot;templateFolderPath&quot;.
1. Legen Sie den Pfad fest, zu dem sich der Vorlagenordner innerhalb der von Ihnen importierten SharePoint-Site befindet.

### Cover festlegen Dateiinhalt abrufen

1. Klicken Sie auf die Aktion **Cover**, durch die der Bereich erweitert wird.
1. **Abdeckung erweitern: Dateiinhalt abrufen**.

   Legen Sie die Site-Adresse auf Ihre SharePoint-Site fest.

   ![Screenshot des erweiterten Covers](assets/documentautomation/automation_46.png)



### Ausgewählte Datei festlegen

1. Erweitern Sie die Bereichsaktion **Ausgewählte Datei**.

   Ändern Sie die Site-Adresse und den Bibliotheksnamen in Ihre SharePoint-Site bzw. -Library unter **Dateieigenschaften abrufen**.
Ändern Sie die Site-Adresse in Ihre SharePoint-Site unter **Dateiinhalt abrufen**.

   ![Screenshot der erweiterten Aktion &quot;Ausgewählte Datei&quot;](assets/documentautomation/automation_47.png)

### Festlegen von Whitepapern

1. Klicken Sie auf die Aktion **Whitepaper**.
1. **Bedingung erweitern: Whitepaper hinzufügen**.

   ![Screenshot der erweiterten Bedingung &quot;Whitepaper hinzufügen&quot;](assets/documentautomation/automation_48.png)

1. Erweitern Sie **Whitepaper 1: Abrufen von Dateiinhalten mithilfe des Pfads**.
Bearbeiten Sie die Site-Adresse für die angegebene SharePoint-Site.

Wiederholen Sie dieselben Schritte für **Bedingung: Whitepaper hinzufügen 2**.

### Erstellungsdatei festlegen

1. Erweitern Sie **Datei erstellen**.

   Bearbeiten Sie die Site-Adresse und den Ordnerpfad zur SharePoint-Site und zum Pfad, in dem sich der Ordner &quot;Generated Docs&quot; befindet.

1. Klicke auf **Speichern**.

### Testen des Interaktionsflusses

1. Navigieren Sie in SharePoint zum Angebotsordner.
1. Wählen Sie den Ordner Angebot.docx .

   ![Screenshot der Auswahl des Angebotsordners](assets/documentautomation/automation_49.png)

1. Wählen Sie Ihren Flow im Menü **Automatisieren** aus.

   ![Screenshot der Auswahl des Automatisierungsmenüs](assets/documentautomation/automation_50.png)

1. Klicken Sie auf **Weiter**, um den Textfluss zu starten.

   ![Screenshot der Auswahl der Schaltfläche &quot;Weiter&quot;](assets/documentautomation/automation_51.png)

1. Wählen Sie Ihr Cover und die Whitepaper, die Sie anhängen möchten.
1. Klicken Sie auf **Textfluss ausführen**.

   ![Screenshot der Schaltfläche &quot;Textfluss ausführen&quot;](assets/documentautomation/automation_52.png)

Navigieren Sie zum Ordner &quot;Dokumente generieren&quot;. Sie sollten jetzt Ihre generierte PDF-Datei sehen.

![Screenshot des SharePoint-Verzeichnisses mit neuer PDF-Datei](assets/documentautomation/automation_53.png)

### Hinzufügen von Protect und anderen Aktionen zum Flow

Nachdem Sie einen Textfluss erstellt haben, bearbeiten Sie den Textfluss, um das PDF-Dokument mit einem Kennwort zu verschlüsseln. In diesem Video wird auch erläutert, wie Sie andere Aktionen verwenden können.

1. Navigieren Sie zurück zum Ende des Textflusses.
1. Klicken Sie auf das Symbol **+** zwischen **PDF zusammenführen** und **Datei erstellen**.

   ![Screenshot der Stelle, an der + Symbol ausgewählt werden soll](assets/documentautomation/automation_54.png)

1. Wählen Sie **Aktion hinzufügen**.
1. Suchen Sie nach &quot;Adobe PDF Tools&quot;.

   ![Screenshot der Suche nach Adobe PDF](assets/documentautomation/automation_55.png)

1. Wählen Sie **Protect PDF aus der Anzeige aus**.
1. Verwenden Sie &quot;Dynamischer Inhalt&quot;, um das Feld &quot;Dateiname&quot; auf &quot;**&quot; festzulegen. PDF-Dateiname aus Merge-PDF**.

   ![Screenshot des dynamischen Inhalts](assets/documentautomation/automation_56.png)

   Im Trigger befindet sich das Feld Kennwort, das Teil des Initiierungsformulars ist. Wir können das hier verwenden.

1. Suchen Sie mithilfe von Dynamic Content nach **Kennwortfeld** und platzieren Sie es im Kennwortfeld.

   ![Screenshot der Suche nach Kennwort](assets/documentautomation/automation_57.png)

1. Verwenden Sie dynamischen Inhalt, um ihn auf **PDF Dateiinhalt aus Merge-PDF** im Feld Dateiinhalt festzulegen.
1. Ändern Sie die **Erstellungsdatei**, um den Dateiinhalt von der Protect-PDF zu erhalten, anstatt PDF zusammenzuführen.
1. Erweitern Sie **Datei erstellen**.
1. Löschen Sie das Feld Dateiinhalt.
1. Verwenden Sie &quot;Dynamischer Inhalt&quot;, um **PDF-Dateiinhalt** aus **Protect-PDF aus der Ansicht zu platzieren**.

### Testen des Interaktionsflusses

1. Navigieren Sie in SharePoint zum Angebotsordner.
1. Wählen Sie Angebot.docx.

   ![Screenshot der Auswahl des Angebotsordners](assets/documentautomation/automation_58.png)

1. Wählen Sie **Automatisieren** aus, um Ihren Flow auszuwählen.

   ![Screenshot der Auswahl von &quot;Automatisch&quot; aus dem Menü &#x200B;](assets/documentautomation/automation_59.png)

1. Klicken Sie auf **Weiter**, um den Textfluss zu starten.

   ![Screenshot der Auswahl von &quot;Weiter&quot;](assets/documentautomation/automation_60.png)

1. Wählen Sie das Cover und die Whitepaper aus, die Sie anhängen möchten.
1. Legen Sie im Feld Kennwort das Kennwort fest, das Sie festlegen möchten.
1. Klicken Sie auf **Textfluss ausführen**.

   ![Screenshot der ausgewählten Dateien und Schaltfläche &quot;Textfluss ausführen&quot;](assets/documentautomation/automation_61.png)

1. Navigieren Sie zum Ordner &quot;Dokumente generieren&quot;.
Sie sollten Ihre generierte PDF-Datei sehen. Öffnen Sie die PDF-Datei und Sie werden aufgefordert, Ihr PDF-Kennwort einzugeben.

   ![Screenshot der generierten PDF im SharePoint-Verzeichnis](assets/documentautomation/automation_62.png)
