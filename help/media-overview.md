---
seo-title: Misurazione di audio e video in Adobe Analytics
title: Misurazione di audio e video in Adobe Analytics
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: 5fc38098bcd497f3305f76ae2b23757b5f81ac69

---


# Misurazione di audio e video in Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>La documentazione fornita di seguito è specifica per i client che utilizzano la versione 1.5 o successiva dell’SDK *Adobe* Media per la misurazione heartbeat o l’API *Adobe* Media Collection più recente per la misurazione heartbeat. Non include istruzioni relative all’implementazione video legacy di Milestone. Invitiamo tutti i clienti ad adottare una o entrambe le più recenti soluzioni di monitoraggio dei supporti, al fine di sfruttare al meglio i miglioramenti e l'espansione delle misurazioni. Puoi visualizzare i [vantaggi della transizione alle soluzioni](media-overview.md#section_cnj_5st_p1b) più recenti riportate di seguito. Anche se continueremo a supportare il metodo Milestone (pietra miliare) per il tracciamento dei video, non ci saranno aggiornamenti, correzioni o miglioramenti delle funzionalità pianificati. Per ulteriori domande, contattate il vostro Adobe Account Manager.

## Panoramica {#section_8BFE4F8DA64B4A5F826A4940B11AA466}

Adobe Analytics for Media (altrimenti denominato Media Analytics) è un componente aggiuntivo dell'offerta Analytics di base che fornisce ai client una misurazione affidabile dei contenuti multimediali per contenuti, audio e annunci pubblicitari. Media Analytics offre molti vantaggi ai clienti per consentire il monitoraggio in tempo reale, analisi dettagliate, informazioni fruibili e opportunità di monetizzazione.

Il tracciamento dei file multimediali è abilitato tramite una delle seguenti opzioni:

* **Media SDK -** Si integra con i lettori multimediali più comunemente utilizzati.
* **API di Media Collection -** (RESTful API) Si integra con lettori per i quali non è disponibile alcun supporto SDK (o con lettori per i quali non è richiesta alcuna integrazione SDK).

Adobe Analytics per Media consente ai clienti di monitorare l'intero percorso del cliente attraverso il sito, che include il consumo di supporti, e queste misure sono facilmente integrate nei report di Analytics e in altri prodotti Experience Cloud. La misurazione dei file multimediali consente di suddividere i dati in più dimensioni e segmenti, acquisire tutti i metadati necessari per eseguire un’analisi completa e dettagliata e attribuire i criteri di successo a supporti completamente utilizzati, al tempo medio trascorso e agli annunci completati.

Le soluzioni per i media non solo misurano le metriche di distribuzione vitali correlate ai QoS, come fotogrammi saltati, tempo impiegato nel buffering e bitrate medio. Possono anche essere combinati con i dati del tuo sito web o dell'app per visualizzare il flusso del cliente e i loro interessi, per essere in grado di formulare raccomandazioni e personalizzare le loro esperienze tramite Adobe Experience Cloud.

## Vantaggi {#section_7712BA90EAE64C118218D1C581EF68B7}

Tra i numerosi vantaggi offerti dalle soluzioni di misurazione dei supporti di Adobe, figurano:

