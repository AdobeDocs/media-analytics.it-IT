---
title: Dati federati
description: Conta le sessioni ricevute tramite una condivisione di dati federata anziché tramite l’implementazione di un cliente.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 6%

---


# Dati federati

>[!AVAILABILITY]
>
>Il servizio Federated Analytics è disponibile solo quando si utilizzano funzioni di streaming multimediale con Adobe Analytics. Federated Analytics non è disponibile in Customer Journey Analytics.

La metrica **Dati federati** conta le sessioni ricevute tramite una condivisione dati federata anziché dalla tua implementazione. Utilizzala per misurare il volume di sessioni condivise dai partner e confrontare coinvolgimento, completamento o qualità rispetto alle sessioni di prime parti.

Per ulteriori informazioni, vedi il caso d&#39;uso [Federated Media](/help/use-cases/federated-media.md).

>[!TIP]
>
>Se si desidera utilizzare i dati federati come dimensione, creare una [Regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che mappi la variabile di dati di contesto `a.media.federated` a un eVar.

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag quando la sessione arriva su un canale federato. La metrica viene incrementata una volta per sessione qualificata e indicata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.federated` quando [[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isFederated`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.federated` |
