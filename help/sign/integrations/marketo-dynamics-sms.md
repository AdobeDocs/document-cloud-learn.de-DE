---
title: Senden von Benachrichtigungen mit Acrobat Sign für Microsoft Dynamics 365 und Marketo
description: Erfahren Sie, wie Sie eine Textnachricht, eine E-Mail oder eine Push-Benachrichtigung senden, damit der Unterzeichner weiß, dass eine Vereinbarung in Bearbeitung ist.
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: 60582eeaf8437ca1206f45b0b6daf96629c16b61
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Senden von Benachrichtigungen mit Adobe Sign für Microsoft Dynamics 365 und Marketo

Erfahren Sie, wie Sie mit Adobe Sign, Adobe Sign für Microsoft Dynamic, Marketo und Marketo Microsoft Dynamics Sync eine Textnachricht, eine E-Mail oder eine Push-Benachrichtigung senden, um den Unterzeichner darüber zu informieren, dass eine Vereinbarung in Bearbeitung ist. Um Benachrichtigungen von Marketo zu senden, müssen Sie zunächst eine Marketo-SMS-Verwaltungsfunktion erwerben oder konfigurieren. In dieser exemplarischen Vorgehensweise werden [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), aber es sind auch andere Marketo SMS-Lösungen verfügbar.

## Voraussetzungen

