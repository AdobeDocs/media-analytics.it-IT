---
title: Configurare il Web SDK per lo streaming di file multimediali
description: Configura Adobe Experience Platform Web SDK (alloy.js) per inviare dati multimediali in streaming ad Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# Configurare il Web SDK per lo streaming di file multimediali

Il componente `streamingMedia` di Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview) (`alloy.js`, versione 2.20.0 o successiva) raccoglie i dati della sessione multimediale sul sito Web e li invia ad Edge Network. Questa pagina descrive la configurazione nel codice (`alloy.js`). Per configurare il Web SDK tramite i tag, vedere [Configurare l&#39;estensione tag Web SDK per lo streaming di file multimediali](web-sdk-tags.md).

* **Prerequisiti**:
   * Completa la [Panoramica sull&#39;implementazione di Edge](overview.md) (schema, set di dati, flusso di dati con [!UICONTROL Media Analytics] abilitato).
   * Installare Web SDK 2.20.0 o versione successiva. Vedere [Installare Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/install/overview).

## Configurare il componente streamingMedia

Aggiungere il componente `streamingMedia` alla configurazione `alloy`:

```js
alloy("configure", {
  edgeConfigId: "<datastreamID>",
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

Per informazioni dettagliate sulla configurazione, vedere il comando [`streamingMedia`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/streamingmedia).

### Migrazione da Media JS SDK

Se ti stai spostando da Media JS (3.x) SDK, il comando Web SDK [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/getmediaanalyticstracker) restituisce un&#39;istanza di tracciamento che espone le stesse API di [3.x Media SDK](/help/implementation/analytics-only/javascript.md), in modo che le chiamate di tracciamento esistenti continuino a funzionare.

## Tracciare gli eventi multimediali

Con il SDK configurato, inviare ogni evento multimediale chiamando [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview). Per conoscere i payload esatti, consulta la scheda **Web SDK** su ogni pagina [event](/help/implementation/events/overview.md) e [variable](/help/implementation/variables/overview.md).

## Passaggio successivo

Una volta completata l&#39;implementazione, puoi [Configurare la generazione di rapporti per le implementazioni di Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Panoramica di Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview)
>* [Panoramica eventi](/help/implementation/events/overview.md)
>* [Panoramica delle variabili](/help/implementation/variables/overview.md)
