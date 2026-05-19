---
title: Panoramica sulla migrazione
description: Scopri come effettuare la migrazione dalle versioni 1.x alle versioni 2.x dell’SDK per contenuti multimediali.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mM6vZFyx6BG5MZXrzOc5hkBM6pOdzBCLiSL3WgON9LU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 235
ht-degree: 100%

---

# Panoramica della Migrazione legacy da VHL 1.x a VHL 2.x {#migration-overview}

La migrazione da VHL 1.x a VHL 2.x è semplice, con la nuova versione con API semplificate per l’inizializzazione, la configurazione e i delegati del lettore.

Di seguito sono riportate le principali differenze tra 1.x e 2.x:

* **Plug-in, delegati -** Non è più necessario implementare plug-in e delegati per Analytics, VideoPlayer e Heartbeat.
* **Configurazione -** Non è più necessario creare istanze di configurazioni per i plug-in 1.x.

## Vantaggi di 2.x {#benefits-of-two-x}

* Tutti i metodi pubblici sono consolidati nella classe `MediaHeartbeat` per semplificare l’implementazione per gli sviluppatori.
* Tutte le configurazioni sono ora consolidate nella classe `MediaHeartbeatConfig`.
* Non è più necessario creare un’istanza delle configurazioni per i plug-in Analytics, VideoPlayer e Heartbeat. È sufficiente creare un’istanza della classe `MediaHeartbeat` con le istanze `MediaHeartbeatDelegate` e `MediaHeartbeatConfig`. Questa è l’unica implementazione necessaria per inizializzare Media Analytics.

  Con l’inizializzazione di `MediaHeartbeat`, puoi eliminare in tutta sicurezza l’implementazione di Analytics Plugin, VideoPlayer Plugin e Heartbeat Plugin. Inoltre, rimuovi tutta l’implementazione esistente per l’inizializzazione che richiede un array di plug-in come input. Puoi vedere confronti affiancati delle implementazioni 1.x e 2.x qui: [Confronto dei codici: da 1.x a 2.x](./code-comparison-1x-2x.md)

Le nuove API in 2.x sono descritte in dettaglio qui: [Conversione da API 1.x a 2.x.](./1x-2x-api-change.md)
