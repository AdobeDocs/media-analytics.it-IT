---
title: Contenuto
description: Segnala ogni elemento multimediale univoco riprodotto, identificato dall’ID contenuto.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 6%

---


# Contenuto

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Contenuto**. Per informazioni su come raccogliere questa variabile, vedere [ID contenuto](/help/implementation/variables/core/content-id.md).*

>[!ENDSHADEBOX]

La dimensione **Contenuto** riporta ogni elemento multimediale univoco riprodotto, definito dall&#39;ID contenuto impostato all&#39;inizio della sessione. È il raggruppamento principale per il reporting dei contenuti multimediali in streaming e la chiave di unione per dimensioni di classificazione come Nome video, Lunghezza video, ID risorsa, Data prima messa in onda e Valutazione contenuto.

## Compilazione di questa dimensione

All’inizio della sessione, il contenuto viene impostato dal lettore come identificatore stabile della risorsa. Lo stesso ID di contenuto viene segnalato per ogni evento successivo della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.name` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. Persiste per la durata della visita. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.name`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `video`, `post_video` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!IMPORTANT]
>
>È necessario specificare l’ID contenuto. Se non è impostata o è vuota, la sessione viene eliminata dal reporting dei contenuti multimediali in streaming e non verrà visualizzata in alcun report multimediale o nel segmento [!UICONTROL All streaming media].

## Elementi dimensionali

Ogni elemento è un ID di contenuto univoco segnalato all’inizio della sessione. Utilizza un identificatore stabile (ad esempio, un ID CMS interno, un ID settore come EIDR o TMS/Gracenote o un tag persistente) in modo che le sessioni per la stessa risorsa vengano aggregate in un singolo elemento nel tempo.

## Segmenti consigliati

| Segmento | Regola |
| --- | --- |
| [!UICONTROL All streaming media] | Il contenuto (ID) esiste |
