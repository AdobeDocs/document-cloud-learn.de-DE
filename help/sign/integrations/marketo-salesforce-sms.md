---
title: Senden von Benachrichtigungen mit Adobe Sign für Salesforce und Marketo
description: Erfahren Sie, wie Sie eine Textnachricht, eine E-Mail oder eine Push-Benachrichtigung senden, damit der Unterzeichner weiß, dass eine Vereinbarung in Bearbeitung ist.
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: 089b6768cee4e3af8f1a349d5754d84aa3f4f69a
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Senden von Benachrichtigungen mit Adobe Sign für Salesforce und Marketo

Erfahren Sie, wie Sie eine Textnachricht, eine E-Mail oder eine Push-Benachrichtigung senden, um den Unterzeichnern mitzuteilen, dass eine Vereinbarung in Bearbeitung ist, indem Sie Adobe Sign, Adobe Sign für Salesforce, Marketo und Marketo Salesforce Sync verwenden. Um Benachrichtigungen von Marketo zu senden, müssen Sie zunächst eine Marketo-SMS-Verwaltungsfunktion erwerben oder konfigurieren. In dieser exemplarischen Vorgehensweise werden [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), aber es sind auch andere Marketo SMS-Lösungen verfügbar.

## Voraussetzungen

1. Installieren Sie Marketo Salesforce Sync.

   Informationen und das neueste Plug-in für Salesforce Sync sind verfügbar [hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Installieren Sie Adobe Sign für Salesforce.

   Informationen zu diesem Plug-in sind verfügbar [hier.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Benutzerdefiniertes Objekt suchen

Sobald die Marketo Salesforce-Synchronisationskonfiguration und die Konfiguration von Adobe Sign für Salesforce abgeschlossen sind, werden im Marketo Admin-Terminal mehrere neue Optionen angezeigt.

![Admin](assets/adminTab.png)

![Objektsynchronisation](assets/salesforceAdmin.png)

1. Klicken **Schema synchronisieren** wenn dies Ihr erstes Mal ist. Klicken Sie andernfalls auf **Schema aktualisieren**.

   ![Aktualisieren](assets/refreshSchema1.png)

1. Wenn die globale Synchronisation ausgeführt wird, deaktivieren Sie sie, indem Sie auf **Globale Synchronisierung deaktivieren**.

   ![Deaktivieren](assets/disableGlobal.png)

1. Klicken **Schema aktualisieren**.

   ![Aktualisieren 2](assets/refreshSchema2.png)

## Benutzerdefinierte Objekte synchronisieren

Auf der rechten Seite finden Sie weitere Informationen unter Lead-, Kontakt- und Account-basierte benutzerdefinierte Objekte.

**Synchronisation aktivieren** für die Objekte unter Lead, wenn Sie beim Hinzufügen eines Leads zu einer Vereinbarung in Salesforce ausgelöst werden möchten.

**Synchronisation aktivieren** für die Objekte unter Kontakt, wenn Sie beim Hinzufügen eines Kontakts zu einer Vereinbarung in Salesforce ausgelöst werden möchten.

**Synchronisation aktivieren** für die Objekte unter Konto, wenn Sie beim Hinzufügen eines Kontos zu einer Vereinbarung in Salesforce ausgelöst werden möchten.

1. **Synchronisation aktivieren** für die benutzerdefinierten Objekte, die unter dem gewünschten übergeordneten Objekt (Lead, Kontakt oder Konto) angezeigt werden.

   ![Benutzerdefinierte Objekte](assets/customObjects.png)

1. Die folgenden Elemente zeigen, wie Sie **Synchronisation aktivieren**.

   ![Benutzerdefinierte Synchronisation 1](assets/customObjectSync1.png)

   ![Benutzerdefinierte Synchronisation 2](assets/customObjectSync2.png)

1. Wenn Sie die Synchronisation für die benutzerdefinierten Objekte aktiviert haben, aktivieren Sie die Synchronisation erneut.

   ![Global aktivieren](assets/enableGlobal.png)

## Programm erstellen

1. Klicken Sie im Abschnitt &quot;Marketingaktivitäten&quot; von Marketo mit der rechten Maustaste auf **Marketing-Aktivitäten** auf der linken Leiste, wählen Sie **Neuer Kampagnenordner** und geben Sie ihm einen Namen.

   ![Neuer Ordner](assets/newFolder.png)

1. Klicken Sie mit der rechten Maustaste auf den erstellten Ordner, wählen Sie **Neues Programm** und geben Sie ihm einen Namen. Behalten Sie alles andere als Standard bei, und klicken Sie dann auf **Erstellen**.

   ![Neues Programm 1](assets/newProgram1.png)

   ![Neues Programm 2](assets/newProgram2.png)

## Twilio SMS einrichten

Stellen Sie zunächst sicher, dass Sie ein aktives Twilio-Konto haben und die SMS-Funktionen erworben haben, die Sie benötigen.

Das Einrichten des Marketo - Twilio SMS-Webhooks erfordert drei Twilio-Parameter von Ihrem Konto.

- Konto-SID
- Konto-Token
- Twilio-Telefonnummer

Rufen Sie diese Parameter von Ihrem Konto ab und öffnen Sie jetzt Ihre Marketo-Instanz.

1. Klicken Sie auf **Administrator** oben rechts.

   ![Administrator](assets/adminTab.png)

1. Klicken Sie auf **Webhooks**, dann **Neuer Webhook**.

   ![WebHooks](assets/webhooks.png)

1. Geben Sie einen **Webhook-Name** und **Beschreibung**.

1. Geben Sie die folgende URL ein, und ersetzen Sie **[ACCOUNT_SID]** und **[AUTH_TOKEN]** mit Ihren Twilio-Anmeldedaten.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Auswählen **POST** als Anforderungstyp.

1. Geben Sie Folgendes ein **Vorlage** und ersetzen Sie **[MY_TWILIO_NUMBER]** mit Ihrer Twilio Telefonnummer und **[YOUR_MESSAGE]** mit einer Nachricht Ihrer Wahl.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Legen Sie die Codierung für Anforderungstoken auf Formular/URL fest.

1. Legen Sie den Antworttyp auf JSON fest und klicken Sie dann auf **Speichern**.

## Smart Campaign-Trigger einrichten

1. Klicken Sie im Abschnitt Marketingaktivitäten mit der rechten Maustaste auf das von Ihnen erstellte Programm, und wählen Sie dann **Neue Smart Campaign**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Benennen Sie ihn und klicken Sie dann auf **Erstellen**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Wenn die Konfiguration für die benutzerdefinierte Objektsynchronisation korrekt durchgeführt wurde, sollten die folgenden Trigger angezeigt werden, die im Salesforce-Ordner verfügbar sind.

1. Klicken Sie auf Zur Vereinbarung hinzugefügt und ziehen Sie sie in die Smart List. Fügen Sie Einschränkungen hinzu, die für den Auslöser gelten sollen.

   ![Zur Vereinbarung 2 hinzugefügt](assets/addedToAgreement2.png)

## Einrichten des Smart Campaign Flow

1. Klicken Sie auf die Schaltfläche **Fluss** in der Smart Campaign. Suchen Sie nach dem Element und ziehen Sie es **Webhook aufrufen** auf die Arbeitsfläche und wählen Sie den im vorherigen Abschnitt erstellten Webhook aus.

   ![Webhook aufrufen](assets/callWebhook.png)

1. Ihre SMS-Benachrichtigungskampagne für Leads, die einer Vereinbarung hinzugefügt werden, ist jetzt eingerichtet.

>[!TIP]
>
>Dieses Tutorial ist Teil des Kurses [Schnellere Vertriebszyklen - mit Adobe Sign für Salesforce und Marketo.](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) das auf Experience League kostenlos erhältlich ist!