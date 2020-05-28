---
title: Esempi di tracciamento dello stato del lettore
description: Questo argomento include esempi della funzione di tracciamento dello stato del lettore.
translation-type: tm+mt
source-git-commit: 1c2992d2a5992b07fa24823501d542c1878aa296
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Esempi di tracciamento dello stato del lettore


## Esempio di pausa lunga

Quando una sessione video ha una durata di pausa superiore a 30 minuti, l&#39;API richiede una nuova sessione. In questo caso, il client deve generare un nuovo ID sessione. Per entrambe le sessioni video, il client deve mantenere tutti gli stati in cui è presente un lettore e inviare tutte le informazioni come `stateStart` evento subito dopo la `sessionStart` chiamata.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd
`

Dopo l&#39; `sessionEnd` invio, è necessario avviare una nuova sessione video e i primi eventi API saranno:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

L’esempio di pausa lunga mostra che il lettore memorizza anche i relativi stati, in modo che possano essere inviati alla nuova sessione video.
