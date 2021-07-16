---
title: Scopri come tenere traccia degli errori su Android
description: Scopri come implementare il tracciamento degli errori utilizzando Media SDK su Android.
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
exl-id: 6c4f693d-45c0-4a9c-bda1-c8721afe31f5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 2%

---

# Tracciamento errori su Android{#track-errors-on-android}

Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione tramite SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

1. Tracciare gli errori del lettore multimediale:

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID");
   }
   ```

>[!NOTE]
>
>Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento dei contenuti multimediali. Se l&#39;errore del lettore multimediale impedisce il proseguimento della riproduzione, assicurati che la sessione di tracciamento dei contenuti multimediali sia chiusa chiamando `trackSessionEnd` dopo aver chiamato `trackError`.
