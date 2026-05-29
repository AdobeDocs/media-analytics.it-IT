---
title: Tipo di spettacolo
description: Segnala il formato del contenuto (episodio completo, anteprima, clip o altro).
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 13%

---


# Tipo di spettacolo

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione di reporting **Tipo di spettacolo**. Per informazioni su come raccogliere la variabile, vedere [Mostra tipo](/help/implementation/variables/standard-metadata/show-type.md).*

>[!ENDSHADEBOX]

La dimensione **Mostra tipo** riporta il formato del contenuto utilizzando un codice intero stringa. Utilizzatela per separare la visualizzazione di un programma completo da contenuti brevi come trailer e clip durante la misurazione del coinvolgimento.

## Compilazione di questa dimensione

Il tipo di spettacolo è impostato dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.type` quando [[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.showType`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoshowtype`, `post_videoshowtype` |
| Audience Manager | `c_contextdata.a.media.type` |

## Elementi dimensionali

| Valore | Descrizione |
| --- | --- |
| `0` | Episodio completo |
| `1` | Anteprima o trailer |
| `2` | Clip |
| `3` | Altro |

I valori vengono segnalati come stringhe. I valori personalizzati sono accettati, ma non vengono aggregati nei quattro bucket incorporati.
