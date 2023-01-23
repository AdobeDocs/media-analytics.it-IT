---
title: Scopri come tracciare il buffering utilizzando JavaScript 3.x
description: Scopri come tracciare gli eventi di buffering nelle app del browser (JS).
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '120'
ht-degree: 100%

---

# Tracciare il buffering utilizzando JavaScript 3.x{#track-buffering-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 3.x.

>[!IMPORTANT]
>
>Se implementi una versione precedente dell’SDK, puoi scaricare le Guide per sviluppatori qui: [Scaricare gli SDK.](/help/getting-started/download-sdks.md)

## Costanti di tracciamento del buffer

| Nome costante | Descrizione     |
|---|---|
| `BufferStart` | Costante per il tracciamento dell’evento di avvio del buffer |
| `BufferComplete` | Costante per il tracciamento dell’evento di completamento del buffer |

## Implementare il buffering

1. Ascolta gli eventi di buffering della riproduzione dal lettore multimediale e alla notifica dell’evento di inizio buffer, traccia il buffering utilizzando l’evento `BufferStart`.

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. Alla notifica del completamento del buffering dal lettore multimediale, traccia la fine del buffering utilizzando l’evento `BufferComplete`.

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

Esamina lo scenario di tracciamento [Riproduzione VOD con buffering](/help/use-cases/tracking-scenarios/vod-buffering.md) per ulteriori informazioni.
