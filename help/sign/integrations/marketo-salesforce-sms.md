---
title: Senden von Benachrichtigungen mit Acrobat Sign für Salesforce und Marketo
description: Erfahren Sie, wie Sie eine Textnachricht, eine E-Mail oder eine Push-Benachrichtigung senden, damit der Unterzeichner weiß, dass eine Vereinbarung in Bearbeitung ist.
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
jira: KT-7247
topic: Integrations
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: 51d1a59999a7132cb6e47351cc39a93d9a38eaeb
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Benachrichtigungen mit Acrobat Sign für [!DNL Salesforce] und [!DNL Marketo] senden

Erfahren Sie, wie Sie eine Textnachricht, eine E-Mail oder eine Push-Benachrichtigung senden, um den Unterzeichnern mitzuteilen, dass eine Vereinbarung in Bearbeitung ist, indem Sie Acrobat Sign, Acrobat Sign für Salesforce, Marketo und die Marketo Salesforce-Synchronisation verwenden. Um Benachrichtigungen von Marketo zu senden, müssen Sie zunächst eine Marketo-SMS-Verwaltungsfunktion erwerben oder konfigurieren. Für diese exemplarische Vorgehensweise wird [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/) verwendet, es sind jedoch andere Marketo-SMS-Lösungen verfügbar.

## Voraussetzungen

