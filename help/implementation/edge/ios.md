---
title: Configurare iOS per lo streaming dei contenuti multimediali
description: Configura Adobe Experience Platform Mobile SDK su iOS per inviare dati multimediali in streaming ad Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Configurare iOS per lo streaming dei contenuti multimediali

L&#39;estensione Adobe Streaming Media for Edge Network (`AEPEdgeMedia`) raccoglie i dati della sessione multimediale nell&#39;app iOS o tvOS e li invia ad Edge Network. Questa pagina descrive la configurazione nel codice. Per configurare SDK tramite una proprietà mobile Tag, vedere [Configurare iOS per lo streaming di file multimediali con Tag](ios-tags.md).

* **Prerequisiti**:
   * Completa la [Panoramica sull&#39;implementazione di Edge](overview.md) (schema, set di dati, flusso di dati con [!UICONTROL Media Analytics] abilitato).
   * Aggiungi le estensioni `AEPCore`, `AEPEdge`, `AEPEdgeIdentity` e `AEPEdgeMedia` all&#39;app. Consulta [Adobe Streaming Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/) per l&#39;installazione e la registrazione.

## Configurare i file multimediali per iOS

Impostare le chiavi di configurazione del supporto quando si inizializza SDK:

```swift
let configuration = [
  "edgeMedia.channel": "sample_channel",
  "edgeMedia.playerName": "player_name",
  "edgeMedia.appVersion": "app_version"
]
MobileCore.updateConfiguration(configuration)
```

Quindi crea un tracker per gestire una sessione multimediale:

```swift
let tracker = Media.createTracker()
```

Per le chiavi di configurazione e l&#39;API di tracciamento completa, vedi il riferimento API [Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/).

## Tracciare gli eventi multimediali

Una volta creato il tracciatore, tieni traccia di ogni evento multimediale utilizzando il relativo metodo di tracciamento. Per le chiamate esatte, vedi la scheda **iOS** su ogni pagina [event](/help/implementation/events/overview.md) e [variable](/help/implementation/variables/overview.md).

## Passaggio successivo

Una volta completata l&#39;implementazione, puoi [Configurare la generazione di rapporti per le implementazioni di Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Contenuti multimediali in streaming Adobe per Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Configura iOS per Streaming Media con Tag](ios-tags.md)
>* [Panoramica eventi](/help/implementation/events/overview.md)
