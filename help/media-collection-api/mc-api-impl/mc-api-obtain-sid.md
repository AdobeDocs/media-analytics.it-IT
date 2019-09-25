---
seo-title: Ottenimento di un ID sessione
title: Ottenimento di un ID sessione
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Ottenimento di un ID sessione{#obtaining-a-session-id}

Questo frammento di codice del lettore di riferimento mostra un modo per codificare una richiesta di [sessioni,](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) insieme all'estrazione dell'ID sessione (e della versione API di Media Collection) dall'intestazione Posizione nella risposta:

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

