---
title: Configurare Chromecast per contenuti multimediali in streaming
description: Installa e configura Media SDK per Chromecast per le implementazioni multimediali in streaming solo per Analytics.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 10%
---
# Configurare Chromecast per contenuti multimediali in streaming

Media SDK for Chromecast invia i dati multimediali in streaming dalle app di ricezione Chromecast direttamente ad Adobe Analytics. SDK e la relativa documentazione sono ospitati su GitHub.

* **Prerequisiti**:
  * Completa la [Panoramica sull&#39;implementazione di sola Analytics](overview.md).
  * [Scarica Media SDK per Chromecast](/help/getting-started/download-sdks.md).

## Installare e configurare SDK

Aggiungi il SDK all’app ricevitore Chromecast e configura il tracker come descritto nei riferimenti canonici:

* [Configurare il SDK Chromecast](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/docs/2.x/chromecast-setup.md)
* [Riferimento API per SDK Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)

## Tracciare gli eventi multimediali

Una volta creato il tracciatore, tieni traccia di ogni evento multimediale utilizzando il relativo metodo di tracciamento. Per le chiamate esatte, vedi la scheda **Chromecast** su ogni pagina [event](/help/implementation/events/overview.md) e [variable](/help/implementation/variables/overview.md).

## Passaggio successivo

Una volta completata l&#39;implementazione, puoi [Configurare la generazione di rapporti per le implementazioni solo Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Riferimento API SDK per Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)
>* [Panoramica eventi](/help/implementation/events/overview.md)
>* [Panoramica delle variabili](/help/implementation/variables/overview.md)
