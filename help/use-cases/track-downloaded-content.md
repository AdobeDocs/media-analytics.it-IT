---
title: Come tenere traccia dei contenuti scaricati offline in Adobe Streaming Media
description: Scopri come utilizzare la funzione Contenuto scaricato per tenere traccia del consumo di contenuti multimediali quando un utente è offline.
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
exl-id: 82d3e5d7-4f88-425c-8bdb-e9101fc1db92
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: cdc5ea361829c749dfbb457288ac5ba51a530961
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 100%

---

# Tracciare i contenuti scaricati {#track-downloaded-content}

## Panoramica  {#overview}

La funzione Contenuto scaricato consente di tenere traccia del consumo di contenuti multimediali mentre un utente è offline. Ad esempio, un utente scarica e installa un’app su un dispositivo mobile, quindi utilizza l’app per scaricare contenuti nell’archiviazione locale sul dispositivo. Per tenere traccia dei dati scaricati, Adobe ha sviluppato la funzione Contenuto scaricato. Con questa funzione, quando l’utente riproduce il contenuto dallo storage di un dispositivo, i dati di tracciamento vengono memorizzati sul dispositivo indipendentemente dalla connettività del dispositivo. Quando l’utente termina la sessione di riproduzione e il dispositivo torna online, le informazioni di tracciamento memorizzate vengono inviate al back-end API di Media Collection all’interno di un singolo payload. Le informazioni di tracciamento memorizzate vengono quindi elaborate e riportate come di consueto nell’API Media Collection.

Contrasto tra i due approcci:

* Online

   Con questo approccio in tempo reale, il lettore multimediale invia i dati di tracciamento per ogni evento del lettore e invia ping di rete ogni dieci secondi (ogni secondo per gli annunci), uno per uno al back-end.

* Offline (funzionalità Contenuto scaricato)

   Con questo approccio di elaborazione batch, è necessario generare gli stessi eventi di sessione, ma vengono memorizzati sul dispositivo fino a quando non vengono inviati al back-end come una singola sessione (vedi l’esempio di seguito).

Ogni approccio presenta vantaggi e svantaggi:
* Lo scenario online segue in tempo reale; questo richiede un controllo della connettività prima di ogni chiamata di rete.
* Lo scenario offline (funzionalità Contenuto scaricato) richiede un solo controllo della connettività di rete, ma richiede anche un maggiore spazio di memoria sul dispositivo.

## Implementazione {#implementation}

### Piattaforme supportate

Il tracciamento dei contenuti è supportato sui dispositivi mobili iOS e Android.

### Schemi evento

La funzione Contenuto scaricato è la versione offline dell’API di raccolta multimediale online (standard), pertanto i dati dell’evento che il lettore batch e invia al back-end devono utilizzare gli stessi schemi dell’evento utilizzati quando effettui chiamate online. Per informazioni su questi schemi, vedi:
* [Panoramica;](/help/implementation/media-collection-api/mc-api-overview.md)
* [Convalida delle richieste evento ](/help/implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordine degli eventi

* Il primo evento nel payload batch deve essere `sessionStart` come di consueto con l’API Media Collection.
* **Devi includere`media.downloaded: true`** nei parametri di metadati standard (chiave `params`) sull’evento `sessionStart` per indicare al back-end che stai inviando il contenuto scaricato. Se questo parametro non è presente o è impostato su false quando invii i dati scaricati, l’API restituirà un codice di risposta 400 (Richiesta errata). Questo parametro distingue il contenuto scaricato dal vivo dal back-end. Se `media.downloaded: true` è impostato su una sessione in tempo reale, ne conseguirà una risposta 400 dell’API.
* È responsabilità dell’implementazione memorizzare correttamente gli eventi del lettore in base all’ordine del loro aspetto.

### Codici di risposta

* 201 - Creato: richiesta riuscita; i dati sono validi e la sessione è stata creata e verrà elaborata.
* 400 - Richiesta Errata; convalida dello schema non riuscita. Tutti i dati vengono scartati. Nessun dato di sessione verrà elaborato.

## Integrazione con Adobe Analytics {#integration-with-adobe-analtyics}

Quando si calcolano le chiamate di avvio/chiusura di Analytics per lo scenario di contenuto scaricato, il back-end imposta un campo Analytics aggiuntivo denominato `ts.`. Si tratta di marche temporali per il primo e l’ultimo evento ricevuto (inizio e completamento). Questo meccanismo consente di posizionare una sessione multimediale completata nel momento corretto (ovvero, anche se l’utente non torna online per diversi giorni, la sessione multimediale viene segnalata come se si fosse verificata nel momento in cui il contenuto è stato effettivamente visualizzato). Abilita questo meccanismo sul lato Adobe Analytics creando una _suite di rapporti opzionale con marca temporale._ Per abilitare una suite di rapporti opzionale con marca temporale, vedi [Marca temporale opzionale.](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/timestamp-optional.html?lang=it)

## Confronto delle sessioni di esempio {#sample-session-comparison}

### Contenuto online

```
POST /api/v1/sessions HTTP/1.1

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

### Contenuto scaricato

```
POST /api/v1/downloaded HTTP/1.1

[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },  
    params:{...},
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

### Avviso elementi obsoleti

>[!IMPORTANT]
>
>In precedenza era possibile inviare anche il contenuto scaricato a API `/api/v1/sessions`. Questo modo di tenere traccia del contenuto scaricato è **obsoleto** e verrà **rimosso** in futuro.


L’API `/api/v1/sessions` accetterà solo gli eventi di inizializzazione della sessione.
Quando si utilizza la nuova API, il flag `media.downloaded` precedentemente obbligatorio non è più necessario.
Si consiglia vivamente di utilizzare l’API `/api/v1/downloaded` per le nuove implementazioni di contenuti scaricati, nonché per l’aggiornamento delle implementazioni esistenti che si basano sulla vecchia API.


```
POST /api/v1/sessions HTTP/1.1
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },
    params:{
        "media.downloaded": true,
        ...
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

## Riferimento API per il tracciamento dei contenuti multimediali

Per informazioni su come configurare il contenuto scaricato, consulta il [Riferimento API per il tracciamento dei contenuti multimediali](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/).
