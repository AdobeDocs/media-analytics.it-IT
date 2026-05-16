---
title: Fascia oraria
description: Segnala il periodo fisso dell’ora del giorno (Mattino, Pomeriggio, Primetime, Late Night) in cui il contenuto è stato trasmesso o riprodotto.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 10%

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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.dayPart` quando [[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videodaypart`, `post_videodaypart` |
| Audience Manager | `c_contextdata.a.media.dayPart` |

## Elementi dimensionali

Ogni elemento rappresenta l&#39;etichetta daypart letterale riportata all&#39;inizio della sessione. Utilizza un set fisso di valori tra le implementazioni per mantenere coerenza tra gli elementi della riga.
