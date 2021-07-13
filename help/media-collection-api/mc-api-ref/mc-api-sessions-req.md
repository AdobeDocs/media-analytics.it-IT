---
title: Endpoint di richiesta per le sessioni dell'API di Media Collection in streaming �
description: '"Quali sono i parametri e le risposte dell’endpoint della richiesta delle sessioni API di Media Collection?"'
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
exl-id: f55f5838-610f-4f82-b3c5-72165ea2c86b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 10%

---

# Richiesta sessioni{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## Parametri URI

None

## Corpo della richiesta

Il corpo della richiesta deve essere JSON e deve avere la stessa struttura del corpo della richiesta di esempio:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "sessionStart", 
    "params": { 
        "media.playerName": "sample-html5-api-player", 
        "analytics.trackingServer": "<your-aa-tracking-server>", 
        "analytics.reportSuite": "<your-aa-rsid>", 
        "analytics.visitorId": "<your-userId>", 
        "media.contentType": "VOD", 
        "media.length": 60.39333333333333, 
        "media.id": "MA API Sample Player", 
        "visitor.marketingCloudOrgId": "<your-org-id>", 
        "media.name": "ClickMe", 
        "media.channel": "sample-channel", 
        "media.sdkVersion": "va-api-0.0.0", 
        "analytics.enableSSL": false 
    }, 
    "customMetadata": { 
        "myCustomData": "<your metadata>", 
        "myCustomData2": "<your metadata>", 
        ... 
    }, 
    "qoeData": { 
        "param1": "<your param-value>", 
        "param2": "<your param-value>", 
        ... 
    } 
}
```

* `playerTime` (Obbligatorio)
   * `playhead` - Deve essere in secondi, ma può essere un galleggiante.
   * `ts` - Timestamp; deve essere in millisecondi.
* `eventType` (Obbligatorio)

   **Valore valido:** `sessionStart`
* `params` (Obbligatorio)
* `customMetadata` (Facoltativo)
* `qoeData` (Facoltativo)

## Risposta

```
HTTP/1.1 201 Created 
Server: nginx/1.13.5 
Date: Wed, 06 Dec 2017 19:14:51 GMT 
Content-Type: application/octet-stream 
Content-Length: 0 
Location: /api/v1/sessions/bfcca2ca597a3c71bc03b4ce357833ad02b3570d262ecd0c595fcf8f2ae4df58 
Access-Control-Allow-Origin: * 
Access-Control-Allow-Methods: OPTIONS,POST,PUT 
Access-Control-Allow-Headers: Content-Type 
Access-Control-Expose-Headers: Location 
Age: 0 
Via: 1.1 wsg.sanjose08
```

`Location:` header - La  `/api/v1/` parte fornisce la versione API. La parte dopo `[…]sessions/` è l’ID sessione.

## Codici di risposta

| Codice di risposta HTTP | Descrizione |
|---|---|
| 201 | Sessione creata |
| 400 | Richiesta non valida |
| 500 | Errore del server |
