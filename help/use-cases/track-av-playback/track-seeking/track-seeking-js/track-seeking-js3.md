---
title: Scopri come tracciare gli annunci utilizzando JavaScript 3.x
description: Scopri come tracciare gli eventi di inizio e di completamento della ricerca utilizzando Media SDK nelle app del browser (JS 3.x).
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '134'
ht-degree: 100%

---

# Tracciare gli annunci utilizzando JavaScript 3.x{#track-seeking-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 3.x.

>[!IMPORTANT]
>
>Se implementi una versione precedente dell’SDK, puoi scaricare le Guide per sviluppatori qui: [Scaricare gli SDK.](/help/getting-started/download-sdks.md)

## Costanti di tracciamento della ricerca

| Nome costante | Descrizione     |
|---|---|
| `SeekStart` | Costante per il tracciamento dell’evento di inizio ricerca |
| `SeekComplete` | Costante per il tracciamento dell’evento di completamento della ricerca |

## Implementare la ricerca

1. Ascolta gli eventi di ricerca della riproduzione dal lettore multimediale e alla notifica dell’evento di inizio della ricerca, traccia la ricerca utilizzando l’evento `SeekStart`:

   ```js
   _onSeekStart = function() {
       tracker.trackEvent(ADB.Media.Event.SeekStart);
   };
   ```

1. Alla notifica del completamento della ricerca dal lettore multimediale, traccia la fine della ricerca utilizzando l’evento `SeekComplete`:

   ```js
   _onSeekComplete = function() {
       tracker.trackEvent(ADB.Media.Event.SeekComplete);
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con ricerca nel contenuto principale](/help/use-cases/tracking-scenarios/vod-seeking.md).
