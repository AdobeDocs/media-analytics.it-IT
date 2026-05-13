---
title: ID errore SDK del lettore
description: Segnala identificatori di errore univoci generati dal lettore di contenuti SDK.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 6%

---


# ID errore SDK del lettore

La dimensione **ID errore SDK del lettore** riporta identificatori di errore univoci generati dal SDK del lettore di contenuti durante una sessione. Il lettore deve fornire i codici o gli ID al momento dell’implementazione tramite l’API di tracciamento degli errori. Sono supportati più ID di errore per sessione.

## Compilazione di questa dimensione

Il lettore trasmette gli ID di errore del lettore-SDK al tracker in `media.error` eventi. Il backend raccoglie ID univoci in tutta la sessione e li segnala nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.playerSdkErrors` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.playerSdkErrors`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoeplayersdkerrors, post_videoqoeplayersdkerrors` |

## Elementi dimensionali

Ogni elemento è un codice di errore o un ID generato dal lettore SDK. Utilizza una tassonomia stabile tra le implementazioni in modo che gli ID di errore vengano aggregati correttamente tra le sessioni.
