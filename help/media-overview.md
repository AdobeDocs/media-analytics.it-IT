---
title: Misurazione del supporto Steaming in  Adobe Analytics
description: Adobe Analytics for Media (altrimenti denominato Media Analytics) fornisce ai clienti una misurazione affidabile dei file multimediali per contenuto, audio e annunci pubblicitari.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: fdec4da99a43d889690638f1ff3579e145548b69
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 85%

---


# Misurazione del supporto Steaming in  Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

## Informazioni su  Adobe Analytics per lo streaming di file multimediali

 Adobe Analytics per Streaming Media è un componente aggiuntivo per  Adobe Analytics che offre potenti strumenti di misura per audio, video e annunci pubblicitari. Adobe Analytics fa parte di Adobe Experience Platform.

 Adobe Analytics per Streaming Media consente di monitorare l’intero percorso del cliente attraverso il sito. Le metriche si integrano facilmente nei rapporti di Adobe Analytics e in altri prodotti Adobe Experience Cloud. La misurazione dei file multimediali consente di classificare i dati in più dimensioni e segmenti e di acquisire così tutti i metadati necessari per svolgere un’analisi completa e dettagliata. Puoi quindi analizzare i dati e attribuire criteri di successo ai file multimediali utilizzati interamente, al tempo trascorso in media e agli annunci completati.

Puoi misurare le metriche di distribuzione vitali correlate alla QoS, come fotogrammi saltati, tempo impiegato nel buffering e bitrate medio. Inoltre, le metriche possono essere combinate con i dati del tuo sito web o app per visualizzare il percorso e gli interessi del cliente. In questo modo è possibile ottenere raccomandazioni migliori e personalizzare l’esperienza del cliente con Adobe Experience Cloud.

## Funzioni {#features}

 i vantaggi offerti da Adobe Analytics per lo streaming di contenuti multimediali comprendono monitoraggio in tempo reale, analisi dettagliate, approfondimenti fruibili e opportunità di monetizzazione.
* **Analisi in tempo reale**: prendi decisioni attuabili in tempo reale utilizzando metriche delle prestazioni chiave quali durata, ex2 ed ex3 su più canali. Gli eventi di contenuto principale vengono misurati a intervalli di 10 secondi per acquisire tutte le attività mentre si verificano. Gli eventi di tracciamento degli annunci si verificano a intervalli di 1 secondo.
* **Aumento dell’engagement**: coinvolgi maggiormente gli utenti con meno eventi di buffering e capendo dove e quando far riprodurre gli annunci all’interno dei contenuti per offrire un’esperienza fluida, meno invasiva e in grado di favorire visite ripetute.
* **Immagine olistica**: combina più punti dati tra tutti i distributori di contenuti per ottenere una visione completa di tutte le attività multimediali. Misura l’engagement e le visualizzazioni/gli ascolti tra tutti i canali possibili con la funzione Federated Analytics.
* **Maggiore granularità**: valuta il comportamento di visualizzazione a livello granulare, inclusa l’ora del giorno del singolo visitatore, visualizzatori/ascoltatori simultanei per minuto e per quanto tempo in media vengono visualizzati i contenuti.
* **Misurazione precisa**: misura sui diversi dispositivi utilizzati per il consumo di contenuti multimediali, tra cui OTT, smartphone, tablet, desktop e altro per monitorare i pattern e le abitudini di engagement degli utenti.
* **Segmentazione**: applica delle classificazioni ai tuoi lettori, dispositivi, generi, capitoli e presentazioni per vedere in che modo ciascuno di essi influisce sulle visualizzazioni/sugli ascolti complessivi e sul coinvolgimento dei clienti con contenuti, audio, annunci pubblicitari e combinazioni di questi.

## Misurazione con Heartbeat {#heartbeat}

