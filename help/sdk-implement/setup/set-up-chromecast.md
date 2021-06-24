---
title: Come impostare lo SKD di Media per Chromecast
description: Segui questi passaggi per configurare l’applicazione Media SDK su Chromecast.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 6%

---

# Configurazione Chromecast{#set-up-chromecast}

## Domande frequenti

_Devo usare l&#39;SDK JavaScript per Chromecast o posso usare l&#39;SDK JavaScript standard?_

La risposta corretta è &quot;Chromecast&quot;, per i motivi seguenti:
* Le librerie AppMeasurement e VisitorAPI nell’SDK JS standard non sono certificate per funzionare sulle piattaforme OTT. Nell’SDK di Chromecast JS, la Video Heartbeat Library (VHL), Analytics e VisitorAPI sono tutti incorporati nell’SDK unico, unificato e certificato per Chromecast.
* L’SDK di Chromecast è molto più leggero dell’SDK JS standard. Questo è fondamentale per l&#39;hardware di fascia bassa utilizzato dalle piattaforme OTT.

## Prerequisiti

* **Ottieni parametri di configurazione validi per**
HeartbeatQuesti parametri possono essere ottenuti da un rappresentante di Adobe dopo aver configurato il tuo account media analytics.
* **Fornisci le seguenti funzionalità nel lettore multimediale:**
   * *Un’API per abbonarti agli eventi*  del lettore: l’SDK per contenuti multimediali richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni*  sul lettore. Queste informazioni includono dettagli quali il nome del contenuto multimediale e la posizione della testina di riproduzione.

Adobe Mobile Services fornisce una nuova interfaccia utente che riunisce le capacità mobile marketing per applicazioni mobile da Adobe Marketing Cloud. Inizialmente, Mobile Services fornisce un’integrazione perfetta delle funzionalità di analisi e targeting delle app per le soluzioni Adobe Analytics e Adobe Target. Per ulteriori informazioni, consulta la [documentazione Adobe Mobile Services .](https://experienceleague.adobe.com/docs/mobile-services/using/home.html)

L’SDK 2.x per Chromecast per le soluzioni Experience Cloud consente di misurare le applicazioni Chromecast scritte in JavaScript, sfruttare e raccogliere i dati sul pubblico tramite Gestione dell’audience e misurare l’interazione video attraverso gli heartbeat video.

## Implementazione SDK

1. Aggiungi la [libreria Chromecast scaricata](/help/sdk-implement/download-sdks.md#download-2x-sdks) al tuo progetto.

   1. Il file zip `AdobeMobileLibrary-Chromecast-[version]` è costituito dai seguenti componenti software:

      * `adbmobile-chromecast.min.js`:

         Questo file libreria verrà incluso nella cartella di origine dell’app Chromecast.

      * `ADBMobileConfig` config

         Questo file di configurazione SDK è personalizzato per la tua app. Un esempio di implementazione `ADBMobileConfig` viene fornito con l&#39;SDK (in `samples/`). Ottieni le impostazioni corrette da un rappresentante di Adobe.
   1. Aggiungi il file della libreria al file `index.html` e crea la variabile globale `ADBMobileConfig` come segue (la variabile globale utilizzata per configurare Adobe Mobile per Heartbeat ha una chiave esclusiva denominata `mediaHeartbeat`):

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
              "ssl": true,
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
              "ssl": true,
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
      >Se `mediaHeartbeat` non è configurato correttamente, il modulo multimediale (VHL) immette uno stato di errore e smetterà di inviare chiamate di tracciamento.

      Parametri di configurazione ADBMobile per la chiave mediaHeartbeat:
   | Parametro di configurazione | Descrizione     |
   | --- | --- |
   | `server` | Stringa che rappresenta l’URL dell’endpoint di tracciamento sul backend. |
   | `publisher` | Stringa che rappresenta l’identificatore univoco dell’editore del contenuto. |
   | `channel` | Stringa che rappresenta il nome del canale di distribuzione del contenuto. |
   | `ssl` | Valore Boolean che indica se SSL deve essere utilizzato per il tracciamento delle chiamate. |
   | `ovp` | Stringa che rappresenta il nome del provider del lettore video. |
   | `sdkversion` | Stringa che rappresenta la versione corrente dell&#39;app/SDK. |
   | `playerName` | Stringa che rappresenta il nome del lettore. |


1. Configura l&#39;ID visitatore di Experience Cloud.

   Il servizio ID visitatore di Experience Cloud fornisce un ID visitatore universale nelle soluzioni Experience Cloud. Il servizio ID visitatore è richiesto da Video Heartbeat e altre integrazioni di Marketing Cloud.

   Verifica che la tua configurazione `ADBMobileConfig` contenga il tuo `marketingCloud` ID organizzazione.

   ```js
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   Gli ID organizzazione di Experience Cloud identificano in modo univoco ogni società cliente in Adobe Marketing Cloud e hanno un valore simile al seguente: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Assicurati di includere `@AdobeOrg`.

   Al termine della configurazione, viene generato un ID visitatore di Experience Cloud che viene incluso in tutti gli hit. Gli altri ID visitatore, come `custom` e `automatically-generated`, continuano a essere inviati con ogni hit.

   **Metodi del servizio ID visitatori di Experience Cloud**

   >[!TIP]
   >
   >Ad Experience Cloud, i metodi ID visitatore hanno il prefisso `visitor`.

   | Metodo | Descrizione |
   | --- | --- |
   | `getMarketingCloudID()` | Recupera l’ID visitatore Experience Cloud dal servizio ID visitatore.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Con l’ID visitatore Experience Cloud, puoi impostare ID cliente aggiuntivi da associare a ogni visitatore. L’API visitatore accetta più ID cliente per lo stesso visitatore e un identificatore del tipo di cliente per separare l’ambito dei diversi ID cliente. Questo metodo corrisponde a `setCustomerIDs()` nella libreria JavaScript.  Ad esempio: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |



<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
