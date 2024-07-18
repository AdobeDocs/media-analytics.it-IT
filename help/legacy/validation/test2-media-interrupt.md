---
title: 'Prova 2: interruzione contenuto multimediale'
description: Scopri la prova di interruzione dei contenuti multimediali utilizzata nella convalida.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '249'
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

   La terza chiamata sopra comunica al server Media Analytics che Media SDK ha richiesto che la chiamata di Avvio di Adobe Analytics (`pev2=ms_s`) sia inviata al server Adobe Analytics.

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
