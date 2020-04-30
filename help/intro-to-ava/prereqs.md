---
title: Prerequisiti
description: null
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Prerequisiti{#prerequisites}

## Decisioni {#decision}

Prima di iniziare l&#39;implementazione di tracciamento, devi prendere alcune decisioni anticipate, riguardo a quale implementazione è più appropriata per la tua situazione:

* **Media Analytics -** Utilizzo degli SDK Media più recenti (implementazione standard e consigliata) e/o dell&#39;API Media Collection (RESTful)
* **Milestone -** Implementazione di tracciamento Adobe meno recente
* **API di inserimento dei dati - Implementazione del tracciamento** senza utilizzare gli SDK di Media

## Attività {#prereq-tasks}

Per un&#39;implementazione di *Media Analytics* , prima di iniziare devi completare le seguenti attività:

1. **Abilita Experience Cloud.**

   Devi implementare Adobe Experience Platform Identity Service.

   Il servizio identità abilita il framework comune di identificazione per i servizi di base, le soluzioni e gli attributi cliente e pubblico di Experience Cloud nel servizio di base Persone. Funziona tramite l&#39;assegnazione di un ID univoco persistente a un visitatore del sito. Quando l&#39;organizzazione implementa il servizio ID, tale ID consente di identificare lo stesso visitatore del sito e i relativi dati in diverse soluzioni Experience Cloud.

   ![](assets/mc_id_service_graphic.png)

   Il servizio ID può anche sostituire i diversi ID specifici della soluzione (ad esempio, AID di Analytics). Through the [Customer IDs and Authentication States](https://docs.adobe.com/content/help/it-IT/id-service/using/reference/authenticated-state.html) functionality, the ID service lets you pass in your own customer IDs to the Experience Cloud. Ricorda, tuttavia, che il servizio ID funziona solo con le soluzioni alle quali hai già effettuato la sottoscrizione. Se non ti sei registrato per l’accesso ad altri prodotti, il servizio ID non fornisce l’accesso.

   Il servizio ID è un componente integrale di un gran numero di funzioni, miglioramenti e servizi correnti e futuri di Experience Cloud. Currently, the ID service supports [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) and [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Per partecipare ad Adobe Experience Cloud Device Co-op, è necessario il servizio Experience Cloud ID.

   Se non hai implementato il servizio ID, ti consigliamo di considerare fin d&#39;ora una strategia di migrazione. For more information about the importance and role of the ID service, see [Why the Identity Service Should be on Your Radar.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >In assenza di informazioni ID utente presenti nelle chiamate specifiche per i supporti, si applicano i metodi [ID](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) fallback di analisi predefiniti.

   Per ulteriori informazioni sull&#39;Experience Cloud ID, consulta Panoramica [Experience Cloud ID,](https://docs.adobe.com/content/help/it-IT/id-service/using/intro/overview.html) e Servizio identità [Adobe Experience Platform.](https://docs.adobe.com/content/help/it-IT/id-service/using/home.html)

1. **Abilita rapporti di Adobe Analytics.**

   Per abilitare i report in Analytics e visualizzare il contenuto e i dati degli annunci che stai raccogliendo, consulta Abilitazione dei report [multimediali.](/help/media-reports/media-reports-enable.md)

