---
title: Implementazione di contenuti multimediali in streaming per Adobe Analytics o Customer Journey Analytics
description: Informazioni sui percorsi di implementazione di Streaming Media.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: a26e4e283646e5ceb352f357789748f376f5c747
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 13%

---

# Implementazione di Streaming Media per Adobe Analytics o CUSTOMER JOURNEY ANALYTICS

Esistono diversi modi per implementare Streaming Media. Per un confronto dettagliato dei dispositivi e delle piattaforme supportati per i metodi di implementazione descritti in questa pagina, vedi [Piattaforme e dispositivi supportati](/help/getting-started/supported-devices.md).

## Metodi di implementazione Edge

È consigliabile utilizzare Edge durante l’implementazione di Media Analytics per tutti i nuovi clienti Adobe Analytics o Customer Journey Analytics.

* **Media for Edge Network SDK/Estensione:** Raccoglie dati dai dispositivi iOS e Android e li invia a Edge. I dati possono quindi essere inviati a Customer Journey Analytics o Adobe Analytics.

  Per ulteriori informazioni su Media for Edge Network SDK/Estensione, consulta [Installare Media Analytics con Experience Platform Edge](/help/implementation/edge/implementation-edge.md).

  >[!NOTE]
  >
  >Questo metodo di implementazione non supporta attualmente Web SDK o Roku. Tuttavia, entrambi sono supportati quando si implementano con l’API Media Edge.

* **API Media Edge:** Può essere personalizzato per raccogliere dati da qualsiasi dispositivo o formato (inclusi dispositivi mobili, web e over-the-top) e invia dati a Edge. I dati possono quindi essere inviati a Customer Journey Analytics o Adobe Analytics.

  <!-- For more information about the Media Edge API, see (link to John's docs when they're ready) -->

![Flusso di lavoro in CJA](assets/cja-implementation.png)

## Metodi di implementazione solo per Adobe Analytics

I metodi di implementazione Edge descritti in precedenza sono consigliati sia per il Customer Journey Analytics che per Adobe Analytics, in particolare per le nuove implementazioni.

Oltre ai metodi di implementazione di Edge, sono disponibili altri metodi di implementazione. Questi metodi di implementazione sono stati progettati per l’utilizzo con Adobe Analytics. Tuttavia, i clienti esistenti con uno dei seguenti metodi di implementazione possono ancora rendere disponibili i dati nel Customer Journey Analytics creando un [Connessione sorgente Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=it).

* **Estensione multimediale con tag:** L’estensione Adobe Medium Analytics for Audio and Video fornisce la funzionalità per aggiungere l’istanza di tracciamento Media a un sito o a un progetto abilitato per i tag. I dati vengono inviati ad Adobe Analytics.

  Per informazioni sull’installazione, la configurazione e l’implementazione di Media Extension con i tag, consulta [Panoramica dell’estensione Adobe Medium Analytics (3.x SDK) for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html).

* **Media SDK:**  I dati vengono inviati ad Adobe Analytics.

  Per informazioni sul download e l’installazione di Media SDK e delle estensioni, consulta [Ottenere Media SDK e le estensioni tramite tag e SDK OTT](/help/getting-started/download-sdks.md).

* **API Media Collection:** Tracciare gli eventi audio e video utilizzando le chiamate HTTP RESTful. I dati vengono inviati ad Adobe Analytics.

  Per informazioni sull’utilizzo delle API Media Collection, consulta [API Media Collection](media-collection-api/mc-api-overview.md).


![Flusso di lavoro di analisi](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
