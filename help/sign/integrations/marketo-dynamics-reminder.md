---
title: Erinnerungen mit Adobe Sign für Microsoft Dynamics 365 und Marketo senden
description: Erfahren Sie, wie Sie eine E-Mail-Erinnerung senden, wenn eine Vereinbarung nach einem bestimmten Zeitraum nicht signiert bleibt
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: bcddb0ee106239f2786debaed908b2a2ec5ce792
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 3%

---

# Erinnerungen mit Adobe Sign für Microsoft Dynamics 365 und Marketo senden

Erfahren Sie, wie Sie eine E-Mail-Erinnerung senden, wenn eine Vereinbarung nach einem bestimmten Zeitraum nicht signiert wurde. Diese Integration basiert auf Adobe Sign, Adobe Sign für Microsoft Dynamics, Marketo und Marketo Microsoft Dynamics Sync.

## Voraussetzungen

1. Installieren Sie Marketo Microsoft Dynamics Sync.

   Informationen und das neueste Plugin für Microsoft Dynamics Sync sind hier verfügbar. [Hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Installieren Sie [Adobe Sign für Microsoft Dynamics](https://appsource.microsoft.com/de-de/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86).

   Informationen zu diesem Plug-in finden Sie hier.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)[

## Benutzerdefiniertes Objekt suchen

Sobald die Marketo-Konfigurationen für Microsoft Dynamics Sync und Adobe Sign for Dynamics abgeschlossen sind, werden im Marketo Admin Terminal zwei neue Optionen angezeigt.

![Admin](assets/adminTerminal.png)

1. Klicken Sie auf **[!UICONTROL Dynamics Entities Sync]**.

   Die Synchronisierung muss deaktiviert werden, bevor benutzerdefinierte Entitäten synchronisiert werden. Klicken Sie auf **Schema synchronisieren**, wenn dies Ihr erstes Mal ist. Andernfalls klicken Sie auf **Schema aktualisieren**.

   ![Aktualisieren](assets/refreshSchema.png)

## Benutzerdefiniertes Objekt synchronisieren

1. Suchen Sie auf der rechten Seite nach [!UICONTROL Lead], [!UICONTROL Kontakt] und [!UICONTROL Konto]-basierten benutzerdefinierten Objekten.

   * **Aktivieren Sie die** Synchronisation für die Objekte unter &quot; **** Leadif&quot;, wenn Sie eine Erinnerung senden möchten, wenn ein   Leader keine Vereinbarung in Dynamics signiert hat.

   * **Aktivieren Sie die** Synchronisierung für die Objekte unter  **** Kontakt, wenn Sie eine Erinnerung senden möchten, wenn ein   Kontakt keine Vereinbarung in Dynamics signiert hat.

   * **Aktivieren Sie die** Synchronisierung der Objekte unter  **** Konto, wenn Sie eine Erinnerung senden möchten, wenn ein   Konto keine Vereinbarung in Dynamics signiert hat.

   * **Aktivieren Sie die** Synchronisierung für das Vereinbarungsobjekt unter dem gewünschten  **[!UICONTROL übergeordneten]**  Element ([!UICONTROL Lead],  [!UICONTROL Kontakt] oder  [!UICONTROL Konto]).

   ![Benutzerdefinierte Objekte](assets/enableSyncDynamics.png)

1. Wählen Sie im neuen Fenster die Eigenschaften aus, die Sie unter Vereinbarung auswählen möchten, und aktivieren Sie dann die Kontrollkästchen unter **Constraint** und **Trigger**, um sie Ihren Marketingaktivitäten anzuzeigen.

   ![Benutzerdefinierte Synchronisation 1](assets/entitySync1.png)

   ![Benutzerdefinierte Synchronisation 2](assets/entitySync2.png)

1. Aktivieren Sie die Synchronisierung erneut, nachdem die Synchronisierung für die benutzerdefinierten Objekte aktiviert wurde.

   Wechseln Sie zurück zum Admin Terminal, klicken Sie auf **Microsoft Dynamics** und klicken Sie dann auf **Synchronisierung aktivieren**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Global aktivieren](assets/enableGlobalDynamics.png)

## Programm und Token erstellen

1. Klicken Sie im Bereich Marketingaktivitäten von Marketo mit der rechten Maustaste auf **Marketingaktivitäten** in der linken Leiste.

   Wählen Sie **Neuer Kampagnenordner** und geben Sie ihm einen Namen.

   ![Neuer Ordner](assets/newFolder.png)

1. Klicken Sie mit der rechten Maustaste auf den erstellten Ordner, wählen Sie **Neues Programm** und geben Sie ihm einen Namen.

   Behalten Sie alle anderen Standardeinstellungen bei und klicken Sie auf **Erstellen**.

   ![Neues Programm 1](assets/newProgram1.png)

   ![Neues Programm 2](assets/newProgram2.png)

1. Klicken Sie auf **Meine Tokens** und ziehen Sie **E-Mail-Skript** auf die Arbeitsfläche.

   ![E-Mail-Skript](assets/emailScript.png)

1. Geben Sie einen Namen ein und klicken Sie auf **Klicken Sie auf**, um zu bearbeiten.

   ![Name und Bearbeiten](assets/nameAndSave.png)

1. Erweitern Sie auf der rechten Seite **[!UICONTROL Benutzerdefinierte Objekte]** und dann das **[!UICONTROL Agreement]**-Objekt.

   Suchen Sie die URL [!UICONTROL Name], Vereinbarungsstatus, Gesendet am und Aktueller Unterzeichner und ziehen Sie sie auf die Arbeitsfläche.

1. Schreiben Sie ein Velocity-Skript mit diesen Token, um die Vereinbarungs-URL einer Vereinbarung anzuzeigen, die eine Woche lang nicht unterschrieben wird. Im Folgenden finden Sie ein Beispiel, das das aktuelle Datum mit &quot;Gesendet am&quot;vergleicht:

   ```
   #foreach($agreement in $adobe_agreementList)
       #if($agreement.adobe_esagreementstatus == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.adobe_datesent)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.adobe_name)
               #set($agreementURL = $agreement.adobe_currentsignerurl.substring(8))
               #break
           #else
           #end
       #else
       #end
   #end
   
   #if(${agreementName})
       <a href="https://${agreementURL}">${agreementName}</a>
   #else
       Please contact us. 
   #end
   ```

1. Klicken Sie auf **[!UICONTROL Speichern]**.

## Erinnerung erstellen und Personalisierung hinzufügen

Beispiele für Personalisierung: den Namen des Unterzeichners, den Namen der Vereinbarung, einen Link zur Vereinbarung usw.

1. Klicken Sie mit der rechten Maustaste auf das erstellte Programm und klicken Sie auf **[!UICONTROL Neues lokales Element]** und wählen Sie **[!UICONTROL E-Mail]**.

   ![Neue E-Mail](assets/createNewEmail.png)

1. Geben Sie auf der neuen Registerkarte einen **[!UICONTROL Name]** und **[!UICONTROL Beschreibung]** für die E-Mail ein und wählen Sie eine Vorlage aus dem Vorlagenwähler.

   ![Vorlagenwähler](assets/templatePicker.png)

1. Klicken Sie auf **[!UICONTROL Erstellen]**.

1. Legen Sie **[!UICONTROL Von Name]** und **[!UICONTROL Von Adresse]** fest.

   ![Erinnerung-E-Mail](assets/reminderEmail.png)

1. Klicken Sie auf den Nachrichtentext, um den Editor zu aktivieren.

   Klicken Sie auf die Schaltfläche **[!UICONTROL Token einfügen]**, suchen Sie das von Ihnen erstellte benutzerdefinierte Vereinbarungs-URL-Token und klicken Sie auf **[!UICONTROL Einfügen]**. Schließen Sie die Anpassung Ihrer E-Mail ab und klicken Sie auf **[!UICONTROL Speichern]**.

   ![Token einfügen](assets/insertToken.png)

1. Vorschau mithilfe eines Profils, dem eine Vereinbarung zugewiesen ist.

   Es sollte ein Link zur URL mit dem Vereinbarungsnamen als Beschriftung angezeigt werden.

   ![E-Mail-Link](assets/emailLink.png)

## Einrichten des Smart Campaign-Filters

1. Klicken Sie mit der rechten Maustaste auf das von Ihnen erstellte Programm und dann auf **[!UICONTROL Neue Smart-Kampagne]**.

   ![Intelligente Kampagne 1](assets/smartCampaign1.png)

1. Geben Sie einen Namen Ihrer Wahl ein und klicken Sie auf **[!UICONTROL Erstellen]**.

   ![Intelligente Kampagne 2](assets/smartCampaign2.png)

1. Suchen Sie nach und klicken Sie auf **[!UICONTROL Hat Vereinbarung]** und ziehen Sie sie in die Smart-Liste.

   ![Vereinbarung](assets/hasAgreementDynamics1.png)

   Die Felder, die Sie dem Auslöser bereitstellen, sollten unter **[!UICONTROL Begrenzung hinzufügen]** verfügbar sein.

1. Wählen Sie **[!UICONTROL Vereinbarungsstatus]** und alle anderen Felder aus, nach denen Sie filtern möchten.

   Definieren Sie für jedes hinzugefügte Feld die Werte, nach denen gefiltert werden soll. In diesem Fall wird nur ausgelöst, wenn **[!UICONTROL Vereinbarungsstatus]** *Zum Unterschreiben gesendet* und **[!UICONTROL Zum Unterschreiben gesendet]** *in der Vergangenheit vor 1 Woche* ist.

   ![Vereinbarungsstatus](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > Fügen Sie den Bedingungen einen eindeutigen Bezeichner hinzu, z. B. **Name**, wenn diese Kampagne nur für bestimmte Vereinbarungen ausgeführt werden soll.

1. Bestätigen Sie die Kampagnenzielgruppe und sehen Sie, wer sich auf der Registerkarte &quot;Zeitplan&quot;qualifizieren wird.

   ![Qualifikatoren](assets/qualifiers.png)

## Einrichten des Smart Campaign-Flows

Da der Kampagnenfilter **Tage bis zum Ablauf** verwendet wurde, können Sie eine geplante Wiederholung für die Kampagne verwenden.

1. Klicken Sie auf die Registerkarte **[!UICONTROL Flow]** in [!UICONTROL Smart Campaign].

   Suchen Sie den Textfluss **E-Mail senden** und ziehen Sie ihn auf die Arbeitsfläche. Wählen Sie dann die E-Mail-Erinnerung aus, die Sie im vorherigen Abschnitt erstellt haben.

   ![E-Mail senden](assets/sendEmail.png)

1. Klicken Sie in der Smart-Kampagne auf die Registerkarte **[!UICONTROL Plan]**. Stellen Sie sicher, dass der Kampagnenfluss in den **Smart-Campaign-Einstellungen** nur einmal pro Person ausgeführt wird. Klicken Sie dann auf die Registerkarte **Zeitplanwiederholung**.

   ![Registerkarte &quot;Zeitplan&quot;](assets/scheduleTab.png)

1. Setzen Sie **Schedule** auf _Daily_. Wählen Sie bei Bedarf einen Starttag, eine Uhrzeit und ein Enddatum für die Kampagne aus.

   ![Zeitplaneinstellungen](assets/scheduleSettings.png)

>[!TIP]
>
>Dieses Tutorial ist Teil des Kurses [Verkürzung der Verkaufszyklen mit Adobe Sign für Microsoft Dynamics und Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1), der kostenlos auf der Experience League verfügbar ist!