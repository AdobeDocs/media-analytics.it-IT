---
title: Test 2 Interruzione del supporto
description: Questo argomento descrive il test di interruzione del supporto utilizzato per la convalida.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: cebf5697e3746721d29bfaa5356d5a2748fea435

---


# Test 2: Media interruption{#test-media-interruption}

Questo test case convalida il comportamento di interruzione mobile.

## Procedura di prova

È necessario completare e registrare tali attività nel seguente ordine:

1. **Avviare il lettore multimediale**

   All&#39;avvio del lettore multimediale, le seguenti chiamate vengono inviate nell&#39;ordine seguente:

   1. Avvio di Adobe Analytics (AppMeasurement)
   1. Avvio di Media Analytics (heartbeat)
   1. Media Analytics (heartbeat): richiesta di avvio di Adobe Analytics
   Le prime due chiamate di cui sopra contengono metadati e variabili aggiuntive. Per i parametri delle chiamate e i metadati, consultate [Test dei dettagli delle chiamate.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   La terza chiamata precedente indica al server Media Analytics che Media SDK ha richiesto l&#39;invio della chiamata di avvio di Adobe Analytics (`pev2=ms_s`) al server Adobe Analytics.

1. **Riproduci il contenuto principale per almeno 5 minuti senza interruzioni**

   **Riproduzione contenuto**

   Durante la riproduzione del contenuto, Media SDK invia chiamate di riproduzione (heartbeat) al server Media Analytics ogni dieci secondi.

   Per i parametri delle chiamate e i metadati, consultate [Test dei dettagli delle chiamate.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Vedi anche le istruzioni [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) della tua piattaforma per ulteriori informazioni su queste chiamate Ad.

1. **Spostare l&#39;app o il browser in background**

   Mentre l&#39;app viene eseguita in background, solo `main:pause` le chiamate devono essere inviate al server Media Analytics, a partire dalla versione 1.6.6 e successive di VHL.

1. **Porta in primo piano app o browser**

   Al ritorno dallo sfondo, la riproduzione del contenuto dovrebbe riprendere.

1. **Riproduci contenuti multimediali principali per almeno 5 minuti ininterrotti**

   Per i parametri e i metadati delle chiamate, vedi Dettagli chiamata di [prova.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Chiudi lettore multimediale**

   Dopo la chiusura del lettore multimediale, non devono essere attivate chiamate di tracciamento aggiuntive.
