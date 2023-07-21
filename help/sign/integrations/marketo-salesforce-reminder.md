---
title: Erinnerungen mithilfe des Acrobat Sign für Salesforce- und Marketo-Konfigurationshandbuchs senden
description: Hier erfahren Sie, wie Sie eine E-Mail-Erinnerung von Marketo senden, wenn ein Vertrag nach einer bestimmten Zeit nicht signiert wurde.
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
jira: KT-7248
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: ad54f7afa78b0fbb31eccf455723a8890cb92355
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# Erinnerungen mithilfe des Acrobat Sign für Salesforce- und Marketo-Konfigurationshandbuchs senden

Hier erfahren Sie, wie Sie eine E-Mail-Erinnerung von Marketo senden, wenn ein Vertrag nach einer bestimmten Zeit nicht signiert wurde. Diese Integration verwendet Acrobat Sign, Acrobat Sign für Salesforce, Marketo sowie die Marketo und Salesforce Sync.

## Voraussetzungen

1. Installieren Sie Marketo Salesforce Sync.

   Informationen und das neueste Plug-in für Salesforce Sync sind verfügbar [hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Installieren Sie Acrobat Sign für Salesforce.

   Informationen zu diesem Plug-in sind verfügbar [hier.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Benutzerdefiniertes Objekt suchen

Wenn die Marketo Salesforce-Synchronisationskonfiguration und die Konfiguration von Acrobat Sign für Salesforce abgeschlossen sind, werden im Marketo Admin-Terminal mehrere neue Optionen angezeigt.

![Administration](assets/adminTab.png)

![Objektsynchronisation](assets/salesforceAdmin.png)

1. Klicken **Schema synchronisieren** wenn dies Ihr erstes Mal ist. Klicken Sie andernfalls auf **Schema aktualisieren**.

   ![Aktualisieren](assets/refreshSchema1.png)

1. Wenn die globale Synchronisation ausgeführt wird, deaktivieren Sie sie, indem Sie auf **Globale Synchronisierung deaktivieren**.

   ![Deaktivieren](assets/disableGlobal.png)

1. Klicken **Schema aktualisieren**.

   ![Aktualisieren 2](assets/refreshSchema2.png)

## Benutzerdefiniertes Objekt synchronisieren

Auf der rechten Seite finden Sie weitere Informationen unter Lead-, Kontakt- und Account-basierte benutzerdefinierte Objekte.

**Synchronisation aktivieren** für die Objekte unter &quot;Lead&quot;, wenn Sie eine Erinnerung senden möchten, wenn ein Lead keine Vereinbarung in Salesforce unterzeichnet hat.

**Synchronisation aktivieren** für die Objekte unter Kontakt, wenn Sie eine Erinnerung senden möchten, wenn ein Kontakt keine Vereinbarung in Salesforce unterzeichnet hat.

**Synchronisation aktivieren** für die Objekte unter Konto, wenn Sie eine Erinnerung senden möchten, wenn ein Konto keine Vereinbarung in Salesforce signiert hat.

1. **Synchronisation aktivieren** für die **Vereinbarung** Objekt, das unter dem gewünschten übergeordneten Element (Lead, Kontakt oder Konto) angezeigt wird. Führen Sie diesen Schritt für alle anderen benutzerdefinierten Objekte durch, die synchronisiert werden sollen.

   ![Vereinbarungsobjekt](assets/agreementObject.png)

1. Die folgenden Elemente zeigen, wie Sie **Synchronisation aktivieren**.

   ![Benutzerdefinierte Synchronisation 1](assets/customObjectSync1.png)

   ![Benutzerdefinierte Synchronisation 2](assets/customObjectSync2.png)

## Auslöser für benutzerdefinierte Objektfelder verfügbar machen

1. Während die globale Synchronisation deaktiviert ist, wählen Sie das benutzerdefinierte Vereinbarungsobjekt aus, für das Sie die Synchronisation aktiviert haben, und **Sichtbare Felder bearbeiten**.

1. Aktivieren Sie das Feld &quot;Vereinbarungsname&quot; in der Trigger-Spalte, um es den Triggern für Kampagnenaktionen anzuzeigen. Überprüfen Sie alle anderen Felder, nach denen Sie filtern möchten, und **Speichern**.

   ![Sichtbare Felder bearbeiten 1](assets/editVisible1.png)

   ![Sichtbare Felder bearbeiten 2](assets/editVisible2.png)

1. Wenn Sie die Synchronisation für die benutzerdefinierten Objekte aktiviert und die Auslöserwerte verfügbar gemacht haben, müssen Sie die Synchronisation erneut aktivieren:

   ![Global aktivieren](assets/enableGlobal.png)

## Programm und Token erstellen

1. Klicken Sie im Abschnitt &quot;Marketingaktivitäten&quot; von Marketo mit der rechten Maustaste auf **Marketing-Aktivitäten** auf der linken Leiste, wählen Sie **Neuer Kampagnenordner** und geben Sie ihm einen Namen.

   ![Neuer Ordner](assets/newFolder.png)

1. Klicken Sie mit der rechten Maustaste auf den erstellten Ordner, wählen Sie **Neues Programm** und geben Sie ihm einen Namen. Behalten Sie alles andere als Standard bei, und klicken Sie dann auf **Erstellen**.

   ![Neues Programm 1](assets/newProgram1.png)

   ![Neues Programm 2](assets/newProgram2.png)

1. Klicken Sie auf **Meine Tokens** und ziehen Sie  **E-Mail-Skript** auf die Arbeitsfläche.

   ![E-Mail-Skript](assets/emailScript.png)

1. Geben Sie einen Namen ein, und klicken Sie auf **Klicken, um zu bearbeiten**.

   ![Benennen und bearbeiten](assets/nameAndSave.png)

1. Erweitern **Benutzerdefinierte Objekte** auf der rechten Seite, und erweitern Sie dann die **Vereinbarung** Objekt. Suchen Sie den Vereinbarungsnamen, den Vereinbarungsstatus, das Signaturdatum und die Signatur-URL und ziehen Sie sie auf die Arbeitsfläche.

1. Schreiben Sie ein Velocity -Skript mit diesen Token, um die Vereinbarungs-URL einer Vereinbarung anzuzeigen, die eine Woche lang nicht signiert wurde. Hier ist ein Beispiel, das das aktuelle Datum mit dem Sendedatum vergleicht:

   ```
   #foreach($agreement in $echosign_dev1__SIGN_Agreement__cList)
       #if($agreement.echosign_dev1__Status__c == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.echosign_dev1__DateSent__c)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.Name)
               #set($agreementURL = $agreement.echosign_dev1__Signing_URL__c.substring(8))
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

1. Klicken Sie auf **Speichern**.

## Erinnerung erstellen und Personalisierung hinzufügen

Beispiele für die Personalisierung: den Namen des Unterzeichners, den Namen der Vereinbarung, einen Link zur Vereinbarung usw.

1. Klicken Sie mit der rechten Maustaste auf das von Ihnen erstellte Programm, und klicken Sie auf **Neues lokales Element** und wählen Sie dann **Email**.

   ![Neue E-Mail](assets/createNewEmail.png)

1. Geben Sie auf der neuen Registerkarte eine **Name** und **Beschreibung** für die E-Mail und wählen Sie in der Vorlagenauswahl eine Vorlage aus. Klicken Sie auf **Erstellen**.

   ![Vorlagenauswahl](assets/templatePicker.png)

1. Legen Sie die **Von Name** und **Von Adresse**.

   ![Erinnerungs-E-Mail](assets/reminderEmail.png)

1. Klicken Sie auf den Nachrichtentext, um den Editor zu aktivieren. Klicken Sie auf die Schaltfläche **Token einfügen** das von Ihnen erstellte benutzerdefinierte Vereinbarungs-URL-Token und klicken Sie auf **Einfügen**. Passen Sie Ihre E-Mail-Adresse an und klicken Sie auf **Speichern**.

   ![Token einfügen](assets/insertToken.png)

1. Vorschau mit einem Profil, dem eine Vereinbarung zugewiesen ist. Sie sollten einen Link zur URL mit dem Vereinbarungsnamen als Beschriftung sehen.

   ![E-Mail-Link](assets/emailLink.png)

## Einrichten des Smart Campaign-Filters

1. Klicken Sie mit der rechten Maustaste auf das von Ihnen erstellte Programm, und klicken Sie dann auf **Neue Smart Campaign**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Geben Sie einen Namen Ihrer Wahl ein, und klicken Sie auf **Erstellen**.

   ![Smart Campaign 2](assets/smartCampaign2.png)

1. Suchen nach, dann klicken und ziehen **Hat Vereinbarung** in die Smart-Liste aufnehmen.

   ![Hat Vereinbarung](assets/hasAgreement.png)

1. Die Felder, die Sie dem Auslöser ausgesetzt haben, sollten jetzt im **Einschränkung hinzufügen**. Auswählen **Vereinbarungsstatus** und alle anderen Felder, nach denen Sie filtern möchten. Definieren Sie für jedes hinzugefügte Feld die Werte, nach denen gefiltert werden soll. In diesem Fall wird es nur ausgelöst, wenn das Attribut **Vereinbarungsstatus** ist Zur Signatur versandt und **Sendedatum** ist in der Vergangenheit vor 7 Tagen.

   ![Vereinbarungsstatus](assets/agreementStatus.png)

   >[!NOTE]
   >
   > einen eindeutigen Bezeichner für die Einschränkungen hinzufügen, z. B. **Vereinbarungsname**, wenn diese Kampagne nur für bestimmte Vereinbarungen ausgeführt werden soll.

1. Bestätigen Sie die Zielgruppe der Kampagne, und sehen Sie auf der Registerkarte &quot;Zeitplan&quot;, wer sich qualifiziert.

   ![Qualifizierer](assets/qualifiers.png)

## Einrichten des Smart Campaign Flow

Weil der Kampagnenfilter **Tage ohne Vorzeichen** verwendet wurde, können Sie eine geplante Wiederholung für die Kampagne verwenden.

1. Klicken Sie auf die Schaltfläche **Fluss** in der Smart Campaign. Suchen Sie nach dem Element und ziehen Sie es **E-Mail senden** auf die Arbeitsfläche und wählen Sie die Erinnerungs-E-Mail aus, die Sie im vorherigen Abschnitt erstellt haben.

   ![E-Mail senden](assets/sendEmail.png)

1. Klicken Sie auf die Schaltfläche **Planen** in der Smart Campaign. Stellen Sie sicher, dass der Kampagnen-Flow auf nur einmal pro Person im **Smart Campaign-Einstellungen**. Klicken Sie dann auf die Schaltfläche **Wiederholung planen** &quot; ändern.

   ![Registerkarte Zeitplan](assets/scheduleTab.png)

1. Legen Sie die **Planen** Wählen Sie für &quot;Täglich&quot; einen Starttag und eine Startzeit sowie bei Bedarf ein Enddatum für die Kampagne aus.

   ![Zeitplaneinstellungen](assets/scheduleSettings.png)

>[!TIP]
>
>Dieses Tutorial ist Teil des Kurses [Schnellere Vertriebszyklen - mit Acrobat Sign für Salesforce und Marketo.](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) das auf Experience League kostenlos erhältlich ist!
