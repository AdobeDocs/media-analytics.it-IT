---
title: Tempo di avvio (dimensione)
description: Segnala il tempo trascorso prima del rendering del primo fotogramma.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 5%

---


# Tempo di avvio (dimensione)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione **Tempo di avvio**. Adobe Analytics compila automaticamente una coppia di [Tempo di avvio (metrica)](/help/reporting/metrics/time-to-start.md) dalla stessa variabile di dati di contesto `a.media.qoe.timeToStart`. Customer Journey Analytics espone un singolo campo `mediaReporting.qoeDataDetails.timeToStart` che è possibile utilizzare come dimensione o come metrica. Vedi [Ora di inizio](/help/implementation/variables/quality/time-to-start.md) per informazioni su come raccogliere questa variabile.*

>[!ENDSHADEBOX]

La dimensione **Tempo di avvio** indica il tempo trascorso tra l&#39;inizio della sessione e il rendering del primo fotogramma. Utilizza la dimensione per suddividere il coinvolgimento in base al bucket del tempo di avvio. Adobe memorizza il valore in secondi e converte al momento dell’acquisizione dai millisecondi riportati dal lettore.

## Compilazione di questa dimensione

Il lettore imposta `timeToStart` sull&#39;oggetto QoE prima dell&#39;avvio della sessione. Il backend riporta il valore nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.timeToStart` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoetimetostartevar, post_videoqoetimetostartevar` |

## Elementi dimensionali

Ogni elemento è il valore letterale del tempo di avvio riportato nella chiamata di chiusura.
