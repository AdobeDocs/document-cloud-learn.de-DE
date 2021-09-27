---
title: Benachrichtigungen mit Adobe Sign für Salesforce und Marketo senden
description: Erfahren Sie, wie Sie eine Textnachricht, E-Mail oder Push-Benachrichtigung senden, um dem Unterzeichner mitzuteilen, dass eine Vereinbarung auf dem Weg ist
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: bc79bbde966c99bdf32231ff073b49cfc759d928
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Benachrichtigungen mit Adobe Sign für Salesforce und Marketo senden

Erfahren Sie, wie Sie eine Textnachricht, E-Mail-Benachrichtigung oder Push-Benachrichtigung senden, um den Unterzeichner darüber zu informieren, dass ein Vertrag gerade mit Adobe Sign, Adobe Sign für Salesforce, Marketo und der Marketo Salesforce-Synchronisierung läuft. Um Benachrichtigungen von Marketo zu senden, müssen Sie zunächst eine Marketo SMS-Verwaltungsfunktion erwerben oder konfigurieren. Für diese exemplarische Vorgehensweise wird [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/) verwendet, es sind jedoch weitere Marketo SMS-Lösungen verfügbar.

## Voraussetzungen

1. Installieren Sie die Marketo Salesforce-Synchronisation.

   Informationen und das neueste Plugin für die Salesforce-Synchronisation finden Sie hier.[Hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Installieren Sie Adobe Sign für Salesforce.

   Informationen zu diesem Plug-in finden Sie hier.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)[

## Benutzerdefiniertes Objekt suchen

Sobald die Marketo Salesforce-Synchronisierung und die Adobe Sign für Salesforce-Konfigurationen abgeschlossen sind, werden im Marketo Admin Terminal mehrere neue Optionen angezeigt.

![Admin](assets/adminTab.png)

![Objektsynchronisierung](assets/salesforceAdmin.png)

1. Klicken Sie auf **Schema synchronisieren**, wenn dies Ihr erstes Mal ist. Andernfalls klicken Sie auf **Schema aktualisieren**.

   ![Aktualisieren](assets/refreshSchema1.png)

1. Wenn die globale Synchronisierung ausgeführt wird, deaktivieren Sie sie, indem Sie auf **Globale Synchronisierung deaktivieren** klicken.

   ![Deaktivieren](assets/disableGlobal.png)

1. Klicken Sie auf **Schema aktualisieren**.

   ![Aktualisieren 2](assets/refreshSchema2.png)

## Benutzerdefinierte Objekte synchronisieren

Auf der rechten Seite finden Sie weitere Informationen zu Lead-, Kontakt- und kontobasierten benutzerdefinierten Objekten.

**Aktivieren Sie die** Synchronisierung für die Objekte unter Lead, wenn Sie auslösen möchten, wenn ein Lead zu einer Vereinbarung in Salesforce hinzugefügt wird.

**Aktivieren Sie die** Synchronisierung für die Objekte unter Kontakt, wenn Sie auslösen möchten, wenn ein Kontakt zu einer Vereinbarung in Salesforce hinzugefügt wird.

**Aktivieren Sie die** Synchronisierung für die Objekte unter Konto, wenn Sie auslösen möchten, wenn ein Konto zu einer Vereinbarung in Salesforce hinzugefügt wird.

1. **Aktivieren Sie die** Synchronisierung für die benutzerdefinierten Objekte, die unter dem gewünschten übergeordneten Element (Lead, Kontakt oder Konto) angezeigt werden.

   ![Benutzerdefinierte Objekte](assets/customObjects.png)

1. Die folgenden Elemente zeigen, wie **Synchronisierung aktivieren** aktiviert wird.

   ![Benutzerdefinierte Synchronisation 1](assets/customObjectSync1.png)

   ![Benutzerdefinierte Synchronisation 2](assets/customObjectSync2.png)

1. Wenn Sie die Synchronisierung für die benutzerdefinierten Objekte aktiviert haben, aktivieren Sie die Synchronisierung erneut.

   ![Global aktivieren](assets/enableGlobal.png)

## Programm erstellen

1. Klicken Sie im Bereich Marketingaktivitäten von Marketo mit der rechten Maustaste auf **Marketingaktivitäten** in der linken Leiste, wählen Sie **Neuer Campaign-Ordner** und geben Sie ihm einen Namen.

   ![Neuer Ordner](assets/newFolder.png)

1. Klicken Sie mit der rechten Maustaste auf den erstellten Ordner, wählen Sie **Neues Programm** und geben Sie ihm einen Namen. Behalten Sie alle anderen Standardeinstellungen bei und klicken Sie auf **Erstellen**.

   ![Neues Programm 1](assets/newProgram1.png)

   ![Neues Programm 2](assets/newProgram2.png)

## Einrichten von Twilio SMS

Stellen Sie zunächst sicher, dass Sie über ein aktives Twilio-Konto verfügen und die SMS-Funktionen erworben haben, die Sie benötigen.

Das Einrichten des Marketo - Twilio SMS webhook erfordert drei Twilio Parameter von Ihrem Konto.

- KONTOSID
- Konto-Token
- Zweifachtelefonnummer

Rufen Sie diese Parameter von Ihrem Konto ab und öffnen Sie jetzt Ihre Marketo-Instanz.

1. Klicken Sie rechts oben auf **Admin**.

   ![Admin](assets/adminTab.png)

1. Klicken Sie auf **Webhooks**, dann **New Webhook**.

   ![WebHooks](assets/webhooks.png)

1. Geben Sie einen **Webhook-Namen** und **Beschreibung** ein.

1. Geben Sie die folgende URL ein und stellen Sie sicher, dass Sie die **[ACCOUNT_SID]** und **[AUTH_TOKEN]** durch Ihre Twilio-Anmeldedaten ersetzen.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Wählen Sie **POST** als Anforderungstyp aus.

1. Geben Sie die folgende **Vorlage** ein und stellen Sie sicher, dass **[MY_TWILIO_NUMBER]** durch Ihre Twilio-Telefonnummer und **[YOUR_MESSAGE]** durch eine Nachricht Ihrer Wahl ersetzt wird.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Legen Sie die Kodierung des Anforderungstokens auf Formular/URL fest.

1. Stellen Sie den Antworttyp auf JSON ein und klicken Sie auf **Speichern**.

## Einrichten des Smart Campaign-Triggers

1. Klicken Sie im Bereich Marketingaktivitäten mit der rechten Maustaste auf das von Ihnen erstellte Programm und wählen Sie **Neue Smart-Kampagne**.

   ![Intelligente Kampagne 1](assets/smartCampaign1.png)

1. Geben Sie einen Namen ein und klicken Sie auf **Erstellen**.

   ![Intelligente Kampagne 2](assets/smartCampaign3.png)

   Wenn die Konfiguration für die benutzerdefinierte Objektsynchronisierung korrekt ausgeführt wurde, sollten Sie die folgenden Auslöser sehen, die im Salesforce-Ordner zur Verwendung verfügbar sind.

1. Klicken Sie auf &quot;Der Vereinbarung hinzugefügt&quot;und ziehen Sie sie in die Smart-Liste. Fügen Sie Einschränkungen hinzu, die Sie für den Trigger haben möchten.

   ![Dem Abkommen 2 hinzugefügt](assets/addedToAgreement2.png)

## Einrichten des Smart Campaign-Flows

1. Klicken Sie in der Smart-Kampagne auf die Registerkarte **Flow**. Suchen und ziehen Sie den Textfluss **Call Webhook** auf die Arbeitsfläche und wählen Sie das webhook aus, das Sie im vorherigen Abschnitt erstellt haben.

   ![Webhook anrufen](assets/callWebhook.png)

1. Ihre SMS-Werbekampagne für Leads, die zu einem Vertrag hinzugefügt wurden, wurde jetzt eingerichtet.

>[!TIP]
>
>Dieses Tutorial ist Teil des Kurses [Verkürzung der Verkaufszyklen mit Adobe Sign für Salesforce und Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1), der kostenlos auf der Experience League verfügbar ist!