---
title: Scopri come tenere traccia della ricerca con JavaScript 2.x
description: Scopri come tenere traccia degli eventi Seek Start e Seek Complete utilizzando Media SDK nelle app del browser (JS 2.x).
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
exl-id: 90f35376-24d8-405d-82b4-d6b737acf7b9
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 25%

---

# Tracciamento ricerca con JavaScript 2.x{#track-seeking-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK.](/help/getting-started/download-sdks.md)

## Costanti di tracciamento ricerca

| Nome costante | Descrizione     |
|---|---|
| `SeekStart` | Costante per il tracciamento dell’evento Seek Start . |
| `SeekComplete` | Costante per il tracciamento dell’evento Seek Complete . |

## Implementare la ricerca

1. Ascoltare gli eventi di ricerca della riproduzione dal lettore multimediale e, alla ricerca della notifica dell&#39;evento di avvio, tenere traccia della ricerca utilizzando il `SeekStart` evento:

   ```js
   _onSeekStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
   };
   ```

1. Al momento della ricerca della notifica completa da parte del lettore multimediale, tieni traccia della fine della ricerca utilizzando il `SeekComplete` evento:

   ```js
   _onSeekComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
   };
   ```

Vedi lo scenario di tracciamento [Riproduzione VOD con ricerca nel contenuto principale](/help/use-cases/tracking-scenarios/vod-seeking.md) per ulteriori informazioni.
