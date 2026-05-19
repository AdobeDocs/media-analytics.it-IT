---
title: 'Prova 2: interruzione contenuto multimediale'
description: Scopri la prova di interruzione dei contenuti multimediali utilizzata nella convalida.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/gVEDMjM05nDnzCB6l-9CjyUzoArcmyN4jgsjmjllRiY
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 248
ht-degree: 100%

---

# Prova 2: interruzione del contenuto multimediale{#test-media-interruption}

Questo caso di test convalida il comportamento di interruzione mobile.

## Procedura del test

È necessario completare e registrare queste attività nel seguente ordine:

1. **Avvio del lettore multimediale**

   All’avvio del lettore multimediale, le seguenti chiamate vengono inviate nell’ordine che segue:

   1. Avvio di Adobe Analytics (AppMeasurement)
   1. Avvio di Media Analytics (heartbeat)
   1. Richiesta chiamata Avvio di Adobe Analytics di Media Analytics (heartbeat)

   Le prime due chiamate contengono metadati e variabili aggiuntive. Per i parametri e i metadati delle chiamate, consulta [Dettagli delle chiamate di prova.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   La terza chiamata comunica al server di Media Analytics che Media SDK ha richiesto che la chiamata Start di Adobe Analytics (`pev2=ms_s`) sia inviata al server di Adobe Analytics.

1. **Riproduzione del contenuto principale senza interruzioni per almeno 5 minuti**

   **Riproduzione dei contenuti**

   Durante la riproduzione del contenuto, Media SDK invia chiamate di riproduzione (heartbeat) al server di Media Analytics ogni dieci secondi.

   Per i parametri e i metadati della chiamata, consulta [Dettagli della chiamata di prova.](/help/legacy/validation/test-call-details.md#play-main-content)

   Per maggiori informazioni sulle chiamate dell’annuncio, consulta anche le istruzioni per il [Tracciamento annunci](/help/use-cases/track-ads/track-ads-overview.md) della tua piattaforma.

1. **Spostamento in background dell’app o del browser**

   Quando l’app viene eseguita in background, solo le chiamate `main:pause` devono essere inviate al server di Media Analytics, partendo dalla versione 1.6.6 di VHL e successive.

1. **Porta in primo piano l’app o il browser**

   Tornando dall’esecuzione in background, la riproduzione del contenuto dovrebbe riprendere.

1. **Riproduzione dei contenuti multimediali principali senza interruzioni per almeno 5 minuti**

   Per i parametri e i metadati della chiamata, consulta [Dettagli della chiamata di prova.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Chiudere il lettore multimediale**

   Dopo la chiusura del lettore multimediale, non deve essere attivata alcuna chiamata di tracciamento aggiuntiva.
