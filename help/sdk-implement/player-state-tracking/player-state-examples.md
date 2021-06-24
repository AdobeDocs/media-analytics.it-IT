---
title: Esempi di tracciamento dello stato del lettore
description: Questo argomento include esempi della funzione di tracciamento dello stato del lettore.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: 8a421ee4ee5d2e61126fc6ac8f10f326427e78a7
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 1%

---

# Esempi di tracciamento dello stato del lettore


## Esempio di lunga pausa

Quando una sessione video ha una durata di pausa superiore a 30 minuti, l’API richiede una nuova sessione. In questo caso, il client deve generare un nuovo ID sessione. Per entrambe le sessioni video, il client deve mantenere tutti gli stati in cui si trova un lettore e inviare tutte le informazioni come un evento `stateStart` subito dopo la chiamata `sessionStart`.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Dopo l’invio del file `sessionEnd`, è necessario avviare una nuova sessione video e i primi eventi API saranno:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

L’esempio di pausa lunga mostra che il lettore memorizza anche i suoi stati, in modo che possano essere inviati alla nuova sessione video.
