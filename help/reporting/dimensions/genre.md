---
title: Genere
description: Genere di contenuti report. Il contenuto multi-genere si suddivide tra gli elementi di riga, ciascuno dei quali riceve lo stesso peso metrico.
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
source-wordcount: '179'
ht-degree: 8%
---

# Genere

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Genere**. Per informazioni su come raccogliere questa variabile, vedere [Genere](/help/implementation/variables/standard-metadata/genre.md).*

>[!ENDSHADEBOX]

La dimensione **Genere** riporta il genere di contenuto. Il genere viene raccolto come stringa delimitata da virgole e memorizzato come dimensione elenco. Il contenuto multi-genere si suddivide tra righe separate, ciascuna delle quali riceve lo stesso peso metrico. Utilizzalo per confrontare il coinvolgimento tra generi diversi senza dover contare due volte il tempo trascorso su una singola risorsa multigenero.

## Compilazione di questa dimensione

Il genere viene impostato dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.genre` (memorizzati come variabile elenco) quando [[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) o [`xdm.mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) (legacy) |
| Feed di dati | `videogenre`, `post_videogenre` |
| Audience Manager | `c_contextdata.a.media.genre` |

## Elementi dimensionali

Ogni elemento è un valore di genere. Le sessioni di più generi (ad esempio, `"Drama,Action"`) vengono visualizzate come due righe separate (`Drama` e `Action`), e ogni elemento riceve il merito completo per la sessione.
