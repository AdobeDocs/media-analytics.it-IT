---
title: Panoramica sulla migrazione
description: Questo argomento fornisce una panoramica sulla migrazione dalle versioni 1.x a 2.x dell’SDK per file multimediali.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

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

   Con l'inizializzazione di `MediaHeartbeat`, puoi eliminare tutta l'implementazione per i plug-in Analytics, VideoPlayer Plugin e Heartbeat Plugin. Inoltre, rimuovete tutta l'implementazione esistente per l'inizializzazione che richiede un array di plug-in come input. Di seguito sono riportati confronti affiancati delle implementazioni 1.x e 2.x: Confronto [codice: da 1,x a 2,x](./code-comparison-1x-2x.md)

Le nuove API in 2.x sono descritte in dettaglio qui: [Conversione da API 1.x a 2.x.](./1x-2x-api-change.md)
