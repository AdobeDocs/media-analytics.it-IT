---
title: Autore
description: Segnala l’autore del contenuto audio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 10%

---


# Autore

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Publisher**. Per informazioni su come raccogliere questa variabile, vedere [Publisher](/help/implementation/variables/standard-metadata/publisher.md).*

>[!ENDSHADEBOX]

La dimensione **Editore** segnala l&#39;editore del contenuto audio (ad esempio, un editore di rete di podcast o di audiolibri). Utilizzalo per confrontare il coinvolgimento tra gli editori in un catalogo audio curato.

## Compilazione di questa dimensione

Il programma di pubblicazione viene impostato dal lettore all&#39;inizio della sessione per il contenuto audio.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.publisher` quando [[!UICONTROL Audio Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudiopublisher` |

## Elementi dimensionali

Ogni elemento rappresenta il nome letterale dell&#39;editore riportato all&#39;inizio della sessione.
