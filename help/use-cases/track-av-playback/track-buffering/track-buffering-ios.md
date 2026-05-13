---
title: Scopri come tenere traccia del buffering in iOS
description: Scopri come tenere traccia degli eventi di buffering su iOS.
uuid: 4f4db23a-489b-4b41-bb6e-393ec64d52a2
exl-id: 5f0a3c4b-7c9e-499d-98d0-6fcf316c4d9c
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/yCZGk7-ylrZBW4q3c6e6f-5Eprtkm7ipg-yIykCo-Yo
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 100%

---

# Tracciare il buffering su iOS{#track-buffering-on-ios}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK.](/help/getting-started/download-sdks.md)

## Costanti di tracciamento del buffer


| Nome costante | Descrizione     |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | Costante per il tracciamento dell’evento di avvio del buffer |
| `ADBMediaHeartbeatEventBufferComplete` | Costante per il tracciamento dell’evento di completamento del buffer |

## Implementare il buffering

1. Ascolta gli eventi di buffering di riproduzione dal lettore multimediale, e sulla notifica evento di avvio del buffer, tieni traccia del buffering utilizzando l’evento `BufferStart`:

   ```
   - (void)onBufferStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Al momento della notifica di completamento del buffer da parte del lettore multimediale, tieni traccia della fine del buffering utilizzando l’evento `BufferComplete`:

   ```
   - (void)onBufferComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

Esamina lo scenario di tracciamento [Riproduzione VOD con buffering](/help/use-cases/tracking-scenarios/vod-buffering.md) per ulteriori informazioni.
