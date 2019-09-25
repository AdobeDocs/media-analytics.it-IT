---
seo-title: Panoramica sulla migrazione
title: Panoramica sulla migrazione
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Panoramica sulla migrazione{#migration-overview}

La migrazione da VHL 1.x a VHL 2.x è semplice, con la nuova versione con API semplificate per l'inizializzazione, la configurazione e i delegati di lettore.

Di seguito sono riportate le differenze principali tra 1.x e 2.x:

* **Plug-in, delegati -** Non è più necessario implementare plug-in e delegati per Analytics, VideoPlayer e Heartbeat.
* **Configurazione: non è più necessario creare un'istanza delle configurazioni per i plug-in 1.x.**

## Vantaggi di 2.x {#benefits-of-two-x}

* Tutti i metodi pubblici sono consolidati nella `MediaHeartbeat` classe per semplificare l'implementazione per gli sviluppatori.
* Tutte le configurazioni sono ora consolidate nella `MediaHeartbeatConfig` classe.
* Non è più necessario creare un'istanza delle configurazioni per i plug-in Analytics, VideoPlayer e Heartbeat. È sufficiente creare un'istanza della `MediaHeartbeat` classe con `MediaHeartbeatDelegate` e `MediaHeartbeatConfig` istanze. Questa è l'unica implementazione necessaria per inizializzare Media Analytics.

   Con l'inizializzazione di `MediaHeartbeat`, puoi eliminare tutta l'implementazione per i plug-in Analytics, VideoPlayer Plugin e Heartbeat Plugin. Inoltre, rimuovete tutta l'implementazione esistente per l'inizializzazione che richiede un array di plug-in come input. You can see side-by-side comparisons of the 1.x and 2.x implementations here: [Code comparison: 1.x to 2.x.](./code-comparison-1x-2x.md)

Le nuove API in 2.x sono descritte in dettaglio qui: [Conversione da API 1.x a 2.x.](./1x-2x-api-change.md)
