---
title: Implementazione dei servizi di streaming media per Adobe Analytics o Customer Journey Analytics
description: Scopri i percorsi di implementazione per i servizi multimediali di streaming di Adobe.
uuid: null
feature: Streaming Media
role: User, Admin, Developer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
TQID: https://experienceleague.adobe.com/aFrxbzBLlf1ngetaM-GsNFXz6TUXi6Pic3quLVI297c
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c8add8f2-4250-4fd9-9cde-9707036c567did: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 522
ht-degree: 8%

---

# Implementazione dei servizi di streaming media per Adobe Analytics o Customer Journey Analytics

Esistono diversi modi per implementare Adobe Streaming Media Services. Per un confronto dettagliato dei dispositivi e delle piattaforme supportati per i metodi di implementazione descritti in questa pagina, vedere [Piattaforme e dispositivi supportati](/help/getting-started/supported-devices.md).

## Metodi di implementazione di Edge

Per tutti i nuovi clienti Adobe Analytics o Customer Journey Analytics, consigliamo di utilizzare Edge durante l’implementazione dei servizi di streaming multimediale.

I metodi di implementazione di Edge utilizzano il componente aggiuntivo Streaming Media Collection.

* **Media for Edge Network SDK / Estensione:** raccoglie dati dal Web, dai dispositivi iOS e Android o dai dispositivi Roku e li invia ad Edge Network. I dati possono quindi essere inviati a Customer Journey Analytics o Adobe Analytics.

  Per ulteriori informazioni su Media for Edge Network SDK / Extension, consulta [Implementare Streaming Media Collection utilizzando Edge Network](/help/implementation/edge/implementation-edge.md).

* **API Media Edge:** può essere personalizzata per raccogliere dati da qualsiasi dispositivo o formato (inclusi dispositivi mobili, web e over-the-top) e invia dati ad Edge Network. I dati possono quindi essere inviati a Customer Journey Analytics o Adobe Analytics.

  Per ulteriori informazioni sull&#39;API di Media Edge, consulta [Panoramica dell&#39;API di Media Edge](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/).

![Flusso di lavoro in CJA](assets/streaming-media-edge.png)

## Metodi di implementazione solo per Adobe Analytics

I metodi di implementazione di Edge descritti in precedenza sono consigliati sia per Customer Journey Analytics che per Adobe Analytics, in particolare per le nuove implementazioni.

Oltre ai metodi di implementazione di Edge, sono disponibili altri metodi di implementazione. Questi metodi di implementazione sono stati progettati per l’utilizzo con Adobe Analytics. Tuttavia, i clienti esistenti con uno dei seguenti metodi di implementazione possono comunque rendere disponibili i dati in Customer Journey Analytics creando una [connessione di origine Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=it).

I metodi di implementazione solo per Adobe Analytics utilizzano il componente aggiuntivo Adobe Analytics for Streaming Media.

* **Estensione Media con tag:** L&#39;estensione Adobe Media Analytics for Audio and Video fornisce la funzionalità per aggiungere l&#39;istanza di tracciamento Media a un sito o a un progetto abilitato per i tag. I dati vengono inviati ad Adobe Analytics.

  Per informazioni sull&#39;installazione, la configurazione e l&#39;implementazione dell&#39;estensione Media con i tag, consulta [Panoramica dell&#39;estensione Adobe Media Analytics (3.x SDK) for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html).

* **Media SDK:** Media SDK consente di misurare più piattaforme multimediali, tra cui siti Web, telefoni cellulari, TV connesse, tablet, dispositivi OTT, set-top box e console di gioco. Per ulteriori informazioni, vedere [Piattaforme e dispositivi supportati](/help/getting-started/supported-devices.md).

  I Media SDK utilizzano le API Media Collection per il tracciamento. I dati vengono inviati ad Adobe Analytics.

  Per informazioni sul download e l’installazione di Media SDK e delle estensioni, consulta [Ottenere Media SDK e le estensioni tramite tag e SDK OTT](/help/getting-started/download-sdks.md).

* **API Media Collection:** Poiché le API Media Collection sono personalizzabili, possono essere utilizzate per applicazioni che richiedono funzionalità di tracciamento personalizzate e per dispositivi non supportati da Media SDK. Le API Media Collection tengono traccia degli eventi audio e video utilizzando le chiamate HTTP RESTful. I dati vengono inviati ad Adobe Analytics.

  Per informazioni sull’utilizzo delle API Media Collection, consulta [API Media Collection](media-collection-api/mc-api-overview.md).


![Flusso di lavoro di Analytics](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
