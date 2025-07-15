---
title: 'Eventi in coda quando la risposta delle sessioni è lenta '
description: Scopri cosa fare quando l’ID sessione viene restituito dopo che il lettore attiva gli eventi.
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 100%

---

# Eventi in coda quando la risposta delle sessioni è lenta {#queueing-events-when-sessions-response-is-slow}

L’API Media Collection è RESTful: ad esempio effettui una richiesta HTTP e attendi la risposta. Questo è un punto importante solo se esegui una [Richiesta sessioni](../mc-api-ref/mc-api-sessions-req.md) per ottenere un ID sessione all’inizio della riproduzione video. È importante perché l’ID sessione è necessario per tutte le chiamate di tracciamento successive.

È possibile che il lettore possa attivare eventi _prima che venga restituita la Richiesta sessioni_ (con il parametro ID sessione) dal backend. In questo caso, l’app deve mettere in coda tutti gli eventi di tracciamento che arrivano tra la [Richiesta sessioni](../mc-api-ref/mc-api-sessions-req.md) e la relativa risposta. Quando la Risposta sessioni arriva, devi prima elaborare tutti gli [eventi](../mc-api-ref/mc-api-events-req.md) in coda, quindi puoi iniziare l’elaborazione degli eventi _live_ con le chiamate [Eventi](../mc-api-ref/mc-api-events-req.md).

>[!NOTE]
>
>La [Richiesta eventi](../mc-api-ref/mc-api-events-req.md) non restituisce i dati al client oltre un codice di risposta HTTP.

Controlla il Lettore di riferimento nella tua distribuzione per sapere come elaborare gli eventi prima di ricevere un ID sessione. Ad esempio:

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

**Elabora tutti gli eventi in coda**. Il lettore di riferimento elabora gli eventi in coda come segue:

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
