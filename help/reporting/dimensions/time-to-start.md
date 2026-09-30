---
title: Tempo di avvio (dimensione)
description: Segnala il tempo trascorso prima del rendering del primo fotogramma.
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
source-wordcount: '188'
ht-degree: 7%
---

# Tempo di avvio (dimensione)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione **Tempo di avvio**. Adobe Analytics compila automaticamente una coppia di [Tempo di avvio (metrica)](/help/reporting/metrics/time-to-start.md) dalla stessa variabile di dati di contesto `a.media.qoe.timeToStart`. Customer Journey Analytics espone un singolo campo `xdm.mediaReporting.qoeDataDetails.timeToStart` che è possibile utilizzare come dimensione o come metrica. Vedi [Ora di inizio](/help/implementation/variables/quality/time-to-start.md) per informazioni su come raccogliere questa variabile.*

>[!ENDSHADEBOX]

La dimensione **Tempo di avvio** indica il tempo trascorso tra l&#39;inizio della sessione e il rendering del primo fotogramma. Utilizza la dimensione per suddividere il coinvolgimento in base al bucket del tempo di avvio. Adobe memorizza il valore in secondi e converte al momento dell’acquisizione dai millisecondi riportati dal lettore.

## Compilazione di questa dimensione

Il lettore imposta `timeToStart` sull&#39;oggetto QoE prima dell&#39;avvio della sessione. Il backend riporta il valore nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.timeToStart` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoetimetostartevar`, `post_videoqoetimetostartevar` |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |

## Elementi dimensionali

Ogni elemento è il valore letterale del tempo di avvio riportato nella chiamata di chiusura.
