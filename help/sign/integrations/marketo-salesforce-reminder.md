---
title: Senden von Erinnerungen mithilfe des Adobe Sign für Salesforce und des Marketo-Konfigurationshandbuchs
description: Erfahren Sie, wie Sie eine E-Mail-Erinnerung von Marketo senden, wenn eine Vereinbarung nach einem bestimmten Zeitraum nicht signiert bleibt
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: bc79bbde966c99bdf32231ff073b49cfc759d928
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# Senden von Erinnerungen mithilfe des Adobe Sign für Salesforce und des Marketo-Konfigurationshandbuchs

Erfahren Sie, wie Sie eine E-Mail-Erinnerung von Marketo senden, wenn eine Vereinbarung nach einem bestimmten Zeitraum nicht signiert wurde. Diese Integration basiert auf Adobe Sign, Adobe Sign für Salesforce, Marketo und der Marketo- und Salesforce-Synchronisation.

## Voraussetzungen

1. Installieren Sie die Marketo Salesforce-Synchronisation.

   Informationen und das neueste Plugin für die Salesforce-Synchronisation finden Sie hier.[Hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Installieren Sie Adobe Sign für Salesforce.

   Informationen zu diesem Plug-in finden Sie hier.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)[

## Benutzerdefiniertes Objekt suchen

Wenn die Marketo Salesforce Sync- und Adobe Sign for Salesforce-Konfigurationen abgeschlossen sind, werden im Marketo Admin Terminal mehrere neue Optionen angezeigt.

![Admin](assets/adminTab.png)

![Objektsynchronisierung](assets/salesforceAdmin.png)

1. Klicken Sie auf **Schema synchronisieren**, wenn dies Ihr erstes Mal ist. Andernfalls klicken Sie auf **Schema aktualisieren**.

   ![Aktualisieren](assets/refreshSchema1.png)

1. Wenn die globale Synchronisierung ausgeführt wird, deaktivieren Sie sie, indem Sie auf **Globale Synchronisierung deaktivieren** klicken.

   ![Deaktivieren](assets/disableGlobal.png)

1. Klicken Sie auf **Schema aktualisieren**.

   ![Aktualisieren 2](assets/refreshSchema2.png)

## Benutzerdefiniertes Objekt synchronisieren

Auf der rechten Seite finden Sie weitere Informationen zu Lead-, Kontakt- und kontobasierten benutzerdefinierten Objekten.

**Aktivieren Sie die** Synchronisierung der Objekte unter Lead, wenn Sie eine Erinnerung senden möchten, wenn ein Lead keine Vereinbarung in Salesforce signiert hat.

**Aktivieren Sie die** Synchronisierung der Objekte unter &quot;Kontakt&quot;, wenn Sie eine Erinnerung senden möchten, wenn ein Kontakt keine Vereinbarung in Salesforce signiert hat.

**Aktivieren Sie die** Synchronisierung der Objekte unter Konto, wenn Sie eine Erinnerung senden möchten, wenn ein Konto keine Vereinbarung in Salesforce signiert hat.

1. **Aktivieren Sie die** Synchronisierung für das  **** Vereinbarungsobjekt, das unter dem gewünschten übergeordneten Element (Lead, Kontakt oder Konto) angezeigt wird. Führen Sie diese Schritte für alle anderen benutzerdefinierten Objekte aus, die synchronisiert werden sollen.

   ![Vereinbarungsobjekt](assets/agreementObject.png)

1. Die folgenden Elemente zeigen, wie **Synchronisierung aktivieren** aktiviert wird.

   ![Benutzerdefinierte Synchronisation 1](assets/customObjectSync1.png)

   ![Benutzerdefinierte Synchronisation 2](assets/customObjectSync2.png)

## Auslöser für benutzerdefinierte Objektfelder öffnen

1. Während die globale Synchronisation deaktiviert ist, wählen Sie das benutzerdefinierte Vereinbarungsobjekt aus, für das Sie die Synchronisierung aktiviert haben, und **Sichtbare Felder bearbeiten**.

1. Aktivieren Sie das Feld &quot;Vereinbarungsname&quot;in der Auslöserspalte, um es Ihren Kampagnenaktionssauslösern anzuzeigen. Überprüfen Sie alle anderen Felder, nach denen Sie filtern möchten, und klicken Sie dann auf **Speichern**.

   ![Sichtbare Felder bearbeiten 1](assets/editVisible1.png)

   ![Sichtbare Felder bearbeiten 2](assets/editVisible2.png)

1. Wenn Sie die Synchronisierung für die benutzerdefinierten Objekte aktiviert und die Auslöserwerte angezeigt haben, müssen Sie die Synchronc erneut aktivieren:

   ![Global aktivieren](assets/enableGlobal.png)

## Programm und Token erstellen

1. Klicken Sie im Bereich Marketingaktivitäten von Marketo mit der rechten Maustaste auf **Marketingaktivitäten** in der linken Leiste, wählen Sie **Neuer Campaign-Ordner** und geben Sie ihm einen Namen.

   ![Neuer Ordner](assets/newFolder.png)

1. Klicken Sie mit der rechten Maustaste auf den erstellten Ordner, wählen Sie **Neues Programm** und geben Sie ihm einen Namen. Behalten Sie alle anderen Standardeinstellungen bei und klicken Sie auf **Erstellen**.

   ![Neues Programm 1](assets/newProgram1.png)

   ![Neues Programm 2](assets/newProgram2.png)

1. Klicken Sie auf **Meine Tokens** und ziehen Sie **E-Mail-Skript** auf die Arbeitsfläche.

   ![E-Mail-Skript](assets/emailScript.png)

1. Geben Sie einen Namen ein und klicken Sie auf **Klicken Sie auf**, um zu bearbeiten.

   ![Name und Bearbeiten](assets/nameAndSave.png)

1. Erweitern Sie auf der rechten Seite **Benutzerdefinierte Objekte** und dann das **Agreement**-Objekt. Suchen Sie den Vereinbarungsnamen, den Vereinbarungsstatus, das Signaturdatum und die Signatur-URL und ziehen Sie sie auf die Arbeitsfläche.

1. Schreiben Sie ein Velocity-Skript mit diesen Token, um die Vereinbarungs-URL einer Vereinbarung anzuzeigen, die eine Woche lang nicht unterschrieben wird. Im Folgenden finden Sie ein Beispiel, das das aktuelle Datum mit dem gesendeten Datum vergleicht:

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

Beispiele für Personalisierung: den Namen des Unterzeichners, den Namen der Vereinbarung, einen Link zur Vereinbarung usw.

1. Klicken Sie mit der rechten Maustaste auf das erstellte Programm und klicken Sie auf **Neues lokales Element** und wählen Sie **E-Mail**.

   ![Neue E-Mail](assets/createNewEmail.png)

1. Geben Sie auf der neuen Registerkarte einen **Name** und **Beschreibung** für die E-Mail ein und wählen Sie eine Vorlage aus dem Vorlagenwähler. Klicken Sie auf **Erstellen**.

   ![Vorlagenwähler](assets/templatePicker.png)

1. Legen Sie **Von Name** und **Von Adresse** fest.

   ![Erinnerung-E-Mail](assets/reminderEmail.png)

1. Klicken Sie auf den Nachrichtentext, um den Editor zu aktivieren. Klicken Sie auf die Schaltfläche **Token einfügen**, suchen Sie das von Ihnen erstellte benutzerdefinierte Vereinbarungs-URL-Token und klicken Sie auf **Einfügen**. Schließen Sie die Anpassung Ihrer E-Mail ab und klicken Sie auf **Speichern**.

   ![Token einfügen](assets/insertToken.png)

1. Vorschau mithilfe eines Profils, dem eine Vereinbarung zugewiesen ist. Es sollte ein Link zur URL mit dem Vereinbarungsnamen als Beschriftung angezeigt werden.

   ![E-Mail-Link](assets/emailLink.png)

## Einrichten des Smart Campaign-Filters

1. Klicken Sie mit der rechten Maustaste auf das von Ihnen erstellte Programm und dann auf **Neue Smart-Kampagne**.

   ![Intelligente Kampagne 1](assets/smartCampaign1.png)

1. Geben Sie einen Namen Ihrer Wahl ein und klicken Sie auf **Erstellen**.

   ![Intelligente Kampagne 2](assets/smartCampaign2.png)

1. Suchen Sie nach und klicken Sie auf **Hat Vereinbarung** und ziehen Sie sie in die Smart-Liste.

   ![Vereinbarung](assets/hasAgreement.png)

1. Die Felder, die Sie dem Auslöser ausgeben, sollten jetzt unter **Begrenzung hinzufügen** verfügbar sein. Wählen Sie **Vereinbarungsstatus** und alle anderen Felder aus, nach denen Sie filtern möchten. Definieren Sie für jedes hinzugefügte Feld die Werte, nach denen gefiltert werden soll. In diesem Fall wird sie nur ausgelöst, wenn **Vereinbarungsstatus** zum Unterschreiben gesendet wurde und **Datum gesendet** sich in der Vergangenheit vor 7 Tagen befindet.

   ![Vereinbarungsstatus](assets/agreementStatus.png)

   >[!NOTE]
   >
   > d einen eindeutigen Bezeichner für die Bedingungen, z. B. **Vereinbarungsname**, wenn diese Kampagne nur für bestimmte Vereinbarungen ausgeführt werden soll.

1. Bestätigen Sie die Kampagnenzielgruppe und sehen Sie, wer sich auf der Registerkarte &quot;Zeitplan&quot;qualifizieren wird.

   ![Qualifikatoren](assets/qualifiers.png)

## Einrichten des Smart Campaign-Flows

Da der Kampagnenfilter **Tage unsigniert** verwendet wurde, können Sie eine geplante Wiederholung für die Kampagne verwenden.

1. Klicken Sie in der Smart-Kampagne auf die Registerkarte **Flow**. Suchen Sie den Textfluss **E-Mail senden** und ziehen Sie ihn auf die Arbeitsfläche. Wählen Sie dann die E-Mail-Erinnerung aus, die Sie im vorherigen Abschnitt erstellt haben.

   ![E-Mail senden](assets/sendEmail.png)

1. Klicken Sie in der Smart-Kampagne auf die Registerkarte **Plan**. Stellen Sie sicher, dass der Kampagnenfluss in den **Smart-Campaign-Einstellungen** nur einmal pro Person ausgeführt wird. Klicken Sie dann auf die Registerkarte **Zeitplanwiederholung**.

   ![Registerkarte &quot;Zeitplan&quot;](assets/scheduleTab.png)

1. Setzen Sie **Plan** auf &quot;Täglich&quot;, wählen Sie einen Starttag und eine Startzeit sowie ggf. ein Enddatum für die Kampagne.

   ![Zeitplaneinstellungen](assets/scheduleSettings.png)

>[!TIP]
>
>Dieses Tutorial ist Teil des Kurses [Verkürzung der Verkaufszyklen mit Adobe Sign für Salesforce und Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1), der kostenlos auf der Experience League verfügbar ist!
