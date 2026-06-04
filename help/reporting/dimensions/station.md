---
title: Stazione
description: Segnala il nome o l'ID della stazione radio per il contenuto della trasmissione audio.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 10%

---


# Stazione

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Stazione**. Per informazioni su come raccogliere questa variabile, vedere [Stazione](/help/implementation/variables/standard-metadata/station.md).*

>[!ENDSHADEBOX]

La dimensione **Stazione** riporta il nome o l&#39;ID della stazione radio che trasmette il contenuto audio (ad esempio, `"NPR"` o `"WXYZ-FM"`). Utilizzalo per confrontare il coinvolgimento tra le stazioni in una rete sindacata.

## Compilazione di questa dimensione

La stazione viene impostata dal lettore all&#39;inizio della sessione per il contenuto audio.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.station` quando [[!UICONTROL Audio Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudiostation` |
| Audience Manager | `c_contextdata.a.media.station` |

## Elementi dimensionali

Ogni elemento rappresenta il nome o l&#39;ID letterale della stazione segnalato all&#39;inizio della sessione. Utilizza un singolo identificatore canonico per stazione in modo che il coinvolgimento non si frammenti tra le varianti di segnale di chiamata.