* **Analisi tempestiva: prendere decisioni in tempo reale e fruibili utilizzando metriche delle prestazioni chiave (ad esempio, durata) su più canali.** Gli eventi di contenuto principale vengono misurati a intervalli di **10 secondi** per acquisire tutte le attività mentre si verifica. Gli eventi di tracciamento degli annunci si verificano a intervalli di **1 secondo** .
* **Stimolare il coinvolgimento degli utenti -** Coinvolgere gli utenti in un numero minore di eventi di buffering e comprendere dove e quando gli annunci dovrebbero essere riprodotti all'interno dei contenuti per fornire un'esperienza fluida e meno intrusiva che possa richiamare gli utenti e offrire visite ripetute.
* **Immagine olistica: combinare più punti dati tra tutti i distributori di contenuti per ottenere una visione completa di tutte le attività multimediali e misurare il coinvolgimento e le visualizzazioni/gli accessi tra tutti i possibili canali attraverso la funzione** Federated Analytics [](/help/federated-analytics.md) .
* **Maggiore granularità:** valutate il comportamento di visualizzazione al livello più granulare, inclusa l'ora del giorno per singolo visitatore, gli utenti simultanei/i listener per minuto e la durata media del consumo del contenuto.
* **Misurazione precisa - Misurate** tra i diversi dispositivi utilizzati per il consumo di contenuti multimediali, inclusi OTT, smartphone, tablet, desktop e molto altro, per monitorare i pattern e le abitudini di coinvolgimento degli utenti.
* **Segmentazione: applica le classificazioni ai tuoi lettori, dispositivi, generi, capitoli e presentazioni per vedere in che modo ciascuno di essi ha un impatto sulle viste/sugli ascolti complessivi e sul coinvolgimento dei clienti con contenuti, audio, annunci pubblicitari e insieme.**

## Vantaggi di Heartbeat e Milestone {#section_cnj_5st_p1b}

Adobe Analytics for Media può essere misurato in due modi: il metodo Milestone (solo video) e il metodo Heartbeats corrente (audio e video, disponibile sia in Media SDK che nell’API di Media Collection). Il metodo Heartbeats è il metodo di misura preferito e invitiamo tutti i clienti a passare a questa versione, se non lo hanno già fatto, per sfruttare i vantaggi descritti di seguito.

Il metodo Milestone (legacy) è basato su singole chiamate server al server Analytics, per avvii video, quartili, durata e completati. Il metodo Heartbeats fornisce una soluzione di monitoraggio dei supporti più affidabile che misura i contenuti principali a intervalli di 10 secondi per fornire metriche migliorate e standardizzate. Inoltre, Adobe ha tratto insegnamenti dal nostro metodo Milestone per fornire un processo di implementazione più fluido e semplificato tramite Media SDK o Media Collection API utilizzata da Heartbeats.

Alcuni dei molti vantaggi del metodo Heartbeats includono:

* **Processo di implementazione semplificato: mappate più facilmente le variabili tramite l'API del lettore e convalidate le implementazioni tramite Adobe Debug Tool per garantire che tutte le variabili necessarie siano tracciate con precisione.**
* **Integrazione** automatica di Adobe Experience Cloud - Sfruttate l'integrazione automatica con Adobe Experience Cloud tramite Experience Cloud ID, segmentate il pubblico dei supporti, miratelo e formulate raccomandazioni sui supporti in base alle preferenze degli utenti.
* **Dati condivisi tramite Federated Analytics -** Sfruttate le nostre prime funzionalità di condivisione dei contenuti multimediali per valutare i dati in modo olistico tra tutti i partner di distribuzione dei contenuti multimediali: operatori, programmatori e distributori.
* **Partnership con i partner di classificazioni certificate -** Adobe collabora con il partner Nielsen per la valutazione del pubblico allo scopo di fornire misurazioni neutre del censimento di terze parti per consentire valutazioni affidabili e certificate.
* **Soluzione standardizzata su tutte le piattaforme: abilita variabili coerenti e standardizzate su tutti i supporti e le piattaforme per consentire un confronto tra campagne, dispositivi e fornitori più efficiente.**
* **Tracciamento dei contenuti scaricati - Consente di tenere traccia dei contenuti multimediali (video e audio) scaricati e riprodotti su un dispositivo, indipendentemente dalla connettività.**

### Grafico di confronto

