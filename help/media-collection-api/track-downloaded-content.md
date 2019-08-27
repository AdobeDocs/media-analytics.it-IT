---
seo-title: Tracciamento del contenuto scaricato
title: Tracciamento del contenuto scaricato
uuid: 0718689 d -9602-4 e 3 f -833 c -8297 aae 1 d 909
translation-type: tm+mt
source-git-commit: b9298de98eeb85c0e2ea0a456c98eac479f43b51

---


# Tracciamento del contenuto scaricato{#track-downloaded-content}

## Panoramica {#section_hcy_3pk_cfb}

La funzione Contenuto scaricato permette di tenere traccia del consumo di supporti mentre un utente è offline. Ad esempio, un utente scarica e installa un'app su un dispositivo mobile. L'utente quindi scarica il contenuto utilizzando l'app nella memorizzazione locale sul dispositivo. Per tenere traccia dei dati scaricati, Adobe ha sviluppato la funzione Contenuto scaricato. Con questa funzione, quando l'utente riproduce contenuto dall'archivio di un dispositivo, i dati di tracciamento vengono memorizzati sul dispositivo, indipendentemente dalla connettività del dispositivo. Quando l'utente conclude la sessione di riproduzione e il dispositivo torna online, le informazioni di tracciamento memorizzate vengono inviate all'API di Media Collection all'interno di un singolo payload. Da qui, l'elaborazione e il reporting procede normalmente nell'API di Media Collection.

Contrasto i due approcci:

* Online

   Con questo approccio in tempo reale, il lettore multimediale invia dati di tracciamento a ciascun evento del lettore e invia coppie di rete ogni dieci secondi (ogni secondo per gli annunci), una per una al back-end.

* Offline (funzione Contenuto scaricato)

   Con questo approccio di elaborazione batch, gli stessi eventi di sessione devono essere generati, ma sono memorizzati sul dispositivo finché non vengono inviati al back-end come una singola sessione (vedi esempio di seguito).

Ogni approccio presenta vantaggi e svantaggi:
* Le tracce dello scenario online in tempo reale; questo richiede un controllo di connettività prima di ogni chiamata di rete.
* Lo scenario offline (funzione Contenuto scaricato) richiede solo un controllo di connettività di rete, ma richiede anche un ingrandimento della memoria più grande sul dispositivo.

## Implementazione {#section_jhp_jpk_cfb}

### Schemi evento

La funzione Contenuto scaricato è semplicemente la versione offline dell'API online di Media Collection (standard), quindi i dati dell'evento che i batch di lettore e invia al back-end devono usare gli stessi schemi di eventi utilizzati per effettuare chiamate online. Per informazioni su questi schemi, vedi:
* [Panoramica;](/help/media-collection-api/mc-api-overview.md)
* [Convalida delle richieste degli eventi](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordine degli eventi

* Il primo evento nel payload batch deve essere `sessionStart` uguale al solito con l'API Media Collection.
* **Dovete includere`media.downloaded: true`** nei parametri di metadati standard (`params` chiave) `sessionStart` per indicare al back-end che state inviando contenuto scaricato. Se questo parametro non è presente o è impostato su false quando inviate dati scaricati, l'API restituirà un codice di risposta 400 (Richiesta non valida). Questo parametro distingue il contenuto scaricato e quello live al back-end. (Tenete `media.downloaded: true` presente che se viene impostato su una sessione dal vivo, ciò darà luogo a una risposta 400 dall'API.)
* È responsabilità dell'implementazione memorizzare correttamente gli eventi del lettore in base al loro aspetto.

### Codici di risposta

* 201 - Creato: Richiesta di successo; i dati sono validi e la sessione è stata creata e sarà elaborata.
* 400 - Richiesta non valida; la convalida dello schema non è riuscita, tutti i dati vengono eliminati, non vengono elaborati dati delle sessioni.

## Integrazione con Adobe Analytyics {#section_cty_kpk_cfb}

Quando si calcolano le chiamate start/close di Analytics per lo scenario di contenuto scaricato, il back-end imposta un campo Analytics aggiuntivo chiamato `ts.` , contenente le marche temporali per il primo e l'ultimo evento ricevuto (avvio e completato). Questo meccanismo consente di inserire una sessione media completata nel momento corretto nel tempo (ovvero, anche se l'utente non torna online per più giorni, la sessione multimediale si verifica al momento della visualizzazione del contenuto). Devi abilitare questo meccanismo su Adobe Analytics creando una _suite di rapporti opzionale con marca temporale._ Per abilitare una suite di rapporti opzionale con marca temporale, vedi [Marca temporale opzionale.](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## Confronto delle sessioni di esempio {#section_qnk_lpk_cfb}

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

