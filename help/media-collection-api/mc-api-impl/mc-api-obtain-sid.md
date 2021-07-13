---
title: Ottenimento di un ID sessione
description: Scopri come codificare una richiesta di sessioni per ottenere l’ID di sessione dall’intestazione Posizione in una risposta.
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 9%

---

# Ottenimento di un ID sessione{#obtaining-a-session-id}

Questo frammento di codice da Reference Player mostra un modo per codificare una richiesta [Sessions,](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) insieme all&#39;estrazione dell&#39;ID sessione (e della versione API Media Collection) dall&#39;intestazione Location (Posizione) nella risposta:

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
