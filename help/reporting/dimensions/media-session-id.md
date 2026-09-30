---
title: ID sessione multimediale
description: Identifica in modo univoco ogni sessione di riproduzione.
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
source-wordcount: '205'
ht-degree: 6%
---

# ID sessione multimediale

La dimensione **ID sessione multimediale** identifica in modo univoco ogni sessione di riproduzione. Viene generato dal backend e timbrato su ogni evento della sessione. Utilizzala per isolare gli eventi di una singola sessione per il debug o per deduplicare le sessioni nelle analisi personalizzate.

## Compilazione di questa dimensione

L&#39;ID sessione viene generato automaticamente quando il backend riceve un evento [inizio sessione](/help/implementation/events/session/session-start.md). Le implementazioni Web SDK e Mobile SDK acquisiscono e mantengono l&#39;ID per te; le implementazioni Direct API devono leggere l&#39;ID sessione dalla risposta `sessionStart` (l&#39;intestazione `Location` per l&#39;API Media Collection o l&#39;handle `media-analytics:new-session` per l&#39;API Media Edge) e includerlo negli eventi successivi.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.vsid` a un eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videosessionid`, `post_videosessionid` |
| Audience Manager | `c_contextdata.a.media.vsid` |

## Elementi dimensionali

Ogni elemento è un ID di sessione univoco generato dal backend (in genere una stringa alfanumerica di 22 caratteri). Utilizza il campo Filtro o Ricerca per cercare una sessione specifica.
