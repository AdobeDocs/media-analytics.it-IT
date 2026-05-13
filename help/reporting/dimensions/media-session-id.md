---
title: ID sessione multimediale
description: Identifica in modo univoco ogni sessione di riproduzione.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 5%

---


# ID sessione multimediale

La dimensione **ID sessione multimediale** identifica in modo univoco ogni sessione di riproduzione. Viene generato dal backend e timbrato su ogni evento della sessione. Utilizzala per isolare gli eventi di una singola sessione per il debug o per deduplicare le sessioni nelle analisi personalizzate.

## Compilazione di questa dimensione

L&#39;ID sessione viene generato automaticamente quando il backend riceve un evento `media.sessionStart`. Le implementazioni Web SDK e Mobile SDK acquisiscono e mantengono l&#39;ID per te; le implementazioni Direct API devono leggere l&#39;ID sessione dalla risposta `sessionStart` (l&#39;intestazione `Location` per l&#39;API Media Collection o l&#39;handle `media-analytics:new-session` per l&#39;API Media Edge) e includerlo negli eventi successivi.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.vsid` a un eVar. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.ID`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videosessionid, post_videosessionid` |

## Elementi dimensionali

Ogni elemento è un ID di sessione univoco generato dal backend (in genere una stringa alfanumerica di 22 caratteri). Utilizza il campo Filtro o Ricerca per cercare una sessione specifica.
