---
title: Percorso file multimediale
description: Acquisisce l’ID contenuto come variabile di traffico per l’analisi del percorso.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 5%

---


# Percorso file multimediale

La dimensione **Percorso file multimediale** acquisisce l&#39;ID contenuto come variabile di traffico (prop) in modo che possa essere utilizzata nell&#39;analisi dei percorsi (ad esempio, nei rapporti di flusso contenuto successivo e precedente). È univoco per Adobe Analytics: Customer Journey Analytics non memorizza le variabili di traffico e il percorso viene eseguito direttamente sulla dimensione Contenuto (ID).

## Compilazione di questa dimensione

Il percorso multimediale viene derivato automaticamente dall’ID contenuto impostato all’inizio della sessione. Nessuna variabile separata da impostare. La colonna del feed dati `videopath` viene popolata ogni volta che si popola il contenuto (ID).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati di contesto `a.media.name` come variabile di traffico (prop) quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | N/D: utilizzare [Contenuto](content.md) per l&#39;analisi dei percorsi |
| Feed di dati | `videopath`, `post_videopath` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!NOTE]
>
>Le proprietà Adobe Analytics hanno un limite di 100 byte. I valori superiori a 100 byte vengono troncati.

>[!IMPORTANT]
>
>I rapporti sui percorsi confrontano il valore prop tra gli hit all’interno della stessa visita. Se il contenuto (ID) cambia all’interno di una visita (ad esempio, quando un visualizzatore si sposta da un contenuto all’altro), il rapporto del percorso mostra tale flusso.

## Elementi dimensionali

Ogni elemento è un ID di contenuto segnalato durante una visita. Utilizza i rapporti Flusso pagina successivo e Flusso pagina precedente in Contenuto > Percorso file multimediali in Adobe Analytics per visualizzare i percorsi di navigazione da contenuto a contenuto.
