---
title: Informazioni sui prerequisiti per Adobe Streaming Media Services
description: Introduzione ai servizi di streaming multimediale. Scopri cosa serve per l’implementazione.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/e9iYwDwT-zSSZ3hV20U1w7p-MtKaK4Q8-vGMCrnenpc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
    internal-label: Reports
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
    internal-label: Implementations
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
subfeature_v2:
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
    internal-label: Methods
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 2%
---
# Prerequisiti {#prerequisites}

Prima di iniziare a implementare i servizi di streaming media di Adobe, completa le seguenti attività:

1. **Conferma il tuo modello di prezzo**<br>
Il modello di prezzo corrente per il componente aggiuntivo Customer Journey Analytics Streaming Media Collection e per il componente aggiuntivo Adobe Analytics for Streaming Media si basa sui flussi video. Se necessario, contatta il rappresentante commerciale o il team dell’account Adobe, poiché il componente aggiuntivo viene venduto separatamente per Adobe Analytics e Adobe Experience Platform.

1. **Abilita i rapporti di Adobe Analytics** *(implementazioni solo di Analytics)*<br>
Per abilitare i rapporti in Analytics e visualizzare il contenuto e i dati degli annunci che stai raccogliendo, devi abilitare i rapporti. Consulta [Configurare la generazione di rapporti per le implementazioni solo Analytics](/help/reporting/setup/analytics-reporting.md).

1. **Configura identità**<br>

   I requisiti di configurazione delle identità variano a seconda del metodo di implementazione:

   * **Implementazioni di Edge**: l&#39;identità è gestita tramite la configurazione dello spazio dei nomi Adobe Experience Platform Identity. Non è richiesta alcuna configurazione separata del servizio ID visitatore. Per informazioni dettagliate, consulta [Panoramica sull&#39;implementazione di Edge](/help/implementation/edge/overview.md).

   * **Implementazioni solo per Analytics**: il servizio ID visitatore di Adobe deve essere abilitato per identificare i visitatori in modo coerente nelle soluzioni CX Enterprise. Il Servizio ID visitatore assegna un ID univoco e costante a ciascun visitatore del sito e consente di condividerlo tra tutte le soluzioni CX Enterprise a cui sei abbonato.

     Per ulteriori informazioni, consulta la [documentazione del servizio ID visitatore di Adobe](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it).

1. **Visualizza prerequisiti aggiuntivi per il metodo di implementazione**

   A seconda di come prevedi di implementare Streaming Media Services, visualizza i prerequisiti per uno dei seguenti metodi di implementazione:

   * [Panoramica sull’implementazione solo per Analytics](/help/implementation/analytics-only/overview.md)

   * [Panoramica sull’implementazione di Edge](/help/implementation/edge/overview.md)

   Utilizza la [Panoramica sull&#39;implementazione](/help/implementation/overview.md) per determinare quale metodo di implementazione è più adatto alle tue esigenze.