Adobe Analytics utilizza gli “heartbeat” per raccogliere le metriche video. Durante la riproduzione del video gli heartbeat vengono inviati al server che li traccia per misurare il tempo di riproduzione. Le chiamate heartbeat vengono inviate ogni dieci secondi. Gli heartbeat generano metriche granulari di coinvolgimento video e rapporti di fallout video più precisi.  Adobe Analytics per Streaming Media misura i heartbeat mediante  lancio del Adobe con estensione Media Analytics, Media SDK e Media Collection API. I componenti `AppMeasurement` e `VisitorID` vengono utilizzati per ricevere i dati video.

Utilizzando heartbeat  Adobe Analytics per Streaming Media potete ottenere i seguenti vantaggi:

| Funzione | Descrizione |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Eventi multimediali | Eventi dettagliati e personalizzati vengono inviati ogni 10 secondi per il contenuto principale e a intervalli di 1 secondo per gli annunci |
| Metriche e dimensioni | Metriche, dimensioni e benchmark standardizzate e chiare per fornitori diversi<br>Con una soluzione standardizzata su tutte le piattaforme puoi utilizzare variabili coerenti e standardizzate su tutti i contenuti multimediali e le piattaforme per consentire un confronto più efficiente tra campagne, dispositivi e fornitori. |
| Integrazioni | Experience Cloud ID è collegato ad Adobe Experience Cloud per effettuare analisi incrociate più facilmente<br>Grazie all’integrazione automatica di Adobe Experience Cloud puoi segmentare il pubblico dei file multimediali, targetizzarlo e formulare raccomandazioni per il contenuto multimediale in base alle preferenze degli utenti. |
| Prezzi | Tracciamento trasparente per flusso multimediale (singolo) |
| Implementazione e supporto | Configurazione semplificata con continui aggiornamenti e miglioramenti<br>Un processo di implementazione semplificato ti consente di mappare rapidamente le variabili tramite l’API del lettore e convalidare le implementazioni tramite lo strumento Adobe Debug per garantire che tutte le variabili necessarie siano tracciate con precisione. |
| Condivisione partner | Federated Analytics e metriche certificate<br>Con i dati condivisi tramite Federated Analytics puoi sfruttare le nostre funzionalità avanzate di condivisione dei contenuti multimediali per valutare i dati in modo olistico tra tutti i partner di distribuzione di contenuti multimediali: operatori, programmatori e distributori. |
| Tracciamento avanzato | Tracciamento dei contenuti scaricati, tracciamento del recupero errori e visualizzatori simultanei<br>Potete tenere traccia dei contenuti multimediali in streaming scaricati e riprodotti su un dispositivo, indipendentemente dalla connettività. |



## Sicurezza {#security}

Noi di Adobe abbiamo a cuore la sicurezza delle tue risorse digitali. Dalla nostra rigorosa integrazione della sicurezza nel processo e negli strumenti di sviluppo del software interno ai nostri team interfunzionali di risposta agli incidenti, puntiamo sempre ad essere proattivi e agili. Inoltre, la nostra collaborazione con partner, ricercatori e altre organizzazioni del settore ci aiuta a comprendere le ultime minacce e le best practice in materia di sicurezza, oltre a rafforzare costantemente la sicurezza dei prodotti e dei servizi che offriamo.


### Transport Layer Security {#transport-layer-security}

**Avviso TLS:** Adobe ha standard di conformità per la sicurezza che richiedono la fine del ciclo di vita dei vecchi protocolli di sicurezza. Per continuare a soddisfare gli standard in continua evoluzione relativi ai protocolli di sicurezza, Adobe sta optando per l’uso di TLS 1.2, al fine di disporre della versione più aggiornata e sicura in uso. Dal 20 febbraio 2019, Adobe supporterà solo TLS 1.1 o versioni successive. Con questa modifica, Adobe non raccoglierà più dati dagli utenti finali con dispositivi o browser Web meno recenti che utilizzano TLS 1.0. La migrazione a TLS 1.2 offre una maggiore sicurezza. È importante che esamini a fondo le specifiche e pianifichi le modifiche per una transizione senza problemi.

>[!NOTE]
>
>TLS è attualmente tra i protocolli di sicurezza distribuiti più ampiamente ed è utilizzato nei browser web e altre applicazioni dove i dati devono essere scambiati in modo sicuro all’interno di una rete.
