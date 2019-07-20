---
seo-title: Set Up Roku
title: Set Up Roku
uuid: 904 dfda 0-4782-41 da-b 4 ab -212 e 81156633
translation-type: tm+mt
source-git-commit: bb3a303edba724c8f444d612b3be9d7250eea363

---


# Set Up Roku{#set-up-roku}

## Prerequisiti

* **Ottenete parametri di configurazione validi per Heartbeats**
Questi parametri possono essere ottenuti da un rappresentante Adobe dopo aver configurato l'account di analisi multimediale.
* **Fornite le seguenti funzionalità nel lettore multimediale:**
   * _API per l'iscrizione agli eventi del lettore_ - L'SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * _API che fornisce informazioni_ sul lettore: informazioni dettagliate quali il nome del supporto e la posizione della testina di riproduzione.

Adobe Mobile Services fornisce una nuova interfaccia utente che riunisce le capacità mobile marketing per applicazioni mobile da Adobe Marketing Cloud. Inizialmente, Mobile Services fornisce un'integrazione perfetta delle funzionalità di analisi e targeting delle app per le soluzioni Adobe Analytics e Adobe Target.

Learn more at [Adobe Mobile Services documentation.](https://marketing.adobe.com/resources/help/en_US/mobile/)

Roku SDK 2. x per soluzioni Experience Cloud consente di misurare le applicazioni Roku scritte in brightscript, sfruttare e raccogliere dati sul pubblico tramite Gestione dell'audience e misurare il coinvolgimento video tramite heartbeat video.

## Implementazione SDK

1. Add your [downloaded](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Roku library to your project.

   1. The `AdobeMobileLibrary-2.*-Roku.zip` download file consists of the following software components:

      * `adbmobile.brs`: Questo file di libreria verrà incluso nella cartella dell'origine app Roku.

      * `ADBMobileConfig.json`: Questo file di configurazione SDK viene personalizzato per l'app.
   1. Aggiungi il file libreria e il file di configurazione JSON all'origine del progetto.

      The JSON that is used to configure Adobe Mobile has an exclusive key for media heartbeats called `mediaHeartbeat`. Qui si trovano i parametri di configurazione per i heartbeat multimediali.

      >[!TIP]
      >
      >A sample `ADBMobileConfig` JSON file is provided with the package. Contattate i rappresentanti Adobe per le impostazioni.

      Ad esempio:

      ```
      {
        "version":"1.0", 
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8", 
          "ssl":false, 
          "offlineEnabled":false, 
          "lifecycleTimeout":30, 
          "batchLimit":50, 
          "privacyDefault":"optedin", 
          "poi":[ ]
      },
      "marketingCloud":{
        "org":""
      },
      "target":{ 
        "clientCode":"", 
        "timeout":5
      },
      "audienceManager":{ 
        "server":""
      },
      "acquisition":{ 
        "server":"example.com",
        "appid":"sample-app-id"
      },
      
      "mediaHeartbeat":{ 
         "server":"example.com", 
         "publisher":"sample-publisher", 
         "channel":"sample-channel", 
         "ssl":false,
         "ovp":"sample-ovp", 
         "sdkVersion":"sample-sdk", 
         "playerName":"roku"
         }    
      }
      ```

      | Parametro di configurazione | Descrizione     |
      | --- | --- |
      | `server` | Stringa che rappresenta l'URL dell'endpoint di tracciamento sul backend. |
      | `publisher` | Stringa che rappresenta l'identificatore univoco dell'editore del contenuto. |
      | `channel` | Stringa che rappresenta il nome del canale di distribuzione del contenuto. |
      | `ssl` | Booleano che rappresenta se SSL deve essere utilizzato per il tracciamento delle chiamate. |
      | `ovp` | Stringa che rappresenta il nome del fornitore del lettore video. |
      | `sdkversion` | Stringa che rappresenta la versione corrente dell'app/SDK. |
      | `playerName` | Stringa che rappresenta il nome del lettore. |

      >[!IMPORTANT]
      >
      >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.


1. Configura ID visitatore Experience Cloud.

   Il servizio ID visitatori di Experience Cloud fornisce un ID visitatore universale nelle soluzioni Experience Cloud. Il servizio ID visitatori è richiesto per video heartbeat e altre integrazioni Marketing Cloud.

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```
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

   |  Metodo   | Descrizione |
   | --- | --- |
   | `visitorMarketingCloudID` | Retrieves the Experience Cloud visitor ID from the visitor ID service.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Con l'ID visitatore di Experience Cloud, puoi impostare altri ID cliente da associare a ogni visitatore. L'API Visitor accetta più ID cliente per lo stesso visitatore e un identificatore del tipo di cliente per separare l'ambito dei diversi ID cliente. This method corresponds to `setCustomerIDs`. For example: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Utilizzato per impostare l'ID Roku per la pubblicità (RIDA) sull'SDK. Ad esempio: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>`"<sample_roku_identifier_for_advertising>")`<br/><br/><br/>Ottieni l'ID Roku per Pubblicità (RIDA) utilizzando l'API Roku SDK [getrida ()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) . |

   <!--
    Roku Api Reference: 
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->
