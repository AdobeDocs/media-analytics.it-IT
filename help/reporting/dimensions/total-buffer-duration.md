---
title: Durata totale buffer (dimensione)
description: Segnala i secondi cumulativi dedicati al buffering per sessione.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 5%

---


# Durata totale buffer (dimensione)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione **Durata totale buffer**. Adobe Analytics compila automaticamente una coppia di [durata totale del buffer (metrica)](/help/reporting/metrics/total-buffer-duration.md) dalla stessa variabile di dati di contesto `a.media.qoe.bufferTime`. Customer Journey Analytics espone un singolo campo `mediaReporting.qoeDataDetails.bufferTime` che è possibile utilizzare come dimensione o come metrica.*

>[!ENDSHADEBOX]

La dimensione **Durata totale buffer** riporta il tempo cumulativo, in secondi, trascorso dal lettore in uno stato di buffer durante una sessione. Utilizza la dimensione per suddividere il coinvolgimento in base al valore di durata esatta del buffer.

## Compilazione di questa dimensione

Il backend del supporto somma la durata di ogni intervallo di buffer (da `media.bufferStart` alla successiva modifica dello stato). Il valore viene segnalato nella chiamata di chiusura. Analysis Workspace mostra il valore come `HH:MM:SS`; Feed dati, Data Warehouse e API di reporting mostrano il valore in secondi.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bufferTime` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoebuffertimeevar, post_videoqoebuffertimeevar` |

## Elementi dimensionali

Ogni elemento è il valore di durata letterale, in secondi, riportato nella chiamata di chiusura.
