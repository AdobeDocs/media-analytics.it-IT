---
seo-title: Tracciamento delle azioni dell'app
title: Tracciamento delle azioni dell'app
uuid: 9 cdc 048 a -419 a -4725-bd 61-6 ca 6 d 909 cf 10
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Track app actions{#track-app-actions}

Per "azioni" si intendono gli eventi che si verificano nell’app oggetto delle misurazioni.

A ogni azione corrispondono una o più metriche che vengono incrementate ogni volta che si verifica l’evento. For example, you might send a `trackAction` call for each new subscription, or each time content is rated, or each time a level is completed.

Actions are not tracked automatically, so call `trackAction` when an event that you want to track occurs, and map the action to a custom event.

1. When an event that you want to track occurs, call `trackAction`.

   * **Roku:**

      ```js
      ADBMobile().trackAction("myapp.ActionName", {})
      ```

   * **Chromecast:**

      ```js
      ADBMobile.analytics.trackAction("myapp.ActionName", {});
      ```

1. Mappate l'azione su un evento personalizzato.

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

Con ogni chiamata di tracciamento delle azioni puoi anche inviare dati di contesto aggiuntivi.

