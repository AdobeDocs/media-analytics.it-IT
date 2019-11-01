---
title: Panoramica delle attività cardine
description: null
uuid: 2f9ec6bb-8860-4863-98bc-5cffb356ccc5
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Panoramica delle attività cardine{#milestone-overview}

>[!CAUTION]
>
>Questa opzione di misura è stata rimossa.

[Documentazione precedente di Milestone](milestone_analytics_video.pdf)

## Configurazione {#configuration}

### Configurazione video cardine

Per tracciare il video, specificate un set di variabili *di conversione* personalizzate (eVar) ed eventi ** personalizzati da usare per il tracciamento e il reporting. Per il percorso viene utilizzata anche una variabile *Custom Insight* ( `s.prop` ).

Le variabili selezionate per ciascuna metrica vengono aggiunte alla pagina di configurazione video. Questo consente al sistema di generare e formattare automaticamente i rapporti video standard. Il nome ** video eVar e il contatore delle viste ** video sono entrambi obbligatori. Altre variabili sono facoltative ma consigliate per la misurazione completa. Dopo aver abilitato il tracciamento video, potete visualizzare i rapporti generati dai dati video segnalati mediante il tracciamento video.

Potete anche tenere traccia di un numero qualsiasi di metriche aggiuntive per i video. Ad esempio, se usate più lettori video sul sito, potreste compilare un eVar con il nome del lettore. Alcune delle variabili selezionate possono essere utilizzate anche in altre aree del sito. Ad esempio, se utilizzata in tutto il sito, la variabile del tipo *di* contenuto può consentire di misurare la percentuale di visualizzazioni di pagina che proviene dal video e consentire di collegare gli eventi di conversione al video.

### Configurazione dei rapporti sulle attività cardine

Per impostare il reporting video per un'implementazione Milestone, passate a **[!UICONTROL Admin > Report Suite Manager].** Selezionate la suite di rapporti, quindi scegliete **[!UICONTROL Video Management > Video Reporting]:**

<!--![](assets/0clip_image002_1537416456.png){width="248"}-->
![](assets/rs1.png)

Nella prima schermata, solo Video Core funziona con i dati Milestone. Selezionate **[!UICONTROL Video Core]** e fate clic su **[!UICONTROL Save].**

![](assets/video-core-check.png)

Nella schermata successiva, selezionate **[!UICONTROL Use Custom Variables].**

<!--![](assets/0clip_image006_-1561510960.png){width="470"}-->
![](assets/rs2.png)

Nella schermata finale, selezionate le due eVar e i tre eventi da usare per la misurazione video:

<!--![](assets/0clip_image008_-92166399.png)-->
![](assets/rs3.png)

## Riferimento variabile video {#video-variable-reference}

La tabella seguente contiene ulteriori dettagli sulle variabili commerce e gli eventi personalizzati per i video:

| Metrica video | Tipo di variabile | Descrizione |
| --- | --- | --- |
| Contenuto | Scadenza <br/>predefinita eVar: Visita | (Obbligatorio) Raccoglie il nome del video, come specificato nell’implementazione. |
| Tipo di contenuto | eVar <br/>Default expiration: Page view | Raccoglie dati relativi al tipo di contenuto visualizzato da un visitatore. Agli hit inviati dalla misurazione video viene assegnato un tipo di contenuto di `video.` <br/>Questa variabile non deve essere riservata esclusivamente al tracciamento video. La presenza di altri tipi di contenuto nei rapporti con la stessa variabile consente di analizzare la distribuzione dei visitatori tra i diversi tipi di contenuto. For example, you could tag other content types using values such as `article` or `product page` using this variable. <br/>Dal punto di vista della misurazione video, *Content Type* (Tipo di contenuto) consente di identificare i visitatori del video e quindi calcolare i tassi di conversione del video. |
| Tempo contenuto trascorso | Tipo <br/>evento: Contatore | Conta il tempo, in secondi, trascorso a guardare un video dall'ultimo processo di raccolta di dati (richiesta immagine). |
| Avvio video | Tipo <br/>evento: Contatore | Indica che un visitatore ha visualizzato una parte di un video. Tuttavia, non fornisce informazioni sulla parte specifica visualizzata, né sulla durata della visualizzazione. |
| Completamento video | Tipo <br/>evento: Contatore | Indica che un utente ha visualizzato un video completo. Per impostazione predefinita, l'evento completo è misurato 1 secondo prima della fine del video.  <br/>Durante l'implementazione, puoi specificare quanti secondi dalla fine del video considerare come una visualizzazione dell'intero video. Per i video in diretta e altri flussi che non hanno una fine definita, puoi specificare un punto personalizzato per misurare il completamento. Ad esempio, dopo un tempo di visualizzazione specifico. |

## Variabili del modulo multimediale {#media-module-variables}

Le seguenti variabili consentono di configurare la misurazione video. È necessario definire i valori per le variabili nella tabella Variabili richieste. Inoltre, per tenere traccia degli eventi nel lettore video, è necessario abilitare autoTrack (per i lettori supportati) o implementare il tracciamento personalizzato degli eventi del lettore utilizzando i metodi open, play, stop e close.

| Variabile    | Descrizione |
| --- | --- |
| `Media.trackUsingContextData` | **Sintassi:** <br/><br/> `s.Media.trackUsingContextData = true;` <br/>Questa opzione consente il tracciamento video integrato. Quando è impostato su true, il modulo multimediale genera i dati contestuali per il tracciamento dei supporti, invece che per le versioni precedenti `pev3`. <br/>Utilizzare `Media.contextDataMapping` per mappare i dati contestuali alle eVar ed Eventi selezionati.<br/>Valore predefinito: `false` |
| `Media.contextDataMapping` | **Sintassi:** <br/><br/> `s.Media.contextDataMapping = {`<br/>      `"a.media.name":"eVar2, prop2",` <br/>     `"a.media.segment":"eVar3",` <br/>     `"a.contentType":"eVar1",` <br/>     `"a.media.timePlayed":"event3",` <br/>     `"a.media.view":"event1",` <br/>     `"a.media.segmentView":"event2",` <br/>     `"a.media.complete":"event7",` <br/>     `"a.media.milestones":{` <br/>         `25:"event4",` <br/>         `50:"event5",` <br/>         `75:"event6"` <br/>     ` }` <br/> `};` Oggetto <br/><br/>che definisce la mappatura delle variabili a eVar ed Eventi da utilizzare per la misurazione video. L'oggetto deve mappare i campi seguenti: <br/><br/> **** a.media.name: (Obbligatorio) Compila le variabili con il nome del video. Specificate l'eVar selezionata per memorizzare il nome del video e la variabile Video personalizzato ( `s.prop` ) da usare per il percorso del video. Immettete i valori in un elenco separato da virgole. <br/><br/> **** a.media.segment: (Facoltativo) L'eVar che si desidera memorizzare il nome del segmento del supporto. a.contentType: (Facoltativo) L'eVar che desideri memorizzare il valore video, che contiene il tracciamento delle visite e dei visitatori abilitato per generare rapporti sulle visite video e sui visitatori. La variabile selezionata è probabilmente già utilizzata per memorizzare i dati, ad esempio la presentazione articolo o la pagina prodotto <br/><br/> **** a.media.view: (Obbligatorio) L’evento al quale si desidera conteggiare le visualizzazioni dei file multimediali. <br/><br/> **** a.media.segmentView: (Facoltativo) L’evento che si desidera contare sulle visualizzazioni dei segmenti. <br/><br/> **** a.media.complete: (Facoltativo) L’evento da conteggiare come viste complete. <br/><br/> **** a.media.timePlayed: (Facoltativo, fortemente consigliato) L’evento numerico per il quale memorizzare il numero di secondi di video riprodotti. <br/><br/> **** a.media.milestones: (Facoltativo) Un oggetto che esegue la mappatura delle pietre miliari s.Media.trackMilestones per contrastare gli eventi. Se definisci le tappe, Media.segmentByMilestones deve essere impostato su true. <br/><br/> **Tracciamento** annunci Per tenere traccia degli annunci, sono disponibili le seguenti variabili di dati contestuali: <br/> **** a.media.ad.naà: (Obbligatorio) Compila le variabili con il nome dell'annuncio. Fornite l'eVar selezionata per memorizzare il nome dell'annuncio e la variabile Video personalizzato ( `s.prop` ) da utilizzare per il percorso. Immettete i valori in un elenco separato da virgole. <br/><br/> **** a.media.ad.pod: Posizione nel contenuto principale in cui è stato riprodotto l’annuncio. <br/><br/> **** a.media.ad.podPosition: Posizione all’interno del contenitore in cui viene riprodotto l’annuncio. <br/><br/> **** a.media.ad.CPM: CPM o CPM crittografato (con il prefisso "~") che si applica a questa riproduzione. <br/><br/> **** a.media.ad.vià: Funziona come `a.media.view`<br/><br/> **** a.media.ad.cl: Numero di clic per l’annuncio (`Media.click` chiamate) <br/><br/> **** a.media.ad.timePlayed: Funziona come `a.media.timePlayed`<br/><br/> **** a.media.ad.complete: Funziona come `a.media.complete` a.media.ad.segment: Funziona come `a.media.segment`<br/><br/> **** a.media.ad.seegmentView: Funziona come `a.media.segmentView`<br/><br/> **** a.media.ad.milestones: Funziona come `a.media.milestones`<br/><br/> **** a.media.ad.offsetMilestones: Funziona come `a.media.offsetMilestones` |
| `Media.trackVars` | **Sintassi:** <br/><br/> `s.Media.trackVars =` <br/>    `"events,``prop2,` `eVar1,` `eVar2,` `eVar3";` <br/><br/>Elenco separato da virgole di tutte le variabili impostate nel codice di tracciamento video. |
| `Media.trackEvents` | **Sintassi:** <br/><br/> `s.Media.trackEvents =` <br/>    `"event1,``event2,``event3,``event4,``event5,` `event6,` `event7"` <br/><br/>Elenco separato da virgole di tutti gli eventi impostati nel codice di tracciamento video. |

## Variabili facoltative {#optional-variables}

|  Variabile    | Descrizione |
| --- | --- |
| `Media.autoTrack` | **Sintassi:** <br/><br/> `s.Media.autoTrack = true` <br/><br/>Abilita il tracciamento automatico per i lettori supportati. I lettori supportati sono i seguenti: <ul> <li> Open Source Media Framework (OSMF) </li> <li> FLVPlayback (lettori video creati dalla procedura guidata di importazione video in Flash Professional) </li> <li> Silverlight </li> <li> MediaDisplay </li> <li> MediaPlayback </li> <li> Brightcove API versioni 2 e 3 (consultate [Brightcove](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_other_players.html)) </li> <li> Windows Media Player, Quicktime o Real Player con JavaScript </li> </ul> <br/><br/>Se non si utilizza uno dei lettori di cui sopra è possibile utilizzare `Media.open``Media.play` `Media.stop` `Media.close` per tenere traccia degli eventi dei giocatori. |
| `Media.autoTrackNetStreams` | **Sintassi:** <br/><br/> `s.Media.autoTrackNetStreams = true` <br/><br/>Flash 10.3 ha introdotto nuove funzionalità per il componente NetStream che consentono il tracciamento video migliorato. Se si utilizza un lettore Flash NetStream personalizzato, è possibile abilitare questa variabile per abilitare funzionalità simili a autoTrack. Questo metodo richiede che i video vengano visualizzati in Flash 10.3 o versioni successive. |
| `Media.completeByCloseOffset` | **Sintassi:** <br/><br/> <br/><br/>`s.Media.completeByCloseOffset = true` <br/><br/>Questa impostazione consente di contare una visualizzazione video completa qualche secondo prima della fine effettiva del video.  <br/><br/>L’evento viene inviato in base al numero di secondi specificato in `completeCloseOffsetThreshold`. Questo consente di misurare i completamenti in lettori video che non riportano mai un offset uguale alla lunghezza del video.<br/><br/>Per impostazione predefinita, questo valore è impostato su true e la soglia è impostata su 1 secondo. Con queste impostazioni predefinite, l’evento completo viene inviato 1 secondo prima della fine del video. |
| `Media.completeCloseOffsetThreshold` | **Sintassi:** <br/><br/> `s.Media.completeCloseOffsetThreshold = 1` <br/><br/>Questa soglia consente di contare una visualizzazione video completa alcuni secondi prima della fine effettiva del video.  `Media.completeByCloseOffset` deve essere impostato su true per utilizzare questa soglia.<br/><br/>Il valore intero fornito determina la distanza in secondi dell’offset rispetto alla lunghezza del video alla chiusura e al conteggio come completo. Questo consente di misurare i completamenti in lettori video che non riportano mai un offset uguale alla lunghezza del video.  <br/><br/>La soglia predefinita è 1 secondo. |
| `Media.playerName` | **Sintassi:** <br/><br/> `s.Media.playerName = "Custom Player Name"` <br/><br/>Specifica un nome di lettore video personalizzato. |
| `Media.trackSeconds` | **Sintassi:** <br/><br/> `s.Media.trackSeconds = 15` <br/><br/>Definisce l’intervallo, in secondi, per l’invio dei dati di tracciamento video ai server di raccolta dati Adobe durante la riproduzione del video. Il valore deve essere impostato in incrementi di 5 secondi. <br/><br/> L'attivazione `Media.trackSeconds` attiva solo gli eventi definiti in `Media.contextDataMapping`. Per inviare ulteriori variabili al di fuori di quelle specificate per la misurazione video, è necessario utilizzare Media.Monitor. |
| `Media.trackMilestones` | Tiene traccia delle pietre miliari come percentuale della lunghezza del video.  <br/><br/> **Sintassi:** <br/><br/> `s.Media.trackMilestones = "25, 50, 75";` Definisce <br/><br/>l’intervallo, in percentuale della lunghezza del video, per l’invio dei dati di tracciamento video ai server di raccolta dati Adobe. Specificare le pietre miliari come un elenco separato da virgole di numeri interi. Ad esempio: 10 = 10%, 23 = 23%.  <br/><br/>Poiché queste pietre miliari sono punti fissi nel video, se un visitatore visualizza oltre la soglia del 10%, quindi riavvolge e passa di nuovo la soglia del 10%, il modulo multimediale invia i dati di tracciamento più volte. Allo stesso modo, se un visitatore inoltra rapidamente oltre una pietra miliare, il modulo multimediale non invia i dati di tracciamento per quella pietra miliare.  <br/><br/>L'attivazione `Media.trackMilestones` attiva solo gli eventi definiti in `Media.contextDataMapping`. Per inviare ulteriori variabili al di fuori di quelle specificate per la misurazione video, è necessario utilizzare Media.Monitor. |
| `Media.trackOffsetMilestones` | Tiene traccia dei punti cardine come secondi trascorsi dall’inizio del video.  <br/><br/> **Sintassi:** <br/><br/> `s.Media.trackOffsetMilestones = "20, 40, 60";` <br/><br/>Definisce l’intervallo, in secondi trascorsi dall’inizio del video, per l’invio dei dati di tracciamento video ai server di raccolta dati Adobe. Specificare le pietre miliari come un elenco separato da virgole di numeri interi. Ad esempio: 20 = 20 secondi, 40 = 40 secondi).  <br/><br/>Poiché queste pietre miliari sono punti fissi nel video, se un visitatore visualizza oltre la fase cardine di 20 secondi, quindi riavvolge e passa nuovamente la fase cardine di 20 secondi, il modulo multimediale invia i dati di tracciamento più volte. Allo stesso modo, se un visitatore inoltra rapidamente oltre una pietra miliare, il modulo multimediale non invia i dati di tracciamento per quella pietra miliare.  <br/><br/> L'attivazione `Media.trackOffsetMilestones` attiva solo gli eventi definiti in `Media.contextDataMapping`. Per inviare ulteriori variabili al di fuori di quelle specificate per la misurazione video, è necessario utilizzare Media.Monitor. |
| `Media.segmentByMilestones` | **Sintassi:** <br/><br/> `s.Media.segmentByMilestones = true;` Genera <br/><br/>automaticamente i dati relativi al nome del segmento, al numero del segmento e alla lunghezza del segmento, in base alla lunghezza del supporto e alle tappe specificate in `Media.trackMilestones` Segmentazione per <br/><br/>fasi miliari è l’unico modo per definire i segmenti quando si utilizza `autoTrack`. <br/><br/>Valore predefinito: `false` |
| `Media.segmentByOffsetMilestones` | **Sintassi:** <br/><br/> `s.Media.segmentByOffsetMilestones = true;` Genera <br/><br/>automaticamente i dati relativi al nome del segmento, al numero del segmento e alla lunghezza del segmento, in base alla lunghezza del supporto e alle tappe specificate in `Media.trackOffsetMilestones` Segmentazione per <br/><br/>fasi miliari è l’unico modo per definire i segmenti quando si utilizza `autoTrack`.  <br/><br/>Valore predefinito: `false` |

