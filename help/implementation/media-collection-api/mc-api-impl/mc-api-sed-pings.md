---
title: Invio di eventi ping
description: Gli eventi ping sono l’heartbeat dei servizi multimediali in streaming di Adobe. Scopri come inviare un ping temporizzato per il contenuto principale o il tracciamento degli annunci.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/EJ6R7DILB56bcHgAki-Lvto3yYbuhf-wYfklvPElDeM
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 110
ht-degree: 50%

---

# Invio di eventi ping{#sending-ping-events}

**È necessario attivare gli eventi ping ogni 10 secondi, dopo i primi 10 secondi di riproduzione, indipendentemente dagli altri eventi API inviati. Questo vale sia per il contenuto principale che per il tracciamento degli annunci.**

Gli eventi ping sono l’&quot;heartbeat&quot; dei servizi multimediali di streaming di Adobe. Gli unici parametri richiesti per una chiamata ping sono `eventType: ping` insieme all’oggetto `playerTime` (posizione della testina di riproduzione e marca temporale).

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
