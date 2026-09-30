---
title: Tipo di contenuto
description: Riporta il formato del flusso (VOD, Live, Lineare, podcast, canzone e così via).
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 16%
---

# Tipo di contenuto

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Tipo di contenuto**. Per informazioni su come raccogliere questa variabile, vedere [Tipo di contenuto](/help/implementation/variables/core/content-type.md).*

>[!ENDSHADEBOX]

La dimensione **Tipo di contenuto** riporta il formato del flusso (ad esempio, VOD, Live o Linear per video e canzone, podcast o audiolibro per audio).

## Compilazione di questa dimensione

Il tipo di contenuto viene impostato dal lettore all’inizio della sessione e trasmesso attraverso ogni evento. Non è derivato; il valore riportato corrisponde a quello inviato durante la raccolta.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.contentType` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videocontenttype`, `post_videocontenttype` |
| Audience Manager | `c_contextdata.a.contentType` |

>[!IMPORTANT]
>
>Se il tipo di contenuto non è impostato o è vuoto, la dimensione segnala `missing_content_type` per la sessione. Usa questo valore per trovare le implementazioni che devono essere corrette.

## Elementi dimensionali

I valori definiti da Adobe popolano i segmenti e i rapporti incorporati. Le stringhe personalizzate sono accettate ma non corrispondono ai segmenti incorporati.

| Tipo di flusso | Valori consigliati |
| --- | --- |
| Video | `vod`, `live`, `linear`, `ugc`, `dvod` |
| Audio | `song`, `podcast`, `audiobook`, `radio` |

## Segmenti consigliati

| Segmento | Regola |
| --- | --- |
| [!UICONTROL VOD content] | Tipo di contenuto = `vod` |
| [!UICONTROL Live content] | Tipo di contenuto = `live` |
| [!UICONTROL Linear content] | Tipo di contenuto = `linear` |