## Variabili di tracciamento annunci {#ad-tracking-variables}

Queste variabili vengono utilizzate per inviare informazioni sugli annunci insieme al metodo openAd. Consultate [VAST Video Ad Tracking.](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_ads.html)

| Variabile    | Descrizione |
| --- | --- |
| `Media.adTrackSeconds` | **Sintassi:** <br/><br/> `s.Media.adTrackSeconds = 15;` <br/><br/>Definisce l'intervallo, in secondi, per l'invio di dati di tracciamento annuncio video ai server di raccolta dati Adobe durante la riproduzione del video. Il valore deve essere impostato in incrementi di 5 secondi.  <br/><br/> L'attivazione `Media.adTrackSeconds` attiva solo gli eventi definiti in `Media.contextDataMapping`. Per inviare ulteriori variabili al di fuori di quelle specificate per la misurazione video, è necessario utilizzare `Media.monitor`. |
| `Media.adTrackMilestones` | Tiene traccia e pietre miliari come percentuale della lunghezza dell'annuncio.  <br/><br/> **Sintassi:** <br/><br/> `s.Media.adTrackMilestones = "25, 50, 75";` <br/><br/>Definisce l'intervallo, in percentuale della lunghezza dell'annuncio, per l'invio dei dati di tracciamento annunci ai server di raccolta dati Adobe. Specificare le pietre miliari come un elenco separato da virgole di numeri interi. Ad esempio: 10 = 10%, 23 = 23%).  <br/><br/>Poiché queste pietre miliari sono punti fissi nell’annuncio, se un visitatore visualizza oltre il 10% della pietra miliare, quindi riavvolge e passa nuovamente il 10% della pietra miliare, il modulo multimediale invia i dati di tracciamento più volte. Allo stesso modo, se un visitatore inoltra rapidamente oltre una pietra miliare, il modulo multimediale non invia i dati di tracciamento per quella pietra miliare.  <br/><br/> L'attivazione `Media.adTrackMilestones` attiva solo gli eventi definiti in `Media.contextDataMapping`. Per inviare ulteriori variabili al di fuori di quelle specificate per la misurazione video, è necessario utilizzare `Media.monitor`. |
| `Media.adTrackOffsetMilestones` | Tiene traccia e punti intermedi come secondi trascorsi dall’inizio dell’annuncio.  <br/><br/> **Sintassi:** <br/><br/> `s.Media.adTrackOffsetMilestones = "20, 40, 60";` <br/><br/>Definisce l’intervallo, in secondi trascorsi dall’inizio dell’annuncio, per l’invio dei dati di tracciamento annunci ai server di raccolta dati Adobe. Specificare le pietre miliari come un elenco separato da virgole di numeri interi. Ad esempio: 20 = 20 secondi, 40 = 40 secondi).  <br/><br/>Poiché queste pietre miliari sono punti fissi nell’annuncio, se un visitatore visualizza oltre i 20 secondi di attività cardine, riavvolge e passa nuovamente la fase cardine di 20 secondi, il modulo multimediale invia i dati di tracciamento più volte. Allo stesso modo, se un visitatore inoltra rapidamente oltre una pietra miliare, il modulo multimediale non invia i dati di tracciamento per quella pietra miliare.  <br/><br/> L'attivazione `Media.adTrackOffsetMilestones` attiva solo gli eventi definiti in `Media.contextDataMapping`. Per inviare ulteriori variabili al di fuori di quelle specificate per la misurazione video, è necessario utilizzare `Media.monitor`. |
| `Media.adSegmentByMilestones` | **Sintassi:** <br/><br/> `s.Media.adSegmentByMilestones = true;` Genera <br/><br/>automaticamente i dati relativi al nome del segmento, al numero del segmento e alla lunghezza del segmento, in base alla lunghezza del supporto e alle tappe specificate in `Media.adTrackMilestones` Segmentazione per <br/><br/>fasi miliari è l’unico modo per definire i segmenti quando si utilizza `autoTrack`.  <br/><br/>Valore predefinito: `false` |
| `Media.adSegmentByOffsetMilestones` | **Sintassi:** <br/><br/> `s.Media.adSegmentByOffsetMilestones = true;` Genera <br/><br/>automaticamente i dati relativi al nome del segmento, al numero del segmento e alla lunghezza del segmento, in base alla lunghezza del supporto e alle tappe specificate in `Media.adTrackOffsetMilestones` Segmentazione per <br/><br/>fasi miliari è l’unico modo per definire i segmenti quando si utilizza `autoTrack`. <br/><br/>Valore predefinito: `false` |

