---
seo-title: Misurazione di audio e video in Adobe Analytics
title: Misurazione di audio e video in Adobe Analytics
uuid: b 3 cbe 240-b 94 d -42 b 8-a 99 c -0280334 aaa 14
translation-type: tm+mt
source-git-commit: 1915261ec21679f510350663a472096abe7fdf63

---


# Measuring audio and video in Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>The documentation provided here is specific to clients utilizing version 1.5 or higher of Adobe's *Media SDK* for heartbeat measurement, or Adobe's newer *Media Collection API* for heartbeat measurement. Non include istruzioni sulla precedente implementazione di video Pietra miliare. Invitiamo tutti i clienti ad adottare una o entrambe le soluzioni di tracciamento dei contenuti multimediali più recenti, al fine di sfruttare i miglioramenti e la misurazione estesa. You can view the [benefits of transitioning to the latest solutions](media-overview.md#section_cnj_5st_p1b) below. Anche se continueremo a supportare il metodo milestone (Pietra miliare) dei video, non verranno pianificati aggiornamenti, correzioni o miglioramenti pianificati. Contattate il vostro Adobe Account Manager per ulteriori domande.

## Panoramica {#section_8BFE4F8DA64B4A5F826A4940B11AA466}

Adobe Analytics for Media (denominato anche Media Analytics) è un componente aggiuntivo all'offerta di base Analytics che offre ai client una misurazione solida dei contenuti multimediali per contenuto, audio e annunci pubblicitari. Media Analytics offre molti vantaggi ai clienti per consentire il monitoraggio in tempo reale, analisi dettagliate, approfondimenti fruibili e opportunità di monetizzazione.

Il tracciamento file multimediali è abilitato tramite una delle seguenti operazioni:

* **Media SDK -** Integrazione con i lettori multimediali più comunemente utilizzati.
* **API di Media Collection -** (API restful) si integrano con lettori per i quali non è supportato alcun supporto SDK (o con lettori per i quali non è richiesta alcuna integrazione SDK).

   L'API di Media Collection fornisce inoltre una funzionalità aggiuntiva non ancora disponibile nell'SDK:

   * **Tracciamento dei contenuti scaricato -** Fornisce supporto per il tracciamento del contenuto multimediale (video e audio) che viene scaricato e riprodotto da un dispositivo, a prescindere dalla connettività. Questa funzionalità è basata sull'API Media Collection e segue la stessa specifica di tracciamento del lettore. (Al momento il supporto per l’SDK non è disponibile.)

Adobe Analytics for Media consente ai client di monitorare l'intero percorso del cliente nel sito, incluso il consumo di contenuti multimediali, e tali misure sono facilmente integrate nei report di Analytics e in altri prodotti Experience Cloud. La misurazione file multimediali consente di suddividere e adattare i dati in più dimensioni e segmenti, acquisendo tutti i metadati necessari per un'analisi dettagliata e per attribuire criteri di successo a supporti completamente consumati, tempo medio trascorso e annunci completati.

Le soluzioni per contenuti multimediali non solo misurano metriche di consegna fondamentali correlate a QOS, come fotogrammi rilasciati, buffering trascorso e bitrate medio. Possono anche essere combinati con i dati del sito Web o dell'app per visualizzare il flusso del cliente e i relativi interessi, in modo da riuscire a formulare raccomandazioni e personalizzare le loro esperienze tramite Adobe Experience Cloud.

## Vantaggi {#section_7712BA90EAE64C118218D1C581EF68B7}

Alcuni dei numerosi vantaggi offerti dalle soluzioni di misurazione dei contenuti multimediali di Adobe includono:

