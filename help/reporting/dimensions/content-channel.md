---
title: Canale del contenuto
description: Segnala la stazione di distribuzione, la rete o la proprietà in cui è stata riprodotta ogni sessione.
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
source-wordcount: '161'
ht-degree: 8%
---

# Canale del contenuto

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Canale contenuto**. Per informazioni su come raccogliere questa variabile, consulta [Canale contenuto](/help/implementation/variables/core/content-channel.md).*

>[!ENDSHADEBOX]

La dimensione **Canale contenuto** riporta la stazione di distribuzione, la rete o la proprietà in cui è stata riprodotta ogni sessione. Utilizzalo per interrompere la riproduzione per rete o sezione di una proprietà.

## Compilazione di questa dimensione

Il canale viene impostato dal lettore all’inizio della sessione e persiste per la sua durata.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.channel` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>Se channel non è impostato, la dimensione viene scompilata per quella sessione.

## Elementi dimensionali

Ogni elemento rappresenta la stringa letterale impostata all&#39;inizio della sessione. Qualsiasi stringa viene accettata. I valori tipici sono un nome di rete, una parte del percorso di un sito o un identificatore di proprietà interno.
