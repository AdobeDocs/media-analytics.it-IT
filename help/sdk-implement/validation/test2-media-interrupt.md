---
title: Test 2 Interruzione del supporto
description: Scopri il test di interruzione dei file multimediali utilizzato nella convalida.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Prova 2: Interruzione del supporto{#test-media-interruption}

Questo caso di test convalida il comportamento di interruzione mobile.

## Procedura di prova

È necessario completare e registrare queste attività nel seguente ordine:

1. **Avvia il lettore multimediale**

   All&#39;avvio del lettore multimediale, le seguenti chiamate vengono inviate nell&#39;ordine seguente:

   1. Avvio di Adobe Analytics (AppMeasurement)
   1. Avvio di Media Analytics (heartbeat)
   1. Media Analytics (heartbeat) Richiesta di avvio Adobe Analytics

   Le prime due chiamate di cui sopra contengono metadati e variabili aggiuntive. Per i parametri e i metadati della chiamata, consulta [Testare i dettagli della chiamata.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   La terza chiamata di cui sopra comunica al server Media Analytics che Media SDK ha richiesto l’invio al server Adobe Analytics della chiamata di avvio di Adobe Analytics (`pev2=ms_s`).

1. **Riprodurre il contenuto principale per almeno 5 minuti ininterrotti**

   **Riproduzione dei contenuti**

   Durante la riproduzione del contenuto, Media SDK invia chiamate di riproduzione (heartbeat) al server Media Analytics ogni dieci secondi.

   Per i parametri e i metadati della chiamata, consulta [Testare i dettagli della chiamata.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Consulta anche le istruzioni [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) della tua piattaforma per ulteriori informazioni su queste chiamate Ad.

1. **Sposta in background l’app o il browser**

   Mentre l’app viene eseguita in background, solo le chiamate `main:pause` devono essere inviate al server Media Analytics, a partire dalla versione 1.6.6 di VHL e successive.

1. **Porta in primo piano app o browser**

   Al ritorno dallo sfondo, la riproduzione del contenuto dovrebbe riprendere.

1. **Riprodurre contenuti multimediali principali per almeno 5 minuti senza interruzioni**

   Per i parametri e i metadati della chiamata, vedi [Dettagli della chiamata di prova.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Chiudi lettore multimediale**

   Dopo la chiusura del lettore multimediale, non deve essere attivata alcuna chiamata di tracciamento aggiuntiva.
