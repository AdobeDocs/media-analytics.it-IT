---
seo-title: Tracciamento del contenuto scaricato
title: Tracciamento del contenuto scaricato
uuid: 0718689 d -9602-4 e 3 f -833 c -8297 aae 1 d 909
translation-type: tm+mt
source-git-commit: 501bbfe8b44a2a8e9b2ac2caab49b2317f9ea0f3

---


# Track downloaded content{#track-downloaded-content}

## Panoramica {#section_hcy_3pk_cfb}

L'API Contenuto scaricato permette di tenere traccia del consumo di supporti mentre un utente è offline. Ad esempio, un utente scarica e installa un'app su un dispositivo mobile. L'utente quindi scarica il contenuto utilizzando l'app nella memorizzazione locale sul dispositivo. Per tenere traccia dei dati scaricati, Adobe ha sviluppato l'API Contenuto scaricato. Con questa API, quando l'utente riproduce contenuto dall'archivio di un dispositivo, i dati di tracciamento vengono memorizzati sul dispositivo, indipendentemente dalla connettività del dispositivo. Quando l'utente conclude la sessione di riproduzione e il dispositivo è online, le informazioni di tracciamento memorizzate vengono inviate all'API di Media Collection all'interno di un singolo payload. Da qui, l'elaborazione e il reporting procede normalmente nell'API Media Collection, su cui si basa tale API.

Contrasto i due approcci:

* API di raccolta multimediale

   Con questo approccio in tempo reale, il lettore multimediale invia dati di tracciamento a ciascun evento del lettore e invia coppie di rete ogni dieci secondi (ogni secondo per gli annunci), una per una al back-end.

* API contenuto scaricato

   Con questo approccio di elaborazione batch, gli stessi eventi di sessione devono essere generati ma memorizzati sul dispositivo finché non vengono inviati al back-end come una singola sessione (vedi esempio di seguito).

Ogni approccio presenta vantaggi e svantaggi: le tracce API di Media Collection in tempo reale, ma richiede un controllo di connettività prima di ogni chiamata di rete; L'API Contenuto scaricato richiede solo un controllo di connettività di rete, ma richiede anche un ingrandimento della memoria più grande sul dispositivo.

## Implementazione {#section_jhp_jpk_cfb}

### Schemi evento

L'API Contenuto scaricato si basa sull'API Media Collection, quindi i dati dell'evento che i batch di lettore e invia richiedono che gli stessi schemi eventi siano utilizzati come nell'API di Media Collection. For information on these schemas, see: [Overview;](../media-collection-api/mc-api-overview.md) and [Validating event requests.](../media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordine degli eventi

* The first event in the batch payload must be `sessionStart`.
* You must include `media.downloaded: true` in the standard metadata parameters ( `params` key) on the `sessionStart` event. Se questo parametro non è presente o è impostato su false, l'API Contenuto scaricato restituirà un codice di risposta 400 (Richiesta non valida). In questo modo il back-end può distinguere tra contenuto scaricato e live ed elaborarlo di conseguenza. (Note that if `media.downloaded: true`is set on a live session, this will likewise result in a 400 response from the Media Collection API.)

* È responsabilità dell'implementazione memorizzare correttamente gli eventi del lettore in base al loro aspetto.

### Codici di risposta

* 201 - Creato: Richiesta di successo; i dati sono validi e la sessione è stata creata e sarà elaborata.
* 400 - Richiesta non valida; la convalida dello schema non è riuscita, tutti i dati vengono eliminati, non vengono elaborati dati delle sessioni.

## Integration with Adobe Analtyics {#section_cty_kpk_cfb}

When computing the Analytics start/close calls for the downloaded content scenario, the back-end sets an extra Analytics field called `ts`. Queste sono marche temporali per il primo e l'ultimo evento ricevuto (avvio e completato). Questo meccanismo consente di inserire una sessione media completata nel momento corretto nel tempo (ovvero, anche se l'utente non torna online per più giorni, la sessione multimediale si verifica al momento della visualizzazione del contenuto). You must enable this mechanism on the Adobe Analytics side by creating a *timestamp optional report suite*. To enable a timestamp optional report suite, see [Timestamps Optional.](https://marketing.adobe.com/resources/help/en_US/reference/timestamp-optional.html)

## Sample session comparison {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### API di raccolta multimediale

```
{ 
  eventType: "sessionStart", 
  playerTime: { 
    playhead: 0,  
    ts: 1529997923478},  
  params: { /* Standard metadata parameters as documented */ },  
  customMetadata: { /* Custom metadata parameters as documented */ },  
  qoeData: { /* QoE parameters as documented */ } 
}
```

### API contenuto scaricato

```
[{ 
    eventType: "sessionStart", 
    playerTime:{playhead: 0, ts: 1529997923478},  
    params:{
        "media.downloaded": true
    }, 
    customMetadata:{},  
    qoeData:{} 
}, 
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}}, 
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}}, 
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}}, 
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},}, 
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559} 
}]
```

