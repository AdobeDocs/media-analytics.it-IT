---
title: Percorso file multimediale
description: Acquisisce l’ID contenuto come variabile di traffico per l’analisi del percorso.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 6%
---

# Percorso file multimediale

La dimensione **Percorso file multimediale** acquisisce l&#39;ID contenuto come variabile di traffico (prop) in modo che possa essere utilizzata nell&#39;analisi dei percorsi (ad esempio, nei rapporti di flusso contenuto successivo e precedente). È univoco per Adobe Analytics: Customer Journey Analytics non memorizza le variabili di traffico e il percorso viene eseguito direttamente sulla dimensione Contenuto (ID).

## Compilazione di questa dimensione

Il percorso multimediale viene derivato automaticamente dall’ID contenuto impostato all’inizio della sessione. Nessuna variabile separata da impostare. La colonna del feed dati `videopath` viene popolata ogni volta che si popola il contenuto (ID).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati di contesto `a.media.name` come variabile di traffico (prop) quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | N/D: utilizzare [Contenuto](content.md) per l&#39;analisi dei percorsi. |
| Feed di dati | `videopath`, `post_videopath` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!NOTE]
>
>Le proprietà Adobe Analytics hanno un limite di 100 byte. I valori superiori a 100 byte vengono troncati.

>[!IMPORTANT]
>
>I rapporti sui percorsi confrontano il valore prop tra gli hit all’interno della stessa visita. Se il contenuto (ID) cambia all’interno di una visita (ad esempio, quando un visualizzatore si sposta da un contenuto all’altro), il rapporto del percorso mostra tale flusso.

## Elementi dimensionali

Ogni elemento è un ID di contenuto segnalato durante una visita. Puoi utilizzare i pannelli Flusso per visualizzare i percorsi di navigazione tra contenuti.
