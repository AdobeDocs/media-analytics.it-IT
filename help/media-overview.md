---
title: Misurazione di audio e video in Adobe Analytics
description: 'Adobe Analytics for Media (altrimenti denominato Media Analytics) fornisce ai clienti una misurazione affidabile dei file multimediali per contenuto, audio e annunci pubblicitari. '
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: 689b7d4ce632d3ddba6704bb8040eec52bfc326f

---


# Misurazione di audio e video in Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>La documentazione fornita di seguito è specifica per i clienti che, per la misurazione heartbeat, utilizzano la versione 1.5 o successiva di *Media SDK* di Adobe o il più recente *API Media Collection* di Adobe. Non include istruzioni relative all’implementazione video precedente di Milestone. Invitiamo tutti i clienti ad adottare una o entrambe le più recenti soluzioni di tracciamento dei contenuti multimediali, al fine di sfruttare al meglio i miglioramenti e le misurazioni estese. Puoi visualizzare i [vantaggi della transizione alle soluzioni più recenti](media-overview.md#heartbeat-versus-milestone-benefits) di seguito. Anche se continueremo a supportare il metodo Milestone per il tracciamento dei video, non ci saranno aggiornamenti, correzioni o miglioramenti delle funzionalità pianificati. Per ulteriori domande, contatta il tuo Adobe Account Manager.

## Panoramica {#overview}

Adobe Analytics for Media (altrimenti denominato Media Analytics) è un componente aggiuntivo dell’offerta Analytics di base che fornisce ai clienti una misurazione affidabile dei file multimediali per contenuto, audio e annunci pubblicitari. Media Analytics offre molti vantaggi ai clienti grazie a monitoraggio in tempo reale, analisi dettagliate, informazioni utili e opportunità di monetizzazione.

Il tracciamento dei contenuti multimediali è abilitato tramite una delle seguenti opzioni:

* **Media SDK:** si integra con i lettori multimediali più comunemente utilizzati.
* **API Media Collection:** (RESTful API) si integra con lettori per i quali non è disponibile alcun supporto SDK (o con lettori per i quali non è richiesta alcuna integrazione SDK).

Adobe Analytics for Media consente di monitorare l’intero percorso del cliente attraverso il sito, incluso il consumo di file multimediali. Queste misure vengono facilmente integrate nei report di Analytics e in altri prodotti Experience Cloud. La misurazione dei file multimediali consente di suddividere i dati in più dimensioni e segmenti, acquisire tutti i metadati necessari per eseguire un’analisi completa e dettagliata e attribuire criteri di successo a supporti completamente utilizzati, al tempo medio trascorso e agli annunci completati.

Le soluzioni per i media non solo misurano le metriche di distribuzione vitali correlate ai QoS come fotogrammi saltati, tempo impiegato nel buffering e bitrate medio. Possono anche essere combinate con i dati del tuo sito web o dell’app per visualizzare il flusso dei clienti e i loro interessi, per poter formulare raccomandazioni e personalizzare le loro esperienze tramite Adobe Experience Cloud.

## Vantaggi {#benefits}

Tra i numerosi vantaggi offerti dalle soluzioni di misurazione dei contenuti multimediali di Adobe, figurano:

