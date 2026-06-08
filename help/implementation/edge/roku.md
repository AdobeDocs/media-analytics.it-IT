---
title: Configurare Roku Edge per lo streaming di file multimediali
description: Configura Adobe Experience Platform Roku SDK per inviare i dati multimediali in streaming ad Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Configurare Roku Edge per lo streaming di file multimediali

[Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku) (BrightScript) raccoglie i dati della sessione multimediale nel tuo canale Roku e li invia ad Edge Network. Roku è configurato nel codice; non utilizza i tag.

* **Prerequisiti**:
   * Completa la [Panoramica sull&#39;implementazione di Edge](overview.md) (schema, set di dati, flusso di dati con [!UICONTROL Media Analytics] abilitato).
   * Scarica il SDK dalle [versioni di GitHub](https://github.com/adobe/aepsdk-roku/releases) e aggiungilo al tuo canale, come descritto nella [guida introduttiva](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/getting-started.md).

## Configurare Roku Edge SDK per i file multimediali

Inizializza SDK e imposta la configurazione dello stream di dati e dei file multimediali:

```brightscript
m.aepSdk = AdobeAEPSDKInit()
ADB_CONSTANTS = AdobeAEPSDKConstants()

configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<datastreamID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "sample_channel"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
m.aepSdk.updateConfiguration(configuration)
```

Quindi apri una sessione con `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": { "name": "video-123", "length": 128, "contentType": "vod", "streamType": "video" },
            "playhead": 0
        }
    }
})
```

>[!IMPORTANT]
>
>Invia un evento `media.ping` almeno una volta al secondo con il valore della testina di riproduzione più recente durante la riproduzione. Il SDK di Roku Edge si basa su questi ping per funzionare correttamente.

Per le chiavi di configurazione e l&#39;API completa, vedere il riferimento API [Roku Edge SDK](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/api-reference.md).

## Tracciare gli eventi multimediali

Dopo l&#39;apertura della sessione, inviare ogni evento multimediale con `sendMediaEvent`. Per conoscere i payload esatti, consulta la scheda **Roku Edge** su ogni pagina [event](/help/implementation/events/overview.md) e [variable](/help/implementation/variables/overview.md).

## Passaggio successivo

Una volta completata l&#39;implementazione, puoi [Configurare la generazione di rapporti per le implementazioni di Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [SDK Adobe Experience Platform Roku](https://github.com/adobe/aepsdk-roku)
>* [Panoramica eventi](/help/implementation/events/overview.md)
>* [Panoramica delle variabili](/help/implementation/variables/overview.md)
