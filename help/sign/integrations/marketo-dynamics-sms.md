---
title: Senden von Benachrichtigungen mit Adobe Sign für Microsoft Dynamics 365 und Marketo
description: Erfahren Sie, wie Sie eine Textnachricht, E-Mail oder Push-Benachrichtigung senden, um dem Unterzeichner mitzuteilen, dass eine Vereinbarung auf dem Weg ist
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: bcddb0ee106239f2786debaed908b2a2ec5ce792
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Senden von Benachrichtigungen mit Adobe Sign für Microsoft Dynamics 365 und Marketo

Erfahren Sie, wie Sie eine Textnachricht, E-Mail oder Push-Benachrichtigung versenden, um den Unterzeichner darüber zu informieren, dass eine Vereinbarung mit Adobe Sign, Adobe Sign für Microsoft Dynamic, Marketo und Marketo Microsoft Dynamics Sync auf dem Weg ist. Um Benachrichtigungen von Marketo zu senden, müssen Sie zunächst eine Marketo SMS-Verwaltungsfunktion erwerben oder konfigurieren. Für diese exemplarische Vorgehensweise wird [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/) verwendet, es sind jedoch weitere Marketo SMS-Lösungen verfügbar.

## Voraussetzungen

1. Installieren Sie Marketo Microsoft Dynamics Sync.

   Informationen und das neueste Plugin für Microsoft Dynamics Sync sind hier verfügbar. [Hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Installieren Sie Adobe Sign für Microsoft Dynamics.

   Informationen zu diesem Plug-in finden Sie hier.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)[

## Benutzerdefiniertes Objekt suchen

Sobald die Marketo-Konfigurationen für Microsoft Dynamics Sync und Adobe Sign for Dynamics abgeschlossen sind, werden im Marketo Admin Terminal zwei neue Optionen angezeigt.

![Admin](assets/adminTerminal.png)

* Klicken Sie auf **[!UICONTROL Dynamics Entities Sync]**.

   Die Synchronisierung muss deaktiviert werden, bevor benutzerdefinierte Entitäten synchronisiert werden. Klicken Sie auf **[!UICONTROL Schema synchronisieren]**, wenn dies Ihr erstes Mal ist. Andernfalls klicken Sie auf **[!UICONTROL Schema aktualisieren]**.

   ![Aktualisieren](assets/refreshSchema.png)

## Benutzerdefiniertes Objekt synchronisieren

1. Suchen Sie auf der rechten Seite nach [!UICONTROL Lead], [!UICONTROL Kontakt] und [!UICONTROL Konto]-basierten benutzerdefinierten Objekten.

   * **[!UICONTROL Aktivieren Sie die]** Synchronisation für die Objekte unter Lead, wenn Sie auslösen möchten, wenn ein Lead zu einer Vereinbarung in Dynamics hinzugefügt wird.

   * **[!UICONTROL Aktivieren Sie die]** Synchronisierung der Objekte unter &quot;Kontakt&quot;, wenn Sie auslösen möchten, wenn einem Vertrag in Dynamics ein Kontakt hinzugefügt wird.

   * **[!UICONTROL Aktivieren Sie die]** Synchronisierung für die Objekte unter Konto, wenn Sie auslösen möchten, wenn ein Konto zu einer Vereinbarung in Dynamics hinzugefügt wird.

   * **Aktivieren Sie die** Synchronisierung für das Vereinbarungsobjekt unter dem gewünschten übergeordneten Element (Lead, Kontakt oder Konto).

   ![Benutzerdefinierte Objekte](assets/enableSyncDynamics.png)

1. Wählen Sie im neuen Fenster die Eigenschaften aus, die Sie unter Vereinbarung auswählen möchten.

   Aktivieren Sie die Felder unter **[!UICONTROL Constraint]** und **[!UICONTROL Trigger]**, um sie Ihren Marketingaktivitäten anzuzeigen.

   ![Benutzerdefinierte Synchronisation 1](assets/entitySync1.png)

   ![Benutzerdefinierte Synchronisation 2](assets/entitySync2.png)

1. Aktivieren Sie die Synchronisierung erneut, nachdem die Synchronisierung für die benutzerdefinierten Objekte aktiviert wurde.

   Wechseln Sie zurück zum [!UICONTROL Admin Terminal], klicken Sie auf **[!UICONTROL Microsoft Dynamics]** und dann auf **[!UICONTROL Synchronisierung aktivieren]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Global aktivieren](assets/enableGlobalDynamics.png)

