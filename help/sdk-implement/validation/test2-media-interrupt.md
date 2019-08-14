---
seo-title: Test 2 - Interruzione media
title: Test 2 - Interruzione media
uuid: eeccd 534-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Test 2: Interruzione file multimediali{#test-media-interruption}

Questo caso di test è richiesto come parte del modulo di richiesta di certificazione e convalida il comportamento delle interruzioni mobili.

Scaricate la richiesta di certificazione qui: [Modulo richiesta di certificazione.](cert_req_form.docx)

È necessario completare e registrare queste attività nel seguente ordine:

1. **Avviare il lettore multimediale**

   All'avvio del lettore multimediale, le seguenti chiamate vengono inviate nel seguente ordine:

   1. Inizio analisi file multimediali
   1. Avvio heartbeat
   1. Analytics Analytics start
   Le prime due chiamate sopra contengono metadati e variabili aggiuntive. Per i parametri e i metadati delle chiamate, consultate [Dettagli sulle chiamate di test.](/help/sdk-implement/validation/test-call-details.md)

1. **Riproduci contenuti multimediali principali per almeno 5 minuti senza interruzioni**

   **Riproduzione contenuto**

   Durante la riproduzione di contenuto principale normale, le chiamate Heartbeat vengono inviate al server Heartbeat ogni dieci secondi.

   Per i parametri e i metadati delle chiamate, consultate [Dettagli sulle chiamate di test.](/help/sdk-implement/validation/test-call-details.md)

   Consultate anche le istruzioni [della vostra piattaforma per monitorare gli annunci](/help/sdk-implement/track-ads/track-ads-overview.md) per informazioni aggiuntive su queste chiamate ad annuncio.

1. **Spostare l'app o il browser in background**

   Mentre l'app viene eseguita in background, solo principale: le chiamate in pausa devono essere inviate al server Heartbeat, a partire dalla versione VHL 1.6.6 e successive.

1. **Porta in background app o browser**

   Tornando dallo sfondo, la riproduzione del contenuto deve riprendere.

1. **Riproduci contenuti multimediali principali per almeno 5 minuti senza interruzioni**

   Per i parametri e i metadati delle chiamate, consultate [Test Call Details (Dettagli chiamata per i test).](/help/sdk-implement/validation/test-call-details.md)

1. **Chiudi lettore multimediale**

   Non dovrebbero essere attivate chiamate di tracciamento aggiuntive dopo la chiusura del lettore multimediale.

