---
title: Contenuti multimediali scaricati
description: Segnala le sessioni che hanno eseguito il download di contenuto offline.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
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
