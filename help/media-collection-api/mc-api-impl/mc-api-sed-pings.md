---
seo-title: Invio di eventi di ping
title: Invio di eventi di ping
uuid: c 92 c 1 a 92-3 af 6-4474-9 e 42-ffb 8 f 6 c 94 b 33
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Sending ping events{#sending-ping-events}

**Per il contenuto principale, dovete attivare gli eventi ogni 10 secondi, a partire da 10 secondi di riproduzione, indipendentemente dagli altri eventi API che avete inviato. For Ad tracking, you must fire ping events every 1 second.**

Gli eventi di ping sono letteralmente "heartbeat" di Media Analytics. The only required parameters for a ping call are `eventType: ping` along with the `playerTime` object (playhead position and timestamp).

Lo snippet di codice seguente mostra uno dei metodi per implementare un meccanismo di aggancio temporizzato per il contenuto principale (10 secondo intervallo):

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

