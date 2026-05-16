---
title: Tipo di feed multimediale
description: Segnala il feed del broadcast (ad esempio, East-HD o West-SD) quando lo stesso contenuto viene distribuito tramite più feed.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 7%

---


# Tipo di feed multimediale

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Tipo di feed multimediale**. Per informazioni su come raccogliere questa variabile, vedere [Tipo di feed multimediale](/help/implementation/variables/standard-metadata/media-feed-type.md).*

>[!ENDSHADEBOX]

La dimensione **Tipo di feed multimediale** riporta il feed di trasmissione per ogni sessione (ad esempio, `"East-HD"`, `"West-SD"` o `"4K"`). Utilizzalo quando lo stesso contenuto viene distribuito tramite più feed regionali o di qualità e il coinvolgimento deve essere segnalato per feed.

## Compilazione di questa dimensione

Il tipo di feed multimediale viene impostato dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.feed` quando [[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## Elementi dimensionali

Ogni elemento rappresenta il valore di feed letterale riportato all’inizio della sessione. Utilizza un set stabile di identificatori dei mangimi per suddivisione regionale o di qualità.
