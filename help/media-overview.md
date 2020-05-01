---
title: Misurazione di audio e video in Adobe Analytics
description: Adobe Analytics for Media (altrimenti denominato Media Analytics) fornisce ai clienti una misurazione affidabile dei file multimediali per contenuto, audio e annunci pubblicitari.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: bddcbcd844145788518c60399bee9e4744e42d3a

---


# Misurazione di audio e video in Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

## Informazioni su Adobe Analytics per audio e video

Adobe Analytics per audio e video è un componente aggiuntivo di Adobe Analytics che fornisce potenti strumenti di misurazione per audio, video e annunci pubblicitari. Adobe Analytics fa parte di Adobe Experience Platform.

Adobe Analytics per audio e video consente di monitorare l’intero percorso del cliente attraverso il sito. Le metriche si integrano facilmente in Adobe Analytics Reports e altri prodotti Adobe Experience Cloud. La misurazione dei file multimediali consente di classificare i dati in più dimensioni e segmenti, acquisendo tutti i metadati necessari per un’analisi completa e dettagliata. Potete quindi analizzare i dati e attribuire i criteri di successo a supporti completamente utilizzati, al tempo medio trascorso e agli annunci completati.

Potete misurare le metriche di consegna vitali correlate ai QoS, come fotogrammi saltati, buffering del tempo trascorso e bitrate medio. Inoltre, le metriche possono essere combinate con i dati del tuo sito web o dell&#39;app per visualizzare il percorso e gli interessi del cliente, per fornire raccomandazioni migliorate e personalizzare le esperienze dei clienti tramite Adobe Experience Cloud.

## Funzioni {#features}

I vantaggi di Adobe Analytics per audio e video comprendono monitoraggio in tempo reale, analisi dettagliate, approfondimenti fruibili e opportunità di monetizzazione.
* **Analisi** in tempo reale - È possibile prendere decisioni in tempo reale e fruibili utilizzando metriche delle prestazioni chiave come durata, ex2 ed ex3, su più canali. Gli eventi di contenuto principale vengono misurati a intervalli di 10 secondi per acquisire tutte le attività mentre si verificano. Gli eventi di tracciamento degli annunci si verificano a intervalli di 1 secondo.
* **Stimolare il coinvolgimento**- Coinvolgere appieno gli utenti attraverso un numero inferiore di eventi buffering e comprendendo dove e quando gli annunci dovrebbero essere riprodotti all&#39;interno dei contenuti per fornire un&#39;esperienza fluida e meno intrusiva che offra visite ripetute.
* **Immagine** olistica - Combinate più punti dati tra tutti i distributori di contenuti per ottenere una visione completa di tutte le attività multimediali. Misura il coinvolgimento e visualizza/ascolta tutti i possibili canali tramite la funzione di analisi federata.
* **Maggiore granularità**- Valutate il comportamento della visualizzazione al livello più granulare, inclusi l&#39;ora del giorno per singolo visitatore, gli utenti simultanei/i listener per minuto e la durata media del consumo del contenuto.
* **Misurazione** precisa - Misurate i diversi dispositivi utilizzati per il consumo di supporti, inclusi OTT, smartphone, tablet, desktop e altro ancora, per monitorare i pattern e le abitudini di coinvolgimento degli utenti.
* **Segmentazione**- Applica classificazioni a lettori, dispositivi, generi, capitoli e presentazioni per vedere in che modo ciascuna di esse ha un impatto sulle viste/sugli ascolti complessivi e sul coinvolgimento dei clienti con contenuti, audio, annunci pubblicitari e insieme.

## Heartbeat measurement {#heartbeat}

