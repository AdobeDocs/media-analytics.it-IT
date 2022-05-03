---
title: Esempi di tracciamento dello stato del lettore
description: Questo argomento include esempi della funzione di tracciamento dello stato del lettore.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '119'
ht-degree: 100%

---

# Esempi di tracciamento dello stato del lettore


## Esempio di pausa lunga

Quando la pausa della sessione video ha una durata superiore a 30 minuti, l’API richiede una nuova sessione. In questo caso, il client deve generare un nuovo ID sessione. Per entrambe le sessioni video, il client deve mantenere tutti gli stati in cui si trova un lettore e inviare tutte le informazioni come evento `stateStart` subito dopo la chiamata `sessionStart`.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Dopo che `sessionEnd` viene inviato, è necessario avviare una nuova sessione video e i primi eventi API saranno:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

L’esempio di pausa lunga mostra che il lettore memorizza anche i propri stati, in modo che possano essere inviati alla nuova sessione video.