* **Analisi tempestiva:** prendi decisioni utili in tempo reale utilizzando metriche delle prestazioni chiave (ad esempio, durata) su più canali. Gli eventi di contenuto principale vengono misurati a intervalli di **10 secondi** per acquisire tutte le attività mentre si verificano. Gli eventi di tracciamento degli annunci si verificano a intervalli di **1 secondo**.
* **Aumento del coinvolgimento:** coinvolgi totalmente gli utenti con meno eventi di buffering e capendo dove e quando gli annunci dovrebbero essere riprodotti all’interno dei contenuti per fornire un’esperienza fluida e meno invasiva che possa richiamare gli utenti e offrire visite ripetute.
* **Immagine olistica:** combina più punti dati tra tutti i distributori di contenuti per ottenere una visione completa di tutte le attività multimediali e misurare il coinvolgimento e le visualizzazioni/gli ascolti tra tutti i possibili canali attraverso la funzione [Federated Analytics](/help/federated-analytics.md).
* **Maggiore granularità:** valuta il comportamento di visualizzazione al livello più granulare, inclusa l’ora del giorno per singolo visitatore, visualizzatori/ascoltatori simultanei per minuto e durata media di consumo del contenuto.
* **Misurazione precisa:** misura tra i diversi dispositivi utilizzati per il consumo di contenuti multimediali, inclusi OTT, smartphone, tablet, desktop e molto altro, per monitorare i pattern e le abitudini di coinvolgimento degli utenti.
* **Segmentazione:** applica le classificazioni ai tuoi lettori, dispositivi, generi, capitoli e presentazioni per vedere in che modo ciascuno di essi ha un impatto sulle visualizzazioni/sugli ascolti complessivi e sul coinvolgimento dei clienti con contenuti, audio, annunci pubblicitari e combinazioni di questi.

## Vantaggi di Heartbeat rispetto a Milestone {#heartbeat-versus-milestone-benefits}

Adobe Analytics for Media può effettuare le misurazioni in due modi: con il metodo precedente Milestone (solo video) e il metodo attuale Heartbeat (audio e video, disponibile sia in Media SDK che nell’API Media Collection). Il metodo Heartbeat è il metodo di misura preferito e invitiamo tutti i clienti a passare a questa versione, se non lo hanno già fatto, per sfruttare i vantaggi descritti di seguito.

Il metodo Milestone (precedente) si basa su singole chiamate server al server Analytics, per avvii, quartili, durata e completamenti video. Il metodo Heartbeat fornisce una soluzione di monitoraggio dei contenuti multimediali più affidabile che misura i contenuti principali a intervalli di 10 secondi per fornire metriche migliorate e standardizzate. Inoltre, Adobe ha tratto insegnamenti dal nostro metodo Milestone per fornire un processo di implementazione più fluido e semplificato tramite Media SDK o API Media Collection utilizzati da Heartbeat.

Alcuni dei molti vantaggi del metodo Heartbeat includono:

* **Processo di implementazione semplificato:** mappa più facilmente le variabili tramite l’API del lettore e convalida le implementazioni tramite lo strumento Adobe Debug per garantire che tutte le variabili necessarie siano tracciate con precisione.
* **Integrazione automatica di Adobe Experience Cloud**: sfrutta l’integrazione automatica con Adobe Experience Cloud tramite l’Experience Cloud ID, segmenta il pubblico dei contenuti multimediali, personalizza l’offerta e formula raccomandazioni multimediali in base alle preferenze degli utenti.
* **Dati condivisi tramite Federated Analytics:** sfrutta le nostre funzionalità di condivisione dei contenuti multimediali all’avanguardia per valutare i dati in modo olistico tra tutti i partner di distribuzione dei contenuti multimediali: operatori, programmatori e distributori.
* **Soluzione standardizzata su tutte le piattaforme:** abilita variabili coerenti e standardizzate su tutti i contenuti multimediali e le piattaforme per consentire un confronto tra campagne, dispositivi e fornitori più efficiente.
* **Tracciamento dei contenuti scaricati:** tieni traccia dei contenuti multimediali (video e audio) scaricati e riprodotti su un dispositivo, indipendentemente dalla connettività.

### Grafico di confronto

