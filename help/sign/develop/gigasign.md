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
TQID: https://experienceleague.adobe.com/62xUXPGJ-H5XyknrYgKSEErD-mW0zIZc-qxQJvzXgCM
product_v2:
  - id: b12c730b-5ddb-4a2d-ba42-da774988b909
  - id: c1c5fb98-9105-44ed-9df1-9e04d062a784
  - id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2:
  - id: a1028f9a-6dbc-4a4f-adf5-eb9f85a408a6
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: d92345097c162b68b9d8405122534371c87c5f1a
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 2%

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
