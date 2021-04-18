---
title: Invio di eventi ping
description: Invio di eventi ping
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

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