|  | Video Analytics - Milestone | Media Analytics - Heartbeat |
|---|---|---|
| **Eventi multimediali** | Eventi standard di alto livello | Eventi dettagliati e personalizzati ogni 10 anni per i contenuti principali, ogni 1 anno per gli annunci |
| **Metriche e dimensioni** | Variazioni tra fornitori, metriche e dimensioni non standardizzate | Metriche, dimensioni e benchmark chiari e standardizzati tra fornitori |
| **Integrazioni con i prodotti Adobe** | Sessioni singole con alcune mappature e integrazioni | ID Experience Cloud unito collegato ad Adobe Experience Cloud completo per facilitare l’analisi incrociata |
| **Prezzi** | Tracciato e fatturato rispetto a ogni chiamata al server | Tracciamento trasparente per flusso multimediale (singolo) |
| **Implementazione e supporto** | Integrazioni più lunghe con supporto limitato alle versioni precedenti e nessun aggiornamento | Configurazione semplificata con aggiornamenti e miglioramenti continui |
| **Condivisione partner** | N/D | Analisi federate e metriche certificate |
| **Tracciamento avanzato** | N/D | Tracciamento del recupero errori e visualizzatori simultanei |

## Dispositivi supportati {#section_lkm_l5t_p1b}

Adobe Analytics for Media si è evoluto con il settore per fornire potenti strumenti di raccolta dati che garantiscano la raccolta e la generazione di report su tutti i dispositivi significativi. Il nostro Media SDK è sviluppato per tutti i dispositivi più utilizzati, tra cui:

* Smartphone e tablet iOS e Android
* Dispositivi OTT per ROKU, AppleTV, FireTV e Android TV
* Browser JavaScript per desktop e notebook

Gli SDK vengono costantemente aggiornati quando vengono rilasciate nuove versioni di dispositivi e puoi utilizzare questi SDK per integrarsi con la maggior parte dei lettori multimediali più grandi di oggi, inclusi Brightcove e Ooyala.

Per i dispositivi o le piattaforme che al momento non dispongono del supporto SDK (o anche se lo fanno), puoi implementare l'API Media Collection, tramite la quale effettuerai chiamate RESTful API direttamente dal dispositivo/piattaforma al backend di Media Analytics.

La tabella seguente fornisce un elenco dei dispositivi attualmente supportati tramite l’implementazione di Media SDK e l’implementazione di Media Collection API. Per scaricare la versione più recente dell’SDK, consulta [Scaricare gli SDK.](sdk-implement/download-sdks.md) Se esiste un dispositivo che non è elencato e su cui si desidera effettuare la misurazione, contattare l'assistenza clienti o il consulente della soluzione per informazioni sullo stato del dispositivo.

|      | Media SDK | API di raccolta multimediale |
|---|:---:|:---:|
| **Browser JavaScript** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Dispositivi iOS** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Dispositivi Android** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Piattaforme Windows unificate (UWP)** |  | ![](assets/icon-blue-check.png) |
| **Blackberry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV (nuovo/precedente)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (JS)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (app nativa)** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **TV a fuoco** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Chromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **Sony PS3/PS4** |  | ![](assets/icon-blue-check.png) |
| **(altri/nuovi dispositivi collegati)** |  | ![](assets/icon-blue-check.png) |

Per Media SDK, consulta anche Supporto versione [minima della piattaforma](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Sicurezza dei livelli di trasporto {#transport-layer-security}

**Avviso TLS —** Adobe ha standard di conformità per la sicurezza che richiedono la fine del ciclo di vita dei vecchi protocolli di sicurezza. Per continuare a soddisfare gli standard in continua evoluzione relativi ai protocolli di sicurezza, Adobe si sta muovendo verso l'uso di TLS 1.2, al fine di disporre della versione più aggiornata e sicura in uso. Dal 20 febbraio 2019, Adobe supporterà solo TLS 1.1 o versione successiva. Con questa modifica, Adobe non raccoglierà più dati dagli utenti finali con dispositivi o browser Web meno recenti che implementano TLS 1.0. La migrazione a TLS 1.2 offre una maggiore sicurezza. È importante che esamini a fondo le specifiche e pianifichi le modifiche per una transizione senza problemi.

>[!NOTE]
>
>TLS è attualmente il protocollo di sicurezza più diffuso utilizzato nei browser Web e in altre applicazioni che richiedono lo scambio sicuro dei dati in rete.
