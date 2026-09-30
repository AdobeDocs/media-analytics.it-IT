---
title: Configurare l’estensione tag Web SDK per contenuti multimediali in streaming
description: Configura la raccolta di file multimediali in streaming nell’estensione tag Adobe Experience Platform Web SDK.
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
source-wordcount: '267'
ht-degree: 0%
---
# Configurare l’estensione tag Web SDK per contenuti multimediali in streaming

L&#39;estensione tag Adobe Experience Platform Web SDK consente di configurare la raccolta di file multimediali in streaming nell&#39;interfaccia utente di Data Collection, senza codice di configurazione `alloy.js`. Questa pagina descrive la configurazione dei tag. Per configurare il Web SDK nel codice, vedere [Configurare il Web SDK per Streaming Media](web-sdk.md).

* **Prerequisiti**:
  * Completa la [Panoramica sull&#39;implementazione di Edge](overview.md) (schema, set di dati, flusso di dati con [!UICONTROL Media Analytics] abilitato).
  * Installa e configura l’estensione tag Web SDK. Consulta la [panoramica dell&#39;estensione tag Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview).

## Configurare i contenuti multimediali in streaming nell’estensione

1. Nell&#39;interfaccia utente di Data Collection, apri la proprietà Web e seleziona **[!UICONTROL Extensions]**.
1. Nell&#39;estensione **Adobe Experience Platform Web SDK** installata, selezionare **[!UICONTROL Configure]**.
1. Espandere la sezione **[!UICONTROL Streaming Media]** e impostare quanto segue:
   * **[!UICONTROL Channel]**: nome del canale segnalato per ogni sessione.
   * **[!UICONTROL Player name]**: nome del lettore multimediale in uso.
   * **[!UICONTROL Application version]**: versione dell&#39;applicazione lettore.
   * **[!UICONTROL Main ping interval]** e **[!UICONTROL Ad ping interval]**: la cadenza del ping (in secondi) per il contenuto principale e gli annunci.
1. Salva la configurazione dell’estensione e pubblica le modifiche.

## Tracciare gli eventi multimediali

Con l&#39;estensione configurata, invia ogni evento multimediale con l&#39;azione **[!UICONTROL Send Event]** (o il comando `sendEvent`). Per conoscere i payload esatti, consulta la scheda **Web SDK** su ogni pagina [event](/help/implementation/events/overview.md) e [variable](/help/implementation/variables/overview.md).

## Passaggio successivo

Una volta completata l&#39;implementazione, puoi [Configurare la generazione di rapporti per le implementazioni di Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Panoramica dell&#39;estensione tag Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview)
>* [Configurazione del Web SDK per lo streaming di file multimediali (nel codice)](web-sdk.md)
>* [Panoramica eventi](/help/implementation/events/overview.md)
