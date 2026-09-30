---
title: Etichetta
description: Segnala l’etichetta discografica che ha rilasciato il contenuto audio.
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
source-wordcount: '132'
ht-degree: 10%
---

# Etichetta

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Label**. Per informazioni su come raccogliere questa variabile, vedere [Label](/help/implementation/variables/standard-metadata/label.md).*

>[!ENDSHADEBOX]

La dimensione **Label** riporta l&#39;etichetta record che ha rilasciato il contenuto audio (ad esempio, `"Capitol Records"`). Utilizzalo per confrontare il coinvolgimento tra le etichette in un catalogo musicale o podcast.

## Compilazione di questa dimensione

L’etichetta viene impostata dal lettore all’inizio della sessione per il contenuto audio.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.label` quando [[!UICONTROL Audio Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.label`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudiolabel` |
| Audience Manager | `c_contextdata.a.media.label` |

## Elementi dimensionali

Ogni elemento è il nome letterale dell’etichetta riportato all’inizio della sessione. Utilizza un nome stabile e canonico per etichetta in modo che il coinvolgimento non si frammenti tra le varianti di controllo ortografico o di stampa.
