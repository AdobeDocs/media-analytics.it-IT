---
title: 'Adobe Streaming Media in Adobe Analytics '
description: '"Approfondisci la misurazione di contenuti multimediali in streaming allo stato dell’arte per contenuti, audio e annunci pubblicitari. Scopri Adobe Analytics for Streaming Media."'
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 80%

---

# Misurazione dei file multimediali in streaming in Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

## Informazioni su Adobe Analytics per i file multimediali in streaming

Adobe Analytics for Streaming Media è un componente aggiuntivo di Adobe Analytics che fornisce potenti strumenti di misurazione per audio, video e annunci pubblicitari. Adobe Analytics fa parte di Adobe Experience Platform.

Adobe Analytics for Streaming Media consente di tenere traccia dell’intero percorso dei clienti all’interno del sito. Le metriche si integrano facilmente nei rapporti di Adobe Analytics e in altri prodotti Adobe Experience Cloud. La misurazione dei file multimediali consente di classificare i dati in più dimensioni e segmenti e di acquisire così tutti i metadati necessari per svolgere un’analisi completa e dettagliata. Puoi quindi analizzare i dati e attribuire criteri di successo ai file multimediali utilizzati interamente, al tempo trascorso in media e agli annunci completati.

Puoi misurare le metriche di distribuzione vitali correlate alla QoS, come fotogrammi saltati, tempo impiegato nel buffering e bitrate medio. Inoltre, le metriche possono essere combinate con i dati del tuo sito web o app per visualizzare il percorso e gli interessi del cliente. In questo modo è possibile ottenere raccomandazioni migliori e personalizzare l’esperienza del cliente con Adobe Experience Cloud.

## Funzioni {#features}

I vantaggi di Adobe Analytics per i contenuti in streaming includono monitoraggio in tempo reale, analisi dettagliate, informazioni utili e opportunità di monetizzazione.
* **Analisi** in tempo reale: prendi decisioni attuabili in tempo reale utilizzando metriche delle prestazioni chiave come gli avvii dei contenuti multimediali su più canali.
* **Aumento dell’engagement**: coinvolgi maggiormente gli utenti con meno eventi di buffering e capendo dove e quando far riprodurre gli annunci all’interno dei contenuti per offrire un’esperienza fluida, meno invasiva e in grado di favorire visite ripetute.
* **Immagine olistica**: combina più punti dati tra tutti i distributori di contenuti per ottenere una visione completa di tutte le attività multimediali. Misura l’engagement e le visualizzazioni/gli ascolti tra tutti i canali possibili con la funzione Federated Analytics.
* **Maggiore granularità**: valuta il comportamento di visualizzazione a livello granulare, inclusa l’ora del giorno del singolo visitatore, visualizzatori/ascoltatori simultanei per minuto e per quanto tempo in media vengono visualizzati i contenuti.
* **Misurazione precisa**: misura sui diversi dispositivi utilizzati per il consumo di contenuti multimediali, tra cui OTT, smartphone, tablet, desktop e altro per monitorare i pattern e le abitudini di engagement degli utenti.
* **Segmentazione**: applica delle classificazioni ai tuoi lettori, dispositivi, generi, capitoli e presentazioni per vedere in che modo ciascuno di essi influisce sulle visualizzazioni/sugli ascolti complessivi e sul coinvolgimento dei clienti con contenuti, audio, annunci pubblicitari e combinazioni di questi.

## Misurazione con Heartbeat {#heartbeat}

Adobe Analytics utilizza gli “heartbeat” per raccogliere le metriche video. Durante la riproduzione del video gli heartbeat vengono inviati al server che li traccia per misurare il tempo di riproduzione. Le chiamate heartbeat vengono inviate ogni dieci secondi. Gli heartbeat generano metriche granulari di coinvolgimento video e rapporti di fallout video più precisi. Adobe Analytics for Streaming Media misura gli heartbeat utilizzando Adobe Launch con l’estensione Media Analytics, Media SDK e l’API Media Collection. I componenti `AppMeasurement` e `VisitorID` vengono utilizzati per ricevere i dati video.