|  | Video Analytics - Milestone | Media Analytics - Heartbeat |
|---|---|---|
| **Eventi multimediali** | Eventi standard di alto livello | Eventi dettagliati e personalizzati ogni 10 secondi per i contenuti principali, ogni secondo per gli annunci |
| **Metriche e dimensioni** | Variazioni tra fornitori, metriche e dimensioni non standardizzate | Metriche, dimensioni e benchmark chiari e standardizzati tra fornitori |
| **Integrazioni con i prodotti Adobe** | Sessioni singole con alcune mappature e integrazioni | Experience Cloud ID collegato ad Adobe Experience Cloud completo per facilitare l’analisi incrociata |
| **Prezzi** | Tracciato e fatturato rispetto a ogni chiamata al server | Tracciamento trasparente per flusso multimediale (singolo) |
| **Implementazione e supporto** | Integrazioni più lunghe con supporto limitato alle versioni precedenti e nessun aggiornamento | Configurazione semplificata con aggiornamenti e miglioramenti continui |
| **Condivisione partner** | N/D | Federated Analytics e Certified Metrics |
| **Tracciamento avanzato** | N/D | Tracciamento recupero errori e visualizzatori simultanei |

## Dispositivi supportati {#devices-supported}

Adobe Analytics for Media si è evoluto con il settore per fornire potenti strumenti di raccolta dati che garantiscano la raccolta di ogni flusso multimediale e la generazione di report su tutti i dispositivi significativi. Il nostro Media SDK è stato sviluppato per tutti i dispositivi più utilizzati, tra cui:

* Smartphone e tablet iOS e Android
* Dispositivi OTT per ROKU, AppleTV, FireTV e Android TV
* Browser JavaScript per desktop e laptop

Gli SDK vengono costantemente aggiornati quando vengono rilasciate nuove versioni di dispositivi e puoi utilizzarli integrandoli con la maggior parte dei lettori multimediali più grandi di oggi, inclusi Brightcove e Ooyala.

Per i dispositivi o le piattaforme che al momento non dispongono (o anche se dispongono) del supporto SDK, puoi implementare l’API Media Collection, con cui effettuare chiamate RESTful API direttamente dal dispositivo/piattaforma al back-end Media Analytics.

La tabella seguente fornisce un elenco dei dispositivi attualmente supportati tramite l’implementazione Media SDK e quella API Media Collection. Per scaricare la versione più recente dell’SDK, consulta [Scaricare gli SDK.](sdk-implement/download-sdks.md) Se un dispositivo su cui si desidera effettuare la misurazione non è presente nell’elenco, contatta l’assistenza clienti o il consulente di soluzione per informazioni sullo stato del dispositivo.

|      | Media SDK | API Media Collection |
|---|:---:|:---:|
| **Browser JavaScript** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Dispositivi iOS** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Dispositivi Android** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Piattaforme universali di Windows (UWP)** |  | ![](assets/icon-blue-check.png) |
| **Blackberry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV (nuova/precedente)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (JS)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (app nativa)** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **Fire TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Chromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **Sony PS3/PS4** |  | ![](assets/icon-blue-check.png) |
| **(altri/nuovi dispositivi collegati)** |  | ![](assets/icon-blue-check.png) |

Per Media SDK, consulta anche [Supporto versione minima della piattaforma](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Transport Layer Security {#transport-layer-security}

**Avviso TLS:** Adobe ha standard di conformità per la sicurezza che richiedono la fine del ciclo di vita dei vecchi protocolli di sicurezza. Per continuare a soddisfare gli standard in continua evoluzione relativi ai protocolli di sicurezza, Adobe sta optando per l’uso di TLS 1.2, al fine di disporre della versione più aggiornata e sicura in uso. Dal 20 febbraio 2019, Adobe supporterà solo TLS 1.1 o versioni successive. Con questa modifica, Adobe non raccoglierà più dati dagli utenti finali con dispositivi o browser Web meno recenti che utilizzano TLS 1.0. La migrazione a TLS 1.2 offre una maggiore sicurezza. È importante che esamini a fondo le specifiche e pianifichi le modifiche per una transizione senza problemi.

>[!NOTE]
>
>TLS è attualmente tra i protocolli di sicurezza distribuiti più ampiamente ed è utilizzato nei browser web e altre applicazioni dove i dati devono essere scambiati in modo sicuro all’interno di una rete.