Adobe Analytics utilizza &quot;heartbeat&quot; per raccogliere le metriche video. Durante la riproduzione del video, i heartbeat vengono inviati al server di tracciamento heartbeat per misurare il tempo di riproduzione. Le chiamate heartbeat vengono inviate ogni dieci secondi. I heartbeat generano metriche di coinvolgimento video granulari e report di abbandono video più accurati. Adobe Analytics per audio e video misura i battimenti cardiaci utilizzando Adobe Launch con estensione Media Analytics, Media SDK e Media Collection API. I `AppMeasurement` componenti e `VisitorID` i componenti vengono utilizzati per ricevere i dati video.

L&#39;utilizzo di heartbeat in Adobe Analytics per audio e video offre i seguenti vantaggi:

| Funzione | Descrizione |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Eventi multimediali | Eventi dettagliati e personalizzati vengono inviati ogni 10 secondi per il contenuto principale e ogni 1 secondo per gli annunci |
| Metriche e dimensioni | Cancella metriche, dimensioni e benchmark standardizzati tra<br>fornitoriCon una soluzione standardizzata su tutte le piattaforme, puoi utilizzare variabili coerenti e standardizzate su tutti i supporti e le piattaforme per consentire un confronto tra campagne, dispositivi e fornitori più efficiente. |
| Integrazioni | Experience Cloud ID è collegato ad Adobe Experience Cloud per<br>effettuare analisi incrociate più facilmenteGrazie all’integrazione automatica di Adobe Experience Cloud, puoi segmentare il pubblico dei media, mirarlo e formulare raccomandazioni multimediali in base alle preferenze degli utenti. |
| Prezzi | Tracciamento trasparente per flusso multimediale (singolo) |
| Implementazione e supporto | Configurazione semplificata con continui aggiornamenti e<br>miglioramentiCon un processo di implementazione semplificato, puoi mappare rapidamente le variabili tramite l’API del lettore e convalidare le implementazioni tramite Adobe Debug Tool per garantire che tutte le variabili necessarie siano tracciate con precisione. |
| Condivisione partner | Federated Analytics and Certified Metrics<br>With shared data through Federated Analytics, you can capitalize on our industry-first media sharing capabilities, to evaluate data holistically across all of your media distribution partners—operators, programmers, and distributors. |
| Tracciamento avanzato | Download del tracciamento del contenuto, tracciamento del recupero degli errori e<br>visualizzatori simultaneiPotete tenere traccia del contenuto audio e video scaricato e riprodotto su un dispositivo indipendentemente dalla sua connettività. |



## Sicurezza {#security}

In Adobe, prendiamo sul serio la sicurezza delle tue risorse digitali. Dalla nostra rigorosa integrazione della sicurezza nel nostro processo e negli strumenti di sviluppo software interni ai nostri team di risposta agli incidenti cross-functional, ci sforziamo di essere proattivi e agili. Inoltre, il nostro lavoro collaborativo con partner, ricercatori e altre organizzazioni del settore ci aiuta a comprendere le ultime minacce e le best practice in materia di sicurezza, oltre a rafforzare costantemente la sicurezza nei prodotti e nei servizi che offriamo.


### Transport Layer Security {#transport-layer-security}

**Avviso TLS:** Adobe ha standard di conformità per la sicurezza che richiedono la fine del ciclo di vita dei vecchi protocolli di sicurezza. Per continuare a soddisfare gli standard in continua evoluzione relativi ai protocolli di sicurezza, Adobe sta optando per l’uso di TLS 1.2, al fine di disporre della versione più aggiornata e sicura in uso. Dal 20 febbraio 2019, Adobe supporterà solo TLS 1.1 o versioni successive. Con questa modifica, Adobe non raccoglierà più dati dagli utenti finali con dispositivi o browser Web meno recenti che utilizzano TLS 1.0. La migrazione a TLS 1.2 offre una maggiore sicurezza. È importante che esamini a fondo le specifiche e pianifichi le modifiche per una transizione senza problemi.

>[!NOTE]
>
>TLS è attualmente tra i protocolli di sicurezza distribuiti più ampiamente ed è utilizzato nei browser web e altre applicazioni dove i dati devono essere scambiati in modo sicuro all’interno di una rete.