* **Analisi tempestiva -** Prendere decisioni fruibili in tempo reale utilizzando metriche chiave delle prestazioni (ad es. durata) su più canali. Main content events are measured in **10-second** intervals to capture all activity as it occurs. Ad tracking events occur at **1-second** intervals.
* **Coinvolgimento del coinvolgimento -** Coinvolgere completamente gli utenti tramite un minor numero di eventi di buffering e capire dove e quando gli annunci devono essere riprodotti all'interno del contenuto per fornire un'esperienza fluida e meno coinvolgente che reindirizza gli utenti e distribuisca visite ripetute.
* **Illustrazione olistica -** Combinate più punti dati tra tutti i distributori di contenuti per visualizzare una visione completa di tutte le attività multimediali, misurare il coinvolgimento e visualizzare e ascoltare in tutti i canali possibili tramite la [funzione Federated Analytics](federated-analytics.md) .
* **Granularità aumentata:** valuta il comportamento di visualizzazione al livello più granulare, incluso l'ora del singolo visitatore, i visualizzatori/listener simultanei per minuto e la durata media del contenuto.
* **Misurazione precisa -** Misura tra i diversi dispositivi utilizzati per il consumo di contenuti multimediali, tra cui OTT, smartphone, tablet, desktop e altro ancora, per monitorare i pattern e le abitudini di coinvolgimento degli utenti.
* **Segmentazione -** Applica classificazioni ai tuoi giocatori, dispositivi, genres, capitoli e mostra il modo in cui ciascuna ha un impatto sulla vista/ascolto globale e sul coinvolgimento dei clienti con contenuto, audio, annunci e combinazione.

## Heartbeat versus Milestone benefits {#section_cnj_5st_p1b}

