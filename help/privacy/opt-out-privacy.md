---
title: Spiegazione di rinuncia e privacy
description: Scopri come gestire il consenso, la rinuncia e la privacy.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eF09wxu2mIUoFph5EdHz5y0XtcpXHHLINqSGLQEMoHU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 382
ht-degree: 87%

---

# Rinuncia e privacy{#opt-out-and-privacy}

## Rinuncia / Consenso {#opt-out-opt-in}

Puoi controllare se l’attività di tracciamento è consentita su un dispositivo specifico:

* **App mobili:** le estensioni di file multimediali rispettano le impostazioni privacy nella Raccolta dati. Per rinunciare al tracciamento, è necessario impostare la privacy su [Rifiutata nei tag](https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/#create-a-mobile-property) o [Aggiorna lo stato della privacy in Mobile SDK](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#getprivacystatus).
* **App JavaScript/browser:** la libreria VA rispetta le impostazioni di privacy e rinuncia della `VisitorAPI`. Per evitare il tracciamento, devi rinunciare al servizio Visitor API. Per ulteriori informazioni su rinuncia e privacy, consulta [Servizio Adobe Experience Platform Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it).
* **App OTT (Chromecast, Roku):** gli SDK OTT forniscono API che supportano i requisiti del Regolamento generale sulla protezione dei dati (GDPR) e che consentono di impostare i flag di stato `opt` per la raccolta e la trasmissione dei dati e per il recupero di identità memorizzate localmente.

  >[!NOTE]
  >
  >Le chiamate di tracciamento heartbeat multimediale sono disattivate anche se lo stato di privacy è impostato su rinuncia.

  Puoi controllare se i dati di Analytics vengono inviati o meno su un dispositivo specifico utilizzando le seguenti impostazioni:

   * L’impostazione `privacyDefault` nel file di configurazione `ADBMobile.json`. Questo settaggio controlla l’impostazione iniziale che viene mantenuta finché non viene modificata nel codice.

   * Il metodo `ADBMobile().setPrivacyStatus()`.

      * **Rinuncia:**

         * **Chromecast:**

           ```
           ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
           ```

         * **Roku:**

           ```
           ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
           ```

        >[!IMPORTANT]
        >
        >Quando un utente rinuncia al tracciamento, tutti i dati e gli ID del dispositivo persistenti verranno eliminati finché l’utente non dà il consenso.

      * **Consenso:**

         * **Chromecast:**

           ```
           ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
           ```

         * **Roku:**

           ```
           ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
           ```

      * **Restituisce l’impostazione corrente:**

         * **Chromecast:**

           ```
           ADBMobile.config.getPrivacyStatus()
           ```

         * **Roku:**

           ```
           ADBMobile().getPrivacyStatus()
           ```

  Dopo aver modificato l’impostazione della privacy utilizzando `setPrivacyStatus`, la modifica rimane permanente finché non viene nuovamente modificata utilizzando questo metodo, oppure finché l’app non viene disinstallata e reinstallata.

## Recupero di identificatori memorizzati (app OTT) {#retrieving-stored-identifiers-ott-apps}

Queste informazioni sono utili per recuperare identità utente memorizzate localmente dall’app Roku.

>[!IMPORTANT]
>
>Il metodo per recuperare tutti gli identificatori fa sì che tutte le identità utente siano note e mantenute dall’SDK. Tale metodo deve essere chiamato **prima** che l’utente neghi il consenso.

Le identità memorizzate localmente vengono restituite in una stringa JSON che può contenere:

* Contesto dell’azienda - ID organizzazione IMS
* ID utente
* Experience Cloud ID (MCID)
* ID Data Source (DPID, DPUUID)
* ID di Analytics (AVID, AID, VID e RSID associati)
* ID Audience Manager (UUID)

Ad esempio:

* **Chromecast:**

  ```
  ADBMobile.config.getAllIdentifiersAsync(callback)
  ```

* **Roku:**

  ```
  vids = ADBMobile().getAllIdentifiers()
  ```
