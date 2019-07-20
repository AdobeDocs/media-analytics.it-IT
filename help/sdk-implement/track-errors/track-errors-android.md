---
seo-title: Tenere traccia degli errori su Android
title: Tenere traccia degli errori su Android
uuid: 7 d 0 c 77 e 5-924 c -4619-8 e 29-3484748 ab 736
translation-type: tm+mt
source-git-commit: 5ff3566fae2c1df559341057fafdd289774e4b2f

---


# Track errors on Android{#track-errors-on-android}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

1. Errori del lettore multimediale:

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID"); 
   }
   ```

>[!NOTE]
>
>Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento multimediale. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

