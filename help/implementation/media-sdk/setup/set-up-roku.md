---
title: Come impostare SDK per contenuti multimediali per Roku
description: Segui questi passaggi per configurare l’applicazione SDK per contenuti multimediali su Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 92%

---

# Configurare Mobile SDK v2.x per Roku {#set-up-roku}

## Prerequisiti {#roku-prerequisites}

* **Ottieni parametri di configurazione validi per Adobe Streaming Media Services**

  Questi parametri possono essere ottenuti da un rappresentante di Adobe dopo la configurazione dell’account per il componente aggiuntivo Adobe Streaming Media Collection o Adobe Analytics for Streaming Media.

* **Includi le seguenti API nel lettore multimediale**

   * _API per abbonarsi agli eventi del lettore_: Media SDK richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * _API che fornisce informazioni sul lettore_ - Queste informazioni includono dettagli quali il nome del supporto e la posizione della testina di riproduzione.

Roku SDK 2.x per le soluzioni Experience Cloud consente di misurare le applicazioni Roku scritte in BrightScript, sfruttare e raccogliere i dati sul pubblico tramite la gestione del pubblico e misurare il coinvolgimento con contenuti video attraverso gli eventi video.

## Implementazione della libreria mobile/SDK

1. Aggiungi la Libreria Roku [scaricata](/help/getting-started/download-sdks.md) al tuo progetto.

   1. Il file di download `AdobeMobileLibrary-2.*-Roku.zip` è costituito dai seguenti componenti software:

      * `adbmobile.brs`: questo file libreria verrà incluso nella cartella di origine dell’app Roku.

      * `ADBMobileConfig.json`: file di configurazione dell’SDK personalizzato per la tua app.

   1. Aggiungi il file di libreria e il file di configurazione JSON alla tua origine del progetto.

      Il JSON utilizzato per configurare Adobe Mobile ha una chiave esclusiva per Media Analytics denominata `mediaHeartbeat`. Qui appartengono i parametri di configurazione per Media Analytics.

      >[!TIP]
      >
      >Un campione del file JSON `ADBMobileConfig` viene fornito con il pacchetto. Contatta i rappresentanti di Adobe per le impostazioni.

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
      | `ssl` | Valore booleano che indica se SSL deve essere utilizzato per il tracciamento delle chiamate. |
      | `ovp` | Stringa che rappresenta il nome del provider del lettore video. |
      | `sdkversion` | Stringa che rappresenta la versione corrente dell’app/SDK. |
      | `playerName` | Stringa che rappresenta il nome del lettore. |

      >[!IMPORTANT]
      >
      >Se `mediaHeartbeat` non è configurato correttamente, il modulo multimediale (VHL) immette uno stato di errore e interrompe l’invio di chiamate di tracciamento.

1. ID visitatore di Experience Cloud.

   Il servizio ID visitatore Experience Cloud fornisce un ID visitatore universale per le soluzioni Experience Cloud. Il servizio ID visitatore è richiesto da eventi video e altre integrazioni di Marketing Cloud.

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

   |  Metodo   | Descrizione |
   | --- | --- |
   | `visitorMarketingCloudID` | Recupera l’ID visitatore di Experience Cloud dal servizio ID visitatore. <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Insieme all’ID visitatore di Experience Cloud, puoi impostare altri ID cliente da associare a ogni visitatore. L’API visitatore accetta più ID cliente per lo stesso visitatore, con un identificatore del tipo di cliente che consente di distinguere l’ambito dei diversi ID cliente. Questo metodo corrisponde a `setCustomerIDs`. Ad esempio: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Utilizzato per impostare l’ID Roku per la pubblicità (RIDA) sull’SDK. Ad esempio: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Ottenere l’ID Roku per la pubblicità (RIDA) utilizzando l’API [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) dell’SDK Roku. |
   | `getAllIdentifiers` | Restituisce un elenco di tutti gli identificatori memorizzati dall’SDK, inclusi Analytics, visitatore, Audience Manager e identificatori personalizzati. <br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |

   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   **API pubbliche aggiuntive**

   **DebugLogging**

   |  Metodo   | Descrizione |
   | --- | --- |
   | `setDebugLogging` | Utilizzato per abilitare o disabilitare la registrazione di debug per l’SDK. <br/><br/>`ADBMobile().setDebugLogging(true)` |
   | `getDebugLogging` | Restituisce true se la registrazione di debug è abilitata. <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   **PrivacyStatus**

   |  Costante   | Descrizione |
   | --- | --- |
   | `PRIVACY_STATUS_OPT_IN` | Costante da passare con la chiamata setPrivacyStatus per il consenso. <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN` |
   | `PRIVACY_STATUS_OPT_OUT` | Costante da passare durante la chiamata setPrivacyStatus per la rinuncia. <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT` |

   |  Metodo   | Descrizione |
   | --- | --- |
   | `setPrivacyStatus` | Imposta lo stato di privacy sull’SDK. <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | Ottiene lo stato di privacy corrente impostato nell’SDK. <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   >[!IMPORTANT]
   >
   >Assicurati di chiamare le funzioni `processMessages` e `processMediaMessages` nel ciclo dell’evento principale ogni 250 ms per garantire che l’SDK invii correttamente i ping.

   |  Metodo   | Descrizione |
   | --- | --- |
   | `processMessages` | Responsabile del passaggio degli eventi di Analytics all’SDK da gestire. <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | Responsabile del passaggio degli eventi multimediali all’SDK da gestire. <br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html?lang=it) -->
