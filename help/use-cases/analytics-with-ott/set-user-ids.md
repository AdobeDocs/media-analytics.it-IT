---
title: Configurare gli ID utente
description: API per l’impostazione degli ID utente, da usare come identificatori univoci dei clienti.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Media Analytics, API"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '53'
ht-degree: 100%

---

# Configurare gli ID utente {#set-user-ids}

L’ID utente è un identificatore visitatore personalizzato univoco, definito dall’applicazione per un utente.

Per impostare e ottenere l’ID utente univoco con ADBMobile SDK:

* **Impostare:**

   * **Roku:**

      ```
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

   * **Chromecast:**

      ```
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

* **Ottenere:**

   * **Roku:**

      ```
      vid = ADBMobile().userIdentifer()
      ```

   * **Chromecast:**

      ```
      vid = ADBMobile().config.getUserIdentifer();
      ```
