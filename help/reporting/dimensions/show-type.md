---
title: Tipo di spettacolo
description: Segnala il formato del contenuto (episodio completo, anteprima, clip o altro).
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
source-wordcount: '143'
ht-degree: 14%
---

# Tipo di spettacolo

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione di reporting **Tipo di spettacolo**. Per informazioni su come raccogliere la variabile, vedere [Mostra tipo](/help/implementation/variables/standard-metadata/show-type.md).*

>[!ENDSHADEBOX]

La dimensione **Mostra tipo** riporta il formato del contenuto utilizzando un codice intero stringa. Utilizzatela per separare la visualizzazione di un programma completo da contenuti brevi come trailer e clip durante la misurazione del coinvolgimento.

## Compilazione di questa dimensione

Il tipo di spettacolo è impostato dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.type` quando [[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.showType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoshowtype`, `post_videoshowtype` |
| Audience Manager | `c_contextdata.a.media.type` |

## Elementi dimensionali

| Valore | Descrizione |
| --- | --- |
| `0` | Episodio completo |
| `1` | Anteprima o trailer |
| `2` | Clip |
| `3` | Altro |

I valori vengono segnalati come stringhe. I valori personalizzati sono accettati, ma non vengono aggregati nei quattro bucket incorporati.
