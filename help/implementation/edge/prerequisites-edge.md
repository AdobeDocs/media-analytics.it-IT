---
title: Prerequisiti per le implementazioni basate solo su Adobe Analytics
description: Scopri i prerequisiti per utilizzare Streaming Media Collection con implementazioni solo Adobe Analytics o Edge
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 0b0b4a373b15191dcb37dc436413f68cdc70768e
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 5%

---

# Prerequisiti per le implementazioni di Edge

I prerequisiti descritti in questa sezione sono specifici per l’implementazione di Adobe Streaming Media Collection con le implementazioni di Edge.

1. **Completare i prerequisiti generali**<br>
Che tu implementi la raccolta di file multimediali in streaming per le implementazioni basate solo su Adobe Analytics o per quelle basate su Edge, accertati di soddisfare i [prerequisiti generali](/help/getting-started/prereqs.md).

1. **Conferma l&#39;implementazione di una soluzione Adobe compatibile con Edge Network e Streaming Media Collection**<br>
Quando implementi Streaming Media Collection con Edge, devi anche disporre di un’implementazione funzionante di Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer o Real-Time Customer Data Platform. Per ulteriori informazioni, consulta le seguenti risorse della documentazione:
   * [Guida a Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=it)
   * [Implementazione di Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=it)
   * [Documentazione di Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=it)
   * [Documentazione di Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=it)

1. **Ottieni l&#39;URL del server di tracciamento dei contenuti multimediali**<br>
Chiedi al tuo rappresentante Customer Journey Analytics l&#39;URL del server di tracciamento dei contenuti multimediali. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implementa la raccolta di contenuti multimediali in streaming utilizzando Edge Network**<br>
Segui i passaggi in [Implementare la raccolta multimediale in streaming utilizzando Edge Network](/help/implementation/edge/implementation-edge.md).
