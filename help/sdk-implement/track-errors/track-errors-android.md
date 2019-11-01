---
title: Tenere traccia degli errori su Android
description: In questo argomento viene descritta l’implementazione del tracciamento degli errori tramite Media SDK su Android.
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Tenere traccia degli errori su Android{#track-errors-on-android}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

1. Tracciare gli errori del lettore multimediale:

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID"); 
   }
   ```

>[!NOTE]
>
>Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento del supporto. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, accertatevi che la sessione di tracciamento dei contenuti multimediali sia chiusa chiamando `trackSessionEnd` dopo la chiamata `trackError`.

