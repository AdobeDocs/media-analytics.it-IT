---
title: Versione app
description: Configura la stringa di versione dell’applicazione lettore multimediale.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 2%

---


# Versione app

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **App version**. Vedi [Versione app](/help/reporting/dimensions/app-version.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile di versione dell’app identifica la versione dell’applicazione lettore multimediale. Impostalo una volta durante l’inizializzazione di SDK; il valore viene incluso automaticamente in ogni richiesta di avvio di sessione successiva. Utilizzare una stringa di versione corrispondente al ciclo di rilascio dell&#39;applicazione (ad esempio, `"2.1.0"` o `"prod-YYYY-03-15"`).

>[!NOTE]
>
>Questo campo acquisisce la versione dell&#39;**applicazione lettore multimediale**, non la libreria SDK di Adobe. La versione della libreria SDK di Adobe viene raccolta automaticamente come campo interno separato.

| Proprietà | Valore |
| --- | --- |
| **Campo raccolta XDM** | [`xdm.mediaCollection.sessionDetails.appVersion`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Parametro API Media Collection** | `media.sdkVersion` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md) |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `appVersion` nell&#39;oggetto di configurazione `streamingMedia` durante la chiamata a [`configure`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/streamingmedia):

```javascript
alloy("configure", {
  streamingMedia: {
    channel: "Sports Channel",
    playerName: "HTML5 Player",
    appVersion: "2.1.0",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

>[!TAB iOS]

Imposta `edgeMedia.appVersion` nella configurazione dell&#39;app prima di inizializzare il tracciatore multimediale:

```swift
var config: [String: Any] = [:]
config["edgeMedia.channel"] = "sample_channel"
config["edgeMedia.playerName"] = "player_name"
config["edgeMedia.appVersion"] = "2.1.0"
MobileCore.updateConfiguration(config)
```

>[!TAB Android]

Imposta `edgeMedia.appVersion` nella configurazione dell&#39;app prima di inizializzare il tracciatore multimediale:

```kotlin
val config: Map<String, Any> = mapOf(
    "edgeMedia.channel" to "sample_channel",
    "edgeMedia.playerName" to "player_name",
    "edgeMedia.appVersion" to "2.1.0"
)
MobileCore.updateConfiguration(config)
```

>[!TAB Edge Roku]

Impostare la versione dell&#39;app nella configurazione SDK utilizzando `ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION`:

```brightscript
ADB_CONSTANTS = AdobeAEPSDKConstants()
configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<YOUR_CONFIG_ID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "channel_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION] = "2.1.0"
m.aepSdk.updateConfiguration(configuration)
```

>[!TAB API Media Edge]

Includi `appVersion` nell&#39;oggetto `sessionDetails` della richiesta [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "appVersion": "2.1.0"
        },
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Imposta `appVersion` sull&#39;oggetto `MediaConfig` prima di chiamare `ADB.Media.configure`:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "2.1.0";
ADB.Media.configure(mediaConfig, appMeasurement);
```

>[!TAB Chromecast]

Impostare `sdkVersion` nella sezione `mediaHeartbeat` della configurazione ADBMobile. Questo campo acquisisce la versione dell’applicazione del lettore, non la versione della libreria SDK Chromecast.

```javascript
var ADBMobileConfig = {
  "mediaHeartbeat": {
    "server": "obumobile5.hb-api.omtrdc.net",
    "publisher": "<YOUR_PUBLISHER_ID>@AdobeOrg",
    "channel": "sample-channel",
    "ssl": true,
    "playerName": "Chromecast Player",
    "sdkVersion": "2.1.0"
  }
};
```

>[!TAB Roku 2.x]

Imposta `sdkVersion` nella sezione `mediaHeartbeat` di `ADBMobileConfig.json`. Questo campo acquisisce la versione dell’applicazione del lettore, non la versione della libreria SDK Roku 2.x:

```json
"mediaHeartbeat": {
  "sdkVersion": "2.1.0"
}
```

>[!TAB API Media Collection]

Includi `media.sdkVersion` nell&#39;oggetto `params` della richiesta POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "sample-html5-api-player",
    "media.sdkVersion": "2.1.0",
    "media.channel": "sample-channel"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).

>[!ENDTABS]
