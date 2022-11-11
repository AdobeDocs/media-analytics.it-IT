---
title: Panoramica sulla migrazione
description: Scopri come effettuare la migrazione dalle versioni 1.x alle versioni 2.x dell’SDK per contenuti multimediali.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 85%

---

# Panoramica sulla migrazione legacy per VHL 1.x a VHL 2.x {#migration-overview}

La migrazione da VHL 1.x a VHL 2.x è semplice, con la nuova versione con API semplificate per l&#39;inizializzazione, la configurazione e i delegati del lettore.i

Di seguito sono riportate le principali differenze tra 1.x e 2.x:

* **Plug-in, delegati -** Non è più necessario implementare plug-in e delegati per Analytics, VideoPlayer e Heartbeat.
* **Configurazione -** Non è più necessario creare istanze di configurazioni per i plug-in 1.x.

## Vantaggi di 2.x {#benefits-of-two-x}

* Tutti i metodi pubblici sono consolidati nella classe `MediaHeartbeat` per semplificare l’implementazione per gli sviluppatori.
* Tutte le configurazioni sono ora consolidate nella classe `MediaHeartbeatConfig`.
* Non è più necessario creare un’istanza delle configurazioni per i plug-in Analytics, VideoPlayer e Heartbeat. È sufficiente creare un’istanza della classe `MediaHeartbeat` con le istanze `MediaHeartbeatDelegate` e `MediaHeartbeatConfig`. Questa è l’unica implementazione necessaria per inizializzare Media Analytics.

   Con l’inizializzazione di `MediaHeartbeat`, puoi eliminare in tutta sicurezza l’implementazione di Analytics Plugin, VideoPlayer Plugin e Heartbeat Plugin. Inoltre, rimuovi tutta l’implementazione esistente per l’inizializzazione che richiede un array di plug-in come input. Puoi vedere confronti affiancati delle implementazioni 1.x e 2.x qui: [Confronto dei codici: da 1.x a 2.x](./code-comparison-1x-2x.md)

Le nuove API in 2.x sono descritte in dettaglio qui: [Conversione da API 1.x a 2.x.](./1x-2x-api-change.md)
