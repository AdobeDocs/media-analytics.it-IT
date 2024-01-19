---
title: Invio di eventi ping
description: Gli eventi ping sono l’heartbeat di Streaming Media Analytics. Scopri come inviare un ping temporizzato per il contenuto principale o il tracciamento degli annunci.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: e84864164adf056f47f24d65f0400c89d53d1630
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 70%

---

# Invio di eventi ping {#sending-ping-events}

**Devi attivare gli eventi ping ogni 10 secondi, dopo i primi 10 secondi di riproduzione, indipendentemente dagli altri eventi API inviati. Questo vale sia per il contenuto principale che per il tracciamento degli annunci.**

Gli eventi ping sono letteralmente gli “heartbeat” di Media Analytics. Gli unici parametri richiesti per una chiamata ping sono `eventType: ping` insieme all’oggetto `playerTime` (posizione della testina di riproduzione e marca temporale).

Il seguente frammento di codice mostra un modo per implementare un meccanismo di ping temporizzato per il contenuto principale (ogni 10 secondi):

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
