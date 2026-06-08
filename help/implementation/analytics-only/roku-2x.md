---
title: Configurare Roku 2.x per contenuti multimediali in streaming
description: Installa e configura Adobe Media SDK 2.x per Roku per implementazioni di contenuti multimediali in streaming solo per Analytics, inclusi i canali SceneGraph.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---

# Configurare Roku 2.x per contenuti multimediali in streaming

Adobe Media SDK 2.x per Roku (`adbmobile.brs`) invia i dati multimediali in streaming dai canali Roku scritti in BrightScript direttamente ad Adobe Analytics. Raccoglie inoltre dati sul pubblico tramite Audience Manager e misura il coinvolgimento attraverso gli eventi multimediali.

>[!NOTE]
>
>Questa pagina descrive Media SDK 2.x per Roku, disponibile solo in Analytics. Per le nuove implementazioni, Adobe consiglia l&#39;[Roku Edge SDK](/help/implementation/edge/roku.md), che rende i dati disponibili per Customer Journey Analytics, Adobe Journey Optimizer e Real-Time CDP oltre ad Adobe Analytics.

* **Prerequisiti**:
   * Completa la [Panoramica sull&#39;implementazione di sola Analytics](overview.md).
   * [Scarica Media SDK per Roku](/help/getting-started/download-sdks.md).
   * Includi un’API nel lettore multimediale per abbonarti agli eventi del lettore e un’API che fornisce informazioni sul lettore come il nome del file multimediale e la posizione della testina di riproduzione.

## Installare SDK

Il download di `AdobeMobileLibrary-2.*-Roku.zip` contiene due componenti:

* `adbmobile.brs`: il file di libreria. Copiarlo nella directory `pkg:/source/` del tuo canale.
* `ADBMobileConfig.json`: file di configurazione di SDK personalizzato per l&#39;app.

Per i canali di SceneGraph, copiare anche `adbmobileTask.brs` e `adbmobileTask.xml` nella directory `pkg:/components/`. Consulta [Supporto di SceneGraph](#scenegraph).

## Configurare ADBMobileConfig.json

Il JSON di configurazione ha una chiave `mediaHeartbeat` esclusiva per lo streaming multimediale. Aggiungi `ADBMobileConfig.json` all&#39;origine del progetto e imposta i valori `mediaHeartbeat`, `marketingCloud` e `analytics`:

```json
{
  "analytics": {
    "rsids": "your-report-suite-id",
    "server": "your-analytics-server"
  },
  "marketingCloud": {
    "org": "YOUR-MCORG-ID@AdobeOrg"
  },
  "mediaHeartbeat": {
    "server": "your-namespace.hb-api.omtrdc.net",
    "publisher": "your-publisher-id",
    "channel": "sample-channel",
    "ssl": true,
    "ovp": "sample-ovp",
    "sdkVersion": "sample-sdk",
    "playerName": "Roku Player"
  }
}
```

| Parametro di configurazione | Descrizione |
| --- | --- |
| `server` | URL dell’endpoint di tracciamento dei contenuti multimediali. Consulta la [Panoramica sull&#39;implementazione di sola Analytics](overview.md). |
| `publisher` | Identificatore univoco dell’editore del contenuto. |
| `channel` | Nome del canale di distribuzione del contenuto. Riportato come [Canale contenuto](/help/implementation/variables/core/content-channel.md). |
| `ssl` | Se SSL viene utilizzato per il tracciamento delle chiamate. |
| `ovp` | Nome del provider della piattaforma video online. |
| `sdkVersion` | Versione corrente dell’app o del SDK. |
| `playerName` | Nome del lettore. Segnalato come [Nome del lettore di contenuti](/help/implementation/variables/core/content-player-name.md). |

>[!IMPORTANT]
>
>Se `mediaHeartbeat` non è configurato correttamente, il modulo multimediale immette uno stato di errore e interrompe l&#39;invio di chiamate di tracciamento. Assicurarsi che il valore `marketingCloud.org` includa `@AdobeOrg`.

## Inizializzare SDK ed elaborare i messaggi

Ottieni un&#39;istanza di SDK con `ADBMobile()`. Il servizio ID visitatore di Experience Cloud genera un ID visitatore incluso in tutti gli hit.

>[!IMPORTANT]
>
>Chiama `processMessages` e `processMediaMessages` nel ciclo dell&#39;evento principale ogni 250 ms in modo che SDK invii i ping correttamente.

```brightscript
adb = ADBMobile()

' In your main event loop, every ~250 ms:
adb.processMessages()
adb.processMediaMessages()
```

| Metodo | Descrizione |
| --- | --- |
| `processMessages` | Passa gli eventi di Analytics in coda a SDK. |
| `processMediaMessages` | Passa gli eventi multimediali in coda al SDK, inclusi i ping automatici. |

## Tracciare gli eventi multimediali

Traccia ogni evento multimediale chiamando il relativo metodo SDK. Consulta la scheda **Roku 2.x** su ogni pagina [event](/help/implementation/events/overview.md) e [variable](/help/implementation/variables/overview.md) per informazioni sulle chiamate, i generatori e le costanti esatte.

Una sessione tipica inizia con la creazione di un oggetto multimediale e la chiamata a `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("Mr. Robot", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

contextData = { "a.media.show": "Mr. Robot" }

adb.mediaTrackSessionStart(mediaInfo, contextData)
```

I generatori di `adb_media_init_*` globali creano gli oggetti multimediali, ad, ad-break, chapter e QoS utilizzati dalle chiamate di tracciamento:

| Builder | Firma |
| --- | --- |
| Media | `adb_media_init_mediainfo(name, id, length, streamType, mediaType)` |
| Annuncio | `adb_media_init_adinfo(name, id, position, length)` |
| Interruzione pubblicitaria | `adb_media_init_adbreakinfo(name, startTime, position)` |
| Capitolo | `adb_media_init_chapterinfo(name, position, length, startTime)` |
| QoS | `adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)` |

I metadati standard vengono passati come array associativo di `a.media.*` chiavi (SDK definisce anche costanti denominate come `MEDIA_VideoMetadataKeySHOW` per queste chiavi). Consulta le pagine [Variabili](/help/implementation/variables/overview.md) per la chiave corrispondente a ciascuna dimensione.

## Configurare l’ID visitatore di Experience Cloud, la privacy e la registrazione

I metodi seguenti nell&#39;istanza `ADBMobile()` gestiscono l&#39;identità, la privacy e il debug:

| Metodo | Descrizione |
| --- | --- |
| `visitorMarketingCloudID()` | Recupera l&#39;Experience Cloud ID (ECID). |
| `visitorSyncIdentifiers(identifiers)` | Imposta ID cliente aggiuntivi per lo stesso visitatore. |
| `setAdvertisingIdentifier(rida)` | Imposta l&#39;ID Roku per Advertising (RIDA). Ottienila con l&#39;API Roku [`getRIDA()`](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic). |
| `getAllIdentifiers()` | Restituisce tutti gli identificatori memorizzati da SDK, inclusi Analytics, Visitatore, Audience Manager e identificatori personalizzati. |
| `setPrivacyStatus(status)` | Imposta lo stato di privacy. Passaggio `adb.PRIVACY_STATUS_OPT_IN` o `adb.PRIVACY_STATUS_OPT_OUT`. Vedi [Privacy](/help/implementation/opt-out-privacy.md). |
| `getPrivacyStatus()` | Restituisce lo stato di privacy corrente. |
| `setDebugLogging(flag)` | Abilita o disabilita la registrazione di debug. |
| `getDebugLogging()` | Restituisce `true` se la registrazione di debug è abilitata. |

## Supporto di SceneGraph {#scenegraph}

Il framework XML Roku SceneGraph non può chiamare direttamente le API legacy di SDK BrightScript perché SDK utilizza componenti (come i thread) che non sono disponibili per un’app SceneGraph. Per colmare questo gap, SDK fornisce un connettore che restituisce un’istanza compatibile con SceneGraph che espone le stesse API, oltre a un meccanismo di callback per le API che restituiscono dati.

Il ponte ha tre parti:

* **`adbmobileTask`nodo**: nodo attività SceneGraph che esegue API SDK su un thread in background e restituisce dati alle scene.
* **Istanza del connettore**: esegue il wrapping di tutte le API pubbliche legacy e comunica con il nodo `adbmobileTask`.
* Callback **`API_RESPONSE`**: campo osservato dall&#39;app per ricevere i valori restituiti dalle API getter.

Per inizializzare SDK in un canale SceneGraph:

1. Importa `adbmobile.brs` nella tua scena:

   ```brightscript
   <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
   ```

1. Crea il nodo `adbmobileTask`, ottieni l’istanza del connettore e carica le costanti SceneGraph:

   ```brightscript
   m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
   m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
   m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
   ```

1. Registra un callback per ricevere gli oggetti di risposta per le API che restituiscono dati:

   ```brightscript
   m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE, "onAdbmobileApiResponse")
   
   function onAdbmobileApiResponse() as void
       responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]
       if responseObject <> invalid
           methodName = responseObject.apiName
           retVal = responseObject.returnValue
           if methodName = m.adbmobileConstants.PRIVACY_STATUS
               print "Privacy status: " + retVal
           end if
       end if
   end function
   ```

L&#39;istanza del connettore (`m.adbmobile`) espone gli stessi metodi multimediali del SDK legacy (`mediaTrackSessionStart`, `mediaTrackPlay`, `mediaTrackPause`, `mediaTrackComplete`, `mediaTrackSessionEnd`, `mediaTrackError`, `mediaTrackEvent`, `mediaUpdatePlayhead` e `mediaUpdateQoS`) in modo che le chiamate visualizzate nelle pagine evento e variabile funzionino allo stesso modo. Le API di impostazione vengono chiamate direttamente; le API di getter restituiscono i loro valori tramite il callback `API_RESPONSE`.

## Passaggio successivo

Una volta completata l&#39;implementazione, puoi [Configurare la generazione di rapporti per le implementazioni solo Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Panoramica eventi](/help/implementation/events/overview.md)
>* [Panoramica delle variabili](/help/implementation/variables/overview.md)
>* [Roku Edge SDK](/help/implementation/edge/roku.md)
