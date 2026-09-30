---
title: Autore
description: Segnala l’autore del contenuto. Utilizzato principalmente per gli audiolibri.
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
source-wordcount: '117'
ht-degree: 11%
---

# Autore

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Autore**. Per informazioni su come raccogliere questa variabile, vedere [Autore](/help/implementation/variables/standard-metadata/author.md).*

>[!ENDSHADEBOX]

La dimensione **Autore** segnala l&#39;autore del contenuto, ad esempio `"Eleanor Clementine"`. Utilizzato principalmente per gli audiolibri, ma valido anche per i podcast il cui host o produttore rappresenta l’attribuzione pertinente.

## Compilazione di questa dimensione

L’autore viene impostato dal lettore all’inizio della sessione per i contenuti audio.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.author` quando [[!UICONTROL Audio Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudioauthor` |
| Audience Manager | `c_contextdata.a.media.author` |

## Elementi dimensionali

Ogni elemento rappresenta il nome dell’autore letterale riportato all’inizio della sessione.
