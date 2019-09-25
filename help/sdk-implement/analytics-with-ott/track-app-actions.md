---
seo-title: Tracciare le azioni dell'app
title: Tracciare le azioni dell'app
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Track app actions{#track-app-actions}

Per "azioni" si intendono gli eventi che si verificano nell’app oggetto delle misurazioni.

A ogni azione corrispondono una o più metriche che vengono incrementate ogni volta che si verifica l’evento. For example, you might send a `trackAction` call for each new subscription, or each time content is rated, or each time a level is completed.

Actions are not tracked automatically, so call `trackAction` when an event that you want to track occurs, and map the action to a custom event.

1. Quando si verifica un evento che si desidera monitorare, chiama `trackAction`.

   * **Roku:**

      ```js
      ADBMobile().trackAction("myapp.ActionName", {})
      ```

   * **Chromecast:**

      ```js
      ADBMobile.analytics.trackAction("myapp.ActionName", {});
      ```

1. Mappare l'azione su un evento personalizzato.

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

