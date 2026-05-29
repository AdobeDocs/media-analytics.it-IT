---
title: Nome del lettore di contenuti
description: Segnala quale lettore ha eseguito il rendering di ogni sessione multimediale.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.playerName` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.playerName`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoplayername`, `post_videoplayername` |
| Audience Manager | `c_contextdata.a.media.playerName` |

>[!IMPORTANT]
>
>Se il nome del lettore non è impostato, la dimensione viene rimossa per quella sessione. Le sessioni senza un nome di lettore non possono essere suddivise per lettore nel reporting.

## Elementi dimensionali

Ogni elemento rappresenta la stringa letterale impostata all&#39;inizio della sessione. Utilizza un nome distinto e stabile per lettore in modo che i dati di lettori diversi non vengano compressi in un singolo elemento di riga.
