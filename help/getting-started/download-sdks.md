---
title: Ottenere Media SDK, estensioni e API
description: Collegamenti ai download dell’SDK per le piattaforme disponibili, inclusi Android, iOS, JavaScript, Chromecast e Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: b18eab3deb3d15a08adf2f7ecf61d73235bbc6e5
workflow-type: tm+mt
source-wordcount: 575
ht-degree: 32%

---

# Ottenere Media SDK, estensioni e API

## Implementazioni di Edge (consigliato) {#edge-sdks}

Le implementazioni di Edge raccolgono i dati una volta e li distribuiscono tramite Adobe Experience Platform Edge Network a più destinazioni: Adobe Analytics, Customer Journey Analytics, Adobe Journey Optimizer e Real-Time CDP. Per le piattaforme senza un SDK nativo (come Smart TV, console di gioco e set-top box), utilizza l’API Media Edge.

| | Documentazione | Esempio |
|:---:|---|---|
| [![Icona JavaScript](assets/javascript-icon.png)](https://experienceleague.adobe.com/it/docs/experience-platform/web-sdk/install/overview)<br>[Web SDK](https://experienceleague.adobe.com/it/docs/experience-platform/web-sdk/install/overview) | [Configura Web SDK per Streaming Media](/help/implementation/edge/web-sdk.md) | [Esempio](https://github.com/adobe/alloy-samples/blob/main/media-collection/STANDALONE.md) |
| [![Icona estensione](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html)<br>[Estensione tag Web SDK](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html) | [Configurare l&#39;estensione tag Web SDK per Streaming Media](/help/implementation/edge/web-sdk-tags.md) | [Esempio](https://github.com/adobe/alloy-samples/blob/main/media-collection/TAGS_IMPL.md) |
| [![Icona Android](assets/android.png)](https://github.com/adobe/aepsdk-media-android)<br>[Android SDK](https://github.com/adobe/aepsdk-media-android) | [Configura Android per Streaming Media](/help/implementation/edge/android.md) | [Esempio](https://github.com/adobe/aepsdk-media-android/tree/main/code/testapp) |
| [![Icona Apple iOS](assets/apple.png)](https://github.com/adobe/aepsdk-media-ios)<br>[iOS / tvOS SDK](https://github.com/adobe/aepsdk-media-ios) | [Configura iOS per Streaming Media](/help/implementation/edge/ios.md) | [Esempio](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| [![Icona estensione](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[Estensione tag Android](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Configura l&#39;estensione tag Android per Streaming Media](/help/implementation/edge/android-tags.md) | |
| [![Icona estensione](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[Estensione tag iOS / tvOS](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Configura l&#39;estensione tag iOS per Streaming Media](/help/implementation/edge/ios-tags.md) | |
| [![Icona Roku](assets/roku-icon.png)](https://github.com/adobe/aepsdk-roku)<br>[SDK Roku](https://github.com/adobe/aepsdk-roku) | [Configura Roku per Streaming Media](/help/implementation/edge/roku.md) | [Esempio](https://github.com/adobe/aepsdk-roku/tree/main/sample/simple-videoplayer-channel) |
| [![Icona API](assets/api.png)](https://developer.adobe.com/data-collection-apis/docs/api/media-edge)<br>[API Media Edge](https://developer.adobe.com/data-collection-apis/docs/api/media-edge) | [Configura API Media Edge](/help/implementation/edge/media-edge-api.md) | [Esempio](https://developer.adobe.com/data-collection-apis/docs/getting-started/media-edge-examples) |

## Implementazioni solo per Analytics {#analytics-only-sdks}

Questi SDK ed estensioni inviano i dati direttamente ad Adobe Analytics. Per le nuove implementazioni, utilizza le implementazioni di Edge precedenti. Per inserire dati di Analytics esistenti in Customer Journey Analytics o in altre applicazioni Experience Platform, utilizza il [connettore di origine Analytics](https://experienceleague.adobe.com/it/docs/experience-platform/sources/connectors/adobe-applications/analytics).

| | Documentazione | Esempio |
|:---:|---|---|
| [![Icona JavaScript](assets/javascript-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2)<br>[Media SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Configura JavaScript per Streaming Media](/help/implementation/analytics-only/javascript.md) | [Esempio](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| [![Icona estensione](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=it)<br>[Estensione file multimediali](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=it) | [Configura JavaScript utilizzando i tag per i contenuti multimediali in streaming](/help/implementation/analytics-only/javascript-tags.md) | [Esempio](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| [![Icona Chromecast](assets/chromecast-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3)<br>[SDK Chromecast 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Configura Chromecast per contenuti multimediali in streaming](/help/implementation/analytics-only/chromecast.md) | [Esempio](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/chromecast/samples/BasicPlayerSample) |
| [![Icona API](assets/api.png)](/help/implementation/media-collection-api/mc-api-overview.md)<br>[API Media Collection](/help/implementation/media-collection-api/mc-api-overview.md) | [Configura API Media Collection](/help/implementation/analytics-only/media-collection-api.md) | |
