---
title: Tipo di contenuto
description: Riporta il formato del flusso (VOD, Live, Lineare, podcast, canzone e così via).
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 9%

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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.contentType` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.contentType`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
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
