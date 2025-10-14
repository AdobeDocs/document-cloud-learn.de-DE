---
title: Senden von Benachrichtigungen mit Acrobat Sign für Microsoft Dynamics 365 und Marketo
description: Erfahren Sie, wie Sie eine Textnachricht, eine E-Mail oder eine Push-Benachrichtigung senden, damit der Unterzeichner weiß, dass eine Vereinbarung in Bearbeitung ist.
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo Engage, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7249
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: a88ec5a68aa2a02ec2f118332ec31f47d3d5d300
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Senden von Benachrichtigungen mit Acrobat Sign für Microsoft Dynamics 365 und Marketo

Erfahren Sie, wie Sie mit Acrobat Sign, Acrobat Sign für Microsoft Dynamic, Marketo und Marketo Microsoft Dynamics Sync eine Textnachricht, eine E-Mail oder eine Push-Benachrichtigung senden, um den Unterzeichner darüber zu informieren, dass eine Vereinbarung in Bearbeitung ist. Um Benachrichtigungen von Marketo zu senden, müssen Sie zunächst eine Marketo-SMS-Verwaltungsfunktion erwerben oder konfigurieren. Für diese exemplarische Vorgehensweise wird [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/) verwendet, es sind jedoch andere Marketo-SMS-Lösungen verfügbar.

## Voraussetzungen

1. Installieren Sie Marketo Microsoft Dynamics Sync.

   Informationen und das neueste Plug-in für Microsoft Dynamics Sync sind hier [verfügbar.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html?lang=de)

1. Installieren Sie Acrobat Sign für Microsoft Dynamics.

   Informationen zu diesem Plug-in sind hier [&#x200B; verfügbar.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Benutzerdefiniertes Objekt suchen

Sobald die Marketo-Konfigurationen für Microsoft Dynamics Sync und Acrobat Sign for Dynamics abgeschlossen sind, werden zwei neue Optionen im Marketo Admin-Terminal angezeigt.

![Administrator](assets/adminTerminal.png)

* Klicken Sie auf **[!UICONTROL Synchronisierung der Dynamics-Entitäten]**.

  Die Synchronisation muss deaktiviert sein, bevor benutzerdefinierte Entitäten synchronisiert werden. Klicken Sie auf **[!UICONTROL Schema synchronisieren]**, wenn dies Ihr erstes Mal ist. Klicken Sie andernfalls auf **[!UICONTROL Schema aktualisieren]**.

  ![Aktualisieren](assets/refreshSchema.png)

## Benutzerdefiniertes Objekt synchronisieren

1. Suchen Sie auf der rechten Seite nach [!UICONTROL Lead], [!UICONTROL Kontakt] und [!UICONTROL Account]-basierten benutzerdefinierten Objekten.

   * **[!UICONTROL Aktivieren Sie Synchronisation]** für die Objekte unter Lead, wenn Sie auslösen möchten, wenn ein Lead zu einer Vereinbarung in Dynamics hinzugefügt wird.

   * **[!UICONTROL Aktivieren Sie Synchronisation]** für die Objekte unter Kontakt, wenn Sie auslösen möchten, wenn ein Kontakt zu einer Vereinbarung in Dynamics hinzugefügt wird.

   * **[!UICONTROL Aktivieren Sie Synchronisation]** für die Objekte unter Konto, wenn Sie auslösen möchten, wenn ein Konto einer Vereinbarung in Dynamics hinzugefügt wird.

   * **Synchronisierung aktivieren** für das Vereinbarungsobjekt unter dem gewünschten übergeordneten Objekt (Lead, Kontakt oder Konto).

   ![Benutzerdefinierte Objekte](assets/enableSyncDynamics.png)

1. Wählen Sie im neuen Fenster die gewünschten Eigenschaften unter Vereinbarung aus.

   Aktivieren Sie die Felder unter **[!UICONTROL Einschränkung]** und **[!UICONTROL Auslöser]**, um sie für Ihre Marketingaktivitäten verfügbar zu machen.

   ![Benutzerdefinierte Synchronisierung 1](assets/entitySync1.png)

   ![Benutzerdefinierte Synchronisierung 2](assets/entitySync2.png)

1. Aktivieren Sie die Synchronisation erneut, nachdem Sie die Synchronisation für die benutzerdefinierten Objekte aktiviert haben.

   Kehren Sie zum [!UICONTROL Admin-Terminal] zurück, klicken Sie auf **[!UICONTROL Microsoft Dynamics]**, und klicken Sie dann auf **[!UICONTROL Synchronisation aktivieren]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Global aktivieren](assets/enableGlobalDynamics.png)

