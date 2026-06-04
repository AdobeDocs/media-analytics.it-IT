---
title: Configurare l’estensione tag di Media Analytics
description: Utilizza l’estensione tag Adobe Media Analytics (3.x SDK) for Audio and Video per implementare contenuti multimediali in streaming solo per Analytics.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 12%

---

# Configurare l’estensione tag di Media Analytics

L’estensione tag Adobe Media Analytics (3.x SDK) for Audio and Video distribuisce Media SDK for JavaScript (3.x) tramite Tag, senza l’installazione manuale di JavaScript. Questa pagina descrive la configurazione dei tag. Per installare SDK nel codice, vedere [Configurare JavaScript per Streaming Media](javascript.md). Per le nuove implementazioni, considera il percorso Edge consigliato per l&#39;[estensione tag Web SDK](/help/implementation/edge/web-sdk-tags.md).

* **Prerequisiti**: completa la [panoramica sull&#39;implementazione di sola Analytics](overview.md).

## Installare e configurare l’estensione

Aggiungi l’istanza di tracciamento Media a un sito abilitato per i tag installando e configurando l’estensione nell’interfaccia utente di Data Collection. Per informazioni dettagliate sull&#39;installazione e la configurazione, vedere [Estensione Adobe Media Analytics (3.x SDK) for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=it).

## Tracciare gli eventi multimediali

Con l’estensione configurata, tieni traccia di ogni evento multimediale utilizzando il relativo metodo di tracciamento. Consulta la scheda **Media SDK JS 3.x** su ogni pagina [event](/help/implementation/events/overview.md) e [variable](/help/implementation/variables/overview.md) per informazioni sulle chiamate esatte.

## Passaggio successivo

Una volta completata l&#39;implementazione, puoi [Configurare la generazione di rapporti per le implementazioni solo Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Estensione Adobe Media Analytics (3.x SDK) for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=it)
>* [Configura JavaScript per Streaming Media (nel codice)](javascript.md)
>* [Panoramica eventi](/help/implementation/events/overview.md)
