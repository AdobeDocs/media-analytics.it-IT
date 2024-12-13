---
title: Implementare Streaming Media Collection
description: Scopri i percorsi di implementazione per Streaming Media Collection.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 7%

---

# Implementare Streaming Media Collection

Esistono diversi modi per implementare Adobe Streaming Media Collection. Per un confronto dettagliato dei dispositivi e delle piattaforme supportati per i metodi di implementazione descritti in questa pagina, vedere [Piattaforme e dispositivi supportati](/help/getting-started/supported-devices.md).

## Metodi di implementazione di Edge

Per tutti i nuovi clienti di Adobe Analytics o di Customer Journey Analytics, consigliamo di utilizzare Edge durante l’implementazione di Streaming Media Collection.

* **Media per Edge Network SDK / Estensione:** Raccoglie dati dal Web, dai dispositivi iOS e Android o dai dispositivi Roku e li invia ad Edge Network. I dati possono quindi essere inviati a Customer Journey Analytics o Adobe Analytics.

  Per ulteriori informazioni sui file multimediali, ad Edge Network SDK/Estensione, vedere [Implementare la raccolta multimediale in streaming utilizzando l&#39;Edge Network](/help/implementation/edge/implementation-edge.md).

* **API Media Edge:** può essere personalizzata per raccogliere dati da qualsiasi dispositivo o formato (inclusi dispositivi mobili, web e over-the-top) e invia dati ad Edge Network. I dati possono quindi essere inviati a Customer Journey Analytics o Adobe Analytics.

  Per ulteriori informazioni sull&#39;API di Media Edge, consulta [Panoramica dell&#39;API di Media Edge](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/).

![Flusso di lavoro in CJA](assets/streaming-media-edge.png)

## Metodi di implementazione solo per Adobe Analytics

I metodi di implementazione di Edge descritti in precedenza sono consigliati sia per il Customer Journey Analytics che per Adobe Analytics, in particolare per le nuove implementazioni.

Oltre ai metodi di implementazione di Edge, sono disponibili altri metodi di implementazione. Questi metodi di implementazione sono stati progettati per l’utilizzo con Adobe Analytics. Tuttavia, i clienti esistenti con uno dei seguenti metodi di implementazione possono comunque rendere disponibili i dati nel Customer Journey Analytics creando una [connessione di origine Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=it).

* **Estensione Media con tag:** L&#39;estensione Adobe Medium Analytics for Audio and Video fornisce la funzionalità necessaria per aggiungere l&#39;istanza di tracciamento Media a un sito o a un progetto abilitato per i tag. I dati vengono inviati ad Adobe Analytics.

  Per informazioni sull&#39;installazione, la configurazione e l&#39;implementazione dell&#39;estensione Media con i tag, consulta [Panoramica dell&#39;estensione Analytics (3.x SDK) for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html) di Adobe Medium Analytics.

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
