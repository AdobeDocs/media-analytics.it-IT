---
title: Spettacolo
description: Segnala il nome del programma o della serie per il contenuto video che fa parte di una serie.
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
source-wordcount: '156'
ht-degree: 10%
---

# Spettacolo

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Show**. Per informazioni su come raccogliere questa variabile, vedere [Show](/help/implementation/variables/standard-metadata/show.md).*

>[!ENDSHADEBOX]

La dimensione **Mostra** riporta il nome del programma o della serie. Gli episodi di più stagioni vengono aggregati alla stessa riga dello spettacolo, quindi utilizzali per confrontare il coinvolgimento nell’intera durata di una serie.

## Compilazione di questa dimensione

Lo spettacolo è impostato dal lettore all’inizio della sessione quando il contenuto fa parte di una serie.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.show` quando [[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoshow`, `post_videoshow` |
| Audience Manager | `c_contextdata.a.media.show` |

## Elementi dimensionali

Ogni elemento rappresenta il nome visualizzato letterale riportato all&#39;inizio della sessione (ad esempio, `"Blinding Light"`). Utilizzare nomi distinti e stabili per mostrare in modo che i dati non vengano compressi in programmi non correlati che condividono una parola.
