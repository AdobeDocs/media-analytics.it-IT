---
seo-title: Panoramica sulla migrazione
title: Panoramica sulla migrazione
uuid: d 84 f 55 bc-fa 90-45 c 1-b 97 d-cb 5 fe 58 e 80 c 0
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Migration overview{#migration-overview}

La migrazione da VHL 1. x a VHL 2. x è diretta, con la nuova versione che presenta API semplificate per inizializzazione, configurazione e delegati di giocatori.

Di seguito sono riportate le differenze principali tra 1. x e 2. x:

* **Plug-in, Delegati -** Non è più necessario implementare plug-in e delegati per Analytics, videoplayer e Heartbeat.
* **Configurazione:** non è più necessario creare configurazioni per i plug-in 1. x.

## Benefits of 2.x {#benefits-of-two-x}

* All of the public methods are consolidated into the `MediaHeartbeat` class to make implementation easier on developers.
* All configs are now consolidated into the `MediaHeartbeatConfig` class.
* Non è più necessario creare le configs per i plug-in Analytics, videoplayer e Heartbeat. You only need to instantiate the `MediaHeartbeat` class with `MediaHeartbeatDelegate` and `MediaHeartbeatConfig` instances. Questa è l'unica implementazione necessaria per inizializzare Media Analytics.

   With the initialization of `MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin, and Heartbeat Plugin. Rimuovete inoltre tutta l'implementazione esistente per l'inizializzazione che utilizza un array di plug-in come input. You can see side-by-side comparisons of the 1.x and 2.x implementations here: [Code comparison: 1.x to 2.x.](./code-comparison-1x-2x.md)

Le nuove API in 2.x sono descritte in dettaglio qui: [Conversione da API 1.x a 2.x.](./1x-2x-api-change.md)