## Erstellen des Programms

1. Klicken Sie in [!UICONTROL Marketingaktivitäten] in der linken Leiste mit der rechten Maustaste auf **[!UICONTROL Marketingaktivitäten]**, wählen Sie **[!UICONTROL Neuer Kampagnenordner]** aus, und geben Sie einen Namen ein.

   ![Neuer Ordner](assets/newFolder.png)

1. Klicken Sie mit der rechten Maustaste auf den erstellten Ordner, wählen Sie **[!UICONTROL Neues Programm]** aus, und geben Sie ihm einen Namen.

   Behalten Sie alles andere als Standard bei, und klicken Sie dann auf **[!UICONTROL Erstellen]**.

   ![Neues Programm 1](assets/newProgram1.png)

   ![Neues Programm 2](assets/newProgram2.png)

## [!DNL Twilio] SMS einrichten

Stellen Sie zunächst sicher, dass Sie über ein aktives [!DNL Twilio]-Konto verfügen und die erforderlichen SMS-Funktionen erworben haben.

Das Einrichten des Marketo - [!DNL Twilio] SMS-Webhooks erfordert drei [!DNL Twilio] Parameter von Ihrem Konto.

* Konto-SID
* Konto-Token
* Twilio-Telefonnummer

Rufen Sie diese Parameter von Ihrem Konto ab und öffnen Sie jetzt Ihre Marketo-Instanz.

1. Klicken Sie oben rechts auf **[!UICONTROL Admin]**.

   ![Administrator](assets/adminTab.png)

1. Klicken Sie auf **[!UICONTROL Webhooks]**, und klicken Sie dann auf **[!UICONTROL Neues Webhook]**.

   ![WebHooks](assets/webhooks.png)

1. Geben Sie einen **[!UICONTROL Webhook-Namen]** und **[!UICONTROL Beschreibung]** ein.

1. Geben Sie die folgende URL ein, und stellen Sie sicher, dass `ACCOUNT_SID` und `AUTH_TOKEN` durch Ihre [!DNL Twilio]-Anmeldeinformationen ersetzt werden.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Wählen Sie **[!UICONTROL POST]** als Anforderungstyp aus.

1. Geben Sie die **Vorlage** ein, und vergewissern Sie sich, dass `MY_TWILIO_NUMBER` durch Ihre [!DNL Twilio] Telefonnummer und `YOUR_MESSAGE` durch eine Nachricht Ihrer Wahl ersetzt wird.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Legen Sie die **[!UICONTROL Anforderungstokencodierung]** auf *Form/URL* fest.

1. Setzen Sie den Antworttyp auf *JSON*, und klicken Sie dann auf **[!UICONTROL Speichern]**.

## Smart Campaign-Trigger einrichten

1. Klicken Sie im Abschnitt Marketingaktivitäten mit der rechten Maustaste auf das von Ihnen erstellte Programm, und wählen Sie dann **[!UICONTROL Neue Smart Campaign]** aus.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Benennen Sie ihn, und klicken Sie dann auf **[!UICONTROL Erstellen]**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Unter dem Ordner &quot;Microsoft&quot; sollten verschiedene Trigger angezeigt werden, die verwendet werden können.

1. Klicken Sie auf **[!UICONTROL Zu Vereinbarung hinzugefügt]** hinzugefügt, und ziehen Sie es in die **[!UICONTROL Smart List]**. Fügen Sie dann die Einschränkungen hinzu, die für den Trigger gelten sollen.

   ![Zur Vereinbarung hinzugefügt](assets/addedToAgreementDynamics.png)

## Einrichten des Smart Campaign Flow

1. Klicken Sie in der [!UICONTROL Smart Campaign] auf die Registerkarte **[!UICONTROL Flow]**.

   Suchen Sie den Flow **Webhook aufrufen**, ziehen Sie ihn auf die Arbeitsfläche und wählen Sie den Webhook aus, den Sie im vorherigen Abschnitt erstellt haben.

   ![Webhook aufrufen](assets/callWebhook.png)

1. Ihre SMS-Benachrichtigungskampagne für Leads, die einer Vereinbarung hinzugefügt werden, ist jetzt eingerichtet.
