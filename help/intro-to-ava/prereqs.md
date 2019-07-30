---
seo-title: Prerequisiti
title: Prerequisiti
uuid: 4 c 0 b 37 f 3-8615-4 cc 0-b 9 c 9-eeb 029067064
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Prerequisiti{#prerequisites}

## Decisions {#decision}

Prima di iniziare l'implementazione del tracciamento, hai alcune decisioni introduttive da prendere in considerazione di quale implementazione rende più rilevante la tua situazione:

* **Media Analytics -** Utilizzo degli SDK multimediali più recenti (implementazione standard consigliata) e/o dell'API di Media Collection (restful)
* **Milestone -** The old Adobe tracking implementation
* **API di inserimento dati -** Implementazione del tracciamento senza usare gli SDK multimediali

## Tasks {#prereq-tasks}

For a *Media Analytics* implementation, here are the tasks you must complete before you begin:

1. **Abilita Experience Cloud.**

   Devi implementare Adobe Experience Platform Identity Service.

   Il servizio identità abilita il framework comune di identificazione dei servizi di base, delle soluzioni e degli attributi del cliente di Experience Cloud nel servizio di base Persone. Funziona tramite l'assegnazione di un ID univoco persistente a un visitatore del sito. Quando l'organizzazione implementa il servizio ID, tale ID consente di identificare lo stesso visitatore del sito e i relativi dati in diverse soluzioni Experience Cloud.

   ![](assets/mc_id_service_graphic.png)

   Il servizio ID può anche sostituire i diversi ID specifici della soluzione (ad esempio, AID di Analytics). Through the [Customer IDs and Authentication States](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-authenticated-state.html) functionality, the ID service lets you pass in your own customer IDs to the Experience Cloud. Ricorda però che il servizio ID funziona solo con le soluzioni che hai già sottoscritto. Se non sei iscritto ad altri prodotti, il servizio ID non fornisce l'accesso.

   Il servizio ID è un componente integrale di un gran numero di funzioni, miglioramenti e servizi correnti e futuri di Experience Cloud. Currently, the ID service supports [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) and [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Per partecipare ad Adobe Experience Cloud Device Co-op, è necessario il servizio Experience Cloud ID.

   Se non hai implementato il servizio ID, ti consigliamo di considerare fin d'ora una strategia di migrazione. For more information about the importance and role of the ID service, see [Why the Identity Service Should be on Your Radar.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >In the absence of any user ID information present on the media-specific calls, the default analytics [Fallback ID Methods](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) will apply.

   For additional information about the Experience Cloud ID, see [Experience Cloud ID Overview,](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html) and [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/)

1. **Abilitare i report di Adobe Analytics.**

   To enable reports in Analytics and see the content and ad data you are collecting, see [Media reports enablement.](/help/media-reports/media-reports-enable.md)

