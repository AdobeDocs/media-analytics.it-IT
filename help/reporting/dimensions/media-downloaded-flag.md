---
title: Contenuti multimediali scaricati
description: Segnala le sessioni che hanno eseguito il download di contenuto offline.
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
source-wordcount: '195'
ht-degree: 7%
---

# Contenuti multimediali scaricati

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **File multimediali scaricati**. Per informazioni su come raccogliere questa variabile, vedere [Flag di contenuto multimediale scaricato](/help/implementation/variables/core/media-downloaded-flag.md).*

>[!ENDSHADEBOX]

La dimensione **File multimediali scaricati** contrassegna le sessioni che hanno riprodotto contenuto offline scaricato in precedenza anziché un flusso live da Internet. Utilizzalo per separare la riproduzione offline dalle sessioni in streaming durante il confronto di coinvolgimento, completamento o qualità.

## Compilazione di questa dimensione

Il flag scaricato viene impostato dal lettore in uno dei tre modi seguenti. Inizializza il tracker con il flag (Mobile SDK), invia `sessionStart` alla variante dell&#39;endpoint `/downloaded` (direttamente API Media Edge) oppure includi `media.downloaded: true` nei parametri `sessionStart` (API Media Collection).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.downloaded` a un eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.downloaded`) |
| Audience Manager | `c_contextdata.a.media.downloaded` |

## Elementi dimensionali

| Valore | Descrizione |
| --- | --- |
| `true` | La sessione ha riprodotto il contenuto offline scaricato. |
| (vuoto) | La sessione è stata riprodotta in streaming. Il campo viene omesso anziché impostato su `false`. |
