---
title: Sammeln von Dokumenten mit hohem Volumen mit GigaSign
description: Mit Gigasign könnt ihr Dokumente zur Unterzeichnung an mehrere Tausend Personen gleichzeitig senden, erfassen und nachverfolgen
role: User, Admin
product: adobe sign
level: Intermediate
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
source-git-commit: e02b1250de94ec781e7984c6c146dbae993f5d31
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Sammeln von Dokumenten mit großen Volumen mit GigaSign

Mit Gigasign könnt ihr Dokumente zur Unterzeichnung an mehrere Tausend Personen gleichzeitig senden, erfassen und nachverfolgen. Es wurde für die großvolumige Kommunikation mit Ihren Mitarbeitern und Kunden entwickelt und unterstützt bis zu 2.500 Empfänger bei jedem Massenversand. GigaSign verwendet die Acrobat Sign-API, um die gleiche Funktionalität wie MegaSign zu bieten, und bietet Unterstützung für mehrere Unterzeichner, Empfängergruppen, Empfängerrollen, Vereinbarungsnamen, Carbon Copy und mehr.

>[!VIDEO](https://video.tv.adobe.com/v/328113?hidetitle=true)

## GigaSign-App herunterladen und installieren

[GigaSign-ZIP-Datei herunterladen](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:8975dbca-98d5-4e66-9164-d21163c91c7f)

[Download-Link für Java 1.8 (nur bei Bedarf)](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target=&quot;_blank&quot;}

[IP-Adressen in weiße Liste (nur bei Bedarf)](https://helpx.adobe.com/de/sign/system-requirements.html#IPs){target=&quot;_blank&quot;}

## Grundlegende Setup-Anweisungen

1. Melden Sie sich bei Ihrem Acrobat Sign-Konto an.

1. Klicken **[!UICONTROL Gruppe]** oder **[!UICONTROL Konto]**, je nachdem, was Sie oben sehen.

1. Gib im Suchfeld links &quot;Access tokens&quot; ein.

1. Tippe rechts auf das Pluszeichen.

1. Erstellen Sie einen Schlüssel mit den erforderlichen Geltungsbereichen (User_Read, Agreement_Read, Agreement_Write, Agreement_Send, Library_Read).

1. Doppelklicken Sie auf den von Ihnen erstellten Schlüssel und kopieren Sie den VOLLSTÄNDIGEN Text (er verschwindet nach rechts vom Bildschirm, stellen Sie also sicher, dass Sie alles erhalten).

1. Öffnen Sie GigaSign.

1. Klicken Sie auf **[!UICONTROL Einstellungen]** oben rechts.

1. Fügen Sie den Integrationsschlüssel in die erste Zeile ein.

1. Geben Sie die E-Mail-Adresse des Kontos ein, mit dem dieser Schlüssel in der zweiten Zeile erstellt wurde.

1. Klicken **[!UICONTROL Senden]**.
