---
title: API di raccolta multimediale in streaming ‐ endpoint di richiesta eventi
description: Quali sono i parametri e le risposte dell’endpoint della richiesta degli eventi API di Media Collection?
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/yFHQhj33PM209WycWdPZsV-Yi8qN1DN-DC0KyyqFK1I
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: 263
ht-degree: 70%

---

# Richiesta eventi{#events-request}

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

* `playerTime` (obbligatorio)
   * `playhead`: deve essere in secondi, ma può essere in compensazione.
   * `ts`: marca temporale; deve essere in millisecondi.
* `eventType` (obbligatorio)
* `params` (facoltativo)
* `customMetadata` (Facoltativo; invia solo con i tipi di evento `adStart` e `chapterStart`)
* `qoeData` (Facoltativo)

Per un elenco dei tipi di evento validi ed esempi di implementazione per SDK, vedi [Panoramica eventi](/help/implementation/events/overview.md).

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
| **400** | **Richiesta non valida.** <br/><br/>Formato della richiesta non corretto. | Controlla gli [schemi di convalida JSON](mc-api-json-validation.md) per il tipo di richiesta. |
| **404** | **Non Trovato.** <br/><br/>Impossibile trovare l&#39;ID sessione per la sessione multimediale nel servizio back-end. | L’applicazione client deve utilizzare l’API [Richiesta sessioni](mc-api-sessions-req.md) per creare un’altra sessione multimediale e segnalarne il tracciamento. |
| **410** | **Non più.** <br/><br/>La sessione multimediale è stata trovata nel servizio back-end, ma il client non può più segnalare l&#39;attività. | L’applicazione client deve utilizzare l’API [Richiesta sessioni](mc-api-sessions-req.md) per creare un’altra sessione multimediale e segnalarne il tracciamento. |
| **500** | **Errore del server** | N/D |
