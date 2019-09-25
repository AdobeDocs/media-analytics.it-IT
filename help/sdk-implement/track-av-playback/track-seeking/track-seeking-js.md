---
seo-title: Tracciare la ricerca in JavaScript
title: Tracciare la ricerca in JavaScript
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracciare la ricerca in JavaScript{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento delle ricerche

| Nome costante | Descrizione     |
|---|---|
| `SeekStart` | Costante per il tracciamento dell'evento Seek Start. |
| `SeekComplete` | Costante per il tracciamento dell'evento Seek Complete. |

## Implementa ricerca

1. Ascoltare gli eventi di ricerca della riproduzione dal lettore multimediale e, durante la ricerca, avviare la notifica dell’evento, tenere traccia della ricerca mediante l’ `SeekStart` evento:

   ```js
   _onSeekStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
   };
   ```

1. Alla ricerca della notifica completa dal lettore multimediale, tenete traccia della fine della ricerca mediante l’ `SeekComplete` evento:

   ```js
   _onSeekComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
   };
   ```

Per ulteriori informazioni, vedi la riproduzione [VOD dello scenario di tracciamento con la ricerca nel contenuto](/help/sdk-implement/tracking-scenarios/vod-seeking.md) principale.
