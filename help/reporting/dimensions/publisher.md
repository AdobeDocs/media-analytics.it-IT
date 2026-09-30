---
title: Autore
description: Segnala l’autore del contenuto audio.
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
source-wordcount: '112'
ht-degree: 12%
---

# Autore

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Publisher**. Per informazioni su come raccogliere questa variabile, vedere [Publisher](/help/implementation/variables/standard-metadata/publisher.md).*

>[!ENDSHADEBOX]

La dimensione **Editore** segnala l&#39;editore del contenuto audio (ad esempio, un editore di rete di podcast o di audiolibri). Utilizzalo per confrontare il coinvolgimento tra gli editori in un catalogo audio curato.

## Compilazione di questa dimensione

Il programma di pubblicazione viene impostato dal lettore all&#39;inizio della sessione per il contenuto audio.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.publisher` quando [[!UICONTROL Audio Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudiopublisher` |
| Audience Manager | `c_contextdata.a.media.publisher` |

## Elementi dimensionali

Ogni elemento rappresenta il nome letterale dell&#39;editore riportato all&#39;inizio della sessione.
