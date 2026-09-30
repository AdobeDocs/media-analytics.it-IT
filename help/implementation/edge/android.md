---
title: Configurare Android per lo streaming dei contenuti multimediali
description: Configura Adobe Experience Platform Mobile SDK su Android per inviare dati multimediali in streaming ad Edge Network.
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
source-wordcount: '235'
ht-degree: 0%
---
# Configurare Android per lo streaming dei contenuti multimediali

L&#39;estensione Adobe Streaming Media for Edge Network (`EdgeMedia`) raccoglie i dati della sessione multimediale nell&#39;app Android e li invia ad Edge Network. Questa pagina descrive la configurazione nel codice. Per configurare SDK tramite una proprietà mobile Tag, vedere [Configurare Android per lo streaming di file multimediali con Tag](android-tags.md).

* **Prerequisiti**:
  * Completa la [Panoramica sull&#39;implementazione di Edge](overview.md) (schema, set di dati, flusso di dati con [!UICONTROL Media Analytics] abilitato).
  * Aggiungi le estensioni `Core`, `Edge`, `EdgeIdentity` e `EdgeMedia` all&#39;app. Consulta [Adobe Streaming Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/) per l&#39;installazione e la registrazione.

## Configurare i file multimediali per Android

Impostare le chiavi di configurazione del supporto quando si inizializza SDK:

```kotlin
val configuration = mapOf(
  "edgeMedia.channel" to "sample_channel",
  "edgeMedia.playerName" to "player_name",
  "edgeMedia.appVersion" to "app_version"
)
MobileCore.updateConfiguration(configuration)
```

Quindi crea un tracker per gestire una sessione multimediale:

```kotlin
val tracker = Media.createTracker()
```

Per le chiavi di configurazione e l&#39;API di tracciamento completa, vedi il riferimento API [Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/).

## Tracciare gli eventi multimediali

Una volta creato il tracciatore, tieni traccia di ogni evento multimediale utilizzando il relativo metodo di tracciamento. Per le chiamate esatte, vedi la scheda **Android** su ogni pagina [event](/help/implementation/events/overview.md) e [variable](/help/implementation/variables/overview.md).

## Passaggio successivo

Una volta completata l&#39;implementazione, puoi [Configurare la generazione di rapporti per le implementazioni di Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Contenuti multimediali in streaming Adobe per Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Configura Android per Streaming Media con Tag](android-tags.md)
>* [Panoramica eventi](/help/implementation/events/overview.md)
