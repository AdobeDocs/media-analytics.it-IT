---
title: Rinuncia e privacy
description: Come gestire l’opt-in, la rinuncia e la privacy.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 9%

---

# Rinuncia e privacy{#opt-out-and-privacy}

## Rinuncia / Opt-in {#opt-out-opt-in}

Puoi controllare se l’attività di tracciamento è consentita su un dispositivo specifico:

* **App mobili:** la libreria VA rispetta le impostazioni di privacy e rinuncia della  `AdobeMobile` libreria. Per rinunciare al tracciamento, devi utilizzare la libreria `AdobeMobile` . Per ulteriori informazioni sulle impostazioni di privacy e rinuncia della libreria `AdobeMobile`, consulta [Impostazioni di rinuncia e privacy](https://experienceleague.adobe.com/docs/mobile-services/android/gdpr-privacy-android/privacy.html).
* **App JavaScript/browser:** la libreria VA rispetta le impostazioni di  `VisitorAPI` privacy e rinuncia. Per evitare il tracciamento, devi rinunciare al servizio API visitatore. Per ulteriori informazioni su privacy e rinuncia, consulta [Servizio Adobe Experience Platform Identity.](https://experienceleague.adobe.com/docs/id-service/using/home.html).
* **App OTT (Chromecast, Roku):** gli SDK OTT forniscono API che supportano i requisiti del Regolamento generale sulla protezione dei dati (RGPD) e che consentono di impostare i flag di  `opt` stato per la raccolta e la trasmissione dei dati e di recuperare le identità memorizzate localmente.

   >[!NOTE]
   >
   >Le chiamate di tracciamento heartbeat multimediale sono disattivate anche se lo stato di privacy è impostato su rinuncia.

   Puoi controllare se i dati di Analytics vengono inviati o meno su un dispositivo specifico utilizzando le seguenti impostazioni:

   * L&#39;impostazione `privacyDefault` nel file di configurazione `ADBMobile.json`. Questa opzione controlla l’impostazione iniziale e persiste finché non viene modificata nel codice.

   * Il metodo `ADBMobile().setPrivacyStatus()`.

      * **Consenso negato:**

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
         >Quando un utente rinuncia al tracciamento, tutti i dati e gli ID del dispositivo persistenti verranno eliminati finché l&#39;utente non ritorna all&#39;interno.

      * **Consenso negato:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **Restituisce l&#39;impostazione corrente:**

         * **Chromecast:**

            ```
            ADBMobile.config.getPrivacyStatus()
            ```

         * **Roku:**

            ```
            ADBMobile().getPrivacyStatus()
            ```
   Dopo che l&#39;impostazione della privacy viene modificata utilizzando `setPrivacyStatus`, la modifica rimane permanente finché non viene nuovamente modificata utilizzando questo metodo, oppure finché l&#39;app non viene disinstallata e reinstallata.

## Recupero di ID memorizzati (app OTT) {#retrieving-stored-identifiers-ott-apps}

Queste informazioni sono utili per recuperare identità utente memorizzate localmente dall’app Roku.

>[!IMPORTANT]
>
>Il metodo per recuperare tutti gli identificatori fa sì che tutte le identità utente siano note e mantenute dall’SDK. È necessario chiamare questo metodo **prima** di un utente che rinuncia.

Le identità memorizzate localmente vengono restituite in una stringa JSON che può contenere:

* Contesto aziendale - ID organizzazione IMS
* ID utente
* ID Experience Cloud (MCID)
* ID di origine dati (DPID, DPUUID)
* ID Analytics (AVID, AID, VID e RSID associati)
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
