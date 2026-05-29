---
title: Autorizzato
description: Conta le sessioni il cui utente è stato autorizzato tramite Adobe Pass.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.pass.auth` quando [[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.pass.auth` |
