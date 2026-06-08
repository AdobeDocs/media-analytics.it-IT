---
title: Caricamenti degli annunci
description: Segnala il tipo di caricamento dell’annuncio utilizzato per ogni sessione di contenuti multimediali in streaming.
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 7%

---


# Caricamenti degli annunci

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Caricamenti annuncio**. Per informazioni su come raccogliere questa variabile, vedere [Tipo di caricamento annuncio](/help/implementation/variables/standard-metadata/ad-load-type.md).*

>[!ENDSHADEBOX]

La dimensione **Caricamenti annuncio** riporta il tipo di annuncio caricato all&#39;inizio di ogni sessione di streaming multimediale. Il valore è definito dal cliente e consente alle organizzazioni di classificare le sessioni in base al meccanismo di distribuzione degli annunci (ad esempio, `"linear"`, `"dynamic"` o `"programmatic"`).

## Compilazione di questa dimensione

Il tipo di caricamento dell’annuncio viene impostato dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.adLoad` quando [[!UICONTROL Streaming Media]](/help/reporting/setup/analytics-reporting.md) è configurato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoadload`, `post_videoadload` |
| Audience Manager | `c_contextdata.a.media.adLoad` |

## Elementi dimensionali

Ogni elemento è la stringa letterale del tipo di caricamento dell’annuncio impostata all’inizio della sessione. I valori non sono vincolati a un’enumerazione standard. Definisci una tassonomia coerente nelle implementazioni in modo che i valori vengano aggregati in modo prevedibile nei rapporti.
