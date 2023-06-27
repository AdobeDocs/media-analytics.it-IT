---
title: Panoramica di Adobe Analytics for Streaming Media
description: Utilizza Streaming Media Analytics per ottenere informazioni approfondite su contenuti, audio e annunci pubblicitari.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 355b3b079d53ae8e83822f61fc79e60e47f6d715
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 72%

---

# Panoramica di Adobe Analytics for Streaming Media

![Banner](./assets/media_analytics_banner.png)

Adobe Analytics for Streaming Media è un componente aggiuntivo di Adobe Analytics che fornisce potenti strumenti di misurazione per audio, video e annunci pubblicitari. Con Analytics per contenuti in streaming, puoi ottenere dettagli granulari sulla durata, le interruzioni e gli avvii in tempo reale che ti consentono di valutare e combinare metriche video e audio. Queste informazioni consentono di comprendere le abitudini di visualizzazione e ascolto dei clienti e di aumentare il coinvolgimento con consigli altamente personalizzati.

Adobe Analytics for Streaming Media consente di monitorare l’intero percorso del cliente all’interno del sito e delle app di streaming. È possibile combinare le metriche di Streaming Media con altre funzionalità di Adobe Analytics, come Audience Analytics, Mobile o Cross-Device Analytics. Le metriche si integrano facilmente nei rapporti di Adobe Analytics e in altri prodotti Adobe Experience Platform. La misurazione dei file multimediali consente di classificare i dati in più dimensioni e segmenti e di acquisire così tutti i metadati necessari per svolgere un’analisi completa e dettagliata. Puoi quindi analizzare i dati e attribuire criteri di successo ai file multimediali utilizzati interamente, al tempo trascorso in media e agli annunci completati.

Puoi misurare le metriche di consegna vitali correlate alla QoS (Qualità dell’esperienza), come fotogrammi saltati, tempo impiegato nel buffering e bitrate medio. Inoltre, le metriche possono essere combinate con i dati del tuo sito web o app per visualizzare il percorso e gli interessi del cliente. In questo modo è possibile ottenere consigli migliori e personalizzare l’esperienza del cliente con Adobe Experience Platform.

## Come funziona

I dati di tracciamento dei contenuti multimediali in streaming vengono raccolti da un lettore utilizzando Media for Edge Network SDK/Extension, Media Extension con tag, Media SDK, Media Edge API o Media Collection API.

Tutti i dati granulari (fino a 10 secondi) vengono inviati al servizio Media Analytics o a Experience Edge (a seconda della [metodo di implementazione](/help/implementation/overview.md) scegliere), che raccoglie ed elabora i dati per ogni singola sessione di riproduzione.

Al termine di una sessione di riproduzione, i dati di tracciamento calcolati vengono inviati ad Adobe Analytics o al Customer Journey Analytics per l’archiviazione e il reporting.

>[!NOTE]
>
>Con le implementazioni di Customer Journey Analytics, i dati possono essere inviati al Customer Journey Analytics utilizzando Experience Edge o Analytics Data Connector (ADC).


Consulta [Implementazione di contenuti multimediali in streaming per Adobe Analytics o Customer Journey Analytics](/help/implementation/overview.md) per ulteriori informazioni.

## Funzioni

I vantaggi di Adobe Analytics for Streaming Media comprendono monitoraggio in tempo reale, analisi dettagliate, approfondimenti fruibili e opportunità di monetizzazione.

* **Analisi in tempo reale**: prendi decisioni attuabili in tempo reale utilizzando metriche delle prestazioni chiave, quale l’avvio del file multimediale, su più canali.

* **Aumento del coinvolgimento**: coinvolgi maggiormente gli utenti con meno eventi di buffering e capendo dove e quando gli annunci dovrebbero essere riprodotti all’interno dei contenuti per offrire un’esperienza fluida, meno invasiva e in grado di favorire visite ripetute.

* **Immagine olistica**: combina più punti dati tra tutti i distributori di contenuti per ottenere una visione completa di tutte le attività multimediali. Misura il coinvolgimento e le visualizzazioni/gli ascolti tra tutti i canali possibili con la funzione Federated Analytics.

* **Maggiore granularità**: valuta il comportamento di visualizzazione a livello più granulare, inclusa l’ora del giorno del singolo visitatore, visualizzatori/ascoltatori simultanei per minuto e per quanto tempo in media vengono visualizzati i contenuti.

* **Misurazione precisa**: misura sui diversi dispositivi utilizzati per il consumo di contenuti multimediali, tra cui OTT, smartphone, tablet, desktop e altro per monitorare i pattern e le abitudini di coinvolgimento degli utenti.

* **Segmentazione**: applica delle classificazioni ai tuoi lettori, dispositivi, generi, capitoli e presentazioni per vedere in che modo ciascuno di essi influisce sulle visualizzazioni/sugli ascolti complessivi e sul coinvolgimento dei clienti con contenuti, audio, annunci pubblicitari e combinazioni di questi.