1. Installieren Sie Marketo Salesforce Sync.

   Informationen und das neueste Plug-in für Salesforce Sync sind hier [verfügbar.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Installieren Sie Acrobat Sign für Salesforce.

   Informationen zu diesem Plug-in sind hier [ verfügbar.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Benutzerdefiniertes Objekt suchen

Sobald die Marketo Salesforce-Synchronisationskonfiguration und die Konfiguration von Acrobat Sign für Salesforce abgeschlossen sind, werden im Marketo Admin-Terminal mehrere neue Optionen angezeigt.

![Administrator](assets/adminTab.png)

![Objektsynchronisierung](assets/salesforceAdmin.png)

1. Klicken Sie auf **Schema synchronisieren**, wenn dies Ihr erstes Mal ist. Klicken Sie andernfalls auf **Schema aktualisieren**.

   ![Aktualisieren](assets/refreshSchema1.png)

1. Wenn die globale Synchronisierung ausgeführt wird, deaktivieren Sie sie, indem Sie auf **Globale Synchronisierung deaktivieren** klicken.

   ![Deaktivieren](assets/disableGlobal.png)

1. Klicken Sie auf **Schema aktualisieren**.

   ![Aktualisieren von 2](assets/refreshSchema2.png)

## Benutzerdefinierte Objekte synchronisieren

Auf der rechten Seite finden Sie weitere Informationen unter Lead-, Kontakt- und Account-basierte benutzerdefinierte Objekte.

**Aktivieren Sie Sync** für die Objekte unter Lead, wenn Sie auslösen möchten, wenn ein Lead zu einer Vereinbarung in Salesforce hinzugefügt wird.

**Aktivieren Sie Synchronisation** für die Objekte unter Kontakt, wenn Sie auslösen möchten, wenn einer Vereinbarung in Salesforce ein Kontakt hinzugefügt wird.

**Aktivieren Sie Synchronisation** für die Objekte unter Konto, wenn Sie auslösen möchten, wenn ein Konto einer Vereinbarung in Salesforce hinzugefügt wird.

1. **Aktivieren Sie die Synchronisation** für die benutzerdefinierten Objekte, die unter dem gewünschten übergeordneten Objekt (Lead, Kontakt oder Konto) angezeigt werden.

   ![Benutzerdefinierte Objekte](assets/customObjects.png)

1. Die folgenden Assets zeigen, wie **Synchronisierung aktivieren**.

   ![Benutzerdefinierte Synchronisierung 1](assets/customObjectSync1.png)

   ![Benutzerdefinierte Synchronisierung 2](assets/customObjectSync2.png)

1. Wenn Sie die Synchronisation für die benutzerdefinierten Objekte aktiviert haben, aktivieren Sie die Synchronisation erneut.

   ![Global aktivieren](assets/enableGlobal.png)

## Erstellen des Programms

1. Klicken Sie im Abschnitt &quot;Marketingaktivitäten&quot; von Marketo mit der rechten Maustaste auf **Marketingaktivitäten** in der linken Leiste, wählen Sie **Neuer Kampagnenordner** aus, und geben Sie ihm einen Namen.

   ![Neuer Ordner](assets/newFolder.png)

1. Klicken Sie mit der rechten Maustaste auf den erstellten Ordner, wählen Sie **Neues Programm** aus, und geben Sie ihm einen Namen. Behalten Sie alles andere als Standard bei, und klicken Sie dann auf **Erstellen**.

   ![Neues Programm 1](assets/newProgram1.png)

   ![Neues Programm 2](assets/newProgram2.png)

## Twilio-SMS einrichten

Stellen Sie zunächst sicher, dass Sie über ein aktives Twilio-Konto verfügen und die SMS-Funktionen erworben haben, die Sie benötigen.

Das Einrichten des Marketo - Twilio SMS-Webhooks erfordert drei Twilio-Parameter von Ihrem Konto.

- Konto-SID
- Konto-Token
- Twilio-Telefonnummer

Rufen Sie diese Parameter von Ihrem Konto ab und öffnen Sie jetzt Ihre Marketo-Instanz.

1. Klicken Sie rechts oben auf **Admin**.

   ![Administrator](assets/adminTab.png)

1. Klicken Sie auf **Webhooks** und anschließend auf **Neues Webhook**.

   ![WebHooks](assets/webhooks.png)

1. Geben Sie einen **Webhook-Namen** und **Beschreibung** ein.

1. Geben Sie die folgende URL ein, und ersetzen Sie **[ACCOUNT_SID]** und **[AUTH_TOKEN]** durch Ihre Twilio-Anmeldeinformationen.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Wählen Sie **POST** als Anforderungstyp aus.

1. Geben Sie die folgende **Vorlage** ein, und ersetzen Sie **[MY_TWILIO_NUMBER]** durch Ihre Twilio-Telefonnummer und **[YOUR_MESSAGE]** durch eine Nachricht Ihrer Wahl.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Legen Sie die Codierung für Anforderungstoken auf Formular/URL fest.

1. Legen Sie den Antworttyp auf JSON fest, und klicken Sie dann auf **Speichern**.

## Smart Campaign-Trigger einrichten

1. Klicken Sie im Abschnitt Marketingaktivitäten mit der rechten Maustaste auf das von Ihnen erstellte Programm, und wählen Sie dann **Neue Smart Campaign** aus.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Benennen Sie ihn, und klicken Sie dann auf **Erstellen**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Wenn die Konfiguration für die benutzerdefinierte Objektsynchronisation korrekt durchgeführt wurde, sollten die folgenden Trigger angezeigt werden, die im Salesforce-Ordner verfügbar sind.

1. Klicken Sie auf Zur Vereinbarung hinzugefügt und ziehen Sie sie in die Smart List. Fügen Sie die Einschränkungen hinzu, die für den Auslöser gelten sollen.

   ![Zur Vereinbarung 2](assets/addedToAgreement2.png) hinzugefügt

## Einrichten des Smart Campaign Flow

1. Klicken Sie in der Smart Campaign auf die Registerkarte **Flow**. Suchen Sie den Flow **Webhook aufrufen**, ziehen Sie ihn auf die Arbeitsfläche und wählen Sie den Webhook aus, den Sie im vorherigen Abschnitt erstellt haben.

   ![Webhook aufrufen](assets/callWebhook.png)

1. Ihre SMS-Benachrichtigungskampagne für Leads, die einer Vereinbarung hinzugefügt werden, ist jetzt eingerichtet.
