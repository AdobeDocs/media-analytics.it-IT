---
title: Configurazione Chromecast
description: Configurazione dell’applicazione Media SDK per l’implementazione in Chromecast.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
translation-type: tm+mt
source-git-commit: be82be2eb58f89344f2125288599fef461db441e

---


# Configurazione Chromecast{#set-up-chromecast}

## Domande frequenti

_Dovrei usare l’SDK JavaScript per Chromecast o l’SDK JavaScript standard?_

La risposta corretta è &quot;Chromecast&quot;, per i seguenti motivi:
* Le librerie AppMeasurement e VisitorAPI dell’SDK JS standard non sono certificate per funzionare sulle piattaforme OTT. Nell’SDK Chromecast JS, la Video Heartbeats Library (VHL), Analytics e VisitorAPI sono tutte integrate nell’SDK unico, unificato e certificato per Chromecast.
* Chromecast SDK è molto più leggero dell&#39;SDK JS standard. Questo è fondamentale per l&#39;hardware di fascia bassa utilizzato dalle piattaforme OTT.

## Prerequisiti

* **Ottenete parametri di configurazione validi per Heartbeats** Questi parametri possono essere ottenuti da un rappresentante Adobe dopo che avete configurato il vostro account di analisi dei supporti.
* **Fornite le seguenti funzionalità nel lettore multimediale:**
   * *Un&#39;API per iscriversi agli eventi* del lettore - L&#39;SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni* sul lettore - Queste informazioni includono dettagli quali il nome del supporto e la posizione della testina di riproduzione.

Adobe Mobile Services fornisce una nuova interfaccia utente che riunisce le capacità mobile marketing per applicazioni mobile da Adobe Marketing Cloud. Inizialmente, Mobile Services fornisce un&#39;integrazione perfetta delle funzionalità di analisi e targeting delle app per le soluzioni Adobe Analytics e Adobe Target. Learn more at [Adobe Mobile Services documentation.](https://docs.adobe.com/content/help/it-IT/mobile-services/using/home.html)

L’SDK 2.x per Chromecast per le soluzioni Experience Cloud consente di misurare le applicazioni Chromecast scritte in JavaScript, sfruttare e raccogliere i dati sul pubblico tramite la gestione dell’audience e misurare il coinvolgimento dei video attraverso heartbeat video.

## Implementazione SDK

1. Aggiungete al progetto la libreria Chromecast [scaricata](/help/sdk-implement/download-sdks.md#download-2x-sdks) .

   1. Il file `AdobeMobileLibrary-Chromecast-[version]` zip è costituito dai seguenti componenti software:

      * `adbmobile-chromecast.min.js`:

         Questo file libreria verrà incluso nella cartella di origine dell&#39;app Chromecast.

      * `ADBMobileConfig` config

         Questo file di configurazione SDK è personalizzato per la tua app. Con l’SDK (in `ADBMobileConfig` ) viene fornita un’implementazione di esempio `samples/`. Ottenete le impostazioni corrette da un rappresentante Adobe.
   1. Aggiungete il file della libreria al `index.html` file e create la variabile `ADBMobileConfig` globale come segue (la variabile globale utilizzata per configurare Adobe Mobile per Heartbeats ha una chiave esclusiva denominata `mediaHeartbeat`):

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
      >Se `mediaHeartbeat` è configurata in modo errato, il modulo multimediale (VHL) immette uno stato di errore e interrompe l&#39;invio di chiamate di tracciamento.

      Parametri di configurazione ADBMobile per la chiave mediaHeartbeat:
   | Parametro di configurazione | Descrizione     |
   | --- | --- |
   | `server` | Stringa che rappresenta l&#39;URL dell&#39;endpoint di tracciamento sul backend. |
   | `publisher` | Stringa che rappresenta l&#39;identificatore univoco dell&#39;autore del contenuto. |
   | `channel` | Stringa che rappresenta il nome del canale di distribuzione del contenuto. |
   | `ssl` | Valore booleano che rappresenta se SSL deve essere utilizzato per il tracciamento delle chiamate. |
   | `ovp` | Stringa che rappresenta il nome del fornitore del lettore video. |
   | `sdkversion` | Stringa che rappresenta la versione corrente dell&#39;app/SDK. |
   | `playerName` | Stringa che rappresenta il nome del lettore. |


1. Configura ID visitatore Experience Cloud.

   Il servizio ID visitatori di Experience Cloud fornisce un ID visitatore universale nelle soluzioni Experience Cloud. Il servizio Visitor ID è richiesto da Video Heartbeat e da altre integrazioni Marketing Cloud.

   Verifica che la tua `ADBMobileConfig` configurazione contenga il tuo ID `marketingCloud` organizzazione.

   ```js
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

   | Metodo | Descrizione |
   | --- | --- |
   | `getMarketingCloudID()` | Retrieves the Experience Cloud Visitor ID from the Visitor ID service.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Con l’ID visitatore di Experience Cloud, puoi impostare altri ID cliente da associare a ogni visitatore. L&#39;API Visitor accetta più ID cliente per lo stesso visitatore e un identificatore del tipo di cliente per separare l&#39;ambito dei diversi ID cliente. Questo metodo corrisponde a `setCustomerIDs()` nella libreria JavaScript.  Ad esempio: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |



<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://docs.adobe.com/content/help/en/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->

