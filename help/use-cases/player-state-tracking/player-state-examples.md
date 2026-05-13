---
title: Esempi di tracciamento dello stato del lettore
description: Questo argomento include esempi della funzione di tracciamento dello stato del lettore.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eJ9Pb4tWQy0lRhkNXmexUyflt3qT0105FM--jAsGldQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 100%

---

# Esempi di tracciamento dello stato del lettore


## Esempio di pausa lunga

Quando la pausa della sessione video ha una durata superiore a 30 minuti, l’API richiede una nuova sessione. In questo caso, il client deve generare un nuovo ID sessione. Per entrambe le sessioni video, il client deve mantenere tutti gli stati in cui si trova un lettore e inviare tutte le informazioni come evento `stateStart` subito dopo la chiamata `sessionStart`.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Dopo che `sessionEnd` viene inviato, è necessario avviare una nuova sessione video e i primi eventi API saranno:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

L’esempio di pausa lunga mostra che il lettore memorizza anche i propri stati, in modo che possano essere inviati alla nuova sessione video.
