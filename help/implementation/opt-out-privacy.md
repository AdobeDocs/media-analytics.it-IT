---
title: Informazioni sulla rinuncia e sulla privacy
description: Scopri come gestire il consenso, la rinuncia e la privacy.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '385'
ht-degree: 100%

---

# Rinuncia e privacy {#opt-out-and-privacy}

## Rinuncia / Consenso {#opt-out-opt-in}

Puoi controllare se l’attività di tracciamento è consentita su un dispositivo specifico:

* **App mobili:** la libreria VA rispetta le impostazioni `AdobeMobile` relative alla privacy e alla rinuncia della libreria. Per rinunciare al tracciamento, devi utilizzare la libreria `AdobeMobile`. Per ulteriori informazioni sulla le impostazioni di rinuncia e privacy della libreria `AdobeMobile`, vedi [Impostazioni di privacy e rinuncia](https://experienceleague.adobe.com/docs/mobile-services/android/gdpr-privacy-android/privacy.html?lang=it).
* **App JavaScript/browser:** la libreria VA rispetta le impostazioni di privacy e rinuncia della `VisitorAPI`. Per evitare il tracciamento, devi rinunciare al servizio Visitor API. Per ulteriori informazioni su rinuncia e privacy, vedi [Servizio Adobe Experience Platform Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it).
* **App OTT (Chromecast, Roku):** gli SDK OTT forniscono API che supportano i requisiti del Regolamento generale sulla protezione dei dati (RGPD) e che consentono di impostare i flag di stato `opt` per la raccolta e la trasmissione dei dati e per il recupero di identità memorizzate localmente.

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