## Metodi del modulo multimediale {#media-module-methods}

I metodi del modulo multimediale sono utilizzati per monitorare manualmente gli eventi del lettore e per tenere traccia di metriche aggiuntive che non fanno parte dei rapporti video standard.

Se utilizzi `Media.autoTrack` e non esegui il tracciamento di metriche aggiuntive, non devi chiamare direttamente nessuno di questi metodi. Tutti gli argomenti sono obbligatori, a meno che non siano specificati come facoltativi.

| Metodo    | Descrizione |
| --- | --- |
| `Media.open` | **Sintassi:** <br/><br/> `s.Media.open(mediaName, mediaLength, mediaPlayerName)` <br/><br/>Prepara il modulo multimediale a raccogliere i dati di tracciamento video. Questo metodo accetta i seguenti parametri: <ul><li> **** mediaName: (Obbligatorio) Il nome del video come desiderate venga visualizzato nei rapporti video. </li><li>  **** mediaLength: (Obbligatorio) Lunghezza del video in secondi.  </li><li> **** mediaPlayerName: (Obbligatorio) Il nome del lettore multimediale utilizzato per visualizzare il video, così come si desidera venga visualizzato nei rapporti video. </li></ul> |
| `Media.openAd` | **Sintassi:** <br/><br/> `s.Media.openAd(name, length, playerName, parentName,`<br/>   `parentPod, parentPodPosition, CPM)` <br/><br/>Prepara il modulo multimediale a raccogliere i dati di tracciamento annunci. Questo metodo accetta i seguenti parametri: <ul> <li> **** name: (Obbligatorio) Il nome o l'ID dell'annuncio.  </li> <li> **** lunghezza: (Obbligatorio) Lunghezza dell’annuncio.  </li> <li> **** playerName: (Obbligatorio) Il nome del lettore multimediale utilizzato per visualizzare l’annuncio.  </li> <li> **** parentName: Nome o ID del contenuto principale in cui l’annuncio è incorporato.  </li> <li> **** parentPod: Posizione nel contenuto principale in cui è stato riprodotto l’annuncio.  </li> <li> **** parentPodPosition: Posizione all’interno del contenitore in cui viene riprodotto l’annuncio.  </li> <li> **** CPM: CPM o CPM crittografato (con il prefisso "~") che si applica a questa riproduzione.  </li> </ul> |
| `Media.click` | **Sintassi:** <br/><br/> `s.Media.click(name, offset)` Tieni <br/><br/>traccia quando si fa clic su un annuncio in un video. Questo metodo accetta i seguenti parametri: <ul> <li> **** name: Nome dell’annuncio. Deve corrispondere al nome utilizzato in Media.openAd.  </li> <li> **** offset: L'offset nell'annuncio quando si è verificato il clic.  </li> </ul> |
| `Media.close` | **Sintassi:** <br/><br/> `s.Media.close(mediaName)` Termina <br/><br/>la raccolta dei dati video e invia informazioni ai server di raccolta dati Adobe. Chiama questo metodo alla fine del video. Questo metodo utilizza il seguente parametro: <br/><br/> **** mediaName: Nome del video. Deve corrispondere al nome utilizzato in `Media.open`. |
| `Media.complete` | **Sintassi:** <br/><br/> `s.Media.complete(name, offset)` <br/><br/>Questo metodo tiene traccia manuale di un evento completo. Questo metodo viene utilizzato quando è necessario attivare eventi utilizzando una logica speciale che non può essere gestita tramite `Media.completeByCloseOffset`. <br/><br/>Ad esempio, se state misurando un flusso live che non ha una fine definita, potete attivare un completamento dopo che un utente visualizza un flusso live per X secondi. È possibile misurare un completamento utilizzando un calcolo percentuale basato sulla lunghezza e sul tipo di contenuto. Questo metodo accetta i seguenti parametri: <ul> <li> **** mediaName: Nome del video. Deve corrispondere al nome utilizzato in Media.open.  </li> <li> **** mediaOffset: Il numero di secondi trascorsi nel video durante l’invio dell’evento completo. Specificate l'offset in base al video che inizia con il secondo zero. <br/><br/>Se il lettore multimediale tiene traccia dei millisecondi, assicurarsi che il valore sia convertito in secondi prima di chiamare Media.complete.  </li> </ul> Se prevedete di chiamare il completamento manuale, impostate <br/><br/> `s.Media.completeByCloseOffset = false`. |
| `Media.play` | **Sintassi:** <br/><br/> `s.Media.play(name, offset, segmentNum, segment, segmentLength)` Chiama <br/><br/>questo metodo ogni volta che inizia la riproduzione di un video. Quando si utilizza la misurazione video manuale, è possibile fornire i dati del segmento corrente durante l’invio dei dati di misurazione video.  <br/><br/>Se il giocatore passa da un segmento all'altro, per qualsiasi motivo, devi chiamare `Media.stop``Media.play`. <br/><br/>Questo metodo accetta i seguenti parametri: <br/><br/> **** mediaName: Nome del video. Deve corrispondere al nome utilizzato in Media.open.  <br/><br/> **** mediaOffset: Il numero di secondi dall'inizio della riproduzione del video. Specificate l'offset in base al video che inizia con il secondo zero. Se il lettore multimediale tiene traccia dei millisecondi, assicurarsi che il valore sia convertito in secondi prima di chiamare Media.play.  <br/><br/> **** segmentNum: (Facoltativo) Il numero del segmento corrente, utilizzato dai rapporti di marketing per ordinare la visualizzazione dei segmenti nei rapporti. Il parametro segmentNum deve essere maggiore di zero.  <br/><br/> **** segmento: (Facoltativo) Il nome del segmento corrente.  <br/><br/> **** segmentLength: (Facoltativo) <br/><br/>La lunghezza del segmento corrente, in secondi.  <br/><br/>Ad esempio: <br/><br/> `s.Media.play("My Video", 1800, 2,"Second Quarter", 1800)` <br/><br/> `s.Media.play("My Video", 0, 1,"Preroll", 30)` |
| `Media.stop` | **Sintassi:** <br/><br/> `s.Media.stop(mediaName, mediaOffset)` Tiene <br/><br/>traccia di un evento stop (stop, pause, ecc.) per il video specificato. Questo metodo accetta i seguenti parametri: <ul> <li> **** mediaName: Nome del video. Deve corrispondere al nome utilizzato in `Media.open`.  </li> <li> **** mediaOffset: Il numero di secondi trascorsi nel video per cui si verifica l'evento stop o pause. Specificate l'offset in base al video che inizia con il secondo zero.  </li> </ul> |
| `Media.monitor` | **Sintassi:** <br/><br/> `s.Media.monitor(s, media)` <br/><br/> **** Sintassi Silverlight: <br/><br/> `s.Media.monitor =` <br/>`new AppMeasurement_Media_Monitor(myMediaMonitor);` <br/><br/>Il monitor di supporto per app Silverlight implementa il pattern di progettazione di delegate Objective-C. Il metodo `myMediaMonitor` class accetta i `s` parametri e `media` . <br/><br/>Usate questo metodo per inviare metriche video aggiuntive. Potete impostare ulteriori variabili (Prop, eVar, Eventi) e inviarle utilizzando `Media.track` lo stato corrente del video durante la riproduzione. <br/><br/>Consultate [Misurazione di metriche aggiuntive tramite Media.monitor.](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_mediamonitor.html) <br/><br/>Questo metodo accetta i seguenti parametri: <br/><br/>  **** s: L' `AppMeasurement` istanza (o oggetto JavaScript `s` ). <br/><br/> **** media: Un oggetto con membri che forniscono lo stato del video. Tali membri includono:  <ul><li> `media.name:` Nome del video. Deve corrispondere al nome utilizzato in `Media.open`; </li><li> `media.length:` la lunghezza del video in secondi fornita nella chiamata a `Media.open`; </li><li> `media.playerName:` il nome del lettore multimediale fornito nella chiamata a `Media.open`; </li><li> `media.openTime:` Un oggetto NSDate contenente dati su quando `Media.open` è stato chiamato; </li><li> `media.offset:` L'offset corrente, in secondi, (punto effettivo nel video) nel video. L’offset inizia a zero (il primo secondo del video è il secondo 0); </li><li> `media.percent:` Percentuale corrente del video riprodotto, in base alla lunghezza del video e all’offset corrente.;  </li><li> `media.timePlayed:` il numero totale di secondi riprodotti finora;  </li><li> `media.eventFirstTime:` Indica se è stata la prima volta che l’evento multimediale è stato chiamato per questo video; </li><li> `media.mediaEvent:` Una stringa contenente il nome dell'evento che ha causato la chiamata al monitor. </li></ul> |
|  | `media.mediaEvent` events: <ul><li> `OPEN:` Quando la riproduzione è osservata per la prima volta attraverso `Media.autoTrack` o una chiamata a `Media.play`; </li><li> `CLOSE:` Quando la riproduzione termina al completamento del video attraverso `Media.autoTrack` o a una chiamata a `Media.close`;</li><li> `PLAY:` quando la riproduzione riprende dopo essere stata messa in pausa o aver fatto scorrere `Media.autoTrack` o aver effettuato una seconda chiamata a `Media.play`;</li><li> `STOP:` Quando la riproduzione si arresta a causa di una pausa dell’inizio dello scorrimento `Media.autoTrack` o di una chiamata a `Media.stop`;</li><li> `MONITOR:` Quando il monitoraggio automatico controlla lo stato del video durante la riproduzione (ogni secondo);</li><li> `SECONDS:` al secondo intervallo definito dalla `Media.trackSeconds` variabile;</li><li> `MILESTONE:` alle tappe definite dalla `Media.trackMilestones` variabile; </li></ul> |
| `Media.track` | **Sintassi:** <br/><br/> `s.Media.track(mediaName)` Invia <br/><br/>immediatamente lo stato del video corrente, insieme a qualsiasi `Media.trackVars` e Media.trackEvents definito. Questo metodo viene utilizzato all’interno `Media.monitor`. <br/><br/>Consultate [Misurazione di metriche aggiuntive tramite Media.monitor.](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_mediamonitor.html) Chiamare <br/><br/>Call `Media.open` e `Media.play` il video prima di chiamare questo metodo. Questo metodo utilizza il seguente parametro: <ul> <li> **mediaName**: Nome del video. Deve corrispondere al nome utilizzato in `Media.open`.</li> </ul> Questo metodo è l’unico modo per inviare variabili aggiuntive durante la riproduzione del video. Ripristina a zero l’intervallo di secondi e la percentuale dei contatori delle attività cardine per evitare più hit di tracciamento. |


