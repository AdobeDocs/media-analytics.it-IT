---
seo-title: Rinuncia e privacy
title: Rinuncia e privacy
uuid: 7 e 60 c 7 bd -8 dba -4 c 7 a -9 c 3 c -0 c 634 b 815397
translation-type: tm+mt
source-git-commit: 80208f1c4773857f7907be0b8566c55a03e6106c

---


# Opt-out and privacy{#opt-out-and-privacy}

## Opt-out / Opt-in {#section_zfb_syq_v2b}

Potete controllare se l'attività di tracciamento è consentita su un dispositivo specifico:

* **App mobili -** La libreria VA rispetta le `AdobeMobile` impostazioni relative alla privacy e alla privacy della libreria. To opt-out of tracking, you need to use the `AdobeMobile` library. For more information on the `AdobeMobile` library’s opt-out and privacy settings, see [Opt-Out and Privacy Settings](https://docs.adobe.com/content/help/en/mobile-services/android/gdpr-privacy-android/privacy.html).
* **App javascript/Browser:** la libreria VA rispetta le impostazioni `VisitorAPI` relative alla privacy e al rifiuto. Per rifiutare il tracciamento, devi rifiutare il servizio Visitor API. For further information on opt­out and privacy, see [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/).
* **OTT Apps (Chromecast, Roku) -** Gli SDK OTT forniscono API che consentono di impostare `opt` lo stato per la raccolta dati e la trasmissione e per recuperare identità memorizzate localmente.

   >[!NOTE]
   >
   >Anche le chiamate di tracciamento heartbeat multimediali vengono disattivate se lo stato di privacy è impostato per la rinuncia.

   Puoi controllare se i dati di Analytics vengono inviati su un dispositivo specifico utilizzando le impostazioni seguenti:

   * `privacyDefault` Impostazione nel file `ADBMobile.json` di configurazione. Questo controlla l'impostazione iniziale e persiste finché non viene modificata nel codice.

   * The `ADBMobile().setPrivacyStatus()` method.

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
         >Quando un utente non rileva il tracciamento, tutti i dati e gli ID dei dispositivi persistenti verranno eliminati fino a quando l'utente non effettua nuovamente l'accesso.

      * **Rimuovi in:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **Restituisce l'impostazione corrente:**

         * **Chromecast:**

            ```
            ADBMobile.config.getPrivacyStatus()
            ```

         * **Roku:**

            ```
            ADBMobile().getPrivacyStatus()
            ```
   After the privacy setting is changed using `setPrivacyStatus`, the change is permanent until it is changed again using this method, or the app is uninstalled and reinstalled.

## Retrieving Stored Identifiers (OTT Apps) {#section_mky_2yq_v2b}

Queste informazioni sono utili per recuperare identità utente memorizzate localmente dall'app Roku.

>[!IMPORTANT]
>
>Il metodo per il recupero di tutti gli identificatori ottiene tutte le identità utente conosciute e persistenti dall'SDK. You must call this method **before** a user opts-out.

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

