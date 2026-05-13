---
title: Spettacolo
description: Segnala il nome del programma o della serie per il contenuto video che fa parte di una serie.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 7%

---


# Spettacolo

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Show**. Per informazioni su come raccogliere questa variabile, vedere [Show](/help/implementation/variables/standard-metadata/show.md).*

>[!ENDSHADEBOX]

La dimensione **Mostra** riporta il nome del programma o della serie. Gli episodi di più stagioni vengono aggregati alla stessa riga dello spettacolo, quindi utilizzali per confrontare il coinvolgimento nell’intera durata di una serie.

## Compilazione di questa dimensione

Lo spettacolo è impostato dal lettore all’inizio della sessione quando il contenuto fa parte di una serie.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.show` quando [[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoshow, post_videoshow` |

## Elementi dimensionali

Ogni elemento rappresenta il nome visualizzato letterale riportato all&#39;inizio della sessione (ad esempio, `"Blinding Light"`). Utilizzare nomi distinti e stabili per mostrare in modo che i dati non vengano compressi in programmi non correlati che condividono una parola.
