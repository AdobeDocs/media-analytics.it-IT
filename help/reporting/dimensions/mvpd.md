---
title: MVPD
description: Segnala il provider via cavo, satellite o virtuale tramite il quale l'utente ha eseguito l'autenticazione.
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
source-wordcount: '148'
ht-degree: 10%
---

# MVPD

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **MVPD**. Per informazioni su come raccogliere questa variabile, vedere [MVPD](/help/implementation/variables/standard-metadata/mvpd.md).*

>[!ENDSHADEBOX]

La dimensione **MVPD** (distributore di programmazione video multicanale) segnala il provider tramite il quale l&#39;utente ha eseguito l&#39;autenticazione tramite Adobe Pass (ad esempio, `"Comcast"` o `"DirecTV"`). Utilizzalo per interrompere il coinvolgimento da parte del provider di autenticazione.

## Compilazione di questa dimensione

MVPD viene impostato dal lettore all’inizio della sessione quando il contenuto viene inviato dietro Adobe Pass.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.pass.mvpd` quando [[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videomvpd`, `post_videomvpd` |
| Audience Manager | `c_contextdata.a.media.pass.mvpd` |

## Elementi dimensionali

Ogni elemento è il nome letterale di MVPD riportato all’inizio della sessione. Utilizza l’identificatore canonico Adobe Pass MVPD per provider, in modo che i dati vengano aggregati a una singola riga per provider.
