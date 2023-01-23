---
title: Scopri come tracciare la ricerca utilizzando JavaScript 2.x
description: Scopri come tracciare gli eventi di inizio e di completamento della ricerca utilizzando il Media SDK nelle app del browser (JS 2.x).
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
exl-id: 90f35376-24d8-405d-82b4-d6b737acf7b9
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '135'
ht-degree: 100%

---

# Tracciare la ricerca utilizzando JavaScript 2.x {#track-seeking-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK.](/help/getting-started/download-sdks.md)

## Costanti di tracciamento della ricerca

| Nome costante | Descrizione     |
|---|---|
| `SeekStart` | Costante per il tracciamento dell’evento di inizio ricerca |
| `SeekComplete` | Costante per il tracciamento dell’evento di completamento della ricerca |

## Implementare la ricerca

1. Ascolta gli eventi di ricerca della riproduzione dal lettore multimediale e alla notifica dell’evento di inizio della ricerca, traccia la ricerca utilizzando l’evento `SeekStart`:

   ```js
   _onSeekStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
   };
   ```

1. Alla notifica del completamento della ricerca dal lettore multimediale, traccia la fine della ricerca utilizzando l’evento `SeekComplete`:

   ```js
   _onSeekComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con ricerca nel contenuto principale](/help/use-cases/tracking-scenarios/vod-seeking.md).
