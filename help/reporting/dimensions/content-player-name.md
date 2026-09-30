---
title: Nome del lettore di contenuti
description: Segnala quale lettore ha eseguito il rendering di ogni sessione multimediale.
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
source-wordcount: '194'
ht-degree: 7%
---

# Nome del lettore di contenuti

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione di reporting **Nome lettore di contenuti**. Per informazioni su come raccogliere questa variabile, consulta [Nome lettore di contenuti](/help/implementation/variables/core/content-player-name.md).*

>[!ENDSHADEBOX]

La dimensione **Nome lettore contenuto** segnala il rendering eseguito dal lettore per ogni sessione multimediale (ad esempio, `HTML5 Player`, `Brightcove` o `Roku Player`). Utilizzalo per confrontare coinvolgimento, completamento e qualità tra i giocatori nella stessa proprietà.

## Compilazione di questa dimensione

Il nome del lettore viene impostato dal lettore all’inizio della sessione e persiste per la sua durata. Il valore viene inviato per ogni evento e riportato sia in Adobe Analytics che in Customer Journey Analytics.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.playerName` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoplayername`, `post_videoplayername` |
| Audience Manager | `c_contextdata.a.media.playerName` |

>[!IMPORTANT]
>
>Se il nome del lettore non è impostato, la dimensione viene rimossa per quella sessione. Le sessioni senza un nome di lettore non possono essere suddivise per lettore nel reporting.

## Elementi dimensionali

Ogni elemento rappresenta la stringa letterale impostata all&#39;inizio della sessione. Utilizza un nome distinto e stabile per lettore in modo che i dati di lettori diversi non vengano compressi in un singolo elemento di riga.
