---
seo-title: Test 2 - Interruzione media
title: Test 2 - Interruzione media
uuid: eeccd 534-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# Test 2: Interruzione file multimediali{#test-media-interruption}

Questo caso di test convalida il comportamento delle interruzioni mobile. È un elemento obbligatorio della richiesta di certificazione.

## Modulo richiesta di certificazione

**Scarica il modulo della richiesta di certificazione qui: = = &gt;**  [Modulo di richiesta certificazione.](cert_req_form.docx)

## Procedura di test

È necessario completare e registrare queste attività nel seguente ordine:

1. **Avviare il lettore multimediale**

   All'avvio del lettore multimediale, le seguenti chiamate vengono inviate nel seguente ordine:

   1. Adobe Analytics (appmeasurement) Start
   1. Media Analytics (heartbeats) Start
   1. Media Analytics (heartbeats) Chiamata di avvio di Adobe Analytics richiesta
   Le prime due chiamate sopra contengono metadati e variabili aggiuntive. Per i parametri e i metadati delle chiamate, consultate [Dettagli sulle chiamate di test.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   La terza chiamata sopra indica al server Media Analytics che Media SDK ha richiesto che il call call di Adobe Analytics (`pev2=ms_s`) venga inviato al server Adobe Analytics.

1. **Riproduci contenuto principale per almeno 5 minuti senza interruzioni**

   **Riproduzione contenuto**

   Durante la riproduzione del contenuto, Media SDK invia chiamate di riproduzione (heartbeat) al server Media Analytics ogni dieci secondi.

   Per i parametri e i metadati delle chiamate, consultate [Dettagli sulle chiamate di test.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Consultate anche le istruzioni [della vostra piattaforma per monitorare gli annunci](/help/sdk-implement/track-ads/track-ads-overview.md) per informazioni aggiuntive su queste chiamate ad annuncio.

1. **Spostare l'app o il browser in background**

   Mentre l'app viene eseguita in background, `main:pause` è necessario inviare solo chiamate al server Media Analytics, a partire dalla versione VHL 1.6.6 e successive.

1. **Reindirizza l'app o il browser in primo piano**

   Tornando dallo sfondo, la riproduzione del contenuto deve riprendere.

1. **Riproduci contenuti multimediali principali per almeno 5 minuti senza interruzioni**

   Per i parametri e i metadati delle chiamate, consultate [Test Call Details (Dettagli chiamata per i test).](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Chiudi lettore multimediale**

   Non dovrebbero essere attivate chiamate di tracciamento aggiuntive dopo la chiusura del lettore multimediale.

