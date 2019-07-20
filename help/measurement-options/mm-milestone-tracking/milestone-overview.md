---
seo-title: Panoramica milestone (Pietra miliare)
title: Panoramica milestone (Pietra miliare)
uuid: 2 f 9 ec 6 bb -8860-4863-98 bc -5 cffb 356 ccc 5
translation-type: tm+mt
source-git-commit: bb5478b0934e0a3bf27def86ff70c7f92af67e6a

---


# Milestone overview{#milestone-overview}

>[!CAUTION]
>
>Questa opzione di misurazione è stata rimossa.

[Documentazione milestone precedente](milestone_analytics_video.pdf)

## Configurazione {#section_rzx_j1z_cfb}

### Milestone Video Configuration (Configurazione video milestone)

To track video, designate a set of *Custom Conversion Variables* (eVars) and *Custom Events* for use in tracking and reporting. One *Custom Insight* variable ( `s.prop` ) is also used for pathing.

Le variabili selezionate per ogni metrica vengono aggiunte alla pagina di configurazione video. Questo consente al sistema di generare e formattare automaticamente i rapporti video standard. The *video name* eVar and the *video views* counter are both required. Altre variabili sono facoltative, ma consigliate per la misurazione completa. Dopo aver abilitato il tracciamento video, potete visualizzare i rapporti generati dai dati video che avete segnalato mediante il tracciamento video.

Puoi anche tenere traccia di qualsiasi numero di metriche aggiuntive per i video. Ad esempio, se utilizzate più lettori video sul sito, potete comporre una evar con il nome del lettore. Alcune delle variabili selezionate possono essere utilizzate anche in altre aree del sito. For example, if used across your site, the *content type* variable can let you measure what percentage of your page views are coming from video, and let you relate conversion events to video.

### Configurazione dei rapporti milestone (Pietra miliare)

To set-up video reporting for a Milestone implementation, go to **[!UICONTROL Admin > Report Suite Manager].** Seleziona la suite di rapporti, quindi scegli **[!UICONTROL Video Management > Video Reporting]:**

![](assets/0clip_image002_1537416456.png){width = "248"}

Nella prima schermata, solo i Video Core funzioneranno con i dati milestone. Select **[!UICONTROL Video Core]** and click **[!UICONTROL Save].**

![](assets/video-core-check.png)

On the next screen, select **[!UICONTROL Use Custom Variables].**

![](assets/0clip_image006_-1561510960.png){width = "470"}

Nella schermata finale, seleziona le due evar e tre eventi da usare con la misurazione video:

![](assets/0clip_image008_-92166399.png)

## Video variable reference {#section_emg_c1z_cfb}

La tabella seguente contiene ulteriori dettagli sulle variabili di commerce e gli eventi personalizzati per i video:

| Metrica video | Tipo di variabile | Descrizione |
| --- | --- | --- |
| Contenuto | eVar <br/>Default expiration: Visit | (Obbligatorio) Raccoglie il nome del video, come specificato nell'implementazione. |
| Tipo di contenuto | eVar <br/>Default expiration: Page view | Raccoglie dati relativi al tipo di contenuto visualizzato da un visitatore. Hits sent by video measurement are assigned a content type of `video.` <br/>This variable does not need to be reserved exclusively for video tracking. L'utilizzo di altri tipi di contenuto per rapporti con questa stessa variabile consente di analizzare la distribuzione dei visitatori tra i diversi tipi di contenuto. For example, you could tag other content types using values such as `article` or `product page` using this variable. <br/>Dal punto di vista della misurazione video, *il tipo di contenuto* consente di identificare i visitatori del video e quindi calcolare i tassi di conversione video. |
| Tempo contenuto trascorso | Event <br/>Type: Counter | Conta il tempo, in secondi, trascorso a guardare un video dall'ultimo processo di raccolta di dati (richiesta immagine). |
| Video avviato | Event <br/>Type: Counter | Indica che un visitatore ha visualizzato una parte di un video. Tuttavia, non fornisce informazioni sulla parte specifica visualizzata, né sulla durata della visualizzazione. |
| Completamenti video | Event <br/>Type: Counter | Indica che un utente ha visualizzato un video completo. Per impostazione predefinita, l'evento completo è misurato 1 secondo prima della fine del video.  <br/>Durante l'implementazione, puoi specificare quanti secondi dalla fine del video considerare come una visualizzazione dell'intero video. Per i video in diretta e altri flussi che non hanno una fine definita, puoi specificare un punto personalizzato per misurare il completamento. Ad esempio, dopo un tempo di visualizzazione specifico. |

