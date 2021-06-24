---
title: Configurazione ID utente
description: API per l’impostazione degli ID utente, che server come identificatore univoco del cliente.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: '"Media Analytics, API"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 8%

---

# Imposta ID utente{#set-user-ids}

L&#39;ID utente è un identificatore visitatore personalizzato univoco definito dall&#39;applicazione per un utente.

Imposta e ottieni l&#39;ID utente univoco sull&#39;SDK ADBMobile come segue:

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
