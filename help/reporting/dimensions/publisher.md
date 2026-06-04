---
title: Autore
description: Segnala l’autore del contenuto audio.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 12%

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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.publisher` quando [[!UICONTROL Audio Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudiopublisher` |
| Audience Manager | `c_contextdata.a.media.publisher` |

## Elementi dimensionali

Ogni elemento rappresenta il nome letterale dell&#39;editore riportato all&#39;inizio della sessione.
