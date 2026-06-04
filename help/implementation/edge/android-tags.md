---
title: Configurare Android per lo streaming di file multimediali con i tag
description: Configura la raccolta di contenuti multimediali in streaming per Android utilizzando l’estensione tag Adobe Streaming Media for Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Configurare Android per lo streaming di file multimediali con i tag

Puoi configurare la raccolta di file multimediali in streaming per l’app Android tramite una proprietà mobile Tag, con le impostazioni per file multimediali gestite nell’interfaccia utente di Data Collection. Questa pagina descrive la configurazione dei tag. Per configurare SDK nel codice, vedere [Configurare Android per Streaming Media](android.md).

* **Prerequisiti**:
   * Completa la [Panoramica sull&#39;implementazione di Edge](overview.md) (schema, set di dati, flusso di dati con [!UICONTROL Media Analytics] abilitato).
   * Crea una proprietà mobile nell’interfaccia utente di Data Collection. Consulta [Adobe Streaming Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/).

## Configurare l&#39;estensione

1. Nell&#39;interfaccia utente di Data Collection, apri la proprietà mobile e seleziona **[!UICONTROL Extensions]**.
1. Nella scheda **[!UICONTROL Catalog]**, individua l&#39;estensione **Adobe Streaming Media for Edge Network** e seleziona **[!UICONTROL Install]**.
1. Imposta quanto segue, quindi salva:
   * **[!UICONTROL Channel]**: il nome del canale riportato per ogni sessione.
   * **[!UICONTROL Player name]**: nome del lettore multimediale in uso.
   * **[!UICONTROL Application version]**: versione dell&#39;applicazione lettore.
1. Pubblica le modifiche, quindi aggiungi le dipendenze `Core`, `Edge`, `EdgeIdentity` e `EdgeMedia` all&#39;app e registrale con Mobile Core.

## Tracciare gli eventi multimediali

Con la proprietà pubblicata e il tracciatore creato, tieni traccia di ogni evento multimediale utilizzando il relativo metodo di tracciamento. Per le chiamate esatte, vedi la scheda **Android** su ogni pagina [event](/help/implementation/events/overview.md) e [variable](/help/implementation/variables/overview.md).

## Passaggio successivo

Una volta completata l&#39;implementazione, puoi [Configurare la generazione di rapporti per le implementazioni di Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Contenuti multimediali in streaming Adobe per Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Configura Android per Streaming Media (nel codice)](android.md)
>* [Panoramica eventi](/help/implementation/events/overview.md)
