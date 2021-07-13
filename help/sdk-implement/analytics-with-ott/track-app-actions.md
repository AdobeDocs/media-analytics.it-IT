---
title: Tracciamento azioni eseguite nell’app
description: Le azioni eseguite nell’app sono gli eventi che si verificano nell’app e che desideri misurare.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 29%

---

# Tracciare le azioni eseguite nell’app{#track-app-actions}

Le azioni sono gli eventi che si verificano nell’app che desideri misurare.

Ogni azione ha una o più metriche corrispondenti che vengono incrementate ogni volta che si verifica l’evento. Ad esempio, puoi inviare una chiamata `trackAction` per ogni nuovo abbonamento, ogni volta che il contenuto viene valutato o ogni volta che viene completato un livello.

Le azioni non vengono tracciate automaticamente, quindi chiama `trackAction` quando si verifica un evento che desideri tracciare e mappa l&#39;azione a un evento personalizzato.

1. Quando si verifica un evento di cui desideri tenere traccia, invoca `trackAction`.

   * **Roku:**

      ```js
      ADBMobile().trackAction("myapp.ActionName", {})
      ```

   * **Chromecast:**

      ```js
      ADBMobile.analytics.trackAction("myapp.ActionName", {});
      ```

1. Mappa l’azione a un evento personalizzato.

   * **Roku:**

      ```js
      dictionary = {} 
      dictionary["myapp.social.SocialSource"] = "Twitter"  
      ADBMobile().trackAction("myapp.SocialShare", dictionary)
      ```

   * **Chromecast:**

      ```js
      var dictionary = {}; 
      dictionary["myapp.social.SocialSource"] = "Twitter"; 
      ADBMobile.analytics.trackAction("myapp.SocialShare", dictionary);
      ```

Puoi anche inviare dati di contesto aggiuntivi con ogni chiamata di tracciamento delle azioni.
