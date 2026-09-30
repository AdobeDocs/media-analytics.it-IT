---
title: Autorizzato
description: Conta le sessioni il cui utente è stato autorizzato tramite Adobe Pass.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 12%
---

# Autorizzato

>[!BEGINSHADEBOX]

*Questa pagina contiene la metrica di reporting **Authorized**. Vedi [Autorizzato](/help/implementation/variables/standard-metadata/authorized.md) per informazioni su come raccogliere questa variabile.*

>[!ENDSHADEBOX]

La metrica **Authorized** conta le sessioni il cui utente è stato autorizzato tramite Adobe Pass o TV-Everywhere. Associa la dimensione [MVPD](/help/reporting/dimensions/mvpd.md) per suddividere il volume di autenticazione per provider.

## Come è calcolata questa metrica

Il backend multimediale incrementa il conteggio quando il lettore contrassegna la sessione come autorizzata all’avvio della sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.pass.auth` quando [[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.pass.auth` |
