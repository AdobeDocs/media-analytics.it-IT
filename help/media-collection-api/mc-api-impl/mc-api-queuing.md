---
title: Eventi in coda quando la risposta delle sessioni è lenta
description: 'Scopri cosa fare quando l’ID sessione viene restituito dopo che il lettore attiva gli eventi. '
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 5%

---

# Eventi in coda quando la risposta delle sessioni è lenta{#queueing-events-when-sessions-response-is-slow}

L’API Media Collection è RESTful: Ad esempio, effettui una richiesta HTTP e attendi la risposta. Questo è un punto importante solo per quando effettui una [richiesta di sessioni](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) per ottenere un ID sessione all&#39;inizio della riproduzione video. Questo è importante perché l’ID sessione è necessario per tutte le chiamate di tracciamento successive.

È possibile che il lettore attivi eventi _prima che la risposta Sessions restituisca_ (con il parametro ID sessione) dal back-end. In questo caso, l&#39;app deve mettere in coda tutti gli eventi di tracciamento che arrivano tra la [richiesta di sessioni](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) e la relativa risposta. Quando arriva la risposta Sessions, devi prima elaborare tutti gli eventi [in coda](/help/media-collection-api/mc-api-ref/mc-api-events-req.md), quindi puoi iniziare a elaborare gli eventi _live_ con le chiamate [Eventi](/help/media-collection-api/mc-api-ref/mc-api-events-req.md).

>[!NOTE]
>
>La [richiesta di eventi](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) non restituisce i dati al client oltre un codice di risposta HTTP.

Controlla il Reference Player nella tua distribuzione per sapere come elaborare gli eventi prima di ricevere un ID sessione. Ad esempio:

```js
var eventData = {};            // JSON payload 
eventData.playerTime = getPlayerTime(); // Required 
eventData.eventType = "play";           // Required 
eventData.params = {};                  // Optional for events 
 
VideoPlayer.prototype._collectEvent =  
  function(eventData) { 
 
    // If we don't have a Session ID yet,  
    // queue the event and return... 
    if (!sessionStarted) { 
        console.log("[Player] Queueing event "); 
        _pendingEvents.push(eventData); 
        return; 
    } 
 
    // If we DO have a Session ID, process the 
    // tracking event...     
    apiClient.request({ 
        "baseUrl": "{endpoint}", 
        "path": "api/v1/{sid}/events", // events request 
        "method": "POST", 
        "data": eventData 
    }).then((response) => {   
        […] 
    } 
} 
 
VideoPlayer.prototype.collectEvent =  
  function (eventType, eventParams) { 
         
    if (typeof eventParams === 'undefined') {   
        eventParams = {}; 
    } 
 
    this._collectEvent({                   
        eventType: eventType,            // Required 
        playerTime: getPlayerTime(),     // Required 
        params: eventParams              // Optional  
    });                                    
}; 
 
VideoPlayer.prototype.getPlayerTime = function() { 
    return { 
        playhead: this.getPlayhead(),    // playhead value in seconds 
        ts: this.getCurrentTimestamp()   // timestamp value in milliseconds 
    }; 
};
```

**Elabora tutti gli eventi in coda -** Il lettore di riferimento elabora gli eventi in coda come segue:

```js
    […] 
    this._processPendingEvents();    // Once you have a Session ID, 
    […]                              // process any queued events 
 
VideoPlayer.prototype._processPendingEvents =  
  function() { 
    this._pendingEvents.forEach((eventData) => { 
        this._collectEvent(eventData); 
    }); 
 
    this._pendingEvents = []; 
}
```

Continua a elaborare gli eventi di tracciamento man mano che si verificano.
