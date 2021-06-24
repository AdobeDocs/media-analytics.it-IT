---
title: Invio di eventi ping
description: Gli eventi ping sono l'heartbeat di Streaming Media Analytics. Scopri come inviare un ping temporizzato per il contenuto principale o il tracciamento degli annunci.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 4%

---

# Invio di eventi ping{#sending-ping-events}

**Per il contenuto principale, è necessario attivare gli eventi di ping ogni 10 secondi, a partire da dopo 10 secondi di riproduzione, indipendentemente dagli altri eventi API inviati. Per il tracciamento degli annunci, è necessario attivare gli eventi di ping ogni 1 secondo.**

Gli eventi ping sono letteralmente il &quot;battito cardiaco&quot; di Media Analytics. Gli unici parametri richiesti per una chiamata ping sono `eventType: ping` insieme all&#39;oggetto `playerTime` (posizione della testina di riproduzione e marca temporale).

Il seguente frammento di codice mostra un modo per implementare un meccanismo di ping temporizzato per il contenuto principale (10 secondi di intervallo):

```js
... 
Pinger.init(10000); 
... 
Pinger.kill();

var Pinger = { 
    init: function(interval) { 
        this._timer = window.setInterval(function() { 
                $.event.trigger({type: "onPing", _data: ""}); 
            }, interval); 
    }, 
     
    kill: function() { 
        window.clearInterval(this._timer); 
    } 
}
```