## Media Module variables {#section_ts5_11z_cfb}

Le seguenti variabili consentono di configurare la misurazione video. È necessario definire i valori per le variabili nella tabella Variabili richieste. Inoltre, per tenere traccia degli eventi nel lettore video, dovete abilitare autotrack (per lettori supportati) o implementare il tracciamento personalizzato degli eventi del lettore utilizzando i metodi di apertura, riproduzione, interruzione e chiusura.

| Variabile    | Descrizione |
| --- | --- |
| `Media.trackUsingContextData` | **Sintassi:** <br/><br/> `s.Media.trackUsingContextData = true;`<br/>Questa opzione consente il tracciamento video integrato. When set to true, the media module generates context data for media tracking, instead of the legacy `pev3`. <br/>Utilizza `Media.contextDataMapping` per mappare i dati contestuali alle evar ed eventi selezionati.<br/>Valore predefinito: `false` |
| `Media.contextDataMapping` | **Sintassi:** <br/><br/> `s.Media.contextDataMapping = {`<br/>      `"a.media.name":"eVar2, prop2",` <br/>     `"a.media.segment":"eVar3",` <br/>     `"a.contentType":"eVar1",` <br/>     `"a.media.timePlayed":"event3",` <br/>     `"a.media.view":"event1",` <br/>     `"a.media.segmentView":"event2",` <br/>     `"a.media.complete":"event7",` <br/>     `"a.media.milestones":{` <br/>         `25:"event4",` <br/>         `50:"event5",` <br/>         `75:"event6"` <br/>     ` }` <br/> `};`<br/><br/>Un oggetto che definisce mappatura variabile alle evar ed Eventi che desiderate utilizzare per la misurazione video. The object must map the following fields: <br/><br/> **a. media. name:** (Obbligatorio) Compila le variabili con il nome del video. Provide the eVar that you selected to store the video name, and the Custom Insight Video variable ( `s.prop` ) you want to use for video pathing. Provide the values in a comma-separated list. <br/><br/> **a. media. segment:** (Facoltativo) La evar che desideri memorizzare nel nome del segmento multimediale. a. contenttype: (Facoltativo) La evar che desideri memorizzare nel valore del video, che contiene il tracciamento visitatore e visita abilitato per generare la visita video e il reporting dei visitatori. The variable you select is likely already used to store data such as article slide show or product page <br/><br/> **a. media. view:** (Obbligatorio) L'evento che intendete conteggiare visualizzando le visualizzazioni dei contenuti multimediali. <br/><br/> **a. media. segmentview:** (Facoltativo) L'evento di cui desiderate conteggiare le visualizzazioni dei segmenti. <br/><br/> **a. media. complete:** (Facoltativo) L'evento a cui desiderate conteggiare le visualizzazioni complete. <br/><br/> **a. media. timeplayed:** (Facoltativo, fortemente consigliato) L'evento numerico che si desidera memorizzare per memorizzare il numero di secondi trascorsi. <br/><br/> **a. media. milestones:** (Facoltativo) Un oggetto associato a elementi. Media. trackmilestones per il contatore Eventi. Media.segmentByMilestones should be set to true if you define milestones. <br/><br/> **Tracciamento** annunci per tracciare annunci, sono disponibili le seguenti variabili di dati di contesto: <br/> **a.media.ad.na me:** (Obbligatorio) Compila le variabili con il nome dell'annuncio. Provide the eVar that you selected to store the ad name, and the Custom Insight Video variable ( `s.prop` ) you want to use for pathing. Provide the values in a comma-separated list. <br/><br/> **a.media.ad.po d:** La posizione nel contenuto principale in cui è stato riprodotto l'annuncio. <br/><br/> **a.media.ad.po Dposition:** Posizione all'interno del contenitore in cui viene riprodotto l'annuncio. <br/><br/> **a.media.ad.CP M:** CPM o CPM cifrato (prefisso a " ~") che si applica a questa riproduzione. <br/><br/> **a.media.ad.vi ew:** Funziona come `a.media.view`<br/><br/> **a.media.ad.cl:** Conteggio del numero di clic per l'annuncio (`Media.click` chiamate) <br/><br/> **a.media.ad.ti Meplay:** Funziona come `a.media.timePlayed`<br/><br/> **a.media.ad.com:** Funziona come `a.media.complete` a.media.ad.se gment: Funziona come `a.media.segment`<br/><br/> **a.media.ad.se Gmentview:** Funziona come `a.media.segmentView`<br/><br/> **a.media.ad.mi lestones:** Funziona come `a.media.milestones`<br/><br/> **a.media.ad.of Fsetmilestones:** Funziona come `a.media.offsetMilestones` |
| `Media.trackVars` | **Sintassi:** <br/><br/> `s.Media.trackVars =` <br/> `"events,``prop2,``eVar1,``eVar2,``eVar3";`<br/><br/>Elenco separato da virgole di tutte le variabili impostate nel codice di tracciamento video. |
| `Media.trackEvents` | **Sintassi:** <br/><br/> `s.Media.trackEvents =` <br/> `"event1,``event2,``event3,``event4,``event5,``event6,``event7"`<br/><br/>Elenco separato da virgole di tutti gli eventi impostati nel codice di tracciamento video. |

