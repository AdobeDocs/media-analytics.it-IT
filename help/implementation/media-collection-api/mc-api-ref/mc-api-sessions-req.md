---
title: API di Streaming Media Collection - Endpoint di richiesta sessioni
description: “Quali sono i parametri e le risposte dell’endpoint della richiesta sessioni dell'API di Media Collection?”
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
exl-id: f55f5838-610f-4f82-b3c5-72165ea2c86b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 100%

---

# Richiesta sessioni {#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## Parametri URI

Nessuno

## Corpo della richiesta

Il corpo della richiesta deve essere in formato JSON e avere la stessa struttura del corpo della richiesta di esempio:

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

* `playerTime` (obbligatorio)
   * `playhead` - Se il contenuto è in diretta, l&#39;indicatore di riproduzione deve essere il secondo corrente del giorno, 0 &lt;= indicatore di riproduzione &lt; 86400. Se il contenuto è registrato, l&#39;indicatore di riproduzione deve essere il secondo corrente del contenuto, 0 &lt;= indicatore di riproduzione &lt; lunghezza contenuto. Il valore può essere un numero a virgola mobile.
   * `ts` - Marca temporale; deve essere espresso in millisecondi; Coordinated Universal Time (UTC).
* `eventType` (obbligatorio)

   **Valore valido:** `sessionStart`
* `params` (obbligatorio)
* `customMetadata` (facoltativo)
* `qoeData` (facoltativo)

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

`Location:` intestazione - La parte `/api/v1/` fornisce la versione dell&#39;API. La parte dopo `[…]sessions/` è l&#39;ID sessione.

## Codici di risposta

| Codice di risposta HTTP | Descrizione |
|---|---|
| 201 | Sessione creata |
| 400 | Richiesta errata |
| 500 | Errore del server |
