---
title: Endpoint di richiesta eventi per l'API di raccolta multimediale in streaming �
description: '"Quali sono i parametri e le risposte dell’endpoint della richiesta degli eventi API di Media Collection?"'
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 6%

---

# Richiesta eventi{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## Parametro URI

`sid`: L&#39;ID sessione restituito da una richiesta  [Sessions.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

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
   * `playhead` - Deve essere in secondi, ma può essere un galleggiante.
   * `ts` - Timestamp; deve essere in millisecondi.
* `eventType` (Obbligatorio)
* `params` (Facoltativo)
* `customMetadata` (Facoltativo; invia solo con  `adStart` e i tipi di  `chapterStart` evento)
* `qoeData` (Facoltativo)

Per un elenco dei tipi di evento validi per questa versione, consulta [Tipi di evento e descrizioni.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Tracciamento annunci -**Puoi tenere traccia solo degli annunci all’interno di un`adBreak`*.
>
>In assenza degli eventi `adBreakStart` e `adBreakComplete` &quot;bookend&quot; intorno agli annunci, `adStart` e `adComplete` verranno semplicemente ignorati e la corrispondente durata dell’annuncio verrà tracciata come durata del contenuto principale. Ciò potrebbe avere un impatto significativo sui dati aggregati che saranno disponibili in Adobe Analytics.

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
| **204** | **Nessun contenuto.** <br/><br/>Chiamata Heartbeat riuscita. | N/D |
| **400** | **Richiesta non valida.** <br/><br/>Formato della richiesta non corretto. | Controlla gli [schemi di convalida JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) per il tipo di richiesta. |
| **404** | **Non trovato.** <br/><br/>Impossibile trovare l&#39;ID sessione per la sessione multimediale nel servizio back-end. | L&#39;applicazione client deve utilizzare l&#39;API [Richiesta sessioni](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) per creare un&#39;altra sessione multimediale e generare rapporti su di essa. |
| **410** | **Andato.** <br/><br/>La sessione multimediale è stata trovata nel servizio back-end, ma il client non può più segnalare l&#39;attività su di esso. | L&#39;applicazione client deve utilizzare l&#39;API [Richiesta sessioni](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) per creare un&#39;altra sessione multimediale e generare rapporti su di essa. |
| **500** | **Errore del server** | N/D |
