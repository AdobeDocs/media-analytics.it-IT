---
title: Nome del contenuto
description: Riporta il titolo leggibile di ogni sessione multimediale.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 8%

---


# Nome del contenuto

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Nome contenuto**. Per informazioni su come raccogliere questa variabile, vedere [Nome contenuto](/help/implementation/variables/core/content-name.md).*

>[!ENDSHADEBOX]

La dimensione **Nome contenuto** riporta il titolo leggibile di ogni sessione multimediale.

## Compilazione di questa dimensione

Il nome descrittivo viene impostato dal lettore all’inizio della sessione. Il valore riportato corrisponde a quello inviato.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.friendlyName` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoname, post_videoname` |

>[!NOTE]
>
>In Adobe Analytics, questo valore corrisponde anche a una classificazione **Video name** nella dimensione [Content](content.md). L’utente è responsabile di compilare e mantenere tale classificazione separatamente. Customer Journey Analytics utilizza direttamente questa dimensione.

>[!IMPORTANT]
>
>Se il nome del contenuto non è impostato, la dimensione viene scompilata per quella sessione.

## Elementi dimensionali

Ogni elemento è il titolo letterale riportato all&#39;inizio della sessione (ad esempio, `"Blinding Light"`).
