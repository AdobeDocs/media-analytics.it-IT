---
seo-title: Controllo dell'ordine degli eventi
title: Controllo dell'ordine degli eventi
uuid: 007 fccc 6-be 72-4 b 79-826 d -588 c 957 ccf 15
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# Controlling the order of events{#controlling-the-order-of-events}

Poiché l'API Media Collection è parametful e il tracciamento dei video è un'operazione altamente dipendente dal tempo, un implementatore potrebbe essere preoccupato delle chiamate di tracciamento API Media Collection che arrivano al back-end out of order. The back end *does* attempt to queue up and reorder events based on the provided timestamp in the `playerTime` object. Tuttavia, esiste un limite a questa funzionalità. Al momento, il riordinamento potrebbe non riuscire se i ritardi tra le chiamate all'ordine arrivano più di un secondo. Questo "tempo di ritardo accettabile" può essere ottimizzato e/o può essere configurato in aggiornamenti futuri.