Adobe Analytics for Media può essere misurato tramite due metodi: il metodo milestone legacy (solo video) e il metodo Heartbeats corrente (audio e video, contenuti sia in Media SDK che nell'API Media Collection). Il metodo Heartbeats è il metodo di misura preferito e invitiamo tutti i client a passare a questa versione, se non lo hanno già fatto, per sfruttare i vantaggi descritti di seguito.

Il metodo milestone legacy si basa su singole chiamate server al server Analytics, per avvii di video, quariture, durata e completamenti. Il metodo Heartbeats offre una soluzione di tracciamento multimediale più solida che misura il contenuto principale a intervalli di 10 secondi per fornire metriche migliorate e standardizzate. Inoltre, Adobe ha derivato dal nostro metodo milestone per fornire un processo di implementazione più semplice e ottimizzato tramite Media SDK o Media Collection API utilizzato da Heartbeats.

Alcuni dei numerosi vantaggi del metodo Heartbeat includono:

* **Processo di implementazione semplificato -** Mappate le variabili più facilmente attraverso l'API del lettore e convalidate le implementazioni tramite Adobe Debug Tool per assicurarvi che tutte le variabili necessarie vengano tracciate con precisione.
* **Integrazione automatica di Adobe Experience Cloud** - Sfruttate l'integrazione automatica con Adobe Experience Cloud tramite Experience Cloud ID, segmentate i tipi di pubblico, impostateli e realizzate raccomandazioni sui supporti in base alle preferenze utente.
* **Dati condivisi tramite Analytics Federated -** Capitalize on our industry-first media sharing capabilities, to evaluate data oloriically in a media distribution partners (operatori, programmatori e distributori).
* **Partnership con partner di valutazione certificati -** Partner Adobe con partner Nielsen per fornire misurazioni di terze parti neutre per consentire valutazioni affidabili e certificate.
* **Soluzione standardizzata su tutte le piattaforme -** Abilita variabili coerenti e standardizzate su tutti i supporti e le piattaforme, per consentire un confronto più efficiente tra più campagne, dispositivi e fornitori.

### Grafico di confronto

|  | Analisi video - Pietra miliare | Media Analytics - Heartbeats |
|---|---|---|
| **Eventi multimediali** | Eventi standard di alto livello | Eventi dettagliati e personalizzati ogni 10 s per il contenuto principale, ogni 1 per annunci pubblicitari |
| **Metriche e dimensioni** | Varianti tra fornitori, metriche non standardizzate e dimensioni | Cancella, Metriche standardizzate, dimensioni e benchmark tra i fornitori |
| **Integrazioni w/Prodotti Adobe** | Sessioni individuali con mappature e integrazioni | ID di Experience Cloud completo collegato a Adobe Experience Cloud completo per una più semplice analisi incrociata |
| **Prezzi** | Tracciamento e fatturazione rispetto a ogni chiamata server | Tracciamento trasparente per flusso multimediale (singolo) |
| **Implementazione e supporto** | Integrazioni più lunghe con supporto limitato su versioni precedenti e nessun aggiornamento | Configurazione semplificata con aggiornamenti e miglioramenti continui |
| **Condivisione partner** | N/D | Analisi federate e metriche certificate |
| **Tracciamento avanzato** | N/D | Errori di recupero errori e visualizzatori simultanei |

## Devices supported {#section_lkm_l5t_p1b}

Adobe Analytics for Media si è evoluto con il settore per fornire sofisticati strumenti di raccolta dati per garantire che ogni flusso multimediale venga raccolto e segnalato su tutti i dispositivi significativi. Il nostro SDK Media è sviluppato per tutti i dispositivi più utilizzati, tra cui:

* Smartphone iOS e Android e tablet
* Dispositivi OTT per dispositivi ROKU, appletv, firetv e Android TV
* Browser javascript per Desktop e Laptop

Gli SDK vengono costantemente aggiornati quando vengono rilasciate nuove versioni dei dispositivi, e puoi usare questi SDK per l'integrazione con la maggior parte dei principali lettori multimediali oggi, inclusi Brightcove e Ooyala.

Per i dispositivi o le piattaforme che al momento non dispongono di supporto SDK (o anche se sono), puoi implementare l'API Media Collection API tramite la quale effettuerai chiamate API restful direttamente dal dispositivo o dalla piattaforma al back-backend di Media Analytics.

La tabella seguente fornisce un elenco dei dispositivi attualmente supportati tramite l'implementazione Media SDK e l'implementazione API di Media Collection. To download the most recent version of the SDK, see [Download SDKs.](sdk-implement/download-sdks.md) Se esiste un dispositivo a cui stai cercando la misurazione, contatta l'assistenza clienti o il consulente della soluzione per lo stato del dispositivo.

|      | Media SDK | API di raccolta multimediale |
|---|:---:|:---:|
| **Browser javascript** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Dispositivi iOS** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Dispositivi Android** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Piattaforme Windows (UWP) unificate** |  | ![](assets/icon-blue-check.png) |
| **Blackberry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV (nuovo/legacy)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (JS)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (app nativa)** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **Fire TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Chromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **Sony PS 3/PS 4** |  | ![](assets/icon-blue-check.png) |
| **(Altri dispositivi connessi)** |  | ![](assets/icon-blue-check.png) |

For Media SDK, also see [Minimum Platform Version Support](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Transport Layer Security {#transport-layer-security}

**Avviso TLS —** Adobe offre standard di conformità alla sicurezza che richiedono la fine di vecchi protocolli di sicurezza. Per continuare a soddisfare gli standard del protocollo di protezione in evoluzione, Adobe si sposta verso l'utilizzo di TLS 1.2, per disporre della versione più aggiornata e sicura utilizzata. Dal 20 febbraio 2019, Adobe supporterà solo TLS 1.1 o versione successiva. Con questa modifica, Adobe non raccoglierà più i dati degli utenti finali con dispositivi meno recenti o browser Web che implementano TLS 1.0. La migrazione a TLS 1.2 offre una maggiore protezione. È importante che esamini a fondo le specifiche e pianifichi le modifiche per una transizione senza problemi.

>[!NOTE]
>
>TLS è il protocollo di protezione più diffuso utilizzato nei browser Web e in altre applicazioni che richiedono la sicurezza sicura dei dati attraverso una rete.
