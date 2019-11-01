---
title: Eventi, richiesta
description: null
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Eventi, richiesta{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## Parametro URI

`sid`: L'ID sessione restituito da una richiesta di [sessioni.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## Corpo della richiesta

Il corpo della richiesta deve essere JSON e deve avere la stessa struttura del corpo della richiesta di esempio:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "{event-type}", 
    "params": {}, 
    "qoeData": {}, 
    "customMetadata": {} 
}
```

* `playerTime` (Obbligatorio)
   * `playhead` - Deve essere in secondi, ma può essere un float.
   * `ts` - marca temporale; deve essere in millisecondi.
* `eventType` (Obbligatorio)
* `params` (Facoltativo)
* `customMetadata` (Facoltativo; invio solo con `adStart` e con i tipi di `chapterStart` evento)
* `qoeData` (Facoltativo)

Per un elenco dei tipi di evento validi per questa versione, consultate Tipi di [evento e descrizioni.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Ad Tracking -**Puoi tenere traccia solo degli annunci all’interno di un`adBreak`*.
>
>In assenza di annunci `adBreakStart` e `adBreakComplete` "reggilibri" intorno agli annunci, `adStart` e `adComplete` gli eventi saranno semplicemente ignorati, e la durata dell'annuncio corrispondente verrà tracciata come durata del contenuto principale. Ciò potrebbe avere un impatto significativo sui dati aggregati che saranno disponibili in Adobe Analytics.

## Risposta

```
HTTP/1.1 204 No Content 
Server nginx/1.13.5 
Date Thu, 26 Oct 2017 19:15:24 GMT 
Connection keep-alive 
Access-Control-Allow-Origin * 
Access-Control-Allow-Methods OPTIONS,POST,PUT 
Access-Control-Allow-Headers Content-Type 
Access-Control-Expose-Headers Location
```

## Codici di risposta HTTP

| Codice di risposta HTTP | Descrizione | Elementi azione client |
|---|---|---|
| **204** | **Nessun contenuto.** La chiamata <br/><br/>Heartbeat ha avuto successo. | N/D |
| **400** | **Richiesta non valida.** Formato <br/><br/>della richiesta non corretto. | Controllate gli schemi [di convalida](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) JSON per il tipo di richiesta. |
| **404** | **Non trovato.** <br/><br/>L'ID sessione per la sessione multimediale non è stato trovato nel servizio back-end. | L'applicazione client deve utilizzare l'API di richiesta [](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Sessions per creare un'altra sessione multimediale e per eseguire il tracciamento dei report su di essa. |
| **410** | **Andato.** <br/><br/>La sessione multimediale è stata trovata nel servizio back-end, ma il client non può più generare rapporti sull'attività. | L'applicazione client deve utilizzare l'API di richiesta [](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Sessions per creare un'altra sessione multimediale e per eseguire il tracciamento dei report su di essa. |
| **500** | **Errore del server** | N/D |

