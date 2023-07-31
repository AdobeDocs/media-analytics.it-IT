---
title: Informazioni sui prerequisiti per Streaming Media
description: Guida introduttiva ad Adobe Analytics Streaming Media. Scopri cosa serve per implementare Adobe Analytics for Streaming Media.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: b12e6547ef32bfad7e8d6787a26d6467bcfeb23c
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 74%

---

# Prerequisiti  {#prerequisites}

Prima di iniziare a implementare Streaming Media, completa le seguenti attività:

1. **Consulta la panoramica su Streaming Media**<br>
Prima di iniziare l’implementazione di Streaming Media, controlla [Panoramica di Streaming Media](/help/media-overview.md) per assicurarsi che Streaming Media soddisfi le tue esigenze.

1. **Conferma il modello di prezzo per Streaming Media**<br>
Il modello di prezzo corrente si basa sui flussi video. Se necessario, contatta il rappresentante commerciale o il team dell’account Adobe, poiché Streaming Media viene venduto separatamente, come componente aggiuntivo di Adobe Analytics.<!--update when media SKUs are added to other AEP apps -->

1. **Abilita i rapporti di Adobe Analytics**<br>
Per abilitare i rapporti in Analytics e visualizzare il contenuto e i dati degli annunci che stai raccogliendo, è necessario abilitare i rapporti in Analytics. Consulta [Abilitazione di rapporti multimediali](/help/reporting/media-reports-enable.md).

1. **Implementazione del servizio Adobe Experience Platform Identity in Experience Cloud**

   Il **servizio Identity** abilita il framework comune di identificazione dei servizi principali e delle soluzioni Experience Cloud, nonché degli attributi cliente e tipi di pubblico del servizio di base People. Funziona tramite l’assegnazione di un ID univoco e persistente a un visitatore del sito. Quando l’organizzazione implementa il servizio ID, questo ID consente di identificare lo stesso visitatore del sito e i relativi dati in diverse soluzioni Experience Cloud.

   ![Grafico del servizio ID](assets/mc_id_service_graphic.png)

   Il servizio ID può anche sostituire i diversi ID specifici della soluzione (ad esempio, AID di Analytics). Quindi, tramite la funzionalità [ID cliente e stati di autenticazione](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=it), il servizio ID ti permette di trasmettere gli ID dei tuoi clienti a Experience Cloud. Il servizio ID funziona solo con le soluzioni per le quali hai effettuato la sottoscrizione. Se hai effettuato la registrazione per l’accesso ad altri prodotti, il servizio ID non fornisce l’accesso.

   Il servizio ID è un componente integrale di un gran numero di funzioni, miglioramenti e servizi di Experience Cloud. Attualmente, il servizio ID supporta [Analytics](https://www.adobe.com/it/marketing-cloud/web-analytics.html) [Audience Manager](https://www.adobe.com/it/marketing-cloud/data-management-platform.html) e [Target.](https://www.adobe.com/it/marketing-cloud/testing-targeting.html)

   Se non hai implementato il servizio ID, ti consigliamo di considerare fin da ora una strategia di migrazione. Per ulteriori informazioni sull’importanza e il ruolo del servizio ID, consulta l’articolo [Why the Identity Service Should be on Your Radar](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/) (Perché considerare il servizio Experience Cloud Identity).

   Per ulteriori informazioni su Experience Cloud ID, consulta [Panoramica di Experience Cloud ID,](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it) e [Servizio Adobe Experience Platform Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it).

1. **Visualizza prerequisiti aggiuntivi per il metodo di implementazione**

   A seconda di come prevedi di implementare Streaming Media, visualizza i prerequisiti per uno dei seguenti metodi di implementazione:

   * [Prerequisiti per le implementazioni basate solo su Adobe Analytics](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Prerequisiti per le implementazioni Edge](/help/implementation/edge/prerequisites-edge.md)

   Utilizza il [Panoramica sull’implementazione](/help/implementation/overview.md) per determinare quale metodo di implementazione è più adatto alle tue esigenze.
