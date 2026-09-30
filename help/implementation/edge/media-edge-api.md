---
title: Configurare l’API di Media Edge per lo streaming di file multimediali
description: Invia dati multimediali in streaming direttamente a Edge Network utilizzando l’API di Media Edge.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%
---
# Configurare l’API di Media Edge per lo streaming di file multimediali

Se non è possibile utilizzare il SDK web, il SDK mobile o il SDK Roku Edge (ad esempio, in un runtime personalizzato o non supportato), puoi inviare dati multimediali in streaming direttamente all’Edge Network con l’API Media Edge. L’API utilizza chiamate HTTP RESTful ed è completamente personalizzabile.

* **Prerequisiti**: completa la [panoramica sull&#39;implementazione di Edge](overview.md) (schema, set di dati, flusso di dati con [!UICONTROL Media Analytics] abilitato).

## Inviare eventi multimediali ad Edge Network

Gli eventi multimediali vengono inviati agli endpoint `/ee/va/v1/`, inseriti nel flusso di dati dal parametro di query `configId`. Ad esempio, una sessione inizia con un POST su `sessionStart`:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId=<datastreamID>" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": { "name": "video-123", "playerName": "player_name", "contentType": "vod", "length": 128, "channel": "sample_channel" },
        "playhead": 0
      }
    }
  }]
}'
```

La risposta restituisce l’ID sessione che tutti gli eventi successivi devono includere. Per il set completo di endpoint, i formati di richiesta/risposta e le specifiche OpenAPI, vedi il [riferimento API di Media Edge](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/).

## Tracciare gli eventi multimediali

Per conoscere i payload esatti, consulta la scheda **API Media Edge** su ogni pagina [event](/help/implementation/events/overview.md) e [variable](/help/implementation/variables/overview.md).

## Passaggio successivo

Una volta completata l&#39;implementazione, puoi [Configurare la generazione di rapporti per le implementazioni di Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Riferimento API di Media Edge](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)
>* [Panoramica eventi](/help/implementation/events/overview.md)
>* [Panoramica delle variabili](/help/implementation/variables/overview.md)
