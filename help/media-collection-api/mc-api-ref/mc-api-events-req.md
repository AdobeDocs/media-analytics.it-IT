---
seo-title: Richiesta eventi
title: Richiesta eventi
uuid: b 237 f 0 a 0-dc 29-418 b -89 ee -04 c 596 a 27 f 39
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Events request{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## Parametro URI

`sid`: L'ID sessione restituito da una [richiesta session.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## Corpo richiesta

Il corpo della richiesta deve essere JSON e deve avere la stessa struttura di questo corpo della richiesta di esempio:

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
   * `playhead` - Deve essere in secondi, ma può essere un mobile.
   * `ts` - Marca temporale; deve essere in millisecondi.
* `eventType` (Obbligatorio)
* `params` (Facoltativo)
* `customMetadata` (Facoltativo; solo con e tipi `adStart``chapterStart` di evento)
* `qoeData` (Facoltativo)

For a list of valid event types for this release, see [Event types and descriptions.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Tracciamento annunci:**puoi tenere traccia solo degli annunci all'interno di`adBreak`* un.
>
>In the absence of the `adBreakStart` and `adBreakComplete` "bookends" around ads, `adStart` and `adComplete` events will simply be ignored, and the corresponding ad duration will be tracked as main content duration. Ciò potrebbe avere un impatto significativo sui dati aggregati che saranno disponibili in Adobe Analytics.

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

| Codice risposta HTTP | Descrizione | Elementi azione client |
|---|---|---|
| **204** | **Nessun contenuto.**<br/><br/>Heartbeat call was successfully. | N/D |
| **400** | **Richiesta non valida.**<br/><br/>La richiesta aveva un formato errato. | Check the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for the request type. |
| **404** | **Non trovato.**<br/><br/>L'ID sessione per la sessione multimediale non è stato trovato nel servizio di back-end. | The client application should use the [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API to create another media session and report tracking on it. |
| **410** | **Gone.**<br/><br/>La sessione multimediale è stata trovata nel servizio di back-end, ma il client non può più generare rapporti sull'attività. | The client application should use the [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API to create another media session and report tracking on it. |
| **500** | **Errore server** | N/D |

