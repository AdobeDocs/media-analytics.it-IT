---
title: Prerequisiti per le implementazioni basate solo su Adobe Analytics
description: Scopri i prerequisiti per utilizzare Streaming Media Collection con implementazioni solo Adobe Analytics o Edge
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
TQID: https://experienceleague.adobe.com/OqimGafihuirpnAaZ4AvrX2lrOmCtr0FLXk3QwoVTew
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 212
ht-degree: 11%

---

# Prerequisiti per le implementazioni di Edge

I prerequisiti descritti in questa sezione sono specifici per l’implementazione di Adobe Streaming Media Collection con le implementazioni di Edge.

1. **Completare i prerequisiti generali**<br>
Che tu implementi la raccolta di file multimediali in streaming per le implementazioni basate solo su Adobe Analytics o su Edge, accertati di soddisfare i [prerequisiti generali](/help/getting-started/prereqs.md).

1. **Conferma l&#39;implementazione di una soluzione Adobe compatibile con Edge Network e Streaming Media Collection**<br>
Quando implementi Streaming Media Collection con Edge, devi anche disporre di un’implementazione funzionante di Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer o Real-Time Customer Data Platform. Per ulteriori informazioni, consulta le seguenti risorse della documentazione:
   * [Guida di Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=it)
   * [Implementazione di Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=it)
   * [Documentazione di Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=it)
   * [Documentazione di Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=it)

1. **Ottieni l&#39;URL del server di tracciamento dei contenuti multimediali**<br>
Chiedi al tuo rappresentante Customer Journey Analytics l&#39;URL del server di tracciamento dei contenuti multimediali. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implementare la raccolta di contenuti multimediali in streaming utilizzando Edge Network**<br>
Segui i passaggi descritti in [Implementare la raccolta multimediale in streaming utilizzando Edge Network](/help/implementation/edge/implementation-edge.md).