## Programm erstellen

1. Klicken Sie in [!UICONTROL Marketingaktivitäten] mit der rechten Maustaste auf **[!UICONTROL Marketingaktivitäten]** in der linken Leiste, wählen Sie **[!UICONTROL Neuer Campaign-Ordner]** und geben Sie ihm einen Namen.

   ![Neuer Ordner](assets/newFolder.png)

1. Klicken Sie mit der rechten Maustaste auf den erstellten Ordner, wählen Sie **[!UICONTROL Neues Programm]** und geben Sie ihm einen Namen.

   Behalten Sie alle anderen Standardeinstellungen bei und klicken Sie auf **[!UICONTROL Erstellen]**.

   ![Neues Programm 1](assets/newProgram1.png)

   ![Neues Programm 2](assets/newProgram2.png)

## Einrichten von [!DNL Twilio] SMS

Stellen Sie zunächst sicher, dass Sie über ein aktives [!DNL Twilio]-Konto verfügen und die benötigten SMS-Funktionen erworben haben.

Das Einrichten des Marketo - [!DNL Twilio] SMS webhook erfordert drei [!DNL Twilio] Parameter von Ihrem Konto.

* KONTOSID
* Konto-Token
* Zweifachtelefonnummer

Rufen Sie diese Parameter von Ihrem Konto ab und öffnen Sie Ihre Marketo-Instanz.

1. Klicken Sie rechts oben auf **[!UICONTROL Admin]**.

   ![Admin](assets/adminTab.png)

1. Klicken Sie auf **[!UICONTROL Webhooks]** und dann auf **[!UICONTROL New Webhook]**.

   ![WebHooks](assets/webhooks.png)

1. Geben Sie einen **[!UICONTROL Webhook-Namen]** und **[!UICONTROL Beschreibung]** ein.

1. Geben Sie die folgende URL ein und stellen Sie sicher, dass `ACCOUNT_SID` und `AUTH_TOKEN` durch Ihre [!DNL Twilio]-Anmeldedaten ersetzt werden.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Wählen Sie **[!UICONTROL POST]** als Anforderungstyp aus.

1. Geben Sie die folgende **Vorlage** ein und stellen Sie sicher, dass `MY_TWILIO_NUMBER` durch Ihre [!DNL Twilio]-Telefonnummer und `YOUR_MESSAGE` durch eine Nachricht Ihrer Wahl ersetzt wird.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Setzen Sie die **[!UICONTROL Request Token Encoding]** auf *Form/URL*.

1. Stellen Sie den Antworttyp auf *JSON* ein und klicken Sie auf **[!UICONTROL Speichern]**.

## Einrichten des Smart Campaign-Triggers

1. Klicken Sie im Bereich Marketingaktivitäten mit der rechten Maustaste auf das von Ihnen erstellte Programm und wählen Sie **[!UICONTROL Neue Smart-Kampagne]**.

   ![Intelligente Kampagne 1](assets/smartCampaign1.png)

1. Geben Sie einen Namen ein und klicken Sie auf **[!UICONTROL Erstellen]**.

   ![Intelligente Kampagne 2](assets/smartCampaign3.png)

   Es sollten mehrere Auslöser angezeigt werden, die im Microsoft-Ordner verwendet werden können.

1. Klicken und ziehen Sie **[!UICONTROL Zur Vereinbarung hinzugefügt]** zur **[!UICONTROL Smart-Liste]** und fügen Sie dann die Einschränkungen hinzu, die Sie für den Trigger haben möchten.

   ![Dem Vertrag hinzugefügt](assets/addedToAgreementDynamics.png)

## Einrichten des Smart Campaign-Flows

1. Klicken Sie auf die Registerkarte **[!UICONTROL Flow]** in [!UICONTROL Smart Campaign].

   Suchen und ziehen Sie den Textfluss **Call Webhook** auf die Arbeitsfläche und wählen Sie das webhook aus, das Sie im vorherigen Abschnitt erstellt haben.

   ![Webhook anrufen](assets/callWebhook.png)

1. Ihre SMS-Werbekampagne für Leads, die zu einem Vertrag hinzugefügt wurden, wurde jetzt eingerichtet.
>[!TIP]
>
>Dieses Tutorial ist Teil des Kurses [Verkürzung der Verkaufszyklen mit Adobe Sign für Microsoft Dynamics und Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1), der kostenlos auf der Experience League verfügbar ist!