---
title: Scopri come tenere traccia della ricerca con JavaScript 3.x
description: Scopri come tenere traccia degli eventi Seek Start e Seek Complete utilizzando Media SDK nelle app del browser (JS 3.x).
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 2%

---

# Tracciamento ricerca con JavaScript 3.x{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione in tutti gli SDK 3.x. Se implementi una versione precedente dell’SDK, puoi scaricare le Guide per sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento ricerca

| Nome costante | Descrizione     |
|---|---|
| `SeekStart` | Costante per il tracciamento dell’evento Seek Start . |
| `SeekComplete` | Costante per il tracciamento dell’evento Seek Complete . |

## Implementare la ricerca

1. Ascoltare gli eventi di ricerca della riproduzione dal lettore multimediale e, alla ricerca della notifica dell&#39;evento di avvio, tenere traccia della ricerca utilizzando l&#39;evento `SeekStart`:

   ```js
   _onSeekStart = function() {
       tracker.trackEvent(ADB.Media.Event.SeekStart);
   };
   ```

1. Al momento della ricerca della notifica completa dal lettore multimediale, tieni traccia della fine della ricerca utilizzando l&#39;evento `SeekComplete` :

   ```js
   _onSeekComplete = function() {
       tracker.trackEvent(ADB.Media.Event.SeekComplete);
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con ricerca nel contenuto principale](/help/sdk-implement/tracking-scenarios/vod-seeking.md) .
