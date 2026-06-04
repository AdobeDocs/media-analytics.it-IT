---
title: Panoramica sull’implementazione solo per Analytics
description: Prerequisiti e metodi di implementazione per il componente aggiuntivo Adobe Analytics for Streaming Media, utilizzato per le implementazioni basate solo su Analytics.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 5%

---

# Panoramica sull’implementazione solo per Analytics

Le implementazioni basate solo su Analytics utilizzano il componente aggiuntivo Adobe Analytics for Streaming Media per inviare dati direttamente ad Adobe Analytics, senza Edge Network. Questi metodi rimangono completamente supportati. Per le nuove implementazioni, Adobe consiglia invece l&#39;implementazione [Edge](/help/implementation/edge/overview.md), perché rende i dati disponibili per Customer Journey Analytics, Adobe Journey Optimizer e Real-Time CDP oltre ad Adobe Analytics.

## Prerequisiti

1. **Completare i prerequisiti generali.** Consulta i [prerequisiti generali](/help/getting-started/prereqs.md).

1. **Conferma un&#39;implementazione di Adobe Analytics.** Un’implementazione di Streaming Media solo per Analytics richiede un’implementazione di base di Adobe Analytics. Consulta [Implementare Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=it).

1. **Ottieni l&#39;URL del server di tracciamento dei contenuti multimediali.** Chiedi al tuo rappresentante Adobe Analytics l&#39;URL del server di tracciamento dei contenuti multimediali (l&#39;URL `collection-api-server`). Il dominio segue in genere il pattern `[your_namespace].hb-api.omtrdc.net`.

1. **Scarica il SDK o installa l&#39;estensione.** A seconda della piattaforma, [scarica il SDK](/help/getting-started/download-sdks.md) corrente o installa l&#39;estensione tag richiesta.

## Scegli il metodo di implementazione

Ogni pagina descrive la configurazione specifica per i contenuti multimediali in streaming. Il codice per evento e per variabile risiede in [Eventi](/help/implementation/events/overview.md) e [Variabili](/help/implementation/variables/overview.md).

| Codebase | In-code | Tramite tag |
|---|---|---|
| Web (JavaScript) | [JavaScript](javascript.md) | [Estensione tag di Media Analytics](javascript-tags.md) |
| Chromecast | [Chromecast](chromecast.md) | — |
| API | [API Media Collection](media-collection-api.md) | — |

## Passaggio successivo

Una volta completata l&#39;implementazione, puoi [Configurare la generazione di rapporti per le implementazioni solo Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Panoramica sull&#39;implementazione](/help/implementation/overview.md)
>* [Panoramica eventi](/help/implementation/events/overview.md)
>* [Panoramica delle variabili](/help/implementation/variables/overview.md)
