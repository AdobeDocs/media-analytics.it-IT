---
title: Genere
description: Genere di contenuti report. Il contenuto multi-genere si suddivide tra gli elementi di riga, ciascuno dei quali riceve lo stesso peso metrico.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 7%

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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.genre` (memorizzati come variabile elenco) quando [[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) o [`mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) (legacy) |
| Feed di dati | `videogenre`, `post_videogenre` |
| Audience Manager | `c_contextdata.a.media.genre` |

## Elementi dimensionali

Ogni elemento è un valore di genere. Le sessioni di più generi (ad esempio, `"Drama,Action"`) vengono visualizzate come due righe separate (`Drama` e `Action`), e ogni elemento riceve il merito completo per la sessione.
