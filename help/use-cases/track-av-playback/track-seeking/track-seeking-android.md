---
title: Scopri come tenere traccia della ricerca su Android
description: Scopri come tenere traccia degli eventi Seek Start e Seek Complete utilizzando Media SDK su Android.
uuid: 65addd99-eebf-4a80-8b4a-d5fbdff8ab06
exl-id: 8a8fcbcf-3232-4565-8c27-4167b6741613
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 26%

---

# Tracciamento ricerca su Android{#track-seeking-on-android}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK.](/help/getting-started/download-sdks.md)

## Costanti di tracciamento ricerca

| Nome costante | Descrizione     |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | Costante per il tracciamento dell’evento Seek Start . |
| `MediaHeartbeat.Event.SeekComplete` | Costante per il tracciamento dell’evento Seek Complete . |

## Implementare la ricerca

1. Ascoltare gli eventi di ricerca della riproduzione dal lettore multimediale e, alla ricerca della notifica dell&#39;evento di avvio, tenere traccia della ricerca utilizzando il `SeekStart` evento:

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null);
   }
   ```

1. Al momento della ricerca della notifica completa da parte del lettore multimediale, tieni traccia della fine della ricerca utilizzando il `SeekComplete` evento:

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null);
   }
   ```

Vedi lo scenario di tracciamento [Riproduzione VOD con ricerca nel contenuto principale](/help/use-cases/tracking-scenarios/vod-seeking.md) per ulteriori informazioni.