---
seo-title: Eventi in coda quando la risposta delle sessioni è lenta
title: Eventi in coda quando la risposta delle sessioni è lenta
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Eventi in coda quando la risposta delle sessioni è lenta{#queueing-events-when-sessions-response-is-slow}

L'API Media Collection è RESTful: ad esempio, effettuerete una richiesta HTTP e attenderete la risposta. Si tratta di un punto importante solo quando effettuate una richiesta [di](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) sessioni per ottenere un ID sessione all’inizio della riproduzione video. Questo è importante perché l'ID sessione è richiesto per tutte le chiamate di tracciamento successive.

È possibile che il lettore attivi eventi _prima che la risposta Sessioni restituisca_ (con il parametro ID sessione) dal backend. In tal caso, l'app deve mettere in coda tutti gli eventi di tracciamento che arrivano tra la richiesta [](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Sessioni e la relativa risposta. Quando arriva la risposta Sessioni, devi prima elaborare qualsiasi [evento](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)in coda, quindi puoi iniziare a elaborare eventi _live_ con le chiamate [Eventi](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) .

>[!NOTE]
>
>La richiesta [](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) Eventi non restituisce i dati al client oltre un codice di risposta HTTP.

Controllate il lettore di riferimento nella distribuzione per trovare un modo per elaborare gli eventi prima di ricevere un ID sessione. Ad esempio:

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

Continuate a elaborare gli eventi di tracciamento man mano che si verificano.
