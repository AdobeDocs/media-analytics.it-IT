---
title: Come impostare Media SDK per Roku
description: Segui questi passaggi per configurare l’applicazione Media SDK su Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 07192eca8bad89d005d88fa084ec891df346f96a
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 7%

---

# Configurazione Roku{#set-up-roku}

## Prerequisiti

* **Ottenere parametri di configurazione validi per Heartbeat**
Questi parametri possono essere ottenuti da un rappresentante di Adobe dopo la configurazione dell&#39;account media analytics.
* **Fornisci le seguenti funzionalità nel lettore multimediale:**
   * _Un’API per abbonarsi agli eventi del lettore_ - Media SDK richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * _API che fornisce informazioni sul lettore_ - Queste informazioni includono dettagli quali il nome del supporto e la posizione della testina di riproduzione.

Adobe Mobile Services fornisce una nuova interfaccia utente che riunisce le capacità mobile marketing per applicazioni mobile da Adobe Marketing Cloud. Inizialmente, Mobile Services fornisce un’integrazione perfetta delle funzionalità di analisi e targeting delle app per le soluzioni Adobe Analytics e Adobe Target.

Per saperne di più, consulta [Documentazione di Adobe Mobile Services .](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=it)

L’SDK 2.x Roku per le soluzioni di Experience Cloud consente di misurare le applicazioni Roku scritte in BrightScript, sfruttare e raccogliere i dati sul pubblico tramite la gestione dell’audience e misurare il coinvolgimento video attraverso gli heartbeat video.

## Implementazione SDK

1. Aggiungi il tuo [scaricato](/help/sdk-implement/download-sdks.md#download-2x-sdks) Libreria Roku al tuo progetto.

   1. La `AdobeMobileLibrary-2.*-Roku.zip` il file di download è costituito dai seguenti componenti software:

      * `adbmobile.brs`: Questo file libreria verrà incluso nella cartella di origine dell’app Roku.

      * `ADBMobileConfig.json`: Questo file di configurazione SDK è personalizzato per la tua app.
   1. Aggiungi il file di libreria e il file di configurazione JSON alla tua origine del progetto.

      Il JSON utilizzato per configurare Adobe Mobile ha una chiave esclusiva per gli heartbeat multimediali denominati `mediaHeartbeat`. Qui appartengono i parametri di configurazione per gli heartbeat multimediali.

      >[!TIP]
      >
      >Un campione `ADBMobileConfig` Il file JSON viene fornito con il pacchetto. Contatta i rappresentanti di Adobe per le impostazioni.

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
      >Se `mediaHeartbeat` non è configurato correttamente, il modulo multimediale (VHL) immette uno stato di errore e interrompe l’invio di chiamate di tracciamento.


1. Configura l&#39;ID visitatore di Experience Cloud.

   Il servizio ID visitatore di Experience Cloud fornisce un ID visitatore universale nelle soluzioni Experience Cloud. Il servizio ID visitatore è richiesto da Video Heartbeat e altre integrazioni di Marketing Cloud.

   Verifica che la tua `ADBMobileConfig` La configurazione contiene `marketingCloud` ID organizzazione.

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   Gli ID organizzazione di Experience Cloud identificano in modo univoco ogni società cliente in Adobe Marketing Cloud e hanno un valore simile al seguente: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Assicurati di includere `@AdobeOrg`.

   Al termine della configurazione, viene generato un ID visitatore di Experience Cloud che viene incluso in tutti gli hit. Altri ID visitatore, ad esempio `custom` e `automatically-generated`, continua a essere inviato con ogni hit.

   **Metodi del servizio ID visitatori di Experience Cloud**

   >[!TIP]
   >
   >Ad Experience Cloud, i metodi ID visitatore hanno il prefisso `visitor`.

   |  Metodo   | Descrizione |
   | --- | --- |
   | `visitorMarketingCloudID` | Recupera l&#39;ID visitatore Experience Cloud dal servizio ID visitatore.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Con l’ID visitatore Experience Cloud, puoi impostare ID cliente aggiuntivi da associare a ogni visitatore. L’API visitatore accetta più ID cliente per lo stesso visitatore e un identificatore del tipo di cliente per separare l’ambito dei diversi ID cliente. Questo metodo corrisponde a `setCustomerIDs`. Ad esempio: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Utilizzato per impostare l’ID Roku per la pubblicità (RIDA) sull’SDK. Ad esempio: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Ottenere l&#39;ID Roku per la pubblicità (RIDA) utilizzando l&#39;SDK Roku [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API. |
   | `getAllIdentifiers` | Restituisce un elenco di tutti gli identificatori memorizzati dall&#39;SDK, inclusi Analytics, Visitor, Audience Manager e custom Identifiers. <br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |
   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   **API pubbliche aggiuntive**

   **DebugLogging**

   |  Metodo   | Descrizione |
   | --- | --- |
   | `setDebugLogging` | Utilizzato per abilitare o disabilitare la registrazione di debug per l&#39;SDK.  <br/><br/>`ADBMobile().setDebugLogging(true)` |
   | `getDebugLogging` | Restituisce true se la registrazione di debug è abilitata.  <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   **PrivacyStatus**

   |  Costante   | Descrizione |
   | --- | --- |
   | `PRIVACY_STATUS_OPT_IN` | Costante da passare quando si chiama setPrivacyStatus per l&#39;opt-in. <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN` |
   | `PRIVACY_STATUS_OPT_OUT` | Costante da passare durante la chiamata di setPrivacyStatus per la rinuncia. <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT` |

   |  Metodo   | Descrizione |
   | --- | --- |
   | `setPrivacyStatus` | Imposta lo stato di privacy sull&#39;SDK.  <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | Ottiene lo stato di privacy corrente impostato nell&#39;SDK.  <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   >[!IMPORTANT]
   >
   >Assicurati di chiamare `processMessages` e `processMediaMessages` funziona nel ciclo eventi principale ogni 250 ms per garantire che l&#39;SDK invii correttamente i ping.

   |  Metodo   | Descrizione |
   | --- | --- |
   | `processMessages` | Responsabile del passaggio degli eventi di Analytics all&#39;SDK da gestire.  <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | Responsabile del passaggio degli eventi multimediali all’SDK da gestire. <br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
