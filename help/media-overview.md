---
title: Panoramica sui contenuti multimediali in streaming di Adobe
description: Utilizza le soluzioni Adobe Streaming Media per ottenere potenti insight per contenuti, audio e annunci pubblicitari.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/EJ6osO9PkXBubSF7a7HebRJhpSTamNnghofASOs7E-E
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c8add8f2-4250-4fd9-9cde-9707036c567did: df312454-73c4-43f6-a90e-18f5043f074cid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5520579-b31f-4df7-9281-f0d9f91e2edcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: e0eb8757-182f-49f3-94a4-1587d16f5094id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 606
ht-degree: 36%

---

# Panoramica di Adobe streaming media services

![Banner](./assets/media_analytics_banner.png)

I servizi multimediali di streaming di Adobe forniscono potenti strumenti di raccolta, misurazione e personalizzazione per contenuti multimediali in streaming, come audio, video e annunci pubblicitari per i provider di contenuti multimediali in streaming. Puoi combinare le metriche dei contenuti multimediali in streaming con funzionalità quali Audience Analytics, Mobile o Cross-Device Analytics.

I dati multimediali in streaming si integrano facilmente nei seguenti prodotti Adobe Experience Platform:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Per implementare i servizi di streaming media, contatta il rappresentante commerciale Adobe o il team dell’account Adobe per assicurarti che il componente aggiuntivo Customer Journey Analytics Streaming Media Collection o il componente aggiuntivo Adobe Analytics for Streaming Media facciano parte del tuo portfolio di prodotti.

## Funzioni chiave

I vantaggi dei servizi di streaming media includono monitoraggio in tempo reale, analisi dettagliate, informazioni fruibili, opportunità di monetizzazione e altro ancora.

* **Analisi in tempo reale**: prendi decisioni attuabili in tempo reale utilizzando metriche delle prestazioni chiave, quale l’avvio del file multimediale, su più canali.

  Con i servizi di streaming media, puoi ottenere dettagli granulari sulla durata, le interruzioni e gli avvii in tempo reale che ti consentono di valutare e combinare metriche video e audio. Queste informazioni consentono di comprendere le abitudini di visualizzazione e ascolto dei clienti e di aumentare il coinvolgimento con consigli altamente personalizzati.

* **Aumento del coinvolgimento**: coinvolgi maggiormente gli utenti con meno eventi di buffering e capendo dove e quando gli annunci dovrebbero essere riprodotti all’interno dei contenuti per offrire un’esperienza fluida, meno invasiva e in grado di favorire visite ripetute.

* **Immagine olistica**: combina più punti dati tra tutti i distributori di contenuti per ottenere una visione completa di tutte le attività multimediali. Misura il coinvolgimento e le visualizzazioni/gli ascolti su tutti i canali possibili.

  I servizi multimediali in streaming consentono di monitorare l’intero percorso dei clienti nel sito e nelle app di streaming per visualizzare il percorso e gli interessi dei clienti, fornire consigli avanzati e personalizzare le esperienze dei clienti.  La misurazione dei file multimediali consente di classificare i dati in più dimensioni e segmenti e di acquisire così tutti i metadati necessari per svolgere un’analisi completa e dettagliata. Puoi quindi analizzare i dati e attribuire criteri di successo ai file multimediali utilizzati interamente, al tempo trascorso in media e agli annunci completati.

* **Metriche vitali**: misura le metriche di consegna vitali correlate alla qualità dell&#39;esperienza (QoE) come fotogrammi saltati, tempo impiegato nel buffering e bitrate medio.

* **Maggiore granularità**: valuta il comportamento di visualizzazione a livello più granulare, inclusa l’ora del giorno del singolo visitatore, visualizzatori/ascoltatori simultanei per minuto e per quanto tempo in media vengono visualizzati i contenuti.

* **Misurazione precisa**: misura sui diversi dispositivi utilizzati per il consumo di contenuti multimediali, tra cui OTT, smartphone, tablet, desktop e altro per monitorare i pattern e le abitudini di coinvolgimento degli utenti.

* **Segmentazione**: applica delle classificazioni ai tuoi lettori, dispositivi, generi, capitoli e presentazioni per vedere in che modo ciascuno di essi influisce sulle visualizzazioni/sugli ascolti complessivi e sul coinvolgimento dei clienti con contenuti, audio, annunci pubblicitari e combinazioni di questi.


## Come funziona

I dati di tracciamento dei servizi multimediali in streaming vengono raccolti da un lettore utilizzando Media for Edge Network SDK/Extension, Media Extension with Tags, Media SDK, Media Edge API o Media Collection API.

Tutti i dati granulari (fino a 10 secondi) vengono inviati al servizio Media Analytics o a Experience Edge (a seconda del [metodo di implementazione](/help/implementation/overview.md) scelto), che raccolgono ed elaborano i dati per ogni singola sessione di riproduzione.

Al termine di una sessione di riproduzione, i dati di tracciamento calcolati vengono inviati ad Adobe Analytics o Customer Journey Analytics per l’archiviazione e il reporting.

>[!NOTE]
>
>Con le implementazioni di Customer Journey Analytics, i dati possono essere inviati a Customer Journey Analytics utilizzando Experience Edge o Analytics Data Connector (ADC).


Per informazioni dettagliate sui vari metodi di implementazione, vedere [Implementare servizi multimediali in streaming per Adobe Analytics o Customer Journey Analytics](/help/implementation/overview.md).
