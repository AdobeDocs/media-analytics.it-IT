---
title: Panoramica di Adobe Analytics per contenuti multimediali in streaming
description: Utilizza Streaming Media Analytics per ottenere informazioni approfondite su contenuti, audio e annunci pubblicitari.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 16%

---

# Panoramica di Adobe Analytics per contenuti in streaming

![Banner](./assets/media_analytics_banner.png)

Adobe Analytics for Streaming Media è un componente aggiuntivo di Adobe Analytics che fornisce potenti strumenti di misurazione per audio, video e annunci pubblicitari. Con Analytics per contenuti in streaming, puoi ottenere dettagli granulari sulla durata, gli arresti e gli avvii in tempo reale, che consentono di valutare e combinare metriche video e audio. Queste informazioni consentono di comprendere le abitudini di visualizzazione e ascolto dei clienti e di aumentare il coinvolgimento con consigli altamente personalizzati.

Adobe Analytics per contenuti in streaming consente di tenere traccia dell’intero percorso dei clienti all’interno del sito e nelle app in streaming. È possibile combinare le metriche di Streaming Media con altre funzionalità di Adobe Analytics, ad Audience Analytics, Mobile o Cross-Device Analytics. Le metriche si integrano facilmente in Adobe Analytics Reports e altri prodotti Adobe Experience Platform. La misurazione dei file multimediali consente di classificare i dati in più dimensioni e segmenti e di acquisire così tutti i metadati necessari per svolgere un’analisi completa e dettagliata. Puoi quindi analizzare i dati e attribuire criteri di successo ai file multimediali utilizzati interamente, al tempo trascorso in media e agli annunci completati.

Puoi misurare le metriche di distribuzione vitali correlate alla qualità dell’esperienza (QoE), ad esempio fotogrammi saltati, tempo impiegato nel buffering e bitrate medio. Inoltre, le metriche possono essere combinate con i dati del sito web o dell’app per visualizzare il percorso e gli interessi del cliente, per fornire raccomandazioni migliorate e personalizzare l’esperienza del cliente tramite Adobe Experience Platform.

## Come funziona

I dati di tracciamento dei contenuti multimediali in streaming vengono raccolti da un lettore utilizzando gli SDK per contenuti multimediali, le API Media Collection o le estensioni multimediali (con tag). Tutti i dati granulari (fino a 10 secondi) vengono inviati al Media Analytics Service che raccoglie ed elabora i dati per ogni singola sessione di riproduzione. Al termine di una sessione di riproduzione, i dati di tracciamento calcolati vengono inviati ad Adobe Analytics per l’archiviazione e il reporting. Con le implementazioni di Adobe Customer Journey Analytics (CJA), i dati possono essere inviati a CJA utilizzando il Connettore dati di Analytics (ADC), in modo che i clienti possano utilizzare CJA come strumento di reporting.

<!-- ![streaming media process](./assets/streaming-process1.png) -->

<div style="text-align: center;">
<img src="./assets/streaming-process1.png" alt="Processo multimediale in streaming" width="75%">
</div>

## Funzioni

I vantaggi di Adobe Analytics for Streaming Media comprendono monitoraggio in tempo reale, analisi dettagliate, approfondimenti fruibili e opportunità di monetizzazione.

* **Analisi in tempo reale**: Prendi decisioni attuabili in tempo reale utilizzando metriche delle prestazioni chiave come gli avvii dei contenuti multimediali su più canali.

* **Aumento del coinvolgimento**: Coinvolgi completamente gli utenti con meno eventi di buffering e capendo dove e quando gli annunci dovrebbero essere riprodotti all’interno dei contenuti per fornire un’esperienza fluida e meno invasiva che fornisca visite ripetute.

* **Immagine olistica**: Combina più punti dati tra tutti i distributori di contenuti per ottenere una visione completa di tutte le attività multimediali. Misura il coinvolgimento e le visualizzazioni/gli ascolti tra tutti i canali possibili attraverso la funzione Federated Analytics.

* **Maggiore granularità**: Valutare il comportamento di visualizzazione a livello granulare, inclusa l’ora del giorno del singolo visitatore, visualizzatori simultanei o ascoltatori per minuto, e la durata media del consumo del contenuto.

* **Misurazione precisa**: Misura tra i diversi dispositivi utilizzati per il consumo di contenuti multimediali, inclusi OTT, smartphone, tablet, desktop e altro, per monitorare i pattern e le abitudini di coinvolgimento degli utenti.

* **Segmentazione**: Applica le classificazioni ai tuoi lettori, dispositivi, generi, capitoli e presentazioni per vedere in che modo ciascuno di essi ha un impatto sulle visualizzazioni/sugli ascolti complessivi e sul coinvolgimento dei clienti con contenuti, audio, annunci pubblicitari e combinazioni di questi.
