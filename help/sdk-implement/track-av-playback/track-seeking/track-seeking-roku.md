---
title: Ricerca di tracce su Roku
description: In questo argomento viene descritta l’implementazione del tracciamento delle ricerche mediante l’SDK per file multimediali su Roku.
uuid: 0572252b-397f-4aa2-b4b5-c5346b75244a
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Ricerca di tracce su Roku{#track-seeking-on-roku}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento delle ricerche

| Nome costante | Descrizione     |
|---|---|
| `SeekStart` | Costante per il tracciamento dell'evento Seek Start. |
| `SeekComplete` | Costante per il tracciamento dell'evento Seek Complete. |

## Implementa ricerca

1. Ascoltare gli eventi di ricerca della riproduzione dal lettore multimediale e, durante la ricerca, avviare la notifica dell'evento, tenere traccia della ricerca mediante l' `SeekStart` evento.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_START, seekInfo, seekContextData)
   ```

1. Alla ricerca della notifica completa dal lettore multimediale, tenete traccia della fine della ricerca mediante l’ `SeekComplete` evento.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_COMPLETE, seekInfo, seekContextData)
   ```

Per ulteriori informazioni, vedi la riproduzione [VOD dello scenario di tracciamento con la ricerca nel contenuto](/help/sdk-implement/tracking-scenarios/vod-seeking.md) principale.
