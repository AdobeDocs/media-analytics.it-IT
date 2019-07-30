---
seo-title: Avvio rapido
title: Avvio rapido
uuid: ca 20 bad 4-2 c 8 f -406 b -833 e-b 4883 a 9 aa 534
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Quick start{#quick-start}

>[!TIP]
>
>Gather the request data necessary for completing a successful [Session request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) to the Media Analytics (MA) Collection API back-end server. You can quickly verify your request data by sending requests manually (with `curl`, or Postman, etc.). Questo vi fornirà un feedback immediato sulla presenza di problemi con tipi di dati errati o su informazioni errate nella richiesta. Use the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) to verify that you are supplying proper request data.

1. Raccogli lo standard, i dati Adobe Analytics e i dati visitatore richiesti per eseguire una qualsiasi delle applicazioni Experience Cloud:

   * ID organizzazione Experience Cloud per visitatore
   * ID utente di Experience Cloud
   * ID suite di rapporti di Analytics
   * URL del server di tracciamento di Analytics

1. Create a JSON object for your `sessions` request body, containing the minimum data required for a successful call. Ad esempio:

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
   >Devi utilizzare i tipi di dati corretti nel corpo della richiesta JSON. E.g., `analytics.enableSSL` requires a boolean, `media.length` is numeric, etc. You can check parameter types and mandatory versus optional requirements by checking the [JSON validation schemas.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. Inviate le richieste sessioni all'endpoint API raccolta. If your request payload is invalid, identify the problem and retry until you get a `201 Created` response. In this `curl` example, the JSON request body is in a file named `sample_data_session`:

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

If the [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) succeeds, you receive a `201 Created` response similar to the one above. La risposta include un ID sessione nell'intestazione Posizione. L'ID sessione è l'elemento fondamentale della risposta, in quanto è richiesto per tutte le chiamate di tracciamento successive. After a successful return of a [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md), you can confidently proceed with implementing video tracking using the MA API in your video player.
