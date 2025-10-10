---
title: API di raccolta multimediale in streaming ‐ endpoint di richiesta eventi
description: Quali sono i parametri e le risposte dell’endpoint della richiesta degli eventi API di Media Collection?
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 95%

---

# Richiesta eventi {#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## Parametro URI

`sid`: l’ID sessione restituito da una [Richiesta sessioni](mc-api-sessions-req.md).

## Corpo della richiesta

Il corpo della richiesta deve essere in formato JSON e avere la stessa struttura del corpo della richiesta di esempio:

```json
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
   * `playhead`: deve essere in secondi, ma può essere in compensazione.
   * `ts`: marca temporale; deve essere in millisecondi.
* `eventType` (Obbligatorio)
* `params` (Facoltativo)
* `customMetadata` (Facoltativo; invia solo con i tipi di evento `adStart` e `chapterStart`)
* `qoeData` (Facoltativo)

Per un elenco dei tipi di evento validi per questa versione, consulta [Tipi di eventi e descrizioni.](mc-api-event-types.md)

>[!IMPORTANT]
>
>***Tracciamento annunci:**&#x200B;puoi tenere traccia degli annunci solo all’interno di un`adBreak`*.
>
>In assenza di “bookend” `adBreakStart` e `adBreakComplete` intorno agli annunci, gli eventi `adStart` e `adComplete` verranno semplicemente ignorati e la corrispondente durata dell’annuncio verrà tracciata come durata del contenuto principale. Ciò potrebbe avere un impatto significativo sui dati aggregati che saranno disponibili in Adobe Analytics.

## Risposta

```text
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
| **204** | **Nessun contenuto.** <br/><br/>Chiamata heartbeat riuscita. | N/D |
| **400** | **Richiesta errata.** <br/><br/>Formato della richiesta non corretto. | Controlla gli [schemi di convalida JSON](mc-api-json-validation.md) per il tipo di richiesta. |
| **404** | **Non trovato.** <br/><br/>Impossibile trovare l’ID sessione della sessione multimediale nel servizio back-end. | L’applicazione client deve utilizzare l’API [Richiesta sessioni](mc-api-sessions-req.md) per creare un’altra sessione multimediale e segnalarne il tracciamento. |
| **410** | **Perso.** <br/><br/>La sessione multimediale è stata trovata nel servizio back-end, ma il client non può più segnalarne l’attività. | L’applicazione client deve utilizzare l’API [Richiesta sessioni](mc-api-sessions-req.md) per creare un’altra sessione multimediale e segnalarne il tracciamento. |
| **500** | **Errore del server** | N/D |
