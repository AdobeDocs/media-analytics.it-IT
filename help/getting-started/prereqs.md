---
title: Scopri i prerequisiti per il componente aggiuntivo Streaming Media Collection di Adobe
description: Introduzione al componente aggiuntivo Streaming Media Collection. Scopri cosa serve per l’implementazione.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 54%

---

# Prerequisiti {#prerequisites}

Prima di iniziare l’implementazione del componente aggiuntivo Streaming Media Collection di Adobe, completa le seguenti attività:

1. **Rivedi la panoramica del componente aggiuntivo Streaming Media Collection**<br>
Prima di iniziare a implementare il componente aggiuntivo Streaming Media Collection, controlla [Panoramica del componente aggiuntivo Streaming Media Collection](/help/media-overview.md) per assicurarti che soddisfi le tue esigenze.

1. **Conferma il tuo modello di prezzo**<br>
Il modello di prezzo corrente per il componente aggiuntivo Streaming Media Collection di Adobe si basa sui flussi video. Se necessario, contatta il rappresentante commerciale o il team dell’account Adobe, poiché il componente aggiuntivo viene venduto separatamente per Adobe Analytics e Adobe Experience Platform.

1. **Abilita rapporti Adobe Analytics**<br>
Per abilitare i rapporti in Analytics o Customer Journey Analytics e visualizzare il contenuto e i dati degli annunci che stai raccogliendo, devi abilitare i rapporti. Consulta [Abilitazione di rapporti multimediali](/help/reporting/media-reports-enable.md).

1. **Implementazione del servizio Adobe Experience Platform Identity in Experience Cloud**

   Il **servizio Identity** abilita il framework comune di identificazione dei servizi principali e delle soluzioni Experience Cloud, nonché degli attributi cliente e tipi di pubblico del servizio di base People. Funziona tramite l’assegnazione di un ID univoco e persistente a un visitatore del sito. Quando l’organizzazione implementa il servizio ID, questo ID consente di identificare lo stesso visitatore del sito e i relativi dati in diverse soluzioni Experience Cloud.

   ![Grafico del servizio ID](assets/mc_id_service_graphic.png)

   Il servizio ID può anche sostituire i diversi ID specifici della soluzione (ad esempio, AID di Analytics). Quindi, tramite la funzionalità [ID cliente e stati di autenticazione](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=it), il servizio ID ti permette di trasmettere gli ID dei tuoi clienti a Experience Cloud. Il servizio ID funziona solo con le soluzioni per le quali hai effettuato la sottoscrizione. Se hai effettuato la registrazione per l’accesso ad altri prodotti, il servizio ID non fornisce l’accesso.

   Il servizio ID è un componente integrale di un gran numero di funzioni, miglioramenti e servizi di Experience Cloud. Attualmente, il servizio ID supporta [Analytics](https://www.adobe.com/it/marketing-cloud/web-analytics.html) [Audience Manager](https://www.adobe.com/it/marketing-cloud/data-management-platform.html) e [Target.](https://www.adobe.com/it/marketing-cloud/testing-targeting.html)

   Se non hai implementato il servizio ID, ti consigliamo di considerare fin da ora una strategia di migrazione. Per ulteriori informazioni sull’importanza e il ruolo del servizio ID, consulta l’articolo [Why the Identity Service Should be on Your Radar](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/) (Perché considerare il servizio Experience Cloud Identity).

   Per ulteriori informazioni su Experience Cloud ID, consulta [Panoramica di Experience Cloud ID,](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it) e [Servizio Adobe Experience Platform Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it).

1. **Visualizza prerequisiti aggiuntivi per il metodo di implementazione**

   A seconda di come prevedi di implementare il componente aggiuntivo Streaming Media Collection, visualizza i prerequisiti per uno dei seguenti metodi di implementazione:

   * [Prerequisiti per le implementazioni basate solo su Adobe Analytics](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Prerequisiti per le implementazioni di Edge](/help/implementation/edge/prerequisites-edge.md)

   Utilizza la [Panoramica sull&#39;implementazione](/help/implementation/overview.md) per determinare quale metodo di implementazione è più adatto alle tue esigenze.
