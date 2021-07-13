---
title: Informazioni sui prerequisiti per lo streaming multimediale
description: Guida introduttiva ad Adobe Analytics Streaming Media. Scopri cosa devi implementare Adobe Analytics per Streaming Media.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: '"Media Analytics, Requisiti di sistema"'
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 19%

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

   Il servizio Identity abilita il framework comune di identificazione dei servizi di base e delle soluzioni di Experience Cloud, nonché degli attributi cliente e pubblico nel servizio di base Persone. Funziona tramite l’assegnazione di un ID univoco e persistente a un visitatore del sito. Quando l’organizzazione implementa il servizio ID, questo ID consente di identificare lo stesso visitatore del sito e i relativi dati in diverse soluzioni Experience Cloud.

   ![](assets/mc_id_service_graphic.png)

   Il servizio ID può anche sostituire i diversi ID specifici della soluzione (ad esempio, AID di Analytics). Attraverso la funzionalità [ID cliente e stati di autenticazione](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) , il servizio ID ti consente di trasmettere gli ID dei tuoi clienti all&#39;Experience Cloud. Il servizio ID funziona solo con le soluzioni per le quali hai effettuato la sottoscrizione. Se non sei registrato per l&#39;accesso ad altri prodotti, il servizio ID non fornisce l&#39;accesso.

   Il servizio ID è un componente integrale di un gran numero di funzioni, miglioramenti e servizi correnti e futuri di Experience Cloud. Attualmente, il servizio ID supporta [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) e [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Per partecipare ad Adobe Experience Cloud Device Co-op, è necessario il servizio ID Experience Cloud.

   Se non hai implementato il servizio ID, ti consigliamo di considerare fin d&#39;ora una strategia di migrazione. Per ulteriori informazioni sull’importanza e il ruolo del servizio ID, consulta [Perché il servizio Identity dovrebbe trovarsi nel tuo radar.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Per ulteriori informazioni sull’ID Experience Cloud, consulta [Panoramica ID Experience Cloud,](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) e [Servizio Adobe Experience Platform Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it).

1. **Abilitare i rapporti di Adobe Analytics.**

   Per abilitare i rapporti in Analytics e visualizzare il contenuto e i dati degli annunci che stai raccogliendo, consulta [Abilitazione dei rapporti multimediali.](/help/media-reports/media-reports-enable.md)
