---
seo-title: Rifiuto e privacy
title: Rifiuto e privacy
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
translation-type: tm+mt
source-git-commit: 80208f1c4773857f7907be0b8566c55a03e6106c

---


# Rifiuto e privacy{#opt-out-and-privacy}

## Consenso/consenso {#section_zfb_syq_v2b}

Potete controllare se l'attività di tracciamento è consentita su un dispositivo specifico:

* **App mobili -** La libreria VA rispetta le impostazioni relative alla privacy e al rifiuto della `AdobeMobile` libreria. Per rifiutare il tracciamento, è necessario utilizzare la `AdobeMobile` libreria. Per ulteriori informazioni sulle impostazioni di privacy e rinuncia della `AdobeMobile` libreria, consultate [Impostazioni](https://docs.adobe.com/content/help/en/mobile-services/android/gdpr-privacy-android/privacy.html)di privacy e rinuncia.
* **JavaScript/Browser Apps -** La libreria VA rispetta le impostazioni relative alla `VisitorAPI` privacy e all'esclusione. Per evitare il tracciamento, devi rifiutare il servizio API Visitor. Per ulteriori informazioni su optout e privacy, consulta [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/).
* **App OTT (Chromecast, Roku) -** Gli SDK OTT forniscono API GDPR (General Data Protection Regulation) pronte che consentono di impostare `opt` i flag di stato per la raccolta e la trasmissione dei dati e di recuperare identità memorizzate localmente.

   >[!NOTE]
   >
   >Le chiamate di tracciamento heartbeat multimediali sono disattivate anche se lo stato di privacy è impostato su opt-out.

   Puoi controllare se i dati di Analytics vengono inviati o meno su un dispositivo specifico utilizzando le seguenti impostazioni:

   * Impostazione `privacyDefault` nel file di `ADBMobile.json` configurazione. Questo controlla l’impostazione iniziale e persiste finché non viene modificata nel codice.

   * Il `ADBMobile().setPrivacyStatus()` metodo.

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
         >Quando un utente si oppone al tracciamento, tutti i dati e gli ID del dispositivo persistenti vengono eliminati finché l'utente non ritorna.

      * **Opzione di rifiuto:**

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
   Dopo che l'impostazione della privacy è stata modificata utilizzando `setPrivacyStatus`, la modifica è permanente finché non viene nuovamente modificata con questo metodo, oppure finché l'app non viene disinstallata e reinstallata.

## Recupero Di Identificatori Memorizzati (App OTT) {#section_mky_2yq_v2b}

Queste informazioni sono utili per recuperare identità utente memorizzate localmente dall’app Roku.

>[!IMPORTANT]
>
>Il metodo per il recupero di tutti gli identificatori ottiene tutte le identità utente note e persistenti dall’SDK. You must call this method **before** a user opts-out.

Le identità memorizzate localmente vengono restituite in una stringa JSON che può contenere:

* Contesto aziendale - ID organizzazione IMS
* ID utente
* Experience Cloud ID (MCID)
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

