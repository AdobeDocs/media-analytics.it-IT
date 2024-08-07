---
title: Ottenimento di un ID sessione
description: Scopri come codificare una Richiesta di sessioni per ottenere l’ID di sessione dall’intestazione Posizione in una risposta.
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 100%

---

# Ottenimento di un ID sessione {#obtaining-a-session-id}

Questo frammento di codice dal Lettore di riferimento mostra un modo per codificare una [Richiesta sessioni](../mc-api-ref/mc-api-sessions-req.md) insieme all’estrazione dell’ID sessione (e della versione API di Media Collection) dall’intestazione Posizione nella risposta:

```js
var  
sessionData = { 
        ... 
        "media.contentType": "VOD", 
        "media.channel": "sample-channel", 
        ... 
    } 
}; 
...

const SESSION_ID_EXTRACTOR = /^\/api\/(.*)\/sessions\/(.*)/; 
    ...
    apiClient.request({ 
        "baseUrl": config.apiBaseUrl,   // The endpoint 
        "path": config.apiSessionsPath, // api/v1/sessions/ 
        "method": "POST",               // (Always POST) 
        "data": sessionData             // Mandatory params 
     }).then((response) => { 
        // Extract Session ID (and API version) 
        const [, apiVersion, sessionId] =  response.headers.Location.match(SESSION_ID_EXTRACTOR);  
        this.sessionId = sessionId;     // Session ID obtained 
        this._sessionStarted = true;    // Session started. 
    ...
```