1. Installieren Sie Marketo Microsoft Dynamics Sync.

   Informationen und das neueste Plug-in für Microsoft Dynamics Sync sind verfügbar [hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Installieren Sie Adobe Sign für Microsoft Dynamics.

   Informationen zu diesem Plug-in sind verfügbar [hier.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Benutzerdefiniertes Objekt suchen

Sobald die Konfigurationen von Marketo Microsoft Dynamics Sync und Adobe Sign for Dynamics abgeschlossen sind, werden zwei neue Optionen im Marketo Admin-Terminal angezeigt.

![Admin](assets/adminTerminal.png)

* Klicken **[!UICONTROL Dynamics-Entitäten synchronisieren]**.

   Die Synchronisation muss deaktiviert sein, bevor benutzerdefinierte Entitäten synchronisiert werden. Klicken **[!UICONTROL Schema synchronisieren]** wenn dies Ihr erstes Mal ist. Klicken Sie andernfalls auf **[!UICONTROL Schema aktualisieren]**.

   ![Aktualisieren](assets/refreshSchema.png)

## Benutzerdefiniertes Objekt synchronisieren

1. Suchen Sie auf der rechten Seite nach [!UICONTROL Blei], [!UICONTROL Kontakt]und [!UICONTROL Konto]-basierte benutzerdefinierte Objekte.

   * **[!UICONTROL Synchronisation aktivieren]** für die Objekte unter Lead, wenn Sie beim Hinzufügen eines Leads zu einer Vereinbarung in Dynamics auslösen möchten.

   * **[!UICONTROL Synchronisation aktivieren]** für die Objekte unter Kontakt, wenn Sie beim Hinzufügen eines Kontakts zu einer Vereinbarung in Dynamics auslösen möchten.

   * **[!UICONTROL Synchronisation aktivieren]** für die Objekte unter Konto, wenn Sie auslösen möchten, wenn ein Konto einer Vereinbarung in Dynamics hinzugefügt wird.

   * **Synchronisation aktivieren** für das Vereinbarungsobjekt unter dem gewünschten übergeordneten Objekt (Lead, Kontakt oder Konto).

   ![Benutzerdefinierte Objekte](assets/enableSyncDynamics.png)

1. Wählen Sie im neuen Fenster die gewünschten Eigenschaften unter Vereinbarung aus.

   Aktivieren Sie die Felder unter **[!UICONTROL Einschränkung]** und **[!UICONTROL Trigger]** , um sie Ihren Marketingaktivitäten vorzustellen.

   ![Benutzerdefinierte Synchronisation 1](assets/entitySync1.png)

   ![Benutzerdefinierte Synchronisation 2](assets/entitySync2.png)

1. Aktivieren Sie die Synchronisation erneut, nachdem Sie die Synchronisation für die benutzerdefinierten Objekte aktiviert haben.

   Gehen Sie zurück zur [!UICONTROL Admin-Terminal]und klicken dann auf **[!UICONTROL Microsoft Dynamics]** klicken Sie dann auf **[!UICONTROL Synchronisation aktivieren]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Global aktivieren](assets/enableGlobalDynamics.png)

## Programm erstellen

1. In [!UICONTROL Marketing-Aktivitäten]mit der rechten Maustaste klicken **[!UICONTROL Marketing-Aktivitäten]** auf der linken Leiste, wählen Sie **[!UICONTROL Neuer Kampagnenordner]** und benennen Sie ihn.

   ![Neuer Ordner](assets/newFolder.png)

1. Klicken Sie mit der rechten Maustaste auf den erstellten Ordner, wählen Sie **[!UICONTROL Neues Programm]** und geben Sie ihm einen Namen.

   Behalten Sie alles andere als Standard bei, und klicken Sie dann auf **[!UICONTROL Erstellen]**.

   ![Neues Programm 1](assets/newProgram1.png)

   ![Neues Programm 2](assets/newProgram2.png)

## Einrichten [!DNL Twilio] SMS

Stellen Sie zunächst sicher, dass Sie über ein aktives [!DNL Twilio] und hat die SMS-Funktionen erworben, die Sie benötigen.

Einrichten der Marketo - [!DNL Twilio] SMS-Webhook erfordert drei [!DNL Twilio] -Parameter aus Ihrem Konto löschen.

* Konto-SID
* Konto-Token
* Twilio-Telefonnummer

Rufen Sie diese Parameter von Ihrem Konto ab und öffnen Sie jetzt Ihre Marketo-Instanz.

1. Klicken **[!UICONTROL Administrator]** oben rechts.

   ![Administrator](assets/adminTab.png)

1. Klicken **[!UICONTROL Webhooks]** und klicken dann auf **[!UICONTROL Neuer Webhook]**.

   ![WebHooks](assets/webhooks.png)

1. Geben Sie einen **[!UICONTROL Webhook-Name]** und **[!UICONTROL Beschreibung]**.

1. Geben Sie die folgende URL ein, und ersetzen Sie `ACCOUNT_SID` und `AUTH_TOKEN` mit Ihrem [!DNL Twilio] Anmeldedaten.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Auswählen **[!UICONTROL POST]** als Anforderungstyp.

1. Geben Sie Folgendes ein **Vorlage** und ersetzen Sie `MY_TWILIO_NUMBER` mit Ihrem [!DNL Twilio] Telefonnummer und `YOUR_MESSAGE` mit einer Nachricht Ihrer Wahl.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Legen Sie die **[!UICONTROL Token-Codierung anfordern]** bis *Formular/URL*.

1. Legen Sie den Antworttyp auf fest. *JSON* klicken Sie dann auf **[!UICONTROL Speichern]**.

## Smart Campaign-Trigger einrichten

1. Klicken Sie im Abschnitt Marketingaktivitäten mit der rechten Maustaste auf das von Ihnen erstellte Programm, und wählen Sie dann **[!UICONTROL Neue Smart Campaign]**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Benennen Sie ihn und klicken Sie dann auf **[!UICONTROL Erstellen]**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Unter dem Ordner &quot;Microsoft&quot; sollten verschiedene Trigger zur Verwendung verfügbar sein.

1. Klicken und ziehen **[!UICONTROL Zur Vereinbarung hinzugefügt]** in der **[!UICONTROL Smart List]** und fügen Sie dann die Einschränkungen hinzu, die für den Auslöser gelten sollen.

   ![Zur Vereinbarung hinzugefügt](assets/addedToAgreementDynamics.png)

## Einrichten des Smart Campaign Flow

1. Klicken Sie auf **[!UICONTROL Fluss]** &quot; im Dialogfeld &quot; [!UICONTROL Smart Campaign].

   Suchen Sie nach dem Element und ziehen Sie es **Webhook aufrufen** auf die Arbeitsfläche und wählen Sie den im vorherigen Abschnitt erstellten Webhook aus.

   ![Webhook aufrufen](assets/callWebhook.png)

1. Ihre SMS-Benachrichtigungskampagne für Leads, die einer Vereinbarung hinzugefügt werden, ist jetzt eingerichtet.
>[!TIP]
>
>Dieses Tutorial ist Teil des Kurses [Schnellere Vertriebszyklen - mit Adobe Sign für Microsoft Dynamics und Marketo.](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) das auf Experience League kostenlos erhältlich ist!