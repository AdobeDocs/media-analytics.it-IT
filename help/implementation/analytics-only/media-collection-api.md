---
title: Configurare l’API Media Collection per lo streaming dei contenuti multimediali
description: Utilizza l’API Media Collection per inviare dati multimediali in streaming direttamente ad Adobe Analytics con chiamate HTTP RESTful.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 1%

---

# Configurare l’API Media Collection per lo streaming dei contenuti multimediali

L’API Media Collection invia i dati multimediali in streaming direttamente ad Adobe Analytics utilizzando le chiamate HTTP RESTful. Poiché è completamente personalizzabile, supporta il tracciamento personalizzato e i dispositivi non coperti dagli SDK. Utilizzalo quando un SDK non è un’opzione per la tua piattaforma.

* **Prerequisiti**: completa la [panoramica sull&#39;implementazione di sola Analytics](overview.md).

## Implementare l’API

Aprire una sessione con una richiesta `sessionStart`, quindi inviare gli eventi successivi alla sessione restituita. Per i formati completi di richiesta/risposta, i parametri, gli schemi di convalida e le linee guida per l&#39;implementazione, vedi il [riferimento API di Media Collection](../media-collection-api/mc-api-overview.md).

## Tracciare gli eventi multimediali

Per conoscere i payload esatti, consulta la scheda **API Media Collection** su ogni pagina [evento](/help/implementation/events/overview.md) e [variabile](/help/implementation/variables/overview.md).

## Passaggio successivo

Una volta completata l&#39;implementazione, puoi [Configurare la generazione di rapporti per le implementazioni solo Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Riferimento API Media Collection](../media-collection-api/mc-api-overview.md)
>* [Panoramica eventi](/help/implementation/events/overview.md)
>* [Panoramica delle variabili](/help/implementation/variables/overview.md)
