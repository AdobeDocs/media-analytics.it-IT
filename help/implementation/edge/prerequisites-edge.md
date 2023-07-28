---
title: Prerequisiti per le implementazioni basate solo su Adobe Analytics
description: Informazioni sui prerequisiti per l’utilizzo di Streaming Media con implementazioni basate solo su Adobe Analytics
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 13%

---

# Prerequisiti per le implementazioni Edge

I prerequisiti descritti in questa sezione sono specifici per l’implementazione di Streaming Media con implementazioni Edge.

1. **Completare i prerequisiti generali**<br>
Che tu implementi Streaming Media per implementazioni basate solo su Adobe Analytics o Edge, assicurati di soddisfare i requisiti [prerequisiti generali](/help/getting-started/prereqs.md).

1. **Conferma l’implementazione di una soluzione Adobe compatibile con Edge e Streaming Media**<br>
Quando implementi Streaming Media con Edge, devi anche disporre di un Customer Journey Analytics di lavoro, Adobe Analytics, Adobe Journey Optimizer o un’implementazione Real-time Customer Data Platform. Per ulteriori informazioni, consulta le seguenti risorse della documentazione:
   * [Guida a Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=it)
   * [Implementazione di Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=it)
   * [Documentazione di Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=it)
   * [Documentazione di Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **Ottenere l’URL del server di tracciamento dei contenuti multimediali**<br>
Chiedi al rappresentante del Customer Journey Analytics l’URL del server di tracciamento dei contenuti multimediali. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Installare Media Analytics con Edge**<br>
Segui i passaggi descritti in [Installare Media Analytics con Experienci Platform Edge](/help/implementation/edge/implementation-edge.md).