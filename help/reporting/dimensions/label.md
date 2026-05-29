---
title: Etichetta
description: Segnala l’etichetta discografica che ha rilasciato il contenuto audio.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 10%

---


# Etichetta

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Label**. Per informazioni su come raccogliere questa variabile, vedere [Label](/help/implementation/variables/standard-metadata/label.md).*

>[!ENDSHADEBOX]

La dimensione **Label** riporta l&#39;etichetta record che ha rilasciato il contenuto audio (ad esempio, `"Capitol Records"`). Utilizzalo per confrontare il coinvolgimento tra le etichette in un catalogo musicale o podcast.

## Compilazione di questa dimensione

L’etichetta viene impostata dal lettore all’inizio della sessione per il contenuto audio.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.label` quando [[!UICONTROL Audio Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.label`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudiolabel` |
| Audience Manager | `c_contextdata.a.media.label` |

## Elementi dimensionali

Ogni elemento è il nome letterale dell’etichetta riportato all’inizio della sessione. Utilizza un nome stabile e canonico per etichetta in modo che il coinvolgimento non si frammenti tra le varianti di controllo ortografico o di stampa.
