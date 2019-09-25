---
seo-title: Impostare gli ID utente
title: Impostare gli ID utente
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Impostare gli ID utente{#set-user-ids}

L’ID utente è un identificatore visitatore personalizzato univoco definito dall’applicazione per un utente.

Imposta e ottieni l’ID utente univoco nell’SDK ADBMobile come segue:

* **Set:**

   * **Roku:**

      ```
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

   * **Chromecast:**

      ```
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

* **Get:**

   * **Roku:**

      ```
      vid = ADBMobile().userIdentifer()
      ```

   * **Chromecast:**

      ```
      vid = ADBMobile().config.getUserIdentifer();
      ```
