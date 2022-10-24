---
title: Informazioni sui prerequisiti per lo streaming multimediale
description: Guida introduttiva ad Adobe Analytics Streaming Media. Scopri cosa serve per implementare Adobe Analytics for Streaming Media.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: e5d1d86a2534a8c0fac63948e37a14b1dc1e896e
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 98%

---

# Prerequisiti {#prerequisites}

## Decisioni {#decision}

Prima di iniziare l’implementazione del tracciamento, devi prendere alcune decisioni preliminari riguardo a quale implementazione ha più senso per la tua situazione:

* **Media Analytics -** Utilizzo degli SDK per contenuti multimediali più recenti (implementazione standard e consigliata) e/o dell’API Media Collection (RESTful)
* **Milestone -** Implementazione del tracciamento Adobe precedente
* **API di inserimento dati -** Implementazione del tracciamento senza l’utilizzo degli SDK per contenuti multimediali

## Attività {#prereq-tasks}

Per l’implementazione di *Media Analytics*, ecco le attività da completare prima di iniziare:

1. **Abilita Experience Cloud.**

   È necessario implementare il servizio Adobe Experience Platform Identity.

   Il servizio Identity abilita il framework comune di identificazione dei servizi principali e delle soluzioni Experience Cloud, nonché degli attributi cliente e tipi di pubblico del servizio People. Funziona tramite l’assegnazione di un ID univoco e persistente a un visitatore del sito. Quando l’organizzazione implementa il servizio ID, questo ID consente di identificare lo stesso visitatore del sito e i relativi dati in diverse soluzioni Experience Cloud.

   ![](assets/mc_id_service_graphic.png)

   Il servizio ID può anche sostituire i diversi ID specifici della soluzione (ad esempio, AID di Analytics). Quindi, tramite la funzionalità [ID cliente e stati di autenticazione](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=it), il servizio ID ti permette di trasmettere gli ID dei tuoi clienti a Experience Cloud. Il servizio ID funziona solo con le soluzioni per le quali hai effettuato la sottoscrizione. Se hai effettuato la registrazione per l’accesso ad altri prodotti, il servizio ID non fornisce l’accesso.

   Il servizio ID è un componente integrale di un gran numero di funzioni, miglioramenti e servizi correnti e futuri di Experience Cloud. Attualmente, il servizio ID supporta [Analytics](https://www.adobe.com/it/marketing-cloud/web-analytics.html) [Audience Manager](https://www.adobe.com/it/marketing-cloud/data-management-platform.html) e [Target.](https://www.adobe.com/it/marketing-cloud/testing-targeting.html)

   Se non hai implementato il servizio ID, ti consigliamo di considerare fin da ora una strategia di migrazione. Per ulteriori informazioni sull’importanza e il ruolo del servizio ID, consulta l’articolo [Why the Identity Service Should be on Your Radar](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/) (Perché considerare il servizio Experience Cloud Identity).

   Per ulteriori informazioni su Experience Cloud ID, consulta [Panoramica di Experience Cloud ID,](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it) e [Servizio Adobe Experience Platform Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it).

1. **Abilita i rapporti di Adobe Analytics.**

   Per abilitare i rapporti in Analytics e visualizzare il contenuto e i dati degli annunci che stai raccogliendo, consulta [Abilitazione dei rapporti multimediali.](/help/media-reports/media-reports-enable.md)
