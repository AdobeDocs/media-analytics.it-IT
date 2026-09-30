---
title: Durata totale buffer (dimensione)
description: Segnala i secondi cumulativi dedicati al buffering per sessione.
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
source-wordcount: '192'
ht-degree: 7%
---

# Durata totale buffer (dimensione)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione **Durata totale buffer**. Adobe Analytics compila automaticamente una coppia di [durata totale del buffer (metrica)](/help/reporting/metrics/total-buffer-duration.md) dalla stessa variabile di dati di contesto `a.media.qoe.bufferTime`. Customer Journey Analytics espone un singolo campo `xdm.mediaReporting.qoeDataDetails.bufferTime` che è possibile utilizzare come dimensione o come metrica.*

>[!ENDSHADEBOX]

La dimensione **Durata totale buffer** riporta il tempo cumulativo, in secondi, trascorso dal lettore in uno stato di buffer durante una sessione. Utilizza la dimensione per suddividere il coinvolgimento in base al valore di durata esatta del buffer.

## Compilazione di questa dimensione

Il backend del supporto somma la durata di ogni intervallo di buffer (da [inizio buffer](/help/implementation/events/playback/buffer-start.md) alla successiva modifica dello stato). Il valore viene segnalato nella chiamata di chiusura. Analysis Workspace mostra il valore come `HH:MM:SS`; Feed dati, Data Warehouse e API di reporting mostrano il valore in secondi.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bufferTime` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoebuffertimeevar`, `post_videoqoebuffertimeevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |

## Elementi dimensionali

Ogni elemento è il valore di durata letterale, in secondi, riportato nella chiamata di chiusura.
