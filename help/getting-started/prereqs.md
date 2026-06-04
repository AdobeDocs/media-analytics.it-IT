---
title: Informazioni sui prerequisiti per Adobe Streaming Media Services
description: Introduzione ai servizi di streaming multimediale. Scopri cosa serve per l’implementazione.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/e9iYwDwT-zSSZ3hV20U1w7p-MtKaK4Q8-vGMCrnenpc
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c8add8f2-4250-4fd9-9cde-9707036c567d
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 490
ht-degree: 39%

---

# Prerequisiti {#prerequisites}

Prima di iniziare a implementare i servizi di streaming media di Adobe, completa le seguenti attività:

1. **Consulta la panoramica dei servizi di streaming multimediale Adobe**<br>
Prima di iniziare a implementare i servizi di streaming multimediale, controlla la [panoramica dei servizi di streaming multimediale](/help/media-overview.md) di Adobe per assicurarti che soddisfi le tue esigenze.

1. **Conferma il tuo modello di prezzo**<br>
Il modello di prezzo corrente per il componente aggiuntivo Customer Journey Analytics Streaming Media Collection e per il componente aggiuntivo Adobe Analytics for Streaming Media si basa sui flussi video. Se necessario, contatta il rappresentante commerciale o il team dell’account Adobe, poiché il componente aggiuntivo viene venduto separatamente per Adobe Analytics e Adobe Experience Platform.

1. **Abilita rapporti Adobe Analytics**<br>
Per abilitare i rapporti in Analytics o Customer Journey Analytics e visualizzare il contenuto e i dati degli annunci che stai raccogliendo, devi abilitare i rapporti. Consulta [Configurare la generazione di rapporti per le implementazioni solo Analytics](/help/reporting/setup/analytics-reporting.md).

1. **Implementazione del servizio Adobe Experience Platform Identity in CX Enterprise**

   Il **servizio Identity** abilita il framework comune di identificazione dei servizi principali e delle soluzioni CX Enterprise, nonché degli attributi cliente e tipi di pubblico del servizio di base Persone. Funziona tramite l’assegnazione di un ID univoco e persistente a un visitatore del sito. Quando l&#39;organizzazione implementa il servizio ID, questo ID consente di identificare lo stesso visitatore del sito e i relativi dati in diverse soluzioni CX Enterprise.

   ![Grafico del servizio ID](assets/mc_id_service_graphic.png)

   Il servizio ID può anche sostituire i diversi ID specifici della soluzione (ad esempio, AID di Analytics). Tramite la funzionalità [ID cliente e stati di autenticazione](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=it), il servizio ID ti consente di trasmettere gli ID dei tuoi clienti a CX Enterprise. Il servizio ID funziona solo con le soluzioni per le quali hai effettuato la sottoscrizione. Se hai effettuato la registrazione per l’accesso ad altri prodotti, il servizio ID non fornisce l’accesso.

   Il servizio ID è un componente integrale di molte funzioni, miglioramenti e servizi di CX Enterprise. Attualmente, il servizio ID supporta [Analytics](https://www.adobe.com/it/marketing-cloud/web-analytics.html) [Audience Manager](https://www.adobe.com/it/marketing-cloud/data-management-platform.html) e [Target.](https://www.adobe.com/it/marketing-cloud/testing-targeting.html)

   Se non hai implementato il servizio ID, ti consigliamo di considerare fin da ora una strategia di migrazione. Per ulteriori informazioni sull’importanza e il ruolo del servizio ID, consulta l’articolo [Why the Identity Service Should be on Your Radar](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/) (Perché considerare il servizio Experience Cloud Identity).

   Per ulteriori informazioni su Experience Cloud ID, consulta [Panoramica di Experience Cloud ID,](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it) e [Servizio Adobe Experience Platform Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it).

1. **Visualizza prerequisiti aggiuntivi per il metodo di implementazione**

   A seconda di come prevedi di implementare Streaming Media Services, visualizza i prerequisiti per uno dei seguenti metodi di implementazione:

   * [Panoramica sull’implementazione solo per Analytics](/help/implementation/analytics-only/overview.md)

   * [Panoramica sull’implementazione di Edge](/help/implementation/edge/overview.md)

   Utilizza la [Panoramica sull&#39;implementazione](/help/implementation/overview.md) per determinare quale metodo di implementazione è più adatto alle tue esigenze.
