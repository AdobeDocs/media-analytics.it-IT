---
title: Configurazione Roku
description: Configurazione dell’applicazione Media SDK per l’implementazione su Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Configurazione Roku{#set-up-roku}

## Prerequisiti

* **Ottenete parametri di configurazione validi per Heartbeats** Questi parametri possono essere ottenuti da un rappresentante Adobe dopo che avete configurato il vostro account di analisi dei supporti.
* **Fornite le seguenti funzionalità nel lettore multimediale:**
   * _Un&#39;API per iscriversi agli eventi_ del lettore - L&#39;SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * _API che fornisce informazioni_ sul lettore - Queste informazioni includono dettagli quali il nome del supporto e la posizione della testina di riproduzione.

Adobe Mobile Services fornisce una nuova interfaccia utente che riunisce le capacità mobile marketing per applicazioni mobile da Adobe Marketing Cloud. Inizialmente, Mobile Services fornisce un&#39;integrazione perfetta delle funzionalità di analisi e targeting delle app per le soluzioni Adobe Analytics e Adobe Target.

Learn more at [Adobe Mobile Services documentation.](https://docs.adobe.com/content/help/it-IT/mobile-services/using/home.html)

L’SDK 2.x Roku per le soluzioni Experience Cloud consente di misurare le applicazioni Roku scritte in BrightScript, sfruttare e raccogliere i dati sul pubblico tramite la gestione dell’audience e misurare il coinvolgimento video attraverso heartbeat video.

## Implementazione SDK

1. Aggiungi la libreria Roku [scaricata](/help/sdk-implement/download-sdks.md#download-2x-sdks) al tuo progetto.

   1. Il file di `AdobeMobileLibrary-2.*-Roku.zip` download è costituito dai seguenti componenti software:

      * `adbmobile.brs`: Questo file libreria verrà incluso nella cartella di origine dell&#39;app Roku.

      * `ADBMobileConfig.json`: Questo file di configurazione SDK è personalizzato per la tua app.
   1. Aggiungete il file di libreria e il file di configurazione JSON alla sorgente del progetto.

      Il JSON utilizzato per configurare Adobe Mobile dispone di una chiave esclusiva per i heartbeat multimediali denominati `mediaHeartbeat`. Qui appartengono i parametri di configurazione per i heartbeat multimediali.

      >[!TIP]
      >
      >Un file `ADBMobileConfig` JSON di esempio viene fornito con il pacchetto. Contattate i rappresentanti Adobe per le impostazioni.

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
      | `server` | Stringa che rappresenta l&#39;URL dell&#39;endpoint di tracciamento sul backend. |
      | `publisher` | Stringa che rappresenta l&#39;identificatore univoco dell&#39;autore del contenuto. |
      | `channel` | Stringa che rappresenta il nome del canale di distribuzione del contenuto. |
      | `ssl` | Valore booleano che rappresenta se SSL deve essere utilizzato per il tracciamento delle chiamate. |
      | `ovp` | Stringa che rappresenta il nome del fornitore del lettore video. |
      | `sdkversion` | Stringa che rappresenta la versione corrente dell&#39;app/SDK. |
      | `playerName` | Stringa che rappresenta il nome del lettore. |

      >[!IMPORTANT]
      >
      >Se `mediaHeartbeat` è configurata in modo errato, il modulo multimediale (VHL) immette uno stato di errore e interrompe l&#39;invio di chiamate di tracciamento.


1. Configura ID visitatore Experience Cloud.

   Il servizio ID visitatori di Experience Cloud fornisce un ID visitatore universale nelle soluzioni Experience Cloud. Il servizio Visitor ID è richiesto da Video Heartbeat e da altre integrazioni Marketing Cloud.

   Verifica che la tua `ADBMobileConfig` configurazione contenga il tuo ID `marketingCloud` organizzazione.

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Accertatevi di includere `@AdobeOrg`.

   Al termine della configurazione, viene generato un ID visitatore Experience Cloud che viene incluso in tutti gli hit. Other Visitor IDs, such as `custom` and `automatically-generated`, continue to be sent with each hit.

   **Metodi del servizio ID visitatori di Experience Cloud**

   >[!TIP]
   >
   >Experience Cloud Visitor ID methods are prefixed with `visitor`.

   |  Metodo   | Descrizione |
   | --- | --- |
   | `visitorMarketingCloudID` | Retrieves the Experience Cloud visitor ID from the visitor ID service.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Con l’ID visitatore di Experience Cloud, puoi impostare altri ID cliente da associare a ogni visitatore. L&#39;API Visitor accetta più ID cliente per lo stesso visitatore e un identificatore del tipo di cliente per separare l&#39;ambito dei diversi ID cliente. Questo metodo corrisponde a `setCustomerIDs`. Ad esempio: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Utilizzato per impostare l’ID Roku per la pubblicità (RIDA) sull’SDK. Ad esempio: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Ottenete l&#39;ID Roku per la pubblicità (RIDA) tramite l&#39;API Roku SDK [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) . |

   <!--
    Roku Api Reference: 
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://docs.adobe.com/content/help/en/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
