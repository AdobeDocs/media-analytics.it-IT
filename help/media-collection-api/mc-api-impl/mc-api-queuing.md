---
seo-title: Invio in coda di eventi quando la risposta delle sessioni è lenta
title: Invio in coda di eventi quando la risposta delle sessioni è lenta
uuid: 39 ea 59 d 9-89 d 3-4087-a 806-48 a 43 ecf 0 c 98
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Queueing events when sessions response is slow{#queueing-events-when-sessions-response-is-slow}

L'API Media Collection è parametful: ad esempio, eseguite una richiesta HTTP e attendete la risposta. This is an important point only for when you make a [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) to obtain a Session ID at the beginning of video playback. Questo è importante perché l'ID sessione è richiesto per tutte le chiamate di tracciamento successive.

It is possible that your player may fire events _before the Sessions response returns_ (with the Session ID parameter) from the backend. If this occurs, your app must queue any tracking events that arrive between the [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) and its response. When the Sessions response arrives, you should first process any queued [events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md), then you can start processing _live_ events with the [Events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) calls.

>[!NOTE]
>
>The [Events request](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) does not return data back to the client beyond an HTTP response code.

Controllate il lettore di riferimento nella distribuzione per un modo di elaborazione prima di ricevere un ID sessione. Ad esempio:

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

Continuate a monitorare gli eventi di tracciamento quando si verificano.