L’utilizzo di heartbeat in Adobe Analytics per i file multimediali in streaming offre i seguenti vantaggi:

| Funzione | Descrizione |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Eventi multimediali | Eventi dettagliati e personalizzati vengono inviati ogni 10 secondi per il contenuto principale e a intervalli di 1 secondo per gli annunci |
| Metriche e dimensioni | Metriche, dimensioni e benchmark standardizzate e chiare per fornitori diversi<br>Con una soluzione standardizzata su tutte le piattaforme puoi utilizzare variabili coerenti e standardizzate su tutti i contenuti multimediali e le piattaforme per consentire un confronto più efficiente tra campagne, dispositivi e fornitori. |
| Integrazioni | Experience Cloud ID è collegato ad Adobe Experience Cloud per effettuare analisi incrociate più facilmente<br>Grazie all’integrazione automatica di Adobe Experience Cloud puoi segmentare il pubblico dei file multimediali, targetizzarlo e formulare raccomandazioni per il contenuto multimediale in base alle preferenze degli utenti. |
| Prezzi | Tracciamento trasparente per flusso multimediale (singolo) |
| Implementazione e supporto | Configurazione semplificata con continui aggiornamenti e miglioramenti<br>Un processo di implementazione semplificato ti consente di mappare rapidamente le variabili tramite l’API del lettore e convalidare le implementazioni tramite lo strumento Adobe Debug per garantire che tutte le variabili necessarie siano tracciate con precisione. |
| Condivisione partner | Federated Analytics e metriche certificate<br>Con i dati condivisi tramite Federated Analytics puoi sfruttare le nostre funzionalità avanzate di condivisione dei contenuti multimediali per valutare i dati in modo olistico tra tutti i partner di distribuzione di contenuti multimediali: operatori, programmatori e distributori. |
| Tracciamento avanzato | Tracciamento del contenuto scaricato, tracciamento del recupero degli errori e visualizzatori simultanei<br>È possibile tenere traccia del contenuto multimediale in streaming scaricato e riprodotto su un dispositivo indipendentemente dalla connettività. |



## Sicurezza {#security}

Noi di Adobe abbiamo a cuore la sicurezza delle tue risorse digitali. Dalla nostra rigorosa integrazione della sicurezza nel processo e negli strumenti di sviluppo del software interno ai nostri team interfunzionali di risposta agli incidenti, puntiamo sempre ad essere proattivi e agili. Inoltre, la nostra collaborazione con partner, ricercatori e altre organizzazioni del settore ci aiuta a comprendere le ultime minacce e le best practice in materia di sicurezza, oltre a rafforzare costantemente la sicurezza dei prodotti e dei servizi che offriamo.


### Transport Layer Security {#transport-layer-security}

**Avviso TLS:** Adobe ha standard di conformità per la sicurezza che richiedono la fine del ciclo di vita dei vecchi protocolli di sicurezza. Per continuare a soddisfare gli standard in continua evoluzione relativi ai protocolli di sicurezza, Adobe sta optando per l’uso di TLS 1.2, al fine di disporre della versione più aggiornata e sicura in uso. Dal 20 febbraio 2019, Adobe supporterà solo TLS 1.1 o versioni successive. Con questa modifica, Adobe non raccoglierà più dati dagli utenti finali con dispositivi o browser Web meno recenti che utilizzano TLS 1.0. La migrazione a TLS 1.2 offre una maggiore sicurezza. È importante che esamini a fondo le specifiche e pianifichi le modifiche per una transizione senza problemi.

>[!NOTE]
>
>TLS è attualmente tra i protocolli di sicurezza distribuiti più ampiamente ed è utilizzato nei browser web e altre applicazioni dove i dati devono essere scambiati in modo sicuro all’interno di una rete.
