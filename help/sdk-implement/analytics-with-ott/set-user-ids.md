---
seo-title: Impostazione degli ID utente
title: Impostazione degli ID utente
uuid: fdd 54 fec -79 cd -4 bf 8-b 17 e -4 d 61 d 84 f 6310
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Set user IDs{#set-user-ids}

L'ID utente è un identificatore visitatore univoco definito dall'applicazione per un utente.

Imposta e ottieni l'ID utente univoco sull'SDK adbmobile, come segue:

* **Imposta:**

   * **Roku:**

      ```
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

   * **Chromecast:**

      ```
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

* **Ottieni:**

   * **Roku:**

      ```
      vid = ADBMobile().userIdentifer()
      ```

   * **Chromecast:**

      ```
      vid = ADBMobile().config.getUserIdentifer();
      ```
