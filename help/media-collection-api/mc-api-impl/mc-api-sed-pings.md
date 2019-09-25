---
seo-title: Invio di eventi di ping
title: Invio di eventi di ping
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Invio di eventi di ping{#sending-ping-events}

**Per il contenuto principale, è necessario attivare gli eventi di ping ogni 10 secondi, a partire da 10 secondi di riproduzione, indipendentemente dagli altri eventi API inviati. Per il tracciamento degli annunci, devi attivare gli eventi di ping ogni 1 secondo.**

Gli eventi ping sono letteralmente il "battito di cuore" di Media Analytics. Gli unici parametri richiesti per una chiamata ping sono `eventType: ping` insieme all' `playerTime` oggetto (posizione dell'indicatore di riproduzione e marca temporale).

Il frammento di codice seguente mostra un modo per implementare un meccanismo di ping temporizzato per il contenuto principale (10 secondi di intervallo):

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

