---
title: Panoramica di Adobe Analytics for Streaming Media
description: Utilizza Streaming Media Analytics per ottenere informazioni approfondite su contenuti, audio e annunci pubblicitari.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b12e6547ef32bfad7e8d6787a26d6467bcfeb23c
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 43%

---

# Panoramica di Adobe Analytics per contenuti in streaming

![Banner](./assets/media_analytics_banner.png)

Adobe Analytics per contenuti in streaming fornisce potenti strumenti di misurazione per audio, video e annunci pubblicitari. È possibile combinare le metriche di Streaming Media con altre funzionalità di Adobe Analytics, come Audience Analytics, Mobile o Cross-Device Analytics.

Streaming Media può essere acquistato come componente aggiuntivo di Adobe Analytics<!-- update this when SKUs are available for other AEP products -->Le metriche di , e Streaming Media si integrano facilmente nei seguenti prodotti Adobe Experience Platform:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Per implementare Adobe Analytics Adobe Streaming Media, contatta il tuo rappresentante commerciale o il team dell’account Adobe per assicurarti che Streaming Media faccia parte del tuo portfolio di prodotti.

## Funzioni chiave

I vantaggi di Adobe Analytics per contenuti in streaming includono monitoraggio in tempo reale, analisi dettagliate, informazioni fruibili, opportunità di monetizzazione e altro ancora.

* **Analisi in tempo reale**: prendi decisioni attuabili in tempo reale utilizzando metriche delle prestazioni chiave, quale l’avvio del file multimediale, su più canali.

  Con Analytics per contenuti in streaming, puoi ottenere dettagli granulari sulla durata, le interruzioni e gli avvii in tempo reale che ti consentono di valutare e combinare metriche video e audio. Queste informazioni consentono di comprendere le abitudini di visualizzazione e ascolto dei clienti e di aumentare il coinvolgimento con consigli altamente personalizzati.

* **Aumento del coinvolgimento**: coinvolgi maggiormente gli utenti con meno eventi di buffering e capendo dove e quando gli annunci dovrebbero essere riprodotti all’interno dei contenuti per offrire un’esperienza fluida, meno invasiva e in grado di favorire visite ripetute.

* **Immagine olistica**: combina più punti dati tra tutti i distributori di contenuti per ottenere una visione completa di tutte le attività multimediali. Misura il coinvolgimento e le visualizzazioni/gli ascolti su tutti i canali possibili.

  Adobe Analytics per contenuti in streaming consente di monitorare l’intero percorso dei clienti nel sito e nelle app di streaming, per visualizzare il percorso e gli interessi del cliente, fornire consigli avanzati e personalizzare l’esperienza del cliente.  La misurazione dei file multimediali consente di classificare i dati in più dimensioni e segmenti e di acquisire così tutti i metadati necessari per svolgere un’analisi completa e dettagliata. Puoi quindi analizzare i dati e attribuire criteri di successo ai file multimediali utilizzati interamente, al tempo trascorso in media e agli annunci completati.

* **Metriche vitali**: misura le metriche di consegna vitali correlate alla Qualità dell’esperienza (QoE) come fotogrammi saltati, tempo impiegato nel buffering e bitrate medio.

* **Maggiore granularità**: valuta il comportamento di visualizzazione a livello più granulare, inclusa l’ora del giorno del singolo visitatore, visualizzatori/ascoltatori simultanei per minuto e per quanto tempo in media vengono visualizzati i contenuti.

* **Misurazione precisa**: misura sui diversi dispositivi utilizzati per il consumo di contenuti multimediali, tra cui OTT, smartphone, tablet, desktop e altro per monitorare i pattern e le abitudini di coinvolgimento degli utenti.

* **Segmentazione**: applica delle classificazioni ai tuoi lettori, dispositivi, generi, capitoli e presentazioni per vedere in che modo ciascuno di essi influisce sulle visualizzazioni/sugli ascolti complessivi e sul coinvolgimento dei clienti con contenuti, audio, annunci pubblicitari e combinazioni di questi.


## Come funziona

I dati di tracciamento dei contenuti multimediali in streaming vengono raccolti da un lettore utilizzando Media for Edge Network SDK/Extension, Media Extension con tag, Media SDK, Media Edge API o Media Collection API.

Tutti i dati granulari (fino a 10 secondi) vengono inviati al servizio Media Analytics o a Experience Edge (a seconda della [metodo di implementazione](/help/implementation/overview.md) scegliere), che raccoglie ed elabora i dati per ogni singola sessione di riproduzione.

Al termine di una sessione di riproduzione, i dati di tracciamento calcolati vengono inviati ad Adobe Analytics o al Customer Journey Analytics per l’archiviazione e il reporting.

>[!NOTE]
>
>Con le implementazioni di Customer Journey Analytics, i dati possono essere inviati al Customer Journey Analytics utilizzando Experience Edge o Analytics Data Connector (ADC).


Per informazioni dettagliate sui vari metodi di implementazione, consulta [Implementazione di contenuti multimediali in streaming per Adobe Analytics o Customer Journey Analytics](/help/implementation/overview.md).
