---
title: Nome del contenuto
description: Riporta il titolo leggibile di ogni sessione multimediale.
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
source-wordcount: '160'
ht-degree: 11%
---

# Nome del contenuto

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Nome contenuto**. Per informazioni su come raccogliere questa variabile, vedere [Nome contenuto](/help/implementation/variables/core/content-name.md).*

>[!ENDSHADEBOX]

La dimensione **Nome contenuto** riporta il titolo leggibile di ogni sessione multimediale.

## Compilazione di questa dimensione

Il nome descrittivo viene impostato dal lettore all’inizio della sessione. Il valore riportato corrisponde a quello inviato.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.friendlyName` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoname`, `post_videoname` |
| Audience Manager | `c_contextdata.a.media.friendlyName` |

>[!NOTE]
>
>In Adobe Analytics, questo valore corrisponde anche a una classificazione **Video name** nella dimensione [Content](content.md). L’utente è responsabile di compilare e mantenere tale classificazione separatamente. Customer Journey Analytics utilizza direttamente questa dimensione.

>[!IMPORTANT]
>
>Se il nome del contenuto non è impostato, la dimensione viene scompilata per quella sessione.

## Elementi dimensionali

Ogni elemento è il titolo letterale riportato all&#39;inizio della sessione (ad esempio, `"Blinding Light"`).
