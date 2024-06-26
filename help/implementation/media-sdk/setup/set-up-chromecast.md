---
title: Come configurare Media SDK per Chromecast
description: Segui questi passaggi per configurare l’applicazione Media SDK su Chromecast.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 97%

---

# Configurare Mobile SDK v3.x per Chromecast {#set-up-chromecast}

In questa sezione vengono descritti i prerequisiti per la configurazione di un&#39;installazione Chromecast per il componente aggiuntivo Streaming Media Collection.

## Prerequisiti

* **Ottenere parametri di configurazione validi**

  Questi parametri possono essere ottenuti da un rappresentante di Adobe dopo la configurazione dell’account di Media Analytics.
* **Includi le seguenti API nel lettore multimediale**

   * *API per abbonarsi agli eventi del lettore*: Media SDK richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni sul lettore* - Queste informazioni includono dettagli quali il nome del supporto e la posizione della testina di riproduzione.

Adobe Mobile Services fornisce una nuova interfaccia utente che riunisce le capacità mobile marketing per applicazioni per dispositivi mobili da Adobe Experience Cloud. Inizialmente, Mobile Services fornisce un’integrazione diretta delle funzionalità per analisi delle app e targeting per le soluzioni Adobe Analytics e Adobe Target. Maggiori informazioni nella [documentazione di Adobe Mobile Services.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=it)

La libreria mobile di Adobe per Chromecast v3.x per soluzioni Experience Cloud consente di misurare le applicazioni Chromecast scritte in JavaScript, sfruttare e raccogliere i dati sul pubblico tramite Gestione dell’audience e misurare l’interazione video.

## Implementazione della libreria mobile/SDK

1. Aggiungi la libreria Chromecast scaricata al progetto.

   1. Il file zip `AdobeMobileLibrary-Chromecast-[version]` è costituito dai seguenti componenti software:

      * `adbmobile-chromecast.min.js`:

        Questo file della libreria verrà incluso nella cartella di origine dell’app Chromecast.

      * File di configurazione `ADBMobileConfig`

        Questo file di configurazione dell’SDK è personalizzato per la tua app. Un esempio dell’implementazione `ADBMobileConfig` viene fornita con l’SDK (in `samples/`). Ottieni le impostazioni corrette da un rappresentante di Adobe.

   1. Aggiungi il file della libreria al tuo file `index.html` e crea la variabile globale `ADBMobileConfig` come segue (la variabile globale utilizzata per configurare Adobe Mobile per Media Analytics ha una chiave esclusiva denominata `mediaHeartbeat`):

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
              "rsids": "example.sample.player",
              "server": "example.sc.omtrc.net",
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
              "server": "example.hb-api.omtrdc.net",
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
      >se `mediaHeartbeat` non è configurato correttamente, il modulo multimediale entra in uno stato di errore e interrompe l’invio delle chiamate di tracciamento.

      Parametri di configurazione ADBMobile per la chiave mediaHeartbeat:

   | Parametro di configurazione | Descrizione     |
   | --- | --- |
   | `server` | Stringa che rappresenta l’URL dell’endpoint di tracciamento sul backend. |
   | `publisher` | Stringa che rappresenta l’identificatore univoco dell’editore del contenuto. |
   | `channel` | Stringa che rappresenta il nome del canale di distribuzione del contenuto. |
   | `ssl` | Valore booleano che indica se SSL deve essere utilizzato per il tracciamento delle chiamate. |
   | `ovp` | Stringa che rappresenta il nome del provider del lettore video. |
   | `sdkversion` | Stringa che rappresenta la versione corrente dell’app/SDK. |
   | `playerName` | Stringa che rappresenta il nome del lettore. |


1. ID visitatore di Experience Cloud.

   Il servizio ID visitatore Experience Cloud fornisce un ID visitatore universale per le soluzioni Experience Cloud. Il servizio ID visitatore è richiesto da Media Analytics e altre integrazioni di Marketing Cloud.

   Verifica che la configurazione `ADBMobileConfig` contenga il tuo ID organizzazione `marketingCloud`.

   ```
   "marketingCloud": {
       "org": "YOUR-MCORG-ID"
   }
   ```

   Gli ID organizzazione di Experience Cloud identificano in modo univoco ogni società cliente in Adobe Experience Cloud e hanno un valore simile al seguente: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Assicurati di includere `@AdobeOrg`.

   Quando la configurazione è completa, viene generato un ID visitatore Experience Cloud che viene incluso in tutti gli hit. Altri ID visitatori, come `custom` e `automatically-generated`, continuano a essere inviati con ciascun hit.

   **Metodi del servizio ID visitatore Experience Cloud**

   >[!TIP]
   >
   >I metodi ID visitatore di Experience Cloud hanno il prefisso `visitor`.

   | Metodo | Descrizione |
   | --- | --- |
   | `getMarketingCloudID()` | Recupera l’ID visitatore di Experience Cloud dal servizio ID visitatore. <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Insieme all’ID visitatore di Experience Cloud, puoi impostare altri ID cliente da associare a ogni visitatore. L’API visitatore accetta più ID cliente per lo stesso visitatore, con un identificatore del tipo di cliente che consente di distinguere l’ambito dei diversi ID cliente. Questo metodo corrisponde a `setCustomerIDs()` nella libreria JavaScript.  Ad esempio: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |

1. Per il tracciamento dei contenuti multimediali, implementa il protocollo MediaDelegate

   ```js
    var delegate = {
      // Replace <currentPlaybackTime> with the video player current playback time
      getCurrentPlaybackTime = function() {
        return <currentPlaybackTime>;
      },
      // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.
      getQoSObject = function() {
         return ADBMobile.media.createQoSObject(<bitrate>, <startupTime>, <fps>, <droppedFrames>);
      }
    }
   
    ADBMobile.media.setDelegate(delegate);
   }
   ```

<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