## Optional variables {#section_ufg_zzy_cfb}

|  Variabile    | Descrizione |
| --- | --- |
| `Media.autoTrack` | **Sintassi:** <br/><br/> `s.Media.autoTrack = true`<br/><br/>Abilita il tracciamento automatico per i lettori supportati. I lettori supportati sono i seguenti: <ul> <li> Open Source Media Framework (OSMF) </li> <li> Flvplayback (lettori video creati dalla procedura guidata Importazione video in Flash Professional) </li> <li> Silverlight </li> <li> Mediadisplay </li> <li> Mediaplayback </li> <li> Brightcove API versions 2 &amp; 3 ( see [Brightcove](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_other_players.html)) </li> <li> Windows Media Player, Quicktime o Real Player mediante javascript </li> </ul> <br/><br/>Se non utilizzate uno dei lettori riportati sopra per tenere traccia `Media.open``Media.play``Media.stop``Media.close` degli eventi del lettore. |
| `Media.autoTrackNetStreams` | **Sintassi:** <br/><br/> `s.Media.autoTrackNetStreams = true`<br/><br/>Flash 10.3 ha introdotto nuove funzionalità al componente netstream per consentire un tracciamento video avanzato. Se utilizzate un lettore Flash netstream personalizzato, potete abilitare questa variabile per abilitare la funzionalità simile a autotrack. Questo metodo richiede che i video vengano visualizzati in Flash 10.3 o versione successiva. |
| `Media.completeByCloseOffset` | **Sintassi:** <br/><br/> <br/><br/>`s.Media.completeByCloseOffset = true`<br/><br/>Questa impostazione consente di contare una visualizzazione video completa pochi secondi prima della fine del video. <br/><br/>L'evento viene inviato in base al numero di secondi specificati `completeCloseOffsetThreshold`. Questo consente di misurare le visualizzazioni complete nei lettori video che non segnalano mai un offset pari alla lunghezza del video.<br/><br/>Per impostazione predefinita, questo valore è impostato su true e la soglia è impostata su 1 secondo. Con queste impostazioni predefinite l'evento complete viene inviato 1 secondo prima della fine del video. |
| `Media.completeCloseOffsetThreshold` | **Sintassi:** <br/><br/> `s.Media.completeCloseOffsetThreshold = 1`<br/><br/>Questa soglia consente di contare una visualizzazione video completa pochi secondi prima della fine effettiva del video. `Media.completeByCloseOffset` devono essere impostati su true per utilizzare questa soglia.<br/><br/>Il valore intero fornito determina quanto distante in secondi l'offset può essere allontanato dalla lunghezza del video alla chiusura e continua a conteggiare come completa. Questo consente di misurare le visualizzazioni complete nei lettori video che non segnalano mai un offset pari alla lunghezza del video. <br/><br/>La soglia predefinita è 1 secondo. |
| `Media.playerName` | **Sintassi:** <br/><br/> `s.Media.playerName = "Custom Player Name"`<br/><br/>Specifica il nome di un lettore video personalizzato. |
| `Media.trackSeconds` | **Sintassi:** <br/><br/> `s.Media.trackSeconds = 15`<br/><br/>Definisce l'intervallo, in secondi, per l'invio dei dati di tracciamento video ai server di raccolta dati Adobe durante la riproduzione del video. Il valore deve essere impostato con incrementi di 5 secondi. <br/><br/> Attivando `Media.trackSeconds` attiva solo gli eventi definiti. `Media.contextDataMapping` Per inviare ulteriori variabili al di fuori di quelle specificate per la misurazione video, è necessario utilizzare Media. Monitor. |
| `Media.trackMilestones` | Tracks milestones as percentage of the video length.  <br/><br/> **Sintassi:** <br/><br/> `s.Media.trackMilestones = "25, 50, 75";`<br/><br/>Definisce l'intervallo, come percentuale della lunghezza del video, per l'invio dei dati di tracciamento video ai server di raccolta dati Adobe. Specificate i milestoni come elenco separato da virgole di numeri interi. Ad esempio: 10 = 10%, 23 = 23%. <br/><br/>Poiché queste pietre miliari sono punti fissi nel video, se una visualizzazione del visitatore oltre la pietra miliare 10%, riavvolge e passa di nuovo il 10% milestone, il modulo multimediale invia i dati di tracciamento più volte. Allo stesso modo, se un visitatore avanza rapidamente oltre una pietra miliare, il modulo multimediale non invia i dati di tracciamento per quella pietra miliare. <br/><br/>Attivando `Media.trackMilestones` attiva solo gli eventi definiti. `Media.contextDataMapping` Per inviare ulteriori variabili al di fuori di quelle specificate per la misurazione video, è necessario utilizzare Media. Monitor. |
| `Media.trackOffsetMilestones` | Tracks milestones as seconds elapsed from the beginning of the video.  <br/><br/> **Sintassi:** <br/><br/> `s.Media.trackOffsetMilestones = "20, 40, 60";`<br/><br/>Definisce l'intervallo, come secondi trascorsi dall'inizio del video, per l'invio dei dati di tracciamento video ai server di raccolta dati Adobe. Specificate i milestoni come elenco separato da virgole di numeri interi. Ad esempio: 20 = 20 secondi, 40 = 40 secondi). <br/><br/>Poiché queste pietre miliari sono punti fissi nel video, se visualizzano un visitatore oltre i 20 secondi di pietra miliare, riavvolgono e trascorrono di nuovo i 20 secondi milestone, il modulo multimediale invia i dati di tracciamento più volte. Allo stesso modo, se un visitatore avanza rapidamente oltre una pietra miliare, il modulo multimediale non invia i dati di tracciamento per quella pietra miliare. <br/><br/> Attivando `Media.trackOffsetMilestones` attiva solo gli eventi definiti. `Media.contextDataMapping` Per inviare ulteriori variabili al di fuori di quelle specificate per la misurazione video, è necessario utilizzare Media. Monitor. |
| `Media.segmentByMilestones` | **Sintassi:** <br/><br/> `s.Media.segmentByMilestones = true;`<br/><br/>Genera automaticamente il nome del segmento, il numero di segmento e i dati sulla lunghezza del segmento, in base alla lunghezza del supporto e i milestoni specificati in `Media.trackMilestones`<br/><br/>Segmentazione da più linee sono l'unico modo per definire i segmenti quando usi `autoTrack`. <br/><br/>Valore predefinito: `false` |
| `Media.segmentByOffsetMilestones` | **Sintassi:** <br/><br/> `s.Media.segmentByOffsetMilestones = true;`<br/><br/>Genera automaticamente il nome del segmento, il numero di segmento e i dati sulla lunghezza del segmento, in base alla lunghezza del supporto e i milestoni specificati in `Media.trackOffsetMilestones`<br/><br/>Segmentazione da più linee sono l'unico modo per definire i segmenti quando usi `autoTrack`. <br/><br/>Valore predefinito: `false` |