## Track video player events {#track-video-player-events}

È possibile tenere traccia dei lettori multimediali creando funzioni collegate ai gestori di eventi del lettore video. Questo consente di chiamare `Media.open`, `Media.play`, `Media.stop`e `Media.close` nei momenti opportuni. Ad esempio:

* **** Carica: Chiama `Media.open` e `Media.play`
* **** Pausa: Chiama `Media.stop`. Ad esempio, se un utente mette in pausa un video dopo 15 secondi, chiama `s.Media.stop("Video1", 15)`
* **** Buffer: Chiamata `Media.stop` durante il buffer video. Chiama `Media.play` quando la riproduzione riprende.
* **** Riprendi: Chiama `Media.play`. Ad esempio, quando un utente riprende un video dopo aver inizialmente riprodotto 15 secondi del video, chiamate `s.Media.play("Video1", 15)`.
* **** Cursore (cursore): Quando l’utente trascina il cursore del video, chiama `Media.stop`. Quando l’utente rilascia il cursore del video, chiama `Media.play`.
* **** Fine: Chiama `Media.stop`, allora `Media.close`. Ad esempio, alla fine di un video di 100 secondi, chiamate `s.Media.stop("Video1", 100)`, quindi `s.Media.close("Video1")`.

A tal fine, è possibile definire quattro funzioni personalizzate che è possibile chiamare dai gestori eventi del lettore multimediale. I vari parametri passati in `Media.open`, `Media.play`, `Media.stop`e `Media.close` provengono dal lettore. Lo pseudocodice seguente illustra come eseguire questa operazione:

