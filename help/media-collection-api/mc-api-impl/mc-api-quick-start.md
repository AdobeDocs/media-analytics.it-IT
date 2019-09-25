---
seo-title: Avvio rapido
title: Avvio rapido
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Quick start{#quick-start}

>[!TIP]
>
>Raccogli i dati della richiesta necessari per completare la richiesta [di](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) sessione con esito positivo al server back-end API di Media Analytics (MA) Collection. Potete verificare rapidamente i dati della richiesta inviando manualmente le richieste (tramite `curl`, o Postman, ecc.). Questo ti darà un feedback immediato se hai dei problemi con tipi di dati errati o informazioni errate nella tua richiesta. Utilizzate gli schemi [di convalida](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) JSON per verificare di fornire dati di richiesta corretti.

1. Raccogliere i dati standard e richiesti di Adobe Analytics e dei visitatori da fornire per eseguire una qualsiasi delle applicazioni Experience Cloud:

   * ID organizzazione Experience Cloud per visitatori
   * ID utente Experience Cloud visitatori
   * ID suite di rapporti di Analytics
   * URL del server di tracciamento Analytics

1. Create un oggetto JSON per il corpo della `sessions` richiesta, contenente i dati minimi richiesti per una chiamata riuscita. Ad esempio:

   ```
   { 
       "playerTime": { 
           "playhead": 0, 
           "ts": 1234560890123 
       }, 
       "eventType": "sessionStart", 
       "params": { 
           "media.playerName": "sample-html5-api-player", 
           "analytics.trackingServer": "[YOUR_TS]", 
           "analytics.reportSuite": "[YOUR_RSID]", 
           "media.contentType": "VOD", 
           "media.length": 60.39333333333333, 
           "media.id": "MA Collection API Sample Player", 
           "visitor.marketingCloudOrgId": "[YOUR_ORG_ID]", 
           "visitor.marketingCloudUserId": "[YOUR_ECID]",
           "media.name": "ClickMe", 
           "media.channel": "sample-channel", 
           "media.sdkVersion": "va-api-0.0.0", 
           "analytics.enableSSL": false 
       } 
   }
   ```

   >[!NOTE]
   >
   >Devi usare i tipi di dati corretti nel corpo della richiesta JSON. Ad esempio, `analytics.enableSSL` richiede un valore booleano, `media.length` è numerico, ecc. È possibile controllare i tipi di parametri e i requisiti obbligatori e facoltativi controllando gli schemi di convalida [JSON.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. Inviare le richieste di sessioni all'endpoint API della raccolta MA. Se il payload della richiesta non è valido, identificate il problema e riprovate fino a ottenere una `201 Created` risposta. In questo `curl` esempio, il corpo della richiesta JSON si trova in un file denominato `sample_data_session`:

   ```
   $ curl -i -d \ 
     @sample_data_session https://{uri}/api/v1/sessions \ 
     > curl.sessions.out 
   
   $ cat curl.sessions.out 
   HTTP/1.1 201 Created 
   Server: nginx/1.13.5 
   Date: Mon, 18 Dec 2017 22:34:12 GMT 
   Content-Type: application/octet-stream 
   Content-Length: 0 
   Connection: keep-alive 
   Location: /api/v1/sessions/a39c037641f[...]  # <== Session ID  
   Access-Control-Allow-Origin: * 
   Access-Control-Allow-Methods: OPTIONS,POST,PUT 
   Access-Control-Allow-Headers: Content-Type 
   Access-Control-Expose-Headers: Location
   ```

Se la richiesta [](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Sessioni ha esito positivo, riceverete una `201 Created` risposta simile a quella precedente. La risposta include un ID sessione nell’intestazione Posizione. L’ID sessione è il elemento fondamentale delle informazioni nella risposta, in quanto è richiesto per tutte le chiamate di tracciamento successive. Dopo il ritorno corretto di una richiesta [di](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)sessioni, potete procedere con l'implementazione del tracciamento video mediante l'API MA nel lettore video.
