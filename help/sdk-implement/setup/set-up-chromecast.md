---
seo-title: Configurare Chromecast
title: Configurare Chromecast
uuid: d 664 e 394-02 a 2-4985-bbad-be 1 bcc 44 fb 2 b
translation-type: tm+mt
source-git-commit: ab400b673e97f9b47c6088e09b7e7d9e7b1c9ee6

---


# Set up Chromecast{#set-up-chromecast}

## Domande frequenti

_Posso usare l'SDK Chromecast javascript o posso usare l'SDK Javascript standard?_

La risposta corretta è "Chromecast", per i motivi seguenti:
* Le librerie appmeasurement e visitorapi nell'SDK standard JS non sono certificate per funzionare sulle piattaforme OTT. In Chromecast JS SDK, i Video Heartbeats Library (VHL), Analytics e visitorapi sono integrati nell'SDK singolo, certificato per Chromecast.
* L'SDK Chromecast è molto più leggero rispetto all'SDK standard JS. Questo è molto importante per l'hardware inferiore utilizzato dalle piattaforme OTT.

## Prerequisiti

* **Ottenete parametri di configurazione validi per Heartbeats**
Questi parametri possono essere ottenuti da un rappresentante Adobe dopo aver configurato l'account di analisi multimediale.
* **Fornite le seguenti funzionalità nel lettore multimediale:**
   * *API per l'iscrizione agli eventi del lettore* - L'SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni* sul lettore: informazioni dettagliate quali il nome del supporto e la posizione della testina di riproduzione.

Adobe Mobile Services fornisce una nuova interfaccia utente che riunisce le capacità mobile marketing per applicazioni mobile da Adobe Marketing Cloud. Inizialmente, Mobile Services fornisce un'integrazione perfetta delle funzionalità di analisi e targeting delle app per le soluzioni Adobe Analytics e Adobe Target. Learn more at [Adobe Mobile Services documentation.](https://marketing.adobe.com/resources/help/en_US/mobile/)

Chromecast SDK 2. x per soluzioni Experience Cloud consente di misurare le applicazioni Chromecast scritte in javascript, sfruttare e raccogliere dati sul pubblico tramite Gestione dell'audience e misurare il coinvolgimento video tramite heartbeat video.

## Implementazione SDK

1. Add your [downloaded](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Chromecast library to your project.

   1. The `AdobeMobileLibrary-Chromecast-[version]` zip file consists of the following software components:

      * `adbmobile-chromecast.min.js`:

         Questo file di libreria verrà incluso nella cartella sorgente dell'app Chromecast.

      * `ADBMobileConfig` config

         Questo file di configurazione SDK viene personalizzato per l'app. A sample `ADBMobileConfig` implementation is provided with the SDK (under `samples/`). Ottenete le impostazioni corrette da un rappresentante Adobe.
   1. Add the library file to your `index.html` file, and create the `ADBMobileConfig` global variable as follows (the global variable used to configure Adobe Mobile for Heartbeats has an exclusive key named `mediaHeartbeat`):

      ```js
      <script> 
          var ADBMobileConfig = { 
            "marketingCloud": { 
              "org": "972C898555E9F7BC7F000101@AdobeOrg" 
            }, 
            "target": { 
              "clientCode": "", 
              "timeout": 5 
            }, 
            "audienceManager": { 
              "server": "obumobile5.demdex.net" 
            }, 
            "analytics": { 
              "rsids": "mobile5vhl.sample.player", 
              "server": "obumobile5.sc.omtrdc.net", 
              "ssl": false, 
              "offlineEnabled": false, 
              "charset": "UTF-8", 
              "lifecycleTimeout": 300, 
              "privacyDefault": "optedin", 
              "batchLimit": 0, 
              "timezone": "MDT", 
              "timezoneOffset": -360, 
              "referrerTimeout": 0, 
              "poi": [] 
            }, 
            "mediaHeartbeat": { 
              "server": "obumobile5.hb.omtrdc.net", 
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg", 
              "channel": "test-channel-chromecast", 
              "ssl": false, 
              "ovp": "chromecast-player", 
              "sdkVersion": "chromecast-sdk", 
              "playerName": "Chromecast" 
            } 
          }; 
        </script> 
      <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script>
      ```

      >[!IMPORTANT]
      >
      >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.

      Parametri di configurazione adbmobile per la chiave mediaheartbeat:
   | Parametro di configurazione | Descrizione     |
   | --- | --- |
   | `server` | Stringa che rappresenta l'URL dell'endpoint di tracciamento sul backend. |
   | `publisher` | Stringa che rappresenta l'identificatore univoco dell'editore del contenuto. |
   | `channel` | Stringa che rappresenta il nome del canale di distribuzione del contenuto. |
   | `ssl` | Booleano che rappresenta se SSL deve essere utilizzato per il tracciamento delle chiamate. |
   | `ovp` | Stringa che rappresenta il nome del fornitore del lettore video. |
   | `sdkversion` | Stringa che rappresenta la versione corrente dell'app/SDK. |
   | `playerName` | Stringa che rappresenta il nome del lettore. |


1. Configura ID visitatore Experience Cloud.

   Il servizio ID visitatori di Experience Cloud fornisce un ID visitatore universale nelle soluzioni Experience Cloud. Il servizio ID visitatori è richiesto per video heartbeat e altre integrazioni Marketing Cloud.

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```js
   "marketingCloud": { 
       "org": YOUR-MCORG-ID" 
   }
   ```

   Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Ensure that you include `@AdobeOrg`.

   Una volta completata la configurazione, viene generato un ID visitatore Experience Cloud che viene incluso in tutti gli hit. Other Visitor IDs, such as `custom` and `automatically-generated`, continue to be sent with each hit.

   **Metodi del servizio ID visitatori di Experience Cloud**

   >[!TIP]
   >
   >Experience Cloud Visitor ID methods are prefixed with `visitor`.

   | Metodo | Descrizione |
   | --- | --- |
   | `getMarketingCloudID()` | Retrieves the Experience Cloud Visitor ID from the Visitor ID service.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Con l'ID visitatore di Experience Cloud, puoi impostare altri ID cliente da associare a ogni visitatore. L'API Visitor accetta più ID cliente per lo stesso visitatore e un identificatore del tipo di cliente per separare l'ambito dei diversi ID cliente. Questo metodo corrisponde a `setCustomerIDs()` nella libreria JavaScript.  For example: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |


<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->

