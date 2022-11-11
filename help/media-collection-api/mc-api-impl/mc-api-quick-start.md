---
title: “API Streaming Media Collection - Guida rapida”
description: Guida introduttiva all’API Streaming Media. Scopri come verificare rapidamente i dati della richiesta.
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 100%

---

# Guida introduttiva {#quick-start}

>[!TIP]
>
>Raccogliere i dati della richiesta necessari per completare una [Richiesta di sessione](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) al server back-end API di Media Analytics (MA) Collection. Puoi verificare rapidamente i dati della richiesta inviando manualmente le richieste (con `curl`, o Postman, ecc.). Questo ti darà un feedback immediato su eventuali problemi relativi a tipi di dati errati o informazioni errate nella tua richiesta. Utilizza gli [schemi di convalida JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) per verificare di aver fornito dati di richiesta corretti.

1. Raccogli i dati standard e richiesti di Adobe Analytics e Visitor da fornire per eseguire una qualsiasi delle applicazioni Experience Cloud:

   * ID visitatore organizzazione Experience Cloud
   * ID utente visitatore Experience Cloud
   * ID suite per report di Analytics
   * URL del server di tracciamento di Analytics

1. Creare un oggetto JSON per il corpo della richiesta delle `sessions`, contenente i dati minimi necessari per una chiamata di successo. Ad esempio:

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
   >Devi utilizzare i tipi di dati corretti nel corpo della richiesta JSON. Ad esempio, `analytics.enableSSL` richiede un valore booleano, `media.length` è numerico, ecc. Puoi controllare i tipi di parametri e i requisiti obbligatori rispetto a quelli facoltativi controllando [Schemi di convalida JSON.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. Invia richieste di sessioni all’endpoint API della raccolta MA. Se il payload della richiesta non è valido, identifica il problema e riprova fino a ottenere una risposta `201 Created`. In questo esempio `curl`, il corpo della richiesta JSON si trova in un file denominato `sample_data_session`:

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

Se la [Richiesta sessioni](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) viene eseguita correttamente, viene visualizzato una risposta `201 Created` simile a quella precedente. La risposta include un ID sessione nell’intestazione Posizione. L’ID sessione è la parte cruciale delle informazioni nella risposta, in quanto è richiesto per tutte le chiamate di tracciamento successive. Dopo il ritorno riuscito di una [Richiesta sessioni](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md), puoi procedere con l’implementazione del tracciamento video utilizzando l’API MA nel lettore video.