```javascript
/* Call on video load */ 
function startMovie() { 
    s.Media.open(mediaName, mediaLength, mediaPlayerName); 
    playMovie(); 
} 
 
/* Call on video resume from pause and slider release */ 
function playMovie() { 
    s.Media.play(mediaName, 
                 mediaOffset,  
                 segmentNum,  
                 segment,  
                 segmentLength); 
} 
/* Call on video pause and slider grab */ 
function stopMovie() { 
    s.Media.stop(mediaName, mediaOffset); 
} 
 
/* Call on video end */ 
/* Measuring Video for Developers 43 */ 
function endMovie() { 
    stopMovie(); 
    s.Media.close(mediaName); 
} 
```

## Autotrack JavaScript {#javascript-autotrack}

Il modulo multimediale JavaScript identifica tutti `<embed>` i tag o `<object>` i tag presenti nella pagina HTML. quindi cerca i dati di ciascun tag per determinare quale lettore multimediale viene utilizzato, se presente. Se il lettore è Windows Media Player, Quicktime o Real Player, `autoTrack` può essere utilizzato, anche se `autoTrack` per Windows Media Player funziona solo con Internet Explorer. Per supportare tutti gli altri browser, è necessario tenere traccia manuale di Windows Media Player.

L' `classid` attributo deve essere impostato sull'oggetto da monitorare. Il modulo `classid` deve esporre i gestori di eventi utilizzati dal modulo multimediale per tracciare automaticamente il video.