## Ad Tracking variables {#section_bhv_xzy_cfb}

Queste variabili vengono utilizzate per inviare informazioni pubblicitarie insieme al metodo openad. See [VAST Video Ad Tracking.](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_ads.html)

| Variabile    | Descrizione |
| --- | --- |
| `Media.adTrackSeconds` | **Sintassi:** <br/><br/> `s.Media.adTrackSeconds = 15;`<br/><br/>Definisce l'intervallo, in secondi, per l'invio dei dati di tracciamento degli annunci video ai server di raccolta dati Adobe durante la riproduzione del video. Il valore deve essere impostato con incrementi di 5 secondi. <br/><br/> Attivando `Media.adTrackSeconds` attiva solo gli eventi definiti. `Media.contextDataMapping` To send additional variables outside of those specified for video measurement, you must use `Media.monitor`. |
| `Media.adTrackMilestones` | Tracks ad milestones as percentage of the ad length.  <br/><br/> **Sintassi:** <br/><br/> `s.Media.adTrackMilestones = "25, 50, 75";`<br/><br/>Definisce l'intervallo, come percentuale della lunghezza dell'annuncio, per inviare dati di tracciamento degli annunci ai server di raccolta dati Adobe. Specificate i milestoni come elenco separato da virgole di numeri interi. Ad esempio: 10 = 10%, 23 = 23%). <br/><br/>Poiché queste pietre miliari sono punti fissi nell'annuncio, se una visualizzazione del visitatore oltre la pietra miliare 10%, riavvolge e passa di nuovo il 10% milestone, il modulo multimediale invia i dati di tracciamento più volte. Allo stesso modo, se un visitatore avanza rapidamente oltre una pietra miliare, il modulo multimediale non invia i dati di tracciamento per quella pietra miliare. <br/><br/> Attivando `Media.adTrackMilestones` attiva solo gli eventi definiti. `Media.contextDataMapping` To send additional variables outside of those specified for video measurement, you must use `Media.monitor`. |
| `Media.adTrackOffsetMilestones` | Tracks ad milestones as seconds elapsed from the beginning of the ad.  <br/><br/> **Sintassi:** <br/><br/> `s.Media.adTrackOffsetMilestones = "20, 40, 60";`<br/><br/>Definisce l'intervallo, come secondi trascorsi dall'inizio dell'annuncio, per inviare dati di tracciamento annunci ai server di raccolta dati Adobe. Specificate i milestoni come elenco separato da virgole di numeri interi. Ad esempio: 20 = 20 secondi, 40 = 40 secondi). <br/><br/>Poiché queste pietre miliari sono punti fissi nell'annuncio, se un visitatore visualizza oltre i 20 secondi di pietra miliare, riavvolge e passa di nuovo i 20 secondi milestone (pietra miliare), il modulo multimediale invia più volte i dati di tracciamento. Allo stesso modo, se un visitatore avanza rapidamente oltre una pietra miliare, il modulo multimediale non invia i dati di tracciamento per quella pietra miliare. <br/><br/> Attivando `Media.adTrackOffsetMilestones` attiva solo gli eventi definiti. `Media.contextDataMapping` To send additional variables outside of those specified for video measurement, you must use `Media.monitor`. |
| `Media.adSegmentByMilestones` | **Sintassi:** <br/><br/> `s.Media.adSegmentByMilestones = true;`<br/><br/>Genera automaticamente il nome del segmento, il numero di segmento e i dati sulla lunghezza del segmento, in base alla lunghezza del supporto e i milestoni specificati in `Media.adTrackMilestones`<br/><br/>Segmentazione da più linee sono l'unico modo per definire i segmenti quando usi `autoTrack`. <br/><br/>Valore predefinito: `false` |
| `Media.adSegmentByOffsetMilestones` | **Sintassi:** <br/><br/> `s.Media.adSegmentByOffsetMilestones = true;`<br/><br/>Genera automaticamente il nome del segmento, il numero di segmento e i dati sulla lunghezza del segmento, in base alla lunghezza del supporto e i milestoni specificati in `Media.adTrackOffsetMilestones`<br/><br/>Segmentazione da più linee sono l'unico modo per definire i segmenti quando usi `autoTrack`. <br/><br/>Valore predefinito: `false` |

