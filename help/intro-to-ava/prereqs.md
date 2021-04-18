---
title: Prerequisiti
description: Prerequisiti
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 24%

---

# Prerequisiti{#prerequisites}

## Decisioni {#decision}

Prima di iniziare l’implementazione del tracciamento, devi prendere alcune decisioni preliminari, riguardo a quale implementazione ha più senso per la tua situazione:

* **Media Analytics:** utilizza gli SDK per contenuti multimediali più recenti (implementazione standard e consigliata) e/o l’API Media Collection (RESTful)
* **Milestone -** Implementazione del tracciamento degli Adobi precedente
* **API di inserimento dati -** Implementazione del tracciamento senza l’utilizzo di Media SDK

## Attività {#prereq-tasks}

Per un&#39;implementazione di *Media Analytics* , esegui le seguenti attività prima di iniziare:

1. **Abilita Experience Cloud.**

   È necessario implementare il servizio Adobe Experience Platform Identity.

   Il servizio Identity abilita il framework comune di identificazione dei servizi di base e delle soluzioni di Experience Cloud, nonché degli attributi cliente e pubblico nel servizio di base Persone. Funziona tramite l&#39;assegnazione di un ID univoco e costante a un visitatore del sito. Quando l&#39;organizzazione implementa il servizio ID, tale ID consente di identificare lo stesso visitatore del sito e i relativi dati in diverse soluzioni Experience Cloud.

   ![](assets/mc_id_service_graphic.png)

   Il servizio ID può anche sostituire i diversi ID specifici della soluzione (ad esempio, AID di Analytics). Attraverso la funzionalità [ID cliente e stati di autenticazione](https://docs.adobe.com/content/help/it-IT/id-service/using/reference/authenticated-state.html) , il servizio ID ti consente di trasmettere gli ID dei tuoi clienti all&#39;Experience Cloud. Il servizio ID funziona solo con le soluzioni per le quali hai effettuato la sottoscrizione. Se non sei registrato per l&#39;accesso ad altri prodotti, il servizio ID non fornisce l&#39;accesso.

   Il servizio ID è un componente integrale di un gran numero di funzioni, miglioramenti e servizi correnti e futuri di Experience Cloud. Attualmente, il servizio ID supporta [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) e [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Per partecipare ad Adobe Experience Cloud Device Co-op, è necessario il servizio ID Experience Cloud.

   Se non hai implementato il servizio ID, ti consigliamo di considerare fin d&#39;ora una strategia di migrazione. Per ulteriori informazioni sull’importanza e il ruolo del servizio ID, consulta [Perché il servizio Identity dovrebbe trovarsi nel tuo radar.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >In assenza di informazioni ID utente presenti nelle chiamate specifiche per i file multimediali, si applica l&#39;analisi predefinita [Metodi di fallback ID](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) .

   Per ulteriori informazioni sull’ID Experience Cloud, consulta [Panoramica ID Experience Cloud,](https://docs.adobe.com/content/help/it-IT/id-service/using/intro/overview.html) e [Servizio Adobe Experience Platform Identity.](https://docs.adobe.com/content/help/it-IT/id-service/using/home.html)

1. **Abilitare i rapporti di Adobe Analytics.**

   Per abilitare i rapporti in Analytics e visualizzare il contenuto e i dati degli annunci che stai raccogliendo, consulta [Abilitazione dei rapporti multimediali.](/help/media-reports/media-reports-enable.md)
