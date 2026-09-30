---
title: Fascia oraria
description: Segnala il periodo fisso dell’ora del giorno (Mattino, Pomeriggio, Primetime, Late Night) in cui il contenuto è stato trasmesso o riprodotto.
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
source-wordcount: '149'
ht-degree: 12%
---

# Fascia oraria

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Fascia oraria**. Per informazioni su come raccogliere questa variabile, vedere [Fascia oraria](/help/implementation/variables/standard-metadata/day-part.md).*

>[!ENDSHADEBOX]

La dimensione **Day part** riporta il bucket dell&#39;ora del giorno in cui il contenuto è stato trasmesso o riprodotto. I valori comuni sono `"Morning"`, `"Afternoon"`, `"Primetime"` e `"Late Night"`. Utilizzalo per confrontare il coinvolgimento tra le parti diurne indipendentemente dal fuso orario locale dello spettatore.

## Compilazione di questa dimensione

La parte del giorno viene impostata dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.dayPart` quando [[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videodaypart`, `post_videodaypart` |
| Audience Manager | `c_contextdata.a.media.dayPart` |

## Elementi dimensionali

Ogni elemento rappresenta l&#39;etichetta daypart letterale riportata all&#39;inizio della sessione. Utilizza un set fisso di valori tra le implementazioni per mantenere coerenza tra gli elementi della riga.