## Media Module methods {#section_xp1_wzy_cfb}

I metodi del modulo multimediale vengono utilizzati per tracciamento manuale degli eventi del lettore e per tenere traccia di metriche aggiuntive che non fanno parte dei rapporti video standard.

If you are using `Media.autoTrack` and are not tracking additional metrics, you do not need to call any of these methods directly. Tutti gli argomenti sono obbligatori, se non sono specificati come facoltativi.

| Metodo    | Descrizione |
| --- | --- |
| `Media.open` | **Sintassi:** <br/><br/> `s.Media.open(mediaName, mediaLength, mediaPlayerName)`<br/><br/>Prepara il modulo multimediale per raccogliere i dati di tracciamento video. Questo metodo utilizza i seguenti parametri: <ul><li> **Medianame:** (Obbligatorio) Il nome del video che viene visualizzato nei rapporti video. </li><li>  **Medialength:** (Obbligatorio) La lunghezza del video in secondi.  </li><li> **Mediaplayername:** (Obbligatorio) Il nome del lettore multimediale utilizzato per visualizzare il video, in modo che venga visualizzato nei rapporti video. </li></ul> |
| `Media.openAd` | **Sintassi:** <br/><br/> `s.Media.openAd(name, length, playerName, parentName,`<br/>`parentPod, parentPodPosition, CPM)`<br/><br/>Prepara il modulo multimediale per raccogliere i dati di tracciamento degli annunci. Questo metodo utilizza i seguenti parametri: <ul> <li> **name:** (Obbligatorio) Il nome o l'ID dell'annuncio.  </li> <li> **lunghezza:** (Obbligatorio) Lunghezza dell'annuncio.  </li> <li> **Playername:** (Obbligatorio) Il nome del lettore multimediale utilizzato per visualizzare l'annuncio.  </li> <li> **Parentname:** Nome o ID del contenuto principale in cui è incorporato l'annuncio.  </li> <li> **Parentpod:** La posizione nel contenuto principale in cui è stato riprodotto l'annuncio.  </li> <li> **Parentpodposition:** Posizione all'interno del contenitore in cui viene riprodotto l'annuncio.  </li> <li> **CPM:** CPM o CPM cifrato (prefisso a " ~") che si applica a questa riproduzione.  </li> </ul> |
| `Media.click` | **Sintassi:** <br/><br/> `s.Media.click(name, offset)`<br/><br/>Tracciare quando un annuncio fa clic su un video. Questo metodo utilizza i seguenti parametri: <ul> <li> **name:** Nome dell'annuncio. Deve corrispondere al nome utilizzato in Media. openad.  </li> <li> **offset:** L'offset nell'annuncio al verificarsi del clic.  </li> </ul> |
| `Media.close` | **Sintassi:** <br/><br/> `s.Media.close(mediaName)`<br/><br/>Termina la raccolta dei dati video e invia informazioni ai server di raccolta dati Adobe. Chiama questo metodo alla fine del video. This method takes the following parameter: <br/><br/> **Medianame:** Nome del video. This must match the name used in `Media.open`. |
| `Media.complete` | **Sintassi:** <br/><br/> `s.Media.complete(name, offset)`<br/><br/>Questo metodo tiene traccia manuale di un evento completo. This method is used when you need to trigger events using special logic that can't be handled using `Media.completeByCloseOffset`. <br/><br/>Ad esempio, se stai misurando un flusso live senza fine definito, potresti attivare un completo dopo che un utente visualizza un flusso live per x secondi. Puoi misurare un completamento utilizzando un calcolo percentuale in base alla lunghezza e al tipo di contenuto. Questo metodo utilizza i seguenti parametri: <ul> <li> **Medianame:** Nome del video. Deve corrispondere al nome utilizzato in Media. open.  </li> <li> **Mediaoffset:** Il numero di secondi nel video quando l'evento completo deve essere inviato. Specificate l'offset in base al video a partire da zero. <br/><br/>Se il lettore multimediale tiene traccia di millisecondi, accertatevi che il valore sia convertito in secondi prima di chiamare Media. complete.  </li> </ul> If you plan to call complete manually, set <br/><br/> `s.Media.completeByCloseOffset = false`. |
| `Media.play` | **Sintassi:** <br/><br/> `s.Media.play(name, offset, segmentNum, segment, segmentLength)`<br/><br/>Chiama questo metodo a qualsiasi momento in cui inizia un video. Quando utilizzi la misurazione video manuale, puoi fornire i dati del segmento correnti durante l'invio di dati di misurazione video. <br/><br/>Se il lettore cambia da segmento a un altro, per qualsiasi motivo occorre chiamare `Media.stop``Media.play`. <br/><br/>Questo metodo utilizza i seguenti parametri: <br/><br/> **Medianame:** Nome del video. This must match the name used in Media.open.  <br/><br/> **Mediaoffset:** Il numero di secondi per il video che inizia la riproduzione. Specificate l'offset in base al video a partire da zero. If your media player tracks using milliseconds, make sure the value is converted to seconds before you call Media.play.  <br/><br/> **Segmentnum:** (Facoltativo) Numero di segmento corrente, utilizzato dai rapporti di marketing per ordinare la visualizzazione dei segmenti nei report. The segmentNum parameter must be greater than zero.  <br/><br/> **segmento:** (Facoltativo) Il nome del segmento corrente. <br/><br/> **Segmentlength:** (Facoltativo) <br/><br/>La lunghezza del segmento corrente, in secondi. <br/><br/>Ad esempio: <br/><br/> `s.Media.play("My Video", 1800, 2,"Second Quarter", 1800)` <br/><br/> `s.Media.play("My Video", 0, 1,"Preroll", 30)` |
| `Media.stop` | **Sintassi:** <br/><br/> `s.Media.stop(mediaName, mediaOffset)`<br/><br/>Tiene traccia di un evento stop (stop, pause, ecc.) per il video specificato. Questo metodo utilizza i seguenti parametri: <ul> <li> **Medianame:** Nome del video. This must match the name used in `Media.open`.  </li> <li> **Mediaoffset:** Il numero di secondi in cui si verifica l'evento stop o pause. Specificate l'offset in base al video a partire da zero.  </li> </ul> |
| `Media.monitor` | **Sintassi:** <br/><br/> `s.Media.monitor(s, media)` <br/><br/> **Sintassi Silverlight:**<br/><br/> `s.Media.monitor =`<br/>`new AppMeasurement_Media_Monitor(myMediaMonitor);`<br/><br/>Il monitor dell'app Silverlight implementa il pattern di progettazione delegate Objective-C. The `myMediaMonitor` class method takes the `s` and `media` parameters. <br/><br/>Utilizzate questo metodo per inviare metriche video aggiuntive. You can setup additional variables (Props, eVars, Events) and send them using `Media.track` based on the current state of the video as it is playing. <br/><br/>Consultate [Misurazione di metriche aggiuntive tramite Media. monitor.](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_mediamonitor.html)<br/><br/>Questo metodo utilizza i seguenti parametri: <br/><br/>  **s:** L' `AppMeasurement` istanza (o l'oggetto javascript `s` ). <br/><br/> **media:** Un oggetto con i membri che forniscono lo stato del video. Questi membri includono:  <ul><li> `media.name:` Nome del video. This must match the name used in `Media.open`; </li><li> `media.length:` La lunghezza del video in secondi a cui corrisponde la chiamata `Media.open`; </li><li> `media.playerName:` Nome del lettore multimediale assegnato nella chiamata `Media.open`; </li><li> `media.openTime:` Un oggetto nsdate contenente dati su quando `Media.open` è stato chiamato; </li><li> `media.offset:` L'offset corrente, in secondi, (punto effettivo del video) nel video. L'offset inizia da zero (il primo secondo del video è il secondo 0); </li><li> `media.percent:` La percentuale corrente del video riprodotto, in base alla lunghezza del video e all'offset corrente.  </li><li> `media.timePlayed:` Il numero totale di secondi riprodotti finora;  </li><li> `media.eventFirstTime:` Indica se questa è la prima volta che si chiama questo evento multimediale per il video; </li><li> `media.mediaEvent:` Stringa contenente il nome dell'evento che ha provocato la chiamata al monitor. </li></ul> |
|  | `media.mediaEvent` events: <ul><li> `OPEN:` Quando la riproduzione viene osservata per la prima volta tramite `Media.autoTrack` o una chiamata a `Media.play`; </li><li> `CLOSE:` Quando la riproduzione termina al termine del video attraverso `Media.autoTrack` o a una chiamata a `Media.close`;</li><li> `PLAY:` Quando la riproduzione riprende dopo essere stata messa in pausa o scorre o `Media.autoTrack` una seconda chiamata a `Media.play`;</li><li> `STOP:` Quando la riproduzione si interrompe a causa di una pausa dell'inizio dello scorrimento o `Media.autoTrack` di una chiamata a `Media.stop`;</li><li> `MONITOR:` Quando il monitoraggio automatico controlla lo stato del video durante la riproduzione (ogni secondo);</li><li> `SECONDS:` Al secondo intervallo definito dalla `Media.trackSeconds` variabile;</li><li> `MILESTONE:` Ai milestoni definiti dalla `Media.trackMilestones` variabile; </li></ul> |
| `Media.track` | **Sintassi:** <br/><br/> `s.Media.track(mediaName)`<br/><br/>Invia immediatamente lo stato del video corrente, insieme a qualsiasi `Media.trackVars` e Media. trackevents definito. This method is used within `Media.monitor`. <br/><br/>Consultate [Misurazione di metriche aggiuntive tramite Media. monitor.](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_mediamonitor.html)<br/><br/>Chiamate `Media.open` e `Media.play` sul video prima di richiamare questo metodo. Questo metodo assume il seguente parametro: <ul> <li> **Medianame**: Nome del video. This must match the name used in `Media.open`.</li> </ul> Questo metodo è l'unico modo per inviare ulteriori variabili durante la riproduzione del video. Reimposta i contatori di intervallo di secondi e percentuali su zero per evitare più hit di tracciamento. |


## Track video player events {#section_dsg_rzy_cfb}

Potete tenere traccia dei lettori multimediali creando funzioni associate ai gestori di eventi del lettore video. This lets you call `Media.open`, `Media.play`, `Media.stop`, and `Media.close` at the appropriate times. Ad esempio:

* **Carica:** Chiamata `Media.open` e `Media.play`
* **Pausa:** Chiamata `Media.stop`. For example, if a user pauses a video after 15 seconds, call `s.Media.stop("Video1", 15)`
* **Buffer:** Chiamata `Media.stop` durante il buffer video. Call `Media.play` when playback resumes.
* **Riprendi:** Chiamata `Media.play`. For example, when a user resumes a video after initially playing 15 seconds of the video, call `s.Media.play("Video1", 15)`.
* **Scrub (cursore):** Quando l'utente trascina il cursore video, chiama `Media.stop`. When the user releases the video slider, call `Media.play`.
* **Fine:** Call `Media.stop`, then `Media.close`. For example, at the end of a 100-second video, call `s.Media.stop("Video1", 100)`, then `s.Media.close("Video1")`.

A tal fine, è possibile definire quattro funzioni personalizzate da chiamare dai gestori di eventi multimediali. The various parameters passed into `Media.open`, `Media.play`, `Media.stop`, and `Media.close` come from the player. La seguente pseudocodice illustra come procedere:

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

## JavaScript autotrack {#section_ahz_pzy_cfb}

The JavaScript media module identifies all `<embed>` or `<object>` tags in the page HTML. Quindi consente di cercare i dati in ciascun tag per determinare quale lettore multimediale, se presente, viene utilizzato. If the player is Windows Media Player, Quicktime, or Real Player, `autoTrack` can be used, though `autoTrack` for Windows media player works only with Internet Explorer. Per supportare tutti gli altri browser è necessario tenere traccia manuale di Windows Media Player.

You must have the `classid` attribute set on the object you want to track. The `classid` is required to expose the event handlers used by the Media Module to automatically track the video.

```javascript
s.Media.autoTrack = true
```

## JavaScript sample code {#section_i4g_4zy_cfb}

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

