---
title: Tenere traccia del contenuto scaricato
description: null
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: be68a7abf7d5fd4cc725b040583801f2308ab066
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---


# Track downloaded content{#track-downloaded-content}

## Panoramica {#overview}

La funzione Contenuto scaricato consente di tenere traccia dell’utilizzo dei contenuti multimediali mentre un utente è offline. Ad esempio, un utente scarica e installa un&#39;app su un dispositivo mobile, quindi utilizza l&#39;app per scaricare contenuto nello spazio di archiviazione locale sul dispositivo. Per tenere traccia dei dati scaricati, Adobe ha sviluppato la funzione Contenuto scaricato. Con questa funzione, quando l&#39;utente riproduce il contenuto dallo storage di un dispositivo, i dati di tracciamento vengono memorizzati sul dispositivo, indipendentemente dalla connettività del dispositivo. Al termine della sessione di riproduzione e quando il dispositivo torna online, le informazioni di tracciamento memorizzate vengono inviate al back-end API di Media Collection all’interno di un singolo payload. Le informazioni di tracciamento memorizzate vengono quindi elaborate e riportate come di consueto nell’API di Media Collection.

Contrasto tra i due approcci:

* Online

   Con questo approccio in tempo reale, il lettore multimediale invia i dati di tracciamento per ogni evento del lettore e invia i ping di rete ogni dieci secondi (ogni secondo per gli annunci), uno per uno, al back-end.

* Offline (funzione Contenuto scaricato)

   Con questo approccio di elaborazione batch, è necessario generare gli stessi eventi di sessione, ma vengono memorizzati sul dispositivo fino a quando non vengono inviati al back-end come una singola sessione (vedere l&#39;esempio di seguito).

Ogni approccio presenta vantaggi e svantaggi:
* Lo scenario online segue in tempo reale; questo richiede un controllo della connettività prima di ogni chiamata di rete.
* Lo scenario offline (funzione Contenuto scaricato) richiede un solo controllo della connettività di rete, ma richiede anche un maggiore spazio di memoria sul dispositivo.

## Implementazione {#implementation}

### Piattaforme supportate

Il tracciamento del contenuto è supportato sui dispositivi mobili iOS e Android.

### Schemi evento

La funzione Contenuto scaricato è la versione offline dell&#39;API Media Collection (standard) online, pertanto i dati dell&#39;evento che il lettore batch e invia al back-end devono utilizzare gli stessi schemi dell&#39;evento utilizzati per effettuare chiamate online. Per informazioni su questi schemi, vedete:
* [Panoramica;](/help/media-collection-api/mc-api-overview.md)
* [Convalida delle richieste di eventi](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordine degli eventi

* Il primo evento nel payload batch deve essere `sessionStart` come di consueto con l&#39;API Media Collection.
* **Dovete includere`media.downloaded: true`**nei parametri di metadati standard (`params`chiave) dell&#39;`sessionStart`evento per indicare al back-end che state inviando il contenuto scaricato. Se questo parametro non è presente o è impostato su false quando inviate i dati scaricati, l&#39;API restituirà un codice di risposta 400 (Richiesta non valida). Questo parametro distingue il contenuto scaricato da quello live verso il back-end. Se`media.downloaded: true`è impostata su una sessione in diretta, si verificherà anche una risposta 400 da parte dell&#39;API.
* È responsabilità dell&#39;implementazione memorizzare correttamente gli eventi del lettore nell&#39;ordine del loro aspetto.

### Codici di risposta

* 201 - Creato: Richiesta Di Successo; i dati sono validi e la sessione è stata creata e verrà elaborata.
* 400 - Richiesta Cattiva; convalida dello schema non riuscita. Tutti i dati vengono scartati, non verranno elaborati dati delle sessioni.

## Integrazione con Adobe Analytics {#integration-with-adobe-analtyics}

Quando si calcolano le chiamate di avvio/chiusura  Analytics per lo scenario di contenuto scaricato, il back-end imposta un  campo Analytics aggiuntivo denominato `ts.` Queste sono marche temporali per il primo e l&#39;ultimo evento ricevuto (inizio e completamento). Questo meccanismo consente di posizionare una sessione multimediale completata nel momento giusto (anche se l’utente non torna online per diversi giorni, la sessione multimediale si riferisce al momento in cui il contenuto è stato effettivamente visualizzato). È necessario attivare questo meccanismo sul lato Adobe  Analytics creando una suite di rapporti opzionale per _marca temporale._ Per abilitare una suite di rapporti opzionale per marca temporale, vedi [Marca temporale opzionale.](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## Esempio di confronto delle sessioni {#sample-session-comparison}

```
[url]/api/v1/sessions
```

### Contenuto online

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

### Contenuto scaricato

```
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478},  
    params:{
        "media.downloaded": true
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

## Riferimento API Media Tracker

Per informazioni su come configurare il contenuto scaricato, consultate il riferimento API [Media tracker](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#media-api-reference).
