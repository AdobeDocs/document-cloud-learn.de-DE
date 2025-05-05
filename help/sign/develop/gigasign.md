---
title: Sammeln von Dokumenten mit hohem Volumen mit GigaSign
description: Mit Gigasign könnt ihr Dokumente zur Unterzeichnung an mehrere Tausend Personen gleichzeitig senden, erfassen und nachverfolgen
feature: Workflow
role: Developer
level: Intermediate
jira: KT-6626
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
source-git-commit: ba9931920ab3bfb6ea38a92cac4a35da1d0295cd
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# Sammeln von Dokumenten mit großen Volumen mit GigaSign

Mit Gigasign könnt ihr Dokumente zur Unterzeichnung an mehrere Tausend Personen gleichzeitig senden, erfassen und nachverfolgen. Es wurde für die großvolumige Kommunikation mit Ihren Mitarbeitern und Kunden entwickelt und unterstützt bis zu 2.500 Empfänger bei jedem Massenversand. GigaSign verwendet die Acrobat Sign-API, um dieselbe Funktionalität wie MegaSign bereitzustellen, und unterstützt mehrere Unterzeichner, Empfängergruppen, Empfängerrollen, Vereinbarungsnamen, Carbon Copy und mehr.

>[!IMPORTANT]
>
>GigaSign wird nicht mehr auf die neueste Version von Java oder Acrobat Sign aktualisiert und wird nur begrenzte Unterstützung erhalten. Die Funktionen von GigaSign werden dem Produkt unter der [Massenversand](https://experienceleague.adobe.com/docs/document-cloud-learn/sign-learning-hub/admin-set-up/getting-started-admin/megasign.html?lang=de&)-Funktion hinzugefügt. Bitte verwenden Sie Massenversand für alle Anwendungsfälle, die nicht explizit die Verwendung von GigaSign erfordern.

>[!VIDEO](https://video.tv.adobe.com/v/328113?quality=12&learn=on&hidetitle=true)

## GigaSign-App herunterladen und installieren

[GigaSign-Zip-Datei herunterladen](https://acrobat.adobe.com/id/urn:aaid:sc:US:001cf62d-1cab-46c7-aa96-661ac8680206)

[Download-Link für Java 1.8 (nur bei Bedarf)](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html){target="_blank"} 

[IP-Adressen in weiße Liste (nur bei Bedarf)](https://helpx.adobe.com/de/sign/system-requirements.html#IPs){target="_blank"}

## Grundlegende Setup-Anweisungen

1. Melden Sie sich bei Ihrem Acrobat Sign-Konto an.

1. Klicken Sie auf **[!UICONTROL Gruppe]** oder **[!UICONTROL Konto]**, je nachdem, was oben angezeigt wird.

1. Gib im Suchfeld links &quot;Access tokens&quot; ein.

1. Klicken Sie rechts auf das Pluszeichen (+).

1. Erstellen Sie einen Schlüssel mit den erforderlichen Geltungsbereichen (User_Read, Agreement_Read, Agreement_Write, Agreement_Send, Library_Read).

1. Doppelklicken Sie auf den von Ihnen erstellten Schlüssel und kopieren Sie den VOLLSTÄNDIGEN Text (er verschwindet nach rechts vom Bildschirm, stellen Sie also sicher, dass Sie alles erhalten).

1. Öffnen Sie GigaSign.

1. Klicken Sie rechts oben auf das Symbol **[!UICONTROL Einstellungen]**.

1. Fügen Sie den Integrationsschlüssel in die erste Zeile ein.

1. Geben Sie die E-Mail-Adresse des Kontos ein, das zum Erstellen dieses Schlüssels in der zweiten Zeile verwendet wurde.

1. Klicken Sie auf **[!UICONTROL Senden]**.
