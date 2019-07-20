---
seo-title: Test 2 Video interruzioni
title: Test 2 Video interruzioni
uuid: eeccd 534-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Test 2: Video interruption{#test-video-interruption}

Questo caso di test è richiesto come parte del modulo di richiesta di certificazione e convalida il comportamento delle interruzioni mobili.

Download the certification request here: [Certification Request Form.](cert_req_form_nielsen.docx)

È necessario completare e registrare queste attività nel seguente ordine:

1. **Avviare il lettore video**

   All'avvio del lettore video, le seguenti chiamate vengono inviate nel seguente ordine:

   1. Inizio analisi file multimediali
   1. Avvio heartbeat
   1. Analytics Analytics start
   Le prime due chiamate sopra contengono metadati e variabili aggiuntive. For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

1. **Riproduci video principale per almeno 5 minuti senza interruzioni**

   **Riproduzione contenuto**

   Durante la riproduzione di contenuto principale normale, le chiamate Heartbeat vengono inviate al server Heartbeat ogni dieci secondi.

   For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](../../sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Spostare l'app o il browser in background**

   Mentre l'app viene eseguita in background, solo principale: le chiamate in pausa devono essere inviate al server Heartbeat, a partire dalla versione VHL 1.6.6 e successive.

1. **Porta in background app o browser**

   Tornando dallo sfondo, la riproduzione del contenuto deve riprendere.

1. **Riproduci video principale per almeno 5 minuti senza interruzioni**

   For call parameters and metadata, see [Test Call Details.](../../sdk-implement/validation/test-call-details.md)

1. **Chiudi lettore video**

   Non viene attivata alcuna chiamata di tracciamento aggiuntiva dopo la chiusura del lettore video.

