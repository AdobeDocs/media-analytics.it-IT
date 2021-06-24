---
title: Come impostare il Media SDK per Roku
description: Segui questi passaggi per configurare l’applicazione Media SDK su Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 5%

---

# Configurazione Roku{#set-up-roku}

## Prerequisiti

* **Ottieni parametri di configurazione validi per**
HeartbeatQuesti parametri possono essere ottenuti da un rappresentante di Adobe dopo aver configurato il tuo account media analytics.
* **Fornisci le seguenti funzionalità nel lettore multimediale:**
   * _Un’API per abbonarti agli eventi_  del lettore: l’SDK per contenuti multimediali richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * _API che fornisce informazioni_  sul lettore. Queste informazioni includono dettagli quali il nome del contenuto multimediale e la posizione della testina di riproduzione.

Adobe Mobile Services fornisce una nuova interfaccia utente che riunisce le capacità mobile marketing per applicazioni mobile da Adobe Marketing Cloud. Inizialmente, Mobile Services fornisce un’integrazione perfetta delle funzionalità di analisi e targeting delle app per le soluzioni Adobe Analytics e Adobe Target.

Per ulteriori informazioni, consulta la [documentazione Adobe Mobile Services .](https://experienceleague.adobe.com/docs/mobile-services/using/home.html)

L’SDK 2.x Roku per le soluzioni di Experience Cloud consente di misurare le applicazioni Roku scritte in BrightScript, sfruttare e raccogliere i dati sul pubblico tramite la gestione dell’audience e misurare il coinvolgimento video attraverso gli heartbeat video.

## Implementazione SDK

1. Aggiungi la libreria Roku [scaricata](/help/sdk-implement/download-sdks.md#download-2x-sdks) al tuo progetto.

   1. Il file di download `AdobeMobileLibrary-2.*-Roku.zip` è costituito dai seguenti componenti software:

      * `adbmobile.brs`: Questo file libreria verrà incluso nella cartella di origine dell’app Roku.

      * `ADBMobileConfig.json`: Questo file di configurazione SDK è personalizzato per la tua app.
   1. Aggiungi il file di libreria e il file di configurazione JSON alla tua origine del progetto.

      Il JSON utilizzato per configurare Adobe Mobile ha una chiave esclusiva per gli heartbeat multimediali chiamati `mediaHeartbeat`. Qui appartengono i parametri di configurazione per gli heartbeat multimediali.

      >[!TIP]
      >
      >Il pacchetto fornisce un file JSON di esempio `ADBMobileConfig` . Contatta i rappresentanti di Adobe per le impostazioni.

      Ad esempio:

      ```
      {
        "version":"1.0",
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8",
          "ssl":true,
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
         "ssl":true,
         "ovp":"sample-ovp",
         "sdkVersion":"sample-sdk",
         "playerName":"roku"
         }    
      }
      ```

      | Parametro di configurazione | Descrizione     |
      | --- | --- |
      | `server` | Stringa che rappresenta l’URL dell’endpoint di tracciamento sul backend. |
      | `publisher` | Stringa che rappresenta l’identificatore univoco dell’editore del contenuto. |
      | `channel` | Stringa che rappresenta il nome del canale di distribuzione del contenuto. |
      | `ssl` | Valore Boolean che indica se SSL deve essere utilizzato per il tracciamento delle chiamate. |
      | `ovp` | Stringa che rappresenta il nome del provider del lettore video. |
      | `sdkversion` | Stringa che rappresenta la versione corrente dell&#39;app/SDK. |
      | `playerName` | Stringa che rappresenta il nome del lettore. |

      >[!IMPORTANT]
      >
      >Se `mediaHeartbeat` non è configurato correttamente, il modulo multimediale (VHL) immette uno stato di errore e smetterà di inviare chiamate di tracciamento.


1. Configura l&#39;ID visitatore di Experience Cloud.

   Il servizio ID visitatore di Experience Cloud fornisce un ID visitatore universale nelle soluzioni Experience Cloud. Il servizio ID visitatore è richiesto da Video Heartbeat e altre integrazioni di Marketing Cloud.

   Verifica che la tua configurazione `ADBMobileConfig` contenga il tuo `marketingCloud` ID organizzazione.

   ```
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

   |  Metodo   | Descrizione |
   | --- | --- |
   | `visitorMarketingCloudID` | Recupera l&#39;ID visitatore Experience Cloud dal servizio ID visitatore.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Con l’ID visitatore Experience Cloud, puoi impostare ID cliente aggiuntivi da associare a ogni visitatore. L’API visitatore accetta più ID cliente per lo stesso visitatore e un identificatore del tipo di cliente per separare l’ambito dei diversi ID cliente. Questo metodo corrisponde a `setCustomerIDs`. Ad esempio: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Utilizzato per impostare l’ID Roku per la pubblicità (RIDA) sull’SDK. Ad esempio: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Ottieni l&#39;ID Roku per la pubblicità (RIDA) utilizzando l&#39;API Roku SDK  [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) . |
   | `getAllIdentifiers` | Restituisce un elenco di tutti gli identificatori memorizzati dall&#39;SDK, inclusi Analytics, Visitor, Audience Manager e custom Identifiers. <br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |
   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   <br/><br/>

   **API pubbliche aggiuntive**

   **DebugLogging**
|, metodo   | Descrizione | | — | — | |  `setDebugLogging` | Utilizzato per abilitare o disabilitare la registrazione di debug per l&#39;SDK.  <br/><br/>`ADBMobile().setDebugLogging(true)` | |  `getDebugLogging` | Restituisce true se la registrazione di debug è abilitata.   <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   <br/><br/>

   **PrivacyStatus**
| Costante   | Descrizione | | — | — | |  `PRIVACY_STATUS_OPT_IN` | Costante da passare quando si chiama setPrivacyStatus per l’opzione di consenso. <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN`| |  `PRIVACY_STATUS_OPT_OUT` | Costante da passare quando si richiama setPrivacyStatus per la rinuncia.  <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT`|

   <br/>

   |  Metodo   | Descrizione |
   | --- | --- |
   | `setPrivacyStatus` | Imposta lo stato di privacy sull&#39;SDK. <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | Ottiene lo stato di privacy corrente impostato sull&#39;SDK. <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   <br/><br/>
   >[!IMPORTANT]
   >
   >Assicurati di chiamare la funzione `processMessages` e `processMediaMessages` nel ciclo di eventi principale ogni 250 ms per assicurarti che l&#39;SDK invii correttamente i ping.

   |  Metodo   | Descrizione |
   | --- | --- |
   | `processMessages` | Responsabile del passaggio degli eventi di Analytics all&#39;SDK da gestire.  <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | Responsabile del passaggio degli eventi multimediali all’SDK da gestire. <br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