```javascript
s.Media.autoTrack = true
```

## Codice di esempio JavaScript {#javascript-sample-code}

```javascript
// Sample implementation 
s.usePlugins=true 
function s_doPlugins(s) { 
    /* Add manual calls to modules and plugins here */ 
} 
 
s.doPlugins=s_doPlugins 
 
/*********Media Module Calls**************/ 
s.loadModule("Media") 
 
/*Configure Media Module Functions */ 
s.Media.autoTrack= true; 
s.Media.trackVars="events, prop2, eVar1, eVar2, eVar3"; 
s.Media.trackEvents="event1, event2, event3, event4, event5, event6, event7" 
s.Media.trackMilestones="25, 50, 75"; 
s.Media.playerName="My Media Player"; 
s.Media.segmentByMilestones = true; 
s.Media.trackUsingContextData = true; 
s.Media.contextDataMapping = { 
    "a.media.name":"eVar2, prop2", 
    "a.media.segment":"eVar3", 
    "a.contentType":"eVar1", 
    "a.media.timePlayed":"event3", 
    "a.media.view":"event1", 
    "a.media.segmentView":"event2", 
    "a.media.complete":"event7", 
    "a.media.milestones":{ 
        25:"event4", 
        50:"event5", 
        75:"event6" 
    } 
} 
 
s.Media.monitor = function (s, media) { } //If Needed

/* Turn on and configure debugging here */ 
s.debugTracking = true; 
s.trackLocal = true; 
 
/* WARNING: Changing any of the below variables will cause drastic changes to how your visitor 
data is collected. Changes should only be made when instructed to do so by your account 
manager.*/ 
s.visitorNamespace = "yourNamespace"; 
s.trackingServer="metrics.mysite.com" //Use only if using first party cookies 
s.trackingServerSecure="smetrics.mysite.com" // Use only if using first party cookies in  
                                             // conjunction with SSL 
s.dc = '122'; 
 
/************************** PLUGINS SECTION *************************/ 
/* Insert any plugins code you want to use here. */ 
 
/****************************** MODULES *****************************/ 
/* Insert the media module tracking code here. */ 
```

